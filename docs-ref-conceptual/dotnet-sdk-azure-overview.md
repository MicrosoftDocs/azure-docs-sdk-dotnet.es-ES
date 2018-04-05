---
title: API de Azure .NET
description: Introducción a las API de Azure para .NET
keywords: Azure, .NET, SDK, API, NuGet, bibliotecas, paquetes
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 26360a516220ca9d3e8901e60cb23ecbd02863cd
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="azure-net-apis"></a><span data-ttu-id="60a18-104">API de Azure .NET</span><span class="sxs-lookup"><span data-stu-id="60a18-104">Azure .NET APIs</span></span>

<span data-ttu-id="60a18-105">Las API de Azure .NET le permiten usar servicios de Azure y administrar recursos de Azure desde el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60a18-105">The Azure .NET APIs let you use Azure services and manage Azure resources from your application code.</span></span> <span data-ttu-id="60a18-106">Las API están disponibles como [paquetes NuGet](/dotnet/api/overview/azure/) para su uso en proyectos .NET.</span><span class="sxs-lookup"><span data-stu-id="60a18-106">The APIs are available as [NuGet packages](/dotnet/api/overview/azure/) for use in your .NET projects.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="60a18-107">Administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="60a18-107">Manage Azure resources</span></span>

<span data-ttu-id="60a18-108">Las bibliotecas de Azure para .NET le permiten crear y administrar recursos de Azure de las aplicaciones .NET.</span><span class="sxs-lookup"><span data-stu-id="60a18-108">The Azure libraries for .NET let you create and manage Azure resources from your .NET applications.</span></span>

<span data-ttu-id="60a18-109">Muchos de los paquetes para la administración de recursos de Azure tienen una interfaz [fluida](dotnet-sdk-azure-concepts.md) para configurar los recursos exactamente según sus especificaciones.</span><span class="sxs-lookup"><span data-stu-id="60a18-109">Many of the packages for managing Azure resources have a [fluent](dotnet-sdk-azure-concepts.md) interface to configure resources exactly to your specifications.</span></span> <span data-ttu-id="60a18-110">Por ejemplo, para crear una máquina virtual Windows escribiría el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="60a18-110">For example, to create a Windows VM you would write the following code:</span></span>

```csharp
var windowsVM = azure.VirtualMachines.Define(windowsVmName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername(username)
    .WithAdminPassword(password)
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
 ```

<span data-ttu-id="60a18-111">Revise la [lista de servicios de .NET](/dotnet/api/overview/azure/) para empezar a usar las bibliotecas inmediatamente con los proyectos.</span><span class="sxs-lookup"><span data-stu-id="60a18-111">Review the [.NET service list](/dotnet/api/overview/azure/) to start using the libraries immediately with your projects.</span></span> <span data-ttu-id="60a18-112">A continuación, lea el [artículo de introducción](dotnet-sdk-azure-get-started.md) para configurar la autenticación y ejecutar el código de ejemplo en su propia suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="60a18-112">Then read the [get started article](dotnet-sdk-azure-get-started.md) to set up authentication and run sample code against your own Azure subscription.</span></span>  <span data-ttu-id="60a18-113">El [artículo de conceptos](dotnet-sdk-azure-concepts.md) se adentra en las convenciones que usa el SDK y cómo aprovecharlas para simplificar el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="60a18-113">The [concepts article](dotnet-sdk-azure-concepts.md) goes into the conventions the SDK uses and how to leverage them to simplify your application code.</span></span> <span data-ttu-id="60a18-114">Las nuevas características, cambios importantes e instrucciones de migración están disponibles en las [notas de la versión](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="60a18-114">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

## <a name="consume-azure-services"></a><span data-ttu-id="60a18-115">Uso de servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="60a18-115">Consume Azure services</span></span>

<span data-ttu-id="60a18-116">Además de usar las API de .NET para crear y administrar mediante programación los recursos dentro de Azure, también puede usar las API de .NET para conectar sus aplicaciones a estos recursos y utilizarlos en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="60a18-116">In addition to using .NET APIs to create and programmatically manage resources within Azure, you can also then use .NET APIs to connect your applications to these resources and use them at runtime.</span></span>  <span data-ttu-id="60a18-117">Por ejemplo, puede conectarse a SQL Database o almacenar datos en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="60a18-117">For example, you might connect to a SQL Database or store data within Azure Storage.</span></span>  <span data-ttu-id="60a18-118">Puede identificar qué paquete NuGet debe usar para un determinado servicio de Azure explorando nuestra [lista completa de API de servicio](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="60a18-118">You can identify which NuGet package to use for a particular Azure service by browsing our [full list of service APIs](/dotnet/api/overview/azure/).</span></span>  

## <a name="samples"></a><span data-ttu-id="60a18-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="60a18-119">Samples</span></span>

<span data-ttu-id="60a18-120">Los ejemplos siguientes tratan tareas comunes de automatización con bibliotecas de Azure para .NET:</span><span class="sxs-lookup"><span data-stu-id="60a18-120">The following samples cover common automation tasks with the Azure libraries for .NET:</span></span>

- [<span data-ttu-id="60a18-121">Máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="60a18-121">Virtual machines</span></span>](dotnet-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="60a18-122">Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="60a18-122">Web apps</span></span>](dotnet-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="60a18-123">SQL Database</span><span class="sxs-lookup"><span data-stu-id="60a18-123">SQL Database</span></span>](dotnet-sdk-azure-sql-database-samples.md)

<span data-ttu-id="60a18-124">Hay disponible una [referencia](/dotnet/api/overview/azure/?view=azure-dotnet) unificada para todos los paquetes tanto del servicio como de las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="60a18-124">A unified [reference](/dotnet/api/overview/azure/?view=azure-dotnet) is available for all packages in both the service and management libraries.</span></span> <span data-ttu-id="60a18-125">Las nuevas características, cambios importantes e instrucciones de migración están disponibles en las [notas de la versión](dotnet-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="60a18-125">New features, breaking changes, and migration instructions are available in the [release notes](dotnet-sdk-azure-release-notes.md).</span></span>

[!include[Contribute and community](includes/contribute.md)]