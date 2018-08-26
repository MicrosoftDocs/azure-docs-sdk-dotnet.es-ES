<span data-ttu-id="9748f-101">Cree un archivo de texto llamado `azureauth.json`.</span><span class="sxs-lookup"><span data-stu-id="9748f-101">Create a text file named `azureauth.json`.</span></span> <span data-ttu-id="9748f-102">Pegue la salida JSON de la creación de la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="9748f-102">Paste the JSON output from when you created the service principal.</span></span>

<span data-ttu-id="9748f-103">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="9748f-103">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="9748f-104">Use PowerShell para establecer una variable de entorno denominada `AZURE_AUTH_LOCATION` con la ruta de acceso completa al archivo, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9748f-104">Use PowerShell to set an environment variable named `AZURE_AUTH_LOCATION` with the full path to the file, for example:</span></span>

```powershell
[Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\src\azureauth.json", "User")
```
