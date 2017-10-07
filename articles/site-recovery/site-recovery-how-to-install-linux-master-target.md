---
title: aaaHow tooinstall un server di destinazione master Linux per il failover da locale tooon Azure | Documenti Microsoft
description: "Prima di eseguire la riprotezione di una macchina virtuale Linux, è necessario dotarsi di un server di destinazione master Linux. Informazioni su come tooinstall uno."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: d7c55d115712b9862414979f89efb1f177c5f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="800dd-104">Installare un server di destinazione master Linux</span><span class="sxs-lookup"><span data-stu-id="800dd-104">Install a Linux master target server</span></span>
<span data-ttu-id="800dd-105">Dopo aver eseguito il failover delle macchine virtuali, è possibile eseguire il backup hello macchine virtuali toohello nel sito locale.</span><span class="sxs-lookup"><span data-stu-id="800dd-105">After you fail over your virtual machines, you can fail back hello virtual machines toohello on-premises site.</span></span> <span data-ttu-id="800dd-106">toofail nuovamente, è necessario tooreprotect hello macchina virtuale Azure toohello nel sito locale.</span><span class="sxs-lookup"><span data-stu-id="800dd-106">toofail back, you need tooreprotect hello virtual machine from Azure toohello on-premises site.</span></span> <span data-ttu-id="800dd-107">Per questo processo, è necessario un traffico di hello tooreceive del server di destinazione master di on-premise.</span><span class="sxs-lookup"><span data-stu-id="800dd-107">For this process, you need an on-premises master target server tooreceive hello traffic.</span></span> 

<span data-ttu-id="800dd-108">Se quella protetta è una macchina virtuale Windows, è necessario un server di destinazione master Windows.</span><span class="sxs-lookup"><span data-stu-id="800dd-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="800dd-109">Per una macchina virtuale Linux è necessario un server di destinazione master Linux.</span><span class="sxs-lookup"><span data-stu-id="800dd-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="800dd-110">Lettura hello seguenti passaggi viene toolearn come toocreate e installare Linux master destinazione.</span><span class="sxs-lookup"><span data-stu-id="800dd-110">Read hello following steps toolearn how toocreate and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="800dd-111">A partire dalla versione del server di destinazione master hello 9.10.0, hello più recente destinazione master server può essere installato solo su un server Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="800dd-111">Starting with release of hello 9.10.0 master target server, hello latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="800dd-112">Le nuove installazioni non sono consentite nei server CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="800dd-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="800dd-113">Tuttavia, è possibile continuare tooupgrade i server di destinazione master precedente utilizzando la versione di hello 9.10.0.</span><span class="sxs-lookup"><span data-stu-id="800dd-113">However, you can continue tooupgrade your old master target servers by using hello 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="800dd-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="800dd-114">Overview</span></span>
<span data-ttu-id="800dd-115">In questo articolo vengono fornite istruzioni per la modalità tooinstall Linux master di destinazione.</span><span class="sxs-lookup"><span data-stu-id="800dd-115">This article provides instructions for how tooinstall a Linux master target.</span></span>

<span data-ttu-id="800dd-116">Registrare commenti o domande alla fine di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="800dd-116">Post comments or questions at hello end of this article or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="800dd-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="800dd-117">Prerequisites</span></span>

* <span data-ttu-id="800dd-118">host di hello toochoose in quale destinazione master hello toodeploy, determinare se il failback hello verrà toobe tooan locali esistenti tooa nuova macchina virtuale o macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="800dd-118">toochoose hello host on which toodeploy hello master target, determine if hello failback is going toobe tooan existing on-premises virtual machine or tooa new virtual machine.</span></span> 
    * <span data-ttu-id="800dd-119">Per una macchina virtuale esistente, hello host di destinazione master hello deve disporre di accesso toohello di archivi di dati della macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-119">For an existing virtual machine, hello host of hello master target should have access toohello data stores of hello virtual machine.</span></span>
    * <span data-ttu-id="800dd-120">Se non esiste una macchina virtuale locale di hello, macchina virtuale di failback hello viene creato in hello stesso host di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-120">If hello on-premises virtual machine does not exist, hello failback virtual machine is created on hello same host as hello master target.</span></span> <span data-ttu-id="800dd-121">È possibile scegliere qualsiasi host ESXi di destinazione master di tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-121">You can choose any ESXi host tooinstall hello master target.</span></span>
* <span data-ttu-id="800dd-122">la destinazione master Hello deve trovarsi in una rete in grado di comunicare con il server di elaborazione hello e il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-122">hello master target should be on a network that can communicate with hello process server and hello configuration server.</span></span>
* <span data-ttu-id="800dd-123">versione di Hello della destinazione master hello deve essere tooor uguale precedenza rispetto alle versioni hello del server di elaborazione hello e il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-123">hello version of hello master target must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="800dd-124">Ad esempio, se versione hello hello del server di configurazione di 9.4, può essere versione hello della destinazione master hello 9.4 o 9.3 ma non di 9,5.</span><span class="sxs-lookup"><span data-stu-id="800dd-124">For example, if hello version of hello configuration server is 9.4, hello version of hello master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="800dd-125">la destinazione master Hello può essere solo una macchina virtuale VMware e non un server fisico.</span><span class="sxs-lookup"><span data-stu-id="800dd-125">hello master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-hello-master-target-according-toohello-sizing-guidelines"></a><span data-ttu-id="800dd-126">Creare la destinazione master di hello in base a toohello linee guida di ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="800dd-126">Create hello master target according toohello sizing guidelines</span></span>

<span data-ttu-id="800dd-127">Creare la destinazione master di hello in base alle indicazioni di ridimensionamento hello:</span><span class="sxs-lookup"><span data-stu-id="800dd-127">Create hello master target in accordance with hello following sizing guidelines:</span></span>
- <span data-ttu-id="800dd-128">**RAM**: almeno 6 GB</span><span class="sxs-lookup"><span data-stu-id="800dd-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="800dd-129">**Dimensioni del disco del sistema operativo**: 100 GB o più (tooinstall CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="800dd-129">**OS disk size**: 100 GB or more (tooinstall CentOS6.6)</span></span>
- <span data-ttu-id="800dd-130">**Dimensioni disco aggiuntive per l'unità di conservazione**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="800dd-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="800dd-131">**Core CPU**: almeno 4 core</span><span class="sxs-lookup"><span data-stu-id="800dd-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="800dd-132">esempio Hello supportato Ubuntu kernel sono supportati.</span><span class="sxs-lookup"><span data-stu-id="800dd-132">hello following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="800dd-133">Serie di kernel</span><span class="sxs-lookup"><span data-stu-id="800dd-133">Kernel Series</span></span>  |<span data-ttu-id="800dd-134">Supporto troppo alto</span><span class="sxs-lookup"><span data-stu-id="800dd-134">Support up too</span></span> |
|---------|---------|
|<span data-ttu-id="800dd-135">4.4</span><span class="sxs-lookup"><span data-stu-id="800dd-135">4.4</span></span>      |<span data-ttu-id="800dd-136">4.4.0-81-generico</span><span class="sxs-lookup"><span data-stu-id="800dd-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="800dd-137">4.8</span><span class="sxs-lookup"><span data-stu-id="800dd-137">4.8</span></span>      |<span data-ttu-id="800dd-138">4.8.0-56-generico</span><span class="sxs-lookup"><span data-stu-id="800dd-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="800dd-139">4.10</span><span class="sxs-lookup"><span data-stu-id="800dd-139">4.10</span></span>     |<span data-ttu-id="800dd-140">4.10.0-24-generico</span><span class="sxs-lookup"><span data-stu-id="800dd-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-hello-master-target-server"></a><span data-ttu-id="800dd-141">Distribuire il server di destinazione master hello</span><span class="sxs-lookup"><span data-stu-id="800dd-141">Deploy hello master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="800dd-142">Installare Ubuntu 16.04.2 Minimal</span><span class="sxs-lookup"><span data-stu-id="800dd-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="800dd-143">Richiedere hello seguenti del sistema operativo a 64 bit di hello passaggi tooinstall hello Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="800dd-143">Take hello following hello steps tooinstall hello Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="800dd-144">**Passaggio 1:** passare toohello [collegamento per il download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) scegliere mirror di hello più vicino da cui scaricare un file ISO di Ubuntu 16.04.2 minimo a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="800dd-144">**Step 1:** Go toohello [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose hello closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="800dd-145">Mantenere un'immagine ISO a 64 bit minimo di Ubuntu 16.04.2 nell'unità DVD hello e avviare hello del sistema.</span><span class="sxs-lookup"><span data-stu-id="800dd-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in hello DVD drive and start hello system.</span></span>

<span data-ttu-id="800dd-146">**Passaggio 2:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selezionare una lingua](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="800dd-148">**Passaggio 3:** selezionare **Install Ubuntu Server** (Installa server Ubuntu) e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selezionare Installa server Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="800dd-150">**Passaggio 4:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selezionare English (Inglese) come lingua preferita](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="800dd-152">**Passaggio 5:** selezionare hello opzione appropriata hello **fuso orario** elenco di opzioni e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-152">**Step 5:** Select hello appropriate option from hello **Time Zone** options list, and then select **Enter**.</span></span>

![Selezionare il fuso orario corretti di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="800dd-154">**Passaggio 6:** selezionare **n** (hello. opzione predefinita), quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-154">**Step 6:** Select **No** (hello default option), and then select **Enter**.</span></span>


![Configurare hello tastiera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="800dd-156">**Passaggio 7:** selezionare **inglese (Stati Uniti)** come hello paese di origine per la tastiera hello e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-156">**Step 7:** Select **English (US)** as hello country of origin for hello keyboard, and then select **Enter**.</span></span>

![Selezionare Usa come paese hello di origine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="800dd-158">**Passaggio 8:** selezionare **inglese (Stati Uniti)** come layout di tastiera hello, quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-158">**Step 8:** Select **English (US)** as hello keyboard layout, and then select **Enter**.</span></span>

![Selezionare l'inglese come layout di tastiera hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="800dd-160">**Passaggio 9:** immettere nome host di hello del server in hello **Hostname** e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="800dd-160">**Step 9:** Enter hello hostname for your server in hello **Hostname** box, and then select **Continue**.</span></span>

![Immettere nome host di hello del server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="800dd-162">**Passaggio 10:** toocreate un account utente, immettere nome utente hello e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="800dd-162">**Step 10:** toocreate a user account, enter hello user name, and then select **Continue**.</span></span>

![Crea un account utente](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="800dd-164">**Passaggio 11:** immettere hello password per account utente nuovo hello e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="800dd-164">**Step 11:** Enter hello password for hello new user account, and then select **Continue**.</span></span>

![Immettere la password di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="800dd-166">**Passaggio 12:** Conferma password hello hello nuovo utente e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="800dd-166">**Step 12:** Confirm hello password for hello new user, and then select **Continue**.</span></span>

![Conferma password hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="800dd-168">**Passaggio 13:** selezionare **n** (hello. opzione predefinita), quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-168">**Step 13:** Select **No** (hello default option), and then select **Enter**.</span></span>

![Configurare utenti e password](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="800dd-170">**Passaggio 14:** se hello fuso orario visualizzato sia corretto, selezionare **Sì** (hello. opzione predefinita), quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-170">**Step 14:** If hello time zone that's displayed is correct, select **Yes** (hello default option), and then select **Enter**.</span></span>

<span data-ttu-id="800dd-171">tooreconfigure il fuso orario **n**.</span><span class="sxs-lookup"><span data-stu-id="800dd-171">tooreconfigure your time zone, select **No**.</span></span>

![Configurare orologio hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="800dd-173">**Passaggio 15:** hello metodo opzioni di partizionamento, selezionare **interattiva - utilizzare l'intero disco**, quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-173">**Step 15:** From hello partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selezionare l'opzione metodo di partizionamento hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="800dd-175">**Passaggio 16:** selezionare hello disco appropriato da hello **selezionare disco toopartition** opzioni e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-175">**Step 16:** Select hello appropriate disk from hello **Select disk toopartition** options, and then select **Enter**.</span></span>


![Selezionare il disco hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="800dd-177">**Passaggio 17:** selezionare **Sì** toowrite hello toodisk modifiche e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-177">**Step 17:** Select **Yes** toowrite hello changes toodisk, and then select **Enter**.</span></span>

![Scrivere hello modifiche toodisk](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="800dd-179">**Passaggio 18:** selezionare l'opzione predefinita di hello, selezionare **continua**, quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-179">**Step 18:** Select hello default option, select **Continue**, and then select **Enter**.</span></span>

![Selezionare l'opzione predefinita hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="800dd-181">**Passaggio 19:** selezionare hello opzione appropriata per la gestione degli aggiornamenti del sistema e quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-181">**Step 19:** Select hello appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selezionare la modalità di aggiornamento toomanage](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="800dd-183">Poiché il server di destinazione master hello Azure Site Recovery richiede una versione di hello Ubuntu molto specifica, è necessario tooensure tale kernel hello gli aggiornamenti sono disabilitati per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-183">Because hello Azure Site Recovery master target server requires a very specific version of hello Ubuntu, you need tooensure that hello kernel upgrades are disabled for hello virtual machine.</span></span> <span data-ttu-id="800dd-184">Se sono abilitati, eventuali aggiornamenti regolari causano toomalfunction server di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-184">If they are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span> <span data-ttu-id="800dd-185">Assicurarsi di selezionare hello **alcun aggiornamento automatico** opzione.</span><span class="sxs-lookup"><span data-stu-id="800dd-185">Make sure you select hello **No automatic updates** option.</span></span>


<span data-ttu-id="800dd-186">**Passaggio 20:** selezionare le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="800dd-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="800dd-187">Se si desidera openSSH per la connessione SSH, selezionare hello **server OpenSSH** opzione e quindi selezionare **continua**.</span><span class="sxs-lookup"><span data-stu-id="800dd-187">If you want openSSH for SSH connect, select hello **OpenSSH server** option, and then select **Continue**.</span></span>

![Selezionare il software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="800dd-189">**Passaggio 21:** selezionare **Sì** e quindi **Invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Caricatore di avvio installazione hello GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="800dd-191">**Passaggio 22:** selezionare hello dispositivi appropriati per l'installazione del caricatore di avvio hello (preferibilmente **dev/sda**), quindi selezionare **invio**.</span><span class="sxs-lookup"><span data-stu-id="800dd-191">**Step 22:** Select hello appropriate device for hello boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selezionare un dispositivo per l'installazione del caricatore di avvio](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="800dd-193">**Passaggio 23:** selezionare **continua**, quindi selezionare **invio** installazione hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="800dd-193">**Step 23:** Select **Continue**, and then select **Enter** toofinish hello installation.</span></span>

![Completare l'installazione di hello](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="800dd-195">Al termine dell'installazione di hello, accedi toohello VM con le nuove credenziali utente hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-195">After hello installation has finished, sign in toohello VM with hello new user credentials.</span></span> <span data-ttu-id="800dd-196">(Vedere troppo**passaggio 10** per ulteriori informazioni.)</span><span class="sxs-lookup"><span data-stu-id="800dd-196">(Refer too**Step 10** for more information.)</span></span>

<span data-ttu-id="800dd-197">Eseguire i passaggi di hello descritti nella seguente schermata tooset hello radice hello password utente.</span><span class="sxs-lookup"><span data-stu-id="800dd-197">Take hello steps that are described in hello following screenshot tooset hello ROOT user password.</span></span> <span data-ttu-id="800dd-198">Quindi, accedere come utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="800dd-198">Then sign in as ROOT user.</span></span>

![Password dell'utente ROOT hello set](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-hello-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="800dd-200">Preparare il computer di hello per la configurazione come server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="800dd-200">Prepare hello machine for configuration as a master target server</span></span>
<span data-ttu-id="800dd-201">Successivamente, preparare il computer di hello per la configurazione come server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="800dd-201">Next, prepare hello machine for configuration as a master target server.</span></span>

<span data-ttu-id="800dd-202">ID di hello tooget per ogni disco rigido SCSI in una macchina virtuale Linux, abilitare hello **disco. EnableUUID = TRUE** parametro.</span><span class="sxs-lookup"><span data-stu-id="800dd-202">tooget hello ID for each SCSI hard disk in a Linux virtual machine, enable hello **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="800dd-203">tooenable questo parametro, hello take seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="800dd-203">tooenable this parameter, take hello following steps:</span></span>

1. <span data-ttu-id="800dd-204">Arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="800dd-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="800dd-205">Voce hello per la macchina virtuale hello nel riquadro di sinistra hello e quindi scegliere **Modifica impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="800dd-205">Right-click hello entry for hello virtual machine in hello left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="800dd-206">Seleziona hello **opzioni** scheda.</span><span class="sxs-lookup"><span data-stu-id="800dd-206">Select hello **Options** tab.</span></span>

4. <span data-ttu-id="800dd-207">Nel riquadro sinistro hello selezionare **avanzate** > **generale**, quindi selezionare hello **parametri di configurazione** pulsante nella parte inferiore destra hello della schermata di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-207">In hello left pane, select **Advanced** > **General**, and then select hello **Configuration Parameters** button on hello lower-right part of hello screen.</span></span>

    ![Scheda Opzioni](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="800dd-209">Hello **parametri di configurazione** opzione non è disponibile quando hello macchina è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="800dd-209">hello **Configuration Parameters** option is not available when hello machine is running.</span></span> <span data-ttu-id="800dd-210">toomake questa scheda è attiva, spegnere la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-210">toomake this tab active, shut down hello virtual machine.</span></span>

5. <span data-ttu-id="800dd-211">Controllare se esiste già una riga con il valore **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="800dd-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="800dd-212">Se il valore di hello esiste e viene impostato troppo**False**, modificare il valore di hello troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="800dd-212">If hello value exists and is set too**False**, change hello value too**True**.</span></span> <span data-ttu-id="800dd-213">(valori hello non sono distinzione maiuscole/minuscole).</span><span class="sxs-lookup"><span data-stu-id="800dd-213">(hello values are not case-sensitive.)</span></span>

    - <span data-ttu-id="800dd-214">Se il valore di hello esiste e viene impostato troppo**True**selezionare **Annulla**.</span><span class="sxs-lookup"><span data-stu-id="800dd-214">If hello value exists and is set too**True**, select **Cancel**.</span></span>

    - <span data-ttu-id="800dd-215">Se il valore di hello non esiste, selezionare **Aggiungi riga**.</span><span class="sxs-lookup"><span data-stu-id="800dd-215">If hello value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="800dd-216">Nella colonna nome hello, aggiungere **disco. EnableUUID**, quindi impostare il valore di hello troppo**TRUE**.</span><span class="sxs-lookup"><span data-stu-id="800dd-216">In hello name column, add **disk.EnableUUID**, and then set hello value too**TRUE**.</span></span>

    ![Controllare se esiste già una riga con il valore disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="800dd-218">Disabilitare gli aggiornamenti del kernel</span><span class="sxs-lookup"><span data-stu-id="800dd-218">Disable kernel upgrades</span></span>

<span data-ttu-id="800dd-219">Server di destinazione master di Azure Site Recovery richiede una versione molto specifica di hello Ubuntu, verificare che gli aggiornamenti kernel hello sono disabilitati per la macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-219">Azure Site Recovery master target server requires a very specific version of hello Ubuntu, ensure that hello kernel upgrades are disabled for hello virtual machine.</span></span>

<span data-ttu-id="800dd-220">Se sono abilitati gli aggiornamenti del kernel, eventuali aggiornamenti regolari causano toomalfunction server di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-220">If kernel upgrades are enabled, then any regular upgrades cause hello master target server toomalfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="800dd-221">Scaricare e installare i pacchetti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="800dd-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="800dd-222">Assicurarsi di aver toodownload connettività Internet e installare pacchetti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="800dd-222">Make sure that you have Internet connectivity toodownload and install additional packages.</span></span> <span data-ttu-id="800dd-223">Se non si dispone di connettività Internet, è necessario toomanually trovare questi pacchetti RPM e installarli.</span><span class="sxs-lookup"><span data-stu-id="800dd-223">If you don't have Internet connectivity, you need toomanually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-hello-installer-for-setup"></a><span data-ttu-id="800dd-224">Ottenere installer hello per il programma di installazione</span><span class="sxs-lookup"><span data-stu-id="800dd-224">Get hello installer for setup</span></span>

<span data-ttu-id="800dd-225">Se la destinazione master disponga della connettività Internet, è possibile utilizzare hello seguente programma di installazione di passaggi toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-225">If your master target has Internet connectivity, you can use hello following steps toodownload hello installer.</span></span> <span data-ttu-id="800dd-226">In caso contrario, è possibile copiare installer hello dal server di elaborazione hello e quindi installarlo.</span><span class="sxs-lookup"><span data-stu-id="800dd-226">Otherwise, you can copy hello installer from hello process server and then install it.</span></span>

#### <a name="download-hello-master-target-installation-packages"></a><span data-ttu-id="800dd-227">Scaricare i pacchetti di installazione di destinazione master hello</span><span class="sxs-lookup"><span data-stu-id="800dd-227">Download hello master target installation packages</span></span>

<span data-ttu-id="800dd-228">[Scaricare i bit di hello più recente Linux destinazione master installazione](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="800dd-228">[Download hello latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="800dd-229">toodownload usando Linux, tipo:</span><span class="sxs-lookup"><span data-stu-id="800dd-229">toodownload it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="800dd-230">Assicurarsi di scaricare e decomprimere installer hello nella home directory.</span><span class="sxs-lookup"><span data-stu-id="800dd-230">Make sure that you download and unzip hello installer in your home directory.</span></span> <span data-ttu-id="800dd-231">Se decomprimere troppo**usr/Local**, installazione hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="800dd-231">If you unzip too**/usr/Local**, then hello installation  fails.</span></span>


#### <a name="access-hello-installer-from-hello-process-server"></a><span data-ttu-id="800dd-232">Programma di installazione di accesso hello dal server di elaborazione hello</span><span class="sxs-lookup"><span data-stu-id="800dd-232">Access hello installer from hello process server</span></span>

1. <span data-ttu-id="800dd-233">Nel server di elaborazione hello, andare troppo**C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="800dd-233">On hello process server, go too**C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="800dd-234">Copiare il file di programma di installazione necessari hello dal server di elaborazione hello e salvarlo come **latestlinuxmobsvc.tar.gz** nella home directory.</span><span class="sxs-lookup"><span data-stu-id="800dd-234">Copy hello required installer file from hello process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="800dd-235">Applicare le modifiche di configurazione personalizzate</span><span class="sxs-lookup"><span data-stu-id="800dd-235">Apply custom configuration changes</span></span>

<span data-ttu-id="800dd-236">modifiche di configurazione personalizzata tooapply, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="800dd-236">tooapply custom configuration changes, use hello following steps:</span></span>


1. <span data-ttu-id="800dd-237">Eseguire hello binario hello toountar di comando seguente.</span><span class="sxs-lookup"><span data-stu-id="800dd-237">Run hello following command toountar hello binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermata di hello comando toorun](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="800dd-239">Comando che segue di esecuzione hello toogive autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="800dd-239">Run hello following command toogive permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="800dd-240">Eseguire lo script di comando toorun hello seguente hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-240">Run hello following command toorun hello script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="800dd-241">Eseguire script hello una sola volta nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-241">Run hello script only once on hello server.</span></span> <span data-ttu-id="800dd-242">Arrestare il server di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-242">Shut down hello server.</span></span> <span data-ttu-id="800dd-243">Quindi riavviare hello server dopo aver aggiunto un disco, come descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-243">Then restart hello server after you add a disk, as described in hello next section.</span></span>

### <a name="add-a-retention-disk-toohello-linux-master-target-virtual-machine"></a><span data-ttu-id="800dd-244">Aggiungere una macchina virtuale destinazione master Linux di memorizzazione disco toohello</span><span class="sxs-lookup"><span data-stu-id="800dd-244">Add a retention disk toohello Linux master target virtual machine</span></span>

<span data-ttu-id="800dd-245">Utilizzare hello seguendo i passaggi toocreate un disco di conservazione:</span><span class="sxs-lookup"><span data-stu-id="800dd-245">Use hello following steps toocreate a retention disk:</span></span>

1. <span data-ttu-id="800dd-246">Collegare una nuova disco 1 TB toohello Linux destinazione master macchina virtuale e quindi avviare hello macchina.</span><span class="sxs-lookup"><span data-stu-id="800dd-246">Attach a new 1-TB disk toohello Linux master target virtual machine, and then start hello machine.</span></span>

2. <span data-ttu-id="800dd-247">Hello utilizzare **a percorsi multipli -ll** toolearn ID con percorsi multipli hello del disco di conservazione hello di comando.</span><span class="sxs-lookup"><span data-stu-id="800dd-247">Use hello **multipath -ll** command toolearn hello multipath ID of hello retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![ID di multipath Hello del disco di conservazione di hello](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="800dd-249">Formattare l'unità di hello e quindi creare un file system hello nuova unità.</span><span class="sxs-lookup"><span data-stu-id="800dd-249">Format hello drive, and then create a file system on hello new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Creazione di un file system nell'unità hello](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="800dd-251">Dopo aver creato il sistema di file hello, montare il disco di conservazione hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-251">After you create hello file system, mount hello retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Disco di conservazione di montaggio hello](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="800dd-253">Creare hello **fstab** voce toomount hello unità di conservazione ogni volta che viene avviato il sistema hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-253">Create hello **fstab** entry toomount hello retention drive every time hello system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="800dd-254">Selezionare **inserire** toobegin modifica file hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-254">Select **Insert** toobegin editing hello file.</span></span> <span data-ttu-id="800dd-255">Creare una nuova riga e quindi inserire dopo testo hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-255">Create a new line, and then insert hello following text.</span></span> <span data-ttu-id="800dd-256">Modificare multipath ID disco hello in base all'ID di multipath hello evidenziata dal comando precedente hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-256">Edit hello disk multipath ID based on hello highlighted multipath ID from hello previous command.</span></span>

    <span data-ttu-id="800dd-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="800dd-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="800dd-258">Selezionare **Esc**, quindi digitare **: wq** (scrivere e chiudere) finestra dell'editor tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-258">Select **Esc**, and then type **:wq** (write and quit) tooclose hello editor window.</span></span>

### <a name="install-hello-master-target"></a><span data-ttu-id="800dd-259">Installare la destinazione master hello</span><span class="sxs-lookup"><span data-stu-id="800dd-259">Install hello master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="800dd-260">versione di Hello del server di destinazione master hello deve essere tooor uguale precedenza rispetto alle versioni hello del server di elaborazione hello e il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-260">hello version of hello master target server must be equal tooor earlier than hello versions of hello process server and hello configuration server.</span></span> <span data-ttu-id="800dd-261">Se la versione del server master di destinazione è superiore, la riprotezione avrà esito positivo, ma la replica avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="800dd-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="800dd-262">Prima di installare il server di destinazione master hello, verificare che hello **/e così via/host** file nella macchina virtuale hello contiene voci che mappa gli indirizzi IP toohello di nome host locale hello che sono associati a tutte le schede di rete.</span><span class="sxs-lookup"><span data-stu-id="800dd-262">Before you install hello master target server, check that hello **/etc/hosts** file on hello virtual machine contains entries that map hello local hostname toohello IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="800dd-263">Copiare la passphrase hello da **C:\ProgramData\Microsoft Azure sito Recovery\private\connection.passphrase** nel server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-263">Copy hello passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on hello configuration server.</span></span> <span data-ttu-id="800dd-264">Quindi salvarlo come **passphrase.txt** in hello stessa directory locale eseguendo hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="800dd-264">Then save it as **passphrase.txt** in hello same local directory by running hello following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="800dd-265">Esempio:</span><span class="sxs-lookup"><span data-stu-id="800dd-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="800dd-266">Nota l'indirizzo IP del server di configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-266">Note hello configuration server's IP address.</span></span> <span data-ttu-id="800dd-267">È necessario nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-267">You need it in hello next step.</span></span>

3. <span data-ttu-id="800dd-268">Eseguire hello seguente server di destinazione master comando tooinstall hello e registrare server hello con il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-268">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="800dd-269">Esempio:</span><span class="sxs-lookup"><span data-stu-id="800dd-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="800dd-270">Attendere il completamento dello script hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-270">Wait until hello script finishes.</span></span> <span data-ttu-id="800dd-271">Se la destinazione master hello registra correttamente, la destinazione master hello è elencata in hello **infrastruttura di Site Recovery** pagina del portale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-271">If hello master target registers sucessfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


#### <a name="install-hello-master-target-by-using-interactive-installation"></a><span data-ttu-id="800dd-272">Installare la destinazione master hello utilizzando Installazione interattiva</span><span class="sxs-lookup"><span data-stu-id="800dd-272">Install hello master target by using interactive installation</span></span>

1. <span data-ttu-id="800dd-273">Eseguire hello seguente destinazione di comando tooinstall hello master.</span><span class="sxs-lookup"><span data-stu-id="800dd-273">Run hello following command tooinstall hello master target.</span></span> <span data-ttu-id="800dd-274">Per il ruolo dell'agente hello scegliere **destinazione Master**.</span><span class="sxs-lookup"><span data-stu-id="800dd-274">For hello agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="800dd-275">Selezionare il percorso predefinito hello per l'installazione e quindi selezionare **invio** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="800dd-275">Choose hello default location for installation, and then select **Enter** toocontinue.</span></span>

    ![Scelta di un percorso predefinito per l'installazione del server di destinazione master](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="800dd-277">Al termine dell'installazione di hello, registrare il server di configurazione di hello dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-277">After hello installation has finished, register hello configuration server by using hello command line.</span></span>

1. <span data-ttu-id="800dd-278">Nota l'indirizzo IP hello hello del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="800dd-278">Note hello IP address of hello configuration server.</span></span> <span data-ttu-id="800dd-279">È necessario nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-279">You need it in hello next step.</span></span>

2. <span data-ttu-id="800dd-280">Eseguire hello seguente server di destinazione master comando tooinstall hello e registrare server hello con il server di configurazione di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-280">Run hello following command tooinstall hello master target server and register hello server with hello configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="800dd-281">Esempio:</span><span class="sxs-lookup"><span data-stu-id="800dd-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="800dd-282">Attendere il completamento dello script hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-282">Wait until hello script finishes.</span></span> <span data-ttu-id="800dd-283">Se la destinazione master hello è registrato correttamente, la destinazione master hello è elencata in hello **infrastruttura di Site Recovery** pagina del portale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-283">If hello master target is registered succesfully, hello master target is listed on hello **Site Recovery Infrastructure** page of hello portal.</span></span>


### <a name="upgrade-hello-master-target"></a><span data-ttu-id="800dd-284">Aggiornare la destinazione master hello</span><span class="sxs-lookup"><span data-stu-id="800dd-284">Upgrade hello master target</span></span>

<span data-ttu-id="800dd-285">Eseguire l'installazione guidata di hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-285">Run hello installer.</span></span> <span data-ttu-id="800dd-286">Rileva automaticamente che l'agente di hello è installato nella destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-286">It automatically detects that hello agent is installed on hello master target.</span></span> <span data-ttu-id="800dd-287">tooupgrade, selezionare **Y**.  Al termine dell'installazione di hello, controllare la versione hello della destinazione master di hello installato utilizzando hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="800dd-287">tooupgrade, select **Y**.  After hello setup has been completed, check hello version of hello master target installed by using hello following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="800dd-288">È possibile visualizzare tale hello **versione** campo fornisce il numero di versione hello della destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-288">You can see that hello **Version** field gives hello version number of hello master target.</span></span>

### <a name="install-vmware-tools-on-hello-master-target-server"></a><span data-ttu-id="800dd-289">Installare gli strumenti VMware nel server di destinazione master hello</span><span class="sxs-lookup"><span data-stu-id="800dd-289">Install VMware tools on hello master target server</span></span>

<span data-ttu-id="800dd-290">È necessario tooinstall VMware tools nella destinazione master hello in modo che è possibile rilevare gli archivi dati hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-290">You need tooinstall VMware tools on hello master target so that it can discover hello data stores.</span></span> <span data-ttu-id="800dd-291">Se non sono installati gli strumenti di hello, schermata di riprotezione hello non elencato in archivi dati hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-291">If hello tools are not installed, hello reprotect screen isn't listed in hello data stores.</span></span> <span data-ttu-id="800dd-292">Dopo l'installazione di strumenti di VMware hello, è necessario toorestart.</span><span class="sxs-lookup"><span data-stu-id="800dd-292">After installation of hello VMware tools, you need toorestart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="800dd-293">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="800dd-293">Next steps</span></span>
<span data-ttu-id="800dd-294">Dopo l'installazione hello e la registrazione della destinazione master hello è finsihed, è possibile visualizzare la destinazione master hello vengono visualizzati nel hello **destinazione Master** sezione **infrastruttura di Site Recovery**, in hello Panoramica di server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="800dd-294">After hello installation and registration of hello master target has finsihed, you can see hello master target appear on hello **Master Target** section in **Site Recovery Infrastructure**, under hello configuration server overview.</span></span>

<span data-ttu-id="800dd-295">È ora possibile procedere con la [riprotezione](site-recovery-how-to-reprotect.md), seguita dal failback.</span><span class="sxs-lookup"><span data-stu-id="800dd-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="800dd-296">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="800dd-296">Common issues</span></span>

* <span data-ttu-id="800dd-297">Verificare che Storage vMotion non sia abilitato in alcun componente di gestione, ad esempio il server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="800dd-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="800dd-298">Se la destinazione master hello Sposta dopo un riprotezione ha esito positivo, non è possibile scollegare i dischi di macchina virtuale di hello (VMDK).</span><span class="sxs-lookup"><span data-stu-id="800dd-298">If hello master target moves after a successful reprotect, hello virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="800dd-299">In questo caso, il failback avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="800dd-299">In this case, failback fails.</span></span>

* <span data-ttu-id="800dd-300">la destinazione master Hello non deve avere uno snapshot nella macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-300">hello master target should not have any snapshots on hello virtual machine.</span></span> <span data-ttu-id="800dd-301">Se sono presenti snapshot, il failback avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="800dd-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="800dd-302">A causa di toosome NIC le configurazioni personalizzate in alcuni clienti, l'interfaccia di rete hello è disabilitato durante l'avvio e non è possibile inizializzare l'agente di destinazione master hello.</span><span class="sxs-lookup"><span data-stu-id="800dd-302">Due toosome custom NIC configurations at some customers, hello network interface is disabled during startup, and hello master target agent cannot initialize.</span></span> <span data-ttu-id="800dd-303">Verificare che tale hello le proprietà seguenti sono state impostate correttamente.</span><span class="sxs-lookup"><span data-stu-id="800dd-303">Make sure that hello following properties are correctly set.</span></span> <span data-ttu-id="800dd-304">Controllare queste proprietà in hello Ethernet /etc/sysconfig/network-scripts/ifcfg del file di scheda-eth *.</span><span class="sxs-lookup"><span data-stu-id="800dd-304">Check these properties in hello Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="800dd-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="800dd-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="800dd-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="800dd-306">ONBOOT=yes</span></span>
