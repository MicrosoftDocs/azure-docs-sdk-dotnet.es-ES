---
title: Bibliotecas de Azure Backup para .NET
description: Referencia de las bibliotecas de Azure Backup para .NET
keywords: Azure, .NET, SDK, API, Backup
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/24/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 93eeaeda1860e3b7190dfb0ae917b4b85b5a3609
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-backup-libraries-for-net"></a><span data-ttu-id="4a809-104">Bibliotecas de Azure Backup para .NET</span><span class="sxs-lookup"><span data-stu-id="4a809-104">Azure Backup libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4a809-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4a809-105">Overview</span></span>

<span data-ttu-id="4a809-106">Azure Backup es un servicio en la nube que se puede usar para realizar copias de seguridad, proteger y restaurar datos.</span><span class="sxs-lookup"><span data-stu-id="4a809-106">Azure Backup is the cloud service you can use to back up, protect, and restore your data.</span></span>

<span data-ttu-id="4a809-107">Para más información acerca de Azure Backup, consulte [Introducción a las características de Azure Backup](/azure/backup/backup-introduction-to-azure-backup).</span><span class="sxs-lookup"><span data-stu-id="4a809-107">Learn more about Azure Backup by reading [What is Azure Backup?](/azure/backup/backup-introduction-to-azure-backup).</span></span>

## <a name="management-library"></a><span data-ttu-id="4a809-108">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="4a809-108">Management library</span></span>

<span data-ttu-id="4a809-109">Utilice la biblioteca de administración de Backup para administrar las copias de seguridad y configurar los almacenes de Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="4a809-109">Use the backup management library to manage backups and set up Recovery Services vaults.</span></span>

<span data-ttu-id="4a809-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="4a809-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.RecoveryServices.Backup) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4a809-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a809-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.RecoveryServices.Backup
```

```bash
dotnet add package Microsoft.Azure.Management.RecoveryServices.Backup
```

<span data-ttu-id="4a809-112">En el código de ejemplo siguiente se utiliza la biblioteca de administración para desencadenar una copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4a809-112">The following code example uses the management library to trigger a backup.</span></span>

```csharp
RecoveryServicesBackupManagementClient client = new RecoveryServicesBackupManagementClient(credentials);
TriggerBackupRequest triggerBackupRequest = new TriggerBackupRequest();
BaseRecoveryServicesJobResponse resp =
    await client.Backups.TriggerBackupAsync(resourceGroupName, resourceName, null,
        fabricName, containerName, protectedItemName, triggerBackupRequest);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a809-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="4a809-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/backup/management)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
