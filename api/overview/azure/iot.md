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
# <a name="azure-iot-libraries-for-net"></a>Bibliotecas de Azure IoT para .NET

## <a name="overview"></a>Información general

[Azure IoT Hub](https://azure.microsoft.com/services/iot-hub/) es un servicio totalmente administrado que permite la comunicación bidireccional confiable y segura entre millones de dispositivos y un back-end de la solución.

Los dispositivos y orígenes de datos en una solución de IoT pueden ir de un sensor sencillo conectado a la red a un dispositivo informático eficaz e independiente. Dispositivos que tienen limitada la funcionalidad de proceso, la memoria, el ancho de banda de comunicación y la compatibilidad con el protocolo de comunicación. Los [SDK de dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks) de IoT le permiten implementar aplicaciones cliente para una amplia variedad de dispositivos y aplicaciones back-end.

El SDK de dispositivo para .NET facilita la creación dispositivos que ejecutan .NET y que se conectan a Azure IoT Hub.

El SDK de servicio para .NET facilita la creación de aplicaciones de back-end que utilizan .NET y que administran y permiten dispositivos de control desde la nube.

[Más información sobre Azure IoT](https://docs.microsoft.com/azure/iot-hub/).


## <a name="client-library"></a>Biblioteca de cliente

Utilice el cliente de dispositivos IoT de .NET para conectarse y enviar mensajes a su instancia de IoT Hub.

Instale el [paquete NuGet]( https://www.nuget.org/packages/Microsoft.Azure.Devices.Client) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Devices.Client
```

```bash
dotnet add package Microsoft.Azure.Devices.Client
```
### <a name="code-examples"></a>Ejemplos de código 

En este ejemplo se conecta a IoT Hub y se envía un mensaje por segundo.

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/iot/client)

## <a name="samples"></a>Muestras

- [Servicio web genérico al escenario de centro de eventos](https://azure.microsoft.com/resources/samples/event-hubs-dotnet-importfromweb/)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=dotnet&service=iot-hub) de ejemplos de Azure IoT Hub.

Consulte la [guía para desarrolladores de Azure IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide) para más información.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
