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
# <a name="azure-application-insights-libraries-for-net"></a>Bibliotecas de Azure Application Insights para .NET

## <a name="overview"></a>Información general

Application Insights es un servicio de supervisión y diagnóstico extensible para los desarrolladores de web con funcionalidades avanzadas de análisis ad hoc. Puede utilizar las clases en el espacio de nombres ApplicationInsights para configurar la recopilación de datos de telemetría y enviar datos de telemetría personalizados desde las aplicaciones que desea supervisar.

## <a name="client-library"></a>Biblioteca de cliente

El SDK de cliente de Application Insights para .NET permite registrar eventos, datos agregados, excepciones, dependencias y métricas en Azure para su posterior análisis.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.ApplicationInsights ) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.ApplicationInsights 
```

```bash
dotnet add package Microsoft.ApplicationInsights 
```

### <a name="example"></a>Ejemplo

En este ejemplo se realiza un seguimiento de un evento personalizado para Application Insights.

```csharp
TelemetryClient client = new TelemetryClient();
client.TrackEvent("MyCustomEvent");
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/insights/client)



## <a name="samples"></a>Muestras

- [Application Insights Analytics con OpenSchema](https://azure.microsoft.com/resources/samples/guidance-appinsights-openschema/)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?service=application-insights&platform=dotnet) de ejemplos de Azure Application Insights.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
