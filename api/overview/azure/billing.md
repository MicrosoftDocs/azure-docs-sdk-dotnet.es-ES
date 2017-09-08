---
title: Bibliotecas de Azure Billing para .NET
description: Referencia de las bibliotecas de Azure Billing para .NET
keywords: Azure, .NET, SDK, API, Billing
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 0a401bf9ccc345d3c6e99a010c74f9c7f6f5914e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="0a9fe-104">Bibliotecas de Azure Billing para .NET</span><span class="sxs-lookup"><span data-stu-id="0a9fe-104">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0a9fe-105">Información general</span><span class="sxs-lookup"><span data-stu-id="0a9fe-105">Overview</span></span>

<span data-ttu-id="0a9fe-106">La API de Azure Billing (versión preliminar) proporciona acceso mediante programación a la información de facturación y a las facturas de Azure.</span><span class="sxs-lookup"><span data-stu-id="0a9fe-106">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="0a9fe-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="0a9fe-107">Management library</span></span>

<span data-ttu-id="0a9fe-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0a9fe-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0a9fe-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0a9fe-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="0a9fe-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0a9fe-110">Code Example</span></span>

<span data-ttu-id="0a9fe-111">Conectarse a Azure y obtener una lista de facturas.</span><span class="sxs-lookup"><span data-stu-id="0a9fe-111">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="0a9fe-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="0a9fe-112">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="0a9fe-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="0a9fe-113">Samples</span></span>

* [<span data-ttu-id="0a9fe-114">API Usage</span><span class="sxs-lookup"><span data-stu-id="0a9fe-114">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="0a9fe-115">API de RateCard</span><span class="sxs-lookup"><span data-stu-id="0a9fe-115">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="0a9fe-116">Aplicación web multiinquilino</span><span class="sxs-lookup"><span data-stu-id="0a9fe-116">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
