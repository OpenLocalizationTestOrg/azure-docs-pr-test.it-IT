---
title: Configurare l'origine e la destinazione per la replica Hyper-V in Azure (senza System Center VMM) con Azure Site Recovery| Microsoft Docs
description: Vengono riepilogati i passaggi per configurare le impostazioni di origine e di destinazione per la replica di VM Hyper-V in Archiviazione di Azure con Azure Site Recovery
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
ms.openlocfilehash: b38eb3a011d46f2239891ea1d1bcac2a4059a866
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-hyper-v-replication-to-azure"></a><span data-ttu-id="cd82c-103">Passaggio 8: Configurare l'origine e la destinazione per la replica Hyper-V in Azure</span><span class="sxs-lookup"><span data-stu-id="cd82c-103">Step 8: Set up the source and target for Hyper-V replication to Azure</span></span>

<span data-ttu-id="cd82c-104">Questo articolo illustra come configurare le impostazioni di origine e di destinazione per la replica di macchine virtuali Hyper-V locali (senza System Center VMM) in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cd82c-104">This article describes how to configure source and target settings when replicating on-premises Hyper-V virtual machines (without System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="cd82c-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cd82c-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="cd82c-106">Configurare l'ambiente di origine</span><span class="sxs-lookup"><span data-stu-id="cd82c-106">Set up the source environment</span></span>

<span data-ttu-id="cd82c-107">Configurare il sito Hyper-V, installare il provider di Azure Site Recovery e l'agente di Servizi di ripristino di Azure negli host Hyper-V e registrare il sito nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="cd82c-107">Set up the Hyper-V site, install the Azure Site Recovery Provider and the Azure Recovery Services agent on Hyper-V hosts, and register the site in the vault.</span></span>

1. <span data-ttu-id="cd82c-108">In **Preparare l'infrastruttura** fare clic su **Origine**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-108">In **Prepare Infrastructure**, click **Source**.</span></span> <span data-ttu-id="cd82c-109">Per aggiungere un nuovo sito Hyper-V come contenitore per i cluster o gli host Hyper-V, fare clic su **+ Sito Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-109">To add a new Hyper-V site as a container for your Hyper-V hosts or clusters, click **+Hyper-V Site**.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source1.png)
2. <span data-ttu-id="cd82c-111">In **Crea il sito Hyper-V** specificare un nome per il sito.</span><span class="sxs-lookup"><span data-stu-id="cd82c-111">In **Create Hyper-V site**, specify a name for the site.</span></span> <span data-ttu-id="cd82c-112">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-112">Then click **OK**.</span></span> <span data-ttu-id="cd82c-113">A questo punto, selezionare il sito creato e fare clic su **+Server Hyper-V** per aggiungere un server al sito.</span><span class="sxs-lookup"><span data-stu-id="cd82c-113">Now, select the site you created, and click **+Hyper-V Server** to add a server to the site.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source2.png)

3. <span data-ttu-id="cd82c-115">In **Aggiungi server** > **Tipo di server** verificare che sia visualizzato **Server Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-115">In **Add Server** > **Server type**, check that **Hyper-V server** is displayed.</span></span>

    - <span data-ttu-id="cd82c-116">Verificare che il server Hyper-V che si desidera aggiungere sia conforme ai [prerequisiti](#on-premises-prerequisites) e sia in grado di accedere agli URL specificati.</span><span class="sxs-lookup"><span data-stu-id="cd82c-116">Make sure that the Hyper-V server you want to add complies with the [prerequisites](#on-premises-prerequisites), and is able to access the specified URLs.</span></span>
    - <span data-ttu-id="cd82c-117">Scaricare il file di installazione del provider di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cd82c-117">Download the Azure Site Recovery Provider installation file.</span></span> <span data-ttu-id="cd82c-118">Eseguire questo file per installare il provider e l'agente di Servizi di ripristino in ogni host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cd82c-118">You run this file to install the Provider and the Recovery Services agent on each Hyper-V host.</span></span>

    ![Impostare l'origine](./media/hyper-v-site-walkthrough-source-target/set-source3.png)


## <a name="install-the-provider-and-agent"></a><span data-ttu-id="cd82c-120">Installare provider e agente</span><span class="sxs-lookup"><span data-stu-id="cd82c-120">Install the Provider and agent</span></span>

1. <span data-ttu-id="cd82c-121">Eseguire il file di installazione del provider in ogni host aggiunto al sito Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cd82c-121">Run the Provider setup file on each host you added to the Hyper-V site.</span></span> <span data-ttu-id="cd82c-122">Se l'installazione viene eseguita in un cluster Hyper-V, eseguire il file di installazione in ogni nodo del cluster.</span><span class="sxs-lookup"><span data-stu-id="cd82c-122">If you're installing on a Hyper-V cluster, run setup on each cluster node.</span></span> <span data-ttu-id="cd82c-123">L'installazione e la registrazione di ogni nodo del cluster Hyper-V garantisce che le macchine virtuali siano protette anche se ne viene eseguita la migrazione tra i nodi.</span><span class="sxs-lookup"><span data-stu-id="cd82c-123">Installing and registering each Hyper-V cluster node ensures that VMs are protected, even if they migrate across nodes.</span></span>
2. <span data-ttu-id="cd82c-124">In **Microsoft Update** è possibile acconsentire esplicitamente agli aggiornamenti in modo che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="cd82c-124">In **Microsoft Update**, you can opt in for updates so that Provider updates are installed in accordance with your Microsoft Update policy.</span></span>
3. <span data-ttu-id="cd82c-125">In **Installazione** accettare o modificare il percorso predefinito di installazione del provider e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-125">In **Installation**, accept or modify the default Provider installation location and click **Install**.</span></span>
4. <span data-ttu-id="cd82c-126">In **Impostazioni dell'insieme di credenziali** fare clic su **Esplora** per selezionare il file di chiave dell'insieme di credenziali scaricato.</span><span class="sxs-lookup"><span data-stu-id="cd82c-126">In **Vault Settings**, click **Browse** to select the vault key file that you downloaded.</span></span> <span data-ttu-id="cd82c-127">Specificare la sottoscrizione di Azure Site Recovery, il nome dell'insieme di credenziali e il sito Hyper-V a cui appartiene il server Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cd82c-127">Specify the Azure Site Recovery subscription, the vault name, and the Hyper-V site to which the Hyper-V server belongs.</span></span>

    ![Server registration](./media/hyper-v-site-walkthrough-source-target/provider3.png)

5. <span data-ttu-id="cd82c-129">In **Impostazioni proxy** specificare in che modo il provider in esecuzione negli host Hyper-V si connette ad Azure Site Recovery tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="cd82c-129">In **Proxy Settings**, specify how the Provider running on Hyper-V hosts connects to Azure Site Recovery over the internet.</span></span>

    * <span data-ttu-id="cd82c-130">Per fare in modo che il provider si connetta direttamente, selezionare **Connetti direttamente ad Azure Site Recovery senza server proxy**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-130">If you want the Provider to connect directly select **Connect directly to Azure Site Recovery without a proxy**.</span></span>
    * <span data-ttu-id="cd82c-131">Se per il proxy esistente è necessaria l'autenticazione o si desidera usare un proxy personalizzato per la connessione al provider, selezionare **Connetti ad Azure Site Recovery usando un server proxy**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-131">If your existing proxy requires authentication, or you want to use a custom proxy for the Provider connection, select **Connect to Azure Site Recovery using a proxy server**.</span></span>
    * <span data-ttu-id="cd82c-132">Se si usa un proxy:</span><span class="sxs-lookup"><span data-stu-id="cd82c-132">If you use a proxy:</span></span>
        - <span data-ttu-id="cd82c-133">Specificare l'indirizzo, la porta e le credenziali.</span><span class="sxs-lookup"><span data-stu-id="cd82c-133">Specify the address, port, and credentials</span></span>
        - <span data-ttu-id="cd82c-134">Assicurarsi che sia possibile accedere tramite il proxy agli URL indicati nei [prerequisiti](#prerequisites) .</span><span class="sxs-lookup"><span data-stu-id="cd82c-134">Make sure the URLs described in the [prerequisites](#prerequisites) are allowed through the proxy.</span></span>

    ![Internet](./media/hyper-v-site-walkthrough-source-target/provider7.png)

6. <span data-ttu-id="cd82c-136">Al termine dell'installazione fare clic su **Registra** per registrare il server nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="cd82c-136">After installation finishes, click **Register** to register the server in the vault.</span></span>

    ![Percorso di installazione](./media/hyper-v-site-walkthrough-source-target/provider2.png)

7. <span data-ttu-id="cd82c-138">Al termine della registrazione, i metadati del server Hyper-V vengono recuperati da Azure Site Recovery e il server viene visualizzato in **Site Recovery Infrastructure** >  (Infrastruttura di Site Recovery)**Hyper-V Hosts** (Host Hyper-V).</span><span class="sxs-lookup"><span data-stu-id="cd82c-138">After registration finishes, metadata from the Hyper-V server is retrieved by Azure Site Recovery, and the server is displayed in **Site Recovery Infrastructure** > **Hyper-V Hosts**.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="cd82c-139">Configurare l'ambiente di destinazione</span><span class="sxs-lookup"><span data-stu-id="cd82c-139">Set up the target environment</span></span>

<span data-ttu-id="cd82c-140">Specificare l'account di archiviazione di Azure per la replica e la rete di Azure a cui le macchine virtuali di Azure dovranno connettersi dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="cd82c-140">Specify the Azure storage account for replication, and the Azure network to which Azure VMs will connect after failover.</span></span>

1. <span data-ttu-id="cd82c-141">Fare clic su **Preparare l'infrastruttura** > **Destinazione**.</span><span class="sxs-lookup"><span data-stu-id="cd82c-141">Click **Prepare infrastructure** > **Target**.</span></span>
2. <span data-ttu-id="cd82c-142">Selezionare la sottoscrizione e il gruppo di risorse in cui si desidera creare le macchine virtuali di Azure dopo il failover.</span><span class="sxs-lookup"><span data-stu-id="cd82c-142">Select the subscription and the resource group in which you want to create the Azure VMs after failover.</span></span> <span data-ttu-id="cd82c-143">Scegliere il modello di distribuzione (classica o Resource Manager) da usare in Azure per le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="cd82c-143">Choose the deployment model that you want to use in Azure (classic or resource management) for the VMs.</span></span>

3. <span data-ttu-id="cd82c-144">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="cd82c-144">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

    - <span data-ttu-id="cd82c-145">Se non si dispone di un account di archiviazione, fare clic su **+ Archiviazione** per creare un account basato su Resource Manager inline.</span><span class="sxs-lookup"><span data-stu-id="cd82c-145">If you don't have a storage account, click **+Storage** to create a Resource Manager-based account inline.</span></span> 
    - <span data-ttu-id="cd82c-146">Se non si dispone di una rete Azure, fare clic su **+Rete** per creare una rete basata su Resource Manager inline.</span><span class="sxs-lookup"><span data-stu-id="cd82c-146">If you don't have a Azure network, click **+Network** to create a Resource Manager-based network inline.</span></span>






## <a name="next-steps"></a><span data-ttu-id="cd82c-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cd82c-147">Next steps</span></span>

<span data-ttu-id="cd82c-148">Andare al [Passaggio 9: Configurare i criteri di replica](hyper-v-site-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cd82c-148">Go to [Step 9: Set up a replication policy](hyper-v-site-walkthrough-replication.md)</span></span>
