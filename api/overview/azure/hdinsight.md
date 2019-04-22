---
title: SDK de Azure HDInsight para .NET
description: Referencia del SDK de Azure HDInsight para .NET
ms.date: 04/10/2019
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 2282a302b269a52c71ed88c26e021344cdca4382
ms.sourcegitcommit: 4328168172ac1b1a448e16988f75199262bc5c2d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2019
ms.locfileid: "59700263"
---
# <a name="azure-hdinsight-sdk-for-net"></a><span data-ttu-id="90451-103">SDK de Azure HDInsight para .NET</span><span class="sxs-lookup"><span data-stu-id="90451-103">Azure HDInsight SDK for .NET</span></span>

<span data-ttu-id="90451-104">Azure HDInsight ofrece SDK de administración y trabajos para .NET, que proporcionan clases para administrar clústeres de HDInsight y enviar y supervisar trabajos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="90451-104">Azure HDInsight offers management and job SDKs for .NET that provide classes for managing your HDInsight cluster and submitting and monitoring Hadoop jobs.</span></span>

## <a name="management"></a><span data-ttu-id="90451-105">Administración</span><span class="sxs-lookup"><span data-stu-id="90451-105">Management</span></span>

<span data-ttu-id="90451-106">El SDK de administración de HDInsight para .NET proporciona clases y métodos que permiten administrar los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90451-106">The HDInsight management SDK for .NET provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="90451-107">Incluye operaciones para crear, eliminar, actualizar, enumerar, cambiar tamaño, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight, entre otras.</span><span class="sxs-lookup"><span data-stu-id="90451-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90451-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="90451-108">Prerequisites</span></span>

* <span data-ttu-id="90451-109">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="90451-109">An Azure account.</span></span> <span data-ttu-id="90451-110">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="90451-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="90451-111">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90451-111">Visual Studio</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a><span data-ttu-id="90451-112">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="90451-112">SDK Installation</span></span>

<span data-ttu-id="90451-113">En el proyecto de Visual Studio, abra la Consola del Administrador de paquetes; para ello, haga clic en **Herramientas**, **Administrador de paquetes de NuGet** y luego haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="90451-113">From your Visual Studio project, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>

<span data-ttu-id="90451-114">En la Consola del Administrador de paquetes, ejecute los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="90451-114">In the Package Manager Console, execute the following commands:</span></span>

```
  Install-Package Microsoft.Azure.Management.HDInsight
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a><span data-ttu-id="90451-115">Authentication</span><span class="sxs-lookup"><span data-stu-id="90451-115">Authentication</span></span>

<span data-ttu-id="90451-116">En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="90451-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="90451-117">Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="90451-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="90451-118">Una vez hecho esto, tendrá una instancia de `HDInsightManagementClient`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="90451-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="90451-119">Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="90451-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="90451-120">Todos los métdosos se describen aquí: [Autenticación con las bibliotecas de Azure para .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span><span class="sxs-lookup"><span data-stu-id="90451-120">All methods are outlined here: [Authenticate with the Azure Libraries for .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="90451-121">Ejemplo de autenticación con una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="90451-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="90451-122">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="90451-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="90451-123">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="90451-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="90451-124">La información de la suscripción se muestra en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="90451-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="90451-125">Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta:</span><span class="sxs-lookup"><span data-stu-id="90451-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="90451-126">Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="90451-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="90451-127">Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90451-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="90451-128">A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90451-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="90451-129">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="90451-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="90451-130">Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="90451-130">Copy the below snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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

## <a name="cluster-management"></a><span data-ttu-id="90451-131">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="90451-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="90451-132">En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClient`, y que la ha almacenado en una variable llamada `client`.</span><span class="sxs-lookup"><span data-stu-id="90451-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="90451-133">En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="90451-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="90451-134">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="90451-134">Create a Cluster</span></span>

<span data-ttu-id="90451-135">Para crear un nuevo clúster, se puede llamar a `client.Clusters.Create()`.</span><span class="sxs-lookup"><span data-stu-id="90451-135">A new cluster can be created by calling `client.Clusters.Create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="90451-136">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="90451-136">Samples</span></span>

<span data-ttu-id="90451-137">Hay disponibles ejemplos de código para crear varios tipos comunes de clústeres de HDInsight: [Ejemplos de Azure HDInsight para .NET](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span><span class="sxs-lookup"><span data-stu-id="90451-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight .NET Samples](https://github.com/Azure-Samples/hdinsight-dotnet-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="90451-138">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-138">Example</span></span>

<span data-ttu-id="90451-139">En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="90451-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="90451-140">En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante.</span><span class="sxs-lookup"><span data-stu-id="90451-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="90451-141">Si ya los ha creado, puede omitir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="90451-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="90451-142">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="90451-142">Creating a Resource Group</span></span>

<span data-ttu-id="90451-143">Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90451-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="90451-144">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="90451-144">Creating a Storage Account</span></span>

<span data-ttu-id="90451-145">Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="90451-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="90451-146">Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):</span><span class="sxs-lookup"><span data-stu-id="90451-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="90451-147">El siguiente fragmento de código de .NET crea un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="90451-147">The below .NET snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="90451-148">Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="90451-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="90451-149">Obtención de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="90451-149">Get Cluster Details</span></span>

<span data-ttu-id="90451-150">Para obtener las propiedades de un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="90451-150">To get properties for a given cluster:</span></span>

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="90451-151">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-151">Example</span></span>

<span data-ttu-id="90451-152">Puede usar `get` para confirmar que ha creado correctamente el clúster.</span><span class="sxs-lookup"><span data-stu-id="90451-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

<span data-ttu-id="90451-153">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="90451-153">The output should look like:</span></span>

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> <span data-ttu-id="90451-154">El valor devuelto de `get`, almacenado en la variable `myCluster`, es de tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span><span class="sxs-lookup"><span data-stu-id="90451-154">The return value of `get`, stored in variable `myCluster`, is of type `Microsoft.Azure.Management.HDInsight.ModelsCluster`.</span></span> <span data-ttu-id="90451-155">Encontrará una lista completa de las propiedades de este objeto [aquí](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span><span class="sxs-lookup"><span data-stu-id="90451-155">A full list of this object's properties can be found [here](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).</span></span>


### <a name="list-clusters"></a><span data-ttu-id="90451-156">Lista de clústeres</span><span class="sxs-lookup"><span data-stu-id="90451-156">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="90451-157">Lista de clústeres de la suscripción</span><span class="sxs-lookup"><span data-stu-id="90451-157">List Clusters Under The Subscription</span></span>

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="90451-158">Lista de clústeres por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="90451-158">List Clusters By Resource Group</span></span>

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> <span data-ttu-id="90451-159">Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `IPage<Cluster>`.</span><span class="sxs-lookup"><span data-stu-id="90451-159">Both `List()` and `ListByResourceGroup()` return an `IPage<Cluster>` object.</span></span> <span data-ttu-id="90451-160">Para obtener la siguiente página, llame a `client.Clusters.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="90451-160">To get the next page, you can call `client.Clusters.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="90451-161">Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="90451-161">This can be repeated until `NextPageLink` is `null`, as shown in the example below.</span></span>

#### <a name="example"></a><span data-ttu-id="90451-162">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-162">Example</span></span>
<span data-ttu-id="90451-163">El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="90451-163">The following example prints the properties of all clusters for the current subscription:</span></span>

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

### <a name="delete-a-cluster"></a><span data-ttu-id="90451-164">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="90451-164">Delete a Cluster</span></span>

<span data-ttu-id="90451-165">Para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="90451-165">To delete a cluster:</span></span>

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a><span data-ttu-id="90451-166">Actualización de las etiquetas del clúster</span><span class="sxs-lookup"><span data-stu-id="90451-166">Update Cluster Tags</span></span>

<span data-ttu-id="90451-167">Puede actualizar las etiquetas de un clúster determinado de este modo:</span><span class="sxs-lookup"><span data-stu-id="90451-167">You can update the tags of a given cluster like so:</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a><span data-ttu-id="90451-168">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-168">Example</span></span>

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a><span data-ttu-id="90451-169">Cambio del tamaño de clúster</span><span class="sxs-lookup"><span data-stu-id="90451-169">Resize Cluster</span></span>

<span data-ttu-id="90451-170">Para cambiar el tamaño de un número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño como sigue:</span><span class="sxs-lookup"><span data-stu-id="90451-170">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="90451-171">Supervisión de clústeres</span><span class="sxs-lookup"><span data-stu-id="90451-171">Cluster Monitoring</span></span>

<span data-ttu-id="90451-172">El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="90451-172">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="90451-173">Habilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="90451-173">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="90451-174">Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="90451-174">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="90451-175">Si aún no ha creado una, puede aprender a hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="90451-175">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="90451-176">Para habilitar OMS Monitoring en el clúster:</span><span class="sxs-lookup"><span data-stu-id="90451-176">To enable OMS Monitoring on your cluster:</span></span>

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="90451-177">Ver el estado de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="90451-177">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="90451-178">Para obtener el estado de OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="90451-178">To get the status of OMS on your cluster:</span></span>

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="90451-179">Deshabilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="90451-179">Disable OMS Monitoring</span></span>

<span data-ttu-id="90451-180">Para deshabilitar OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="90451-180">To disable OMS on your cluster:</span></span>

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a><span data-ttu-id="90451-181">Acciones de script</span><span class="sxs-lookup"><span data-stu-id="90451-181">Script Actions</span></span>

<span data-ttu-id="90451-182">HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="90451-182">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="90451-183">Encontrará más información sobre cómo usar acciones de script aquí: [Personalización de clústeres de HDInsight basados en Linux mediante acciones de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span><span class="sxs-lookup"><span data-stu-id="90451-183">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="90451-184">Ejecución de acciones de script</span><span class="sxs-lookup"><span data-stu-id="90451-184">Execute Script Actions</span></span>

<span data-ttu-id="90451-185">Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:</span><span class="sxs-lookup"><span data-stu-id="90451-185">You can execute script actions on a given cluster like so:</span></span>

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="90451-186">Eliminación de una acción de script</span><span class="sxs-lookup"><span data-stu-id="90451-186">Delete Script Action</span></span>

<span data-ttu-id="90451-187">Para eliminar una acción de script persistente específica en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="90451-187">To delete a specified persisted script action on a given cluster:</span></span>

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="90451-188">Lista de acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="90451-188">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="90451-189">`ListPersistedScripts()` y `List()` devuelven un objeto `IPage<RuntimeScriptActionDetail>`.</span><span class="sxs-lookup"><span data-stu-id="90451-189">`ListPersistedScripts()` and `List()` return an `IPage<RuntimeScriptActionDetail>` object.</span></span> <span data-ttu-id="90451-190">Para obtener la siguiente página, llame a `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span><span class="sxs-lookup"><span data-stu-id="90451-190">To get the next page, you can call `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` or `client.ScriptExecutionHistory.ListNext("Next Page Link")`.</span></span> <span data-ttu-id="90451-191">Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en los ejemplos siguientes.</span><span class="sxs-lookup"><span data-stu-id="90451-191">This can be repeated until `NextPageLink` is `null`, as shown in the examples below.</span></span>

<span data-ttu-id="90451-192">Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="90451-192">To list all persisted script actions for the specified cluster:</span></span>
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="90451-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-193">Example</span></span>

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

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="90451-194">Lista del historial de ejecución de todos los scripts</span><span class="sxs-lookup"><span data-stu-id="90451-194">List All Scripts' Execution History</span></span>

<span data-ttu-id="90451-195">Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="90451-195">To list all scripts' execution history for the specified cluster:</span></span>

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a><span data-ttu-id="90451-196">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="90451-196">Example</span></span>

<span data-ttu-id="90451-197">Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.</span><span class="sxs-lookup"><span data-stu-id="90451-197">This example prints all the details for all past script executions.</span></span>

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

## <a name="jobs"></a><span data-ttu-id="90451-198">Trabajos</span><span class="sxs-lookup"><span data-stu-id="90451-198">Jobs</span></span>

<span data-ttu-id="90451-199">Utilice el SDK de trabajos de Azure HDInsight para .NET para crear, administrar y supervisar trabajos en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="90451-199">Use the Azure HDInsight job SDK for .NET to create, manage, and monitor jobs on a Hadoop cluster.</span></span>

### <a name="sdk-installation"></a><span data-ttu-id="90451-200">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="90451-200">SDK Installation</span></span>

<span data-ttu-id="90451-201">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directamente desde la [Consola del Administrador de paquetes] de Visual Studio [PackageManager] o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="90451-201">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="90451-202">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="90451-202">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

### <a name="code-example"></a><span data-ttu-id="90451-203">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="90451-203">Code Example</span></span>

<span data-ttu-id="90451-204">En este ejemplo se ejecuta un trabajo de Hive en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="90451-204">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="samples"></a><span data-ttu-id="90451-205">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="90451-205">Samples</span></span>

- [<span data-ttu-id="90451-206">Ejecución de trabajos de Hive</span><span class="sxs-lookup"><span data-stu-id="90451-206">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="90451-207">Ejecución de trabajos de Pig</span><span class="sxs-lookup"><span data-stu-id="90451-207">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="90451-208">Más trabajos</span><span class="sxs-lookup"><span data-stu-id="90451-208">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)
