---
title: Azure Recovery Services y las bibliotecas de Backup para .NET
description: Referencia de Azure Recovery Services y las bibliotecas de Backup para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: recovery-services
ms.openlocfilehash: c0381ce9a566b5371faca24307edc7b26174e785
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190805"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="74ebb-103">Azure Recovery Services y las bibliotecas de Backup para .NET</span><span class="sxs-lookup"><span data-stu-id="74ebb-103">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="74ebb-104">Información general</span><span class="sxs-lookup"><span data-stu-id="74ebb-104">Overview</span></span>

<span data-ttu-id="74ebb-105">Azure Recovery Services es un conjunto de servicios de recuperación de datos, incluidos [Azure Backup](/azure/backup/) y [Azure Site Recovery](/azure/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="74ebb-105">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="74ebb-106">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="74ebb-106">Management library</span></span>

<span data-ttu-id="74ebb-107">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="74ebb-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="74ebb-108">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="74ebb-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="74ebb-109">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="74ebb-109">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="74ebb-110">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="74ebb-110">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="74ebb-111">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="74ebb-111">Code Example</span></span>

<span data-ttu-id="74ebb-112">En el código de ejemplo siguiente se utiliza la biblioteca de administración para desencadenar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="74ebb-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
