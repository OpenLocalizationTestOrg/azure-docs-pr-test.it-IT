---
title: modello di Azure Resource Manager aaaExport | Documenti Microsoft
description: Utilizzare Gestione risorse di Azure tooexport un modello da un gruppo di risorse esistente.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 5f5ca940-eef8-4125-b6a0-f44ba04ab5ab
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/06/2017
ms.author: tomfitz
ms.openlocfilehash: 94daa4812da2fec705044ca31c8e74e6d59bd53f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="9475b-103">Esportare un modello di Azure Resource Manager da risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="9475b-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="9475b-104">In questo articolo viene illustrato come tooexport un modello di gestione risorse da risorse esistenti nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9475b-104">In this article, you learn how tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="9475b-105">È possibile utilizzare tale toogain modello generato una migliore comprensione della sintassi dei modelli.</span><span class="sxs-lookup"><span data-stu-id="9475b-105">You can use that generated template toogain a better understanding of template syntax.</span></span>

<span data-ttu-id="9475b-106">Esistono due modi tooexport un modello:</span><span class="sxs-lookup"><span data-stu-id="9475b-106">There are two ways tooexport a template:</span></span>

* <span data-ttu-id="9475b-107">È possibile esportare hello **modello effettivo utilizzato per la distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="9475b-107">You can export hello **actual template used for deployment**.</span></span> <span data-ttu-id="9475b-108">modello esportato Hello include tutti i parametri di hello e variabili, esattamente come appaiono nel modello originale hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="9475b-109">Questo approccio è utile per la distribuzione di risorse tramite il portale di hello e desidera toosee hello modello toocreate tali risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-109">This approach is helpful when you deployed resources through hello portal, and want toosee hello template toocreate those resources.</span></span> <span data-ttu-id="9475b-110">Il modello è immediatamente utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="9475b-110">This template is readily usable.</span></span> 
* <span data-ttu-id="9475b-111">È possibile esportare un **generato modello che rappresenta lo stato corrente di hello hello del gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="9475b-111">You can export a **generated template that represents hello current state of hello resource group**.</span></span> <span data-ttu-id="9475b-112">modello esportato Hello non è basato su qualsiasi modello utilizzato per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-112">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="9475b-113">Al contrario, viene creato un modello che è uno snapshot hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-113">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="9475b-114">modello esportato Hello molti valori hardcoded e probabilmente non tutti i parametri in genere è possibile definire.</span><span class="sxs-lookup"><span data-stu-id="9475b-114">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="9475b-115">Questo approccio è utile quando è stato modificato il gruppo di risorse hello dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-115">This approach is useful when you have modified hello resource group after deployment.</span></span> <span data-ttu-id="9475b-116">Il modello richiede in genere modifiche prima di poter essere usato.</span><span class="sxs-lookup"><span data-stu-id="9475b-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="9475b-117">Questo argomento vengono illustrati entrambi gli approcci tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-117">This topic shows both approaches through hello portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="9475b-118">Distribuire le risorse</span><span class="sxs-lookup"><span data-stu-id="9475b-118">Deploy resources</span></span>
<span data-ttu-id="9475b-119">Iniziamo distribuendo tooAzure risorse che è possibile utilizzare per l'esportazione come modello.</span><span class="sxs-lookup"><span data-stu-id="9475b-119">Let's start by deploying resources tooAzure that you can use for exporting as a template.</span></span> <span data-ttu-id="9475b-120">Se si dispone già di un gruppo di risorse nella sottoscrizione che si desidera tooexport tooa modello, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9475b-120">If you already have a resource group in your subscription that you want tooexport tooa template, you can skip this section.</span></span> <span data-ttu-id="9475b-121">resto Hello di questo articolo si presuppone che è stato distribuito hello web app e soluzioni di database SQL illustrate in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9475b-121">hello remainder of this article assumes you have deployed hello web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="9475b-122">Se si utilizza una soluzione diversa, l'esperienza potrebbe essere leggermente diversa, ma i passaggi di hello tooexport un modello sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="9475b-122">If you use a different solution, your experience might be a little different, but hello steps tooexport a template are hello same.</span></span> 

1. <span data-ttu-id="9475b-123">In hello [portale di Azure](https://portal.azure.com)selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="9475b-123">In hello [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![Selezionare Nuovo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="9475b-125">Cercare **web app + SQL** e selezionare le opzioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-125">Search for **web app + SQL** and select it from hello available options.</span></span>
   
      ![Cercare App Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="9475b-127">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9475b-127">Select **Create**.</span></span>

      ![Selezionare Crea](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="9475b-129">Fornire valori hello necessario per hello web app e il database SQL.</span><span class="sxs-lookup"><span data-stu-id="9475b-129">Provide hello required values for hello web app and SQL database.</span></span> <span data-ttu-id="9475b-130">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9475b-130">Select **Create**.</span></span>

      ![Specificare i valori per Web e SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="9475b-132">distribuzione di Hello potrebbe richiedere un minuto.</span><span class="sxs-lookup"><span data-stu-id="9475b-132">hello deployment may take a minute.</span></span> <span data-ttu-id="9475b-133">Al termine della distribuzione di hello, la sottoscrizione contiene la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-133">After hello deployment finishes, your subscription contains hello solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="9475b-134">Visualizzare il modello dalla cronologia delle distribuzioni</span><span class="sxs-lookup"><span data-stu-id="9475b-134">View template from deployment history</span></span>
1. <span data-ttu-id="9475b-135">Andare a pannello di gruppo di risorse toohello per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-135">Go toohello resource group blade for your new resource group.</span></span> <span data-ttu-id="9475b-136">Si noti che pannello hello illustra il risultato di hello dell'ultima distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-136">Notice that hello blade shows hello result of hello last deployment.</span></span> <span data-ttu-id="9475b-137">Selezionare questo collegamento.</span><span class="sxs-lookup"><span data-stu-id="9475b-137">Select this link.</span></span>
   
      ![pannello Gruppo di risorse](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="9475b-139">Visualizzare una cronologia delle distribuzioni per il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-139">You see a history of deployments for hello group.</span></span> <span data-ttu-id="9475b-140">Il caso, il pannello hello Elenca probabilmente solo una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-140">In your case, hello blade probably lists only one deployment.</span></span> <span data-ttu-id="9475b-141">Selezionare questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-141">Select this deployment.</span></span>
   
     ![ultima distribuzione](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="9475b-143">Pannello Hello Visualizza un riepilogo della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-143">hello blade displays a summary of hello deployment.</span></span> <span data-ttu-id="9475b-144">Hello riepilogo include stato hello della distribuzione di hello e relativi valori di hello forniti per i parametri e operazioni.</span><span class="sxs-lookup"><span data-stu-id="9475b-144">hello summary includes hello status of hello deployment and its operations and hello values that you provided for parameters.</span></span> <span data-ttu-id="9475b-145">modello di hello toosee utilizzato per la distribuzione di hello, seleziona **modello di visualizzazione**.</span><span class="sxs-lookup"><span data-stu-id="9475b-145">toosee hello template that you used for hello deployment, select **View template**.</span></span>
   
     ![visualizzare il riepilogo della distribuzione](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="9475b-147">Gestione risorse recupera hello i seguenti sette file automaticamente:</span><span class="sxs-lookup"><span data-stu-id="9475b-147">Resource Manager retrieves hello following seven files for you:</span></span>
   
   1. <span data-ttu-id="9475b-148">**Modello** -modello hello che definisce l'infrastruttura di hello per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-148">**Template** - hello template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="9475b-149">Durante la creazione di account di archiviazione hello tramite il portale di hello, Gestione risorse utilizzato toodeploy un modello e salvato il modello per riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="9475b-149">When you created hello storage account through hello portal, Resource Manager used a template toodeploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="9475b-150">**I parametri** -un file di parametri che è possibile usare nei valori toopass durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-150">**Parameters** - A parameter file that you can use toopass in values during deployment.</span></span> <span data-ttu-id="9475b-151">Contiene valori hello forniti durante la distribuzione prima di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-151">It contains hello values that you provided during hello first deployment.</span></span> <span data-ttu-id="9475b-152">È possibile modificare questi valori quando si ridistribuisce il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-152">You can change any of these values when you redeploy hello template.</span></span>
   3. <span data-ttu-id="9475b-153">**CLI** -file script di Azure un'interfaccia di riga comando (CLI) che è possibile utilizzare il modello di hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   3. <span data-ttu-id="9475b-154">**2.0 CLI** -file script di Azure un'interfaccia di riga comando (CLI) che è possibile utilizzare il modello di hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use toodeploy hello template.</span></span>
   4. <span data-ttu-id="9475b-155">**PowerShell** -file di script di PowerShell di Azure che è possibile utilizzare il modello di hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-155">**PowerShell** - An Azure PowerShell script file that you can use toodeploy hello template.</span></span>
   5. <span data-ttu-id="9475b-156">**.NET** -classe di oggetto .NET che è possibile utilizzare il modello di hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-156">**.NET** - A .NET class that you can use toodeploy hello template.</span></span>
   6. <span data-ttu-id="9475b-157">**Ruby** -classe A Ruby che è possibile utilizzare il modello di hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-157">**Ruby** - A Ruby class that you can use toodeploy hello template.</span></span>
      
      <span data-ttu-id="9475b-158">file Hello sono disponibili tramite i collegamenti tra blade hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-158">hello files are available through links across hello blade.</span></span> <span data-ttu-id="9475b-159">Per impostazione predefinita, il pannello hello Visualizza modello hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-159">By default, hello blade displays hello template.</span></span>
      
       ![Visualizza modello](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="9475b-161">Questo modello è modello effettivo hello utilizzato toocreate l'app web e database SQL.</span><span class="sxs-lookup"><span data-stu-id="9475b-161">This template is hello actual template used toocreate your web app and SQL database.</span></span> <span data-ttu-id="9475b-162">Si noti che contiene i parametri che consentono di valori diversi tooprovide durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-162">Notice it contains parameters that enable you tooprovide different values during deployment.</span></span> <span data-ttu-id="9475b-163">toolearn ulteriori informazioni su struttura hello di un modello, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9475b-163">toolearn more about hello structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-hello-template-from-resource-group"></a><span data-ttu-id="9475b-164">Esportare il modello di hello dal gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9475b-164">Export hello template from resource group</span></span>
<span data-ttu-id="9475b-165">Se si manualmente hanno modificato le risorse o aggiunta di risorse in più distribuzioni, il recupero di un modello dalla cronologia della distribuzione di hello non riflette lo stato corrente di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from hello deployment history does not reflect hello current state of hello resource group.</span></span> <span data-ttu-id="9475b-166">In questa sezione viene illustrato come un modello che rispecchia tooexport hello stato corrente del gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-166">This section shows you how tooexport a template that reflects hello current state of hello resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="9475b-167">Non è possibile esportare un modello per un gruppo di risorse con più di 200 risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="9475b-168">modello di hello tooview per un gruppo di risorse, seleziona **script di automazione**.</span><span class="sxs-lookup"><span data-stu-id="9475b-168">tooview hello template for a resource group, select **Automation script**.</span></span>
   
      ![esportare un gruppo di risorse](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="9475b-170">Gestione risorse analizza hello le risorse nel gruppo di risorse hello e genera un modello per tali risorse.</span><span class="sxs-lookup"><span data-stu-id="9475b-170">Resource Manager evaluates hello resources in hello resource group, and generates a template for those resources.</span></span> <span data-ttu-id="9475b-171">Non tutti i tipi di risorse supportano la funzione di modello di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-171">Not all resource types support hello export template function.</span></span> <span data-ttu-id="9475b-172">Potrebbe essere visualizzato un errore che informa che si è verificato un problema con l'esportazione di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-172">You may see an error stating that there is a problem with hello export.</span></span> <span data-ttu-id="9475b-173">Si apprenderà come toohandle tali problemi nel hello [esportazione problemi](#fix-export-issues) sezione.</span><span class="sxs-lookup"><span data-stu-id="9475b-173">You learn how toohandle those issues in hello [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="9475b-174">Vedrai nuovamente sei file hello che è possibile utilizzare soluzioni hello tooredeploy.</span><span class="sxs-lookup"><span data-stu-id="9475b-174">You again see hello six files that you can use tooredeploy hello solution.</span></span> <span data-ttu-id="9475b-175">Tuttavia, questo modello in fase di hello è leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="9475b-175">However, this time hello template is a little different.</span></span> <span data-ttu-id="9475b-176">Si noti che il modello hello generato contiene meno parametri di modello hello nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="9475b-176">Notice that hello generated template contains fewer parameters than hello template in previous section.</span></span> <span data-ttu-id="9475b-177">Inoltre, molti dei valori di hello (ad esempio, percorso e i valori di SKU) sono hardcoded in questo modello, piuttosto che accetta un valore di parametro.</span><span class="sxs-lookup"><span data-stu-id="9475b-177">Also, many of hello values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="9475b-178">Prima di riutilizzare questo modello, è opportuno tooedit hello modello toomake migliorare l'utilizzo di parametri.</span><span class="sxs-lookup"><span data-stu-id="9475b-178">Before reusing this template, you might want tooedit hello template toomake better use of parameters.</span></span> 
   
3. <span data-ttu-id="9475b-179">Sono disponibili due opzioni per la continuazione toowork con questo modello.</span><span class="sxs-lookup"><span data-stu-id="9475b-179">You have a couple of options for continuing toowork with this template.</span></span> <span data-ttu-id="9475b-180">È possibile scaricare il modello di hello e lavorare localmente su di esso con un editor di JSON.</span><span class="sxs-lookup"><span data-stu-id="9475b-180">You can either download hello template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="9475b-181">In alternativa, è possibile salvare hello modello tooyour raccolta e il lavoro tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-181">Or, you can save hello template tooyour library and work on it through hello portal.</span></span>
   
     <span data-ttu-id="9475b-182">Se si ha familiarità con un editor di JSON come [Visual Studio Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), è preferibile scaricare modello hello in locale e utilizzare tale editor.</span><span class="sxs-lookup"><span data-stu-id="9475b-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading hello template locally and using that editor.</span></span> <span data-ttu-id="9475b-183">toowork in locale, selezionare **scaricare**.</span><span class="sxs-lookup"><span data-stu-id="9475b-183">toowork locally, select **Download**.</span></span>
   
      ![scaricare il modello](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="9475b-185">Se non è configurato con un editor di JSON, è preferibile modificare hello modello tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-185">If you are not set up with a JSON editor, you might prefer editing hello template through hello portal.</span></span> <span data-ttu-id="9475b-186">resto Hello di questo argomento si presuppone che è stato salvato libreria tooyour di hello modelli nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-186">hello remainder of this topic assumes you have saved hello template tooyour library in hello portal.</span></span> <span data-ttu-id="9475b-187">Tuttavia, si apportano hello stesso modello toohello modifiche di sintassi se si lavora in locale con un editor di JSON o tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-187">However, you make hello same syntax changes toohello template whether working locally with a JSON editor or through hello portal.</span></span> <span data-ttu-id="9475b-188">Selezionare toowork tramite il portale di hello **aggiungere toolibrary**.</span><span class="sxs-lookup"><span data-stu-id="9475b-188">toowork through hello portal, select **Add toolibrary**.</span></span>
   
      ![aggiungere toolibrary](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="9475b-190">Quando si aggiunge una raccolta di modelli di toohello, assegnare il modello di hello un nome e una descrizione.</span><span class="sxs-lookup"><span data-stu-id="9475b-190">When adding a template toohello library, give hello template a name and description.</span></span> <span data-ttu-id="9475b-191">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9475b-191">Then, select **Save**.</span></span>
   
     ![impostare i valori di modello](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="9475b-193">tooview un modello salvato nella libreria, selezionare **più servizi**, tipo **modelli** toofilter risultati, selezionare **modelli**.</span><span class="sxs-lookup"><span data-stu-id="9475b-193">tooview a template saved in your library, select **More services**, type **Templates** toofilter results, select **Templates**.</span></span>
   
      ![trovare i modelli](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="9475b-195">Selezionare il modello di hello con nome hello che è stato salvato.</span><span class="sxs-lookup"><span data-stu-id="9475b-195">Select hello template with hello name you saved.</span></span>
   
      ![selezionare modello](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-hello-template"></a><span data-ttu-id="9475b-197">Personalizzare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="9475b-197">Customize hello template</span></span>
<span data-ttu-id="9475b-198">funzionamento del modello Hello esportata correttamente che se si desidera toocreate hello stesso web app e il database SQL per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-198">hello exported template works fine if you want toocreate hello same web app and SQL database for every deployment.</span></span> <span data-ttu-id="9475b-199">Le opzioni disponibili in Resource Manager consentono, tuttavia, di distribuire modelli con maggiore flessibilità.</span><span class="sxs-lookup"><span data-stu-id="9475b-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="9475b-200">Questo articolo illustra come parametri tooadd per hello database password e nome di amministratore.</span><span class="sxs-lookup"><span data-stu-id="9475b-200">This article shows you how tooadd parameters for hello database administrator name and password.</span></span> <span data-ttu-id="9475b-201">È possibile utilizzare questo stesso tooadd approccio una maggiore flessibilità per gli altri valori nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-201">You can use this same approach tooadd more flexibility for other values in hello template.</span></span>

1. <span data-ttu-id="9475b-202">modello di hello toocustomize, selezionare **modifica**.</span><span class="sxs-lookup"><span data-stu-id="9475b-202">toocustomize hello template, select **Edit**.</span></span>
   
     ![visualizzare il modello](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="9475b-204">Selezionare il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-204">Select hello template.</span></span>
   
     ![modificare un modello](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="9475b-206">i valori hello in grado di toopass toobe che è possibile toospecify durante la distribuzione, aggiungere hello seguenti due parametri toohello **parametri** sezione nel modello hello:</span><span class="sxs-lookup"><span data-stu-id="9475b-206">toobe able toopass hello values that you might want toospecify during deployment, add hello following two parameters toohello **parameters** section in hello template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="9475b-207">nuovi parametri hello toouse, sostituire la definizione di hello SQL server in hello **risorse** sezione.</span><span class="sxs-lookup"><span data-stu-id="9475b-207">toouse hello new parameters, replace hello SQL server definition in hello **resources** section.</span></span> <span data-ttu-id="9475b-208">Si noti che in **administratorLogin** e **administratorLoginPassword** vengono ora usati valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="9475b-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

   ```json
   {
       "comments": "Generalized from resource: '/subscriptions/{subscription-id}/resourceGroups/exportsite/providers/Microsoft.Sql/servers/tfserverexport'.",
       "type": "Microsoft.Sql/servers",
       "kind": "v12.0",
       "name": "[parameters('servers_tfserverexport_name')]",
       "apiVersion": "2014-04-01-preview",
       "location": "South Central US",
       "scale": null,
       "properties": {
           "administratorLogin": "[parameters('administratorLogin')]",
           "administratorLoginPassword": "[parameters('administratorLoginPassword')]",
           "version": "12.0"
       },
       "dependsOn": []
   },
   ```

6. <span data-ttu-id="9475b-209">Selezionare **OK** al termine modifica modello hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-209">Select **OK** when you are done editing hello template.</span></span>
7. <span data-ttu-id="9475b-210">Selezionare **salvare** modello toohello di toosave hello le modifiche.</span><span class="sxs-lookup"><span data-stu-id="9475b-210">Select **Save** toosave hello changes toohello template.</span></span>
   
     ![salvare il modello](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="9475b-212">modello di hello aggiornato tooredeploy, selezionare **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="9475b-212">tooredeploy hello updated template, select **Deploy**.</span></span>
   
     ![distribuire un modello](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="9475b-214">Fornire i valori dei parametri e selezionare un gruppo toodeploy hello di risorse per.</span><span class="sxs-lookup"><span data-stu-id="9475b-214">Provide parameter values, and select a resource group toodeploy hello resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="9475b-215">Risolvere i problemi di esportazione</span><span class="sxs-lookup"><span data-stu-id="9475b-215">Fix export issues</span></span>
<span data-ttu-id="9475b-216">Non tutti i tipi di risorse supportano la funzione di modello di esportazione hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-216">Not all resource types support hello export template function.</span></span> <span data-ttu-id="9475b-217">Questo problema, manualmente tooresolve aggiungere risorse mancanti hello nuovamente nel modello.</span><span class="sxs-lookup"><span data-stu-id="9475b-217">tooresolve this issue, manually add hello missing resources back into your template.</span></span> <span data-ttu-id="9475b-218">messaggio di errore Hello include i tipi di risorsa hello che non possono essere esportati.</span><span class="sxs-lookup"><span data-stu-id="9475b-218">hello error message includes hello resource types that cannot be exported.</span></span> <span data-ttu-id="9475b-219">Trovare il tipo di risorsa nelle [informazioni di riferimento sui modelli](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="9475b-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="9475b-220">Ad esempio, di aggiungere un gateway di rete virtuale, vedere toomanually [riferimento a un modello Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="9475b-220">For example, toomanually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="9475b-221">Si verificano problemi di esportazione solo quando si esporta da un gruppo di risorse invece che dalla cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="9475b-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="9475b-222">Se l'ultima distribuzione in modo accurato rappresenta lo stato corrente di hello hello del gruppo di risorse, è necessario esportare il modello di hello dalla cronologia della distribuzione hello anziché dal gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-222">If your last deployment accurately represents hello current state of hello resource group, you should export hello template from hello deployment history rather than from hello resource group.</span></span> <span data-ttu-id="9475b-223">Esportare solo da un gruppo di risorse quando sono state apportate gruppo di risorse toohello modifiche che non sono definiti in un unico modello.</span><span class="sxs-lookup"><span data-stu-id="9475b-223">Only export from a resource group when you have made changes toohello resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="9475b-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9475b-224">Next steps</span></span>
<span data-ttu-id="9475b-225">Si è appreso come tooexport un modello dalle risorse di cui è stato creato nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9475b-225">You have learned how tooexport a template from resources that you created in hello portal.</span></span>

* <span data-ttu-id="9475b-226">È possibile distribuire un modello tramite [PowerShell](resource-group-template-deploy.md), l'[interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md) o l'[API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="9475b-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="9475b-227">toosee tooexport un modello tramite PowerShell, vedere [tramite Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9475b-227">toosee how tooexport a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="9475b-228">toosee tooexport un modello tramite l'interfaccia CLI di Azure, vedere [hello utilizzare CLI di Azure per Mac, Linux e Windows con Gestione risorse di Azure](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9475b-228">toosee how tooexport a template through Azure CLI, see [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

