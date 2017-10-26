---
title: API de Azure SQL Database para .NET
description: Referencia de las bibliotecas de Azure SQL Database para .NET
keywords: Azure, .NET, SDK, API, SQL, base de datos
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: sql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 61b98b3096123b509b5c9f08bfc654aa37cf2149
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-sql-database-apis-for-net"></a><span data-ttu-id="79302-104">API de Azure SQL Database para .NET</span><span class="sxs-lookup"><span data-stu-id="79302-104">Azure SQL Database APIs for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="79302-105">Información general</span><span class="sxs-lookup"><span data-stu-id="79302-105">Overview</span></span>

<span data-ttu-id="79302-106">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos basado en el motor Microsoft SQL Server que admite datos relacionales, de tabla, JSON, espaciales y XML.</span><span class="sxs-lookup"><span data-stu-id="79302-106">[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) is a database service using the Microsoft SQL Server engine that supports relational, JSON, spatial, and XML data.</span></span> 

<span data-ttu-id="79302-107">Para aprender más sobre el uso de SQL Database con .NET, consulte [Uso de .NET (C#) con Visual Studio para conectarse y consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="79302-107">To learn more about the using SQL Database with .NET, see [Use .NET with Visual Studio to connect and query an Azure SQL database](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).</span></span>

## <a name="client-library"></a><span data-ttu-id="79302-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="79302-108">Client library</span></span>

<span data-ttu-id="79302-109">Use la biblioteca de SQL para .NET para conectarse a su base de datos y autenticarse en ella y ejecutar instrucciones y procedimientos almacenados T-SQL ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="79302-109">Use the .NET SQL client library to connect and authenticate with your database and execute ad-hoc T-SQL statements and stored procedures.</span></span>

<span data-ttu-id="79302-110">Instale el [paquete NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) directamente desde la [Consola del Administrador de paquetes](https://docs.microsoft.com/nuget/tools/package-manager-console) de Visual Studio o con la [CLI de .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="79302-110">Install the [NuGet package]( https://www.nuget.org/packages/System.Data.SqlClient) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="79302-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79302-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a><span data-ttu-id="79302-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="79302-112">.NET Core CLI</span></span>

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a><span data-ttu-id="79302-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="79302-113">Code Example</span></span>

<span data-ttu-id="79302-114">En este ejemplo se conecta a una base de datos y se leen las filas de una tabla.</span><span class="sxs-lookup"><span data-stu-id="79302-114">This example connects to a database and reads rows from a table.</span></span>

```csharp
/* Include this 'using' directive...
using System.Data.SqlClient;
*/

// Always store connection strings securely. 
string connectionString = "Server=tcp:[serverName].database.windows.net;" 
    + "Database=myDataBase;User ID=[loginname]@[serverName];Password=myPassword;"
    + "Trusted_Connection=False;Encrypt=True;";

// Best practice is to scope the SqlConnection to a "using" block
using (SqlConnection conn = new SqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    SqlCommand selectCommand = new SqlCommand("SELECT * FROM MyTable", conn);
    SqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="79302-115">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="79302-115">Explore the client APIs</span></span>](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a><span data-ttu-id="79302-116">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="79302-116">Management library</span></span>

<span data-ttu-id="79302-117">Use la biblioteca de administración de Azure SQL Database para crear, administrar y escalar instancias de servidor de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="79302-117">Use the Azure SQL Database management library to create, manage, and scale Azure SQL Database server instances.</span></span>

<span data-ttu-id="79302-118">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directamente desde la [Consola del Administrador de paquetes](https://docs.microsoft.com/nuget/tools/package-manager-console) de Visual Studio o con la [CLI de .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span><span class="sxs-lookup"><span data-stu-id="79302-118">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directly from the Visual Studio [Package Manager console](https://docs.microsoft.com/nuget/tools/package-manager-console) or with the [.NET Core CLI](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="79302-119">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="79302-119">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a><span data-ttu-id="79302-120">Línea de comandos de .NET Core</span><span class="sxs-lookup"><span data-stu-id="79302-120">.NET Core command line</span></span>

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a><span data-ttu-id="79302-121">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="79302-121">Code Example</span></span>

<span data-ttu-id="79302-122">En este ejemplo se crea una nueva instancia de servidor de SQL Database y luego se crea una nueva base de datos en esa instancia.</span><span class="sxs-lookup"><span data-stu-id="79302-122">This example creates a new SQL Database server instance and then creates a new database on that instance.</span></span>

```csharp
/* Include these 'using' directives...
using Microsoft.Azure.Management.Sql.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

string startAddress = "0.0.0.0";
string endAddress = "255.255.255.255";

// Create the SQL server instance
ISqlServer sqlServer = azure.SqlServers.Define("UniqueServerName")
    .WithRegion(Region.USEast)
    .WithNewResourceGroup("ResourceGroupName")
    .WithAdministratorLogin("UserName")
    .WithAdministratorPassword("Password")
    .WithNewFirewallRule(startAddress, endAddress)
    .Create();

// Create the database
ISqlDatabase sqlDb = sqlServer.Databases.Define("DatabaseName").Create();
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="79302-123">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="79302-123">Explore the management APIs</span></span>](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a><span data-ttu-id="79302-124">Muestras</span><span class="sxs-lookup"><span data-stu-id="79302-124">Samples</span></span>

- [<span data-ttu-id="79302-125">Ejemplos de código de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="79302-125">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="79302-126">Ejemplos de bibliotecas de administración de Azure para .NET en SQL Database</span><span class="sxs-lookup"><span data-stu-id="79302-126">Azure management libraries for .NET samples for SQL Database</span></span>](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

<span data-ttu-id="79302-127">Vea la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database) de ejemplos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="79302-127">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database) of Azure SQL Database samples.</span></span>

