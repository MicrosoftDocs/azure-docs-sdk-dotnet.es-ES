---
title: Azure Recovery Services y las bibliotecas de Backup para .NET
description: Referencia de Azure Recovery Services y las bibliotecas de Backup para .NET
keywords: Azure, .NET, SDK, API, Recovery Services, Backup
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: recovery-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6186411b668d0950328b49bb826e5b05c5ee0304
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065435"
---
# <a name="azure-recovery-services-and-backup-libraries-for-net"></a><span data-ttu-id="0ee24-104">Azure Recovery Services y las bibliotecas de Backup para .NET</span><span class="sxs-lookup"><span data-stu-id="0ee24-104">Azure Recovery Services and Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="0ee24-105">Información general</span><span class="sxs-lookup"><span data-stu-id="0ee24-105">Overview</span></span>

<span data-ttu-id="0ee24-106">Azure Recovery Services es un conjunto de servicios de recuperación de datos, incluidos [Azure Backup](/azure/backup/) y [Azure Site Recovery](/azure/site-recovery/).</span><span class="sxs-lookup"><span data-stu-id="0ee24-106">Azure Recovery Services is a suite of services for data recovery, including [Azure Backup](/azure/backup/) and [Azure Site Recovery](/azure/site-recovery/).</span></span>

## <a name="management-library"></a><span data-ttu-id="0ee24-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="0ee24-107">Management library</span></span>

<span data-ttu-id="0ee24-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="0ee24-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="0ee24-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0ee24-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

#### <a name="net-core-cli"></a><span data-ttu-id="0ee24-110">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="0ee24-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="0ee24-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="0ee24-111">Explore the management APIs</span></span>](/dotnet/api/overview/azure/recoveryservices/management)


## <a name="code-example"></a><span data-ttu-id="0ee24-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="0ee24-112">Code Example</span></span>

<span data-ttu-id="0ee24-113">En el código de ejemplo siguiente se utiliza la biblioteca de administración para desencadenar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0ee24-113">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
