---
title: Configurare l'origine e la destinazione per la replica Hyper-V in un sito secondario con Azure Site Recovery | Microsoft Docs
description: Descrive come configurare l'origine e la destinazione durante la replica di VM Hyper-V in un sito VMM secondario con Azure Site Recovery.
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
ms.openlocfilehash: 07135e9b5e619971a59cc22ec68a0a4e8bcaabe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-set-up-the-replication-source-and-target"></a><span data-ttu-id="089dd-103">Passaggio 6: Configurare l'origine e la destinazione della replica</span><span class="sxs-lookup"><span data-stu-id="089dd-103">Step 6: Set up the replication source and target</span></span>


<span data-ttu-id="089dd-104">Dopo la creazione di un insieme di credenziali di Servizi di ripristino per la replica Hyper-V in un sito VMM secondario con [Azure Site Recovery](site-recovery-overview.md), usare le istruzioni disponibili in questo articolo per configurare le posizioni di origine e di destinazione della replica.</span><span class="sxs-lookup"><span data-stu-id="089dd-104">After creating a Recovery Services vault for Hyper-V replication to a secondary VMM site with [Azure Site Recovery](site-recovery-overview.md), use this article to set up the source and target replication locations.</span></span> 

<span data-ttu-id="089dd-105">È possibile inviare commenti nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="089dd-105">After reading this article, post any comments at the bottom, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="set-up-the-source-environment"></a><span data-ttu-id="089dd-106">Configurare l'ambiente di origine</span><span class="sxs-lookup"><span data-stu-id="089dd-106">Set up the source environment</span></span>

<span data-ttu-id="089dd-107">Installare il provider di Azure Site Recovery nei server VMM, rilevare e registrare il server nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-107">Install the Azure Site Recovery Provider on VMM servers, and discover and register servers in the vault.</span></span>

1. <span data-ttu-id="089dd-108">Fare clic su **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="089dd-108">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. <span data-ttu-id="089dd-110">In **Prepara origine** fare clic su **+ VMM** per aggiungere un server VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-110">In **Prepare source**, click **+ VMM** to add a VMM server.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. <span data-ttu-id="089dd-112">In **Aggiungi server** verificare che in **Tipo di server** sia visualizzato **System Center VMM server** (Server System Center VMM) e che il server VMM sia conforme ai [prerequisiti](#prerequisites).</span><span class="sxs-lookup"><span data-stu-id="089dd-112">In **Add Server**, check that **System Center VMM server** appears in **Server type** and that the VMM server meets the [prerequisites](#prerequisites).</span></span>
4. <span data-ttu-id="089dd-113">Scaricare il file di installazione del provider di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="089dd-113">Download the Azure Site Recovery Provider installation file.</span></span>
5. <span data-ttu-id="089dd-114">Scaricare la chiave di registrazione,</span><span class="sxs-lookup"><span data-stu-id="089dd-114">Download the registration key.</span></span> <span data-ttu-id="089dd-115">che sarà necessaria durante l'installazione.</span><span class="sxs-lookup"><span data-stu-id="089dd-115">You need this when you run setup.</span></span> <span data-ttu-id="089dd-116">La chiave è valida per cinque giorni dal momento in cui viene generata.</span><span class="sxs-lookup"><span data-stu-id="089dd-116">The key is valid for five days after you generate it.</span></span>

    ![Impostare l'origine](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. <span data-ttu-id="089dd-118">Installare il provider di Azure Site Recovery nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-118">Install the Azure Site Recovery Provider on the VMM server.</span></span> <span data-ttu-id="089dd-119">Nei server host Hyper-V non è necessario installare niente in modo esplicito.</span><span class="sxs-lookup"><span data-stu-id="089dd-119">You don't need to explicitly install anything on Hyper-V host servers.</span></span>


## <a name="install-the-azure-site-recovery-provider"></a><span data-ttu-id="089dd-120">Installare il provider di Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="089dd-120">Install the Azure Site Recovery Provider</span></span>

1. <span data-ttu-id="089dd-121">Eseguire il file di installazione del provider in ogni server VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-121">Run the Provider setup file on each VMM server.</span></span> <span data-ttu-id="089dd-122">Se VMM viene distribuito in un cluster, procedere come segue per la prima installazione:</span><span class="sxs-lookup"><span data-stu-id="089dd-122">If VMM is deployed in a cluster, do the following the first time you install:</span></span>
    -  <span data-ttu-id="089dd-123">Installare il provider in un nodo attivo e completare l'installazione per registrare il server VMM nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-123">Install the provider on an active node, and finish the installation to register the VMM server in the vault.</span></span>
    - <span data-ttu-id="089dd-124">Quindi, installare il provider negli altri nodi.</span><span class="sxs-lookup"><span data-stu-id="089dd-124">Then, install the Provider on the other nodes.</span></span> <span data-ttu-id="089dd-125">Tutti i nodi del cluster devono eseguire la stessa versione del provider.</span><span class="sxs-lookup"><span data-stu-id="089dd-125">Cluster nodes should all run the same version of the Provider.</span></span>
2. <span data-ttu-id="089dd-126">Il programma di installazione esegue alcune verifiche dei prerequisiti e chiede l'autorizzazione per arrestare il servizio VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-126">Setup runs a few prerequisite checks, and requests permission to stop the VMM service.</span></span> <span data-ttu-id="089dd-127">Il servizio VMM verrà riavviato automaticamente al termine dell'installazione.</span><span class="sxs-lookup"><span data-stu-id="089dd-127">The VMM service will be restarted automatically when setup finishes.</span></span> <span data-ttu-id="089dd-128">Se si esegue l'installazione in un cluster VMM, verrà richiesto di interrompere il ruolo Cluster.</span><span class="sxs-lookup"><span data-stu-id="089dd-128">If you install on a VMM cluster, you're prompted to stop the Cluster role.</span></span>
3. <span data-ttu-id="089dd-129">In **Microsoft Update** è possibile acconsentire per specificare esplicitamente che gli aggiornamenti del provider vengano installati in base ai criteri di Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="089dd-129">In **Microsoft Update**, you can opt in to specify that provider updates are installed in accordance with your Microsoft Update policy.</span></span>
4. <span data-ttu-id="089dd-130">In **Installazione** accettare o modificare il percorso predefinito di installazione e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="089dd-130">In **Installation**, accept or modify the default installation location, and click **Install**.</span></span>

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. <span data-ttu-id="089dd-132">Al termine dell'installazione fare clic su **Registra** per registrare il server nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-132">After installation is complete, click **Register** to register the server in the vault.</span></span>

    ![Percorso di installazione](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. <span data-ttu-id="089dd-134">In **Vault name**verificare il nome dell'insieme di credenziali in cui verrà registrato il server.</span><span class="sxs-lookup"><span data-stu-id="089dd-134">In **Vault name**, verify the name of the vault in which the server will be registered.</span></span> <span data-ttu-id="089dd-135">Fare clic su *Avanti*.</span><span class="sxs-lookup"><span data-stu-id="089dd-135">Click *Next*.</span></span>

    ![Server registration](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. <span data-ttu-id="089dd-137">Nella pagina **Connessione Internet** specificare la modalità di connessione ad Azure del provider in esecuzione sul server VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-137">In **Internet Connection**, specify how the provider running on the VMM server connects to Azure.</span></span>

    ![Internet Settings](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - <span data-ttu-id="089dd-139">È possibile specificare che il provider debba connettersi direttamente a Internet o tramite un proxy.</span><span class="sxs-lookup"><span data-stu-id="089dd-139">You can specify that the provider should connect directly to the internet, or via a proxy.</span></span>
   - <span data-ttu-id="089dd-140">Se necessario, specificare le impostazioni proxy.</span><span class="sxs-lookup"><span data-stu-id="089dd-140">Specify proxy settings if needed.</span></span>
   - <span data-ttu-id="089dd-141">Se si usa un proxy, viene creato automaticamente un account RunAs di VMM (DRAProxyAccount) con le credenziali del proxy specificate.</span><span class="sxs-lookup"><span data-stu-id="089dd-141">If you use a proxy, a VMM RunAs account (DRAProxyAccount) is created automatically using the specified proxy credentials.</span></span> <span data-ttu-id="089dd-142">Configurare il server proxy in modo che l'account possa eseguire correttamente l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="089dd-142">Configure the proxy server so that this account can authenticate successfully.</span></span> <span data-ttu-id="089dd-143">È possibile modificare le impostazioni dell'account RunAs nella console di VMM > **Impostazioni** > **Sicurezza** > **Account RunAs**.</span><span class="sxs-lookup"><span data-stu-id="089dd-143">The RunAs account settings can be modified in the VMM console > **Settings** > **Security** > **Run As Accounts**.</span></span> <span data-ttu-id="089dd-144">Riavviare il servizio VMM per aggiornare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="089dd-144">Restart the VMM service to update changes.</span></span>
8. <span data-ttu-id="089dd-145">In **Chiave di registrazione**selezionare il codice di registrazione scaricato da Azure Site Recovery e copiato nel server VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-145">In **Registration Key**, select the key that you downloaded from Azure Site Recovery and copied to the VMM server.</span></span>
9. <span data-ttu-id="089dd-146">L'impostazione di crittografia viene usata solo quando si esegue la replica di VM Hyper-V in cloud VMM in Azure.</span><span class="sxs-lookup"><span data-stu-id="089dd-146">The encryption setting is only used when you're replicating Hyper-V VMs in VMM clouds to Azure.</span></span> <span data-ttu-id="089dd-147">Non viene usata se si esegue la replica in un sito secondario.</span><span class="sxs-lookup"><span data-stu-id="089dd-147">If you're replicating to a secondary site it's not used.</span></span>
10. <span data-ttu-id="089dd-148">In **Nome server**specificare un nome descrittivo per identificare il server VMM nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-148">In **Server name**, specify a friendly name to identify the VMM server in the vault.</span></span> <span data-ttu-id="089dd-149">In una configurazione cluster specificare il nome del ruolo relativo al cluster VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-149">In a cluster configuration specify the VMM cluster role name.</span></span>
11. <span data-ttu-id="089dd-150">In **Sincronizza i metadati cloud** scegliere se sincronizzare i metadati per tutti i cloud presenti nel server VMM con l'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-150">In **Synchronize cloud metadata**, select whether you want to synchronize metadata for all clouds on the VMM server with the vault.</span></span> <span data-ttu-id="089dd-151">È necessario eseguire questa azione solo una volta in ogni server.</span><span class="sxs-lookup"><span data-stu-id="089dd-151">This action only needs to happen once on each server.</span></span> <span data-ttu-id="089dd-152">Se non si vogliono sincronizzare tutti i cloud, è possibile lasciare deselezionata questa opzione e sincronizzare ogni cloud singolarmente nelle proprietà del cloud nella console VMM.</span><span class="sxs-lookup"><span data-stu-id="089dd-152">If you don't want to synchronize all clouds, you can leave this setting unchecked, and synchronize each cloud individually in the cloud properties in the VMM console.</span></span>
12. <span data-ttu-id="089dd-153">Fare clic su **Avanti** per completare il processo.</span><span class="sxs-lookup"><span data-stu-id="089dd-153">Click **Next** to complete the process.</span></span> <span data-ttu-id="089dd-154">Dopo la registrazione, i metadati del server VMM vengono recuperati da Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="089dd-154">After registration, metadata from the VMM server is retrieved by Azure Site Recovery.</span></span> <span data-ttu-id="089dd-155">Il server viene visualizzato nella scheda **Server VMM** della pagina **Server** nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="089dd-155">The server is displayed on the **VMM Servers** tab on the **Servers** page in the vault.</span></span>

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. <span data-ttu-id="089dd-157">Quando il server sarà disponibile nella console di Site Recovery, in **Origine** > **Prepara origine** selezionare il server VMM e quindi il cloud in cui si trova l'host Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="089dd-157">After the server is available in the Site Recovery console, in **Source** > **Prepare source** select the VMM server, and select the cloud in which the Hyper-V host is located.</span></span> <span data-ttu-id="089dd-158">Fare quindi clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="089dd-158">Then click **OK**.</span></span>

<span data-ttu-id="089dd-159">È anche possibile installare il provider dalla riga di comando:</span><span class="sxs-lookup"><span data-stu-id="089dd-159">You can also install the provider from the command line:</span></span>

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-the-target-environment"></a><span data-ttu-id="089dd-160">Configurare l'ambiente di destinazione</span><span class="sxs-lookup"><span data-stu-id="089dd-160">Set up the target environment</span></span>

<span data-ttu-id="089dd-161">Selezionare il server VMM di destinazione e il cloud:</span><span class="sxs-lookup"><span data-stu-id="089dd-161">Select the target VMM server and cloud:</span></span>

1. <span data-ttu-id="089dd-162">Fare clic su **Preparare l'infrastruttura** > **Destinazione** e selezionare il server VMM di destinazione da usare.</span><span class="sxs-lookup"><span data-stu-id="089dd-162">Click **Prepare infrastructure** > **Target**, and select the target VMM server you want to use.</span></span>
2. <span data-ttu-id="089dd-163">Verranno visualizzati i cloud nel server sincronizzati con Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="089dd-163">Clouds on the server that are synchronized with Site Recovery will be displayed.</span></span> <span data-ttu-id="089dd-164">Selezionare il cloud di destinazione.</span><span class="sxs-lookup"><span data-stu-id="089dd-164">Select the target cloud.</span></span>

   ![Destinazione](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a><span data-ttu-id="089dd-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="089dd-166">Next steps</span></span>

<span data-ttu-id="089dd-167">Andare al [Passaggio 7: Configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).</span><span class="sxs-lookup"><span data-stu-id="089dd-167">Go to [Step 7: Configure network mapping](vmm-to-vmm-walkthrough-network-mapping.md).</span></span>
