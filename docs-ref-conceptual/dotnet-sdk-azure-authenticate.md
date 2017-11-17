---
title: "Autenticación con las bibliotecas de Azure para .NET"
description: "Autenticación en las bibliotecas de Azure para .NET"
keywords: "Azure, .NET, SDK, API, autenticación, active directory, entidad de servicio"
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: c9755d7e9c20186c7677b4bfe69d4033f9852607
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a><span data-ttu-id="8eaf2-104">Autenticación con las bibliotecas de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="8eaf2-104">Authenticate with the Azure Libraries for .NET</span></span>

## <a name="connect-to-services-with-connection-strings"></a><span data-ttu-id="8eaf2-105">Conexión a los servicios con cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="8eaf2-105">Connect to services with connection strings</span></span>

<span data-ttu-id="8eaf2-106">La mayoría de las bibliotecas de servicio de Azure necesitan claves o una cadena de conexión para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-106">Most Azure service libraries require a connection string or keys for authentication.</span></span> <span data-ttu-id="8eaf2-107">Por ejemplo, SQL Database usa una cadena de conexión SQL estándar:</span><span class="sxs-lookup"><span data-stu-id="8eaf2-107">For example, SQL Database uses a standard SQL connection string:</span></span>

```csharp
var builder = new SqlConnectionStringBuilder();
builder.DataSource = "example.database.windows.net";
builder.InitialCatalog = "MyDatabase";
builder.UserID = "sampleuser@example"; // Format user ID as "user@server"
builder.Password = password;
builder.Encrypt = true;
builder.TrustServerCertificate = true;
                
using (var conn = new SqlConnection(builder.ConnectionString))
{
    conn.Open();
    // Do things with the connection...
    // ...
}
```

<span data-ttu-id="8eaf2-108">Azure Storage usa una clave de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="8eaf2-108">Azure Storage uses a storage key:</span></span>

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

<span data-ttu-id="8eaf2-109">Las cadenas de conexión de servicio se utilizan en otros servicios de Azure como [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) y [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues), y puede obtener estas cadenas mediante Azure Portal, la CLI o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-109">Service connection strings are used in other Azure services like [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache), and [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues) and you can get those strings using the Azure portal, CLI, or PowerShell.</span></span>  <span data-ttu-id="8eaf2-110">También puede usar las bibliotecas de administración de Azure para .NET para consultar recursos para generar cadenas de conexión en el código.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-110">You can also use the Azure management libraries for .NET to query resources to build connection strings in your code.</span></span> 

<span data-ttu-id="8eaf2-111">Este fragmento de código usa las bibliotecas de administración para crear una cadena de conexión de la cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="8eaf2-111">This snippet uses the management libraries to create a storage account connection string:</span></span>

```csharp
// Get a storage account
var storage = azure.StorageAccounts.GetByResourceGroup("myResourceGroup", "myStorageAccount");

// Extract the keys
var storageKeys = storage.GetKeys();

// Build the connection string
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

// Connect
var account = CloudStorageAccount.Parse(storageConnectionString);

// Do things with the account here...
```

<span data-ttu-id="8eaf2-112">Otras bibliotecas requieren que la aplicación se ejecute con una [entidad de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza la ejecución de la aplicación con las credenciales otorgadas.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-112">Other libraries require your application to run with a [service principal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) authorizing the application to run with granted credentials.</span></span> <span data-ttu-id="8eaf2-113">Esta configuración es similar a los pasos de la autenticación basada en objetos para la biblioteca de administración que se enumeran a continuación.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-113">This configuration is similar to the object-based authentication steps for the management library listed below.</span></span>

## <span data-ttu-id="8eaf2-114"><a name="mgmt-auth"></a>Bibliotecas de administración de Azure para .NET y Java</span><span class="sxs-lookup"><span data-stu-id="8eaf2-114"><a name="mgmt-auth"></a>Azure management libraries for .NET authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

<span data-ttu-id="8eaf2-115">Ahora que ya está creada la entidad de servicio, hay dos opciones disponibles para autenticarse en la entidad de servicio para crear y administrar los recursos.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-115">Now that the service principal is created, two options are available to authenticate to the service principal to create and manage resources.</span></span>

<span data-ttu-id="8eaf2-116">En ambas opciones, debe agregar los siguientes paquetes NuGet al proyecto.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-116">For both options you will need to add the following nuget packages to your project.</span></span>

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a><span data-ttu-id="8eaf2-117">Autenticación con credenciales de token</span><span class="sxs-lookup"><span data-stu-id="8eaf2-117">Authenticate with token credentials</span></span>

<span data-ttu-id="8eaf2-118">El primer método consiste en generar el objeto de credencial de token en el código.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-118">The first method is to build the token credential object in code.</span></span>  <span data-ttu-id="8eaf2-119">Debe almacenar las credenciales de forma segura en un archivo de configuración, el Registro o Azure KeyVault.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-119">You should store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

- <span data-ttu-id="8eaf2-120">clientId: use el valor de *ApplicationId* de la salida de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-120">clientId: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="8eaf2-121">clientSecret: use el parámetro *-Password* asignado al ejecutar `New-AzureRmADServicePrincipal` (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="8eaf2-121">clientSecret: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="8eaf2-122">tenantId: use el valor de *TenantId* obtenido cuando ejecutó `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-122">tenantId: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="8eaf2-123">Después, cree el objeto `Azure` de punto de entrada para empezar a trabajar con la API:</span><span class="sxs-lookup"><span data-stu-id="8eaf2-123">Then create the entry point `Azure` object to start working with the API:</span></span>

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <span data-ttu-id="8eaf2-124"><a name="mgmt-file"></a>Autenticación basada en archivo</span><span class="sxs-lookup"><span data-stu-id="8eaf2-124"><a name="mgmt-file"></a>File-based authentication</span></span>

<span data-ttu-id="8eaf2-125">La autenticación basada en archivo permite colocar las credenciales de la entidad de servicio en un archivo de texto sin formato y protegerlo en el sistema de archivos.</span><span class="sxs-lookup"><span data-stu-id="8eaf2-125">File-based authentication allows you to put the service principal credentials in a plain text file and secure it within the file system.</span></span>

[!include[File-based authentication](includes/file-based-auth.md)]

<span data-ttu-id="8eaf2-126">Lea el contenido del archivo y cree el objeto `Azure` de punto de entrada para empezar a trabajar con la API:</span><span class="sxs-lookup"><span data-stu-id="8eaf2-126">Read the contents of the file and create the entry point `Azure` object to start working with the API:</span></span>

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
