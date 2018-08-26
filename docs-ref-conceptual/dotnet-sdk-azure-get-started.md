---
title: Introducción a las API de .NET y .NET Core de Azure
description: Adéntrese en el uso básico de las bibliotecas de Azure para .NET y .NET Core con su propia suscripción de Azure.
keywords: Azure,. NET, .NET Core, ASP.NET, ASP.NET Core SDK, API, autenticar, introducción
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 08/22/2018
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: ad894e47704fcccc83f7d02acb8e418b167993f9
ms.sourcegitcommit: b2a53a3aea9de6720bd975fb7fe4e722e9d182a3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/23/2018
ms.locfileid: "42703058"
---
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a>Introducción a las API de .NET y .NET Core de Azure

En este tutorial se demuestra el uso de varias [API de Azure para .NET](/dotnet/api/overview/azure/).  Configurará la autenticación, creará y usará una cuenta de Azure Storage, creará y usará una instancia de Azure SQL Database, implementará algunas máquinas virtuales e implementará una aplicación web de Azure App Service desde GitHub.

## <a name="prerequisites"></a>Requisitos previos

- Una cuenta de Azure. Si no tiene una, [consiga una evaluación gratuita](https://azure.microsoft.com/free/).

## <a name="set-up-authentication"></a>Configuración de la autenticación

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a>Creación de un nuevo proyecto 

Cree un nuevo proyecto de aplicación de consola.  En Visual Studio, haga clic en **Archivo**, **Nuevo** y luego haga clic en **Proyecto...** .  En las plantillas de Visual C#, seleccione **Aplicación de consola (.NET Core)**, asigne un nombre a su proyecto y luego haga clic en **Aceptar**.

![Cuadro de diálogo Nuevo proyecto](media/dotnet-sdk-azure-get-started/new-project.png)

Cuando se cree la nueva aplicación de consola, abra la Consola del Administrador de paquetes; para ello, haga clic en **Herramientas**, **Administrador de paquetes de NuGet** y luego haga clic en **Consola del Administrador de paquetes**.  En la consola, ejecute los tres comandos siguientes para obtener los paquetes que necesita:

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a>Directivas

Edite el archivo `Program.cs` de la aplicación.  Reemplace las directivas `using` de la parte superior por lo siguiente:

```csharp
using System;
using System.Linq;
using Microsoft.Azure.Management.Compute.Fluent;
using Microsoft.Azure.Management.Compute.Fluent.Models;
using Microsoft.Azure.Management.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Data.SqlClient;
```

## <a name="create-a-virtual-machine"></a>de una máquina virtual

En este ejemplo se implementa una máquina virtual. 

Reemplace el método `Main` por lo siguiente:  No olvide proporcionar valores reales de `username` y `password` para la máquina virtual.

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string username = "MY_USERNAME";
    string password = "MY_PASSWORD";
    string rgName = "sampleResourceGroup";
    string windowsVmName = "sampleWindowsVM";
    string publicIpDnsLabel = "samplePublicIP" + (new Random().Next(0,100000)).ToString();

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the VM
    Console.WriteLine("Creating VM...");
    var windowsVM = azure.VirtualMachines.Define(windowsVmName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewPrimaryNetwork("10.0.0.0/28")
        .WithPrimaryPrivateIPAddressDynamic()
        .WithNewPrimaryPublicIPAddress(publicIpDnsLabel)
        .WithPopularWindowsImage(KnownWindowsVirtualMachineImage.WindowsServer2012R2Datacenter)
        .WithAdminUsername(username)
        .WithAdminPassword(password)
        .WithSize(VirtualMachineSizeTypes.StandardD2V2)
        .Create();

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Presione **F5** para ejecutar el ejemplo.

Al cabo de varios minutos, el programa finalizará y le pedirá que presione Entrar. Presione ENTRAR y, después, compruebe la máquina virtual de su suscripción con Cloud Shell:

```azurecli-interactive
az vm list
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>Implementación de una aplicación web desde un repositorio de GitHub

Ahora, modificará el código para crear e implementar una nueva aplicación web desde un repositorio de GitHub existente. Reemplace el método `Main` por el código siguiente:

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string appName = SdkContext.RandomResourceName("WebApp", 20);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the web app
    Console.WriteLine("Creating Web App...");
    var app = azure.WebApps.Define(appName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithNewFreeAppServicePlan()
        .DefineSourceControl()
        .WithPublicGitRepository("https://github.com/Azure-Samples/app-service-web-dotnet-get-started")
        .WithBranch("master")
        .Attach()
        .Create();
    Console.WriteLine("Your web app is live at: https://{0}", app.HostNames.First());

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Ejecute el código como antes con **F5**.  Compruebe la implementación; para ello, abra un explorador y navegue hasta la dirección URL que se muestra en la consola.

## <a name="connect-to-a-sql-database"></a>Conexión a una base de datos SQL

En este ejemplo se crea una nueva instancia de Azure SQL Database y se realizan algunas operaciones SQL.

Reemplace el método `Main` por lo siguiente y asegúrese de asignar una contraseña segura para `dbPassword`:

```csharp
 static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string adminUser = SdkContext.RandomResourceName("db", 8);
    string sqlServerName = SdkContext.RandomResourceName("sql", 10);
    string sqlDbName = SdkContext.RandomResourceName("dbname", 8);
    string dbPassword = "YOUR_PASSWORD_HERE";

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the SQL server and database
    Console.WriteLine("Creating server...");
    var sqlServer = azure.SqlServers.Define(sqlServerName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .WithAdministratorLogin(adminUser)
        .WithAdministratorPassword(dbPassword)
        .WithNewFirewallRule("0.0.0.0", "255.255.255.255")
        .Create();

    Console.WriteLine("Creating database...");
    var sqlDb = sqlServer.Databases.Define(sqlDbName).Create();

    // Display information for connecting later...
    Console.WriteLine("Created database {0} in server {1}.", sqlDbName, sqlServer.FullyQualifiedDomainName);
    Console.WriteLine("Your user name is {0}.", adminUser + "@" + sqlServer.Name);

    // Build the connection string
    var builder = new SqlConnectionStringBuilder();
    builder.DataSource = sqlServer.FullyQualifiedDomainName;
    builder.InitialCatalog = sqlDbName;
    builder.UserID = adminUser + "@" + sqlServer.Name; // Format user ID as "user@server"
    builder.Password = dbPassword;
    builder.Encrypt = true;
    builder.TrustServerCertificate = true;

    // connect to the database, create a table and insert an entry into it
    using (var conn = new SqlConnection(builder.ConnectionString))
    {
        conn.Open();

        Console.WriteLine("Populating database...");
        var createCommand = new SqlCommand("CREATE TABLE CLOUD (name varchar(255), code int);", conn);
        createCommand.ExecuteNonQuery();

        var insertCommand = new SqlCommand("INSERT INTO CLOUD (name, code ) VALUES ('Azure', 1);", conn);
        insertCommand.ExecuteNonQuery();

        Console.WriteLine("Reading from database...");
        var selectCommand = new SqlCommand("SELECT * FROM CLOUD", conn);
        var results = selectCommand.ExecuteReader();
        while(results.Read())
        {
            Console.WriteLine("Name: {0} Code: {1}", results[0], results[1]);
        }
    }

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Ejecute el código como antes con **F5**.  La salida de la consola debe validar que el servidor se ha creado y que funciona según lo esperado, pero puede conectarse a él directamente con una herramienta como SQL Server Management Studio si así lo desea.

## <a name="write-a-blob-into-a-new-storage-account"></a>Escritura de un blob en una nueva cuenta de almacenamiento

En este ejemplo se crea una cuenta de almacenamiento y se carga un blob.  

Reemplace el método `Main` por lo siguiente:

```csharp
static void Main(string[] args)
{
    // Set some variables...
    string rgName = "sampleResourceGroup";
    string storageAccountName = SdkContext.RandomResourceName("st", 10);

    // Authenticate
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .Authenticate(credentials)
        .WithDefaultSubscription();

    // Create the storage account
    Console.WriteLine("Creating storage account...");
    var storage = azure.StorageAccounts.Define(storageAccountName)
        .WithRegion(Region.USEast)
        .WithNewResourceGroup(rgName)
        .Create();

    var storageKeys = storage.GetKeys();
    string storageConnectionString = "DefaultEndpointsProtocol=https;"
        + "AccountName=" + storage.Name
        + ";AccountKey=" + storageKeys[0].Value
        + ";EndpointSuffix=core.windows.net";

    var account = CloudStorageAccount.Parse(storageConnectionString);
    var serviceClient = account.CreateCloudBlobClient();

    // Create container. Name must be lower case.
    Console.WriteLine("Creating container...");
    var container = serviceClient.GetContainerReference("helloazure");
    container.CreateIfNotExistsAsync().Wait();

    // Make the container public
    var containerPermissions = new BlobContainerPermissions()
        { PublicAccess = BlobContainerPublicAccessType.Container };
    container.SetPermissionsAsync(containerPermissions).Wait();

    // write a blob to the container
    Console.WriteLine("Uploading blob...");
    var blob = container.GetBlockBlobReference("helloazure.txt");
    blob.UploadTextAsync("Hello, Azure!").Wait();
    Console.WriteLine("Your blob is located at {0}", blob.StorageUri.PrimaryUri);

    // Wait for the user
    Console.WriteLine("Press enter to continue...");
    Console.ReadLine();
}
```

Presione **F5** para ejecutar el ejemplo.

Varios minutos después, el programa finaliza. Vaya a la dirección URL mostrada en la consola para comprobar que el blob se ha cargado.  Debería ver el texto "Hello, Azure!" en el explorador.

## <a name="clean-up"></a>Limpieza

> [!IMPORTANT]
> Si no limpia los recursos de este tutorial, le seguirán cobrando por ellos.  Asegúrese de realizar este paso.

Para eliminar todos los recursos que ha creado, escriba lo siguiente en Cloud Shell:

```azurecli-interactive
az group delete --name sampleResourceGroup
```

## <a name="explore-more-samples"></a>Ver más ejemplos

Para aprender más sobre cómo usar las bibliotecas de Azure para .NET para administrar recursos y automatizar tareas, consulte nuestro código de ejemplo para [máquinas virtuales](dotnet-sdk-azure-virtual-machine-samples.md), [aplicaciones web](dotnet-sdk-azure-web-apps-samples.md) y [bases de datos SQL](dotnet-sdk-azure-sql-database-samples.md).

## <a name="reference"></a>Referencia

Hay una [referencia](http://docs.microsoft.com/dotnet/api) disponible para todos los paquetes.

[!include[Contribute and community](includes/contribute.md)]
