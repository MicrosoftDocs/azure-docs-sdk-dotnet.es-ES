---
title: Bibliotecas de Azure Automation para .NET
description: Referencia de las bibliotecas de Azure Automation para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: automation
ms.openlocfilehash: 4890faab86d1319fe802a30e3735419ac65e8d64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190288"
---
# <a name="azure-automation-libraries-for-net"></a><span data-ttu-id="dd155-103">Bibliotecas de Azure Automation para .NET</span><span class="sxs-lookup"><span data-stu-id="dd155-103">Azure Automation libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="dd155-104">Información general</span><span class="sxs-lookup"><span data-stu-id="dd155-104">Overview</span></span>

<span data-ttu-id="dd155-105">Microsoft Azure Automation ofrece a los usuarios una manera de automatizar las tareas que se realizan normalmente en un entorno empresarial y en la nube.</span><span class="sxs-lookup"><span data-stu-id="dd155-105">Microsoft Azure Automation provides a way for users to automate the tasks that are commonly performed in a cloud and enterprise environment.</span></span> 

<span data-ttu-id="dd155-106">Para más información, lea [Introducción a Azure Automation](/azure/automation/automation-intro).</span><span class="sxs-lookup"><span data-stu-id="dd155-106">Learn more by reading the [Azure Automation Overview](/azure/automation/automation-intro).</span></span>

## <a name="management-library"></a><span data-ttu-id="dd155-107">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="dd155-107">Management library</span></span>

<span data-ttu-id="dd155-108">Uso de la biblioteca de administración para administrar runbooks y trabajos, y administrar la configuración de Desired State Configuration.</span><span class="sxs-lookup"><span data-stu-id="dd155-108">Using the management library to manage runbooks and jobs and manage Desired State Configuration settings.</span></span>

<span data-ttu-id="dd155-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="dd155-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.Automation) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="dd155-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd155-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.Automation
```

```bash
dotnet add package Microsoft.Azure.Management.Automation
```

### <a name="code-example"></a><span data-ttu-id="dd155-111">Ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="dd155-111">Code Example</span></span>

<span data-ttu-id="dd155-112">En el ejemplo siguiente se ilustra cómo iniciar un trabajo nuevo basado en un runbook existente.</span><span class="sxs-lookup"><span data-stu-id="dd155-112">The following example illustrates how to start a new job based on an existing runbook.</span></span>

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
> [<span data-ttu-id="dd155-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="dd155-113">Explore the management APIs</span></span>](/dotnet/api/overview/azure/automation/management)

## <a name="samples"></a><span data-ttu-id="dd155-114">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="dd155-114">Samples</span></span>

* <span data-ttu-id="dd155-115">[AzureBot](https://github.com/Microsoft/AzureBot) utiliza la biblioteca de Automation con [Framework Bot](https://docs.microsoft.com/bot-framework/) y [Cognitive Services](/cognitive-services) para mejorar la productividad de los desarrolladores en Azure</span><span class="sxs-lookup"><span data-stu-id="dd155-115">[AzureBot](https://github.com/Microsoft/AzureBot) uses the automation library with the [Bot Framework](https://docs.microsoft.com/bot-framework/) and [Cognitive Services](/cognitive-services) to improve developer productivity on Azure</span></span>

<span data-ttu-id="dd155-116">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="dd155-116">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
