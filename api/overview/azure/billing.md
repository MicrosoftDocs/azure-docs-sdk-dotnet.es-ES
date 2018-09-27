---
title: Bibliotecas de Azure Billing para .NET
description: Referencia de las bibliotecas de Azure Billing para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: 88b90c71d29eacf61e4da2099f8a054d74df4a83
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190258"
---
# <a name="azure-billing-libraries-for-net"></a><span data-ttu-id="c5d32-103">Bibliotecas de Azure Billing para .NET</span><span class="sxs-lookup"><span data-stu-id="c5d32-103">Azure Billing libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c5d32-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c5d32-104">Overview</span></span>

<span data-ttu-id="c5d32-105">La API de Azure Billing (versión preliminar) proporciona acceso mediante programación a la información de facturación y a las facturas de Azure.</span><span class="sxs-lookup"><span data-stu-id="c5d32-105">Azure Billing API (preview) provides programmatic access to your Azure billing information and invoices.</span></span>

## <a name="management-library"></a><span data-ttu-id="c5d32-106">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="c5d32-106">Management library</span></span>

<span data-ttu-id="c5d32-107">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c5d32-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c5d32-108">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c5d32-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a><span data-ttu-id="c5d32-109">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c5d32-109">Code Example</span></span>

<span data-ttu-id="c5d32-110">Conectarse a Azure y obtener una lista de facturas.</span><span class="sxs-lookup"><span data-stu-id="c5d32-110">Connect to Azure and get a list of invoices.</span></span>

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
> [<span data-ttu-id="c5d32-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="c5d32-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a><span data-ttu-id="c5d32-112">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c5d32-112">Samples</span></span>

* [<span data-ttu-id="c5d32-113">API Usage</span><span class="sxs-lookup"><span data-stu-id="c5d32-113">Usage API</span></span>](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [<span data-ttu-id="c5d32-114">API de RateCard</span><span class="sxs-lookup"><span data-stu-id="c5d32-114">RateCard API</span></span>](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [<span data-ttu-id="c5d32-115">Aplicación web multiinquilino</span><span class="sxs-lookup"><span data-stu-id="c5d32-115">Multi-Tenant Web Application</span></span>](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
