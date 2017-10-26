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
---
# <a name="azure-billing-libraries-for-net"></a>Bibliotecas de Azure Billing para .NET

## <a name="overview"></a>Información general

La API de Azure Billing (versión preliminar) proporciona acceso mediante programación a la información de facturación y a las facturas de Azure.

## <a name="management-library"></a>Biblioteca de administración

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Billing) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Billing
```

```bash
dotnet add package Microsoft.Azure.Management.Billing
```

### <a name="code-example"></a>Ejemplo de código

Conectarse a Azure y obtener una lista de facturas.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/billing/management)

## <a name="samples"></a>Muestras

* [API Usage](https://github.com/Azure-Samples/billing-dotnet-usage-api)
* [API de RateCard](https://github.com/Azure-Samples/billing-dotnet-ratecard-api)
* [Aplicación web multiinquilino](https://github.com/Azure-Samples/billing-dotnet-webapp-multitenant)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
