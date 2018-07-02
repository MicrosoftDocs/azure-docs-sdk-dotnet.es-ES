---
title: Bibliotecas de Azure Cosmos DB para .NET
description: Referencia de las bibliotecas de Azure Cosmos DB para .NET
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4407e59cbcc7ceedc0c7964981d29d6e14a4aa95
ms.sourcegitcommit: 903457bd531e77797a86e6aedcfc94c1fb79fe6d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/29/2018
ms.locfileid: "37132056"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="a60aa-104">Bibliotecas de Azure Cosmos DB para .NET</span><span class="sxs-lookup"><span data-stu-id="a60aa-104">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a60aa-105">Información general</span><span class="sxs-lookup"><span data-stu-id="a60aa-105">Overview</span></span>

<span data-ttu-id="a60aa-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un almacén de datos distribuido y escalable, que admite diversos tipos de bases de datos.</span><span class="sxs-lookup"><span data-stu-id="a60aa-106">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a distributed and scalable data store, supporting multiple different types of databases.</span></span>

<span data-ttu-id="a60aa-107">[Introducción a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a60aa-107">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="a60aa-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a60aa-108">Client library</span></span>

<span data-ttu-id="a60aa-109">Utilice la biblioteca de cliente de Azure Cosmos DB para .NET para almacenar los datos y acceder a ellos en un almacén de datos de Azure Cosmos DB existente.</span><span class="sxs-lookup"><span data-stu-id="a60aa-109">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span>  <span data-ttu-id="a60aa-110">Para automatizar la creación de una nueva cuenta de Azure Cosmos DB, use Azure Portal, la CLI o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a60aa-110">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="a60aa-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a60aa-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a60aa-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a60aa-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="a60aa-113">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="a60aa-113">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="a60aa-114">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="a60aa-114">Code Example</span></span>

<span data-ttu-id="a60aa-115">Este ejemplo se conecta a una base de datos existente SQL API de Azure Cosmos DB, lee un documento de una colección y lo deserializa como un objeto `Item`.</span><span class="sxs-lookup"><span data-stu-id="a60aa-115">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString().Result;
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a60aa-116">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="a60aa-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="a60aa-117">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a60aa-117">Samples</span></span>

* [<span data-ttu-id="a60aa-118">Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a60aa-118">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="a60aa-119">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a60aa-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
