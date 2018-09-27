---
title: Bibliotecas de Power BI Embedded para .NET
description: Referencia de las bibliotecas de Power BI Embedded para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: multiple
ms.openlocfilehash: acb327b56e89522142e51016a6a9b279f995a674
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190378"
---
# <a name="power-bi-embedded-libraries-for-net"></a><span data-ttu-id="5cec8-103">Bibliotecas de Power BI Embedded para .NET</span><span class="sxs-lookup"><span data-stu-id="5cec8-103">Power BI Embedded libraries for .NET</span></span>

<span data-ttu-id="5cec8-104">[Power BI](https://powerbi.microsoft.com/) es un servicio de análisis empresarial basado en la nube que ofrece una vista única de sus datos empresariales más importantes.</span><span class="sxs-lookup"><span data-stu-id="5cec8-104">[Power BI](https://powerbi.microsoft.com/) is a cloud-based business analytics service that gives you a single view of your most critical business data.</span></span>

<span data-ttu-id="5cec8-105">Para más información sobre el uso de Power BI con .NET, consulte [Inserción con Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span><span class="sxs-lookup"><span data-stu-id="5cec8-105">To learn more about using Power BI with .NET, see [Embedding with Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).</span></span>

## <a name="client-library"></a><span data-ttu-id="5cec8-106">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="5cec8-106">Client library</span></span>

<span data-ttu-id="5cec8-107">Use la biblioteca de cliente para conectarse con las API de Power BI para acceder e interactuar con conjuntos de datos e informes.</span><span class="sxs-lookup"><span data-stu-id="5cec8-107">Use the client library to connect with Power BI APIs to access and interact with data sets and reports.</span></span>

<span data-ttu-id="5cec8-108">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5cec8-108">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directly from the Visual Studio [Package Manager console][PackageManager].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="5cec8-109">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5cec8-109">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a><span data-ttu-id="5cec8-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="5cec8-110">Example</span></span>

<span data-ttu-id="5cec8-111">En el ejemplo siguiente se recupera y se muestra una lista de conjuntos de datos e informes.</span><span class="sxs-lookup"><span data-stu-id="5cec8-111">The following example retrieves and displays a list of datasets and reports.</span></span>

```csharp
/* Include these'using' directive:
using Microsoft.PowerBI.Api.V2;
using Microsoft.PowerBI.Api.V2.Models;
*/
using (PowerBIClient client = new PowerBIClient(new Uri(apiUrl), tokenCredentials))
{

    Console.WriteLine("\r*** DATASETS ***\r");

    // List of datasets in a group/app workspace
    ODataResponseListDataset datasetList = client.Datasets.GetDatasetsInGroup(groupId);

    foreach(Dataset ds in datasetList.Value)
    {
        Console.WriteLine(ds.Id + " | " + ds.Name);
    }

    Console.WriteLine("\r*** REPORTS ***\r");

    // List of reports in a group/app workspace
    ODataResponseListReport reportList = client.Reports.GetReportsInGroup(groupId);

    foreach (Report rpt in reportList.Value)
    {
        Console.WriteLine(rpt.Id + " | " + rpt.Name +  " | DatasetID = " + rpt.DatasetId);
    }
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="5cec8-112">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="5cec8-112">Explore the client APIs</span></span>](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a><span data-ttu-id="5cec8-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="5cec8-113">Samples</span></span>

* [<span data-ttu-id="5cec8-114">Ejemplos para desarrolladores de Power BI</span><span class="sxs-lookup"><span data-stu-id="5cec8-114">Power BI Developer Samples</span></span>](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [<span data-ttu-id="5cec8-115">Repositorio de GitHub de .NET de Power BI</span><span class="sxs-lookup"><span data-stu-id="5cec8-115">Power BI .NET GitHub repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)

<span data-ttu-id="5cec8-116">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5cec8-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
