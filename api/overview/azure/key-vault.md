---
title: Bibliotecas de Azure Key Vault para .NET
description: Referencia de las bibliotecas de Azure Key Vault para .NET
ms.date: 10/19/2017
ms.topic: reference
ms.service: key-vault
ms.openlocfilehash: a42eb9684bcfb8e8d2209235f61bbf6962cf5e9e
ms.sourcegitcommit: 5d9b713653b3d03e1d0a67f6e126ee399d1c2a60
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2018
ms.locfileid: "47190558"
---
# <a name="azure-key-vault-libraries-for-net"></a><span data-ttu-id="a67bf-103">Bibliotecas de Azure Key Vault para .NET</span><span class="sxs-lookup"><span data-stu-id="a67bf-103">Azure Key Vault libraries for .NET</span></span>

## <a name="overview"></a><span data-ttu-id="a67bf-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a67bf-104">Overview</span></span>

<span data-ttu-id="a67bf-105">Azure Key Vault ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="a67bf-105">Azure Key Vault helps safeguard cryptographic keys and secrets used by cloud applications and services.</span></span>

<span data-ttu-id="a67bf-106">Consulte los artículos [¿Qué es Azure Key Vault?](/azure/key-vault/key-vault-whatis), [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Uso de Azure Key Vault desde una aplicación web](/azure/key-vault/key-vault-use-from-web-application).</span><span class="sxs-lookup"><span data-stu-id="a67bf-106">Read more about [What is Key Vault?](/azure/key-vault/key-vault-whatis) then [Get started with Azure Key Vault](/azure/key-vault/key-vault-get-started) or learn how to [Use Key Vault from a web app](/azure/key-vault/key-vault-use-from-web-application).</span></span>

## <a name="client-library"></a><span data-ttu-id="a67bf-107">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="a67bf-107">Client library</span></span>

<span data-ttu-id="a67bf-108">Use la biblioteca de cliente para administrar las claves y los recursos relacionados, como certificados y secretos.</span><span class="sxs-lookup"><span data-stu-id="a67bf-108">Use the client library to manage keys and related assets such as certificates and secrets.</span></span>

<span data-ttu-id="a67bf-109">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a67bf-109">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a67bf-110">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a67bf-110">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a><span data-ttu-id="a67bf-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a67bf-111">Example</span></span>

<span data-ttu-id="a67bf-112">En el ejemplo siguiente se recupera el secreto de una clave concreta que se identifica en la configuración de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a67bf-112">The following example retrieves the secret for a specific key that is identified in the application settings.</span></span>

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a67bf-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="a67bf-113">Explore the client APIs</span></span>](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a><span data-ttu-id="a67bf-114">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="a67bf-114">Management library</span></span>

<span data-ttu-id="a67bf-115">Utilice la biblioteca de administración para crear, eliminar y consultar almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="a67bf-115">Use the management library to create, delete, and query key vaults.</span></span>

<span data-ttu-id="a67bf-116">Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].</span><span class="sxs-lookup"><span data-stu-id="a67bf-116">Install the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directly from the Visual Studio [Package Manager console][PackageManager] or with the [.NET Core CLI][DotNetCLI].</span></span>

#### <a name="visual-studio-package-manager"></a><span data-ttu-id="a67bf-117">Administrador de paquetes de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a67bf-117">Visual Studio Package Manager</span></span>

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a><span data-ttu-id="a67bf-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a67bf-118">Example</span></span>

<span data-ttu-id="a67bf-119">En el ejemplo siguiente se muestra cómo crear un nuevo almacén de claves para un grupo de recursos y una ubicación dados.</span><span class="sxs-lookup"><span data-stu-id="a67bf-119">The following example demonstrates how to create a new key vault for a given resource group and location.</span></span>

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
> [<span data-ttu-id="a67bf-120">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a67bf-120">Explore the management APIs</span></span>](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="a67bf-121">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="a67bf-121">Samples</span></span>

* [<span data-ttu-id="a67bf-122">Descargar los ejemplos de cliente Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a67bf-122">Download the Azure Key Vault client samples</span></span>](https://www.microsoft.com/download/details.aspx?id=45343)
* <span data-ttu-id="a67bf-123">[Getting Started with Azure Client Side Encryption in .NET](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/) (Introducción al cifrado del lado cliente de Azure en .NET)</span><span class="sxs-lookup"><span data-stu-id="a67bf-123">[Getting Started with Azure Client Side Encryption in .NET](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/)</span></span>


<span data-ttu-id="a67bf-124">Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a67bf-124">Explore more [sample .NET code](https://azure.microsoft.com/resources/samples/?platform=dotnet) you can use in your apps.</span></span>

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
