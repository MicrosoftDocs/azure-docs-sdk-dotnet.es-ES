---
title: Bibliotecas de Azure Redis Cache para .NET
description: Referencia de las bibliotecas de Azure Redis Cache para .NET
keywords: Azure, .NET, SDK, API, Redis Cache
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: redis-cache
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 64bb5a43cec8c82412b3dc7b60fea1e8566ab399
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-redis-cache-libraries-for-net"></a>Bibliotecas de Azure Redis Cache para .NET

## <a name="overview"></a>Información general

Azure Redis Cache es un agente de mensajería y memoria caché de datos segura que proporciona a las aplicaciones un acceso de alto rendimiento y baja latencia a los datos.  Para más información, consulte [Cómo usar Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).

## <a name="client-library"></a>Biblioteca de cliente

Azure Redis Cache es compatible con cualquier API de cliente de Redis, incluida `StackExchange.Redis`.

Instale el [paquete NuGet](https://www.nuget.org/packages/StackExchange.Redis) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a>Ejemplo

En este ejemplo se conecta a una instancia de base de datos de Redis Cache, agrega algunas cadenas a la memoria caché por nombre y las recupera de nuevo.

```csharp
/* Include this "using" directive.
using StackExchange.Redis;
*/

ConnectionMultiplexer connection = 
    ConnectionMultiplexer.Connect("contoso.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    IDatabase cache = connection.GetDatabase();

// Perform cache operations using the cache object...
// Simple put of integral data types into the cache
cache.StringSet("key1", "value");
cache.StringSet("key2", 25);

// Simple get of data types from the cache
string key1 = cache.StringGet("key1");
int key2 = (int)cache.StringGet("key2");
```

## <a name="management-library"></a>Biblioteca de administración

La biblioteca de administración de Redis Cache permite administrar los recursos de Redis Cache y las claves de acceso.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a>Ejemplo

En este ejemplo se crea una nueva instancia de Redis Cache.

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.Azure.Management.Redis.Fluent;
*/

IRedisCache redisCache1 = azure.RedisCaches.Define("RedisCacheName")
    .WithRegion(Region.USCentral)
    .WithNewResourceGroup("ResourceGroupName")
    .WithBasicSku()
    .Create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a>Muestras

* [Introducción a Redis: administrar Redis, en .NET](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
