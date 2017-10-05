---
title: Creare, compilare e distribuire le app per la logica in Visual Studio - App per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: e7f5cf483d22e4c60dedbe5176ceb0bc8b2b6e66
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="design-build-and-deploy-azure-logic-apps-in-visual-studio"></a><span data-ttu-id="f2aa2-103">Progettare, compilare e distribuire app per la logica di Azure in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2aa2-103">Design, build, and deploy Azure Logic Apps in Visual Studio</span></span>

<span data-ttu-id="f2aa2-104">Anche se il [portale di Azure](https://portal.azure.com/) è uno strumento eccellente per la creazione e la gestione delle app per la logica di Azure, è possibile usare Visual Studio per progettarle, compilarle e distribuirle.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-104">Although the [Azure portal](https://portal.azure.com/) offers a great way for you to create and manage Azure Logic Apps, you can use Visual Studio for designing, building, and deploying your logic apps.</span></span> <span data-ttu-id="f2aa2-105">Visual Studio offre strumenti avanzati, come la finestra di progettazione di app per la logica, per creare app per la logica, configurare i modelli di distribuzione e automazione e distribuirli in qualsiasi ambiente.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-105">Visual Studio provides rich tools like the Logic App Designer for you to create logic apps, configure deployment and automation templates, and deploy to any environment.</span></span> 

<span data-ttu-id="f2aa2-106">Per un'introduzione alle app per la logica di Azure, imparare a [creare la prima app per la logica nel Portale di Azure](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f2aa2-106">To get started with Azure Logic Apps, learn [how to create your first logic app in the Azure portal](logic-apps-create-a-logic-app.md).</span></span>

## <a name="installation-steps"></a><span data-ttu-id="f2aa2-107">Procedura di installazione</span><span class="sxs-lookup"><span data-stu-id="f2aa2-107">Installation steps</span></span>

<span data-ttu-id="f2aa2-108">Per installare e configurare gli strumenti di Visual Studio per le app per la logica di Azure, seguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-108">To install and configure Visual Studio tools for Azure Logic Apps, follow these steps.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f2aa2-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f2aa2-109">Prerequisites</span></span>

* <span data-ttu-id="f2aa2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) o Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="f2aa2-110">[Visual Studio 2017](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) or Visual Studio 2015</span></span>
* <span data-ttu-id="f2aa2-111">[Versione più recente di Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 o versione successiva)</span><span class="sxs-lookup"><span data-stu-id="f2aa2-111">[Latest Azure SDK](https://azure.microsoft.com/downloads/) (2.9.1 or greater)</span></span>
* [<span data-ttu-id="f2aa2-112">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2aa2-112">Azure PowerShell</span></span>](https://github.com/Azure/azure-powershell#installation)
* <span data-ttu-id="f2aa2-113">Accesso al Web mentre viene usata la finestra di progettazione incorporata</span><span class="sxs-lookup"><span data-stu-id="f2aa2-113">Access to the web when using the embedded designer</span></span>

### <a name="install-visual-studio-tools-for-azure-logic-apps"></a><span data-ttu-id="f2aa2-114">Installare gli strumenti di Visual Studio per le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="f2aa2-114">Install Visual Studio tools for Azure Logic Apps</span></span>

<span data-ttu-id="f2aa2-115">Dopo aver installato i prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-115">After you install the prerequisites:</span></span>

1. <span data-ttu-id="f2aa2-116">Aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-116">Open Visual Studio.</span></span> <span data-ttu-id="f2aa2-117">Scegliere **Estensioni e aggiornamenti** dal menu **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-117">On the **Tools** menu, select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="f2aa2-118">Espandere la categoria **In rete** per poter eseguire le ricerche in rete.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-118">Expand the **Online** category so you can search online.</span></span>
3. <span data-ttu-id="f2aa2-119">Sfogliare o cercare **App per la logica** per visualizzare **Azure Logic Apps Tools for Visual Studio** (Strumenti per app per la logica di Azure per Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="f2aa2-119">Browse or search for **Logic Apps** until you find **Azure Logic Apps Tools for Visual Studio**.</span></span>
4. <span data-ttu-id="f2aa2-120">Fare clic sul pulsante **Scarica** per scaricare e installare l'estensione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-120">To download and install the extension, click **Download**.</span></span>
5. <span data-ttu-id="f2aa2-121">Al termine dell'installazione riavviare Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-121">Restart Visual Studio after installation.</span></span>

> [!NOTE]
> <span data-ttu-id="f2aa2-122">È anche possibile scaricare gli [strumenti per Visual Studio 2017 di app per la logica di Azure](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) e gli [strumenti per Visual Studio 2015 di app per la logica di Azure](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) direttamente da Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-122">You can also download [Azure Logic Apps Tools for Visual Studio 2017](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio-18551) and the [Azure Logic Apps Tools for Visual Studio 2015](https://marketplace.visualstudio.com/items?itemName=VinaySinghMSFT.AzureLogicAppsToolsforVisualStudio) directly from the Visual Studio Marketplace.</span></span>

<span data-ttu-id="f2aa2-123">Al completamento dell'installazione è possibile usare il progetto Gruppo di risorse di Azure con la Progettazione delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-123">After you finish installation, you can use the Azure Resource Group project with Logic App Designer.</span></span>

## <a name="create-your-project"></a><span data-ttu-id="f2aa2-124">Creare il progetto</span><span class="sxs-lookup"><span data-stu-id="f2aa2-124">Create your project</span></span>

1. <span data-ttu-id="f2aa2-125">Nel menu **File**, andare in **Nuovo**e selezionare **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-125">On the **File** menu, go to **New**, and select **Project**.</span></span> <span data-ttu-id="f2aa2-126">Oppure per aggiungere il progetto a una soluzione esistente, andare in **Aggiungi**e selezionare **Nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-126">Or to add your project to an existing solution, go to **Add**, and select **New Project**.</span></span>

    ![File menu](./media/logic-apps-deploy-from-vs/filemenu.png)

2. <span data-ttu-id="f2aa2-128">Nella finestra **Nuovo progetto** cercare **Cloud** e selezionare **Gruppo di risorse di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-128">In the **New Project** window, find **Cloud**, and select **Azure Resource Group**.</span></span> <span data-ttu-id="f2aa2-129">Assegnare un nome al progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-129">Name your project, and click **OK**.</span></span>

    ![Add new project](./media/logic-apps-deploy-from-vs/addnewproject.png)

3. <span data-ttu-id="f2aa2-131">Selezionare il modello **App per la logica** che crea un modello di distribuzione delle app per la logica vuoto che è possibile usare.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-131">Select the **Logic App** template, which creates a blank logic app deployment template for you to use.</span></span> <span data-ttu-id="f2aa2-132">Dopo aver selezionato il modello, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-132">After you select your template, click **OK**.</span></span>

    ![Selezionare il modello App per la logica](./media/logic-apps-deploy-from-vs/selectazuretemplate1.png)

    <span data-ttu-id="f2aa2-134">Il progetto di app per la logica viene aggiunto alla soluzione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-134">You've now added your logic app project to your solution.</span></span> 
    <span data-ttu-id="f2aa2-135">Il file di distribuzione verrà visualizzato in Esplora soluzioni.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-135">In the Solution Explorer, your deployment file should appear.</span></span>

    ![File di distribuzione](./media/logic-apps-deploy-from-vs/deployment.png)

## <a name="create-your-logic-app-with-logic-app-designer"></a><span data-ttu-id="f2aa2-137">Creare l'app per la logica con la finestra di progettazione</span><span class="sxs-lookup"><span data-stu-id="f2aa2-137">Create your logic app with Logic App Designer</span></span>

<span data-ttu-id="f2aa2-138">Dopo aver creato un progetto Gruppo di risorse di Azure contenente un'app per la logica, è possibile aprire Progettazione app per la logica in Visual Studio per creare il flusso di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-138">When you have an Azure Resource Group project that contains a logic app, you can open the Logic App Designer in Visual Studio to create your workflow.</span></span> 

> [!NOTE]
> <span data-ttu-id="f2aa2-139">La finestra di progettazione richiede una connessione internet ai connettori di query per i dati e le proprietà disponibili.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-139">The designer requires an internet connection to query connectors for available properties and data.</span></span> <span data-ttu-id="f2aa2-140">Ad esempio, se si utilizza il connettore di Dynamics CRM Online, la finestra di progettazione richiede l'istanza CRM per visualizzare le proprietà predefinite e personalizzate disponibili.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-140">For example, if you use the Dynamics CRM Online connector, the designer queries your CRM instance to show available custom and default properties.</span></span>

1. <span data-ttu-id="f2aa2-141">Fare clic con il pulsante destro del mouse sul file `<template>.json` e scegliere **Open with Logic App Designer** (Apri con Progettazione app per la logica).</span><span class="sxs-lookup"><span data-stu-id="f2aa2-141">Right-click your `<template>.json` file, and select **Open with Logic App Designer**.</span></span> <span data-ttu-id="f2aa2-142">(`Ctrl+L`)</span><span class="sxs-lookup"><span data-stu-id="f2aa2-142">(`Ctrl+L`)</span></span>

2. <span data-ttu-id="f2aa2-143">Scegliere la sottoscrizione di Azure, il gruppo di risorse e la posizione per il modello di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-143">Choose your Azure subscription, resource group, and location for your deployment template.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2aa2-144">Progettando un'app per la logica verranno create risorse di connessione API per l'esecuzione di query per ottenere le proprietà durante la progettazione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-144">Designing a logic app creates API Connection resources that query for properties during design.</span></span> <span data-ttu-id="f2aa2-145">Il gruppo di risorse selezionato viene usato da Visual Studio per creare tali connessioni durante la fase di progettazione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-145">Visual Studio uses your selected resource group to create those connections during design time.</span></span> <span data-ttu-id="f2aa2-146">Per visualizzare o modificare qualsiasi connessione API, andare nel Portale di Azure e cercare **Connessioni API**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-146">To view or change any API Connections, go to the Azure portal, and browse for **API Connections**.</span></span>

    ![Selezione della sottoscrizione](./media/logic-apps-deploy-from-vs/designer_picker.png)

    <span data-ttu-id="f2aa2-148">La finestra di progettazione usa la definizione nel file `<template>.json` per il rendering.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-148">The designer uses the definition in the `<template>.json` file for rendering.</span></span>

4. <span data-ttu-id="f2aa2-149">Creare e progettare l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-149">Create and design your logic app.</span></span> <span data-ttu-id="f2aa2-150">Il modello di distribuzione viene aggiornato con le modifiche.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-150">Your deployment template is updated with your changes.</span></span>

    ![Progettazione app per la logica in Visual Studio](./media/logic-apps-deploy-from-vs/designer_in_vs.png)

<span data-ttu-id="f2aa2-152">Visual Studio aggiunge le risorse `Microsoft.Web/connections` al file di risorse per tutte le connessioni necessarie all'app per la logica per funzionare.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-152">Visual Studio adds `Microsoft.Web/connections` resources to your resource file for any connections your logic app needs to function.</span></span> <span data-ttu-id="f2aa2-153">Queste proprietà di connessione possono essere impostate al momento della distribuzione ed essere gestite successivamente in **Connessioni API** nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-153">These connection properties can be set when you deploy, and managed after you deploy in **API Connections** in the Azure portal.</span></span>

### <a name="switch-to-json-code-view"></a><span data-ttu-id="f2aa2-154">Passare alla visualizzazione del codice JSON</span><span class="sxs-lookup"><span data-stu-id="f2aa2-154">Switch to JSON code view</span></span>

<span data-ttu-id="f2aa2-155">È possibile selezionare la scheda **Visualizzazione Codice** nella parte inferiore della finestra di progettazione per visualizzare la rappresentazione JSON dell'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-155">To show the JSON representation for your logic app, select the **Code View** tab at the bottom of the designer.</span></span>

<span data-ttu-id="f2aa2-156">Per tornare al file di risorse JSON completo, fare clic con il pulsante destro del mouse su `<template>.json` e scegliere **Apri**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-156">To switch back to the full resource JSON, right-click the `<template>.json` file, and select **Open**.</span></span>

### <a name="add-references-for-dependent-resources-to-visual-studio-deployment-templates"></a><span data-ttu-id="f2aa2-157">Aggiungere riferimenti per le risorse dipendenti ai modelli di distribuzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2aa2-157">Add references for dependent resources to Visual Studio deployment templates</span></span>

<span data-ttu-id="f2aa2-158">Quando si vuole che l'app per la logica faccia riferimento alle risorse dipendenti, è possibile usare le [funzioni del modello di Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) nel modello di distribuzione di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-158">When you want your logic app to reference dependent resources, you can use [Azure Resource Manager template functions](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-functions) in your logic app deployment template.</span></span> <span data-ttu-id="f2aa2-159">Ad esempio, l'utente può fare in modo che l'app per la logica faccia riferimento a una funzione di Azure o a un account di integrazione che si desidera distribuire insieme all'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-159">For example, you might want your logic app to reference an Azure Function or integration account that you want to deploy alongside your logic app.</span></span> <span data-ttu-id="f2aa2-160">Seguire queste linee guida sull'uso dei parametri nel modello di distribuzione in modo che la Progettazione app per la logica esegua il rendering correttamente.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-160">Follow these guidelines about how to use parameters in your deployment template so that the Logic App Designer renders correctly.</span></span> 

<span data-ttu-id="f2aa2-161">È possibile usare i parametri dell'app per la logica in questi tipi di trigger e azioni:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-161">You can use logic app parameters in these kinds of triggers and actions:</span></span>

*   <span data-ttu-id="f2aa2-162">Flusso di lavoro figlio</span><span class="sxs-lookup"><span data-stu-id="f2aa2-162">Child workflow</span></span>
*   <span data-ttu-id="f2aa2-163">App per le funzioni</span><span class="sxs-lookup"><span data-stu-id="f2aa2-163">Function app</span></span>
*   <span data-ttu-id="f2aa2-164">Chiamata APIM</span><span class="sxs-lookup"><span data-stu-id="f2aa2-164">APIM call</span></span>
*   <span data-ttu-id="f2aa2-165">URL di runtime della connessione API</span><span class="sxs-lookup"><span data-stu-id="f2aa2-165">API connection runtime URL</span></span>
*   <span data-ttu-id="f2aa2-166">Percorso di connessione API</span><span class="sxs-lookup"><span data-stu-id="f2aa2-166">API connection path</span></span>

<span data-ttu-id="f2aa2-167">Ed è possibile usare le funzioni di modello, ad esempio parametri, variabili, resourceId, CONCAT e così via. Ad esempio, ecco come è possibile sostituire l'ID di risorsa della funzione di Azure:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-167">And you can use template functions such as parameters, variables, resourceId, concat, etc. For example, here's how you can replace the Azure Function resource ID:</span></span>

```
"parameters":{
    "functionName": {
        "type":"string",
        "minLength":1,
        "defaultValue":"<FunctionName>"
    }
},
```

<span data-ttu-id="f2aa2-168">E dove si useranno i parametri:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-168">And where you would use parameters:</span></span>

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
<span data-ttu-id="f2aa2-169">È anche possibile, ad esempio, impostare il parametro per l'operazione di invio messaggio del bus di servizio:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-169">As another example you can parameterize the Service Bus send message operation:</span></span>

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
> <span data-ttu-id="f2aa2-170">host.runtimeUrl è facoltativo e può essere rimosso dal modello, se presente.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-170">host.runtimeUrl is optional and can be removed from your template if present.</span></span>
> 


> [!NOTE] 
> <span data-ttu-id="f2aa2-171">Affinché la Progettazione dell'app per la logica funzioni quando si usano i parametri, è necessario fornire valori predefiniti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="f2aa2-171">For the Logic App Designer to work when you use parameters, you must provide default values, for example:</span></span>
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

### <a name="save-your-logic-app"></a><span data-ttu-id="f2aa2-172">Salvare l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="f2aa2-172">Save your logic app</span></span>

<span data-ttu-id="f2aa2-173">Per salvare l'app per la logica in qualsiasi momento, andare in **File** > **Salva**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-173">To save your logic app at anytime, go to **File** > **Save**.</span></span> <span data-ttu-id="f2aa2-174">(`Ctrl+S`)</span><span class="sxs-lookup"><span data-stu-id="f2aa2-174">(`Ctrl+S`)</span></span> 

<span data-ttu-id="f2aa2-175">Se quando si salva l'applicazione l'app per la logica presenta errori, questi vengono visualizzati in Visual Studio nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-175">If your logic app has any errors when you save your app, they appear in the Visual Studio **Outputs** window.</span></span>

## <a name="deploy-your-logic-app-from-visual-studio"></a><span data-ttu-id="f2aa2-176">Distribuire l'app per la logica da Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2aa2-176">Deploy your logic app from Visual Studio</span></span>

<span data-ttu-id="f2aa2-177">Dopo aver configurato l'app, è possibile distribuirla direttamente da Visual Studio in pochi passaggi.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-177">After configuring your app, you can deploy directly from Visual Studio in just a couple steps.</span></span> 

1. <span data-ttu-id="f2aa2-178">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto e scegliere **Distribuisci** > **Nuova distribuzione...**</span><span class="sxs-lookup"><span data-stu-id="f2aa2-178">In Solution Explorer, right-click your project, and go to **Deploy** > **New Deployment...**</span></span>

    ![New deployment](./media/logic-apps-deploy-from-vs/newdeployment.png)

2. <span data-ttu-id="f2aa2-180">Quando verrà richiesto, accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-180">When you're prompted, sign in to your Azure subscription.</span></span> 

3. <span data-ttu-id="f2aa2-181">A questo punto è necessario selezionare i dettagli del gruppo di risorse in cui si desidera distribuire l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-181">Now you must select the details for the resource group where you want to deploy your logic app.</span></span> <span data-ttu-id="f2aa2-182">Al termine, fare clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-182">When you're done, select **Deploy**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2aa2-183">Assicurarsi di selezionare il modello e i parametri corretti per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-183">Make sure that you select the correct template and parameters file for the resource group.</span></span> <span data-ttu-id="f2aa2-184">Ad esempio, se si desidera distribuire in un ambiente di produzione, scegliere il file dei parametri di produzione.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-184">For example, if you want to deploy to a production environment, choose the production parameters file.</span></span>

    ![Deploy to resource group](./media/logic-apps-deploy-from-vs/deploytoresourcegroup.png)

    <span data-ttu-id="f2aa2-186">Lo stato di distribuzione viene visualizzato nella finestra **Output**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-186">The deployment status appears in the **Output** window.</span></span> 
    <span data-ttu-id="f2aa2-187">Potrebbe essere necessario selezionare **Provisioning Azure** nell'elenco **Mostra output di**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-187">You might have to select **Azure Provisioning** in the **Show output from** list.</span></span>

    ![Output dello stato di distribuzione](./media/logic-apps-deploy-from-vs/output.png)

<span data-ttu-id="f2aa2-189">In futuro sarà possibile modificare l'app per la logica nel controllo del codice sorgente e usare Visual Studio per distribuire nuove versioni.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-189">In the future, you can edit your logic app in source control, and use Visual Studio to deploy new versions.</span></span>

> [!NOTE]
> <span data-ttu-id="f2aa2-190">Se si modifica la definizione direttamente nel Portale di Azure, tali modifiche saranno sovrascritte alla successiva distribuzione da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-190">If you change the definition in the Azure portal directly, those changes are overwritten when you deploy from Visual Studio next time.</span></span> 

## <a name="add-your-logic-app-to-an-existing-resource-group-project"></a><span data-ttu-id="f2aa2-191">Aggiungere un'app per la logica a un progetto Gruppo di risorse esistente</span><span class="sxs-lookup"><span data-stu-id="f2aa2-191">Add your logic app to an existing Resource Group project</span></span>

<span data-ttu-id="f2aa2-192">Se si dispone di un progetto Gruppo di risorse esistente, è possibile aggiungere l'app per la logica al progetto nella finestra Struttura JSON.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-192">If you have an existing Resource Group project, you can add your logic app to that project in the JSON Outline window.</span></span> <span data-ttu-id="f2aa2-193">È inoltre possibile aggiungere un'altra app per la logica con l'applicazione creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-193">You can also add another logic app alongside the app you previously created.</span></span>

1. <span data-ttu-id="f2aa2-194">Aprire il file `<template>.json` .</span><span class="sxs-lookup"><span data-stu-id="f2aa2-194">Open the `<template>.json` file.</span></span>

2. <span data-ttu-id="f2aa2-195">Per aprire la finestra Struttura JSON andare in **Visualizza** > **Altre finestre** > **Struttura JSON**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-195">To open the JSON Outline window, go to **View** > **Other Windows** > **JSON Outline**.</span></span>

3. <span data-ttu-id="f2aa2-196">Per aggiungere una risorsa al file del modello, fare clic su **Aggiungi risorsa** nella parte superiore della finestra Struttura JSON.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-196">To add a resource to the template file, click **Add Resource** at the top of the JSON Outline window.</span></span> <span data-ttu-id="f2aa2-197">Oppure nella finestra Struttura JSON fare clic con il tasto destro del mouse su **risorse**e selezionare **Aggiungi nuova risorsa**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-197">Or in the JSON Outline window, right-click **resources**, and select **Add New Resource**.</span></span>

    ![Finestra Struttura JSON](./media/logic-apps-deploy-from-vs/jsonoutline.png)
    
4. <span data-ttu-id="f2aa2-199">Nella finestra di dialogo **Aggiungi risorsa**, individuare e selezionare **App per la logica**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-199">In the **Add Resource** dialog box, find and select **Logic App**.</span></span> <span data-ttu-id="f2aa2-200">Dare un nome all'app per la logica e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="f2aa2-200">Name your logic app, and choose **Add**.</span></span>

    ![Aggiungere una risorsa](./media/logic-apps-deploy-from-vs/addresource.png)

## <a name="next-steps"></a><span data-ttu-id="f2aa2-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f2aa2-202">Next Steps</span></span>

* [<span data-ttu-id="f2aa2-203">Gestire le app per la logica con Visual Studio Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="f2aa2-203">Manage logic apps with Visual Studio Cloud Explorer</span></span>](logic-apps-manage-from-vs.md)
* [<span data-ttu-id="f2aa2-204">Visualizzare esempi e scenari comuni</span><span class="sxs-lookup"><span data-stu-id="f2aa2-204">View common examples and scenarios</span></span>](logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="f2aa2-205">Introduzione all'automazione dei processi aziendali con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="f2aa2-205">Learn how to automate business processes with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/T694)
* [<span data-ttu-id="f2aa2-206">Informazioni su come integrare i sistemi con le app per la logica di Azure</span><span class="sxs-lookup"><span data-stu-id="f2aa2-206">Learn how to integrate your systems with Azure Logic Apps</span></span>](http://channel9.msdn.com/Events/Build/2016/P462)
