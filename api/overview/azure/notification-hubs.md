---
title: Bibliotecas de Azure Notification Hubs para .NET
description: Referencia de las bibliotecas de Azure Notification Hubs para .NET
keywords: Azure, .NET, SDK, API, Notification Hubs
author: camsoper
ms.author: casoper
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 630cdd465fdf6c77ad5d46d9f231c3f331467587
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="e7709-104">Bibliotecas de Azure Notification Hubs para .NET</span><span class="sxs-lookup"><span data-stu-id="e7709-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="e7709-105">Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="e7709-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="e7709-106">Con una única llamada de API multiplataforma puede enviar fácilmente notificaciones push específicas y personalizadas a cualquier plataforma móvil desde cualquier back-end local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="e7709-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="e7709-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="e7709-107">Client library</span></span>

<span data-ttu-id="e7709-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e7709-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e7709-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7709-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="e7709-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="e7709-110">Code Example</span></span>

<span data-ttu-id="e7709-111">En este ejemplo se conecta a una base de datos y se leen las filas de una tabla.</span><span class="sxs-lookup"><span data-stu-id="e7709-111">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7709-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="e7709-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="e7709-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="e7709-113">Management library</span></span>

<span data-ttu-id="e7709-114">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="e7709-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="e7709-115">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e7709-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e7709-116">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="e7709-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="e7709-117">Muestras</span><span class="sxs-lookup"><span data-stu-id="e7709-117">Samples</span></span>

- [<span data-ttu-id="e7709-118">Introducción a Windows Universal</span><span class="sxs-lookup"><span data-stu-id="e7709-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
