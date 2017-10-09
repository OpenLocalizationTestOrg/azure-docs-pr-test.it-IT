
<span data-ttu-id="1f6ba-101">Creare un [app per le API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` il piano di servizio App con hello [az webapp creare](/cli/azure/appservice/web#create) comando.</span><span class="sxs-lookup"><span data-stu-id="1f6ba-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="1f6ba-102">app web Hello fornisce uno spazio di hosting per l'API e fornisce un'applicazione hello distribuito tooview di URL.</span><span class="sxs-lookup"><span data-stu-id="1f6ba-102">hello web app provides a hosting space for your API and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="1f6ba-103">In hello seguente comando, sostituire  *\<nome_app >* con un nome univoco.</span><span class="sxs-lookup"><span data-stu-id="1f6ba-103">In hello following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="1f6ba-104">Se `<app_name>` è non univoco, viene visualizzato il messaggio di errore hello "Sito Web con il nome specificato < nome_app > esiste già."</span><span class="sxs-lookup"><span data-stu-id="1f6ba-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="1f6ba-105">URL dell'app web hello predefinito è Hello `https://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="1f6ba-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="1f6ba-106">Quando hello web app è stata creata, hello Azure CLI indica toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="1f6ba-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```