---
title: Bibliotecas de Azure Cosmos DB para .NET
description: Referencia de las bibliotecas de Azure Cosmos DB para .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 21a2f2168259528a0d27103783e34aa532d7e17a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190807"
---
# <a name="azure-cosmos-db-libraries-for-net"></a><span data-ttu-id="a7502-103">Bibliotecas de Azure Cosmos DB para .NET</span><span class="sxs-lookup"><span data-stu-id="a7502-103">Azure Cosmos DB libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a7502-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a7502-104">Overview</span></span>

<span data-ttu-id="a7502-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un servicio de base de datos multimodelo distribuido globalmente.</span><span class="sxs-lookup"><span data-stu-id="a7502-105">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) is a globally distributed, multi-model database service.</span></span> <span data-ttu-id="a7502-106">Está diseñado para permitir que los clientes escalen de manera elástica e independiente el rendimiento y el almacenamiento en cualquier número de regiones geográficas con un completo SLA.</span><span class="sxs-lookup"><span data-stu-id="a7502-106">It is designed to elastically and independently scale throughput and storage across any number of geographical regions with a comprehensive SLA.</span></span> <span data-ttu-id="a7502-107">Con Azure Cosmos DB, puede almacenar y tener acceso a bases de datos de documentos, de pares clave-valor, columnares y de grafos mediante API y modelos de programación.</span><span class="sxs-lookup"><span data-stu-id="a7502-107">With Azure Cosmos DB, you can store and access document, key-value, wide-column, and graph databases by using APIs and programming models.</span></span> 

<span data-ttu-id="a7502-108">[Introducción a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span><span class="sxs-lookup"><span data-stu-id="a7502-108">[Get started with Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="a7502-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a7502-109">Client library</span></span>

<span data-ttu-id="a7502-110">Utilice la biblioteca de cliente de Azure Cosmos DB para .NET para almacenar los datos y acceder a ellos en un almacén de datos de Azure Cosmos DB existente.</span><span class="sxs-lookup"><span data-stu-id="a7502-110">Use the Azure Cosmos DB .NET client library to access and store data in an existing Azure Cosmos DB data store.</span></span> <span data-ttu-id="a7502-111">Para automatizar la creación de una nueva cuenta de Azure Cosmos DB, use Azure Portal, la CLI o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a7502-111">To automate creation of a new Azure Cosmos DB account, use the Azure portal, CLI, or PowerShell.</span></span>

<span data-ttu-id="a7502-112">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a7502-112">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a7502-113">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7502-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a><span data-ttu-id="a7502-114">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="a7502-114">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a><span data-ttu-id="a7502-115">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="a7502-115">Code Example</span></span>

<span data-ttu-id="a7502-116">Este ejemplo se conecta a una base de datos existente SQL API de Azure Cosmos DB, lee un documento de una colección y lo deserializa como un objeto `Item`.</span><span class="sxs-lookup"><span data-stu-id="a7502-116">This example connects to an existing Azure Cosmos DB SQL API database, reads a document from a collection, and deserializes it as an `Item` object.</span></span>   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a7502-117">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="a7502-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a><span data-ttu-id="a7502-118">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a7502-118">Samples</span></span>

* [<span data-ttu-id="a7502-119">Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a7502-119">Developing a .NET app using Azure Cosmos DB's MongoDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

<span data-ttu-id="a7502-120">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a7502-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) of Azure Cosmos DB samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
