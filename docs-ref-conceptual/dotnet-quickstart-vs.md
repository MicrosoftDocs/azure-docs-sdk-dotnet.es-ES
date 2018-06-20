---
title: Implementación en Azure desde Visual Studio
description: Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con Visual Studio y .NET.
keywords: Azure .NET, SDK, referencia de API de Azure .NET, biblioteca de clases de Azure .NET
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.openlocfilehash: 87f65d8b8b1b1a5184b9d71770c08be472c7e498
ms.sourcegitcommit: e1a0e91988bb849c75e9583a80e3e6d712083785
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2018
ms.locfileid: "31005892"
---
# <a name="deploy-to-azure-from-visual-studio"></a>Implementación en Azure desde Visual Studio

Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con Visual Studio y .NET.  Cuando termine, tendrá una aplicación web de tareas pendientes integrada en ASP.NET MVC Core, hospedada como aplicación web de Azure y que usa Azure Cosmos DB para el almacenamiento de datos.

## <a name="prerequisites"></a>requisitos previos

* [Visual Studio 2017](https://www.visualstudio.com/downloads/)
* Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/).

## <a name="create-an-azure-cosmos-db-account"></a>Creación de una cuenta de Azure Cosmos DB

En este tutorial se utiliza Azure Cosmos DB para almacenar los datos, por lo que necesitará crear una cuenta.  Ejecute este script localmente o en Cloud Shell para crear una cuenta de SQL API en Azure Cosmos DB.  Haga clic en el botón **Pruébelo** en el bloque de código siguiente para iniciar [Azure Cloud Shell](/azure/cloud-shell/), y copiar y pegar el bloque de script en el shell.

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the Azure Cosmos DB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

Tome nota de los valores de **authKey** y **endpoint** que aparecen 

## <a name="downloading-and-running-the-application"></a>Descarga y ejecución de la aplicación

Vamos a obtener el código de ejemplo de este tutorial y a enlazarlo con su cuenta de Azure Cosmos DB.

1. Descargue el código de ejemplo.  También puede [obtenerlo de GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) o, si tiene el [cliente de la línea de comandos de git](https://git-scm.com/), clónelo en la máquina local con el siguiente comando:

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. Abra **todo.csproj** en Visual Studio.

3. Abra **appsettings.json** en el proyecto web.  Busque las líneas siguientes:

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    Reemplace **AUTHKEYVALUE** y **ENDPOINTVALUE** con los valores que anotó anteriormente.

4. Presione **F5** para restaurar los paquetes de NuGet del proyecto, compile el proyecto y ejecútelo de forma local.

La aplicación web debe ejecutarse localmente en el explorador.  Puede agregar nuevos elementos a la lista de tareas; para ello, haga clic en **Create new** (Crear nuevo).  Tenga en cuenta que los datos que especifique en la aplicación se van a almacenar en la cuenta de Azure Cosmos DB.  Para ver los datos en [Azure Portal](https://portal.azure.com), seleccione Azure Cosmos DB en el menú de la izquierda, seleccione la cuenta y, a continuación, seleccione **Explorador de datos**.

## <a name="deploying-the-application-as-an-azure-web-app"></a>Implementación de la aplicación como aplicación web de Azure

Ha creado correctamente una aplicación que utiliza servicios de Azure como Azure Cosmos DB.  A continuación, implementaremos la aplicación web en la nube.

> [!IMPORTANT]
> Asegúrese de que ha iniciado sesión en Visual Studio con la cuenta asociada a la suscripción de Azure.

1. En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el nombre del proyecto y seleccione **Publicar...**

2. En el cuadro de diálogo Publicar, seleccione **Microsoft Azure App Service**, **Crear nuevo** y haga clic en **Publicar**

3. Rellene el cuadro de diálogo Crear servicio de aplicaciones como sigue:

    * Escriba un **nombre de la aplicación web** único.  Formará parte de la dirección URL de la aplicación.
    * Seleccione la **suscripción** de Azure donde la vaya a implementar.  Use la misma suscripción donde inició sesión en Cloud Shell anteriormente.
    * Seleccione *DotNetAzureTutorial* para el **Grupo de recursos** de la aplicación web.
    * Seleccione o cree un **Plan de App Service** para determinar el precio de la aplicación.  Aquí encontrará [más información sobre los Planes de App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).

4. Haga clic en **Crear** para implementar la aplicación.  Cuando se completa la implementación, se abre un explorador con la aplicación implementada.

![Aplicación completa](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Limpieza

Cuando haya terminado de probar la aplicación y examinar el código y los recursos, puede eliminar la aplicación web y la cuenta de Azure Cosmos DB; para ello, elimine el grupo de recursos en Cloud Shell.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>Pasos siguientes

* [Uso de Azure Active Directory para la autenticación en una aplicación web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Compilación de una aplicación web de Azure con Azure SQL Database](/azure/app-service-web/web-sites-dotnet-get-started)
* [Prueba de una aplicación .NET de ejemplo con Azure Storage](/azure/storage/storage-samples-dotnet)


