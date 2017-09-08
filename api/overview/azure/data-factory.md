---
title: Bibliotecas de Azure Data Factory para .NET
description: Referencia de las bibliotecas de Azure Data Factory para .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/20/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: e0b85d7d3988febca6dce7f4038825d74e4b8d2e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-data-factory-libraries-for-net"></a><span data-ttu-id="b7a83-104">Bibliotecas de Azure Data Factory para .NET</span><span class="sxs-lookup"><span data-stu-id="b7a83-104">Azure Data Factory libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="b7a83-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b7a83-105">Overview</span></span>

<span data-ttu-id="b7a83-106">Azure Data Factory es un servicio de integración de datos en la nube.</span><span class="sxs-lookup"><span data-stu-id="b7a83-106">Azure Data Factory is a cloud-based data integration service.</span></span> <span data-ttu-id="b7a83-107">Permite crear flujos de trabajo controlados por datos en la nube para orquestar y automatizar tanto el movimiento de datos como la transformación de datos.</span><span class="sxs-lookup"><span data-stu-id="b7a83-107">It enables you to create data-driven workflows in the cloud to orchestrate and automate data movement and data transformation.</span></span>

<span data-ttu-id="b7a83-108">Para más información, lea [Introducción a Azure Data Factory](/azure/data-factory/data-factory-introduction).</span><span class="sxs-lookup"><span data-stu-id="b7a83-108">To learn more, read the [Introduction to Azure Data Factory](/azure/data-factory/data-factory-introduction).</span></span>

## <a name="management-library"></a><span data-ttu-id="b7a83-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="b7a83-109">Management library</span></span>

<span data-ttu-id="b7a83-110">Utilice la biblioteca de administración para crear y programar flujos de trabajo controlados por datos (canalizaciones).</span><span class="sxs-lookup"><span data-stu-id="b7a83-110">Use the management library to create and schedule data-driven workflows (pipelines).</span></span>

<span data-ttu-id="b7a83-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="b7a83-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b7a83-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b7a83-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a><span data-ttu-id="b7a83-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="b7a83-113">Code Example</span></span>

<span data-ttu-id="b7a83-114">En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="b7a83-114">The following example uses the management library to create a data factory.</span></span>

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
> [<span data-ttu-id="b7a83-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="b7a83-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a><span data-ttu-id="b7a83-116">Muestras</span><span class="sxs-lookup"><span data-stu-id="b7a83-116">Samples</span></span>

* <span data-ttu-id="b7a83-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving: una aplicación de ejemplo para Azure IOT y dispositivos móviles) que usa Data Factory para proporcionar la información.</span><span class="sxs-lookup"><span data-stu-id="b7a83-117">[MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) that uses Data Factory to drive insights.</span></span>

<span data-ttu-id="b7a83-118">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b7a83-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
