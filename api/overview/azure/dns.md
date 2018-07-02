---
title: Bibliotecas de Azure DNS para .NET
description: Referencia de las bibliotecas de Azure DNS para .NET
keywords: Azure, .NET, SDK, API, DNS
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: dns
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 0360c4d5a0e276b4adf05d43689896fab6622f51
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065335"
---
# <a name="azure-dns-libraries-for-net"></a><span data-ttu-id="fdd1a-104">Bibliotecas de Azure DNS para .NET</span><span class="sxs-lookup"><span data-stu-id="fdd1a-104">Azure DNS libraries for .NET</span></span>

<span data-ttu-id="fdd1a-105">Use las bibliotecas de Microsoft Azure DNS para .NET para crear y modificar las zonas DNS y los registros que se hospedan en Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd1a-105">Use the Microsoft Azure DNS libraries for .NET to create and modify DNS zones and records hosted within Azure.</span></span> <span data-ttu-id="fdd1a-106">Las zonas y registros se administran como recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd1a-106">Zones and records are managed as Azure Resources.</span></span> <span data-ttu-id="fdd1a-107">Para más información, lea la [Introducción a Azure DNS](/azure/dns/dns-overview).</span><span class="sxs-lookup"><span data-stu-id="fdd1a-107">Learn more by reading the [Azure DNS overview](/azure/dns/dns-overview).</span></span>

## <a name="management-library"></a><span data-ttu-id="fdd1a-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="fdd1a-108">Management library</span></span>

<span data-ttu-id="fdd1a-109">Utilice la biblioteca de administración para crear y modificar las zonas DNS y los registros que se hospedan en Azure.</span><span class="sxs-lookup"><span data-stu-id="fdd1a-109">Use the management library to create and modify DNS zones and records that are hosted in Azure.</span></span>

<span data-ttu-id="fdd1a-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="fdd1a-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="fdd1a-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fdd1a-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a><span data-ttu-id="fdd1a-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="fdd1a-112">Example</span></span>

<span data-ttu-id="fdd1a-113">En el siguiente ejemplo se crea una nueva zona DNS.</span><span class="sxs-lookup"><span data-stu-id="fdd1a-113">The following example creates a new DNS zone.</span></span>

```csharp
/*
using Microsoft.Rest.Azure.Authentication;
using Microsoft.Azure.Management.Dns;
using Microsoft.Azure.Management.Dns.Models;
*/
Microsoft.Rest.ServiceClientCredentials serviceCreds = await ApplicationTokenProvider.LoginSilentAsync(tenantId, clientId, secret);
DnsManagementClient dnsClient = new DnsManagementClient(serviceCreds);            
Zone dnsZoneParams = new Zone("global");
dnsZoneParams.Tags = new Dictionary<string, string>();
dnsZoneParams.Tags.Add("dept", "finance");
Zone dnsZone =
    await dnsClient.Zones.CreateOrUpdateAsync(resourceGroupName, zoneName, dnsZoneParams, null, "*");
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdd1a-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="fdd1a-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a><span data-ttu-id="fdd1a-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="fdd1a-115">Samples</span></span>

* [<span data-ttu-id="fdd1a-116">Proyecto de ejemplo del SDK de .NET de Azure DNS</span><span class="sxs-lookup"><span data-stu-id="fdd1a-116">Azure DNS .NET SDK Sample Project</span></span>](https://www.microsoft.com/download/details.aspx?id=47268)

<span data-ttu-id="fdd1a-117">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="fdd1a-117">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
