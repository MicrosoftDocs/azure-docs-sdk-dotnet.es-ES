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
ms.locfileid: "23566346"
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="6cbb8-104">Bibliotecas de Azure Redis Cache para .NET</span><span class="sxs-lookup"><span data-stu-id="6cbb8-104">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6cbb8-105">Información general</span><span class="sxs-lookup"><span data-stu-id="6cbb8-105">Overview</span></span>

<span data-ttu-id="6cbb8-106">Azure Redis Cache es un agente de mensajería y memoria caché de datos segura que proporciona a las aplicaciones un acceso de alto rendimiento y baja latencia a los datos.</span><span class="sxs-lookup"><span data-stu-id="6cbb8-106">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="6cbb8-107">Para más información, consulte [Cómo usar Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="6cbb8-107">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="6cbb8-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="6cbb8-108">Client library</span></span>

<span data-ttu-id="6cbb8-109">Azure Redis Cache es compatible con cualquier API de cliente de Redis, incluida `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="6cbb8-109">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="6cbb8-110">Instale el [paquete NuGet](https://www.nuget.org/packages/StackExchange.Redis) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6cbb8-110">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6cbb8-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cbb8-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="6cbb8-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6cbb8-112">Example</span></span>

<span data-ttu-id="6cbb8-113">En este ejemplo se conecta a una instancia de base de datos de Redis Cache, agrega algunas cadenas a la memoria caché por nombre y las recupera de nuevo.</span><span class="sxs-lookup"><span data-stu-id="6cbb8-113">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="6cbb8-114">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="6cbb8-114">Management library</span></span>

<span data-ttu-id="6cbb8-115">La biblioteca de administración de Redis Cache permite administrar los recursos de Redis Cache y las claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="6cbb8-115">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="6cbb8-116">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6cbb8-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6cbb8-117">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6cbb8-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="6cbb8-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6cbb8-118">Example</span></span>

<span data-ttu-id="6cbb8-119">En este ejemplo se crea una nueva instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="6cbb8-119">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="6cbb8-120">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="6cbb8-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="6cbb8-121">Muestras</span><span class="sxs-lookup"><span data-stu-id="6cbb8-121">Samples</span></span>

* [<span data-ttu-id="6cbb8-122">Introducción a Redis: administrar Redis, en .NET</span><span class="sxs-lookup"><span data-stu-id="6cbb8-122">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
