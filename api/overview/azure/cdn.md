---
title: Bibliotecas de CDN de Azure para .NET
description: Referencia de las bibliotecas de CDN de Azure para .NET
keywords: Azure, .NET, SDK, API, CDN
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: cdn
ms.custom: devcenter, svc-overview
ms.openlocfilehash: afc63f943fcac3afd9afb7d85f6e699079829244
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="azure-cdn-libraries-for-net"></a>Bibliotecas de CDN de Azure para .NET

## <a name="overview"></a>Información general

Content Delivery Network (CDN) de Azure almacena en caché contenido de web estático en ubicaciones colocadas estratégicamente para proporcionar el máximo rendimiento a la hora de proporcionar contenido a los usuarios. CDN ofrece a los desarrolladores una solución global para entregar contenido de alto ancho de banda almacenando en caché el contenido en nodos físicos en todo el mundo.

Para aprender sobre CDN de Azure, consulte [Información general de Content Delivery Network (CDN) de Azure](https://docs.microsoft.com/azure/cdn/cdn-overview).


## <a name="management-library"></a>Biblioteca de administración

Puede usar la biblioteca de CDN de Azure para .NET para automatizar la creación y administración de perfiles y puntos de conexión de CDN. 

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Cdn.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Cdn.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.Cdn.Fluent
```

### <a name="example"></a>Ejemplo

En este ejemplo se crea un nuevo perfil de CDN con un nuevo punto de conexión que apunta a `www.contoso.com`.

```csharp
/* Include these "using" directives.
using Microsoft.Azure.Management.Cdn.Fluent;
using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
*/

ICdnProfile profileDefinition = azure.CdnProfiles.Define("CdnProfileName")
    .WithRegion(Region.USCentral)
    .WithExistingResourceGroup("ResourceGroupName")
    .WithStandardVerizonSku()
    .WithNewEndpoint("www.contoso.com")
    .Create();

```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/cdn/management)


## <a name="samples"></a>Muestras

* [Getting started with CDN - Manage CDN - in .NET](https://github.com/Azure-Samples/cdn-dotnet-manage-cdn) (Introducción a CDN y administración de CDN en .NET)

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
