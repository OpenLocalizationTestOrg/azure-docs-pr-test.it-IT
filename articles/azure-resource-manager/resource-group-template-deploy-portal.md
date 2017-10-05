---
title: Uso del portale di Azure per distribuire le risorse di Azure | Microsoft Docs
description: Utilizzare il portale di Azure e Azure Resource Manager per distribuire le risorse.
services: azure-resource-manager,azure-portal
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: a4cac5834c667976b0a2d1f2748e4309a166d16a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="ff044-103">Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ff044-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff044-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff044-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="ff044-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="ff044-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="ff044-106">Portale</span><span class="sxs-lookup"><span data-stu-id="ff044-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="ff044-107">API REST</span><span class="sxs-lookup"><span data-stu-id="ff044-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="ff044-108">Questo argomento illustra come usare il [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) per distribuire le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ff044-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="ff044-109">Per altre informazioni sulla gestione delle risorse, vedere [Gestire le risorse di Azure mediante il portale](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="ff044-110">Non tutti i servizi attualmente supportano il portale o Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="ff044-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="ff044-111">Per questi servizi sarà necessario usare il [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ff044-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="ff044-112">Per lo stato di ogni servizio, vedere il [grafico della disponibilità del portale di Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="ff044-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="ff044-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ff044-113">Create resource group</span></span>
1. <span data-ttu-id="ff044-114">Per creare un gruppo di risorse vuoto, selezionare **Nuovo** > **Gestione** > **Gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="ff044-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![creare un gruppo di risorse vuoto](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="ff044-116">Assegnare un nome e un percorso e, se necessario, selezionare una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ff044-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="ff044-117">È necessario specificare un percorso per il gruppo di risorse perché nel gruppo di risorse vengono archiviati i metadati delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ff044-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="ff044-118">Per motivi di conformità può essere opportuno specificare dove vengono archiviati i metadati.</span><span class="sxs-lookup"><span data-stu-id="ff044-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="ff044-119">In generale è consigliabile specificare un percorso in cui risiederà la maggior parte delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ff044-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="ff044-120">Usando lo stesso percorso è possibile semplificare il modello.</span><span class="sxs-lookup"><span data-stu-id="ff044-120">Using the same location can simplify your template.</span></span>
   
    ![impostare i valori del gruppo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="ff044-122">Distribuire le risorse da Marketplace</span><span class="sxs-lookup"><span data-stu-id="ff044-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="ff044-123">Dopo aver creato il gruppo di risorse, è possibile distribuire le risorse da Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ff044-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="ff044-124">Marketplace fornisce soluzioni predefinite per scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="ff044-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="ff044-125">Per avviare una distribuzione, selezionare **Nuovo** e il tipo di risorsa da distribuire.</span><span class="sxs-lookup"><span data-stu-id="ff044-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="ff044-126">Dopodiché, cercare la versione specifica della risorsa che si desidera distribuire.</span><span class="sxs-lookup"><span data-stu-id="ff044-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![distribuire risorse](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="ff044-128">Se la specifica soluzione che si desidera distribuire non è visualizzata, è possibile cercarla nel Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ff044-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![cercare nel Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="ff044-130">A seconda del tipo di risorsa selezionato, sarà necessario impostare una serie di proprietà pertinenti prima della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ff044-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="ff044-131">Le opzioni non sono visualizzate in questo articolo, perché variano in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="ff044-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="ff044-132">Per tutti i tipi è necessario selezionare un gruppo di risorse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ff044-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="ff044-133">L'immagine seguente mostra come creare un'app Web e distribuirla nel gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="ff044-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![Creare un gruppo di risorse](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="ff044-135">In alternativa, è possibile decidere di creare un gruppo di risorse durante la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="ff044-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="ff044-136">Selezionare **Crea nuovo** e assegnare un nome al gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="ff044-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![creare un nuovo gruppo di risorse](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="ff044-138">La distribuzione ha inizio.</span><span class="sxs-lookup"><span data-stu-id="ff044-138">Your deployment begins.</span></span> <span data-ttu-id="ff044-139">La distribuzione può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="ff044-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="ff044-140">Al termine della distribuzione verrà visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="ff044-140">When the deployment has finished, you see a notification.</span></span>
   
    ![visualizzare notifiche](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="ff044-142">Dopo aver distribuito le risorse, è possibile aggiungerne altre al gruppo di risorse usando il comando **Aggiungi** nel pannello del gruppo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="ff044-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![aggiungere una risorsa](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="ff044-144">Distribuire risorse da un modello personalizzato</span><span class="sxs-lookup"><span data-stu-id="ff044-144">Deploy resources from custom template</span></span>
<span data-ttu-id="ff044-145">Se si desidera eseguire una distribuzione ma non usare i modelli in Marketplace, è possibile creare un modello personalizzato che definisce l'infrastruttura per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="ff044-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="ff044-146">Per altre informazioni sulla creazione dei modelli, vedere [Creazione di modelli di Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="ff044-147">Per distribuire un modello personalizzato tramite il portale, selezionare **Nuovo** e quindi iniziare a digitare **Distribuzione modello** nella casella di ricerca fino a quando non è selezionabile nelle opzioni.</span><span class="sxs-lookup"><span data-stu-id="ff044-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![cercare la distribuzione del modello](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="ff044-149">Selezionare **Distribuzione modello** nelle risorse disponibili.</span><span class="sxs-lookup"><span data-stu-id="ff044-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![selezionare la distribuzione del modello](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="ff044-151">Dopo aver avviato la distribuzione del modello, aprire il modello vuoto disponibile per la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="ff044-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![creare un modello](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="ff044-153">Nell'editor, aggiungere la sintassi JSON che definisce le risorse da distribuire.</span><span class="sxs-lookup"><span data-stu-id="ff044-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="ff044-154">Al termine, selezionare **Salva** .</span><span class="sxs-lookup"><span data-stu-id="ff044-154">Select **Save** when done.</span></span> <span data-ttu-id="ff044-155">Per indicazioni sulla scrittura della sintassi JSON, vedere [Procedura dettagliata per un modello di Resource Manager](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![modificare un modello](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="ff044-157">In alternativa, è possibile selezionare un modello preesistente dai [Modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="ff044-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="ff044-158">Questi modelli sono forniti dalla community.</span><span class="sxs-lookup"><span data-stu-id="ff044-158">These templates are contributed by the community.</span></span> <span data-ttu-id="ff044-159">I modelli sono relativi a molti scenari comuni ed è possibile che qualcuno abbia aggiunto un modello simile a quello che si sta provando a distribuire.</span><span class="sxs-lookup"><span data-stu-id="ff044-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="ff044-160">È possibile eseguire ricerche nei modelli per trovare aspetti corrispondenti al proprio scenario.</span><span class="sxs-lookup"><span data-stu-id="ff044-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![selezionare un modello di Guida introduttiva](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="ff044-162">È possibile visualizzare il modello selezionato nell'editor.</span><span class="sxs-lookup"><span data-stu-id="ff044-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="ff044-163">Dopo aver fornito tutti gli altri valori, selezionare **Crea** per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ff044-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![distribuire un modello](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="ff044-165">Distribuire risorse da un modello salvato nel proprio account</span><span class="sxs-lookup"><span data-stu-id="ff044-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="ff044-166">Il portale consente di salvare un modello nel proprio account Azure e di ridistribuirlo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="ff044-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="ff044-167">Per altre informazioni sull'uso dei modelli salvati, vedere [Introduzione ai modelli privati nel portale di Azure](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="ff044-168">Per trovare i modelli salvati, selezionare **Esplora** > **Modelli**.</span><span class="sxs-lookup"><span data-stu-id="ff044-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![esplorare i modelli](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="ff044-170">Nell'elenco dei modelli salvati nel proprio account selezionare quello che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="ff044-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![modelli salvati](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="ff044-172">Selezionare **Distribuisci** per ridistribuire il modello salvato.</span><span class="sxs-lookup"><span data-stu-id="ff044-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![distribuire un modello salvato](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="ff044-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ff044-174">Next steps</span></span>
* <span data-ttu-id="ff044-175">Per visualizzare i log di controllo, vedere [Operazioni di controllo con Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="ff044-176">Per risolvere gli errori di distribuzione, vedere [View deployment operations](resource-manager-deployment-operations.md) (Visualizzare le operazioni di distribuzione).</span><span class="sxs-lookup"><span data-stu-id="ff044-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="ff044-177">Per recuperare un modello da un gruppo di risorse o di distribuzione, vedere [Esportare un modello di Azure Resource Manager da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="ff044-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="ff044-178">Per indicazioni su come le aziende possono usare Resource Manager per gestire efficacemente le sottoscrizioni, vedere [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md) (Scaffolding aziendale Azure - Governance prescrittiva per le sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="ff044-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

