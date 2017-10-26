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
---
# <a name="azure-search-libraries-for-net"></a>Bibliotecas de Azure Search para .NET

## <a name="overview"></a>Información general

[Azure Search](https://docs.microsoft.com/azure/search/search-what-is-azure-search) es un servicio de búsqueda en la nube totalmente administrado que proporciona una experiencia de búsqueda enriquecida en los datos de aplicaciones web, móviles y empresariales.

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente de Azure Search para acceder y ejecutar las operaciones de indexación y de búsqueda en un servicio de búsqueda, índice, documentos u otro objeto. Para una introducción paso a paso, consulte [Cómo usar Azure Search desde una aplicación .NET](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Search) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Search
```

```bash
dotnet add package Microsoft.Azure.Search
```

### <a name="code-example"></a>Ejemplo de código

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/search/client)


## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración de Azure Search para aprovisionar un servicio, administrar las claves de API y ajustar los recursos. La administración de servicio tiene una dependencia en Azure Resource Manager para la identificación del suscriptor y del inquilino. Normalmente, el registro de autenticación y de aplicación con Azure Active Directory también es necesario para admitir el flujo de trabajo. Para obtener una introducción al aprovisionamiento del servicio Azure Search, consulte [How to use the Management REST API](https://docs.microsoft.com/rest/api/searchmanagement/search-howto-management-rest-api) (Uso de la API de REST de administración).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Search) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Search
```

```bash
dotnet add package Microsoft.Azure.Management.Search
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/search/management)

## <a name="samples"></a>Muestras

 + [Ejemplos de Azure/ search-dotnet--getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started)
 + [Ejemplos de Azure/ search-dotnet-management-api](https://github.com/Azure-Samples/search-dotnet-management-api)

Busque más ejemplos de búsqueda en el [repositorio de ejemplos de Azure](https://github.com/Azure-Samples/) en Github.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
