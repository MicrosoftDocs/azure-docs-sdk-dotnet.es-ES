---
title: Bibliotecas de Azure Traffic Manager para .NET
description: Referencia de las bibliotecas de Azure Traffic Manager para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: traffic-manager
ms.openlocfilehash: a75b5c566496f73475d24d62288a00c7d5775168
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190828"
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="5ba1e-103">Bibliotecas de Azure Traffic Manager para .NET</span><span class="sxs-lookup"><span data-stu-id="5ba1e-103">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5ba1e-104">Información general</span><span class="sxs-lookup"><span data-stu-id="5ba1e-104">Overview</span></span>

<span data-ttu-id="5ba1e-105">Microsoft Azure Traffic Manager permite controlar la distribución del tráfico de los usuarios para puntos de conexión de servicio en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="5ba1e-105">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="5ba1e-106">Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="5ba1e-106">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="5ba1e-107">También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure.</span><span class="sxs-lookup"><span data-stu-id="5ba1e-107">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="5ba1e-108">Más información acerca de [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="5ba1e-108">Learn more about [Azure Traffic Manager](/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="5ba1e-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="5ba1e-109">Management library</span></span>

<span data-ttu-id="5ba1e-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5ba1e-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5ba1e-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ba1e-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5ba1e-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="5ba1e-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="5ba1e-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5ba1e-113">Samples</span></span>

<span data-ttu-id="5ba1e-114">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5ba1e-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package