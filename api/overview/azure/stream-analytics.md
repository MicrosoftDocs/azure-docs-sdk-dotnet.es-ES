---
title: Bibliotecas de Azure Stream Analytics para .NET
description: Referencia de las bibliotecas de Azure Stream Analytics para .NET
keywords: Azure, .NET, SDK, API, Stream Analytics
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: b812f0948b2153d717987fbc6912ed4665154b3f
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-stream-analytics-libraries-for-net"></a><span data-ttu-id="49385-104">Bibliotecas de Azure Stream Analytics para .NET</span><span class="sxs-lookup"><span data-stu-id="49385-104">Azure Stream Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="49385-105">Información general</span><span class="sxs-lookup"><span data-stu-id="49385-105">Overview</span></span>

<span data-ttu-id="49385-106">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) es un motor de procesamiento de eventos totalmente administrado que permite configurar cálculos analíticos en tiempo real sobre datos de transmisión.</span><span class="sxs-lookup"><span data-stu-id="49385-106">[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) is a fully managed event-processing engine that lets you set up real-time analytic computations on streaming data.</span></span> <span data-ttu-id="49385-107">Los datos pueden proceder de dispositivos, sensores, sitios web, fuentes de redes sociales, aplicaciones, sistemas de infraestructura, etc.</span><span class="sxs-lookup"><span data-stu-id="49385-107">The data can come from devices, sensors, web sites, social media feeds, applications, infrastructure systems, and more.</span></span> 

<span data-ttu-id="49385-108">Para más información acerca de Azure Stream Analytics, consulte [Introducción al uso de Azure Stream Analytics: detección de fraudes en tiempo real](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span><span class="sxs-lookup"><span data-stu-id="49385-108">To learn more about Azure Stream Analytics, see [Get started with Azure Stream Analytics Real-time fraud detection](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).</span></span>


## <a name="management-library"></a><span data-ttu-id="49385-109">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="49385-109">Management library</span></span>

<span data-ttu-id="49385-110">Utilice la biblioteca de administración de Azure Stream Analytics para crear, iniciar y detener trabajos de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="49385-110">Use the Azure Stream Analytics management library to create, start, and stop Azure Stream Analytics jobs.</span></span>

<span data-ttu-id="49385-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="49385-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="49385-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="49385-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a><span data-ttu-id="49385-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="49385-113">Code Example</span></span>

<span data-ttu-id="49385-114">En este ejemplo se crea una instancia de un cliente de Stream Analytics y se crea un trabajo de streaming.</span><span class="sxs-lookup"><span data-stu-id="49385-114">This example instantiates a Stream Analytics client and creates a streaming job.</span></span>

```csharp
/* Include these 'using' directives:
using Microsoft.Azure.Management.StreamAnalytics;
*/
SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

// Get credentials
ServiceClientCredentials credentials = GetCredentials().Result;

// Create Stream Analytics management client
StreamAnalyticsManagementClient streamAnalyticsManagementClient = new StreamAnalyticsManagementClient(credentials)
{
    SubscriptionId = subscriptionId
};

// Create a streaming job
StreamingJob streamingJob = new StreamingJob()
{
    Tags = new Dictionary<string, string>()
    {
        { "Origin", ".NET SDK" },
        { "ReasonCreated", "Getting started tutorial" }
    },
    Location = "West US",
    EventsOutOfOrderPolicy = EventsOutOfOrderPolicy.Drop,
    EventsOutOfOrderMaxDelayInSeconds = 5,
    EventsLateArrivalMaxDelayInSeconds = 16,
    OutputErrorPolicy = OutputErrorPolicy.Drop,
    DataLocale = "en-US",
    CompatibilityLevel = CompatibilityLevel.OneFullStopZero,
    Sku = new Sku()
    {
        Name = SkuName.Standard
    }
};
StreamingJob createStreamingJobResult = streamAnalyticsManagementClient.StreamingJobs.CreateOrReplace(streamingJob, resourceGroupName, streamingJobName);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="49385-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="49385-115">Explore the management APIs</span></span>](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a><span data-ttu-id="49385-116">Muestras</span><span class="sxs-lookup"><span data-stu-id="49385-116">Samples</span></span>

- [<span data-ttu-id="49385-117">SDK de .NET de administración: configuración y ejecución de trabajos de análisis mediante la API de Azure Stream Analytics para .NET</span><span class="sxs-lookup"><span data-stu-id="49385-117">Management .NET SDK: Set up and run analytics jobs using the Azure Stream Analytics API for .NET</span></span>](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

<span data-ttu-id="49385-118">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) de ejemplos de Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="49385-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) of Azure Stream Analytics samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
