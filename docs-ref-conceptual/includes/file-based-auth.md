Cree un archivo de texto llamado `azureauth.json`. Pegue la salida JSON de la creación de la entidad de servicio.

Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo. Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
