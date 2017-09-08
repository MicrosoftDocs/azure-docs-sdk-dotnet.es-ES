---
title: Bibliotecas de Azure Compute para .NET
description: Referencia de las bibliotecas Azure Compute para .NET
keywords: "Azure, .NET, SDK, API, VM, máquinas virtuales, Compute"
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: b30c1433b8f25941fc1d4ea4718aa07c0a870580
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-virtual-machine-libraries-for-net"></a><span data-ttu-id="2e03f-104">Bibliotecas de Azure Virtual Machines para .NET</span><span class="sxs-lookup"><span data-stu-id="2e03f-104">Azure virtual machine libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="2e03f-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2e03f-105">Overview</span></span>

<span data-ttu-id="2e03f-106">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="2e03f-106">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="2e03f-107">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="2e03f-107">To get started with Azure virtual machines, see [Create a Linux virtual machine with the Azure portal](https://review.docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="2e03f-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="2e03f-108">Management APIs</span></span>

<span data-ttu-id="2e03f-109">Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="2e03f-109">Create, configure, and scale out Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="2e03f-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="2e03f-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="2e03f-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2e03f-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="2e03f-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="2e03f-112">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a><span data-ttu-id="2e03f-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="2e03f-113">Code Example</span></span>

<span data-ttu-id="2e03f-114">Creación de una máquina virtual Windows.</span><span class="sxs-lookup"><span data-stu-id="2e03f-114">Create a Windows VM.</span></span>

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
> [<span data-ttu-id="2e03f-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="2e03f-115">Explore the management APIs</span></span>](https://review.docs.microsoft.com/en-us/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a><span data-ttu-id="2e03f-116">Muestras</span><span class="sxs-lookup"><span data-stu-id="2e03f-116">Samples</span></span>

* [<span data-ttu-id="2e03f-117">Creación y administración de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="2e03f-117">Create and manage virtual machines</span></span>](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [<span data-ttu-id="2e03f-118">Implementación de una máquina virtual habilitada para SSH con una plantilla con .NET</span><span class="sxs-lookup"><span data-stu-id="2e03f-118">Deploy an SSH-enabled VM with a Template with .NET</span></span>](https://azure.microsoft.com/en-us/resources/samples/resource-manager-dotnet-template-deployment/)

<span data-ttu-id="2e03f-119">Ver el [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) de ejemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2e03f-119">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=VM) of virtual machine samples.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
