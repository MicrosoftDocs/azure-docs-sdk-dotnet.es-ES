La aplicación .NET necesita permisos para leer y crear recursos en la suscripción de Azure para poder usar las bibliotecas de administración de Azure para .NET. Cree a una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales para conceder este acceso. Las entidades de servicio son una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.

En primer lugar, inicie sesión en Azure PowerShell:

```powershell
Login-AzureRmAccount
```

Anote la información mostrada sobre el inquilino y la suscripción:

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

[Cree una entidad de servicio con PowerShell](/powershell/azure/create-azure-service-principal-azureps), así:

```powershell
# Create the service principal (use a strong password)
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password "password"

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

Asegúrese de anotar el valor de ApplicationId:

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
