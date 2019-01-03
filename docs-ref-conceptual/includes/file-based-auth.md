---
ms.service: multiple
ms.date: 9/20/2018
ms.topic: include
ms.openlocfilehash: 7f7c24957d2bc0574fc0b1bf2a8ae8fe8b4dfc64
ms.sourcegitcommit: e25b6ac74033f3b0a7610bf66feb654acb43054c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53430539"
---
Cree un archivo de texto llamado `azureauth.json`. Pegue la salida JSON de la creación de la entidad de servicio.

Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo. Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
