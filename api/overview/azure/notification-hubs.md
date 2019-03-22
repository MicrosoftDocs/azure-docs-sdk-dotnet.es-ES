---
title: Bibliotecas de Azure Notification Hubs para .NET
description: Referencia de las bibliotecas de Azure Notification Hubs para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: notification-hubs
ms.openlocfilehash: 750a51e8dfa7323f6afb54735b4bfc517f9ec15f
ms.sourcegitcommit: 4b68c73652cb7e44cf4db36f70cb33a17dd863ce
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "58085842"
---
# <a name="azure-notification-hubs-libraries-for-net"></a><span data-ttu-id="a5506-103">Bibliotecas de Azure Notification Hubs para .NET</span><span class="sxs-lookup"><span data-stu-id="a5506-103">Azure Notification Hubs libraries for .NET</span></span>

<span data-ttu-id="a5506-104">Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="a5506-104">Azure Notification Hubs provide an easy-to-use, multi-platform, scaled-out push engine.</span></span> <span data-ttu-id="a5506-105">Con una única llamada de API multiplataforma puede enviar fácilmente notificaciones push específicas y personalizadas a cualquier plataforma móvil desde cualquier back-end local o en la nube.</span><span class="sxs-lookup"><span data-stu-id="a5506-105">With a single cross-platform API call, you can easily send targeted and personalized push notifications to any mobile platform from any cloud or on-premises backend.</span></span>

## <a name="client-library"></a><span data-ttu-id="a5506-106">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a5506-106">Client library</span></span>

<span data-ttu-id="a5506-107">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a5506-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

> [!NOTE]
> <span data-ttu-id="a5506-108">El [paquete NuGet de Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) ahora es compatible con .NET Standard, que permite utilizar .NET Core para el uso de back-end de Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="a5506-108">The [Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) now supports .NET Standard, which allows using .NET core for backend use of Notifications Hubs</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a5506-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5506-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a><span data-ttu-id="a5506-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="a5506-110">Code Example</span></span>

<span data-ttu-id="a5506-111">En este ejemplo se conecta a Centro de notificaciones y se envía un mensaje de Servicios de notificaciones de inserción de Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="a5506-111">This example connects to a Notification Hub and sends a Windows Push Notification Service (WNS) message.</span></span>

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5506-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="a5506-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/client)

## <a name="management-library"></a><span data-ttu-id="a5506-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="a5506-113">Management library</span></span>

<span data-ttu-id="a5506-114">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a5506-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a5506-115">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a5506-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a5506-116">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a5506-116">Explore the management APIs</span></span>](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a><span data-ttu-id="a5506-117">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a5506-117">Samples</span></span>

- [<span data-ttu-id="a5506-118">Introducción a Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a5506-118">Getting Started with Windows Universal</span></span>](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
