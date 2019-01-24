---
title: Bibliotecas de Azure Cosmos DB para .NET
description: Referencia de las bibliotecas de Azure Cosmos DB para .NET
ms.date: 08/31/2018
ms.topic: reference
ms.service: cosmos-db
ms.openlocfilehash: 95fcd8468c3d472cfcadeaae3b56ae789c3b1e7a
ms.sourcegitcommit: 55ee51501678d1575e5159f0ac0e475b5bf9daf3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2019
ms.locfileid: "54453999"
---
# <a name="azure-cosmos-db-libraries-for-net"></a>Bibliotecas de Azure Cosmos DB para .NET

## <a name="overview"></a>Información general

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un servicio de base de datos multimodelo distribuido globalmente. Está diseñado para permitir que los clientes escalen de manera elástica e independiente el rendimiento y el almacenamiento en cualquier número de regiones geográficas con un completo SLA. Con Azure Cosmos DB, puede almacenar y tener acceso a bases de datos de documentos, de pares clave-valor, columnares y de grafos mediante API y modelos de programación. 

[Introducción a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente de Azure Cosmos DB para .NET para almacenar los datos y acceder a ellos en un almacén de datos de Azure Cosmos DB existente. Para automatizar la creación de una nueva cuenta de Azure Cosmos DB, use Azure Portal, la CLI o PowerShell.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

Para instalar la versión 2.x:

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

Para instalar la versión preliminar de la versión 3.0, dirigida a .NET estándar: 

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Cosmos -prerelease
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.Cosmos
```


### <a name="code-example"></a>Ejemplo de código

Este ejemplo se conecta a una base de datos existente SQL API de Azure Cosmos DB, lee un documento de una colección y lo deserializa como un objeto `TodoItem`. En este ejemplo, se usa la versión 2.x del SDK para .NET.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
var todoItem = client.ReadDocumentAsync<TodoItem>(documentUri);
```

En este ejemplo, se conecta con una base de datos de SQL API de Azure Cosmos DB existente, se crea una nueva base de datos y un contenedor, se lee un elemento del contenedor y se deserializa en un objeto `TodoItem`. En este ejemplo, se usa la versión 3.x del SDK para .NET.   

```csharp
using (CosmosClient cosmosClient = new CosmosClient("endpoint", "primaryKey"))
{
    // Read item from container
    CosmosItemResponse<TodoItem> todoItemResponse = await cosmosClient.Databases["DatabaseId"].Containers["ContainerId"].Items.ReadItemAsync<TodoItem>("partitionKeyValue", "ItemId");
}
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Ejemplos

* [Desarrollo de una aplicación .NET con SQL API de Azure Cosmos DB (versión 2.x)](https://github.com/Azure-Samples/documentdb-dotnet-todo-app/)
* [Desarrollo de una aplicación .NET con SQL API de Azure Cosmos DB (versión preliminar de la versión 3.x)](https://github.com/Azure-Samples/cosmos-dotnet-todo-app/)
* [Desarrollo de una aplicación .NET Core con SQL API de Azure Cosmos DB (versión preliminar de la versión 3.x)](https://github.com/Azure-Samples/cosmos-dotnet-core-getting-started)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
