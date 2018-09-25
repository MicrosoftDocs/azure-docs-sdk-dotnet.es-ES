---
title: Bibliotecas de Azure Event Grid para .NET
description: Referencia de las bibliotecas de Azure Event Grid para .NET
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: 894b8a5beaf0507ab50e8eed6a5ab20d10a71ba6
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750603"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="c4383-103">Bibliotecas de Azure Event Grid para .NET</span><span class="sxs-lookup"><span data-stu-id="c4383-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="c4383-104">Cree aplicaciones orientadas a eventos que escuchen y reaccionen a los eventos de los servicios de Azure y orígenes personalizados mediante un control de eventos simple basado en HTTP con Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="c4383-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="c4383-105">[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span><span class="sxs-lookup"><span data-stu-id="c4383-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="client-sdk"></a><span data-ttu-id="c4383-106">Client SDK</span><span class="sxs-lookup"><span data-stu-id="c4383-106">Client SDK</span></span>

<span data-ttu-id="c4383-107">Puede crear eventos, autenticar y enviar a temas con Client SDK de Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="c4383-107">Create events, authenticate, and post to topics using the Azure Event Grid Client SDK.</span></span>

<span data-ttu-id="c4383-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c4383-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c4383-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4383-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="c4383-110">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="c4383-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="publish-events"></a><span data-ttu-id="c4383-111">Publicación de eventos</span><span class="sxs-lookup"><span data-stu-id="c4383-111">Publish events</span></span>

<span data-ttu-id="c4383-112">El código siguiente se autentica con Azure y publica una `List` de eventos `EventGridEvent` de un tipo personalizado (en este ejemplo, `Contoso.Items.ItemsReceivedEvent`) en un tema.</span><span class="sxs-lookup"><span data-stu-id="c4383-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="c4383-113">La clave del tema y la dirección del punto de conexión utilizadas en el ejemplo se pueden recuperar de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c4383-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

```powershell
$endpoint = (Get-AzureRmEventGridTopic -ResourceGroupName gridResourceGroup -Name <topic-name>).Endpoint
$keys = Get-AzureRmEventGridTopicKey -ResourceGroupName gridResourceGroup -Name <topic-name>
```

```csharp
string topicEndpoint = "https://<topic-name>.<region>-1.eventgrid.azure.net/api/events";
string topicKey = "<topic-key>";
string topicHostname = new Uri(topicEndpoint).Host;

TopicCredentials topicCredentials = new TopicCredentials(topicKey);
EventGridClient client = new EventGridClient(topicCredentials);

client.PublishEventsAsync(topicHostname, GetEventsList()).GetAwaiter().GetResult();
Console.Write("Published events to Event Grid.");

static IList<EventGridEvent> GetEventsList()
{
    List<EventGridEvent> eventsList = new List<EventGridEvent>();
    for (int i = 0; i < 1; i++)
    {
        eventsList.Add(new EventGridEvent()
        {
            Id = Guid.NewGuid().ToString(),
            EventType = "Contoso.Items.ItemReceivedEvent",
            Data = new ContosoItemReceivedEventData()
            {
                ItemUri = "ContosoSuperItemUri"
            },

            EventTime = DateTime.Now,
            Subject = "Door1",
            DataVersion = "2.0"
        });
    }
    return eventsList;
}
```

### <a name="consume-events"></a><span data-ttu-id="c4383-114">Consumo de eventos</span><span class="sxs-lookup"><span data-stu-id="c4383-114">Consume events</span></span>

<span data-ttu-id="c4383-115">Este fragmento de código utiliza eventos, incluido un evento personalizado `Contoso.Items.ItemsReceived`, así como eventos desencadenados por servicios de Azure, como Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c4383-115">This snippet consumes events, including a custom event `Contoso.Items.ItemsReceived` as well as events triggered from other Azure services, such as Blob Storage.</span></span>

```csharp
string response = string.Empty;
string requestContent = await req.Content.ReadAsStringAsync();

EventGridSubscriber eventGridSubscriber = new EventGridSubscriber();

// Optionally add one or more custom event type mappings
eventGridSubscriber.AddOrUpdateCustomEventMapping("Contoso.Items.ItemReceived", typeof(ContosoItemReceivedEventData));

var events = eventGridSubscriber.DeserializeEventGridEvents(requestContent);            
 
foreach (EventGridEvent receivedEvent in events)
{
    if (receivedEvent.Data is SubscriptionValidationEventData)
    {
        SubscriptionValidationEventData eventData = (SubscriptionValidationEventData)receivedEvent.Data;
        log.Info($"Got SubscriptionValidation event data, validationCode: {eventData.ValidationCode},  validationUrl: {eventData.ValidationUrl}, topic: {eventGridEvent.Topic}");
        // Handle subscription validation
    }
    else if (receivedEvent.Data is StorageBlobCreatedEventData)
    {
        StorageBlobCreatedEventData eventData = (StorageBlobCreatedEventData)receivedEvent.Data;
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
        // Handle StorageBlobCreatedEventData
    }
    else if (receivedEvent.Data is ContosoItemReceivedEventData)
    {
        ContosoItemReceivedEventData eventData = (ContosoItemReceivedEventData)receivedEvent.Data;
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4383-116">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="c4383-116">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="c4383-117">SDK de administración</span><span class="sxs-lookup"><span data-stu-id="c4383-117">Management SDK</span></span>

<span data-ttu-id="c4383-118">El SDK de administración permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.</span><span class="sxs-lookup"><span data-stu-id="c4383-118">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="c4383-119">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c4383-119">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c4383-120">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c4383-120">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="c4383-121">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="c4383-121">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4383-122">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="c4383-122">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="c4383-123">Más información</span><span class="sxs-lookup"><span data-stu-id="c4383-123">Learn more</span></span>

- [<span data-ttu-id="c4383-124">Recepción de eventos mediante el SDK de Event Grid</span><span class="sxs-lookup"><span data-stu-id="c4383-124">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
