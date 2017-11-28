---
title: Automatizzare la distribuzione di risorse per un'app per le funzioni in Funzioni di Azure | Microsoft Docs
description: Informazioni su come creare un modello di Azure Resource Manager per distribuire l'app per le funzioni.
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: funzioni di azure, funzioni, architettura senza server, infrastruttura come codice, azure resource manager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="0a063-104">Automatizzare la distribuzione di risorse per l'app per le funzioni in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="0a063-105">È possibile usare un modello di Azure Resource Manager per distribuire un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="0a063-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="0a063-106">Questo articolo descrive le risorse e i parametri necessari per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="0a063-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="0a063-107">A seconda dei [trigger e dei binding](functions-triggers-bindings.md) potrebbe essere necessario distribuire risorse aggiuntive nell'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="0a063-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="0a063-108">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0a063-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="0a063-109">Per i modelli di esempio, vedere:</span><span class="sxs-lookup"><span data-stu-id="0a063-109">For sample templates, see:</span></span>
- <span data-ttu-id="0a063-110">[App per le funzioni nel piano a consumo]</span><span class="sxs-lookup"><span data-stu-id="0a063-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="0a063-111">[App per le funzioni nel piano di servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="0a063-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="0a063-112">Risorse necessarie</span><span class="sxs-lookup"><span data-stu-id="0a063-112">Required resources</span></span>

<span data-ttu-id="0a063-113">Un'app per le funzioni richiede le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a063-113">A function app requires these resources:</span></span>

* <span data-ttu-id="0a063-114">Un account di [archiviazione di Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="0a063-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="0a063-115">Un piano di hosting (piano a consumo o piano di servizio app)</span><span class="sxs-lookup"><span data-stu-id="0a063-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="0a063-116">Un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="0a063-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="0a063-117">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="0a063-117">Storage account</span></span>

<span data-ttu-id="0a063-118">Per un'app per le funzioni è necessario l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a063-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="0a063-119">È necessario un account per utilizzo generico che supporti BLOB, tabelle, code e i file.</span><span class="sxs-lookup"><span data-stu-id="0a063-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="0a063-120">Per altre informazioni, vedere i [requisiti dell'account di archiviazione per Funzioni di Azure](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="0a063-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="0a063-121">È anche necessario specificare le proprietà `AzureWebJobsStorage` e `AzureWebJobsDashboard` come impostazioni dell'app nella configurazione del sito.</span><span class="sxs-lookup"><span data-stu-id="0a063-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="0a063-122">Il runtime di Funzioni di Azure usa la stringa di connessione `AzureWebJobsStorage` per creare code interne.</span><span class="sxs-lookup"><span data-stu-id="0a063-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="0a063-123">La stringa di connessione `AzureWebJobsDashboard` viene usata per accedere all'archivio tabelle di Azure e abilitare la scheda **Monitoraggio** nel portale.</span><span class="sxs-lookup"><span data-stu-id="0a063-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="0a063-124">Queste proprietà sono specificate nella raccolta `appSettings` dell'oggetto `siteConfig`:</span><span class="sxs-lookup"><span data-stu-id="0a063-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="0a063-125">Piano di hosting</span><span class="sxs-lookup"><span data-stu-id="0a063-125">Hosting plan</span></span>

<span data-ttu-id="0a063-126">La definizione del piano di hosting varia a seconda che si usi un piano a consumo o un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="0a063-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="0a063-127">Vedere [Distribuire un'app per le funzioni nel piano a consumo](#consumption) e [Distribuire un'app per le funzioni nel piano di servizio app](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="0a063-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="0a063-128">App per le funzioni</span><span class="sxs-lookup"><span data-stu-id="0a063-128">Function app</span></span>

<span data-ttu-id="0a063-129">L'app per le funzioni viene definita usando una risorsa **Microsoft.Web/Site** di tipo **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="0a063-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="0a063-130">Distribuire un'app per le funzioni nel piano a consumo</span><span class="sxs-lookup"><span data-stu-id="0a063-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="0a063-131">È possibile eseguire un'app per le funzioni in due modalità diverse, ovvero con piano a consumo e piano di servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a063-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="0a063-132">Il piano a consumo alloca automaticamente funzionalità di calcolo durante l'esecuzione del codice, aumenta il numero di istanze in base alla necessità per gestire il carico e quindi riduce le prestazioni quando il codice non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="0a063-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="0a063-133">Non è quindi necessario pagare per le macchine virtuali inattive e riservare in anticipo la capacità.</span><span class="sxs-lookup"><span data-stu-id="0a063-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="0a063-134">Per altre informazioni sui piani di hosting, vedere [Piani a consumo e piani di servizio app di Funzioni di Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="0a063-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="0a063-135">Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano a consumo].</span><span class="sxs-lookup"><span data-stu-id="0a063-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="0a063-136">Creare un piano a consumo</span><span class="sxs-lookup"><span data-stu-id="0a063-136">Create a Consumption plan</span></span>

<span data-ttu-id="0a063-137">Un piano a consumo è un tipo particolare di risorsa "serverfarm".</span><span class="sxs-lookup"><span data-stu-id="0a063-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="0a063-138">Viene specificato usando il valore `Dynamic` per le proprietà `computeMode` e `sku`:</span><span class="sxs-lookup"><span data-stu-id="0a063-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="0a063-139">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="0a063-139">Create a function app</span></span>

<span data-ttu-id="0a063-140">Un piano a consumo richiede anche due impostazioni aggiuntive nella configurazione del sito: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="0a063-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="0a063-141">Queste proprietà consentono di configurare l'account di archiviazione e il percorso in cui vengono archiviati il codice dell'app per le funzioni e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="0a063-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="0a063-142">Distribuire un'app per le funzioni nel piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="0a063-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="0a063-143">Nel piano di servizio app, le app per le funzioni vengono eseguite in macchine virtuali dedicate in SKU Basic, Standard e Premium, analogamente alle app Web.</span><span class="sxs-lookup"><span data-stu-id="0a063-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="0a063-144">Per informazioni dettagliate sul funzionamento del piano di servizio app, vedere [Panoramica approfondita dei piani di servizio app di Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0a063-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="0a063-145">Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano di servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="0a063-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="0a063-146">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="0a063-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="0a063-147">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="0a063-147">Create a function app</span></span> 

<span data-ttu-id="0a063-148">Dopo aver selezionato un'opzione di scalabilità, creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="0a063-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="0a063-149">L'app è il contenitore che incorpora tutte le funzioni.</span><span class="sxs-lookup"><span data-stu-id="0a063-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="0a063-150">Un'app per le funzioni contiene numerose risorse figlio che possono essere usate nella distribuzione, incluse le impostazioni dell'app e le opzioni di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="0a063-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="0a063-151">È anche possibile scegliere di rimuovere la risorsa figlio **sourcecontrols** e usare un'altra [opzione di distribuzione](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0a063-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a063-152">Per poter distribuire l'applicazione usando Azure Resource Manager, è importante comprendere come vengono distribuite le risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="0a063-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="0a063-153">Nell'esempio seguente, le configurazioni di livello superiore vengono applicate usando **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="0a063-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="0a063-154">È importante impostare le configurazioni a un livello superiore perché forniscono informazioni al motore di runtime e di distribuzione di Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a063-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="0a063-155">Le informazioni di livello superiore sono necessarie prima di applicare la risorsa figlia **sourcecontrols/web**.</span><span class="sxs-lookup"><span data-stu-id="0a063-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="0a063-156">Anche se è possibile configurare queste impostazioni nella risorsa **config/appSettings** del livello figlio, in alcuni casi l'app per le funzioni deve essere distribuita *prima* di applicare **config/appSettings**.</span><span class="sxs-lookup"><span data-stu-id="0a063-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="0a063-157">Quando ad esempio si usano le funzioni con [app per la logica](../logic-apps/index.md), le funzioni sono una dipendenza di un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="0a063-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="0a063-158">Questo modello usa il valore dell'impostazione app [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file), che imposta la directory di base in cui il motore di distribuzione di Funzioni di Azure (Kudu) cercherà il codice distribuibile.</span><span class="sxs-lookup"><span data-stu-id="0a063-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="0a063-159">Nel repository le funzioni sono in una sottocartella della cartella **src**.</span><span class="sxs-lookup"><span data-stu-id="0a063-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="0a063-160">Pertanto, nell'esempio precedente abbiamo impostato il valore di impostazione dell'app su `src`.</span><span class="sxs-lookup"><span data-stu-id="0a063-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="0a063-161">Se le funzioni sono nella radice del repository o se non si sta distribuendo dal controllo del codice sorgente, è possibile rimuovere questo valore di impostazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="0a063-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="0a063-162">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="0a063-162">Deploy your template</span></span>

<span data-ttu-id="0a063-163">Il modello può essere distribuito in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0a063-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="0a063-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a063-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="0a063-165">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="0a063-166">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="0a063-167">API REST</span><span class="sxs-lookup"><span data-stu-id="0a063-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="0a063-168">Pulsante Deploy to Azure per la distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-168">Deploy to Azure button</span></span>

<span data-ttu-id="0a063-169">Sostituire ```<url-encoded-path-to-azuredeploy-json>``` con una versione [con codifica URL](https://www.bing.com/search?q=url+encode) del percorso non elaborato del file `azuredeploy.json` in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0a063-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="0a063-170">Di seguito è riportato un esempio che usa la sintassi markdown:</span><span class="sxs-lookup"><span data-stu-id="0a063-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="0a063-171">Di seguito è riportato un esempio che usa HTML:</span><span class="sxs-lookup"><span data-stu-id="0a063-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="0a063-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0a063-172">Next steps</span></span>

<span data-ttu-id="0a063-173">Altre informazioni su come sviluppare e configurare le Funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="0a063-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="0a063-174">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="0a063-175">Come configurare le impostazioni dell'app per le funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="0a063-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* <span data-ttu-id="0a063-176">[Create your first Azure function](functions-create-first-azure-function.md) (Creare la prima funzione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0a063-176">[Create your first Azure function](functions-create-first-azure-function.md)</span></span>

<!-- LINKS -->

[App per le funzioni nel piano a consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[App per le funzioni nel piano di servizio app di Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
