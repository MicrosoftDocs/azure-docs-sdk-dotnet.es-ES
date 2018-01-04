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
# <a name="migrate-a-sql-server-database-to-azure"></a><span data-ttu-id="63e1f-104">Migración de una base de datos de SQL Server a Azure</span><span class="sxs-lookup"><span data-stu-id="63e1f-104">Migrate a SQL Server database to Azure</span></span>

<span data-ttu-id="63e1f-105">Azure tiene dos opciones principales para migrar una base de datos de SQL Server de producción:</span><span class="sxs-lookup"><span data-stu-id="63e1f-105">Azure has two primary options for migrating a production SQL Server database:</span></span>

1. <span data-ttu-id="63e1f-106">[SQL Server en máquinas virtuales de Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/): una instancia de SQL Server instalada y hospedada en una máquina Virtual Windows que se ejecuta en Azure, también conocida como Infraestructura como servicio (IaaS).</span><span class="sxs-lookup"><span data-stu-id="63e1f-106">[SQL Server on Azure VMs](https://azure.microsoft.com/services/virtual-machines/sql-server/): A SQL Server instance installed and hosted on a Windows Virtual Machine running in Azure, also known as Infrastructure as a Service (IaaS).</span></span>
2. <span data-ttu-id="63e1f-107">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/): un servicio de base de datos SQL de Azure completamente administrado, también conocido como Plataforma como servicio (PaaS).</span><span class="sxs-lookup"><span data-stu-id="63e1f-107">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/): A fully managed SQL database Azure service, also known as Platform as a Service (PaaS).</span></span>

<span data-ttu-id="63e1f-108">Ambos tiene ventajas y desventajas que debe evaluar antes de migrar.</span><span class="sxs-lookup"><span data-stu-id="63e1f-108">Both come with pros and cons that you will need to evaluate before migrating.</span></span>

## <a name="choosing-iaas-or-paas"></a><span data-ttu-id="63e1f-109">Elección de IaaS o PaaS</span><span class="sxs-lookup"><span data-stu-id="63e1f-109">Choosing IaaS or PaaS</span></span>

<span data-ttu-id="63e1f-110">En primer lugar, debe determinar si IaaS o PaaS es más adecuado para usted.</span><span class="sxs-lookup"><span data-stu-id="63e1f-110">First, you should determine if IaaS or PaaS is more appropriate for you.</span></span>

<span data-ttu-id="63e1f-111">**Elija SQL Server en máquinas virtuales de Azure si:**</span><span class="sxs-lookup"><span data-stu-id="63e1f-111">**You should choose SQL Server in Azure VMs if:**</span></span>

* <span data-ttu-id="63e1f-112">Desea migrar mediante “lift and shift” la base de datos y las aplicaciones ningún cambio, o muy pocos.</span><span class="sxs-lookup"><span data-stu-id="63e1f-112">You are looking to "lift and shift" your database and applications with minimal to no changes.</span></span>
* <span data-ttu-id="63e1f-113">Prefiere tener control total sobre el servidor de base de datos y la máquina virtual donde se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="63e1f-113">You prefer having full control over your database server and the VM it runs on.</span></span>
* <span data-ttu-id="63e1f-114">Ya tiene licencias de SQL Server y Windows Server, y tiene previsto usarlas.</span><span class="sxs-lookup"><span data-stu-id="63e1f-114">You already have SQL Server and Windows Server licenses that you intend to use.</span></span>

<span data-ttu-id="63e1f-115">**Elija Azure SQL Database si:**</span><span class="sxs-lookup"><span data-stu-id="63e1f-115">**You should choose Azure SQL Database if:**</span></span>

* <span data-ttu-id="63e1f-116">Desea modernizar las aplicaciones y va a realizar la migración para usar otros servicios de PaaS en Azure.</span><span class="sxs-lookup"><span data-stu-id="63e1f-116">You are looking to modernize your applications and are migrating to use other PaaS services in Azure.</span></span>
* <span data-ttu-id="63e1f-117">No desea administrar el servidor de base de datos y la máquina virtual donde se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="63e1f-117">You do not wish to manage your database server and the VM it runs on.</span></span>
* <span data-ttu-id="63e1f-118">No tiene licencias de SQL Server o Windows Server, o tiene previsto dejar que las licencias que tiene expiren.</span><span class="sxs-lookup"><span data-stu-id="63e1f-118">You do not have SQL Server or Windows Server licenses, or you intend to let licenses you have expire.</span></span>

<span data-ttu-id="63e1f-119">En la tabla siguiente se describen las diferencias entre cada servicio según los distintos escenarios.</span><span class="sxs-lookup"><span data-stu-id="63e1f-119">The following table describes differences between each service based on a set of scenarios.</span></span>

| <span data-ttu-id="63e1f-120">Escenario</span><span class="sxs-lookup"><span data-stu-id="63e1f-120">Scenario</span></span> | <span data-ttu-id="63e1f-121">SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="63e1f-121">SQL Server in Azure VMs</span></span> | <span data-ttu-id="63e1f-122">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="63e1f-122">Azure SQL Database</span></span> |
|----------|-------------------------|--------------------|
| <span data-ttu-id="63e1f-123">Migración</span><span class="sxs-lookup"><span data-stu-id="63e1f-123">Migration</span></span> | <span data-ttu-id="63e1f-124">Requiere cambios mínimos en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="63e1f-124">Requires minimal changes to your database.</span></span> | <span data-ttu-id="63e1f-125">Puede requerir cambios en la base de datos si usa características no disponibles en Azure SQL, según determine el [Asistente para la migración de datos](https://www.microsoft.com/download/details.aspx?id=53595), o si tiene otras dependencias tales como archivos ejecutables instalados localmente.</span><span class="sxs-lookup"><span data-stu-id="63e1f-125">May require changes to your database if you use features unavailable in Azure SQL, as determined by the [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595), or if you have other dependencies such as locally installed executables.</span></span>|
| <span data-ttu-id="63e1f-126">Administración de la disponibilidad, la recuperación y las actualizaciones</span><span class="sxs-lookup"><span data-stu-id="63e1f-126">Managing availability, recovery, and upgrades</span></span> | <span data-ttu-id="63e1f-127">La disponibilidad y la recuperación se configuran manualmente.</span><span class="sxs-lookup"><span data-stu-id="63e1f-127">Availability and recovery is configured manually.</span></span> <span data-ttu-id="63e1f-128">Las actualizaciones se pueden automatizar con los [conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade).</span><span class="sxs-lookup"><span data-stu-id="63e1f-128">Upgrades can be automated with [VM Scale Sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade).</span></span> | <span data-ttu-id="63e1f-129">Se administra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="63e1f-129">Automatically managed for you.</span></span> |
| <span data-ttu-id="63e1f-130">Configuración del sistema operativo subyacente</span><span class="sxs-lookup"><span data-stu-id="63e1f-130">Underlying OS configuration</span></span> | <span data-ttu-id="63e1f-131">Configuración manual.</span><span class="sxs-lookup"><span data-stu-id="63e1f-131">Manual configuration.</span></span> | <span data-ttu-id="63e1f-132">Se administra automáticamente.</span><span class="sxs-lookup"><span data-stu-id="63e1f-132">Automatically managed for you.</span></span> |
| <span data-ttu-id="63e1f-133">Administración del tamaño de base de datos</span><span class="sxs-lookup"><span data-stu-id="63e1f-133">Managing database size</span></span> | <span data-ttu-id="63e1f-134">Admite hasta 64 TB de almacenamiento por cada instancia de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="63e1f-134">Supports up to 64TB of storage per SQL Server instance.</span></span> | <span data-ttu-id="63e1f-135">Admite 4 TB de almacenamiento antes de necesitar una partición horizontal.</span><span class="sxs-lookup"><span data-stu-id="63e1f-135">Supports 4TB of storage before needing a horizontal partition.</span></span> |
| <span data-ttu-id="63e1f-136">Administración de los costos</span><span class="sxs-lookup"><span data-stu-id="63e1f-136">Managing costs</span></span> | <span data-ttu-id="63e1f-137">Debe administrar los costos de las licencias de SQL Server, los costos de las licencias de Windows Server y los costos de las máquinas virtuales (en función del número de núcleos, la memoria RAM y el almacenamiento).</span><span class="sxs-lookup"><span data-stu-id="63e1f-137">You must manage SQL Server license costs, Windows Server license costs, and VM costs (based on cores, RAM, and storage).</span></span> | <span data-ttu-id="63e1f-138">Debe administrar los costos del servicio (en función del número de [eDTU o DTU](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), el almacenamiento y el número de bases de datos si usa un grupo elástico).</span><span class="sxs-lookup"><span data-stu-id="63e1f-138">You must manage service costs (based on [eDTUs or DTUs](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu), storage, and number of databases if using an elastic pool).</span></span>  <span data-ttu-id="63e1f-139">También debe administrar el costo de los SLA.</span><span class="sxs-lookup"><span data-stu-id="63e1f-139">You must also manage the cost of any SLA.</span></span> |

<span data-ttu-id="63e1f-140">Para más información acerca de las diferencias entre los dos, lea [Choose a cloud SQL Server option: Azure SQL Database or SQL Server on Azure VMs](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas) (Elegir una opción de SQL Server en la nube: Azure SQL Database o SQL Server en máquinas virtuales de Azure).</span><span class="sxs-lookup"><span data-stu-id="63e1f-140">To learn more about the differences between the two, read [Choose a cloud SQL Server option: Azure SQL Database or SQL Server on Azure VMs](https://docs.microsoft.com/azure/sql-database/sql-database-paas-vs-sql-server-iaas).</span></span>

## <a name="get-started"></a><span data-ttu-id="63e1f-141">Introducción</span><span class="sxs-lookup"><span data-stu-id="63e1f-141">Get started</span></span>

<span data-ttu-id="63e1f-142">El siguiente paso es migrar la base de datos.</span><span class="sxs-lookup"><span data-stu-id="63e1f-142">The next step is to migrate your database.</span></span>  <span data-ttu-id="63e1f-143">Las siguientes son guías de migración útiles, dependiendo de lo que elija:</span><span class="sxs-lookup"><span data-stu-id="63e1f-143">The following guides are useful migration guides, depending on what you chose:</span></span>

* [<span data-ttu-id="63e1f-144">Migración de una base de datos SQL Server a SQL Server en una VM de Azure</span><span class="sxs-lookup"><span data-stu-id="63e1f-144">Migrate a SQL Server database to SQL Server in an Azure VM</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-migrate-sql)
* [<span data-ttu-id="63e1f-145">Migración de una base de datos SQL Server a Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="63e1f-145">Migrate your SQL Server database to Azure SQL Database</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-migrate-your-sql-server-database)

<span data-ttu-id="63e1f-146">Además, los vínculos siguientes le ayudarán a comprender mejor las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="63e1f-146">Additionally, the following links will help you understand VMs better:</span></span>

* [<span data-ttu-id="63e1f-147">Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="63e1f-147">High availability and disaster recovery for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-high-availability-dr)
* [<span data-ttu-id="63e1f-148">Procedimientos recomendados para SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="63e1f-148">Performance best practices for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)
* [<span data-ttu-id="63e1f-149">Estrategias de desarrollo y patrones de aplicación de SQL Server en Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="63e1f-149">Application Patterns and Development Strategies for SQL Server in Azure Virtual Machines</span></span>](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-app-patterns-dev-strategies)

<span data-ttu-id="63e1f-150">Y los vínculos siguientes le ayudarán a comprender mejor Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="63e1f-150">And the following links will help you understand Azure SQL Database better:</span></span>

* [<span data-ttu-id="63e1f-151">Creación y administración de servidores y bases de datos de Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="63e1f-151">Create and manage Azure SQL Database servers and databases</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-servers-databases)
* [<span data-ttu-id="63e1f-152">Unidades de transacción de bases de datos (DTU) y unidades de transacción de bases de datos elásticas (eDTU)</span><span class="sxs-lookup"><span data-stu-id="63e1f-152">Database Transaction Units (DTUs) and elastic Database Transaction Units (eDTUs)</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-what-is-a-dtu)
* [<span data-ttu-id="63e1f-153">Límites de recursos de SQL Database</span><span class="sxs-lookup"><span data-stu-id="63e1f-153">Azure SQL Database resource limits</span></span>](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits)

## <a name="faq"></a><span data-ttu-id="63e1f-154">P+F</span><span class="sxs-lookup"><span data-stu-id="63e1f-154">FAQ</span></span>

* <span data-ttu-id="63e1f-155">**¿Puedo seguir usando herramientas como SQL Server Management Studio y SQL Server Reporting Services (SSRS) con SQL Server en máquinas virtuales de Azure o con Azure SQL Database?**</span><span class="sxs-lookup"><span data-stu-id="63e1f-155">**Can I still use tools such as SQL Server Management Studio and SQL Server Reporting Services (SSRS) with SQL Server in Azure VMs or Azure SQL Database?**</span></span>

    <span data-ttu-id="63e1f-156">Sí.</span><span class="sxs-lookup"><span data-stu-id="63e1f-156">Yes!</span></span> <span data-ttu-id="63e1f-157">Todas las herramientas de Microsoft SQL funcionan con ambos servicios.</span><span class="sxs-lookup"><span data-stu-id="63e1f-157">All Microsoft SQL tooling works with both services.</span></span> <span data-ttu-id="63e1f-158">Sin embargo, SSRS no forma parte de Azure SQL Database. Se recomienda ejecutarlo en una máquina virtual de Azure y, a continuación, hacer que apunte a la instancia de base de datos.</span><span class="sxs-lookup"><span data-stu-id="63e1f-158">SSRS is not part of Azure SQL Database, though, and it's recommended that you run it in an Azure VM and then point it to your database instance.</span></span>
    
* <span data-ttu-id="63e1f-159">**Quiero cambiar a PaaS pero no estoy seguro de si mi base de datos es compatible. ¿Hay alguna herramienta que pueda ayudar?**</span><span class="sxs-lookup"><span data-stu-id="63e1f-159">**I want to go PaaS but I'm not sure if my database is compatible. Are there tools to help?**</span></span>

    <span data-ttu-id="63e1f-160">Sí.</span><span class="sxs-lookup"><span data-stu-id="63e1f-160">Yes.</span></span> <span data-ttu-id="63e1f-161">El [Asistente para la migración de datos](https://www.microsoft.com/download/details.aspx?id=53595) es una herramienta que se usa como parte de la migración a Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="63e1f-161">The [Data Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) is a tool that is used as a part of migrating to Azure SQL Database.</span></span>  <span data-ttu-id="63e1f-162">[Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) es un servicio en versión preliminar que puede usar para IaaS o PaaS.</span><span class="sxs-lookup"><span data-stu-id="63e1f-162">The [Azure Database Migration Service](https://azure.microsoft.com/campaigns/database-migration/) is a preview service which you can use for either IaaS or PaaS.</span></span>

* <span data-ttu-id="63e1f-163">**¿Puedo calcular los costos?**</span><span class="sxs-lookup"><span data-stu-id="63e1f-163">**Can I estimate costs?**</span></span>

    <span data-ttu-id="63e1f-164">Sí.</span><span class="sxs-lookup"><span data-stu-id="63e1f-164">Yes.</span></span>  <span data-ttu-id="63e1f-165">Puede usar la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/) para calcular los costos de todos los servicios de Azure, incluidos los servicios de máquinas virtuales y base de datos.</span><span class="sxs-lookup"><span data-stu-id="63e1f-165">The [Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) can be used for estimating costs for all Azure services, including VMs and database services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63e1f-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="63e1f-166">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63e1f-167">Elección de la opción de hospedaje de Azure correcta</span><span class="sxs-lookup"><span data-stu-id="63e1f-167">Choose the right Azure hosting option</span></span>](dotnet-howto-choose-migration.md)