---
title: Risolvere i problemi di distribuzione della macchina virtuale Windows in Azure | Microsoft Docs
description: Risolvere i problemi di distribuzione della macchina virtuale Windows in Azure con il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: genlin
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4e383427-4aff-4bf3-a0f4-dbff5c6f0c81
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: genli
ms.openlocfilehash: 6800c137097c2803f28dec7365f6d3f2a173b411
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="c6fa2-103">Risolvere i problemi di distribuzione della macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="c6fa2-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="c6fa2-104">Per risolvere i problemi relativi alla distribuzione della macchina virtuale (VM) in Azure, esaminare i [problemi principali](#top-issues) per errori e risoluzioni comuni.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-104">To troubleshoot virtual machine (VM) deployment issues in Azure, review the [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="c6fa2-105">Per ricevere assistenza in qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-105">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="c6fa2-106">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="c6fa2-107">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/support/options/) e selezionare **Ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-107">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="c6fa2-108">Problemi principali</span><span class="sxs-lookup"><span data-stu-id="c6fa2-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="the-cluster-cannot-support-the-requested-vm-size"></a><span data-ttu-id="c6fa2-109">Il cluster non supporta le dimensioni della VM richieste</span><span class="sxs-lookup"><span data-stu-id="c6fa2-109">The cluster cannot support the requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="c6fa2-110">Ripetere la richiesta usando una VM di dimensioni inferiori.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-110">Retry the request using a smaller VM size.</span></span>
- <span data-ttu-id="c6fa2-111">Se le dimensioni della VM richieste non possono essere modificate:</span><span class="sxs-lookup"><span data-stu-id="c6fa2-111">If the size of the requested VM cannot be changed:</span></span>
    - <span data-ttu-id="c6fa2-112">Arrestare tutte le VM nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-112">Stop all the VMs in the availability set.</span></span> <span data-ttu-id="c6fa2-113">Fare clic su **Gruppi di risorse** > il proprio gruppo di risorse > **Risorse** > il proprio set di disponibilità > **Macchine virtuali** > la propria macchina virtuale > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="c6fa2-114">Dopo l'arresto di tutte le VM creare la VM con le dimensioni desiderate.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-114">After all the VMs stop, create the VM in the desired size.</span></span>
    - <span data-ttu-id="c6fa2-115">Avviare prima la nuova VM, quindi selezionare ogni VM arrestata e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-115">Start the new VM first, and then select each of the stopped VMs and click Start.</span></span>


## <a name="the-cluster-does-not-have-free-resources"></a><span data-ttu-id="c6fa2-116">Il cluster non ha risorse disponibili</span><span class="sxs-lookup"><span data-stu-id="c6fa2-116">The cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="c6fa2-117">Ripetere la richiesta più tardi.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-117">Retry the request later.</span></span>
- <span data-ttu-id="c6fa2-118">Se la nuova VM può far parte di un set di disponibilità diverso</span><span class="sxs-lookup"><span data-stu-id="c6fa2-118">If the new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="c6fa2-119">Creare una VM in un altro set di disponibilità nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-119">Create a VM in a different availability set (in the same region).</span></span>
    - <span data-ttu-id="c6fa2-120">Aggiungere la nuova VM alla stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-120">Add the new VM to the same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="c6fa2-121">Come si usa e si distribuisce un'immagine client Windows in Azure?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="c6fa2-122">Se si ha di una sottoscrizione appropriata di Visual Studio (in precedenza MSDN) è possibile usare Windows 7, Windows 8 o Windows 10 in Azure per scenari di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="c6fa2-123">In questo [articolo](client-images.md) sono descritti i requisiti di idoneità per l'esecuzione di client Windows in Azure e l'uso delle immagini della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-123">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and uses of the Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-the-hybrid-use-benefit-hub"></a><span data-ttu-id="c6fa2-124">Come distribuire una macchina virtuale usando il vantaggio Hybrid Use (HUB, Hybrid Use Benefit)?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-124">How can I deploy a virtual machine using the Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="c6fa2-125">Esistono due modi per distribuire le macchine virtuali di Windows con il vantaggio Azure Hybrid Use.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-125">There are a couple of different ways to deploy Windows virtual machines with the Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="c6fa2-126">Per una sottoscrizione con un contratto Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="c6fa2-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="c6fa2-127">•   Distribuire le VM da immagini specifiche di Marketplace preconfigurate con il vantaggio Azure Hybrid Use.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="c6fa2-128">Per il contratto Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="c6fa2-128">For Enterprise agreement:</span></span>

<span data-ttu-id="c6fa2-129">•   Caricare una VM personalizzata e distribuirla usando un modello di Resource Manager o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="c6fa2-130">Per altre informazioni, vedere le seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="c6fa2-130">For more information, see the following resources:</span></span>

 - [<span data-ttu-id="c6fa2-131">Panoramica del vantaggio Azure Hybrid Use </span><span class="sxs-lookup"><span data-stu-id="c6fa2-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="c6fa2-132">Domande frequenti scaricabili</span><span class="sxs-lookup"><span data-stu-id="c6fa2-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="c6fa2-133">[Vantaggio Azure Hybrid Use per Windows Server e Windows Client](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="c6fa2-134">Come usare il vantaggio Hybrid Use in Azure</span><span class="sxs-lookup"><span data-stu-id="c6fa2-134">How can I use the Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="c6fa2-135">Come attivare il credito mensile per Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="c6fa2-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="c6fa2-136">Per attivare il credito mensile, vedere questo [articolo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-136">To activate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-to-add-enterprise-devtest-to-my-enterprise-agreement-ea-to-get-access-to-window-client-images"></a><span data-ttu-id="c6fa2-137">Come aggiungere Sviluppo/test Enterprise al contratto Enterprise Agreement (EA) per ottenere l'accesso a immagini client Windows?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-137">How to add Enterprise Dev/Test to my Enterprise Agreement (EA) to get access to Window client images?</span></span>

<span data-ttu-id="c6fa2-138">La possibilità di creare sottoscrizioni basate sull'offerta Sviluppo/test Enterprise è riservata ai proprietari di account che hanno ricevuto l'autorizzazione corrispondente da un amministratore dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-138">The ability to create subscriptions based on the Enterprise Dev/Test offer is restricted to Account Owners who have been given permission to do so by an Enterprise Administrator.</span></span> <span data-ttu-id="c6fa2-139">Il proprietario dell'account crea sottoscrizioni tramite il portale degli account di Azure e quindi deve aggiungere i sottoscrittori di Visual Studio attivi come coamministratori.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-139">The Account Owner creates subscriptions via the Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="c6fa2-140">In tal modo il proprietario dell'account può gestire e usare le risorse necessarie per sviluppo e test.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-140">So that they can manage and use the resources needed for development and testing.</span></span> <span data-ttu-id="c6fa2-141">Per altre informazioni, vedere [Sviluppo/test Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="c6fa2-142">I driver della VM Windows Serie N non sono disponibili</span><span class="sxs-lookup"><span data-stu-id="c6fa2-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="c6fa2-143">I driver per le macchine virtuali basate su Windows si trovano [qui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="c6fa2-144">Nella VM Serie N non è disponibile un'istanza GPU</span><span class="sxs-lookup"><span data-stu-id="c6fa2-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="c6fa2-145">Per usufruire delle funzionalità GPU delle VM serie N di Azure che eseguono Windows Server 2016 o Windows Server 2012 R2, è necessario installare i driver della scheda grafica NVIDIA in ciascuna VM dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-145">To take advantage of the GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="c6fa2-146">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](n-series-driver-setup.md) e le [VM Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="c6fa2-147">Le immagini client sono supportate per la Serie N?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="c6fa2-148">Attualmente Azure supporta la Serie N solo sulle VM che eseguono i sistemi operativi Windows Server e Linux.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="c6fa2-149">Le VM Serie N sono disponibili nella mia area?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="c6fa2-150">È possibile controllare la disponibilità nella tabella [Prodotti disponibili in base all'area](https://azure.microsoft.com/regions/services) e verificare i prezzi [qui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-150">You can check the availability from the [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-to-i-get-them"></a><span data-ttu-id="c6fa2-151">Quali immagini client è possibile usare e distribuire in Azure e come ottenerle?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-151">What client images can I use and deploy in Azure, and how to I get them?</span></span>

<span data-ttu-id="c6fa2-152">A condizione di disporre di una sottoscrizione appropriata di Visual Studio (in precedenza MSDN), è possibile usare Windows 7, Windows 8 o Windows 10 in Azure per scenari di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="c6fa2-153">Le immagini di Windows 10 sono disponibili nella raccolta di Azure in [Offerte idonee](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-153">Windows 10 images are available from the Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="c6fa2-154">I sottoscrittori di Visual Studio per qualsiasi tipo di offerta possono anche [preparare e creare](prepare-for-upload-vhd-image.md) un'immagine a 64 bit di Windows 7, Windows 8 o Windows 10 e quindi [caricarla in Azure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-generalized-managed.md).</span></span> <span data-ttu-id="c6fa2-155">L'utilizzo rimane limitato alle attività di sviluppo e test da parte dei sottoscrittori di Visual Studio attivi.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-155">The use remains limited to dev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="c6fa2-156">In questo [articolo](client-images.md) sono descritti i requisiti di idoneità per l'esecuzione di client Windows in Azure e l'uso delle immagini della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-156">This [article](client-images.md) outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.</span></span>

## <a name="i-am-not-able-to-see-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="c6fa2-157">Durante il ridimensionamento della VM non è possibile visualizzare la famiglia Dimensioni macchina virtuale desiderata.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-157">I am not able to see VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="c6fa2-158">Quando una VM è in esecuzione, viene distribuita su un server fisico.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-158">When a VM is running, it is deployed to a physical server.</span></span> <span data-ttu-id="c6fa2-159">I server fisici nelle aree di Azure sono raggruppati in cluster di hardware fisico comune.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-159">The physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="c6fa2-160">Il ridimensionamento di una VM che ne richiede lo spostamento in un cluster hardware diverso varia a seconda del modello usato per la distribuzione della VM.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-160">Resizing a VM that requires the VM to be moved to different hardware clusters is different depending on which deployment model was used to deploy the VM.</span></span>

- <span data-ttu-id="c6fa2-161">Nel caso delle VM distribuite con il modello di distribuzione classica è necessario rimuovere e ripetere la distribuzione del servizio cloud per impostare le VM su dimensioni appartenenti a un'altra famiglia di dimensioni.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-161">VMs deployed in Classic deployment model, the cloud service deployment must be removed and redeployed to change the VMs to a size in another size family.</span></span>

- <span data-ttu-id="c6fa2-162">Nel caso delle VM distribuite con il modello di distribuzione di Gestione risorse, prima di modificare le dimensioni di una VM è necessario arrestare tutte le VM del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in the availability set before changing the size of any VM in the availability set.</span></span>

## <a name="the-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="c6fa2-163">Le dimensioni della VM elencate non sono supportate durante la distribuzione nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-163">The listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="c6fa2-164">Scegliere dimensioni supportate nel cluster del set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-164">Choose a size that is supported on the availability set's cluster.</span></span> <span data-ttu-id="c6fa2-165">Quando si crea un set di disponibilità è consigliabile scegliere per la VM le dimensioni massime che si prevede di usare e impostare la VM risultante come prima distribuzione nel set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-165">It is recommended when creating an availability set to choose the largest VM size you think you need, and have that be your first deployment to the Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-to-an-availability-set"></a><span data-ttu-id="c6fa2-166">È possibile aggiungere una VM classica esistente a un set di disponibilità?</span><span class="sxs-lookup"><span data-stu-id="c6fa2-166">Can I add an existing Classic VM to an availability set?</span></span>

<span data-ttu-id="c6fa2-167">Sì.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-167">Yes.</span></span> <span data-ttu-id="c6fa2-168">È possibile aggiungere una VM classica esistente a un set di disponibilità nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-168">You can add an existing classic VM to a new or existing Availability Set.</span></span> <span data-ttu-id="c6fa2-169">Per altre informazioni, vedere [Aggiungere una macchina virtuale esistente a un set di disponibilità](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-169">For more information see [Add an existing virtual machine to an availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c6fa2-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6fa2-170">Next steps</span></span>
<span data-ttu-id="c6fa2-171">Per ricevere assistenza in qualsiasi punto di questo articolo, contattare gli esperti di Azure nei [forum MSDN e Stack Overflow relativi ad Azure](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="c6fa2-171">If you need more help at any point in this article, you can contact the Azure experts on [the MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="c6fa2-172">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="c6fa2-173">Accedere al [sito del supporto di Azure](https://azure.microsoft.com/support/options/) e selezionare **Ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="c6fa2-173">Go to the [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
