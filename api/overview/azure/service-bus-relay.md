---
title: Bibliotecas de Azure Service Bus Relay para .NET
description: Referencia de las bibliotecas de Azure Service Bus Relay para .NET
keywords: Azure, .NET, SDK, API, Service Bus Relay
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
ms.openlocfilehash: 1a869d5939e357c98ec417e6474f711b9ac8c466
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
ms.locfileid: "23566166"
---
# <a name="azure-service-bus-relay-libraries-for-net"></a><span data-ttu-id="3cbe3-104">Bibliotecas de Azure Service Bus Relay para .NET</span><span class="sxs-lookup"><span data-stu-id="3cbe3-104">Azure Service Bus Relay libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3cbe3-105">Información general</span><span class="sxs-lookup"><span data-stu-id="3cbe3-105">Overview</span></span>

<span data-ttu-id="3cbe3-106">El servicio Azure Relay crea aplicaciones híbridas, ya que permite exponer de forma segura los servicios que se encuentran en una red corporativa en la nube pública sin tener que abrir una conexión de firewall y sin que sea necesario realizar cambios intrusivos en una infraestructura de red corporativa.</span><span class="sxs-lookup"><span data-stu-id="3cbe3-106">The Azure Relay service creates hybrid applications by enabling you to securely expose services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or require intrusive changes to a corporate network infrastructure.</span></span> <span data-ttu-id="3cbe3-107">Relay admite diversos protocolos de transporte y estándares de servicios web.</span><span class="sxs-lookup"><span data-stu-id="3cbe3-107">Relay supports a variety of different transport protocols and web services standards.</span></span>
          
<span data-ttu-id="3cbe3-108">Más información acerca de [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span><span class="sxs-lookup"><span data-stu-id="3cbe3-108">Learn more about [Azure Relay](/azure/service-bus-relay/relay-what-is-it).</span></span>

## <a name="client-library"></a><span data-ttu-id="3cbe3-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="3cbe3-109">Client library</span></span>

<span data-ttu-id="3cbe3-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Relay) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3cbe3-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Relay) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3cbe3-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3cbe3-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Relay
```

```bash
dotnet add package Microsoft.Azure.Relay
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3cbe3-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="3cbe3-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/relay/client)

## <a name="samples"></a><span data-ttu-id="3cbe3-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="3cbe3-113">Samples</span></span>

<span data-ttu-id="3cbe3-114">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3cbe3-114">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package