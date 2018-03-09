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
ms.openlocfilehash: 050782871c3fe4ccb0d15bf9933c3b11c88ce661
ms.sourcegitcommit: dbec35008347b581dd238b882354300e427bec70
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2018
---
# <a name="migrate-an-aspnet-web-application-to-azure-app-service"></a>Migración de una aplicación web ASP.NET a Azure App Service

[App Service](https://docs.microsoft.com/azure/app-service/app-service-web-overview#why-use-web-apps) es una plataforma de procesos completamente administrada y optimizada para el hospedaje de sitios y aplicaciones web escalables. En este documento se proporciona información acerca de cómo realizar una migración mediante “lift and shift” de una aplicación existente al Azure App Service, las modificaciones que hay que tener en cuenta y los recursos adicionales para trasladarse a la nube.

¿Ya está listo para comenzar? [Publique su una aplicación ASP.NET + SQL en Azure App Service](https://go.microsoft.com/fwlink/?linkid=863214).

# <a name="preparation"></a>Preparación   
* [Cómo determinar si la aplicación cumple los requisitos para App Service](https://azure.microsoft.com/downloads/migration-assistant/)
* [Traslado de la base de datos a la nube](https://go.microsoft.com/fwlink/?linkid=863217)

# <a name="considerations"></a>Consideraciones
Hay varios factores que debe tener en cuenta antes de migrar la aplicación. La siguiente es una lista de posibles modificaciones que quizás deba realizar en la aplicación, y cómo hacerlas.

## <a name="sql-database-configuration"></a>Configuración de SQL Database
Si la aplicación usa una base de datos local, tiene varias opciones para la aplicación web. [Obtenga más información acerca de cómo migrar bases de datos SQL a Azure](https://go.microsoft.com/fwlink/?linkid=863217).

## <a name="iis"></a>IIS
Todo lo que tradicionalmente se configuraba mediante applicationHost.config en la aplicación, ahora se puede configurar mediante Azure Portal. Esto se aplica al valor de bits de AppPool, la opción para habilitar y deshabilitar websockets, la versión de canalización administrada, la versión de .NET Framework (2.0 o 4.0), etc. Para modificar la [configuración de la aplicación](https://docs.microsoft.com/azure/app-service/web-sites-configure), vaya a [Azure Portal](https://portal.azure.com), abra la hoja de la aplicación web y, a continuación, seleccione la pestaña **Configuración de la aplicación**.

## <a name="authentication"></a>Autenticación
Si la aplicación autentica a los usuarios en cualquier momento, tendrá que modificar esta funcionalidad para que funcione una vez que la aplicación esté implementada en Azure Web Apps. Una posibilidad es usar Azure AD Connect para integrar sus directorios locales con Azure Active Directory. [Obtenga más información acerca de cómo integrar sus directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

## <a name="virtual-network-modification"></a>Modificación de la red virtual
Si usa más de un servicio de Azure, piense en la posibilidad de usar una red virtual para la comunicación segura entre estos servicios. Puede configurar una conexión desde la red local a una [red virtual de Azure](https://docs.microsoft.com/azure/app-service/web-sites-integrate-with-vnet) mediante VPN o ExpressRoute.

## <a name="monitoring-and-diagnostics"></a>Supervisión y diagnóstico
Es poco probable que sus soluciones locales de supervisión y diagnóstico funcionen en la nube. Sin embargo, Azure proporciona herramientas de registro, supervisión y diagnóstico para que pueda identificar y depurar los problemas con las aplicaciones web. Puede habilitar fácilmente el diagnóstico de la aplicación web en su configuración, y puede ver los registros guardados por Azure Application Insights. [Obtenga más información acerca de cómo habilitar el registro de diagnósticos para las aplicaciones web](https://docs.microsoft.com/azure/app-service/web-sites-enable-diagnostic-log).

## <a name="connection-strings-and-application-settings"></a>Configuración de la aplicación y cadenas de conexión
Una opción para mantener la información segura es usar [Azure KeyVault](https://docs.microsoft.com/azure/key-vault/), un servicio que almacena de forma segura la información confidencial que se usa en la aplicación. También puede almacenar estos datos como un valor de configuración de App Service.

## <a name="dns"></a>DNS
Puede que tenga que actualizar las opciones de configuración de DNS según los requisitos de la aplicación. Las opciones de DNS pueden configurarse en la [configuración de dominio personalizado](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain), en App Service. Otro factor a tener en cuenta es el [enlace de un certificado SSL personalizado existente](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-ssl).

## <a name="file-system-and-storage"></a>Sistema de archivos y almacenamiento
Si la aplicación conserva los datos, debe actualizarla para que use Azure Storage en su lugar. Azure Storage es un servicio que proporciona recursos compartidos de archivos para compartir mediante el protocolo SMB, almacenamiento de blobs, colas simples y tablas no relacionales. [Obtenga más información acerca de Azure Storage](https://docs.microsoft.com/azure/storage/files/storage-files-introduction).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Migración de una aplicación web de ASP.NET a Azure App Service](https://aka.ms/azure-webapp-migrate)
