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
# <a name="azure-notification-hubs-libraries-for-net"></a>Bibliotecas de Azure Notification Hubs para .NET

Azure Notification Hubs proporciona un motor de inserción fácil de usar, multiplataforma y escalado horizontalmente. Con una única llamada de API multiplataforma puede enviar fácilmente notificaciones push específicas y personalizadas a cualquier plataforma móvil desde cualquier back-end local o en la nube.

## <a name="client-library"></a>Biblioteca de cliente

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.NotificationHubs
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se conecta a una base de datos y se leen las filas de una tabla.

```csharp
NotificationHubClient hub = NotificationHubClient
                                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
string toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
await hub.SendWindowsNativeNotificationAsync(toast);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/notificationhubs/client)


## <a name="management-library"></a>Biblioteca de administración

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.NotificationHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.NotificationHubs
```

```bash
dotnet add package Microsoft.Azure.Management.NotificationHubs
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/notificationhubs/management)

## <a name="samples"></a>Muestras

- [Introducción a Windows Universal](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package