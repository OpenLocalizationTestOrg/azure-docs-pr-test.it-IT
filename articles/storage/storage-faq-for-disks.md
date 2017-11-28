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
ms.openlocfilehash: 9e5eed35334f1b95441b8181c8e90645be78b389
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="d366b-103">Domande frequenti sui dischi e sui dischi Premium delle macchine virtuali IaaS di Azure (gestiti e non gestiti)</span><span class="sxs-lookup"><span data-stu-id="d366b-103">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="d366b-104">Questo articolo risponde alle domande frequenti su Managed Disks e Archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="d366b-104">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="d366b-105">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="d366b-105">Managed Disks</span></span>

<span data-ttu-id="d366b-106">**Che cos'è Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="d366b-106">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="d366b-107">Managed Disks è una funzionalità che semplifica la gestione dei dischi per le macchine virtuali IaaS di Azure, gestendo l'account di archiviazione per conto dell'utente.</span><span class="sxs-lookup"><span data-stu-id="d366b-107">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="d366b-108">Per altre informazioni, vedere [Panoramica di Azure Managed Disks](storage-managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d366b-108">For more information, see the [Managed Disks overview](storage-managed-disks-overview.md).</span></span>

<span data-ttu-id="d366b-109">**Se si crea un disco gestito Standard da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="d366b-109">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="d366b-110">Un disco gestito Standard creato da un disco rigido virtuale da 80 GB viene considerato come il disco Standard immediatamente successivo in termini di dimensioni, ovvero un disco S10.</span><span class="sxs-lookup"><span data-stu-id="d366b-110">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="d366b-111">Il costo addebitato corrisponde al prezzo del disco S10.</span><span class="sxs-lookup"><span data-stu-id="d366b-111">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="d366b-112">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="d366b-112">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="d366b-113">**Sono previsti costi di transazione per i dischi gestiti Standard?**</span><span class="sxs-lookup"><span data-stu-id="d366b-113">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="d366b-114">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-114">Yes.</span></span> <span data-ttu-id="d366b-115">Sì, ogni transazione prevede un addebito.</span><span class="sxs-lookup"><span data-stu-id="d366b-115">You're charged for each transaction.</span></span> <span data-ttu-id="d366b-116">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="d366b-116">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="d366b-117">**Per un disco gestito Standard, si riceverà un addebito per le dimensioni effettive dei dati su disco o per la capacità con provisioning del disco?**</span><span class="sxs-lookup"><span data-stu-id="d366b-117">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="d366b-118">L'addebito viene effettuato in base alla capacità con provisioning del disco.</span><span class="sxs-lookup"><span data-stu-id="d366b-118">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="d366b-119">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="d366b-119">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="d366b-120">**In che modo il prezzo della versione Premium dei dischi gestiti è diverso da quello dei dischi non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-120">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="d366b-121">Il prezzo della versione Premium dei dischi gestiti è uguale a quello della versione Premium dei dischi non gestiti.</span><span class="sxs-lookup"><span data-stu-id="d366b-121">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="d366b-122">**È possibile modificare il tipo di account di archiviazione (Standard o Premium) dei dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-122">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="d366b-123">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-123">Yes.</span></span> <span data-ttu-id="d366b-124">È possibile modificare il tipo di account di archiviazione dei dischi gestiti tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d366b-124">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="d366b-125">**È possibile copiare o esportare un disco gestito in un account di archiviazione privato?**</span><span class="sxs-lookup"><span data-stu-id="d366b-125">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="d366b-126">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-126">Yes.</span></span> <span data-ttu-id="d366b-127">Sì, è possibile esportare i dischi gestiti tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d366b-127">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="d366b-128">**È possibile usare un file di disco rigido virtuale in un account di archiviazione di Azure per creare un disco gestito con una sottoscrizione diversa?**</span><span class="sxs-lookup"><span data-stu-id="d366b-128">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="d366b-129">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-129">No.</span></span>

<span data-ttu-id="d366b-130">**È possibile usare un file di disco rigido virtuale in un account di archiviazione di Azure per creare un disco gestito in un'area geografica diversa?**</span><span class="sxs-lookup"><span data-stu-id="d366b-130">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="d366b-131">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-131">No.</span></span>

<span data-ttu-id="d366b-132">**Ci sono limitazioni di scalabilità per i clienti che usano dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-132">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="d366b-133">Managed Disks elimina i limiti legati agli account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d366b-133">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="d366b-134">Tuttavia, il numero di dischi gestiti per ogni sottoscrizione è limitato a 2.000 per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d366b-134">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="d366b-135">È possibile aumentare questo numero rivolgendosi al supporto.</span><span class="sxs-lookup"><span data-stu-id="d366b-135">You can call support to increase this number.</span></span>

<span data-ttu-id="d366b-136">**È possibile fare uno snapshot incrementale di un disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="d366b-136">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="d366b-137">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-137">No.</span></span> <span data-ttu-id="d366b-138">La funzionalità snapshot corrente crea una copia completa di un disco gestito.</span><span class="sxs-lookup"><span data-stu-id="d366b-138">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="d366b-139">Tuttavia è previsto un supporto futuro per gli snapshot incrementali.</span><span class="sxs-lookup"><span data-stu-id="d366b-139">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="d366b-140">**Le macchine virtuali in un set di disponibilità possono essere composte da una combinazione di dischi gestiti e non gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-140">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="d366b-141">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-141">No.</span></span> <span data-ttu-id="d366b-142">No, i dischi nelle macchine virtuali in un set di disponibilità devono essere o tutti gestiti o tutti non gestiti.</span><span class="sxs-lookup"><span data-stu-id="d366b-142">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="d366b-143">Quando si crea un set di disponibilità, è possibile scegliere il tipo di dischi da usare.</span><span class="sxs-lookup"><span data-stu-id="d366b-143">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="d366b-144">**Managed Disks è l'opzione predefinita nel portale di Azure?**</span><span class="sxs-lookup"><span data-stu-id="d366b-144">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="d366b-145">Non attualmente, ma diventerà l'impostazione predefinita in futuro.</span><span class="sxs-lookup"><span data-stu-id="d366b-145">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="d366b-146">**È possibile creare un disco vuoto gestito?**</span><span class="sxs-lookup"><span data-stu-id="d366b-146">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="d366b-147">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-147">Yes.</span></span> <span data-ttu-id="d366b-148">È possibile creare un disco vuoto.</span><span class="sxs-lookup"><span data-stu-id="d366b-148">You can create an empty disk.</span></span> <span data-ttu-id="d366b-149">Un disco gestito può essere creato indipendentemente da una macchina virtuale, ad esempio non collegandolo a una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d366b-149">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="d366b-150">**Qual è il numero di domini di errore supportati per un set di disponibilità con Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="d366b-150">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="d366b-151">Il numero di domini di errore supportato per i set di disponibilità con Managed Disks è di 2 o 3, a seconda dell'area in cui si trovano.</span><span class="sxs-lookup"><span data-stu-id="d366b-151">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="d366b-152">**Come viene configurato l'account di archiviazione Standard per l'impostazione della diagnostica?**</span><span class="sxs-lookup"><span data-stu-id="d366b-152">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="d366b-153">Si imposta un account di archiviazione privato per la diagnostica della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d366b-153">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="d366b-154">In futuro, si intende estendere la diagnostica anche a Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="d366b-154">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="d366b-155">**Che tipo di supporto per il controllo degli accessi in base al ruolo è disponibile per Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="d366b-155">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="d366b-156">Managed Disks supporta tre ruoli predefiniti principali:</span><span class="sxs-lookup"><span data-stu-id="d366b-156">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="d366b-157">Proprietario: può gestire tutto, compresi gli accessi</span><span class="sxs-lookup"><span data-stu-id="d366b-157">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="d366b-158">Collaboratore: può gestire tutto ad eccezione degli accessi</span><span class="sxs-lookup"><span data-stu-id="d366b-158">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="d366b-159">Lettore: può visualizzare tutto, ma non apportare modifiche</span><span class="sxs-lookup"><span data-stu-id="d366b-159">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="d366b-160">**È possibile copiare o esportare un disco gestito in un account di archiviazione privato?**</span><span class="sxs-lookup"><span data-stu-id="d366b-160">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="d366b-161">È possibile ottenere un URI di firma di accesso condiviso di sola lettura per il disco gestito e usarla per copiare i contenuti in un account di archiviazione privato o in un archivio locale.</span><span class="sxs-lookup"><span data-stu-id="d366b-161">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="d366b-162">**È possibile creare una copia del proprio disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="d366b-162">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="d366b-163">I clienti possono eseguire uno snapshot dei relativi dischi gestiti e usarlo per creare un altro disco gestito.</span><span class="sxs-lookup"><span data-stu-id="d366b-163">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="d366b-164">**I dischi non gestiti sono ancora supportati?**</span><span class="sxs-lookup"><span data-stu-id="d366b-164">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="d366b-165">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-165">Yes.</span></span> <span data-ttu-id="d366b-166">Sì, sono supportati sia i dischi gestiti che quelli non gestiti.</span><span class="sxs-lookup"><span data-stu-id="d366b-166">We support unmanaged and managed disks.</span></span> <span data-ttu-id="d366b-167">È consigliabile usare i dischi gestiti per i nuovi carichi di lavoro ed eseguire la migrazione dei carichi di lavoro correnti a dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="d366b-167">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="d366b-168">**Se si crea un disco da 128 GB e si aumentano le dimensioni a 130 GB, verranno addebitati i costi relativi al livello di dimensioni successivo (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="d366b-168">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="d366b-169">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-169">Yes.</span></span>

<span data-ttu-id="d366b-170">**È possibile creare dischi gestiti per l'archiviazione con ridondanza locale, l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza della zona?**</span><span class="sxs-lookup"><span data-stu-id="d366b-170">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="d366b-171">Attualmente Azure Managed Disks supporta solo dischi gestiti per l'archiviazione con ridondanza locale.</span><span class="sxs-lookup"><span data-stu-id="d366b-171">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="d366b-172">**È possibile ridurre/ridimensionare i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-172">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="d366b-173">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-173">No.</span></span> <span data-ttu-id="d366b-174">Questa funzionalità non è attualmente supportata.</span><span class="sxs-lookup"><span data-stu-id="d366b-174">This feature is not supported currently.</span></span> 

<span data-ttu-id="d366b-175">**È possibile modificare la proprietà del nome del computer quando si usa un disco del sistema operativo specializzato (non preparato con Utilità preparazione sistema o generalizzato) per il provisioning di una VM?**</span><span class="sxs-lookup"><span data-stu-id="d366b-175">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="d366b-176">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-176">No.</span></span> <span data-ttu-id="d366b-177">Non è possibile aggiornare la proprietà del nome del computer.</span><span class="sxs-lookup"><span data-stu-id="d366b-177">You can't update the computer name property.</span></span> <span data-ttu-id="d366b-178">La nuova VM eredita la proprietà dalla VM padre usata per creare il disco del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d366b-178">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="d366b-179">**Dove si possono trovare modelli di Azure Resource Manager di esempio per creare macchine virtuali con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-179">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="d366b-180">Elenco di modelli che usano Managed Disks</span><span class="sxs-lookup"><span data-stu-id="d366b-180">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="d366b-181">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="d366b-181">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="d366b-182">Managed Disks e crittografia del servizio di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d366b-182">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="d366b-183">**La crittografia del servizio di archiviazione è abilitata per impostazione predefinita quando si crea un nuovo disco gestito?**</span><span class="sxs-lookup"><span data-stu-id="d366b-183">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="d366b-184">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-184">Yes.</span></span>

<span data-ttu-id="d366b-185">**Chi gestisce le chiavi di crittografia?**</span><span class="sxs-lookup"><span data-stu-id="d366b-185">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="d366b-186">Le chiavi di crittografia sono gestite da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d366b-186">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="d366b-187">**È possibile disabilitare la crittografia del servizio di archiviazione per i dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-187">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="d366b-188">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-188">No.</span></span>

<span data-ttu-id="d366b-189">**La crittografia del servizio di archiviazione è disponibile solo in aree specifiche?**</span><span class="sxs-lookup"><span data-stu-id="d366b-189">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="d366b-190">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-190">No.</span></span> <span data-ttu-id="d366b-191">È disponibile in tutte le aree in cui è disponibile Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="d366b-191">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="d366b-192">Managed Disks è disponibile in tutte le aree pubbliche e in Germania.</span><span class="sxs-lookup"><span data-stu-id="d366b-192">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="d366b-193">**Come si può determinare se un disco gestito è crittografato?**</span><span class="sxs-lookup"><span data-stu-id="d366b-193">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="d366b-194">Si può scoprire quando è stato creato il disco gestito tramite il portale di Azure, PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d366b-194">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="d366b-195">Se è stato creato dopo il 9 giugno 2017, il disco è crittografato.</span><span class="sxs-lookup"><span data-stu-id="d366b-195">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="d366b-196">**Come è possibile crittografare i dischi esistenti creati prima del 10 giugno 2017?**</span><span class="sxs-lookup"><span data-stu-id="d366b-196">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="d366b-197">A partire dal 10 giugno 2017, i nuovi dati scritti nei dischi gestiti esistenti vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d366b-197">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="d366b-198">È anche prevista l'implementazione della crittografia dei dati esistenti, che verrà eseguita in modo asincrono in background.</span><span class="sxs-lookup"><span data-stu-id="d366b-198">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="d366b-199">Se è necessario crittografare i dati esistenti adesso, creare una copia del disco.</span><span class="sxs-lookup"><span data-stu-id="d366b-199">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="d366b-200">I nuovi dischi verranno crittografati.</span><span class="sxs-lookup"><span data-stu-id="d366b-200">New disks will be encrypted.</span></span>

* [<span data-ttu-id="d366b-201">Copiare i dischi gestiti tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d366b-201">Copy managed disks by using the Azure CLI</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="d366b-202">Copiare i dischi gestiti tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="d366b-202">Copy managed disks by using PowerShell</span></span>](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="d366b-203">**Le immagini e gli snapshot gestiti vengono crittografati?**</span><span class="sxs-lookup"><span data-stu-id="d366b-203">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="d366b-204">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-204">Yes.</span></span> <span data-ttu-id="d366b-205">Tutte le immagini e gli snapshot gestiti creati dopo il 9 giugno 2017 vengono crittografati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d366b-205">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="d366b-206">**È possibile convertire macchine virtuali con dischi non gestiti ubicati in account di archiviazione che sono o sono stati crittografati in precedenza in VM con dischi gestiti?**</span><span class="sxs-lookup"><span data-stu-id="d366b-206">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="d366b-207">Sì</span><span class="sxs-lookup"><span data-stu-id="d366b-207">Yes</span></span>

<span data-ttu-id="d366b-208">**Un disco rigido virtuale esportato da un disco gestito o uno snapshot verrà crittografato?**</span><span class="sxs-lookup"><span data-stu-id="d366b-208">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="d366b-209">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-209">No.</span></span> <span data-ttu-id="d366b-210">Se però si esporta un disco rigido virtuale da un disco gestito o uno snapshot crittografato a un account di archiviazione crittografato, verrà crittografato.</span><span class="sxs-lookup"><span data-stu-id="d366b-210">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="d366b-211">Dischi Premium, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="d366b-211">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="d366b-212">**Se una macchina virtuale usa una serie di dimensioni che supporta Archiviazione Premium, ad esempio DSv2, è possibile collegare dischi dati sia Premium che Standard?**</span><span class="sxs-lookup"><span data-stu-id="d366b-212">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="d366b-213">Sì.</span><span class="sxs-lookup"><span data-stu-id="d366b-213">Yes.</span></span>

<span data-ttu-id="d366b-214">**È possibile collegare dischi sia Premium che Standard a una serie di dimensioni che non supporta Archiviazione Premium, come le serie D, Dv2, G o F?**</span><span class="sxs-lookup"><span data-stu-id="d366b-214">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="d366b-215">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-215">No.</span></span> <span data-ttu-id="d366b-216">È possibile collegare solo dischi dati Standard alle macchine virtuali che non usano una serie di dimensioni con supporto di Archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="d366b-216">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="d366b-217">**Se si crea un disco dati Premium da un disco rigido virtuale esistente da 80 GB, qual è il costo?**</span><span class="sxs-lookup"><span data-stu-id="d366b-217">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="d366b-218">Un disco dati Premium creato da un disco rigido virtuale da 80 GB viene considerato come il disco Premium immediatamente successivo in termini di dimensioni, ovvero un disco P10.</span><span class="sxs-lookup"><span data-stu-id="d366b-218">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="d366b-219">Il costo addebitato corrisponde al prezzo del disco P10.</span><span class="sxs-lookup"><span data-stu-id="d366b-219">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="d366b-220">**Sono previsti costi per transazione per usare Archiviazione Premium?**</span><span class="sxs-lookup"><span data-stu-id="d366b-220">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="d366b-221">È previsto un costo fisso per ogni dimensione di disco con provisioning di un certo numero di IOPS e di una certa velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="d366b-221">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="d366b-222">Gli altri costi sono la larghezza di banda in uscita e la capacità di snapshot, se applicabile.</span><span class="sxs-lookup"><span data-stu-id="d366b-222">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="d366b-223">Per altre informazioni vedere la [pagina dei prezzi](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="d366b-223">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="d366b-224">**Quali sono i limiti per IOPS e velocità effettiva che è possibile ottenere dalla cache del disco?**</span><span class="sxs-lookup"><span data-stu-id="d366b-224">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="d366b-225">I limiti combinati per la cache e l'unità SSD locale per la serie DS sono 4.000 IOPS per core e 33 MB al secondo per core.</span><span class="sxs-lookup"><span data-stu-id="d366b-225">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="d366b-226">La serie GS offre 5,000 IOPS per core e 50 MB al secondo per core.</span><span class="sxs-lookup"><span data-stu-id="d366b-226">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="d366b-227">**Sono supportate le unità SSD locali per le macchine virtuali di Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="d366b-227">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="d366b-228">L'unità SSD locale è un archivio temporaneo che è incluso in una macchina virtuale di Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="d366b-228">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="d366b-229">Questa archiviazione temporanea non comporta costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="d366b-229">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="d366b-230">Si consiglia di non usare questa unità SSD locale per archiviare dati applicazione, perché non vengono salvati in modo permanente nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d366b-230">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="d366b-231">**L'uso di TRIM su dischi Premium ha ripercussioni?**</span><span class="sxs-lookup"><span data-stu-id="d366b-231">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="d366b-232">L'uso di TRIM su dischi Azure Premium o Standard non ha alcun impatto negativo.</span><span class="sxs-lookup"><span data-stu-id="d366b-232">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="d366b-233">Dimensioni dei nuovi dischi, gestiti e non gestiti</span><span class="sxs-lookup"><span data-stu-id="d366b-233">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="d366b-234">**Quali sono le dimensioni massime supportate per i dischi dati e del sistema operativo?**</span><span class="sxs-lookup"><span data-stu-id="d366b-234">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="d366b-235">Il tipo di partizione supportata da Azure per un disco del sistema operativo è MBR (Master Boot Record).</span><span class="sxs-lookup"><span data-stu-id="d366b-235">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="d366b-236">Il formato MBR supporta dischi di dimensioni fino a 2 TB.</span><span class="sxs-lookup"><span data-stu-id="d366b-236">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="d366b-237">Azure supporta dischi del sistema operativo di dimensioni massime pari a 2 TB.</span><span class="sxs-lookup"><span data-stu-id="d366b-237">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="d366b-238">Azure supporta fino a 4 TB per i dischi dati.</span><span class="sxs-lookup"><span data-stu-id="d366b-238">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="d366b-239">**Quali sono le dimensioni massime supportate per un BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="d366b-239">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="d366b-240">Le dimensioni massime supportate da Azure per un BLOB di pagine sono di 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="d366b-240">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="d366b-241">Non sono supportati BLOB di pagine di dimensioni superiori a 4 TB (4.095 GB) collegati a una VM come dischi dati o del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d366b-241">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="d366b-242">**È necessario usare una nuova versione degli strumenti di Azure per creare, collegare, ridimensionare e caricare dischi più grandi di 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="d366b-242">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="d366b-243">Non è necessario aggiornare gli strumenti di Azure esistenti per creare, collegare o ridimensionare i dischi di dimensioni superiori a 1 TB.</span><span class="sxs-lookup"><span data-stu-id="d366b-243">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="d366b-244">Per caricare il file VHD dall'ambiente locale direttamente in Azure come BLOB di pagine o disco non gestito, è necessario usare i set di strumenti più recenti:</span><span class="sxs-lookup"><span data-stu-id="d366b-244">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="d366b-245">Strumenti di Azure</span><span class="sxs-lookup"><span data-stu-id="d366b-245">Azure tools</span></span>      | <span data-ttu-id="d366b-246">Versioni supportate</span><span class="sxs-lookup"><span data-stu-id="d366b-246">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="d366b-247">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d366b-247">Azure PowerShell</span></span> | <span data-ttu-id="d366b-248">Numero di versione 4.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="d366b-248">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="d366b-249">Interfaccia della riga di comando di Azure v1</span><span class="sxs-lookup"><span data-stu-id="d366b-249">Azure CLI v1</span></span>     | <span data-ttu-id="d366b-250">Numero di versione 0.10.13: versione di maggio 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="d366b-250">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="d366b-251">AzCopy</span><span class="sxs-lookup"><span data-stu-id="d366b-251">AzCopy</span></span>           | <span data-ttu-id="d366b-252">Numero di versione 6.1.0: versione di giugno 2017 o successiva</span><span class="sxs-lookup"><span data-stu-id="d366b-252">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="d366b-253">Il supporto per l'interfaccia della riga di comando di Azure v2 e Azure Storage Explorer sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="d366b-253">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="d366b-254">**Le dimensioni del disco P4 e P6 sono supportate per i dischi gestiti o i BLOB di pagine?**</span><span class="sxs-lookup"><span data-stu-id="d366b-254">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="d366b-255">No.</span><span class="sxs-lookup"><span data-stu-id="d366b-255">No.</span></span> <span data-ttu-id="d366b-256">Le dimensioni del disco P4 (32 GB) e P6 (64 GB) sono supportate solo per i dischi gestiti.</span><span class="sxs-lookup"><span data-stu-id="d366b-256">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="d366b-257">Il supporto per dischi non gestiti e BLOB di pagine sarà disponibile a breve.</span><span class="sxs-lookup"><span data-stu-id="d366b-257">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="d366b-258">**Come viene fatturato un disco gestito Premium di dimensioni inferiori a 64 GB creato prima dell'abilitazione dei dischi più piccoli (intorno al 15 giugno 2017)?**</span><span class="sxs-lookup"><span data-stu-id="d366b-258">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="d366b-259">I dischi Premium esistenti di dimensioni inferiori a 64 GB continuano a essere fatturati in base al piano tariffario P10.</span><span class="sxs-lookup"><span data-stu-id="d366b-259">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="d366b-260">**Come è possibile modificare il piano tariffario dei dischi Premium di dimensioni inferiori a 64 GB da P10 a P4 o P6?**</span><span class="sxs-lookup"><span data-stu-id="d366b-260">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="d366b-261">È possibile creare uno snapshot dei dischi di piccole dimensioni e quindi creare un disco per passare automaticamente al piano tariffario a P4 o P6 in base alla dimensione del disco di cui viene effettuato il provisioning.</span><span class="sxs-lookup"><span data-stu-id="d366b-261">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="d366b-262">Cosa fare se non è disponibile una risposta alla domanda?</span><span class="sxs-lookup"><span data-stu-id="d366b-262">What if my question isn't answered here?</span></span>

<span data-ttu-id="d366b-263">Se la domanda non è elencata qui, invitiamo gli utenti a comunicarcela per consentirci di fornire il nostro aiuto.</span><span class="sxs-lookup"><span data-stu-id="d366b-263">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="d366b-264">È possibile pubblicare una domanda nei commenti alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d366b-264">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="d366b-265">Per interagire con il team di Archiviazione di Azure e altri membri della community in merito a questo articolo, usare il [forum MSDN di Archiviazione di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="d366b-265">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="d366b-266">Per richiedere funzionalità, inviare richieste e idee al [forum dei commenti su Archiviazione di Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="d366b-266">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
