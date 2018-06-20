---
title: Bibliotecas de Azure Search para .NET
description: Referencia de las bibliotecas de Azure Search para .NET
keywords: Azure, .NET, SDK, API, Search
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: search
ms.custom: devcenter, svc-overview
ms.openlocfilehash: bd0899d6dbc6d474389eebac78a77a62b86c5255
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566306"
---
# <a name="azure-search-libraries-for-net"></a><span data-ttu-id="5b35b-104">Bibliotecas de Azure Search para .NET</span><span class="sxs-lookup"><span data-stu-id="5b35b-104">Azure Search libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="5b35b-105">Información general</span><span class="sxs-lookup"><span data-stu-id="5b35b-105">Overview</span></span>

<span data-ttu-id="5b35b-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) es un servicio de búsqueda en la nube totalmente administrado que proporciona una experiencia de búsqueda enriquecida en los datos de aplicaciones web, móviles y empresariales.</span><span class="sxs-lookup"><span data-stu-id="5b35b-106">[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) is a fully managed cloud search service that provides a rich search experience over data in web, mobile, and enterprise applications.</span></span>

## <a name="client-library"></a><span data-ttu-id="5b35b-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="5b35b-107">Client library</span></span>

<span data-ttu-id="5b35b-108">Utilice la biblioteca de cliente de Azure Search para acceder y ejecutar las operaciones de indexación y de búsqueda en un servicio de búsqueda, índice, documentos u otro objeto.</span><span class="sxs-lookup"><span data-stu-id="5b35b-108">Use the Azure Search client library to access and execute indexing and search operations on a search service, index, documents, or other object.</span></span> <span data-ttu-id="5b35b-109">Para una introducción paso a paso, consulte [Cómo usar Azure Search desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="5b35b-109">For a step-by-step introduction, see [How to use Azure Search from a .NET application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

<span data-ttu-id="5b35b-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5b35b-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5b35b-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b35b-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a><span data-ttu-id="5b35b-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="5b35b-112">Code Example</span></span>

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
> [<span data-ttu-id="5b35b-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="5b35b-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a><span data-ttu-id="5b35b-114">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="5b35b-114">Management library</span></span>

<span data-ttu-id="5b35b-115">Utilice la biblioteca de administración de Azure Search para aprovisionar un servicio, administrar las claves de API y ajustar los recursos.</span><span class="sxs-lookup"><span data-stu-id="5b35b-115">Use the Azure Search management library to provision a service, manage api-keys, and adjust resources.</span></span> <span data-ttu-id="5b35b-116">La administración de servicio tiene una dependencia en Azure Resource Manager para la identificación del suscriptor y del inquilino.</span><span class="sxs-lookup"><span data-stu-id="5b35b-116">Service management has a dependency on Azure Resource Manager for subscriber and tenant identification.</span></span> <span data-ttu-id="5b35b-117">Normalmente, el registro de autenticación y de aplicación con Azure Active Directory también es necesario para admitir el flujo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="5b35b-117">Typically, authentication and application registration with Azure Active Directory is also necessary to support the workflow.</span></span> <span data-ttu-id="5b35b-118">Para obtener una introducción al aprovisionamiento del servicio Azure Search, consulte [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Uso de la API de REST de administración).</span><span class="sxs-lookup"><span data-stu-id="5b35b-118">For an introduction to Azure Search service provisioning, see [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api).</span></span>

<span data-ttu-id="5b35b-119">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="5b35b-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5b35b-120">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b35b-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5b35b-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="5b35b-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a><span data-ttu-id="5b35b-122">Muestras</span><span class="sxs-lookup"><span data-stu-id="5b35b-122">Samples</span></span>

 + [<span data-ttu-id="5b35b-123">Ejemplos de Azure/ search-dotnet--getting-started</span><span class="sxs-lookup"><span data-stu-id="5b35b-123">Azure Samples / search-dotnet-getting-started</span></span>](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [<span data-ttu-id="5b35b-124">Ejemplos de Azure/ search-dotnet-management-api</span><span class="sxs-lookup"><span data-stu-id="5b35b-124">Azure Samples / search-dotnet-management-api</span></span>](https://github.com/Azure-Samples/search-dotnet-management-api)

<span data-ttu-id="5b35b-125">Busque más ejemplos de búsqueda en el [repositorio de ejemplos de Azure](https://github.com/Azure-Samples/) en Github.</span><span class="sxs-lookup"><span data-stu-id="5b35b-125">Find more search samples in the [Azure samples repository](https://github.com/Azure-Samples/) on Github.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
