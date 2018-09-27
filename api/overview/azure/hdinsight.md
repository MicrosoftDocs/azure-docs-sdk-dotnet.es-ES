---
title: SDK de Azure HDInsight para .NET
description: Referencia del SDK de Azure HDInsight para .NET
ms.date: 9/19/2018
ms.topic: reference
ms.service: hd-insight
ms.openlocfilehash: d25bdb1c9086cd93190b97f519654f2c193b9dc3
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190688"
---
# <a name="azure-hdinsight-net-sdk"></a><span data-ttu-id="c61ab-103">SDK de Azure HDInsight para .NET</span><span class="sxs-lookup"><span data-stu-id="c61ab-103">Azure HDInsight .NET SDK</span></span>

## <a name="azure-hdinsight-libraries-for-net-2x"></a><span data-ttu-id="c61ab-104">Bibliotecas de Azure HDInsight para .NET 2.X</span><span class="sxs-lookup"><span data-stu-id="c61ab-104">Azure HDInsight libraries for .NET 2.X</span></span>

## <a name="overview"></a><span data-ttu-id="c61ab-105">Información general</span><span class="sxs-lookup"><span data-stu-id="c61ab-105">Overview</span></span>

<span data-ttu-id="c61ab-106">El SDK de .NET del servicio HDInsight proporciona clases que se relacionan con la creación, configuración, envío y supervisión de trabajos de Hadoop administrados por un servicio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c61ab-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="c61ab-107">Además, proporciona clases para administrar suscripciones de Azure con el servicio HDInsight y para configurar los clústeres, las cuentas de almacenamiento y otros recursos asociados a los clústeres de HDInsight administrados por una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ab-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="c61ab-108">Bibliotecas de administración</span><span class="sxs-lookup"><span data-stu-id="c61ab-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="c61ab-109">Trabajos</span><span class="sxs-lookup"><span data-stu-id="c61ab-109">Jobs</span></span>

<span data-ttu-id="c61ab-110">Utilice el SDK de cliente de Azure HDInsight para crear, administrar y supervisar trabajos en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c61ab-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="c61ab-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c61ab-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c61ab-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c61ab-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="c61ab-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c61ab-113">Code Example</span></span>

<span data-ttu-id="c61ab-114">En este ejemplo se ejecuta un trabajo de Hive en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c61ab-114">This example runs a Hive job in a Hadoop cluster.</span></span>

```csharp
HDInsightJobManagementClient managementClient = new HDInsightJobManagementClient(clusterUri, credentials);

Dictionary<string, string> defines = new Dictionary<string, string> {
    { "hive.execution.engine", "tez" },
    { "hive.exec.reducers.max", "1" }
};
List<string> arguments = new List<string> { { "argA" }, { "argB" } };
HiveJobSubmissionParameters parameters = new HiveJobSubmissionParameters
{
    Query = "SHOW TABLES",
    Defines = defines,
    Arguments = arguments
};

JobSubmissionResponse jobResponse = managementClient.JobManagement.SubmitHiveJob(parameters);
```

### <a name="hdinsight"></a><span data-ttu-id="c61ab-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="c61ab-115">HDInsight</span></span>

<span data-ttu-id="c61ab-116">Use la SDK de administración de Azure HDInsight para crear, administrar, iniciar, detener y escalar clústeres de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c61ab-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="c61ab-117">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c61ab-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c61ab-118">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c61ab-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="c61ab-119">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c61ab-119">Code Example</span></span>

<span data-ttu-id="c61ab-120">En este ejemplo se crea un clúster de Linux Hadoop de dos nodos de HDInsight con una instancia de Azure Blob Storage existente.</span><span class="sxs-lookup"><span data-stu-id="c61ab-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

```csharp
HDInsightManagementClient managementClient = new HDInsightManagementClient(authToken);
// Set parameters for the new cluster
ClusterCreateParameters parameters = new ClusterCreateParameters
{
    ClusterSizeInNodes = 2,
    UserName = "admin",
    Password = "<Enter HTTP User Password>",
    ClusterType = "Hadoop",
    OSType = OSType.Linux,
    Version = "3.5",
    // Use an Azure storage account as the default storage
    DefaultStorageInfo = new AzureStorageInfo("<StorageAccount>", "<StorageKey>", "<BlobContainerName>"),
    Location = "EAST US 2",
    SshUserName = "sshuser",
    SshPassword = "<Enter SSH User Password>",
};

// Create the cluster
managementClient.Clusters.Create("<ExistingResourceGroupName>", "<NewClusterName>", parameters);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c61ab-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="c61ab-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="c61ab-122">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c61ab-122">Samples</span></span>

- [<span data-ttu-id="c61ab-123">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="c61ab-124">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="c61ab-125">Ejecución de trabajos de Hive</span><span class="sxs-lookup"><span data-stu-id="c61ab-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="c61ab-126">Ejecución de trabajos de Pig</span><span class="sxs-lookup"><span data-stu-id="c61ab-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="c61ab-127">Más trabajos</span><span class="sxs-lookup"><span data-stu-id="c61ab-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="c61ab-128">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) de ejemplos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c61ab-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

## <a name="hdinsight-net-management-sdk-3x-preview"></a><span data-ttu-id="c61ab-129">SDK de administración de HDInsight para .NET 3.X (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="c61ab-129">HDInsight .NET Management SDK 3.X Preview</span></span>

## <a name="overview"></a><span data-ttu-id="c61ab-130">Información general</span><span class="sxs-lookup"><span data-stu-id="c61ab-130">Overview</span></span>

<span data-ttu-id="c61ab-131">El SDK de HDInsight para .NET proporciona clases y métodos que permiten administrar los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c61ab-131">The HDInsight .NET SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="c61ab-132">Incluye operaciones para crear, eliminar, actualizar, enumerar, escalar, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight y mucho más.</span><span class="sxs-lookup"><span data-stu-id="c61ab-132">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c61ab-133">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c61ab-133">Prerequisites</span></span>

* <span data-ttu-id="c61ab-134">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ab-134">An Azure account.</span></span> <span data-ttu-id="c61ab-135">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c61ab-135">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="c61ab-136">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c61ab-136">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="c61ab-137">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="c61ab-137">SDK Installation</span></span>

<span data-ttu-id="c61ab-138">En el proyecto de Visual Studio, abra la Consola del Administrador de paquetes; para ello, haga clic en **Herramientas**, **Administrador de paquetes de NuGet** y luego haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="c61ab-138">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="c61ab-139">En la Consola del Administrador de paquetes, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="c61ab-139">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="c61ab-140">Autenticación</span><span class="sxs-lookup"><span data-stu-id="c61ab-140">Authentication</span></span>

<span data-ttu-id="c61ab-141">En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="c61ab-141">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="c61ab-142">Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="c61ab-142">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="c61ab-143">Una vez hecho esto, tendrá una instancia de `HDInsightManagementClient`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="c61ab-143">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="c61ab-144">Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="c61ab-144">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="c61ab-145">Todos los métodos se describen aquí: [Autenticación con las bibliotecas de Azure para .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="c61ab-145">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="c61ab-146">Ejemplo de autenticación con una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="c61ab-146">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="c61ab-147">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="c61ab-147">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="c61ab-148">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c61ab-148">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="c61ab-149">La información de la suscripción se muestra en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c61ab-149">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="c61ab-150">Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta:</span><span class="sxs-lookup"><span data-stu-id="c61ab-150">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="c61ab-151">Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="c61ab-151">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="c61ab-152">Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c61ab-152">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="c61ab-153">A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c61ab-153">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="c61ab-154">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c61ab-154">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="c61ab-155">Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="c61ab-155">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```csharp
using Microsoft.Azure.Management.HDInsight;
using Microsoft.Azure.Management.HDInsight.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent;

namespace HDI_SDK_Test
{
    class Program
    {
        static void Main(string[] args)
        {
            // Tenant ID for your Azure Subscription
            var TENANT_ID = "";
            // Your Service Principal App Client ID
            var CLIENT_ID = "";
            // Your Service Principal Client Secret
            var CLIENT_SECRET = "";
            // Azure Subscription ID
            var SUBSCRIPTION_ID = "";

            var credentials = SdkContext.AzureCredentialsFactory
                .FromServicePrincipal(
                CLIENT_ID,
                CLIENT_SECRET,
                TENANT_ID,
                AzureEnvironment.AzureGlobalCloud);

            var client = new HDInsightManagementClient(credentials);
            client.SubscriptionId = SUBSCRIPTION_ID;
        }
    }
}
```


## <a name="cluster-management"></a><span data-ttu-id="c61ab-156">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-156">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="c61ab-157">En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClient`, y que la ha almacenado en una variable llamada `client`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-157">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="c61ab-158">En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-158">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="c61ab-159">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="c61ab-159">Create a Cluster</span></span>

<span data-ttu-id="c61ab-160">Para crear un nuevo clúster, se puede llamar a `client.Clusters.Create()`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-160">A new cluster can be created by calling `client.Clusters.Create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="c61ab-161">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-161">Example</span></span>

<span data-ttu-id="c61ab-162">En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c61ab-162">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="c61ab-163">En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante.</span><span class="sxs-lookup"><span data-stu-id="c61ab-163">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="c61ab-164">Si ya los ha creado, puede omitir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="c61ab-164">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="c61ab-165">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c61ab-165">Creating a Resource Group</span></span>

<span data-ttu-id="c61ab-166">Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c61ab-166">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="c61ab-167">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c61ab-167">Creating a Storage Account</span></span>

<span data-ttu-id="c61ab-168">Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="c61ab-168">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="c61ab-169">Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):</span><span class="sxs-lookup"><span data-stu-id="c61ab-169">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="c61ab-170">El siguiente fragmento de código de .NET crea un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="c61ab-170">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="c61ab-171">Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="c61ab-171">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```csharp
// The name for the cluster you are creating
var clusterName = "";
// The name of your existing Resource Group
var resourceGroupName = "";
// Choose a username
var username = "";
// Choose a password
var password = "";
// Replace <> with the name of your storage account
var storageAccount = "<>.blob.core.windows.net";
// Storage account key you obtained above
var storageAccountKey = "";
// Choose a region
var location = "";
var container = "default";

var parameters = new ClusterCreateParametersExtended
{
    Location = location,
    Tags = new Dictionary<string, string>(),
    Properties = new ClusterCreateProperties
    {
        ClusterVersion = "3.6",
        OsType = OSType.Linux,
        ClusterDefinition = new ClusterDefinition
        {
            Kind = "Hadoop",            
            Configurations = new Dictionary<string, Dictionary<string, string>>()
            {                
                { "gateway", new Dictionary<string, string>
                    {
                        { "restAuthCredential.isEnabled", "true" },
                        { "restAuthCredential.username", username},
                        { "restAuthCredential.password", password}
                    }
                }
            }
        },
        Tier = Tier.Standard,
        ComputeProfile = new ComputeProfile
        {
            Roles = new List<Role>{
                new Role
                {
                    Name = "headnode",
                    TargetInstanceCount = 2,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
                new Role
                {
                    Name = "workernode",
                    TargetInstanceCount = 1,
                    HardwareProfile = new HardwareProfile
                    {
                        VmSize = "Large"
                    },
                    OsProfile = new OsProfile
                    {
                        LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
                        {
                            Username = username,
                            Password = password
                        }
                    }
                },
            }
        },
        StorageProfile = new StorageProfile
        {
            Storageaccounts = new[]
            {
                new StorageAccount
                {
                    Name = storageAccount,
                    Key = storageAccountKey,
                    Container = container,
                    IsDefault = true
                }
            }
        }
    }
};
client.Clusters.Create(
    resourceGroupName,
    clusterName,
    parameters
);
```

### <a name="get-cluster-details"></a><span data-ttu-id="c61ab-172">Obtención de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="c61ab-172">Get Cluster Details</span></span>

<span data-ttu-id="c61ab-173">Para obtener las propiedades de un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="c61ab-173">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="c61ab-174">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-174">Example</span></span>

<span data-ttu-id="c61ab-175">Puede usar `get` para confirmar que ha creado correctamente el clúster.</span><span class="sxs-lookup"><span data-stu-id="c61ab-175">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="c61ab-176">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="c61ab-176">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="c61ab-177">El valor devuelto de `get`, almacenado en la variable `myCluster`, es de tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-177">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="c61ab-178">Encontrará una lista completa de las propiedades de este objeto [aquí](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span><span class="sxs-lookup"><span data-stu-id="c61ab-178">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="c61ab-179">Lista de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-179">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="c61ab-180">Lista de clústeres de la suscripción</span><span class="sxs-lookup"><span data-stu-id="c61ab-180">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="c61ab-181">Lista de clústeres por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c61ab-181">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="c61ab-182">Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `IPage<Cluster>`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-182">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="c61ab-183">Para obtener la siguiente página, llame a `client.Clusters.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-183">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="c61ab-184">Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="c61ab-184">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="c61ab-185">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-185">Example</span></span>
<span data-ttu-id="c61ab-186">El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="c61ab-186">The following example prints the properties of all clusters for the current subscription:</span></span>

```csharp
var clustersPaged = client.Clusters.List();
while (true)
{
  foreach (var cluster in clustersPaged)
  {
    Debug.WriteLine(cluster.Name);
  
}  if (clustersPaged.NextPageLink == null)
  {
    break;
  }
  clustersPaged = client.Clusters.ListNext(clustersPaged.NextPageLink);
}
```

### <a name="delete-a-cluster"></a><span data-ttu-id="c61ab-187">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="c61ab-187">Delete a Cluster</span></span>

<span data-ttu-id="c61ab-188">Para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="c61ab-188">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="c61ab-189">Actualización de las etiquetas del clúster</span><span class="sxs-lookup"><span data-stu-id="c61ab-189">Update Cluster Tags</span></span>

<span data-ttu-id="c61ab-190">Puede actualizar las etiquetas de un clúster determinado de este modo:</span><span class="sxs-lookup"><span data-stu-id="c61ab-190">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="c61ab-191">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-191">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="scale-cluster"></a><span data-ttu-id="c61ab-192">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-192">Scale Cluster</span></span>

<span data-ttu-id="c61ab-193">Para escalar el número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño:</span><span class="sxs-lookup"><span data-stu-id="c61ab-193">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="c61ab-194">Supervisión de clústeres</span><span class="sxs-lookup"><span data-stu-id="c61ab-194">Cluster Monitoring</span></span>

<span data-ttu-id="c61ab-195">El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="c61ab-195">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="c61ab-196">Habilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="c61ab-196">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="c61ab-197">Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="c61ab-197">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="c61ab-198">Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="c61ab-198">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="c61ab-199">Para habilitar OMS Monitoring en el clúster:</span><span class="sxs-lookup"><span data-stu-id="c61ab-199">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="c61ab-200">Ver el estado de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="c61ab-200">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="c61ab-201">Para obtener el estado de OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="c61ab-201">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="c61ab-202">Deshabilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="c61ab-202">Disable OMS Monitoring</span></span>

<span data-ttu-id="c61ab-203">Para deshabilitar OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="c61ab-203">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="c61ab-204">Acciones de script</span><span class="sxs-lookup"><span data-stu-id="c61ab-204">Script Actions</span></span>

<span data-ttu-id="c61ab-205">HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="c61ab-205">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="c61ab-206">Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="c61ab-206">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="c61ab-207">Ejecución de acciones de script</span><span class="sxs-lookup"><span data-stu-id="c61ab-207">Execute Script Actions</span></span>

<span data-ttu-id="c61ab-208">Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="c61ab-208">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="c61ab-209">Eliminación de una acción de script</span><span class="sxs-lookup"><span data-stu-id="c61ab-209">Delete Script Action</span></span>

<span data-ttu-id="c61ab-210">Para eliminar una acción de script persistente específica en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="c61ab-210">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="c61ab-211">Lista de acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="c61ab-211">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="c61ab-212">`ListPersistedScripts()` y `List()` devuelven un objeto `IPage<RuntimeScriptActionDetail>`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-212">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="c61ab-213">Para obtener la siguiente página, llame a `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="c61ab-213">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="c61ab-214">Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="c61ab-214">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="c61ab-215">Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="c61ab-215">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="c61ab-216">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-216">Example</span></span>

```csharp
var scriptsPaged = client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.
    }
    if (scriptsPaged.NextPageLink == null)
    {
        break;
    }
    scriptsPaged = client.ScriptActions.ListPersistedScriptsNext(scriptsPaged.NextPageLink);
}
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="c61ab-217">Lista del historial de ejecución de todos los scripts</span><span class="sxs-lookup"><span data-stu-id="c61ab-217">List All Scripts' Execution History</span></span>

<span data-ttu-id="c61ab-218">Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="c61ab-218">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="c61ab-219">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c61ab-219">Example</span></span>

<span data-ttu-id="c61ab-220">Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.</span><span class="sxs-lookup"><span data-stu-id="c61ab-220">This example prints all the details for all past script executions.</span></span>

```csharp
var scriptExecutionsPaged = client.ScriptExecutionHistory.List("<Resource Group Name>", "<Cluster Name>");
while (true)
{
    foreach (var script in scriptExecutionsPaged)
    {
        Debug.WriteLine(script.Name); //There are other properties of RuntimeScriptActionDetail besides Name, such as Status, Operation, StartTime, EndTime, etc. See reference documentation.

    }
    if (scriptExecutionsPaged.NextPageLink == null)
    {
        break;
    }
    scriptExecutionsPaged = client.ScriptExecutionHistory.ListNext(scriptExecutionsPaged.NextPageLink);
}
```
