# Blazor.BFF.AzureAD.Template

[![.NET](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/actions/workflows/dotnet.yml/badge.svg)](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/actions/workflows/dotnet.yml) [![NuGet Status](http://img.shields.io/nuget/v/Blazor.BFF.AzureAD.Template.svg?style=flat-square)](https://www.nuget.org/packages/Blazor.BFF.AzureAD.Template/) [Change log](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/blob/main/Changelog.md)

This template can be used to create a Blazor WASM application hosted in an ASP.NET Core Web app using Azure AD and Microsoft.Identity.Web to authenticate using the BFF security architecture. (server authentication) This removes the tokens form the browser and uses cookies with each HTTP request, response. The template also adds the required security headers as best it can for a Blazor application.

![Blazor BFF Azure AD](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/blob/main/images/blazorBFFAzureAD.png)

## Features

- WASM hosted in ASP.NET Core 6
- BFF with Azure AD using Microsoft.Identity.Web
- OAuth2 and OpenID Connect OIDC
- No tokens in the browser

## Other templates

[Blazor BFF Azure B2C](https://github.com/damienbod/Blazor.BFF.AzureB2C.Template)

[Blazor BFF Azure OpenID Connect](https://github.com/damienbod/Blazor.BFF.OpenIDConnect.Template)

## Using the template

### install

```
dotnet new -i Blazor.BFF.AzureAD.Template
```

### run

```
dotnet new blazorbffaad -n YourCompany.Bff
```

Use the `-n` or `--name` parameter to change the name of the output created. This string is also used to substitute the namespace name in the .cs file for the project.

## Setup after installation

Add the Azure AD App registration settings

```
{
  "AzureAd": {
    "Instance": "https://login.microsoftonline.com/",
    "Domain": "[Enter the domain of your tenant, e.g. contoso.onmicrosoft.com]",
    "TenantId": "[Enter 'common', or 'organizations' or the Tenant Id (Obtained from the Azure portal. Select 'Endpoints' from the 'App registrations' blade and use the GUID in any of the URLs), e.g. da41245a5-11b3-996c-00a8-4d99re19f292]",
    "ClientId": "[Enter the Client Id (Application ID obtained from the Azure portal), e.g. ba74781c2-53c2-442a-97c2-3d60re42f403]",
    "ClientSecret": "[Copy the client secret added to the app from the Azure portal]",
    "ClientCertificates": [
    ],
    // the following is required to handle Continuous Access Evaluation challenges
    "ClientCapabilities": [ "cp1" ],
    "CallbackPath": "/signin-oidc"
  },
```

Add the scopes for the downstream API if required

```
  "DownstreamApi": {
    "Scopes": "User.ReadBasic.All user.read"
  },
```

### Use Continuous Access Evaluation CAE with downstream API (access_token)

Any API call for the Blazor WASM could be implemented like this:

```
[HttpGet]
public async Task<IActionResult> Get()
{
	try
	{
		// do business which calls an API and throws claims challenge WebApiMsalUiRequiredException 
		// The WWW-Authenticate header is set using the OpenID Connect standards and Signals spec.
	}
	catch (WebApiMsalUiRequiredException hex)
	{
		var claimChallenge = WwwAuthenticateParameters
			.GetClaimChallengeFromResponseHeaders(hex.Headers);
			
		return Unauthorized(claimChallenge);
	}
}
```

the API call could look like this:

```
public async Task<T> CallApiAsync(string url)
{
	var client = _clientFactory.CreateClient();

	// ... add bearer token
	
	var response = await client.GetAsync(url);
	if (response.IsSuccessStatusCode)
	{
		var stream = await response.Content.ReadAsStreamAsync();
		var payload = await JsonSerializer.DeserializeAsync<T>(stream);

		return payload;
	}

	// ... you could check  the WWW-Authenticate header first, if it is a CAE challenge
	
	throw new WebApiMsalUiRequiredException($"Error: {response.StatusCode}.", response);
}
```

### Use Continuous Access Evaluation CAE as standalone (id_token)

If using a CAE authcontext in a standalone project, you only need to challenge against the claims in the application.

```
private readonly CaeCliamsChallengeService _caeCliamsChallengeService;

public AdminApiCallsController(CaeCliamsChallengeService caeCliamsChallengeService)
{
	_caeCliamsChallengeService = caeCliamsChallengeService;
}

[HttpGet]
public async Task<IActionResult> Get()
{
	// if CAE claim missing in id token, the required claims challenge is returned
	var claimsChallenge = _caeCliamsChallengeService
		.CheckForRequiredAuthContextIdToken(AuthContextId.C1, HttpContext);

	if (claimsChallenge != null)
	{
		return Unauthorized(claimsChallenge);
	}
```

### uninstall

```
dotnet new -u Blazor.BFF.AzureAD.Template
```

## Development

### build

https://docs.microsoft.com/en-us/dotnet/core/tutorials/create-custom-template

```
nuget pack content/Blazor.BFF.AzureAD.Template.nuspec
```

### install developement

Locally built nupkg:

```
dotnet new -i Blazor.BFF.AzureAD.Template.1.1.0.nupkg
```

Local folder:

```
dotnet new -i <PATH>
```

Where `<PATH>` is the path to the folder containing .template.config.

## Azure App registrations documentation

https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app

## Credits, Used NuGet packages + ASP.NET Core 6.0 standard packages

- NetEscapades.AspNetCore.SecurityHeaders
- IdentityModel.AspNetCore

## Links

https://github.com/AzureAD/microsoft-identity-web

