---
title: Bibliotecas de Azure Service Fabric para .NET
description: Referencia de las bibliotecas de Azure Service Fabric para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: service-fabric
ms.openlocfilehash: 064f95a4eae3182c4ac5b31779a5d22b592a75b2
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190768"
---
# <a name="azure-service-fabric-libraries-for-net"></a><span data-ttu-id="f22b8-103">Bibliotecas de Azure Service Fabric para .NET</span><span class="sxs-lookup"><span data-stu-id="f22b8-103">Azure Service Fabric libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="f22b8-104">Información general</span><span class="sxs-lookup"><span data-stu-id="f22b8-104">Overview</span></span>

<span data-ttu-id="f22b8-105">Azure Service Fabric es una plataforma de sistemas distribuidos que facilita el empaquetado, la implementación y la administración de microservicios y contenedores escalables y confiables.</span><span class="sxs-lookup"><span data-stu-id="f22b8-105">Azure Service Fabric is a distributed systems platform that makes it easy to package, deploy, and manage scalable and reliable microservices and containers.</span></span>  <span data-ttu-id="f22b8-106">Para más información, consulte la [documentación de Azure Service Fabric](/azure/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="f22b8-106">For more information, see the [Azure Service Fabric Documentation](/azure/service-fabric/).</span></span>

## <a name="client-library"></a><span data-ttu-id="f22b8-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="f22b8-107">Client library</span></span>

<span data-ttu-id="f22b8-108">Utilice la biblioteca de cliente de Service Fabric para interactuar con un clúster de Service Fabric existente.</span><span class="sxs-lookup"><span data-stu-id="f22b8-108">Use the Service Fabric client library to interact with an existing Service Fabric cluster.</span></span>  <span data-ttu-id="f22b8-109">La biblioteca contiene tres categorías de API:</span><span class="sxs-lookup"><span data-stu-id="f22b8-109">The library contains three categories of APIs:</span></span>

* <span data-ttu-id="f22b8-110">**Cliente** Las API se utilizan para administrar, escalar y reciclar el clúster, así como para implementar paquetes de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="f22b8-110">**Client** APIs are used to manage, scale, and recycle the cluster, as well as deploy application packages.</span></span>
* <span data-ttu-id="f22b8-111">**En tiempo de ejecución** Las API se utilizan para que la aplicación en ejecución pueda interactuar con el clúster que la aloja.</span><span class="sxs-lookup"><span data-stu-id="f22b8-111">**Runtime** APIs are used for the running application to interact with its hosting cluster.</span></span>
* <span data-ttu-id="f22b8-112">**Común** Las API contienen tipos usados tanto en API de **cliente** como **en tiempo de ejecución**.</span><span class="sxs-lookup"><span data-stu-id="f22b8-112">**Common** APIs contain types used in both **client** and **runtime** APIs.</span></span>

<span data-ttu-id="f22b8-113">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.ServiceFabric) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f22b8-113">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f22b8-114">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f22b8-114">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.ServiceFabric
```

```bash
dotnet add package Microsoft.ServiceFabric
```

### <a name="code-examples"></a><span data-ttu-id="f22b8-115">Ejemplos de código</span><span class="sxs-lookup"><span data-stu-id="f22b8-115">Code Examples</span></span>

<span data-ttu-id="f22b8-116">En el ejemplo siguiente se utilizan las API de **cliente** de Service Fabric para copiar un paquete de aplicación en el almacén de imágenes, aprovisionar el tipo de aplicación y crear una instancia de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="f22b8-116">The following example uses the Service Fabric **client** APIs to copy an application package to the image store, provisions the application type, and create an application instance.</span></span>

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
> [<span data-ttu-id="f22b8-117">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="f22b8-117">Explore the client APIs</span></span>](/dotnet/api/overview/azure/servicefabric/client)

<span data-ttu-id="f22b8-118">Este ejemplo utiliza las API **en tiempo de ejecución** y **común** de Service Fabric desde una aplicación hospedada para actualizar una [Colección confiable](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) en tiempo de ejecución.</span><span class="sxs-lookup"><span data-stu-id="f22b8-118">This example uses the Service Fabric **runtime** and **common** APIs from within a hosted application to update a [Reliable Collection](/azure/service-fabric/service-fabric-reliable-services-reliable-collections) at runtime.</span></span>

```csharp
using System.Fabric;
using Microsoft.ServiceFabric.Data.Collections;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

/// <summary>
/// This is the main entry point for your service replica.
/// This method executes when this replica of your service becomes primary and has write status.
/// </summary>
/// <param name="cancellationToken">Canceled when Service Fabric needs to shut down this service replica.</param>
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();
        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");
            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }
        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f22b8-119">Explorar la API en tiempo de ejecución</span><span class="sxs-lookup"><span data-stu-id="f22b8-119">Explore the runtime APIs</span></span>](/dotnet/api/overview/azure/servicefabric/runtime)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f22b8-120">Explorar la API común</span><span class="sxs-lookup"><span data-stu-id="f22b8-120">Explore the common APIs</span></span>](/dotnet/api/overview/azure/servicefabric/common)

## <a name="management-library"></a><span data-ttu-id="f22b8-121">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="f22b8-121">Management Library</span></span>

<span data-ttu-id="f22b8-122">La biblioteca de administración se utiliza para crear, actualizar y eliminar clústeres de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f22b8-122">The management library is used to create, update, and delete Service Fabric clusters.</span></span>

<span data-ttu-id="f22b8-123">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="f22b8-123">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.ServiceFabric) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="f22b8-124">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f22b8-124">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.ServiceFabric
```

```bash
dotnet add package Microsoft.Azure.Management.ServiceFabric
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f22b8-125">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="f22b8-125">Explore the management APIs</span></span>](/dotnet/api/overview/azure/servicefabric/management)

## <a name="samples"></a><span data-ttu-id="f22b8-126">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="f22b8-126">Samples</span></span>

* [<span data-ttu-id="f22b8-127">Implementación y eliminación de aplicaciones mediante FabricClient</span><span class="sxs-lookup"><span data-stu-id="f22b8-127">Deploy and remove applications using FabricClient</span></span>](/azure/service-fabric/service-fabric-deploy-remove-applications-fabricclient)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
