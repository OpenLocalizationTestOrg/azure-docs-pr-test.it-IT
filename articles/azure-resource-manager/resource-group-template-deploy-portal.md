---
title: aaaUse toodeploy portale Azure le risorse di Azure | Documenti Microsoft
description: Utilizzare il portale di Azure e gestire risorse di Azure toodeploy le risorse.
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
ms.openlocfilehash: 5a5217f94c8dfc0c1ebd613903ea3dcbe1197bfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="38d05-103">Distribuire le risorse con i modelli di Azure Resource Manager e il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="38d05-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38d05-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38d05-104">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="38d05-105">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="38d05-105">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="38d05-106">Portale</span><span class="sxs-lookup"><span data-stu-id="38d05-106">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="38d05-107">API REST</span><span class="sxs-lookup"><span data-stu-id="38d05-107">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="38d05-108">Questo argomento viene illustrato come hello toouse [portale di Azure](https://portal.azure.com) con [Azure Resource Manager](resource-group-overview.md) toodeploy le risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="38d05-108">This topic shows how toouse hello [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) toodeploy your Azure resources.</span></span> <span data-ttu-id="38d05-109">toolearn sulla gestione delle risorse, vedere [le risorse di gestione di Azure tramite il portale](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-109">toolearn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="38d05-110">Attualmente, non a ogni servizio supporta portale hello o gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="38d05-110">Currently, not every service supports hello portal or Resource Manager.</span></span> <span data-ttu-id="38d05-111">Per tali servizi, è necessario hello toouse [portale classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="38d05-111">For those services, you need toouse hello [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="38d05-112">Per hello lo stato di ogni servizio, vedere [grafico disponibilità portale Azure](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="38d05-112">For hello status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="38d05-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="38d05-113">Create resource group</span></span>
1. <span data-ttu-id="38d05-114">Selezionare un gruppo di risorse vuoto, toocreate **New** > **Management** > **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="38d05-114">toocreate an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![creare un gruppo di risorse vuoto](./media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="38d05-116">Assegnare un nome e un percorso e, se necessario, selezionare una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="38d05-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="38d05-117">È necessario tooprovide un percorso per il gruppo di risorse hello perché il gruppo di risorse hello archivia i metadati sulle risorse hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-117">You need tooprovide a location for hello resource group because hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="38d05-118">Per motivi di conformità, è consigliabile toospecify archiviati che i metadati.</span><span class="sxs-lookup"><span data-stu-id="38d05-118">For compliance reasons, you may want toospecify where that metadata is stored.</span></span> <span data-ttu-id="38d05-119">In generale è consigliabile specificare un percorso in cui risiederà la maggior parte delle risorse.</span><span class="sxs-lookup"><span data-stu-id="38d05-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="38d05-120">Utilizzando hello stessa posizione può semplificare il modello.</span><span class="sxs-lookup"><span data-stu-id="38d05-120">Using hello same location can simplify your template.</span></span>
   
    ![impostare i valori del gruppo](./media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="38d05-122">Distribuire le risorse da Marketplace</span><span class="sxs-lookup"><span data-stu-id="38d05-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="38d05-123">Dopo aver creato un gruppo di risorse, è possibile distribuire le risorse tooit da hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="38d05-123">After you create a resource group, you can deploy resources tooit from hello Marketplace.</span></span> <span data-ttu-id="38d05-124">Hello Marketplace fornisce soluzioni predefinite per gli scenari comuni.</span><span class="sxs-lookup"><span data-stu-id="38d05-124">hello Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="38d05-125">toostart una distribuzione, selezionare **New** e hello tipo di risorsa desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="38d05-125">toostart a deployment, select **New** and hello type of resource you would like toodeploy.</span></span> <span data-ttu-id="38d05-126">Esaminare per una particolare versione di hello della risorsa hello quali toodeploy.</span><span class="sxs-lookup"><span data-stu-id="38d05-126">Then, look for hello particular version of hello resource you would like toodeploy.</span></span>
   
    ![distribuire risorse](./media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="38d05-128">Se non viene visualizzata particolare soluzione hello toodeploy desiderato, è possibile cercare hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="38d05-128">If you do not see hello particular solution you would like toodeploy, you can search hello Marketplace for it.</span></span>
   
    ![cercare nel Marketplace](./media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="38d05-130">A seconda di tipo hello di risorse selezionato, è una raccolta di proprietà rilevanti tooset prima della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="38d05-130">Depending on hello type of selected resource, you have a collection of relevant properties tooset before deployment.</span></span> <span data-ttu-id="38d05-131">Le opzioni non sono visualizzate in questo articolo, perché variano in base al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="38d05-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="38d05-132">Per tutti i tipi è necessario selezionare un gruppo di risorse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="38d05-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="38d05-133">esempio Hello figura viene illustrato come toocreate un'app web e distribuirlo toohello gruppo di risorse creato.</span><span class="sxs-lookup"><span data-stu-id="38d05-133">hello following image shows how toocreate a web app and deploy it toohello resource group you created.</span></span>
   
    ![Creare un gruppo di risorse](./media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="38d05-135">In alternativa, è possibile decidere toocreate un gruppo di risorse durante la distribuzione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="38d05-135">Alternatively, you can decide toocreate a resource group when deploying your resources.</span></span> <span data-ttu-id="38d05-136">Selezionare **Crea nuovo** e assegnare un nome di gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-136">Select **Create new** and give hello resource group a name.</span></span>
   
    ![creare un nuovo gruppo di risorse](./media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="38d05-138">La distribuzione ha inizio.</span><span class="sxs-lookup"><span data-stu-id="38d05-138">Your deployment begins.</span></span> <span data-ttu-id="38d05-139">distribuzione di Hello potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="38d05-139">hello deployment could take a few minutes.</span></span> <span data-ttu-id="38d05-140">Al termine della distribuzione di hello, viene visualizzata una notifica.</span><span class="sxs-lookup"><span data-stu-id="38d05-140">When hello deployment has finished, you see a notification.</span></span>
   
    ![visualizzare notifiche](./media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="38d05-142">Dopo la distribuzione delle risorse, è possibile aggiungere un gruppo di risorse di ulteriori risorse toohello utilizzando hello **Aggiungi** comando pannello della risorsa gruppo hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-142">After deploying your resources, you can add more resources toohello resource group by using hello **Add** command on hello resource group blade.</span></span>
   
    ![aggiungere una risorsa](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="38d05-144">Distribuire risorse da un modello personalizzato</span><span class="sxs-lookup"><span data-stu-id="38d05-144">Deploy resources from custom template</span></span>
<span data-ttu-id="38d05-145">Se si desidera tooexecute una distribuzione ma non utilizzare nessuno dei modelli di hello in hello Marketplace, è possibile creare un modello personalizzato che definisce l'infrastruttura di hello per la soluzione.</span><span class="sxs-lookup"><span data-stu-id="38d05-145">If you want tooexecute a deployment but not use any of hello templates in hello Marketplace, you can create a customized template that defines hello infrastructure for your solution.</span></span> <span data-ttu-id="38d05-146">toolearn sulla creazione di modelli, vedere [modelli Authoring Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-146">toolearn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="38d05-147">Selezionare un modello personalizzato tramite il portale di hello toodeploy **New**e iniziare a cercare **distribuzione modello** fino a quando non è possibile scegliere le opzioni di hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-147">toodeploy a customized template through hello portal, select **New**, and start searching for **Template Deployment** until you can select it from hello options.</span></span>
   
    ![cercare la distribuzione del modello](./media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="38d05-149">Selezionare **distribuzione modello** dalle risorse disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-149">Select **Template Deployment** from hello available resources.</span></span>
   
    ![selezionare la distribuzione del modello](./media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="38d05-151">Dopo aver avviato la distribuzione dei modelli di hello, aprire il modello vuoto hello che è disponibile per la personalizzazione.</span><span class="sxs-lookup"><span data-stu-id="38d05-151">After launching hello template deployment, open hello blank template that is available for customizing.</span></span>
   
    ![creare un modello](./media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="38d05-153">Nell'editor di hello, aggiungere la sintassi JSON hello che definisce le risorse di hello desiderato toodeploy.</span><span class="sxs-lookup"><span data-stu-id="38d05-153">In hello editor, add hello JSON syntax that defines hello resources you want toodeploy.</span></span> <span data-ttu-id="38d05-154">Al termine, selezionare **Salva** .</span><span class="sxs-lookup"><span data-stu-id="38d05-154">Select **Save** when done.</span></span> <span data-ttu-id="38d05-155">Per istruzioni su come scrivere la sintassi JSON hello, vedere [procedura dettagliata di modello di gestione risorse](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-155">For guidance on writing hello JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![modificare un modello](./media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="38d05-157">In alternativa, è possibile selezionare un modello esistente da hello [modelli di avvio rapido di Azure](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="38d05-157">Or, you can select a pre-existing template from hello [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="38d05-158">Questi modelli vengono forniti dalla community di hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-158">These templates are contributed by hello community.</span></span> <span data-ttu-id="38d05-159">Coprono molti scenari comuni e un utente può essere aggiunti a un modello simile toowhat che si sta tentando di toodeploy.</span><span class="sxs-lookup"><span data-stu-id="38d05-159">They cover many common scenarios, and someone may have added a template that is similar toowhat you are trying toodeploy.</span></span> <span data-ttu-id="38d05-160">È possibile cercare hello modelli toofind un elemento che corrisponde allo scenario.</span><span class="sxs-lookup"><span data-stu-id="38d05-160">You can search hello templates toofind something that matches your scenario.</span></span>
   
    ![selezionare un modello di Guida introduttiva](./media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="38d05-162">È possibile visualizzare modello selezionato hello nell'editor di hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-162">You can view hello selected template in hello editor.</span></span>
5. <span data-ttu-id="38d05-163">Dopo aver fornito hello tutti gli altri valori, selezionare **crea** modello hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="38d05-163">After providing all hello other values, select **Create** toodeploy hello template.</span></span> 
   
    ![distribuire un modello](./media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-tooyour-account"></a><span data-ttu-id="38d05-165">Distribuire le risorse da un modello salvato tooyour account</span><span class="sxs-lookup"><span data-stu-id="38d05-165">Deploy resources from a template saved tooyour account</span></span>
<span data-ttu-id="38d05-166">portale Hello consente si toosave tooyour un modello account Azure e distribuirlo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="38d05-166">hello portal enables you toosave a template tooyour Azure account, and redeploy it later.</span></span> <span data-ttu-id="38d05-167">Per ulteriori informazioni sull'utilizzo di questi modelli, salvato [introduzione privati modelli nel portale di Azure hello](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-167">For more information about working with these saved templates, [Get started with private templates on hello Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="38d05-168">Selezionare i modelli salvati, toofind **Sfoglia** > **modelli**.</span><span class="sxs-lookup"><span data-stu-id="38d05-168">toofind your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![esplorare i modelli](./media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="38d05-170">Hello l'elenco dei modelli salvati tooyour account, selezionare quello che si desidera toowork su hello.</span><span class="sxs-lookup"><span data-stu-id="38d05-170">From hello list of templates saved tooyour account, select hello one you wish toowork on.</span></span>
   
    ![modelli salvati](./media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="38d05-172">Selezionare **Distribuisci** tooredeploy questo modello salvato.</span><span class="sxs-lookup"><span data-stu-id="38d05-172">Select **Deploy** tooredeploy this saved template.</span></span>
   
    ![distribuire un modello salvato](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="38d05-174">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38d05-174">Next steps</span></span>
* <span data-ttu-id="38d05-175">vedere i log di controllo, tooview [controllare le operazioni con Gestione risorse di](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-175">tooview audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="38d05-176">vedere gli errori di distribuzione, tootroubleshoot [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-176">tootroubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="38d05-177">tooretrieve un modello da una distribuzione o un gruppo di risorse, vedere [modello esportare Gestione risorse di Azure da risorse esistenti](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-177">tooretrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="38d05-178">Per istruzioni su come le aziende possono usare tooeffectively Gestione risorse di gestione di sottoscrizioni, vedere [lo scaffolding di Azure enterprise - governance sottoscrizione rigorosa](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="38d05-178">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

