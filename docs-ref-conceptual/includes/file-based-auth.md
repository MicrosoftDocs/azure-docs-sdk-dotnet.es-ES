<span data-ttu-id="1e6db-101">Cree un archivo de texto denominado `azureauth.properties` con las credenciales de la entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="1e6db-101">Create a text file named `azureauth.properties` using the service principal credentials:</span></span>

```plaintext
# sample management library properties file
subscription=15dbcfa8-4b93-4c9a-881c-6189d39f04d4
client=a2ab11af-01aa-4759-8345-7803287dbd39
key=password
tenant=43413cc1-5886-4711-9804-8cfea3d1c3ee
managementURI=https://management.core.windows.net/
baseURL=https://management.azure.com/
authURL=https://login.windows.net/
graphURL=https://graph.windows.net/
```

- <span data-ttu-id="1e6db-102">suscripción: use el valor de *SubscriptionId* de cuando ejecutó `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="1e6db-102">subscription: use the *SubscriptionId* value from when you ran `Login-AzureRmAccount`.</span></span>
- <span data-ttu-id="1e6db-103">cliente: use el valor de *ApplicationId* de la salida de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="1e6db-103">client: use the *ApplicationId* value from the service principal output.</span></span>
- <span data-ttu-id="1e6db-104">clave: use el parámetro *-Password* asignado al ejecutar `New-AzureRmADServicePrincipal` (sin comillas).</span><span class="sxs-lookup"><span data-stu-id="1e6db-104">key: use the *-Password* parameter you assigned when you ran `New-AzureRmADServicePrincipal` (without quotes).</span></span>
- <span data-ttu-id="1e6db-105">inquilino: use el valor de *TenantId* de cuando ejecutó `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="1e6db-105">tenant: use the *TenantId* value from when you ran `Login-AzureRmAccount`.</span></span>

<span data-ttu-id="1e6db-106">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="1e6db-106">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="1e6db-107">Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1e6db-107">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
