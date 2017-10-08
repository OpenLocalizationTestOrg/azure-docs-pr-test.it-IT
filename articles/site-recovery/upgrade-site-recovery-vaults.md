---
title: insieme di credenziali di servizi di ripristino di Azure tooan aaaUpgrade un insieme di credenziali di Site Recovery
description: Informazioni su come un insieme di credenziali di Azure Site Recovery tooupgrade tooa servizi di ripristino dell'insieme di credenziali
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
ms.openlocfilehash: a18a923ee3bad91873e654c9b9b5bf8b83acc123
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-site-recovery-vault-tooan-azure-resource-manager-based-recovery-services-vault"></a><span data-ttu-id="ac213-103">L'aggiornamento di un archivio di servizi di ripristino basate su Gestione risorse di Azure Site Recovery tooan insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="ac213-103">Upgrade a Site Recovery vault tooan Azure Resource Manager-based Recovery Services vault</span></span>

<span data-ttu-id="ac213-104">In questo articolo viene descritto come tooupgrade Azure Site Recovery insiemi di credenziali di insiemi di credenziali del servizio di ripristino basate su Gestione risorse tooAzure senza alcun impatto sulla replica in corso.</span><span class="sxs-lookup"><span data-stu-id="ac213-104">This article describes how tooupgrade Azure Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults without any impact on ongoing replication.</span></span> <span data-ttu-id="ac213-105">Per altre informazioni sulle funzionalità e sui vantaggi di Azure Resource Manager, vedere [Panoramica di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-105">For more information about Azure Resource Manager features and benefits, see [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="ac213-106">Introduzione</span><span class="sxs-lookup"><span data-stu-id="ac213-106">Introduction</span></span>
<span data-ttu-id="ac213-107">Un insieme di credenziali di servizi di ripristino è una risorsa di gestione risorse di Azure per la gestione dei backup e ripristino di emergenza in modo nativo nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-107">A Recovery Services vault is an Azure Resource Manager resource for managing backup and disaster recovery natively in hello cloud.</span></span> <span data-ttu-id="ac213-108">È un insieme di credenziali unificata che è possibile utilizzare in hello nuovo portale di Azure e sostituisce backup classico hello e insiemi di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ac213-108">It is a unified vault that you can use in hello new Azure portal, and it replaces hello classic backup and Site Recovery vaults.</span></span>

<span data-ttu-id="ac213-109">Gli insiemi di credenziali di Servizi di ripristino offrono una nuova gamma di funzionalità, elencate di seguito:</span><span class="sxs-lookup"><span data-stu-id="ac213-109">Recovery Services vaults offer an array of features, including:</span></span>

* <span data-ttu-id="ac213-110">Supporto di Azure Resource Manager: è possibile proteggere ed eseguire il failover delle macchine virtuali e dei computer fisici in uno stack di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ac213-110">Azure Resource Manager support: You can protect and fail over your virtual machines and physical machines into an Azure Resource Manager stack.</span></span>

* <span data-ttu-id="ac213-111">Escludere il disco: se si dispone di file temporanei o elevata varianza dei dati che non si desidera toouse tutta la larghezza di banda per, è possibile escludere i volumi di replica.</span><span class="sxs-lookup"><span data-stu-id="ac213-111">Exclude disk: If you have temp files or high churn data that you don’t want toouse all your bandwidth for, you can exclude volumes from replication.</span></span> <span data-ttu-id="ac213-112">Questa funzionalità è stata abilitata in *VMware tooAzure* e *tooAzure Hyper-V* e viene estesa anche scenari tooother.</span><span class="sxs-lookup"><span data-stu-id="ac213-112">This capability has been enabled currently in *VMware tooAzure* and *Hyper-V tooAzure* and is extended tooother scenarios as well.</span></span>

* <span data-ttu-id="ac213-113">Supporto per premium e l'archiviazione con ridondanza locale: È ora possibile proteggere i server nel servizio di archiviazione premium gli account che consentono agli utenti di applicazioni tooprotect con versioni successive operazioni di input/output al secondo (IOPS).</span><span class="sxs-lookup"><span data-stu-id="ac213-113">Support for premium and locally redundant storage: You can now protect servers in premium storage accounts that allow customers tooprotect applications with higher input/output operations per second (IOPS).</span></span> <span data-ttu-id="ac213-114">Questa funzionalità è attualmente abilitata *tooAzure VMware*.</span><span class="sxs-lookup"><span data-stu-id="ac213-114">This capability is currently enabled in *VMware tooAzure*.</span></span>

* <span data-ttu-id="ac213-115">Guida introduttiva esperienza semplificata: hello avanzata esperienza di Guida introduttiva è stata progettata l'installazione di ripristino di emergenza toomake semplice.</span><span class="sxs-lookup"><span data-stu-id="ac213-115">Streamlined getting-started experience: hello enhanced getting-started experience has been designed toomake disaster-recovery setup easy.</span></span>

* <span data-ttu-id="ac213-116">Backup e gestione di ripristino del sito da hello stesso insieme di credenziali: È ora possibile proteggere i server per il ripristino di emergenza o eseguire il backup da hello stesso insieme di credenziali, che può ridurre il sovraccarico in modo significativo la gestione.</span><span class="sxs-lookup"><span data-stu-id="ac213-116">Backup and Site Recovery management from hello same vault: You can now protect servers for disaster recovery or perform backup from hello same vault, which can reduce your management overhead significantly.</span></span>

<span data-ttu-id="ac213-117">Per ulteriori informazioni sull'esperienza hello aggiornato e le funzionalità, vedere hello [blog di archiviazione, Backup e ripristino](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span><span class="sxs-lookup"><span data-stu-id="ac213-117">For more information about hello upgraded experience and features, see hello [Storage, Backup, and Recovery blog](https://azure.microsoft.com/blog/azure-site-recovery-now-available-in-a-new-experience-with-support-for-arm-and-csp/).</span></span>

## <a name="salient-features"></a><span data-ttu-id="ac213-118">Funzionalità principali</span><span class="sxs-lookup"><span data-stu-id="ac213-118">Salient features</span></span>

* <span data-ttu-id="ac213-119">Nessun impatto sulla replica in corso: le repliche in corso continuano senza interruzioni durante e dopo l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-119">No impact on ongoing replication: Ongoing replications continue without any interruption during and post upgrade.</span></span>

* <span data-ttu-id="ac213-120">Nessun costo aggiuntivo: è possibile ottenere un intero set di funzionalità aggiornate senza costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="ac213-120">No additional cost: Get an entire set of updated capabilities at no additional cost.</span></span>

* <span data-ttu-id="ac213-121">Senza perdita di dati: poiché questo processo è un aggiornamento e non una migrazione, punti di ripristino esistenti di replica e le impostazioni rimangono invariate durante e dopo l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-121">No data loss: Because this process is an upgrade and not a migration, existing replication recovery points and settings remain intact during and after hello upgrade.</span></span>


## <a name="what-happens-during-hello-vault-upgrade"></a><span data-ttu-id="ac213-122">Cosa accade durante l'aggiornamento dell'insieme di credenziali hello?</span><span class="sxs-lookup"><span data-stu-id="ac213-122">What happens during hello vault upgrade?</span></span>

<span data-ttu-id="ac213-123">Durante l'aggiornamento di hello, è possibile eseguire operazioni quali la registrazione di un nuovo server o l'abilitazione della replica per una macchina virtuale (VM).</span><span class="sxs-lookup"><span data-stu-id="ac213-123">During hello upgrade, you cannot perform operations such as registering a new server or enabling replication for a virtual machine (VM).</span></span> <span data-ttu-id="ac213-124">Le operazioni che coinvolgono la lettura o di scrittura dati toohello insieme di credenziali, ad esempio la replica in corso dell'insieme di credenziali toohello gli elementi protetti, senza interruzioni.</span><span class="sxs-lookup"><span data-stu-id="ac213-124">Operations that involve reading data from or writing data toohello vault, such as ongoing replication of protected items toohello vault, continue uninterrupted.</span></span>

### <a name="changes-tooautomation-and-tooling-after-hello-upgrade"></a><span data-ttu-id="ac213-125">Tooautomation modifiche e gli strumenti dopo l'aggiornamento di hello</span><span class="sxs-lookup"><span data-stu-id="ac213-125">Changes tooautomation and tooling after hello upgrade</span></span>
<span data-ttu-id="ac213-126">Come si aggiorna il tipo di insieme di credenziali hello dal modello di distribuzione di gestione delle risorse modello toohello hello distribuzione classica, aggiornare automazione esistente hello o tooensure gli strumenti che continui toowork dopo l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-126">As you upgrade hello vault type from hello classic deployment model toohello Resource Manager deployment model, update hello existing automation or tooling tooensure that it continues toowork after hello upgrade.</span></span>

### <a name="prepare-your-environment-for-hello-upgrade"></a><span data-ttu-id="ac213-127">Preparare l'ambiente per l'aggiornamento di hello</span><span class="sxs-lookup"><span data-stu-id="ac213-127">Prepare your environment for hello upgrade</span></span>

* [<span data-ttu-id="ac213-128">Installare PowerShell o l'aggiornamento tooversion 5 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="ac213-128">Install PowerShell or upgrade it tooversion 5 or later</span></span>](https://www.microsoft.com/download/details.aspx?id=50395)
* [<span data-ttu-id="ac213-129">Installare hello la versione più recente di Azure PowerShell MSI</span><span class="sxs-lookup"><span data-stu-id="ac213-129">Install hello latest version of Azure PowerShell MSI</span></span>](https://github.com/Azure/azure-powershell/releases)
* [<span data-ttu-id="ac213-130">Scaricare script di aggiornamento dell'insieme di credenziali di servizi di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="ac213-130">Download hello Recovery Services vault upgrade script</span></span>](https://aka.ms/vaultupgradescript)

### <a name="prerequisites"></a><span data-ttu-id="ac213-131">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac213-131">Prerequisites</span></span>
<span data-ttu-id="ac213-132">gli insiemi di credenziali del servizio di ripristino basate su Gestione risorse tooAzure insiemi di credenziali di tooupgrade da Site Recovery, è necessario soddisfare i seguenti requisiti hello:</span><span class="sxs-lookup"><span data-stu-id="ac213-132">tooupgrade from Site Recovery vaults tooAzure Resource Manager-based Recovery Service vaults, you must meet hello following requirements:</span></span>

* <span data-ttu-id="ac213-133">Versione minima dell'agente: versione di hello del Provider di Azure Site Recovery installato nel server deve essere 5.1.1700.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="ac213-133">Minimum agent version: hello version of Azure Site Recovery Provider installed on your server must be 5.1.1700.0 or later.</span></span>

* <span data-ttu-id="ac213-134">Configurazione supportata: non è possibile configurare l'insieme di credenziali con la rete di archiviazione (SAN) o i gruppi di disponibilità AlwaysOn di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ac213-134">Supported configuration: You cannot configure your vault with storage area network (SAN) or SQL Server AlwaysOn Availability Groups.</span></span> <span data-ttu-id="ac213-135">Sono supportate tutte le altre configurazioni.</span><span class="sxs-lookup"><span data-stu-id="ac213-135">All other configurations are supported.</span></span>

    >[!NOTE]
    ><span data-ttu-id="ac213-136">Dopo l'aggiornamento di hello, è possibile gestire i mapping di archiviazione solo tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac213-136">After hello upgrade, you can manage storage mapping only via PowerShell.</span></span>

* <span data-ttu-id="ac213-137">Scenario di distribuzione supportati: l'insieme di credenziali non devono essere hello *tooAzure VMware* modello di distribuzione legacy.</span><span class="sxs-lookup"><span data-stu-id="ac213-137">Supported deployment scenario: Your vault shouldn’t be hello *VMware tooAzure* legacy deployment model.</span></span> <span data-ttu-id="ac213-138">Prima di procedere, spostare innanzitutto il modello di distribuzione avanzata di toohello.</span><span class="sxs-lookup"><span data-stu-id="ac213-138">Before you proceed, first move toohello enhanced deployment model.</span></span>

* <span data-ttu-id="ac213-139">Nessun processo attivo avviata dall'utente che coinvolgono gestione piano operations: perché il piano di gestione toohello di accesso è limitato durante l'aggiornamento, completare tutte le azioni del piano di gestione prima attivare l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-139">No active user-initiated jobs that involve management plane operations: Because access toohello management plane is restricted during upgrade, complete all your management plane actions before you trigger hello upgrade.</span></span> <span data-ttu-id="ac213-140">Questo processo non include la replica in corso.</span><span class="sxs-lookup"><span data-stu-id="ac213-140">This process doesn’t include ongoing replication.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="ac213-141">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="ac213-141">Frequently asked questions</span></span>

<span data-ttu-id="ac213-142">**L'aggiornamento influisce sulla replica in corso?**</span><span class="sxs-lookup"><span data-stu-id="ac213-142">**Does this upgrade affect my ongoing replication?**</span></span>

<span data-ttu-id="ac213-143">No.</span><span class="sxs-lookup"><span data-stu-id="ac213-143">No.</span></span> <span data-ttu-id="ac213-144">La replica in corso continua senza interruzioni durante e dopo l'aggiornamento di hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-144">Your ongoing replication continues uninterrupted during and after hello upgrade.</span></span>

<span data-ttu-id="ac213-145">**Cosa accade toonetwork impostazioni, ad esempio le impostazioni IP e VPN da sito a sito?**</span><span class="sxs-lookup"><span data-stu-id="ac213-145">**What happens toonetwork settings such as site-to-site VPN and IP settings?**</span></span>

<span data-ttu-id="ac213-146">aggiornamento di Hello non influenza le impostazioni di rete hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-146">hello upgrade doesn't affect hello network settings.</span></span> <span data-ttu-id="ac213-147">Tutte le connessioni da Azure a locale rimangono inalterate.</span><span class="sxs-lookup"><span data-stu-id="ac213-147">All Azure-to-on-premises connections remain intact.</span></span>

<span data-ttu-id="ac213-148">**Gli insiemi di credenziali toomy cosa accade se non è previsto tooupgrade in hello prossimo futuro?**</span><span class="sxs-lookup"><span data-stu-id="ac213-148">**What happens toomy vaults if I don’t plan tooupgrade in hello near future?**</span></span>

<span data-ttu-id="ac213-149">Supporto per l'insieme di credenziali di Site Recovery nel portale di Azure precedente hello verrà deprecato a partire settembre 2017.</span><span class="sxs-lookup"><span data-stu-id="ac213-149">Support for Site Recovery vault in hello old Azure portal will be deprecated starting September 2017.</span></span> <span data-ttu-id="ac213-150">È consigliabile utilizzare hello funzionalità di aggiornamento toomove toohello nuovo portale.</span><span class="sxs-lookup"><span data-stu-id="ac213-150">We strongly recommend that you use hello upgrade feature toomove toohello new portal.</span></span>

<span data-ttu-id="ac213-151">**Qual è l'impatto di questo piano di migrazione per gli strumenti esistenti?**</span><span class="sxs-lookup"><span data-stu-id="ac213-151">**What does this migration plan mean for my existing tooling?**</span></span>  

<span data-ttu-id="ac213-152">L'aggiornamento del modello di distribuzione di gestione delle risorse toohello strumenti è una delle modifiche più importanti hello che è necessario tener conto nei piani di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-152">Updating your tooling toohello Resource Manager deployment model is one of hello most important changes that you must account for in your upgrade plans.</span></span> <span data-ttu-id="ac213-153">gli insiemi di credenziali di Hello servizi di ripristino sono basati sul modello di distribuzione di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-153">hello Recovery Services vaults are based on hello Resource Manager deployment model.</span></span> 

<span data-ttu-id="ac213-154">**Il tempo hello tempi di inattività gestione piano ultimo?**</span><span class="sxs-lookup"><span data-stu-id="ac213-154">**How long does hello management-plane downtime last?**</span></span>

<span data-ttu-id="ac213-155">aggiornamento di Hello richiede in genere circa 15 minuti too30 e potrebbero richiedere tooa massima di un'ora.</span><span class="sxs-lookup"><span data-stu-id="ac213-155">hello upgrade ordinarily takes about 15 too30 minutes, and it could take up tooa maximum of one hour.</span></span>

<span data-ttu-id="ac213-156">**È possibile eseguire il ripristino dello stato precedente dopo l'aggiornamento?**</span><span class="sxs-lookup"><span data-stu-id="ac213-156">**Can I roll back after upgrading?**</span></span>

<span data-ttu-id="ac213-157">No.</span><span class="sxs-lookup"><span data-stu-id="ac213-157">No.</span></span> <span data-ttu-id="ac213-158">Eseguire il rollback non è supportato dopo risorse hello sono state aggiornate.</span><span class="sxs-lookup"><span data-stu-id="ac213-158">Rollback is not supported after hello resources have been successfully upgraded.</span></span>

<span data-ttu-id="ac213-159">**È possibile convalidare la sottoscrizione o risorse toosee se possono essere aggiornate?**</span><span class="sxs-lookup"><span data-stu-id="ac213-159">**Can I validate my subscription or resources toosee whether they can be upgraded?**</span></span>

<span data-ttu-id="ac213-160">Sì.</span><span class="sxs-lookup"><span data-stu-id="ac213-160">Yes.</span></span> <span data-ttu-id="ac213-161">In hello piattaforma supportata l'opzione di aggiornamento, hello innanzitutto l'aggiornamento di hello è toovalidate che le risorse di hello siano in grado di un aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-161">In hello platform-supported upgrade option, hello first step in hello upgrade is toovalidate that hello resources are capable of an upgrade.</span></span> <span data-ttu-id="ac213-162">Se la convalida di hello non riesce, si riceverà i messaggi di errore appropriato o avvisi.</span><span class="sxs-lookup"><span data-stu-id="ac213-162">If hello validation fails, you will receive appropriate error messages or warnings.</span></span>

<span data-ttu-id="ac213-163">**Come è possibile segnalare un problema con l'aggiornamento di hello?**</span><span class="sxs-lookup"><span data-stu-id="ac213-163">**How do I report an issue with hello upgrade?**</span></span>

<span data-ttu-id="ac213-164">Se si verificano eventuali errori durante l'aggiornamento di hello, notare l'ID operazione hello elencato in errore hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-164">If you experience any failures during hello upgrade, note hello operation ID that's listed in hello error.</span></span> <span data-ttu-id="ac213-165">Supporto Microsoft funzionerà in modo proattivo sulla risoluzione problema hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-165">Microsoft Support will proactively work on resolving hello issue.</span></span> <span data-ttu-id="ac213-166">È anche possibile contattare il team di supporto hello con l'ID sottoscrizione, nome insieme di credenziali e l'ID dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="ac213-166">You can also contact hello Support team with your subscription ID, vault name, and operation ID.</span></span> <span data-ttu-id="ac213-167">Supporto funzionerà problema hello tooresolve più rapidamente possibile.</span><span class="sxs-lookup"><span data-stu-id="ac213-167">Support will work tooresolve hello issue as quickly as possible.</span></span> <span data-ttu-id="ac213-168">Non ripetere l'operazione di hello a meno che non si è toodo in modo esplicito istruzioni riportata in questo caso da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ac213-168">Do not retry hello operation unless you are explicitly instructed toodo so by Microsoft.</span></span>

## <a name="run-hello-script"></a><span data-ttu-id="ac213-169">Eseguire script hello</span><span class="sxs-lookup"><span data-stu-id="ac213-169">Run hello script</span></span>

<span data-ttu-id="ac213-170">In PowerShell eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="ac213-170">In PowerShell, run hello following command:</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionID <subscriptionID>  -VaultName <vaultname> -Location <location> -ResourceType HyperVRecoveryManagerVault -TargetResourceGroupName <rgname>

* <span data-ttu-id="ac213-171">SubscriptionID: hello ID sottoscrizione associato a credenziali hello che si esegue l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-171">SubscriptionID: hello subscription ID that's associated with hello vault that you're upgrading.</span></span>

* <span data-ttu-id="ac213-172">VaultName: nome di hello dell'insieme di credenziali hello che si esegue l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-172">VaultName: hello name of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="ac213-173">: Hello posizione dell'insieme di credenziali hello che si esegue l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-173">Location: hello location of hello vault that you're upgrading.</span></span>

* <span data-ttu-id="ac213-174">ResourceType: HyperVRecoveryManagerVault per gli insiemi di credenziali di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="ac213-174">ResourceType: HyperVRecoveryManagerVault for Site Recovery vaults.</span></span>

* <span data-ttu-id="ac213-175">TargetResourceGroupName: gruppo di risorse hello in cui si desidera hello aggiornato toobe insieme di credenziali inserito.</span><span class="sxs-lookup"><span data-stu-id="ac213-175">TargetResourceGroupName: hello resource group into which you want hello upgraded vault toobe placed.</span></span> <span data-ttu-id="ac213-176">TargetResourceGroupName può essere un gruppo di risorse esistente in Azure Resource Manager o uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="ac213-176">TargetResourceGroupName can be an existing resource group in Azure Resource Manager or a new one.</span></span> <span data-ttu-id="ac213-177">Se hello TargetResourceGroupName fornito non esiste, viene creato come parte dell'aggiornamento hello in hello stessa località dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-177">If hello TargetResourceGroupName that's supplied does not exist, it is created as part of hello upgrade in hello same location as hello vault.</span></span> <span data-ttu-id="ac213-178">Per ulteriori informazioni, vedere sezione "Gruppi di risorse" hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).</span><span class="sxs-lookup"><span data-stu-id="ac213-178">For more information, see hello "Resource groups" section of [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md#resource-groups).</span></span>

    >[!NOTE]
    ><span data-ttu-id="ac213-179">Denominazione di gruppo di risorse è vincoli toocertain soggetto.</span><span class="sxs-lookup"><span data-stu-id="ac213-179">Resource group naming is subject toocertain constraints.</span></span> <span data-ttu-id="ac213-180">insieme di credenziali tooprevent aggiornare errore, essere attentamente che hello tooobserve convenzione di denominazione.</span><span class="sxs-lookup"><span data-stu-id="ac213-180">tooprevent vault upgrade failure, be sure tooobserve hello naming convention carefully.</span></span>
    >
    ><span data-ttu-id="ac213-181">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="ac213-181">For example:</span></span>
    >
    ><span data-ttu-id="ac213-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span><span class="sxs-lookup"><span data-stu-id="ac213-182">.\RecoveryServicesVaultUpgrade-1.0.0.ps1 -SubscriptionId 1234-54123-354354-56416-8645 -VaultName gen2dr -Location "north europe" -ResourceType hypervrecoverymanagervault -TargetResourceGroupName abc</span></span>

<span data-ttu-id="ac213-183">In alternativa, è possibile eseguire lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-183">Alternatively, you can run hello following script.</span></span> <span data-ttu-id="ac213-184">Per i parametri di hello richiesto, immettere i valori di hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-184">Enter hello values for hello required parameters.</span></span>

    PS > .\RecoveryServicesVaultUpgrade-1.0.0.ps1
    cmdlet RecoveryServicesVaultUpgrade-1.0.0.ps1 at command pipeline position 1

    Supply values for hello following parameters:
    SubscriptionId:
    VaultName:
    Location:
    ResourceType:
    TargetResourceGroupName:

1. <span data-ttu-id="ac213-185">Hello script di PowerShell richiesto è tooenter le credenziali.</span><span class="sxs-lookup"><span data-stu-id="ac213-185">hello PowerShell script prompts you tooenter your credentials.</span></span> <span data-ttu-id="ac213-186">Immetterli due volte, una volta per conto del modello di distribuzione classica hello e una volta per hello account di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac213-186">Enter them twice, once for hello classic deployment model account and once for hello Azure Resource Manager account.</span></span>

2. <span data-ttu-id="ac213-187">Dopo aver immesso le credenziali, script hello viene eseguito un toodetermine di controllo se il hello soddisfa il programma di installazione di infrastruttura indicato in precedenza requisiti.</span><span class="sxs-lookup"><span data-stu-id="ac213-187">After you've entered your credentials, hello script runs a check toodetermine whether your infrastructure setup meets hello previously mentioned requirements.</span></span>

3. <span data-ttu-id="ac213-188">Dopo prerequisiti hello sono stati verificati e confermati, si è tooproceed richiesta con l'aggiornamento dell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-188">After hello prerequisites have been checked and confirmed, you are prompted tooproceed with hello vault upgrade.</span></span> <span data-ttu-id="ac213-189">processo di aggiornamento Hello avvia l'insieme di credenziali di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="ac213-189">hello upgrade process starts upgrading your vault.</span></span> <span data-ttu-id="ac213-190">intero aggiornamento Hello può richiedere 15 too30 minuti toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ac213-190">hello entire upgrade can take 15 too30 minutes toocomplete.</span></span>

4. <span data-ttu-id="ac213-191">Dopo l'aggiornamento di hello è stata completata, è possibile accedere hello aggiornato dell'insieme di credenziali nel portale di Azure nuova hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-191">After hello upgrade has been completed successfully, you can access hello upgraded vault in hello new Azure portal.</span></span>

## <a name="post-upgrade-vault-management"></a><span data-ttu-id="ac213-192">Gestione dell'insieme di credenziali successiva all'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="ac213-192">Post-upgrade vault management</span></span>

### <a name="replicate-by-using-azure-site-recovery-in-hello-recovery-services-vault"></a><span data-ttu-id="ac213-193">La replica tramite Azure Site Recovery in hello che insieme di credenziali di servizi di ripristino</span><span class="sxs-lookup"><span data-stu-id="ac213-193">Replicate by using Azure Site Recovery in hello Recovery Services vault</span></span>

* <span data-ttu-id="ac213-194">È ora possibile proteggere le macchine virtuali di Azure da un'area tooanother.</span><span class="sxs-lookup"><span data-stu-id="ac213-194">You can now protect your Azure VMs from one region tooanother.</span></span> <span data-ttu-id="ac213-195">Per altre informazioni, vedere [Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery](site-recovery-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-195">For more information, see [Replicate Azure VMs between regions with Azure Site Recovery](site-recovery-azure-to-azure.md).</span></span>

* <span data-ttu-id="ac213-196">Per ulteriori informazioni sulla replica tooAzure le macchine virtuali VMware, vedere [tooAzure di replicare le macchine virtuali VMware con il ripristino del sito](vmware-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-196">For more information about replicating VMware VMs tooAzure, see [Replicate VMware VMs tooAzure with Site Recovery](vmware-walkthrough-overview.md).</span></span>

* <span data-ttu-id="ac213-197">Per ulteriori informazioni sulla replica tooAzure macchine virtuali Hyper-V (senza VMM), vedere [replica Hyper-V le macchine virtuali (senza VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-197">For more information about replicating Hyper-V VMs (without VMM) tooAzure, see [Replicate Hyper-V virtual machines (without VMM) tooAzure](hyper-v-site-walkthrough-overview.md).</span></span>

* <span data-ttu-id="ac213-198">Per ulteriori informazioni sulla replica tooAzure macchine virtuali Hyper-V (con VMM), vedere [hello di macchine virtuali di replica Hyper-V in VMM cloud tooAzure usando Site Recovery nel portale di Azure](vmm-to-azure-walkthrough-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-198">For more information about replicating Hyper-V VMs (with VMM) tooAzure, see [Replicate Hyper-V virtual machines in VMM clouds tooAzure using Site Recovery in hello Azure portal](vmm-to-azure-walkthrough-overview.md).</span></span>

* <span data-ttu-id="ac213-199">Per ulteriori informazioni sulla replica sito secondario tooa di Hyper-macchine virtuali (con VMM), vedere [hello di macchine virtuali di replica Hyper-V in VMM cloud tooa secondario VMM del sito utilizzando il portale di Azure](site-recovery-vmm-to-vmm.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-199">For more information about replicating Hyper-VMs (with VMM) tooa secondary site, see [Replicate Hyper-V virtual machines in VMM clouds tooa secondary VMM site using hello Azure portal](site-recovery-vmm-to-vmm.md).</span></span>

* <span data-ttu-id="ac213-200">Per ulteriori informazioni sulla replica sito secondario di tooa le macchine virtuali VMware, vedere [replica locale macchine virtuali VMware o un sito secondario di server fisici tooa nel portale di Azure classico hello](site-recovery-vmware-to-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-200">For more information about replicating VMware VMs tooa secondary site, see [Replicate on-premises VMware virtual machines or physical servers tooa secondary site in hello classic Azure portal](site-recovery-vmware-to-vmware.md).</span></span>

### <a name="view-your-replicated-items"></a><span data-ttu-id="ac213-201">Visualizzare gli elementi replicati</span><span class="sxs-lookup"><span data-stu-id="ac213-201">View your replicated items</span></span>

<span data-ttu-id="ac213-202">Hello immagine seguente mostra la pagina hello servizi di ripristino dell'insieme di credenziali dashboard che consente di visualizzare le entità di chiave per l'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="ac213-202">hello following image shows hello Recovery Services vault dashboard page that displays key entities for hello vault.</span></span> <span data-ttu-id="ac213-203">Selezionare un elenco di entità protetti nell'insieme di credenziali hello tooview **Site Recovery** > **gli elementi replicati**.</span><span class="sxs-lookup"><span data-stu-id="ac213-203">tooview a list of protected entities in hello vault, select **Site Recovery** > **Replicated items**.</span></span>


![Elementi replicati](./media/upgrade-site-recovery-vaults/replicateditems.png)

<span data-ttu-id="ac213-205">Hello immagine seguente viene illustrato del flusso di lavoro hello per la visualizzazione delle elementi replicati e hello **Failover** comando per avviare un failover.</span><span class="sxs-lookup"><span data-stu-id="ac213-205">hello following image shows hello workflow for viewing your replicated items and hello **Failover** command for initiating a failover.</span></span>

![Elementi replicati](./media/upgrade-site-recovery-vaults/failover.png)

### <a name="view-your-replication-settings"></a><span data-ttu-id="ac213-207">Visualizzare le impostazioni di replica</span><span class="sxs-lookup"><span data-stu-id="ac213-207">View your replication settings</span></span>

<span data-ttu-id="ac213-208">Nell'insieme di credenziali Site Recovery hello ogni gruppo protezione dati è configurato con la frequenza di copia, conservazione del punto di ripristino, frequenza di snapshot coerenti dell'applicazione e altre impostazioni di replica.</span><span class="sxs-lookup"><span data-stu-id="ac213-208">In hello Site Recovery vault, each protection group is configured with copy frequency, recovery point retention, frequency of application consistent snapshots, and other replication settings.</span></span> <span data-ttu-id="ac213-209">Nell'insieme di credenziali di hello servizi di ripristino, queste impostazioni sono configurate come un criterio di replica.</span><span class="sxs-lookup"><span data-stu-id="ac213-209">In hello Recovery Services vault, these settings are configured as a replication policy.</span></span> <span data-ttu-id="ac213-210">nome di Hello del criterio di hello è il nome di hello del gruppo protezione dati hello o hello *primarycloud_Policy*.</span><span class="sxs-lookup"><span data-stu-id="ac213-210">hello name of hello policy is hello name of hello protection group or hello *primarycloud_Policy*.</span></span>

<span data-ttu-id="ac213-211">Per ulteriori informazioni sui criteri di replica, vedere [gestire criteri di replica per VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="ac213-211">For more information about replication policy, see [Manage replication policy for VMware tooAzure](site-recovery-setup-replication-settings-vmware.md).</span></span>
