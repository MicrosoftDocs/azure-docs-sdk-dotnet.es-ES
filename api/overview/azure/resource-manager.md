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
# <a name="azure-resource-manager-libraries-for-net"></a>Bibliotecas de Azure Resource Manager para .NET

## <a name="overview"></a>Información general

Azure Resource Manager permite trabajar con los recursos de la solución como un grupo.  Para más información sobre Resource Manager, consulte [Información general de Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).

## <a name="management-library"></a>Biblioteca de administración

La biblioteca de Azure Resource Manager para .NET permite crear, actualizar, eliminar y enumerar los recursos y grupos de recursos.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ResourceManager.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

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
using Microsoft.Azure.Management.ResourceManager.Fluent
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IResourceGroup resourceGroup = azure.ResourceGroups
    .Define("ResourceGroupName")
    .WithRegion(Region.USWest)
    .Create();
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/resources/management)


## <a name="samples"></a>Muestras

* [Administración de grupos de recursos](https://github.com/Azure-Samples/resources-dotnet-manage-resource-group)
* [Administración de recursos](https://github.com/Azure-Samples/resources-dotnet-manage-resource)
* [Implementación de recursos con plantillas de ARM](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template)
* [Implementación de recursos con plantillas de ARM (con progreso)](https://github.com/Azure-Samples/resources-dotnet-deploy-using-arm-template-with-progress)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
