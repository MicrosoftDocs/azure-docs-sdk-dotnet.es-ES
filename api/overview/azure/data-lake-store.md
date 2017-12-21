---
title: Bibliotecas de Azure Data Lake Store para .NET
description: Referencia de las bibliotecas de Azure Data Lake Store para .NET
keywords: Azure, .NET, SDK, API, Data Lake Store
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: data-lake-store
ms.custom: devcenter, svc-overview
ms.openlocfilehash: e8380c4a9ebf86f03fe87fc800dffda10e48e60a
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2017
---
# <a name="azure-data-lake-store-libraries-for-net"></a>Bibliotecas de Azure Data Lake Store para .NET

## <a name="overview"></a>Información general

El Almacén de Azure Data Lake es un repositorio de gran escala en toda la empresa para cargas de trabajo de análisis de macrodatos. Azure Data Lake permite capturar datos de cualquier tamaño, tipo y velocidad de ingesta en un único lugar para realizar análisis exploratorios y operativos.

Para más información, consulte [Información general de Azure Data Lake Store](/azure/data-lake-store/data-lake-store-overview).

## <a name="client-library"></a>Biblioteca de cliente

Utilice la biblioteca de cliente para realizar operaciones del sistema de archivos en Data Lake Store, como crear carpetas en una cuenta de Data Lake Store, cargar archivos y descargar archivos.  Para obtener un tutorial completo sobre el uso de Data Lake Store con .NET, consulte [Operaciones del sistema de archivos en Azure Data Lake Store con .NET SDK](/azure/data-lake-store/data-lake-store-data-operations-net-sdk).

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.DataLake.Store
```
### <a name="authentication"></a>Autenticación

* Para la autenticación del usuario final para la aplicación, consulte el artículo sobre la [autenticación del usuario final con Data Lake Store mediante el SDK de .NET](/azure/data-lake-store/data-lake-store-end-user-authenticate-net-sdk).
* Para la autenticación entre servicios para la aplicación, consulte el artículo sobre la [autenticación entre servicios con Data Lake Store mediante el SDK de .NET](/azure/data-lake-store/data-lake-store-service-to-service-authenticate-net-sdk).

### <a name="code-example"></a>Ejemplo de código

El fragmento de código siguiente crea los objetos de cliente del sistema de archivos de Data Lake Store, que se usan para emitir solicitudes al servicio.

```csharp
// Create client objects
AdlsClient client = AdlsClient.CreateClient(_adlsAccountName, adlCreds);
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/datalakestore/client)


## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración para conectarse a sus repositorios de macrodatos y administrarlos.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.DataLake.Store) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.DataLake.Store
```

```bash
dotnet add package Microsoft.Azure.Management.DataLake.Store
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/datalakestore/management)


## <a name="samples"></a>Muestras

* [Ejemplo de cliente de .NET de Azure Data Lake](https://azure.microsoft.com/en-us/resources/samples/data-lake-dotnet-client/)

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
