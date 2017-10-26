---
title: Bibliotecas de Power BI Embedded para .NET
description: Referencia de las bibliotecas de Power BI Embedded para .NET
keywords: Azure, .NET, SDK, API, Power BI Embedded
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, svc-overview
ms.openlocfilehash: f61c931d930fce75d038af8b8f1355f1de9cde7c
ms.sourcegitcommit: fe3e1475208ba47d4630788bac88b952cc3fe61f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2017
---
# <a name="power-bi-embedded-libraries-for-net"></a>Bibliotecas de Power BI Embedded para .NET

[Power BI](https://powerbi.microsoft.com/) es un servicio de análisis empresarial basado en la nube que ofrece una vista única de sus datos empresariales más importantes.

Para más información sobre el uso de Power BI con .NET, consulte [Inserción con Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-developer-embedding/).

## <a name="client-library"></a>Biblioteca de cliente

Use la biblioteca de cliente para conectarse con las API de Power BI para acceder e interactuar con conjuntos de datos e informes.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.PowerBI.Api) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio.

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.PowerBI.Api
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se recupera y se muestra una lista de conjuntos de datos e informes.

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
> [Explorar las API de cliente](https://powerbi.microsoft.com/documentation/powerbi-developer-rest-api-reference/)

## <a name="samples"></a>Muestras

* [Ejemplos para desarrolladores de Power BI](https://github.com/Microsoft/PowerBI-Developer-Samples)
* [Repositorio de GitHub de .NET de Power BI](https://github.com/Microsoft/PowerBI-CSharp)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
