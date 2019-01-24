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

## <a name="example-source"></a>Ejemplo de código fuente

Si desea ver los ejemplos de código siguientes en contexto, los encontrará en el repositorio de GitHub siguiente:

[Azure-Samples/aci-docs-sample-dotnet](https://github.com/Azure-Samples/aci-docs-sample-dotnet)

## <a name="authentication"></a>Autenticación

Una de las maneras más fáciles de autenticar clientes de SDK es con la [autenticación basada en archivo][sdk-auth]. La autenticación basada en archivo analiza un archivo de credenciales al crear una instancia del objeto de cliente [IAzure][iazure] que, después, usa esas credenciales al autenticarse con Azure. Para usar la autenticación basada en archivo

1. Cree un archivo de credenciales con la [CLI de Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Si usa [Cloud Shell](https://shell.azure.com/) para generar el archivo de credenciales, copie su contenido en un archivo local al que la aplicación de .NET pueda tener acceso.

2. Establezca la variable de entorno `AZURE_AUTH_LOCATION` en la ruta de acceso completa del archivo de credenciales generado. Por ejemplo (en el shell de Bash):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Después de crear el archivo de credenciales y rellenar la entorno variable `AZURE_AUTH_LOCATION`, use el método [Azure.Authenticate][iazure-authenticate] para inicializar el objeto de cliente [IAzure][iazure]. El proyecto de ejemplo obtiene en primer lugar el valor `AZURE_AUTH_LOCATION` y, después, llama a un método que devuelve un objeto de cliente `IAzure` inicializado:

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#L29-L35 "Get environment variable")]

Este método de la aplicación de ejemplo devuelve la instancia de [IAzure][iazure] inicializada que, a continuación, se pasa como primer parámetro a todos los otros métodos del ejemplo:

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[authenticate](~/aci-docs-sample-dotnet/Program.cs#azure_auth "Authenticate IAzure client object")]

Para más información acerca de los métodos de autenticación disponibles en las bibliotecas de administración de .NET para Azure, consulte [Autenticación con las bibliotecas de administración de Azure para .NET][sdk-auth].

## <a name="create-container-group---single-container"></a>Creación de un grupo de contenedores: un solo contenedor

En este ejemplo se crea un grupo de contenedores con un solo contenedor.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group](~/aci-docs-sample-dotnet/Program.cs#create_container_group "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Creación de un grupo de contenedores: varios contenedores

En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_multi](~/aci-docs-sample-dotnet/Program.cs#create_container_group_multi "Create multi-container group")]

## <a name="asynchronous-container-create-with-polling"></a>Creación asincrónica de un contenedor con sondeo

En este ejemplo se crea un grupo de contenedores con un solo contenedor con el método de creación asincrónica. Después, sondea el grupo de contenedores en Azure y proporciona el estado del grupo de contenedores hasta que el estado es "En ejecución".

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_polling](~/aci-docs-sample-dotnet/Program.cs#create_container_group_polling "Create single-container group with async and polling")]

## <a name="create-task-based-container-group"></a>Creación de un grupo de contenedores basado en tareas

En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas. El contenedor se configura con una [directiva de reinicio](/azure/container-instances/container-instances-restart-policy) "Never" y una [línea de comandos personalizada](/azure/container-instances/container-instances-restart-policy#command-line-override).

Si desea ejecutar un único comando con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una matriz de cadenas al método `WithStartingCommandLines`. Por ejemplo: 

`WithStartingCommandLines("echo", "FOO", "BAR")`

En cambio, si desea ejecutar varios comandos con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento. Por ejemplo, esto ejecuta los comandos `echo` y `tail`:

`WithStartingCommandLines("/bin/sh", "-c", "echo FOO BAR && tail -f /dev/null")`

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[create_container_group_task](~/aci-docs-sample-dotnet/Program.cs#create_container_group_task "Run a task-based container")]

## <a name="list-container-groups"></a>Enumeración de grupos de contenedores

En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[list_container_groups](~/aci-docs-sample-dotnet/Program.cs#list_container_groups "List container groups")]

## <a name="get-an-existing-container-group"></a>Obtención de un grupo de contenedores existente

En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades y sus valores.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-dotnet -->  
[!code-csharp[get_container_group](~/aci-docs-sample-dotnet/Program.cs#get_container_group "Get container group")]

## <a name="delete-a-container-group"></a>Eliminación de grupo de contenedores

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

<!-- LINKS - External -->
[aci-docs-sample-dotnet]: https://github.com/Azure-Samples/aci-docs-sample-dotnet
[samples]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[sdk-auth]: https://github.com/Azure/azure-libraries-for-net/blob/master/AUTH.md

<!-- LINKS - Internal -->
[DotNetCLI]: /dotnet/core/tools/dotnet-add-package
[PackageManager]: /nuget/tools/package-manager-console
[iazure]: /dotnet/api/microsoft.azure.management.fluent.azure
[iazure-authenticate]: /dotnet/api/microsoft.azure.management.fluent.azure.authenticate
