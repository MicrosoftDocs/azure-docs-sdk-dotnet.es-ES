---
title: Bibliotecas de Azure Database para PostgreSQL para .NET
description: "Documentación de referencia para las bibliotecas de cliente de .NET para Azure Database para PostgreSQL"
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, base de datos, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e3153a35845a2d7660aded64e5dbc3787c62afb6
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="4c213-104">Bibliotecas de Azure Database para PostgreSQL para .NET</span><span class="sxs-lookup"><span data-stu-id="4c213-104">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="4c213-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4c213-105">Overview</span></span>

<span data-ttu-id="4c213-106">Trabajo con datos y recursos almacenados en [Azure Database para PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="4c213-106">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="4c213-107">API de cliente</span><span class="sxs-lookup"><span data-stu-id="4c213-107">Client API</span></span>

<span data-ttu-id="4c213-108">La biblioteca de cliente recomendada para acceder a Azure Database para PostgreSQL es código abierto [proveedor de datos Npgsql ADO.NET](http://www.npgsql.org/) de código abierto.</span><span class="sxs-lookup"><span data-stu-id="4c213-108">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="4c213-109">Utilice el proveedor ADO.NET para conectarse a la base de datos y ejecutar instrucciones SQL directamente o a través de Entity Framework con los proveedores [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) de Npgsql.</span><span class="sxs-lookup"><span data-stu-id="4c213-109">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="4c213-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Npgsql) directamente desde la [Consola del Administrador de paquetes] de Visual Studio [PackageManager] o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="4c213-110">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="4c213-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4c213-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="4c213-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="4c213-112">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="4c213-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="4c213-113">Code Example</span></span>

```csharp
/* Include this 'using' directive...
using Npgsql;
*/

// Always store connection strings securely. 
string connectionString = "Server=[servername].postgres.database.azure.com; " +
    "Port=5432; Database=myDataBase; User Id=[userid]@[servername]; Password=password;";

// Best practice is to scope the NpgsqlConnection to a "using" block
using (NpgsqlConnection conn = new NpgsqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    NpgsqlCommand selectCommand = new NpgsqlCommand("SELECT * FROM MyTable", conn);
    NpgsqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

### <a name="samples"></a><span data-ttu-id="4c213-114">Muestras</span><span class="sxs-lookup"><span data-stu-id="4c213-114">Samples</span></span>

- [<span data-ttu-id="4c213-115">Ejemplos de código de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="4c213-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- <span data-ttu-id="4c213-116">[Diseño de una base de datos PostgreSQL mediante la CLI de Azure](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package</span><span class="sxs-lookup"><span data-stu-id="4c213-116">[Design a PostgreSQL database using the Azure CLI](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package</span></span>