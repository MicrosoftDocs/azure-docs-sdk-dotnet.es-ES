---
title: Bibliotecas de Azure Service Bus para .NET
description: Referencia de las bibliotecas de Azure Service Bus para .NET
keywords: Azure, .NET, SDK, API, Service Bus
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: service-bus
ms.custom: devcenter, svc-overview
ms.openlocfilehash: c2019fd39f42f9bc4a39dd4e642db9f90b7a917c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="azure-service-bus-libraries-for-net"></a>Bibliotecas de Azure Service Bus para .NET

## <a name="overview"></a>Información general

[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) es una infraestructura de mensajería que se encuentra entre las aplicaciones que les permite intercambiar mensajes para mejorar el escalado y la resistencia.

## <a name="client-library"></a>Biblioteca de cliente

Instale el [paquete NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio.

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package WindowsAzure.ServiceBus
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se envía un mensaje a una cola de Service Bus.

```csharp
// using Microsoft.ServiceBus.Messaging;

QueueClient client = QueueClient.CreateFromConnectionString(connectionString, queueName);
BrokeredMessage message = new BrokeredMessage("This is a test message!");
client.Send(message);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a>Biblioteca de administración

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea una cola de Service Bus con un tamaño máximo de 1024 MB.

```csharp
// using Microsoft.Azure.Management.ServiceBus.Fluent;
// using Microsoft.Azure.Management.ServiceBus.Fluent.Models;

using (ServiceBusManagementClient client = new ServiceBusManagementClient(credentials))
{
    client.SubscriptionId = subscriptionId;
    QueueInner parameters = new QueueInner
    {
        MaxSizeInMegabytes = 1024
    };
    await client.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, queueName, parameters);
}
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a>Muestras

- [Conceptos básicos de la cola de Service Bus - .NET](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [Características avanzadas de la cola de Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [Conceptos básicos de publicación y suscripción de Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [Características avanzadas de publicación y suscripción de Service Bus - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [Service Bus con la autorización basada en notificaciones - .Net](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?term=service+bus) de ejemplos de Azure Service Bus.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
