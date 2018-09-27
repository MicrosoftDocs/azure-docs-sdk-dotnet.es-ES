---
title: Bibliotecas de Azure Resource Manager para .NET
description: Referencias de las bibliotecas de Azure Resource Manager para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 6d3a27c5f7ba94f5579723cc4f798826c8bdefd6
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190849"
---
# <a name="azure-resource-manager-libraries-for-net"></a><span data-ttu-id="6960b-103">Bibliotecas de Azure Resource Manager para .NET</span><span class="sxs-lookup"><span data-stu-id="6960b-103">Azure Resource Manager libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6960b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="6960b-104">Overview</span></span>

<span data-ttu-id="6960b-105">Azure Resource Manager permite trabajar con los recursos de la solución como un grupo.</span><span class="sxs-lookup"><span data-stu-id="6960b-105">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span>  <span data-ttu-id="6960b-106">Para más información sobre Resource Manager, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="6960b-106">For more information about Resource Manager, see [Azure Resource Manager overview](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="6960b-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="6960b-107">Management library</span></span>

<span data-ttu-id="6960b-108">La biblioteca de Azure Resource Manager para .NET permite crear, actualizar, eliminar y enumerar los recursos y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="6960b-108">The Azure Resource Manager library for .NET enables you to create, update, delete, and list resources and resource groups.</span></span>

<span data-ttu-id="6960b-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6960b-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6960b-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6960b-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a><span data-ttu-id="6960b-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="6960b-111">Example</span></span>

<span data-ttu-id="6960b-112">En este ejemplo se crea un grupo de recursos nuevo.</span><span class="sxs-lookup"><span data-stu-id="6960b-112">This example creates a new resource group.</span></span>

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="6960b-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="6960b-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a><span data-ttu-id="6960b-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="6960b-114">Samples</span></span>

* [<span data-ttu-id="6960b-115">Administración de grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="6960b-115">Manage resource groups</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [<span data-ttu-id="6960b-116">Administración de recursos</span><span class="sxs-lookup"><span data-stu-id="6960b-116">Manage resources</span></span>](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [<span data-ttu-id="6960b-117">Implementación de recursos con plantillas de ARM</span><span class="sxs-lookup"><span data-stu-id="6960b-117">Deploy resources with ARM templates</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [<span data-ttu-id="6960b-118">Implementación de recursos con plantillas de ARM (con progreso)</span><span class="sxs-lookup"><span data-stu-id="6960b-118">Deploy resources with ARM templates (with progress)</span></span>](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
