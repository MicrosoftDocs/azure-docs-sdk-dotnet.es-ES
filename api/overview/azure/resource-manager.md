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
# <a name="azure-resource-manager-libraries-for-net"></a>Bibliotecas de Azure Resource Manager para .NET

## <a name="overview"></a>Información general

Azure Resource Manager permite trabajar con los recursos de la solución como un grupo.  Para más información sobre Resource Manager, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-library"></a>Biblioteca de administración

La biblioteca de Azure Resource Manager para .NET permite crear, actualizar, eliminar y enumerar los recursos y grupos de recursos.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="example"></a>Ejemplo

En este ejemplo se crea un grupo de recursos nuevo.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a>Ejemplos

* [Administración de grupos de recursos](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [Administración de recursos](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [Implementación de recursos con plantillas de ARM](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [Implementación de recursos con plantillas de ARM (con progreso)](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
