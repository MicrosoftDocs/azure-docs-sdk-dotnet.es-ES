---
title: Bibliotecas de Azure App Service para .NET
description: Referencia de las bibliotecas de Azure App Service para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: app-service
ms.openlocfilehash: 82f8eccfafd2f7b1cf1df1ce0f40212509ccddd3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189998"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="77eed-103">Bibliotecas de Azure App Service para .NET</span><span class="sxs-lookup"><span data-stu-id="77eed-103">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="77eed-104">Información general</span><span class="sxs-lookup"><span data-stu-id="77eed-104">Overview</span></span>

<span data-ttu-id="77eed-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) le permite implementar y escalar sitios web, aplicaciones web, servicios y API de REST.</span><span class="sxs-lookup"><span data-stu-id="77eed-105">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="77eed-106">API de administración</span><span class="sxs-lookup"><span data-stu-id="77eed-106">Management API</span></span>

<span data-ttu-id="77eed-107">Implemente, administre y escale elementos hospedados en Azure App Service con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="77eed-107">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="77eed-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="77eed-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="77eed-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="77eed-109">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="77eed-110">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="77eed-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="77eed-111">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="77eed-111">Code Example</span></span>

<span data-ttu-id="77eed-112">Cree una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="77eed-112">Create a new web app.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.AppService.Fluent;
*/

IWebApp app1 = azure.WebApps
    .Define("MyUniqueWebAddress")
    .WithRegion(Region.USWest)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewWindowsPlan(PricingTier.StandardS1)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="77eed-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="77eed-113">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="77eed-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="77eed-114">Samples</span></span>

* [<span data-ttu-id="77eed-115">Administración de aplicaciones web con el SDK de .NET de Azure</span><span class="sxs-lookup"><span data-stu-id="77eed-115">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="77eed-116">Ejemplo de ASP.NET para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="77eed-116">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="77eed-117">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) de ejemplos de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="77eed-117">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package