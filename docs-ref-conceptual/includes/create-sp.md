La aplicación .NET necesita permisos para leer y crear recursos en la suscripción de Azure para poder usar las bibliotecas de administración de Azure para .NET. Cree a una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales para conceder este acceso. Las entidades de servicio proporcionan una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.

En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash). Compruebe que está usando la suscripción en la que desea crear la entidad de servicio. 

```azurecli-interactive
az account show
```

Se muestra la información de la suscripción.

```json
{
  "environmentName": "AzureCloud",
  "id": "15dbcfa8-4b93-4c9a-881c-6189d39f04d4",
  "isDefault": true,
  "name": "my-subscription",
  "state": "Enabled",
  "tenantId": "43413cc1-5886-4711-9804-8cfea3d1c3ee",
  "user": {
    "cloudShellID": true,
    "name": "jane@contoso.com",
    "type": "user"
  }
}
```

Si no ha iniciado sesión en la suscripción correcta, escriba `az account set -s <name or ID of subscription>` para seleccionar la correcta.

Cree la entidad de servicio con el siguiente comando:

```azurecli-interactive
az ad sp create-for-rbac --sdk-auth
```

La información de la entidad de servicio se muestra con formato JSON.

```json
{
  "clientId": "b52dd125-9272-4b21-9862-0be667bdf6dc",
  "clientSecret": "ebc6e170-72b2-4b6f-9de2-99410964d2d0",
  "subscriptionId": "ffa52f27-be12-4cad-b1ea-c2c241b6cceb",
  "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```

Copie y pegue la salida JSON en un editor de texto para usarla más adelante.
