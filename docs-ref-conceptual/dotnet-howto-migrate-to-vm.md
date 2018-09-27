---
title: Migración de una aplicación web ASP.NET a una máquina virtual de Azure
description: Vea cómo migrar una aplicación web ASP.NET de un entorno local a una máquina virtual de Azure.
ms.date: 11/15/2017
ms.service: virtual-machines
ms.openlocfilehash: b33bffdf774688d9d7eb5947f1a080b021ba259c
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190708"
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a>Migración de una aplicación web ASP.NET a una máquina virtual de Azure

En este documento se describe cómo migrar una aplicación web ASP.NET de un entorno local a una máquina virtual de Azure.

## <a name="quickstart"></a>Guía de inicio rápido

Vea cómo crear una máquina virtual y publicar la aplicación en ella: [Publicar en una máquina virtual de Azure](https://tutorials.visualstudio.com/aspnet-vm/intro)

## <a name="get-started"></a>Introducción

Estos tutoriales muestran los pasos para crear (o migrar) una máquina virtual, publicar la aplicación web en ella y otras tareas que pueden ser necesarias para admitir la aplicación en Azure.

- Cree una máquina virtual para la aplicación ASP.NET en Azure mediante una de las dos opciones siguientes:
    - [Creación de una nueva máquina virtual para aplicaciones ASP.NET](https://go.microsoft.com/fwlink/?linkid=863237)
    - [Migración de una máquina virtual local existente](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [Publicación de la aplicación mediante Visual Studio](https://go.microsoft.com/fwlink/?linkid=863240)
- [Creación de una red virtual segura para sus máquinas virtuales](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [Creación de una canalización de CI/CD para la aplicación](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [Traslado a un conjunto de escalado de máquinas virtuales para alta disponibilidad y escalabilidad](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a>Consideraciones

### <a name="benefits"></a>Ventajas

Las máquinas virtuales ofrecen una ruta más sencilla para migrar una aplicación de un entorno local a la nube.  Permiten replicar el mismo entorno que la aplicación usa de forma local, pero elimina la necesidad de mantener sus propios centros de datos.  Los conjuntos de escalado de máquinas virtuales proporcionan alta disponibilidad y escalabilidad para las aplicaciones que se ejecutan en las máquinas virtuales.

### <a name="virtual-machine-size"></a>Tamaño de la máquina virtual

Elija el tamaño y el tipo de máquina virtual más adecuados para la carga de trabajo.  Para más información, consulte [Tamaños de las máquinas virtuales Windows en Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).

### <a name="maintenance"></a>Mantenimiento 

Al igual que una máquina local, es su responsabilidad de mantener y actualizar la máquina virtual<sup>&#42;</sup>.  Si la aplicación puede ejecutarse en un entorno de Plataforma como servicio (PaaS), por ejemplo, [Azure App Service](https://docs.microsoft.com/azure/app-service/) o en un [contenedor](https://docs.microsoft.com/azure/app-service/containers/), esto ya no será necesario.

*<sup>&#42;</sup>[Las actualizaciones automáticas del sistema operativo para los conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) están disponibles en versión preliminar.*

### <a name="virtual-networks"></a>Virtual Networks

Azure Virtual Network permite:
- Crear una infraestructura híbrida bajo su control
- Traer sus propias direcciones IP y servidores DNS
- Crear un entorno aislado y de alta seguridad para sus aplicaciones
- Conectar su máquina virtual a la red local mediante diversas [opciones de conectividad](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)
- Integrar la máquina virtual en la red local mediante [ExpressRoute](https://azure.microsoft.com/services/expressroute/)

Para comenzar, consulte la [documentación de Virtual Network](https://docs.microsoft.com/azure/virtual-network/)

### <a name="active-directory"></a>Active Directory
Muchas aplicaciones usan Active Directory para la autenticación y administración de identidades.  
- Azure AD Connect permite integrar sus directorios locales con Azure Active Directory.  Para comenzar, consulte [Integración de los directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).  
- [ExpressRoute](https://azure.microsoft.com/services/expressroute/) también permite que la aplicación tenga acceso a su directorio local de Active Directory.

### <a name="sql-databases"></a>Instancias de SQL Database

Si su aplicación usa una base de datos local, la aplicación no podrá comunicarse con ella de forma predeterminada. Puede:
- Configurar una red híbrida que permita que la aplicación tenga acceso a la base de datos que se ejecuta de forma local.  
- Migrar la base de datos a Azure.  Para más información, consulte [Migración de una base de datos SQL Server a Azure SQL Database](dotnet-howto-migrate-sql.md).

### <a name="high-availability-and-scalability"></a>Alta disponibilidad y escalabilidad

#### <a name="virtual-machine-scale-sets"></a>Virtual Machine Scale Sets
Si desea asegurarse de que la aplicación tenga alta disponibilidad y pueda escalar, migre la imagen de su máquina virtual a un conjunto de escalado de máquinas virtuales de Azure para mejorar la disponibilidad y escalabilidad de la aplicación.  VM Scale Sets permite usar una máquina virtual existente ya configurada o configurar una canalización de compilación para crear una imagen con la aplicación.  

Para comenzar, consulte [Implementación de la aplicación en conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).

#### <a name="centralized-logging"></a>Registro centralizado
Si la aplicación se ejecuta en varias instancias, considere la posibilidad de almacenar los registros en una ubicación centralizada, por ejemplo, [Azure Storage](https://docs.microsoft.com/azure/storage/).

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Migración de una base de datos de SQL Server a Azure](dotnet-howto-migrate-sql.md)