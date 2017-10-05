---
title: Gestire le risorse di Azure tramite il portale di Azure | Microsoft Docs
description: Utilizzare il portale di Azure e Azure Resource Manager per gestire le risorse. Illustra come usare i dashboard per monitorare le risorse.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0725bbf2-5913-4c07-af6e-24e11d957fbc
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: 7a94fd5065de93384460e851627a9813d439956b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="feb4c-104">Gestire le risorse di Azure mediante il portale</span><span class="sxs-lookup"><span data-stu-id="feb4c-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="feb4c-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="feb4c-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="feb4c-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="feb4c-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="feb4c-107">Portale</span><span class="sxs-lookup"><span data-stu-id="feb4c-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="feb4c-108">API REST</span><span class="sxs-lookup"><span data-stu-id="feb4c-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="feb4c-109">Questo argomento illustra come usare il [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) per gestire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="feb4c-109">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to manage your Azure resources.</span></span> <span data-ttu-id="feb4c-110">Per informazioni sulla distribuzione delle risorse tramite il portale, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-110">To learn about deploying resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="feb4c-111">Non tutti i servizi attualmente supportano il portale o Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-111">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="feb4c-112">Per questi servizi sarà necessario usare il [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="feb4c-112">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="feb4c-113">Per lo stato di ogni servizio, vedere il [grafico della disponibilità del portale di Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="feb4c-113">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="feb4c-114">Gestire gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-114">Manage resource groups</span></span>

<span data-ttu-id="feb4c-115">Un gruppo di risorse è un contenitore con risorse correlate per una soluzione Azure.</span><span class="sxs-lookup"><span data-stu-id="feb4c-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="feb4c-116">Il gruppo di risorse può includere tutte le risorse della soluzione o solo le risorse da gestire come gruppo.</span><span class="sxs-lookup"><span data-stu-id="feb4c-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="feb4c-117">L'utente decide come allocare le risorse ai gruppi di risorse nel modo più appropriato per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="feb4c-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="feb4c-118">È in genere consigliabile aggiungere risorse che condividono lo stesso ciclo di vita allo stesso gruppo di risorse per poterle distribuire, aggiornare ed eliminare facilmente come gruppo.</span><span class="sxs-lookup"><span data-stu-id="feb4c-118">Generally, add resources that share the same lifecycle to the same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="feb4c-119">Il gruppo di risorse archivia i metadati delle risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-119">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="feb4c-120">Quando si specifica un percorso per il gruppo di risorse, si specifica il percorso di archiviazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="feb4c-120">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="feb4c-121">Per motivi di conformità potrebbe essere necessario assicurarsi che i dati siano archiviati in una determinata area.</span><span class="sxs-lookup"><span data-stu-id="feb4c-121">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="feb4c-122">Per visualizzare tutti i gruppi di risorse della sottoscrizione, selezionare **Gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-122">To see all the resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![esplorare i gruppi di risorse](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="feb4c-124">Per creare un gruppo di risorse vuoto, selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-124">To create an empty resource group, select **Add**.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="feb4c-126">Specificare il nome e il percorso del nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-126">Provide a name and location for the new resource group.</span></span> <span data-ttu-id="feb4c-127">Selezionare **Create**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-127">Select **Create**.</span></span>
   
    ![creare un gruppo di risorse](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="feb4c-129">Potrebbe essere necessario selezionare **Aggiorna** per visualizzare il gruppo di risorse creato di recente.</span><span class="sxs-lookup"><span data-stu-id="feb4c-129">You may need to select **Refresh** to see the recently created resource group.</span></span>
   
    ![aggiornare un gruppo di risorse](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="feb4c-131">Per personalizzare le informazioni visualizzate per i gruppi di risorse, selezionare **Colonne**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-131">To customize the information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizzare colonne](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="feb4c-133">Selezionare le colonne da aggiungere, quindi selezionare **Aggiorna**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-133">Select the columns to add, and then select **Update**.</span></span>
   
    ![aggiungere colonne](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="feb4c-135">Per informazioni sulla distribuzione delle risorse nel nuovo gruppo di risorse, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-135">To learn about deploying resources to your new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="feb4c-136">Per accedere rapidamente al gruppo di risorse, è possibile aggiungere il pannello al dashboard.</span><span class="sxs-lookup"><span data-stu-id="feb4c-136">For quick access to a resource group, you can pin the blade to your dashboard.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="feb4c-138">Il dashboard visualizza il gruppo di risorse e le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-138">The dashboard displays the resource group and its resources.</span></span> <span data-ttu-id="feb4c-139">È possibile selezionare i gruppi di risorse o le relative risorse per passare all'elemento.</span><span class="sxs-lookup"><span data-stu-id="feb4c-139">You can select either the resource groups or any of its resources to navigate to the item.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="feb4c-141">Aggiungere tag alle risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-141">Tag resources</span></span>
<span data-ttu-id="feb4c-142">È possibile applicare tag ai gruppi di risorse e alle risorse per organizzare logicamente gli asset.</span><span class="sxs-lookup"><span data-stu-id="feb4c-142">You can apply tags to resource groups and resources to logically organize your assets.</span></span> <span data-ttu-id="feb4c-143">Per informazioni sull'uso dei tag, vedere [Uso dei tag per organizzare le risorse di Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-143">For information about working with tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="feb4c-144">Monitorare le risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-144">Monitor resources</span></span>
<span data-ttu-id="feb4c-145">Quando si seleziona una risorsa, il pannello della risorsa visualizza grafici e tabelle predefiniti per il monitoraggio di quel tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="feb4c-145">When you select a resource, the resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="feb4c-146">Selezionare una risorsa ed esaminare la sezione **Monitoraggio**,</span><span class="sxs-lookup"><span data-stu-id="feb4c-146">Select a resource and notice the **Monitoring** section.</span></span> <span data-ttu-id="feb4c-147">che include i grafici relativi al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="feb4c-147">It includes graphs that are relevant to the resource type.</span></span> <span data-ttu-id="feb4c-148">L'immagine seguente illustra i dati di monitoraggio predefiniti per un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="feb4c-148">The following image shows the default monitoring data for a storage account.</span></span>
   
    ![visualizzare il monitoraggio](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="feb4c-150">È possibile aggiungere una sezione del pannello al dashboard selezionando i puntini di sospensione (...) sopra la sezione.</span><span class="sxs-lookup"><span data-stu-id="feb4c-150">You can pin a section of the blade to your dashboard by selecting the ellipsis (...) above the section.</span></span> <span data-ttu-id="feb4c-151">È inoltre possibile personalizzare le dimensioni della sezione nel pannello o rimuoverla completamente.</span><span class="sxs-lookup"><span data-stu-id="feb4c-151">You can also customize the size the section in the blade or remove it completely.</span></span> <span data-ttu-id="feb4c-152">L'immagine seguente illustra come aggiungere, personalizzare o rimuovere la sezione relativa a CPU e memoria.</span><span class="sxs-lookup"><span data-stu-id="feb4c-152">The following image shows how to pin, customize, or remove the CPU and Memory section.</span></span>
   
    ![sezione di aggiunta](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="feb4c-154">Dopo avere aggiunto la sezione al dashboard, ne verrà visualizzato il riepilogo.</span><span class="sxs-lookup"><span data-stu-id="feb4c-154">After pinning the section to the dashboard, you will see the summary on the dashboard.</span></span> <span data-ttu-id="feb4c-155">Selezionandola si potranno vedere altri dettagli sui dati.</span><span class="sxs-lookup"><span data-stu-id="feb4c-155">And, selecting it immediately takes you to more details about the data.</span></span>
   
    ![visualizzare il dashboard](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="feb4c-157">Per personalizzare completamente i dati monitorati dal portale, passare al dashboard predefinito e selezionare **Nuovo dashboard**.</span><span class="sxs-lookup"><span data-stu-id="feb4c-157">To completely customize the data you monitor through the portal, navigate to your default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="feb4c-159">Assegnare un nome al nuovo dashboard e trascinare i riquadri sul dashboard.</span><span class="sxs-lookup"><span data-stu-id="feb4c-159">Give your new dashboard a name and drag tiles onto the dashboard.</span></span> <span data-ttu-id="feb4c-160">I riquadri vengono filtrati in base a opzioni diverse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-160">The tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="feb4c-162">Per informazioni sull'uso dei dashboard, vedere [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md)(Creazione e condivisione di dashboard nel portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="feb4c-162">To learn about working with dashboards, see [Creating and sharing dashboards in the Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="feb4c-163">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-163">Manage resources</span></span>
<span data-ttu-id="feb4c-164">Nel pannello di una risorsa sono visibili le opzioni per la gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-164">In the blade for a resource, you see the options for managing the resource.</span></span> <span data-ttu-id="feb4c-165">Il portale presenta le opzioni di gestione per quel particolare tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="feb4c-165">The portal presents management options for that particular resource type.</span></span> <span data-ttu-id="feb4c-166">I comandi per la gestione vengono visualizzati nella parte superiore del pannello della risorsa e sul lato sinistro.</span><span class="sxs-lookup"><span data-stu-id="feb4c-166">You see the management commands across the top of the resource blade and on the left side.</span></span>

![Gestire risorse](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="feb4c-168">Con queste opzioni, è possibile eseguire operazioni come l'avvio e l'arresto di una macchina virtuale o la riconfigurazione delle proprietà della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="feb4c-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring the properties of the virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="feb4c-169">Spostare le risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-169">Move resources</span></span>
<span data-ttu-id="feb4c-170">Per spostare una risorsa in un altro gruppo di risorse o in un'altra sottoscrizione, vedere [Spostare le risorse in un gruppo di risorse o una sottoscrizione nuovi](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-170">If you need to move resources to another resource group or another subscription, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="feb4c-171">Bloccare le risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-171">Lock resources</span></span>
<span data-ttu-id="feb4c-172">È possibile bloccare una sottoscrizione, una risorsa o un gruppo di risorse per impedire che altri utenti nell'organizzazione modifichino o eliminino accidentalmente risorse strategiche.</span><span class="sxs-lookup"><span data-stu-id="feb4c-172">You can lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="feb4c-173">Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="feb4c-174">Visualizzare la sottoscrizione e i costi</span><span class="sxs-lookup"><span data-stu-id="feb4c-174">View your subscription and costs</span></span>
<span data-ttu-id="feb4c-175">È possibile visualizzare informazioni sulla sottoscrizione e un riepilogo dei costi per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-175">You can view information about your subscription and the rolled-up costs for all your resources.</span></span> <span data-ttu-id="feb4c-176">Selezionare **Sottoscrizioni** e quindi la sottoscrizione da visualizzare.</span><span class="sxs-lookup"><span data-stu-id="feb4c-176">Select **Subscriptions** and the subscription you want to see.</span></span> <span data-ttu-id="feb4c-177">Potrebbe essere disponibile una sola sottoscrizione da selezionare.</span><span class="sxs-lookup"><span data-stu-id="feb4c-177">You might only have one subscription to select.</span></span>

![sottoscrizione](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="feb4c-179">Nel pannello della sottoscrizione viene visualizzata la velocità.</span><span class="sxs-lookup"><span data-stu-id="feb4c-179">Within the subscription blade, you see a burn rate.</span></span>

![velocità](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="feb4c-181">E una suddivisione dei costi in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="feb4c-181">And, a breakdown of costs by resource type.</span></span>

![costo delle risorse](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="feb4c-183">Esportare il modello</span><span class="sxs-lookup"><span data-stu-id="feb4c-183">Export template</span></span>
<span data-ttu-id="feb4c-184">Dopo avere configurato il gruppo di risorse, è possibile che si voglia visualizzare il modello di Azure Resource Manager per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="feb4c-184">After setting up your resource group, you may want to view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="feb4c-185">L'esportazione del modello offre due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="feb4c-185">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="feb4c-186">È possibile automatizzare le distribuzioni future della soluzione perché il modello contiene l'infrastruttura completa.</span><span class="sxs-lookup"><span data-stu-id="feb4c-186">You can easily automate future deployments of the solution because the template contains all the complete infrastructure.</span></span>
2. <span data-ttu-id="feb4c-187">È possibile acquisire familiarità con la sintassi del modello esaminando il codice JSON (JavaScript Object Notation) che rappresenta la soluzione.</span><span class="sxs-lookup"><span data-stu-id="feb4c-187">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="feb4c-188">Per istruzioni dettagliate, vedere [Esportare un modello di Azure Resource Manager da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="feb4c-189">Eliminare risorse o gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="feb4c-189">Delete resource group or resources</span></span>
<span data-ttu-id="feb4c-190">Se si elimina un gruppo di risorse, vengono eliminate tutte le risorse contenute in esso.</span><span class="sxs-lookup"><span data-stu-id="feb4c-190">Deleting a resource group deletes all the resources contained within it.</span></span> <span data-ttu-id="feb4c-191">È anche possibile eliminare singole risorse all'interno di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="feb4c-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="feb4c-192">Prestare attenzione quando si elimina un gruppo di risorse perché è possibile che altri gruppi di risorse includano risorse collegate ad esso.</span><span class="sxs-lookup"><span data-stu-id="feb4c-192">You want to exercise caution when you delete a resource group because there might be resources in other resource groups that are linked to it.</span></span> <span data-ttu-id="feb4c-193">Resource Manager non elimina le risorse collegate, ma le risorse potrebbero non funzionare correttamente senza le risorse necessarie.</span><span class="sxs-lookup"><span data-stu-id="feb4c-193">Resource Manager does not delete linked resources, but they may not operate correctly without the expected resources.</span></span>

![eliminare un gruppo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="feb4c-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="feb4c-195">Next steps</span></span>
* <span data-ttu-id="feb4c-196">Per visualizzare i log attività, vedere [Operazioni di controllo con Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-196">To view activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="feb4c-197">Per visualizzare i dettagli su una distribuzione, vedere [View deployment operations](resource-manager-deployment-operations.md) (Visualizzare le operazioni di distribuzione).</span><span class="sxs-lookup"><span data-stu-id="feb4c-197">To view details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="feb4c-198">Per la distribuzione di risorse tramite il portale, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-198">To deploy resources through the portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="feb4c-199">Per gestire l'accesso alle risorse, vedere [Usare le assegnazioni di ruolo per gestire l'accesso alle risorse della sottoscrizione di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="feb4c-199">To manage access to resources, see [Use role assignments to manage access to your Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="feb4c-200">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="feb4c-200">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

