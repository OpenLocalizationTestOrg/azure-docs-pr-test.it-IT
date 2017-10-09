Creare un [app web](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` il piano di servizio App con hello [az webapp creare](/cli/azure/webapp#create) comando. 

app web Hello fornisce uno spazio di hosting per il codice e fornisce un'applicazione hello distribuito tooview di URL.

In hello seguente comando, sostituire  *\<nome_app >* con un nome univoco (i caratteri validi sono `a-z`, `0-9`, e `-`). Se `<app_name>` è non univoco, viene visualizzato il messaggio di errore hello "Sito Web con il nome specificato < nome_app > esiste già." URL dell'app web hello predefinito è Hello `https://<app_name>.azurewebsites.net`. 

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

Sfoglia toohello sito toosee app web appena creato.

```bash
http://<app_name>.azurewebsites.net
```
