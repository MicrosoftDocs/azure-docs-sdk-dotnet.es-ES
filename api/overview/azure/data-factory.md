---
title: Bibliotecas de Azure Data Factory para .NET
description: Referencia de las bibliotecas de Azure Data Factory para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: data-factory
ms.openlocfilehash: 9a779f223cd0e158e99afcf1ee011d121f2fe838
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190328"
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="eb47f-103">Bibliotecas de Azure Data Factory para .NET</span><span class="sxs-lookup"><span data-stu-id="eb47f-103">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="eb47f-104">Información general</span><span class="sxs-lookup"><span data-stu-id="eb47f-104">Overview</span></span>

<span data-ttu-id="eb47f-105">Azure Data Factory es un servicio de integración de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="eb47f-105">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="eb47f-106">Permite crear flujos de trabajo controlados por datos en la nube para orquestar y automatizar tanto el movimiento de datos como la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="eb47f-106">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="eb47f-107">Para más información, lea [Introducción a Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="eb47f-107">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library---data-factory-v2-preview"></a><span data-ttu-id="eb47f-108">Biblioteca de administración: Data Factory V2 (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="eb47f-108">Management library - Data Factory V2 (Preview)</span></span>

<span data-ttu-id="eb47f-109">La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory V2 (versión preliminar).</span><span class="sxs-lookup"><span data-stu-id="eb47f-109">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory V2 (Preview).</span></span>  <span data-ttu-id="eb47f-110">Para más información, consulte [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net) (Crear una factoría de datos y una canalización mediante SDK de .NET).</span><span class="sxs-lookup"><span data-stu-id="eb47f-110">For more information, see [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net).</span></span>

<span data-ttu-id="eb47f-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="eb47f-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="eb47f-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb47f-112">Visual Studio Package Manager</span></span>

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a><span data-ttu-id="eb47f-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="eb47f-113">Code Example</span></span>

<span data-ttu-id="eb47f-114">En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="eb47f-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="eb47f-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="eb47f-115">Explore the management APIs</span></span>](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a><span data-ttu-id="eb47f-116">Biblioteca de administración: Data Factory V1</span><span class="sxs-lookup"><span data-stu-id="eb47f-116">Management library - Data Factory V1</span></span>

<span data-ttu-id="eb47f-117">La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory, versión 1.</span><span class="sxs-lookup"><span data-stu-id="eb47f-117">Use the management library to create and schedule data-driven workflows (pipelines) in Data Factory Version 1.</span></span>  <span data-ttu-id="eb47f-118">Para más información, consulte la documentación de [Data Factory, versión 1](/azure/data-factory/v1/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="eb47f-118">For more information, review the documentation for [Data Factory Version 1](/azure/data-factory/v1/data-factory-introduction).</span></span>

<span data-ttu-id="eb47f-119">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="eb47f-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="eb47f-120">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb47f-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="eb47f-121">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="eb47f-121">Code Example</span></span>

<span data-ttu-id="eb47f-122">En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="eb47f-122">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="eb47f-123">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="eb47f-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="eb47f-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="eb47f-124">Samples</span></span>

* <span data-ttu-id="eb47f-125">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving: una aplicación de ejemplo para Azure IOT y dispositivos móviles) que usa Data Factory para proporcionar la información.</span><span class="sxs-lookup"><span data-stu-id="eb47f-125">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="eb47f-126">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="eb47f-126">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
