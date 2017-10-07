---
title: la prima funzione hello Azure CLI aaaCreate | Documenti Microsoft
description: Informazioni su come toocreate di Azure prima funzione per l'esecuzione senza tramite hello CLI di Azure.
services: functions
keywords: 
author: ggailey777
ms.author: glenga
ms.assetid: 674a01a7-fd34-4775-8b69-893182742ae0
ms.date: 08/22/2017
ms.topic: hero-article
ms.service: functions
ms.custom: mvc
ms.devlang: azure-cli
manager: erikre
ms.openlocfilehash: 5feed0045d4998b88b0e1bb50996cb7bb42b0822
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-hello-azure-cli"></a>Creare la prima funzione utilizzando hello CLI di Azure

In questa esercitazione Guida introduttiva illustra in dettaglio come toouse Azure funzioni toocreate la prima funzione. Utilizzare hello Azure CLI toocreate un'app di funzione, ovvero infrastruttura senza hello che ospita la funzione. Hello codice della funzione viene distribuito da un repository GitHub degli esempi.    

È possibile eseguire operazioni di hello seguenti utilizza un computer Mac, Windows o Linux. 

## <a name="prerequisites"></a>Prerequisiti 

Prima di eseguire questo esempio, è necessario disporre delle seguenti hello:

+ Un account [GitHub](https://github.com) attivo. 
+ Una sottoscrizione di Azure attiva.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create). Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app per le funzioni, database e account di archiviazione.

esempio Hello crea un gruppo di risorse denominato `myResourceGroup`.  
Se non si usa Cloud Shell, prima è necessario accedere usando `az login`.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a>Creare un account di Archiviazione di Azure

Funzioni utilizza uno stato toomaintain account di archiviazione di Azure e altre informazioni sulle funzioni. Creare un account di archiviazione nel gruppo di risorse hello creato utilizzando hello [creare account di archiviazione az](/cli/azure/storage/account#create) comando.

In hello seguente comando, sostituire il proprio nome di account di archiviazione univoco globale in cui si vedere hello `<storage_name>` segnaposto. I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

Dopo aver creato l'account di archiviazione hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "creationTime": "2017-04-15T17:14:39.320307+00:00",
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myresourcegroup/...",
  "kind": "Storage",
  "location": "westeurope",
  "name": "myfunctionappstorage",
  "primaryEndpoints": {
    "blob": "https://myfunctionappstorage.blob.core.windows.net/",
    "file": "https://myfunctionappstorage.file.core.windows.net/",
    "queue": "https://myfunctionappstorage.queue.core.windows.net/",
    "table": "https://myfunctionappstorage.table.core.windows.net/"
  },
     ....
    // Remaining output has been truncated for readability.
}
```

## <a name="create-a-function-app"></a>Creare un'app per le funzioni

È necessario disporre di un'esecuzione di hello toohost app funzione delle funzioni. app di funzione Hello offre un ambiente per l'esecuzione del codice di funzione senza server. Consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse. Creare un'app di funzione tramite hello [functionapp az creare](/cli/azure/functionapp#create) comando. 

In hello seguente comando, sostituire il proprio nome di app di funzione univoco in cui si vedere hello `<app_name>` segnaposto e hello Nome account di archiviazione per `<storage_name>`. Hello `<app_name>` viene utilizzato come dominio DNS predefinito di hello per app di funzione hello e nome hello in questo caso è necessario toobe univoco tra tutte le App in Azure. 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
Per impostazione predefinita, un'app di funzione viene creata con hello consumo piano di hosting, che significa che le risorse vengono aggiunte in modo dinamico come richiesto dalle funzioni e si paga solo quando le funzioni sono in esecuzione. Per ulteriori informazioni, vedere [piano di hosting corretto hello scegliere](functions-scale.md). 

Dopo aver hello funzione app è stata creata, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "containerSize": 1536,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "quickstart.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "quickstart.azurewebsites.net",
    "quickstart.scm.azurewebsites.net"
  ],
   ....
    // Remaining output has been truncated for readability.
}
```

Dopo aver creato un'app di funzione, è possibile distribuire il codice della funzione hello dal repository di esempio hello GitHub.

## <a name="deploy-your-function-code"></a>Distribuire il codice di funzione  

Esistono diversi modi toocreate il codice di funzione nell'app nuova funzione. In questo argomento si connette tooa repository di esempio in GitHub. Come in precedenza, hello seguente di codice sostituire hello `<app_name>` con nome hello dell'app di funzione hello è stato creato. 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
Dopo la distribuzione di hello impostazione di origine, hello CLI di Azure Mostra toohello simile di informazioni (i valori null rimossi per leggibilità) di esempio seguente:

```json
{
  "branch": "master",
  "deploymentRollbackEnabled": false,
  "id": "/subscriptions/bbbef702-e769-477b-9f16-bc4d3aa97387/resourceGroups/myResourceGroup/...",
  "isManualIntegration": true,
  "isMercurial": false,
  "location": "West Europe",
  "name": "quickstart",
  "repoUrl": "https://github.com/Azure-Samples/functions-quickstart",
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.Web/sites/sourcecontrols"
}
```

## <a name="test-hello-function"></a>Funzione hello test

Funzione cURL tootest hello distribuito in un computer Mac o Linux o con Bash in Windows. Eseguire hello cURL comando, sostituendo hello seguente `<app_name>` segnaposto con il nome di hello dell'app in funzione. Aggiungere la stringa di query hello `&name=<yourname>` toohello URL.

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

Se non è disponibile nella riga di comando cURL, immettere hello stesso URL nell'indirizzo hello del web browser. Nuovamente, sostituire hello `<app_name>` segnaposto con il nome di hello dell'app in funzione e aggiungere la stringa di query hello `&name=<yourname>` toohello URL ed eseguire la richiesta hello. 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a>Pulire le risorse

Altre guide di avvio rapido di questa raccolta si basano sulla presente guida di avvio rapido. Se si intende toocontinue toowork nelle successive Guide rapide o con le esercitazioni di hello, pulire le risorse di hello create in questa Guida rapida. Se non si prevede toocontinue, utilizzare tutte le risorse create da questa Guida rapida hello toodelete di comando seguente:

```azurecli-interactive
az group delete --name myResourceGroup
```
Quando richiesto, digitare `y`.

## <a name="next-steps"></a>Passaggi successivi

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
