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
# <a name="azure-cosmosdb-libraries-for-net"></a>Bibliotecas de Azure CosmosDB para .NET

## <a name="overview"></a>Información general

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un almacén de datos distribuidos y escalables, compatibles con varios tipos diferentes de las bases de datos.

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente CosmosDB .NET para acceder y almacenar datos en un almacén de datos CosmosDB.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.DocumentDB.Core
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.DocumentDB.Core
```

### <a name="code-example"></a>Ejemplo de código

Este ejemplo se conecta a una base de datos existente de API de CosmosDB DocumentDB, lee un documento de una colección y lo deserializa como un objeto `Item`.

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Muestras

* [Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

Consulte la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
