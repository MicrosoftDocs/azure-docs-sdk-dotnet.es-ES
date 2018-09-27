---
title: API de almacenamiento de .NET de Azure
description: Referencia de las bibliotecas de Azure Storage para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: storage
ms.openlocfilehash: 2f278f0e3cb10d11190d529f427fa64040ee8b1d
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47189978"
---
# <a name="azure-storage-apis-for-net"></a><span data-ttu-id="f6a61-103">API de Azure Storage para .NET</span><span class="sxs-lookup"><span data-stu-id="f6a61-103">Azure Storage APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f6a61-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f6a61-104">Overview</span></span>

<span data-ttu-id="f6a61-105">Lea y escriba archivos, datos de blob (objeto), pares de clave-valor y mensajes desde las aplicaciones .NET con [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="f6a61-105">Read and write files, blob (object) data, key-value pairs, and messages from your .NET applications with [Azure Storage](https://docs.microsoft.com/azure/storage/storage-introduction).</span></span>

<span data-ttu-id="f6a61-106">Para comenzar a usar Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="f6a61-106">To get started with Azure Storage, see [Get started with Azure Blob storage using .NET](/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

## <a name="client-library"></a><span data-ttu-id="f6a61-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="f6a61-107">Client library</span></span>

<span data-ttu-id="f6a61-108">Use [cadenas de conexión](/azure/storage/storage-create-storage-account#manage-your-storage-account) para conectarse a una cuenta de Azure Storage y, a continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con almacenamiento de blobs, tablas, archivos o colas.</span><span class="sxs-lookup"><span data-stu-id="f6a61-108">Use [connection strings](/azure/storage/storage-create-storage-account#manage-your-storage-account) to connect to an Azure Storage account, then use the client libraries' classes and methods to work with blob, table, file, or queue storage.</span></span>

<span data-ttu-id="f6a61-109">Instale el [paquete NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f6a61-109">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f6a61-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6a61-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a><span data-ttu-id="f6a61-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="f6a61-111">.NET Core CLI</span></span>

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a><span data-ttu-id="f6a61-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="f6a61-112">Code Example</span></span>

<span data-ttu-id="f6a61-113">En este ejemplo se crea un nuevo blob para un nuevo contenedor de una cuenta de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="f6a61-113">This example creates a new blob to a new container in an existing storage account.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
*/

string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=[Storage Account Name]"
    + ";AccountKey=[Storage Account Key]"
    + ";EndpointSuffix=core.windows.net";

CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);
CloudBlobClient serviceClient = account.CreateCloudBlobClient();

// Create container. Name must be lower case.
Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("mycontainer");
container.CreateIfNotExistsAsync().Wait();

// write a blob to the container
CloudBlockBlob blob = container.GetBlockBlobReference("helloworld.txt");
blob.UploadTextAsync("Hello, World!").Wait();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="f6a61-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="f6a61-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a><span data-ttu-id="f6a61-115">API de administración</span><span class="sxs-lookup"><span data-stu-id="f6a61-115">Management APIs</span></span>

<span data-ttu-id="f6a61-116">Cree y administre cuentas y claves de conexión de Azure Storage con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="f6a61-116">Create and manage Azure Storage accounts and connection keys with the management API.</span></span>

<span data-ttu-id="f6a61-117">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f6a61-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f6a61-118">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f6a61-118">Visual Studio package manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="f6a61-119">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="f6a61-119">.NET Core CLI</span></span>

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a><span data-ttu-id="f6a61-120">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="f6a61-120">Code Example</span></span>

<span data-ttu-id="f6a61-121">En este ejemplo se crea una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f6a61-121">This example creates a storage account.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Management.Storage.Fluent
*/

IStorageAccount storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .Create();
```

> [!div class="nextstepactions"]
> [<span data-ttu-id="f6a61-122">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="f6a61-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a><span data-ttu-id="f6a61-123">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f6a61-123">Samples</span></span>

* [<span data-ttu-id="f6a61-124">Introducción a Azure Blob Storage en .NET</span><span class="sxs-lookup"><span data-stu-id="f6a61-124">Get started with Azure Blob Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [<span data-ttu-id="f6a61-125">Introducción a Azure Queue Storage en .NET</span><span class="sxs-lookup"><span data-stu-id="f6a61-125">Get started with Azure Queue Storage in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

<span data-ttu-id="f6a61-126">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) de ejemplos de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f6a61-126">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) of Azure Storage samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package