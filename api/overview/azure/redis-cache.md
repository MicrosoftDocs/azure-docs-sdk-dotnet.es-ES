---
title: Bibliotecas de Azure Redis Cache para .NET
description: Referencia de las bibliotecas de Azure Redis Cache para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: redis-cache
ms.openlocfilehash: cc043bbc6ea5915f7b6c2265b606210efb72d9d0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190528"
---
# <a name="azure-redis-cache-libraries-for-net"></a><span data-ttu-id="381a9-103">Bibliotecas de Azure Redis Cache para .NET</span><span class="sxs-lookup"><span data-stu-id="381a9-103">Azure Redis Cache libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="381a9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="381a9-104">Overview</span></span>

<span data-ttu-id="381a9-105">Azure Redis Cache es un agente de mensajería y memoria caché de datos segura que proporciona a las aplicaciones un acceso de alto rendimiento y baja latencia a los datos.</span><span class="sxs-lookup"><span data-stu-id="381a9-105">Azure Redis Cache is a secure data cache and messaging broker that provides high throughput and low-latency access to data for applications.</span></span>  <span data-ttu-id="381a9-106">Para más información, consulte [Cómo usar Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span><span class="sxs-lookup"><span data-stu-id="381a9-106">For more information, see [How to Use Redis Cache](https://docs.microsoft.com/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache).</span></span>

## <a name="client-library"></a><span data-ttu-id="381a9-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="381a9-107">Client library</span></span>

<span data-ttu-id="381a9-108">Azure Redis Cache es compatible con cualquier API de cliente de Redis, incluida `StackExchange.Redis`.</span><span class="sxs-lookup"><span data-stu-id="381a9-108">Azure Redis Cache is compatible with any Redis client API, including `StackExchange.Redis`.</span></span>

<span data-ttu-id="381a9-109">Instale el [paquete NuGet](https://www.nuget.org/packages/StackExchange.Redis) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="381a9-109">Install the [NuGet package](https://www.nuget.org/packages/StackExchange.Redis) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="381a9-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381a9-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package StackExchange.Redis
```

```bash
dotnet add package StackExchange.Redis
```

### <a name="example"></a><span data-ttu-id="381a9-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a9-111">Example</span></span>

<span data-ttu-id="381a9-112">En este ejemplo se conecta a una instancia de base de datos de Redis Cache, agrega algunas cadenas a la memoria caché por nombre y las recupera de nuevo.</span><span class="sxs-lookup"><span data-stu-id="381a9-112">This example connects to a Redis Cache database instance, adds some strings to the cache by name, and then retrieves them again.</span></span>

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

## <a name="management-library"></a><span data-ttu-id="381a9-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="381a9-113">Management library</span></span>

<span data-ttu-id="381a9-114">La biblioteca de administración de Redis Cache permite administrar los recursos de Redis Cache y las claves de acceso.</span><span class="sxs-lookup"><span data-stu-id="381a9-114">The Redis Cache management library allows you to manage Redis Cache resources and access keys.</span></span>

<span data-ttu-id="381a9-115">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="381a9-115">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Redis.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="381a9-116">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="381a9-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Redis.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Redis.Fluent
```

### <a name="example"></a><span data-ttu-id="381a9-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="381a9-117">Example</span></span>

<span data-ttu-id="381a9-118">En este ejemplo se crea una nueva instancia de Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="381a9-118">This example creates a new Redis Cache.</span></span>

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
> [<span data-ttu-id="381a9-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="381a9-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/rediscache/management)


## <a name="samples"></a><span data-ttu-id="381a9-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="381a9-120">Samples</span></span>

* [<span data-ttu-id="381a9-121">Introducción a Redis: administrar Redis, en .NET</span><span class="sxs-lookup"><span data-stu-id="381a9-121">Getting Started with Redis - Manage Redis - in .NET</span></span>](https://github.com/Azure-Samples/redis-cache-dotnet-manage-cache)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
