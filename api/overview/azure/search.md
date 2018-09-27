---
title: Bibliotecas de Azure Search para .NET
description: Referencia de las bibliotecas de Azure Search para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: search
ms.openlocfilehash: cf622ccb59f10a5270c02fa76d7396345fbb1a9b
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190248"
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="cca66-103">Bibliotecas de Azure Search para .NET</span><span class="sxs-lookup"><span data-stu-id="cca66-103">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="cca66-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cca66-104">Overview</span></span>

<span data-ttu-id="cca66-105">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) es un servicio de búsqueda en la nube totalmente administrado que proporciona una experiencia de búsqueda enriquecida en los datos de aplicaciones web, móviles y empresariales.</span><span class="sxs-lookup"><span data-stu-id="cca66-105">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="cca66-106">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="cca66-106">Client library</span></span>

<span data-ttu-id="cca66-107">Utilice la biblioteca de cliente de Azure Search para acceder y ejecutar las operaciones de indexación y de búsqueda en un servicio de búsqueda, índice, documentos u otro objeto.</span><span class="sxs-lookup"><span data-stu-id="cca66-107">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="cca66-108">Para una introducción paso a paso, consulte [Cómo usar Azure Search desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="cca66-108">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="cca66-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="cca66-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="cca66-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cca66-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="cca66-111">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="cca66-111">Code Example</span></span>

```csharp
/* Include these 'using' directives:
   using Microsoft.Azure.Search;
   using Microsoft.Azure.Search.Models;
*/

// A service endpoint and an api-key are required on a connection.
// Set them in a config file (not shown) and then connect to the client.
IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
IConfigurationRoot configuration = builder.Build();

SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

// Create an index named hotels
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cca66-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="cca66-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="cca66-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="cca66-113">Management library</span></span>

<span data-ttu-id="cca66-114">Utilice la biblioteca de administración de Azure Search para aprovisionar un servicio, administrar las claves de API y ajustar los recursos.</span><span class="sxs-lookup"><span data-stu-id="cca66-114">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="cca66-115">La administración de servicio tiene una dependencia en Azure Resource Manager para la identificación del suscriptor y del inquilino.</span><span class="sxs-lookup"><span data-stu-id="cca66-115">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="cca66-116">Normalmente, el registro de autenticación y de aplicación con Azure Active Directory también es necesario para admitir el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="cca66-116">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="cca66-117">Para obtener una introducción al aprovisionamiento del servicio Azure Search, consulte [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Uso de la API de REST de administración).</span><span class="sxs-lookup"><span data-stu-id="cca66-117">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="cca66-118">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="cca66-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="cca66-119">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cca66-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="cca66-120">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="cca66-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="cca66-121">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="cca66-121">Samples</span></span>

 + [<span data-ttu-id="cca66-122">Ejemplos de Azure/ search-dotnet--getting-started</span><span class="sxs-lookup"><span data-stu-id="cca66-122">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="cca66-123">Ejemplos de Azure/ search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="cca66-123">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="cca66-124">Busque más ejemplos de búsqueda en el [repositorio de ejemplos de Azure](https://github.com/Azure-Samples/) en Github.</span><span class="sxs-lookup"><span data-stu-id="cca66-124">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
