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
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="81163-103">Bibliotecas de Azure Database para MySQL para .NET</span><span class="sxs-lookup"><span data-stu-id="81163-103">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="81163-104">Información general</span><span class="sxs-lookup"><span data-stu-id="81163-104">Overview</span></span>

<span data-ttu-id="81163-105">Trabajo con datos y recursos almacenados en [Azure Database para MySQL](/azure/mysql/overview).</span><span class="sxs-lookup"><span data-stu-id="81163-105">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="81163-106">API de cliente</span><span class="sxs-lookup"><span data-stu-id="81163-106">Client APIs</span></span>

<span data-ttu-id="81163-107">La biblioteca de cliente recomendada para acceder a Azure Database para MySQL es [Connector/Net](https://dev.mysql.com/doc/connector-net/en) de MySQL.</span><span class="sxs-lookup"><span data-stu-id="81163-107">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="81163-108">Use el paquete para conectarse a la base de datos y ejecutar instrucciones SQL directamente.</span><span class="sxs-lookup"><span data-stu-id="81163-108">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="81163-109">Instale el [paquete NuGet](https://www.nuget.org/packages/MySql.Data) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="81163-109">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="81163-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="81163-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="81163-111">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="81163-111">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="81163-112">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="81163-112">Code Example</span></span>

<span data-ttu-id="81163-113">Conexión a una base de datos MySQL y ejecución de una consulta:</span><span class="sxs-lookup"><span data-stu-id="81163-113">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="81163-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="81163-114">Samples</span></span>

- [<span data-ttu-id="81163-115">Ejemplos de código de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="81163-115">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="81163-116">Diseño de una base de datos MySQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="81163-116">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
