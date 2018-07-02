---
title: Bibliotecas de Azure Active Directory para .NET
description: Referencia de las bibliotecas de Azure Active Directory para .NET
keywords: Azure, .NET, SDK, API, AAD, Active Directory
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: active-directory
ms.custom: devcenter, svc-overview
ms.openlocfilehash: a5a228fcde29dbef6a6e8d0482121ee710b002a4
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065865"
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="5b773-104">Bibliotecas de Azure Active Directory para .NET</span><span class="sxs-lookup"><span data-stu-id="5b773-104">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5b773-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5b773-105">Overview</span></span>

<span data-ttu-id="5b773-106">Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5b773-106">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="5b773-107">Para empezar a trabajar con Azure Active Directory, consulte [Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span><span class="sxs-lookup"><span data-stu-id="5b773-107">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="5b773-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="5b773-108">Client library</span></span>

<span data-ttu-id="5b773-109">Conecte y autentique a los usuarios o aplicaciones a través de OAuth2, OpenID Connect, autenticación de Graph API de Active Directory o [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="5b773-109">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="5b773-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5b773-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5b773-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b773-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="5b773-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="5b773-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="5b773-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="5b773-113">Code Example</span></span>

<span data-ttu-id="5b773-114">Recupere un token de acceso para una aplicación de escritorio.</span><span class="sxs-lookup"><span data-stu-id="5b773-114">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="5b773-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="5b773-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="5b773-116">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5b773-116">Samples</span></span>

* [<span data-ttu-id="5b773-117">Uso de OpenID Connect para autenticar a los usuarios de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="5b773-117">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [<span data-ttu-id="5b773-118">Uso de Oauth2 para llamar a una API web con permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="5b773-118">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [<span data-ttu-id="5b773-119">Uso del control de acceso basado en rol (RBAC) en una aplicación</span><span class="sxs-lookup"><span data-stu-id="5b773-119">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

<span data-ttu-id="5b773-120">Explore la colección completa de [ejemplos de código de Azure Active Directory](/azure/active-directory/develop/active-directory-code-samples).</span><span class="sxs-lookup"><span data-stu-id="5b773-120">Explore the full collection of [Azure Active Directory code samples](/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
