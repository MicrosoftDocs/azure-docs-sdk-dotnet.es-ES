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
# <a name="azure-management-library-for-net-fluent-concepts"></a>Biblioteca de administración de Azure para conceptos fluidos de .NET

Este artículo le ayudará a aprender a utilizar de forma eficaz la interfaz fluida de las bibliotecas de administración de Azure para .NET.

## <a name="building-resources-using-a-fluent-interface"></a>Creación de recursos con una interfaz fluida

Una interfaz fluida es un tipo específico de patrón de generador que crea objetos mediante una cadena de método que aplica la configuración correcta de un recurso. Por ejemplo, el objeto de Azure de punto de entrada se crea mediante una interfaz fluida:

```csharp
var azure = Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

## <a name="resource-collections"></a>Colecciones de recursos

El objeto `Microsoft.Azure.Management.Fluent.Azure` mostrado anteriormente es el punto de entrada de toda la creación de recursos en las bibliotecas de administración fluida. Seleccione el tipo de recursos con los que trabajar con las colecciones de recursos del objeto `Azure`. Por ejemplo, para SQL Database:

```csharp
var sql = azure.SqlServers.Define(sqlServerName)
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName)
    .WithAdministratorLogin(administratorLogin)
    .WithAdministratorPassword(administratorPassword)
    .Create();
```

Como ya se ha visto, las "conversaciones" más fluidas que mantiene con la API comienzan con la selección de la colección de recursos adecuada para los recursos de Azure con los que necesita trabajar.  A continuación, IntelliSense en Visual Studio le guiará por la conversación. 

![GIF de Intellisense en Visual Studio dirigiendo una conversación fluida](media/dotnet-sdk-azure-concepts/vs-fluent.gif)   

## <a name="lists-and-iterations"></a>Listas e iteraciones

Cada colección de recursos tiene un método `List()` que devuelve todas las instancias de ese recurso en la suscripción actual. Por ejemplo, `Azure.SqlServers.List()` devuelve todos los servidores SQL de la suscripción.

Use el método `ListByResourceGroup()` para establecer el ámbito de la lista devuelta en un determinado [grupo de recursos de Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups).  

Recorra en iteración la colección devuelta simplemente como lo haría con una `List<T>` normal:

```csharp
var vmList = azure.VirtualMachines.List();
foreach(var vm in vmList)
{
    Console.WriteLine("VM Name: {0}", vm.Name);
}
```   

## <a name="actionable-verbs"></a>Verbos procesables

Los métodos de colección de recursos con verbos en sus nombres realizan una acción inmediata en Azure. Estos métodos funcionan de forma sincrónica y bloquean la ejecución en el subproceso actual hasta que terminan. 

| Verbo   |  Ejemplo de uso |
|--------|---------------|
| Crear | `azure.VirtualMachines.Create(listOfVMCreatables)` |
| Aplicar  | `virtualMachineScaleSet.Update().WithCapacity(6).Apply()` |
| Eliminar | `azure.Disks.DeleteById(id)` | 
| Enumerar   | `azure.SqlServers.List()` | 
| Obtener    | `var vm  = azure.VirtualMachines.GetByResourceGroup(group, vmName)` |

>[!NOTE]
> `Define()` y `Update()` son verbos pero no bloquean a menos que vayan seguidos por `Create()` o `Apply()`.
 
Algunos objetos de recursos tienen verbos que cambian el estado del recurso en Azure. Por ejemplo:

```csharp
var vmToRestart = azure.VirtualMachines.GetById(id);
vmToRestart.Restart();
```

La mayoría de los métodos descritos en esta sección tienen también una versión asincrónica, indicada con el sufijo `Async`.

```csharp
Task restartTask = azure.VirtualMachines.GetById(id).RestartAsync();
```

## <a name="lazy-resource-creation"></a>Creación de recursos diferida

Se produce un problema al crear recursos de Azure cuando un nuevo recurso depende de otro recurso que aún no existe. Un ejemplo de ello sería reservar una dirección IP pública y configurar un disco al crear una nueva máquina virtual. No desea comprobar la reserva de la dirección ni la creación del disco, sino simplemente configurar la máquina virtual con esos recursos.

Use objetos que se pueden crear para definir recursos de Azure para utilizarlos en su código, pero créelos solo cuando se necesiten en Azure. El código escrito con objetos que se pueden crear descarga la creación de recursos en el entorno de Azure a la API de administración, lo que incrementa el rendimiento. 

Genere objetos que se pueden crear mediante el verbo `Define()` de las colecciones de recursos sin un verbo `Create()`:

```csharp
// Init a creatable Public IP Address
var publicIpAddressCreatable = azure.PublicIPAddresses.Define("publicIPAddressName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup(rgName);
```

El recurso de Azure definido por el objeto que se puede crear no existe todavía en su suscripción. Un objeto que se puede crear es una representación local de un recurso que la API de administración creará cuando sea necesario (cuando se llama a `.Create()`). Use este objeto que se puede crear en la definición de otros recursos de Azure que necesiten este recurso. 

```csharp
// Init a creatable VM using the creatable Public IP Address
var vmCreatable = azure.VirtualMachines.Define("creatableVM")
    // ...
    .withNewPrimaryPublicIPAddress(publicIPAddressCreatable)
    // ...
```

Cree los recursos en su suscripción de Azure mediante el método `Create()` para la colección de recursos. 

```csharp
// Create the VM and its Public IP Address
var virtualMachine = azure.VirtualMachines.Create(vmCreatable);
```

Al pasar objetos que se pueden crear a `Create()`, se devuelve un objeto `ICreatedResources` en lugar de un objeto de recurso único.  El objeto `CreatedRelatedResource` le permite tener acceso a todos los recursos creados por la llamada a `Create()` y no solo al tipo de la colección de recursos. Para tener acceso a la dirección IP pública creada en Azure para la máquina virtual creada en el ejemplo anterior:

```csharp
var pip = virtualMachine.CreatedRelatedResource(publicIPAddressCreatable.Key()) as PublicIPAddress;;
```    

## <a name="exception-handling"></a>Control de excepciones

La API de administración define clases de excepción que extienden `Microsoft.Rest.RestException`. Puede detectar las excepciones generadas por la API de administración con un bloque `catch (RestException exception)` después de la correspondiente instrucción `try`.

## <a name="logs-and-tracing"></a>Registros y seguimiento

El registro de las bibliotecas de administración de Azure fluidas para .NET aprovecha el seguimiento del cliente del servicio [AutoRest](https://github.com/Azure/AutoRest) subyacente.

Cree una clase que implemente `Microsoft.Rest.IServiceClientTracingInterceptor`.  Esta clase será responsable de interceptar mensajes de registro y pasarlos a cualquier mecanismo de registro que esté usando.  En este ejemplo, solo se escriben mensajes en la consola, pero también puede pasarlos a Log4Net, `Microsoft.Extensions.Logging` o cualquier otra plataforma de registro.

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

Antes de crear el objeto `Microsoft.Azure.Management.Fluent.Azure`, inicialice la clase `IServiceClientTracingInterceptor` que creó anteriormente llamando a `ServiceClientTracing.AddTracingInterceptor()` y establezca `ServiceClientTracing.IsEnabled` en *true*.  Al crear el objeto `Azure`, incluya los métodos `.WithDelegatingHandler()` y `.WithLogLevel()` para conectar el cliente al seguimiento del cliente del servicio de AutoRest.

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

Los niveles de registro `HttpLoggingDelegatingHandler` se definen de la manera siguiente:

| Nivel de seguimiento | Registro habilitado 
| ------------ | ---------------
| HttpLoggingDelegatingHandler.Level.None | Sin salida
| HttpLoggingDelegatingHandler.Level.Basic | Registra las direcciones URL de las llamadas REST subyacentes, con códigos de respuesta y hora
| HttpLoggingDelegatingHandler.Level.Body | Se registra lo incluido en el nivel BASIC más los cuerpos de solicitud y respuesta de las llamadas REST
| HttpLoggingDelegatingHandler.Level.Headers | Se registra lo incluido en el nivel BASIC más los encabezados de solicitud y respuesta de las llamadas REST
| HttpLoggingDelegatingHandler.Level.BodyAndHeaders | Se registra todo lo incluido en los niveles de registro BODY y HEADERS
