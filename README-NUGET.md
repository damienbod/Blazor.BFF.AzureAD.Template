# Blazor WASM hosted in ASP.NET Core using Azure AD BFF (server authentication)

[![.NET](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/actions/workflows/dotnet.yml/badge.svg)](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/actions/workflows/dotnet.yml) [![NuGet Status](http://img.shields.io/nuget/v/Blazor.BFF.AzureAD.Template.svg?style=flat-square)](https://www.nuget.org/packages/Blazor.BFF.AzureAD.Template/) [Change log](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/blob/main/Changelog.md)

## Features

- WASM hosted in ASP.NET Core 6
- BFF with Azure AD using Microsoft.Identity.Web
- OAuth2 and OpenID Connect OIDC
- No tokens in the browser

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

### uninstall

```
dotnet new -u Blazor.BFF.AzureAD.Template
```


## Credits, Used NuGet packages + ASP.NET Core 6.0 standard packages

- NetEscapades.AspNetCore.SecurityHeaders

## Links

https://github.com/AzureAD/microsoft-identity-web
