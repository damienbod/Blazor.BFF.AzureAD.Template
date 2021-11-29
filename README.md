# Blazor WASM hosted in ASP.NET COre using Azure AD BFF

[![.NET](https://github.com/damienbod/BlazorTemplates/actions/workflows/dotnet.yml/badge.svg)](https://github.com/damienbod/BlazorTemplates/actions/workflows/dotnet.yml) 

[![NuGet Status](http://img.shields.io/nuget/v/IdentityServer4AspNetCoreIdentityTemplate.svg?style=flat-square)](https://www.nuget.org/packages/IdentityServer4AspNetCoreIdentityTemplate/) 

[Change log](https://github.com/damienbod/BlazorTemplates/blob/main/Changelog.md)

## Features

- ASP.NET Core 6
- BFF
- Azure AD


## Using the template

### install

From NuGet:

```
dotnet new -i BlazorBffAzureADTemplate
```

Locally built nupkg:

```
dotnet new -i BlazorBffAzureADTemplate.1.0.0.nupkg
```

Local folder:

```
dotnet new -i <PATH>
```

Where `<PATH>` is the path to the folder containing .template.config.

### run

```
dotnet new blazorbffaad -n YourCompany.Bff
```

Use the `-n` or `--name` parameter to change the name of the output created. This string is also used to substitute the namespace name in the .cs file for the project.

### uninstall

```
dotnet new -u BlazorBffAzureADTemplate
```

## Development

### build

https://docs.microsoft.com/en-us/dotnet/core/tutorials/create-custom-template

```
nuget pack contentaad/BlazorBffAzureADTemplate.nuspec
```


## Credits, Used NuGet packages + ASP.NET Core 6.0 standard packages

- NetEscapades.AspNetCore.SecurityHeaders
- Serilog

## Links
