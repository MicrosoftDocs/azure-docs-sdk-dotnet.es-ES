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
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="a643c-104">Bibliotecas de Azure Container Instances para .NET</span><span class="sxs-lookup"><span data-stu-id="a643c-104">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="a643c-105">Use las bibliotecas de Microsoft Azure Container Instances para .NET para crear y administrar instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="a643c-105">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="a643c-106">Para más información, consulte la [Introducción a Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="a643c-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="a643c-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="a643c-107">Management library</span></span>

<span data-ttu-id="a643c-108">Use la biblioteca de administración para crear y administrar instancias de contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="a643c-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="a643c-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a643c-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="a643c-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a643c-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="examples"></a><span data-ttu-id="a643c-111">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a643c-111">Examples</span></span>

### <a name="create-container-group---single-container"></a><span data-ttu-id="a643c-112">Creación de un grupo de contenedores: un solo contenedor</span><span class="sxs-lookup"><span data-stu-id="a643c-112">Create container group - single container</span></span>

<span data-ttu-id="a643c-113">En este ejemplo se crea un grupo de contenedores con un solo contenedor.</span><span class="sxs-lookup"><span data-stu-id="a643c-113">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

### <a name="create-container-group---multiple-containers"></a><span data-ttu-id="a643c-114">Creación de un grupo de contenedores: varios contenedores</span><span class="sxs-lookup"><span data-stu-id="a643c-114">Create container group - multiple containers</span></span>

<span data-ttu-id="a643c-115">En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.</span><span class="sxs-lookup"><span data-stu-id="a643c-115">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

### <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="a643c-116">Creación asincrónica de un contenedor con sondeo</span><span class="sxs-lookup"><span data-stu-id="a643c-116">Asynchronous container create with polling</span></span>

<span data-ttu-id="a643c-117">En este ejemplo se crea un grupo de contenedores con un solo contenedor con el método de creación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="a643c-117">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="a643c-118">Después, sondea el grupo de contenedores en Azure y proporciona el estado del grupo de contenedores hasta que el estado es "En ejecución".</span><span class="sxs-lookup"><span data-stu-id="a643c-118">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

### <a name="create-task-based-container-group"></a><span data-ttu-id="a643c-119">Creación de un grupo de contenedores basado en tareas</span><span class="sxs-lookup"><span data-stu-id="a643c-119">Create task-based container group</span></span>

<span data-ttu-id="a643c-120">En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas.</span><span class="sxs-lookup"><span data-stu-id="a643c-120">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="a643c-121">El contenedor se configura con una [directiva de reinicio](/azure/container-instances/container-instances-restart-policy) "Never" y una [línea de comandos personalizada](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="a643c-121">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="a643c-122">Si desea ejecutar un único comando con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una matriz de cadenas al método `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="a643c-122">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="a643c-123">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="a643c-123">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="a643c-124">En cambio, si desea ejecutar varios comandos con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento.</span><span class="sxs-lookup"><span data-stu-id="a643c-124">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="a643c-125">Por ejemplo, esto ejecuta los comandos `echo` y `tail`:</span><span class="sxs-lookup"><span data-stu-id="a643c-125">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

### <a name="list-container-groups"></a><span data-ttu-id="a643c-126">Enumeración de grupos de contenedores</span><span class="sxs-lookup"><span data-stu-id="a643c-126">List container groups</span></span>

<span data-ttu-id="a643c-127">En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a643c-127">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

### <a name="get-an-existing-container-group"></a><span data-ttu-id="a643c-128">Obtención de un grupo de contenedores existente</span><span class="sxs-lookup"><span data-stu-id="a643c-128">Get an existing container group</span></span>

<span data-ttu-id="a643c-129">En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades y sus valores.</span><span class="sxs-lookup"><span data-stu-id="a643c-129">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

### <a name="delete-a-container-group"></a><span data-ttu-id="a643c-130">Eliminación de grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="a643c-130">Delete a container group</span></span>

<span data-ttu-id="a643c-131">En este ejemplo se elimina un grupo de contenedores de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a643c-131">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="a643c-132">Referencia de API</span><span class="sxs-lookup"><span data-stu-id="a643c-132">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a643c-133">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a643c-133">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="a643c-134">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a643c-134">Samples</span></span>

* <span data-ttu-id="a643c-135">El código fuente de los ejemplos anteriores se encuentra en GitHub:</span><span class="sxs-lookup"><span data-stu-id="a643c-135">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="a643c-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="a643c-136">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="a643c-137">Más ejemplos de código de Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="a643c-137">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="a643c-138">[Ejemplos de código de Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="a643c-138">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="a643c-139">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a643c-139">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
