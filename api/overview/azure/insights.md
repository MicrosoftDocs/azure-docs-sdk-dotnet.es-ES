---
title: Bibliotecas de Azure Application Insights para .NET
description: Referencia de las bibliotecas de Azure Application Insights para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: application-insights
ms.openlocfilehash: 10b65f536c6461959b0be9b8f9bd3ec56a307bea
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190844"
---
# <a name="azure-application-insights-libraries-for-net"></a><span data-ttu-id="8d1a0-103">Bibliotecas de Azure Application Insights para .NET</span><span class="sxs-lookup"><span data-stu-id="8d1a0-103">Azure Application Insights libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="8d1a0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="8d1a0-104">Overview</span></span>

<span data-ttu-id="8d1a0-105">Application Insights es un servicio de supervisión y diagnóstico extensible para los desarrolladores de web con funcionalidades avanzadas de análisis ad hoc.</span><span class="sxs-lookup"><span data-stu-id="8d1a0-105">Application Insights is an extensible monitoring & diagnostics service for web developers with powerful ad-hoc analytics capabilities.</span></span> <span data-ttu-id="8d1a0-106">Puede utilizar las clases en el espacio de nombres ApplicationInsights para configurar la recopilación de datos de telemetría y enviar datos de telemetría personalizados desde las aplicaciones que desea supervisar.</span><span class="sxs-lookup"><span data-stu-id="8d1a0-106">You can use the classes in the ApplicationInsights namespace to configure telemetry collection and send any custom telemetry from your applications that you want to monitor.</span></span>

## <a name="client-library"></a><span data-ttu-id="8d1a0-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="8d1a0-107">Client library</span></span>

<span data-ttu-id="8d1a0-108">El SDK de cliente de Application Insights para .NET permite registrar eventos, datos agregados, excepciones, dependencias y métricas en Azure para su posterior análisis.</span><span class="sxs-lookup"><span data-stu-id="8d1a0-108">The Application Insights client SDK for .NET allows you to log event, aggregated data, exceptions, dependency, and metrics to Azure for future analysis.</span></span>

<span data-ttu-id="8d1a0-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="8d1a0-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="8d1a0-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d1a0-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a><span data-ttu-id="8d1a0-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="8d1a0-111">Example</span></span>

<span data-ttu-id="8d1a0-112">En este ejemplo se realiza un seguimiento de un evento personalizado para Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d1a0-112">This example tracks a custom event to Application Insights.</span></span>

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d1a0-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="8d1a0-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a><span data-ttu-id="8d1a0-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="8d1a0-114">Samples</span></span>

- [<span data-ttu-id="8d1a0-115">Application Insights Analytics con OpenSchema</span><span class="sxs-lookup"><span data-stu-id="8d1a0-115">Application Insights Analytics with OpenSchema</span></span>](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

<span data-ttu-id="8d1a0-116">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) de ejemplos de Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8d1a0-116">View the [complete list](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) of Azure Application Insights samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
