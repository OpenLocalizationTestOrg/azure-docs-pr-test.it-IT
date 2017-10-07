---
title: aaaCreate, compilare e distribuire App in Visual Studio - App Azure per la logica per la logica | Documenti Microsoft
description: Creare progetti di Visual Studio per poter progettare, compilare e distribuire app per la logica di Azure.
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e484e5ce-77e9-4fa9-bcbe-f851b4eb42a6
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 2/14/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 5154cb05f9a48e9f0f2381a6953947217f7bb114
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="4db77-103">Progettare, compilare e distribuire app per la logica di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4db77-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="4db77-104">Sebbene hello [portale di Azure](https://portal.azure.com/) offre un modo eccellente per si toocreate e gestire le app di logica di Azure, è possibile utilizzare Visual Studio per la progettazione, compilazione e distribuzione di App per la logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-104">Although hello [Azure portal](https://portal.azure.com/) offers a great way for you toocreate and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="4db77-105">Visual Studio fornisce strumenti avanzati come hello progettazione applicazione logica per l'utente toocreate logica App, configurare i modelli di distribuzione e l'automazione e distribuire l'ambiente tooany.</span><span class="sxs-lookup"><span data-stu-id="4db77-105">Visual Studio provides rich tools like hello Logic App Designer for you toocreate logic apps, configure deployment and automation templates, and deploy tooany environment.</span></span> 

<span data-ttu-id="4db77-106">informazioni su tooget iniziare con le app di logica di Azure, [come toocreate la prima app logica nel portale di Azure hello](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4db77-106">tooget started with Azure Logic Apps, learn [how toocreate your first logic app in hello Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="4db77-107">Procedura di installazione</span><span class="sxs-lookup"><span data-stu-id="4db77-107">Installation steps</span></span>

<span data-ttu-id="4db77-108">tooinstall e configurare gli strumenti di Visual Studio per le app di logica di Azure, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="4db77-108">tooinstall and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4db77-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4db77-109">Prerequisites</span></span>

* <span data-ttu-id="4db77-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="4db77-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="4db77-111">[Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="4db77-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="4db77-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4db77-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="4db77-113">Web toohello Access quando si utilizza Progettazione incorporato hello</span><span class="sxs-lookup"><span data-stu-id="4db77-113">Access toohello web when using hello embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="4db77-114">Installare gli strumenti di Visual Studio per le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="4db77-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="4db77-115">Dopo aver installato i prerequisiti di hello:</span><span class="sxs-lookup"><span data-stu-id="4db77-115">After you install hello prerequisites:</span></span>

1. <span data-ttu-id="4db77-116">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4db77-116">Open Visual Studio.</span></span> <span data-ttu-id="4db77-117">In hello **strumenti** dal menu **estensioni e aggiornamenti**.</span><span class="sxs-lookup"><span data-stu-id="4db77-117">On hello **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="4db77-118">Espandere hello **Online** categoria, eseguire la ricerca online.</span><span class="sxs-lookup"><span data-stu-id="4db77-118">Expand hello **Online** category so you can search online.</span></span>
3. <span data-ttu-id="4db77-119">Sfogliare o cercare **App per la logica** per visualizzare **Azure Logic Apps Tools for Visual Studio** (Strumenti per app per la logica di Azure per Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="4db77-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="4db77-120">toodownload e l'estensione di hello installazione, fare clic su **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="4db77-120">toodownload and install hello extension, click **Download**.</span></span>
5. <span data-ttu-id="4db77-121">Al termine dell'installazione riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4db77-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="4db77-122">È inoltre possibile scaricare [Azure logica App Tools per Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) hello e [Azure logica App Tools per Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) direttamente da Visual Studio Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and hello [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from hello Visual Studio Marketplace.</span></span>

<span data-ttu-id="4db77-123">Al termine dell'installazione, è possibile utilizzare il progetto di gruppo di risorse di Azure hello con logica di progettazione di App.</span><span class="sxs-lookup"><span data-stu-id="4db77-123">After you finish installation, you can use hello Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="4db77-124">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="4db77-124">Create your project</span></span>

1. <span data-ttu-id="4db77-125">In hello **File** dal menu Vai troppo**New**e selezionare **progetto**.</span><span class="sxs-lookup"><span data-stu-id="4db77-125">On hello **File** menu, go too**New**, and select **Project**.</span></span> <span data-ttu-id="4db77-126">O tooadd tooan il progetto esistente di soluzione, andare troppo**Aggiungi**e selezionare **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="4db77-126">Or tooadd your project tooan existing solution, go too**Add**, and select **New Project**.</span></span>

    ![File menu](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="4db77-128">In hello **nuovo progetto** finestra Trova **Cloud**e selezionare **il gruppo di risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="4db77-128">In hello **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="4db77-129">Assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4db77-129">Name your project, and click **OK**.</span></span>

    ![Add new project](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="4db77-131">Seleziona hello **logica App** modello, che viene creato un modello di distribuzione app vuota logica toouse.</span><span class="sxs-lookup"><span data-stu-id="4db77-131">Select hello **Logic App** template, which creates a blank logic app deployment template for you toouse.</span></span> <span data-ttu-id="4db77-132">Dopo aver selezionato il modello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4db77-132">After you select your template, click **OK**.</span></span>

    ![Selezionare il modello App per la logica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="4db77-134">È stato aggiunto a questo punto soluzione logica app progetto tooyour.</span><span class="sxs-lookup"><span data-stu-id="4db77-134">You've now added your logic app project tooyour solution.</span></span> 
    <span data-ttu-id="4db77-135">In Esplora soluzioni hello, dovrebbe essere visualizzato il file di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4db77-135">In hello Solution Explorer, your deployment file should appear.</span></span>

    ![File di distribuzione](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="4db77-137">Creare l'app per la logica con la finestra di progettazione</span><span class="sxs-lookup"><span data-stu-id="4db77-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="4db77-138">Quando si dispone di un progetto di gruppo di risorse di Azure che contiene una logica app, è possibile aprire hello logica di progettazione di App in Visual Studio toocreate il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4db77-138">When you have an Azure Resource Group project that contains a logic app, you can open hello Logic App Designer in Visual Studio toocreate your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="4db77-139">finestra di progettazione Hello richiede una connessione a internet eseguire una query troppo connettori per i dati e le proprietà disponibili.</span><span class="sxs-lookup"><span data-stu-id="4db77-139">hello designer requires an internet connection too query connectors for available properties and data.</span></span> <span data-ttu-id="4db77-140">Ad esempio, se si utilizza hello connettore di Dynamics CRM Online, progettazione hello query il personalizzato CRM istanza tooshow disponibile e le proprietà predefinite.</span><span class="sxs-lookup"><span data-stu-id="4db77-140">For example, if you use hello Dynamics CRM Online connector, hello designer queries your CRM instance tooshow available custom and default properties.</span></span>

1. <span data-ttu-id="4db77-141">Fare clic con il pulsante destro del mouse sul file `<template>.json` e scegliere **Open with Logic App Designer** (Apri con Progettazione app per la logica).</span><span class="sxs-lookup"><span data-stu-id="4db77-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="4db77-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="4db77-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="4db77-143">Scegliere la sottoscrizione di Azure, il gruppo di risorse e la posizione per il modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="4db77-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4db77-144">Progettando un'app per la logica verranno create risorse di connessione API per l'esecuzione di query per ottenere le proprietà durante la progettazione.</span><span class="sxs-lookup"><span data-stu-id="4db77-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="4db77-145">Visual Studio Usa il toocreate gruppo di risorse selezionato tali connessioni in fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="4db77-145">Visual Studio uses your selected resource group toocreate those connections during design time.</span></span> <span data-ttu-id="4db77-146">tooview o modificare le connessioni di API, recarsi toohello portale di Azure e cercare **connessioni API**.</span><span class="sxs-lookup"><span data-stu-id="4db77-146">tooview or change any API Connections, go toohello Azure portal, and browse for **API Connections**.</span></span>

    ![Selezione della sottoscrizione](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="4db77-148">finestra di progettazione di Hello Usa definizione hello in hello `<template>.json` file per il rendering.</span><span class="sxs-lookup"><span data-stu-id="4db77-148">hello designer uses hello definition in hello `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="4db77-149">Creare e progettare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-149">Create and design your logic app.</span></span> <span data-ttu-id="4db77-150">Il modello di distribuzione viene aggiornato con le modifiche.</span><span class="sxs-lookup"><span data-stu-id="4db77-150">Your deployment template is updated with your changes.</span></span>

    ![Progettazione app per la logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="4db77-152">Visual Studio aggiunge `Microsoft.Web/connections` troppo la risorsa del file di risorse per tutte le connessioni app logica deve toofunction.</span><span class="sxs-lookup"><span data-stu-id="4db77-152">Visual Studio adds `Microsoft.Web/connections` resources too your resource file for any connections your logic app needs toofunction.</span></span> <span data-ttu-id="4db77-153">Queste proprietà di connessione possono essere impostate durante la distribuzione e gestite dopo aver distribuito **connessioni API** in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4db77-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in hello Azure portal.</span></span>

### <a name="switch-toojson-code-view"></a><span data-ttu-id="4db77-154">Visualizzazione di codice tooJSON commutatore</span><span class="sxs-lookup"><span data-stu-id="4db77-154">Switch tooJSON code view</span></span>

<span data-ttu-id="4db77-155">hello tooshow rappresentazione JSON per l'app di logica, seleziona hello **visualizzazione codice** scheda nella parte inferiore di hello della finestra di progettazione hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-155">tooshow hello JSON representation for your logic app, select hello **Code View** tab at hello bottom of hello designer.</span></span>

<span data-ttu-id="4db77-156">tooswitch toohello completo della risorsa JSON di eseguire il pulsante destro del mouse hello `<template>.json` file e selezionare **aprire**.</span><span class="sxs-lookup"><span data-stu-id="4db77-156">tooswitch back toohello full resource JSON, right-click hello `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-toovisual-studio-deployment-templates"></a><span data-ttu-id="4db77-157">Aggiungere i riferimenti per i modelli di distribuzione di risorse dipendenti tooVisual Studio</span><span class="sxs-lookup"><span data-stu-id="4db77-157">Add references for dependent resources tooVisual Studio deployment templates</span></span>

<span data-ttu-id="4db77-158">Quando si desidera che la logica app tooreference da risorse dipendenti, è possibile utilizzare [funzioni di modello di gestione risorse di Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) nel modello di distribuzione di app logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-158">When you want your logic app tooreference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="4db77-159">Ad esempio, è consigliabile il tooreference app logica un account Azure funzione o di integrazione che si desidera toodeploy insieme all'app di logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-159">For example, you might want your logic app tooreference an Azure Function or integration account that you want toodeploy alongside your logic app.</span></span> <span data-ttu-id="4db77-160">Seguire queste linee guida sulle modalità di rendering correttamente toouse parametri nel modello di distribuzione in modo che hello progettazione applicazione logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-160">Follow these guidelines about how toouse parameters in your deployment template so that hello Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="4db77-161">È possibile usare i parametri dell'app per la logica in questi tipi di trigger e azioni:</span><span class="sxs-lookup"><span data-stu-id="4db77-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="4db77-162">Flusso di lavoro figlio</span><span class="sxs-lookup"><span data-stu-id="4db77-162">Child workflow</span></span>
*   <span data-ttu-id="4db77-163">App per le funzioni</span><span class="sxs-lookup"><span data-stu-id="4db77-163">Function app</span></span>
*   <span data-ttu-id="4db77-164">Chiamata APIM</span><span class="sxs-lookup"><span data-stu-id="4db77-164">APIM call</span></span>
*   <span data-ttu-id="4db77-165">URL di runtime della connessione API</span><span class="sxs-lookup"><span data-stu-id="4db77-165">API connection runtime URL</span></span>
*   <span data-ttu-id="4db77-166">Percorso di connessione API</span><span class="sxs-lookup"><span data-stu-id="4db77-166">API connection path</span></span>

<span data-ttu-id="4db77-167">Ed è possibile usare le funzioni di modello, ad esempio parametri, variabili, resourceId, CONCAT e così via. Ad esempio, ecco come è possibile sostituire l'ID di risorsa di Azure funzione hello:</span><span class="sxs-lookup"><span data-stu-id="4db77-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace hello Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="4db77-168">E dove si useranno i parametri:</span><span class="sxs-lookup"><span data-stu-id="4db77-168">And where you would use parameters:</span></span>

```
"MyFunction": {
    "type": "Function",
    "inputs": {
        "body":{},
        "function":{
            "id":"[resourceid('Microsoft.Web/sites/functions','functionApp',parameters('functionName'))]"
        }
    },
    "runAfter":{}
}
```
<span data-ttu-id="4db77-169">Un altro esempio è possibile parametrizzare hello Bus di servizio invia l'operazione di messaggio:</span><span class="sxs-lookup"><span data-stu-id="4db77-169">As another example you can parameterize hello Service Bus send message operation:</span></span>

```
"Send_message": {
    "type": "ApiConnection",
        "inputs": {
            "host": {
                "connection": {
                    "name": "@parameters('$connections')['servicebus']['connectionId']"
                }
            },
            "method": "post",
            "path": "[concat('/@{encodeURIComponent(''', parameters('queueuname'), ''')}/messages')]",
            "body": {
                "ContentData": "@{base64(triggerBody())}"
            },
            "queries": {
                "systemProperties": "None"
            }
        },
        "runAfter": {}
    }
```
> [!NOTE] 
> <span data-ttu-id="4db77-170">host.runtimeUrl è facoltativo e può essere rimosso dal modello, se presente.</span><span class="sxs-lookup"><span data-stu-id="4db77-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="4db77-171">Per hello progettazione applicazione logica toowork quando si utilizzano parametri, è necessario fornire valori predefiniti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4db77-171">For hello Logic App Designer toowork when you use parameters, you must provide default values, for example:</span></span>
> 
> ```
> "parameters": {
>     "IntegrationAccount": {
>     "type":"string",
>     "minLength":1,
>     "defaultValue":"/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Logic/integrationAccounts/<integrationAccountName>"
>     }
> },
> ```

### <a name="save-your-logic-app"></a><span data-ttu-id="4db77-172">Salvare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="4db77-172">Save your logic app</span></span>

<span data-ttu-id="4db77-173">toosave app logica in qualsiasi momento, andare troppo**File** > **salvare**.</span><span class="sxs-lookup"><span data-stu-id="4db77-173">toosave your logic app at anytime, go too**File** > **Save**.</span></span> <span data-ttu-id="4db77-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="4db77-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="4db77-175">Se l'applicazione di logica ha tutti gli errori quando si salva l'applicazione, vengono visualizzati in Visual Studio hello **output** finestra.</span><span class="sxs-lookup"><span data-stu-id="4db77-175">If your logic app has any errors when you save your app, they appear in hello Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="4db77-176">Distribuire l'app per la logica da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4db77-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="4db77-177">Dopo aver configurato l'app, è possibile distribuirla direttamente da Visual Studio in pochi passaggi.</span><span class="sxs-lookup"><span data-stu-id="4db77-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="4db77-178">In Esplora risorse, mouse sul progetto e passare troppo**Distribuisci** > **nuova distribuzione...**</span><span class="sxs-lookup"><span data-stu-id="4db77-178">In Solution Explorer, right-click your project, and go too**Deploy** > **New Deployment...**</span></span>

    ![New deployment](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="4db77-180">Quando richiesto, accedere tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4db77-180">When you're prompted, sign in tooyour Azure subscription.</span></span> 

3. <span data-ttu-id="4db77-181">A questo punto è necessario selezionare i dettagli di hello per il gruppo di risorse hello in cui si desidera toodeploy app logica.</span><span class="sxs-lookup"><span data-stu-id="4db77-181">Now you must select hello details for hello resource group where you want toodeploy your logic app.</span></span> <span data-ttu-id="4db77-182">Al termine, fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="4db77-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4db77-183">Assicurarsi di selezionare il modello corretto di hello e file dei parametri per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-183">Make sure that you select hello correct template and parameters file for hello resource group.</span></span> <span data-ttu-id="4db77-184">Ad esempio, se si desidera toodeploy tooa ambiente di produzione, scegliere file dei parametri di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-184">For example, if you want toodeploy tooa production environment, choose hello production parameters file.</span></span>

    ![Distribuire un gruppo di tooresource](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="4db77-186">viene visualizzato lo stato di distribuzione Hello in hello **Output** finestra.</span><span class="sxs-lookup"><span data-stu-id="4db77-186">hello deployment status appears in hello **Output** window.</span></span> 
    <span data-ttu-id="4db77-187">Potrebbe essere tooselect **Azure Provisioning** in hello **Mostra output di** elenco.</span><span class="sxs-lookup"><span data-stu-id="4db77-187">You might have tooselect **Azure Provisioning** in hello **Show output from** list.</span></span>

    ![Output dello stato di distribuzione](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="4db77-189">In futuro hello, è possibile modificare l'applicazione logica in un controllo del codice sorgente e utilizzare le nuove versioni toodeploy di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4db77-189">In hello future, you can edit your logic app in source control, and use Visual Studio toodeploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="4db77-190">Se si modifica direttamente la definizione di hello in hello portale di Azure, tali modifiche vengono sovrascritte durante la distribuzione da Visual Studio successivo.</span><span class="sxs-lookup"><span data-stu-id="4db77-190">If you change hello definition in hello Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-tooan-existing-resource-group-project"></a><span data-ttu-id="4db77-191">Aggiungere il progetto di gruppo di risorse esistente logica app tooan</span><span class="sxs-lookup"><span data-stu-id="4db77-191">Add your logic app tooan existing Resource Group project</span></span>

<span data-ttu-id="4db77-192">Se si dispone di un progetto di gruppo di risorse esistente, è possibile aggiungere il progetto di logica app toothat nella finestra Struttura JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-192">If you have an existing Resource Group project, you can add your logic app toothat project in hello JSON Outline window.</span></span> <span data-ttu-id="4db77-193">È anche possibile aggiungere un'altra app logica insieme app hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4db77-193">You can also add another logic app alongside hello app you previously created.</span></span>

1. <span data-ttu-id="4db77-194">Aprire hello `<template>.json` file.</span><span class="sxs-lookup"><span data-stu-id="4db77-194">Open hello `<template>.json` file.</span></span>

2. <span data-ttu-id="4db77-195">hello tooopen finestra Struttura JSON, andare troppo**vista** > **altre finestre** > **struttura JSON**.</span><span class="sxs-lookup"><span data-stu-id="4db77-195">tooopen hello JSON Outline window, go too**View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="4db77-196">Fare clic su un file modello di risorsa toohello, tooadd **Aggiungi risorsa** nella parte superiore di hello della finestra Struttura JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4db77-196">tooadd a resource toohello template file, click **Add Resource** at hello top of hello JSON Outline window.</span></span> <span data-ttu-id="4db77-197">Nella finestra Struttura JSON hello mouse oppure **risorse**e selezionare **Aggiungi nuova risorsa**.</span><span class="sxs-lookup"><span data-stu-id="4db77-197">Or in hello JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Finestra Struttura JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="4db77-199">In hello **Aggiungi risorsa** la finestra di dialogo, trovare e selezionare **logica App**.</span><span class="sxs-lookup"><span data-stu-id="4db77-199">In hello **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="4db77-200">Dare un nome all'app per la logica e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="4db77-200">Name your logic app, and choose **Add**.</span></span>

    ![Aggiungere una risorsa](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="4db77-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4db77-202">Next Steps</span></span>

* [<span data-ttu-id="4db77-203">Gestire le app per la logica con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="4db77-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="4db77-204">Visualizzare esempi e scenari comuni</span><span class="sxs-lookup"><span data-stu-id="4db77-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="4db77-205">Informazioni su come i processi di business tooautomate con Azure logica App</span><span class="sxs-lookup"><span data-stu-id="4db77-205">Learn how tooautomate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="4db77-206">Informazioni su come toointegrate i sistemi con Azure logica App</span><span class="sxs-lookup"><span data-stu-id="4db77-206">Learn how toointegrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
