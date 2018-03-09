---
title: API de almacenamiento de .NET de Azure
description: Referencia de las bibliotecas de Azure Storage para .NET
keywords: Azure, .NET, SDK, API, Storage, blob
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: storage
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8f6e0414b54698d0a1dbe3d4c074456a6ad7b7be
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="azure-storage-apis-for-net"></a>API de Azure Storage para .NET

## <a name="overview"></a>Información general

Lea y escriba archivos, datos de blob (objeto), pares de clave-valor y mensajes desde las aplicaciones .NET con [Azure Storage](https://review.docs.microsoft.com/azure/storage/storage-introduction).

Para comenzar a usar Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](/azure/storage/storage-dotnet-how-to-use-blobs).

## <a name="client-library"></a>Biblioteca de cliente

Use [cadenas de conexión](/azure/storage/storage-create-storage-account#manage-your-storage-account) para conectarse a una cuenta de Azure Storage y, a continuación, use las clases y los métodos de las bibliotecas de cliente para trabajar con almacenamiento de blobs, tablas, archivos o colas.

Instale el [paquete NuGet](https://www.nuget.org/packages/WindowsAzure.Storage) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package WindowsAzure.Storage
```

### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package WindowsAzure.Storage
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea un nuevo blob para un nuevo contenedor de una cuenta de almacenamiento existente.

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/storage/client)

## <a name="management-apis"></a>API de administración

Cree y administre cuentas y claves de conexión de Azure Storage con la API de administración.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Storage.Fluent
```

#### <a name="net-core-cli"></a>CLI de .NET Core

````bash
dotnet add package Microsoft.Azure.Management.Storage.Fluent
````

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea una cuenta de almacenamiento.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/storage/management)

## <a name="samples"></a>Ejemplos

* [Introducción a Azure Blob Storage en .NET](https://azure.microsoft.com/resources/samples/storage-blob-dotnet-getting-started/) 
* [Introducción a Azure Queue Storage en .NET](https://azure.microsoft.com/resources/samples/storage-queue-dotnet-getting-started/)

Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=storage) de ejemplos de Azure Storage.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package