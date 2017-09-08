---
title: Bibliotecas de Azure Database para MySQL para .NET
description: "Documentación de referencia para las bibliotecas de cliente de .NET para Azure Database para MySQL"
keywords: Azure, .NET, SDK, API, SQL, base de datos, MySQL
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/17/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: mysql
ms.openlocfilehash: 1bc373d63b0172fd554277a6ef30fa09772a395b
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-database-for-mysql-libraries-for-net"></a><span data-ttu-id="1e990-104">Bibliotecas de Azure Database para MySQL para .NET</span><span class="sxs-lookup"><span data-stu-id="1e990-104">Azure Database for MySQL libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="1e990-105">Información general</span><span class="sxs-lookup"><span data-stu-id="1e990-105">Overview</span></span>

<span data-ttu-id="1e990-106">Trabajo con datos y recursos almacenados en [Azure Database para MySQL](/azure/mysql/overview).</span><span class="sxs-lookup"><span data-stu-id="1e990-106">Work with data and resources stored in [Azure Database for MySQL](/azure/mysql/overview).</span></span>

## <a name="client-apis"></a><span data-ttu-id="1e990-107">API de cliente</span><span class="sxs-lookup"><span data-stu-id="1e990-107">Client APIs</span></span>

<span data-ttu-id="1e990-108">La biblioteca de cliente recomendada para acceder a Azure Database para MySQL es [Connector/Net](https://dev.mysql.com/doc/connector-net/en) de MySQL.</span><span class="sxs-lookup"><span data-stu-id="1e990-108">The recommended client library for accessing Azure Database for MySQL is MySQL's [Connector/Net](https://dev.mysql.com/doc/connector-net/en).</span></span> <span data-ttu-id="1e990-109">Use el paquete para conectarse a la base de datos y ejecutar instrucciones SQL directamente.</span><span class="sxs-lookup"><span data-stu-id="1e990-109">Use the package to connect to the database and execute SQL statements directly.</span></span> 

<span data-ttu-id="1e990-110">Instale el [paquete NuGet](https://www.nuget.org/packages/MySql.Data) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="1e990-110">Install the [NuGet package](https://www.nuget.org/packages/MySql.Data) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="1e990-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1e990-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package MySql.Data
```

#### <a name="net-core-cli"></a><span data-ttu-id="1e990-112">CLI de .NET Core</span><span class="sxs-lookup"><span data-stu-id="1e990-112">.NET Core CLI</span></span>

```bash
dotnet add package MySql.Data
```

### <a name="code-example"></a><span data-ttu-id="1e990-113">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="1e990-113">Code Example</span></span>

<span data-ttu-id="1e990-114">Conexión a una base de datos MySQL y ejecución de una consulta:</span><span class="sxs-lookup"><span data-stu-id="1e990-114">Connect to a MySQL database and execute a query:</span></span>

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

## <a name="samples"></a><span data-ttu-id="1e990-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="1e990-115">Samples</span></span>

- [<span data-ttu-id="1e990-116">Ejemplos de código de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="1e990-116">ADO.NET code examples</span></span>](/dotnet/framework/data/adonet/ado-net-code-examples)
- [<span data-ttu-id="1e990-117">Diseño de una base de datos MySQL mediante la CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="1e990-117">Design a MySQL database using the Azure CLI</span></span>](https://docs.microsoft.com/azure/mysql/tutorial-design-database-using-cli) 

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
