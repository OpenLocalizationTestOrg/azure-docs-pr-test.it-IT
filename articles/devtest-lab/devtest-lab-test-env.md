---
title: ambienti di test aaaUse Azure DevTest Labs per macchina virtuale e PaaS | Documenti Microsoft
description: Informazioni su come toouse Azure DevTest Labs per macchina virtuale e PaaS testare gli scenari di ambiente.
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
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="145bf-103">Usare Azure DevTest Labs per macchine virtuali e ambienti di test PaaS</span><span class="sxs-lookup"><span data-stu-id="145bf-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="145bf-104">È possibile utilizzare Azure DevTest Labs tooimplement molti scenari chiavi, ma un scenario principale prevede l'uso di macchine toohost DevTest Labs per tester.</span><span class="sxs-lookup"><span data-stu-id="145bf-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="145bf-105">In questo scenario DevTest Labs offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="145bf-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="145bf-106">I tester possono eseguire test più recente della propria applicazione hello rapidamente il provisioning di ambienti Windows e Linux utilizzando gli elementi e modelli riutilizzabili.</span><span class="sxs-lookup"><span data-stu-id="145bf-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="145bf-107">Possono anche aumentare i test di carico eseguendo il provisioning di più agenti di test.</span><span class="sxs-lookup"><span data-stu-id="145bf-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="145bf-108">Gli amministratori possono controllare i costi assicurandosi che:</span><span class="sxs-lookup"><span data-stu-id="145bf-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="145bf-109">I tester non possano ottenere più macchine virtuali del necessario per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="145bf-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="145bf-110">Le VM vengano arrestate quando non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="145bf-110">VMs are shut down when not in use.</span></span>

![Usare DevTest Labs per il training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="145bf-112">In questo articolo si informazioni sui requisiti dei vari Azure DevTest Labs funzionalità utilizzate toomeet tester e hello tooset toofollow la procedura dettagliata di un lab.</span><span class="sxs-lookup"><span data-stu-id="145bf-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="145bf-113">Implementazione di ambienti di test con Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="145bf-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="145bf-114">**Creare hello lab**</span><span class="sxs-lookup"><span data-stu-id="145bf-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="145bf-115">Esercitazioni sono hello Azure DevTest Labs al punto iniziale.</span><span class="sxs-lookup"><span data-stu-id="145bf-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="145bf-116">Dopo aver creato un ambiente lab, è possibile eseguire attività quali l'aggiunta di lab toohello utenti (tester), l'impostazione criteri toocontrol i costi, la definizione di immagini di macchina virtuale che è possono creare rapidamente e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="145bf-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="145bf-117">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-118">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-118">Task</span></span> | <span data-ttu-id="145bf-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-120">Creare un lab di sviluppo/test di Azure</span><span class="sxs-lookup"><span data-stu-id="145bf-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="145bf-121">Informazioni su come toocreate un laboratorio di Azure DevTest Labs in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="145bf-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="145bf-122">**Creare VM in pochi minuti usando immagini del marketplace predefinite e immagini personalizzate**</span><span class="sxs-lookup"><span data-stu-id="145bf-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="145bf-123">È possibile selezionare le immagini predefinite da una vasta gamma di immagini in Azure Marketplace hello e renderle disponibili nel lab hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="145bf-124">Se le immagini predefinite hello non soddisfano i requisiti, è possibile creare un'immagine personalizzata mediante la creazione di un macchina virtuale usando un'immagine da Azure Marketplace, l'installazione di tutto il software necessario, hello e salvataggio hello VM pronti all'uso come immagine personalizzata in lab hello lab.</span><span class="sxs-lookup"><span data-stu-id="145bf-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="145bf-125">Se si utilizzano immagini personalizzate, è consigliabile usare un toocreate factory immagine e distribuire le immagini.</span><span class="sxs-lookup"><span data-stu-id="145bf-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="145bf-126">Una factory di immagini è una soluzione di configurazione come codice che compila e distribuisce automaticamente le immagini configurate a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="145bf-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="145bf-127">Questo toomanually tempi di hello Salva configurare sistema hello dopo aver creata una macchina virtuale con hello del sistema operativo di base.</span><span class="sxs-lookup"><span data-stu-id="145bf-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="145bf-128">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-129">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-129">Task</span></span> | <span data-ttu-id="145bf-130">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-131">Configurare le impostazioni dell'immagine di Azure Marketplace in un lab</span><span class="sxs-lookup"><span data-stu-id="145bf-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="145bf-132">Informazioni su come le immagini di Azure Marketplace whitelist, rendere disponibile per la selezione solo hello le immagini desiderato per i tester hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="145bf-133">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="145bf-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="145bf-134">Per creare un'immagine personalizzata, pre-installare software hello che è necessario in modo che i tester di creare rapidamente una macchina virtuale utilizzando l'immagine personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | <span data-ttu-id="145bf-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) (Informazioni sulla factory di immagini)</span><span class="sxs-lookup"><span data-stu-id="145bf-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/)</span></span> |<span data-ttu-id="145bf-136">Guardare un video che descrive la modalità tooset configurare e utilizzare una factory dell'immagine.</span><span class="sxs-lookup"><span data-stu-id="145bf-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="145bf-137">**Creare modelli riutilizzabili per i computer di test**</span><span class="sxs-lookup"><span data-stu-id="145bf-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="145bf-138">Una formula in Azure DevTest Labs è che un elenco di valori di proprietà predefiniti utilizzati toocreate una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="145bf-139">È possibile creare una formula nel lab hello selezionando un'immagine, una dimensione di macchina virtuale (una combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="145bf-140">Ogni tester può vedere formula hello in lab hello e usarlo toocreate una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="145bf-141">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-142">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-142">Task</span></span> | <span data-ttu-id="145bf-143">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-144">Gestire le formule di DevTest Labs toocreate macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="145bf-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="145bf-145">Informazioni su come creare una formula selezionando un'immagine, una dimensione per la VM (combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="145bf-146">**Creare ambienti di test per più macchine virtuali**</span><span class="sxs-lookup"><span data-stu-id="145bf-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="145bf-147">È possibile utilizzare l'infrastruttura di Azure Resource Manager modelli toodefine hello e configurazione della soluzione Azure e distribuire ripetutamente test più macchine virtuali in uno stato coerente.</span><span class="sxs-lookup"><span data-stu-id="145bf-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="145bf-148">È possibile eseguire il provisioning delle risorse di Azure PaaS in un ambiente usando un modello di Azure Resource Manager che verrà visualizzato nella verifica dei costi.</span><span class="sxs-lookup"><span data-stu-id="145bf-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="145bf-149">Chiusura automatica di macchina virtuale, tuttavia, non si applica tooPaaS risorse.</span><span class="sxs-lookup"><span data-stu-id="145bf-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="145bf-150">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-151">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-151">Task</span></span> | <span data-ttu-id="145bf-152">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-153">Creare ambienti con più macchine virtuali e risorse PaaS con i modelli di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="145bf-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="145bf-154">Informazioni su come distribuire più macchine virtuali in modo coerente nell'ambiente di test.</span><span class="sxs-lookup"><span data-stu-id="145bf-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="145bf-155">**Creare elementi tooenable flessibile VM personalizzazione**</span><span class="sxs-lookup"><span data-stu-id="145bf-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="145bf-156">Gli elementi vengono utilizzati toodeploy e configurare l'applicazione dopo il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="145bf-157">Gli elementi possono essere:</span><span class="sxs-lookup"><span data-stu-id="145bf-157">Artifacts can be:</span></span>

   - <span data-ttu-id="145bf-158">Strumenti che si desidera tooinstall su hello - VM, ad esempio gli agenti, Fiddler e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="145bf-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="145bf-159">Azioni che si desidera toorun su hello - VM, come la clonazione di un repository.</span><span class="sxs-lookup"><span data-stu-id="145bf-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="145bf-160">Applicazioni che si desidera tootest.</span><span class="sxs-lookup"><span data-stu-id="145bf-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="145bf-161">Molti elementi sono già immediatamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="145bf-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="145bf-162">È possibile creare elementi personalizzati per le proprie esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="145bf-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="145bf-163">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-164">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-164">Task</span></span> | <span data-ttu-id="145bf-165">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-166">Creare elementi personalizzati per le macchine virtuali di DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="145bf-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="145bf-167">Creare i propri elementi personalizzati per le macchine virtuali hello nell'ambiente lab.</span><span class="sxs-lookup"><span data-stu-id="145bf-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="145bf-168">Aggiungere un artefatti della toostore repository Git personalizzati e modelli di gestione risorse di Azure per l'uso in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="145bf-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="145bf-169">Informazioni su come toostore gli elementi personalizzati in proprio repository Git privato.</span><span class="sxs-lookup"><span data-stu-id="145bf-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="145bf-170">**Controllare i costi**</span><span class="sxs-lookup"><span data-stu-id="145bf-170">**Control costs**</span></span>
   
    <span data-ttu-id="145bf-171">Azure DevTest Labs consente tooset un criterio hello lab toospecify hello numero massimo di macchine virtuali che possono essere creati da un tester nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="145bf-172">Se il team di test dispone di un set di lavoro Pianificazione e si desidera toostop hello tutte le macchine virtuali a una determinata ora del giorno hello automaticamente riavviarle hello giorno, è possibile eseguire facilmente che l'impostazione auto-arresto e avvio automatico criteri nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="145bf-173">Infine, una volta completato lo sviluppo di app, è possibile eliminare tutte le macchine virtuali hello in una sola volta tramite l'esecuzione di un singolo script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="145bf-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="145bf-174">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-175">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-175">Task</span></span> | <span data-ttu-id="145bf-176">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-177">Definire i criteri del lab</span><span class="sxs-lookup"><span data-stu-id="145bf-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="145bf-178">Controllare i costi tramite l'impostazione di criteri nell'ambiente lab hello.</span><span class="sxs-lookup"><span data-stu-id="145bf-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="145bf-179">Eliminare lab hello tutte le macchine virtuali tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="145bf-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="145bf-180">Eliminare tutti i laboratori di hello in un'unica operazione quando il test è stato completato.</span><span class="sxs-lookup"><span data-stu-id="145bf-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="145bf-181">**Aggiungere un tooa di rete virtuale Lab**</span><span class="sxs-lookup"><span data-stu-id="145bf-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="145bf-182">DevTest Labs crea una nuova rete virtuale quando viene creato un lab.</span><span class="sxs-lookup"><span data-stu-id="145bf-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="145bf-183">Se è stata configurata la propria rete virtuale: ad esempio, tramite ExpressRoute o VPN site-to-site: è possibile aggiungere le impostazioni di rete virtuale del lab tooyour questa rete virtuale in modo che sia disponibile durante la creazione di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="145bf-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="145bf-184">Inoltre, vi è un Azure Active Directory dominio join elemento disponibile che viene aggiunto a un dominio di tooa VM quando viene creato hello VM.</span><span class="sxs-lookup"><span data-stu-id="145bf-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="145bf-185">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-186">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-186">Task</span></span> | <span data-ttu-id="145bf-187">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-188">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="145bf-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="145bf-189">Informazioni su come una rete virtuale in Azure DevTest Labs utilizzando tooconfigure hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="145bf-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="145bf-190">**Condividere lab hello con ogni tester**</span><span class="sxs-lookup"><span data-stu-id="145bf-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="145bf-191">I lab sono direttamente accessibili con un collegamento condiviso con i tester,</span><span class="sxs-lookup"><span data-stu-id="145bf-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="145bf-192">Non ancora hanno toohave un account Azure, come hanno un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="145bf-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="145bf-193">I tester non possono visualizzare le macchine virtuali create da altri tester.</span><span class="sxs-lookup"><span data-stu-id="145bf-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="145bf-194">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-195">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-195">Task</span></span> | <span data-ttu-id="145bf-196">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-197">Aggiungere un ambiente lab tooa tester in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="145bf-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="145bf-198">Utilizzare hello tooadd portale Azure tester tooyour lab.</span><span class="sxs-lookup"><span data-stu-id="145bf-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="145bf-199">Aggiungere lab toohello tester tramite uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="145bf-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="145bf-200">Utilizzare PowerShell tooautomate aggiunta lab tooyour tester.</span><span class="sxs-lookup"><span data-stu-id="145bf-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="145bf-201">Ottenere un ambiente lab toohello collegamento</span><span class="sxs-lookup"><span data-stu-id="145bf-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="145bf-202">Informazioni su come i tester possono accedere direttamente a un lab tramite un collegamento ipertestuale.</span><span class="sxs-lookup"><span data-stu-id="145bf-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="145bf-203">**Automatizzare la creazione del lab per più team**</span><span class="sxs-lookup"><span data-stu-id="145bf-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="145bf-204">È possibile automatizzare la creazione di lab, incluse le impostazioni personalizzate, creazione di un modello di gestione delle risorse e utilizzandolo labs identici toocreate ripetutamente.</span><span class="sxs-lookup"><span data-stu-id="145bf-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="145bf-205">Per altre informazioni facendo clic sui collegamenti hello in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="145bf-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="145bf-206">Attività</span><span class="sxs-lookup"><span data-stu-id="145bf-206">Task</span></span> | <span data-ttu-id="145bf-207">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="145bf-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="145bf-208">Creare un lab usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="145bf-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="145bf-209">Creare lab in Azure DevTest Labs usando modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="145bf-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

