---
title: Bibliotecas de Azure Compute para .NET
description: Referencia de las bibliotecas Azure Compute para .NET
keywords: Azure, .NET, SDK, API, VM, máquinas virtuales, Compute
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 96aabe0953a44b86da9cfd3202c43a4aa0f08a89
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065855"
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="16103-104">Bibliotecas de Azure Virtual Machines para .NET</span><span class="sxs-lookup"><span data-stu-id="16103-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="16103-105">Información general</span><span class="sxs-lookup"><span data-stu-id="16103-105">Overview</span></span>

<span data-ttu-id="16103-106">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="16103-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="16103-107">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="16103-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="16103-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="16103-108">Management APIs</span></span>

<span data-ttu-id="16103-109">Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="16103-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="16103-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="16103-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="16103-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="16103-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="16103-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="16103-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="16103-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="16103-113">Code Example</span></span>

<span data-ttu-id="16103-114">Creación de una máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="16103-114">Create a Windows VM.</span></span>

```csharp
/* Include these "using" directives...
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

IVirtualMachine windowsVM = azure.VirtualMachines.Define("MyVirtualMachine")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("MyResourceGroup")
    .WithNewPrimaryNetwork("10.0.0.0/28")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithNewPrimaryPublicIPAddress("MyIPAddressLabel")
    .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
    .WithAdminUsername("UserName")
    .WithAdminPassword("Password")
    .WithSize(VirtualMachineSizeTypes.StandardD3V2)
    .Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="16103-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="16103-115">Explore the management APIs</span></span>](https://docs.microsoft.com/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="16103-116">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="16103-116">Samples</span></span>

* [<span data-ttu-id="16103-117">Creación y administración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="16103-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [<span data-ttu-id="16103-118">Implementación de una máquina virtual habilitada para SSH con una plantilla con .NET</span><span class="sxs-lookup"><span data-stu-id="16103-118">Deploy an SSH-enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/resources/samples/resource-manager-dotnet-template-deployment/)

<span data-ttu-id="16103-119">Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) de ejemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="16103-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
