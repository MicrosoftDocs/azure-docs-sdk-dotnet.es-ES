---
title: Bibliotecas de Azure Traffic Manager para .NET
description: Referencia de las bibliotecas de Azure Traffic Manager para .NET
keywords: Azure, .NET, SDK, API, Traffic Manager
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0fc747c25fe368b5d67f70af1e2b9afc5e07f615
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-traffic-manager-libraries-for-net"></a><span data-ttu-id="1965c-104">Bibliotecas de Azure Traffic Manager para .NET</span><span class="sxs-lookup"><span data-stu-id="1965c-104">Azure Traffic Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1965c-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1965c-105">Overview</span></span>

<span data-ttu-id="1965c-106">Microsoft Azure Traffic Manager permite controlar la distribución del tráfico de los usuarios para puntos de conexión de servicio en distintos centros de datos.</span><span class="sxs-lookup"><span data-stu-id="1965c-106">Microsoft Azure Traffic Manager allows you to control the distribution of user traffic for service endpoints in different datacenters.</span></span> <span data-ttu-id="1965c-107">Entre los puntos de conexión de servicio compatibles con Traffic Manager, se incluyen máquinas virtuales de Azure, Web Apps y servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="1965c-107">Service endpoints supported by Traffic Manager include Azure VMs, Web Apps, and cloud services.</span></span> <span data-ttu-id="1965c-108">También puede utilizar el Administrador de tráfico con puntos de conexión externos, que no forman parte de Azure.</span><span class="sxs-lookup"><span data-stu-id="1965c-108">You can also use Traffic Manager with external, non-Azure endpoints.</span></span>

<span data-ttu-id="1965c-109">Más información acerca de [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="1965c-109">Learn more about [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview).</span></span>  

## <a name="management-library"></a><span data-ttu-id="1965c-110">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="1965c-110">Management library</span></span>

<span data-ttu-id="1965c-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="1965c-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.TrafficManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1965c-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1965c-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.TrafficManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.TrafficManager.Fluent
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1965c-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="1965c-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/trafficmanager/management)

## <a name="samples"></a><span data-ttu-id="1965c-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="1965c-114">Samples</span></span>

<span data-ttu-id="1965c-115">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="1965c-115">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package