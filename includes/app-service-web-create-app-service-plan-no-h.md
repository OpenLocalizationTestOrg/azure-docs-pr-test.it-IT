<span data-ttu-id="f57dc-101">Creare un piano di servizio app con il comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f57dc-101">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="f57dc-102">L'esempio seguente crea un piano di servizio app denominato `myAppServicePlan` nel piano tariffario **Gratuito**:</span><span class="sxs-lookup"><span data-stu-id="f57dc-102">The following example creates an App Service plan named `myAppServicePlan` in the **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="f57dc-103">Al termine della creazione del piano di servizio app, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f57dc-103">When the App Service plan has been created, the Azure CLI shows information similar to the following example:</span></span>

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