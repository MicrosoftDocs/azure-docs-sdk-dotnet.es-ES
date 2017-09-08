---
title: Bibliotecas de Azure Automation para .NET
description: Referencia de las bibliotecas de Azure Automation para .NET
keywords: Azure, .NET, SDK, API, Automation
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 1e1b5a662947503ff71f3e4a9b67f20a1e2d5f87
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-automation-libraries-for-net"></a>Bibliotecas de Azure Automation para .NET

## <a name="overview"></a>Información general

Microsoft Azure Automation ofrece a los usuarios una manera de automatizar las tareas que se realizan normalmente en un entorno empresarial y en la nube. 

Para más información, lea [Introducción a Azure Automation](/azure/automation/automation-intro).

## <a name="management-library"></a>Biblioteca de administración

Uso de la biblioteca de administración para administrar runbooks y trabajos, y administrar la configuración de Desired State Configuration.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a>Ejemplo de código

En el ejemplo siguiente se ilustra cómo iniciar un trabajo nuevo basado en un runbook existente.

```csharp
/*
  using Microsoft.Azure.Management.Automation;
*/
AutomationManagementClient client =
    new AutomationManagementClient(new CertificateCloudCredentials(subscriptionId, cert));

// Create job create parameters
JobCreateParameters jcParam = new JobCreateParameters
{
    Properties = new JobCreateProperties
    {
        Runbook = new RunbookAssociationProperty
        {
            Name = runbookName
        },
        Parameters = null // optional parameters here
    }
};

// create runbook job. This gives back the Job
Job job = automationManagementClient.Jobs.Create(automationAccountName, jcParam).Job;
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a>Muestras

* [AzureBot](https://github.com/Microsoft/AzureBot) utiliza la biblioteca de Automation con [Framework Bot](https://docs.microsoft.com/bot-framework/) y [Cognitive Services](/cognitive-services) para mejorar la productividad de los desarrolladores en Azure

Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package