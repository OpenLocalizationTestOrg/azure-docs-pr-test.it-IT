### <a name="app-service-plan"></a><span data-ttu-id="38a76-101">Piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="38a76-101">App Service plan</span></span>
<span data-ttu-id="38a76-102">Crea piano di servizio hello per l'hosting hello web app.</span><span class="sxs-lookup"><span data-stu-id="38a76-102">Creates hello service plan for hosting hello web app.</span></span> <span data-ttu-id="38a76-103">Specificare il nome di hello del piano di hello tramite hello **hostingPlanName** parametro.</span><span class="sxs-lookup"><span data-stu-id="38a76-103">You provide hello name of hello plan through hello **hostingPlanName** parameter.</span></span> <span data-ttu-id="38a76-104">percorso di Hello del piano di hello è hello nello stesso percorso utilizzato per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="38a76-104">hello location of hello plan is hello same location used for hello resource group.</span></span> <span data-ttu-id="38a76-105">dimensioni di livello e di lavoro piano tariffario Hello vengono specificate in hello **sku** e **workerSize** parametri</span><span class="sxs-lookup"><span data-stu-id="38a76-105">hello pricing tier and worker size are specified in hello **sku** and **workerSize** parameters</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('hostingPlanName')]",
      "type": "Microsoft.Web/serverfarms",
      "location": "[resourceGroup().location]",
      "sku": {
        "name": "[parameters('sku')]",
        "capacity": "[parameters('workerSize')]"
      },
      "properties": {
        "name": "[parameters('hostingPlanName')]"
      }
    },

