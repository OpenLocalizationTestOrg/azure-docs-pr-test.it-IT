Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando.

[!INCLUDE [app-service-plan](app-service-plan.md)]

esempio Hello crea un piano di servizio App denominato `myAppServicePlan` in hello **libero** tariffario:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Dopo aver creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```