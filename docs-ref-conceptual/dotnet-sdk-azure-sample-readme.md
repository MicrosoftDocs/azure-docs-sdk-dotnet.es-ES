---
title: Instrucciones de ejemplo de bibliotecas de administración de Azure para .NET
description: Obtenga código de ejemplo para la creación y actualización de recursos mediante las bibliotecas de administración de Azure para .NET.
keywords: Azure, .NET, SDK, API, ejemplo
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: a931e623768e1fddad263c7da8eb864c37613379
ms.sourcegitcommit: 9dd801d659803f5efb16d65454cd09258e1cc7d6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2018
ms.locfileid: "29752478"
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a><span data-ttu-id="8ea42-104">Instrucciones de ejemplo de bibliotecas de administración de Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="8ea42-104">Azure management libraries for .NET sample instructions</span></span>

<span data-ttu-id="8ea42-105">En este artículo se describen los requisitos previos y la autenticación necesarios para ejecutar los ejemplos de las bibliotecas de administración de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="8ea42-105">This article describes the prerequisites and authentication required for running the samples for the Azure management libraries for .NET.</span></span>

## <a name="prerequisties"></a><span data-ttu-id="8ea42-106">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="8ea42-106">Prerequisties</span></span> 

* <span data-ttu-id="8ea42-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) o [SDK de .NET Core](https://www.microsoft.com/net/download/core)</span><span class="sxs-lookup"><span data-stu-id="8ea42-107">[Visual Studio 2017](https://www.visualstudio.com/vs/) or [.NET Core SDK](https://www.microsoft.com/net/download/core)</span></span>
* <span data-ttu-id="8ea42-108">Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="8ea42-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="8ea42-109">Cliente de línea de comandos de Git</span><span class="sxs-lookup"><span data-stu-id="8ea42-109">Git command line client</span></span>](https://git-scm.com/)
* [<span data-ttu-id="8ea42-110">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ea42-110">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a><span data-ttu-id="8ea42-111">Autenticación para todos las ejemplos</span><span class="sxs-lookup"><span data-stu-id="8ea42-111">Authentication for all samples</span></span>

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a><span data-ttu-id="8ea42-112">Ejecución de los ejemplos</span><span class="sxs-lookup"><span data-stu-id="8ea42-112">Running the samples</span></span>

<span data-ttu-id="8ea42-113">Una vez que ha usado Git para clonar el ejemplo, puede abrirlo en Visual Studio y ejecutarlo mediante el IDE.</span><span class="sxs-lookup"><span data-stu-id="8ea42-113">Once you have used Git to clone the sample, you can open the sample in Visual Studio and run the sample using the IDE.</span></span>  <span data-ttu-id="8ea42-114">Como alternativa, use el SDK de .NET Core para compilar y ejecutar el ejemplo desde la línea de comandos:</span><span class="sxs-lookup"><span data-stu-id="8ea42-114">Alternatively, use the .NET Core SDK to build and run the sample from the command line, like this:</span></span>

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```