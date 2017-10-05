---
title: Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure - Linux | Microsoft Docs
description: Informazioni sulle principali linee guida di progettazione e implementazione per la denominazione nei servizi di infrastruttura di Azure.
documentationcenter: 
services: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 18ee4fb1-8297-49a1-8d3f-097880be67c7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1b086f0972c02d569a7219820a3d596960b6014b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="45707-103">Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="45707-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="45707-104">Questo articolo è incentrato sulla comprensione dell'approccio alle convenzioni di denominazione delle varie risorse di Azure per la creazione di un set di risorse logico e facilmente identificabile all'interno dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="45707-104">This article focuses on understanding how to approach naming conventions for all your various Azure resources to build a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="45707-105">Linee guida di implementazione per le convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="45707-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="45707-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="45707-106">Decisions:</span></span>

* <span data-ttu-id="45707-107">Quali sono le convenzioni di denominazione per le risorse di Azure?</span><span class="sxs-lookup"><span data-stu-id="45707-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="45707-108">Attività:</span><span class="sxs-lookup"><span data-stu-id="45707-108">Tasks:</span></span>

* <span data-ttu-id="45707-109">Definire gli affissi da usare per mantenere la coerenza delle risorse.</span><span class="sxs-lookup"><span data-stu-id="45707-109">Define the affixes to use across your resources to maintain consistency.</span></span>
* <span data-ttu-id="45707-110">Definire i nomi degli account di archiviazione, rispettando il requisito dell'univocità globale.</span><span class="sxs-lookup"><span data-stu-id="45707-110">Define storage account names given the requirement for them to be globally unique.</span></span>
* <span data-ttu-id="45707-111">Documentare la convenzione di denominazione che sarà usata e distribuire il documento a tutte le parti interessate per garantire la coerenza tra le distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="45707-111">Document the naming convention to be used and distribute to all parties involved to ensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="45707-112">Convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="45707-112">Naming conventions</span></span>
<span data-ttu-id="45707-113">Prima di creare qualsiasi elemento in Azure, è necessaria una buona convenzione di denominazione</span><span class="sxs-lookup"><span data-stu-id="45707-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="45707-114">Una convenzione di denominazione garantisce la possibilità che tutte le risorse dispongano di un nome stimabile, in modo da ridurre il carico amministrativo associato alla gestione di tali risorse.</span><span class="sxs-lookup"><span data-stu-id="45707-114">A naming convention ensures that all the resources have a predictable name, which helps lower the administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="45707-115">È possibile scegliere di seguire un set specifico di convenzioni di denominazione definite per l'intera organizzazione oppure per un account o una sottoscrizione di Azure specifica.</span><span class="sxs-lookup"><span data-stu-id="45707-115">You might choose to follow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="45707-116">Sebbene sia facile per i singoli utenti all'interno delle organizzazioni stabilire le regole implicite quando si usano risorse di Azure, per i team che usano Azure collettivamente è necessaria una certa scalabilità.</span><span class="sxs-lookup"><span data-stu-id="45707-116">Although it is easy for individuals within organizations to establish implicit rules when working with Azure resources, you need to be able to scale for teams working together in Azure.</span></span>

<span data-ttu-id="45707-117">Concordare in anticipo il set di convenzioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="45707-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="45707-118">Alcune considerazioni relative alle convenzioni di denominazione trascendono questi set di regole.</span><span class="sxs-lookup"><span data-stu-id="45707-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="45707-119">Affissi</span><span class="sxs-lookup"><span data-stu-id="45707-119">Affixes</span></span>
<span data-ttu-id="45707-120">Quando si definisce una convenzione di denominazione, occorre stabilire la posizione dell'affisso:</span><span class="sxs-lookup"><span data-stu-id="45707-120">As you look to define a naming convention, one decision is whether the affix is at:</span></span>

* <span data-ttu-id="45707-121">Inizio del nome (prefisso)</span><span class="sxs-lookup"><span data-stu-id="45707-121">The beginning of the name (prefix)</span></span>
* <span data-ttu-id="45707-122">Fine del nome (suffisso)</span><span class="sxs-lookup"><span data-stu-id="45707-122">The end of the name (suffix)</span></span>

<span data-ttu-id="45707-123">Ad esempio, di seguito sono indicati due possibili nomi di un gruppo di risorse nei quali viene usato l'affisso `rg` :</span><span class="sxs-lookup"><span data-stu-id="45707-123">For instance, here are two possible names for a Resource Group using the `rg` affix:</span></span>

* <span data-ttu-id="45707-124">Rg-WebApp (prefisso)</span><span class="sxs-lookup"><span data-stu-id="45707-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="45707-125">WebApp-Rg (suffisso)</span><span class="sxs-lookup"><span data-stu-id="45707-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="45707-126">Gli affissi possono fare riferimento ai diversi aspetti che descrivono le specifiche risorse.</span><span class="sxs-lookup"><span data-stu-id="45707-126">Affixes can refer to different aspects that describe the particular resources.</span></span> <span data-ttu-id="45707-127">La tabella seguente illustra alcuni esempi usati comunemente.</span><span class="sxs-lookup"><span data-stu-id="45707-127">The following table shows some examples typically used.</span></span>

| <span data-ttu-id="45707-128">Aspetto</span><span class="sxs-lookup"><span data-stu-id="45707-128">Aspect</span></span> | <span data-ttu-id="45707-129">esempi</span><span class="sxs-lookup"><span data-stu-id="45707-129">Examples</span></span> | <span data-ttu-id="45707-130">Note</span><span class="sxs-lookup"><span data-stu-id="45707-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="45707-131">Environment</span><span class="sxs-lookup"><span data-stu-id="45707-131">Environment</span></span> |<span data-ttu-id="45707-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="45707-132">dev, stg, prod</span></span> |<span data-ttu-id="45707-133">A seconda dello scopo e del nome di ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="45707-133">Depending on the purpose and name of each environment.</span></span> |
| <span data-ttu-id="45707-134">Percorso</span><span class="sxs-lookup"><span data-stu-id="45707-134">Location</span></span> |<span data-ttu-id="45707-135">usw (Stati Uniti occidentali), use (Stati Uniti orientali 2)</span><span class="sxs-lookup"><span data-stu-id="45707-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="45707-136">A seconda dell'area del data center o dell’area dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="45707-136">Depending on the region of the datacenter or the region of the organization.</span></span> |
| <span data-ttu-id="45707-137">Componente di Azure, servizio o prodotto</span><span class="sxs-lookup"><span data-stu-id="45707-137">Azure component, service, or product</span></span> |<span data-ttu-id="45707-138">Rg per gruppo di risorse, VNet per rete virtuale</span><span class="sxs-lookup"><span data-stu-id="45707-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="45707-139">A seconda del prodotto per il quale la risorsa fornisce il supporto.</span><span class="sxs-lookup"><span data-stu-id="45707-139">Depending on the product for which the resource provides support.</span></span> |
| <span data-ttu-id="45707-140">Ruolo</span><span class="sxs-lookup"><span data-stu-id="45707-140">Role</span></span> |<span data-ttu-id="45707-141">db, app, web</span><span class="sxs-lookup"><span data-stu-id="45707-141">db, app, web</span></span> |<span data-ttu-id="45707-142">A seconda del ruolo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45707-142">Depending on the role of the virtual machine.</span></span> |
| <span data-ttu-id="45707-143">Istanza</span><span class="sxs-lookup"><span data-stu-id="45707-143">Instance</span></span> |<span data-ttu-id="45707-144">01, 02 e 03 e così via.</span><span class="sxs-lookup"><span data-stu-id="45707-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="45707-145">Per le risorse con più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="45707-145">For resources that have more than one instance.</span></span> <span data-ttu-id="45707-146">Ad esempio, i server Web con carico bilanciato in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="45707-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="45707-147">Quando si stabiliscono le convenzioni di denominazione, assicurarsi che siano indicati chiaramente quali affissi usare per ogni tipo di risorsa, e in quale posizione (prefisso o suffisso).</span><span class="sxs-lookup"><span data-stu-id="45707-147">When establishing your naming conventions, make sure that they clearly state which affixes to use for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="45707-148">Date</span><span class="sxs-lookup"><span data-stu-id="45707-148">Dates</span></span>
<span data-ttu-id="45707-149">Molte volte è importante determinare la data di creazione dal nome di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="45707-149">It is often important to determine the date of creation from the name of a resource.</span></span> <span data-ttu-id="45707-150">È consigliabile usare il formato di data AAAAMMGG.</span><span class="sxs-lookup"><span data-stu-id="45707-150">We recommend the YYYYMMDD date format.</span></span> <span data-ttu-id="45707-151">Tale formato garantisce non solo che venga registrata la data completa, ma anche che due risorse i cui nomi si differenziano solo per la data vengano disposte in ordine alfabetico e cronologico.</span><span class="sxs-lookup"><span data-stu-id="45707-151">This format ensures that not only is the full date is recorded, but also that two resources whose names differ only on the date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="45707-152">Nomi delle risorse</span><span class="sxs-lookup"><span data-stu-id="45707-152">Naming resources</span></span>
<span data-ttu-id="45707-153">Definire ogni tipo di risorsa nella convenzione di denominazione, quindi è necessario avere regole che definiscono come assegnare nomi a ogni risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="45707-153">Define each type of resource in the naming convention, which should have rules that define how to assign names to each resource that is created.</span></span> <span data-ttu-id="45707-154">Tali regole devono essere applicate a tutti i tipi di risorse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="45707-154">These rules should apply to all types of resources, for example:</span></span>

* <span data-ttu-id="45707-155">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="45707-155">Subscriptions</span></span>
* <span data-ttu-id="45707-156">Account</span><span class="sxs-lookup"><span data-stu-id="45707-156">Accounts</span></span>
* <span data-ttu-id="45707-157">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="45707-157">Storage accounts</span></span>
* <span data-ttu-id="45707-158">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="45707-158">Virtual networks</span></span>
* <span data-ttu-id="45707-159">Subnet</span><span class="sxs-lookup"><span data-stu-id="45707-159">Subnets</span></span>
* <span data-ttu-id="45707-160">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="45707-160">Availability sets</span></span>
* <span data-ttu-id="45707-161">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="45707-161">Resource groups</span></span>
* <span data-ttu-id="45707-162">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="45707-162">Virtual machines</span></span>
* <span data-ttu-id="45707-163">Endpoint</span><span class="sxs-lookup"><span data-stu-id="45707-163">Endpoints</span></span>
* <span data-ttu-id="45707-164">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="45707-164">Network security groups</span></span>
* <span data-ttu-id="45707-165">Ruoli</span><span class="sxs-lookup"><span data-stu-id="45707-165">Roles</span></span>

<span data-ttu-id="45707-166">Per assicurarsi che il nome fornisca informazioni sufficienti per determinare a quali risorse fa riferimento, è necessario inserire nomi descrittivi.</span><span class="sxs-lookup"><span data-stu-id="45707-166">To ensure that the name provides enough information to determine to which resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="45707-167">Nomi dei computer</span><span class="sxs-lookup"><span data-stu-id="45707-167">Computer names</span></span>
<span data-ttu-id="45707-168">Quando si crea una macchina virtuale (VM), Azure richiede un nome di VM con un massimo di 64 caratteri da usare come nome della risorsa.</span><span class="sxs-lookup"><span data-stu-id="45707-168">When you create a virtual machine (VM), Azure requires a VM name of up to 64 characters that is used for the resource name.</span></span> <span data-ttu-id="45707-169">Azure usa lo stesso nome per il sistema operativo installato nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45707-169">Azure uses the same name for the operating system installed in the VM.</span></span> <span data-ttu-id="45707-170">È possibile tuttavia che questi nomi non siano sempre gli stessi.</span><span class="sxs-lookup"><span data-stu-id="45707-170">However, these names might not always be the same.</span></span>

<span data-ttu-id="45707-171">Se si crea una VM da un file immagine con estensione .vhd che contiene già un sistema operativo, il nome della VM in Azure può essere diverso dal nome del computer del sistema operativo della VM.</span><span class="sxs-lookup"><span data-stu-id="45707-171">If a VM is created from a .vhd image file that already contains an operating system, the VM name in Azure can differ from the VM's operating system computer name.</span></span> <span data-ttu-id="45707-172">Questa situazione può aggiungere un livello di difficoltà alla gestione delle macchine virtuali, quindi è sconsigliata.</span><span class="sxs-lookup"><span data-stu-id="45707-172">This situation can add a degree of difficulty to VM management, which we therefore do not recommend.</span></span> <span data-ttu-id="45707-173">Assicurarsi sempre che il nome della risorsa macchina virtuale di Azure sia lo stesso nome del computer assegnato al sistema operativo di tale macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="45707-173">Assign the Azure VM resource the same name as the computer name that you assign to the operating system of that VM.</span></span>

<span data-ttu-id="45707-174">È consigliabile che il nome della VM di Azure e del computer del sistema operativo sottostante coincidano.</span><span class="sxs-lookup"><span data-stu-id="45707-174">We recommend that the Azure VM name is the same as the underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="45707-175">Nomi account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="45707-175">Storage account names</span></span>
<span data-ttu-id="45707-176">Questa sezione non si applica a [Managed Disks di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), in quanto non si crea un account di archiviazione separato.</span><span class="sxs-lookup"><span data-stu-id="45707-176">This section does not apply to [Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="45707-177">Per i dischi non gestiti, gli account di archiviazione hanno regole speciali che ne controllano i nomi.</span><span class="sxs-lookup"><span data-stu-id="45707-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="45707-178">È possibile usare solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="45707-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="45707-179">Per altre informazioni, vedere [Creare un account di archiviazione](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="45707-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="45707-180">Inoltre, il nome dell'account di archiviazione, con core.windows.net, deve essere un nome DNS a livello globale valido e univoco.</span><span class="sxs-lookup"><span data-stu-id="45707-180">Additionally, the storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="45707-181">Ad esempio, se il nome dell'account di archiviazione è mystorageaccount, i seguenti nomi DNS risultanti devono essere univoci:</span><span class="sxs-lookup"><span data-stu-id="45707-181">For instance, if the storage account is called mystorageaccount, the following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="45707-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="45707-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="45707-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="45707-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="45707-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="45707-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="45707-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45707-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

