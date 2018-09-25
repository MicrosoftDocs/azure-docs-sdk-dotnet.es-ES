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
# <a name="tutorials-for-authenticating-users-in-your-net-apps-running-on-azure"></a><span data-ttu-id="109f3-103">Tutoriales para la autenticación de usuarios en las aplicaciones .NET que se ejecutan en Azure</span><span class="sxs-lookup"><span data-stu-id="109f3-103">Tutorials for authenticating users in your .NET apps running on Azure</span></span>

<span data-ttu-id="109f3-104">La tabla siguiente incluye vínculos a tutoriales detallados para autenticar a los usuarios y proteger las aplicaciones .NET que se ejecutan en Azure.</span><span class="sxs-lookup"><span data-stu-id="109f3-104">The following table links to in-depth tutorials for authenticating users and securing .NET applications running on Azure.</span></span>

<span data-ttu-id="109f3-105">Para el código fuente de ejemplo, consulte la lista de [ejemplos de servicios de Azure](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span><span class="sxs-lookup"><span data-stu-id="109f3-105">For sample source code, see the list of [Azure service samples](https://azure.microsoft.com/resources/samples/?platform=dotnet).</span></span>

| | |
|---|---|
|<span data-ttu-id="109f3-106">**Active Directory**</span><span class="sxs-lookup"><span data-stu-id="109f3-106">**Active Directory**</span></span>||
| <span data-ttu-id="109f3-107">[Adición de Azure Active Directory a una aplicación web mediante Servicios conectados de Visual Studio][5]</span><span class="sxs-lookup"><span data-stu-id="109f3-107">[Add Azure Active Directory to your web application by using Visual Studio Connected Services][5]</span></span> | <span data-ttu-id="109f3-108">Conexión de una aplicación web a Azure AD en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="109f3-108">Connect a web app to Azure AD in Visual Studio</span></span> |
| <span data-ttu-id="109f3-109">[Inicio y cierre de sesión de aplicación web con Azure AD][1]</span><span class="sxs-lookup"><span data-stu-id="109f3-109">[Web app sign-in and sign-out with Azure AD][1]</span></span> | <span data-ttu-id="109f3-110">Inicio y cierre de sesión de usuarios en ASP.NET con la biblioteca ADAL.</span><span class="sxs-lookup"><span data-stu-id="109f3-110">Sign users in and out of your ASP.NET with the ADAL library.</span></span> |
| <span data-ttu-id="109f3-111">[Autenticación de la aplicación de escritorio con Azure AD][2]</span><span class="sxs-lookup"><span data-stu-id="109f3-111">[Desktop application authentication with Azure AD][2]</span></span>| <span data-ttu-id="109f3-112">Integración de Azure AD en una aplicación WPF de escritorio de Windows mediante ADAL.</span><span class="sxs-lookup"><span data-stu-id="109f3-112">Integrate Azure AD into a Windows Desktop WPF app using ADAL.</span></span> | 
| <span data-ttu-id="109f3-113">[Autenticación de API Web con Azure AD][3]</span><span class="sxs-lookup"><span data-stu-id="109f3-113">[Web API authentication with Azure AD][3]</span></span> | <span data-ttu-id="109f3-114">Proteja una API web con tokens de portador de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="109f3-114">Protect a web API using bearer tokens from Azure AD.</span></span> |
|<span data-ttu-id="109f3-115">**Key Vault**</span><span class="sxs-lookup"><span data-stu-id="109f3-115">**Key Vault**</span></span>||
| <span data-ttu-id="109f3-116">[Adición de Key Vault a una aplicación web mediante Servicios conectados de Visual Studio][6]</span><span class="sxs-lookup"><span data-stu-id="109f3-116">[Add Key Vault to your web application by using Visual Studio Connected Services][6]</span></span> | <span data-ttu-id="109f3-117">Conexión de una aplicación web a Azure Key Vault en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="109f3-117">Connect a web app to Azure Key Vault in Visual Studio</span></span> |
| <span data-ttu-id="109f3-118">[Uso de Azure Key Vault desde una aplicación web][4]</span><span class="sxs-lookup"><span data-stu-id="109f3-118">[Use Azure Key Vault from a Web Application][4]</span></span> | <span data-ttu-id="109f3-119">Acceda a un secreto de una instancia de Azure Key Vault para que se pueda usar en su aplicación web.</span><span class="sxs-lookup"><span data-stu-id="109f3-119">Access a secret from an Azure Key Vault so that it can be used in your web application.</span></span> | 

[1]: /azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet
[2]: /azure/active-directory/develop/active-directory-devquickstarts-dotnet
[3]: /azure/active-directory/develop/active-directory-devquickstarts-webapi-dotnet
[4]: /azure/key-vault/key-vault-use-from-web-application
[5]: /azure/active-directory/develop/vs-active-directory-add-connected-service
[6]: /azure/key-vault/vs-key-vault-add-connected-service