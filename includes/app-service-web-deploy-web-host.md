### <a name="app-service-plan"></a>Piano di servizio app
Crea piano di servizio hello per l'hosting hello web app. Specificare il nome di hello del piano di hello tramite hello **hostingPlanName** parametro. percorso di Hello del piano di hello è hello nello stesso percorso utilizzato per il gruppo di risorse hello. dimensioni di livello e di lavoro piano tariffario Hello vengono specificate in hello **sku** e **workerSize** parametri

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

