---
title: "Set di scalabilità macchina virtuale utilizzando Visual Studio aaaDeploy | Documenti Microsoft"
description: "Distribuire set di scalabilità di macchine virtuali tramite Visual Studio e un modello di Resource Manager"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="f94dd-103">Come toocreate Set di scalabilità di macchine virtuali con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f94dd-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="f94dd-104">Questo articolo illustra come toodeploy una scalabilità di macchine virtuali di Azure impostare l'utilizzo di una distribuzione a gruppo di risorse di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f94dd-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="f94dd-105">[Set di scalabilità di macchine virtuali Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) è un toodeploy risorse di calcolo di Azure e gestire una raccolta di macchine virtuali simili con scalabilità automatica e il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f94dd-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="f94dd-106">È possibile eseguire il provisioning e distribuire set di scalabilità di macchine virtuali tramite i [modelli di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="f94dd-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="f94dd-107">I modelli di Azure Resource Manager possono essere distribuiti tramite l'interfaccia della riga di comando di Azure, PowerShell, REST e direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f94dd-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="f94dd-108">Visual Studio offre un set di modelli di esempio che possono essere distribuiti come parte di un progetto di distribuzione del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94dd-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="f94dd-109">Distribuzioni del gruppo di risorse di Azure sono un modo toogroup e pubblicano un set di risorse di Azure correlate in una sola operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="f94dd-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="f94dd-110">Sono disponibili altre informazioni in [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="f94dd-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="f94dd-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f94dd-111">Pre-requisites</span></span>
<span data-ttu-id="f94dd-112">tooget avviata la distribuzione di set di scalabilità di macchine virtuali in Visual Studio, è necessario seguente hello:</span><span class="sxs-lookup"><span data-stu-id="f94dd-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="f94dd-113">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="f94dd-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="f94dd-114">Azure SDK 2.7, 2.8 o 2.9</span><span class="sxs-lookup"><span data-stu-id="f94dd-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="f94dd-115">Queste istruzioni presuppongono l'uso di Visual Studio con [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="f94dd-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="f94dd-116">Creazione di un progetto</span><span class="sxs-lookup"><span data-stu-id="f94dd-116">Creating a Project</span></span>
1. <span data-ttu-id="f94dd-117">Creare un nuovo progetto in Visual Studio scegliendo **File | Nuovo | Progetto**.</span><span class="sxs-lookup"><span data-stu-id="f94dd-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![File Nuovo][file_new]

2. <span data-ttu-id="f94dd-119">In **Visual c# | Cloud**, scegliere **Azure Resource Manager** toocreate un progetto per la distribuzione di un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94dd-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Crea progetto][create_project]

3. <span data-ttu-id="f94dd-121">Hello l'elenco dei modelli, selezionare hello Linux o modello di impostare scala macchina virtuale Windows.</span><span class="sxs-lookup"><span data-stu-id="f94dd-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Seleziona modello][select_Template]

4. <span data-ttu-id="f94dd-123">Una volta creato il progetto vedere PowerShell script di distribuzione, un modello di gestione risorse di Azure e un file di parametro per hello Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f94dd-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Esplora soluzioni][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="f94dd-125">Personalizzare il progetto</span><span class="sxs-lookup"><span data-stu-id="f94dd-125">Customize your project</span></span>
<span data-ttu-id="f94dd-126">Ora è possibile modificare toocustomize modello hello per le esigenze dell'applicazione, ad esempio l'aggiunta di proprietà di estensione di macchina virtuale o la modifica di caricare le regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="f94dd-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="f94dd-127">Per impostazione predefinita modelli di impostare hello macchina virtuale scala sono configurati toodeploy hello AzureDiagnostics estensione rende facile tooadd regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="f94dd-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="f94dd-128">L'estensione inoltre distribuisce un servizio di bilanciamento del carico con un indirizzo IP pubblico, configurato con regole NAT in entrata.</span><span class="sxs-lookup"><span data-stu-id="f94dd-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="f94dd-129">bilanciamento del carico Hello consente di connettersi a istanze di macchina virtuale toohello con SSH (Linux) o RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="f94dd-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="f94dd-130">intervallo di porte front-end di Hello inizia in corrispondenza di 50000.</span><span class="sxs-lookup"><span data-stu-id="f94dd-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="f94dd-131">Per linux, questo significa che se si SSH tooport 50000, si è indirizzato tooport 22 di hello prima macchina virtuale nel Set di scalabilità hello.</span><span class="sxs-lookup"><span data-stu-id="f94dd-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="f94dd-132">Connessione tooport 50001 è indirizzato tooport 22 di hello seconda macchina virtuale e così via.</span><span class="sxs-lookup"><span data-stu-id="f94dd-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="f94dd-133">Tooedit un modo efficace i modelli con Visual Studio è toouse hello struttura JSON tooorganize hello parametri, variabili e le risorse.</span><span class="sxs-lookup"><span data-stu-id="f94dd-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="f94dd-134">Una conoscenza di hello schema Visual Studio può indicare errori nel modello prima di distribuirlo.</span><span class="sxs-lookup"><span data-stu-id="f94dd-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Esplora JSON][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="f94dd-136">Distribuire il progetto hello</span><span class="sxs-lookup"><span data-stu-id="f94dd-136">Deploy hello project</span></span>
1. <span data-ttu-id="f94dd-137">Distribuire hello Azure Resource Manager risorsa modello di toocreate hello Set di scalabilità della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f94dd-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="f94dd-138">Fare clic sul nodo del progetto hello e scegliere **Distribuisci | Nuova distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="f94dd-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Modello di distribuzione][5deploy_Template]
    
2. <span data-ttu-id="f94dd-140">Nella finestra di dialogo "Distribuisci tooResource gruppo" hello, selezionare la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f94dd-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![Modello di distribuzione][6deploy_Template]

3. <span data-ttu-id="f94dd-142">Da qui è possibile creare il modello per toodeploy un gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="f94dd-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![Nuovo gruppo di risorse][new_resource]

4. <span data-ttu-id="f94dd-144">Successivamente, fare clic su **modifica parametri** tooenter i parametri passati tooyour modello.</span><span class="sxs-lookup"><span data-stu-id="f94dd-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="f94dd-145">Prevedere hello del sistema operativo, che è necessario toocreate hello distribuzione hello username e password.</span><span class="sxs-lookup"><span data-stu-id="f94dd-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="f94dd-146">Se non si dispone di PowerShell Tools per Visual Studio installata, è consigliabile toocheck **salvare le password** tooavoid un nascosti della riga di comando di PowerShell richiedere o utilizzare [keyvault supporto](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="f94dd-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Modifica parametri][edit_parameters]

5. <span data-ttu-id="f94dd-148">Fare quindi clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="f94dd-148">Now click **Deploy**.</span></span> <span data-ttu-id="f94dd-149">Hello **Output** finestra viene visualizzato l'avanzamento della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="f94dd-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="f94dd-150">Si noti che l'azione hello esegue hello **deploy-azureresourcegroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="f94dd-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Finestra Output][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="f94dd-152">Esplorare il set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="f94dd-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="f94dd-153">Una volta completata la distribuzione di hello, è possibile visualizzare hello nuova macchina virtuale Set di scalabilità in Visual Studio hello **Cloud Explorer** (aggiornamento hello elenco).</span><span class="sxs-lookup"><span data-stu-id="f94dd-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="f94dd-154">Cloud Explorer consente di gestire le risorse di Azure in Visual Studio durante lo sviluppo di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="f94dd-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="f94dd-155">È inoltre possibile visualizzare il Set di scalabilità della macchina virtuale in hello [portale di Azure](https://portal.azure.com) e [Esplora inventario risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f94dd-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="f94dd-157">portale Hello fornisce migliore hello toovisually gestire l'infrastruttura di Azure con un web browser, mentre Esplora inventario risorse di Azure fornisce un modo semplice di tooexplore e debug delle risorse di Azure, offrendo una finestra in hello "visualizzazione di istanza" e anche con PowerShell comandi per le risorse di hello che si sta esaminando.</span><span class="sxs-lookup"><span data-stu-id="f94dd-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f94dd-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f94dd-158">Next steps</span></span>
<span data-ttu-id="f94dd-159">Dopo aver distribuito il set di scalabilità di macchine virtuali tramite Visual Studio, è possibile personalizzare ulteriormente toosuit il progetto dei requisiti dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="f94dd-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="f94dd-160">Ad esempio, configurare scalabilità automatica tramite l'aggiunta di un **Insights** della risorsa, l'aggiunta di infrastruttura tooyour modello (ad esempio macchine virtuali autonome) o distribuzione di applicazioni mediante l'estensione script personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="f94dd-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="f94dd-161">Modelli di esempio sono disponibili in hello [modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates) repository GitHub (ricerca di "vmss").</span><span class="sxs-lookup"><span data-stu-id="f94dd-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
