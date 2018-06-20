---
title: Bibliotecas de Azure Stream Analytics para .NET
description: Referencia de las bibliotecas de Azure Stream Analytics para .NET
keywords: Azure, .NET, SDK, API, Stream Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: stream-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 2a5e8b8481548d6cfebc5104eb459f8772f51462
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
ms.locfileid: "23487138"
---
# <a name="azure-stream-analytics-libraries-for-net"></a>Bibliotecas de Azure Stream Analytics para .NET

## <a name="overview"></a>Información general

[Azure Stream Analytics](/azure/stream-analytics/stream-analytics-introduction) es un motor de procesamiento de eventos totalmente administrado que permite configurar cálculos analíticos en tiempo real sobre datos de transmisión. Los datos pueden proceder de dispositivos, sensores, sitios web, fuentes de redes sociales, aplicaciones, sistemas de infraestructura, etc. 

Para más información acerca de Azure Stream Analytics, consulte [Introducción al uso de Azure Stream Analytics: detección de fraudes en tiempo real](/azure/stream-analytics/stream-analytics-real-time-fraud-detection).


## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración de Azure Stream Analytics para crear, iniciar y detener trabajos de Azure Stream Analytics.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.StreamAnalytics) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.StreamAnalytics
```

```bash
dotnet add package Microsoft.Azure.Management.StreamAnalytics
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea una instancia de un cliente de Stream Analytics y se crea un trabajo de streaming.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/streamanalytics/management)


## <a name="samples"></a>Muestras

- [SDK de .NET de administración: configuración y ejecución de trabajos de análisis mediante la API de Azure Stream Analytics para .NET](/azure/stream-analytics/stream-analytics-dotnet-management-sdk)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=stream-analytics) de ejemplos de Azure Stream Analytics.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
