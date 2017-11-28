---
title: aaaUse toomanage portale Azure le risorse di Azure | Documenti Microsoft
description: Utilizzare il portale di Azure e gestire risorse di Azure toomanage le risorse. Viene illustrato come toowork con risorse toomonitor dashboard.
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
ms.openlocfilehash: 0c89a197a31c5b6dd03ba457cb4d1fdf9f6d00f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-resources-through-portal"></a><span data-ttu-id="8be1a-104">Gestire le risorse di Azure mediante il portale</span><span class="sxs-lookup"><span data-stu-id="8be1a-104">Manage Azure resources through portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8be1a-105">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="8be1a-105">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="8be1a-106">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8be1a-106">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="8be1a-107">Portale</span><span class="sxs-lookup"><span data-stu-id="8be1a-107">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="8be1a-108">API REST</span><span class="sxs-lookup"><span data-stu-id="8be1a-108">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="8be1a-109">Questo argomento viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toomanage le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="8be1a-109">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toomanage your Azure resources.</span></span> <span data-ttu-id="8be1a-110">vedere toolearn sulla distribuzione di risorse tramite il portale di hello [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-110">toolearn about deploying resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>

<span data-ttu-id="8be1a-111">Attualmente, non a ogni servizio supporta portale hello o gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-111">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="8be1a-112">Per tali servizi, è necessario hello toouse [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8be1a-112">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="8be1a-113">Per hello lo stato di ogni servizio, vedere [grafico disponibilità portale Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="8be1a-113">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="manage-resource-groups"></a><span data-ttu-id="8be1a-114">Gestire gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-114">Manage resource groups</span></span>

<span data-ttu-id="8be1a-115">Un gruppo di risorse è un contenitore con risorse correlate per una soluzione Azure.</span><span class="sxs-lookup"><span data-stu-id="8be1a-115">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="8be1a-116">gruppo di risorse Hello può includere tutte le risorse di hello per soluzione hello o solo le risorse che si desidera toomanage come gruppo.</span><span class="sxs-lookup"><span data-stu-id="8be1a-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="8be1a-117">Si decide come risorse tooallocate tooresource gruppi basati su cosa hello più utile per l'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8be1a-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="8be1a-118">In genere, aggiungere le risorse che condividono hello stesso toohello del ciclo di vita stessa risorsa di raggruppare in modo che è facilmente possibile distribuire, aggiornare ed eliminarli come gruppo.</span><span class="sxs-lookup"><span data-stu-id="8be1a-118">Generally, add resources that share hello same lifecycle toohello same resource group so you can easily deploy, update, and delete them as a group.</span></span> 

<span data-ttu-id="8be1a-119">gruppo di risorse Hello archivia i metadati sulle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-119">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="8be1a-120">Pertanto, quando si specifica un percorso per il gruppo di risorse hello, si specifica la memorizzazione dei metadati.</span><span class="sxs-lookup"><span data-stu-id="8be1a-120">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="8be1a-121">Per motivi di conformità, potrebbe essere necessario tooensure che i dati sono archiviati in una determinata area.</span><span class="sxs-lookup"><span data-stu-id="8be1a-121">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

1. <span data-ttu-id="8be1a-122">Selezionare tutti i gruppi di risorse di hello nella sottoscrizione, toosee **gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-122">toosee all hello resource groups in your subscription, select **Resource groups**.</span></span>
   
    ![esplorare i gruppi di risorse](./media/resource-group-portal/browse-groups.png)
2. <span data-ttu-id="8be1a-124">Selezionare un gruppo di risorse vuoto, toocreate **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-124">toocreate an empty resource group, select **Add**.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/add-resource-group.png)
3. <span data-ttu-id="8be1a-126">Specificare un nome e percorso per il nuovo gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-126">Provide a name and location for hello new resource group.</span></span> <span data-ttu-id="8be1a-127">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-127">Select **Create**.</span></span>
   
    ![Creare un gruppo di risorse](./media/resource-group-portal/create-empty-group.png)
4. <span data-ttu-id="8be1a-129">Potrebbe essere necessario tooselect **aggiornamento** toosee gruppo di risorse hello creato di recente.</span><span class="sxs-lookup"><span data-stu-id="8be1a-129">You may need tooselect **Refresh** toosee hello recently created resource group.</span></span>
   
    ![aggiornare un gruppo di risorse](./media/resource-group-portal/refresh-resource-groups.png)
5. <span data-ttu-id="8be1a-131">informazioni di hello toocustomize visualizzate per i gruppi di risorse, selezionare **colonne**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-131">toocustomize hello information displayed for your resource groups, select **Columns**.</span></span>
   
    ![personalizzare colonne](./media/resource-group-portal/select-columns.png)
6. <span data-ttu-id="8be1a-133">Selezionare tooadd colonne hello e quindi selezionare **aggiornamento**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-133">Select hello columns tooadd, and then select **Update**.</span></span>
   
    ![aggiungere colonne](./media/resource-group-portal/add-columns.png)
7. <span data-ttu-id="8be1a-135">toolearn sulla distribuzione di risorse tooyour nuovo gruppo di risorse, vedere [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-135">toolearn about deploying resources tooyour new resource group, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
8. <span data-ttu-id="8be1a-136">Per gruppo di risorse tooa di accesso rapido, è possibile aggiungere dashboard di tooyour hello blade.</span><span class="sxs-lookup"><span data-stu-id="8be1a-136">For quick access tooa resource group, you can pin hello blade tooyour dashboard.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/pin-group.png)
9. <span data-ttu-id="8be1a-138">Consente di visualizzare dashboard Hello gruppo di risorse hello e le relative risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-138">hello dashboard displays hello resource group and its resources.</span></span> <span data-ttu-id="8be1a-139">È possibile selezionare i gruppi di risorse hello o qualsiasi elemento toohello toonavigate di risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-139">You can select either hello resource groups or any of its resources toonavigate toohello item.</span></span>
   
    ![aggiungere un gruppo di risorse](./media/resource-group-portal/show-resource-group-dashboard.png)

## <a name="tag-resources"></a><span data-ttu-id="8be1a-141">Aggiungere tag alle risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-141">Tag resources</span></span>
<span data-ttu-id="8be1a-142">È possibile applicare tag tooresource gruppi e le risorse toologically organizzare le risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-142">You can apply tags tooresource groups and resources toologically organize your assets.</span></span> <span data-ttu-id="8be1a-143">Per informazioni sull'utilizzo di tag, vedere [tramite tag tooorganize le risorse di Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-143">For information about working with tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

[!INCLUDE [resource-manager-tag-resource](../../includes/resource-manager-tag-resources.md)]

## <a name="monitor-resources"></a><span data-ttu-id="8be1a-144">Monitorare le risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-144">Monitor resources</span></span>
<span data-ttu-id="8be1a-145">Quando si seleziona una risorsa, il pannello della risorsa hello presenta predefinito grafici e tabelle per il monitoraggio di tale tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="8be1a-145">When you select a resource, hello resource blade presents default graphs and tables for monitoring that resource type.</span></span>

1. <span data-ttu-id="8be1a-146">Selezionare una risorsa e notare di hello **monitoraggio** sezione.</span><span class="sxs-lookup"><span data-stu-id="8be1a-146">Select a resource and notice hello **Monitoring** section.</span></span> <span data-ttu-id="8be1a-147">Include grafici che sono il tipo di risorsa toohello pertinente.</span><span class="sxs-lookup"><span data-stu-id="8be1a-147">It includes graphs that are relevant toohello resource type.</span></span> <span data-ttu-id="8be1a-148">Hello immagine seguente mostra i dati per un account di archiviazione di monitoraggio predefinite hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-148">hello following image shows hello default monitoring data for a storage account.</span></span>
   
    ![visualizzare il monitoraggio](./media/resource-group-portal/show-monitoring.png)
2. <span data-ttu-id="8be1a-150">È possibile aggiungere una sezione di dashboard di hello pannello tooyour selezionando hello i puntini di sospensione (…) sopra la sezione hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-150">You can pin a section of hello blade tooyour dashboard by selecting hello ellipsis (...) above hello section.</span></span> <span data-ttu-id="8be1a-151">È anche possibile personalizzare hello dimensioni hello sezione nel pannello hello o rimuoverlo completamente.</span><span class="sxs-lookup"><span data-stu-id="8be1a-151">You can also customize hello size hello section in hello blade or remove it completely.</span></span> <span data-ttu-id="8be1a-152">Hello immagine seguente mostra come toopin, personalizzare o rimuovere una sezione di memoria e CPU hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-152">hello following image shows how toopin, customize, or remove hello CPU and Memory section.</span></span>
   
    ![sezione di aggiunta](./media/resource-group-portal/pin-cpu-section.png)
3. <span data-ttu-id="8be1a-154">Dopo aver aggiunto i dashboard di hello sezione toohello, hello riepilogo verrà visualizzato nel dashboard di hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-154">After pinning hello section toohello dashboard, you will see hello summary on hello dashboard.</span></span> <span data-ttu-id="8be1a-155">E, selezionandolo immediatamente accetta toomore dettagli sui dati hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-155">And, selecting it immediately takes you toomore details about hello data.</span></span>
   
    ![visualizzare il dashboard](./media/resource-group-portal/view-startboard.png)
4. <span data-ttu-id="8be1a-157">toocompletely personalizzare i dati di hello monitorare tramite il portale di hello, spostarsi dashboard predefinito tooyour e selezionare **nuovo dashboard**.</span><span class="sxs-lookup"><span data-stu-id="8be1a-157">toocompletely customize hello data you monitor through hello portal, navigate tooyour default dashboard, and select **New dashboard**.</span></span>
   
    ![dashboard](./media/resource-group-portal/dashboard.png)
5. <span data-ttu-id="8be1a-159">Denominare il nuovo dashboard e trascinare i riquadri nel dashboard hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-159">Give your new dashboard a name and drag tiles onto hello dashboard.</span></span> <span data-ttu-id="8be1a-160">Hello riquadri vengono filtrati in base a opzioni diverse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-160">hello tiles are filtered by different options.</span></span>
   
    ![dashboard](./media/resource-group-portal/create-dashboard.png)
   
     <span data-ttu-id="8be1a-162">toolearn sull'utilizzo dei dashboard, vedere [creazione e condivisione dei dashboard nel portale di Azure hello](../azure-portal/azure-portal-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-162">toolearn about working with dashboards, see [Creating and sharing dashboards in hello Azure portal](../azure-portal/azure-portal-dashboards.md).</span></span>

## <a name="manage-resources"></a><span data-ttu-id="8be1a-163">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-163">Manage resources</span></span>
<span data-ttu-id="8be1a-164">Nel pannello hello per una risorsa, vedrai opzioni hello per la gestione delle risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-164">In hello blade for a resource, you see hello options for managing hello resource.</span></span> <span data-ttu-id="8be1a-165">portale di Hello Visualizza opzioni di gestione per quel determinato tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="8be1a-165">hello portal presents management options for that particular resource type.</span></span> <span data-ttu-id="8be1a-166">Verranno visualizzati i comandi di gestione hello in alto di hello del pannello della risorsa hello e sul lato sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-166">You see hello management commands across hello top of hello resource blade and on hello left side.</span></span>

![Gestire risorse](./media/resource-group-portal/manage-resources.png)

<span data-ttu-id="8be1a-168">Da queste opzioni, è possibile eseguire operazioni quali l'avvio e arresto di una macchina virtuale o riconfigurare le proprietà di hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-168">From these options, you can perform operations such as starting and stopping a virtual machine, or reconfiguring hello properties of hello virtual machine.</span></span>

## <a name="move-resources"></a><span data-ttu-id="8be1a-169">Spostare le risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-169">Move resources</span></span>
<span data-ttu-id="8be1a-170">Se è necessario toomove risorse tooanother risorse gruppo o un'altra sottoscrizione, vedere [spostare sottoscrizione o il gruppo di risorse toonew risorse](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-170">If you need toomove resources tooanother resource group or another subscription, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>

## <a name="lock-resources"></a><span data-ttu-id="8be1a-171">Bloccare le risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-171">Lock resources</span></span>
<span data-ttu-id="8be1a-172">È possibile bloccare una sottoscrizione, un gruppo di risorse o una risorsa tooprevent ad altri utenti nell'organizzazione da un'accidentale eliminazione o modifica di risorse critiche.</span><span class="sxs-lookup"><span data-stu-id="8be1a-172">You can lock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="8be1a-173">Per altre informazioni, vedere [Bloccare le risorse con Gestione risorse di Azure](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-173">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="view-your-subscription-and-costs"></a><span data-ttu-id="8be1a-174">Visualizzare la sottoscrizione e i costi</span><span class="sxs-lookup"><span data-stu-id="8be1a-174">View your subscription and costs</span></span>
<span data-ttu-id="8be1a-175">È possibile visualizzare informazioni sui costi riportati hello e della sottoscrizione per tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-175">You can view information about your subscription and hello rolled-up costs for all your resources.</span></span> <span data-ttu-id="8be1a-176">Selezionare **sottoscrizioni** e sottoscrizione hello da toosee.</span><span class="sxs-lookup"><span data-stu-id="8be1a-176">Select **Subscriptions** and hello subscription you want toosee.</span></span> <span data-ttu-id="8be1a-177">È necessario solo un tooselect di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8be1a-177">You might only have one subscription tooselect.</span></span>

![sottoscrizione](./media/resource-group-portal/select-subscription.png)

<span data-ttu-id="8be1a-179">Nel Pannello di sottoscrizione hello, vedrai una velocità.</span><span class="sxs-lookup"><span data-stu-id="8be1a-179">Within hello subscription blade, you see a burn rate.</span></span>

![velocità](./media/resource-group-portal/burn-rate.png)

<span data-ttu-id="8be1a-181">E una suddivisione dei costi in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="8be1a-181">And, a breakdown of costs by resource type.</span></span>

![costo delle risorse](./media/resource-group-portal/cost-by-resource.png)

## <a name="export-template"></a><span data-ttu-id="8be1a-183">Esportare il modello</span><span class="sxs-lookup"><span data-stu-id="8be1a-183">Export template</span></span>
<span data-ttu-id="8be1a-184">Dopo aver configurato il gruppo di risorse, è opportuno modello di gestione risorse di hello tooview per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-184">After setting up your resource group, you may want tooview hello Resource Manager template for hello resource group.</span></span> <span data-ttu-id="8be1a-185">Esportazione modello hello offre due vantaggi:</span><span class="sxs-lookup"><span data-stu-id="8be1a-185">Exporting hello template offers two benefits:</span></span>

1. <span data-ttu-id="8be1a-186">È possibile automatizzare facilmente le distribuzioni future di soluzione hello perché il modello di hello contiene tutta l'infrastruttura completa hello.</span><span class="sxs-lookup"><span data-stu-id="8be1a-186">You can easily automate future deployments of hello solution because hello template contains all hello complete infrastructure.</span></span>
2. <span data-ttu-id="8be1a-187">È possibile acquisire familiarità con la sintassi dei modelli esaminando hello notazione JSON (JavaScript Object) che rappresenta la soluzione.</span><span class="sxs-lookup"><span data-stu-id="8be1a-187">You can become familiar with template syntax by looking at hello JavaScript Object Notation (JSON) that represents your solution.</span></span>

<span data-ttu-id="8be1a-188">Per istruzioni dettagliate, vedere [Esportare un modello di Azure Resource Manager da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-188">For step-by-step guidance, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="delete-resource-group-or-resources"></a><span data-ttu-id="8be1a-189">Eliminare risorse o gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="8be1a-189">Delete resource group or resources</span></span>
<span data-ttu-id="8be1a-190">Se si elimina un gruppo di risorse, tutte le risorse di hello in esso contenute.</span><span class="sxs-lookup"><span data-stu-id="8be1a-190">Deleting a resource group deletes all hello resources contained within it.</span></span> <span data-ttu-id="8be1a-191">È anche possibile eliminare singole risorse all'interno di un gruppo.</span><span class="sxs-lookup"><span data-stu-id="8be1a-191">You can also delete individual resources within a resource group.</span></span> <span data-ttu-id="8be1a-192">Si desidera tooexercise attenzione quando si elimina un gruppo di risorse perché in altri gruppi di risorse che sono collegati tooit potrebbero essere presenti risorse.</span><span class="sxs-lookup"><span data-stu-id="8be1a-192">You want tooexercise caution when you delete a resource group because there might be resources in other resource groups that are linked tooit.</span></span> <span data-ttu-id="8be1a-193">Gestione risorse non elimina le risorse collegate, ma potrebbero non funzionare correttamente senza risorse hello previsto.</span><span class="sxs-lookup"><span data-stu-id="8be1a-193">Resource Manager does not delete linked resources, but they may not operate correctly without hello expected resources.</span></span>

![eliminare un gruppo](./media/resource-group-portal/delete-group.png)

## <a name="next-steps"></a><span data-ttu-id="8be1a-195">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8be1a-195">Next steps</span></span>
* <span data-ttu-id="8be1a-196">log attività tooview, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-196">tooview activity logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="8be1a-197">Dettagli tooview su una distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-197">tooview details about a deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="8be1a-198">vedere le risorse toodeploy tramite il portale di hello [distribuire le risorse con modelli di gestione risorse e il portale di Azure](resource-group-template-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-198">toodeploy resources through hello portal, see [Deploy resources with Resource Manager templates and Azure portal](resource-group-template-deploy-portal.md).</span></span>
* <span data-ttu-id="8be1a-199">toomanage tooresources di accesso, vedere [utilizzare le risorse di sottoscrizione di Azure tooyour accesso toomanage assegnazioni ruolo](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-199">toomanage access tooresources, see [Use role assignments toomanage access tooyour Azure subscription resources](../active-directory/role-based-access-control-configure.md).</span></span>
* <span data-ttu-id="8be1a-200">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="8be1a-200">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

