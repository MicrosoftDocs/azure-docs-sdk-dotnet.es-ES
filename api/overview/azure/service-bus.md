---
title: Bibliotecas de Azure Service Bus para .NET
description: Referencia de las bibliotecas de Azure Service Bus para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-bus
ms.openlocfilehash: 506be9a669a2418f2437271d128a963e351442e7
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190878"
---
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="53e96-103">Bibliotecas de Azure Service Bus para .NET</span><span class="sxs-lookup"><span data-stu-id="53e96-103">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="53e96-104">Información general</span><span class="sxs-lookup"><span data-stu-id="53e96-104">Overview</span></span>

<span data-ttu-id="53e96-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) es una infraestructura de mensajería que se encuentra entre las aplicaciones que les permite intercambiar mensajes para mejorar el escalado y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="53e96-105">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="53e96-106">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="53e96-106">Client library</span></span>

<span data-ttu-id="53e96-107">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53e96-107">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="53e96-108">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53e96-108">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="53e96-109">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="53e96-109">Code Example</span></span>

<span data-ttu-id="53e96-110">En este ejemplo se envía un mensaje a una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="53e96-110">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.Azure.ServiceBus;
// Microsoft.Azure.ServiceBus 2.0.0 (stable)

byte[] messageBody = System.Text.Encoding.Unicode.GetBytes("Hello, world!");
ServiceBusConnectionStringBuilder builder = new ServiceBusConnectionStringBuilder(connectionString);
QueueClient client = new QueueClient(builder, ReceiveMode.PeekLock);
client.SendAsync(new Message(messageBody));
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="53e96-111">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="53e96-111">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="53e96-112">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="53e96-112">Management library</span></span>

<span data-ttu-id="53e96-113">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="53e96-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="53e96-114">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="53e96-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="53e96-115">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="53e96-115">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="53e96-116">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="53e96-116">Code Example</span></span>

<span data-ttu-id="53e96-117">En este ejemplo se crea una cola de Service Bus con un tamaño máximo de 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="53e96-117">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

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
> [<span data-ttu-id="53e96-118">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="53e96-118">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="53e96-119">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="53e96-119">Samples</span></span>

- [<span data-ttu-id="53e96-120">Conceptos básicos de la cola de Service Bus - .NET</span><span class="sxs-lookup"><span data-stu-id="53e96-120">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="53e96-121">Características avanzadas de la cola de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="53e96-121">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="53e96-122">Conceptos básicos de publicación y suscripción de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="53e96-122">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="53e96-123">Características avanzadas de publicación y suscripción de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="53e96-123">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="53e96-124">Service Bus con la autorización basada en notificaciones - .Net</span><span class="sxs-lookup"><span data-stu-id="53e96-124">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="53e96-125">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?term=service+bus) de ejemplos de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="53e96-125">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
