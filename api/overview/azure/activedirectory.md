---
title: Bibliotecas de Azure Active Directory para .NET
description: Referencia de las bibliotecas de Azure Active Directory para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: active-directory
ms.openlocfilehash: 0226f06546f7dc14b9ab3392008744754d47a19a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190228"
---
# <a name="azure-active-directory-libraries-for-net"></a><span data-ttu-id="edd0d-103">Bibliotecas de Azure Active Directory para .NET</span><span class="sxs-lookup"><span data-stu-id="edd0d-103">Azure Active Directory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="edd0d-104">Información general</span><span class="sxs-lookup"><span data-stu-id="edd0d-104">Overview</span></span>

<span data-ttu-id="edd0d-105">Proporcione inicio de sesión a los usuarios y controle el acceso a aplicaciones y API con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="edd0d-105">Sign-on users and manage access to applications and APIs with Azure Active Directory.</span></span>

<span data-ttu-id="edd0d-106">Para empezar a trabajar con Azure Active Directory, consulte [Inicio y cierre de sesión de la aplicación web de ASP.NET con Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span><span class="sxs-lookup"><span data-stu-id="edd0d-106">To get started with Azure Active Directory, see [ASP.NET web app sign-in and sign-out with Azure AD](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="edd0d-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="edd0d-107">Client library</span></span>

<span data-ttu-id="edd0d-108">Conecte y autentique a los usuarios o aplicaciones a través de OAuth2, OpenID Connect, autenticación de Graph API de Active Directory o [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span><span class="sxs-lookup"><span data-stu-id="edd0d-108">Connect and authenticate users or applications over OAuth2, OpenID Connect, Active Directory Graph API authentication or [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference).</span></span>

<span data-ttu-id="edd0d-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="edd0d-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="edd0d-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="edd0d-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

#### <a name="net-core-cli"></a><span data-ttu-id="edd0d-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="edd0d-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.IdentityModel.Clients.ActiveDirectory
```

### <a name="code-example"></a><span data-ttu-id="edd0d-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="edd0d-112">Code Example</span></span>

<span data-ttu-id="edd0d-113">Recupere un token de acceso para una aplicación de escritorio.</span><span class="sxs-lookup"><span data-stu-id="edd0d-113">Retrieve an access token for a desktop application.</span></span>

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
> [<span data-ttu-id="edd0d-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="edd0d-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/activedirectory/client)

### <a name="samples"></a><span data-ttu-id="edd0d-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="edd0d-115">Samples</span></span>

* [<span data-ttu-id="edd0d-116">Uso de OpenID Connect para autenticar a los usuarios de un inquilino de Azure AD</span><span class="sxs-lookup"><span data-stu-id="edd0d-116">Use OpenID Connect to authenticate users from an Azure AD tenant</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
* [<span data-ttu-id="edd0d-117">Uso de Oauth2 para llamar a una API web con permisos de aplicación</span><span class="sxs-lookup"><span data-stu-id="edd0d-117">Use Oauth2 to call a web API with application permissions</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-webapi-oauth2-appidentity)
* [<span data-ttu-id="edd0d-118">Uso del control de acceso basado en rol (RBAC) en una aplicación</span><span class="sxs-lookup"><span data-stu-id="edd0d-118">Use role-based access control (RBAC) in an application</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims)

<span data-ttu-id="edd0d-119">Explore la colección completa de [ejemplos de código de Azure Active Directory](/azure/active-directory/develop/active-directory-code-samples).</span><span class="sxs-lookup"><span data-stu-id="edd0d-119">Explore the full collection of [Azure Active Directory code samples](/azure/active-directory/develop/active-directory-code-samples).</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
