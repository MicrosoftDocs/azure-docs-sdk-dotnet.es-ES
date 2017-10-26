---
title: Bibliotecas de Azure Media Services para .NET
description: Referencia de las bibliotecas de Azure Media Services para .NET
keywords: Azure, .NET, SDK, API, Media Services
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: media-services
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 872ed60363c0c886e9844d0cb0bef07cf41a0242
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="azure-media-services-libraries-for-net"></a>Bibliotecas de Azure Media Services para .NET

## <a name="overview"></a>Información general

Microsoft Azure Media Services es una plataforma extensible basada en la nube que permite a los desarrolladores crear aplicaciones de administración y entrega de contenido multimedia escalables. Media Services se basa en las API de REST, que permiten cargar, almacenar, codificar y empaquetar de forma segura contenido de audio o vídeo para la entrega bajo demanda y de streaming en vivo a varios clientes (por ejemplo, televisión, PC y dispositivos móviles). 

Para más información, consulte los artículos de [introducción](/azure/media-services/media-services-overview) y [cómo empezar a trabajar con .NET](/azure/media-services/media-services-dotnet-how-to-use). 

## <a name="client-library"></a>Biblioteca de cliente

La biblioteca del SDK de Azure Media Services para .NET permite programar en Media Services mediante .NET. Utilice la biblioteca de cliente de Azure Media Services para conectarse, autenticarse y desarrollar con las API de Media Services.  

Para más información, consulte [Introducción a la entrega de contenido a petición mediante el SDK para .NET](/azure/media-services/media-services-dotnet-get-started).

Instale el [paquete NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package windowsazure.mediaservices
```

### <a name="code-example"></a>Ejemplo de código

En el ejemplo de código siguiente se usa el último SDK para .NET de Servicios multimedia para realizar las siguientes tareas:

- Crear un trabajo de codificación.
- Obtener una referencia al codificador Codificador multimedia estándar.
- Especificar que se utilice el valor predeterminado Streaming adaptable.
- Agregar una única tarea de codificación al trabajo.
- Especificar el recurso de entrada que se va a codificar.
- Crear un recurso de salida que recibirá el recurso codificado.
- Envíe el trabajo.


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
> [Explorar las API de cliente](/dotnet/api/overview/azure/mediaservices/client)

## <a name="samples"></a>Muestras

- [Transmisión de contenido HLS protegido con Apple FairPlay](https://azure.microsoft.com/resources/samples/media-services-dotnet-dynamic-encryption-with-fairplay/)
- [Copia de blobs en un recurso de Azure Media Services mediante extensiones del SDK para .NET](https://azure.microsoft.com/resources/samples/media-services-dotnet-copy-blob-into-asset/)
- [Codificación y entrega de transmisión en directo con Azure Media Services mediante el SDK para .NET](https://azure.microsoft.com/resources/samples/media-services-dotnet-encode-live-stream-with-ams-clear/)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=media-services) de ejemplos de Azure Media Services.


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
