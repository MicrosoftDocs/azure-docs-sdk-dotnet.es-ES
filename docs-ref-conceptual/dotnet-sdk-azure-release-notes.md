---
title: "Notas de la versión de las bibliotecas de administración de Azure para .NET | Microsoft Docs"
description: "Vea cuáles son las novedades y cambios importantes en las bibliotecas de administración de Azure para .NET."
keywords: Azure, .NET, API, referencia, notas, actualizaciones, en desuso
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.custom: devcenter
ms.openlocfilehash: 19008714ee38ae00195b08c05fee5bf943da759f
ms.sourcegitcommit: 3ba0ff4463338a0ab0f3f15a7601b89417c06970
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="release-notes"></a><span data-ttu-id="c81f1-104">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="c81f1-104">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="c81f1-105">Disponibilidad de características y hoja de ruta a partir de la versión 1.0.0</span><span class="sxs-lookup"><span data-stu-id="c81f1-105">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="c81f1-106">26 de abril de 2017</span><span class="sxs-lookup"><span data-stu-id="c81f1-106">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="c81f1-107">Servicio | característica</span><span class="sxs-lookup"><span data-stu-id="c81f1-107">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="c81f1-108">Disponible como GA</span><span class="sxs-lookup"><span data-stu-id="c81f1-108">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="c81f1-109">Disponible como versión preliminar</span><span class="sxs-lookup"><span data-stu-id="c81f1-109">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="c81f1-110">Próximamente</span><span class="sxs-lookup"><span data-stu-id="c81f1-110">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-111">Proceso</span><span class="sxs-lookup"><span data-stu-id="c81f1-111">Compute</span></span></td>
    <td><span data-ttu-id="c81f1-112">Máquinas virtuales y extensiones de estas</span><span class="sxs-lookup"><span data-stu-id="c81f1-112">Virtual machines and VM extensions</span></span><br><span data-ttu-id="c81f1-113">Conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="c81f1-113">Virtual machine scale sets</span></span><br><span data-ttu-id="c81f1-114">Discos administrados</span><span class="sxs-lookup"><span data-stu-id="c81f1-114">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="c81f1-115">Instancias de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c81f1-115">Azure container services</span></span><br><span data-ttu-id="c81f1-116">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c81f1-116">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-117">Storage</span><span class="sxs-lookup"><span data-stu-id="c81f1-117">Storage</span></span></td>
    <td><span data-ttu-id="c81f1-118">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="c81f1-118">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="c81f1-119">Cifrado</span><span class="sxs-lookup"><span data-stu-id="c81f1-119">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-120">SQL Database</span><span class="sxs-lookup"><span data-stu-id="c81f1-120">SQL Database</span></span></td>
    <td><span data-ttu-id="c81f1-121">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="c81f1-121">Databases</span></span><br><span data-ttu-id="c81f1-122">Firewalls</span><span class="sxs-lookup"><span data-stu-id="c81f1-122">Firewalls</span></span><br><span data-ttu-id="c81f1-123">Grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="c81f1-123">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-124">Redes</span><span class="sxs-lookup"><span data-stu-id="c81f1-124">Networking</span></span></td>
    <td><span data-ttu-id="c81f1-125">Redes virtuales</span><span class="sxs-lookup"><span data-stu-id="c81f1-125">Virtual networks</span></span><br><span data-ttu-id="c81f1-126">Interfaces de red</span><span class="sxs-lookup"><span data-stu-id="c81f1-126">Network interfaces</span></span><br><span data-ttu-id="c81f1-127">Direcciones IP</span><span class="sxs-lookup"><span data-stu-id="c81f1-127">IP addresses</span></span><br><span data-ttu-id="c81f1-128">Tabla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="c81f1-128">Routing table</span></span><br><span data-ttu-id="c81f1-129">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="c81f1-129">Network security groups</span></span><br><span data-ttu-id="c81f1-130">DNS</span><span class="sxs-lookup"><span data-stu-id="c81f1-130">DNS</span></span><br><span data-ttu-id="c81f1-131">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c81f1-131">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="c81f1-132">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="c81f1-132">Load balancers</span></span><br><span data-ttu-id="c81f1-133">Puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="c81f1-133">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-134">Más servicios</span><span class="sxs-lookup"><span data-stu-id="c81f1-134">More services</span></span></td>
    <td><span data-ttu-id="c81f1-135">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c81f1-135">Resource Manager</span></span><br><span data-ttu-id="c81f1-136">Key Vault</span><span class="sxs-lookup"><span data-stu-id="c81f1-136">Key Vault</span></span><br><span data-ttu-id="c81f1-137">Redis</span><span class="sxs-lookup"><span data-stu-id="c81f1-137">Redis</span></span><br><span data-ttu-id="c81f1-138">CDN</span><span class="sxs-lookup"><span data-stu-id="c81f1-138">CDN</span></span><br><span data-ttu-id="c81f1-139">Batch</span><span class="sxs-lookup"><span data-stu-id="c81f1-139">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="c81f1-140">App Service: Web Apps</span><span class="sxs-lookup"><span data-stu-id="c81f1-140">App service - Web apps</span></span><br><span data-ttu-id="c81f1-141">Functions</span><span class="sxs-lookup"><span data-stu-id="c81f1-141">Functions</span></span><br><span data-ttu-id="c81f1-142">Service Bus</span><span class="sxs-lookup"><span data-stu-id="c81f1-142">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="c81f1-143">Supervisión</span><span class="sxs-lookup"><span data-stu-id="c81f1-143">Monitor</span></span><br><span data-ttu-id="c81f1-144">Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="c81f1-144">Graph RBAC</span></span><br><span data-ttu-id="c81f1-145">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="c81f1-145">DocumentDB</span></span><br><span data-ttu-id="c81f1-146">Scheduler</span><span class="sxs-lookup"><span data-stu-id="c81f1-146">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="c81f1-147">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="c81f1-147">Fundamentals</span></span></td>
    <td><span data-ttu-id="c81f1-148">Autenticación: principal</span><span class="sxs-lookup"><span data-stu-id="c81f1-148">Authentication - core</span></span></td>
    <td><span data-ttu-id="c81f1-149">Métodos asincrónicos</span><span class="sxs-lookup"><span data-stu-id="c81f1-149">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="c81f1-150">Las características de la *versión preliminar* están marcadas en los comentarios de la documentación en las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="c81f1-150">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="c81f1-151">Estas características están sujetas a cambios.</span><span class="sxs-lookup"><span data-stu-id="c81f1-151">These features are subject to change.</span></span> <span data-ttu-id="c81f1-152">Puede que se modifiquen de cualquier manera (o incluso se eliminen) en el futuro.</span><span class="sxs-lookup"><span data-stu-id="c81f1-152">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
