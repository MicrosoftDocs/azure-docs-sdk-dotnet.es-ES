---
title: Elección de la opción de hospedaje de Azure correcta
description: Vea cuál es la ruta de migración de Azure más adecuada para su aplicación web ASP.NET.
keywords: Azure .NET, ASP.NET, App Service, máquina virtual, aplicación web, migrar, migración
author: CESARDELATORRE
manager: wpickett
ms.author: cesardl
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter, casoper
ms.openlocfilehash: dbf54bb1a6e3d612ef8363a6b30e06b388b4490f
ms.sourcegitcommit: 3e904e6e4f04f1c92d729459434c85faff32e386
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/09/2017
ms.locfileid: "26588468"
---
# <a name="choose-the-right-azure-hosting-option"></a>Elección de la opción de hospedaje de Azure correcta

Este documento ofrece varias consideraciones y comparaciones entre las distintas opciones disponibles en Azure para migrar sus aplicaciones de .NET Framework existentes desde el entorno local a Azure.

Las áreas fundamentales que debe tener en cuenta a la hora de migrar aplicaciones de .NET existentes a Azure son:

1.  Opciones de proceso
2.  Opciones de base de datos
3.  Consideraciones sobre redes y seguridad
4.  Consideraciones sobre autenticación y autorización

## <a name="compute-choices"></a>Opciones de proceso

Hay varias opciones para migrar aplicaciones de .NET Framework existentes a Azure.  Sin embargo, como .NET Framework depende de Windows, las siguientes opciones están limitadas a los servicios de proceso basados en Windows.

En la tabla siguiente se muestran varias comparaciones y recomendaciones para ayudarle a elegir la ruta adecuada para migrar su aplicación de .NET existente.

|                 | Máquinas virtuales de Azure | Azure App Service | Contenedores de Windows |
|-----------------|-----------|-------------------|--------------------|
|Cuándo se deben usar      |<ul><li>La aplicación tiene fuertes dependencias en las instalaciones de .msi local y de servidor.</li><li>Desea la ruta de migración de aplicaciones más sencilla</li></ul>|La aplicación no tiene ninguna dependencia en el servidor, es una aplicación web ASP.NET (MVC, WebForm) limpia o una aplicación de N niveles (Web API, WCF) con acceso a un servidor de base de datos. |<ul><li>La aplicación tiene dependencias en el servidor original, pero esas dependencias pueden incluirse en la imagen Windows de Docker.</li><li>Desea modernizar la aplicación para que esté [preparada para DevOps en la nube](https://docs.microsoft.com/dotnet/standard/modernize-with-azure-and-containers/lift-and-shift-existing-apps-devops/reasons-to-lift-and-shift-existing-net-apps-to-cloud-devops-ready-applications)</li></ul>|
|Ventajas y beneficios  |<ul><li>Ruta de migración más sencilla</li><li>Entorno familiar. El entorno de implementación es una máquina virtual, por lo que es muy similar a los servidores locales.</li></ul> |Mantenimiento de PaaS continuado, la forma de más sencilla de administrar y escalar aplicaciones en Azure. |<ul><li>Preparada para el futuro, preparada para DevOps en la nube con dependencias incluidas en los contenedores de la aplicación.</li><li>Casi no es necesario refactorizar el código .NET o C#.</li></ul> |
|Desventajas             |Es IaaS. El mantenimiento es costoso. Tiene que administrar la infraestructura de las máquinas virtuales: redes, equilibrador de carga, escalabilidad horizontal, administración de IIS, etc. |<ul><li>No todas las aplicaciones son [compatibles](http://www.migratetoazure.net/ReadinessAssessment)</li><li>Quizás sea necesario refactorizar algunas aplicaciones e, incluso, volver a diseñarlas, para que admitan Azure App Service.</li></ul> |<ul><li>Curva de aprendizaje de los conocimientos de Docker</li><li>Algunos cambios en el código y la configuración de la aplicación</li></ul>|
|Requisitos |Máquina virtual Windows Server con los mismos requisitos que la aplicación en el entorno local | Los requisitos de Azure App Service se especifican en [Análisis de compatibilidad para Azure App Service](https://www.migratetoazure.net/Resources). |<ul><li>[Máquina virtual de Azure "Windows Server 2016 with Containers"](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview)<br />o</li><li>[Azure Container Service (AKS)](https://azure.microsoft.com/services/container-service/) (el orquestador de Kubernetes)<br />o<li>Orquestador de [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/)</li></ul> |
|Cómo migrar |Consulte [Migración a máquinas virtuales de Azure](https://go.microsoft.com/fwlink/?linkid=862531) | Consulte [Migración a Azure App Service](https://go.microsoft.com/fwlink/?linkid=862532) | Siga las consideraciones, los escenarios y los tutoriales que se explican en el libro electrónico [Modernizing existing .NET apps with Azure and Windows Containers](https://aka.ms/liftandshiftwithcontainersebook) (Modernización de las aplicaciones .NET existentes con Azure y Windows Containers) |

 El siguiente diagrama de flujo muestra un árbol de decisión a la hora de planear una migración a Azure para las aplicaciones de .NET Framework existentes. La opción A es la primera que se probará para ver si es viable, pero la opción B es la ruta más sencilla.

![Diagrama que muestra el árbol de decisión de hospedaje](media/dotnet-howto-choose-migration/decision-tree.png)

## <a name="database-choices"></a>Opciones de base de datos

Hay varias opciones para migrar las bases de datos relacionales a Azure. Consulte [Migración de su base de datos SQL Server a Azure SQL Database](https://go.microsoft.com/fwlink/?linkid=862533) como ayuda para elegir la ruta de migración correcta de la base de datos para la aplicación de .NET existente.

## <a name="networking-and-security-considerations"></a>Consideraciones sobre redes y seguridad

Al implementar aplicaciones en una nube pública como Microsoft Azure, quizás quiera aislar y proteger determinadas redes mediante la [creación de redes perimetrales](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/), por ejemplo, una [red perimetral entre Azure y el entorno local](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-hybrid) o una [red perimetral entre Azure e Internet](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/secure-vnet-dmz). Las redes perimetrales se pueden implementar con [Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview).
Azure Virtual Network permite:

- Crear una infraestructura híbrida bajo su control
- Traer sus propias direcciones IP y servidores DNS
- Proteja sus conexiones con una red VPN IPsec o ExpressRoute
- Obtenga control detallado del tráfico entre las subredes
- Cree topologías de red sofisticadas con aplicaciones virtuales
- Obtenga un entorno aislado y de alta seguridad para sus aplicaciones
 
Para empezar a crear su propia red virtual, consulte la [documentación de Azure Virtual Network](https://docs.microsoft.com/azure/virtual-network/).

## <a name="authentication-and-authorization-considerations-when-migrating-to-azure"></a>Consideraciones sobre autenticación y autorización para migrar a Azure

Una de las principales preocupaciones de una organización a la hora de trasladarse a la nube es la seguridad. La mayoría de las empresas ha invertido una cantidad considerable de tiempo, dinero e ingeniería en diseñar y desarrollar un modelo de seguridad, y es importante que puedan aprovechar las inversiones existentes, tales como los almacenes de identidades y las soluciones de inicio de sesión único.

Muchas aplicaciones B2E empresariales de .NET existentes que se ejecutan en entornos locales usan Active Directory para la autenticación y administración de identidades.  Azure AD Connect permite integrar sus directorios locales con Azure Active Directory.  Para comenzar, consulte [Integración de los directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).

Vea los [requisitos de identidad para su solución de identidad híbrida](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-business-needs) para poder continuar el planeamiento en relación con Azure Active Directory.

Otras opciones de protocolo de autenticación son [OAuth](https://en.wikipedia.org/wiki/OAuth) y [OpenID](https://en.wikipedia.org/wiki/OpenID), que son comunes en las aplicaciones orientadas al consumidor.  Cuando se utilizan bases de datos de identidad autónomas, como una base de datos SQL de ASP.NET Identity encapsulada por IdentityServer4 que usa OAuth, normalmente no se necesita conectividad a bases de datos o directorios locales.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Migración de una aplicación web ASP.NET a Azure App Service](dotnet-howto-migrate-app-service.md)