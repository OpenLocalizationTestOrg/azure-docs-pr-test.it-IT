---
title: infrastruttura aaaAzure convenzioni di denominazione - Windows | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per la denominazione dei servizi di infrastruttura di Azure.
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
ms.openlocfilehash: 9b4a16ce99cf1cac5804c77675e24590ac2e2b33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-infrastructure-naming-guidelines-for-windows-vms"></a><span data-ttu-id="2e587-103">Linee guida sulle convenzioni di denominazione dell'infrastruttura di Azure per macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="2e587-103">Azure infrastructure naming guidelines for Windows VMs</span></span>

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

<span data-ttu-id="2e587-104">In questo articolo si incentra sulla comprensione di come impostare le convenzioni di denominazione tooapproach per tutti i toobuild risorse di Azure diversi logico e facilmente identificabile delle risorse nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="2e587-104">This article focuses on understanding how tooapproach naming conventions for all your various Azure resources toobuild a logical and easily identifiable set of resources across your environment.</span></span>

## <a name="implementation-guidelines-for-naming-conventions"></a><span data-ttu-id="2e587-105">Linee guida di implementazione per le convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="2e587-105">Implementation guidelines for naming conventions</span></span>
<span data-ttu-id="2e587-106">Decisioni:</span><span class="sxs-lookup"><span data-stu-id="2e587-106">Decisions:</span></span>

* <span data-ttu-id="2e587-107">Quali sono le convenzioni di denominazione per le risorse di Azure?</span><span class="sxs-lookup"><span data-stu-id="2e587-107">What are your naming conventions for Azure resources?</span></span>

<span data-ttu-id="2e587-108">Attività:</span><span class="sxs-lookup"><span data-stu-id="2e587-108">Tasks:</span></span>

* <span data-ttu-id="2e587-109">Definire hello affissi toouse tra la coerenza toomaintain risorse.</span><span class="sxs-lookup"><span data-stu-id="2e587-109">Define hello affixes toouse across your resources toomaintain consistency.</span></span>
* <span data-ttu-id="2e587-110">Definire l'account di archiviazione sono stati specificati nomi hello requisito relativa toobe univoco globale.</span><span class="sxs-lookup"><span data-stu-id="2e587-110">Define storage account names given hello requirement for them toobe globally unique.</span></span>
* <span data-ttu-id="2e587-111">Distribuire tooall parti coinvolte tooensure coerenza tra distribuzioni hello documento toobe convenzione di denominazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="2e587-111">Document hello naming convention toobe used and distribute tooall parties involved tooensure consistency across deployments.</span></span>

## <a name="naming-conventions"></a><span data-ttu-id="2e587-112">Convenzioni di denominazione</span><span class="sxs-lookup"><span data-stu-id="2e587-112">Naming conventions</span></span>
<span data-ttu-id="2e587-113">Prima di creare qualsiasi elemento in Azure, è necessaria una buona convenzione di denominazione</span><span class="sxs-lookup"><span data-stu-id="2e587-113">You should have a good naming convention in place before creating anything in Azure.</span></span> <span data-ttu-id="2e587-114">Una convenzione di denominazione garantisce che tutte le risorse di hello abbiano un nome stimabile, che aiuta a basso carico amministrativo di hello associato alla gestione di tali risorse.</span><span class="sxs-lookup"><span data-stu-id="2e587-114">A naming convention ensures that all hello resources have a predictable name, which helps lower hello administrative burden associated with managing those resources.</span></span>

<span data-ttu-id="2e587-115">È possibile scegliere toofollow un set specifico di convenzioni di denominazione definite per l'intera organizzazione o per una specifica sottoscrizione di Azure o l'account.</span><span class="sxs-lookup"><span data-stu-id="2e587-115">You might choose toofollow a specific set of naming conventions defined for your entire organization or for a specific Azure subscription or account.</span></span> <span data-ttu-id="2e587-116">Anche se è facile per utenti singoli all'interno delle regole di organizzazioni tooestablish implicita quando si utilizzano le risorse di Azure, quando un team deve toowork su un progetto in Azure, tale modello non è facilmente scalabile.</span><span class="sxs-lookup"><span data-stu-id="2e587-116">Although it is easy for individuals within organizations tooestablish implicit rules when working with Azure resources, when a team needs toowork on a project on Azure, that model does not scale well.</span></span>

<span data-ttu-id="2e587-117">Concordare in anticipo il set di convenzioni di denominazione.</span><span class="sxs-lookup"><span data-stu-id="2e587-117">Agree on a set of naming conventions up front.</span></span> <span data-ttu-id="2e587-118">Alcune considerazioni relative alle convenzioni di denominazione trascendono questi set di regole.</span><span class="sxs-lookup"><span data-stu-id="2e587-118">There are some considerations regarding naming conventions that cut across this set of rules.</span></span>

## <a name="affixes"></a><span data-ttu-id="2e587-119">Affissi</span><span class="sxs-lookup"><span data-stu-id="2e587-119">Affixes</span></span>
<span data-ttu-id="2e587-120">Come si osserva toodefine una convenzione di denominazione, viene fornito una decisione se affisso hello è:</span><span class="sxs-lookup"><span data-stu-id="2e587-120">As you look toodefine a naming convention, one decision comes whether hello affix is at:</span></span>

* <span data-ttu-id="2e587-121">inizio Hello del nome hello (prefisso)</span><span class="sxs-lookup"><span data-stu-id="2e587-121">hello beginning of hello name (prefix)</span></span>
* <span data-ttu-id="2e587-122">fine di Hello del nome di hello (suffisso)</span><span class="sxs-lookup"><span data-stu-id="2e587-122">hello end of hello name (suffix)</span></span>

<span data-ttu-id="2e587-123">Ecco ad esempio, due nomi possibili per un gruppo di risorse utilizzando hello `rg` appone:</span><span class="sxs-lookup"><span data-stu-id="2e587-123">For instance, here are two possible names for a Resource Group using hello `rg` affix:</span></span>

* <span data-ttu-id="2e587-124">Rg-WebApp (prefisso)</span><span class="sxs-lookup"><span data-stu-id="2e587-124">Rg-WebApp (prefix)</span></span>
* <span data-ttu-id="2e587-125">WebApp-Rg (suffisso)</span><span class="sxs-lookup"><span data-stu-id="2e587-125">WebApp-Rg (suffix)</span></span>

<span data-ttu-id="2e587-126">Affissi possono fare riferimento a aspetti toodifferent che descrivono le risorse particolare hello.</span><span class="sxs-lookup"><span data-stu-id="2e587-126">Affixes can refer toodifferent aspects that describe hello particular resources.</span></span> <span data-ttu-id="2e587-127">Hello nella tabella seguente vengono illustrati alcuni esempi utilizzati in genere.</span><span class="sxs-lookup"><span data-stu-id="2e587-127">hello following table shows some examples typically used.</span></span>

| <span data-ttu-id="2e587-128">Aspetto</span><span class="sxs-lookup"><span data-stu-id="2e587-128">Aspect</span></span> | <span data-ttu-id="2e587-129">esempi</span><span class="sxs-lookup"><span data-stu-id="2e587-129">Examples</span></span> | <span data-ttu-id="2e587-130">Note</span><span class="sxs-lookup"><span data-stu-id="2e587-130">Notes</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2e587-131">Environment</span><span class="sxs-lookup"><span data-stu-id="2e587-131">Environment</span></span> |<span data-ttu-id="2e587-132">dev, stg, prod</span><span class="sxs-lookup"><span data-stu-id="2e587-132">dev, stg, prod</span></span> |<span data-ttu-id="2e587-133">In base a scopo di hello e il nome di ogni ambiente.</span><span class="sxs-lookup"><span data-stu-id="2e587-133">Depending on hello purpose and name of each environment.</span></span> |
| <span data-ttu-id="2e587-134">Percorso</span><span class="sxs-lookup"><span data-stu-id="2e587-134">Location</span></span> |<span data-ttu-id="2e587-135">usw (Stati Uniti occidentali), use (Stati Uniti orientali 2)</span><span class="sxs-lookup"><span data-stu-id="2e587-135">usw (West US), use (East US 2)</span></span> |<span data-ttu-id="2e587-136">A seconda area hello del Data Center hello o hello nell'area dell'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="2e587-136">Depending on hello region of hello datacenter or hello region of hello organization.</span></span> |
| <span data-ttu-id="2e587-137">Componente di Azure, servizio o prodotto</span><span class="sxs-lookup"><span data-stu-id="2e587-137">Azure component, service, or product</span></span> |<span data-ttu-id="2e587-138">Rg per gruppo di risorse, VNet per rete virtuale</span><span class="sxs-lookup"><span data-stu-id="2e587-138">Rg for resource group, VNet for virtual network</span></span> |<span data-ttu-id="2e587-139">A seconda del prodotto hello fornisce il supporto per i quali hello risorse.</span><span class="sxs-lookup"><span data-stu-id="2e587-139">Depending on hello product for which hello resource provides support.</span></span> |
| <span data-ttu-id="2e587-140">Ruolo</span><span class="sxs-lookup"><span data-stu-id="2e587-140">Role</span></span> |<span data-ttu-id="2e587-141">sql, ora, sp, iis</span><span class="sxs-lookup"><span data-stu-id="2e587-141">sql, ora, sp, iis</span></span> |<span data-ttu-id="2e587-142">In base al ruolo hello della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2e587-142">Depending on hello role of hello virtual machine.</span></span> |
| <span data-ttu-id="2e587-143">Istanza</span><span class="sxs-lookup"><span data-stu-id="2e587-143">Instance</span></span> |<span data-ttu-id="2e587-144">01, 02 e 03 e così via.</span><span class="sxs-lookup"><span data-stu-id="2e587-144">01, 02, 03, etc.</span></span> |<span data-ttu-id="2e587-145">Per le risorse con più di un'istanza.</span><span class="sxs-lookup"><span data-stu-id="2e587-145">For resources that have more than one instance.</span></span> <span data-ttu-id="2e587-146">Ad esempio, i server Web con carico bilanciato in un servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="2e587-146">For example, load balanced web servers in a cloud service.</span></span> |

<span data-ttu-id="2e587-147">Quando si stabiliscono le convenzioni di denominazione, assicurarsi che è chiaramente indicato che appone toouse per ogni tipo di risorsa e in quale posizione (suffisso vs prefisso).</span><span class="sxs-lookup"><span data-stu-id="2e587-147">When establishing your naming conventions, make sure that they clearly state which affixes toouse for each type of resource, and in which position (prefix vs suffix).</span></span>

## <a name="dates"></a><span data-ttu-id="2e587-148">Date</span><span class="sxs-lookup"><span data-stu-id="2e587-148">Dates</span></span>
<span data-ttu-id="2e587-149">È spesso data hello toodetermine importante della creazione dal nome hello di una risorsa.</span><span class="sxs-lookup"><span data-stu-id="2e587-149">It is often important toodetermine hello date of creation from hello name of a resource.</span></span> <span data-ttu-id="2e587-150">Si consiglia di formato di data hello aaaammgg.</span><span class="sxs-lookup"><span data-stu-id="2e587-150">We recommend hello YYYYMMDD date format.</span></span> <span data-ttu-id="2e587-151">Questo formato assicura che non solo data completa hello viene registrato, ma anche che due risorse i cui nomi si differenziano solo per data hello viene ordinato in ordine alfabetico e in ordine cronologico in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="2e587-151">This format ensures that not only hello full date is recorded, but also that two resources whose names differ only on hello date is sorted alphabetically and chronologically at hello same time.</span></span>

## <a name="naming-resources"></a><span data-ttu-id="2e587-152">Nomi delle risorse</span><span class="sxs-lookup"><span data-stu-id="2e587-152">Naming resources</span></span>
<span data-ttu-id="2e587-153">Definire ogni tipo di risorsa nella convenzione di denominazione hello, che dovrebbero essere presenti regole che definiscono come tooassign nomi tooeach risorsa che viene creato.</span><span class="sxs-lookup"><span data-stu-id="2e587-153">Define each type of resource in hello naming convention, which should have rules that define how tooassign names tooeach resource that is created.</span></span> <span data-ttu-id="2e587-154">Queste regole, applicare tooall tipi di risorse, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2e587-154">These rules should apply tooall types of resources, for example:</span></span>

* <span data-ttu-id="2e587-155">Sottoscrizioni</span><span class="sxs-lookup"><span data-stu-id="2e587-155">Subscriptions</span></span>
* <span data-ttu-id="2e587-156">Account</span><span class="sxs-lookup"><span data-stu-id="2e587-156">Accounts</span></span>
* <span data-ttu-id="2e587-157">Account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2e587-157">Storage accounts</span></span>
* <span data-ttu-id="2e587-158">Reti virtuali</span><span class="sxs-lookup"><span data-stu-id="2e587-158">Virtual networks</span></span>
* <span data-ttu-id="2e587-159">Subnet</span><span class="sxs-lookup"><span data-stu-id="2e587-159">Subnets</span></span>
* <span data-ttu-id="2e587-160">Set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="2e587-160">Availability sets</span></span>
* <span data-ttu-id="2e587-161">Gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="2e587-161">Resource groups</span></span>
* <span data-ttu-id="2e587-162">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="2e587-162">Virtual machines</span></span>
* <span data-ttu-id="2e587-163">Endpoint</span><span class="sxs-lookup"><span data-stu-id="2e587-163">Endpoints</span></span>
* <span data-ttu-id="2e587-164">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="2e587-164">Network security groups</span></span>
* <span data-ttu-id="2e587-165">Ruoli</span><span class="sxs-lookup"><span data-stu-id="2e587-165">Roles</span></span>

<span data-ttu-id="2e587-166">tooensure che hello nome fornisce risorse di toowhich toodetermine sufficienti informazioni che fa riferimento, è necessario utilizzare nomi descrittivi.</span><span class="sxs-lookup"><span data-stu-id="2e587-166">tooensure that hello name provides enough information toodetermine toowhich resource it refers, you should use descriptive names.</span></span>

## <a name="computer-names"></a><span data-ttu-id="2e587-167">Nomi dei computer</span><span class="sxs-lookup"><span data-stu-id="2e587-167">Computer names</span></span>
<span data-ttu-id="2e587-168">Quando si crea una macchina virtuale (VM), Microsoft Azure richiede un nome della macchina virtuale di backup too15 caratteri viene utilizzato per il nome di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="2e587-168">When you create a virtual machine (VM), Microsoft Azure requires a VM name of up too15 characters which is used for hello resource name.</span></span> <span data-ttu-id="2e587-169">Azure Usa hello stesso nome del sistema operativo hello installato nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="2e587-169">Azure uses hello same name for hello operating system installed in hello VM.</span></span> <span data-ttu-id="2e587-170">Tuttavia, questi nomi potrebbero non sempre essere hello stesso.</span><span class="sxs-lookup"><span data-stu-id="2e587-170">However, these names might not always be hello same.</span></span>

<span data-ttu-id="2e587-171">In caso di una macchina virtuale viene creata da un file di immagine con estensione vhd che contiene già un sistema operativo, nome della macchina virtuale hello in Azure può differire da hello Nome computer del sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2e587-171">In case a VM is created from a .vhd image file that already contains an operating system, hello VM name in Azure can differ from hello VM's operating system computer name.</span></span> <span data-ttu-id="2e587-172">Questa situazione è possibile aggiungere un livello di gestione di tooVM difficoltà, che pertanto non è consigliabile.</span><span class="sxs-lookup"><span data-stu-id="2e587-172">This situation can add a degree of difficulty tooVM management, which we therefore do not recommend.</span></span> <span data-ttu-id="2e587-173">Assegnare hello hello risorsa macchina virtuale di Azure stesso nome come nome di computer hello assegnare toohello di sistema operativo della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2e587-173">Assign hello Azure VM resource hello same name as hello computer name that you assign toohello operating system of that VM.</span></span>

<span data-ttu-id="2e587-174">Si consiglia di tale nome di macchina virtuale di Azure hello è hello come hello Nome computer del sistema operativo sottostante.</span><span class="sxs-lookup"><span data-stu-id="2e587-174">We recommend that hello Azure VM name is hello same as hello underlying operating system computer name.</span></span>

## <a name="storage-account-names"></a><span data-ttu-id="2e587-175">Nomi account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2e587-175">Storage account names</span></span>
<span data-ttu-id="2e587-176">In questa sezione non si applica troppo[dischi gestiti di Azure](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), come si crea un account di archiviazione separata.</span><span class="sxs-lookup"><span data-stu-id="2e587-176">This section does not apply too[Azure Managed Disks](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), as you do not create a separate storage account.</span></span> <span data-ttu-id="2e587-177">Per i dischi non gestiti, gli account di archiviazione hanno regole speciali che ne controllano i nomi.</span><span class="sxs-lookup"><span data-stu-id="2e587-177">For unmanaged disks, storage accounts have special rules governing their names.</span></span> <span data-ttu-id="2e587-178">È possibile usare solo lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="2e587-178">You can only use lowercase letters and numbers.</span></span> <span data-ttu-id="2e587-179">Per altre informazioni, vedere [Creare un account di archiviazione](../../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2e587-179">For more information, see [Create a storage account](../../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="2e587-180">Inoltre, nome account di archiviazione hello, insieme a core.windows.net, deve essere un nome DNS univoco globale valido.</span><span class="sxs-lookup"><span data-stu-id="2e587-180">Additionally, hello storage account name, along with core.windows.net, should be a globally valid, unique DNS name.</span></span> <span data-ttu-id="2e587-181">Ad esempio, se l'account di archiviazione hello viene chiamato mystorageaccount, hello seguenti nomi DNS risultanti devono essere univoci:</span><span class="sxs-lookup"><span data-stu-id="2e587-181">For instance, if hello storage account is called mystorageaccount, hello following resulting DNS names should be unique:</span></span>

* <span data-ttu-id="2e587-182">mystorageaccount.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2e587-182">mystorageaccount.blob.core.windows.net</span></span>
* <span data-ttu-id="2e587-183">mystorageaccount.table.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2e587-183">mystorageaccount.table.core.windows.net</span></span>
* <span data-ttu-id="2e587-184">mystorageaccount.queue.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2e587-184">mystorageaccount.queue.core.windows.net</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e587-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2e587-185">Next steps</span></span>
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

