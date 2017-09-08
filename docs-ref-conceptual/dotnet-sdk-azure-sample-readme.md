---
title: "Instrucciones de ejemplo de bibliotecas de administración de Azure para .NET"
description: "Obtenga código de ejemplo para la creación y actualización de recursos mediante las bibliotecas de administración de Azure para .NET."
keywords: Azure, .NET, SDK, API, ejemplo
author: camsoper
ms.author: casoper
manager: douge
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: ffda7cca724962e6f953432c5cab04485ddabb03
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-management-libraries-for-net-sample-instructions"></a>Instrucciones de ejemplo de bibliotecas de administración de Azure para .NET

En este artículo se describen los requisitos previos y la autenticación necesarios para ejecutar los ejemplos de las bibliotecas de administración de Azure para .NET.

## <a name="prerequisties"></a>Requisitos previos 

* [Visual Studio 2017](https://www.visualstudio.com/vs/) o [SDK de .NET Core](https://www.microsoft.com/net/download/core)
* Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/)
* [Cliente de línea de comandos de Git](https://git-scm.com/)
* [Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps)

## <a name="authentication-for-all-samples"></a>Autenticación para todos las ejemplos

[!include[Create service principal](includes/create-sp.md)]

[!include[File-based authentication](includes/file-based-auth.md)]

## <a name="running-the-samples"></a>Ejecución de los ejemplos

Una vez que ha usado Git para clonar el ejemplo, puede abrirlo en Visual Studio y ejecutarlo mediante el IDE.  Como alternativa, use el SDK de .NET Core para compilar y ejecutar el ejemplo desde la línea de comandos:

```cmd
git clone https://github.com/Azure-Samples/app-service-dotnet-configure-deployment-sources-for-web-apps.git
cd app-service-dotnet-configure-deployment-sources-for-web-apps
dotnet restore
dotnet run
```