---
title: Bibliotecas de Azure Application Insights para .NET
description: Referencia de las bibliotecas de Azure Application Insights para .NET
keywords: Azure, .NET, SDK, API, Application Insights
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: application-insights
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 081143eafaeea2954703c337609a67fd5a7941c6
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="10c07-104">Bibliotecas de Azure Application Insights para .NET</span><span class="sxs-lookup"><span data-stu-id="10c07-104">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="10c07-105">Información general</span><span class="sxs-lookup"><span data-stu-id="10c07-105">Overview</span></span>

<span data-ttu-id="10c07-106">Application Insights es un servicio de supervisión y diagnóstico extensible para los desarrolladores de web con funcionalidades avanzadas de análisis ad hoc.</span><span class="sxs-lookup"><span data-stu-id="10c07-106">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="10c07-107">Puede utilizar las clases en el espacio de nombres ApplicationInsights para configurar la recopilación de datos de telemetría y enviar datos de telemetría personalizados desde las aplicaciones que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="10c07-107">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="10c07-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="10c07-108">Client library</span></span>

<span data-ttu-id="10c07-109">El SDK de cliente de Application Insights para .NET permite registrar eventos, datos agregados, excepciones, dependencias y métricas en Azure para su posterior análisis.</span><span class="sxs-lookup"><span data-stu-id="10c07-109">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="10c07-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="10c07-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="10c07-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="10c07-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="10c07-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="10c07-112">Example</span></span>

<span data-ttu-id="10c07-113">En este ejemplo se realiza un seguimiento de un evento personalizado para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="10c07-113">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="10c07-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="10c07-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="10c07-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="10c07-115">Samples</span></span>

- [<span data-ttu-id="10c07-116">Application Insights Analytics con OpenSchema</span><span class="sxs-lookup"><span data-stu-id="10c07-116">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="10c07-117">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) de ejemplos de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="10c07-117">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
