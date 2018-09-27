---
title: Implementación en Azure desde la línea de comandos con .NET Core
description: En este artículo se describe cómo implementar una aplicación de ASP.NET Core en Azure App Service mediante herramientas de la línea de comandos.
ms.date: 06/20/2017
ms.openlocfilehash: a29f5474dcfedc6f8d044f09ad4d54c5be6a371f
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190498"
---
# <a name="deploy-to-azure-from-the-command-line-with-net-core"></a>Implementación en Azure desde la línea de comandos con .NET Core

Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con .NET Core.  Cuando termine, tendrá una aplicación web de tareas pendientes integrada en ASP.NET MVC Core, hospedada como aplicación web de Azure y que usa Azure Cosmos DB para el almacenamiento de datos.

## <a name="prerequisites"></a>Requisitos previos

* Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/).
* [.NET Core](https://www.microsoft.com/net/download/core) (opcional)
* [CLI de Azure 2.0](/cli/azure/install-az-cli2) (opcional)
* Cliente de línea de comandos [Git](https://www.git-scm.com/) (opcional)

[Azure Cloud Shell](/azure/cloud-shell/) tiene instalados todos los requisitos previos opcionales para este tutorial.  Solo debe instalar los componentes opcionales anteriores si desea ejecutar el tutorial localmente.  Para iniciar rápidamente Cloud Shell, simplemente haga clic en el botón **Pruébelo**, en la parte superior derecha de los bloques de código siguientes.

## <a name="create-an-azure-cosmos-db-account"></a>Creación de una cuenta de Azure Cosmos DB

En este tutorial se utiliza Azure Cosmos DB para almacenar los datos, por lo que necesitará crear una cuenta.  Ejecute este script localmente o en Cloud Shell para crear una cuenta de SQL API en Azure Cosmos DB.

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

```

## <a name="download-and-configure-the-application"></a>Descarga y configuración de la aplicación

La aplicación que se va a implementar es una [sencilla aplicación de tareas pendientes](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) escrita con ASP.NET MVC Core y las bibliotecas de cliente de Azure Cosmos DB.  Ahora, obtenga el código de este tutorial y configúrelo con la información de Azure Cosmos DB.

```azurecli-interactive
# Get the code from GitHub
git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart

# Change the working directory
cd dotnet-cosmosdb-quickstart

# Replace authKey and endpoint values in appsettings.json
sed -i "s|AUTHKEYVALUE|$cosmosAuthKey|g" appsettings.json
sed -i "s|ENDPOINTVALUE|$cosmosEndpoint|g" appsettings.json

# Now commit your changes to the local Git repository.
git commit -a -m "Modified settings"

```

> [!NOTE]
> Si nunca ha ejecutado `git commit` en este entorno, se le pedirá que establezca su identidad. Siga las instrucciones en pantalla y, a continuación, vuelva a ejecutar el comando `git commit`.

Restaure los paquetes de NuGet y compile la aplicación.

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> Si está usando las herramientas en su propia máquina, ejecute `dotnet run` y vaya a la dirección `localhost` que se indica para probar la aplicación.  No es posible ir a esta dirección en Cloud Shell.  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a>Configuración de Azure App Service e implementación de la aplicación web

Ha descargado y compilado correctamente la aplicación web y está listo para implementarla como una aplicación web de Azure.  Para empezar, creará el recurso de aplicación web.

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

Antes de implementarla, debe establecer las credenciales de implementación en el nivel de cuenta.  Use el siguiente script y asegúrese de incluir sus propios valores en el nombre de usuario y la contraseña.

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

Por último, implemente la aplicación en Azure.  Se le pedirá la contraseña que ha creado anteriormente.

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

La aplicación se compilará e implementará de manera remota.  Para probar la aplicación, vaya a `https://<web app name>.azurewebsites.net`.  Para mostrar la dirección en la consola, use lo siguiente:

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

Puede agregar nuevos elementos a la lista de tareas; para ello, haga clic en **Create new** (Crear nuevo).

![Aplicación completa](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a>Limpieza

Cuando haya terminado de probar la aplicación y examinar el código y los recursos, puede eliminar la aplicación web y la cuenta de Azure Cosmos DB; para ello, elimine el grupo de recursos.

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a>Pasos siguientes

* [Uso de Azure Active Directory para la autenticación en una aplicación web ASP.NET](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [Compilación de una aplicación web de Azure con Azure SQL Database](/azure/app-service-web/web-sites-dotnet-get-started)
* [Prueba de una aplicación .NET de ejemplo con Azure Storage](/azure/storage/storage-samples-dotnet)


