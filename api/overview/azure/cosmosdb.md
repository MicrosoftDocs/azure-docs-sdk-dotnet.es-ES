---
title: Bibliotecas de Azure Cosmos DB para .NET
description: Referencia de las bibliotecas de Azure Cosmos DB para .NET
keywords: Azure, .NET, SDK, API, Cosmos DB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/31/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4928c1dfdb7a5bb50ca4f5023cbfec71e05e9061
ms.sourcegitcommit: 299aa7bdbb9cec1b56e42e25550999e53e23de2c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43839501"
---
# <a name="azure-cosmos-db-libraries-for-net"></a>Bibliotecas de Azure Cosmos DB para .NET

## <a name="overview"></a>Información general

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un servicio de base de datos multimodelo distribuido globalmente. Está diseñado para permitir que los clientes escalen de manera elástica e independiente el rendimiento y el almacenamiento en cualquier número de regiones geográficas con un completo SLA. Con Azure Cosmos DB, puede almacenar y tener acceso a bases de datos de documentos, de pares clave-valor, columnares y de grafos mediante API y modelos de programación. 

[Introducción a Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-dotnet).

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente de Azure Cosmos DB para .NET para almacenar los datos y acceder a ellos en un almacén de datos de Azure Cosmos DB existente. Para automatizar la creación de una nueva cuenta de Azure Cosmos DB, use Azure Portal, la CLI o PowerShell.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>Ejemplo de código

Este ejemplo se conecta a una base de datos existente SQL API de Azure Cosmos DB, lee un documento de una colección y lo deserializa como un objeto `Item`.   

```csharp
/* Include this "using" directive...
using Microsoft.Azure.Documents.Client;
*/

DocumentClient client = new DocumentClient(endpointUri, authKeyString);
Uri documentUri = UriFactory.CreateDocumentUri("MyDatabaseName", "MyCollectionName", "DocumentId");
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString();
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Ejemplos

* [Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB](https://azure.microsoft.com/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
