---
title: Bibliotecas de CDN de Azure para .NET
description: Referencia de las bibliotecas de CDN de Azure para .NET
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: cdn
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 4e5b56ca7e316f3a53d8c6d37fdd90c5d7130e1e
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065825"
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="9eaa9-104">Bibliotecas de CDN de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="9eaa9-104">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="9eaa9-105">Información general</span><span class="sxs-lookup"><span data-stu-id="9eaa9-105">Overview</span></span>

<span data-ttu-id="9eaa9-106">Content Delivery Network (CDN) de Azure almacena en caché contenido de web estático en ubicaciones colocadas estratégicamente para proporcionar el máximo rendimiento a la hora de proporcionar contenido a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9eaa9-106">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="9eaa9-107">CDN ofrece a los desarrolladores una solución global para entregar contenido de alto ancho de banda almacenando en caché el contenido en nodos físicos en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="9eaa9-107">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="9eaa9-108">Para aprender sobre CDN de Azure, consulte [Información general de Content Delivery Network (CDN) de Azure](https://docs.microsoft.com/azure/cdn/cdn-overview).</span><span class="sxs-lookup"><span data-stu-id="9eaa9-108">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="9eaa9-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="9eaa9-109">Management library</span></span>

<span data-ttu-id="9eaa9-110">Puede usar la biblioteca de CDN de Azure para .NET para automatizar la creación y administración de perfiles y puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="9eaa9-110">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="9eaa9-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9eaa9-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9eaa9-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9eaa9-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="9eaa9-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9eaa9-113">Example</span></span>

<span data-ttu-id="9eaa9-114">En este ejemplo se crea un nuevo perfil de CDN con un nuevo punto de conexión que apunta a `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="9eaa9-114">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9eaa9-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="9eaa9-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="9eaa9-116">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9eaa9-116">Samples</span></span>

* <span data-ttu-id="9eaa9-117">[Getting started with CDN - Manage CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn) (Introducción a CDN y administración de CDN en .NET)</span><span class="sxs-lookup"><span data-stu-id="9eaa9-117">[Getting started with CDN - Manage CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
