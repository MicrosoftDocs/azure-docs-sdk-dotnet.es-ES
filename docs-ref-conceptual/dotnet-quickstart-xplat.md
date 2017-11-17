---
title: .NET para los desarrolladores de Azure
description: .NET para los desarrolladores de Azure
keywords: Azure .NET, SDK, referencia de API de Azure .NET, biblioteca de clases de Azure .NET
author: camsoper
manager: douge
ms.author: casoper
ms.date: 06/20/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.assetid: 
ms.openlocfilehash: 14374182ee0511e942940797465858b94ec08876
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="get-started-with-net-cli-tools-for-azure-developers"></a><span data-ttu-id="0b291-104">Introducción a las herramientas de la CLI para .NET para los desarrolladores de Azure</span><span class="sxs-lookup"><span data-stu-id="0b291-104">Get started with .NET CLI tools for Azure developers</span></span>

<span data-ttu-id="0b291-105">Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con .NET Core.</span><span class="sxs-lookup"><span data-stu-id="0b291-105">This tutorial will walk you through building and deploying a Microsoft Azure application using .NET Core.</span></span>  <span data-ttu-id="0b291-106">Cuando termine, tendrá una aplicación web de tareas pendientes integrada en ASP.NET MVC Core, hospedada como aplicación web de Azure y con Azure CosmosDB para el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="0b291-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b291-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="0b291-107">Prerequisites</span></span>

* <span data-ttu-id="0b291-108">Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0b291-108">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>
* [<span data-ttu-id="0b291-109">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0b291-109">.NET Core</span></span>](https://www.microsoft.com/net/download/core) (opcional)
* [<span data-ttu-id="0b291-110">CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="0b291-110">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2) (opcional)
* <span data-ttu-id="0b291-111">Cliente de línea de comandos [Git](https://www.git-scm.com/) (opcional)</span><span class="sxs-lookup"><span data-stu-id="0b291-111">[Git](https://www.git-scm.com/) command line client (optional)</span></span>

<span data-ttu-id="0b291-112">[Azure Cloud Shell](/azure/cloud-shell/) tiene instalados todos los requisitos previos opcionales para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="0b291-112">The [Azure Cloud Shell](/azure/cloud-shell/) has all of the optional prerequisites for this tutorial preinstalled.</span></span>  <span data-ttu-id="0b291-113">Solo debe instalar los componentes opcionales anteriores si desea ejecutar el tutorial localmente.</span><span class="sxs-lookup"><span data-stu-id="0b291-113">You only need to install the optional components above if you wish to run the tutorial locally.</span></span>  <span data-ttu-id="0b291-114">Para iniciar rápidamente Cloud Shell, simplemente haga clic en el botón **Pruébelo**, en la parte superior derecha de los bloques de código siguientes.</span><span class="sxs-lookup"><span data-stu-id="0b291-114">To quickly launch the Cloud Shell, just click the **Try it** button in the top-right of any of the below code blocks.</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="0b291-115">Creación de una cuenta de CosmosDB</span><span class="sxs-lookup"><span data-stu-id="0b291-115">Create a CosmosDB account</span></span>

<span data-ttu-id="0b291-116">En este tutorial se utiliza CosmosDB para almacenar los datos, por lo que necesitará crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="0b291-116">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="0b291-117">Ejecute este script localmente o en Cloud Shell para crear una cuenta de DocumentDB API en Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="0b291-117">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>

```azurecli-interactive
# Create the DotNetAzureTutorial resource group
az group create --name DotNetAzureTutorial --location EastUS

# Generate a unique name for the account
let randomNum=$RANDOM*$RANDOM
cosmosdbname=dotnettutorial$randomNum

# Create the CosmosDB account
az cosmosdb create --name $cosmosdbname --resource-group DotNetAzureTutorial

# Retrieve the endpoint and key (you'll need these later)
cosmosEndpoint=$(az cosmosdb show -n $cosmosdbname -g DotNetAzureTutorial --query [documentEndpoint] -o tsv)
cosmosAuthKey=$(az cosmosdb list-keys -n $cosmosdbname -g DotNetAzureTutorial --query [primaryMasterKey] -o tsv)

```

## <a name="download-and-configure-the-application"></a><span data-ttu-id="0b291-118">Descarga y configuración de la aplicación</span><span class="sxs-lookup"><span data-stu-id="0b291-118">Download and configure the application</span></span>

<span data-ttu-id="0b291-119">La aplicación que se va a implementar es una [sencilla aplicación de tareas pendientes](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) escrita con ASP.NET MVC Core y las bibliotecas de cliente de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="0b291-119">The application you're going to deploy is a [simple to-do app](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) written using ASP.NET MVC Core using the CosmosDB client libraries.</span></span>  <span data-ttu-id="0b291-120">Ahora, obtenga el código de este tutorial y configúrelo con la información de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="0b291-120">Now you'll get the code for this tutorial and configure it with your CosmosDB information.</span></span>

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
> <span data-ttu-id="0b291-121">Si nunca ha ejecutado `git commit` en este entorno, se le pedirá que establezca su identidad.</span><span class="sxs-lookup"><span data-stu-id="0b291-121">If you've never run `git commit` in this environment before, you may be prompted to set your identity.</span></span> <span data-ttu-id="0b291-122">Siga las instrucciones en pantalla y, a continuación, vuelva a ejecutar el comando `git commit`.</span><span class="sxs-lookup"><span data-stu-id="0b291-122">Follow the on-screen instructions and then re-run the `git commit` command.</span></span>

<span data-ttu-id="0b291-123">Restaure los paquetes de NuGet y compile la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0b291-123">Restore the NuGet packages and build the application.</span></span>

```azurecli-interactive
dotnet restore
dotnet build
```

> [!TIP]
> <span data-ttu-id="0b291-124">Si está usando las herramientas en su propia máquina, ejecute `dotnet run` y vaya a la dirección `localhost` que se indica para probar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="0b291-124">If you are using the tools on your own machine, you can test the application by running `dotnet run` and browsing to the displayed `localhost` address.</span></span>  <span data-ttu-id="0b291-125">No es posible ir a esta dirección en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="0b291-125">You are not able to browse to this address in the Cloud Shell, however.</span></span>  

## <a name="configure-azure-app-service-and-deploy-the-web-app"></a><span data-ttu-id="0b291-126">Configuración de Azure App Service e implementación de la aplicación web</span><span class="sxs-lookup"><span data-stu-id="0b291-126">Configure Azure App Service and deploy the web app</span></span>

<span data-ttu-id="0b291-127">Ha descargado y compilado correctamente la aplicación web y está listo para implementarla como una aplicación web de Azure.</span><span class="sxs-lookup"><span data-stu-id="0b291-127">You've successfully downloaded and built the web application, and you're ready to deploy it as an Azure Web App.</span></span>  <span data-ttu-id="0b291-128">Para empezar, creará el recurso de aplicación web.</span><span class="sxs-lookup"><span data-stu-id="0b291-128">You'll start by creating the Web App resource.</span></span>

```azurecli-interactive
# Generate a unique Web App name
let randomNum=$RANDOM*$RANDOM
webappname=todoApp$randomNum

# Create an App Service plan.
az appservice plan create --name $webappname --resource-group DotNetAzureTutorial --sku FREE

# Create the Web App
az webapp create --name $webappname --resource-group DotNetAzureTutorial --plan $webappname

```

<span data-ttu-id="0b291-129">Antes de implementarla, debe establecer las credenciales de implementación en el nivel de cuenta.</span><span class="sxs-lookup"><span data-stu-id="0b291-129">Before you deploy, you need to set the account-level deployment credentials.</span></span>  <span data-ttu-id="0b291-130">Use el siguiente script y asegúrese de incluir sus propios valores en el nombre de usuario y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="0b291-130">Use the script below, making sure to include your own values for the user name and password.</span></span>

```azurecli-interactive
az webapp deployment user set --user-name <desired user name> --password <desired password>
```

<span data-ttu-id="0b291-131">Por último, implemente la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="0b291-131">Finally, deploy the application to Azure.</span></span>  <span data-ttu-id="0b291-132">Se le pedirá la contraseña que ha creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0b291-132">You will be prompted for the password you created above.</span></span>

```azurecli-interactive
# Get the Git deployment URL
giturl=$(az webapp deployment source config-local-git -n $webappname -g DotNetAzureTutorial --query [url] -o tsv)

# Add the URL as a Git remote repository
git remote add azure $giturl

# Push the local repository to the remote
git push azure master
```

<span data-ttu-id="0b291-133">La aplicación se compilará e implementará de manera remota.</span><span class="sxs-lookup"><span data-stu-id="0b291-133">The application will be built remotely and deployed.</span></span>  <span data-ttu-id="0b291-134">Para probar la aplicación, vaya a `https://<web app name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0b291-134">Test the application by browsing to `https://<web app name>.azurewebsites.net`.</span></span>  <span data-ttu-id="0b291-135">Para mostrar la dirección en la consola, use lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="0b291-135">To display the address in the console, use the following:</span></span>

```azurecli-interactive
az webapp show -n $webappname -g DotNetAzureTutorial --query defaultHostName -o tsv
```

<span data-ttu-id="0b291-136">Puede agregar nuevos elementos a la lista de tareas; para ello, haga clic en **Create new** (Crear nuevo).</span><span class="sxs-lookup"><span data-stu-id="0b291-136">You can add new items to the to-do list by clicking **Create New**.</span></span>

![Aplicación completa](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="0b291-138">Limpieza</span><span class="sxs-lookup"><span data-stu-id="0b291-138">Clean up</span></span>

<span data-ttu-id="0b291-139">Cuando haya terminado de probar la aplicación y examinar el código y los recursos, puede eliminar la aplicación web y la cuenta de CosmosDB; para ello, elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b291-139">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="0b291-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0b291-140">Next steps</span></span>

* [<span data-ttu-id="0b291-141">Uso de Azure Active Directory para la autenticación en una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0b291-141">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="0b291-142">Compilación de una aplicación web de Azure con Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0b291-142">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="0b291-143">Prueba de una aplicación .NET de ejemplo con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0b291-143">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


