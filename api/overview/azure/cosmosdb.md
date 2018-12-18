---
title: Bibliotecas de Azure Cosmos DB para .NET
description: Referencia de las bibliotecas de Azure Cosmos DB para .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 8ff565f1cd72eec2f574b45d04ceac526b8c5eb0
ms.sourcegitcommit: 01ec3adba39a6f946015552c28da0a9a6bb57180
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53112023"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="fefb6-103">Bibliotecas de Azure Cosmos DB para .NET</span><span class="sxs-lookup"><span data-stu-id="fefb6-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="fefb6-104">Información general</span><span class="sxs-lookup"><span data-stu-id="fefb6-104">Overview</span></span>

<span data-ttu-id="fefb6-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un servicio de base de datos multimodelo distribuido globalmente.</span><span class="sxs-lookup"><span data-stu-id="fefb6-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="fefb6-106">Está diseñado para permitir que los clientes escalen de manera elástica e independiente el rendimiento y el almacenamiento en cualquier número de regiones geográficas con un completo SLA.</span><span class="sxs-lookup"><span data-stu-id="fefb6-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="fefb6-107">Con Azure Cosmos DB, puede almacenar y tener acceso a bases de datos de documentos, de pares clave-valor, columnares y de grafos mediante API y modelos de programación.</span><span class="sxs-lookup"><span data-stu-id="fefb6-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="fefb6-108">[Introducción a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="fefb6-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="fefb6-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="fefb6-109">Client library</span></span>

<span data-ttu-id="fefb6-110">Utilice la biblioteca de cliente de Azure Cosmos DB para .NET para almacenar los datos y acceder a ellos en un almacén de datos de Azure Cosmos DB existente.</span><span class="sxs-lookup"><span data-stu-id="fefb6-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="fefb6-111">Para automatizar la creación de una nueva cuenta de Azure Cosmos DB, use Azure Portal, la CLI o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fefb6-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="fefb6-112">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="fefb6-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

<span data-ttu-id="fefb6-113">Para instalar la versión 2.x:</span><span class="sxs-lookup"><span data-stu-id="fefb6-113">To install version 2.x:</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fefb6-114">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fefb6-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="fefb6-115">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="fefb6-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

<span data-ttu-id="fefb6-116">Para instalar la versión preliminar de la versión 3.0, dirigida a .NET estándar:</span><span class="sxs-lookup"><span data-stu-id="fefb6-116">To install the preview of version 3.0, which targets .NET standard:</span></span> 

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fefb6-117">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fefb6-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a><span data-ttu-id="fefb6-118">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="fefb6-118">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a><span data-ttu-id="fefb6-119">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="fefb6-119">Code Example</span></span>

<span data-ttu-id="fefb6-120">Este ejemplo se conecta a una base de datos existente SQL API de Azure Cosmos DB, lee un documento de una colección y lo deserializa como un objeto `Item`.</span><span class="sxs-lookup"><span data-stu-id="fefb6-120">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span> <span data-ttu-id="fefb6-121">En este ejemplo, se usa la versión 2.x del SDK para .NET.</span><span class="sxs-lookup"><span data-stu-id="fefb6-121">This example uses version 2.x of the .NET SDK.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

<span data-ttu-id="fefb6-122">En este ejemplo, se conecta con una base de datos de SQL API de Azure Cosmos DB existente, se crea una nueva base de datos y un contenedor, se lee un elemento del contenedor y se deserializa en un objeto `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="fefb6-122">This example connects to an existing Azure Cosmos DB SQL API database, creates a new database and container, reads an item from the container, and deserializes it to a `TodoItem` object.</span></span> <span data-ttu-id="fefb6-123">En este ejemplo, se usa la versión 3.x del SDK para .NET.</span><span class="sxs-lookup"><span data-stu-id="fefb6-123">This example uses version 3.x of the .NET SDK.</span></span>   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fefb6-124">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="fefb6-124">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="fefb6-125">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fefb6-125">Samples</span></span>

* [<span data-ttu-id="fefb6-126">Desarrollo de una aplicación .NET con SQL API de Azure Cosmos DB (versión 2.x)</span><span class="sxs-lookup"><span data-stu-id="fefb6-126">Developing a .NET app using Azure Cosmos DB's SQL API (Version 2.x)</span></span>](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [<span data-ttu-id="fefb6-127">Desarrollo de una aplicación .NET con SQL API de Azure Cosmos DB (versión preliminar de la versión 3.x)</span><span class="sxs-lookup"><span data-stu-id="fefb6-127">Developing a .NET app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [<span data-ttu-id="fefb6-128">Desarrollo de una aplicación .NET Core con SQL API de Azure Cosmos DB (versión preliminar de la versión 3.x)</span><span class="sxs-lookup"><span data-stu-id="fefb6-128">Developing a .NET Core app using Azure Cosmos DB's SQL API (Version 3.x Preview)</span></span>](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

<span data-ttu-id="fefb6-129">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fefb6-129">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
