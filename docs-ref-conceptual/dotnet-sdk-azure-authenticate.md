---
title: Autenticación con las bibliotecas de Azure para .NET
description: Autenticación en las bibliotecas de Azure para .NET
ms.date: 08/22/2018
ms.openlocfilehash: d0d8db89816a887fa23490a213917a3c554ecdb4
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190868"
---
# <a name="authenticate-with-the-azure-libraries-for-net"></a>Autenticación con las bibliotecas de Azure para .NET

## <a name="connect-to-services-with-connection-strings"></a>Conexión a los servicios con cadenas de conexión

La mayoría de las bibliotecas de servicio de Azure necesitan claves o una cadena de conexión para la autenticación. Por ejemplo, SQL Database usa una cadena de conexión SQL estándar:

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

Azure Storage usa una clave de almacenamiento:

```csharp
string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storageName
        + ";AccountKey=" + storageKey
        + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
// Do things with the account here...
```

Las cadenas de conexión de servicio se utilizan en otros servicios de Azure como [CosmosDB](/azure/documentdb/documentdb-dotnet-application#a-nametoc395637769astep-5-wiring-up-azure-cosmos-db), [Redis Cache](/azure/redis-cache/cache-dotnet-how-to-use-azure-redis-cache) y [Service Bus](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues), y puede obtener estas cadenas mediante Azure Portal, la CLI o PowerShell.  También puede usar las bibliotecas de administración de Azure para .NET para consultar recursos para generar cadenas de conexión en el código. 

Este fragmento de código usa las bibliotecas de administración para crear una cadena de conexión de la cuenta de almacenamiento:

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

Otras bibliotecas requieren que la aplicación se ejecute con una [entidad de servicio](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-objects) que autoriza la ejecución de la aplicación con las credenciales otorgadas. Esta configuración es similar a los pasos de la autenticación basada en objetos para la biblioteca de administración que se enumeran a continuación.

## <a name="mgmt-auth"></a>Bibliotecas de administración de Azure para .NET y Java

[!include[Create service principal](includes/create-sp.md)]

Ahora que ya está creada la entidad de servicio, hay dos opciones disponibles para autenticarse en la entidad de servicio para crear y administrar los recursos.

En ambas opciones, debe agregar los siguientes paquetes NuGet al proyecto.

```
Install-Package Microsoft.Azure.Management.Fluent
Install-Package Microsoft.Azure.Management.ResourceManager.Fluent
```

### <a name="authenticate-with-token-credentials"></a>Autenticación con credenciales de token

El primer método consiste en generar el objeto de credencial de token en el código.  Debe almacenar las credenciales de forma segura en un archivo de configuración, el Registro o Azure KeyVault.

```csharp
var credentials = SdkContext.AzureCredentialsFactory
    .FromServicePrincipal(clientId,
    clientSecret,
    tenantId, 
    AzureEnvironment.AzureGlobalCloud);
```

Use los valores de *clientId*, *clientSecret* y *tenantId* de la salida JSON de la creación de la entidad de servicio.

Después, cree el objeto `Azure` de punto de entrada para empezar a trabajar con la API:

```csharp
var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```

### <a name="mgmt-file"></a>Autenticación basada en archivo

La autenticación basada en archivo permite colocar las credenciales de la entidad de servicio en un archivo de texto sin formato y protegerlo en el sistema de archivos.

[!include[File-based authentication](includes/file-based-auth.md)]

Lea el contenido del archivo y cree el objeto `Azure` de punto de entrada para empezar a trabajar con la API:

```csharp
// pull in the location of the authentication properties file from the environment 
var credentials = SdkContext.AzureCredentialsFactory
    .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

var azure = Microsoft.Azure.Management.Fluent.Azure
    .Configure()
    .Authenticate(credentials)
    .WithDefaultSubscription();
```
