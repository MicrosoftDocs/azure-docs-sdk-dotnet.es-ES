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
ms.openlocfilehash: eb7aa364cae9deea4ed2052eefdbd51c85379afa
ms.sourcegitcommit: 2c08a778353ed743b9e437ed85f2e1dfb21b9427
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2017
---
# <a name="get-started-with-net-for-azure-developers"></a><span data-ttu-id="606a5-104">Introducción a .NET para los desarrolladores de Azure</span><span class="sxs-lookup"><span data-stu-id="606a5-104">Get started with .NET for Azure developers</span></span>

<span data-ttu-id="606a5-105">Este tutorial le guiará a través de la compilación e implementación de una aplicación de Microsoft Azure con Visual Studio y .NET.</span><span class="sxs-lookup"><span data-stu-id="606a5-105">This tutorial will walk you through building and deploying a Microsoft Azure application using Visual Studio and .NET.</span></span>  <span data-ttu-id="606a5-106">Cuando termine, tendrá una aplicación web de tareas pendientes integrada en ASP.NET MVC Core, hospedada como aplicación web de Azure y con Azure CosmosDB para el almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="606a5-106">When finished, you'll have a web-based to-do application built in ASP.NET MVC Core, hosted as an Azure Web App, and using Azure CosmosDB for data storage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="606a5-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="606a5-107">Prerequisites</span></span>

* [<span data-ttu-id="606a5-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="606a5-108">Visual Studio 2017</span></span>](https://www.visualstudio.com/downloads/)
* <span data-ttu-id="606a5-109">Una [suscripción a Microsoft Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="606a5-109">A [Microsoft Azure subscription](https://azure.microsoft.com/free/)</span></span>

## <a name="create-a-cosmosdb-account"></a><span data-ttu-id="606a5-110">Creación de una cuenta de CosmosDB</span><span class="sxs-lookup"><span data-stu-id="606a5-110">Create a CosmosDB account</span></span>

<span data-ttu-id="606a5-111">En este tutorial se utiliza CosmosDB para almacenar los datos, por lo que necesitará crear una cuenta.</span><span class="sxs-lookup"><span data-stu-id="606a5-111">CosmosDB is used for data storage in this tutorial, so you'll need to create an account.</span></span>  <span data-ttu-id="606a5-112">Ejecute este script localmente o en Cloud Shell para crear una cuenta de DocumentDB API en Azure CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="606a5-112">Run this script locally or in the Cloud Shell to create an Azure CosmosDB DocumentDB API account.</span></span>  <span data-ttu-id="606a5-113">Haga clic en el botón **Pruébelo** en el bloque de código siguiente para iniciar [Azure Cloud Shell](/azure/cloud-shell/), y copiar y pegar el bloque de script en el shell.</span><span class="sxs-lookup"><span data-stu-id="606a5-113">Click the **Try it** button on the code block below to launch the [Azure Cloud Shell](/azure/cloud-shell/) and copy/paste the script block into the shell.</span></span>

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

<span data-ttu-id="606a5-114">Tome nota de los valores de **authKey** y **endpoint** que aparecen</span><span class="sxs-lookup"><span data-stu-id="606a5-114">Make a note of the displayed **authKey** and **endpoint**</span></span> 

## <a name="downloading-and-running-the-application"></a><span data-ttu-id="606a5-115">Descarga y ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="606a5-115">Downloading and running the application</span></span>

<span data-ttu-id="606a5-116">Vamos a obtener el código de ejemplo de este tutorial y enlazarlo con su cuenta de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="606a5-116">Let's get the sample code for this walkthrough and hook it up to your CosmosDB account.</span></span>

1. <span data-ttu-id="606a5-117">Descargue el código de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="606a5-117">Download the sample code.</span></span>  <span data-ttu-id="606a5-118">También puede [obtenerlo de GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/) o, si tiene el [cliente de la línea de comandos de git](https://git-scm.com/), clónelo en la máquina local con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="606a5-118">You can [get it from GitHub](https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart/), or if you have the [git command line client](https://git-scm.com/), clone it to your local machine with the following command:</span></span>

    ```cmd
    git clone https://github.com/Azure-Samples/dotnet-cosmosdb-quickstart
    ```

2. <span data-ttu-id="606a5-119">Abra **todo.csproj** en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="606a5-119">Open **todo.csproj** in Visual Studio.</span></span>

3. <span data-ttu-id="606a5-120">Abra **appsettings.json** en el proyecto web.</span><span class="sxs-lookup"><span data-stu-id="606a5-120">Open **appsettings.json** in the web project.</span></span>  <span data-ttu-id="606a5-121">Busque las líneas siguientes:</span><span class="sxs-lookup"><span data-stu-id="606a5-121">Look for the following lines:</span></span>

    ```json
    "authKey": "AUTHKEYVALUE",
    "endpoint": "ENDPOINTVALUE",
    ```
    <span data-ttu-id="606a5-122">Reemplace **AUTHKEYVALUE** y **ENDPOINTVALUE** con los valores que anotó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="606a5-122">Replace **AUTHKEYVALUE** and **ENDPOINTVALUE** with the values you noted earlier.</span></span>

4. <span data-ttu-id="606a5-123">Presione **F5** para restaurar los paquetes de NuGet del proyecto, compile el proyecto y ejecútelo de forma local.</span><span class="sxs-lookup"><span data-stu-id="606a5-123">Press **F5** to restore the project's NuGet packages, build the project, and run it locally.</span></span>

<span data-ttu-id="606a5-124">La aplicación web debe ejecutarse localmente en el explorador.</span><span class="sxs-lookup"><span data-stu-id="606a5-124">The web application should run locally in your browser.</span></span>  <span data-ttu-id="606a5-125">Puede agregar nuevos elementos a la lista de tareas; para ello, haga clic en **Crear nuevo**.</span><span class="sxs-lookup"><span data-stu-id="606a5-125">You can add new items to the to-do list by clicking **Create New**.</span></span>  <span data-ttu-id="606a5-126">Tenga en cuenta que se van a almacenar los datos especificados en la aplicación en la cuenta de CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="606a5-126">Note the data you enter in the application is being stored in your CosmosDB account.</span></span>  <span data-ttu-id="606a5-127">También puede [ver los datos en Azure Portal](/azure/documentdb/documentdb-view-json-document-explorer).</span><span class="sxs-lookup"><span data-stu-id="606a5-127">You can [view your data in the Azure portal](/azure/documentdb/documentdb-view-json-document-explorer).</span></span>

## <a name="deploying-the-application-as-an-azure-web-app"></a><span data-ttu-id="606a5-128">Implementación de la aplicación como aplicación web de Azure</span><span class="sxs-lookup"><span data-stu-id="606a5-128">Deploying the application as an Azure Web App</span></span>

<span data-ttu-id="606a5-129">Ha compilado correctamente una aplicación que utiliza servicios de Azure como DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="606a5-129">You've successfully built an application that uses Azure services like DocumentDB.</span></span>  <span data-ttu-id="606a5-130">A continuación, implementaremos la aplicación web en la nube.</span><span class="sxs-lookup"><span data-stu-id="606a5-130">Next, we'll deploy our web application to the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="606a5-131">Asegúrese de que ha iniciado sesión en Visual Studio con la cuenta asociada a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="606a5-131">Be sure you're signed into Visual Studio with the same account your Azure subscription is associated with.</span></span>

1. <span data-ttu-id="606a5-132">En el Explorador de soluciones de Visual Studio, haga clic con el botón derecho en el nombre del proyecto y seleccione **Publicar...**</span><span class="sxs-lookup"><span data-stu-id="606a5-132">In Visual Studio Solution Explorer, right-click on the project name and select **Publish...**</span></span>

2. <span data-ttu-id="606a5-133">En el cuadro de diálogo Publicar, seleccione **Microsoft Azure App Service**, **Crear nuevo** y haga clic en **Publicar**</span><span class="sxs-lookup"><span data-stu-id="606a5-133">Using the Publish dialog, select **Microsoft Azure App Service**, select **Create New**, and then click **Publish**</span></span>

3. <span data-ttu-id="606a5-134">Rellene el cuadro de diálogo Crear servicio de aplicaciones como sigue:</span><span class="sxs-lookup"><span data-stu-id="606a5-134">Complete the Create App Service dialog as follows:</span></span>

    * <span data-ttu-id="606a5-135">Escriba un **nombre de la aplicación web** único.</span><span class="sxs-lookup"><span data-stu-id="606a5-135">Enter a unique **Web App Name**.</span></span>  <span data-ttu-id="606a5-136">Formará parte de la dirección URL de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="606a5-136">This will be part of the URL for your app.</span></span>
    * <span data-ttu-id="606a5-137">Seleccione la **suscripción** de Azure donde la vaya a implementar.</span><span class="sxs-lookup"><span data-stu-id="606a5-137">Select the Azure **Subscription** you're deploying to.</span></span>  <span data-ttu-id="606a5-138">Use la misma suscripción donde inició sesión en Cloud Shell anteriormente.</span><span class="sxs-lookup"><span data-stu-id="606a5-138">Use same subscription with which you were logged into Cloud Shell earlier.</span></span>
    * <span data-ttu-id="606a5-139">Seleccione *DotNetAzureTutorial* para el **Grupo de recursos** de la aplicación web.</span><span class="sxs-lookup"><span data-stu-id="606a5-139">Select *DotNetAzureTutorial* for the **Resource Group** for your web application.</span></span>
    * <span data-ttu-id="606a5-140">Seleccione o cree un **Plan de App Service** para determinar el precio de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="606a5-140">Select or create an **App Service Plan** to determine the pricing your your application.</span></span>  <span data-ttu-id="606a5-141">Aquí encontrará [más información sobre los Planes de App Service](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="606a5-141">Here's [more information about App Service Plans](/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

4. <span data-ttu-id="606a5-142">Haga clic en **Crear** para implementar la aplicación.</span><span class="sxs-lookup"><span data-stu-id="606a5-142">Click **Create** to deploy the application.</span></span>  <span data-ttu-id="606a5-143">Cuando se completa la implementación, se abre un explorador con la aplicación implementada.</span><span class="sxs-lookup"><span data-stu-id="606a5-143">When deployment is complete, a browser will open with your deployed application.</span></span>

![Aplicación completa](./media/dotnet-quickstart/todo.png)

## <a name="clean-up"></a><span data-ttu-id="606a5-145">Limpieza</span><span class="sxs-lookup"><span data-stu-id="606a5-145">Clean up</span></span>

<span data-ttu-id="606a5-146">Cuando haya terminado de probar la aplicación y examinar el código y los recursos, puede eliminar la aplicación web y la cuenta de CosmosDB; para ello, elimine el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="606a5-146">When you're done testing the app and inspecting the code and resources, you can delete the Web App and CosmosDB account by deleting the resource group.</span></span> <span data-ttu-id="606a5-147">de Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="606a5-147">in the Cloud Shell.</span></span>

```azurecli-interactive
az group delete -n DotNetAzureTutorial
```

## <a name="next-steps"></a><span data-ttu-id="606a5-148">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="606a5-148">Next steps</span></span>

* [<span data-ttu-id="606a5-149">Uso de Azure Active Directory para la autenticación en una aplicación web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="606a5-149">Use Azure Active Directory for authentication in an ASP.NET web application</span></span>](/azure/active-directory/develop/active-directory-devquickstarts-webapp-dotnet)
* [<span data-ttu-id="606a5-150">Compilación de una aplicación web de Azure con Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="606a5-150">Build an Azure Web App using Azure SQL Database</span></span>](/azure/app-service-web/web-sites-dotnet-get-started)
* [<span data-ttu-id="606a5-151">Prueba de una aplicación .NET de ejemplo con Azure Storage</span><span class="sxs-lookup"><span data-stu-id="606a5-151">Try a .NET sample application with Azure Storage</span></span>](/azure/storage/storage-samples-dotnet)


