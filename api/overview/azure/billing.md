---
title: Bibliotecas de Azure Billing para .NET
description: Referencia de las bibliotecas de Azure Billing para .NET
keywords: Azure, .NET, SDK, API, Billing
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 8df15d55a80991f29b694f4af06a20514bf20b32
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566086"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="21209-104">Bibliotecas de Azure Billing para .NET</span><span class="sxs-lookup"><span data-stu-id="21209-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="21209-105">Información general</span><span class="sxs-lookup"><span data-stu-id="21209-105">Overview</span></span>

<span data-ttu-id="21209-106">La API de Azure Billing (versión preliminar) proporciona acceso mediante programación a la información de facturación y a las facturas de Azure.</span><span class="sxs-lookup"><span data-stu-id="21209-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="21209-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="21209-107">Management library</span></span>

<span data-ttu-id="21209-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="21209-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="21209-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="21209-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="21209-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="21209-110">Code Example</span></span>

<span data-ttu-id="21209-111">Conectarse a Azure y obtener una lista de facturas.</span><span class="sxs-lookup"><span data-stu-id="21209-111">Connect to Azure and get a list of invoices.</span></span>

```csharp
/* Include these directives
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Billing;
using Microsoft.Azure.Management.Billing.Models;
*/

// Log into Azure
var serviceCreds = ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
var billingClient = new BillingClient(serviceCreds);
billingClient.SubscriptionId = subscriptionId;

// Get list of invoices
billingClient.Invoices.List();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="21209-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="21209-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="21209-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="21209-113">Samples</span></span>

* [<span data-ttu-id="21209-114">API Usage</span><span class="sxs-lookup"><span data-stu-id="21209-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="21209-115">API de RateCard</span><span class="sxs-lookup"><span data-stu-id="21209-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="21209-116">Aplicación web multiinquilino</span><span class="sxs-lookup"><span data-stu-id="21209-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
