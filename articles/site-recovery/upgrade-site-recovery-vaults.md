---
title: Aggiornare un insieme di credenziali di Site Recovery a un insieme di credenziali di Servizi di ripristino di Azure
description: Informazioni su come aggiornare un insieme di credenziali di Site Recovery a un insieme di credenziali di Servizi di ripristino
documentationcenter: 
author: rajani-janaki-ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/31/2017
ms.author: rajani-janaki-ram
ms.openlocfilehash: fdb33ea0d08353b491f2934fcf885fcb6910b9a2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-site-recovery-vault-to-an-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="513d7-103">Aggiornare un insieme di credenziali di Site Recovery a un insieme di credenziali di Servizi di ripristino basato su Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="513d7-103">Upgrade a Site Recovery vault to an Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="513d7-104">Questo articolo descrive come aggiornare gli insiemi di credenziali di Azure Site Recovery agli insiemi di credenziali di Servizi di ripristino basati su Azure Resource Manager senza alcun impatto sulla replica in corso.</span><span class="sxs-lookup"><span data-stu-id="513d7-104">This article describes how to upgrade Azure Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="513d7-105">Per altre informazioni sulle funzionalità e sui vantaggi di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="513d7-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="513d7-106">Introduction</span></span>
<span data-ttu-id="513d7-107">Un insieme di credenziali di Servizi di ripristino è una risorsa di Azure Resource Manager che consente di gestire il backup e il ripristino di emergenza in modo nativo nel cloud.</span><span class="sxs-lookup"><span data-stu-id="513d7-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in the cloud.</span></span> <span data-ttu-id="513d7-108">È un insieme di credenziali unificato che è possibile usare nel nuovo portale di Azure e sostituisce i classici insiemi di credenziali di backup e Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="513d7-108">It is a unified vault that you can use in the new Azure portal, and it replaces the classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="513d7-109">Gli insiemi di credenziali di Servizi di ripristino offrono una nuova gamma di funzionalità, elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="513d7-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="513d7-110">Supporto di Azure Resource Manager: è possibile proteggere ed eseguire il failover delle macchine virtuali e dei computer fisici in uno stack di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="513d7-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="513d7-111">Esclusione del disco: se si hanno file temporanei o dati ad alta varianza per i quali non si vuole usare tutta la larghezza di banda, è possibile escludere volumi dalla replica.</span><span class="sxs-lookup"><span data-stu-id="513d7-111">Exclude disk: If you have temp files or high churn data that you don’t want to use all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="513d7-112">Questa funzionalità è attualmente abilitata negli scenari *da VMware ad Azure* e *da Hyper-V ad Azure* ed è estesa anche ad altri scenari.</span><span class="sxs-lookup"><span data-stu-id="513d7-112">This capability has been enabled currently in *VMware to Azure* and *Hyper-V to Azure* and is extended to other scenarios as well.</span></span>

* <span data-ttu-id="513d7-113">Supporto per l'archiviazione Premium e con ridondanza locale: è possibile ora proteggere i server in account di archiviazione Premium che consentono agli utenti di proteggere le applicazioni con valori di input/output al secondo più elevati.</span><span class="sxs-lookup"><span data-stu-id="513d7-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers to protect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="513d7-114">Questa funzionalità è attualmente abilitata nello scenario *da VMware ad Azure*.</span><span class="sxs-lookup"><span data-stu-id="513d7-114">This capability is currently enabled in *VMware to Azure*.</span></span>

* <span data-ttu-id="513d7-115">Attività iniziali semplificate: le attività iniziali sono state progettate per facilitare la configurazione del ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="513d7-115">Streamlined getting-started experience: The enhanced getting-started experience has been designed to make disaster-recovery setup easy.</span></span>

* <span data-ttu-id="513d7-116">Gestione di Backup e Site Recovery dallo stesso insieme di credenziali: è ora possibile proteggere i server per il ripristino di emergenza o il backup dallo stesso insieme di credenziali, riducendo in modo significativo il sovraccarico di gestione.</span><span class="sxs-lookup"><span data-stu-id="513d7-116">Backup and Site Recovery management from the same vault: You can now protect servers for disaster recovery or perform backup from the same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="513d7-117">Per altre informazioni sull'esperienza e sulle funzionalità aggiornate, vedere il blog [Storage, Backup, and Recovery](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/) (Archiviazione, backup e ripristino).</span><span class="sxs-lookup"><span data-stu-id="513d7-117">For more information about the upgraded experience and features, see the [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="513d7-118">Funzionalità principali</span><span class="sxs-lookup"><span data-stu-id="513d7-118">Salient features</span></span>

* <span data-ttu-id="513d7-119">Nessun impatto sulla replica in corso: le repliche in corso continuano senza interruzioni durante e dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="513d7-120">Nessun costo aggiuntivo: è possibile ottenere un intero set di funzionalità aggiornate senza costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="513d7-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="513d7-121">Nessuna perdita di dati: trattandosi di un processo di aggiornamento e non di migrazione, i punti di ripristino e le impostazioni esistenti della replica rimangono invariate durante e dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after the upgrade.</span></span>


## <a name="what-happens-during-the-vault-upgrade"></a><span data-ttu-id="513d7-122">Che cosa accade durante l'aggiornamento dell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="513d7-122">What happens during the vault upgrade?</span></span>

<span data-ttu-id="513d7-123">Durante l'aggiornamento, non è possibile eseguire operazioni come la registrazione di un nuovo server o l'abilitazione della replica per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="513d7-123">During the upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="513d7-124">Le operazioni che implicano la lettura o la scrittura di dati nell'insieme di credenziali, come la replica in corso di elementi protetti nell'insieme di credenziali, continuano invece senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="513d7-124">Operations that involve reading data from or writing data to the vault, such as ongoing replication of protected items to the vault, continue uninterrupted.</span></span>

### <a name="changes-to-automation-and-tooling-after-the-upgrade"></a><span data-ttu-id="513d7-125">Modifiche all'automazione e agli strumenti dopo l'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="513d7-125">Changes to automation and tooling after the upgrade</span></span>
<span data-ttu-id="513d7-126">Quando si aggiorna il tipo di insieme di credenziali dal modello di distribuzione classica al modello di distribuzione Resource Manager, aggiornare l'automazione o gli strumenti esistenti per accertarsi che continuino a funzionare anche dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-126">As you upgrade the vault type from the classic deployment model to the Resource Manager deployment model, update the existing automation or tooling to ensure that it continues to work after the upgrade.</span></span>

### <a name="prepare-your-environment-for-the-upgrade"></a><span data-ttu-id="513d7-127">Preparare l'ambiente per l'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="513d7-127">Prepare your environment for the upgrade</span></span>

* [<span data-ttu-id="513d7-128">Installare PowerShell o aggiornarlo alla versione 5 o successiva</span><span class="sxs-lookup"><span data-stu-id="513d7-128">Install PowerShell or upgrade it to version 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="513d7-129">Installare la versione più recente del file MSI di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="513d7-129">Install the latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="513d7-130">Scaricare lo script di aggiornamento dell'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="513d7-130">Download the Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="513d7-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="513d7-131">Prerequisites</span></span>
<span data-ttu-id="513d7-132">Per eseguire l'aggiornamento da insiemi di credenziali di Site Recovery a insiemi di credenziali di Servizi di ripristino basati su Azure Resource Manager, è necessario soddisfare i requisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="513d7-132">To upgrade from Site Recovery vaults to Azure Resource Manager-based Recovery Service vaults, you must meet the following requirements:</span></span>

* <span data-ttu-id="513d7-133">Versione minima dell'agente: la versione del provider di Azure Site Recovery installata nel server deve essere 5.1.1700.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="513d7-133">Minimum agent version: The version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="513d7-134">Configurazione supportata: non è possibile configurare l'insieme di credenziali con la rete di archiviazione (SAN) o i gruppi di disponibilità AlwaysOn di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="513d7-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="513d7-135">Sono supportate tutte le altre configurazioni.</span><span class="sxs-lookup"><span data-stu-id="513d7-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="513d7-136">Dopo l'aggiornamento, è possibile gestire il mapping dell'archiviazione solo tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="513d7-136">After the upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="513d7-137">Scenario di distribuzione supportato: l'insieme di credenziali non deve essere il modello di distribuzione legacy *da VMware ad Azure*.</span><span class="sxs-lookup"><span data-stu-id="513d7-137">Supported deployment scenario: Your vault shouldn’t be the *VMware to Azure* legacy deployment model.</span></span> <span data-ttu-id="513d7-138">Prima di continuare, passare al modello di distribuzione avanzata.</span><span class="sxs-lookup"><span data-stu-id="513d7-138">Before you proceed, first move to the enhanced deployment model.</span></span>

* <span data-ttu-id="513d7-139">Nessun processo attivo avviato dall'utente che coinvolga operazioni del piano di gestione: poiché durante l'aggiornamento l'accesso al piano di gestione è limitato, completare tutte le azioni del piano di gestione prima di attivare l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-139">No active user-initiated jobs that involve management plane operations: Because access to the management plane is restricted during upgrade, complete all your management plane actions before you trigger the upgrade.</span></span> <span data-ttu-id="513d7-140">Questo processo non include la replica in corso.</span><span class="sxs-lookup"><span data-stu-id="513d7-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="513d7-141">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="513d7-141">Frequently asked questions</span></span>

<span data-ttu-id="513d7-142">**L'aggiornamento influisce sulla replica in corso?**</span><span class="sxs-lookup"><span data-stu-id="513d7-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="513d7-143">No.</span><span class="sxs-lookup"><span data-stu-id="513d7-143">No.</span></span> <span data-ttu-id="513d7-144">Durante e dopo l'aggiornamento, la replica in corso continua ininterrottamente.</span><span class="sxs-lookup"><span data-stu-id="513d7-144">Your ongoing replication continues uninterrupted during and after the upgrade.</span></span>

<span data-ttu-id="513d7-145">**Che cosa accade alle impostazioni di rete, ad esempio alle impostazioni IP e VPN da sito a sito?**</span><span class="sxs-lookup"><span data-stu-id="513d7-145">**What happens to network settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="513d7-146">L'aggiornamento non influisce sulle impostazioni di rete.</span><span class="sxs-lookup"><span data-stu-id="513d7-146">The upgrade doesn't affect the network settings.</span></span> <span data-ttu-id="513d7-147">Tutte le connessioni da Azure a locale rimangono inalterate.</span><span class="sxs-lookup"><span data-stu-id="513d7-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="513d7-148">**Che cosa accade agli insiemi di credenziali se non si prevede un aggiornamento a breve?**</span><span class="sxs-lookup"><span data-stu-id="513d7-148">**What happens to my vaults if I don’t plan to upgrade in the near future?**</span></span>

<span data-ttu-id="513d7-149">Il supporto per l'insieme di credenziali di Site Recovery nella versione precedente del portale di Azure sarà deprecato a partire dal mese di settembre 2017.</span><span class="sxs-lookup"><span data-stu-id="513d7-149">Support for Site Recovery vault in the old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="513d7-150">È consigliabile usare la funzionalità di aggiornamento per passare al nuovo portale.</span><span class="sxs-lookup"><span data-stu-id="513d7-150">We strongly recommend that you use the upgrade feature to move to the new portal.</span></span>

<span data-ttu-id="513d7-151">**Qual è l'impatto di questo piano di migrazione per gli strumenti esistenti?**</span><span class="sxs-lookup"><span data-stu-id="513d7-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="513d7-152">L'aggiornamento degli strumenti al modello di distribuzione Resource Manager è una delle modifiche più importanti da tenere in considerazione per i piani di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-152">Updating your tooling to the Resource Manager deployment model is one of the most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="513d7-153">Gli insiemi di credenziali di Servizi di ripristino si basano sul modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="513d7-153">The Recovery Services vaults are based on the Resource Manager deployment model.</span></span> 

<span data-ttu-id="513d7-154">**Quale durata ha il tempo di inattività del piano di gestione?**</span><span class="sxs-lookup"><span data-stu-id="513d7-154">**How long does the management-plane downtime last?**</span></span>

<span data-ttu-id="513d7-155">L'aggiornamento richiede in genere da 15 a 30 minuti circa, fino a un massimo di un'ora.</span><span class="sxs-lookup"><span data-stu-id="513d7-155">The upgrade ordinarily takes about 15 to 30 minutes, and it could take up to a maximum of one hour.</span></span>

<span data-ttu-id="513d7-156">**È possibile eseguire il ripristino dello stato precedente dopo l'aggiornamento?**</span><span class="sxs-lookup"><span data-stu-id="513d7-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="513d7-157">No.</span><span class="sxs-lookup"><span data-stu-id="513d7-157">No.</span></span> <span data-ttu-id="513d7-158">Il ripristino dello stato precedente non è supportato dopo il completamento dell'aggiornamento delle risorse.</span><span class="sxs-lookup"><span data-stu-id="513d7-158">Rollback is not supported after the resources have been successfully upgraded.</span></span>

<span data-ttu-id="513d7-159">**È possibile convalidare la sottoscrizione o le risorse per verificare se possono essere aggiornate?**</span><span class="sxs-lookup"><span data-stu-id="513d7-159">**Can I validate my subscription or resources to see whether they can be upgraded?**</span></span>

<span data-ttu-id="513d7-160">Sì.</span><span class="sxs-lookup"><span data-stu-id="513d7-160">Yes.</span></span> <span data-ttu-id="513d7-161">Nell'opzione di aggiornamento supportata dalla piattaforma, il primo passaggio prevede di verificare che le risorse siano idonee per un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="513d7-161">In the platform-supported upgrade option, the first step in the upgrade is to validate that the resources are capable of an upgrade.</span></span> <span data-ttu-id="513d7-162">In caso di esito negativo dell'operazione di convalida, si riceveranno appositi messaggi di errore o avvisi.</span><span class="sxs-lookup"><span data-stu-id="513d7-162">If the validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="513d7-163">**Come è possibile segnalare un problema in fase di aggiornamento?**</span><span class="sxs-lookup"><span data-stu-id="513d7-163">**How do I report an issue with the upgrade?**</span></span>

<span data-ttu-id="513d7-164">Se si verifica un errore durante l'aggiornamento, prendere nota dell'ID dell'operazione elencato nell'errore.</span><span class="sxs-lookup"><span data-stu-id="513d7-164">If you experience any failures during the upgrade, note the operation ID that's listed in the error.</span></span> <span data-ttu-id="513d7-165">Il supporto tecnico Microsoft si impegnerà per risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="513d7-165">Microsoft Support will proactively work on resolving the issue.</span></span> <span data-ttu-id="513d7-166">È anche possibile contattare il supporto tecnico indicando l'ID della sottoscrizione, il nome dell'insieme di credenziali e l'ID dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="513d7-166">You can also contact the Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="513d7-167">Il supporto tecnico si impegnerà per cercare di risolvere il problema il prima possibile.</span><span class="sxs-lookup"><span data-stu-id="513d7-167">Support will work to resolve the issue as quickly as possible.</span></span> <span data-ttu-id="513d7-168">Non ripetere l'operazione a meno che non venga esplicitamente richiesto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="513d7-168">Do not retry the operation unless you are explicitly instructed to do so by Microsoft.</span></span>

## <a name="run-the-script"></a><span data-ttu-id="513d7-169">Esecuzione dello script</span><span class="sxs-lookup"><span data-stu-id="513d7-169">Run the script</span></span>

<span data-ttu-id="513d7-170">In PowerShell eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="513d7-170">In PowerShell, run the following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="513d7-171">SubscriptionID: ID della sottoscrizione associato all'insieme di credenziali che si sta aggiornando.</span><span class="sxs-lookup"><span data-stu-id="513d7-171">SubscriptionID: The subscription ID that's associated with the vault that you're upgrading.</span></span>

* <span data-ttu-id="513d7-172">VaultName: nome dell'insieme di credenziali che si sta aggiornando.</span><span class="sxs-lookup"><span data-stu-id="513d7-172">VaultName: The name of the vault that you're upgrading.</span></span>

* <span data-ttu-id="513d7-173">Location: posizione dell'insieme di credenziali che si sta aggiornando.</span><span class="sxs-lookup"><span data-stu-id="513d7-173">Location: The location of the vault that you're upgrading.</span></span>

* <span data-ttu-id="513d7-174">ResourceType: HyperVRecoveryManagerVault per gli insiemi di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="513d7-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="513d7-175">TargetResourceGroupName: gruppo di risorse in cui si vuole inserire l'insieme di credenziali aggiornato.</span><span class="sxs-lookup"><span data-stu-id="513d7-175">TargetResourceGroupName: The resource group into which you want the upgraded vault to be placed.</span></span> <span data-ttu-id="513d7-176">TargetResourceGroupName può essere un gruppo di risorse esistente in Azure Resource Manager o uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="513d7-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="513d7-177">Se il valore TargetResourceGroupName specificato non esiste, viene creato nel corso del processo di aggiornamento nello stesso percorso dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="513d7-177">If the TargetResourceGroupName that's supplied does not exist, it is created as part of the upgrade in the same location as the vault.</span></span> <span data-ttu-id="513d7-178">Per altre informazioni, vedere la sezione "Gruppi di risorse" di [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="513d7-178">For more information, see the "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="513d7-179">La denominazione del gruppo di risorse è soggetta a determinati vincoli.</span><span class="sxs-lookup"><span data-stu-id="513d7-179">Resource group naming is subject to certain constraints.</span></span> <span data-ttu-id="513d7-180">Per evitare l'errore di aggiornamento dell'insieme di credenziali, assicurarsi di rispettare la convenzione di denominazione,</span><span class="sxs-lookup"><span data-stu-id="513d7-180">To prevent vault upgrade failure, be sure to observe the naming convention carefully.</span></span>
    >
    ><span data-ttu-id="513d7-181">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="513d7-181">For example:</span></span>
    >
    ><span data-ttu-id="513d7-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="513d7-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="513d7-183">In alternativa, è possibile usare lo script seguente.</span><span class="sxs-lookup"><span data-stu-id="513d7-183">Alternatively, you can run the following script.</span></span> <span data-ttu-id="513d7-184">Immettere i valori per i parametri obbligatori.</span><span class="sxs-lookup"><span data-stu-id="513d7-184">Enter the values for the required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for the following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="513d7-185">Lo script di PowerShell richiede di immettere le credenziali.</span><span class="sxs-lookup"><span data-stu-id="513d7-185">The PowerShell script prompts you to enter your credentials.</span></span> <span data-ttu-id="513d7-186">Immetterle due volte, la prima per l'account del modello di distribuzione classica, la seconda per l'account di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="513d7-186">Enter them twice, once for the classic deployment model account and once for the Azure Resource Manager account.</span></span>

2. <span data-ttu-id="513d7-187">Dopo avere immesso le credenziali, lo script esegue un controllo per determinare se la configurazione dell'infrastruttura soddisfa i requisiti descritti prima.</span><span class="sxs-lookup"><span data-stu-id="513d7-187">After you've entered your credentials, the script runs a check to determine whether your infrastructure setup meets the previously mentioned requirements.</span></span>

3. <span data-ttu-id="513d7-188">Dopo che i prerequisiti sono stati controllati e confermati, viene chiesto di continuare con l'aggiornamento dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="513d7-188">After the prerequisites have been checked and confirmed, you are prompted to proceed with the vault upgrade.</span></span> <span data-ttu-id="513d7-189">Il processo di aggiornamento avvia l'aggiornamento dell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="513d7-189">The upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="513d7-190">L'aggiornamento viene completato in 15-30 minuti.</span><span class="sxs-lookup"><span data-stu-id="513d7-190">The entire upgrade can take 15 to 30 minutes to complete.</span></span>

4. <span data-ttu-id="513d7-191">Al termine del processo di aggiornamento, è possibile accedere all'insieme di credenziali aggiornato nel nuovo portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="513d7-191">After the upgrade has been completed successfully, you can access the upgraded vault in the new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="513d7-192">Gestione dell'insieme di credenziali successiva all'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="513d7-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-the-recovery-services-vault"></a><span data-ttu-id="513d7-193">Eseguire la replica usando Azure Site Recovery nell'insieme di credenziali di Servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="513d7-193">Replicate by using Azure Site Recovery in the Recovery Services vault</span></span>

* <span data-ttu-id="513d7-194">È ora possibile proteggere le macchine virtuali di Azure da un'area a un'altra.</span><span class="sxs-lookup"><span data-stu-id="513d7-194">You can now protect your Azure VMs from one region to another.</span></span> <span data-ttu-id="513d7-195">Per altre informazioni, vedere [Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="513d7-196">Per altre informazioni sulla replica di macchine virtuali VMware in Azure, vedere [Replicare VM VMware in Azure con Site Recovery](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-196">For more information about replicating VMware VMs to Azure, see [Replicate VMware VMs to Azure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="513d7-197">Per altre informazioni sulla replica di macchine virtuali Hyper-V (senza VMM) in Azure, vedere [Eseguire la replica di macchine virtuali Hyper-V (senza VMM) in Azure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-197">For more information about replicating Hyper-V VMs (without VMM) to Azure, see [Replicate Hyper-V virtual machines (without VMM) to Azure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="513d7-198">Per altre informazioni sulla replica di macchine virtuali Hyper-V (con VMM) in Azure, vedere [Eseguire la replica di macchine virtuali Hyper-V nei cloud VMM in Azure tramite Site Recovery nel portale di Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-198">For more information about replicating Hyper-V VMs (with VMM) to Azure, see [Replicate Hyper-V virtual machines in VMM clouds to Azure using Site Recovery in the Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="513d7-199">Per altre informazioni sulla replica di macchine virtuali Hyper-V (con VMM) in un sito secondario, vedere [Eseguire la replica di macchine virtuali Hyper-V in cloud VMM in un sito VMM secondario usando il portale di Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-199">For more information about replicating Hyper-VMs (with VMM) to a secondary site, see [Replicate Hyper-V virtual machines in VMM clouds to a secondary VMM site using the Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="513d7-200">Per altre informazioni sulla replica di macchine virtuali VMware in un sito secondario, vedere [Eseguire la replica di macchine virtuali VMware locali o server fisici in un sito secondario nel portale di Azure classico](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-200">For more information about replicating VMware VMs to a secondary site, see [Replicate on-premises VMware virtual machines or physical servers to a secondary site in the classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="513d7-201">Visualizzare gli elementi replicati</span><span class="sxs-lookup"><span data-stu-id="513d7-201">View your replicated items</span></span>

<span data-ttu-id="513d7-202">L'immagine seguente mostra la pagina del dashboard dell'insieme di credenziali di Servizi di ripristino in cui vengono visualizzate le entità principali relative all'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="513d7-202">The following image shows the Recovery Services vault dashboard page that displays key entities for the vault.</span></span> <span data-ttu-id="513d7-203">Per visualizzare un elenco delle entità protette nell'insieme di credenziali, selezionare **Site Recovery** > **Elementi replicati**.</span><span class="sxs-lookup"><span data-stu-id="513d7-203">To view a list of protected entities in the vault, select **Site Recovery** > **Replicated items**.</span></span>


![Elementi replicati](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="513d7-205">L'immagine seguente illustra il flusso di lavoro per visualizzare gli elementi replicati e il comando **Failover** per avviare un failover.</span><span class="sxs-lookup"><span data-stu-id="513d7-205">The following image shows the workflow for viewing your replicated items and the **Failover** command for initiating a failover.</span></span>

![Elementi replicati](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="513d7-207">Visualizzare le impostazioni di replica</span><span class="sxs-lookup"><span data-stu-id="513d7-207">View your replication settings</span></span>

<span data-ttu-id="513d7-208">Nell'insieme di credenziali di Site Recovery ogni gruppo protezione dati è configurato con frequenza di copia, conservazione del punto di ripristino, frequenza degli snapshot coerenti con l'applicazione e altre impostazioni di replica.</span><span class="sxs-lookup"><span data-stu-id="513d7-208">In the Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="513d7-209">Nell'insieme di credenziali di Servizi di ripristino queste impostazioni sono configurate come criteri di replica.</span><span class="sxs-lookup"><span data-stu-id="513d7-209">In the Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="513d7-210">Il nome dei criteri corrisponde al nome del gruppo protezione dati o a *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="513d7-210">The name of the policy is the name of the protection group or the *primarycloud_Policy*.</span></span>

<span data-ttu-id="513d7-211">Per altre informazioni sui criteri di replica, vedere [Gestire i criteri di replica per VMware in Azure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="513d7-211">For more information about replication policy, see [Manage replication policy for VMware to Azure](site-recovery-setup-replication-settings-vmware.md).</span></span>
