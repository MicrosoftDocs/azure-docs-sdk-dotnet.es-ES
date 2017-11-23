---
title: "Migración de una base de datos de SQL Server a Azure"
description: Aprenda a migrar una base de datos de SQL Server de un entorno local a Azure.
keywords: "Azure .NET, ASP.NET, SQL, SQL Server, SQL Database, migrar, migración"
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: sql-database
ms.custom: devcenter
ms.openlocfilehash: 967f034fcd2c2487f6a5709d243ce25fc9b6e85e
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2017
---
# <a name="migrate-a-sql-server-database-to-azure"></a>Migración de una base de datos de SQL Server a Azure

Azure tiene dos opciones principales para migrar una base de datos de SQL Server de producción:

1. [SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): una instancia de SQL Server instalada y hospedada en una máquina Virtual Windows que se ejecuta en Azure, también conocida como Infraestructura como servicio (IaaS).
2. [Azure SQL Database](https://azure.microsoft.com/services/sql-database/): un servicio de base de datos SQL de Azure completamente administrado, también conocido como Plataforma como servicio (PaaS).

Ambos tiene ventajas y desventajas que debe evaluar antes de migrar.

## <a name="choosing-iaas-or-paas"></a>Elección de IaaS o PaaS

En primer lugar, debe determinar si IaaS o PaaS es más adecuado para usted.

**Elija SQL Server en máquinas virtuales de Azure si:**

* Desea migrar mediante “lift and shift” la base de datos y las aplicaciones ningún cambio, o muy pocos.
* Prefiere tener control total sobre el servidor de base de datos y la máquina virtual donde se ejecuta.
* Ya tiene licencias de SQL Server y Windows Server, y tiene previsto usarlas.

**Elija Azure SQL Database si:**

* Desea modernizar las aplicaciones y va a realizar la migración para usar otros servicios de PaaS en Azure.
* No desea administrar el servidor de base de datos y la máquina virtual donde se ejecuta.
* No tiene licencias de SQL Server o Windows Server, o tiene previsto dejar que las licencias que tiene expiren.

En la tabla siguiente se describen las diferencias entre cada servicio según los distintos escenarios.

| Escenario | SQL Server en máquinas virtuales de Azure | Azure SQL Database |
|----------|-------------------------|--------------------|
| Migración | Requiere cambios mínimos en la base de datos. | Puede requerir cambios en la base de datos si usa características no disponibles en Azure SQL, según determine el [Asistente para la migración de datos](https://www.microsoft.com/download/details.aspx?id=53595), o si tiene otras dependencias tales como archivos ejecutables instalados localmente.|
| Administración de la disponibilidad, la recuperación y las actualizaciones | La disponibilidad y la recuperación se configuran manualmente. Las actualizaciones se pueden automatizar con los [conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade). | Se administra automáticamente. |
| Configuración del sistema operativo subyacente | Configuración manual. | Se administra automáticamente. |
| Administración del tamaño de base de datos | Admite hasta 64 TB de almacenamiento por cada instancia de SQL Server. | Admite 4 TB de almacenamiento antes de necesitar una partición horizontal. |
| Administración de los costos | Debe administrar los costos de las licencias de SQL Server, los costos de las licencias de Windows Server y los costos de las máquinas virtuales (en función del número de núcleos, la memoria RAM y el almacenamiento). | Debe administrar los costos del servicio (en función del número de [eDTU o DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), el almacenamiento y el número de bases de datos si usa un grupo elástico).  También debe administrar el costo de los SLA. |

Para más información acerca de las diferencias entre los dos, lea [Choose a cloud SQL Server option: Azure SQL Database or SQL Server on Azure VMs](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) (Elegir una opción de SQL Server en la nube: Azure SQL Database o SQL Server en máquinas virtuales de Azure).

## <a name="get-started"></a>Introducción

El siguiente paso es migrar la base de datos.  Las siguientes son guías de migración útiles, dependiendo de lo que elija:

* [Migración de una base de datos SQL Server a SQL Server en una VM de Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [Migración de una base de datos SQL Server a Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

Además, los vínculos siguientes le ayudarán a comprender mejor las máquinas virtuales:

* [Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [Procedimientos recomendados para SQL Server en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
* [Estrategias de desarrollo y patrones de aplicación de SQL Server en Azure Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

Y los vínculos siguientes le ayudarán a comprender mejor Azure SQL Database:

* [Creación y administración de servidores y bases de datos de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [Unidades de transacción de bases de datos (DTU) y unidades de transacción de bases de datos elásticas (eDTU)](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [Límites de recursos de SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="faq"></a>P+F

* **¿Puedo seguir usando herramientas como SQL Server Management Studio y SQL Server Reporting Services (SSRS) con SQL Server en máquinas virtuales de Azure o con Azure SQL Database?**

    Sí. Todas las herramientas de Microsoft SQL funcionan con ambos servicios. Sin embargo, SSRS no forma parte de Azure SQL Database. Se recomienda ejecutarlo en una máquina virtual de Azure y, a continuación, hacer que apunte a la instancia de base de datos.
    
* **Quiero cambiar a PaaS pero no estoy seguro de si mi base de datos es compatible. ¿Hay alguna herramienta que pueda ayudar?**

    Sí. El [Asistente para la migración de datos](https://www.microsoft.com/download/details.aspx?id=53595) es una herramienta que se usa como parte de la migración a Azure SQL Database.  [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) es un servicio en versión preliminar que puede usar para IaaS o PaaS.

* **¿Puedo calcular los costos?**

    Sí.  Puede usar la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para calcular los costos de todos los servicios de Azure, incluidos los servicios de máquinas virtuales y base de datos.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Elección de la opción de hospedaje de Azure correcta](dotnet-howto-choose-migration.md)