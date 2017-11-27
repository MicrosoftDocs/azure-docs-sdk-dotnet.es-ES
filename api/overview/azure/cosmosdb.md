---
title: Bibliotecas de Azure CosmosDB para .NET
description: Referencia de las bibliotecas de Azure CosmosDB para .NET
keywords: Azure, .NET, SDK, API, CosmosDB
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 11/17/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cosmos-db
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 9f29e53e7f202e48ade12e28f08487bbacd2833c
ms.sourcegitcommit: 9cc5f8da9e9a15ba07fd67fe8b9a2d4ee6b57c73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="azure-cosmosdb-libraries-for-net"></a>Bibliotecas de Azure CosmosDB para .NET

## <a name="overview"></a>Información general

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction) es un almacén de datos distribuidos y escalables, compatibles con varios tipos diferentes de las bases de datos.

[Introducción a CosmosDB](https://docs.microsoft.com/azure/cosmos-db/create-documentdb-dotnet).

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente de CosmosDB para .NET para y almacenar datos y acceder a ellos en un almacén de datos de CosmosDB.  Para automatizar la creación de una nueva cuenta de CosmosDB, use Azure Portal, la CLI o PowerShell.

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
SomeClass myObject = client.ReadDocumentAsync<SomeClass>(documentUri).ToString()).Result;
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/cosmosdb/client)

## <a name="samples"></a>Muestras

* [Desarrollo de una aplicación .NET con la API de MongoDB de Azure Cosmos DB](https://azure.microsoft.com/en-us/resources/samples/azure-cosmos-db-mongodb-dotnet-getting-started/)

Consulte la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=cosmosdb) de ejemplos de Azure Cosmos DB.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
