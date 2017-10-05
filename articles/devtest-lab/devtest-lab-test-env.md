---
title: Usare Azure DevTest Labs per macchine virtuali e ambienti di test PaaS | Microsoft Docs
description: Informazioni su come usare Azure DevTest Labs per macchine virtuali scenari di ambienti di test PaaS.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: a556cee9d7b665cd7df23c97e7e2c8c2afabbe58
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/29/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="1acd2-103">Usare Azure DevTest Labs per macchine virtuali e ambienti di test PaaS</span><span class="sxs-lookup"><span data-stu-id="1acd2-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="1acd2-104">Azure DevTest Labs può essere usato per implementare molti scenari chiave. Uno dei più importanti prevede l'uso di DevTest Labs per ospitare computer per i tester.</span><span class="sxs-lookup"><span data-stu-id="1acd2-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="1acd2-105">In questo scenario DevTest Labs offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="1acd2-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="1acd2-106">I tester possono provare la versione più recente dell'applicazione eseguendo rapidamente il provisioning di ambienti Windows e Linux tramite modelli ed elementi riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="1acd2-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="1acd2-107">Possono anche aumentare i test di carico eseguendo il provisioning di più agenti di test.</span><span class="sxs-lookup"><span data-stu-id="1acd2-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="1acd2-108">Gli amministratori possono controllare i costi assicurandosi che:</span><span class="sxs-lookup"><span data-stu-id="1acd2-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="1acd2-109">I tester non possano ottenere più macchine virtuali del necessario per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="1acd2-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="1acd2-110">Le VM vengano arrestate quando non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="1acd2-110">VMs are shut down when not in use.</span></span>

![Usare DevTest Labs per il training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="1acd2-112">Questo articolo illustra le diverse funzionalità di Azure DevTest Labs usate per soddisfare i requisiti dei tester e i passaggi dettagliati da seguire per configurare un lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="1acd2-113">Implementazione di ambienti di test con Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1acd2-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="1acd2-114">**Creare il lab**</span><span class="sxs-lookup"><span data-stu-id="1acd2-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="1acd2-115">I lab sono il punto di partenza in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="1acd2-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="1acd2-116">Dopo avere creato un lab, è possibile eseguire attività quali aggiungere utenti, ovvero tester, al lab, impostare criteri per controllare i costi, definire le immagini della macchina virtuale per la creazione rapida e altro.</span><span class="sxs-lookup"><span data-stu-id="1acd2-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="1acd2-117">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-118">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-118">Task</span></span> | <span data-ttu-id="1acd2-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-120">Creare un lab di sviluppo/test di Azure</span><span class="sxs-lookup"><span data-stu-id="1acd2-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="1acd2-121">Informazioni su come creare un lab in Azure DevTest Labs nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acd2-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="1acd2-122">**Creare VM in pochi minuti usando immagini del marketplace predefinite e immagini personalizzate**</span><span class="sxs-lookup"><span data-stu-id="1acd2-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="1acd2-123">È possibile selezionare immagini predefinite tra le moltissime presenti in Azure Marketplace e renderle disponibili nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="1acd2-124">Se le immagini predefinite non soddisfano i requisiti, è possibile creare un'immagine personalizzata creando una VM per il lab da un'immagine predefinita di Azure Marketplace, installando tutto il software necessario e salvando la VM come immagine personalizzata nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="1acd2-125">Se si useranno immagini personalizzate, considerare la possibilità di usare una factory di immagini per creare e distribuire le immagini.</span><span class="sxs-lookup"><span data-stu-id="1acd2-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="1acd2-126">Una factory di immagini è una soluzione di configurazione come codice che compila e distribuisce automaticamente le immagini configurate a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="1acd2-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="1acd2-127">In questo modo si risparmia il tempo necessario per configurare manualmente il sistema dopo la creazione di una VM con il sistema operativo di base.</span><span class="sxs-lookup"><span data-stu-id="1acd2-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="1acd2-128">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-129">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-129">Task</span></span> | <span data-ttu-id="1acd2-130">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-131">Configurare le impostazioni dell'immagine di Azure Marketplace in un lab</span><span class="sxs-lookup"><span data-stu-id="1acd2-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="1acd2-132">Informazioni su come aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace, rendendo disponibili per la selezione solo quelle che si vuole usare per i tester.</span><span class="sxs-lookup"><span data-stu-id="1acd2-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="1acd2-133">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="1acd2-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="1acd2-134">Creare un'immagine personalizzata preinstallando il software necessario in modo che i tester possano creare rapidamente una macchina virtuale usando l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1acd2-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | <span data-ttu-id="1acd2-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) (Informazioni sulla factory di immagini)</span><span class="sxs-lookup"><span data-stu-id="1acd2-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/)</span></span> |<span data-ttu-id="1acd2-136">Guardare un video che descrive come configurare e usare una factory di immagini.</span><span class="sxs-lookup"><span data-stu-id="1acd2-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="1acd2-137">**Creare modelli riutilizzabili per i computer di test**</span><span class="sxs-lookup"><span data-stu-id="1acd2-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="1acd2-138">Una formula in Azure DevTest Labs è un elenco di valori predefiniti di proprietà usati per creare una VM.</span><span class="sxs-lookup"><span data-stu-id="1acd2-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="1acd2-139">È possibile creare una formula nel lab selezionando un'immagine, una dimensione per la VM (una combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1acd2-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="1acd2-140">Ogni tester può visualizzare la formula nel lab e usarla per creare una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1acd2-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="1acd2-141">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-142">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-142">Task</span></span> | <span data-ttu-id="1acd2-143">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-144">Gestire le formule dei lab di sviluppo/test per creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="1acd2-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="1acd2-145">Informazioni su come creare una formula selezionando un'immagine, una dimensione per la VM (combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="1acd2-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="1acd2-146">**Creare ambienti di test per più macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="1acd2-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="1acd2-147">I modelli di Azure Resource Manager consentono di definire l'infrastruttura e la configurazione della soluzione di Azure e di distribuire ripetutamente più macchine virtuali di test in modo coerente.</span><span class="sxs-lookup"><span data-stu-id="1acd2-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="1acd2-148">È possibile eseguire il provisioning delle risorse di Azure PaaS in un ambiente usando un modello di Azure Resource Manager che verrà visualizzato nella verifica dei costi.</span><span class="sxs-lookup"><span data-stu-id="1acd2-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="1acd2-149">Tuttavia, l'arresto automatico della macchina virtuale non si applica alle risorse PaaS.</span><span class="sxs-lookup"><span data-stu-id="1acd2-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="1acd2-150">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-151">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-151">Task</span></span> | <span data-ttu-id="1acd2-152">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-153">Creare ambienti con più macchine virtuali e risorse PaaS con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1acd2-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="1acd2-154">Informazioni su come distribuire più macchine virtuali in modo coerente nell'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="1acd2-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="1acd2-155">**Creare elementi per consentire la personalizzazione delle VM flessibile**</span><span class="sxs-lookup"><span data-stu-id="1acd2-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="1acd2-156">Gli elementi vengono usati per distribuire e configurare l'applicazione dopo il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1acd2-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="1acd2-157">Gli elementi possono essere:</span><span class="sxs-lookup"><span data-stu-id="1acd2-157">Artifacts can be:</span></span>

   - <span data-ttu-id="1acd2-158">Strumenti che si vuole installare nella VM, come agenti, Fiddler, Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1acd2-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="1acd2-159">Azioni che si desidera eseguire sulla macchina virtuale, ad esempio la clonazione di un archivio.</span><span class="sxs-lookup"><span data-stu-id="1acd2-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="1acd2-160">Applicazioni che si vuole testare.</span><span class="sxs-lookup"><span data-stu-id="1acd2-160">Applications that you want to test.</span></span>

   <span data-ttu-id="1acd2-161">Molti elementi sono già immediatamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="1acd2-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="1acd2-162">È possibile creare elementi personalizzati per le proprie esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="1acd2-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="1acd2-163">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-164">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-164">Task</span></span> | <span data-ttu-id="1acd2-165">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-166">Creare elementi personalizzati per le macchine virtuali di DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1acd2-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="1acd2-167">Creare elementi personalizzati per le macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="1acd2-168">Aggiungere un repository Git per archiviare gli elementi personalizzati e i modelli di Azure Resource Manager per l'uso in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1acd2-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="1acd2-169">Informazioni su come archiviare gli elementi personalizzati nel repository Git privato.</span><span class="sxs-lookup"><span data-stu-id="1acd2-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="1acd2-170">**Controllare i costi**</span><span class="sxs-lookup"><span data-stu-id="1acd2-170">**Control costs**</span></span>
   
    <span data-ttu-id="1acd2-171">Azure DevTest Labs consente di impostare un criterio nel lab per specificare il numero massimo di macchine virtuali che possono essere create da un tester nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="1acd2-172">Se il team di test ha definito un piano di lavoro e si vuole arrestare tutte le macchine virtuali a una determinata ora del giorno e quindi riavviarle automaticamente il giorno seguente, è possibile impostare criteri di arresto automatico e di riavvio automatico nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="1acd2-173">Infine, al termine dello sviluppo dell'app, è possibile eliminare tutte le VM in una volta eseguendo un unico script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1acd2-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="1acd2-174">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-175">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-175">Task</span></span> | <span data-ttu-id="1acd2-176">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-177">Definire i criteri del lab</span><span class="sxs-lookup"><span data-stu-id="1acd2-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="1acd2-178">Controllare i costi impostando criteri nel lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="1acd2-179">Eliminare tutte le VM del lab usando uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="1acd2-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="1acd2-180">Eliminare tutti i lab con una sola operazione al termine del test.</span><span class="sxs-lookup"><span data-stu-id="1acd2-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="1acd2-181">**Aggiungere una rete virtuale a un lab**</span><span class="sxs-lookup"><span data-stu-id="1acd2-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="1acd2-182">DevTest Labs crea una nuova rete virtuale quando viene creato un lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="1acd2-183">Se si è configurata la propria rete virtuale, ad esempio usando ExpressRoute o la VPN da sito a sito, è possibile aggiungere questa rete virtuale alle impostazioni della rete virtuale del lab in modo che sia disponibile quando si creano le VM.</span><span class="sxs-lookup"><span data-stu-id="1acd2-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="1acd2-184">È anche disponibile un elemento di aggiunta a un dominio di Azure Active Directory che aggiunge una macchina virtuale a un dominio quando la macchina virtuale viene creata.</span><span class="sxs-lookup"><span data-stu-id="1acd2-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="1acd2-185">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-186">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-186">Task</span></span> | <span data-ttu-id="1acd2-187">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-188">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1acd2-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="1acd2-189">Informazioni su come configurare una rete virtuale in Azure DevTest Labs usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1acd2-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="1acd2-190">**Condividere il lab con ogni tester**</span><span class="sxs-lookup"><span data-stu-id="1acd2-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="1acd2-191">I lab sono direttamente accessibili con un collegamento condiviso con i tester,</span><span class="sxs-lookup"><span data-stu-id="1acd2-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="1acd2-192">che non devono nemmeno avere un account Azure, purché abbiano un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="1acd2-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="1acd2-193">I tester non possono visualizzare le macchine virtuali create da altri tester.</span><span class="sxs-lookup"><span data-stu-id="1acd2-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="1acd2-194">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-195">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-195">Task</span></span> | <span data-ttu-id="1acd2-196">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-197">Aggiungere un tester a un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1acd2-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="1acd2-198">Usare il portale di Azure per aggiungere tester al lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="1acd2-199">Aggiungere tester al lab usando uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="1acd2-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="1acd2-200">Usare PowerShell per automatizzare l'aggiunta di tester al lab.</span><span class="sxs-lookup"><span data-stu-id="1acd2-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="1acd2-201">Ottenere un collegamento al lab</span><span class="sxs-lookup"><span data-stu-id="1acd2-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="1acd2-202">Informazioni su come i tester possono accedere direttamente a un lab tramite un collegamento ipertestuale.</span><span class="sxs-lookup"><span data-stu-id="1acd2-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="1acd2-203">**Automatizzare la creazione del lab per più team**</span><span class="sxs-lookup"><span data-stu-id="1acd2-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="1acd2-204">È possibile automatizzare la creazione del lab, incluse le impostazioni personalizzate, creando un modello di Resource Manager e usandolo per creare altri lab identici.</span><span class="sxs-lookup"><span data-stu-id="1acd2-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="1acd2-205">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1acd2-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="1acd2-206">Attività</span><span class="sxs-lookup"><span data-stu-id="1acd2-206">Task</span></span> | <span data-ttu-id="1acd2-207">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="1acd2-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="1acd2-208">Creare un lab usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1acd2-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="1acd2-209">Creare lab in Azure DevTest Labs usando modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1acd2-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

