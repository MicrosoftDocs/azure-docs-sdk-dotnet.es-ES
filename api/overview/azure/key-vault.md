---
title: Bibliotecas de Azure Key Vault para .NET
description: Referencia de las bibliotecas de Azure Key Vault para .NET
keywords: Azure, .NET, SDK, API, Key Vault
author: camsoper
ms.author: casoper
manager: wpickett
ms.date: 10/19/2017
ms.topic: reference
ms.devlang: dotnet
ms.service: key-vault
ms.custom: devcenter, svc-overview
ms.openlocfilehash: 037b80f60616a37665eddb0b7b212d15180700ba
ms.sourcegitcommit: bfa1898c97798991215d08ce89dea87efff44157
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37065455"
---
# <a name="azure-key-vault-libraries-for-net"></a>Bibliotecas de Azure Key Vault para .NET

## <a name="overview"></a>Información general

Azure Key Vault ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.

Consulte los artículos [¿Qué es Azure Key Vault?](/azure/key-vault/key-vault-whatis), [Introducción a Azure Key Vault](/azure/key-vault/key-vault-get-started) o [Uso de Azure Key Vault desde una aplicación web](/azure/key-vault/key-vault-use-from-web-application).

## <a name="client-library"></a>Biblioteca de cliente

Use la biblioteca de cliente para administrar las claves y los recursos relacionados, como certificados y secretos.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.KeyVault) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.KeyVault
```

```bash
dotnet add package Microsoft.Azure.KeyVault
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se recupera el secreto de una clave concreta que se identifica en la configuración de la aplicación.

```csharp
KeyVaultClient kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(securityToken));

SecretBundle sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

// sec.Value holds the secret
```

> [!div class="nextstepaction"]
> [Explorar las API de cliente](/dotnet/api/overview/azure/keyvault/client)

## <a name="management-library"></a>Biblioteca de administración

Utilice la biblioteca de administración para crear, eliminar y consultar almacenes de claves.

Instale el [paquete NuGet](https://www.nuget.org/packages/Microsoft.Azure.Management.KeyVault.Fluent) directamente desde la [Consola del Administración de paquetes][PackageManager] de Visual Studio o con la [CLI de .NET Core][DotNetCLI].

#### <a name="visual-studio-package-manager"></a>Administrador de paquetes de Visual Studio

```powershell
Install-Package Microsoft.Azure.Management.KeyVault.Fluent
```

```bash
dotnet add package Microsoft.Azure.Management.KeyVault.Fluent
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo crear un nuevo almacén de claves para un grupo de recursos y una ubicación dados.

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
> [Explorar las API de administración](/dotnet/api/overview/azure/keyvault/management)

## <a name="samples"></a>Ejemplos

* [Descargar los ejemplos de cliente Azure Key Vault](https://www.microsoft.com/download/details.aspx?id=45343)
* [Getting Started with Azure Client Side Encryption in .NET](https://azure.microsoft.com/resources/samples/storage-dotnet-client-side-encryption/) (Introducción al cifrado del lado cliente de Azure en .NET)


Explore más [código de .NET de ejemplo](https://azure.microsoft.com/resources/samples/?platform=dotnet) que puede usar en sus aplicaciones.

[PackageManager]: https://docs.microsoft.com/nuget/tools/package-manager-console
[DotNetCLI]: https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package
