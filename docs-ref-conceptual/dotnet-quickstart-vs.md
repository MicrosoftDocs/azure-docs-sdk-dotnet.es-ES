---
title: "Implementación en Azure desde Visual Studio"
description: "Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con Visual Studio y .NET."
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
ms.openlocfilehash: 0f8e3e5ea1ef5cde239b2d8ebbc9fe75dd978cb1
ms.sourcegitcommit: c630918c9e17f5e3c6d4f28fe740c041f60b1e66
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/03/2017
---
# <a name="deploy-to-azure-from-visual-studio"></a><span data-ttu-id="5ff8a-104">Implementación en Azure desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5ff8a-104">Deploy to Azure from Visual Studio</span></span>

<span data-ttu-id="5ff8a-105">Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con Visual Studio y .NET.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-105">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="5ff8a-106">Cuando termine, tendrá una aplicación web de tareas pendientes integrada en ASP.NET MVC Core, hospedada como aplicación web de Azure y con Azure CosmosDB para el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ff8a-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="5ff8a-107">Prerequisites</span></span>

* [<span data-ttu-id="5ff8a-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="5ff8a-108">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="5ff8a-109">Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5ff8a-109">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="5ff8a-110">Creación de una cuenta de CosmosDB</span><span class="sxs-lookup"><span data-stu-id="5ff8a-110">Create a CosmosDB account</span></span>

<span data-ttu-id="5ff8a-111">En este tutorial se utiliza CosmosDB para almacenar los datos, por lo que necesitará crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-111">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="5ff8a-112">Ejecute este script localmente o en Cloud Shell para crear una cuenta de DocumentDB API en Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-112">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>  <span data-ttu-id="5ff8a-113">Haga clic en el botón **Pruébelo** en el bloque de código siguiente para iniciar [Azure Cloud Shell](/azure/cloud-shell/), y copiar y pegar el bloque de script en el shell.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-113">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

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
printf "\n\nauthKey: $cosmosAuthKey\nendpoint: $cosmosEndpoint\n\n"

# Done!

```

<span data-ttu-id="5ff8a-114">Tome nota de los valores de **authKey** y **endpoint** que aparecen</span><span class="sxs-lookup"><span data-stu-id="5ff8a-114">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="5ff8a-115">Descarga y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="5ff8a-115">Downloading and running the application</span></span>

<span data-ttu-id="5ff8a-116">Vamos a obtener el código de ejemplo de este tutorial y enlazarlo con su cuenta de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-116">Let's get the sample code for this walkthrough and hook it up to your CosmosDB account.</span></span>

1. <span data-ttu-id="5ff8a-117">Descargue el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-117">Download the sample code.</span></span>  <span data-ttu-id="5ff8a-118">También puede [obtenerlo de GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) o, si tiene el [cliente de la línea de comandos de git](https://git-scm.com/), clónelo en la máquina local con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="5ff8a-118">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="5ff8a-119">Abra **todo.csproj** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-119">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="5ff8a-120">Abra **appsettings.json** en el proyecto web.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-120">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="5ff8a-121">Busque las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="5ff8a-121">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="5ff8a-122">Reemplace **AUTHKEYVALUE** y **ENDPOINTVALUE** con los valores que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-122">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="5ff8a-123">Presione **F5** para restaurar los paquetes de NuGet del proyecto, compile el proyecto y ejecútelo de forma local.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-123">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="5ff8a-124">La aplicación web debe ejecutarse localmente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-124">The web application should run locally in your browser.</span></span>  <span data-ttu-id="5ff8a-125">Puede agregar nuevos elementos a la lista de tareas; para ello, haga clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-125">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="5ff8a-126">Tenga en cuenta que se van a almacenar los datos especificados en la aplicación en la cuenta de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-126">Note the data you enter in the application is being stored in your CosmosDB account.</span></span>  <span data-ttu-id="5ff8a-127">También puede [ver los datos en Azure Portal](/azure/documentdb/documentdb-view-json-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="5ff8a-127">You can [view your data in the Azure portal](/azure/documentdb/documentdb-view-json-document-explorer).</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="5ff8a-128">Implementación de la aplicación como aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="5ff8a-128">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="5ff8a-129">Ha compilado correctamente una aplicación que utiliza servicios de Azure como DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-129">You've successfully built an application that uses Azure services like DocumentDB.</span></span>  <span data-ttu-id="5ff8a-130">A continuación, implementaremos la aplicación web en la nube.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-130">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ff8a-131">Asegúrese de que ha iniciado sesión en Visual Studio con la cuenta asociada a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-131">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="5ff8a-132">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el nombre del proyecto y seleccione **Publicar...**</span><span class="sxs-lookup"><span data-stu-id="5ff8a-132">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="5ff8a-133">En el cuadro de diálogo Publicar, seleccione **Microsoft Azure App Service**, **Crear nuevo** y haga clic en **Publicar**</span><span class="sxs-lookup"><span data-stu-id="5ff8a-133">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="5ff8a-134">Rellene el cuadro de diálogo Crear servicio de aplicaciones como sigue:</span><span class="sxs-lookup"><span data-stu-id="5ff8a-134">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="5ff8a-135">Escriba un **nombre de la aplicación web** único.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-135">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="5ff8a-136">Formará parte de la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-136">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="5ff8a-137">Seleccione la **suscripción** de Azure donde la vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-137">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="5ff8a-138">Use la misma suscripción donde inició sesión en Cloud Shell anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-138">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="5ff8a-139">Seleccione *DotNetAzureTutorial* para el **Grupo de recursos** de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-139">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="5ff8a-140">Seleccione o cree un **Plan de App Service** para determinar el precio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-140">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="5ff8a-141">Aquí encontrará [más información sobre los Planes de App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="5ff8a-141">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="5ff8a-142">Haga clic en **Crear** para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-142">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="5ff8a-143">Cuando se completa la implementación, se abre un explorador con la aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-143">When deployment is complete, a browser will open with your deployed application.</span></span>

![Aplicación completa](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="5ff8a-145">Limpieza</span><span class="sxs-lookup"><span data-stu-id="5ff8a-145">Clean up</span></span>

<span data-ttu-id="5ff8a-146">Cuando haya terminado de probar la aplicación y examinar el código y los recursos, puede eliminar la aplicación web y la cuenta de CosmosDB; para ello, elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-146">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span> <span data-ttu-id="5ff8a-147">de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="5ff8a-147">in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="5ff8a-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ff8a-148">Next steps</span></span>

* [<span data-ttu-id="5ff8a-149">Uso de Azure Active Directory para la autenticación en una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="5ff8a-149">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="5ff8a-150">Compilación de una aplicación web de Azure con Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="5ff8a-150">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="5ff8a-151">Prueba de una aplicación .NET de ejemplo con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ff8a-151">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


