---
title: Bibliotecas de Azure Virtual Network para .NET
description: Referencia de las bibliotecas de Azure Virtual Network para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: virtual-network
ms.openlocfilehash: 54dd79cf0f5bed1eab7b606b8a6e3b30c797ecd0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190668"
---
# <a name="azure-virtual-network-libraries-for-net"></a><span data-ttu-id="0e0ea-103">Bibliotecas de Azure Virtual Network para .NET</span><span class="sxs-lookup"><span data-stu-id="0e0ea-103">Azure Virtual Network libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0e0ea-104">Información general</span><span class="sxs-lookup"><span data-stu-id="0e0ea-104">Overview</span></span>
<span data-ttu-id="0e0ea-105">El servicio [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) le permite conectar de forma segura los recursos de Azure con redes virtuales.</span><span class="sxs-lookup"><span data-stu-id="0e0ea-105">The [Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) service enables you to securely connect Azure resources to each other with virtual networks (VNets).</span></span> <span data-ttu-id="0e0ea-106">Una red virtual es una representación de su propia red en la nube.</span><span class="sxs-lookup"><span data-stu-id="0e0ea-106">A VNet is a representation of your own network in the cloud.</span></span> <span data-ttu-id="0e0ea-107">Puede conectar redes virtuales entre sí para que los recursos conectados a cualquiera de las redes virtuales se comuniquen entre sí.</span><span class="sxs-lookup"><span data-stu-id="0e0ea-107">You can also connect VNets to each other, enabling resources connected to either VNet to communicate with each other.</span></span> 

## <a name="management-library"></a><span data-ttu-id="0e0ea-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="0e0ea-108">Management library</span></span>

<span data-ttu-id="0e0ea-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0e0ea-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0e0ea-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0e0ea-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Network.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="0e0ea-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="0e0ea-111">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Network.Fluent
```

### <a name="code-example"></a><span data-ttu-id="0e0ea-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0e0ea-112">Code Example</span></span>
<span data-ttu-id="0e0ea-113">En este ejemplo se muestra cómo crear una nueva red virtual.</span><span class="sxs-lookup"><span data-stu-id="0e0ea-113">This example shows how you can create a virtual network.</span></span>

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
> [<span data-ttu-id="0e0ea-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="0e0ea-114">Explore the management APIs</span></span>](/dotnet/api/overview/azure/network/management)

## <a name="samples"></a><span data-ttu-id="0e0ea-115">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="0e0ea-115">Samples</span></span>
- [<span data-ttu-id="0e0ea-116">Administración de redes virtuales con subredes</span><span class="sxs-lookup"><span data-stu-id="0e0ea-116">Managing Virtual Networks with subnets</span></span>](https://github.com/Azure-Samples/network-dotnet-manage-virtual-network)

<span data-ttu-id="0e0ea-117">Explore más [código de ejemplo de .NET](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="0e0ea-117">Explore more [.NET sample code](https://azure.microsoft.com/resources/samples/?platform=dotnet) that you can use in your apps.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console 
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package 

