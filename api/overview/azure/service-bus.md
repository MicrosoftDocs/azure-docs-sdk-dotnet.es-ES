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
# <a name="azure-service-bus-libraries-for-net"></a><span data-ttu-id="682ff-104">Bibliotecas de Azure Service Bus para .NET</span><span class="sxs-lookup"><span data-stu-id="682ff-104">Azure Service Bus libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="682ff-105">Información general</span><span class="sxs-lookup"><span data-stu-id="682ff-105">Overview</span></span>

<span data-ttu-id="682ff-106">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) es una infraestructura de mensajería que se encuentra entre las aplicaciones que les permite intercambiar mensajes para mejorar el escalado y la resistencia.</span><span class="sxs-lookup"><span data-stu-id="682ff-106">[Azure Service Bus](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) is a messaging infrastructure that sits between applications allowing them to exchange messages for improved scale and resiliency.</span></span>

## <a name="client-library"></a><span data-ttu-id="682ff-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="682ff-107">Client library</span></span>

<span data-ttu-id="682ff-108">Instale el [paquete NuGet](https://www.nuget.org/packages/WindowsAzure.ServiceBus) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="682ff-108">Install the [NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="682ff-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="682ff-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package WindowsAzure.ServiceBus
```

### <a name="code-example"></a><span data-ttu-id="682ff-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="682ff-110">Code Example</span></span>

<span data-ttu-id="682ff-111">En este ejemplo se envía un mensaje a una cola de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="682ff-111">This example sends a message to a Service Bus queue.</span></span>

```csharp
// using Microsoft.ServiceBus.Messaging;

QueueClient client = QueueClient.CreateFromConnectionString(connectionString, queueName);
BrokeredMessage message = new BrokeredMessage("This is a test message!");
client.Send(message);
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="682ff-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="682ff-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicebus/client)


## <a name="management-library"></a><span data-ttu-id="682ff-113">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="682ff-113">Management library</span></span>

<span data-ttu-id="682ff-114">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="682ff-114">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceBus.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="682ff-115">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="682ff-115">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceBus.Fluent
```

#### <a name="net-core-cli"></a><span data-ttu-id="682ff-116">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="682ff-116">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.ServiceBus.Fluent
```

### <a name="code-example"></a><span data-ttu-id="682ff-117">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="682ff-117">Code Example</span></span>

<span data-ttu-id="682ff-118">En este ejemplo se crea una cola de Service Bus con un tamaño máximo de 1024 MB.</span><span class="sxs-lookup"><span data-stu-id="682ff-118">This example creates a Service Bus queue with a maximum size of 1024 MB.</span></span>

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
> [<span data-ttu-id="682ff-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="682ff-119">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicebus/management)

## <a name="samples"></a><span data-ttu-id="682ff-120">Muestras</span><span class="sxs-lookup"><span data-stu-id="682ff-120">Samples</span></span>

- [<span data-ttu-id="682ff-121">Conceptos básicos de la cola de Service Bus - .NET</span><span class="sxs-lookup"><span data-stu-id="682ff-121">Service Bus Queue Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-basic-features/)
- [<span data-ttu-id="682ff-122">Características avanzadas de la cola de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="682ff-122">Service Bus Queue Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-queue-with-advanced-features/)
- [<span data-ttu-id="682ff-123">Conceptos básicos de publicación y suscripción de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="682ff-123">Service Bus Publish/Subscribe Basics - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-basic-features/)
- [<span data-ttu-id="682ff-124">Características avanzadas de publicación y suscripción de Service Bus - .Net</span><span class="sxs-lookup"><span data-stu-id="682ff-124">Service Bus Publish/Subscribe Advanced Features - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-publish-subscribe-with-advanced-features/)
- [<span data-ttu-id="682ff-125">Service Bus con la autorización basada en notificaciones - .Net</span><span class="sxs-lookup"><span data-stu-id="682ff-125">Service Bus with Claims-Based Authorization - .Net</span></span>](https://azure.microsoft.com/resources/samples/service-bus-dotnet-manage-with-claims-based-authorization/)

<span data-ttu-id="682ff-126">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?term=service+bus) de ejemplos de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="682ff-126">View the [complete list](https://azure.microsoft.com/resources/samples/?term=service+bus) of Azure Service Bus samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
