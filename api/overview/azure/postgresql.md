---
title: Bibliotecas de Azure Database para PostgreSQL para .NET
description: "Documentación de referencia para las bibliotecas de cliente de .NET para Azure Database para PostgreSQL"
keywords: Azure, .NET ODBC, SDK, API, SQL, ADO.NET, base de datos, PostGres, PostgreSQL
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: postgresql
ms.openlocfilehash: 899002b12dd36e6b23a05c8516670ff841abed79
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-postgresql-libraries-for-net"></a>Bibliotecas de Azure Database para PostgreSQL para .NET

## <a name="overview"></a>Información general

Trabajo con datos y recursos almacenados en [Azure Database para PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

## <a name="client-api"></a>API de cliente

La biblioteca de cliente recomendada para acceder a Azure Database para PostgreSQL es código abierto [proveedor de datos Npgsql ADO.NET](http://www.npgsql.org/) de código abierto. Utilice el proveedor ADO.NET para conectarse a la base de datos y ejecutar instrucciones SQL directamente o a través de Entity Framework con los proveedores [Entity Framework 6](http://www.npgsql.org/ef6/index.html) o [Entity Framework Core](http://www.npgsql.org/efcore/index.html) de Npgsql.

Instale el [paquete NuGet](https://www.nuget.org/packages/Npgsql) directamente desde la [Consola del Administrador de paquetes] de Visual Studio [PackageManager] o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Npgsql
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package Npgsql
```

### <a name="code-example"></a>Ejemplo de código

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

### <a name="samples"></a>Muestras

- [Ejemplos de código de ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Diseño una base de datos PostgreSQL mediante la CLI de Azure](https://docs.microsoft.com/azure/postgresql/tutorial-design-database-using-azure-cli) [PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console [DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package