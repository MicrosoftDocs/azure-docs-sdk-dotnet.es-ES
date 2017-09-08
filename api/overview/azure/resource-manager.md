---
title: Bibliotecas de Azure Resource Manager para .NET
description: Referencias de las bibliotecas de Azure Resource Manager para .NET
keywords: Azure, .NET, SDK, API, Resource Manager
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 4dcfdb59e3cbe919053937a62602de6b602bbac1
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="febd1-104">Bibliotecas de Azure Resource Manager para .NET</span><span class="sxs-lookup"><span data-stu-id="febd1-104">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="febd1-105">Información general</span><span class="sxs-lookup"><span data-stu-id="febd1-105">Overview</span></span>

<span data-ttu-id="febd1-106">Azure Resource Manager permite trabajar con los recursos de la solución como un grupo.</span><span class="sxs-lookup"><span data-stu-id="febd1-106">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="febd1-107">Para más información sobre Resource Manager, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="febd1-107">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="febd1-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="febd1-108">Management library</span></span>

<span data-ttu-id="febd1-109">La biblioteca de Azure Resource Manager para .NET permite crear, actualizar, eliminar y enumerar los recursos y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="febd1-109">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="febd1-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="febd1-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="febd1-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="febd1-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="febd1-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="febd1-112">Example</span></span>

<span data-ttu-id="febd1-113">En este ejemplo se crea un grupo de recursos nuevo.</span><span class="sxs-lookup"><span data-stu-id="febd1-113">This example creates a new resource group.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="febd1-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="febd1-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="febd1-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="febd1-115">Samples</span></span>

* [<span data-ttu-id="febd1-116">Administración de grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="febd1-116">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="febd1-117">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="febd1-117">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="febd1-118">Implementación de recursos con plantillas de ARM</span><span class="sxs-lookup"><span data-stu-id="febd1-118">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="febd1-119">Implementación de recursos con plantillas de ARM (con progreso)</span><span class="sxs-lookup"><span data-stu-id="febd1-119">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
