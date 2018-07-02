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
# <a name="azure-virtual-machine-libraries-for-net"></a>Bibliotecas de Azure Virtual Machines para .NET

## <a name="overview"></a>Información general

Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.

Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](https://review.docs.microsoft.com/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-apis"></a>API de administración

Cree, configure y escale horizontalmente máquinas virtuales Windows y Linux de Azure desde código con la API de administración.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Compute.Fluent
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Compute.Fluent
```

### <a name="code-example"></a>Ejemplo de código

Creación de una máquina virtual Windows.

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
> [Explorar las API de administración](https://docs.microsoft.com/dotnet/api/overview/azure/virtualmachines/management?view=azure-dotnet)

### <a name="samples"></a>Ejemplos

* [Creación y administración de máquinas virtuales](/dotnet/azure/dotnet-sdk-azure-virtual-machine-samples)
* [Implementación de una máquina virtual habilitada para SSH con una plantilla con .NET](https://azure.microsoft.com/resources/samples/resource-manager-dotnet-template-deployment/)

Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&term=VM) de ejemplos de máquina virtual.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
