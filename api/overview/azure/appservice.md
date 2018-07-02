---
title: Bibliotecas de Azure App Service para .NET
description: Referencia de las bibliotecas de Azure App Service para .NET
keywords: Azure, .NET, SDK, API, aplicaciones web, App Service, móvil, asp.net
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0fee28930dff5075cdd84fe3cb88850e07bc6ccb
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065805"
---
# <a name="azure-app-service-libraries-for-net"></a><span data-ttu-id="89a92-104">Bibliotecas de Azure App Service para .NET</span><span class="sxs-lookup"><span data-stu-id="89a92-104">Azure App Service libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="89a92-105">Información general</span><span class="sxs-lookup"><span data-stu-id="89a92-105">Overview</span></span>

<span data-ttu-id="89a92-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) le permite implementar y escalar sitios web, aplicaciones web, servicios y API de REST.</span><span class="sxs-lookup"><span data-stu-id="89a92-106">[Azure App Service](/azure/app-service/app-service-value-prop-what-is) allows you to deploy and scale websites, web applications, services, and REST APIs.</span></span>

## <a name="management-api"></a><span data-ttu-id="89a92-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="89a92-107">Management API</span></span>

<span data-ttu-id="89a92-108">Implemente, administre y escale elementos hospedados en Azure App Service con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="89a92-108">Deploy, manage, and scale elements hosted in Azure App Service with the management API.</span></span>

<span data-ttu-id="89a92-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="89a92-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.AppService.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="89a92-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89a92-110">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.AppService.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="89a92-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="89a92-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.AppService.Fluent
```

### <a name="code-example"></a><span data-ttu-id="89a92-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="89a92-112">Code Example</span></span>

<span data-ttu-id="89a92-113">Cree una aplicación web nueva.</span><span class="sxs-lookup"><span data-stu-id="89a92-113">Create a new web app.</span></span>

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
> [<span data-ttu-id="89a92-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="89a92-114">Explore the Management APIs</span></span>](/dotnet/api/overview/azure/appservice/management)

### <a name="samples"></a><span data-ttu-id="89a92-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="89a92-115">Samples</span></span>

* [<span data-ttu-id="89a92-116">Administración de aplicaciones web con el SDK de .NET de Azure</span><span class="sxs-lookup"><span data-stu-id="89a92-116">Manage your web apps with the .NET SDK for Azure</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-manage/)
* [<span data-ttu-id="89a92-117">Ejemplo de ASP.NET para Azure App Service</span><span class="sxs-lookup"><span data-stu-id="89a92-117">ASP.NET sample for Azure App Service</span></span>](https://azure.microsoft.com/resources/samples/app-service-web-dotnet-get-started/)

<span data-ttu-id="89a92-118">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) de ejemplos de Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="89a92-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=app%20service) of Azure App Service samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package