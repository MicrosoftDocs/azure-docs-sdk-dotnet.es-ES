---
title: Bibliotecas de Azure Data Factory para .NET
description: Referencia de las bibliotecas de Azure Data Factory para .NET
keywords: Azure, .NET, SDK, API, Data Factory
author: camsoper
ms.author: casoper
manager: douge
ms.date: 09/22/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-factory
ms.custom: devcenter
ms.openlocfilehash: 6f1a1cf9ac8189af59ff4e3f42dc1d8fb9620ea2
ms.sourcegitcommit: f35939d37f67485b3667739b02621e317db3e391
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2017
---
# <a name="azure-data-factory-libraries-for-net"></a>Bibliotecas de Azure Data Factory para .NET

## <a name="overview"></a>Información general

Azure Data Factory es un servicio de integración de datos en la nube. Permite crear flujos de trabajo controlados por datos en la nube para orquestar y automatizar tanto el movimiento de datos como la transformación de datos.

Para más información, lea [Introducción a Azure Data Factory](/azure/data-factory/data-factory-introduction).

## <a name="management-library---data-factory-v2-preview"></a>Biblioteca de administración: Data Factory V2 (versión preliminar)

La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory V2 (versión preliminar).  Para más información, consulte [Create a data factory and pipeline using .NET SDK](/azure/data-factory/quickstart-create-data-factory-dot-net) (Crear una factoría de datos y una canalización mediante SDK de .NET).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactory) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
# Get the most recent prerelease package
Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
```

```bash
# Be sure to include the most recent version from the NuGet package page
dotnet add package Microsoft.Azure.Management.DataFactory --version 0.2.0-preview
```

### <a name="code-example"></a>Ejemplo de código

En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.

```csharp
/*
using Microsoft.Azure.Management.ResourceManager;
using Microsoft.Azure.Management.DataFactory;
using Microsoft.Azure.Management.DataFactory.Models;
*/

DataFactoryManagementClient client = new DataFactoryManagementClient(tokenCredentials) { SubscriptionId = subscriptionId };
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/microsoft.azure.management.datafactory)

## <a name="management-library---data-factory-v1"></a>Biblioteca de administración: Data Factory V1

La biblioteca de administración se usa para crear y programar flujos de trabajo controlados por datos (canalizaciones) en Data Factory, versión 1.  Para más información, consulte la documentación de [Data Factory, versión 1](/azure/data-factory/v1/data-factory-introduction).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataFactories) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataFactories
```

```bash
dotnet add package Microsoft.Azure.Management.DataFactories
```

### <a name="code-example"></a>Ejemplo de código

En el ejemplo siguiente se utiliza la biblioteca de administración para crear una factoría de datos.

```csharp
DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
client.DataFactories.CreateOrUpdate(resourceGroupName,
    new DataFactoryCreateOrUpdateParameters()
    {
        DataFactory = new DataFactory()
        {
            Name = dataFactoryName,
            Location = "westus",
            Properties = new DataFactoryProperties()
        }
    }
);
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/datafactories/management)

## <a name="samples"></a>Muestras

* [MyDriving - An Azure IOT and Mobile Sample Application](https://azure.microsoft.com/resources/samples/mydriving/) (MyDriving: una aplicación de ejemplo para Azure IOT y dispositivos móviles) que usa Data Factory para proporcionar la información.

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
