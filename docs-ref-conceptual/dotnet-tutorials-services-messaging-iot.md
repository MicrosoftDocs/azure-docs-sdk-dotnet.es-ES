---
title: "Tutoriales de mensajería e IoT con .NET en Azure | Microsoft Docs"
description: "Envíe mensajes entre aplicaciones en la nube y entre los dispositivos y la nube con .NET y los servicios de Azure."
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a6c50af1678c785c6a3fcd3f4f3689171069b2ee
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="net-tutorials-for-enterprise-messaging-and-internet-of-things-iot"></a><span data-ttu-id="5964e-103">Tutoriales de .NET para la mensajería empresarial e Internet de las cosas (IoT)</span><span class="sxs-lookup"><span data-stu-id="5964e-103">.NET tutorials for enterprise messaging and Internet of Things (IoT)</span></span>

<span data-ttu-id="5964e-104">La tabla siguiente incluye vínculos a tutoriales detallados sobre cómo enviar y leer mensajes entre aplicaciones y dispositivos del código .NET con los servicios de Azure.</span><span class="sxs-lookup"><span data-stu-id="5964e-104">The following table links to in-depth tutorials for sending and reading messages between applications and devices in from your .NET code using Azure services.</span></span>

<span data-ttu-id="5964e-105">Para el código fuente de ejemplo, consulte la lista de [ejemplos de servicios de Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span><span class="sxs-lookup"><span data-stu-id="5964e-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>


| | |
|---|---|
| <span data-ttu-id="5964e-106">**Service Bus**</span><span class="sxs-lookup"><span data-stu-id="5964e-106">**Service Bus**</span></span> | |
| <span data-ttu-id="5964e-107">[Utilización de las colas de Service Bus][1]</span><span class="sxs-lookup"><span data-stu-id="5964e-107">[How to use Service Bus queues][1]</span></span> | <span data-ttu-id="5964e-108">Cree colas, envíe y reciba mensajes, y elimine colas.</span><span class="sxs-lookup"><span data-stu-id="5964e-108">Create queues, send and receive messages, and delete queues.</span></span> | 
| <span data-ttu-id="5964e-109">[Uso de temas y suscripciones de Service Bus][2]</span><span class="sxs-lookup"><span data-stu-id="5964e-109">[How to use Service Bus topics and subscriptions][2]</span></span> | <span data-ttu-id="5964e-110">Aprenda a usar el modelo de comunicación de publicación y suscripción con Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5964e-110">Learn how to use publish/subscribe communication model with Service Bus.</span></span>
| <span data-ttu-id="5964e-111">[Uso de Service Bus desde .NET con AMQP 1.0][3]</span><span class="sxs-lookup"><span data-stu-id="5964e-111">[Using Service Bus from .NET with AMQP 1.0][3]</span></span> | <span data-ttu-id="5964e-112">Aprenda a usar AMQP en aplicaciones de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="5964e-112">Learn how to use AMQP in you Service Bus applications.</span></span>
|<span data-ttu-id="5964e-113">**IoT Hub**</span><span class="sxs-lookup"><span data-stu-id="5964e-113">**IoT Hub**</span></span>|
| <span data-ttu-id="5964e-114">[Conexión de un dispositivo simulado a IoT Hub][4]</span><span class="sxs-lookup"><span data-stu-id="5964e-114">[Connect a simulated device to your IoT Hub][4]</span></span> | <span data-ttu-id="5964e-115">Cree una identidad de dispositivo, envíe mensajes y procese la telemetría de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5964e-115">Create a device identity, send messages, and process telemetry from your IoT Hub.</span></span> |   
| <span data-ttu-id="5964e-116">[Procesamiento de mensajes de dispositivo a la nube][5]</span><span class="sxs-lookup"><span data-stu-id="5964e-116">[Process device-to-cloud messages][5]</span></span> | <span data-ttu-id="5964e-117">Envíe mensajes desde un dispositivo simulado y procéselos en la nube.</span><span class="sxs-lookup"><span data-stu-id="5964e-117">Send messages from a simulated device and process them in the cloud.</span></span> |
|<span data-ttu-id="5964e-118">**Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="5964e-118">**Event Hub**</span></span>|
| <span data-ttu-id="5964e-119">[Envío de eventos a Event Hubs][6]</span><span class="sxs-lookup"><span data-stu-id="5964e-119">[Send events to an Event Hub][6]</span></span> | <span data-ttu-id="5964e-120">Envíe eventos a Event Hubs desde una aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="5964e-120">Send events to Event hub from a console application.</span></span>
| <span data-ttu-id="5964e-121">[Recepción de eventos de Event Hubs][7]</span><span class="sxs-lookup"><span data-stu-id="5964e-121">[Receive events from Event Hubs][7]</span></span> | <span data-ttu-id="5964e-122">Reciba mensajes y procéselos en paralelo.</span><span class="sxs-lookup"><span data-stu-id="5964e-122">Receive messages and process them in parallel.</span></span>


[1]: /azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues
[2]: /azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions
[3]: /azure/service-bus-messaging/service-bus-amqp-dotnet
[4]: /azure/iot-hub/iot-hub-csharp-csharp-getstarted
[5]: /azure/iot-hub/iot-hub-csharp-csharp-process-d2c
[6]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-send
[7]: /azure/event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph


