Cree un archivo de texto denominado `azureauth.properties` con las credenciales de la entidad de servicio:

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

- suscripción: use el valor de *SubscriptionId* de cuando ejecutó `Login-AzureRmAccount`.
- cliente: use el valor de *ApplicationId* de la salida de la entidad de servicio.
- clave: use el parámetro *-Password* asignado al ejecutar `New-AzureRmADServicePrincipal` (sin comillas).
- inquilino: use el valor de *TenantId* de cuando ejecutó `Login-AzureRmAccount`.

Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo. Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.properties", "User")
```
