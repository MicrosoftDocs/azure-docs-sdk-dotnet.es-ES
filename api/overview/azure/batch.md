---
title: Bibliotecas de Azure Batch para .NET
description: Referencia de las bibliotecas de Azure Batch para .NET
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: batch
ms.custom: devcenter, svc-overview
ms.openlocfilehash: b6053e19d26247dd36ed7e38fc33030f96aecca8
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065565"
---
# <a name="azure-batch-libraries-for-net"></a><span data-ttu-id="9126b-104">Bibliotecas de Azure Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="9126b-104">Azure Batch libraries for .NET</span></span>

<span data-ttu-id="9126b-105">Azure Batch es un servicio de plataforma para ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento (HPC) de manera eficaz en la nube.</span><span class="sxs-lookup"><span data-stu-id="9126b-105">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="9126b-106">Azure Batch programa el trabajo que conlleva mucho proceso para que se ejecute en una colección administrada de máquinas virtuales y puede escalar automáticamente los recursos de proceso para satisfacer las necesidades de sus trabajos.</span><span class="sxs-lookup"><span data-stu-id="9126b-106">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="9126b-107">Con Azure Batch, se pueden definir fácilmente los recursos de proceso de Azure para ejecutar las aplicaciones en paralelo y a escala.</span><span class="sxs-lookup"><span data-stu-id="9126b-107">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="9126b-108">No es preciso crear, configurar ni administrar manualmente un clúster de HPC, máquinas virtuales individuales, redes virtuales ni una infraestructura compleja de programación de tareas y trabajos.</span><span class="sxs-lookup"><span data-stu-id="9126b-108">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="9126b-109">Azure Batch automatiza o simplifica estas tareas automáticamente.</span><span class="sxs-lookup"><span data-stu-id="9126b-109">Azure Batch automates or simplifies these tasks for you.</span></span>

<span data-ttu-id="9126b-110">Lea más acerca de cómo [ejecutar cargas de trabajo en paralelo de manera intrínseca con Batch](/azure/batch/batch-technical-overview).</span><span class="sxs-lookup"><span data-stu-id="9126b-110">Read more about how to [run intrinsically parallel workloads with Batch](/azure/batch/batch-technical-overview).</span></span> <span data-ttu-id="9126b-111">También puede aprender sobre cómo [comenzar a crear soluciones con la biblioteca de cliente de Batch para .NET](/azure/batch/batch-dotnet-get-started).</span><span class="sxs-lookup"><span data-stu-id="9126b-111">You can also learn how to [get started building solutions with the Batch client library for .NET](/azure/batch/batch-dotnet-get-started).</span></span> <span data-ttu-id="9126b-112">Descubra cómo [administrar cuentas y cuotas de Batch con la biblioteca de administración de Batch para .NET](/azure/batch/batch-management-dotnet).</span><span class="sxs-lookup"><span data-stu-id="9126b-112">Discover how to [manage Batch accounts and quotas with the Batch Management library for .NET](/azure/batch/batch-management-dotnet).</span></span>

## <a name="client-library"></a><span data-ttu-id="9126b-113">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="9126b-113">Client library</span></span>

<span data-ttu-id="9126b-114">Use la biblioteca de cliente para ejecutar cargas de trabajo paralelas con Batch.</span><span class="sxs-lookup"><span data-stu-id="9126b-114">Use the client library to run parallel workloads with Batch.</span></span>

<span data-ttu-id="9126b-115">Instale el [paquete NuGet](https://www.nuget.org/packages/Azure.Batch) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9126b-115">Install the [NuGet package](https://www.nuget.org/packages/Azure.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9126b-116">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9126b-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="9126b-117">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="9126b-117">.NET Core CLI</span></span>

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a><span data-ttu-id="9126b-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9126b-118">Example</span></span>

<span data-ttu-id="9126b-119">En el ejemplo siguiente se usa el SDK de cliente para crear un trabajo y ejecutarlo en Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="9126b-119">The following example uses the client SDK to create a job to run in Azure Batch.</span></span>

```csharp
/*
using Microsoft.Azure.Batch.Auth;
using Microsoft.Azure.Batch;
*/
BatchSharedKeyCredentials credentials = new BatchSharedKeyCredentials(batchUrl, accountName, accountKey);
using (BatchClient batchClient = await BatchClient.OpenAsync(credentials))
{
    //set up pool specification and information along with resource files here
    JobManagerTask jobManagerTask = new JobManagerTask()
    {
        ResourceFiles = jobManagerResourceFiles,
        CommandLine = Constants.JobManagerExecutable,

        //Determines if the job should terminate when the job manager process exits.
        KillJobOnCompletion = true,
        Id = jobManagerTaskId
    };

    string jobId = Environment.GetEnvironmentVariable("USERNAME") + DateTime.UtcNow.ToString("yyyyMMdd-HHmmss");

    CloudJob unboundJob = batchClient.JobOperations.CreateJob(jobId, poolInformation);
    unboundJob.JobManagerTask = jobManagerTask;

    // now interact with the job ...
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9126b-120">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="9126b-120">Explore the client APIs</span></span>](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a><span data-ttu-id="9126b-121">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="9126b-121">Management library</span></span>

<span data-ttu-id="9126b-122">Use la biblioteca de administración para administrar cuentas, cuotas y paquetes de aplicación de Batch mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9126b-122">Use the management library to programmatically manage Batch accounts, quotas, and application packages.</span></span>

<span data-ttu-id="9126b-123">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="9126b-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="9126b-124">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9126b-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a><span data-ttu-id="9126b-125">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="9126b-125">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a><span data-ttu-id="9126b-126">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="9126b-126">Example</span></span>

<span data-ttu-id="9126b-127">En el ejemplo siguiente se recupera la cuota de la suscripción, se crea una cuenta y se vuelve a generar la clave de cuenta principal.</span><span class="sxs-lookup"><span data-stu-id="9126b-127">The following example retrieves the quota for the subscription, creates an account, and regenerates the primary account key.</span></span>

```csharp
/*
using Microsoft.Azure.Management.Batch;
using Microsoft.Azure.Management.Batch.Models;
using Microsoft.Rest;
*/
using (BatchManagementClient batchManagementClient = new BatchManagementClient(new TokenCredentials(accessToken)))
{
    batchManagementClient.SubscriptionId = subscriptionId;

    // Get the account quota for the subscription
    BatchLocationQuota quotaResponse = await batchManagementClient.Location.GetQuotasAsync(location);
    Console.WriteLine("Your subscription can create {0} account(s) in the {1} region.", quotaResponse.AccountQuota, location);

    // Create account
    await batchManagementClient.BatchAccount.CreateAsync(ResourceGroupName, accountName, 
        new BatchAccountCreateParameters() { Location = location });

    // Regenerate primary account key
    BatchAccountKeys newKeys = await batchManagementClient.BatchAccount.RegenerateKeyAsync(
        ResourceGroupName, account.Name, AccountKeyType.Primary);
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9126b-128">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="9126b-128">Explore the management APIs</span></span>](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a><span data-ttu-id="9126b-129">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="9126b-129">Samples</span></span>

* [<span data-ttu-id="9126b-130">Ejemplos de SDK de cliente y administración de Azure Batch para .NET</span><span class="sxs-lookup"><span data-stu-id="9126b-130">Azure Batch Client and Management SDK for .NET Samples</span></span>](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

<span data-ttu-id="9126b-131">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9126b-131">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
