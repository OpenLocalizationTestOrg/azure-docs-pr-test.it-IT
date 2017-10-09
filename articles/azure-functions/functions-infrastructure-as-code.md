---
title: distribuzione di risorse aaaAutomate per un'app di funzione in funzioni di Azure | Documenti Microsoft
description: Informazioni su come toobuild un modello di gestione risorse di Azure che consente di distribuire l'app di funzione.
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
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="b978b-104">Automatizzare la distribuzione di risorse per l'app per le funzioni in Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b978b-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="b978b-105">È possibile utilizzare un toodeploy modello di gestione risorse di Azure un'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="b978b-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="b978b-106">Questo articolo vengono illustrati hello necessarie risorse e i parametri per questa operazione.</span><span class="sxs-lookup"><span data-stu-id="b978b-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="b978b-107">Potrebbe essere necessario toodeploy altre risorse, a seconda di hello [trigger e le associazioni](functions-triggers-bindings.md) nell'app di funzione.</span><span class="sxs-lookup"><span data-stu-id="b978b-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="b978b-108">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="b978b-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="b978b-109">Per i modelli di esempio, vedere:</span><span class="sxs-lookup"><span data-stu-id="b978b-109">For sample templates, see:</span></span>
- <span data-ttu-id="b978b-110">[App per le funzioni nel piano a consumo]</span><span class="sxs-lookup"><span data-stu-id="b978b-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="b978b-111">[App per le funzioni nel piano di servizio app di Azure]</span><span class="sxs-lookup"><span data-stu-id="b978b-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="b978b-112">Risorse necessarie</span><span class="sxs-lookup"><span data-stu-id="b978b-112">Required resources</span></span>

<span data-ttu-id="b978b-113">Un'app per le funzioni richiede le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="b978b-113">A function app requires these resources:</span></span>

* <span data-ttu-id="b978b-114">Un account di [archiviazione di Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="b978b-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="b978b-115">Un piano di hosting (piano a consumo o piano di servizio app)</span><span class="sxs-lookup"><span data-stu-id="b978b-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="b978b-116">Un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="b978b-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="b978b-117">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="b978b-117">Storage account</span></span>

<span data-ttu-id="b978b-118">Per un'app per le funzioni è necessario l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b978b-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="b978b-119">È necessario un account per utilizzo generico che supporti BLOB, tabelle, code e i file.</span><span class="sxs-lookup"><span data-stu-id="b978b-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="b978b-120">Per altre informazioni, vedere i [requisiti dell'account di archiviazione per Funzioni di Azure](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="b978b-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="b978b-121">Inoltre, hello proprietà `AzureWebJobsStorage` e `AzureWebJobsDashboard` deve essere specificata come impostazioni dell'app nella configurazione del sito hello.</span><span class="sxs-lookup"><span data-stu-id="b978b-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="b978b-122">il runtime di Azure funzioni Hello utilizza hello `AzureWebJobsStorage` code interne toocreate stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="b978b-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="b978b-123">stringa di connessione Hello `AzureWebJobsDashboard` è usato toolog tooAzure tabella archiviazione e la potenza hello **monitoraggio** scheda nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="b978b-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="b978b-124">Queste proprietà sono specificate in hello `appSettings` insieme in hello `siteConfig` oggetto:</span><span class="sxs-lookup"><span data-stu-id="b978b-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="b978b-125">Piano di hosting</span><span class="sxs-lookup"><span data-stu-id="b978b-125">Hosting plan</span></span>

<span data-ttu-id="b978b-126">definizione di Hello del piano di hosting hello varia a seconda se si utilizza un piano di servizio App o di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b978b-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="b978b-127">Vedere [distribuire un'app di funzione nel piano di consumo hello](#consumption) e [distribuire un'app di funzione nel piano di servizio App hello](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="b978b-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="b978b-128">App per le funzioni</span><span class="sxs-lookup"><span data-stu-id="b978b-128">Function app</span></span>

<span data-ttu-id="b978b-129">risorse app di funzione Hello sono definita tramite una risorsa di tipo **Microsoft.Web/Site** e tipo **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="b978b-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="b978b-130">Distribuire un'app di funzione nel piano di consumo hello</span><span class="sxs-lookup"><span data-stu-id="b978b-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="b978b-131">È possibile eseguire un'app di funzione in due modalità diverse: hello piano il consumo e hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="b978b-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="b978b-132">piano di consumo Hello alloca automaticamente potenza di calcolo quando il codice è in esecuzione, consente una scalabilità orizzontale come carico toohandle necessarie e quindi il ridimensionamento quando codice non è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b978b-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="b978b-133">In tal caso, non si dispone di toopay per le macchine virtuali inattive e non è la capacità di tooreserve in anticipo.</span><span class="sxs-lookup"><span data-stu-id="b978b-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="b978b-134">vedere toolearn ulteriori informazioni sui piani di hosting [i piani di consumo di funzioni di Azure e servizio App](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="b978b-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="b978b-135">Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano a consumo].</span><span class="sxs-lookup"><span data-stu-id="b978b-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="b978b-136">Creare un piano a consumo</span><span class="sxs-lookup"><span data-stu-id="b978b-136">Create a Consumption plan</span></span>

<span data-ttu-id="b978b-137">Un piano a consumo è un tipo particolare di risorsa "serverfarm".</span><span class="sxs-lookup"><span data-stu-id="b978b-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="b978b-138">Specificare tramite hello `Dynamic` valore per hello `computeMode` e `sku` proprietà:</span><span class="sxs-lookup"><span data-stu-id="b978b-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="b978b-139">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="b978b-139">Create a function app</span></span>

<span data-ttu-id="b978b-140">Inoltre, un piano di consumo richiede due impostazioni aggiuntive nella configurazione del sito hello: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="b978b-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="b978b-141">Queste proprietà consentono di configurare hello storage account e il percorso in cui sono archiviati hello funzione app codice e la configurazione.</span><span class="sxs-lookup"><span data-stu-id="b978b-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="b978b-142">Distribuire un'app di funzione nel piano di servizio App hello</span><span class="sxs-lookup"><span data-stu-id="b978b-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="b978b-143">Nel piano di servizio App hello, l'app di funzione viene eseguita nelle macchine virtuali dedicate Basic, Standard e Premium SKU, App tooweb simile.</span><span class="sxs-lookup"><span data-stu-id="b978b-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="b978b-144">Per informazioni dettagliate sul funzionamento di hello piano di servizio App, vedere hello [piani di servizio App di Azure ad approfondimenti su](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b978b-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="b978b-145">Per un modello di Azure Resource Manager di esempio, vedere [App per le funzioni nel piano di servizio app di Azure].</span><span class="sxs-lookup"><span data-stu-id="b978b-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="b978b-146">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="b978b-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="b978b-147">Creare un'app per le funzioni</span><span class="sxs-lookup"><span data-stu-id="b978b-147">Create a function app</span></span> 

<span data-ttu-id="b978b-148">Dopo aver selezionato un'opzione di scalabilità, creare un'app per le funzioni.</span><span class="sxs-lookup"><span data-stu-id="b978b-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="b978b-149">app Hello è hello contenitore contiene tutte le funzioni.</span><span class="sxs-lookup"><span data-stu-id="b978b-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="b978b-150">Un'app per le funzioni contiene numerose risorse figlio che possono essere usate nella distribuzione, incluse le impostazioni dell'app e le opzioni di controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="b978b-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="b978b-151">È anche possibile scegliere hello tooremove **sourcecontrols** risorse figlio e utilizzare un altro [opzione di distribuzione](functions-continuous-deployment.md) invece.</span><span class="sxs-lookup"><span data-stu-id="b978b-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b978b-152">toosuccessfully distribuire l'applicazione usando Gestione risorse di Azure, è importante toounderstand la distribuzione di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="b978b-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="b978b-153">Nell'esempio seguente di hello, vengono applicate le configurazioni di livello superiore tramite **della configurazione di sito**.</span><span class="sxs-lookup"><span data-stu-id="b978b-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="b978b-154">È importante tooset queste configurazioni in un alto livello, non vengono utilizzati solo informazioni toohello funzioni runtime e la distribuzione del motore.</span><span class="sxs-lookup"><span data-stu-id="b978b-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="b978b-155">Informazioni di primo livello sono necessario prima figlio hello **sourcecontrols/web** è applicata una risorsa.</span><span class="sxs-lookup"><span data-stu-id="b978b-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="b978b-156">Sebbene sia possibile tooconfigure queste impostazioni in hello livello figlio **config/appSettings** risorse, in alcuni casi l'app di funzione deve essere distribuito *prima* **config/appSettings**  viene applicato.</span><span class="sxs-lookup"><span data-stu-id="b978b-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="b978b-157">Quando ad esempio si usano le funzioni con [app per la logica](../logic-apps/index.md), le funzioni sono una dipendenza di un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="b978b-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="b978b-158">Questo modello Usa hello [progetto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valore di impostazioni applicazione, che imposta hello directory di base in cui hello il motore di distribuzione di funzioni (Kudu) esegue la ricerca di codice distribuibile.</span><span class="sxs-lookup"><span data-stu-id="b978b-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="b978b-159">Il repository, nostro funzioni sono in una sottocartella di hello **src** cartella.</span><span class="sxs-lookup"><span data-stu-id="b978b-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="b978b-160">In tal caso, nell'hello sopra riportato, viene impostato il valore delle impostazioni app hello troppo`src`.</span><span class="sxs-lookup"><span data-stu-id="b978b-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="b978b-161">Se le funzioni si trovano nella radice di hello del repository, o se non si sta distribuendo dal controllo del codice sorgente, è possibile rimuovere questo valore di impostazioni di app.</span><span class="sxs-lookup"><span data-stu-id="b978b-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="b978b-162">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="b978b-162">Deploy your template</span></span>

<span data-ttu-id="b978b-163">È possibile utilizzare uno qualsiasi dei seguenti modi toodeploy hello del modello:</span><span class="sxs-lookup"><span data-stu-id="b978b-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="b978b-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b978b-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="b978b-165">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b978b-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="b978b-166">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b978b-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="b978b-167">API REST</span><span class="sxs-lookup"><span data-stu-id="b978b-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="b978b-168">Pulsante tooAzure di distribuzione</span><span class="sxs-lookup"><span data-stu-id="b978b-168">Deploy tooAzure button</span></span>

<span data-ttu-id="b978b-169">Sostituire ```<url-encoded-path-to-azuredeploy-json>``` con un [con codifica URL](https://www.bing.com/search?q=url+encode) versione di hello path non elaborato del `azuredeploy.json` file in GitHub.</span><span class="sxs-lookup"><span data-stu-id="b978b-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="b978b-170">Di seguito è riportato un esempio che usa la sintassi markdown:</span><span class="sxs-lookup"><span data-stu-id="b978b-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="b978b-171">Di seguito è riportato un esempio che usa HTML:</span><span class="sxs-lookup"><span data-stu-id="b978b-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="b978b-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b978b-172">Next steps</span></span>

<span data-ttu-id="b978b-173">Per ulteriori informazioni su toodevelop e configurare le funzioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="b978b-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="b978b-174">Guida di riferimento per gli sviluppatori di Funzioni di Azure</span><span class="sxs-lookup"><span data-stu-id="b978b-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="b978b-175">Funzionamento delle impostazioni dell'app Azure tooconfigure</span><span class="sxs-lookup"><span data-stu-id="b978b-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* <span data-ttu-id="b978b-176">[Create your first Azure function](functions-create-first-azure-function.md) (Creare la prima funzione di Azure)</span><span class="sxs-lookup"><span data-stu-id="b978b-176">[Create your first Azure function](functions-create-first-azure-function.md)</span></span>

<!-- LINKS -->

[App per le funzioni nel piano a consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[App per le funzioni nel piano di servizio app di Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
