---
title: "Distribuire un set di scalabilità di macchine virtuali tramite Visual Studio | Microsoft Docs"
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
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="ea5c7-103">Come creare un set di scalabilità di macchine virtuali con Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea5c7-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="ea5c7-104">Questo articolo descrive come distribuire un set di scalabilità della macchina virtuale di Azure usando una distribuzione del gruppo di risorse di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="ea5c7-105">[Set di scalabilità di macchine virtuali di Azure](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) è una risorsa di calcolo di Azure per distribuire e gestire una raccolta di macchine virtuali simili con scalabilità automatica e bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="ea5c7-106">È possibile eseguire il provisioning e distribuire set di scalabilità di macchine virtuali tramite i [modelli di Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="ea5c7-107">I modelli di Azure Resource Manager possono essere distribuiti tramite l'interfaccia della riga di comando di Azure, PowerShell, REST e direttamente da Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="ea5c7-108">Visual Studio offre un set di modelli di esempio che possono essere distribuiti come parte di un progetto di distribuzione del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="ea5c7-109">Le distribuzioni del gruppo di risorse di Azure sono un modo di raggruppare e pubblicare un set di risorse di Azure correlate con un'unica operazione di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="ea5c7-110">Sono disponibili altre informazioni in [Creazione e distribuzione di gruppi di risorse di Azure tramite Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="ea5c7-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ea5c7-111">Pre-requisites</span></span>
<span data-ttu-id="ea5c7-112">Per iniziare a distribuire set di scalabilità di macchine virtuali in Visual Studio è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ea5c7-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="ea5c7-113">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="ea5c7-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="ea5c7-114">Azure SDK 2.7, 2.8 o 2.9</span><span class="sxs-lookup"><span data-stu-id="ea5c7-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="ea5c7-115">Queste istruzioni presuppongono l'uso di Visual Studio con [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="ea5c7-116">Creazione di un progetto</span><span class="sxs-lookup"><span data-stu-id="ea5c7-116">Creating a Project</span></span>
1. <span data-ttu-id="ea5c7-117">Creare un nuovo progetto in Visual Studio scegliendo **File | Nuovo | Progetto**.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![File Nuovo][file_new]

2. <span data-ttu-id="ea5c7-119">In **Visual C# | Cloud** scegliere **Azure Resource Manager** per creare un progetto per la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Crea progetto][create_project]

3. <span data-ttu-id="ea5c7-121">Dall'elenco dei modelli, selezionare il modello di set di scalabilità della macchina virtuale Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Seleziona modello][select_Template]

4. <span data-ttu-id="ea5c7-123">Dopo aver creato il progetto saranno disponibili gli script di distribuzione di PowerShell, un modello di Azure Resource Manager e un file di parametri per il set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Esplora soluzioni][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="ea5c7-125">Personalizzare il progetto</span><span class="sxs-lookup"><span data-stu-id="ea5c7-125">Customize your project</span></span>
<span data-ttu-id="ea5c7-126">È ora possibile modificare il modello per personalizzarlo in base alle esigenze dell'applicazione, ad esempio aggiungendo proprietà di estensione della macchina virtuale o modificando le regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="ea5c7-127">Per impostazione predefinita, i modelli del set di scalabilità di macchine virtuali sono configurati in modo da distribuire l'estensione AzureDiagnostics, che semplifica l'aggiunta di regole di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="ea5c7-128">L'estensione inoltre distribuisce un servizio di bilanciamento del carico con un indirizzo IP pubblico, configurato con regole NAT in entrata.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="ea5c7-129">Il servizio di bilanciamento del carico consente di connettersi alle istanze della macchina virtuale con SSH (Linux) o RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="ea5c7-130">L'intervallo di porte front-end inizia da 50000.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="ea5c7-131">Per Linux ciò significa che se si usa SSH con la porta 50000, si viene instradati alla porta 22 della prima macchina virtuale nel set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="ea5c7-132">La connessione alla porta 50001 determina l'instradamento alla porta 22 della seconda macchina virtuale e così via.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="ea5c7-133">Un buon metodo per modificare i modelli con Visual Studio consiste nell'usare la struttura JSON per organizzare i parametri, le variabili e le risorse.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="ea5c7-134">Comprendendo lo schema, Visual Studio è in grado di indicare errori nel modello prima che venga distribuito.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![Esplora JSON][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="ea5c7-136">Distribuire il progetto</span><span class="sxs-lookup"><span data-stu-id="ea5c7-136">Deploy the project</span></span>
1. <span data-ttu-id="ea5c7-137">Distribuire il modello di Azure Resource Manager per creare la risorsa set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="ea5c7-138">Fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Distribuisci | Nuova distribuzione**.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Modello di distribuzione][5deploy_Template]
    
2. <span data-ttu-id="ea5c7-140">Selezionare la sottoscrizione nella finestra di dialogo "Distribuisci in gruppo di risorse".</span><span class="sxs-lookup"><span data-stu-id="ea5c7-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Modello di distribuzione][6deploy_Template]

3. <span data-ttu-id="ea5c7-142">Da qui è possibile creare un gruppo di risorse di Azure a cui distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![Nuovo gruppo di risorse][new_resource]

4. <span data-ttu-id="ea5c7-144">Successivamente, fare clic su **Modifica parametri** per immettere i parametri trasmessi al modello.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="ea5c7-145">Specificare nome utente e password per il sistema operativo, che servono per creare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="ea5c7-146">Se PowerShell Tools for Visual Studio non è installato, è consigliabile selezionare **Salva password** per evitare un prompt della riga di comando di PowerShell nascosto, oppure usare il [supporto dell'insieme di credenziali delle chiavi](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Modifica parametri][edit_parameters]

5. <span data-ttu-id="ea5c7-148">Fare quindi clic su **Distribuisci**.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-148">Now click **Deploy**.</span></span> <span data-ttu-id="ea5c7-149">La finestra **Output** visualizza lo stato della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="ea5c7-150">Si noti che l'azione esegue lo script **Deploy-AzureResourceGroup.ps1** .</span><span class="sxs-lookup"><span data-stu-id="ea5c7-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Finestra Output][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="ea5c7-152">Esplorare il set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="ea5c7-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="ea5c7-153">Al termine della distribuzione, è possibile visualizzare il nuovo set di scalabilità di macchine virtuali in **Cloud Explorer** di Visual Studio (aggiornare l'elenco).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="ea5c7-154">Cloud Explorer consente di gestire le risorse di Azure in Visual Studio durante lo sviluppo di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="ea5c7-155">È anche possibile visualizzare il set di scalabilità di macchine virtuali nel [Portale di Azure](https://portal.azure.com) e in [Esplora inventario risorse di Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ea5c7-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="ea5c7-157">Il portale rappresenta il modo migliore per gestire la visualizzazione dell'infrastruttura di Azure con un Web browser, mentre Azure Resource Explorer offre un modo semplice per esplorare le risorse di Azure ed eseguirne il debug, offrendo una "visualizzazione per istanza" e visualizzando anche i comandi PowerShell per le risorse che si stanno analizzando.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea5c7-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ea5c7-158">Next steps</span></span>
<span data-ttu-id="ea5c7-159">Dopo aver distribuito i set di scalabilità di macchine virtuali tramite Visual Studio è possibile personalizzare ulteriormente il progetto in base alle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="ea5c7-160">Ad esempio, è possibile configurare la scalabilità automatica aggiungendo una risorsa di **Insights**, aggiungendo l'infrastruttura al modello (ad esempio macchine virtuali autonome) o distribuendo applicazioni con l'estensione dello script personalizzata.</span><span class="sxs-lookup"><span data-stu-id="ea5c7-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="ea5c7-161">Alcuni esempi utili di modelli sono disponibili nel repository GitHub dedicato ai [modelli della guida introduttiva di Azure](https://github.com/Azure/azure-quickstart-templates) (cercare "vmss").</span><span class="sxs-lookup"><span data-stu-id="ea5c7-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
