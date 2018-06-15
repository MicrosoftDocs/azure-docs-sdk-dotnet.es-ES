---
title: Azure Tools para Visual Studio 2015
description: Obtenga las herramientas para empezar a usar las bibliotecas .NET de Azure desde Visual Studio 2015.
keywords: .NET de Azure, SDK, VS2015, Visual Studio 2015
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 5046781a16b5b330b95c4ad36e8a8187126fef4e
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
ms.locfileid: "29752817"
---
# <a name="azure-tools-for-visual-studio-2015"></a>Azure Tools para Visual Studio 2015

La manera más rápida y sencilla de instalar el **Azure SDK para Visual Studio 2015** y el **Service Fabric SDK y Tools para Visual Studio 2015** es mediante el [Instalador de plataforma web](https://www.microsoft.com/web/downloads/platform.aspx).  El Instalador de plataforma web de Microsoft es una herramienta gratuita que simplifica la descarga, instalación y actualización de algunos de los componentes de la plataforma web de Microsoft, lo que incluye Azure Tools para Visual Studio 2015.  Estos SDK también se pueden descargar e instalar como componentes individuales desde la [página de descargas de Azure](https://azure.microsoft.com/downloads/). 

## <a name="using-the-web-platform-installer"></a>Uso del Instalador de plataforma web

1. Descargue y ejecute este [programa previo del Instalador de plataforma web](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=VWDOrVs2015AzurePack;MicrosoftAzure-ServiceFabric-VS2015).  

2. El programa previo instalará el Instalador de plataforma web (en caso de que sea necesario) y colocará automáticamente las versiones más recientes de los elementos **Azure SDK para Visual Studio 2015** y **Service Fabric SDK y Tools para Visual Studio 2015** en la lista *Elementos para instalar*.  Haga clic en **Instalar**.

    ![Instalador de plataforma web](media/dotnet-sdk-vs2015-install/webpi.png)

3. En la siguiente pantalla, haga clic en **Acepto**.  El Instalador de plataforma web comenzará la descarga e instalación de los componentes que ha seleccionado.

4. Una vez finalizada la instalación, se mostrará una pantalla de confirmación.  Haga clic en **Finalizar**  Ya puede cerrar el Instalador de plataforma web.

## <a name="verifying-the-installation"></a>Comprobación de la instalación

1. En Visual Studio 2015, haga clic en el menú **Herramientas** y, después, en **Extensiones y actualizaciones...**.

2. La lista contendrá varias herramientas de Azure, como **Microsoft Azure App Service Tools**, **Microsoft Azure Storage Connected Service** y **Service Fabric Tools**.

    ![Extensiones y actualizaciones](media\dotnet-sdk-vs2015-install\ext-tools.png)

## <a name="next-steps"></a>Pasos siguientes

[Get started with Azure libraries for .NET](dotnet-sdk-azure-get-started.md) (Introducción a las bibliotecas de Azure para .NET).
