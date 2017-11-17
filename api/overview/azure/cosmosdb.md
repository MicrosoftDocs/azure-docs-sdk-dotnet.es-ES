---
title: Bibliotecas de Azure CosmosDB para .NET
description: Referencia de las bibliotecas de Azure CosmosDB para .NET
keywords: Azure, .NET, SDK, API, CosmosDB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 890c00caeca06bf863425c7159d7833c4db8df38
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a><span data-ttu-id="1007f-104">Bibliotecas de Azure CosmosDB para .NET</span><span class="sxs-lookup"><span data-stu-id="1007f-104">Azure CosmosDB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1007f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1007f-105">Overview</span></span>

<span data-ttu-id="1007f-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un almacén de datos distribuidos y escalables, compatibles con varios tipos diferentes de las bases de datos.</span><span class="sxs-lookup"><span data-stu-id="1007f-106">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

## <a name="client-library"></a><span data-ttu-id="1007f-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="1007f-107">Client library</span></span>

<span data-ttu-id="1007f-108">Utilice la biblioteca de cliente CosmosDB .NET para acceder y almacenar datos en un almacén de datos CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="1007f-108">Use the CosmosDB .NET client library to access and store data in a CosmosDB data store.</span></span>

<span data-ttu-id="1007f-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="1007f-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1007f-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1007f-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="1007f-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="1007f-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="1007f-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="1007f-112">Code Example</span></span>

<span data-ttu-id="1007f-113">Este ejemplo se conecta a una base de datos existente de API de CosmosDB DocumentDB, lee un documento de una colección y lo deserializa como un objeto `Item`.</span><span class="sxs-lookup"><span data-stu-id="1007f-113">This example connects to an existing CosmosDB DocumentDB API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
// "Item" is a class defined elsewhere...
Item item = client.ReadDocumentAsync<Item>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="1007f-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="1007f-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="1007f-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="1007f-115">Samples</span></span>

* [<span data-ttu-id="1007f-116">Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1007f-116">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="1007f-117">Consulte la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1007f-117">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
