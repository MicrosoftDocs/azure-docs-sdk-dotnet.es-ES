---
title: Bibliotecas de Azure IoT para .NET
description: Referencia de las bibliotecas de Azure IoT para .NET
keywords: Azure, .NET, SDK, API, IoT
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: bdbcc37affb55336d1a3fafe24b8e7ffd78ec180
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-iot-libraries-for-net"></a><span data-ttu-id="cf437-104">Bibliotecas de Azure IoT para .NET</span><span class="sxs-lookup"><span data-stu-id="cf437-104">Azure IoT libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="cf437-105">Información general</span><span class="sxs-lookup"><span data-stu-id="cf437-105">Overview</span></span>

<span data-ttu-id="cf437-106">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución.</span><span class="sxs-lookup"><span data-stu-id="cf437-106">[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) is a fully managed service that enables reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span>

<span data-ttu-id="cf437-107">Los dispositivos y orígenes de datos en una solución de IoT pueden ir de un sensor sencillo conectado a la red a un dispositivo informático eficaz e independiente.</span><span class="sxs-lookup"><span data-stu-id="cf437-107">Devices and data sources in an IoT solution can range from a simple network-connected sensor to a powerful, standalone computing device.</span></span> <span data-ttu-id="cf437-108">Dispositivos que tienen limitada la funcionalidad de proceso, la memoria, el ancho de banda de comunicación y la compatibilidad con el protocolo de comunicación.</span><span class="sxs-lookup"><span data-stu-id="cf437-108">Devices may have limited processing capability, memory, communication bandwidth, and communication protocol support.</span></span> <span data-ttu-id="cf437-109">Los [SDK de dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) de IoT le permiten implementar aplicaciones cliente para una amplia variedad de dispositivos y aplicaciones back-end.</span><span class="sxs-lookup"><span data-stu-id="cf437-109">The IoT [device SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) enable you to implement client applications for a wide variety of devices and back-end applications.</span></span>

<span data-ttu-id="cf437-110">El SDK de dispositivo para .NET facilita la creación dispositivos que ejecutan .NET y que se conectan a Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf437-110">The device SDK for .NET facilitates building devices running .NET that connect to Azure IoT Hub.</span></span>

<span data-ttu-id="cf437-111">El SDK de servicio para .NET facilita la creación de aplicaciones de back-end que utilizan .NET y que administran y permiten dispositivos de control desde la nube.</span><span class="sxs-lookup"><span data-stu-id="cf437-111">The service SDK for .NET facilitates building back-end applications using .NET that manage and allow controlling devices from the Cloud.</span></span>

<span data-ttu-id="cf437-112">[Más información sobre Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="cf437-112">[Learn more about Azure IoT](https://docs.microsoft.com/azure/iot-hub/).</span></span>


## <a name="client-library"></a><span data-ttu-id="cf437-113">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="cf437-113">Client library</span></span>

<span data-ttu-id="cf437-114">Utilice el cliente de dispositivos IoT de .NET para conectarse y enviar mensajes a su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf437-114">Use the .NET IoT devices client to connect and send messages to your IoT Hub.</span></span>

<span data-ttu-id="cf437-115">Instale el [paquete NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="cf437-115">Install the [NuGet package]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="cf437-116">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cf437-116">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a><span data-ttu-id="cf437-117">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="cf437-117">Code Examples</span></span> 

<span data-ttu-id="cf437-118">En este ejemplo se conecta a IoT Hub y se envía un mensaje por segundo.</span><span class="sxs-lookup"><span data-stu-id="cf437-118">This example connects to the IoT Hub and sends one message per second.</span></span>

```csharp
string deviceKey = "<deviceKey>";
string deviceId = "<deviceId>";
string iotHubHostName = "<IoTHubHostname>";
DeviceAuthenticationWithRegistrySymmetricKeyvar deviceAuthentication = new DeviceAuthenticationWithRegistrySymmetricKey(deviceId, deviceKey);

DeviceClient deviceClient = DeviceClient.Create(iotHubHostName, deviceAuthentication, TransportType.Mqtt);

while (true)
{
    double currentTemperature = 20 + Rand.NextDouble() * 15;
    double currentHumidity = 60 + Rand.NextDouble() * 20;

    var telemetryDataPoint = new
    {
        messageId = _messageId++,
        deviceId = deviceId,
        temperature = currentTemperature,
        humidity = currentHumidity
    };
    string messageString = JsonConvert.SerializeObject(telemetryDataPoint);
    Message message = new Message(Encoding.ASCII.GetBytes(messageString));
    message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

    await deviceClient.SendEventAsync(message);
    Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

    await Task.Delay(1000);
}
```


> [!div class="nextstepaction"]
> [<span data-ttu-id="cf437-119">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="cf437-119">Explore the client APIs</span></span>](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a><span data-ttu-id="cf437-120">Muestras</span><span class="sxs-lookup"><span data-stu-id="cf437-120">Samples</span></span>

- [<span data-ttu-id="cf437-121">Servicio web genérico al escenario de centro de eventos</span><span class="sxs-lookup"><span data-stu-id="cf437-121">Generic Web Service to Event Hub scenario</span></span>](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

<span data-ttu-id="cf437-122">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) de ejemplos de Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="cf437-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) of Azure IoT Upsamples.</span></span>

<span data-ttu-id="cf437-123">Consulte la [guía para desarrolladores de Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) para más información.</span><span class="sxs-lookup"><span data-stu-id="cf437-123">View the [Azure IoT Hub developer guide](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) for more guidance.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
