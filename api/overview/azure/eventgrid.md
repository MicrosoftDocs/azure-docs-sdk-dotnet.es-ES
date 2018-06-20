---
title: Bibliotecas de Azure Event Grid para .NET
description: Referencia de las bibliotecas de Azure Event Grid para .NET
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/16/2018
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: event-grid
ms.custom: devcenter
ms.openlocfilehash: aa25f76f041e890de512c67d9380903f81216f62
ms.sourcegitcommit: 9f54e3334fc35c1066d0c591ff85b16d46416aa8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33802752"
---
# <a name="azure-event-grid-libraries-for-net"></a><span data-ttu-id="b9911-103">Bibliotecas de Azure Event Grid para .NET</span><span class="sxs-lookup"><span data-stu-id="b9911-103">Azure Event Grid libraries for .NET</span></span>

<span data-ttu-id="b9911-104">Cree aplicaciones orientadas a eventos que escuchen y reaccionen a los eventos de los servicios de Azure y orígenes personalizados mediante un control de eventos simple basado en HTTP con Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="b9911-104">Build event-driven applications that listen and react to events from Azure services and custom sources using simple HTTP-based event handling with Azure Event Grid.</span></span>

<span data-ttu-id="b9911-105">[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span><span class="sxs-lookup"><span data-stu-id="b9911-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart-powershell).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="b9911-106">SDK de publicación</span><span class="sxs-lookup"><span data-stu-id="b9911-106">Publish SDK</span></span>

<span data-ttu-id="b9911-107">Puede crear eventos, autenticar y enviar a temas con el SDK de publicación de Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="b9911-107">Create events, authenticate, and post to topics using the Azure Event Grid publish SDK.</span></span>

<span data-ttu-id="b9911-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="b9911-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b9911-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9911-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="b9911-110">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="b9911-110">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.EventGrid 
```

### <a name="sample-usage"></a><span data-ttu-id="b9911-111">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="b9911-111">Sample usage</span></span>

<span data-ttu-id="b9911-112">El código siguiente se autentica con Azure y publica una `List` de eventos `EventGridEvent` de un tipo personalizado (en este ejemplo, `Contoso.Items.ItemsReceivedEvent`) en un tema.</span><span class="sxs-lookup"><span data-stu-id="b9911-112">The following code authenticates with Azure and publishes a `List` of  `EventGridEvent` events of a custom type (in this example, `Contoso.Items.ItemsReceivedEvent` ) to a topic.</span></span> <span data-ttu-id="b9911-113">La clave del tema y la dirección del punto de conexión utilizadas en el ejemplo se pueden recuperar de Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="b9911-113">The topic key and endpoint address used in the sample can be retrieved from Azure PowerShell:</span></span>

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

<span data-ttu-id="b9911-114">Este fragmento de código controla los eventos publicados cuando se crea un nuevo blob en [Azure Storage](/azure/storage/blobs/storage-blob-event-overview).</span><span class="sxs-lookup"><span data-stu-id="b9911-114">This snippet handles events published when creating a new blob in [Azure Storage](/azure/storage/blobs/storage-blob-event-overview).</span></span>

```csharp
string response = string.Empty;
const string SubscriptionValidationEvent = "Microsoft.EventGrid.SubscriptionValidationEvent";
const string StorageBlobCreatedEvent = "Microsoft.Storage.BlobCreated";

string requestContent = await req.Content.ReadAsStringAsync();
EventGridEvent[] eventGridEvents = JsonConvert.DeserializeObject<EventGridEvent[]>(requestContent);

foreach (EventGridEvent eventGridEvent in eventGridEvents)
{
    JObject dataObject = eventGridEvent.Data as JObject;

    // Deserialize the event data into the appropriate type based on event type 
    if (string.Equals(eventGridEvent.EventType, SubscriptionValidationEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<SubscriptionValidationEventData>();
        log.Info($"Got SubscriptionValidation event data, validation code: {eventData.ValidationCode}, topic: {eventGridEvent.Topic}");

        // Do any additional validation (as required) and then return back the below response
        var responseData = new SubscriptionValidationResponseData();
        responseData.ValidationResponse = eventData.ValidationCode;
        return req.CreateResponse(HttpStatusCode.OK, responseData);
    }

    else if (string.Equals(eventGridEvent.EventType, StorageBlobCreatedEvent, StringComparison.OrdinalIgnoreCase))
    {
        var eventData = dataObject.ToObject<StorageBlobCreatedEventData>();
        log.Info($"Got BlobCreated event data, blob URI {eventData.Url}");
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9911-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="b9911-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="b9911-116">SDK de administración</span><span class="sxs-lookup"><span data-stu-id="b9911-116">Management SDK</span></span>

<span data-ttu-id="b9911-117">El SDK de administración permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.</span><span class="sxs-lookup"><span data-stu-id="b9911-117">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

<span data-ttu-id="b9911-118">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="b9911-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Network.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>


#### <a name="visual-studio-package-manager"></a><span data-ttu-id="b9911-119">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9911-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.EventGrid
```

#### <a name="net-core-cli"></a><span data-ttu-id="b9911-120">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="b9911-120">.NET Core CLI</span></span>

```bash
dotnet add package Microsoft.Azure.Management.EventGrid
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9911-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="b9911-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="b9911-122">Más información</span><span class="sxs-lookup"><span data-stu-id="b9911-122">Learn more</span></span>

- [<span data-ttu-id="b9911-123">Recepción de eventos mediante el SDK de Event Grid</span><span class="sxs-lookup"><span data-stu-id="b9911-123">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
