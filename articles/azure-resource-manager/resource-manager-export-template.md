---
title: Esportare il modello di Azure Resource Manager | Documentazione Microsoft
description: Usare Azure Resource Manager per esportare un modello da un gruppo di risorse esistente.
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
ms.openlocfilehash: 1801ef47e5b182e0bcd5b23970a2999633b4a852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="export-an-azure-resource-manager-template-from-existing-resources"></a><span data-ttu-id="ff05f-103">Esportare un modello di Azure Resource Manager da risorse esistenti</span><span class="sxs-lookup"><span data-stu-id="ff05f-103">Export an Azure Resource Manager template from existing resources</span></span>
<span data-ttu-id="ff05f-104">Questo articolo illustra come esportare un modello di Resource Manager dalle risorse esistenti della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-104">In this article, you learn how to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="ff05f-105">Il modello generato può essere usato per comprendere meglio la sintassi del modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-105">You can use that generated template to gain a better understanding of template syntax.</span></span>

<span data-ttu-id="ff05f-106">Per esportare un modello sono disponibili due modi:</span><span class="sxs-lookup"><span data-stu-id="ff05f-106">There are two ways to export a template:</span></span>

* <span data-ttu-id="ff05f-107">È possibile esportare il **modello effettivo usato per la distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-107">You can export the **actual template used for deployment**.</span></span> <span data-ttu-id="ff05f-108">Il modello esportato include tutti i parametri e le variabili uguali a quelli visualizzati nel modello originale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="ff05f-109">Questo approccio è utile quando si sono distribuite risorse tramite il portale e si vuole visualizzare il modello con cui sono state create.</span><span class="sxs-lookup"><span data-stu-id="ff05f-109">This approach is helpful when you deployed resources through the portal, and want to see the template to create those resources.</span></span> <span data-ttu-id="ff05f-110">Il modello è immediatamente utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="ff05f-110">This template is readily usable.</span></span> 
* <span data-ttu-id="ff05f-111">È possibile esportare un **modello generato che rappresenta lo stato corrente del gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-111">You can export a **generated template that represents the current state of the resource group**.</span></span> <span data-ttu-id="ff05f-112">Il modello esportato non si basa su un modello qualsiasi usato per la distribuzione,</span><span class="sxs-lookup"><span data-stu-id="ff05f-112">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="ff05f-113">ma crea un modello che è uno snapshot del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-113">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="ff05f-114">Il modello esportato ha diversi valori hardcoded e probabilmente meno parametri di quelli che si definiscono in genere.</span><span class="sxs-lookup"><span data-stu-id="ff05f-114">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="ff05f-115">Questo approccio è utile quando il gruppo di risorse è stato modificato dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-115">This approach is useful when you have modified the resource group after deployment.</span></span> <span data-ttu-id="ff05f-116">Il modello richiede in genere modifiche prima di poter essere usato.</span><span class="sxs-lookup"><span data-stu-id="ff05f-116">This template usually requires modifications before it is usable.</span></span>

<span data-ttu-id="ff05f-117">Questo argomento illustra entrambi gli approcci tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-117">This topic shows both approaches through the portal.</span></span>

## <a name="deploy-resources"></a><span data-ttu-id="ff05f-118">Distribuire le risorse</span><span class="sxs-lookup"><span data-stu-id="ff05f-118">Deploy resources</span></span>
<span data-ttu-id="ff05f-119">Per iniziare, distribuire in Azure risorse utilizzabili per l'esportazione come modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-119">Let's start by deploying resources to Azure that you can use for exporting as a template.</span></span> <span data-ttu-id="ff05f-120">Se la sottoscrizione include già un gruppo di risorse che si vuole esportare in un modello, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-120">If you already have a resource group in your subscription that you want to export to a template, you can skip this section.</span></span> <span data-ttu-id="ff05f-121">Il resto di questo articolo presuppone che sia stata distribuita la soluzione di app Web e database SQL illustrata in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-121">The remainder of this article assumes you have deployed the web app and SQL database solution shown in this section.</span></span> <span data-ttu-id="ff05f-122">Se si usa un'altra soluzione, l'esperienza potrebbe essere leggermente diversa, ma i passaggi per esportare un modello saranno gli stessi.</span><span class="sxs-lookup"><span data-stu-id="ff05f-122">If you use a different solution, your experience might be a little different, but the steps to export a template are the same.</span></span> 

1. <span data-ttu-id="ff05f-123">Nel [portale di Azure](https://portal.azure.com) selezionare **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-123">In the [Azure portal](https://portal.azure.com), select **New**.</span></span>
   
      ![Selezionare Nuovo](./media/resource-manager-export-template/new.png)
2. <span data-ttu-id="ff05f-125">Cercare **App Web e SQL** e selezionare tale voce nelle opzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="ff05f-125">Search for **web app + SQL** and select it from the available options.</span></span>
   
      ![Cercare App Web e SQL](./media/resource-manager-export-template/webapp-sql.png)

3. <span data-ttu-id="ff05f-127">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-127">Select **Create**.</span></span>

      ![Selezionare Crea](./media/resource-manager-export-template/create.png)

4. <span data-ttu-id="ff05f-129">Specificare i valori necessari per l'app Web e il database SQL.</span><span class="sxs-lookup"><span data-stu-id="ff05f-129">Provide the required values for the web app and SQL database.</span></span> <span data-ttu-id="ff05f-130">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-130">Select **Create**.</span></span>

      ![Specificare i valori per Web e SQL](./media/resource-manager-export-template/provide-web-values.png)

<span data-ttu-id="ff05f-132">La distribuzione può richiedere un minuto.</span><span class="sxs-lookup"><span data-stu-id="ff05f-132">The deployment may take a minute.</span></span> <span data-ttu-id="ff05f-133">Al termine della distribuzione, la sottoscrizione conterrà la soluzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-133">After the deployment finishes, your subscription contains the solution.</span></span>

## <a name="view-template-from-deployment-history"></a><span data-ttu-id="ff05f-134">Visualizzare il modello dalla cronologia delle distribuzioni</span><span class="sxs-lookup"><span data-stu-id="ff05f-134">View template from deployment history</span></span>
1. <span data-ttu-id="ff05f-135">Passare al pannello Gruppo di risorse per il nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-135">Go to the resource group blade for your new resource group.</span></span> <span data-ttu-id="ff05f-136">Si noti che il pannello visualizza il risultato dell'ultima distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-136">Notice that the blade shows the result of the last deployment.</span></span> <span data-ttu-id="ff05f-137">Selezionare questo collegamento.</span><span class="sxs-lookup"><span data-stu-id="ff05f-137">Select this link.</span></span>
   
      ![pannello Gruppo di risorse](./media/resource-manager-export-template/select-deployment.png)
2. <span data-ttu-id="ff05f-139">Viene visualizzata la cronologia delle distribuzioni per il gruppo.</span><span class="sxs-lookup"><span data-stu-id="ff05f-139">You see a history of deployments for the group.</span></span> <span data-ttu-id="ff05f-140">In questo caso il pannello probabilmente elenca solo una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-140">In your case, the blade probably lists only one deployment.</span></span> <span data-ttu-id="ff05f-141">Selezionare questa distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-141">Select this deployment.</span></span>
   
     ![ultima distribuzione](./media/resource-manager-export-template/select-history.png)
3. <span data-ttu-id="ff05f-143">Il pannello visualizza un riepilogo della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-143">The blade displays a summary of the deployment.</span></span> <span data-ttu-id="ff05f-144">Il riepilogo include lo stato della distribuzione e le relative operazioni e i valori specificati per i parametri.</span><span class="sxs-lookup"><span data-stu-id="ff05f-144">The summary includes the status of the deployment and its operations and the values that you provided for parameters.</span></span> <span data-ttu-id="ff05f-145">Per visualizzare il modello usato per la distribuzione, selezionare **Visualizza modello**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-145">To see the template that you used for the deployment, select **View template**.</span></span>
   
     ![visualizzare il riepilogo della distribuzione](./media/resource-manager-export-template/view-template.png)
4. <span data-ttu-id="ff05f-147">Resource Manager recupera i sette file seguenti.</span><span class="sxs-lookup"><span data-stu-id="ff05f-147">Resource Manager retrieves the following seven files for you:</span></span>
   
   1. <span data-ttu-id="ff05f-148">**Modello** : modello che definisce l'infrastruttura per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-148">**Template** - The template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="ff05f-149">Quando è stato creato l'account di archiviazione tramite il portale, Resource Manager ha usato un modello per distribuirlo e ha salvato tale modello come riferimento futuro.</span><span class="sxs-lookup"><span data-stu-id="ff05f-149">When you created the storage account through the portal, Resource Manager used a template to deploy it and saved that template for future reference.</span></span>
   2. <span data-ttu-id="ff05f-150">**Parametri** : file dei parametri che può essere usato per passare i valori durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-150">**Parameters** - A parameter file that you can use to pass in values during deployment.</span></span> <span data-ttu-id="ff05f-151">Contiene i valori specificati durante la prima distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-151">It contains the values that you provided during the first deployment.</span></span> <span data-ttu-id="ff05f-152">Quando si ridistribuisce il modello è possibile modificare qualsiasi valore.</span><span class="sxs-lookup"><span data-stu-id="ff05f-152">You can change any of these values when you redeploy the template.</span></span>
   3. <span data-ttu-id="ff05f-153">**Interfaccia della riga di comando** : file di script dell'interfaccia della riga di comando di Azure che può essere usato per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-153">**CLI** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   3. <span data-ttu-id="ff05f-154">**Interfaccia della riga di comando 2.0**: file di script dell'interfaccia della riga di comando di Azure che può essere usato per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-154">**CLI 2.0** - An Azure command-line-interface (CLI) script file that you can use to deploy the template.</span></span>
   4. <span data-ttu-id="ff05f-155">**PowerShell** : file di script di Azure PowerShell che può essere usato per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-155">**PowerShell** - An Azure PowerShell script file that you can use to deploy the template.</span></span>
   5. <span data-ttu-id="ff05f-156">**.NET** : classe .NET che può essere usata per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-156">**.NET** - A .NET class that you can use to deploy the template.</span></span>
   6. <span data-ttu-id="ff05f-157">**Ruby** : classe Ruby che può essere usata per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-157">**Ruby** - A Ruby class that you can use to deploy the template.</span></span>
      
      <span data-ttu-id="ff05f-158">I file sono disponibili mediante collegamenti nel pannello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-158">The files are available through links across the blade.</span></span> <span data-ttu-id="ff05f-159">Per impostazione predefinita, il pannello visualizza il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-159">By default, the blade displays the template.</span></span>
      
       ![Visualizza modello](./media/resource-manager-export-template/see-template.png)
      
<span data-ttu-id="ff05f-161">Questo è il modello effettivo usato per creare l'app Web e il database SQL.</span><span class="sxs-lookup"><span data-stu-id="ff05f-161">This template is the actual template used to create your web app and SQL database.</span></span> <span data-ttu-id="ff05f-162">Si noti che contiene parametri che consentono di specificare diversi valori durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-162">Notice it contains parameters that enable you to provide different values during deployment.</span></span> <span data-ttu-id="ff05f-163">Per altre informazioni sulla struttura del modello, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff05f-163">To learn more about the structure of a template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

## <a name="export-the-template-from-resource-group"></a><span data-ttu-id="ff05f-164">Esportare il modello da un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ff05f-164">Export the template from resource group</span></span>
<span data-ttu-id="ff05f-165">Se le risorse sono state modificate manualmente o aggiunte in più distribuzioni, il modello recuperato dalla cronologia delle distribuzioni non riflette lo stato corrente del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-165">If you have manually changed your resources or added resources in multiple deployments, retrieving a template from the deployment history does not reflect the current state of the resource group.</span></span> <span data-ttu-id="ff05f-166">Questa sezione illustra come esportare un modello che rispecchia tale stato.</span><span class="sxs-lookup"><span data-stu-id="ff05f-166">This section shows you how to export a template that reflects the current state of the resource group.</span></span> 

> [!NOTE]
> <span data-ttu-id="ff05f-167">Non è possibile esportare un modello per un gruppo di risorse con più di 200 risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-167">You cannot export a template for a resource group that has more than 200 resources.</span></span>
> 
> 

1. <span data-ttu-id="ff05f-168">Per visualizzare il modello per un gruppo di risorse, selezionare **Script di automazione**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-168">To view the template for a resource group, select **Automation script**.</span></span>
   
      ![esportare un gruppo di risorse](./media/resource-manager-export-template/select-automation.png)
   
     <span data-ttu-id="ff05f-170">Resource Manager valuta le risorse nel gruppo di risorse e genera un modello per tali risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-170">Resource Manager evaluates the resources in the resource group, and generates a template for those resources.</span></span> <span data-ttu-id="ff05f-171">Non tutti i tipi di risorse supportano la funzione di esportazione del modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-171">Not all resource types support the export template function.</span></span> <span data-ttu-id="ff05f-172">Potrebbe essere visualizzato un errore che informa di un problema con l'esportazione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-172">You may see an error stating that there is a problem with the export.</span></span> <span data-ttu-id="ff05f-173">Per informazioni su come gestire tali problemi, vedere la sezione [Risolvere i problemi di esportazione](#fix-export-issues) .</span><span class="sxs-lookup"><span data-stu-id="ff05f-173">You learn how to handle those issues in the [Fix export issues](#fix-export-issues) section.</span></span>
2. <span data-ttu-id="ff05f-174">Vengono visualizzati di nuovo i sei file che è possibile usare per ridistribuire la soluzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-174">You again see the six files that you can use to redeploy the solution.</span></span> <span data-ttu-id="ff05f-175">Questa volta, tuttavia, il modello è leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="ff05f-175">However, this time the template is a little different.</span></span> <span data-ttu-id="ff05f-176">Si noti che il modello generato contiene un numero inferiore di parametri rispetto al modello della sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="ff05f-176">Notice that the generated template contains fewer parameters than the template in previous section.</span></span> <span data-ttu-id="ff05f-177">Inoltre, molti di questi valori (come i valori relativi a località e SKU) sono hardcoded nel modello e non accettano un valore di parametro.</span><span class="sxs-lookup"><span data-stu-id="ff05f-177">Also, many of the values (like location and SKU values) are hard-coded in this template rather than accepting a parameter value.</span></span> <span data-ttu-id="ff05f-178">Prima di riusare il modello, può essere opportuno modificarlo per usare meglio i parametri.</span><span class="sxs-lookup"><span data-stu-id="ff05f-178">Before reusing this template, you might want to edit the template to make better use of parameters.</span></span> 
   
3. <span data-ttu-id="ff05f-179">Per continuare a usare questo modello, sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="ff05f-179">You have a couple of options for continuing to work with this template.</span></span> <span data-ttu-id="ff05f-180">È possibile scaricare il modello e usare un editor JSON per lavorare in locale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-180">You can either download the template and work on it locally with a JSON editor.</span></span> <span data-ttu-id="ff05f-181">In alternativa, è possibile salvare il modello nella libreria e lavorare tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-181">Or, you can save the template to your library and work on it through the portal.</span></span>
   
     <span data-ttu-id="ff05f-182">Se si ha familiarità con un editor di JSON come [Visual Studio Code](https://code.visualstudio.com/) o [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), è preferibile scaricare il modello in locale e usare l'editor.</span><span class="sxs-lookup"><span data-stu-id="ff05f-182">If you are comfortable using a JSON editor like [VS Code](https://code.visualstudio.com/) or [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md), you might prefer downloading the template locally and using that editor.</span></span> <span data-ttu-id="ff05f-183">Per lavorare in locale, selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-183">To work locally, select **Download**.</span></span>
   
      ![scaricare il modello](./media/resource-manager-export-template/download-template.png)
   
     <span data-ttu-id="ff05f-185">Se non si ha familiarità con un editor JSON, è preferibile modificare il modello tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-185">If you are not set up with a JSON editor, you might prefer editing the template through the portal.</span></span> <span data-ttu-id="ff05f-186">Nelle sezioni successive di questo argomento si presuppone che il modello sia stato salvato nella libreria nel portale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-186">The remainder of this topic assumes you have saved the template to your library in the portal.</span></span> <span data-ttu-id="ff05f-187">Tuttavia, si apportano le stesse modifiche di sintassi al modello lavorando tramite il portale o in locale con un editor di JSON.</span><span class="sxs-lookup"><span data-stu-id="ff05f-187">However, you make the same syntax changes to the template whether working locally with a JSON editor or through the portal.</span></span> <span data-ttu-id="ff05f-188">Per usare il portale, selezionare **Aggiungi a raccolta**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-188">To work through the portal, select **Add to library**.</span></span>
   
      ![aggiungere alla libreria](./media/resource-manager-export-template/add-to-library.png)
   
     <span data-ttu-id="ff05f-190">Quando si aggiunge un modello alla libreria, assegnare un nome e una descrizione al modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-190">When adding a template to the library, give the template a name and description.</span></span> <span data-ttu-id="ff05f-191">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-191">Then, select **Save**.</span></span>
   
     ![impostare i valori di modello](./media/resource-manager-export-template/save-library-template.png)
4. <span data-ttu-id="ff05f-193">Per visualizzare un modello salvato nella libreria, selezionare **Altri servizi**, digitare **Modelli** per filtrare i risultati, quindi selezionare **Modelli**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-193">To view a template saved in your library, select **More services**, type **Templates** to filter results, select **Templates**.</span></span>
   
      ![trovare i modelli](./media/resource-manager-export-template/find-templates.png)
5. <span data-ttu-id="ff05f-195">Selezionare il modello con il nome salvato.</span><span class="sxs-lookup"><span data-stu-id="ff05f-195">Select the template with the name you saved.</span></span>
   
      ![selezionare modello](./media/resource-manager-export-template/select-saved-template.png)

## <a name="customize-the-template"></a><span data-ttu-id="ff05f-197">Personalizzare il modello</span><span class="sxs-lookup"><span data-stu-id="ff05f-197">Customize the template</span></span>
<span data-ttu-id="ff05f-198">Il modello esportato funziona correttamente se si vuole creare la stessa app Web e lo stesso database SQL per ogni distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-198">The exported template works fine if you want to create the same web app and SQL database for every deployment.</span></span> <span data-ttu-id="ff05f-199">Le opzioni disponibili in Resource Manager consentono, tuttavia, di distribuire modelli con maggiore flessibilità.</span><span class="sxs-lookup"><span data-stu-id="ff05f-199">However, Resource Manager provides options so that you can deploy templates with a lot more flexibility.</span></span> <span data-ttu-id="ff05f-200">Questo articolo illustra come aggiungere parametri per il nome e la password di amministratore del database.</span><span class="sxs-lookup"><span data-stu-id="ff05f-200">This article shows you how to add parameters for the database administrator name and password.</span></span> <span data-ttu-id="ff05f-201">Questo stesso approccio può essere usato per aggiungere maggiore flessibilità per altri valori del modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-201">You can use this same approach to add more flexibility for other values in the template.</span></span>

1. <span data-ttu-id="ff05f-202">Per personalizzare il modello, selezionare **Modifica**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-202">To customize the template, select **Edit**.</span></span>
   
     ![visualizzare il modello](./media/resource-manager-export-template/select-edit.png)
2. <span data-ttu-id="ff05f-204">Selezionare il modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-204">Select the template.</span></span>
   
     ![modificare un modello](./media/resource-manager-export-template/select-added-template.png)
3. <span data-ttu-id="ff05f-206">Per poter passare i valori da specificare durante la distribuzione, aggiungere i due parametri seguenti nella sezione **parameters** del modello:</span><span class="sxs-lookup"><span data-stu-id="ff05f-206">To be able to pass the values that you might want to specify during deployment, add the following two parameters to the **parameters** section in the template:</span></span>

   ```json
   "administratorLogin": {
       "type": "String"
   },
   "administratorLoginPassword": {
       "type": "SecureString"
   },
   ```

4. <span data-ttu-id="ff05f-207">Per usare i nuovi parametri, sostituire la definizione dell'istanza di SQL Server nella sezione **resources**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-207">To use the new parameters, replace the SQL server definition in the **resources** section.</span></span> <span data-ttu-id="ff05f-208">Si noti che in **administratorLogin** e **administratorLoginPassword** vengono ora usati valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="ff05f-208">Notice that **administratorLogin** and **administratorLoginPassword** now use parameter values.</span></span>

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

6. <span data-ttu-id="ff05f-209">Selezionare **OK** una volta terminata la modifica del modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-209">Select **OK** when you are done editing the template.</span></span>
7. <span data-ttu-id="ff05f-210">Selezionare **Salva** per salvare le modifiche al modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-210">Select **Save** to save the changes to the template.</span></span>
   
     ![salvare il modello](./media/resource-manager-export-template/save-template.png)
8. <span data-ttu-id="ff05f-212">Per ridistribuire il modello aggiornato, selezionare **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="ff05f-212">To redeploy the updated template, select **Deploy**.</span></span>
   
     ![distribuire un modello](./media/resource-manager-export-template/redeploy-template.png)
9. <span data-ttu-id="ff05f-214">Specificare i valori dei parametri e selezionare un gruppo di risorse in cui distribuire le risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-214">Provide parameter values, and select a resource group to deploy the resources to.</span></span>


## <a name="fix-export-issues"></a><span data-ttu-id="ff05f-215">Risolvere i problemi di esportazione</span><span class="sxs-lookup"><span data-stu-id="ff05f-215">Fix export issues</span></span>
<span data-ttu-id="ff05f-216">Non tutti i tipi di risorse supportano la funzione di esportazione del modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-216">Not all resource types support the export template function.</span></span> <span data-ttu-id="ff05f-217">Per risolvere il problema, aggiungere manualmente le risorse mancanti al modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-217">To resolve this issue, manually add the missing resources back into your template.</span></span> <span data-ttu-id="ff05f-218">Il messaggio di errore include i tipi di risorsa che non possono essere esportati.</span><span class="sxs-lookup"><span data-stu-id="ff05f-218">The error message includes the resource types that cannot be exported.</span></span> <span data-ttu-id="ff05f-219">Trovare il tipo di risorsa nelle [informazioni di riferimento sui modelli](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="ff05f-219">Find that resource type in [Template reference](/azure/templates/).</span></span> <span data-ttu-id="ff05f-220">Per aggiungere manualmente un gateway di rete virtuale, ad esempio, vedere le [informazioni di riferimento sul modello Microsoft.Network/virtualNetworkGateways](/azure/templates/microsoft.network/virtualnetworkgateways).</span><span class="sxs-lookup"><span data-stu-id="ff05f-220">For example, to manually add a virtual network gateway, see [Microsoft.Network/virtualNetworkGateways template reference](/azure/templates/microsoft.network/virtualnetworkgateways).</span></span>

> [!NOTE]
> <span data-ttu-id="ff05f-221">Si verificano problemi di esportazione solo quando si esporta da un gruppo di risorse invece che dalla cronologia della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff05f-221">You only encounter export issues when exporting from a resource group rather than from your deployment history.</span></span> <span data-ttu-id="ff05f-222">Se la distribuzione più recente rappresenta con precisione lo stato corrente del gruppo di risorse, è consigliabile esportare il modello dalla cronologia della distribuzione invece che dal gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff05f-222">If your last deployment accurately represents the current state of the resource group, you should export the template from the deployment history rather than from the resource group.</span></span> <span data-ttu-id="ff05f-223">Eseguire l'esportazione da un gruppo di risorse solo quando sono state apportate al gruppo di risorse modifiche non definite in un singolo modello.</span><span class="sxs-lookup"><span data-stu-id="ff05f-223">Only export from a resource group when you have made changes to the resource group that are not defined in a single template.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ff05f-224">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff05f-224">Next steps</span></span>
<span data-ttu-id="ff05f-225">Si è appreso come esportare un modello da risorse create nel portale.</span><span class="sxs-lookup"><span data-stu-id="ff05f-225">You have learned how to export a template from resources that you created in the portal.</span></span>

* <span data-ttu-id="ff05f-226">È possibile distribuire un modello tramite [PowerShell](resource-group-template-deploy.md), l'[interfaccia della riga di comando di Azure](resource-group-template-deploy-cli.md) o l'[API REST](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="ff05f-226">You can deploy a template through [PowerShell](resource-group-template-deploy.md), [Azure CLI](resource-group-template-deploy-cli.md), or [REST API](resource-group-template-deploy-rest.md).</span></span>
* <span data-ttu-id="ff05f-227">Per informazioni su come esportare un modello tramite PowerShell, vedere [Uso di Azure PowerShell con Azure Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ff05f-227">To see how to export a template through PowerShell, see [Using Azure PowerShell with Azure Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="ff05f-228">Per informazioni su come esportare un modello tramite l'interfaccia della riga di comando di Azure, vedere [Usare l'interfaccia della riga di comando di Azure per Mac, Linux e Windows con Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ff05f-228">To see how to export a template through Azure CLI, see [Use the Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>

