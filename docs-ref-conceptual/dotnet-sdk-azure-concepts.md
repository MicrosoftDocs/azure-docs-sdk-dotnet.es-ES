---
title: "Conceptos de uso y patrones de las bibliotecas de administración de Azure para .NET"
description: 
keywords: Azure, .NET, SDK, API, patrones, conceptos, fluidez, registro
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: b2e6849f06c36de18471e55c468e984f4205f646
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-library-for-net-fluent-concepts"></a><span data-ttu-id="68b5b-103">Biblioteca de administración de Azure para conceptos fluidos de .NET</span><span class="sxs-lookup"><span data-stu-id="68b5b-103">Azure management library for .NET fluent concepts</span></span>

<span data-ttu-id="68b5b-104">Este artículo le ayudará a aprender a utilizar de forma eficaz la interfaz fluida de las bibliotecas de administración de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="68b5b-104">This article will help you understand how to effectively use the fluent interface in the Azure management libraries for .NET.</span></span>

## <a name="building-resources-using-a-fluent-interface"></a><span data-ttu-id="68b5b-105">Creación de recursos con una interfaz fluida</span><span class="sxs-lookup"><span data-stu-id="68b5b-105">Building resources using a fluent interface</span></span>

<span data-ttu-id="68b5b-106">Una interfaz fluida es un tipo específico de patrón de generador que crea objetos mediante una cadena de método que aplica la configuración correcta de un recurso.</span><span class="sxs-lookup"><span data-stu-id="68b5b-106">A fluent interface is a specific form of the builder pattern that creates objects through a method chain that enforces correct configuration of a resource.</span></span> <span data-ttu-id="68b5b-107">Por ejemplo, el objeto de Azure de punto de entrada se crea mediante una interfaz fluida:</span><span class="sxs-lookup"><span data-stu-id="68b5b-107">For example, the entry-point Azure object is created using a fluent interface:</span></span>

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a><span data-ttu-id="68b5b-108">Colecciones de recursos</span><span class="sxs-lookup"><span data-stu-id="68b5b-108">Resource collections</span></span>

<span data-ttu-id="68b5b-109">El objeto `Microsoft.Azure.Management.Fluent.Azure` mostrado anteriormente es el punto de entrada de toda la creación de recursos en las bibliotecas de administración fluida.</span><span class="sxs-lookup"><span data-stu-id="68b5b-109">The `Microsoft.Azure.Management.Fluent.Azure` object shown above is the entry point for all resource creation in the fluent management libraries.</span></span> <span data-ttu-id="68b5b-110">Seleccione el tipo de recursos con los que trabajar con las colecciones de recursos del objeto `Azure`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-110">Select which type of resources to work with using the resource collections in the `Azure` object.</span></span> <span data-ttu-id="68b5b-111">Por ejemplo, para SQL Database:</span><span class="sxs-lookup"><span data-stu-id="68b5b-111">For example, for SQL Database:</span></span>

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

<span data-ttu-id="68b5b-112">Como ya se ha visto, las "conversaciones" más fluidas que mantiene con la API comienzan con la selección de la colección de recursos adecuada para los recursos de Azure con los que necesita trabajar.</span><span class="sxs-lookup"><span data-stu-id="68b5b-112">As seen above, most fluent "conversations" you have with the API start with selecting the appropriate resource collection for the Azure resources you need to work with.</span></span>  <span data-ttu-id="68b5b-113">A continuación, IntelliSense en Visual Studio le guiará por la conversación.</span><span class="sxs-lookup"><span data-stu-id="68b5b-113">Intellisense in Visual Studio then guides you through the conversation.</span></span> 

![GIF de Intellisense en Visual Studio dirigiendo una conversación fluida](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a><span data-ttu-id="68b5b-115">Listas e iteraciones</span><span class="sxs-lookup"><span data-stu-id="68b5b-115">Lists and iterations</span></span>

<span data-ttu-id="68b5b-116">Cada colección de recursos tiene un método `List()` que devuelve todas las instancias de ese recurso en la suscripción actual.</span><span class="sxs-lookup"><span data-stu-id="68b5b-116">Every resource collection has a `List()` method to return every instance of that resource in your current subscription.</span></span> <span data-ttu-id="68b5b-117">Por ejemplo, `Azure.SqlServers.List()` devuelve todos los servidores SQL de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="68b5b-117">For example, `Azure.SqlServers.List()` returns all SQL servers in the subscription.</span></span>

<span data-ttu-id="68b5b-118">Use el método `ListByResourceGroup()` para establecer el ámbito de la lista devuelta en un determinado [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="68b5b-118">Use the `ListByResourceGroup()` method to scope the returned List to a specific [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).</span></span>  

<span data-ttu-id="68b5b-119">Recorra en iteración la colección devuelta simplemente como lo haría con una `List<T>` normal:</span><span class="sxs-lookup"><span data-stu-id="68b5b-119">Iterate over the returned collection just as you would a normal `List<T>`:</span></span>

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a><span data-ttu-id="68b5b-120">Verbos procesables</span><span class="sxs-lookup"><span data-stu-id="68b5b-120">Actionable verbs</span></span>

<span data-ttu-id="68b5b-121">Los métodos de colección de recursos con verbos en sus nombres realizan una acción inmediata en Azure.</span><span class="sxs-lookup"><span data-stu-id="68b5b-121">Resource collection methods with verbs in their names take immediate action in Azure.</span></span> <span data-ttu-id="68b5b-122">Estos métodos funcionan de forma sincrónica y bloquean la ejecución en el subproceso actual hasta que terminan.</span><span class="sxs-lookup"><span data-stu-id="68b5b-122">These methods work synchronously and block execution in the current thread until they complete.</span></span> 

| <span data-ttu-id="68b5b-123">Verbo</span><span class="sxs-lookup"><span data-stu-id="68b5b-123">Verb</span></span>   |  <span data-ttu-id="68b5b-124">Ejemplo de uso</span><span class="sxs-lookup"><span data-stu-id="68b5b-124">Sample usage</span></span> |
|--------|---------------|
| <span data-ttu-id="68b5b-125">Crear</span><span class="sxs-lookup"><span data-stu-id="68b5b-125">Create</span></span> | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| <span data-ttu-id="68b5b-126">Aplicar</span><span class="sxs-lookup"><span data-stu-id="68b5b-126">Apply</span></span>  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| <span data-ttu-id="68b5b-127">Eliminar</span><span class="sxs-lookup"><span data-stu-id="68b5b-127">Delete</span></span> | `azure.Disks.DeleteById(id)` | 
| <span data-ttu-id="68b5b-128">Enumerar</span><span class="sxs-lookup"><span data-stu-id="68b5b-128">List</span></span>   | `azure.SqlServers.List()` | 
| <span data-ttu-id="68b5b-129">Obtener</span><span class="sxs-lookup"><span data-stu-id="68b5b-129">Get</span></span>    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> <span data-ttu-id="68b5b-130">`Define()` y `Update()` son verbos pero no bloquean a menos que vayan seguidos por `Create()` o `Apply()`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-130">`Define()` and `Update()` are verbs but do not block unless followed by a `Create()` or `Apply()`.</span></span>
 
<span data-ttu-id="68b5b-131">Algunos objetos de recursos tienen verbos que cambian el estado del recurso en Azure.</span><span class="sxs-lookup"><span data-stu-id="68b5b-131">Specific resource objects have verbs that change the state of the resource in Azure.</span></span> <span data-ttu-id="68b5b-132">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="68b5b-132">For example:</span></span>

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

<span data-ttu-id="68b5b-133">La mayoría de los métodos descritos en esta sección tienen también una versión asincrónica, indicada con el sufijo `Async`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-133">Most of the methods described in this section have an asynchronous version as well, denoted by the suffix `Async`.</span></span>

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a><span data-ttu-id="68b5b-134">Creación de recursos diferida</span><span class="sxs-lookup"><span data-stu-id="68b5b-134">Lazy resource creation</span></span>

<span data-ttu-id="68b5b-135">Se produce un problema al crear recursos de Azure cuando un nuevo recurso depende de otro recurso que aún no existe.</span><span class="sxs-lookup"><span data-stu-id="68b5b-135">A challenge when creating Azure resources arises when a new resource depends on another resource that doesn't yet exist.</span></span> <span data-ttu-id="68b5b-136">Un ejemplo de ello sería reservar una dirección IP pública y configurar un disco al crear una nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="68b5b-136">An example is reserving a public IP address and setting up a disk when creating a new virtual machine.</span></span> <span data-ttu-id="68b5b-137">No desea comprobar la reserva de la dirección ni la creación del disco, sino simplemente configurar la máquina virtual con esos recursos.</span><span class="sxs-lookup"><span data-stu-id="68b5b-137">You don't want to verify reserving the address or the creating the disk, you just want to configure the virtual machine with those resources.</span></span>

<span data-ttu-id="68b5b-138">Use objetos que se pueden crear para definir recursos de Azure para utilizarlos en su código, pero créelos solo cuando se necesiten en Azure.</span><span class="sxs-lookup"><span data-stu-id="68b5b-138">Use creatable objects to define Azure resources for use in your code but only create them when needed in Azure.</span></span> <span data-ttu-id="68b5b-139">El código escrito con objetos que se pueden crear descarga la creación de recursos en el entorno de Azure a la API de administración, lo que incrementa el rendimiento.</span><span class="sxs-lookup"><span data-stu-id="68b5b-139">Code written with creatable objects offloads resource creation in the Azure environment to the management API, boosting performance.</span></span> 

<span data-ttu-id="68b5b-140">Genere objetos que se pueden crear mediante el verbo `Define()` de las colecciones de recursos sin un verbo `Create()`:</span><span class="sxs-lookup"><span data-stu-id="68b5b-140">Generate creatable objects through the resource collections' `Define()` verb without a `Create()` verb:</span></span>

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

<span data-ttu-id="68b5b-141">El recurso de Azure definido por el objeto que se puede crear no existe todavía en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="68b5b-141">The Azure resource defined by the creatable object does not yet exist in your subscription.</span></span> <span data-ttu-id="68b5b-142">Un objeto que se puede crear es una representación local de un recurso que la API de administración creará cuando sea necesario (cuando se llama a `.Create()`).</span><span class="sxs-lookup"><span data-stu-id="68b5b-142">A creatable object is a local representation of a resource that the management API will create when it's needed (when `.Create()` is called).</span></span> <span data-ttu-id="68b5b-143">Use este objeto que se puede crear en la definición de otros recursos de Azure que necesiten este recurso.</span><span class="sxs-lookup"><span data-stu-id="68b5b-143">Use this creatable object in the definition of other Azure resources that need this resource.</span></span> 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

<span data-ttu-id="68b5b-144">Cree los recursos en su suscripción de Azure mediante el método `Create()` para la colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="68b5b-144">Create the resources in your Azure subscription using the `Create()` method for the resource collection.</span></span> 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

<span data-ttu-id="68b5b-145">Al pasar objetos que se pueden crear a `Create()`, se devuelve un objeto `ICreatedResources` en lugar de un objeto de recurso único.</span><span class="sxs-lookup"><span data-stu-id="68b5b-145">Passing creatable objects to `Create()` returns a `ICreatedResources` object instead of a single resource object.</span></span>  <span data-ttu-id="68b5b-146">El objeto `CreatedRelatedResource` le permite tener acceso a todos los recursos creados por la llamada a `Create()` y no solo al tipo de la colección de recursos.</span><span class="sxs-lookup"><span data-stu-id="68b5b-146">The `CreatedRelatedResource` object lets you access all resources created by the `Create()` call, not just the type from the resource collection.</span></span> <span data-ttu-id="68b5b-147">Para tener acceso a la dirección IP pública creada en Azure para la máquina virtual creada en el ejemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="68b5b-147">To access the public IP address created in Azure for the virtual machine created in the above example:</span></span>

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a><span data-ttu-id="68b5b-148">Control de excepciones</span><span class="sxs-lookup"><span data-stu-id="68b5b-148">Exception handling</span></span>

<span data-ttu-id="68b5b-149">La API de administración define clases de excepción que extienden `Microsoft.Rest.RestException`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-149">The management API defines exception classes that extend `Microsoft.Rest.RestException`.</span></span> <span data-ttu-id="68b5b-150">Puede detectar las excepciones generadas por la API de administración con un bloque `catch (RestException exception)` después de la correspondiente instrucción `try`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-150">Catch exceptions generated by management API, with a `catch (RestException exception)` block after the relevant `try` statement.</span></span>

## <a name="logs-and-tracing"></a><span data-ttu-id="68b5b-151">Registros y seguimiento</span><span class="sxs-lookup"><span data-stu-id="68b5b-151">Logs and tracing</span></span>

<span data-ttu-id="68b5b-152">El registro de las bibliotecas de administración de Azure fluidas para .NET aprovecha el seguimiento del cliente del servicio [AutoRest](https://github.com/Azure/AutoRest) subyacente.</span><span class="sxs-lookup"><span data-stu-id="68b5b-152">Logging in the fluent Azure management libraries for .NET leverages the underlying [AutoRest](https://github.com/Azure/AutoRest) service client tracing.</span></span>

<span data-ttu-id="68b5b-153">Cree una clase que implemente `Microsoft.Rest.IServiceClientTracingInterceptor`.</span><span class="sxs-lookup"><span data-stu-id="68b5b-153">Create a class that implements `Microsoft.Rest.IServiceClientTracingInterceptor`.</span></span>  <span data-ttu-id="68b5b-154">Esta clase será responsable de interceptar mensajes de registro y pasarlos a cualquier mecanismo de registro que esté usando.</span><span class="sxs-lookup"><span data-stu-id="68b5b-154">This class will be responsible for intercepting log messages and passing them to whatever logging mechanism you're using.</span></span>  <span data-ttu-id="68b5b-155">En este ejemplo, solo se escriben mensajes en la consola, pero también puede pasarlos a Log4Net, `Microsoft.Extensions.Logging` o cualquier otra plataforma de registro.</span><span class="sxs-lookup"><span data-stu-id="68b5b-155">In this example, we're just writing messages to the console, but you could also pass them to Log4Net, `Microsoft.Extensions.Logging`, or any other logging framework.</span></span>

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

<span data-ttu-id="68b5b-156">Antes de crear el objeto `Microsoft.Azure.Management.Fluent.Azure`, inicialice la clase `IServiceClientTracingInterceptor` que creó anteriormente llamando a `ServiceClientTracing.AddTracingInterceptor()` y establezca `ServiceClientTracing.IsEnabled` en *true*.</span><span class="sxs-lookup"><span data-stu-id="68b5b-156">Before creating the `Microsoft.Azure.Management.Fluent.Azure` object, initialize the `IServiceClientTracingInterceptor` you created above by calling `ServiceClientTracing.AddTracingInterceptor()` and set `ServiceClientTracing.IsEnabled` to *true*.</span></span>  <span data-ttu-id="68b5b-157">Al crear el objeto `Azure`, incluya los métodos `.WithDelegatingHandler()` y `.WithLogLevel()` para conectar el cliente al seguimiento del cliente del servicio de AutoRest.</span><span class="sxs-lookup"><span data-stu-id="68b5b-157">When you create the `Azure` object, include the `.WithDelegatingHandler()` and `.WithLogLevel()` methods to wire up the client to AutoRest's service client tracing.</span></span>

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

<span data-ttu-id="68b5b-158">Los niveles de registro `HttpLoggingDelegatingHandler` se definen de la manera siguiente:</span><span class="sxs-lookup"><span data-stu-id="68b5b-158">The `HttpLoggingDelegatingHandler` log levels are defined as follows:</span></span>

| <span data-ttu-id="68b5b-159">Nivel de seguimiento</span><span class="sxs-lookup"><span data-stu-id="68b5b-159">Trace level</span></span> | <span data-ttu-id="68b5b-160">Registro habilitado</span><span class="sxs-lookup"><span data-stu-id="68b5b-160">Logging enabled</span></span> 
| ------------ | ---------------
| <span data-ttu-id="68b5b-161">HttpLoggingDelegatingHandler.Level.None</span><span class="sxs-lookup"><span data-stu-id="68b5b-161">HttpLoggingDelegatingHandler.Level.None</span></span> | <span data-ttu-id="68b5b-162">Sin salida</span><span class="sxs-lookup"><span data-stu-id="68b5b-162">No output</span></span>
| <span data-ttu-id="68b5b-163">HttpLoggingDelegatingHandler.Level.Basic</span><span class="sxs-lookup"><span data-stu-id="68b5b-163">HttpLoggingDelegatingHandler.Level.Basic</span></span> | <span data-ttu-id="68b5b-164">Registra las direcciones URL de las llamadas REST subyacentes, con códigos de respuesta y hora</span><span class="sxs-lookup"><span data-stu-id="68b5b-164">Logs the URLs to underlying REST calls, response codes and times</span></span>
| <span data-ttu-id="68b5b-165">HttpLoggingDelegatingHandler.Level.Body</span><span class="sxs-lookup"><span data-stu-id="68b5b-165">HttpLoggingDelegatingHandler.Level.Body</span></span> | <span data-ttu-id="68b5b-166">Se registra lo incluido en el nivel BASIC más los cuerpos de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="68b5b-166">Everything in Basic plus request and response bodies for the REST calls</span></span>
| <span data-ttu-id="68b5b-167">HttpLoggingDelegatingHandler.Level.Headers</span><span class="sxs-lookup"><span data-stu-id="68b5b-167">HttpLoggingDelegatingHandler.Level.Headers</span></span> | <span data-ttu-id="68b5b-168">Se registra lo incluido en el nivel BASIC más los encabezados de solicitud y respuesta de las llamadas REST</span><span class="sxs-lookup"><span data-stu-id="68b5b-168">Everything in Basic plus the request and response headers REST calls</span></span>
| <span data-ttu-id="68b5b-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span><span class="sxs-lookup"><span data-stu-id="68b5b-169">HttpLoggingDelegatingHandler.Level.BodyAndHeaders</span></span> | <span data-ttu-id="68b5b-170">Se registra todo lo incluido en los niveles de registro BODY y HEADERS</span><span class="sxs-lookup"><span data-stu-id="68b5b-170">Everything in both Body and Headers log level</span></span>
