---
title: "Notas de la versión de las bibliotecas de administración de Azure para .NET | Microsoft Docs"
description: "Vea cuáles son las novedades y cambios importantes en las bibliotecas de administración de Azure para .NET."
keywords: Azure, .NET, API, referencia, notas, actualizaciones, en desuso
author: camsoper
ms.author: casoper
manager: douge
ms.assetid: 
ms.service: Azure
ms.devlang: dotnet
ms.topic: reference
ms.technology: Azure
ms.date: 06/20/2017
ms.openlocfilehash: b4a66eb2860673f63a0d11c3cf31486337f36131
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="release-notes"></a><span data-ttu-id="cc1b4-104">Notas de la versión</span><span class="sxs-lookup"><span data-stu-id="cc1b4-104">Release Notes</span></span> 

## <a name="feature-availability-and-road-map-as-of-version-100"></a><span data-ttu-id="cc1b4-105">Disponibilidad de características y hoja de ruta a partir de la versión 1.0.0</span><span class="sxs-lookup"><span data-stu-id="cc1b4-105">Feature Availability and Road Map as of Version 1.0.0</span></span> ##
### <a name="april-26-2017"></a><span data-ttu-id="cc1b4-106">26 de abril de 2017</span><span class="sxs-lookup"><span data-stu-id="cc1b4-106">April 26, 2017</span></span>

<table>
  <tr>
    <th align="left"><span data-ttu-id="cc1b4-107">Servicio | característica</span><span class="sxs-lookup"><span data-stu-id="cc1b4-107">Service | feature</span></span></th>
    <th align="left"><span data-ttu-id="cc1b4-108">Disponible como GA</span><span class="sxs-lookup"><span data-stu-id="cc1b4-108">Available as GA</span></span></th>
    <th align="left"><span data-ttu-id="cc1b4-109">Disponible como versión preliminar</span><span class="sxs-lookup"><span data-stu-id="cc1b4-109">Available as Preview</span></span></th>
    <th align="left"><span data-ttu-id="cc1b4-110">Próximamente</span><span class="sxs-lookup"><span data-stu-id="cc1b4-110">Coming soon</span></span></th>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-111">Proceso</span><span class="sxs-lookup"><span data-stu-id="cc1b4-111">Compute</span></span></td>
    <td><span data-ttu-id="cc1b4-112">Máquinas virtuales y extensiones de estas</span><span class="sxs-lookup"><span data-stu-id="cc1b4-112">Virtual machines and VM extensions</span></span><br><span data-ttu-id="cc1b4-113">Conjuntos de escalado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="cc1b4-113">Virtual machine scale sets</span></span><br><span data-ttu-id="cc1b4-114">Discos administrados</span><span class="sxs-lookup"><span data-stu-id="cc1b4-114">Managed disks</span></span></td>
    <td></td>
    <td valign="top"><span data-ttu-id="cc1b4-115">Instancias de Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="cc1b4-115">Azure container services</span></span><br><span data-ttu-id="cc1b4-116">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="cc1b4-116">Azure container registry</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-117">Storage</span><span class="sxs-lookup"><span data-stu-id="cc1b4-117">Storage</span></span></td>
    <td><span data-ttu-id="cc1b4-118">Cuentas de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="cc1b4-118">Storage accounts</span></span></td>
    <td></td>
    <td><span data-ttu-id="cc1b4-119">Cifrado</span><span class="sxs-lookup"><span data-stu-id="cc1b4-119">Encryption</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-120">SQL Database</span><span class="sxs-lookup"><span data-stu-id="cc1b4-120">SQL Database</span></span></td>
    <td><span data-ttu-id="cc1b4-121">Bases de datos</span><span class="sxs-lookup"><span data-stu-id="cc1b4-121">Databases</span></span><br><span data-ttu-id="cc1b4-122">Firewalls</span><span class="sxs-lookup"><span data-stu-id="cc1b4-122">Firewalls</span></span><br><span data-ttu-id="cc1b4-123">Grupos elásticos</span><span class="sxs-lookup"><span data-stu-id="cc1b4-123">Elastic pools</span></span></td>
    <td></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-124">Redes</span><span class="sxs-lookup"><span data-stu-id="cc1b4-124">Networking</span></span></td>
    <td><span data-ttu-id="cc1b4-125">Redes virtuales</span><span class="sxs-lookup"><span data-stu-id="cc1b4-125">Virtual networks</span></span><br><span data-ttu-id="cc1b4-126">Interfaces de red</span><span class="sxs-lookup"><span data-stu-id="cc1b4-126">Network interfaces</span></span><br><span data-ttu-id="cc1b4-127">Direcciones IP</span><span class="sxs-lookup"><span data-stu-id="cc1b4-127">IP addresses</span></span><br><span data-ttu-id="cc1b4-128">Tabla de enrutamiento</span><span class="sxs-lookup"><span data-stu-id="cc1b4-128">Routing table</span></span><br><span data-ttu-id="cc1b4-129">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="cc1b4-129">Network security groups</span></span><br><span data-ttu-id="cc1b4-130">DNS</span><span class="sxs-lookup"><span data-stu-id="cc1b4-130">DNS</span></span><br><span data-ttu-id="cc1b4-131">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="cc1b4-131">Traffic managers</span></span></td>
    <td valign="top"><span data-ttu-id="cc1b4-132">Equilibradores de carga</span><span class="sxs-lookup"><span data-stu-id="cc1b4-132">Load balancers</span></span><br><span data-ttu-id="cc1b4-133">Puertas de enlace de aplicaciones</span><span class="sxs-lookup"><span data-stu-id="cc1b4-133">Application gateways</span></span></td>
    <td valign="top"></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-134">Más servicios</span><span class="sxs-lookup"><span data-stu-id="cc1b4-134">More services</span></span></td>
    <td><span data-ttu-id="cc1b4-135">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cc1b4-135">Resource Manager</span></span><br><span data-ttu-id="cc1b4-136">Key Vault</span><span class="sxs-lookup"><span data-stu-id="cc1b4-136">Key Vault</span></span><br><span data-ttu-id="cc1b4-137">Redis</span><span class="sxs-lookup"><span data-stu-id="cc1b4-137">Redis</span></span><br><span data-ttu-id="cc1b4-138">CDN</span><span class="sxs-lookup"><span data-stu-id="cc1b4-138">CDN</span></span><br><span data-ttu-id="cc1b4-139">Batch</span><span class="sxs-lookup"><span data-stu-id="cc1b4-139">Batch</span></span></td>
    <td valign="top"><span data-ttu-id="cc1b4-140">App Service: Web Apps</span><span class="sxs-lookup"><span data-stu-id="cc1b4-140">App service - Web apps</span></span><br><span data-ttu-id="cc1b4-141">Functions</span><span class="sxs-lookup"><span data-stu-id="cc1b4-141">Functions</span></span><br><span data-ttu-id="cc1b4-142">Service Bus</span><span class="sxs-lookup"><span data-stu-id="cc1b4-142">Service bus</span></span></td>
    <td valign="top"><span data-ttu-id="cc1b4-143">Supervisión</span><span class="sxs-lookup"><span data-stu-id="cc1b4-143">Monitor</span></span><br><span data-ttu-id="cc1b4-144">Graph RBAC</span><span class="sxs-lookup"><span data-stu-id="cc1b4-144">Graph RBAC</span></span><br><span data-ttu-id="cc1b4-145">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cc1b4-145">DocumentDB</span></span><br><span data-ttu-id="cc1b4-146">Scheduler</span><span class="sxs-lookup"><span data-stu-id="cc1b4-146">Scheduler</span></span></td>
  </tr>
  <tr>
    <td><span data-ttu-id="cc1b4-147">Aspectos básicos</span><span class="sxs-lookup"><span data-stu-id="cc1b4-147">Fundamentals</span></span></td>
    <td><span data-ttu-id="cc1b4-148">Autenticación: principal</span><span class="sxs-lookup"><span data-stu-id="cc1b4-148">Authentication - core</span></span></td>
    <td><span data-ttu-id="cc1b4-149">Métodos asincrónicos</span><span class="sxs-lookup"><span data-stu-id="cc1b4-149">Async methods</span></span></td>
    <td valign="top"></td>
  </tr>
</table>

> [!WARNING] 
> <span data-ttu-id="cc1b4-150">Las características de la *versión preliminar* están marcadas en los comentarios de la documentación en las bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="cc1b4-150">*Preview* features are flagged in documentation comments in libraries.</span></span> <span data-ttu-id="cc1b4-151">Estas características están sujetas a cambios.</span><span class="sxs-lookup"><span data-stu-id="cc1b4-151">These features are subject to change.</span></span> <span data-ttu-id="cc1b4-152">Puede que se modifiquen de cualquier manera (o incluso se eliminen) en el futuro.</span><span class="sxs-lookup"><span data-stu-id="cc1b4-152">They can be modified in any way (or even removed) in the future.</span></span>

[!include[Contribute and community](includes/contribute.md)]
