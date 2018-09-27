---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 5c8cb328802cfb94e944e4241852fb9568e8507f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190538"
---
<span data-ttu-id="892ac-101">La aplicación .NET necesita permisos para leer y crear recursos en la suscripción de Azure para poder usar las bibliotecas de administración de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="892ac-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="892ac-102">Cree a una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales para conceder este acceso.</span><span class="sxs-lookup"><span data-stu-id="892ac-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="892ac-103">Las entidades de servicio proporcionan una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.</span><span class="sxs-lookup"><span data-stu-id="892ac-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="892ac-104">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="892ac-104">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="892ac-105">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="892ac-105">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="892ac-106">Se muestra la información de la suscripción.</span><span class="sxs-lookup"><span data-stu-id="892ac-106">Your subscription information is displayed.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

<span data-ttu-id="892ac-107">Si no ha iniciado sesión en la suscripción correcta, escriba `az account set -s <name or ID of subscription>` para seleccionar la correcta.</span><span class="sxs-lookup"><span data-stu-id="892ac-107">If you're not logged into the correct subscription, select the correct one by typing `az account set -s <name or ID of subscription>`.</span></span>

<span data-ttu-id="892ac-108">Cree la entidad de servicio con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="892ac-108">Create the service principal with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

<span data-ttu-id="892ac-109">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="892ac-109">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="892ac-110">Copie y pegue la salida JSON en un editor de texto para usarla más adelante.</span><span class="sxs-lookup"><span data-stu-id="892ac-110">Copy and paste the JSON output to a text editor for use later.</span></span>
