---
title: Usare Azure DevTest Labs per sviluppatori | Microsoft Docs
description: Informazioni su come usare Azure DevTest Labs per gli scenari relativi allo sviluppo.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="0e10e-103">Usare Azure DevTest Labs per sviluppatori</span><span class="sxs-lookup"><span data-stu-id="0e10e-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="0e10e-104">Azure DevTest Labs può essere usato per implementare molti scenari chiave. Uno dei più importanti prevede l'uso di DevTest Labs per ospitare computer di sviluppo per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0e10e-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="0e10e-105">In questo scenario DevTest Labs offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e10e-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="0e10e-106">Gli sviluppatori possono effettuare rapidamente il provisioning dei computer di sviluppo su richiesta.</span><span class="sxs-lookup"><span data-stu-id="0e10e-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="0e10e-107">Gli sviluppatori possono personalizzare facilmente i computer di sviluppo quando è necessario.</span><span class="sxs-lookup"><span data-stu-id="0e10e-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="0e10e-108">Gli amministratori possono controllare i costi assicurandosi che:</span><span class="sxs-lookup"><span data-stu-id="0e10e-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="0e10e-109">Gli sviluppatori non possano ottenere più VM del necessario per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0e10e-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="0e10e-110">Le VM vengano arrestate quando non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="0e10e-110">VMs are shut down when not in use.</span></span> 

![Usare DevTest Labs per il training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="0e10e-112">Questo articolo illustra le diverse funzionalità di Azure DevTest Labs che possono essere usate per soddisfare i requisiti degli sviluppatori e i passaggi dettagliati che è possibile seguire per configurare un lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="0e10e-113">Implementazione di ambienti di sviluppo con Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0e10e-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="0e10e-114">**Creare il lab**</span><span class="sxs-lookup"><span data-stu-id="0e10e-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="0e10e-115">I lab sono il punto di partenza in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="0e10e-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="0e10e-116">Dopo avere creato un lab, è possibile eseguire attività come aggiungere utenti (sviluppatori) al lab, impostare criteri per controllare i costi, definire immagini di VM per la creazione rapida e altro.</span><span class="sxs-lookup"><span data-stu-id="0e10e-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="0e10e-117">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-118">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-118">Task</span></span> | <span data-ttu-id="0e10e-119">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-120">Creare un lab di sviluppo/test di Azure</span><span class="sxs-lookup"><span data-stu-id="0e10e-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="0e10e-121">Informazioni su come creare un lab in Azure DevTest Labs nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e10e-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="0e10e-122">**Creare VM in pochi minuti usando immagini del marketplace predefinite e immagini personalizzate**</span><span class="sxs-lookup"><span data-stu-id="0e10e-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="0e10e-123">È possibile selezionare immagini predefinite tra le moltissime presenti in Azure Marketplace e renderle disponibili nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="0e10e-124">Se le immagini predefinite non soddisfano i requisiti, è possibile creare un'immagine personalizzata creando una VM per il lab da un'immagine predefinita di Azure Marketplace, installando tutto il software necessario e salvando la VM come immagine personalizzata nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="0e10e-125">Se si useranno immagini personalizzate, considerare la possibilità di usare una factory di immagini per creare e distribuire le immagini.</span><span class="sxs-lookup"><span data-stu-id="0e10e-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="0e10e-126">Una factory di immagini è una soluzione di configurazione come codice che compila e distribuisce automaticamente le immagini configurate a intervalli regolari.</span><span class="sxs-lookup"><span data-stu-id="0e10e-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="0e10e-127">In questo modo si risparmia il tempo necessario per configurare manualmente il sistema dopo la creazione di una VM con il sistema operativo di base.</span><span class="sxs-lookup"><span data-stu-id="0e10e-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="0e10e-128">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-129">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-129">Task</span></span> | <span data-ttu-id="0e10e-130">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-131">Configurare le impostazioni dell'immagine di Azure Marketplace in un lab</span><span class="sxs-lookup"><span data-stu-id="0e10e-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="0e10e-132">Informazioni su come aggiungere all'elenco elementi consentiti le immagini di Azure Marketplace, rendendo disponibili per la selezione solo quelle che si vuole usare per gli sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0e10e-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="0e10e-133">Creare un'immagine personalizzata</span><span class="sxs-lookup"><span data-stu-id="0e10e-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="0e10e-134">Creare un'immagine personalizzata preinstallando il software necessario in modo che gli sviluppatori possano creare rapidamente una VM usando l'immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="0e10e-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | <span data-ttu-id="0e10e-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) (Informazioni sulla factory di immagini)</span><span class="sxs-lookup"><span data-stu-id="0e10e-135">[Learn about image factory](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/)</span></span> |<span data-ttu-id="0e10e-136">Guardare un video che descrive come configurare e usare una factory di immagini.</span><span class="sxs-lookup"><span data-stu-id="0e10e-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="0e10e-137">**Creare modelli riutilizzabili per i computer di sviluppo**</span><span class="sxs-lookup"><span data-stu-id="0e10e-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="0e10e-138">Una formula in Azure DevTest Labs è un elenco di valori predefiniti di proprietà usati per creare una VM.</span><span class="sxs-lookup"><span data-stu-id="0e10e-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="0e10e-139">È possibile creare una formula nel lab selezionando un'immagine, una dimensione per la VM (una combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0e10e-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="0e10e-140">Ogni sviluppatore può visualizzare la formula nel lab e usarla per creare una VM.</span><span class="sxs-lookup"><span data-stu-id="0e10e-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="0e10e-141">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-142">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-142">Task</span></span> | <span data-ttu-id="0e10e-143">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-144">Gestire le formule dei lab di sviluppo/test per creare macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="0e10e-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="0e10e-145">Informazioni su come creare una formula selezionando un'immagine, una dimensione per la VM (combinazione di CPU e RAM) e una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0e10e-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="0e10e-146">**Creare elementi per consentire la personalizzazione delle VM flessibile**</span><span class="sxs-lookup"><span data-stu-id="0e10e-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="0e10e-147">Gli elementi vengono usati per distribuire e configurare l'applicazione dopo il provisioning di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="0e10e-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="0e10e-148">Gli elementi possono essere:</span><span class="sxs-lookup"><span data-stu-id="0e10e-148">Artifacts can be:</span></span>

   - <span data-ttu-id="0e10e-149">Strumenti che si vuole installare nella VM, come agenti, Fiddler, Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0e10e-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="0e10e-150">Azioni che si desidera eseguire sulla macchina virtuale, ad esempio la clonazione di un archivio.</span><span class="sxs-lookup"><span data-stu-id="0e10e-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="0e10e-151">Applicazioni che si vuole testare.</span><span class="sxs-lookup"><span data-stu-id="0e10e-151">Applications that you want to test.</span></span>

   <span data-ttu-id="0e10e-152">Molti elementi sono già immediatamente disponibili.</span><span class="sxs-lookup"><span data-stu-id="0e10e-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="0e10e-153">È possibile creare elementi personalizzati per le proprie esigenze specifiche.</span><span class="sxs-lookup"><span data-stu-id="0e10e-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="0e10e-154">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-155">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-155">Task</span></span> | <span data-ttu-id="0e10e-156">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-157">Creare elementi personalizzati per le macchine virtuali di DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0e10e-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="0e10e-158">Creare elementi personalizzati per le macchine virtuali nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="0e10e-159">Aggiungere un repository Git per archiviare gli elementi personalizzati e i modelli di Azure Resource Manager per l'uso in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0e10e-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="0e10e-160">Informazioni su come archiviare gli elementi personalizzati nel repository Git privato.</span><span class="sxs-lookup"><span data-stu-id="0e10e-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="0e10e-161">**Controllare i costi**</span><span class="sxs-lookup"><span data-stu-id="0e10e-161">**Control costs**</span></span>
   
    <span data-ttu-id="0e10e-162">Azure DevTest Labs consente di impostare un criterio nel lab per specificare il numero massimo di VM che possono essere create da uno sviluppatore nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="0e10e-163">Se il team degli sviluppatori ha un piano di lavoro impostato e si vuole arrestare tutte le VM a una determinata ora del giorno e quindi riavviarle automaticamente il giorno seguente, è possibile impostare criteri di arresto automatico e di riavvio automatico nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="0e10e-164">Infine, al termine dello sviluppo dell'app, è possibile eliminare tutte le VM in una volta eseguendo un unico script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0e10e-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="0e10e-165">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-166">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-166">Task</span></span> | <span data-ttu-id="0e10e-167">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-168">Definire i criteri del lab</span><span class="sxs-lookup"><span data-stu-id="0e10e-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="0e10e-169">Controllare i costi impostando criteri nel lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="0e10e-170">Eliminare tutte le VM del lab usando uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e10e-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="0e10e-171">Eliminare tutti i lab con una sola operazione al termine dello sviluppo.</span><span class="sxs-lookup"><span data-stu-id="0e10e-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="0e10e-172">**Aggiungere una rete virtuale a una VM**</span><span class="sxs-lookup"><span data-stu-id="0e10e-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="0e10e-173">DevTest Labs crea una nuova rete virtuale quando viene creato un lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="0e10e-174">Se si è configurata la propria rete virtuale, ad esempio usando ExpressRoute o la VPN da sito a sito, è possibile aggiungere questa rete virtuale alle impostazioni della rete virtuale del lab in modo che sia disponibile quando si creano le VM.</span><span class="sxs-lookup"><span data-stu-id="0e10e-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="0e10e-175">È anche disponibile un elemento di aggiunta a un dominio di Azure Active Directory che aggiungerà una VM a un dominio quando la VM verrà creata.</span><span class="sxs-lookup"><span data-stu-id="0e10e-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="0e10e-176">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-177">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-177">Task</span></span> | <span data-ttu-id="0e10e-178">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-179">Configurare una rete virtuale per Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0e10e-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="0e10e-180">Informazioni su come configurare una rete virtuale in Azure DevTest Labs usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e10e-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="0e10e-181">**Condividere il lab con ogni sviluppatore**</span><span class="sxs-lookup"><span data-stu-id="0e10e-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="0e10e-182">I lab sono direttamente accessibili con un collegamento condiviso con gli sviluppatori,</span><span class="sxs-lookup"><span data-stu-id="0e10e-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="0e10e-183">che non devono nemmeno avere un account Azure, purché abbiano un [account Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="0e10e-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="0e10e-184">Gli sviluppatori non possono visualizzare le VM create da altri sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="0e10e-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="0e10e-185">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-186">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-186">Task</span></span> | <span data-ttu-id="0e10e-187">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-188">Aggiungere uno sviluppatore a un lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0e10e-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="0e10e-189">Usare il portale di Azure per aggiungere sviluppatori al lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="0e10e-190">Aggiungere sviluppatori al lab usando uno script di PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e10e-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="0e10e-191">Usare PowerShell per automatizzare l'aggiunta di sviluppatori al lab.</span><span class="sxs-lookup"><span data-stu-id="0e10e-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="0e10e-192">Ottenere un collegamento al lab</span><span class="sxs-lookup"><span data-stu-id="0e10e-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="0e10e-193">Informazioni su come gli sviluppatori possono accedere direttamente a un lab tramite un collegamento ipertestuale.</span><span class="sxs-lookup"><span data-stu-id="0e10e-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="0e10e-194">**Automatizzare la creazione del lab per più team**</span><span class="sxs-lookup"><span data-stu-id="0e10e-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="0e10e-195">È possibile automatizzare la creazione del lab, incluse le impostazioni personalizzate, creando un modello di Resource Manager e usandolo per creare altri lab identici.</span><span class="sxs-lookup"><span data-stu-id="0e10e-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="0e10e-196">Per altre informazioni, fare clic sui collegamenti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="0e10e-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="0e10e-197">Attività</span><span class="sxs-lookup"><span data-stu-id="0e10e-197">Task</span></span> | <span data-ttu-id="0e10e-198">Contenuto dell'esercitazione</span><span class="sxs-lookup"><span data-stu-id="0e10e-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="0e10e-199">Creare un lab usando un modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0e10e-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="0e10e-200">Creare lab in Azure DevTest Labs usando modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0e10e-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

