---
title: 'Linee guida per la denominazione dell''infrastruttura di Azure: Windows | Microsoft Docs'
description: Informazioni sulle principali linee guida di progettazione e implementazione per la denominazione nei servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 660765fa-4d42-49cb-a9c6-8c596d26d221
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a595d5c2f0316b5214af7b8939f1af8da187ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="91eaf-103">Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="91eaf-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="91eaf-104">Questo articolo è incentrato sulla comprensione dell'approccio alle convenzioni di denominazione delle varie risorse di Azure per la creazione di un set di risorse logico e facilmente identificabile all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="91eaf-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="91eaf-105">Linee guida di implementazione per le convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="91eaf-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="91eaf-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="91eaf-106">Decisions:</span></span>

* <span data-ttu-id="91eaf-107">Quali sono le convenzioni di denominazione per le risorse di Azure?</span><span class="sxs-lookup"><span data-stu-id="91eaf-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="91eaf-108">Attività:</span><span class="sxs-lookup"><span data-stu-id="91eaf-108">Tasks:</span></span>

* <span data-ttu-id="91eaf-109">Definire gli affissi da usare per mantenere la coerenza delle risorse.</span><span class="sxs-lookup"><span data-stu-id="91eaf-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="91eaf-110">Definire i nomi degli account di archiviazione, rispettando il requisito dell'univocità globale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="91eaf-111">Documentare la convenzione di denominazione che sarà usata e distribuire il documento a tutte le parti interessate per garantire la coerenza tra le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="91eaf-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="91eaf-112">Convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="91eaf-112">Naming conventions</span></span>
<span data-ttu-id="91eaf-113">Prima di creare qualsiasi elemento in Azure, è necessaria una buona convenzione di denominazione</span><span class="sxs-lookup"><span data-stu-id="91eaf-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="91eaf-114">Una convenzione di denominazione garantisce la possibilità che tutte le risorse dispongano di un nome stimabile, in modo da ridurre il carico amministrativo associato alla gestione di tali risorse.</span><span class="sxs-lookup"><span data-stu-id="91eaf-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="91eaf-115">È possibile scegliere di seguire un set specifico di convenzioni di denominazione definite per l'intera organizzazione oppure per un account o una sottoscrizione di Azure specifica.</span><span class="sxs-lookup"><span data-stu-id="91eaf-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="91eaf-116">Sebbene sia facile per i singoli utenti all'interno delle organizzazioni stabilire le regole implicite quando si usano risorse di Azure, quando un team deve lavorare a un progetto in Azure, la scalabilità di tale modello non è ottimale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, when a team needs to work on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="91eaf-117">Concordare in anticipo il set di convenzioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="91eaf-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="91eaf-118">Alcune considerazioni relative alle convenzioni di denominazione trascendono questi set di regole.</span><span class="sxs-lookup"><span data-stu-id="91eaf-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="91eaf-119">Affissi</span><span class="sxs-lookup"><span data-stu-id="91eaf-119">Affixes</span></span>
<span data-ttu-id="91eaf-120">Quando si definisce una convenzione di denominazione, una decisione riguarda la posizione dell'affisso:</span><span class="sxs-lookup"><span data-stu-id="91eaf-120">As you look to define a naming convention, one decision comes whether the affix is at:</span></span>

* <span data-ttu-id="91eaf-121">Inizio del nome (prefisso)</span><span class="sxs-lookup"><span data-stu-id="91eaf-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="91eaf-122">Fine del nome (suffisso)</span><span class="sxs-lookup"><span data-stu-id="91eaf-122">The end of the name (suffix)</span></span>

<span data-ttu-id="91eaf-123">Ad esempio, di seguito sono indicati due possibili nomi di un gruppo di risorse nei quali viene usato l'affisso `rg` :</span><span class="sxs-lookup"><span data-stu-id="91eaf-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="91eaf-124">Rg-WebApp (prefisso)</span><span class="sxs-lookup"><span data-stu-id="91eaf-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="91eaf-125">WebApp-Rg (suffisso)</span><span class="sxs-lookup"><span data-stu-id="91eaf-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="91eaf-126">Gli affissi possono fare riferimento ai diversi aspetti che descrivono le specifiche risorse.</span><span class="sxs-lookup"><span data-stu-id="91eaf-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="91eaf-127">La tabella seguente illustra alcuni esempi usati comunemente.</span><span class="sxs-lookup"><span data-stu-id="91eaf-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="91eaf-128">Aspetto</span><span class="sxs-lookup"><span data-stu-id="91eaf-128">Aspect</span></span> | <span data-ttu-id="91eaf-129">esempi</span><span class="sxs-lookup"><span data-stu-id="91eaf-129">Examples</span></span> | <span data-ttu-id="91eaf-130">Note</span><span class="sxs-lookup"><span data-stu-id="91eaf-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="91eaf-131">Environment</span><span class="sxs-lookup"><span data-stu-id="91eaf-131">Environment</span></span> |<span data-ttu-id="91eaf-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="91eaf-132">dev, stg, prod</span></span> |<span data-ttu-id="91eaf-133">A seconda dello scopo e del nome di ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="91eaf-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="91eaf-134">Percorso</span><span class="sxs-lookup"><span data-stu-id="91eaf-134">Location</span></span> |<span data-ttu-id="91eaf-135">usw (Stati Uniti occidentali), use (Stati Uniti orientali 2)</span><span class="sxs-lookup"><span data-stu-id="91eaf-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="91eaf-136">A seconda dell'area del data center o dell’area dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="91eaf-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="91eaf-137">Componente di Azure, servizio o prodotto</span><span class="sxs-lookup"><span data-stu-id="91eaf-137">Azure component, service, or product</span></span> |<span data-ttu-id="91eaf-138">Rg per gruppo di risorse, VNet per rete virtuale</span><span class="sxs-lookup"><span data-stu-id="91eaf-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="91eaf-139">A seconda del prodotto per il quale la risorsa fornisce il supporto.</span><span class="sxs-lookup"><span data-stu-id="91eaf-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="91eaf-140">Ruolo</span><span class="sxs-lookup"><span data-stu-id="91eaf-140">Role</span></span> |<span data-ttu-id="91eaf-141">sql, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="91eaf-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="91eaf-142">A seconda del ruolo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="91eaf-143">Istanza</span><span class="sxs-lookup"><span data-stu-id="91eaf-143">Instance</span></span> |<span data-ttu-id="91eaf-144">01, 02 e 03 e così via.</span><span class="sxs-lookup"><span data-stu-id="91eaf-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="91eaf-145">Per le risorse con più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="91eaf-145">For resources that have more than one instance.</span></span> <span data-ttu-id="91eaf-146">Ad esempio, i server Web con carico bilanciato in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="91eaf-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="91eaf-147">Quando si stabiliscono le convenzioni di denominazione, assicurarsi che siano indicati chiaramente quali affissi usare per ogni tipo di risorsa, e in quale posizione (prefisso o suffisso).</span><span class="sxs-lookup"><span data-stu-id="91eaf-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="91eaf-148">Date</span><span class="sxs-lookup"><span data-stu-id="91eaf-148">Dates</span></span>
<span data-ttu-id="91eaf-149">Molte volte è importante determinare la data di creazione dal nome di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="91eaf-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="91eaf-150">È consigliabile usare il formato di data AAAAMMGG.</span><span class="sxs-lookup"><span data-stu-id="91eaf-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="91eaf-151">Tale formato garantisce non solo che venga registrata la data completa, ma anche che due risorse i cui nomi si differenziano solo per la data verranno ordinate alfabeticamente e allo stesso tempo in ordine cronologico.</span><span class="sxs-lookup"><span data-stu-id="91eaf-151">This format ensures that not only the full date is recorded, but also that two resources whose names differ only on the date is sorted alphabetically and chronologically at the same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="91eaf-152">Nomi delle risorse</span><span class="sxs-lookup"><span data-stu-id="91eaf-152">Naming resources</span></span>
<span data-ttu-id="91eaf-153">Definire ogni tipo di risorsa nella convenzione di denominazione, quindi è necessario avere regole che definiscono come assegnare nomi a ogni risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="91eaf-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="91eaf-154">Tali regole devono essere applicate a tutti i tipi di risorse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="91eaf-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="91eaf-155">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="91eaf-155">Subscriptions</span></span>
* <span data-ttu-id="91eaf-156">Account</span><span class="sxs-lookup"><span data-stu-id="91eaf-156">Accounts</span></span>
* <span data-ttu-id="91eaf-157">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="91eaf-157">Storage accounts</span></span>
* <span data-ttu-id="91eaf-158">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="91eaf-158">Virtual networks</span></span>
* <span data-ttu-id="91eaf-159">Subnet</span><span class="sxs-lookup"><span data-stu-id="91eaf-159">Subnets</span></span>
* <span data-ttu-id="91eaf-160">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="91eaf-160">Availability sets</span></span>
* <span data-ttu-id="91eaf-161">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="91eaf-161">Resource groups</span></span>
* <span data-ttu-id="91eaf-162">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="91eaf-162">Virtual machines</span></span>
* <span data-ttu-id="91eaf-163">Endpoint</span><span class="sxs-lookup"><span data-stu-id="91eaf-163">Endpoints</span></span>
* <span data-ttu-id="91eaf-164">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="91eaf-164">Network security groups</span></span>
* <span data-ttu-id="91eaf-165">Ruoli</span><span class="sxs-lookup"><span data-stu-id="91eaf-165">Roles</span></span>

<span data-ttu-id="91eaf-166">Per assicurarsi che il nome fornisca informazioni sufficienti per determinare a quali risorse fa riferimento, è necessario inserire nomi descrittivi.</span><span class="sxs-lookup"><span data-stu-id="91eaf-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="91eaf-167">Nomi dei computer</span><span class="sxs-lookup"><span data-stu-id="91eaf-167">Computer names</span></span>
<span data-ttu-id="91eaf-168">Quando si crea una macchina virtuale, Microsoft Azure richiede un nome di macchina virtuali con un massimo 15 caratteri che viene usato per il nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="91eaf-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up to 15 characters which is used for the resource name.</span></span> <span data-ttu-id="91eaf-169">Azure usa lo stesso nome per il sistema operativo installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="91eaf-170">È possibile tuttavia che questi nomi non siano sempre gli stessi.</span><span class="sxs-lookup"><span data-stu-id="91eaf-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="91eaf-171">Nel caso in cui viene creata una macchina virtuale da un file immagine con estensione vhd che già contiene un sistema operativo, il nome della macchina virtuale in Azure può essere diverso dal nome computer del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-171">In case a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="91eaf-172">Questa situazione può aggiungere un livello di difficoltà alla gestione delle macchine virtuali, quindi è sconsigliata.</span><span class="sxs-lookup"><span data-stu-id="91eaf-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="91eaf-173">Assicurarsi sempre che il nome della risorsa macchina virtuale di Azure sia lo stesso nome del computer assegnato al sistema operativo di tale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="91eaf-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="91eaf-174">È consigliabile che il nome della VM di Azure e del computer del sistema operativo sottostante coincidano.</span><span class="sxs-lookup"><span data-stu-id="91eaf-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="91eaf-175">Nomi account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="91eaf-175">Storage account names</span></span>
<span data-ttu-id="91eaf-176">Questa sezione non si applica a [Managed Disks di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), in quanto non si crea un account di archiviazione separato.</span><span class="sxs-lookup"><span data-stu-id="91eaf-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="91eaf-177">Per i dischi non gestiti, gli account di archiviazione hanno regole speciali che ne controllano i nomi.</span><span class="sxs-lookup"><span data-stu-id="91eaf-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="91eaf-178">È possibile usare solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="91eaf-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="91eaf-179">Per altre informazioni, vedere [Creare un account di archiviazione](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="91eaf-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="91eaf-180">Inoltre, il nome dell'account di archiviazione, insieme a core.windows.net, deve essere un nome DNS a livello globale valido e univoco.</span><span class="sxs-lookup"><span data-stu-id="91eaf-180">Additionally, the storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="91eaf-181">Ad esempio, se il nome dell'account di archiviazione è mystorageaccount, i seguenti nomi DNS risultanti devono essere univoci:</span><span class="sxs-lookup"><span data-stu-id="91eaf-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="91eaf-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="91eaf-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="91eaf-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="91eaf-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="91eaf-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="91eaf-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="91eaf-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="91eaf-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

