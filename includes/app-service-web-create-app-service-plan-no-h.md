<span data-ttu-id="944a8-101">Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="944a8-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="944a8-102">esempio Hello crea un piano di servizio App denominato `myAppServicePlan` in hello **libero** tariffario:</span><span class="sxs-lookup"><span data-stu-id="944a8-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="944a8-103">Dopo aver creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="944a8-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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