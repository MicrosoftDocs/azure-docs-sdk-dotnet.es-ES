---
title: Azure Tools para Visual Studio 2015
description: Obtenga las herramientas para empezar a usar las bibliotecas .NET de Azure desde Visual Studio 2015.
keywords: .NET de Azure, SDK, VS2015, Visual Studio 2015
author: camsoper
manager: douge
ms.author: casoper
ms.date: 07/25/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: bee09801efd4f7291981bc85cd9c6a5d0b795b6e
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-tools-for-visual-studio-2015"></a><span data-ttu-id="cc6a1-104">Azure Tools para Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="cc6a1-104">Azure tools for Visual Studio 2015</span></span>

<span data-ttu-id="cc6a1-105">La manera más rápida y sencilla de instalar el **Azure SDK para Visual Studio 2015** y el **Service Fabric SDK y Tools para Visual Studio 2015** es mediante el [Instalador de plataforma web](https://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="cc6a1-105">The quickest and easiest way to install the **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** is using the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>  <span data-ttu-id="cc6a1-106">El Instalador de plataforma web de Microsoft es una herramienta gratuita que simplifica la descarga, instalación y actualización de algunos de los componentes de la plataforma web de Microsoft, lo que incluye Azure Tools para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-106">The Microsoft Web Platform Installer is a free tool that streamlines downloading, installing, and updating some of the components of the Microsoft Web Platform, including Azure tools for Visual Studio 2015.</span></span>  <span data-ttu-id="cc6a1-107">Estos SDK también se pueden descargar e instalar como componentes individuales desde la [página de descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cc6a1-107">These SDKs can also be downloaded and installed as individual components from the [Azure Downloads page](https://azure.microsoft.com/downloads/).</span></span> 

## <a name="using-the-web-platform-installer"></a><span data-ttu-id="cc6a1-108">Uso del Instalador de plataforma web</span><span class="sxs-lookup"><span data-stu-id="cc6a1-108">Using the Web Platform Installer</span></span>

1. <span data-ttu-id="cc6a1-109">Descargue y ejecute este [programa previo del Instalador de plataforma web](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).</span><span class="sxs-lookup"><span data-stu-id="cc6a1-109">Download and run this [Web Platform Installer bootstrapper](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).</span></span>  

2. <span data-ttu-id="cc6a1-110">El programa previo instalará el Instalador de plataforma web (en caso de que sea necesario) y colocará automáticamente las versiones más recientes de los elementos **Azure SDK para Visual Studio 2015** y **Service Fabric SDK y Tools para Visual Studio 2015** en la lista *Elementos para instalar*.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-110">The bootstrapper will install Web Platform Installer (if needed) and automatically put the latest versions of the  **Azure SDK for Visual Studio 2015** and **Service Fabric SDK and Tools for Visual Studio 2015** items in your *Items to be installed* list.</span></span>  <span data-ttu-id="cc6a1-111">Haga clic en **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-111">Click **Install**.</span></span>

    ![Instalador de plataforma web](media/dotnet-sdk-vs2015-install/webpi.png)

3. <span data-ttu-id="cc6a1-113">En la siguiente pantalla, haga clic en **Acepto**.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-113">On the next screen, click **I Accept**.</span></span>  <span data-ttu-id="cc6a1-114">El Instalador de plataforma web comenzará la descarga e instalación de los componentes que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-114">Web PI will begin downloading and installing the components you selected.</span></span>

4. <span data-ttu-id="cc6a1-115">Una vez finalizada la instalación, se mostrará una pantalla de confirmación.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-115">After the installation is finished, it will display a confirmation screen.</span></span>  <span data-ttu-id="cc6a1-116">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="cc6a1-116">Click **Finish**.</span></span>  <span data-ttu-id="cc6a1-117">Ya puede cerrar el Instalador de plataforma web.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-117">You can now close Web Platform Installer.</span></span>

## <a name="verifying-the-installation"></a><span data-ttu-id="cc6a1-118">Comprobación de la instalación</span><span class="sxs-lookup"><span data-stu-id="cc6a1-118">Verifying the installation</span></span>

1. <span data-ttu-id="cc6a1-119">En Visual Studio 2015, haga clic en el menú **Herramientas** y, después, en **Extensiones y actualizaciones...**.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-119">In Visual Studio 2015, click the **Tools** menu, and then click **Extensions and Updates...**.</span></span>

2. <span data-ttu-id="cc6a1-120">La lista contendrá varias herramientas de Azure, como **Microsoft Azure App Service Tools**, **Microsoft Azure Storage Connected Service** y **Service Fabric Tools**.</span><span class="sxs-lookup"><span data-stu-id="cc6a1-120">The displayed list will contain several Azure tools, such as **Microsoft Azure App Service Tools**, **Microsoft Azure Storage Connected Service**, and **Service Fabric Tools**.</span></span>

    ![Extensiones y actualizaciones](media\dotnet-sdk-vs2015-install\ext-tools.png)

## <a name="next-steps"></a><span data-ttu-id="cc6a1-122">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cc6a1-122">Next steps</span></span>

<span data-ttu-id="cc6a1-123">[Get started with Azure libraries for .NET](dotnet-sdk-azure-get-started.md) (Introducción a las bibliotecas de Azure para .NET).</span><span class="sxs-lookup"><span data-stu-id="cc6a1-123">[Get started with Azure libraries for .NET](dotnet-sdk-azure-get-started.md).</span></span>
