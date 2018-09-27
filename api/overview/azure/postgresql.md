---
title: Bibliotecas de Azure Database para PostgreSQL para .NET
description: Documentación de referencia para las bibliotecas de cliente de .NET para Azure Database para PostgreSQL
ms.date: 10/19/2017
ms.topic: reference
ms.service: postgresql
ms.openlocfilehash: 4137e024eadba93c9cb3e94c1e7478d0816f8370
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190753"
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a><span data-ttu-id="c0cd2-103">Bibliotecas de Azure Database para PostgreSQL para .NET</span><span class="sxs-lookup"><span data-stu-id="c0cd2-103">Azure Database for PostgreSQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="c0cd2-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c0cd2-104">Overview</span></span>

<span data-ttu-id="c0cd2-105">Trabajo con datos y recursos almacenados en [Azure Database para PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="c0cd2-105">Work with data and resources stored in [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-api"></a><span data-ttu-id="c0cd2-106">API de cliente</span><span class="sxs-lookup"><span data-stu-id="c0cd2-106">Client API</span></span>

<span data-ttu-id="c0cd2-107">La biblioteca de cliente recomendada para acceder a Azure Database para PostgreSQL es código abierto [proveedor de datos Npgsql ADO.NET](http://www.npgsql.org/) de código abierto.</span><span class="sxs-lookup"><span data-stu-id="c0cd2-107">The recommended client library for accessing Azure Database for PostgreSQL is the open-source [Npgsql ADO.NET data provider](http://www.npgsql.org/).</span></span> <span data-ttu-id="c0cd2-108">Utilice el proveedor ADO.NET para conectarse a la base de datos y ejecutar instrucciones SQL directamente o a través de Entity Framework con los proveedores [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) de Npgsql.</span><span class="sxs-lookup"><span data-stu-id="c0cd2-108">Use the ADO.NET provider to connect to the database and execute SQL statements directly or through Entity Framework with the Npgsql's [Entity Framework 6](http://www.npgsql.org/ef6/index.html) or [Entity Framework Core](http://www.npgsql.org/efcore/index.html) providers.</span></span>

<span data-ttu-id="c0cd2-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Npgsql) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="c0cd2-109">Install the [NuGet package](https://www.nuget.org/packages/Npgsql) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="c0cd2-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0cd2-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a><span data-ttu-id="c0cd2-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="c0cd2-111">.NET Core CLI</span></span>

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a><span data-ttu-id="c0cd2-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="c0cd2-112">Code Example</span></span>

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

### <a name="samples"></a><span data-ttu-id="c0cd2-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c0cd2-113">Samples</span></span>

- [<span data-ttu-id="c0cd2-114">Ejemplos de código de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="c0cd2-114">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="c0cd2-115">Diseño de una base de datos PostgreSQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="c0cd2-115">Design a PostgreSQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli)


[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
