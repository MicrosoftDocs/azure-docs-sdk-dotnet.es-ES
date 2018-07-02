---
title: Bibliotecas de Azure Event Hubs para .NET
description: Referencia de las bibliotecas de Azure Event Hubs para .NET
keywords: Azure, .NET, SDK, API, Event Hubs
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: event-hubs
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 5502ae24574c7883c34522ae18ca81bb516a33d2
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065315"
---
# <a name="azure-event-hubs-libraries-for-net"></a>Bibliotecas de Azure Event Hubs para .NET

## <a name="overview"></a>Información general

Azure Event Hubs es una plataforma de streaming de datos muy escalable y un servicio de ingesta de eventos.

Para más información acerca de Azure Event Hubs, lea el artículo [¿Qué es Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).  Para empezar, consulte la [Guía de programación de Event Hubs](/azure/event-hubs/event-hubs-programming-guide).

## <a name="client-library"></a>Biblioteca de cliente

Use al cliente de Event Hubs tanto para enviar mensajes a Event Hubs como para recibirlos de este.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a>Ejemplo de código

El código siguiente crea a un cliente de Event Hubs y envía un mensaje al centro.

```csharp
EventHubsConnectionStringBuilder connectionStringBuilder = new EventHubsConnectionStringBuilder(eventHubConnectionString)
{
    EntityPath = eventHubEntityPath
};

EventHubClient eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
string message = $"Message {i}";
Console.WriteLine($"Sending message: {message}");
await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración de Event Hubs para crear, actualizar y quitar centros y los grupos de consumidores.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a>Ejemplo de código

El siguiente código crea un centro de eventos nuevo.

```csharp
TokenCredentials creds = new TokenCredentials(token);
EventHubManagementClient ehClient = new EventHubManagementClient(creds)
{
    SubscriptionId = subscriptionId
};

EventHubCreateOrUpdateParameters ehParams = new EventHubCreateOrUpdateParameters()
{
    Location = location
};

Console.WriteLine("Creating Event Hub...");
await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
Console.WriteLine("Created Event Hub successfully.");
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a>Tutoriales

* [Envío de eventos a Azure Event Hubs mediante .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [Recepción de eventos de Azure Event Hubs mediante .NET Framework](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a>Ejemplos

* [Ejemplos de Azure Event Hubs](https://github.com/Azure/azure-event-hubs/tree/master/samples)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
