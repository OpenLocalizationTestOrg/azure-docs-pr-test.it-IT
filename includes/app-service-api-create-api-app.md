
Creare un [app per le API](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` il piano di servizio App con hello [az webapp creare](/cli/azure/appservice/web#create) comando. 

app web Hello fornisce uno spazio di hosting per l'API e fornisce un'applicazione hello distribuito tooview di URL.

In hello seguente comando, sostituire  *\<nome_app >* con un nome univoco. Se `<app_name>` è non univoco, viene visualizzato il messaggio di errore hello "Sito Web con il nome specificato < nome_app > esiste già." URL dell'app web hello predefinito è Hello `https://<app_name>.azurewebsites.net`. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando hello web app è stata creata, hello Azure CLI indica toohello di informazioni simili esempio seguente:

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