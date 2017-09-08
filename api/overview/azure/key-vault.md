---
title: Bibliotecas de Azure Key Vault para .NET
description: Referencia de las bibliotecas de Azure Key Vault para .NET
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: douge
ms.date: 07/21/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: dotnet
ms.service: multiple
ms.openlocfilehash: 77a4e710e858bbeb98579a7b540b52b4cb9dd7b0
ms.sourcegitcommit: d95a6ad3774a49b16f652e40e7860e47636c7ad0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/28/2017
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="3fde8-104">Bibliotecas de Azure Key Vault para .NET</span><span class="sxs-lookup"><span data-stu-id="3fde8-104">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="3fde8-105">Información general</span><span class="sxs-lookup"><span data-stu-id="3fde8-105">Overview</span></span>

<span data-ttu-id="3fde8-106">El Almacén de claves de Azure ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="3fde8-106">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="3fde8-107">Consulte los artículos [¿Qué es Azure Key Vault?](/azure/key-vault/key-vault-whatis), [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Uso de Azure Key Vault desde una aplicación web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="3fde8-107">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="3fde8-108">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="3fde8-108">Client library</span></span>

<span data-ttu-id="3fde8-109">Use la biblioteca de cliente para administrar las claves y los recursos relacionados, como certificados y secretos.</span><span class="sxs-lookup"><span data-stu-id="3fde8-109">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="3fde8-110">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3fde8-110">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3fde8-111">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fde8-111">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="3fde8-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3fde8-112">Example</span></span>

<span data-ttu-id="3fde8-113">En el ejemplo siguiente se recupera el secreto de una clave concreta que se identifica en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3fde8-113">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fde8-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="3fde8-114">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="3fde8-115">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="3fde8-115">Management library</span></span>

<span data-ttu-id="3fde8-116">Utilice la biblioteca de administración para crear, eliminar y consultar almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="3fde8-116">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="3fde8-117">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directamente desde la [Consola del Administrador de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="3fde8-117">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="3fde8-118">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3fde8-118">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="3fde8-119">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="3fde8-119">Example</span></span>

<span data-ttu-id="3fde8-120">En el ejemplo siguiente se muestra cómo crear un nuevo almacén de claves para un grupo de recursos y una ubicación dados.</span><span class="sxs-lookup"><span data-stu-id="3fde8-120">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

```csharp
using (KeyVaultManagementClient client = new KeyVaultManagementClient(
    new TokenCloudCredentials(subscriptionId, accessToken)))
{
    client.Vaults.CreateOrUpdate(resourceGroupName, "myKeyVault", new VaultCreateOrUpdateParameters
    {
        Properties = new VaultProperties
        {
            EnabledForDeployment = true,
            EnabledForDiskEncryption = true,
            EnabledForTemplateDeployment = true,
            Location = resourceGroupLocation,
            // SKU level, access policies, tenants, etc.
        }
    });
}
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3fde8-121">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="3fde8-121">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="3fde8-122">Muestras</span><span class="sxs-lookup"><span data-stu-id="3fde8-122">Samples</span></span>

* [<span data-ttu-id="3fde8-123">Descargar los ejemplos de cliente Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="3fde8-123">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* [<span data-ttu-id="3fde8-124">Getting Started with Azure Client Side Encryption in .NET</span><span class="sxs-lookup"><span data-stu-id="3fde8-124">Getting Started with Azure Client Side Encryption in .NET</span></span>](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/) (Introducción al cifrado del lado cliente de Azure en .NET)


<span data-ttu-id="3fde8-125">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3fde8-125">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-add-package
