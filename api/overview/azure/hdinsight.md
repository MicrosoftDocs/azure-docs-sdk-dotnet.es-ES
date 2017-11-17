---
title: Bibliotecas de Azure HDInsight para .NET
description: Referencia de las bibliotecas de Azure HDInsight para .NET
keywords: Azure, .NET, SDK, API, HDInsight
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: hd-insight
ms.custom: devcenter, svc-overview
ms.openlocfilehash: da9023ab4e6106754d48acb31cda58cdb358f5cb
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="azure-hdinsight-libraries-for-net"></a><span data-ttu-id="7ceab-104">Bibliotecas de Azure HDInsight para .NET</span><span class="sxs-lookup"><span data-stu-id="7ceab-104">Azure HDInsight libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7ceab-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7ceab-105">Overview</span></span>

<span data-ttu-id="7ceab-106">El SDK de .NET del servicio HDInsight proporciona clases que se relacionan con la creación, configuración, envío y supervisión de trabajos de Hadoop administrados por un servicio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ceab-106">The HDInsight Service .NET SDK provides classes that relate to the creation, configuration, submission, and monitoring of Hadoop jobs managed by an Azure HDInsight Service.</span></span> <span data-ttu-id="7ceab-107">Además, proporciona clases para administrar suscripciones de Azure con el servicio HDInsight y para configurar los clústeres, las cuentas de almacenamiento y otros recursos asociados a los clústeres de HDInsight administrados por una suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ceab-107">In addition, it provides classes to manage Azure subscriptions using the HDInsight Service and to configure the clusters, storage accounts, and other assets associated with the HDInsight clusters that are managed by an Azure subscription.</span></span>

## <a name="management-libraries"></a><span data-ttu-id="7ceab-108">Bibliotecas de administración</span><span class="sxs-lookup"><span data-stu-id="7ceab-108">Management libraries</span></span>

### <a name="jobs"></a><span data-ttu-id="7ceab-109">Trabajos</span><span class="sxs-lookup"><span data-stu-id="7ceab-109">Jobs</span></span>

<span data-ttu-id="7ceab-110">Utilice el SDK de cliente de Azure HDInsight para crear, administrar y supervisar trabajos en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7ceab-110">Use the Azure HDInsight client SDK to create, manage, and monitor jobs on a Hadoop cluster.</span></span> 

<span data-ttu-id="7ceab-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7ceab-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight.Job) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7ceab-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ceab-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight.Job
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight.Job
```

#### <a name="code-example"></a><span data-ttu-id="7ceab-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7ceab-113">Code Example</span></span>

<span data-ttu-id="7ceab-114">En este ejemplo se ejecuta un trabajo de Hive en un clúster de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7ceab-114">This example runs a Hive job in a Hadoop cluster.</span></span>

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

### <a name="hdinsight"></a><span data-ttu-id="7ceab-115">HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ceab-115">HDInsight</span></span>

<span data-ttu-id="7ceab-116">Use la SDK de administración de Azure HDInsight para crear, administrar, iniciar, detener y escalar clústeres de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="7ceab-116">Use the Azure HDInsight management SDK to create, manage, start, stop, and scale Hadoop clusters.</span></span>

<span data-ttu-id="7ceab-117">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7ceab-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.HDInsight) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7ceab-118">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7ceab-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.HDInsight
```

```bash
dotnet add package Microsoft.Azure.Management.HDInsight
```

#### <a name="code-example"></a><span data-ttu-id="7ceab-119">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7ceab-119">Code Example</span></span>

<span data-ttu-id="7ceab-120">En este ejemplo se crea un clúster de Linux Hadoop de dos nodos de HDInsight con una instancia de Azure Blob Storage existente.</span><span class="sxs-lookup"><span data-stu-id="7ceab-120">This example creates an HDInsight two node Linux Hadoop cluster with an existing Azure Blob Storage.</span></span>

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
> [<span data-ttu-id="7ceab-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="7ceab-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/hdinsights/management)


## <a name="samples"></a><span data-ttu-id="7ceab-122">Muestras</span><span class="sxs-lookup"><span data-stu-id="7ceab-122">Samples</span></span>

- [<span data-ttu-id="7ceab-123">Creación de clústeres</span><span class="sxs-lookup"><span data-stu-id="7ceab-123">Cluster creation</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-create-linux-clusters-dotnet-sdk)
- [<span data-ttu-id="7ceab-124">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="7ceab-124">Cluster management</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-administer-use-dotnet-sdk)
- [<span data-ttu-id="7ceab-125">Ejecución de trabajos de Hive</span><span class="sxs-lookup"><span data-stu-id="7ceab-125">Run Hive jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-hive-dotnet-sdk)
- [<span data-ttu-id="7ceab-126">Ejecución de trabajos de Pig</span><span class="sxs-lookup"><span data-stu-id="7ceab-126">Run Pig jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-use-pig-dotnet-sdk)
- [<span data-ttu-id="7ceab-127">Más trabajos</span><span class="sxs-lookup"><span data-stu-id="7ceab-127">More jobs</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-submit-hadoop-jobs-programmatically)

<span data-ttu-id="7ceab-128">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) de ejemplos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7ceab-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=hdinsight) of Azure SQL Database samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
