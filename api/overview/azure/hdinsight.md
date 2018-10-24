---
title: SDK de Azure HDInsight para .NET
description: Referencia del SDK de Azure HDInsight para .NET
ms.date: 9/19/2018
ms.topic: reference
ms.service: hdinsight
ms.openlocfilehash: 35e2c8c07fb2b86b2d0ae9be4f855e369c1aa86d
ms.sourcegitcommit: 1cf4550df8ed3236d838f561f6177d14d89b5e44
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49348207"
---
# <a name="azure-hdinsight-net-sdk"></a>SDK de Azure HDInsight para .NET

## <a name="azure-hdinsight-libraries-for-net-2x"></a>Bibliotecas de Azure HDInsight para .NET 2.X

## <a name="overview"></a>Información general

El SDK de .NET del servicio HDInsight proporciona clases que se relacionan con la creación, configuración, envío y supervisión de trabajos de Hadoop administrados por un servicio Azure HDInsight. Además, proporciona clases para administrar suscripciones de Azure con el servicio HDInsight y para configurar los clústeres, las cuentas de almacenamiento y otros recursos asociados a los clústeres de HDInsight administrados por una suscripción de Azure.

## <a name="management-libraries"></a>Bibliotecas de administración

### <a name="jobs"></a>Trabajos

Utilice el SDK de cliente de Azure HDInsight para crear, administrar y supervisar trabajos en un clúster de Hadoop. 

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a>Ejemplo de código

En este ejemplo se ejecuta un trabajo de Hive en un clúster de Hadoop.

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

### <a name="hdinsight"></a>HDInsight

Use la SDK de administración de Azure HDInsight para crear, administrar, iniciar, detener y escalar clústeres de Hadoop.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea un clúster de Linux Hadoop de dos nodos de HDInsight con una instancia de Azure Blob Storage existente.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a>Ejemplos

- [Creación de clústeres](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [Administración de clústeres](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [Ejecución de trabajos de Hive](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [Ejecución de trabajos de Pig](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [Más trabajos](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) de ejemplos de Azure SQL Database.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package

## <a name="hdinsight-net-management-sdk-3x-preview"></a>SDK de administración de HDInsight para .NET 3.X (versión preliminar)

## <a name="overview"></a>Información general

El SDK de HDInsight para .NET proporciona clases y métodos que permiten administrar los clústeres de HDInsight. Incluye operaciones para crear, eliminar, actualizar, enumerar, cambiar tamaño, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight, entre otras.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta de Azure. Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).
* [Visual Studio](https://visualstudio.microsoft.com/downloads/)

## <a name="sdk-installation"></a>Instalación del SDK

En el proyecto de Visual Studio, abra la Consola del Administrador de paquetes; para ello, haga clic en **Herramientas**, **Administrador de paquetes de NuGet** y luego haga clic en **Consola del Administrador de paquetes**.

En la Consola del Administrador de paquetes, ejecute los siguientes comandos:

```
  Install-Package Microsoft.Azure.Management.HDInsight -Version 3.1.0-preview
  Install-Package Microsoft.Azure.Management.Fluent
  Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

## <a name="authentication"></a>Autenticación

En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.  Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación. Una vez hecho esto, tendrá una instancia de `HDInsightManagementClient`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).

> [!NOTE]
> Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades. Todos los métodos se describen aquí: [Autenticación con las bibliotecas de Azure para .NET](https://docs.microsoft.com/en-us/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)

### <a name="authentication-example-using-a-service-principal"></a>Ejemplo de autenticación con una entidad de servicio

En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash). Compruebe que está usando la suscripción en la que desea crear la entidad de servicio. 

```azurecli-interactive
az account show
```

La información de la suscripción se muestra en formato JSON.

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

Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación. Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

La información de la entidad de servicio se muestra con formato JSON.

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
Copie el siguiente fragmento de código y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.

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


## <a name="cluster-management"></a>Administración de clústeres

> [!NOTE]
> En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClient`, y que la ha almacenado en una variable llamada `client`. En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClient`.

### <a name="create-a-cluster"></a>Creación de un clúster

Para crear un nuevo clúster, se puede llamar a `client.Clusters.Create()`. 

#### <a name="example"></a>Ejemplo

En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.

> [!NOTE]
> En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante. Si ya los ha creado, puede omitir estos pasos.

##### <a name="creating-a-resource-group"></a>Creación de un grupo de recursos

Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Creación de una cuenta de almacenamiento

Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
El siguiente fragmento de código de .NET crea un clúster de Spark con dos nodos principales y un nodo de trabajo. Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.

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

### <a name="get-cluster-details"></a>Obtención de los detalles del clúster

Para obtener las propiedades de un clúster determinado:

```csharp
client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

Puede usar `get` para confirmar que ha creado correctamente el clúster.

```csharp
var myCluster = client.Clusters.Get("<Resource Group Name>", "<Cluster Name>");
Debug.WriteLine(myCluster.Name); //Prints the name of the cluster
Debug.WriteLine(myCluster.Id) //Prints the resource Id of the cluster
```

La salida debe ser similar a la siguiente:

```
<Cluster Name>
/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>
```
> [!NOTE]
> El valor devuelto de `get`, almacenado en la variable `myCluster`, es de tipo `Microsoft.Azure.Management.HDInsight.ModelsCluster`. Encontrará una lista completa de las propiedades de este objeto [aquí](https://docs.microsoft.com/en-us/dotnet/api/microsoft.azure.management.hdinsight.models.cluster?view=azure-dotnet-preview).


### <a name="list-clusters"></a>Lista de clústeres

#### <a name="list-clusters-under-the-subscription"></a>Lista de clústeres de la suscripción

```csharp
client.Clusters.List();
```
#### <a name="list-clusters-by-resource-group"></a>Lista de clústeres por grupo de recursos

```csharp
client.Clusters.ListByResourceGroup("<Resource Group Name>");
```
> [!NOTE]
> Tanto `List()` como `ListByResourceGroup()` devuelven un objeto `IPage<Cluster>`. Para obtener la siguiente página, llame a `client.Clusters.ListNext("Next Page Link")`. Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en el ejemplo siguiente.

#### <a name="example"></a>Ejemplo
El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:

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

### <a name="delete-a-cluster"></a>Eliminación de un clúster

Para eliminar un clúster:

```csharp
client.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
```

### <a name="update-cluster-tags"></a>Actualización de las etiquetas del clúster

Puede actualizar las etiquetas de un clúster determinado de este modo:

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(<Dictionary of Tags>));
```
#### <a name="example"></a>Ejemplo

```csharp
client.Clusters.Update("<Resource Group Name>", "<Cluster Name>", new ClusterPatchParameters(new Dictionary<string, string> { { "tag1Name", "tag1Value" }, { "tag2Name", "tag2Value" } }));
```

### <a name="resize-cluster"></a>Cambio del tamaño de clúster

Para cambiar el tamaño de un número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño como sigue:

```csharp
client.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <Num of Worker Nodes (int)>)
```

## <a name="cluster-monitoring"></a>Supervisión de clústeres

El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Habilitación de OMS Monitoring

> [!NOTE]
> Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics. Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Para habilitar OMS Monitoring en el clúster:

```csharp
client.Extension.EnableMonitoring("<Resource Group Name", "Cluster Name", new ClusterMonitoringRequest(workspaceId: "<Workspace Id>"));
```

### <a name="view-status-of-oms-monitoring"></a>Ver el estado de OMS Monitoring

Para obtener el estado de OMS en el clúster:

```csharp
client.Extension.GetMonitoringStatus("<Resource Group Name", "Cluster Name");
```

### <a name="disable-oms-monitoring"></a>Deshabilitación de OMS Monitoring

Para deshabilitar OMS en el clúster:

```csharp
client.Extension.DisableMonitoring("<Resource Group Name>", "<Cluster Name>");
```

## <a name="script-actions"></a>Acciones de script

HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.
> [!NOTE]
> Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>Ejecución de acciones de script

Puede ejecutar acciones de script en un clúster determinado de la siguiente manera:

```csharp
var scriptAction1 = new RuntimeScriptAction("<Script Name>", "<URL To Script>", <List<string> of roles>); //valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.Clusters.ExecuteScriptActions("<Resource Group Name>", "<Cluster Name>", new List<RuntimeScriptAction> { scriptAction1 }, <persistOnSuccess (bool)>); //add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Eliminación de una acción de script

Para eliminar una acción de script persistente específica en un clúster determinado:

```csharp
client.ScriptActions.Delete("<Resource Group Name>", "<Cluster Name>", "<Script Name>");
```

### <a name="list-persisted-script-actions"></a>Lista de acciones de script persistentes

> [!NOTE]
> `ListPersistedScripts()` y `List()` devuelven un objeto `IPage<RuntimeScriptActionDetail>`. Para obtener la siguiente página, llame a `client.ScriptActions.ListPersistedScriptsNext("Next Page Link")` o `client.ScriptExecutionHistory.ListNext("Next Page Link")`. Este paso se puede repetir hasta que `NextPageLink` sea `null`, tal y como se muestra en los ejemplos siguientes.

Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:
```csharp
client.ScriptActions.ListPersistedScripts("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

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

### <a name="list-all-scripts-execution-history"></a>Lista del historial de ejecución de todos los scripts

Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:

```csharp
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>");
```

#### <a name="example"></a>Ejemplo

Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.

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
