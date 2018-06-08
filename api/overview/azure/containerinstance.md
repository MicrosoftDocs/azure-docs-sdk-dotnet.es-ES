---
title: Bibliotecas de Azure Container Instances para .NET
description: Referencia de las bibliotecas de Azure Container Instances para .NET
keywords: Azure, .NET, SDK, API, Container Instances, ACI
author: mmacy
ms.author: marsma
manager: jeconnoc
ms.date: 05/25/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: dcontainer-instances
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 033f67a989b0ed6cfcb67a6212c0d5c46c485afa
ms.sourcegitcommit: 4ae9f77a9300a4fe54d0179055ae61191078f207
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2018
ms.locfileid: "34567191"
---
# <a name="azure-container-instances-libraries-for-net"></a>Bibliotecas de Azure Container Instances para .NET

Use las bibliotecas de Microsoft Azure Container Instances para .NET para crear y administrar instancias de contenedor de Azure. Para más información, consulte la [Introducción a Azure Container Instances](/azure/container-instances/container-instances-overview).

## <a name="management-library"></a>Biblioteca de administración

Use la biblioteca de administración para crear y administrar instancias de contenedor en Azure.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a>Ejemplos

### <a name="create-container-group---single-container"></a>Creación de un grupo de contenedores: un solo contenedor

En este ejemplo se crea un grupo de contenedores con un solo contenedor.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a>Creación de un grupo de contenedores: varios contenedores

En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a>Creación asincrónica de un contenedor con sondeo

En este ejemplo se crea un grupo de contenedores con un solo contenedor con el método de creación asincrónica. Después, sondea el grupo de contenedores en Azure y proporciona el estado del grupo de contenedores hasta que el estado es "En ejecución".

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a>Creación de un grupo de contenedores basado en tareas

En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas. El contenedor se configura con una [directiva de reinicio](/azure/container-instances/container-instances-restart-policy) "Never" y una [línea de comandos personalizada](/azure/container-instances/container-instances-restart-policy#command-line-override).

Si desea ejecutar un único comando con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una matriz de cadenas al método `WithStartingCommandLines`. Por ejemplo: 

`WithStartingCommandLines("echo", "FOO", "BAR")`

En cambio, si desea ejecutar varios comandos con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento. Por ejemplo, esto ejecuta los comandos `echo` y `tail`:

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a>Enumeración de grupos de contenedores

En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a>Obtención de un grupo de contenedores existente

En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades y sus valores.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a>Eliminación de grupo de contenedores

En este ejemplo se elimina un grupo de contenedores de un grupo de recursos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a>Referencia de API

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a>Ejemplos

* El código fuente de los ejemplos anteriores se encuentra en GitHub:

  [Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]

* Más ejemplos de código de Azure Container Instances:

  [Ejemplos de código de Azure][samples]

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
