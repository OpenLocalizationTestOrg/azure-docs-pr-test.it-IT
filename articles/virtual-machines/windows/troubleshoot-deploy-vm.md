---
title: distribuzione dei problemi di macchine virtuali in Azure aaaTroubleshoot | Documenti Microsoft
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
ms.openlocfilehash: 30de25827c050cc266761cfc14548bcc64237dac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-windows-virtual-machine-issues-in-azure"></a><span data-ttu-id="16928-103">Risolvere i problemi di distribuzione della macchina virtuale Windows in Azure</span><span class="sxs-lookup"><span data-stu-id="16928-103">Troubleshoot deploying Windows virtual machine issues in Azure</span></span>

<span data-ttu-id="16928-104">problemi relativi alla distribuzione di macchina virtuale (VM) tootroubleshoot in Azure, esaminare hello [problemi principali](#top-issues) per errori e le risoluzioni comuni.</span><span class="sxs-lookup"><span data-stu-id="16928-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="16928-105">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="16928-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="16928-106">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="16928-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="16928-107">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="16928-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="16928-108">Problemi principali</span><span class="sxs-lookup"><span data-stu-id="16928-108">Top issues</span></span>
[!INCLUDE [virtual-machines-windows-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-windows-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="16928-109">non supporta cluster Hello hello richiesto dimensioni delle macchine Virtuali</span><span class="sxs-lookup"><span data-stu-id="16928-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="16928-110">Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16928-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="16928-111">Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="16928-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="16928-112">Arrestare tutte le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="16928-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="16928-113">Fare clic su **Gruppi di risorse** > il proprio gruppo di risorse > **Risorse** > il proprio set di disponibilità > **Macchine virtuali** > la propria macchina virtuale > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="16928-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="16928-114">Dopo che tutti hello arrestare le macchine virtuali, creare hello VM dimensioni hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="16928-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="16928-115">Avviare hello prima nuova macchina virtuale e quindi selezionare hello arrestare le macchine virtuali e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="16928-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="16928-116">cluster Hello privo di liberare le risorse</span><span class="sxs-lookup"><span data-stu-id="16928-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="16928-117">Riprovare più tardi richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="16928-117">Retry hello request later.</span></span>
- <span data-ttu-id="16928-118">Se hello nuova macchina virtuale è possibile essere incluso un diverso set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="16928-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="16928-119">Creare una macchina virtuale in un set di disponibilità diverso (in hello stessa regione).</span><span class="sxs-lookup"><span data-stu-id="16928-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="16928-120">Aggiungere hello nuova VM toohello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="16928-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-can-i-use-and-deploy-a-windows-client-image-into-azure"></a><span data-ttu-id="16928-121">Come si usa e si distribuisce un'immagine client Windows in Azure?</span><span class="sxs-lookup"><span data-stu-id="16928-121">How can I use and deploy a windows client image into Azure?</span></span>

<span data-ttu-id="16928-122">Se si ha di una sottoscrizione appropriata di Visual Studio (in precedenza MSDN) è possibile usare Windows 7, Windows 8 o Windows 10 in Azure per scenari di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="16928-122">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios if you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> <span data-ttu-id="16928-123">Questo [articolo](client-images.md) contorni hello requisiti per l'esecuzione di client Windows in Azure e utilizzi di hello immagini della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="16928-123">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and uses of hello Azure Gallery images.</span></span>

## <a name="how-can-i-deploy-a-virtual-machine-using-hello-hybrid-use-benefit-hub"></a><span data-ttu-id="16928-124">Come distribuire una macchina virtuale utilizzando hello ibrida utilizzare vantaggio (HUB)?</span><span class="sxs-lookup"><span data-stu-id="16928-124">How can I deploy a virtual machine using hello Hybrid Use Benefit (HUB)?</span></span>

<span data-ttu-id="16928-125">Esistono un paio di modi toodeploy le macchine virtuali Windows con hello vantaggio di utilizzare ibrida di Azure.</span><span class="sxs-lookup"><span data-stu-id="16928-125">There are a couple of different ways toodeploy Windows virtual machines with hello Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="16928-126">Per una sottoscrizione con un contratto Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="16928-126">For an Enterprise Agreement subscription:</span></span>

<span data-ttu-id="16928-127">•   Distribuire le VM da immagini specifiche di Marketplace preconfigurate con il vantaggio Azure Hybrid Use.</span><span class="sxs-lookup"><span data-stu-id="16928-127">•   Deploy VMs from specific Marketplace images that are pre-configured with Azure Hybrid Use Benefit.</span></span>

<span data-ttu-id="16928-128">Per il contratto Enterprise Agreement:</span><span class="sxs-lookup"><span data-stu-id="16928-128">For Enterprise agreement:</span></span>

<span data-ttu-id="16928-129">•   Caricare una VM personalizzata e distribuirla usando un modello di Resource Manager o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="16928-129">•   Upload a custom VM and deploy using a Resource Manager template or Azure PowerShell.</span></span>

<span data-ttu-id="16928-130">Per ulteriori informazioni, vedere hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="16928-130">For more information, see hello following resources:</span></span>

 - [<span data-ttu-id="16928-131">Panoramica del vantaggio Azure Hybrid Use </span><span class="sxs-lookup"><span data-stu-id="16928-131">Azure Hybrid Use Benefit overview </span></span>](https://azure.microsoft.com/pricing/hybrid-use-benefit/)

 - [<span data-ttu-id="16928-132">Domande frequenti scaricabili</span><span class="sxs-lookup"><span data-stu-id="16928-132">Downloadable FAQ</span></span>](http://download.microsoft.com/download/4/2/1/4211AC94-D607-4A45-B472-4B30EDF437DE/Windows_Server_Azure_Hybrid_Use_FAQ_EN_US.pdf)

 - <span data-ttu-id="16928-133">[Vantaggio Azure Hybrid Use per Windows Server e Windows Client](hybrid-use-benefit-licensing.md).</span><span class="sxs-lookup"><span data-stu-id="16928-133">[Azure Hybrid Use Benefit for Windows Server and Windows Client](hybrid-use-benefit-licensing.md).</span></span>

 - [<span data-ttu-id="16928-134">Come è possibile utilizzare hello vantaggio di utilizzare ibridi in Azure</span><span class="sxs-lookup"><span data-stu-id="16928-134">How can I use hello Hybrid Use Benefit in Azure</span></span>](https://blogs.msdn.microsoft.com/azureedu/2016/04/13/how-can-i-use-the-hybrid-use-benefit-in-azure)

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="16928-135">Come attivare il credito mensile per Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="16928-135">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="16928-136">tooactivate la frequenza mensile del credito, vedere questo [articolo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="16928-136">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="how-tooadd-enterprise-devtest-toomy-enterprise-agreement-ea-tooget-access-toowindow-client-images"></a><span data-ttu-id="16928-137">Modalità di accesso di immagini client tooWindow tooadd sviluppo/Test Enterprise toomy Enterprise Agreement (EA) tooget.</span><span class="sxs-lookup"><span data-stu-id="16928-137">How tooadd Enterprise Dev/Test toomy Enterprise Agreement (EA) tooget access tooWindow client images?</span></span>

<span data-ttu-id="16928-138">sottoscrizioni di toocreate possibilità Hello basate su hello sviluppo/Test Enterprise offrono i proprietari di tooAccount con restrizioni che sono stati assegnati l'autorizzazione toodo così da un amministratore dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="16928-138">hello ability toocreate subscriptions based on hello Enterprise Dev/Test offer is restricted tooAccount Owners who have been given permission toodo so by an Enterprise Administrator.</span></span> <span data-ttu-id="16928-139">Ciao proprietario dell'Account vengono create sottoscrizioni tramite hello portale per gli Account Azure e deve quindi aggiungere i sottoscrittori di Visual Studio attivi come coamministratori.</span><span class="sxs-lookup"><span data-stu-id="16928-139">hello Account Owner creates subscriptions via hello Azure Account Portal, and then should add active Visual Studio subscribers as co-administrators.</span></span> <span data-ttu-id="16928-140">In modo da poter gestire e utilizzare le risorse di hello necessarie per lo sviluppo e test.</span><span class="sxs-lookup"><span data-stu-id="16928-140">So that they can manage and use hello resources needed for development and testing.</span></span> <span data-ttu-id="16928-141">Per altre informazioni, vedere [Sviluppo/test Enterprise](https://azure.microsoft.com/offers/ms-azr-0148p/).</span><span class="sxs-lookup"><span data-stu-id="16928-141">For more information, see [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/).</span></span>

## <a name="my-drivers-are-missing-for-my-windows-n-series-vm"></a><span data-ttu-id="16928-142">I driver della VM Windows Serie N non sono disponibili</span><span class="sxs-lookup"><span data-stu-id="16928-142">My drivers are missing for my Windows N-Series VM</span></span>

<span data-ttu-id="16928-143">I driver per le macchine virtuali basate su Windows si trovano [qui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="16928-143">Drivers for Windows-based VMs are located [here](n-series-driver-setup.md).</span></span>

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="16928-144">Nella VM Serie N non è disponibile un'istanza GPU</span><span class="sxs-lookup"><span data-stu-id="16928-144">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="16928-145">tootake le funzionalità GPU hello di macchine virtuali di Azure serie N che esegue Windows Server 2016 o Windows Server 2012 R2, è necessario installare i driver grafici NVIDIA in ogni macchina virtuale dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="16928-145">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="16928-146">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](n-series-driver-setup.md) e le [VM Linux](../linux/n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="16928-146">Driver setup information is available for [Windows VMs](n-series-driver-setup.md) and [Linux VMs](../linux/n-series-driver-setup.md).</span></span>

## <a name="are-client-images-supported-for-n-series"></a><span data-ttu-id="16928-147">Le immagini client sono supportate per la Serie N?</span><span class="sxs-lookup"><span data-stu-id="16928-147">Are client images supported for N-Series?</span></span>

<span data-ttu-id="16928-148">Attualmente Azure supporta la Serie N solo sulle VM che eseguono i sistemi operativi Windows Server e Linux.</span><span class="sxs-lookup"><span data-stu-id="16928-148">Currently, Azure only supports N-Series on VMs running Windows Server and Linux operating systems.</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="16928-149">Le VM Serie N sono disponibili nella mia area?</span><span class="sxs-lookup"><span data-stu-id="16928-149">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="16928-150">È possibile controllare la disponibilità di hello da hello [i prodotti disponibili dalla tabella region](https://azure.microsoft.com/regions/services), nonché i prezzi [qui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="16928-150">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="what-client-images-can-i-use-and-deploy-in-azure-and-how-tooi-get-them"></a><span data-ttu-id="16928-151">Le immagini client è possibile utilizzare e distribuire in Azure e come tooI ottenerle?</span><span class="sxs-lookup"><span data-stu-id="16928-151">What client images can I use and deploy in Azure, and how tooI get them?</span></span>

<span data-ttu-id="16928-152">A condizione di disporre di una sottoscrizione appropriata di Visual Studio (in precedenza MSDN), è possibile usare Windows 7, Windows 8 o Windows 10 in Azure per scenari di sviluppo/test.</span><span class="sxs-lookup"><span data-stu-id="16928-152">You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription.</span></span> 

- <span data-ttu-id="16928-153">Sono disponibili immagini di Windows 10 dalla raccolta di Azure hello all'interno di [idonei sviluppo/test offre](client-images.md#eligible-offers).</span><span class="sxs-lookup"><span data-stu-id="16928-153">Windows 10 images are available from hello Azure Gallery within [eligible dev/test offers](client-images.md#eligible-offers).</span></span> 
- <span data-ttu-id="16928-154">Visual Studio i server di sottoscrizione all'interno di qualsiasi tipo di offerta è anche possibile [adeguatamente preparare e creare](prepare-for-upload-vhd-image.md) un'immagine a 64 bit di Windows 7, Windows 8 o Windows 10 e quindi [caricare tooAzure](upload-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="16928-154">Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload tooAzure](upload-generalized-managed.md).</span></span> <span data-ttu-id="16928-155">utilizzo di Hello rimane limitato toodev dei test da Visual Studio attivi.</span><span class="sxs-lookup"><span data-stu-id="16928-155">hello use remains limited toodev/test by active Visual Studio subscribers.</span></span>

<span data-ttu-id="16928-156">Questo [articolo](client-images.md) contorni hello requisiti per l'esecuzione di client Windows in Azure e l'utilizzo di hello immagini della raccolta di Azure.</span><span class="sxs-lookup"><span data-stu-id="16928-156">This [article](client-images.md) outlines hello eligibility requirements for running Windows client in Azure and use of hello Azure Gallery images.</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="16928-157">Non mi toosee in grado di famiglia di dimensioni della macchina virtuale che si desidera quando si ridimensiona la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16928-157">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="16928-158">Quando una macchina virtuale è in esecuzione, è server fisico tooa distribuito.</span><span class="sxs-lookup"><span data-stu-id="16928-158">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="16928-159">i server fisici Hello in aree di Azure vengono raggruppati in cluster dell'hardware fisico comuni.</span><span class="sxs-lookup"><span data-stu-id="16928-159">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="16928-160">Ridimensiona una macchina virtuale che richiede hello VM toobe spostato toodifferent hardware cluster è diversa a seconda di quale modello di distribuzione è stato utilizzato toodeploy hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="16928-160">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="16928-161">Macchine virtuali distribuite nel modello di distribuzione classica, la distribuzione del servizio cloud hello devono essere rimossi e dimensioni di tooa toochange hello macchine virtuali in un altro gruppo di dimensioni di ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="16928-161">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="16928-162">Macchine virtuali distribuite nel modello di distribuzione di gestione delle risorse, è necessario arrestare tutte le macchine virtuali in hello set di disponibilità prima modifica hello dimensioni di qualsiasi macchina virtuale nel set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="16928-162">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="16928-163">Hello elencate dimensioni della macchina virtuale non sono supportata durante la distribuzione in Set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16928-163">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="16928-164">Scegliere una dimensione è supportata in cluster del set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="16928-164">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="16928-165">È consigliabile quando si crea che un gruppo di disponibilità toochoose hello più grande dimensioni delle macchine Virtuali si ritiene che e che il primo toohello distribuzione che set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="16928-165">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="16928-166">È possibile aggiungere un set di disponibilità tooan VM classico esistente?</span><span class="sxs-lookup"><span data-stu-id="16928-166">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="16928-167">Sì.</span><span class="sxs-lookup"><span data-stu-id="16928-167">Yes.</span></span> <span data-ttu-id="16928-168">È possibile aggiungere un classico esistente tooa macchina virtuale nuova o Set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="16928-168">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="16928-169">Per ulteriori informazioni vedere [aggiungere un set di disponibilità tooan macchina virtuale esistente](classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="16928-169">For more information see [Add an existing virtual machine tooan availability set](classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="16928-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="16928-170">Next steps</span></span>
<span data-ttu-id="16928-171">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="16928-171">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="16928-172">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="16928-172">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="16928-173">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="16928-173">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
