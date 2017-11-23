---
title: "Migración de una aplicación web ASP.NET a una máquina virtual de Azure"
description: "Vea cómo migrar una aplicación web ASP.NET de un entorno local a una máquina virtual de Azure."
keywords: "Azure .NET, ASP.NET, máquina virtual, migrar, migración"
author: camsoper
manager: wpickett
ms.author: casoper
ms.date: 11/15/2017
ms.topic: article
ms.technology: azure
ms.devlang: dotnet
ms.service: virtual-machines
ms.custom: devcenter
ms.openlocfilehash: 718d91b98180a7584f78a2383d430c4700743306
ms.sourcegitcommit: c360a22d5bff6eedd714b28b847d2f26b06665f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2017
---
# <a name="migrate-an-aspnet-web-application-to-an-azure-virtual-machine"></a><span data-ttu-id="4a388-104">Migración de una aplicación web ASP.NET a una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="4a388-104">Migrate an ASP.NET Web application to an Azure Virtual Machine</span></span>

<span data-ttu-id="4a388-105">En este documento se describe cómo migrar una aplicación web ASP.NET de un entorno local a una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="4a388-105">This document provides an overview of how to migrate an ASP.NET web application from on-premises to an Azure Virtual Machine.</span></span>

## <a name="get-started"></a><span data-ttu-id="4a388-106">Introducción</span><span class="sxs-lookup"><span data-stu-id="4a388-106">Get Started</span></span>

<span data-ttu-id="4a388-107">Estos tutoriales muestran los pasos para crear (o migrar) una máquina virtual, publicar la aplicación web en ella y otras tareas que pueden ser necesarias para admitir la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="4a388-107">These tutorials demonstrate the steps to create (or migrate) a virtual machine, publish your web application to it, and other tasks that may be required to support your application in Azure.</span></span>

- <span data-ttu-id="4a388-108">Cree una máquina virtual para la aplicación ASP.NET en Azure mediante una de las dos opciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="4a388-108">Create a virtual machine for your ASP.NET application in Azure using one of the following two options:</span></span>
    - [<span data-ttu-id="4a388-109">Creación de una nueva máquina virtual para aplicaciones ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4a388-109">Create a new virtual machine for ASP.NET Applications</span></span>](https://go.microsoft.com/fwlink/?linkid=863237)
    - [<span data-ttu-id="4a388-110">Migración de una máquina virtual local existente</span><span class="sxs-lookup"><span data-stu-id="4a388-110">Migrate an existing on-premises virtual machine</span></span>](https://docs.microsoft.com/azure/site-recovery/tutorial-migrate-on-premises-to-azure)
- [<span data-ttu-id="4a388-111">Publicación de la aplicación mediante Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a388-111">Publish your app using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?linkid=863240)
- [<span data-ttu-id="4a388-112">Creación de una red virtual segura para sus máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="4a388-112">Create a secure virtual network for your VMs</span></span>](https://docs.microsoft.com/azure/virtual-network/virtual-network-get-started-vnet-subnet)
- [<span data-ttu-id="4a388-113">Creación de una canalización de CI/CD para la aplicación</span><span class="sxs-lookup"><span data-stu-id="4a388-113">Create a CI/CD pipeline for your application</span></span>](https://docs.microsoft.com/vsts/build-release/apps/cd/deploy-webdeploy-iis-deploygroups)
- [<span data-ttu-id="4a388-114">Traslado a un conjunto de escalado de máquinas virtuales para alta disponibilidad y escalabilidad</span><span class="sxs-lookup"><span data-stu-id="4a388-114">Move to a VM scale set for high availability and scalability</span></span>](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app)

## <a name="considerations"></a><span data-ttu-id="4a388-115">Consideraciones</span><span class="sxs-lookup"><span data-stu-id="4a388-115">Considerations</span></span>

### <a name="benefits"></a><span data-ttu-id="4a388-116">Ventajas</span><span class="sxs-lookup"><span data-stu-id="4a388-116">Benefits</span></span>

<span data-ttu-id="4a388-117">Las máquinas virtuales ofrecen una ruta más sencilla para migrar una aplicación de un entorno local a la nube.</span><span class="sxs-lookup"><span data-stu-id="4a388-117">Virtual machines offer the easiest path to migrate an application from on-premises to the cloud.</span></span>  <span data-ttu-id="4a388-118">Permiten replicar el mismo entorno que la aplicación usa de forma local, pero elimina la necesidad de mantener sus propios centros de datos.</span><span class="sxs-lookup"><span data-stu-id="4a388-118">They enable you to replicate the same environment your application uses on-premises, while removing the need to maintain your own data centers.</span></span>  <span data-ttu-id="4a388-119">Los conjuntos de escalado de máquinas virtuales proporcionan alta disponibilidad y escalabilidad para las aplicaciones que se ejecutan en las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="4a388-119">Virtual Machine Scale Sets provide high availability and scalability for applications running in Virtual Machines.</span></span>

### <a name="virtual-machine-size"></a><span data-ttu-id="4a388-120">Tamaño de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4a388-120">Virtual Machine Size</span></span>

<span data-ttu-id="4a388-121">Elija el tamaño y el tipo de máquina virtual más adecuados para la carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="4a388-121">Choose the virtual machine size and type that is best optimized for your workload.</span></span>  <span data-ttu-id="4a388-122">Para más información, consulte [Tamaños de las máquinas virtuales Windows en Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span><span class="sxs-lookup"><span data-stu-id="4a388-122">See [sizes for Windows virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) for more information.</span></span>

### <a name="maintenance"></a><span data-ttu-id="4a388-123">Mantenimiento</span><span class="sxs-lookup"><span data-stu-id="4a388-123">Maintenance</span></span>

<span data-ttu-id="4a388-124">Al igual que una máquina local, es su responsabilidad de mantener y actualizar la máquina virtual<sup>&#42;</sup>.</span><span class="sxs-lookup"><span data-stu-id="4a388-124">Just like an on-premises machine, you are responsible for maintaining and updating the virtual machine<sup>&#42;</sup>.</span></span>  <span data-ttu-id="4a388-125">Si la aplicación puede ejecutarse en un entorno de Plataforma como servicio (PaaS), por ejemplo, [Azure App Service](https://docs.microsoft.com/azure/app-service/) o en un [contenedor](https://docs.microsoft.com/azure/app-service/containers/), esto ya no será necesario.</span><span class="sxs-lookup"><span data-stu-id="4a388-125">If your application can run in a Platform as a Service (PaaS) environment such as [Azure App Service](https://docs.microsoft.com/azure/app-service/) or in a [container](https://docs.microsoft.com/azure/app-service/containers/), that will remove this need.</span></span>

<span data-ttu-id="4a388-126">*<sup>&#42;</sup>[Las actualizaciones automáticas del sistema operativo para los conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) están disponibles en versión preliminar.*</span><span class="sxs-lookup"><span data-stu-id="4a388-126">*<sup>&#42;</sup>[Automatic OS upgrades for virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-automatic-upgrade) is currently available as a Preview service.*</span></span>

### <a name="virtual-networks"></a><span data-ttu-id="4a388-127">Virtual Networks</span><span class="sxs-lookup"><span data-stu-id="4a388-127">Virtual Networks</span></span>

<span data-ttu-id="4a388-128">Azure Virtual Network permite:</span><span class="sxs-lookup"><span data-stu-id="4a388-128">Azure Virtual Networks enable you to:</span></span>
- <span data-ttu-id="4a388-129">Crear una infraestructura híbrida bajo su control</span><span class="sxs-lookup"><span data-stu-id="4a388-129">Build a hybrid infrastructure that you control</span></span>
- <span data-ttu-id="4a388-130">Traer sus propias direcciones IP y servidores DNS</span><span class="sxs-lookup"><span data-stu-id="4a388-130">Bring your own IP addresses and DNS servers</span></span>
- <span data-ttu-id="4a388-131">Crear un entorno aislado y de alta seguridad para sus aplicaciones</span><span class="sxs-lookup"><span data-stu-id="4a388-131">Create an isolated and highly-secure environment for your applications</span></span>
- <span data-ttu-id="4a388-132">Conectar su máquina virtual a la red local mediante diversas [opciones de conectividad](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span><span class="sxs-lookup"><span data-stu-id="4a388-132">Connect your VM to your on-premises network using one of several [connectivity options](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpngateways#s2smulti)</span></span>
- <span data-ttu-id="4a388-133">Integrar la máquina virtual en la red local mediante [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span><span class="sxs-lookup"><span data-stu-id="4a388-133">Integrate your virtual machine into your on-premises network using [ExpressRoute](https://azure.microsoft.com/services/expressroute/)</span></span>

<span data-ttu-id="4a388-134">Para comenzar, consulte la [documentación de Virtual Network](https://docs.microsoft.com/azure/virtual-network/)</span><span class="sxs-lookup"><span data-stu-id="4a388-134">To get started, see the [Virtual Network documentation](https://docs.microsoft.com/azure/virtual-network/)</span></span>

### <a name="active-directory"></a><span data-ttu-id="4a388-135">Active Directory</span><span class="sxs-lookup"><span data-stu-id="4a388-135">Active Directory</span></span>
<span data-ttu-id="4a388-136">Muchas aplicaciones usan Active Directory para la autenticación y administración de identidades.</span><span class="sxs-lookup"><span data-stu-id="4a388-136">Many applications use Active Directory for authentication and identity management.</span></span>  
- <span data-ttu-id="4a388-137">Azure AD Connect permite integrar sus directorios locales con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a388-137">Azure AD Connect enables you to integrate your on-premises directories with Azure Active Directory.</span></span>  <span data-ttu-id="4a388-138">Para comenzar, consulte [Integración de los directorios locales con Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span><span class="sxs-lookup"><span data-stu-id="4a388-138">To get started, see [Integrate your on-premises directories with Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>  
- <span data-ttu-id="4a388-139">[ExpressRoute](https://azure.microsoft.com/services/expressroute/) también permite que la aplicación tenga acceso a su directorio local de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4a388-139">Alternatively, [ExpressRoute](https://azure.microsoft.com/services/expressroute/) enables your application to access your on-premises Active Directory.</span></span>

### <a name="sql-databases"></a><span data-ttu-id="4a388-140">Instancias de SQL Database</span><span class="sxs-lookup"><span data-stu-id="4a388-140">SQL Databases</span></span>

<span data-ttu-id="4a388-141">Si su aplicación usa una base de datos local, la aplicación no podrá comunicarse con ella de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="4a388-141">If your application is using an on-premises database, your app will not be able to talk to it by default.</span></span> <span data-ttu-id="4a388-142">Puede:</span><span class="sxs-lookup"><span data-stu-id="4a388-142">You can either:</span></span>
- <span data-ttu-id="4a388-143">Configurar una red híbrida que permita que la aplicación tenga acceso a la base de datos que se ejecuta de forma local.</span><span class="sxs-lookup"><span data-stu-id="4a388-143">Configure a hybrid network that enables your application to access your database running on-premises.</span></span>  
- <span data-ttu-id="4a388-144">Migrar la base de datos a Azure.</span><span class="sxs-lookup"><span data-stu-id="4a388-144">Migrate your database to the Azure.</span></span>  <span data-ttu-id="4a388-145">Para más información, consulte [Migración de una base de datos SQL Server a Azure SQL Database](dotnet-howto-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4a388-145">See [Migrate your SQL Server database to Azure](dotnet-howto-migrate-sql.md) for more information.</span></span>

### <a name="high-availability-and-scalability"></a><span data-ttu-id="4a388-146">Alta disponibilidad y escalabilidad</span><span class="sxs-lookup"><span data-stu-id="4a388-146">High Availability and Scalability</span></span>

#### <a name="virtual-machine-scale-sets"></a><span data-ttu-id="4a388-147">Conjuntos de escalado de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4a388-147">Virtual Machine Scale Sets</span></span>
<span data-ttu-id="4a388-148">Si desea asegurarse de que la aplicación tenga alta disponibilidad y pueda escalar, migre la imagen de su máquina virtual a un conjunto de escalado de máquinas virtuales de Azure para mejorar la disponibilidad y escalabilidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a388-148">You want to make sure that your application is highly available and can scale, migrate your VM image to an Azure Virtual Machine Scale Set to improve the availability and scalability of your application.</span></span>  <span data-ttu-id="4a388-149">Los conjuntos de escalado de máquinas virtuales permiten usar una máquina virtual existente ya configurada o configurar una canalización de compilación para crear una imagen con la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4a388-149">VM Scale Sets provide the ability to use an existing VM you’ve already configured or set up a build pipeline to build an image with your application.</span></span>  

<span data-ttu-id="4a388-150">Para comenzar, consulte [Implementación de la aplicación en conjuntos de escalado de máquinas virtuales](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span><span class="sxs-lookup"><span data-stu-id="4a388-150">To get started, see [Deploy your application on virtual machine scale sets](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-deploy-app).</span></span>

#### <a name="centralized-logging"></a><span data-ttu-id="4a388-151">Registro centralizado</span><span class="sxs-lookup"><span data-stu-id="4a388-151">Centralized Logging</span></span>
<span data-ttu-id="4a388-152">Si la aplicación se ejecuta en varias instancias, considere la posibilidad de almacenar los registros en una ubicación centralizada, por ejemplo, [Azure Storage](https://docs.microsoft.com/azure/storage/).</span><span class="sxs-lookup"><span data-stu-id="4a388-152">When running your application across multiple instances, consider storing your logs in a centralized location such as [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a388-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4a388-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4a388-154">Migración de una base de datos de SQL Server a Azure</span><span class="sxs-lookup"><span data-stu-id="4a388-154">Migrate a SQL Server database to Azure</span></span>](dotnet-howto-migrate-sql.md)