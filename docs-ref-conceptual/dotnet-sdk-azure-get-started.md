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
# <a name="get-started-with-the-azure-net-and-net-core-apis"></a><span data-ttu-id="0fa1e-104">Introducción a las API de .NET y .NET Core de Azure</span><span class="sxs-lookup"><span data-stu-id="0fa1e-104">Get started with the Azure .NET and .NET Core APIs</span></span>

<span data-ttu-id="0fa1e-105">En este tutorial se demuestra el uso de varias [API de Azure para .NET](/dotnet/api/overview/azure/).</span><span class="sxs-lookup"><span data-stu-id="0fa1e-105">This tutorial demonstrates the usage of several [Azure APIs for .NET](/dotnet/api/overview/azure/).</span></span>  <span data-ttu-id="0fa1e-106">Configurará la autenticación, creará y usará una cuenta de Azure Storage, creará y usará una instancia de Azure SQL Database, implementará algunas máquinas virtuales e implementará una aplicación web de Azure App Service desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0fa1e-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0fa1e-107">Prerequisites</span></span>

- <span data-ttu-id="0fa1e-108">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-108">An Azure account.</span></span> <span data-ttu-id="0fa1e-109">Si no tiene una, [consiga una evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0fa1e-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/)</span></span>

## <a name="set-up-authentication"></a><span data-ttu-id="0fa1e-110">Configuración de la autenticación</span><span class="sxs-lookup"><span data-stu-id="0fa1e-110">Set up authentication</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="create-a-new-project"></a><span data-ttu-id="0fa1e-111">Creación de un nuevo proyecto</span><span class="sxs-lookup"><span data-stu-id="0fa1e-111">Create a new project</span></span> 

<span data-ttu-id="0fa1e-112">Cree un nuevo proyecto de aplicación de consola.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-112">Create a new console application project.</span></span>  <span data-ttu-id="0fa1e-113">En Visual Studio, haga clic en **Archivo**, **Nuevo** y luego haga clic en **Proyecto...** .  En las plantillas de Visual C#, seleccione **Aplicación de consola (.NET Core)**, asigne un nombre a su proyecto y luego haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-113">In Visual Studio, do this by clicking **File**, **New**, and then clicking **Project...**.  Under the Visual C# templates, select **Console App (.NET Core)**, name your project, and then click **OK**.</span></span>

![Cuadro de diálogo Nuevo proyecto](media/dotnet-sdk-azure-get-started/new-project.png)

<span data-ttu-id="0fa1e-115">Cuando se cree la nueva aplicación de consola, abra la Consola del Administrador de paquetes; para ello, haga clic en **Herramientas**, **Administrador de paquetes de NuGet** y luego haga clic en **Consola del Administrador de paquetes**.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-115">When the new console app is created, open the Package Manager Console by clicking **Tools**, **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>  <span data-ttu-id="0fa1e-116">En la consola, ejecute los tres comandos siguientes para obtener los paquetes que necesita:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-116">In the console, get the packages you'll need by executing the following three commands:</span></span>

```powershell
# Azure Management Libraries for .NET (Fluent)
Install-Package Microsoft.Azure.Management.Fluent

# Azure Store client libraries
Install-Package WindowsAzure.Storage

# SQL Database client libraries
Install-Package System.Data.SqlClient
```

## <a name="directives"></a><span data-ttu-id="0fa1e-117">Directivas</span><span class="sxs-lookup"><span data-stu-id="0fa1e-117">Directives</span></span>

<span data-ttu-id="0fa1e-118">Edite el archivo `Program.cs` de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-118">Edit your application's `Program.cs` file.</span></span>  <span data-ttu-id="0fa1e-119">Reemplace las directivas `using` de la parte superior por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-119">Replace the `using` directives at the top with the following:</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="0fa1e-120">de una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0fa1e-120">Create a virtual machine</span></span>

<span data-ttu-id="0fa1e-121">En este ejemplo se implementa una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-121">This example deploys a virtual machine.</span></span> 

<span data-ttu-id="0fa1e-122">Reemplace el método `Main` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-122">Replace the `Main` method with the following.</span></span>  <span data-ttu-id="0fa1e-123">No olvide proporcionar valores reales de `username` y `password` para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-123">Be sure to provide an actual `username` and `password` for the virtual machine.</span></span>

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

<span data-ttu-id="0fa1e-124">Presione **F5** para ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-124">Press **F5** to run the sample.</span></span>

<span data-ttu-id="0fa1e-125">Al cabo de varios minutos, el programa finalizará y le pedirá que presione Entrar.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-125">After several minutes, the program will finish, prompting you to press enter.</span></span> <span data-ttu-id="0fa1e-126">Presione ENTRAR y, después, compruebe la máquina virtual de su suscripción con Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-126">After pressing enter, verify the virtual machine in your subscription with the Cloud Shell:</span></span>

```azurecli-interactive
az vm list
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="0fa1e-127">Implementación de una aplicación web desde un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="0fa1e-127">Deploy a web app from a GitHub repo</span></span>

<span data-ttu-id="0fa1e-128">Ahora, modificará el código para crear e implementar una nueva aplicación web desde un repositorio de GitHub existente.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-128">Now you'll modify your code to create a deploy a new web app from an existing GitHub repository.</span></span> <span data-ttu-id="0fa1e-129">Reemplace el método `Main` por el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-129">Replace the `Main` method with the following code:</span></span>

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

<span data-ttu-id="0fa1e-130">Ejecute el código como antes con **F5**.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-130">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="0fa1e-131">Compruebe la implementación; para ello, abra un explorador y navegue hasta la dirección URL que se muestra en la consola.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-131">Verify the deployment by opening a browser and navigating to URL displayed in the console.</span></span>

## <a name="connect-to-a-sql-database"></a><span data-ttu-id="0fa1e-132">Conexión a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="0fa1e-132">Connect to a SQL database</span></span>

<span data-ttu-id="0fa1e-133">En este ejemplo se crea una nueva instancia de Azure SQL Database y se realizan algunas operaciones SQL.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-133">This example creates a new Azure SQL Database and performs a few SQL operations.</span></span>

<span data-ttu-id="0fa1e-134">Reemplace el método `Main` por lo siguiente y asegúrese de asignar una contraseña segura para `dbPassword`:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-134">Replace the `Main` method with the following, making sure to assign a strong password for `dbPassword`:</span></span>

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

<span data-ttu-id="0fa1e-135">Ejecute el código como antes con **F5**.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-135">Run the code as before by pressing **F5**.</span></span>  <span data-ttu-id="0fa1e-136">La salida de la consola debe validar que el servidor se ha creado y que funciona según lo esperado, pero puede conectarse a él directamente con una herramienta como SQL Server Management Studio si así lo desea.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-136">The console output should validate that the server was created and works as expected, but you can connect to it directly with a tool like SQL Server Management Studio if you like.</span></span>

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="0fa1e-137">Escritura de un blob en una nueva cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="0fa1e-137">Write a blob into a new storage account</span></span>

<span data-ttu-id="0fa1e-138">En este ejemplo se crea una cuenta de almacenamiento y se carga un blob.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-138">This example creates a storage account and upload a blob.</span></span>  

<span data-ttu-id="0fa1e-139">Reemplace el método `Main` por lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-139">Replace the `Main` method with the following.</span></span>

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

<span data-ttu-id="0fa1e-140">Presione **F5** para ejecutar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-140">Press **F5** to run the sample.</span></span>

<span data-ttu-id="0fa1e-141">Varios minutos después, el programa finaliza.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-141">After several minutes, the program finishes.</span></span> <span data-ttu-id="0fa1e-142">Vaya a la dirección URL mostrada en la consola para comprobar que el blob se ha cargado.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-142">Verify the blob was uploaded by browsing to the URL displayed in the console.</span></span>  <span data-ttu-id="0fa1e-143">Debería ver el texto "Hello, Azure!"</span><span class="sxs-lookup"><span data-stu-id="0fa1e-143">You should see the text "Hello, Azure!"</span></span> <span data-ttu-id="0fa1e-144">en el explorador.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-144">in your browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="0fa1e-145">Limpieza</span><span class="sxs-lookup"><span data-stu-id="0fa1e-145">Clean up</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0fa1e-146">Si no limpia los recursos de este tutorial, le seguirán cobrando por ellos.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-146">If you don't clean up your resources from this tutorial, you will continue to be charged for them.</span></span>  <span data-ttu-id="0fa1e-147">Asegúrese de realizar este paso.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-147">Be sure to do this step.</span></span>

<span data-ttu-id="0fa1e-148">Para eliminar todos los recursos que ha creado, escriba lo siguiente en Cloud Shell:</span><span class="sxs-lookup"><span data-stu-id="0fa1e-148">Delete all the resources you created by entering the following in the Cloud Shell:</span></span>

```azurecli-interactive
az group delete --name sampleResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="0fa1e-149">Ver más ejemplos</span><span class="sxs-lookup"><span data-stu-id="0fa1e-149">Explore more samples</span></span>

<span data-ttu-id="0fa1e-150">Para aprender más sobre cómo usar las bibliotecas de Azure para .NET para administrar recursos y automatizar tareas, consulte nuestro código de ejemplo para [máquinas virtuales](dotnet-sdk-azure-virtual-machine-samples.md), [aplicaciones web](dotnet-sdk-azure-web-apps-samples.md) y [bases de datos SQL](dotnet-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0fa1e-150">To learn more about how to use the Azure libraries for .NET to manage resources and automate tasks, see our sample code for [virtual machines](dotnet-sdk-azure-virtual-machine-samples.md), [web apps](dotnet-sdk-azure-web-apps-samples.md) and [SQL database](dotnet-sdk-azure-sql-database-samples.md).</span></span>

## <a name="reference"></a><span data-ttu-id="0fa1e-151">Referencia</span><span class="sxs-lookup"><span data-stu-id="0fa1e-151">Reference</span></span>

<span data-ttu-id="0fa1e-152">Hay una [referencia](http://docs.microsoft.com/dotnet/api) disponible para todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="0fa1e-152">A [reference](http://docs.microsoft.com/dotnet/api) is available for all packages.</span></span>

[!include[Contribute and community](includes/contribute.md)]
