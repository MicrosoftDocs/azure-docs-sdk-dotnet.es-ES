---
title: Bibliotecas de Azure Batch para .NET
description: Referencia de las bibliotecas de Azure Batch para .NET
keywords: Azure, .NET, SDK, API, Batch
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/01/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 753721d430de0577c0bc1dd3774d728783a3bfee
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-batch-libraries-for-net"></a>Bibliotecas de Azure Batch para .NET

Azure Batch es un servicio de plataforma para ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento (HPC) de manera eficaz en la nube. Azure Batch programa el trabajo que conlleva mucho proceso para que se ejecute en una colección administrada de máquinas virtuales y puede escalar automáticamente los recursos de proceso para satisfacer las necesidades de sus trabajos.

Con Azure Batch, se pueden definir fácilmente los recursos de proceso de Azure para ejecutar las aplicaciones en paralelo y a escala. No es preciso crear, configurar ni administrar manualmente un clúster de HPC, máquinas virtuales individuales, redes virtuales ni una infraestructura compleja de programación de tareas y trabajos. Azure Batch automatiza o simplifica estas tareas automáticamente.

Lea más acerca de cómo [ejecutar cargas de trabajo en paralelo de manera intrínseca con Batch](/azure/batch/batch-technical-overview). También puede aprender sobre cómo [comenzar a crear soluciones con la biblioteca de cliente de Batch para .NET](/azure/batch/batch-dotnet-get-started). Descubra cómo [administrar cuentas y cuotas de Batch con la biblioteca de administración de Batch para .NET](/azure/batch/batch-management-dotnet).

## <a name="client-library"></a>Biblioteca de cliente

Use la biblioteca de cliente para ejecutar cargas de trabajo paralelas con Batch.

Instale el [paquete NuGet](https://www.nuget.org/packages/Azure.Batch) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Azure.Batch
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Azure.Batch
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se usa el SDK de cliente para crear un trabajo y ejecutarlo en Azure Batch.

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/batch/client)

## <a name="management-library"></a>Biblioteca de administración

Use la biblioteca de administración para administrar cuentas, cuotas y paquetes de aplicación de Batch mediante programación.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Batch) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Batch
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Batch
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se recupera la cuota de la suscripción, se crea una cuenta y se vuelve a generar la clave de cuenta principal.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/batch/management)

## <a name="samples"></a>Muestras

* [Ejemplos de SDK de cliente y administración de Azure Batch para .NET](https://github.com/Azure/azure-batch-samples/tree/master/CSharp)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
