---
title: Bibliotecas de Azure Service Fabric para .NET
description: Referencia de las bibliotecas de Azure Service Fabric para .NET
keywords: Azure, .NET, SDK, API, Service Fabric
author: spboyer
ms.author: casoper
manager: douge
ms.date: 07/07/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: c708ae06fa4b5165e3f615abf636b11bfd95cd3b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="7a584-104">Bibliotecas de Azure Service Fabric para .NET</span><span class="sxs-lookup"><span data-stu-id="7a584-104">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="7a584-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7a584-105">Overview</span></span>

<span data-ttu-id="7a584-106">Azure Service Fabric es una plataforma de sistemas distribuidos que facilita el empaquetado, la implementación y la administración de microservicios y contenedores escalables y confiables.</span><span class="sxs-lookup"><span data-stu-id="7a584-106">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>

## <a name="client-library"></a><span data-ttu-id="7a584-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="7a584-107">Client library</span></span>

<span data-ttu-id="7a584-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="7a584-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="7a584-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a584-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-example"></a><span data-ttu-id="7a584-110">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="7a584-110">Code Example</span></span>

<span data-ttu-id="7a584-111">En el ejemplo siguiente se copia un paquete de aplicación en el almacén de imágenes, se aprovisiona el tipo de aplicación y se crea una instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="7a584-111">The following example copies an application package to the image store, provisions the application type, and creates an application instance.</span></span>

```csharp
/* Include these dependencies
using System.Fabric;
using System.Fabric.Description;
*/

// Connect to the cluster.
FabricClient fabricClient = new FabricClient(clusterConnection);

// Copy the application package to a location in the image store
fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);

// Provision the application.
fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

//  Create the application instance.
ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a584-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="7a584-112">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

## <a name="samples"></a><span data-ttu-id="7a584-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="7a584-113">Samples</span></span>

* [<span data-ttu-id="7a584-114">Implementación y eliminación de aplicaciones mediante FabricClient</span><span class="sxs-lookup"><span data-stu-id="7a584-114">Deploy and remove applications using FabricClient</span></span>](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
