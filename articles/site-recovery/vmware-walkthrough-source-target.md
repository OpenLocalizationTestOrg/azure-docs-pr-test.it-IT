---
title: Impostare l'origine e destinazione per la replica VMware in Azure con Azure Site Recovery | Microsoft Docs
description: Riepilogo dei passaggi per configurare le impostazioni di origine e destinazione per la replica delle macchine virtuali VMware nell'archiviazione di Azure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="335b2-103">Passaggio 8: Configurare l'origine e la destinazione per la replica VMware in Azure</span><span class="sxs-lookup"><span data-stu-id="335b2-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="335b2-104">Questo articolo illustra come configurare impostazioni di origine e destinazione per la replica di macchine virtuali VMware locali in Azure usando il servizio [Azure Site Recovery](site-recovery-overview.md) nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="335b2-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="335b2-105">Inserire commenti e domande nella parte inferiore di questo articolo oppure nel [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="335b2-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="335b2-106">Configurare l'ambiente di origine</span><span class="sxs-lookup"><span data-stu-id="335b2-106">Set up the source environment</span></span>

<span data-ttu-id="335b2-107">Configurare il server di configurazione, registrarlo nell'insieme di credenziali e individuare le VM.</span><span class="sxs-lookup"><span data-stu-id="335b2-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="335b2-108">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="335b2-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="335b2-109">Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="335b2-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="335b2-110">In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="335b2-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="335b2-111">Scaricare il file di installazione per l'Installazione unificata di Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="335b2-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="335b2-112">Scaricare la chiave di registrazione dell'insieme di credenziali,</span><span class="sxs-lookup"><span data-stu-id="335b2-112">Download the vault registration key.</span></span> <span data-ttu-id="335b2-113">che sarà necessaria quando si esegue l'Installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="335b2-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="335b2-114">La chiave è valida per cinque giorni dal momento in cui viene generata.</span><span class="sxs-lookup"><span data-stu-id="335b2-114">The key is valid for five days after you generate it.</span></span>

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="335b2-116">Registrare il server di configurazione nell'insieme di credenziali</span><span class="sxs-lookup"><span data-stu-id="335b2-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="335b2-117">Seguire questa procedura prima di iniziare, quindi eseguire l'Installazione unificata per installare il server di configurazione, il server di elaborazione e il server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="335b2-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="335b2-118">Ottenere una breve panoramica video</span><span class="sxs-lookup"><span data-stu-id="335b2-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="335b2-119">Nella VM del server di configurazione verificare che il clock di sistema sia sincronizzato con un [server di riferimento ora](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="335b2-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="335b2-120">Deve corrispondere.</span><span class="sxs-lookup"><span data-stu-id="335b2-120">It should match.</span></span> <span data-ttu-id="335b2-121">Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="335b2-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="335b2-122">Eseguire l'installazione come amministratore locale nella VM del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="335b2-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="335b2-123">Verificare che nella VM sia abilitato TLS 1.0.</span><span class="sxs-lookup"><span data-stu-id="335b2-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="335b2-124">Il server di configurazione può essere installato anche [dalla riga di comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="335b2-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="335b2-125">Connettersi ai server VMware</span><span class="sxs-lookup"><span data-stu-id="335b2-125">Connect to VMware servers</span></span>

<span data-ttu-id="335b2-126">Per consentire ad Azure Site Recovery di individuare macchine virtuali in esecuzione nell'ambiente locale, è necessario connettere il server VMware vCenter o gli host vSphere ESXi a Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="335b2-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="335b2-127">Prima di iniziare tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="335b2-127">Note the following before you start:</span></span>

- <span data-ttu-id="335b2-128">Se si aggiungono gli host vSphere o il server vCenter a Site Recovery con un account senza privilegi Administrator per il server, per l'account devono essere abilitati i privilegi seguenti:</span><span class="sxs-lookup"><span data-stu-id="335b2-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="335b2-129">Datacenter (Data center), Datastore (Archivio dati), Folder (Cartella), Host, Network (Rete), Resource (Risorsa), Virtual machine (Macchina virtuale) e vSphere Distributed Switch (Switch distribuito vSphere).</span><span class="sxs-lookup"><span data-stu-id="335b2-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="335b2-130">Per il server vCenter sono necessarie le autorizzazioni Storage views (Viste archiviazione).</span><span class="sxs-lookup"><span data-stu-id="335b2-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="335b2-131">Quando si aggiungono server VMware a Site Recovery possono trascorrere 15 o più minuti prima che i server vengano visualizzati nel portale.</span><span class="sxs-lookup"><span data-stu-id="335b2-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="335b2-132">Aggiungere l'account per l'individuazione automatica</span><span class="sxs-lookup"><span data-stu-id="335b2-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="335b2-133">Configurare una connessione</span><span class="sxs-lookup"><span data-stu-id="335b2-133">Set up a connection</span></span>

<span data-ttu-id="335b2-134">Stabilire la connessione ai server come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="335b2-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="335b2-135">Selezionare **+vCenter** per avviare la connessione di un server VMware vCenter o di un host VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="335b2-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="335b2-136">In **Aggiungi vCenter** specificare un nome descrittivo per il server vCenter o l'host vSphere e quindi specificare l'indirizzo IP o il nome di dominio completo del server.</span><span class="sxs-lookup"><span data-stu-id="335b2-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="335b2-137">Lasciare la porta 443, a meno che i server VMware siano configurati per l'ascolto delle richieste su una porta diversa.</span><span class="sxs-lookup"><span data-stu-id="335b2-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="335b2-138">Selezionare l'account che si deve connettere al server VMware vCenter o vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="335b2-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="335b2-139">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="335b2-139">Click **OK**.</span></span>
4. <span data-ttu-id="335b2-140">Site Recovery si connette ai server VMware usando le impostazioni specificate e individua le VM.</span><span class="sxs-lookup"><span data-stu-id="335b2-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="335b2-141">Se si aggiunge un server o un host con un account che non ha privilegi Administrator per il server vCenter o il server host, assicurarsi che questi privilegi siano abilitati per l'account: Datacenter (Data center), Datastore (Archivio dati), Folder (Cartella), Host, Network (Rete), Resource (Risorsa), Virtual machine (Macchina virtuale) e vSphere Distributed Switch (Switch distribuito vSphere).</span><span class="sxs-lookup"><span data-stu-id="335b2-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="335b2-142">Per il server VMware vCenter deve essere abilitato anche il privilegio Storage Views (Viste archiviazione).</span><span class="sxs-lookup"><span data-stu-id="335b2-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="335b2-143">Configurare l'ambiente di destinazione</span><span class="sxs-lookup"><span data-stu-id="335b2-143">Set up the target environment</span></span>

<span data-ttu-id="335b2-144">Prima di configurare l'ambiente di destinazione, verificare di aver configurato una rete virtuale e un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="335b2-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="335b2-145">Fare clic su **Preparare l'infrastruttura** > **Destinazione** e selezionare la sottoscrizione di Azure da usare.</span><span class="sxs-lookup"><span data-stu-id="335b2-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="335b2-146">Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="335b2-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="335b2-147">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="335b2-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destinazione](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="335b2-149">Se non si è creato un account di archiviazione o una rete, fare clic su **+Account di archiviazione** o **+Rete** per creare una rete o un account Resource Manager inline.</span><span class="sxs-lookup"><span data-stu-id="335b2-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="335b2-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="335b2-150">Next steps</span></span>

<span data-ttu-id="335b2-151">Andare al [Passaggio 9: Configurare i criteri di replica](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="335b2-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
