---
title: Bibliotecas de Azure Active Directory para .NET
description: Referencia de las bibliotecas de Azure Active Directory para .NET
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: adbe907888e49066b6d67a4fb26410a6f6b3b095
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-active-directory-libraries-for-net"></a>Bibliotecas de Azure Active Directory para .NET

## <a name="overview"></a>Información general

Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con Azure Active Directory.

Para empezar a trabajar con Azure Active Directory, consulte [Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).

## <a name="client-library"></a>Biblioteca de cliente

Conecte y autentique a los usuarios o aplicaciones a través de OAuth2, OpenID Connect, autenticación de API Graph de Active Directory o [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a>Ejemplo de código

Recupere un token de acceso para una aplicación de escritorio.

```csharp
/* Include this "using" directive...
using Microsoft.IdentityModel.Clients.ActiveDirectory;
*/

AuthenticationResult result = null;
AuthenticationContext authContext = new AuthenticationContext("https://someauthority.com");
try
{
    result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
}
catch (AdalException ex)
{
    // An unexpected error occurred, or user canceled the sign in.
    if (ex.ErrorCode != "access_denied")
        MessageBox.Show(ex.Message);

    return;
}
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a>Muestras

* [Uso de OpenID Connect para autenticar a los usuarios de un inquilino de Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [Uso de Oauth2 para llamar a una API web con permisos de aplicación](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [Uso del control de acceso basado en rol (RBAC) en una aplicación](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

Explore la colección completa de [ejemplos de código de Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-code-samples).

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package