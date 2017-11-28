---
title: aaaSet backup hello origine e di destinazione per il sito secondario di Hyper-V replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset up origine hello e di destinazione quando la replica delle macchine virtuali Hyper-V toosecondary VMM del sito con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a><span data-ttu-id="51619-103">Passaggio 6: Configurare hello replica origine e destinazione</span><span class="sxs-lookup"><span data-stu-id="51619-103">Step 6: Set up hello replication source and target</span></span>


<span data-ttu-id="51619-104">Dopo la creazione di servizi di ripristino di un insieme di credenziali per Hyper-V replica tooa VMM sito secondario con [Azure Site Recovery](site-recovery-overview.md), utilizzare questo tooset articolo codice sorgente hello e percorsi di replica di destinazione.</span><span class="sxs-lookup"><span data-stu-id="51619-104">After creating a Recovery Services vault for Hyper-V replication tooa secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article tooset up hello source and target replication locations.</span></span> 

<span data-ttu-id="51619-105">Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="51619-105">After reading this article, post any comments at hello bottom, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-hello-source-environment"></a><span data-ttu-id="51619-106">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="51619-106">Set up hello source environment</span></span>

<span data-ttu-id="51619-107">Installare il Provider di Azure Site Recovery hello nei server VMM, individuare e registrare i server nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="51619-107">Install hello Azure Site Recovery Provider on VMM servers, and discover and register servers in hello vault.</span></span>

1. <span data-ttu-id="51619-108">Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="51619-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="51619-110">In **origine Prepare**, fare clic su **+ VMM** tooadd un server VMM.</span><span class="sxs-lookup"><span data-stu-id="51619-110">In **Prepare source**, click **+ VMM** tooadd a VMM server.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="51619-112">In **Aggiungi Server**, verificare che **server System Center VMM** viene visualizzato **tipo Server** e tale server VMM hello soddisfa hello [prerequisiti](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="51619-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that hello VMM server meets hello [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="51619-113">Scaricare i file di installazione di Provider di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="51619-113">Download hello Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="51619-114">Scaricare la chiave di registrazione hello.</span><span class="sxs-lookup"><span data-stu-id="51619-114">Download hello registration key.</span></span> <span data-ttu-id="51619-115">che sarà necessaria durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="51619-115">You need this when you run setup.</span></span> <span data-ttu-id="51619-116">chiave di Hello è valida per cinque giorni dopo la generazione è.</span><span class="sxs-lookup"><span data-stu-id="51619-116">hello key is valid for five days after you generate it.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="51619-118">Installare hello Provider di Azure Site Recovery nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="51619-118">Install hello Azure Site Recovery Provider on hello VMM server.</span></span> <span data-ttu-id="51619-119">Non è necessario tooexplicitly installa alcun componente nel server host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="51619-119">You don't need tooexplicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-hello-azure-site-recovery-provider"></a><span data-ttu-id="51619-120">Installare il Provider di Azure Site Recovery hello</span><span class="sxs-lookup"><span data-stu-id="51619-120">Install hello Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="51619-121">Eseguire i file di installazione di Provider di hello in ogni server VMM.</span><span class="sxs-lookup"><span data-stu-id="51619-121">Run hello Provider setup file on each VMM server.</span></span> <span data-ttu-id="51619-122">Se VMM è distribuito in un cluster, eseguire hello seguente hello prima fase di che installazione:</span><span class="sxs-lookup"><span data-stu-id="51619-122">If VMM is deployed in a cluster, do hello following hello first time you install:</span></span>
    -  <span data-ttu-id="51619-123">Installare il provider di hello in un nodo attivo e fine server VMM nell'insieme di credenziali hello hello installazione tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="51619-123">Install hello provider on an active node, and finish hello installation tooregister hello VMM server in hello vault.</span></span>
    - <span data-ttu-id="51619-124">Quindi, installare Provider hello in hello altri nodi.</span><span class="sxs-lookup"><span data-stu-id="51619-124">Then, install hello Provider on hello other nodes.</span></span> <span data-ttu-id="51619-125">I nodi del cluster devono tutti eseguire hello stessa versione di hello Provider.</span><span class="sxs-lookup"><span data-stu-id="51619-125">Cluster nodes should all run hello same version of hello Provider.</span></span>
2. <span data-ttu-id="51619-126">Il programma di installazione esegue alcuni controlli dei prerequisiti e le richieste di servizio VMM hello toostop di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="51619-126">Setup runs a few prerequisite checks, and requests permission toostop hello VMM service.</span></span> <span data-ttu-id="51619-127">Hello servizio VMM verrà riavviato automaticamente al completamento dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="51619-127">hello VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="51619-128">Se si installa in un cluster VMM, si è il ruolo Cluster hello toostop richiesta.</span><span class="sxs-lookup"><span data-stu-id="51619-128">If you install on a VMM cluster, you're prompted toostop hello Cluster role.</span></span>
3. <span data-ttu-id="51619-129">In **Microsoft Update**, è possibile acconsentire esplicitamente toospecify che rispetti i criteri di Microsoft Update sono installati gli aggiornamenti di provider.</span><span class="sxs-lookup"><span data-stu-id="51619-129">In **Microsoft Update**, you can opt in toospecify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="51619-130">In **installazione**, accettare o modificare il percorso di installazione predefinito hello e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="51619-130">In **Installation**, accept or modify hello default installation location, and click **Install**.</span></span>

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="51619-132">Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="51619-132">After installation is complete, click **Register** tooregister hello server in hello vault.</span></span>

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="51619-134">In **nome insieme di credenziali**, verificare il nome di hello dell'insieme di credenziali hello in cui hello server verrà registrato.</span><span class="sxs-lookup"><span data-stu-id="51619-134">In **Vault name**, verify hello name of hello vault in which hello server will be registered.</span></span> <span data-ttu-id="51619-135">Fare clic su *Avanti*.</span><span class="sxs-lookup"><span data-stu-id="51619-135">Click *Next*.</span></span>

    ![Server registration](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="51619-137">In **connessione Internet**, specificare la modalità di connessione tooAzure provider hello in esecuzione nel server VMM hello.</span><span class="sxs-lookup"><span data-stu-id="51619-137">In **Internet Connection**, specify how hello provider running on hello VMM server connects tooAzure.</span></span>

    ![Internet Settings](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="51619-139">È possibile specificare tale provider hello devono connettersi direttamente toohello internet, o tramite un proxy.</span><span class="sxs-lookup"><span data-stu-id="51619-139">You can specify that hello provider should connect directly toohello internet, or via a proxy.</span></span>
   - <span data-ttu-id="51619-140">Se necessario, specificare le impostazioni proxy.</span><span class="sxs-lookup"><span data-stu-id="51619-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="51619-141">Se si usa un proxy, un account RunAs VMM (DRAProxyAccount) viene creato automaticamente tramite hello specificato le credenziali del proxy.</span><span class="sxs-lookup"><span data-stu-id="51619-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using hello specified proxy credentials.</span></span> <span data-ttu-id="51619-142">Configurare il server proxy hello in modo che questo account può autenticare correttamente.</span><span class="sxs-lookup"><span data-stu-id="51619-142">Configure hello proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="51619-143">Hello impostazioni dell'account RunAs possono essere modificate nella console VMM hello > **impostazioni** > **sicurezza** > **account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="51619-143">hello RunAs account settings can be modified in hello VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="51619-144">Riavviare le modifiche tooupdate di servizio VMM hello.</span><span class="sxs-lookup"><span data-stu-id="51619-144">Restart hello VMM service tooupdate changes.</span></span>
8. <span data-ttu-id="51619-145">In **chiave di registrazione**selezionare chiave hello quello scaricato da Azure Site Recovery e copiato toohello server VMM.</span><span class="sxs-lookup"><span data-stu-id="51619-145">In **Registration Key**, select hello key that you downloaded from Azure Site Recovery and copied toohello VMM server.</span></span>
9. <span data-ttu-id="51619-146">impostazione di crittografia Hello viene utilizzato solo quando si esegue la replica di macchine virtuali Hyper-V in VMM cloud tooAzure.</span><span class="sxs-lookup"><span data-stu-id="51619-146">hello encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds tooAzure.</span></span> <span data-ttu-id="51619-147">Se si esegue la replica del sito secondario tooa non utilizzato.</span><span class="sxs-lookup"><span data-stu-id="51619-147">If you're replicating tooa secondary site it's not used.</span></span>
10. <span data-ttu-id="51619-148">In **nome Server**, specificare un server di nome descrittivo tooidentify hello VMM nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="51619-148">In **Server name**, specify a friendly name tooidentify hello VMM server in hello vault.</span></span> <span data-ttu-id="51619-149">In una configurazione cluster specificare il nome del ruolo cluster VMM hello.</span><span class="sxs-lookup"><span data-stu-id="51619-149">In a cluster configuration specify hello VMM cluster role name.</span></span>
11. <span data-ttu-id="51619-150">In **Sincronizza metadati cloud**, selezionare se si desidera toosynchronize metadati per tutti i cloud nel server VMM hello con insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="51619-150">In **Synchronize cloud metadata**, select whether you want toosynchronize metadata for all clouds on hello VMM server with hello vault.</span></span> <span data-ttu-id="51619-151">Questa azione deve solo toohappen una volta in ogni server.</span><span class="sxs-lookup"><span data-stu-id="51619-151">This action only needs toohappen once on each server.</span></span> <span data-ttu-id="51619-152">Se non si desidera toosynchronize tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM hello hello.</span><span class="sxs-lookup"><span data-stu-id="51619-152">If you don't want toosynchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in hello cloud properties in hello VMM console.</span></span>
12. <span data-ttu-id="51619-153">Fare clic su **Avanti** processo hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="51619-153">Click **Next** toocomplete hello process.</span></span> <span data-ttu-id="51619-154">Dopo la registrazione, i metadati dal server VMM hello vengono recuperati da Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="51619-154">After registration, metadata from hello VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="51619-155">server Hello viene visualizzato nella hello **server VMM** scheda hello **server** pagina nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="51619-155">hello server is displayed on hello **VMM Servers** tab on hello **Servers** page in hello vault.</span></span>

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="51619-157">Dopo che il server di hello è disponibile nella console di Site Recovery, hello in **origine** > **origine Prepare** selezionare hello VMM server e cloud selezionare hello in cui hello Hyper-V host si trova.</span><span class="sxs-lookup"><span data-stu-id="51619-157">After hello server is available in hello Site Recovery console, in **Source** > **Prepare source** select hello VMM server, and select hello cloud in which hello Hyper-V host is located.</span></span> <span data-ttu-id="51619-158">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="51619-158">Then click **OK**.</span></span>

<span data-ttu-id="51619-159">È anche possibile installare il provider di hello dalla riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="51619-159">You can also install hello provider from hello command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="51619-160">Configurare un ambiente di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="51619-160">Set up hello target environment</span></span>

<span data-ttu-id="51619-161">Selezionare i cloud e il server VMM di destinazione hello:</span><span class="sxs-lookup"><span data-stu-id="51619-161">Select hello target VMM server and cloud:</span></span>

1. <span data-ttu-id="51619-162">Fare clic su **Prepare infrastruttura** > **destinazione**e si desidera toouse server VMM di destinazione selezionare hello.</span><span class="sxs-lookup"><span data-stu-id="51619-162">Click **Prepare infrastructure** > **Target**, and select hello target VMM server you want toouse.</span></span>
2. <span data-ttu-id="51619-163">Verranno visualizzati i cloud nel server di hello sincronizzati con il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="51619-163">Clouds on hello server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="51619-164">Selezionare il cloud di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="51619-164">Select hello target cloud.</span></span>

   ![Destinazione](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="51619-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51619-166">Next steps</span></span>

<span data-ttu-id="51619-167">Andare troppo[passaggio 7: configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="51619-167">Go too[Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
