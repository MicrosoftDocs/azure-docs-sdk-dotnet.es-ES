---
title: Bibliotecas de Azure Media Services para .NET
description: Referencia de las bibliotecas de Azure Media Services para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: media-services
ms.openlocfilehash: cbb37d5d80c152ef53dba14c83cf2a2695e6b0f0
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190588"
---
# <a name="azure-media-services-libraries-for-net"></a><span data-ttu-id="7c2f1-103">Bibliotecas de Azure Media Services para .NET</span><span class="sxs-lookup"><span data-stu-id="7c2f1-103">Azure Media Services libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7c2f1-104">Información general</span><span class="sxs-lookup"><span data-stu-id="7c2f1-104">Overview</span></span>

<span data-ttu-id="7c2f1-105">Microsoft Azure Media Services es una plataforma extensible basada en la nube que permite a los desarrolladores crear aplicaciones de administración y entrega de contenido multimedia escalables.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-105">Microsoft Azure Media Services is an extensible cloud-based platform that enables developers to build scalable media management and delivery applications.</span></span> <span data-ttu-id="7c2f1-106">Media Services se basa en las API de REST, que permiten cargar, almacenar, codificar y empaquetar de forma segura contenido de audio o vídeo para la entrega bajo demanda y de streaming en vivo a varios clientes (por ejemplo, televisión, PC y dispositivos móviles).</span><span class="sxs-lookup"><span data-stu-id="7c2f1-106">Media Services is based on REST APIs that enable you to securely upload, store, encode, and package video or audio content for both on-demand and live streaming delivery to various clients (for example, TV, PC, and mobile devices).</span></span> 

<span data-ttu-id="7c2f1-107">Para más información, consulte los artículos de [introducción](/azure/media-services/media-services-overview) y [cómo empezar a trabajar con .NET](/azure/media-services/media-services-dotnet-how-to-use).</span><span class="sxs-lookup"><span data-stu-id="7c2f1-107">To learn more, see [Overview](/azure/media-services/media-services-overview) and [Getting started with .NET](/azure/media-services/media-services-dotnet-how-to-use).</span></span> 

## <a name="client-library"></a><span data-ttu-id="7c2f1-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="7c2f1-108">Client library</span></span>

<span data-ttu-id="7c2f1-109">La biblioteca del SDK de Azure Media Services para .NET permite programar en Media Services mediante .NET.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-109">The Azure Media Services .NET SDK library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="7c2f1-110">Utilice la biblioteca de cliente de Azure Media Services para conectarse, autenticarse y desarrollar con las API de Media Services.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-110">Use the Azure Media Services client library to connect, authenticate, and develop against Media Services APIs.</span></span>  

<span data-ttu-id="7c2f1-111">Para más información, consulte [Introducción a la entrega de contenido a petición mediante el SDK para .NET](/azure/media-services/media-services-dotnet-get-started).</span><span class="sxs-lookup"><span data-stu-id="7c2f1-111">For more information, see [Get started with delivering content on demand using .NET SDK](/azure/media-services/media-services-dotnet-get-started).</span></span>

<span data-ttu-id="7c2f1-112">Instale el [paquete NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7c2f1-112">Install the [NuGet package](https://www.nuget.org/packages/windowsazure.mediaservices) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7c2f1-113">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c2f1-113">Visual Studio Package Manager</span></span>

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a><span data-ttu-id="7c2f1-114">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7c2f1-114">Code Example</span></span>

<span data-ttu-id="7c2f1-115">En el ejemplo de código siguiente se usa el último SDK para .NET de Media Services para realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="7c2f1-115">The following code example uses Media Services .NET SDK to perform the following tasks:</span></span>

- <span data-ttu-id="7c2f1-116">Crear un trabajo de codificación.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-116">Create an encoding job.</span></span>
- <span data-ttu-id="7c2f1-117">Obtener una referencia al codificador Codificador multimedia estándar.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-117">Get a reference to the Media Encoder Standard encoder.</span></span>
- <span data-ttu-id="7c2f1-118">Especificar que se utilice el valor predeterminado Streaming adaptable.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-118">Specify to use the Adaptive Streaming preset.</span></span>
- <span data-ttu-id="7c2f1-119">Agregar una única tarea de codificación al trabajo.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-119">Add a single encoding task to the job.</span></span>
- <span data-ttu-id="7c2f1-120">Especificar el recurso de entrada que se va a codificar.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-120">Specify the input asset to be encoded.</span></span>
- <span data-ttu-id="7c2f1-121">Crear un recurso de salida que recibirá el recurso codificado.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-121">Create an output asset to receive the encoded asset.</span></span>
- <span data-ttu-id="7c2f1-122">Envíe el trabajo.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-122">Submit the job.</span></span>


```csharp
/* Include this 'using' directive:
using Microsoft.WindowsAzure.MediaServices.Client;
*/

CloudMediaContext context = new CloudMediaContext(new Uri(mediaServiceRESTAPIEndpoint), tokenProvider);

// Get an uploaded asset.
IAsset asset = context.Assets.FirstOrDefault();

// Encode and generate the output using the "Adaptive Streaming" preset.
// Declare a new job.
IJob job = context.Jobs.Create("Media Encoder Standard Job");
// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = context.MediaProcessors.Where(p => p.Name == mediaProcessorName)
    .ToList().OrderBy(p => new Version(p.Version)).LastOrDefault();
if (processor == null) 
{
    throw new ArgumentException(string.Format("Unknown media processor", mediaProcessorName));
}

// Create a task with the encoding details, using a string preset.
// In this case "Adaptive Streaming" preset is used.
ITask task = job.Tasks.AddNew("My encoding task", processor, "Adaptive Streaming", TaskOptions.None);

// Specify the input asset to be encoded.
task.InputAssets.Add(asset);
// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);

job.Submit();
job.GetExecutionProgressTask(CancellationToken.None).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c2f1-123">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="7c2f1-123">Explore the client APIs</span></span>](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a><span data-ttu-id="7c2f1-124">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="7c2f1-124">Samples</span></span>

- [<span data-ttu-id="7c2f1-125">Transmisión de contenido HLS protegido con Apple FairPlay</span><span class="sxs-lookup"><span data-stu-id="7c2f1-125">Stream your HLS content Protected with Apple FairPlay</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [<span data-ttu-id="7c2f1-126">Copia de blobs en un recurso de Azure Media Services mediante extensiones del SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="7c2f1-126">Copy blob into an Azure Media Services asset using .NET SDK Extensions</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [<span data-ttu-id="7c2f1-127">Codificación y entrega de transmisión en directo con Azure Media Services mediante el SDK para .NET</span><span class="sxs-lookup"><span data-stu-id="7c2f1-127">Encode and Deliver a Live Stream with Azure Media Services using .NET SDK</span></span>](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

<span data-ttu-id="7c2f1-128">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) de ejemplos de Azure Media Services.</span><span class="sxs-lookup"><span data-stu-id="7c2f1-128">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) of Azure Media Services samples.</span></span>


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
