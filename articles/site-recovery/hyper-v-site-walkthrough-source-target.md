---
title: aaaSet backup hello origine e di destinazione per tooAzure di replica Hyper-V (senza System Center VMM) con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di macchine virtuali Hyper-V tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d2010d85-77fd-4dea-84f3-1c960ed4c63f
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 105b90e6ac053d5b842c54a36c460a26d0f5c2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-replication-tooazure"></a><span data-ttu-id="24b7d-103">Passaggio 8: Impostare hello origine e di destinazione per Hyper-V replica tooAzure</span><span class="sxs-lookup"><span data-stu-id="24b7d-103">Step 8: Set up hello source and target for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="24b7d-104">In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure macchine virtuali (senza System Center VMM) di Hyper-V, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="24b7d-104">This article describes how tooconfigure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="24b7d-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="24b7d-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="24b7d-106">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="24b7d-106">Set up hello source environment</span></span>

<span data-ttu-id="24b7d-107">Impostare il sito di hello Hyper-V, installare hello Provider di Azure Site Recovery e l'agente di servizi di ripristino di Azure di hello negli host Hyper-V e registrare sito hello nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-107">Set up hello Hyper-V site, install hello Azure Site Recovery Provider and hello Azure Recovery Services agent on Hyper-V hosts, and register hello site in hello vault.</span></span>

1. <span data-ttu-id="24b7d-108">In **Preparare l'infrastruttura** fare clic su **Origine**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="24b7d-109">Fare clic su un nuovo sito Hyper-V come contenitore per l'host Hyper-V o cluster, tooadd **+ sito Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-109">tooadd a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="24b7d-111">In **sito Hyper-V creare**, specificare un nome per il sito hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-111">In **Create Hyper-V site**, specify a name for hello site.</span></span> <span data-ttu-id="24b7d-112">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-112">Then click **OK**.</span></span> <span data-ttu-id="24b7d-113">Ora, selezionare il sito di hello creata, quindi fare clic su **+ Server Hyper-V** tooadd un sito di toohello server.</span><span class="sxs-lookup"><span data-stu-id="24b7d-113">Now, select hello site you created, and click **+Hyper-V Server** tooadd a server toohello site.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="24b7d-115">In **Aggiungi server** > **Tipo di server** verificare che sia visualizzato **Server Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="24b7d-116">Verificare che tale server hello Hyper-V da tooadd è conforme con hello [prerequisiti](#on-premises-prerequisites), ed è in grado di tooaccess hello URL specificati.</span><span class="sxs-lookup"><span data-stu-id="24b7d-116">Make sure that hello Hyper-V server you want tooadd complies with hello [prerequisites](#on-premises-prerequisites), and is able tooaccess hello specified URLs.</span></span>
    - <span data-ttu-id="24b7d-117">Scaricare i file di installazione di Provider di Azure Site Recovery hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-117">Download hello Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="24b7d-118">Eseguire questo hello tooinstall file Provider e hello agente servizi di ripristino in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="24b7d-118">You run this file tooinstall hello Provider and hello Recovery Services agent on each Hyper-V host.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-hello-provider-and-agent"></a><span data-ttu-id="24b7d-120">Installare hello Provider e agente</span><span class="sxs-lookup"><span data-stu-id="24b7d-120">Install hello Provider and agent</span></span>

1. <span data-ttu-id="24b7d-121">Eseguire i file di installazione di Provider di hello in ogni host aggiunti al sito toohello Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="24b7d-121">Run hello Provider setup file on each host you added toohello Hyper-V site.</span></span> <span data-ttu-id="24b7d-122">Se l'installazione viene eseguita in un cluster Hyper-V, eseguire il file di installazione in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="24b7d-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="24b7d-123">L'installazione e la registrazione di ogni nodo del cluster Hyper-V garantisce che le macchine virtuali siano protette anche se ne viene eseguita la migrazione tra i nodi.</span><span class="sxs-lookup"><span data-stu-id="24b7d-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="24b7d-124">In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="24b7d-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="24b7d-125">In **installazione**, accettare o modificare percorso di installazione di Provider predefinito hello e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-125">In **Installation**, accept or modify hello default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="24b7d-126">In **impostazioni insieme di credenziali**, fare clic su **Sfoglia** tooselect hello insieme di credenziali chiave file scaricato.</span><span class="sxs-lookup"><span data-stu-id="24b7d-126">In **Vault Settings**, click **Browse** tooselect hello vault key file that you downloaded.</span></span> <span data-ttu-id="24b7d-127">Specificare una sottoscrizione di Azure Site Recovery hello, nome di archivio, hello e hello Hyper-V del sito toowhich hello Hyper-V server appartiene.</span><span class="sxs-lookup"><span data-stu-id="24b7d-127">Specify hello Azure Site Recovery subscription, hello vault name, and hello Hyper-V site toowhich hello Hyper-V server belongs.</span></span>

    ![Server registration](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="24b7d-129">In **le impostazioni del Proxy**, specificare la modalità Provider in esecuzione in host Hyper-V si connette tooAzure Site Recovery tramite hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="24b7d-129">In **Proxy Settings**, specify how hello Provider running on Hyper-V hosts connects tooAzure Site Recovery over hello internet.</span></span>

    * <span data-ttu-id="24b7d-130">Se si desidera selezionare direttamente hello Provider tooconnect **connettersi direttamente tooAzure il ripristino del sito senza un proxy**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-130">If you want hello Provider tooconnect directly select **Connect directly tooAzure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="24b7d-131">Se il proxy esistente richiede l'autenticazione, o si desidera toouse un proxy personalizzato per la connessione al Provider di hello, selezionare **connettersi tooAzure ripristino del sito utilizzando un server proxy**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-131">If your existing proxy requires authentication, or you want toouse a custom proxy for hello Provider connection, select **Connect tooAzure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="24b7d-132">Se si usa un proxy:</span><span class="sxs-lookup"><span data-stu-id="24b7d-132">If you use a proxy:</span></span>
        - <span data-ttu-id="24b7d-133">Specificare le credenziali, porta e indirizzo hello</span><span class="sxs-lookup"><span data-stu-id="24b7d-133">Specify hello address, port, and credentials</span></span>
        - <span data-ttu-id="24b7d-134">Rendono che URL hello descritto in hello [prerequisiti](#prerequisites) siano consentiti attraverso il proxy di hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-134">Make sure hello URLs described in hello [prerequisites](#prerequisites) are allowed through hello proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="24b7d-136">Al termine dell'installazione, fare clic su **registrare** server hello tooregister nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-136">After installation finishes, click **Register** tooregister hello server in hello vault.</span></span>

    ![Percorso di installazione](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="24b7d-138">Al termine della registrazione, i metadati dal server hello Hyper-V vengono recuperati da Azure Site Recovery e hello server viene visualizzato nel **infrastruttura di Site Recovery** > **host Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-138">After registration finishes, metadata from hello Hyper-V server is retrieved by Azure Site Recovery, and hello server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="24b7d-139">Configurare un ambiente di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="24b7d-139">Set up hello target environment</span></span>

<span data-ttu-id="24b7d-140">Specificare l'account di archiviazione di Azure hello per la replica e si connetterà hello Azure rete toowhich macchine virtuali di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="24b7d-140">Specify hello Azure storage account for replication, and hello Azure network toowhich Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="24b7d-141">Fare clic su **Preparare l'infrastruttura** > **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="24b7d-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="24b7d-142">Selezionare la sottoscrizione hello e gruppo di risorse hello in cui si desidera toocreate hello macchine virtuali di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="24b7d-142">Select hello subscription and hello resource group in which you want toocreate hello Azure VMs after failover.</span></span> <span data-ttu-id="24b7d-143">Scegliere hello distribuzione modello che si vuole toouse in Azure (classica o risorsa di gestione) per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="24b7d-143">Choose hello deployment model that you want toouse in Azure (classic or resource management) for hello VMs.</span></span>

3. <span data-ttu-id="24b7d-144">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="24b7d-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="24b7d-145">Se non si dispone di un account di archiviazione, fare clic su **+ archiviazione** toocreate inline un account basato su Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="24b7d-145">If you don't have a storage account, click **+Storage** toocreate a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="24b7d-146">Se non si dispone di una rete di Azure, fare clic su **+ rete** toocreate un inline basate su Gestione risorse di rete.</span><span class="sxs-lookup"><span data-stu-id="24b7d-146">If you don't have a Azure network, click **+Network** toocreate a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="24b7d-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="24b7d-147">Next steps</span></span>

<span data-ttu-id="24b7d-148">Andare troppo[passaggio 9: configurare un criterio di replica](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="24b7d-148">Go too[Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
