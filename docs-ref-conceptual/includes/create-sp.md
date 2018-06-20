<span data-ttu-id="494f4-101">La aplicación .NET necesita permisos para leer y crear recursos en la suscripción de Azure para poder usar las bibliotecas de administración de Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="494f4-101">Your .NET application needs permissions to read and create resources in your Azure subscription in order to use the Azure Management Libraries for .NET.</span></span> <span data-ttu-id="494f4-102">Cree a una entidad de servicio y configure la aplicación para que se ejecute con sus credenciales para conceder este acceso.</span><span class="sxs-lookup"><span data-stu-id="494f4-102">Create a service principal and configure your app to run with its credentials to grant this access.</span></span> <span data-ttu-id="494f4-103">Las entidades de servicio son una manera de crear una cuenta no interactiva asociada con su identidad a la que conceder únicamente los privilegios que la aplicación necesita para la ejecución.</span><span class="sxs-lookup"><span data-stu-id="494f4-103">Service principals provide a way to create a non-interactive account associated with your identity to which you grant only the privileges your app needs to run.</span></span>

<span data-ttu-id="494f4-104">En primer lugar, inicie sesión en Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="494f4-104">First, login to Azure PowerShell:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="494f4-105">Anote la información mostrada sobre el inquilino y la suscripción:</span><span class="sxs-lookup"><span data-stu-id="494f4-105">Note the information displayed about your tenant and subscription:</span></span>

```plaintext
Environment           : AzureCloud
Account               : jane@contoso.com
TenantId              : 43413cc1-5886-4711-9804-8cfea3d1c3ee
SubscriptionId        : 15dbcfa8-4b93-4c9a-881c-6189d39f04d4
SubscriptionName      : my-subscription
CurrentStorageAccount : 
```

<span data-ttu-id="494f4-106">[Cree una entidad de servicio con PowerShell](/powershell/azure/create-azure-service-principal-azureps), así:</span><span class="sxs-lookup"><span data-stu-id="494f4-106">[Create a service principal using PowerShell](/powershell/azure/create-azure-service-principal-azureps), like this:</span></span>

```powershell
# Create the service principal (use a strong password)
$sp = New-AzureRmADServicePrincipal -DisplayName "AzureDotNetTest" -Password "password"

# Give it the permissions it needs...
New-AzureRmRoleAssignment -ServicePrincipalName $sp.ApplicationId -RoleDefinitionName Contributor

# Display the Application ID, because we'll need it later.
$sp | Select DisplayName, ApplicationId
```

<span data-ttu-id="494f4-107">Asegúrese de anotar el valor de ApplicationId:</span><span class="sxs-lookup"><span data-stu-id="494f4-107">Make sure to note the ApplicationId:</span></span>

```plaintext
DisplayName     ApplicationId
-----------     -------------
AzureDotNetTest a2ab11af-01aa-4759-8345-7803287dbd39
```
