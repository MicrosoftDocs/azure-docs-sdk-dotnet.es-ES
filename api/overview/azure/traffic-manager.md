---
title: Bibliotecas de Azure Traffic Manager para .NET
description: Referencia de las bibliotecas de Azure Traffic Manager para .NET
keywords: Azure, .NET, SDK, API, Traffic Manager
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: traffic-manager
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 05856cbe48a5cf5f0c9ebf43609a029928f490f9
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065875"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="00711-104">Bibliotecas de Azure Traffic Manager para .NET</span><span class="sxs-lookup"><span data-stu-id="00711-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="00711-105">Información general</span><span class="sxs-lookup"><span data-stu-id="00711-105">Overview</span></span>

<span data-ttu-id="00711-106">Microsoft Azure Traffic Manager permite controlar la distribución del tráfico de los usuarios para puntos de conexión de servicio en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="00711-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="00711-107">Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="00711-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="00711-108">También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure.</span><span class="sxs-lookup"><span data-stu-id="00711-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="00711-109">Más información acerca de [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="00711-109">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="00711-110">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="00711-110">Management library</span></span>

<span data-ttu-id="00711-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="00711-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="00711-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="00711-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="00711-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="00711-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="00711-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="00711-114">Samples</span></span>

<span data-ttu-id="00711-115">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="00711-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package