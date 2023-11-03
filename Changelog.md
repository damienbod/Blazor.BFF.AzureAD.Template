# Blazor.BFF.AzureAD.Template

[Readme](https://github.com/damienbod/Blazor.BFF.AzureAD.Template/blob/main/README.md) 

**2023-11-03** 2.12.0
- Updated packages
- fixed XSS security header

**2023-06-21** 2.1.0
- Switched to Graph SDK 5
- Updated packages
- fixed Graph photo encoding

**2023-03-11** 2.0.2
- Fix security headers, use on app requests including API calls
- Updated packages

**2023-01-22** 2.0.1
- Updated .NET packages

**2022-12-03** 2.0.0
- Updated to .NET 7

**2022-09-23** 1.2.7
- Updated packages

**2022-08-12** 1.2.6
- Http port generator added
- Updated packages

**2022-08-07** 1.2.5
- Improve template
- Updated packages

**2022-07-09** 1.2.4
- Improved UserController
- Updated Nuget packages

**2022-05-22** 1.2.3
- use new top-level statements and remove
- enable ImplicitUsings
- add IAntiforgeryHttpClientFactory/AntiforgeryHttpClientFactory
- Replace of IdentityModel with System.Security.Claims and remove IdentityModel nuget package

**2022-05-20** 1.2.1
- Add support for Azure AD Continuous Access Evaluation CAE
- Add 404, 401, response handling
- Update nuget packages

**2022-03-20** 1.1.0
- Update nuget packages
- Enable nullable checks

**2022-03-05** 1.0.10
- Update nuget packages

**2022-02-11** 1.0.9
- Update namespaces
- Update nuget packages

**2022-01-23** 1.0.8
- Remove PWA items, default template uses anti-forgery cookies and no PWA support
  (Will consider supporting this later, requires switching to CORS preflight CSRF protection)
- Using the AuthorizedHandler for protected requests

**2022-01-21** 1.0.7
- removed unused client file

**2022-01-17** 1.0.6
- removed launchsettings.json from WASM client
- removed unused client files

**2022-01-09** 1.0.5
- small fixes
- removed unused configurations and packages
- switched to MicrosoftGraph

**2022-01-04** 1.0.4
- small fixes
- nuget packages updated

**2021-12-09** 1.0.2
- Removed static host file
- Updated Nuget packages

**2021-11-30** 1.0.0
- Initial release 
- Azure AD authentication using Microsoft.Identity.Web
- Microsoft Graph
- ASP.NET Core 6


