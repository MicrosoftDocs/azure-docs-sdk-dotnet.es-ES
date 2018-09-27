---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190718"
---
<span data-ttu-id="b82b8-101">Cree un archivo de texto llamado `azureauth.json`.</span><span class="sxs-lookup"><span data-stu-id="b82b8-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="b82b8-102">Pegue la salida JSON de la creación de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="b82b8-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="b82b8-103">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="b82b8-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="b82b8-104">Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="b82b8-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
