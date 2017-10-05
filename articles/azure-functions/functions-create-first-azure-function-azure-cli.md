---
title: Creare la prima funzione dall'interfaccia della riga di comando di Azure| Microsoft Docs
description: Informazioni su come creare la prima funzione di Azure per l'esecuzione senza server tramite l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 8bd3e4bb7423db44c48b04f25edcf1074e6ea0bd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-the-azure-cli"></a><span data-ttu-id="79d87-103">Creare la prima funzione usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="79d87-103">Create your first function using the Azure CLI</span></span>

<span data-ttu-id="79d87-104">Questa esercitazione di avvio rapido illustra come usare Funzioni di Azure per creare la prima funzione.</span><span class="sxs-lookup"><span data-stu-id="79d87-104">This quickstart tutorial walks through how to use Azure Functions to create your first function.</span></span> <span data-ttu-id="79d87-105">Si userà l'interfaccia della riga di comando di Azure per creare un'app per le funzioni, ovvero l'infrastruttura senza server che ospita la funzione.</span><span class="sxs-lookup"><span data-stu-id="79d87-105">You use the Azure CLI to create a function app, which is the serverless infrastructure that hosts your function.</span></span> <span data-ttu-id="79d87-106">Il codice della funzione viene distribuito da un repository GitHub di esempio.</span><span class="sxs-lookup"><span data-stu-id="79d87-106">The function code itself is deployed from a GitHub sample repository.</span></span>    

<span data-ttu-id="79d87-107">È possibile eseguire queste procedure con un computer Mac, Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="79d87-107">You can follow the steps below using a Mac, Windows, or Linux computer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="79d87-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="79d87-108">Prerequisites</span></span> 

<span data-ttu-id="79d87-109">Prima di eseguire questo esempio, è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="79d87-109">Before running this sample, you must have the following:</span></span>

+ <span data-ttu-id="79d87-110">Un account [GitHub](https://github.com) attivo.</span><span class="sxs-lookup"><span data-stu-id="79d87-110">An active [GitHub](https://github.com) account.</span></span> 
+ <span data-ttu-id="79d87-111">Una sottoscrizione di Azure attiva.</span><span class="sxs-lookup"><span data-stu-id="79d87-111">An active Azure subscription.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="79d87-112">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="79d87-112">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="79d87-113">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="79d87-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="79d87-114">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="79d87-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="79d87-115">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="79d87-115">Create a resource group</span></span>

<span data-ttu-id="79d87-116">Creare un gruppo di risorse con [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="79d87-116">Create a resource group with the [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="79d87-117">Un gruppo di risorse di Azure è un contenitore logico in cui vengono distribuite e gestite risorse di Azure come app per le funzioni, database e account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="79d87-117">An Azure resource group is a logical container into which Azure resources like function apps, databases, and storage accounts are deployed and managed.</span></span>

<span data-ttu-id="79d87-118">Nell'esempio seguente viene creato il gruppo di risorse denominato `myResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="79d87-118">The following example creates a resource group named `myResourceGroup`.</span></span>  
<span data-ttu-id="79d87-119">Se non si usa Cloud Shell, prima è necessario accedere usando `az login`.</span><span class="sxs-lookup"><span data-stu-id="79d87-119">If you are not using Cloud Shell, you must first sign in using `az login`.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```


## <a name="create-an-azure-storage-account"></a><span data-ttu-id="79d87-120">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="79d87-120">Create an Azure Storage account</span></span>

<span data-ttu-id="79d87-121">Funzioni usa un account di archiviazione di Azure per gestire lo stato e altre informazioni sulle funzioni.</span><span class="sxs-lookup"><span data-stu-id="79d87-121">Functions uses an Azure Storage account to maintain state and other information about your functions.</span></span> <span data-ttu-id="79d87-122">Creare un account di archiviazione nel gruppo di risorse creato usando il comando [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="79d87-122">Create a storage account in the resource group you created by using the [az storage account create](/cli/azure/storage/account#create) command.</span></span>

<span data-ttu-id="79d87-123">Nel comando seguente sostituire il segnaposto `<storage_name>` con il nome globalmente univoco dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="79d87-123">In the following command, substitute your own globally unique storage account name where you see the `<storage_name>` placeholder.</span></span> <span data-ttu-id="79d87-124">I nomi degli account di archiviazione devono avere una lunghezza compresa tra 3 e 24 caratteri e possono contenere solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="79d87-124">Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only.</span></span>

```azurecli-interactive
az storage account create --name <storage_name> --location westeurope --resource-group myResourceGroup --sku Standard_LRS
```

<span data-ttu-id="79d87-125">Al termine della creazione dell'account di archiviazione, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="79d87-125">After the storage account has been created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="create-a-function-app"></a><span data-ttu-id="79d87-126">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="79d87-126">Create a function app</span></span>

<span data-ttu-id="79d87-127">Per ospitare l'esecuzione delle funzioni è necessaria un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="79d87-127">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="79d87-128">L'app per le funzioni offre un ambiente per l'esecuzione senza server del codice di funzione.</span><span class="sxs-lookup"><span data-stu-id="79d87-128">The function app provides an environment for serverless execution of your function code.</span></span> <span data-ttu-id="79d87-129">Consente di raggruppare le funzioni come un'unità logica per semplificare la gestione, la distribuzione e la condivisione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="79d87-129">It lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> <span data-ttu-id="79d87-130">Creare un'app per le funzioni usando il comando [az functionapp create](/cli/azure/functionapp#create).</span><span class="sxs-lookup"><span data-stu-id="79d87-130">Create a function app by using the [az functionapp create](/cli/azure/functionapp#create) command.</span></span> 

<span data-ttu-id="79d87-131">Nel comando seguente sostituire il segnaposto `<app_name>` con il nome univoco dell'app per le funzioni e il nome dell'account di archiviazione con `<storage_name>`.</span><span class="sxs-lookup"><span data-stu-id="79d87-131">In the following command, substitute your own unique function app name where you see the `<app_name>` placeholder and the storage account name for  `<storage_name>`.</span></span> <span data-ttu-id="79d87-132">Dato che verrà usato come dominio DNS predefinito per l'app per le funzioni, è necessario che `<app_name>` sia univoco tra tutte le app in Azure.</span><span class="sxs-lookup"><span data-stu-id="79d87-132">The `<app_name>` is used as the default DNS domain for the function app, and so the name needs to be unique across all apps in Azure.</span></span> 

```azurecli-interactive
az functionapp create --name <app_name> --storage-account  <storage_name>  --resource-group myResourceGroup \
--consumption-plan-location westeurope
```
<span data-ttu-id="79d87-133">Per impostazione predefinita, viene creata un'app per le funzioni con il piano di hosting a consumo, in base al quale le risorse vengono aggiunte dinamicamente in base alle esigenze delle funzioni e si paga solo quando le funzioni sono in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="79d87-133">By default, a function app is created with the Consumption hosting plan, which means that resources are added dynamically as required by your functions and you only pay when functions are running.</span></span> <span data-ttu-id="79d87-134">Per altre informazioni, vedere [Scegliere il piano di hosting corretto](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="79d87-134">For more information, see [Choose the correct hosting plan](functions-scale.md).</span></span> 

<span data-ttu-id="79d87-135">Al termine della creazione dell'app per le funzioni, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="79d87-135">After the function app has been created, the Azure CLI shows information similar to the following example:</span></span>

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

<span data-ttu-id="79d87-136">Dopo aver creato l'app per le funzioni, è possibile ora distribuire il codice di funzione effettivo dal repository GitHub di esempio.</span><span class="sxs-lookup"><span data-stu-id="79d87-136">Now that you have a function app, you can deploy the actual function code from the GitHub sample repository.</span></span>

## <a name="deploy-your-function-code"></a><span data-ttu-id="79d87-137">Distribuire il codice di funzione</span><span class="sxs-lookup"><span data-stu-id="79d87-137">Deploy your function code</span></span>  

<span data-ttu-id="79d87-138">Esistono diversi modi per creare il codice di funzione nella nuova app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="79d87-138">There are several ways to create your function code in your new function app.</span></span> <span data-ttu-id="79d87-139">In questo argomento viene effettuata la connessione a un repository di esempio in GitHub.</span><span class="sxs-lookup"><span data-stu-id="79d87-139">This topic connects to a sample repository in GitHub.</span></span> <span data-ttu-id="79d87-140">Come in precedenza, nel codice seguente sostituire il segnaposto `<app_name>` con il nome dell'app per le funzioni creata.</span><span class="sxs-lookup"><span data-stu-id="79d87-140">As before, in the following code replace the `<app_name>` placeholder with the name of the function app you created.</span></span> 

```azurecli-interactive
az functionapp deployment source config --name <app_name> --resource-group myResourceGroup --branch master \
--repo-url https://github.com/Azure-Samples/functions-quickstart \
--manual-integration 
```
<span data-ttu-id="79d87-141">Dopo aver impostato l'origine di distribuzione, l'interfaccia della riga di comando di Azure visualizza informazioni simili all'esempio seguente (i valori null sono stati rimossi per una migliore leggibilità):</span><span class="sxs-lookup"><span data-stu-id="79d87-141">After the deployment source been set, the Azure CLI shows information similar to the following example (null values removed for readability):</span></span>

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

## <a name="test-the-function"></a><span data-ttu-id="79d87-142">Testare la funzione</span><span class="sxs-lookup"><span data-stu-id="79d87-142">Test the function</span></span>

<span data-ttu-id="79d87-143">Usare cURL per testare la funzione distribuita in un computer Mac o Linux oppure usando Bash per Windows.</span><span class="sxs-lookup"><span data-stu-id="79d87-143">Use cURL to test the deployed function on a Mac or Linux computer or using Bash on Windows.</span></span> <span data-ttu-id="79d87-144">Eseguire il comando cURL seguente, sostituendo il segnaposto `<app_name>` con il nome dell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="79d87-144">Execute the following cURL command, replacing the `<app_name>` placeholder with the name of your function app.</span></span> <span data-ttu-id="79d87-145">Aggiungere la stringa di query `&name=<yourname>` all'URL.</span><span class="sxs-lookup"><span data-stu-id="79d87-145">Append the query string `&name=<yourname>` to the URL.</span></span>

```bash
curl http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
```  

![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-curl.png)  

<span data-ttu-id="79d87-147">Se nella riga di comando non è disponibile un cURL, immettere lo stesso URL nella barra degli indirizzi del browser Web.</span><span class="sxs-lookup"><span data-stu-id="79d87-147">If you don't have cURL available in your command line, enter the same URL in the address of your web browser.</span></span> <span data-ttu-id="79d87-148">Sostituire il segnaposto `<app_name>` con il nome dell'app per le funzioni, aggiungere la stringa di query `&name=<yourname>` all'URL ed eseguire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="79d87-148">Again, replace the `<app_name>` placeholder with the name of your function app, and append the query string `&name=<yourname>` to the URL and execute the request.</span></span> 

    http://<app_name>.azurewebsites.net/api/HttpTriggerJS1?name=<yourname>
   
![Risposta della funzione visualizzata in un browser.](./media/functions-create-first-azure-function-azure-cli/functions-azure-cli-function-test-browser.png)  

## <a name="clean-up-resources"></a><span data-ttu-id="79d87-150">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="79d87-150">Clean up resources</span></span>

<span data-ttu-id="79d87-151">Altre guide di avvio rapido di questa raccolta si basano sulla presente guida di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="79d87-151">Other quickstarts in this collection build upon this quickstart.</span></span> <span data-ttu-id="79d87-152">Se si prevede di continuare a usare le guide di avvio rapido successive o le esercitazioni, non pulire le risorse create in questa guida di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="79d87-152">If you plan to continue on to work with subsequent quickstarts or with the tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="79d87-153">Se non si prevede di continuare, usare il comando seguente per eliminare tutte le risorse create da questa guida di avvio rapido:</span><span class="sxs-lookup"><span data-stu-id="79d87-153">If you do not plan to continue, use the following command to delete all resources created by this quickstart:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```
<span data-ttu-id="79d87-154">Quando richiesto, digitare `y`.</span><span class="sxs-lookup"><span data-stu-id="79d87-154">Type `y` when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="79d87-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="79d87-155">Next steps</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]
