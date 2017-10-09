---
title: Domande frequenti sui dischi delle macchine virtuali IaaS di Azure | Microsoft Docs
description: Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="15d28-103">Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)</span><span class="sxs-lookup"><span data-stu-id="15d28-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="15d28-104">Questo articolo risponde alle domande frequenti su Managed Disks e Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="15d28-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="15d28-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="15d28-105">Managed Disks</span></span>

<span data-ttu-id="15d28-106">**Che cos'è Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="15d28-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="15d28-107">Managed Disks è una funzionalità che semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure, gestendo l'account di archiviazione per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="15d28-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="15d28-108">Per ulteriori informazioni, vedere hello [Panoramica di dischi gestiti](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="15d28-108">For more information, see hello [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="15d28-109">**Se si crea un disco gestito Standard da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="15d28-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="15d28-110">Un disco gestito standard creato da un disco rigido virtuale di 80 GB viene considerato come dimensione disponibile su disco standard successiva hello, che è un disco S10.</span><span class="sxs-lookup"><span data-stu-id="15d28-110">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="15d28-111">Vengono addebitati in base toohello S10 disco sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="15d28-111">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="15d28-112">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="15d28-112">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="15d28-113">**Sono previsti costi di transazione per i dischi gestiti Standard?**</span><span class="sxs-lookup"><span data-stu-id="15d28-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="15d28-114">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-114">Yes.</span></span> <span data-ttu-id="15d28-115">Sì, ogni transazione prevede un addebito.</span><span class="sxs-lookup"><span data-stu-id="15d28-115">You're charged for each transaction.</span></span> <span data-ttu-id="15d28-116">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="15d28-116">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="15d28-117">**Per un disco gestito standard, addebitata per dimensioni effettive di hello dei dati di hello su disco hello o per la capacità di hello il provisioning del disco hello?**</span><span class="sxs-lookup"><span data-stu-id="15d28-117">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="15d28-118">Vengono addebitati in base alle capacità di hello il provisioning del disco hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-118">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="15d28-119">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="15d28-119">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="15d28-120">**In che modo il prezzo della versione Premium dei dischi gestiti è diverso da quello dei dischi non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="15d28-121">Hello sui prezzi dei dischi premium gestiti hello come i dischi premium non gestito.</span><span class="sxs-lookup"><span data-stu-id="15d28-121">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="15d28-122">**È possibile modificare hello archiviazione tipo di account (Standard o Premium) di dischi personali gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-122">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="15d28-123">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-123">Yes.</span></span> <span data-ttu-id="15d28-124">Per cambiare tipo di account di archiviazione hello i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15d28-124">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="15d28-125">**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-125">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="15d28-126">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-126">Yes.</span></span> <span data-ttu-id="15d28-127">È possibile esportare i dischi gestiti tramite hello portale di Azure, PowerShell o hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="15d28-127">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="15d28-128">**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito con una sottoscrizione diversa?**</span><span class="sxs-lookup"><span data-stu-id="15d28-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="15d28-129">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-129">No.</span></span>

<span data-ttu-id="15d28-130">**È possibile utilizzare un file di disco rigido virtuale in un toocreate di account di archiviazione di Azure un disco gestito in un'area diversa?**</span><span class="sxs-lookup"><span data-stu-id="15d28-130">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="15d28-131">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-131">No.</span></span>

<span data-ttu-id="15d28-132">**Ci sono limitazioni di scalabilità per i clienti che usano dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="15d28-133">Dischi gestiti Elimina i limiti di hello associati agli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="15d28-133">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="15d28-134">Tuttavia, il numero di hello di dischi gestiti per ogni sottoscrizione è limitata too2, 000 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="15d28-134">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="15d28-135">È possibile chiamare il supporto tooincrease questo numero.</span><span class="sxs-lookup"><span data-stu-id="15d28-135">You can call support tooincrease this number.</span></span>

<span data-ttu-id="15d28-136">**È possibile fare uno snapshot incrementale di un disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="15d28-137">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-137">No.</span></span> <span data-ttu-id="15d28-138">funzionalità di snapshot corrente Hello crea una copia completa di un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="15d28-138">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="15d28-139">Tuttavia, si pianificare toosupport snapshot incrementali in hello future.</span><span class="sxs-lookup"><span data-stu-id="15d28-139">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="15d28-140">**Le macchine virtuali in un set di disponibilità possono essere composte da una combinazione di dischi gestiti e non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="15d28-141">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-141">No.</span></span> <span data-ttu-id="15d28-142">Hello macchine virtuali in un set di disponibilità deve utilizzare dischi gestiti o tutti i dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="15d28-142">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="15d28-143">Quando si crea un set di disponibilità, è possibile scegliere quale tipo di disco desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="15d28-143">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="15d28-144">**È l'opzione predefinita di dischi gestiti hello in hello portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="15d28-144">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="15d28-145">Non attualmente, ma sarà utilizzata l'impostazione predefinita, hello in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-145">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="15d28-146">**È possibile creare un disco vuoto gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="15d28-147">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-147">Yes.</span></span> <span data-ttu-id="15d28-148">È possibile creare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="15d28-148">You can create an empty disk.</span></span> <span data-ttu-id="15d28-149">Un disco gestito può essere creato in modo indipendente da una macchina virtuale, ad esempio, senza collegarlo tooa macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15d28-149">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="15d28-150">**Numero di domini di errore hello è supportato per un set di disponibilità che usa dischi gestiti novità**</span><span class="sxs-lookup"><span data-stu-id="15d28-150">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="15d28-151">A seconda area hello set di disponibilità hello che utilizza dischi gestiti in cui si trova, numero di domini di errore hello supportato è 2 o 3.</span><span class="sxs-lookup"><span data-stu-id="15d28-151">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="15d28-152">**È come account di archiviazione standard hello per configurare diagnostica?**</span><span class="sxs-lookup"><span data-stu-id="15d28-152">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="15d28-153">Si imposta un account di archiviazione privato per la diagnostica della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="15d28-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="15d28-154">In futuro hello, contiamo tooswitch Diagnostica dischi tooManaged anche.</span><span class="sxs-lookup"><span data-stu-id="15d28-154">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="15d28-155">**Che tipo di supporto per il controllo degli accessi in base al ruolo è disponibile per Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="15d28-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="15d28-156">Managed Disks supporta tre ruoli predefiniti principali:</span><span class="sxs-lookup"><span data-stu-id="15d28-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="15d28-157">Proprietario: può gestire tutto, compresi gli accessi</span><span class="sxs-lookup"><span data-stu-id="15d28-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="15d28-158">Collaboratore: può gestire tutto ad eccezione degli accessi</span><span class="sxs-lookup"><span data-stu-id="15d28-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="15d28-159">Lettore: può visualizzare tutto, ma non apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="15d28-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="15d28-160">**Esiste un modo che è possibile copiare o esportare un account di archiviazione privato tooa disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-160">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="15d28-161">È possibile ottenere una firma di accesso condiviso di sola lettura URI per hello gestito su disco e usarlo toocopy hello contenuto tooa archiviazione privato locale o account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="15d28-161">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="15d28-162">**È possibile creare una copia del proprio disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="15d28-163">Clienti di uno snapshot di propri dischi gestiti e quindi utilizzare un altro disco gestito toocreate snapshot hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-163">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="15d28-164">**I dischi non gestiti sono ancora supportati?**</span><span class="sxs-lookup"><span data-stu-id="15d28-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="15d28-165">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-165">Yes.</span></span> <span data-ttu-id="15d28-166">Sì, sono supportati sia i dischi gestiti che quelli non gestiti.</span><span class="sxs-lookup"><span data-stu-id="15d28-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="15d28-167">È consigliabile usare dischi gestiti per i nuovi carichi di lavoro e la migrazione dei dischi di toomanaged i carichi di lavoro corrente.</span><span class="sxs-lookup"><span data-stu-id="15d28-167">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="15d28-168">**Se si crea un disco da 128 GB e quindi aumentare hello dimensioni too130 GB, verrà addebitato dimensioni del disco successiva hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="15d28-168">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="15d28-169">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-169">Yes.</span></span>

<span data-ttu-id="15d28-170">**È possibile creare dischi gestiti per l'archiviazione con ridondanza locale, l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza della zona?**</span><span class="sxs-lookup"><span data-stu-id="15d28-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="15d28-171">Attualmente Azure Managed Disks supporta solo dischi gestiti per l'archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="15d28-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="15d28-172">**È possibile ridurre/ridimensionare i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="15d28-173">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-173">No.</span></span> <span data-ttu-id="15d28-174">Questa funzionalità non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="15d28-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="15d28-175">**È possibile modificare proprietà del nome computer hello quando specializzata (non creati tramite l'utilità preparazione sistema hello o generalizzata) disco del sistema operativo è tooprovision usato una macchina virtuale?**</span><span class="sxs-lookup"><span data-stu-id="15d28-175">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="15d28-176">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-176">No.</span></span> <span data-ttu-id="15d28-177">È possibile aggiornare una proprietà del nome computer hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-177">You can't update hello computer name property.</span></span> <span data-ttu-id="15d28-178">Hello nuova macchina virtuale eredita da padre hello VM, che è stato disco del sistema operativo utilizzato toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-178">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="15d28-179">**Dove trovare i modelli per Gestione risorse di Azure esempio toocreate macchine virtuali con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-179">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="15d28-180">Elenco di modelli che usano Managed Disks</span><span class="sxs-lookup"><span data-stu-id="15d28-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="15d28-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="15d28-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="15d28-182">Managed Disks e crittografia del servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="15d28-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="15d28-183">**La crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="15d28-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="15d28-184">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-184">Yes.</span></span>

<span data-ttu-id="15d28-185">**Che gestisce le chiavi di crittografia hello?**</span><span class="sxs-lookup"><span data-stu-id="15d28-185">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="15d28-186">Microsoft gestisce le chiavi di crittografia hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-186">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="15d28-187">**È possibile disabilitare la crittografia del servizio di archiviazione per i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="15d28-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="15d28-188">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-188">No.</span></span>

<span data-ttu-id="15d28-189">**La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**</span><span class="sxs-lookup"><span data-stu-id="15d28-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="15d28-190">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-190">No.</span></span> <span data-ttu-id="15d28-191">È disponibile in tutte le aree di hello in cui i dischi gestiti è disponibili.</span><span class="sxs-lookup"><span data-stu-id="15d28-191">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="15d28-192">Managed Disks è disponibile in tutte le aree pubbliche e in Germania.</span><span class="sxs-lookup"><span data-stu-id="15d28-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="15d28-193">**Come si può determinare se un disco gestito è crittografato?**</span><span class="sxs-lookup"><span data-stu-id="15d28-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="15d28-194">È possibile scoprire hello ora di creazione un disco gestito dal portale di Azure hello, hello CLI di Azure e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="15d28-194">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="15d28-195">Se hello viene eseguita dopo il 9 giugno 2017, il disco è crittografato.</span><span class="sxs-lookup"><span data-stu-id="15d28-195">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="15d28-196">**Come è possibile crittografare i dischi esistenti creati prima del 10 giugno 2017?**</span><span class="sxs-lookup"><span data-stu-id="15d28-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="15d28-197">A partire da 10 giugno 2017, dischi gestiti tooexisting nuovi dati vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="15d28-197">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="15d28-198">È inoltre pianificare i dati esistenti tooencrypt e crittografia hello avverrà in modo asincrono in background hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-198">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="15d28-199">Se è necessario crittografare i dati esistenti adesso, creare una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="15d28-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="15d28-200">I nuovi dischi verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="15d28-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="15d28-201">Copiare i dischi gestiti tramite hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="15d28-201">Copy managed disks by using hello Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="15d28-202">Copiare i dischi gestiti tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="15d28-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="15d28-203">**Le immagini e gli snapshot gestiti vengono crittografati?**</span><span class="sxs-lookup"><span data-stu-id="15d28-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="15d28-204">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-204">Yes.</span></span> <span data-ttu-id="15d28-205">Tutte le immagini e gli snapshot gestiti creati dopo il 9 giugno 2017 vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="15d28-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="15d28-206">**È possibile convertire le macchine virtuali con dischi non gestiti che si trovano sugli account di archiviazione o sono stati crittografati in precedenza toomanaged dischi?**</span><span class="sxs-lookup"><span data-stu-id="15d28-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="15d28-207">Sì</span><span class="sxs-lookup"><span data-stu-id="15d28-207">Yes</span></span>

<span data-ttu-id="15d28-208">**Un disco rigido virtuale esportato da un disco gestito o uno snapshot verrà crittografato?**</span><span class="sxs-lookup"><span data-stu-id="15d28-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="15d28-209">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-209">No.</span></span> <span data-ttu-id="15d28-210">Ma se si esporta un disco rigido virtuale tooan crittografate account di archiviazione da un disco gestito crittografato o di uno snapshot, quindi viene crittografato.</span><span class="sxs-lookup"><span data-stu-id="15d28-210">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="15d28-211">Dischi Premium, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="15d28-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="15d28-212">**Se una macchina virtuale usa una serie di dimensioni che supporta Archiviazione Premium, ad esempio DSv2, è possibile collegare dischi dati sia Premium che Standard?**</span><span class="sxs-lookup"><span data-stu-id="15d28-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="15d28-213">Sì.</span><span class="sxs-lookup"><span data-stu-id="15d28-213">Yes.</span></span>

<span data-ttu-id="15d28-214">**È possibile collegare sia premium e standard dischi tooa dimensioni serie di dati non supporta l'archiviazione Premium, ad esempio la serie D, Dv2, G o F**</span><span class="sxs-lookup"><span data-stu-id="15d28-214">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="15d28-215">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-215">No.</span></span> <span data-ttu-id="15d28-216">È possibile collegare solo i tooVMs dischi dati standard che non usano una serie di dimensioni che supporta l'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="15d28-216">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="15d28-217">**Se si crea un disco dati Premium da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="15d28-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="15d28-218">Un disco dati premium creato da un disco rigido virtuale di 80 GB viene considerato come dimensioni del disco premium disponibile con Avanti hello, che è un disco P10.</span><span class="sxs-lookup"><span data-stu-id="15d28-218">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="15d28-219">Vengono addebitati in base toohello P10 disco sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="15d28-219">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="15d28-220">**Sono presenti i costi di transazione toouse archiviazione Premium?**</span><span class="sxs-lookup"><span data-stu-id="15d28-220">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="15d28-221">È previsto un costo fisso per ogni dimensione di disco con provisioning di un certo numero di IOPS e di una certa velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="15d28-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="15d28-222">Hello altri costi sono la larghezza di banda in uscita e la capacità di snapshot, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="15d28-222">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="15d28-223">Per ulteriori informazioni, vedere hello [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="15d28-223">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="15d28-224">**Quali sono i limiti di hello per IOPS e la velocità effettiva che è possibile ottenere dalla cache di hello disco?**</span><span class="sxs-lookup"><span data-stu-id="15d28-224">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="15d28-225">limiti combinati per cache di Hello e unità SSD locale per una serie di dominio Active Directory sono 4.000 IOPS per ogni core e 33 MB al secondo per ogni core.</span><span class="sxs-lookup"><span data-stu-id="15d28-225">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="15d28-226">Hello serie GS offre 5.000 IOPS per ogni core e 50 MB al secondo per i componenti di base.</span><span class="sxs-lookup"><span data-stu-id="15d28-226">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="15d28-227">**È supportata da unità SSD locale per una macchina virtuale i dischi gestiti hello?**</span><span class="sxs-lookup"><span data-stu-id="15d28-227">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="15d28-228">Hello SSD locale temporanea di archiviazione è incluso in una macchina virtuale i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="15d28-228">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="15d28-229">Questa archiviazione temporanea non comporta costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="15d28-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="15d28-230">È consigliabile non utilizzare questo toostore SSD locale i dati delle applicazioni perché non è persistente nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="15d28-230">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="15d28-231">**Sono presenti eventuali ripercussioni per hello, utilizzare di TRIM su dischi premium?**</span><span class="sxs-lookup"><span data-stu-id="15d28-231">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="15d28-232">Non viene utilizzato toohello svantaggio di TRIM su dischi premium di Azure o i dischi standard.</span><span class="sxs-lookup"><span data-stu-id="15d28-232">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="15d28-233">Dimensioni dei nuovi dischi, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="15d28-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="15d28-234">**Che cos'è hello disco massime supportate per il sistema operativo e i dischi dati?**</span><span class="sxs-lookup"><span data-stu-id="15d28-234">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="15d28-235">tipo di partizione Hello che supporta Azure per un disco del sistema operativo è il record di avvio principale hello (MBR).</span><span class="sxs-lookup"><span data-stu-id="15d28-235">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="15d28-236">formato MBR Hello supporta dimensioni di un disco di too2 TB.</span><span class="sxs-lookup"><span data-stu-id="15d28-236">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="15d28-237">dimensione massima di Hello che supporta Azure per un disco del sistema operativo è di 2 TB.</span><span class="sxs-lookup"><span data-stu-id="15d28-237">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="15d28-238">Azure supporta backup too4 TB per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="15d28-238">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="15d28-239">**Che cos'è hello pagina blob massime supportate?**</span><span class="sxs-lookup"><span data-stu-id="15d28-239">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="15d28-240">Hello pagina blob massime che supporta Azure è 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="15d28-240">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="15d28-241">Maggiore di 4 TB (4.095 GB) collegati tooa macchina virtuale come dischi del sistema operativo o di dati BLOB di pagine non è supportato.</span><span class="sxs-lookup"><span data-stu-id="15d28-241">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="15d28-242">**Necessario toouse una nuova versione di strumenti di Azure toocreate, allegare, ridimensionare e caricare dischi superiori a 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="15d28-242">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="15d28-243">È necessario tooupgrade il toocreate gli strumenti di Azure esistente, collegare o ridimensionare i dischi di dimensioni superiori a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="15d28-243">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="15d28-244">tooupload file disco rigido virtuale locale direttamente tooAzure come un blob di pagine o un disco non gestito, è necessario set di strumenti più recenti toouse hello:</span><span class="sxs-lookup"><span data-stu-id="15d28-244">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="15d28-245">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="15d28-245">Azure tools</span></span>      | <span data-ttu-id="15d28-246">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="15d28-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="15d28-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="15d28-247">Azure PowerShell</span></span> | <span data-ttu-id="15d28-248">Numero di versione 4.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="15d28-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="15d28-249">Interfaccia della riga di comando di Azure v1</span><span class="sxs-lookup"><span data-stu-id="15d28-249">Azure CLI v1</span></span>     | <span data-ttu-id="15d28-250">Numero di versione 0.10.13: versione di maggio 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="15d28-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="15d28-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="15d28-251">AzCopy</span></span>           | <span data-ttu-id="15d28-252">Numero di versione 6.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="15d28-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="15d28-253">supporto di Hello per v2 CLI di Azure e Azure Storage Explorer sarà presto disponibile.</span><span class="sxs-lookup"><span data-stu-id="15d28-253">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="15d28-254">**Le dimensioni del disco P4 e P6 sono supportate per i dischi gestiti o i BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="15d28-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="15d28-255">No.</span><span class="sxs-lookup"><span data-stu-id="15d28-255">No.</span></span> <span data-ttu-id="15d28-256">Le dimensioni del disco P4 (32 GB) e P6 (64 GB) sono supportate solo per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="15d28-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="15d28-257">Il supporto per dischi non gestiti e BLOB di pagine sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="15d28-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="15d28-258">**Se il premio esistente gestiti disco minore di 64 GB è stato creato prima il disco di piccole dimensioni hello è stato abilitato (circa 15 giugno 2017), come la fatturazione?**</span><span class="sxs-lookup"><span data-stu-id="15d28-258">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="15d28-259">Dischi di piccole dimensioni premium esistenti minore di 64 GB continuare toobe fatturato secondo toohello P10 piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="15d28-259">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="15d28-260">**Come è possibile passare a livelli disco hello di dischi di piccole dimensioni premium minore di 64 GB da P10 tooP4 o P6?**</span><span class="sxs-lookup"><span data-stu-id="15d28-260">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="15d28-261">È possibile creare uno snapshot di dischi di piccole dimensioni e quindi creare un hello di commutatore tooautomatically disco prezzi tooP4 livello o P6 in base alle dimensioni di hello il provisioning.</span><span class="sxs-lookup"><span data-stu-id="15d28-261">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="15d28-262">Cosa fare se non è disponibile una risposta alla domanda?</span><span class="sxs-lookup"><span data-stu-id="15d28-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="15d28-263">Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.</span><span class="sxs-lookup"><span data-stu-id="15d28-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="15d28-264">È possibile pubblicare una domanda alla fine di hello di questo articolo in commenti hello.</span><span class="sxs-lookup"><span data-stu-id="15d28-264">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="15d28-265">tooengage con il team di archiviazione di Azure hello e altri membri della community su questo articolo, utilizzare hello MSDN [forum di Azure Storage](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="15d28-265">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="15d28-266">funzionalità toorequest, inviare toohello le richieste e idee [forum sul feedback su archiviazione di Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="15d28-266">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
