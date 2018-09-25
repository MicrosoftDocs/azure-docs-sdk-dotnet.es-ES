---
title: Tutoriales de .NET para proteger las aplicaciones de Azure
description: Tutoriales para la seguridad de las aplicaciones y la administración de identidades en las aplicaciones .NET que se ejecutan en Azure.
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 88ecfc69fbd57becf1adf1163a063c0d2bb086a8
ms.sourcegitcommit: 61638b504b6c4d96b357894835c80c2680a99fe6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/17/2018
ms.locfileid: "45750593"
---
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a>Tutoriales para la autenticación de usuarios en las aplicaciones .NET que se ejecutan en Azure

La tabla siguiente incluye vínculos a tutoriales detallados para autenticar a los usuarios y proteger las aplicaciones .NET que se ejecutan en Azure.

Para el código fuente de ejemplo, consulte la lista de [ejemplos de servicios de Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).

| | |
|---|---|
|**Active Directory**||
| [Adición de Azure Active Directory a una aplicación web mediante Servicios conectados de Visual Studio][5] | Conexión de una aplicación web a Azure AD en Visual Studio |
| [Inicio y cierre de sesión de aplicación web con Azure AD][1] | Inicio y cierre de sesión de usuarios en ASP.NET con la biblioteca ADAL. |
| [Autenticación de la aplicación de escritorio con Azure AD][2]| Integración de Azure AD en una aplicación WPF de escritorio de Windows mediante ADAL. | 
| [Autenticación de API Web con Azure AD][3] | Proteja una API web con tokens de portador de Azure AD. |
|**Key Vault**||
| [Adición de Key Vault a una aplicación web mediante Servicios conectados de Visual Studio][6] | Conexión de una aplicación web a Azure Key Vault en Visual Studio |
| [Uso de Azure Key Vault desde una aplicación web][4] | Acceda a un secreto de una instancia de Azure Key Vault para que se pueda usar en su aplicación web. | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service