---
title: Bibliotecas de Azure Container Instances para .NET
description: Referencia de las bibliotecas de Azure Container Instances para .NET
ms.date: 06/11/2018
ms.topic: reference
ms.service: container-instances
ms.openlocfilehash: 552746b316f1ba80adce5f55bb22412749fd93bc
ms.sourcegitcommit: 4f7bc5c5cd333e41446a3ebe5639a211d8ac9b90
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2019
ms.locfileid: "54841282"
---
# <a name="azure-container-instances-libraries-for-net"></a><span data-ttu-id="68bca-103">Bibliotecas de Azure Container Instances para .NET</span><span class="sxs-lookup"><span data-stu-id="68bca-103">Azure Container Instances libraries for .NET</span></span>

<span data-ttu-id="68bca-104">Use las bibliotecas de Microsoft Azure Container Instances para .NET para crear y administrar instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="68bca-104">Use the Microsoft Azure Container Instances libraries for .NET to create and manage Azure container instances.</span></span> <span data-ttu-id="68bca-105">Para más información, consulte la [Introducción a Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="68bca-105">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="68bca-106">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="68bca-106">Management library</span></span>

<span data-ttu-id="68bca-107">Use la biblioteca de administración para crear y administrar instancias de contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="68bca-107">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="68bca-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="68bca-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ContainerInstance.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

### <a name="visual-studio-package-manager"></a><span data-ttu-id="68bca-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="68bca-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ContainerInstance.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.ContainerInstance.Fluent
```

## <a name="example-source"></a><span data-ttu-id="68bca-110">Ejemplo de código fuente</span><span class="sxs-lookup"><span data-stu-id="68bca-110">Example source</span></span>

<span data-ttu-id="68bca-111">Si desea ver los ejemplos de código siguientes en contexto, los encontrará en el repositorio de GitHub siguiente:</span><span class="sxs-lookup"><span data-stu-id="68bca-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="68bca-112">Azure-Samples/aci-docs-sample-dotnet</span><span class="sxs-lookup"><span data-stu-id="68bca-112">Azure-Samples/aci-docs-sample-dotnet</span></span>](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a><span data-ttu-id="68bca-113">Autenticación</span><span class="sxs-lookup"><span data-stu-id="68bca-113">Authentication</span></span>

<span data-ttu-id="68bca-114">Una de las maneras más fáciles de autenticar clientes de SDK es con la [autenticación basada en archivo][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="68bca-114">One of the easiest ways to authenticate SDK clients is with [file-based authentication][sdk-auth].</span></span> <span data-ttu-id="68bca-115">La autenticación basada en archivo analiza un archivo de credenciales al crear una instancia del objeto de cliente [IAzure][iazure] que, después, usa esas credenciales al autenticarse con Azure.</span><span class="sxs-lookup"><span data-stu-id="68bca-115">File-based authentication parses a credentials file when instantiating the [IAzure][iazure] client object, which then uses those credentials when authenticating with Azure.</span></span> <span data-ttu-id="68bca-116">Para usar la autenticación basada en archivo</span><span class="sxs-lookup"><span data-stu-id="68bca-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="68bca-117">Cree un archivo de credenciales con la [CLI de Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="68bca-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="68bca-118">Si usa [Cloud Shell](https://shell.azure.com/) para generar el archivo de credenciales, copie su contenido en un archivo local al que la aplicación de .NET pueda tener acceso.</span><span class="sxs-lookup"><span data-stu-id="68bca-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your .NET application can access.</span></span>

2. <span data-ttu-id="68bca-119">Establezca la variable de entorno `AZURE_AUTH_LOCATION` en la ruta de acceso completa del archivo de credenciales generado.</span><span class="sxs-lookup"><span data-stu-id="68bca-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="68bca-120">Por ejemplo (en el shell de Bash):</span><span class="sxs-lookup"><span data-stu-id="68bca-120">For example (in the Bash shell):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="68bca-121">Después de crear el archivo de credenciales y rellenar la entorno variable `AZURE_AUTH_LOCATION`, use el método [Azure.Authenticate][iazure-authenticate] para inicializar el objeto de cliente [IAzure][iazure].</span><span class="sxs-lookup"><span data-stu-id="68bca-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the [Azure.Authenticate][iazure-authenticate] method to initialize the [IAzure][iazure] client object.</span></span> <span data-ttu-id="68bca-122">El proyecto de ejemplo obtiene en primer lugar el valor `AZURE_AUTH_LOCATION` y, después, llama a un método que devuelve un objeto de cliente `IAzure` inicializado:</span><span class="sxs-lookup"><span data-stu-id="68bca-122">The example project first obtains the `AZURE_AUTH_LOCATION` value, then calls a method that returns an initialized `IAzure` client object:</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

<span data-ttu-id="68bca-123">Este método de la aplicación de ejemplo devuelve la instancia de [IAzure][iazure] inicializada que, a continuación, se pasa como primer parámetro a todos los otros métodos del ejemplo:</span><span class="sxs-lookup"><span data-stu-id="68bca-123">This method from the sample application returns the initialized [IAzure][iazure] instance, which is then passed as the first parameter to all other methods in the sample:</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

<span data-ttu-id="68bca-124">Para más información acerca de los métodos de autenticación disponibles en las bibliotecas de administración de .NET para Azure, consulte [Autenticación con las bibliotecas de administración de Azure para .NET][sdk-auth].</span><span class="sxs-lookup"><span data-stu-id="68bca-124">For more details about the available authentication methods in the .NET management libraries for Azure, see [Authentication in Azure Management Libraries for .NET][sdk-auth].</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="68bca-125">Creación de un grupo de contenedores: un solo contenedor</span><span class="sxs-lookup"><span data-stu-id="68bca-125">Create container group - single container</span></span>

<span data-ttu-id="68bca-126">En este ejemplo se crea un grupo de contenedores con un solo contenedor.</span><span class="sxs-lookup"><span data-stu-id="68bca-126">This example creates a container group with a single container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="68bca-127">Creación de un grupo de contenedores: varios contenedores</span><span class="sxs-lookup"><span data-stu-id="68bca-127">Create container group - multiple containers</span></span>

<span data-ttu-id="68bca-128">En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.</span><span class="sxs-lookup"><span data-stu-id="68bca-128">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a><span data-ttu-id="68bca-129">Creación asincrónica de un contenedor con sondeo</span><span class="sxs-lookup"><span data-stu-id="68bca-129">Asynchronous container create with polling</span></span>

<span data-ttu-id="68bca-130">En este ejemplo se crea un grupo de contenedores con un solo contenedor con el método de creación asincrónica.</span><span class="sxs-lookup"><span data-stu-id="68bca-130">This example creates a container group with a single container using the async create method.</span></span> <span data-ttu-id="68bca-131">Después, sondea el grupo de contenedores en Azure y proporciona el estado del grupo de contenedores hasta que el estado es "En ejecución".</span><span class="sxs-lookup"><span data-stu-id="68bca-131">It then polls Azure for the container group, and outputs the container group's status until its state is "Running."</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="68bca-132">Creación de un grupo de contenedores basado en tareas</span><span class="sxs-lookup"><span data-stu-id="68bca-132">Create task-based container group</span></span>

<span data-ttu-id="68bca-133">En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas.</span><span class="sxs-lookup"><span data-stu-id="68bca-133">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="68bca-134">El contenedor se configura con una [directiva de reinicio](/azure/container-instances/container-instances-restart-policy) "Never" y una [línea de comandos personalizada](/azure/container-instances/container-instances-restart-policy#command-line-override).</span><span class="sxs-lookup"><span data-stu-id="68bca-134">The container is configured with a [restart policy](/azure/container-instances/container-instances-restart-policy) of "Never" and a [custom command line](/azure/container-instances/container-instances-restart-policy#command-line-override).</span></span>

<span data-ttu-id="68bca-135">Si desea ejecutar un único comando con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una matriz de cadenas al método `WithStartingCommandLines`.</span><span class="sxs-lookup"><span data-stu-id="68bca-135">If you want to run a single command with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string array to the `WithStartingCommandLines` method.</span></span> <span data-ttu-id="68bca-136">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="68bca-136">For example:</span></span>

`WithStartingCommandLines("echo", "FOO", "BAR")`

<span data-ttu-id="68bca-137">En cambio, si desea ejecutar varios comandos con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento.</span><span class="sxs-lookup"><span data-stu-id="68bca-137">If, however, you want to run multiple commands with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="68bca-138">Por ejemplo, esto ejecuta los comandos `echo` y `tail`:</span><span class="sxs-lookup"><span data-stu-id="68bca-138">For example, this executes both an `echo` and a `tail` command:</span></span>

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="68bca-139">Enumeración de grupos de contenedores</span><span class="sxs-lookup"><span data-stu-id="68bca-139">List container groups</span></span>

<span data-ttu-id="68bca-140">En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68bca-140">This example lists the container groups in a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="68bca-141">Obtención de un grupo de contenedores existente</span><span class="sxs-lookup"><span data-stu-id="68bca-141">Get an existing container group</span></span>

<span data-ttu-id="68bca-142">En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades y sus valores.</span><span class="sxs-lookup"><span data-stu-id="68bca-142">This example gets a specific container group residing in a resource group and then prints a few of its properties and their values.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="68bca-143">Eliminación de grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="68bca-143">Delete a container group</span></span>

<span data-ttu-id="68bca-144">En este ejemplo se elimina un grupo de contenedores de un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68bca-144">This example deletes a container group from a resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[delete_container_group](~/aci-docs-sample-dotnet/Program.cs#delete_container_group "Delete container group")]

## <a name="api-reference"></a><span data-ttu-id="68bca-145">Referencia de API</span><span class="sxs-lookup"><span data-stu-id="68bca-145">API reference</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="68bca-146">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="68bca-146">Explore the management APIs</span></span>](/dotnet/api/overview/azure/containerinstances/management)

## <a name="samples"></a><span data-ttu-id="68bca-147">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="68bca-147">Samples</span></span>

* <span data-ttu-id="68bca-148">El código fuente de los ejemplos anteriores se encuentra en GitHub:</span><span class="sxs-lookup"><span data-stu-id="68bca-148">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="68bca-149">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span><span class="sxs-lookup"><span data-stu-id="68bca-149">[Azure-Samples/aci-docs-sample-dotnet][aci-docs-sample-dotnet]</span></span>

* <span data-ttu-id="68bca-150">Más ejemplos de código de Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="68bca-150">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="68bca-151">[Ejemplos de código de Azure][samples]</span><span class="sxs-lookup"><span data-stu-id="68bca-151">[Azure Code Samples][samples]</span></span>

<span data-ttu-id="68bca-152">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="68bca-152">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
