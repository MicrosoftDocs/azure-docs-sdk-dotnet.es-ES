---
title: API de Azure SQL Database para .NET
description: Referencia de las bibliotecas de Azure SQL Database para .NET
keywords: Azure, .NET, SDK, API, SQL, base de datos
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: sql
ms.openlocfilehash: 110b7e554666a4fa6386d6715919684e121441a3
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-sql-database-apis-for-net"></a>API de Azure SQL Database para .NET

## <a name="overview"></a>Información general

[Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-technical-overview) es un servicio de base de datos basado en el motor Microsoft SQL Server que admite datos relacionales, de tabla, JSON, espaciales y XML. 

Para aprender más sobre el uso de SQL Database con .NET, consulte [Uso de .NET (C#) con Visual Studio para conectarse y consultar una base de datos SQL de Azure](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-visual-studio).

## <a name="client-library"></a>Biblioteca de cliente

Use la biblioteca de SQL para .NET para conectarse a su base de datos y autenticarse en ella y ejecutar instrucciones y procedimientos almacenados T-SQL ad-hoc.

Instale el [paquete NuGet]( https://www.nuget.org/packages/System.Data.SqlClient) directamente desde la [Consola del Administrador de paquetes](https://docs.microsoft.com/nuget/tools/package-manager-console) de Visual Studio o con la [CLI de .NET Core](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package System.Data.SqlClient
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package System.Data.SqlClient
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se conecta a una base de datos y se leen las filas de una tabla.

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
> [Explorar las API de cliente](/dotnet/api/overview/azure/sql/client)

## <a name="management-library"></a>Biblioteca de administración

Use la biblioteca de administración de Azure SQL Database para crear, administrar y escalar instancias de servidor de Azure SQL Database.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql.Fluent/) directamente desde la [Consola del Administrador de paquetes](https://docs.microsoft.com/nuget/tools/package-manager-console) de Visual Studio o con la [CLI de .NET Core](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package).

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Sql.Fluent
``` 

#### <a name="net-core-command-line"></a>Línea de comandos de .NET Core

```bash
dotnet add package Microsoft.Azure.Management.Sql.Fluent
```

### <a name="code-example"></a>Ejemplo de código

En este ejemplo se crea una nueva instancia de servidor de SQL Database y luego se crea una nueva base de datos en esa instancia.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/sql/management)

## <a name="samples"></a>Muestras

- [Ejemplos de código de ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Ejemplos de bibliotecas de administración de Azure para .NET en SQL Database](/dotnet/azure/dotnet-sdk-azure-sql-database-samples)

Vea la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=dotnet&term=sql+database) de ejemplos de Azure SQL Database.

