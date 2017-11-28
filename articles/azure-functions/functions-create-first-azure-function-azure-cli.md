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
# <a name="create-your-first-function-using-hello-azure-cli"></a><span data-ttu-id="35010-103">Creare la prima funzione utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="35010-103">Create your first function using hello Azure CLI</span></span>

<span data-ttu-id="35010-104">In questa esercitazione Guida introduttiva illustra in dettaglio come toouse Azure funzioni toocreate la prima funzione.</span><span class="sxs-lookup"><span data-stu-id="35010-104">This quickstart tutorial walks through how toouse Azure Functions toocreate your first function.</span></span> <span data-ttu-id="35010-105">Utilizzare hello Azure CLI toocreate un'app di funzione, ovvero infrastruttura senza hello che ospita la funzione.</span><span class="sxs-lookup"><span data-stu-id="35010-105">You use hello Azure CLI toocreate a function app, which is hello serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="35010-106">Hello codice della funzione viene distribuito da un repository GitHub degli esempi.</span><span class="sxs-lookup"><span data-stu-id="35010-106">hello function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="35010-107">È possibile eseguire operazioni di hello seguenti utilizza un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="35010-107">You can follow hello steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="35010-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="35010-108">Prerequisites</span></span> 

<span data-ttu-id="35010-109">Prima di eseguire questo esempio, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="35010-109">Before running this sample, you must have hello following:</span></span>

+ <span data-ttu-id="35010-110">Un account [GitHub](https://github.com) attivo.</span><span class="sxs-lookup"><span data-stu-id="35010-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="35010-111">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="35010-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35010-112">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="35010-112">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="35010-113">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="35010-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="35010-114">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35010-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="35010-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="35010-115">Create a resource group</span></span>

<span data-ttu-id="35010-116">Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="35010-116">Create a resource group with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="35010-117">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app per le funzioni, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="35010-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="35010-118">esempio Hello crea un gruppo di risorse denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="35010-118">hello following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="35010-119">Se non si usa Cloud Shell, prima è necessario accedere usando `az login`.</span><span class="sxs-lookup"><span data-stu-id="35010-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="35010-120">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="35010-120">Create an Azure Storage account</span></span>

<span data-ttu-id="35010-121">Funzioni utilizza uno stato toomaintain account di archiviazione di Azure e altre informazioni sulle funzioni.</span><span class="sxs-lookup"><span data-stu-id="35010-121">Functions uses an Azure Storage account toomaintain state and other information about your functions.</span></span> <span data-ttu-id="35010-122">Creare un account di archiviazione nel gruppo di risorse hello creato utilizzando hello [creare account di archiviazione az](/cli/azure/storage/account#create) comando.</span><span class="sxs-lookup"><span data-stu-id="35010-122">Create a storage account in hello resource group you created by using hello [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="35010-123">In hello seguente comando, sostituire il proprio nome di account di archiviazione univoco globale in cui si vedere hello `<storage_name>` segnaposto.</span><span class="sxs-lookup"><span data-stu-id="35010-123">In hello following command, substitute your own globally unique storage account name where you see hello `<storage_name>` placeholder.</span></span> <span data-ttu-id="35010-124">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="35010-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="35010-125">Dopo aver creato l'account di archiviazione hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="35010-125">After hello storage account has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="35010-126">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="35010-126">Create a function app</span></span>

<span data-ttu-id="35010-127">È necessario disporre di un'esecuzione di hello toohost app funzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="35010-127">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="35010-128">app di funzione Hello offre un ambiente per l'esecuzione del codice di funzione senza server.</span><span class="sxs-lookup"><span data-stu-id="35010-128">hello function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="35010-129">Consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="35010-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="35010-130">Creare un'app di funzione tramite hello [functionapp az creare](/cli/azure/functionapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="35010-130">Create a function app by using hello [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="35010-131">In hello seguente comando, sostituire il proprio nome di app di funzione univoco in cui si vedere hello `<app_name>` segnaposto e hello Nome account di archiviazione per `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="35010-131">In hello following command, substitute your own unique function app name where you see hello `<app_name>` placeholder and hello storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="35010-132">Hello `<app_name>` viene utilizzato come dominio DNS predefinito di hello per app di funzione hello e nome hello in questo caso è necessario toobe univoco tra tutte le App in Azure.</span><span class="sxs-lookup"><span data-stu-id="35010-132">hello `<app_name>` is used as hello default DNS domain for hello function app, and so hello name needs toobe unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="35010-133">Per impostazione predefinita, un'app di funzione viene creata con hello consumo piano di hosting, che significa che le risorse vengono aggiunte in modo dinamico come richiesto dalle funzioni e si paga solo quando le funzioni sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="35010-133">By default, a function app is created with hello Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="35010-134">Per ulteriori informazioni, vedere [piano di hosting corretto hello scegliere](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="35010-134">For more information, see [Choose hello correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="35010-135">Dopo aver hello funzione app è stata creata, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="35010-135">After hello function app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="35010-136">Dopo aver creato un'app di funzione, è possibile distribuire il codice della funzione hello dal repository di esempio hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="35010-136">Now that you have a function app, you can deploy hello actual function code from hello GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="35010-137">Distribuire il codice di funzione</span><span class="sxs-lookup"><span data-stu-id="35010-137">Deploy your function code</span></span>  

<span data-ttu-id="35010-138">Esistono diversi modi toocreate il codice di funzione nell'app nuova funzione.</span><span class="sxs-lookup"><span data-stu-id="35010-138">There are several ways toocreate your function code in your new function app.</span></span> <span data-ttu-id="35010-139">In questo argomento si connette tooa repository di esempio in GitHub.</span><span class="sxs-lookup"><span data-stu-id="35010-139">This topic connects tooa sample repository in GitHub.</span></span> <span data-ttu-id="35010-140">Come in precedenza, hello seguente di codice sostituire hello `<app_name>` con nome hello dell'app di funzione hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="35010-140">As before, in hello following code replace hello `<app_name>` placeholder with hello name of hello function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="35010-141">Dopo la distribuzione di hello impostazione di origine, hello CLI di Azure Mostra toohello simile di informazioni (i valori null rimossi per leggibilità) di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="35010-141">After hello deployment source been set, hello Azure CLI shows information similar toohello following example (null values removed for readability):</span></span>

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

## <a name="test-hello-function"></a><span data-ttu-id="35010-142">Funzione hello test</span><span class="sxs-lookup"><span data-stu-id="35010-142">Test hello function</span></span>

<span data-ttu-id="35010-143">Funzione cURL tootest hello distribuito in un computer Mac o Linux o con Bash in Windows.</span><span class="sxs-lookup"><span data-stu-id="35010-143">Use cURL tootest hello deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="35010-144">Eseguire hello cURL comando, sostituendo hello seguente `<app_name>` segnaposto con il nome di hello dell'app in funzione.</span><span class="sxs-lookup"><span data-stu-id="35010-144">Execute hello following cURL command, replacing hello `<app_name>` placeholder with hello name of your function app.</span></span> <span data-ttu-id="35010-145">Aggiungere la stringa di query hello `&name=<yourname>` toohello URL.</span><span class="sxs-lookup"><span data-stu-id="35010-145">Append hello query string `&name=<yourname>` toohello URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="35010-147">Se non è disponibile nella riga di comando cURL, immettere hello stesso URL nell'indirizzo hello del web browser.</span><span class="sxs-lookup"><span data-stu-id="35010-147">If you don't have cURL available in your command line, enter hello same URL in hello address of your web browser.</span></span> <span data-ttu-id="35010-148">Nuovamente, sostituire hello `<app_name>` segnaposto con il nome di hello dell'app in funzione e aggiungere la stringa di query hello `&name=<yourname>` toohello URL ed eseguire la richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="35010-148">Again, replace hello `<app_name>` placeholder with hello name of your function app, and append hello query string `&name=<yourname>` toohello URL and execute hello request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="35010-150">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="35010-150">Clean up resources</span></span>

<span data-ttu-id="35010-151">Altre guide di avvio rapido di questa raccolta si basano sulla presente guida di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="35010-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="35010-152">Se si intende toocontinue toowork nelle successive Guide rapide o con le esercitazioni di hello, pulire le risorse di hello create in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="35010-152">If you plan toocontinue on toowork with subsequent quickstarts or with hello tutorials, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="35010-153">Se non si prevede toocontinue, utilizzare tutte le risorse create da questa Guida rapida hello toodelete di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="35010-153">If you do not plan toocontinue, use hello following command toodelete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="35010-154">Quando richiesto, digitare `y`.</span><span class="sxs-lookup"><span data-stu-id="35010-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35010-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35010-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
