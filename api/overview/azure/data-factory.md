---
title: Bibliotecas de Azure Data Factory para .NET
description: Referencia de las bibliotecas de Azure Data Factory para .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 09/22/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter
ms.openlocfilehash: 6f1a1cf9ac8189af59ff4e3f42dc1d8fb9620ea2
ms.sourcegitcommit: f35939d37f67485b3667739b02621e317db3e391
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="d5897-104">Bibliotecas de Azure Data Factory para .NET</span><span class="sxs-lookup"><span data-stu-id="d5897-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="d5897-105">Información general</span><span class="sxs-lookup"><span data-stu-id="d5897-105">Overview</span></span>

<span data-ttu-id="d5897-106">Azure Data Factory es un servicio de integración de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="d5897-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="d5897-107">Permite crear flujos de trabajo controlados por datos en la nube para orquestar y automatizar tanto el movimiento de datos como la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="d5897-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="d5897-108">Para más información, lea [Introducción a Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="d5897-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="d5897-109">Biblioteca de administración: Data Factory V2 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="d5897-109">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="d5897-110">La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory V2 (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="d5897-110">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="d5897-111">Para más información, consulte [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net) (Crear una factoría de datos y una canalización mediante SDK de .NET).</span><span class="sxs-lookup"><span data-stu-id="d5897-111">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="d5897-112">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d5897-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d5897-113">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5897-113">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="d5897-114">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="d5897-114">Code Example</span></span>

<span data-ttu-id="d5897-115">En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d5897-115">The following example uses the management library to create a data factory.</span></span>

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5897-116">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="d5897-116">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="d5897-117">Biblioteca de administración: Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="d5897-117">Management library - Data Factory V1</span></span>

<span data-ttu-id="d5897-118">La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory, versión 1.</span><span class="sxs-lookup"><span data-stu-id="d5897-118">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="d5897-119">Para más información, consulte la documentación de [Data Factory, versión 1](/azure/data-factory/v1/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="d5897-119">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="d5897-120">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="d5897-120">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="d5897-121">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d5897-121">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="d5897-122">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="d5897-122">Code Example</span></span>

<span data-ttu-id="d5897-123">En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="d5897-123">The following example uses the management library to create a data factory.</span></span>

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d5897-124">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="d5897-124">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="d5897-125">Muestras</span><span class="sxs-lookup"><span data-stu-id="d5897-125">Samples</span></span>

* <span data-ttu-id="d5897-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving: una aplicación de ejemplo para Azure IOT y dispositivos móviles) que usa Data Factory para proporcionar la información.</span><span class="sxs-lookup"><span data-stu-id="d5897-126">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="d5897-127">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="d5897-127">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
