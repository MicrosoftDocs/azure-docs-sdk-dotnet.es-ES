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
# <a name="azure-data-lake-analytics-libraries-for-net"></a><span data-ttu-id="66eb8-104">Bibliotecas de Azure Data Lake Analytics para .NET</span><span class="sxs-lookup"><span data-stu-id="66eb8-104">Azure Data Lake Analytics libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="66eb8-105">Información general</span><span class="sxs-lookup"><span data-stu-id="66eb8-105">Overview</span></span>

<span data-ttu-id="66eb8-106">Azure Data Lake Analytics es un servicio de trabajos de análisis a petición que simplifica el análisis de macrodatos.</span><span class="sxs-lookup"><span data-stu-id="66eb8-106">Azure Data Lake Analytics is an on-demand analytics job service to simplify big data analytics.</span></span>

<span data-ttu-id="66eb8-107">Para más información, consulte [Información general de Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span><span class="sxs-lookup"><span data-stu-id="66eb8-107">To learn more, see [Overview of Microsoft Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="66eb8-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="66eb8-108">Management library</span></span>

<span data-ttu-id="66eb8-109">Use la biblioteca de administración para conectarse al servicio y administrar trabajos de análisis.</span><span class="sxs-lookup"><span data-stu-id="66eb8-109">Use the management library to connect to the service and manage analytics jobs.</span></span>

<span data-ttu-id="66eb8-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="66eb8-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Analytics) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="66eb8-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="66eb8-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Analytics
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Analytics
```

### <a name="code-example"></a><span data-ttu-id="66eb8-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="66eb8-112">Code Example</span></span>

<span data-ttu-id="66eb8-113">En este ejemplo se crean los clientes con los que se va a conectar y que administran la cuenta de Analytics.</span><span class="sxs-lookup"><span data-stu-id="66eb8-113">This example creates the clients to connect with and manage the analytics account.</span></span>

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
> [<span data-ttu-id="66eb8-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="66eb8-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a><span data-ttu-id="66eb8-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="66eb8-115">Samples</span></span>
* [<span data-ttu-id="66eb8-116">Ejemplo de cliente de .NET de Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="66eb8-116">Azure Data Lake .NET Client Example</span></span>](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

<span data-ttu-id="66eb8-117">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="66eb8-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
