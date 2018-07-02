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
# <a name="azure-dns-libraries-for-net"></a>Bibliotecas de Azure DNS para .NET

Use las bibliotecas de Microsoft Azure DNS para .NET para crear y modificar las zonas DNS y los registros que se hospedan en Azure. Las zonas y registros se administran como recursos de Azure. Para más información, lea la [Introducción a Azure DNS](/azure/dns/dns-overview).

## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración para crear y modificar las zonas DNS y los registros que se hospedan en Azure.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Dns) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Dns
```

```bash
dotnet add package Microsoft.Azure.Management.Dns
```

### <a name="example"></a>Ejemplo

En el siguiente ejemplo se crea una nueva zona DNS.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/dns/management)

## <a name="samples"></a>Ejemplos

* [Proyecto de ejemplo del SDK de .NET de Azure DNS](https://www.microsoft.com/download/details.aspx?id=47268)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
