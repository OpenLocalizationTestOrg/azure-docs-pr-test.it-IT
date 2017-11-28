---
title: aaaSet backup hello origine e di destinazione per VMware replica tooAzure con Azure Site Recovery | Documenti Microsoft
description: Riepiloga hello passaggi tooset le impostazioni di origine e di destinazione per la replica di archiviazione di macchine virtuali VMware tooAzure con Azure Site Recovery
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
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="5df02-103">Passaggio 8: Impostare hello origine e di destinazione per tooAzure replica VMware</span><span class="sxs-lookup"><span data-stu-id="5df02-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="5df02-104">In questo articolo viene descritto come le impostazioni di tooconfigure origine e di destinazione durante la replica locale tooAzure di macchine virtuali VMware, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5df02-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="5df02-105">Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5df02-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="5df02-106">Configurare un ambiente di origine hello</span><span class="sxs-lookup"><span data-stu-id="5df02-106">Set up hello source environment</span></span>

<span data-ttu-id="5df02-107">Configurare il server di configurazione di hello, registrarla nell'insieme di credenziali hello e individuare le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5df02-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="5df02-108">Fare clic su **Site Recovery** > **Passaggio 1: Preparare l'infrastruttura** > **Origine**.</span><span class="sxs-lookup"><span data-stu-id="5df02-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="5df02-109">Se non è disponibile un server di configurazione, fare clic su **+Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5df02-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="5df02-110">In **Aggiungi server** verificare che **Tipo di server** contenga **Server di configurazione**.</span><span class="sxs-lookup"><span data-stu-id="5df02-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="5df02-111">Scaricare i file di installazione di hello installazione unificata di Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="5df02-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="5df02-112">Scaricare la chiave di registrazione dell'insieme di credenziali di hello.</span><span class="sxs-lookup"><span data-stu-id="5df02-112">Download hello vault registration key.</span></span> <span data-ttu-id="5df02-113">che sarà necessaria quando si esegue l'Installazione unificata.</span><span class="sxs-lookup"><span data-stu-id="5df02-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="5df02-114">chiave di Hello è valida per cinque giorni dopo la generazione è.</span><span class="sxs-lookup"><span data-stu-id="5df02-114">hello key is valid for five days after you generate it.</span></span>

   ![Impostare l'origine](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="5df02-116">Registrare il server di configurazione di hello nell'insieme di credenziali hello</span><span class="sxs-lookup"><span data-stu-id="5df02-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="5df02-117">Seguito hello prima di avviare, quindi eseguire il programma di installazione unificata tooinstall hello configurazione server, il server di elaborazione hello e il server di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="5df02-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="5df02-118">Ottenere una breve panoramica video</span><span class="sxs-lookup"><span data-stu-id="5df02-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="5df02-119">Nel server di configurazione hello VM, verificare che l'orologio di sistema hello è sincronizzato con un [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="5df02-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="5df02-120">Deve corrispondere.</span><span class="sxs-lookup"><span data-stu-id="5df02-120">It should match.</span></span> <span data-ttu-id="5df02-121">Se è avanti o indietro di 15 minuti, l'installazione potrebbe avere esito negativo.</span><span class="sxs-lookup"><span data-stu-id="5df02-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="5df02-122">Eseguire l'installazione come amministratore locale nel server di configurazione hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5df02-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="5df02-123">Assicurarsi che sia abilitato TLS 1.0 su hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5df02-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="5df02-124">può anche essere installato il server di configurazione di Hello [dalla riga di comando hello](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="5df02-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="5df02-125">Connettere i server tooVMware</span><span class="sxs-lookup"><span data-stu-id="5df02-125">Connect tooVMware servers</span></span>

<span data-ttu-id="5df02-126">macchine virtuali toodiscover Azure Site Recovery tooallow in esecuzione nell'ambiente locale, è necessario tooconnect il Server VMware vCenter o l'host ESXi vSphere con il ripristino del sito.</span><span class="sxs-lookup"><span data-stu-id="5df02-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="5df02-127">Si noti seguenti hello prima di iniziare:</span><span class="sxs-lookup"><span data-stu-id="5df02-127">Note hello following before you start:</span></span>

- <span data-ttu-id="5df02-128">Se si aggiunge il server vCenter hello o vSphere host tooSite ripristino con un account senza privilegi di amministratore nel server di hello, account hello necessita di questi privilegi abilitati:</span><span class="sxs-lookup"><span data-stu-id="5df02-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="5df02-129">Datacenter (Data center), Datastore (Archivio dati), Folder (Cartella), Host, Network (Rete), Resource (Risorsa), Virtual machine (Macchina virtuale) e vSphere Distributed Switch (Switch distribuito vSphere).</span><span class="sxs-lookup"><span data-stu-id="5df02-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="5df02-130">server vCenter Hello necessita di autorizzazioni di viste di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5df02-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="5df02-131">Quando si aggiunge VMware server tooSite ripristino, può richiedere 15 minuti o più per tali tooappear nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="5df02-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="5df02-132">Aggiungere account hello per l'individuazione automatica</span><span class="sxs-lookup"><span data-stu-id="5df02-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="5df02-133">Configurare una connessione</span><span class="sxs-lookup"><span data-stu-id="5df02-133">Set up a connection</span></span>

<span data-ttu-id="5df02-134">Connettersi tooservers come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5df02-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="5df02-135">Selezionare **+ vCenter** toostart la connessione a un server VMware vCenter o un host VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="5df02-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="5df02-136">In **aggiungere vCenter**, specificare un nome descrittivo per il server vCenter o l'host di vSphere hello e quindi specificare l'indirizzo IP hello o il nome FQDN del server di hello.</span><span class="sxs-lookup"><span data-stu-id="5df02-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="5df02-137">Lasciare la porta hello 443, a meno che i server VMware sono toolisten configurato per le richieste su una porta diversa.</span><span class="sxs-lookup"><span data-stu-id="5df02-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="5df02-138">Selezionare l'account hello tooconnect toohello VMware vCenter server o di vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="5df02-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="5df02-139">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="5df02-139">Click **OK**.</span></span>
4. <span data-ttu-id="5df02-140">Il ripristino del sito si connette a server tooVMware hello utilizzando le impostazioni specificate e individua le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="5df02-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="5df02-141">Se si aggiunge un host con un account che non dispone dei privilegi di amministratore nel server vCenter o l'host di hello o un server, verificare che account hello avere questi privilegi abilitati: Data Center, l'archivio dati, cartella, Host, rete, risorsa, la macchina virtuale, e vSphere Switch distribuiti.</span><span class="sxs-lookup"><span data-stu-id="5df02-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="5df02-142">Inoltre, è necessario hello archiviazione viste privilegio abilitato server hello VMware vCenter.</span><span class="sxs-lookup"><span data-stu-id="5df02-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="5df02-143">Configurare un ambiente di destinazione hello</span><span class="sxs-lookup"><span data-stu-id="5df02-143">Set up hello target environment</span></span>

<span data-ttu-id="5df02-144">Prima configurare un ambiente di destinazione hello, verificare di che disporre di un account di archiviazione di Azure e una configurazione di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5df02-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="5df02-145">Fare clic su **Prepare infrastruttura** > **destinazione**, e selezionare hello sottoscrizione di Azure da toouse.</span><span class="sxs-lookup"><span data-stu-id="5df02-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="5df02-146">Specificare se per la destinazione deve essere usato il modello di distribuzione classica o Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5df02-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="5df02-147">Site Recovery verifica la disponibilità di uno o più account di archiviazione di Azure e reti compatibili.</span><span class="sxs-lookup"><span data-stu-id="5df02-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destinazione](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="5df02-149">Se è stata creata una rete o un account di archiviazione, fare clic su **+ account di archiviazione** o **+ rete**, toocreate un inline di account o rete di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="5df02-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5df02-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5df02-150">Next steps</span></span>

<span data-ttu-id="5df02-151">Andare troppo[passaggio 9: configurare un criterio di replica](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="5df02-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
