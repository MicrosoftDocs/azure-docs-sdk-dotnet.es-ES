---
title: Bibliotecas de Azure Event Hubs para .NET
description: Referencia de las bibliotecas de Azure Event Hubs para .NET
keywords: Azure, .NET, SDK, API, Event Hubs
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 1dca44ed716e387d531661093d4c7cfc7780964b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-event-hubs-libraries-for-net"></a><span data-ttu-id="6b1d6-104">Bibliotecas de Azure Event Hubs para .NET</span><span class="sxs-lookup"><span data-stu-id="6b1d6-104">Azure Event Hubs libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="6b1d6-105">Información general</span><span class="sxs-lookup"><span data-stu-id="6b1d6-105">Overview</span></span>

<span data-ttu-id="6b1d6-106">Azure Event Hubs es una plataforma de streaming de datos muy escalable y un servicio de ingesta de eventos.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-106">Azure Event Hubs is a highly scalable data streaming platform and event ingestion service.</span></span>

<span data-ttu-id="6b1d6-107">Para más información acerca de Azure Event Hubs, lea el artículo [¿Qué es Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span><span class="sxs-lookup"><span data-stu-id="6b1d6-107">To learn more about Azure Event Hubs, read the article [What is Event Hubs?](/azure/event-hubs/event-hubs-what-is-event-hubs).</span></span>  <span data-ttu-id="6b1d6-108">Para empezar, consulte la [Guía de programación de Event Hubs](/azure/event-hubs/event-hubs-programming-guide).</span><span class="sxs-lookup"><span data-stu-id="6b1d6-108">To get started, check out the [Event Hubs Programming Guide](/azure/event-hubs/event-hubs-programming-guide).</span></span>

## <a name="client-library"></a><span data-ttu-id="6b1d6-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="6b1d6-109">Client library</span></span>

<span data-ttu-id="6b1d6-110">Use al cliente de Event Hubs tanto para enviar mensajes a Event Hubs como para recibirlos de este.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-110">Use the Event Hubs client to send and receive messages to and from Event Hubs.</span></span>

<span data-ttu-id="6b1d6-111">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6b1d6-111">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6b1d6-112">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b1d6-112">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventHubs
```

```bash
dotnet add package Microsoft.Azure.EventHubs
```

### <a name="code-example"></a><span data-ttu-id="6b1d6-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="6b1d6-113">Code Example</span></span>

<span data-ttu-id="6b1d6-114">El código siguiente crea a un cliente de Event Hubs y envía un mensaje al centro.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-114">The following code creates an Event Hubs client and sends a message to the hub.</span></span>

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
> [<span data-ttu-id="6b1d6-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="6b1d6-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventhub/client)

## <a name="management-library"></a><span data-ttu-id="6b1d6-116">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="6b1d6-116">Management library</span></span>

<span data-ttu-id="6b1d6-117">Utilice la biblioteca de administración de Event Hubs para crear, actualizar y quitar centros y los grupos de consumidores.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-117">Use the Event Hubs management library to create, update, and remove hubs and consumer groups.</span></span>

<span data-ttu-id="6b1d6-118">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="6b1d6-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.EventHub) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="6b1d6-119">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6b1d6-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventHub
```

```bash
dotnet add package Microsoft.Azure.Management.EventHub
```

### <a name="code-example"></a><span data-ttu-id="6b1d6-120">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="6b1d6-120">Code Example</span></span>

<span data-ttu-id="6b1d6-121">El siguiente código crea un centro de eventos nuevo.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-121">The following code creates a new event hub.</span></span>

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
> [<span data-ttu-id="6b1d6-122">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="6b1d6-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventhub/management)

## <a name="tutorials"></a><span data-ttu-id="6b1d6-123">Tutoriales</span><span class="sxs-lookup"><span data-stu-id="6b1d6-123">Tutorials</span></span>

* [<span data-ttu-id="6b1d6-124">Envío de eventos a Azure Event Hubs mediante .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6b1d6-124">Send events to Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-send)

* [<span data-ttu-id="6b1d6-125">Recepción de eventos de Azure Event Hubs mediante .NET Framework</span><span class="sxs-lookup"><span data-stu-id="6b1d6-125">Receive events from Azure Event Hubs using the .NET Framework</span></span>](/azure/event-hubs/event-hubs-dotnet-framework-getstarted-receive-eph)

## <a name="samples"></a><span data-ttu-id="6b1d6-126">Muestras</span><span class="sxs-lookup"><span data-stu-id="6b1d6-126">Samples</span></span>

* [<span data-ttu-id="6b1d6-127">Ejemplos de Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="6b1d6-127">Azure Event Hubs Samples</span></span>](https://github.com/Azure/azure-event-hubs/tree/master/samples)

<span data-ttu-id="6b1d6-128">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="6b1d6-128">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
