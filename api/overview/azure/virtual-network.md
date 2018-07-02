---
title: Bibliotecas de Azure Virtual Network para .NET
description: Referencia de las bibliotecas de Azure Virtual Network para .NET
keywords: Azure, .NET, SDK, API, Virtual Network
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: virtual-network
ms.custom: devcenter, svc-overview
ms.openlocfilehash: eb2300522e63339386bf08b5dfac3b803a1e5efd
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065295"
---
# <a name="azure-virtual-network-libraries-for-net"></a>Bibliotecas de Azure Virtual Network para .NET

## <a name="overview"></a>Información general
El servicio [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) le permite conectar de forma segura los recursos de Azure con redes virtuales. Una red virtual es una representación de su propia red en la nube. Puede conectar redes virtuales entre sí para que los recursos conectados a cualquiera de las redes virtuales se comuniquen entre sí. 

## <a name="management-library"></a>Biblioteca de administración

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a>Ejemplo de código
En este ejemplo se muestra cómo crear una nueva red virtual.

```csharp
/* 
  Include these "using" directives...
  
  using Microsoft.Azure.Management.Network.Fluent;
  using Microsoft.Azure.Management.Network.Fluent.Models;
*/
using (NetworkManagementClient client = new NetworkManagementClient(credentials))
{
    // Define VNet
    VirtualNetworkInner vnet = new VirtualNetworkInner()
    {
        Location = "West US",
        AddressSpace = new AddressSpace()
        {
            AddressPrefixes = new List<string>() { "0.0.0.0/16" }
        },

        DhcpOptions = new DhcpOptions()
        {
            DnsServers = new List<string>() { "1.1.1.1", "1.1.2.4" }
        },

        Subnets = new List<Subnet>()
        {
            new Subnet()
            {
                Name = subnet1Name,
                AddressPrefix = "1.0.1.0/24",
            },
            new Subnet()
            {
                Name = subnet2Name,
               AddressPrefix = "1.0.2.0/24",
            }
        }
    };
    
    await client.VirtualNetworks.CreateOrUpdateAsync(resourceGroupName, vNetName, vnet);
}

```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a>Ejemplos
- [Administración de redes virtuales con subredes](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

Explore más [código de ejemplo de .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

