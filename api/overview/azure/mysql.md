---
title: Bibliotecas de Azure Database para MySQL para .NET
description: Documentación de referencia para las bibliotecas de cliente de .NET para Azure Database para MySQL
ms.date: 10/19/2017
ms.topic: reference
ms.service: mysql
ms.openlocfilehash: 34550c7089a2ec05164f7a16f24bfc8b18391f8a
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190158"
---
# <a name="azure-database-for-mysql-libraries-for-net"></a>Bibliotecas de Azure Database para MySQL para .NET

## <a name="overview"></a>Información general

Trabajo con datos y recursos almacenados en [Azure Database para MySQL](/azure/mysql/overview).

## <a name="client-apis"></a>API de cliente

La biblioteca de cliente recomendada para acceder a Azure Database para MySQL es [Connector/Net](https://dev.mysql.com/doc/connector-net/en) de MySQL. Use el paquete para conectarse a la base de datos y ejecutar instrucciones SQL directamente. 

Instale el [paquete NuGet](https://www.nuget.org/packages/MySql.Data) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a>CLI de .NET Core

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a>Ejemplo de código

Conexión a una base de datos MySQL y ejecución de una consulta:

```csharp
/* Include this "using" directive...
using MySql.Data.MySqlClient;
*/

string connectionString = "Server=[servername].mysql.database.azure.com; " +
    "Database=myDataBase; Uid=[userid]@[servername]; Pwd=myPassword;";

// Best practice is to scope the MySqlConnection to a "using" block
using (MySqlConnection conn = new MySqlConnection(connectionString))
{
    // Connect to the database
    conn.Open();

    // Read rows
    MySqlCommand selectCommand = new MySqlCommand("SELECT * FROM MyTable", conn);
    MySqlDataReader results = selectCommand.ExecuteReader();
    
    // Enumerate over the rows
    while(results.Read())
    {
        Console.WriteLine("Column 0: {0} Column 1: {1}", results[0], results[1]);
    }
}
```

## <a name="samples"></a>Ejemplos

- [Ejemplos de código de ADO.NET](/dotnet/framework/data/adonet/ado-net-code-examples)
- [Diseño de una base de datos MySQL mediante la CLI de Azure](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
