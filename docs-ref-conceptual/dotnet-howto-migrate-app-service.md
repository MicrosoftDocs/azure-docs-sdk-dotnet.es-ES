---
title: "Migración de una aplicación web ASP.NET a Azure App Service"
description: "Aprenda a migrar una aplicación web ASP.NET de un entorno local a Azure App Service."
keywords: "Azure. NET, ASP.NET, App Service, aplicación web, migrar, migración"
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: app-service
ms.custom: devcenter
ms.openlocfilehash: 8ad1bcd11a823c1b6f7e592a5990dd6f7ed06e97
ms.sourcegitcommit: ccc95adb96cf7d56ebce5e09bedf10c2d48f5e1f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a><span data-ttu-id="82bb5-104">Migración de una aplicación web ASP.NET a Azure App Service</span><span class="sxs-lookup"><span data-stu-id="82bb5-104">Migrate an ASP.NET web application to Azure App Service</span></span>

<span data-ttu-id="82bb5-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) es una plataforma de procesos completamente administrada y optimizada para el hospedaje de sitios y aplicaciones web escalables.</span><span class="sxs-lookup"><span data-stu-id="82bb5-105">[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) is a fully-managed compute platform service that is optimized for hosting scalable websites and web applications.</span></span> <span data-ttu-id="82bb5-106">En este documento se proporciona información acerca de cómo realizar una migración mediante “lift and shift” de una aplicación existente al Azure App Service, las modificaciones que hay que tener en cuenta y los recursos adicionales para trasladarse a la nube.</span><span class="sxs-lookup"><span data-stu-id="82bb5-106">This document provides information on how to lift-and-shift an existing application to Azure App Service, modifications to consider, and additional resources for moving to the cloud.</span></span>

<span data-ttu-id="82bb5-107">¿Ya está listo para comenzar?</span><span class="sxs-lookup"><span data-stu-id="82bb5-107">Ready to get started?</span></span> <span data-ttu-id="82bb5-108">[Publique su una aplicación ASP.NET + SQL en Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).</span><span class="sxs-lookup"><span data-stu-id="82bb5-108">[Publish your ASP.NET + SQL application to Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).</span></span>

# <a name="preparation"></a><span data-ttu-id="82bb5-109">Preparación</span><span class="sxs-lookup"><span data-stu-id="82bb5-109">Preparation</span></span>   
* [<span data-ttu-id="82bb5-110">Cómo determinar si la aplicación cumple los requisitos para App Service</span><span class="sxs-lookup"><span data-stu-id="82bb5-110">How to determine if your app qualifies for App Service</span></span>](https://azure.microsoft.com/downloads/migration-assistant/)
* [<span data-ttu-id="82bb5-111">Traslado de la base de datos a la nube</span><span class="sxs-lookup"><span data-stu-id="82bb5-111">Moving your database to the cloud</span></span>](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a><span data-ttu-id="82bb5-112">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="82bb5-112">Considerations</span></span>
<span data-ttu-id="82bb5-113">Hay varios factores que debe tener en cuenta antes de migrar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82bb5-113">There are several factors you must consider before migrating your application.</span></span> <span data-ttu-id="82bb5-114">La siguiente es una lista de posibles modificaciones que quizás deba realizar en la aplicación, y cómo hacerlas.</span><span class="sxs-lookup"><span data-stu-id="82bb5-114">Below is a list of potential modifications you might have to make to your application, and how to go about doing them.</span></span>

## <a name="sql-database-configuration"></a><span data-ttu-id="82bb5-115">Configuración de SQL Database</span><span class="sxs-lookup"><span data-stu-id="82bb5-115">SQL Database configuration</span></span>
<span data-ttu-id="82bb5-116">Si la aplicación usa una base de datos local, tiene varias opciones para la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="82bb5-116">If your application is using an on-premises database, you have several options for your web app.</span></span> <span data-ttu-id="82bb5-117">[Obtenga más información acerca de cómo migrar bases de datos SQL a Azure](https://go.microsoft.com/fwlink/?linkid=863217).</span><span class="sxs-lookup"><span data-stu-id="82bb5-117">[Read more about migrating SQL databases to Azure](https://go.microsoft.com/fwlink/?linkid=863217).</span></span>

## <a name="iis"></a><span data-ttu-id="82bb5-118">IIS</span><span class="sxs-lookup"><span data-stu-id="82bb5-118">IIS</span></span>
<span data-ttu-id="82bb5-119">Todo lo que tradicionalmente se configuraba mediante applicationHost.config en la aplicación, ahora se puede configurar mediante Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="82bb5-119">Everything traditionally configured via applicationHost.config in your application can now be configured through the Azure portal.</span></span> <span data-ttu-id="82bb5-120">Esto se aplica al valor de bits de AppPool, la opción para habilitar y deshabilitar websockets, la versión de canalización administrada, la versión de .NET Framework (2.0 o 4.0), etc. Para modificar la [configuración de la aplicación](https://docs.microsoft.com/en-us/azure/app-service/web-sites-configure), vaya a [Azure Portal](https://portal.azure.com), abra la hoja de la aplicación web y, a continuación, seleccione la pestaña **Configuración de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="82bb5-120">This applies to AppPool bitness, enable/disable websockets, managed pipeline version, .NET Framework version (2.0/4.0), etc. To modify your [application settings](https://docs.microsoft.com/en-us/azure/app-service/web-sites-configure), navigate to the [Azure portal](https://portal.azure.com), open the blade for your web app, and then select the **Application Settings** tab.</span></span>

## <a name="authentication"></a><span data-ttu-id="82bb5-121">Autenticación</span><span class="sxs-lookup"><span data-stu-id="82bb5-121">Authentication</span></span>
<span data-ttu-id="82bb5-122">Si la aplicación autentica a los usuarios en cualquier momento, tendrá que modificar esta funcionalidad para que funcione una vez que la aplicación esté implementada en Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="82bb5-122">If your application authenticates users at any point, you will have to modify this functionality to work once the application deployed on Azure Web Apps.</span></span> <span data-ttu-id="82bb5-123">Una posibilidad es usar Azure AD Connect para integrar sus directorios locales con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="82bb5-123">One possibility is to use Azure AD Connect to integrate your on-premises directories with Azure Active Directory.</span></span> <span data-ttu-id="82bb5-124">[Obtenga más información acerca de cómo integrar sus directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span><span class="sxs-lookup"><span data-stu-id="82bb5-124">[Learn more about how to integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>

## <a name="virtual-network-modification"></a><span data-ttu-id="82bb5-125">Modificación de la red virtual</span><span class="sxs-lookup"><span data-stu-id="82bb5-125">Virtual Network Modification</span></span>
<span data-ttu-id="82bb5-126">Si usa más de un servicio de Azure, piense en la posibilidad de usar una red virtual para la comunicación segura entre estos servicios.</span><span class="sxs-lookup"><span data-stu-id="82bb5-126">If you use more than one Azure service you may consider using a virtual network to securely communicate between these services.</span></span> <span data-ttu-id="82bb5-127">Puede configurar una conexión desde la red local a una [red virtual de Azure](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet) mediante VPN o ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="82bb5-127">You can configure a connection from your on-premises network to an [Azure Virtual Network](https://docs.microsoft.com/en-us/azure/app-service/web-sites-integrate-with-vnet) using VPN or ExpressRoute.</span></span>

## <a name="monitoring-and-diagnostics"></a><span data-ttu-id="82bb5-128">Supervisión y diagnóstico</span><span class="sxs-lookup"><span data-stu-id="82bb5-128">Monitoring and Diagnostics</span></span>
<span data-ttu-id="82bb5-129">Es poco probable que sus soluciones locales de supervisión y diagnóstico funcionen en la nube.</span><span class="sxs-lookup"><span data-stu-id="82bb5-129">Your current on-premises solutions for monitoring and diagnostics are unlikely to work in the cloud.</span></span> <span data-ttu-id="82bb5-130">Sin embargo, Azure proporciona herramientas de registro, supervisión y diagnóstico para que pueda identificar y depurar los problemas con las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="82bb5-130">However, Azure provides tools for logging, monitoring, and diagnostics so that you can identify and debug issues with web apps.</span></span> <span data-ttu-id="82bb5-131">Puede habilitar fácilmente el diagnóstico de la aplicación web en su configuración, y puede ver los registros guardados por Azure Application Insights.</span><span class="sxs-lookup"><span data-stu-id="82bb5-131">You can easily enable diagnostics for your web app in its configuration, and you can view the logs recorded in Azure Application Insights.</span></span> <span data-ttu-id="82bb5-132">[Obtenga más información acerca de cómo habilitar el registro de diagnósticos para las aplicaciones web](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).</span><span class="sxs-lookup"><span data-stu-id="82bb5-132">[Learn more about enabling diagnostics logging for web apps](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).</span></span>

## <a name="connection-strings-and-application-settings"></a><span data-ttu-id="82bb5-133">Configuración de la aplicación y cadenas de conexión</span><span class="sxs-lookup"><span data-stu-id="82bb5-133">Connection Strings and application settings</span></span>
<span data-ttu-id="82bb5-134">Una opción para mantener la información segura es usar [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), un servicio que almacena de forma segura la información confidencial que se usa en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82bb5-134">One option for keeping information safe is to use [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), a service that securely stores sensitive information used in your application.</span></span> <span data-ttu-id="82bb5-135">También puede almacenar estos datos como un valor de configuración de App Service.</span><span class="sxs-lookup"><span data-stu-id="82bb5-135">Alternatively, you can store this data as an App Service setting.</span></span>

## <a name="dns"></a><span data-ttu-id="82bb5-136">DNS</span><span class="sxs-lookup"><span data-stu-id="82bb5-136">DNS</span></span>
<span data-ttu-id="82bb5-137">Puede que tenga que actualizar las opciones de configuración de DNS según los requisitos de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="82bb5-137">You may need to update DNS configurations based on the requirements of your application.</span></span> <span data-ttu-id="82bb5-138">Las opciones de DNS pueden configurarse en la [configuración de dominio personalizado](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain), en App Service.</span><span class="sxs-lookup"><span data-stu-id="82bb5-138">These DNS settings can be configured in the App Service [custom domain settings](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain).</span></span> <span data-ttu-id="82bb5-139">Otro factor a tener en cuenta es el [enlace de un certificado SSL personalizado existente](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl).</span><span class="sxs-lookup"><span data-stu-id="82bb5-139">Another factor to consider is [binding an existing custom SSL certificate](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-tutorial-custom-ssl).</span></span>

## <a name="file-system-and-storage"></a><span data-ttu-id="82bb5-140">Sistema de archivos y almacenamiento</span><span class="sxs-lookup"><span data-stu-id="82bb5-140">File system and Storage</span></span>
<span data-ttu-id="82bb5-141">Si la aplicación conserva los datos, debe actualizarla para que use Azure Storage en su lugar.</span><span class="sxs-lookup"><span data-stu-id="82bb5-141">If your application persists data, you will need to update it to use Azure Storage instead.</span></span> <span data-ttu-id="82bb5-142">Azure Storage es un servicio que proporciona recursos compartidos de archivos para compartir mediante el protocolo SMB, almacenamiento de blobs, colas simples y tablas no relacionales.</span><span class="sxs-lookup"><span data-stu-id="82bb5-142">Azure Storage is a service that provides file shares for sharing via SMB protocol, blob storage, simple queues, and non-relational tables.</span></span> <span data-ttu-id="82bb5-143">[Obtenga más información acerca de Azure Storage](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).</span><span class="sxs-lookup"><span data-stu-id="82bb5-143">[Learn more about Azure Storage file shares](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).</span></span>

## <a name="next-steps"></a><span data-ttu-id="82bb5-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82bb5-144">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82bb5-145">Migración de una aplicación web de ASP.NET a Azure App Service</span><span class="sxs-lookup"><span data-stu-id="82bb5-145">Migrate an ASP.NET Web application to Azure App Service</span></span>](https://aka.ms/azure-webapp-migrate)