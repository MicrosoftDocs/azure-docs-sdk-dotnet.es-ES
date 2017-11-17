---
title: Bibliotecas de Azure Notification Hubs para .NET
description: Referencia de las bibliotecas de Azure Notification Hubs para .NET
keywords: Azure, .NET, SDK, API, Notification Hubs
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: notification-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 6fe4e3f25aa420322478dc7c10aecd055a70f5c8
ms.sourcegitcommit: 4114b8821f20e02f4185fcea7549d716f29b9c90
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2017
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="db6bd-104">Bibliotecas de Azure Notification Hubs para .NET</span><span class="sxs-lookup"><span data-stu-id="db6bd-104">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="db6bd-105">Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="db6bd-105">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="db6bd-106">Con una única llamada de API multiplataforma puede enviar fácilmente notificaciones push específicas y personalizadas a cualquier plataforma móvil desde cualquier back-end local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="db6bd-106">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="db6bd-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="db6bd-107">Client library</span></span>

<span data-ttu-id="db6bd-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="db6bd-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="db6bd-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db6bd-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="db6bd-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="db6bd-110">Code Example</span></span>

<span data-ttu-id="db6bd-111">En este ejemplo se conecta a una base de datos y se leen las filas de una tabla.</span><span class="sxs-lookup"><span data-stu-id="db6bd-111">This example connects to a database and reads rows from a table.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="db6bd-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="db6bd-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a><span data-ttu-id="db6bd-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="db6bd-113">Management library</span></span>

<span data-ttu-id="db6bd-114">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="db6bd-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="db6bd-115">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db6bd-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="db6bd-116">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="db6bd-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="db6bd-117">Muestras</span><span class="sxs-lookup"><span data-stu-id="db6bd-117">Samples</span></span>

- [<span data-ttu-id="db6bd-118">Introducción a Windows Universal</span><span class="sxs-lookup"><span data-stu-id="db6bd-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
