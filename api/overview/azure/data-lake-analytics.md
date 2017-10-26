---
title: Bibliotecas de Azure Data Lake Analytics para .NET
description: Referencia de las bibliotecas de Azure Data Lake Analytics para .NET
keywords: Azure, .NET, SDK, API, Data Lake Analytics
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-analytics
ms.custom: devcenter, svc-overview
ms.openlocfilehash: aa99608ec5568450a90cc2b93c3f1c5d0e38bfb1
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-data-lake-analytics-libraries-for-net"></a>Bibliotecas de Azure Data Lake Analytics para .NET

## <a name="overview"></a>Información general

Azure Data Lake Analytics es un servicio de trabajos de análisis a petición que simplifica el análisis de macrodatos.

Para más información, consulte [Información general de Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

## <a name="management-library"></a>Biblioteca de administración

Use la biblioteca de administración para conectarse al servicio y administrar trabajos de análisis.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crean los clientes con los que se va a conectar y que administran la cuenta de Analytics.

```csharp
/*
using AdlClient 
*/

// Setup authentication for this demo
Authentication auth = new Authentication("microsoft.onmicrosoft.com"); // change this to YOUR tenant
auth.Authenticate();

// Identify the accounts
AnalyticsAccountRef adla_account = new AnalyticsAccountRef(subscriptionId, resourceGroup, userName);

// Create the clients
AzureClient az = new AzureClient(auth);
AnalyticsClient adla = new AnalyticsClient(auth, adla_account);
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Muestras
* [Ejemplo de cliente de .NET de Azure Data Lake](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
