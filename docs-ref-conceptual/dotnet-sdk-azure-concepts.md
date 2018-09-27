---
title: Conceptos de uso y patrones de las bibliotecas de administración de Azure para .NET
description: ''
ms.date: 10/19/2017
ms.openlocfilehash: 0a6ae94046680b81f1222c3c2acc6df9871bff4a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190608"
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="a3f15-102">Biblioteca de administración de Azure para conceptos fluidos de .NET</span><span class="sxs-lookup"><span data-stu-id="a3f15-102">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="a3f15-103">Este artículo le ayudará a aprender a utilizar de forma eficaz la interfaz fluida de las bibliotecas de administración de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="a3f15-103">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="a3f15-104">Creación de recursos con una interfaz fluida</span><span class="sxs-lookup"><span data-stu-id="a3f15-104">Building resources using a fluent interface</span></span>

<span data-ttu-id="a3f15-105">Una interfaz fluida es un tipo específico de patrón de generador que crea objetos mediante una cadena de método que aplica la configuración correcta de un recurso.</span><span class="sxs-lookup"><span data-stu-id="a3f15-105">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="a3f15-106">Por ejemplo, el objeto de Azure de punto de entrada se crea mediante una interfaz fluida:</span><span class="sxs-lookup"><span data-stu-id="a3f15-106">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="a3f15-107">Colecciones de recursos</span><span class="sxs-lookup"><span data-stu-id="a3f15-107">Resource collections</span></span>

<span data-ttu-id="a3f15-108">El objeto `Microsoft.Azure.Management.Fluent.Azure` mostrado anteriormente es el punto de entrada de toda la creación de recursos en las bibliotecas de administración fluida.</span><span class="sxs-lookup"><span data-stu-id="a3f15-108">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="a3f15-109">Seleccione el tipo de recursos con los que trabajar con las colecciones de recursos del objeto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-109">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="a3f15-110">Por ejemplo, para SQL Database:</span><span class="sxs-lookup"><span data-stu-id="a3f15-110">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="a3f15-111">Como ya se ha visto, las "conversaciones" más fluidas que mantiene con la API comienzan con la selección de la colección de recursos adecuada para los recursos de Azure con los que necesita trabajar.</span><span class="sxs-lookup"><span data-stu-id="a3f15-111">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="a3f15-112">A continuación, IntelliSense en Visual Studio le guiará por la conversación.</span><span class="sxs-lookup"><span data-stu-id="a3f15-112">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![GIF de Intellisense en Visual Studio dirigiendo una conversación fluida](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="a3f15-114">Listas e iteraciones</span><span class="sxs-lookup"><span data-stu-id="a3f15-114">Lists and iterations</span></span>

<span data-ttu-id="a3f15-115">Cada colección de recursos tiene un método `List()` que devuelve todas las instancias de ese recurso en la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="a3f15-115">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="a3f15-116">Por ejemplo, `Azure.SqlServers.List()` devuelve todos los servidores SQL de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="a3f15-116">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="a3f15-117">Use el método `ListByResourceGroup()` para establecer el ámbito de la lista devuelta en un determinado [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="a3f15-117">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="a3f15-118">Recorra en iteración la colección devuelta simplemente como lo haría con una `List<T>` normal:</span><span class="sxs-lookup"><span data-stu-id="a3f15-118">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="a3f15-119">Verbos procesables</span><span class="sxs-lookup"><span data-stu-id="a3f15-119">Actionable verbs</span></span>

<span data-ttu-id="a3f15-120">Los métodos de colección de recursos con verbos en sus nombres realizan una acción inmediata en Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f15-120">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="a3f15-121">Estos métodos funcionan de forma sincrónica y bloquean la ejecución en el subproceso actual hasta que terminan.</span><span class="sxs-lookup"><span data-stu-id="a3f15-121">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="a3f15-122">Verbo</span><span class="sxs-lookup"><span data-stu-id="a3f15-122">Verb</span></span>   |  <span data-ttu-id="a3f15-123">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="a3f15-123">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="a3f15-124">Crear</span><span class="sxs-lookup"><span data-stu-id="a3f15-124">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="a3f15-125">Aplicar</span><span class="sxs-lookup"><span data-stu-id="a3f15-125">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="a3f15-126">Eliminar</span><span class="sxs-lookup"><span data-stu-id="a3f15-126">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="a3f15-127">Enumerar</span><span class="sxs-lookup"><span data-stu-id="a3f15-127">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="a3f15-128">Obtener</span><span class="sxs-lookup"><span data-stu-id="a3f15-128">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="a3f15-129">`Define()` y `Update()` son verbos, pero no producen bloqueos a menos que vayan seguidos por `Create()` o `Apply()`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-129">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="a3f15-130">Algunos objetos de recursos tienen verbos que cambian el estado del recurso en Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f15-130">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="a3f15-131">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="a3f15-131">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="a3f15-132">La mayoría de los métodos descritos en esta sección tienen también una versión asincrónica, indicada con el sufijo `Async`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-132">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="a3f15-133">Creación de recursos diferida</span><span class="sxs-lookup"><span data-stu-id="a3f15-133">Lazy resource creation</span></span>

<span data-ttu-id="a3f15-134">Se produce un problema al crear recursos de Azure cuando un nuevo recurso depende de otro recurso que aún no existe.</span><span class="sxs-lookup"><span data-stu-id="a3f15-134">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="a3f15-135">Un ejemplo de ello sería reservar una dirección IP pública y configurar un disco al crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a3f15-135">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="a3f15-136">No desea comprobar la reserva de la dirección ni la creación del disco, sino simplemente configurar la máquina virtual con esos recursos.</span><span class="sxs-lookup"><span data-stu-id="a3f15-136">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="a3f15-137">Use objetos que se pueden crear para definir recursos de Azure para utilizarlos en su código, pero créelos solo cuando se necesiten en Azure.</span><span class="sxs-lookup"><span data-stu-id="a3f15-137">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="a3f15-138">El código escrito con objetos que se pueden crear descarga la creación de recursos en el entorno de Azure a la API de administración, lo que incrementa el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="a3f15-138">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="a3f15-139">Genere objetos que se pueden crear mediante el verbo `Define()` de las colecciones de recursos sin un verbo `Create()`:</span><span class="sxs-lookup"><span data-stu-id="a3f15-139">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="a3f15-140">El recurso de Azure definido por el objeto que se puede crear no existe todavía en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="a3f15-140">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="a3f15-141">Un objeto que se puede crear es una representación local de un recurso que la API de administración creará cuando sea necesario (cuando se llama a `.Create()`).</span><span class="sxs-lookup"><span data-stu-id="a3f15-141">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="a3f15-142">Use este objeto que se puede crear en la definición de otros recursos de Azure que necesiten este recurso.</span><span class="sxs-lookup"><span data-stu-id="a3f15-142">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="a3f15-143">Cree los recursos en su suscripción de Azure mediante el método `Create()` para la colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3f15-143">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="a3f15-144">Al pasar objetos que se pueden crear a `Create()`, se devuelve un objeto `ICreatedResources` en lugar de un objeto de recurso único.</span><span class="sxs-lookup"><span data-stu-id="a3f15-144">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="a3f15-145">El objeto `CreatedRelatedResource` le permite tener acceso a todos los recursos creados por la llamada a `Create()` y no solo al tipo de la colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="a3f15-145">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="a3f15-146">Para tener acceso a la dirección IP pública creada en Azure para la máquina virtual creada en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="a3f15-146">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="a3f15-147">Control de excepciones</span><span class="sxs-lookup"><span data-stu-id="a3f15-147">Exception handling</span></span>

<span data-ttu-id="a3f15-148">La API de administración define clases de excepción que extienden `Microsoft.Rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-148">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="a3f15-149">Puede detectar las excepciones generadas por la API de administración con un bloque `catch (RestException exception)` después de la correspondiente instrucción `try`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-149">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="a3f15-150">Registros y seguimiento</span><span class="sxs-lookup"><span data-stu-id="a3f15-150">Logs and tracing</span></span>

<span data-ttu-id="a3f15-151">El registro de las bibliotecas de administración de Azure fluidas para .NET aprovecha el seguimiento del cliente del servicio [AutoRest](https://github.com/Azure/AutoRest) subyacente.</span><span class="sxs-lookup"><span data-stu-id="a3f15-151">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="a3f15-152">Cree una clase que implemente `Microsoft.Rest.IServiceClientTracingInterceptor`.</span><span class="sxs-lookup"><span data-stu-id="a3f15-152">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="a3f15-153">Esta clase será responsable de interceptar mensajes de registro y pasarlos a cualquier mecanismo de registro que esté usando.</span><span class="sxs-lookup"><span data-stu-id="a3f15-153">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="a3f15-154">En este ejemplo, solo se escriben mensajes en la consola, pero también puede pasarlos a Log4Net, `Microsoft.Extensions.Logging` o cualquier otra plataforma de registro.</span><span class="sxs-lookup"><span data-stu-id="a3f15-154">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

```csharp
class ConsoleTracer : IServiceClientTracingInterceptor
{
    public void Information(string message)
    {
        Console.WriteLine(message);
    }

    public void TraceError(string invocationId, Exception exception)
    {
        Console.WriteLine("Exception in {0}: {1}", invocationId, exception);
    }

    public void ReceiveResponse(string invocationId, HttpResponseMessage response) { }

    public void SendRequest(string invocationId, HttpRequestMessage request) { }

    public void Configuration(string source, string name, string value) { }

    public void EnterMethod(string invocationId, object instance, string method, IDictionary<string, object> parameters) { }

    public void ExitMethod(string invocationId, object returnValue) { }
}
```

<span data-ttu-id="a3f15-155">Antes de crear el objeto `Microsoft.Azure.Management.Fluent.Azure`, inicialice la clase `IServiceClientTracingInterceptor` que creó anteriormente llamando a `ServiceClientTracing.AddTracingInterceptor()` y establezca `ServiceClientTracing.IsEnabled` en *true*.</span><span class="sxs-lookup"><span data-stu-id="a3f15-155">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="a3f15-156">Al crear el objeto `Azure`, incluya los métodos `.WithDelegatingHandler()` y `.WithLogLevel()` para conectar el cliente al seguimiento del cliente del servicio de AutoRest.</span><span class="sxs-lookup"><span data-stu-id="a3f15-156">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

```csharp
ServiceClientTracing.AddTracingInterceptor(new ConsoleTracer());
ServiceClientTracing.IsEnabled = true;

var azure = Azure
    .Configure()
    .WithDelegatingHandler(new HttpLoggingDelegatingHandler())
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

<span data-ttu-id="a3f15-157">Los niveles de registro `HttpLoggingDelegatingHandler` se definen de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="a3f15-157">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="a3f15-158">Nivel de seguimiento</span><span class="sxs-lookup"><span data-stu-id="a3f15-158">Trace level</span></span> | <span data-ttu-id="a3f15-159">Registro habilitado</span><span class="sxs-lookup"><span data-stu-id="a3f15-159">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="a3f15-160">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="a3f15-160">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="a3f15-161">Sin salida</span><span class="sxs-lookup"><span data-stu-id="a3f15-161">No output</span></span>
| <span data-ttu-id="a3f15-162">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="a3f15-162">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="a3f15-163">Registra las direcciones URL de las llamadas REST subyacentes, con códigos de respuesta y hora</span><span class="sxs-lookup"><span data-stu-id="a3f15-163">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="a3f15-164">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="a3f15-164">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="a3f15-165">Se registra lo incluido en el nivel BASIC más los cuerpos de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="a3f15-165">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="a3f15-166">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="a3f15-166">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="a3f15-167">Se registra lo incluido en el nivel BASIC más los encabezados de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="a3f15-167">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="a3f15-168">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="a3f15-168">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="a3f15-169">Se registra todo lo incluido en los niveles de registro BODY y HEADERS</span><span class="sxs-lookup"><span data-stu-id="a3f15-169">Everything in both Body and Headers log level</span></span>
