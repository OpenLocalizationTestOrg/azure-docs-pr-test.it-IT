---
title: una Cache Redis con Azure Resource Manager aaaProvision | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure modello toodeploy Cache Redis di Azure.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Creare una Cache Redis utilizzando un modello
In questo argomento è illustrato come toocreate un modello di gestione risorse di Azure che distribuisce un Azure Redis Cache. cache di Hello è utilizzabile con un'archiviazione account tookeep diagnostica dati esistenti. Verrà inoltre descritto come toodefine quali risorse vengono distribuite come toodefine parametri e che vengono specificati quando è eseguita la distribuzione di hello. È possibile utilizzare questo modello per la propria distribuzioni o personalizzarlo toomeet esigenze.

Attualmente, le impostazioni di diagnostica vengono condivisi per tutte le cache di hello stessa area per una sottoscrizione. Aggiornamento della cache di una regione hello influisce su tutte le altre cache nell'area di hello.

Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Gestione risorse di Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Per il modello di hello completo, vedere [modello Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Modelli di gestione risorse per hello nuovo [livello Premium](cache-premium-tier-intro.md) sono disponibili. 
> 
> * [Creare una Cache Redis Premium con il clustering](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Creare una Cache Redis Premium con persistenza dei dati](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Creare una Cache Redis Premium con rete virtuale e clustering facoltativo](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck per i modelli più recenti di hello, vedere [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/) e cercare `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Elementi distribuiti
In questo modello, verrà distribuita una Cache Redis di Azure che utilizza un account di archiviazione esistente per dati di diagnostica.

toorun hello automaticamente la distribuzione, fare clic su hello seguente pulsante:

[![Distribuire tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>parameters
Con Gestione risorse di Azure, si definiscono i parametri per i valori si desidera toospecify quando viene distribuito il modello di hello. modello Hello include una sezione denominata parametri che contiene tutti i valori di parametro hello.
È necessario definire un parametro per i valori che variano in base progetto hello che si distribuisce o Hello che si distribuisce ambiente di hello. Non definire parametri per i valori che restano sempre hello stesso. Ogni valore del parametro viene utilizzato in hello modello toodefine hello le risorse distribuite. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
percorso di Hello di hello Cache Redis. Per prestazioni ottimali, utilizzare hello stesso percorso come hello app toobe utilizzato con cache di hello.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
nome di Hello di hello esistente toouse account di archiviazione per diagnostica. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
Un valore booleano che indica se tooallow accedere tramite le porte non SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Valore che indica se la diagnostica è abilitata. Utilizzare ON o OFF.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Risorse toodeploy
### <a name="redis-cache"></a>Cache Redis
Crea hello Cache Redis di Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Comandi toorun distribuzione
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


