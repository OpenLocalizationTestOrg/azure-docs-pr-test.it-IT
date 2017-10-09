---
title: distribuzione di problemi di macchine virtuali Linux in Azure aaaTroubleshoot | Documenti Microsoft
description: Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure con il modello di distribuzione Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
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
ms.openlocfilehash: d1092ca3d9d51af7510b19c8c9a79e6dda588697
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deploying-linux-virtual-machine-issues-in-azure"></a><span data-ttu-id="8ee9a-103">Risolvere i problemi di distribuzione della macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="8ee9a-103">Troubleshoot deploying Linux virtual machine issues in Azure</span></span>

<span data-ttu-id="8ee9a-104">problemi relativi alla distribuzione di macchina virtuale (VM) tootroubleshoot in Azure, esaminare hello [problemi principali](#top-issues) per errori e le risoluzioni comuni.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-104">tootroubleshoot virtual machine (VM) deployment issues in Azure, review hello [top issues](#top-issues) for common failures and resolutions.</span></span>

<span data-ttu-id="8ee9a-105">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-105">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span> <span data-ttu-id="8ee9a-106">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-106">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="8ee9a-107">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-107">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>

## <a name="top-issues"></a><span data-ttu-id="8ee9a-108">Problemi principali</span><span class="sxs-lookup"><span data-stu-id="8ee9a-108">Top issues</span></span>
[!INCLUDE [virtual-machines-linux-troubleshoot-deploy-vm-top](../../../includes/virtual-machines-linux-troubleshoot-deploy-vm-top.md)]

## <a name="hello-cluster-cannot-support-hello-requested-vm-size"></a><span data-ttu-id="8ee9a-109">non supporta cluster Hello hello richiesto dimensioni delle macchine Virtuali</span><span class="sxs-lookup"><span data-stu-id="8ee9a-109">hello cluster cannot support hello requested VM size</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="8ee9a-110">Riprovare hello richiesta utilizzando una dimensione più piccola di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-110">Retry hello request using a smaller VM size.</span></span>
- <span data-ttu-id="8ee9a-111">Se hello dimensioni hello richieste di che macchina virtuale non può essere modificato:</span><span class="sxs-lookup"><span data-stu-id="8ee9a-111">If hello size of hello requested VM cannot be changed:</span></span>
    - <span data-ttu-id="8ee9a-112">Arrestare tutte le macchine virtuali hello in set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-112">Stop all hello VMs in hello availability set.</span></span> <span data-ttu-id="8ee9a-113">Fare clic su **Gruppi di risorse** > il proprio gruppo di risorse > **Risorse** > il proprio set di disponibilità > **Macchine virtuali** > la propria macchina virtuale > **Arresta**.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-113">Click **Resource groups** > your resource group > **Resources** > your availability set > **Virtual Machines** > your virtual machine > **Stop**.</span></span>
    - <span data-ttu-id="8ee9a-114">Dopo che tutti hello arrestare le macchine virtuali, creare hello VM dimensioni hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-114">After all hello VMs stop, create hello VM in hello desired size.</span></span>
    - <span data-ttu-id="8ee9a-115">Avviare hello prima nuova macchina virtuale e quindi selezionare hello arrestare le macchine virtuali e fare clic su Avvia.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-115">Start hello new VM first, and then select each of hello stopped VMs and click Start.</span></span>


## <a name="hello-cluster-does-not-have-free-resources"></a><span data-ttu-id="8ee9a-116">cluster Hello privo di liberare le risorse</span><span class="sxs-lookup"><span data-stu-id="8ee9a-116">hello cluster does not have free resources</span></span>
<properties
supportTopicIds="123456789"
resourceTags="windows"
productPesIds="1234, 5678"
/>
- <span data-ttu-id="8ee9a-117">Riprovare più tardi richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-117">Retry hello request later.</span></span>
- <span data-ttu-id="8ee9a-118">Se hello nuova macchina virtuale è possibile essere incluso un diverso set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="8ee9a-118">If hello new VM can be part of a different availability set</span></span>
    - <span data-ttu-id="8ee9a-119">Creare una macchina virtuale in un set di disponibilità diverso (in hello stessa regione).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-119">Create a VM in a different availability set (in hello same region).</span></span>
    - <span data-ttu-id="8ee9a-120">Aggiungere hello nuova VM toohello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-120">Add hello new VM toohello same virtual network.</span></span>

## <a name="how-do-i-activate-my-monthly-credit-for-visual-studio-enterprise-bizspark"></a><span data-ttu-id="8ee9a-121">Come attivare il credito mensile per Visual Studio Enterprise (BizSpark)</span><span class="sxs-lookup"><span data-stu-id="8ee9a-121">How do I activate my monthly credit for Visual studio Enterprise (BizSpark)</span></span>

<span data-ttu-id="8ee9a-122">tooactivate la frequenza mensile del credito, vedere questo [articolo](https://azure.microsoft.com/offers/ms-azr-0064p/).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-122">tooactivate your monthly  credit, see this [article](https://azure.microsoft.com/offers/ms-azr-0064p/).</span></span>

## <a name="why-can-i-not-install-hello-gpu-driver-for-an-ubuntu-nv-vm"></a><span data-ttu-id="8ee9a-123">Motivo per cui è possibile non installare driver della GPU hello per una macchina virtuale NV Ubuntu?</span><span class="sxs-lookup"><span data-stu-id="8ee9a-123">Why can I not install hello GPU driver for an Ubuntu NV VM?</span></span>

<span data-ttu-id="8ee9a-124">Attualmente, il supporto per GPU Linux è disponibile solo sulle macchine virtuali NC di Azure che eseguono Ubuntu Server 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-124">Currently, Linux GPU support is only available on Azure NC VMs running Ubuntu Server 16.04 LTS.</span></span> <span data-ttu-id="8ee9a-125">Per altre informazioni, vedere [Configurare i driver GPU per le VM serie N che eseguono Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-125">For more information, see [Set up GPU drivers for N-series VMs running Linux](n-series-driver-setup.md).</span></span>

## <a name="my-drivers-are-missing-for-my-linux-n-series-vm"></a><span data-ttu-id="8ee9a-126">I driver della VM serie N di Linux non sono disponibili</span><span class="sxs-lookup"><span data-stu-id="8ee9a-126">My drivers are missing for my Linux N-Series VM</span></span>

<span data-ttu-id="8ee9a-127">I driver per le macchine virtuali basate su Linux si trovano [qui](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-127">Drivers for Linux-based VMs are located [here](n-series-driver-setup.md).</span></span> 

## <a name="i-cant-find-a-gpu-instance-within-my-n-series-vm"></a><span data-ttu-id="8ee9a-128">Nella VM Serie N non è disponibile un'istanza GPU</span><span class="sxs-lookup"><span data-stu-id="8ee9a-128">I can’t find a GPU instance within my N-Series VM</span></span>

<span data-ttu-id="8ee9a-129">tootake le funzionalità GPU hello di macchine virtuali di Azure serie N che esegue Windows Server 2016 o Windows Server 2012 R2, è necessario installare i driver grafici NVIDIA in ogni macchina virtuale dopo la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-129">tootake advantage of hello GPU capabilities of Azure N-series VMs running Windows Server 2016 or Windows Server 2012 R2, you must install NVIDIA graphics drivers on each VM after deployment.</span></span> <span data-ttu-id="8ee9a-130">Le informazioni di configurazione dei driver sono disponibili anche per le [VM Windows](../windows/n-series-driver-setup.md) e le [VM Linux](n-series-driver-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-130">Driver setup information is available for [Windows VMs](../windows/n-series-driver-setup.md) and [Linux VMs](n-series-driver-setup.md).</span></span>

## <a name="is-n-series-vms-available-in-my-region"></a><span data-ttu-id="8ee9a-131">Le VM Serie N sono disponibili nella mia area?</span><span class="sxs-lookup"><span data-stu-id="8ee9a-131">Is N-Series VMs available in my region?</span></span>

<span data-ttu-id="8ee9a-132">È possibile controllare la disponibilità di hello da hello [i prodotti disponibili dalla tabella region](https://azure.microsoft.com/regions/services), nonché i prezzi [qui](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-132">You can check hello availability from hello [Products available by region table](https://azure.microsoft.com/regions/services), and pricing [here](https://azure.microsoft.com/pricing/details/virtual-machines/series/#n-series).</span></span>

## <a name="i-am-not-able-toosee-vm-size-family-that-i-want-when-resizing-my-vm"></a><span data-ttu-id="8ee9a-133">Non mi toosee in grado di famiglia di dimensioni della macchina virtuale che si desidera quando si ridimensiona la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-133">I am not able toosee VM Size family that I want when resizing my VM.</span></span>

<span data-ttu-id="8ee9a-134">Quando una macchina virtuale è in esecuzione, è server fisico tooa distribuito.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-134">When a VM is running, it is deployed tooa physical server.</span></span> <span data-ttu-id="8ee9a-135">i server fisici Hello in aree di Azure vengono raggruppati in cluster dell'hardware fisico comuni.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-135">hello physical servers in Azure regions are grouped in clusters of common physical hardware.</span></span> <span data-ttu-id="8ee9a-136">Ridimensiona una macchina virtuale che richiede hello VM toobe spostato toodifferent hardware cluster è diversa a seconda di quale modello di distribuzione è stato utilizzato toodeploy hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-136">Resizing a VM that requires hello VM toobe moved toodifferent hardware clusters is different depending on which deployment model was used toodeploy hello VM.</span></span>

- <span data-ttu-id="8ee9a-137">Macchine virtuali distribuite nel modello di distribuzione classica, la distribuzione del servizio cloud hello devono essere rimossi e dimensioni di tooa toochange hello macchine virtuali in un altro gruppo di dimensioni di ridistribuzione.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-137">VMs deployed in Classic deployment model, hello cloud service deployment must be removed and redeployed toochange hello VMs tooa size in another size family.</span></span>

- <span data-ttu-id="8ee9a-138">Macchine virtuali distribuite nel modello di distribuzione di gestione delle risorse, è necessario arrestare tutte le macchine virtuali in hello set di disponibilità prima modifica hello dimensioni di qualsiasi macchina virtuale nel set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-138">VMs deployed in Resource Manager deployment model, you must stop all VMs in hello availability set before changing hello size of any VM in hello availability set.</span></span>

## <a name="hello-listed-vm-size-is-not-supported-while-deploying-in-availability-set"></a><span data-ttu-id="8ee9a-139">Hello elencate dimensioni della macchina virtuale non sono supportata durante la distribuzione in Set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-139">hello listed VM size is not supported while deploying in Availability Set.</span></span>

<span data-ttu-id="8ee9a-140">Scegliere una dimensione è supportata in cluster del set di disponibilità hello.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-140">Choose a size that is supported on hello availability set's cluster.</span></span> <span data-ttu-id="8ee9a-141">È consigliabile quando si crea che un gruppo di disponibilità toochoose hello più grande dimensioni delle macchine Virtuali si ritiene che e che il primo toohello distribuzione che set di disponibilità.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-141">It is recommended when creating an availability set toochoose hello largest VM size you think you need, and have that be your first deployment toohello Availability set.</span></span>

## <a name="what-linux-distributionsversions-are-supported-on-azure"></a><span data-ttu-id="8ee9a-142">Quali distribuzioni/versioni di Linux sono supportate in Azure?</span><span class="sxs-lookup"><span data-stu-id="8ee9a-142">What Linux distributions/versions are supported on Azure?</span></span>

<span data-ttu-id="8ee9a-143">È possibile trovare l'elenco di hello in Linux nel [Azure-Endorsed distribuzioni](endorsed-distros.md).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-143">You can find hello list at Linux on [Azure-Endorsed Distributions](endorsed-distros.md).</span></span>

## <a name="can-i-add-an-existing-classic-vm-tooan-availability-set"></a><span data-ttu-id="8ee9a-144">È possibile aggiungere un set di disponibilità tooan VM classico esistente?</span><span class="sxs-lookup"><span data-stu-id="8ee9a-144">Can I add an existing Classic VM tooan availability set?</span></span>

<span data-ttu-id="8ee9a-145">Sì.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-145">Yes.</span></span> <span data-ttu-id="8ee9a-146">È possibile aggiungere un classico esistente tooa macchina virtuale nuova o Set di disponibilità esistente.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-146">You can add an existing classic VM tooa new or existing Availability Set.</span></span> <span data-ttu-id="8ee9a-147">Per ulteriori informazioni vedere [aggiungere un set di disponibilità tooan macchina virtuale esistente](../windows/classic/configure-availability.md#addmachine).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-147">For more information see [Add an existing virtual machine tooan availability set](../windows/classic/configure-availability.md#addmachine).</span></span>


## <a name="next-steps"></a><span data-ttu-id="8ee9a-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ee9a-148">Next steps</span></span>
<span data-ttu-id="8ee9a-149">Se è necessario ulteriore assistenza in qualsiasi punto in questo articolo, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="8ee9a-149">If you need more help at any point in this article, you can contact hello Azure experts on [hello MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/support/forums/).</span></span>

<span data-ttu-id="8ee9a-150">In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-150">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="8ee9a-151">Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.</span><span class="sxs-lookup"><span data-stu-id="8ee9a-151">Go toohello [Azure support site](https://azure.microsoft.com/support/options/) and select **Get Support**.</span></span>
