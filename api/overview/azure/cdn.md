---
title: Bibliotecas de Azure CDN para .NET
description: Referencia de las bibliotecas de Azure CDN para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: azure-cdn
ms.openlocfilehash: b06b886531510d442c415fdc483d8083b6622c8e
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348067"
---
# <a name="azure-cdn-libraries-for-net"></a><span data-ttu-id="90888-103">Bibliotecas de Azure CDN para .NET</span><span class="sxs-lookup"><span data-stu-id="90888-103">Azure CDN libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="90888-104">Información general</span><span class="sxs-lookup"><span data-stu-id="90888-104">Overview</span></span>

<span data-ttu-id="90888-105">Content Delivery Network (CDN) de Azure almacena en caché contenido de web estático en ubicaciones colocadas estratégicamente para proporcionar el máximo rendimiento a la hora de proporcionar contenido a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="90888-105">The Azure Content Delivery Network (CDN) caches static web content at strategically placed locations to provide maximum throughput for delivering content to users.</span></span> <span data-ttu-id="90888-106">CDN ofrece a los desarrolladores una solución global para entregar contenido de alto ancho de banda almacenando en caché el contenido en nodos físicos en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="90888-106">The CDN offers developers a global solution for delivering high-bandwidth content by caching the content at physical nodes across the world.</span></span>

<span data-ttu-id="90888-107">Para aprender sobre Azure CDN, consulte [Información general de Content Delivery Network (CDN) de Azure](https://docs.microsoft.com/azure/cdn/cdn-overview).</span><span class="sxs-lookup"><span data-stu-id="90888-107">To learn more about Azure CDN, see [Overview of the Azure Content Delivery Network](https://docs.microsoft.com/azure/cdn/cdn-overview).</span></span>


## <a name="management-library"></a><span data-ttu-id="90888-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="90888-108">Management library</span></span>

<span data-ttu-id="90888-109">Puede usar la biblioteca de Azure CDN para .NET para automatizar la creación y administración de perfiles y puntos de conexión de CDN.</span><span class="sxs-lookup"><span data-stu-id="90888-109">You can use the Azure CDN Library for .NET to automate creation and management of CDN profiles and endpoints.</span></span> 

<span data-ttu-id="90888-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="90888-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="90888-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90888-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a><span data-ttu-id="90888-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90888-112">Example</span></span>

<span data-ttu-id="90888-113">En este ejemplo se crea un nuevo perfil de CDN con un nuevo punto de conexión que apunta a `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="90888-113">This example creates a new CDN profile with a new endpoint pointed to `www.contoso.com`.</span></span>

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
> [<span data-ttu-id="90888-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="90888-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a><span data-ttu-id="90888-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="90888-115">Samples</span></span>

* <span data-ttu-id="90888-116">[Getting started with CDN - Manage CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn) (Introducción a CDN y administración de CDN en .NET)</span><span class="sxs-lookup"><span data-stu-id="90888-116">[Getting started with CDN - Manage CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn)</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
