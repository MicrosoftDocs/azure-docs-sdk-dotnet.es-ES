---
title: Bibliotecas de Azure Data Lake Store para .NET
description: Referencia de las bibliotecas de Azure Data Lake Store para .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2b1c51575872b12a94eb44c7c082996bb879bcc9
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a><span data-ttu-id="491fd-104">Bibliotecas de Azure Data Lake Store para .NET</span><span class="sxs-lookup"><span data-stu-id="491fd-104">Azure Data Lake Store libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="491fd-105">Información general</span><span class="sxs-lookup"><span data-stu-id="491fd-105">Overview</span></span>

<span data-ttu-id="491fd-106">El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="491fd-106">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="491fd-107">Azure Data Lake permite capturar datos de cualquier tamaño, tipo y velocidad de ingesta en un único lugar para realizar análisis exploratorios y operativos.</span><span class="sxs-lookup"><span data-stu-id="491fd-107">Azure Data Lake enables you to capture data of any size, type, and ingestion speed in one single place for operational and exploratory analytics.</span></span>

<span data-ttu-id="491fd-108">Para más información, consulte [Información general de Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="491fd-108">To learn more, see [Overview of Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="491fd-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="491fd-109">Management library</span></span>

<span data-ttu-id="491fd-110">Utilice la biblioteca de administración para conectarse a sus repositorios de macrodatos y administrarlos.</span><span class="sxs-lookup"><span data-stu-id="491fd-110">Use the management library to connect to and manage your big data repositories.</span></span>

<span data-ttu-id="491fd-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="491fd-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="491fd-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="491fd-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

### <a name="code-example"></a><span data-ttu-id="491fd-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="491fd-113">Code Example</span></span>

<span data-ttu-id="491fd-114">En este ejemplo se realiza la autenticación en una cuenta y almacén de Analytics, y se crean los clientes necesarios para la administración.</span><span class="sxs-lookup"><span data-stu-id="491fd-114">This example authenticates to an analytics account and store and creates the clients necessary for management.</span></span>

```csharp
/*
using AdlClient
using AdlClient.Models 
*/

// Setup authentication 
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
StoreAccountRef adls_account = new StoreAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
StoreClient adls = new StoreClient(auth, adls_account);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="491fd-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="491fd-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakestore/management)

## <a name="samples"></a><span data-ttu-id="491fd-116">Muestras</span><span class="sxs-lookup"><span data-stu-id="491fd-116">Samples</span></span>

* [<span data-ttu-id="491fd-117">Ejemplo de cliente de .NET de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="491fd-117">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="491fd-118">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="491fd-118">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
