---
title: infrastruttura aaaAzure convenzioni di denominazione - Linux | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la denominazione dei servizi di infrastruttura di Azure.
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
ms.openlocfilehash: 333146e7b2071e43527a5d7dc2ec02ebfb316eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-linux-vms"></a><span data-ttu-id="43194-103">Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure per macchine virtuali Linux</span><span class="sxs-lookup"><span data-stu-id="43194-103">Azure infrastructure naming guidelines for Linux VMs</span></span> 

[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-intro](../../../includes/virtual-machines-linux-infrastructure-guidelines-intro.md)]

<span data-ttu-id="43194-104">In questo articolo si incentra sulla comprensione di come impostare le convenzioni di denominazione tooapproach per tutti i toobuild risorse di Azure diversi logico e facilmente identificabile delle risorse nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="43194-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="43194-105">Linee guida di implementazione per le convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="43194-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="43194-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="43194-106">Decisions:</span></span>

* <span data-ttu-id="43194-107">Quali sono le convenzioni di denominazione per le risorse di Azure?</span><span class="sxs-lookup"><span data-stu-id="43194-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="43194-108">Attività:</span><span class="sxs-lookup"><span data-stu-id="43194-108">Tasks:</span></span>

* <span data-ttu-id="43194-109">Definire hello affissi toouse tra la coerenza toomaintain risorse.</span><span class="sxs-lookup"><span data-stu-id="43194-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="43194-110">Definire l'account di archiviazione sono stati specificati nomi hello requisito relativa toobe univoco globale.</span><span class="sxs-lookup"><span data-stu-id="43194-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="43194-111">Distribuire tooall parti coinvolte tooensure coerenza tra distribuzioni hello documento toobe convenzione di denominazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="43194-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="43194-112">Convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="43194-112">Naming conventions</span></span>
<span data-ttu-id="43194-113">Prima di creare qualsiasi elemento in Azure, è necessaria una buona convenzione di denominazione</span><span class="sxs-lookup"><span data-stu-id="43194-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="43194-114">Una convenzione di denominazione garantisce che tutte le risorse di hello abbiano un nome stimabile, che aiuta a basso carico amministrativo di hello associato alla gestione di tali risorse.</span><span class="sxs-lookup"><span data-stu-id="43194-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="43194-115">È possibile scegliere toofollow un set specifico di convenzioni di denominazione definite per l'intera organizzazione o per una specifica sottoscrizione di Azure o l'account.</span><span class="sxs-lookup"><span data-stu-id="43194-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="43194-116">Anche se è facile per utenti singoli all'interno delle regole di organizzazioni tooestablish implicita quando si utilizzano le risorse di Azure, è necessario tooscale in grado di toobe per i team collaborano in Azure.</span><span class="sxs-lookup"><span data-stu-id="43194-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, you need toobe able tooscale for teams working together in Azure.</span></span>

<span data-ttu-id="43194-117">Concordare in anticipo il set di convenzioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="43194-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="43194-118">Alcune considerazioni relative alle convenzioni di denominazione trascendono questi set di regole.</span><span class="sxs-lookup"><span data-stu-id="43194-118">There are some considerations regarding naming conventions that cut across that sets of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="43194-119">Affissi</span><span class="sxs-lookup"><span data-stu-id="43194-119">Affixes</span></span>
<span data-ttu-id="43194-120">Osservando toodefine una convenzione di denominazione, una decisione è se affisso hello in:</span><span class="sxs-lookup"><span data-stu-id="43194-120">As you look toodefine a naming convention, one decision is whether hello affix is at:</span></span>

* <span data-ttu-id="43194-121">inizio Hello del nome hello (prefisso)</span><span class="sxs-lookup"><span data-stu-id="43194-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="43194-122">fine di Hello del nome di hello (suffisso)</span><span class="sxs-lookup"><span data-stu-id="43194-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="43194-123">Ecco ad esempio, due nomi possibili per un gruppo di risorse utilizzando hello `rg` appone:</span><span class="sxs-lookup"><span data-stu-id="43194-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="43194-124">Rg-WebApp (prefisso)</span><span class="sxs-lookup"><span data-stu-id="43194-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="43194-125">WebApp-Rg (suffisso)</span><span class="sxs-lookup"><span data-stu-id="43194-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="43194-126">Affissi possono fare riferimento a aspetti toodifferent che descrivono le risorse particolare hello.</span><span class="sxs-lookup"><span data-stu-id="43194-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="43194-127">Hello nella tabella seguente vengono illustrati alcuni esempi utilizzati in genere.</span><span class="sxs-lookup"><span data-stu-id="43194-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="43194-128">Aspetto</span><span class="sxs-lookup"><span data-stu-id="43194-128">Aspect</span></span> | <span data-ttu-id="43194-129">esempi</span><span class="sxs-lookup"><span data-stu-id="43194-129">Examples</span></span> | <span data-ttu-id="43194-130">Note</span><span class="sxs-lookup"><span data-stu-id="43194-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="43194-131">Environment</span><span class="sxs-lookup"><span data-stu-id="43194-131">Environment</span></span> |<span data-ttu-id="43194-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="43194-132">dev, stg, prod</span></span> |<span data-ttu-id="43194-133">In base a scopo di hello e il nome di ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="43194-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="43194-134">Percorso</span><span class="sxs-lookup"><span data-stu-id="43194-134">Location</span></span> |<span data-ttu-id="43194-135">usw (Stati Uniti occidentali), use (Stati Uniti orientali 2)</span><span class="sxs-lookup"><span data-stu-id="43194-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="43194-136">A seconda area hello del Data Center hello o hello nell'area dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="43194-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="43194-137">Componente di Azure, servizio o prodotto</span><span class="sxs-lookup"><span data-stu-id="43194-137">Azure component, service, or product</span></span> |<span data-ttu-id="43194-138">Rg per gruppo di risorse, VNet per rete virtuale</span><span class="sxs-lookup"><span data-stu-id="43194-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="43194-139">A seconda del prodotto hello fornisce il supporto per i quali hello risorse.</span><span class="sxs-lookup"><span data-stu-id="43194-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="43194-140">Ruolo</span><span class="sxs-lookup"><span data-stu-id="43194-140">Role</span></span> |<span data-ttu-id="43194-141">db, app, web</span><span class="sxs-lookup"><span data-stu-id="43194-141">db, app, web</span></span> |<span data-ttu-id="43194-142">In base al ruolo hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="43194-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="43194-143">Istanza</span><span class="sxs-lookup"><span data-stu-id="43194-143">Instance</span></span> |<span data-ttu-id="43194-144">01, 02 e 03 e così via.</span><span class="sxs-lookup"><span data-stu-id="43194-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="43194-145">Per le risorse con più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="43194-145">For resources that have more than one instance.</span></span> <span data-ttu-id="43194-146">Ad esempio, i server Web con carico bilanciato in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="43194-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="43194-147">Quando si stabiliscono le convenzioni di denominazione, assicurarsi che è chiaramente indicato che appone toouse per ogni tipo di risorsa e in quale posizione (suffisso vs prefisso).</span><span class="sxs-lookup"><span data-stu-id="43194-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="43194-148">Date</span><span class="sxs-lookup"><span data-stu-id="43194-148">Dates</span></span>
<span data-ttu-id="43194-149">È spesso data hello toodetermine importante della creazione dal nome hello di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="43194-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="43194-150">Si consiglia di formato di data hello aaaammgg.</span><span class="sxs-lookup"><span data-stu-id="43194-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="43194-151">Questo formato garantisce che non solo è hello completo data verrà registrata, ma anche che due risorse i cui nomi si differenziano solo per data hello vengono ordinati in ordine alfabetico e in ordine cronologico.</span><span class="sxs-lookup"><span data-stu-id="43194-151">This format ensures that not only is hello full date is recorded, but also that two resources whose names differ only on hello date are sorted alphabetically and chronologically.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="43194-152">Nomi delle risorse</span><span class="sxs-lookup"><span data-stu-id="43194-152">Naming resources</span></span>
<span data-ttu-id="43194-153">Definire ogni tipo di risorsa nella convenzione di denominazione hello, che dovrebbero essere presenti regole che definiscono come tooassign nomi tooeach risorsa che viene creato.</span><span class="sxs-lookup"><span data-stu-id="43194-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="43194-154">Queste regole, applicare tooall tipi di risorse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="43194-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="43194-155">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="43194-155">Subscriptions</span></span>
* <span data-ttu-id="43194-156">Account</span><span class="sxs-lookup"><span data-stu-id="43194-156">Accounts</span></span>
* <span data-ttu-id="43194-157">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="43194-157">Storage accounts</span></span>
* <span data-ttu-id="43194-158">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="43194-158">Virtual networks</span></span>
* <span data-ttu-id="43194-159">Subnet</span><span class="sxs-lookup"><span data-stu-id="43194-159">Subnets</span></span>
* <span data-ttu-id="43194-160">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="43194-160">Availability sets</span></span>
* <span data-ttu-id="43194-161">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="43194-161">Resource groups</span></span>
* <span data-ttu-id="43194-162">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="43194-162">Virtual machines</span></span>
* <span data-ttu-id="43194-163">Endpoint</span><span class="sxs-lookup"><span data-stu-id="43194-163">Endpoints</span></span>
* <span data-ttu-id="43194-164">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="43194-164">Network security groups</span></span>
* <span data-ttu-id="43194-165">Ruoli</span><span class="sxs-lookup"><span data-stu-id="43194-165">Roles</span></span>

<span data-ttu-id="43194-166">tooensure che hello nome fornisce risorse di toowhich toodetermine sufficienti informazioni che fa riferimento, è necessario utilizzare nomi descrittivi.</span><span class="sxs-lookup"><span data-stu-id="43194-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="43194-167">Nomi dei computer</span><span class="sxs-lookup"><span data-stu-id="43194-167">Computer names</span></span>
<span data-ttu-id="43194-168">Quando si crea una macchina virtuale (VM), Azure richiede un nome della macchina virtuale di backup too64 caratteri che viene utilizzato per il nome di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="43194-168">When you create a virtual machine (VM), Azure requires a VM name of up too64 characters that is used for hello resource name.</span></span> <span data-ttu-id="43194-169">Azure Usa hello stesso nome del sistema operativo hello installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="43194-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="43194-170">Tuttavia, questi nomi potrebbero non sempre essere hello stesso.</span><span class="sxs-lookup"><span data-stu-id="43194-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="43194-171">Se una macchina virtuale viene creata da un file di immagine con estensione vhd che contiene già un sistema operativo, nome della macchina virtuale hello in Azure può differire da hello Nome computer del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="43194-171">If a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="43194-172">Questa situazione è possibile aggiungere un livello di gestione di tooVM difficoltà, che pertanto non è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="43194-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="43194-173">Assegnare hello hello risorsa macchina virtuale di Azure stesso nome come nome di computer hello assegnare toohello di sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="43194-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="43194-174">Si consiglia di tale nome di macchina virtuale di Azure hello è hello come hello Nome computer del sistema operativo sottostante.</span><span class="sxs-lookup"><span data-stu-id="43194-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="43194-175">Nomi account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="43194-175">Storage account names</span></span>
<span data-ttu-id="43194-176">In questa sezione non si applica troppo[dischi gestiti di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), come si crea un account di archiviazione separata.</span><span class="sxs-lookup"><span data-stu-id="43194-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="43194-177">Per i dischi non gestiti, gli account di archiviazione hanno regole speciali che ne controllano i nomi.</span><span class="sxs-lookup"><span data-stu-id="43194-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="43194-178">È possibile usare solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="43194-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="43194-179">Per altre informazioni, vedere [Creare un account di archiviazione](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="43194-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="43194-180">Inoltre, nome account di archiviazione hello, con core.windows.net, deve essere un nome DNS univoco globale valido.</span><span class="sxs-lookup"><span data-stu-id="43194-180">Additionally, hello storage account name, with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="43194-181">Ad esempio, se l'account di archiviazione hello viene chiamato mystorageaccount, hello seguenti nomi DNS risultanti devono essere univoci:</span><span class="sxs-lookup"><span data-stu-id="43194-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="43194-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="43194-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="43194-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="43194-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="43194-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="43194-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="43194-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43194-185">Next steps</span></span>
[!INCLUDE [virtual-machines-linux-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-linux-infrastructure-guidelines-next-steps.md)]

