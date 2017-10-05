---
title: Come installare un server di destinazione master Linux per il failover da Azure a locale | Documentazione Microsoft
description: "Prima di eseguire la riprotezione di una macchina virtuale Linux, è necessario dotarsi di un server di destinazione master Linux. Di seguito viene descritto come installarlo."
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
ms.openlocfilehash: 5341e3e56e0c366079958dd9a885f6ee3e8436cb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="install-a-linux-master-target-server"></a><span data-ttu-id="6ccd8-104">Installare un server di destinazione master Linux</span><span class="sxs-lookup"><span data-stu-id="6ccd8-104">Install a Linux master target server</span></span>
<span data-ttu-id="6ccd8-105">Dopo aver eseguito il failover delle macchine virtuali, è possibile eseguirne il failback nel sito locale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-105">After you fail over your virtual machines, you can fail back the virtual machines to the on-premises site.</span></span> <span data-ttu-id="6ccd8-106">Per eseguire il failback, è necessario riproteggere la macchina virtuale da Azure al sito locale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-106">To fail back, you need to reprotect the virtual machine from Azure to the on-premises site.</span></span> <span data-ttu-id="6ccd8-107">A tale scopo, è necessario un server di destinazione master locale che riceva il traffico.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-107">For this process, you need an on-premises master target server to receive the traffic.</span></span> 

<span data-ttu-id="6ccd8-108">Se quella protetta è una macchina virtuale Windows, è necessario un server di destinazione master Windows.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-108">If your protected virtual machine is a Windows virtual machine, then you need a Windows master target.</span></span> <span data-ttu-id="6ccd8-109">Per una macchina virtuale Linux è necessario un server di destinazione master Linux.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-109">For a Linux virtual machine, you need a Linux master target.</span></span> <span data-ttu-id="6ccd8-110">Per informazioni su come creare e installare server di destinazione master Linux, vedere la procedura riportata di seguito.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-110">Read the following steps to learn how to create and install a Linux master target.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ccd8-111">A partire dalla versione 9.10.0 del server di destinazione master, il server di destinazione master più recente può essere installato solo in un server Ubuntu 16.04.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-111">Starting with release of the 9.10.0 master target server, the latest master target server can be only installed on an Ubuntu 16.04 server.</span></span> <span data-ttu-id="6ccd8-112">Le nuove installazioni non sono consentite nei server CentOS6.6.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-112">New installations aren't allowed on  CentOS6.6 servers.</span></span> <span data-ttu-id="6ccd8-113">È comunque possibile continuare ad aggiornare i server di destinazione master precedenti con la versione 9.10.0.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-113">However, you can continue to upgrade your old master target servers by using the 9.10.0 version.</span></span>

## <a name="overview"></a><span data-ttu-id="6ccd8-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="6ccd8-114">Overview</span></span>
<span data-ttu-id="6ccd8-115">Questo articolo contiene istruzioni per l'installazione di un server di destinazione master Linux.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-115">This article provides instructions for how to install a Linux master target.</span></span>

<span data-ttu-id="6ccd8-116">Per inviare commenti o domande è possibile usare la parte inferiore di questo articolo oppure il [forum sui Servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-116">Post comments or questions at the end of this article or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ccd8-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6ccd8-117">Prerequisites</span></span>

* <span data-ttu-id="6ccd8-118">Per scegliere l'host in cui distribuire il server di destinazione master, determinare se il failback verrà eseguito in una macchina virtuale locale esistente o in una macchina virtuale nuova.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-118">To choose the host on which to deploy the master target, determine if the failback is going to be to an existing on-premises virtual machine or to a new virtual machine.</span></span> 
    * <span data-ttu-id="6ccd8-119">Se viene eseguito in una macchina virtuale esistente, l'host del server di destinazione master deve poter accedere agli archivi dati della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-119">For an existing virtual machine, the host of the master target should have access to the data stores of the virtual machine.</span></span>
    * <span data-ttu-id="6ccd8-120">Se la macchina virtuale locale non esiste, la macchina virtuale di failback viene creata nello stesso host del server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-120">If the on-premises virtual machine does not exist, the failback virtual machine is created on the same host as the master target.</span></span> <span data-ttu-id="6ccd8-121">Per l'installazione del server di destinazione master è possibile scegliere qualsiasi host ESXi.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-121">You can choose any ESXi host to install the master target.</span></span>
* <span data-ttu-id="6ccd8-122">Il server deve trovarsi in una rete in grado di comunicare con il server di elaborazione e il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-122">The master target should be on a network that can communicate with the process server and the configuration server.</span></span>
* <span data-ttu-id="6ccd8-123">La versione del server di destinazione master deve essere uguale o precedente a quella del server di elaborazione e del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-123">The version of the master target must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="6ccd8-124">Ad esempio, se la versione del server di configurazione è 9.4, la versione del server di destinazione master può essere 9.4 o 9.3 ma non 9.5.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-124">For example, if the version of the configuration server is 9.4, the version of the master target can be 9.4 or 9.3 but not 9.5.</span></span>
* <span data-ttu-id="6ccd8-125">Il server di destinazione master può essere solo una macchina virtuale VMware e non un server fisico.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-125">The master target can only be a VMware virtual machine and not a physical server.</span></span>

## <a name="create-the-master-target-according-to-the-sizing-guidelines"></a><span data-ttu-id="6ccd8-126">Creare il server di destinazione master in base alle linee guida per il ridimensionamento</span><span class="sxs-lookup"><span data-stu-id="6ccd8-126">Create the master target according to the sizing guidelines</span></span>

<span data-ttu-id="6ccd8-127">Creare il server di destinazione master in base alle linee guida per il ridimensionamento seguenti:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-127">Create the master target in accordance with the following sizing guidelines:</span></span>
- <span data-ttu-id="6ccd8-128">**RAM**: almeno 6 GB</span><span class="sxs-lookup"><span data-stu-id="6ccd8-128">**RAM**: 6 GB or more</span></span>
- <span data-ttu-id="6ccd8-129">**Dimensioni disco sistema operativo**: almeno 100 GB (per installare CentOS6.6)</span><span class="sxs-lookup"><span data-stu-id="6ccd8-129">**OS disk size**: 100 GB or more (to install CentOS6.6)</span></span>
- <span data-ttu-id="6ccd8-130">**Dimensioni disco aggiuntive per l'unità di conservazione**: 1 TB</span><span class="sxs-lookup"><span data-stu-id="6ccd8-130">**Additional disk size for retention drive**: 1 TB</span></span>
- <span data-ttu-id="6ccd8-131">**Core CPU**: almeno 4 core</span><span class="sxs-lookup"><span data-stu-id="6ccd8-131">**CPU cores**: 4 cores or more</span></span>

<span data-ttu-id="6ccd8-132">Sono supportati i kernel Ubuntu seguenti.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-132">The following supported Ubuntu kernels are supported.</span></span>


|<span data-ttu-id="6ccd8-133">Serie di kernel</span><span class="sxs-lookup"><span data-stu-id="6ccd8-133">Kernel Series</span></span>  |<span data-ttu-id="6ccd8-134">Supporta fino a</span><span class="sxs-lookup"><span data-stu-id="6ccd8-134">Support up to</span></span>  |
|---------|---------|
|<span data-ttu-id="6ccd8-135">4.4</span><span class="sxs-lookup"><span data-stu-id="6ccd8-135">4.4</span></span>      |<span data-ttu-id="6ccd8-136">4.4.0-81-generico</span><span class="sxs-lookup"><span data-stu-id="6ccd8-136">4.4.0-81-generic</span></span>         |
|<span data-ttu-id="6ccd8-137">4.8</span><span class="sxs-lookup"><span data-stu-id="6ccd8-137">4.8</span></span>      |<span data-ttu-id="6ccd8-138">4.8.0-56-generico</span><span class="sxs-lookup"><span data-stu-id="6ccd8-138">4.8.0-56-generic</span></span>         |
|<span data-ttu-id="6ccd8-139">4.10</span><span class="sxs-lookup"><span data-stu-id="6ccd8-139">4.10</span></span>     |<span data-ttu-id="6ccd8-140">4.10.0-24-generico</span><span class="sxs-lookup"><span data-stu-id="6ccd8-140">4.10.0-24-generic</span></span>        |


## <a name="deploy-the-master-target-server"></a><span data-ttu-id="6ccd8-141">Distribuire il server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-141">Deploy the master target server</span></span>

### <a name="install-ubuntu-16042-minimal"></a><span data-ttu-id="6ccd8-142">Installare Ubuntu 16.04.2 Minimal</span><span class="sxs-lookup"><span data-stu-id="6ccd8-142">Install Ubuntu 16.04.2 Minimal</span></span>

<span data-ttu-id="6ccd8-143">Attenersi ai passaggi seguenti per installare il sistema operativo a 64 bit di Ubuntu 16.04.2.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-143">Take the following the steps to install the Ubuntu 16.04.2 64-bit operating system.</span></span>

<span data-ttu-id="6ccd8-144">**Passaggio 1:** andare al [collegamento per il download](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) e scegliere il mirror più vicino da cui scaricare un file ISO di Ubuntu 16.04.2 Minimal a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-144">**Step 1:** Go to the [download link](https://www.ubuntu.com/download/server/thank-you?version=16.04.2&architecture=amd64) and choose the closest mirror from which download an Ubuntu 16.04.2 minimal 64-bit ISO.</span></span>

<span data-ttu-id="6ccd8-145">Mantenere l'ISO di Ubuntu 16.04.2 Minimal a 64 bit nell'unità DVD e avviare il sistema.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-145">Keep an Ubuntu 16.04.2 minimal 64-bit ISO in the DVD drive and start the system.</span></span>

<span data-ttu-id="6ccd8-146">**Passaggio 2:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-146">**Step 2:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selezionare una lingua](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image1.png)

<span data-ttu-id="6ccd8-148">**Passaggio 3:** selezionare **Install Ubuntu Server** (Installa server Ubuntu) e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-148">**Step 3:** Select **Install Ubuntu Server**, and then select **Enter**.</span></span>

![Selezionare Installa server Ubuntu](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image2.png)

<span data-ttu-id="6ccd8-150">**Passaggio 4:** selezionare **English** (Inglese) come lingua preferita e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-150">**Step 4:** Select **English** as your preferred language, and then select **Enter**.</span></span>

![Selezionare English (Inglese) come lingua preferita](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image3.png)

<span data-ttu-id="6ccd8-152">**Passaggio 5:** selezionare l'opzione appropriata nell'elenco di opzioni **Time Zone** (Fuso orario) e selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-152">**Step 5:** Select the appropriate option from the **Time Zone** options list, and then select **Enter**.</span></span>

![Selezionare il fuso orario corretto](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image4.png)

<span data-ttu-id="6ccd8-154">**Passaggio 6:** selezionare **No** (opzione predefinita), quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-154">**Step 6:** Select **No** (the default option), and then select **Enter**.</span></span>


![Configurare la tastiera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image5.png)

<span data-ttu-id="6ccd8-156">**Passaggio 7:** selezionare **English (US)** (Inglese Stati Uniti) come paese di origine per la tastiera e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-156">**Step 7:** Select **English (US)** as the country of origin for the keyboard, and then select **Enter**.</span></span>

![Selezionare USA come paese di origine](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image6.png)

<span data-ttu-id="6ccd8-158">**Passaggio 8:** selezionare **English (US)** (Inglese Stati Uniti) come layout per la tastiera e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-158">**Step 8:** Select **English (US)** as the keyboard layout, and then select **Enter**.</span></span>

![Selezionare US English (Inglese USA) per il layout di tastiera](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image7.png)

<span data-ttu-id="6ccd8-160">**Passaggio 9:** immettere il nome host del server nella casella **Hostname** (Nome host) e quindi fare clic su **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-160">**Step 9:** Enter the hostname for your server in the **Hostname** box, and then select **Continue**.</span></span>

![Immettere il nome host per il server](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image8.png)

<span data-ttu-id="6ccd8-162">**Passaggio 10:** per creare un account utente, immettere il nome utente e quindi selezionare **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-162">**Step 10:** To create a user account, enter the user name, and then select **Continue**.</span></span>

![Crea un account utente](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image9.png)

<span data-ttu-id="6ccd8-164">**Passaggio 11:** immettere la password per il nuovo account utente e quindi selezionare **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-164">**Step 11:** Enter the password for the new user account, and then select **Continue**.</span></span>

![Immettere la password](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image10.png)

<span data-ttu-id="6ccd8-166">**Passaggio 12:** confermare la password per il nuovo account utente e quindi selezionare **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-166">**Step 12:** Confirm the password for the new user, and then select **Continue**.</span></span>

![Confermare le password](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image11.png)

<span data-ttu-id="6ccd8-168">**Passaggio 13:** selezionare **No** (opzione predefinita), quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-168">**Step 13:** Select **No** (the default option), and then select **Enter**.</span></span>

![Configurare utenti e password](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image12.png)

<span data-ttu-id="6ccd8-170">**Passaggio 14:** se il fuso orario visualizzato è corretto, selezionare **Sì** (opzione predefinita), quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-170">**Step 14:** If the time zone that's displayed is correct, select **Yes** (the default option), and then select **Enter**.</span></span>

<span data-ttu-id="6ccd8-171">Per riconfigurare il fuso orario, selezionare **No**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-171">To reconfigure your time zone, select **No**.</span></span>

![Configurare l'orologio](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image13.png)

<span data-ttu-id="6ccd8-173">**Passaggio 15:** tra le opzioni per il metodo di partizionamento selezionare **Guided - use entire disk** (Guidato - Usare l'intero disco) e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-173">**Step 15:** From the partitioning method options, select **Guided - use entire disk**, and then select **Enter**.</span></span>

![Selezionare l'opzione per il metodo partizionamento](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image14.png)

<span data-ttu-id="6ccd8-175">**Passaggio 16:** selezionare il disco appropriato tra le opzioni **Select disk to partition** (Selezionare il disco da partizionare) e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-175">**Step 16:** Select the appropriate disk from the **Select disk to partition** options, and then select **Enter**.</span></span>


![Selezionare il disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image15.png)

<span data-ttu-id="6ccd8-177">**Passaggio 17:** selezionare **Sì** per scrivere le modifiche su disco e quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-177">**Step 17:** Select **Yes** to write the changes to disk, and then select **Enter**.</span></span>

![Scrivere le modifiche su disco](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image16.png)

<span data-ttu-id="6ccd8-179">**Passaggio 18:** selezionare l'opzione predefinita, selezionare **Continue** (Continua) e premere **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-179">**Step 18:** Select the default option, select **Continue**, and then select **Enter**.</span></span>

![Selezionare l'opzione predefinita](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image17.png)

<span data-ttu-id="6ccd8-181">**Passaggio 19:** selezionare l'opzione appropriata per la gestione degli aggiornamenti del sistema, quindi **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-181">**Step 19:** Select the appropriate option for managing upgrades on your system, and then select **Enter**.</span></span>

![Selezionare la modalità di gestione degli aggiornamenti](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image18.png)

> [!WARNING]
> <span data-ttu-id="6ccd8-183">Dato che il server di destinazione master per Azure Site Recovery richiede una versione molto specifica di Ubuntu, è necessario assicurarsi che gli aggiornamenti del kernel siano disabilitati per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-183">Because the Azure Site Recovery master target server requires a very specific version of the Ubuntu, you need to ensure that the kernel upgrades are disabled for the virtual machine.</span></span> <span data-ttu-id="6ccd8-184">Se sono abilitati, eventuali aggiornamenti regolari causeranno malfunzionamenti del server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-184">If they are enabled, then any regular upgrades cause the master target server to malfunction.</span></span> <span data-ttu-id="6ccd8-185">Assicurarsi di selezionare l'opzione **No automatic updates** (Aggiornamenti automatici non consentiti).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-185">Make sure you select the **No automatic updates** option.</span></span>


<span data-ttu-id="6ccd8-186">**Passaggio 20:** selezionare le opzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-186">**Step 20:** Select default options.</span></span> <span data-ttu-id="6ccd8-187">Per usare connessioni openSSH per SSH, selezionare l'opzione **OpenSSH server** (Server OpenSSH) e selezionare **Continue** (Continua).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-187">If you want openSSH for SSH connect, select the **OpenSSH server** option, and then select **Continue**.</span></span>

![Selezionare il software](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image19.png)

<span data-ttu-id="6ccd8-189">**Passaggio 21:** selezionare **Sì** e quindi **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-189">**Step 21:** Select **Yes**, and then select **Enter**.</span></span>

![Installare il caricatore di avvio GRUB](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image20.png)

<span data-ttu-id="6ccd8-191">**Passaggio 22:** selezionare il dispositivo appropriato per l'installazione del caricatore di avvio (preferibilmente **/dev/sda**), quindi selezionare **Invio**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-191">**Step 22:** Select the appropriate device for the boot loader installation (preferably **/dev/sda**), and then select **Enter**.</span></span>

![Selezionare un dispositivo per l'installazione del caricatore di avvio](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image21.png)

<span data-ttu-id="6ccd8-193">**Passaggio 23:** selezionare **Continue** (Continua) e premere **Invio** per completare l'installazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-193">**Step 23:** Select **Continue**, and then select **Enter** to finish the installation.</span></span>

![Completare l'installazione](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image22.png)

<span data-ttu-id="6ccd8-195">Al termine dell'installazione, accedere alla macchina virtuale con le nuove credenziali utente.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-195">After the installation has finished, sign in to the VM with the new user credentials.</span></span> <span data-ttu-id="6ccd8-196">(Fare riferimento al **Passaggio 10** per ulteriori informazioni.)</span><span class="sxs-lookup"><span data-stu-id="6ccd8-196">(Refer to **Step 10** for more information.)</span></span>

<span data-ttu-id="6ccd8-197">Eseguire i passaggi descritti nella schermata seguente per impostare la password dell'utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-197">Take the steps that are described in the following screenshot to set the ROOT user password.</span></span> <span data-ttu-id="6ccd8-198">Quindi, accedere come utente ROOT.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-198">Then sign in as ROOT user.</span></span>

![Impostare la password dell'utente ROOT](./media/site-recovery-how-to-install-linux-master-target/ubuntu/image23.png)


### <a name="prepare-the-machine-for-configuration-as-a-master-target-server"></a><span data-ttu-id="6ccd8-200">Preparare il computer per la configurazione come server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-200">Prepare the machine for configuration as a master target server</span></span>
<span data-ttu-id="6ccd8-201">Successivamente, preparare il computer per la configurazione come server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-201">Next, prepare the machine for configuration as a master target server.</span></span>

<span data-ttu-id="6ccd8-202">Per ottenere l'ID per ogni disco rigido SCSI in una macchina virtuale Linux, abilitare il parametro **disk.EnableUUID = TRUE**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-202">To get the ID for each SCSI hard disk in a Linux virtual machine, enable the **disk.EnableUUID = TRUE** parameter.</span></span>

<span data-ttu-id="6ccd8-203">Per abilitare il parametro, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-203">To enable this parameter, take the following steps:</span></span>

1. <span data-ttu-id="6ccd8-204">Arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-204">Shut down your virtual machine.</span></span>

2. <span data-ttu-id="6ccd8-205">Fare clic con il pulsante destro del mouse sulla voce della macchina virtuale nel riquadro a sinistra e quindi scegliere **Edit Settings**(Modifica impostazioni).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-205">Right-click the entry for the virtual machine in the left pane, and then select **Edit Settings**.</span></span>

3. <span data-ttu-id="6ccd8-206">Scegliere la scheda **Options** (Opzioni).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-206">Select the **Options** tab.</span></span>

4. <span data-ttu-id="6ccd8-207">Nel riquadro a sinistra, selezionare **Advanced** > **General** (Avanzate - Generale, quindi selezionare il pulsante **Configuration Parameters** (Parametri di configurazione) nella parte inferiore destra della schermata.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-207">In the left pane, select **Advanced** > **General**, and then select the **Configuration Parameters** button on the lower-right part of the screen.</span></span>

    ![Scheda Opzioni](./media/site-recovery-how-to-install-linux-master-target/media/image20.png)

    <span data-ttu-id="6ccd8-209">L'opzione **Configuration Parameters** (Parametri di configurazione) è disponibile solo quando il computer è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-209">The **Configuration Parameters** option is not available when the machine is running.</span></span> <span data-ttu-id="6ccd8-210">Per attivare la scheda, arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-210">To make this tab active, shut down the virtual machine.</span></span>

5. <span data-ttu-id="6ccd8-211">Controllare se esiste già una riga con il valore **disk.EnableUUID**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-211">See whether a row with **disk.EnableUUID** already exists.</span></span>

    - <span data-ttu-id="6ccd8-212">Se il valore esiste ed è impostato su **False**, modificarlo in **True**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-212">If the value exists and is set to **False**, change the value to **True**.</span></span> <span data-ttu-id="6ccd8-213">(I valori non fanno distinzione tra maiuscole e minuscole.)</span><span class="sxs-lookup"><span data-stu-id="6ccd8-213">(The values are not case-sensitive.)</span></span>

    - <span data-ttu-id="6ccd8-214">Se il valore è presente ed è impostato su **True**, selezionare **Cancel** (Annulla).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-214">If the value exists and is set to **True**, select **Cancel**.</span></span>

    - <span data-ttu-id="6ccd8-215">Se il valore non esiste, selezionare **Add Row**(Aggiungi riga).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-215">If the value does not exist, select **Add Row**.</span></span>

    - <span data-ttu-id="6ccd8-216">Nella colonna del nome, aggiungere **disk.EnableUUID**, quindi impostare il valore su **TRUE**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-216">In the name column, add **disk.EnableUUID**, and then set the value to **TRUE**.</span></span>

    ![Controllare se esiste già una riga con il valore disk.EnableUUID](./media/site-recovery-how-to-install-linux-master-target/media/image21.png)

#### <a name="disable-kernel-upgrades"></a><span data-ttu-id="6ccd8-218">Disabilitare gli aggiornamenti del kernel</span><span class="sxs-lookup"><span data-stu-id="6ccd8-218">Disable kernel upgrades</span></span>

<span data-ttu-id="6ccd8-219">Dato che il server di destinazione master per Azure Site Recovery richiede una versione molto specifica di Ubuntu, assicurarsi che gli aggiornamenti del kernel siano disabilitati per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-219">Azure Site Recovery master target server requires a very specific version of the Ubuntu, ensure that the kernel upgrades are disabled for the virtual machine.</span></span>

<span data-ttu-id="6ccd8-220">Se sono abilitati, eventuali aggiornamenti regolari causeranno malfunzionamenti del server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-220">If kernel upgrades are enabled, then any regular upgrades cause the master target server to malfunction.</span></span>

#### <a name="download-and-install-additional-packages"></a><span data-ttu-id="6ccd8-221">Scaricare e installare i pacchetti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="6ccd8-221">Download and install additional packages</span></span>

> [!NOTE]
> <span data-ttu-id="6ccd8-222">Verificare di disporre della connettività Internet per scaricare e installare pacchetti aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-222">Make sure that you have Internet connectivity to download and install additional packages.</span></span> <span data-ttu-id="6ccd8-223">Se non si dispone di connettività Internet, è necessario trovare manualmente i pacchetti RPM e installarli.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-223">If you don't have Internet connectivity, you need to manually find these RPM packages and install them.</span></span>

```
apt-get install -y multipath-tools lsscsi python-pyasn1 lvm2 kpartx
```

### <a name="get-the-installer-for-setup"></a><span data-ttu-id="6ccd8-224">Ottenere il programma di installazione per l'installazione</span><span class="sxs-lookup"><span data-stu-id="6ccd8-224">Get the installer for setup</span></span>

<span data-ttu-id="6ccd8-225">Se il server di destinazione master dispone della connettività Internet, è possibile attenersi alla procedura seguente per scaricare il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-225">If your master target has Internet connectivity, you can use the following steps to download the installer.</span></span> <span data-ttu-id="6ccd8-226">In caso contrario, copiare il programma di installazione dal server di elaborazione e installarlo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-226">Otherwise, you can copy the installer from the process server and then install it.</span></span>

#### <a name="download-the-master-target-installation-packages"></a><span data-ttu-id="6ccd8-227">Scaricare i pacchetti di installazione del server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-227">Download the master target installation packages</span></span>

<span data-ttu-id="6ccd8-228">[Scaricare il file di installazione più recente del server di destinazione master Linux](https://aka.ms/latestlinuxmobsvc).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-228">[Download the latest Linux master target installation bits](https://aka.ms/latestlinuxmobsvc).</span></span>

<span data-ttu-id="6ccd8-229">Per scaricarli usando Linux, digitare:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-229">To download it by using Linux, type:</span></span>

```
wget https://aka.ms/latestlinuxmobsvc -O latestlinuxmobsvc.tar.gz
```

<span data-ttu-id="6ccd8-230">Verificare di scaricare e decomprimere il programma di installazione nella home directory.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-230">Make sure that you download and unzip the installer in your home directory.</span></span> <span data-ttu-id="6ccd8-231">Se il file viene decompresso nel percorso **/usr/Locale**, l'installazione avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-231">If you unzip to **/usr/Local**, then the installation  fails.</span></span>


#### <a name="access-the-installer-from-the-process-server"></a><span data-ttu-id="6ccd8-232">Accedere al programma di installazione dal server di elaborazione</span><span class="sxs-lookup"><span data-stu-id="6ccd8-232">Access the installer from the process server</span></span>

1. <span data-ttu-id="6ccd8-233">Sul server di elaborazione passare alla directory **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-233">On the process server, go to **C:\Program Files (x86)\Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository**.</span></span>

2. <span data-ttu-id="6ccd8-234">Copiare il file del programma di installazione necessario dal server di elaborazione e salvarlo come **latestlinuxmobsvc.tar.gz** nella home directory.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-234">Copy the required installer file from the process server, and save it as **latestlinuxmobsvc.tar.gz** in your home directory.</span></span>


### <a name="apply-custom-configuration-changes"></a><span data-ttu-id="6ccd8-235">Applicare le modifiche di configurazione personalizzate</span><span class="sxs-lookup"><span data-stu-id="6ccd8-235">Apply custom configuration changes</span></span>

<span data-ttu-id="6ccd8-236">Per applicare le modifiche di configurazione personalizzate, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-236">To apply custom configuration changes, use the following steps:</span></span>


1. <span data-ttu-id="6ccd8-237">Eseguire il seguente comando per decomprimere il file binario.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-237">Run the following command to untar the binary.</span></span>
    ```
    tar -zxvf latestlinuxmobsvc.tar.gz
    ```
    ![Schermata del comando da eseguire](./media/site-recovery-how-to-install-linux-master-target/image16.png)

2. <span data-ttu-id="6ccd8-239">Eseguire il comando seguente per fornire le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-239">Run the following command to give permission.</span></span>
    ```
    chmod 755 ./ApplyCustomChanges.sh
    ```

3. <span data-ttu-id="6ccd8-240">Eseguire il comando seguente per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-240">Run the following command to run the script.</span></span>
    ```
    ./ApplyCustomChanges.sh
    ```
> [!NOTE]
> <span data-ttu-id="6ccd8-241">Eseguire lo script solo una volta sul server.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-241">Run the script only once on the server.</span></span> <span data-ttu-id="6ccd8-242">Arrestare il server.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-242">Shut down the server.</span></span> <span data-ttu-id="6ccd8-243">Riavviare il server dopo aver aggiunto un disco come indicato nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-243">Then restart the server after you add a disk, as described in the next section.</span></span>

### <a name="add-a-retention-disk-to-the-linux-master-target-virtual-machine"></a><span data-ttu-id="6ccd8-244">Aggiungere un disco di conservazione alla macchina virtuale del server di destinazione master Linux</span><span class="sxs-lookup"><span data-stu-id="6ccd8-244">Add a retention disk to the Linux master target virtual machine</span></span>

<span data-ttu-id="6ccd8-245">Per creare un disco di conservazione, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-245">Use the following steps to create a retention disk:</span></span>

1. <span data-ttu-id="6ccd8-246">Collegare un nuovo disco da 1 TB alla macchina virtuale del server di destinazione master Linux e avviare il computer.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-246">Attach a new 1-TB disk to the Linux master target virtual machine, and then start the machine.</span></span>

2. <span data-ttu-id="6ccd8-247">Usare il comando **multipath -ll** per conoscere l'ID a percorsi multipli del disco di conservazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-247">Use the **multipath -ll** command to learn the multipath ID of the retention disk.</span></span>

    ```
    multipath -ll
    ```
    ![ID a percorsi multipli del disco di conservazione](./media/site-recovery-how-to-install-linux-master-target/media/image22.png)

3. <span data-ttu-id="6ccd8-249">Formattare l'unità e creare un file system nella nuova unità.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-249">Format the drive, and then create a file system on the new drive.</span></span>

    ```
    mkfs.ext4 /dev/mapper/<Retention disk's multipath id>
    ```
    ![Creazione di un file system nell'unità](./media/site-recovery-how-to-install-linux-master-target/media/image23.png)

4. <span data-ttu-id="6ccd8-251">Dopo aver creato il file system, montare il disco di conservazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-251">After you create the file system, mount the retention disk.</span></span>
    ```
    mkdir /mnt/retention
    mount /dev/mapper/<Retention disk's multipath id> /mnt/retention
    ```
    ![Montaggio del disco di conservazione](./media/site-recovery-how-to-install-linux-master-target/media/image24.png)

5. <span data-ttu-id="6ccd8-253">Creare la voce **fstab** per montare l'unità di conservazione a ogni avvio del sistema.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-253">Create the **fstab** entry to mount the retention drive every time the system starts.</span></span>
    ```
    vi /etc/fstab
    ```
    <span data-ttu-id="6ccd8-254">Selezionare **Inserisci** per iniziare a modificare il file.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-254">Select **Insert** to begin editing the file.</span></span> <span data-ttu-id="6ccd8-255">Creare una nuova riga e inserirvi il testo seguente.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-255">Create a new line, and then insert the following text.</span></span> <span data-ttu-id="6ccd8-256">Modificare l'ID a percorsi multipli disco in base all'ID a percorsi multipli evidenziato dal comando precedente.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-256">Edit the disk multipath ID based on the highlighted multipath ID from the previous command.</span></span>

    <span data-ttu-id="6ccd8-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span><span class="sxs-lookup"><span data-stu-id="6ccd8-257">**/dev/mapper/<Retention disks multipath id> /mnt/retention ext4 rw 0 0**</span></span>

    <span data-ttu-id="6ccd8-258">Premere **Esc** e digitare **:wq**, che sta per scrivi ed esci, per chiudere la finestra dell'editor.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-258">Select **Esc**, and then type **:wq** (write and quit) to close the editor window.</span></span>

### <a name="install-the-master-target"></a><span data-ttu-id="6ccd8-259">Installare il server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-259">Install the master target</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ccd8-260">La versione del server di destinazione master deve essere uguale o precedente a quella del server di elaborazione e del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-260">The version of the master target server must be equal to or earlier than the versions of the process server and the configuration server.</span></span> <span data-ttu-id="6ccd8-261">Se la versione del server master di destinazione è superiore, la riprotezione avrà esito positivo, ma la replica avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-261">If this condition is not met, reprotect succeeds, but replication fails.</span></span>


> [!NOTE]
> <span data-ttu-id="6ccd8-262">Prima di installare il server master di destinazione, assicurarsi che il file **/etc/hosts** nella macchina virtuale contenga le voci che eseguono il mapping del nome host locale agli indirizzi IP associati a tutte le schede di rete.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-262">Before you install the master target server, check that the **/etc/hosts** file on the virtual machine contains entries that map the local hostname to the IP addresses that are associated with all network adapters.</span></span>

1. <span data-ttu-id="6ccd8-263">Copiare la passphrase CS da **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** nel server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-263">Copy the passphrase from **C:\ProgramData\Microsoft Azure Site Recovery\private\connection.passphrase** on the configuration server.</span></span> <span data-ttu-id="6ccd8-264">Quindi salvarla come **passphrase.txt** nella stessa directory locale eseguendo il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-264">Then save it as **passphrase.txt** in the same local directory by running the following command:</span></span>

    ```
    echo <passphrase> >passphrase.txt
    ```
    <span data-ttu-id="6ccd8-265">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-265">Example:</span></span> 
    
    ```
    echo itUx70I47uxDuUVY >passphrase.txt
    ```

2. <span data-ttu-id="6ccd8-266">Prendere nota dell'indirizzo IP del server di configurazione,</span><span class="sxs-lookup"><span data-stu-id="6ccd8-266">Note the configuration server's IP address.</span></span> <span data-ttu-id="6ccd8-267">perché sarà necessario nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-267">You need it in the next step.</span></span>

3. <span data-ttu-id="6ccd8-268">Eseguire il comando seguente per installare il server di destinazione master e registrarlo con il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-268">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```

    <span data-ttu-id="6ccd8-269">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-269">Example:</span></span> 
    
    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

    <span data-ttu-id="6ccd8-270">Attendere il termine dello script.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-270">Wait until the script finishes.</span></span> <span data-ttu-id="6ccd8-271">Se il server di destinazione master viene registrato correttamente, viene elencato nella pagina **Infrastruttura di Site Recovery** nel portale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-271">If the master target registers sucessfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


#### <a name="install-the-master-target-by-using-interactive-installation"></a><span data-ttu-id="6ccd8-272">Installazione interattiva del server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-272">Install the master target by using interactive installation</span></span>

1. <span data-ttu-id="6ccd8-273">Eseguire il comando seguente per installare il server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-273">Run the following command to install the master target.</span></span> <span data-ttu-id="6ccd8-274">Per il ruolo agente selezionare **Master Target**.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-274">For the agent role, choose **Master Target**.</span></span>

    ```
    ./install
    ```

2. <span data-ttu-id="6ccd8-275">Selezionare il percorso predefinito per l'installazione, quindi premere **Invio** per continuare.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-275">Choose the default location for installation, and then select **Enter** to continue.</span></span>

    ![Scelta di un percorso predefinito per l'installazione del server di destinazione master](./media/site-recovery-how-to-install-linux-master-target/image17.png)

<span data-ttu-id="6ccd8-277">Dopo aver completato l'installazione, registrare il server di configurazione tramite la riga di comando.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-277">After the installation has finished, register the configuration server by using the command line.</span></span>

1. <span data-ttu-id="6ccd8-278">Annotare l'indirizzo IP del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-278">Note the IP address of the configuration server.</span></span> <span data-ttu-id="6ccd8-279">perché sarà necessario nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-279">You need it in the next step.</span></span>

2. <span data-ttu-id="6ccd8-280">Eseguire il comando seguente per installare il server di destinazione master e registrarlo con il server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-280">Run the following command to install the master target server and register the server with the configuration server.</span></span>

    ```
    ./install -q -d /usr/local/ASR -r MT -v VmWare
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <ConfigurationServer IP Address> -P passphrase.txt
    ```
    <span data-ttu-id="6ccd8-281">Esempio:</span><span class="sxs-lookup"><span data-stu-id="6ccd8-281">Example:</span></span> 

    ```
    /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i 104.40.75.37 -P passphrase.txt
    ```

   <span data-ttu-id="6ccd8-282">Attendere il termine dello script.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-282">Wait until the script finishes.</span></span> <span data-ttu-id="6ccd8-283">Se il server di destinazione master viene registrato correttamente, viene elencato nella pagina **Infrastruttura di Site Recovery** nel portale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-283">If the master target is registered succesfully, the master target is listed on the **Site Recovery Infrastructure** page of the portal.</span></span>


### <a name="upgrade-the-master-target"></a><span data-ttu-id="6ccd8-284">Aggiornare il server di destinazione master</span><span class="sxs-lookup"><span data-stu-id="6ccd8-284">Upgrade the master target</span></span>

<span data-ttu-id="6ccd8-285">Eseguire il programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-285">Run the installer.</span></span> <span data-ttu-id="6ccd8-286">Tale programma rileva automaticamente che l'agente è installato nella destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-286">It automatically detects that the agent is installed on the master target.</span></span> <span data-ttu-id="6ccd8-287">Selezionare **Y** per eseguire l'aggiornamento.  Una volta completata l'installazione, controllare la versione della destinazione master installata con il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-287">To upgrade, select **Y**.  After the setup has been completed, check the version of the master target installed by using the following command.</span></span>

    ```
    cat /usr/local/.vx_version
    ```

<span data-ttu-id="6ccd8-288">È possibile vedere che il campo **Version** indica il numero di versione della destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-288">You can see that the **Version** field gives the version number of the master target.</span></span>

### <a name="install-vmware-tools-on-the-master-target-server"></a><span data-ttu-id="6ccd8-289">Installare gli strumenti VMware nel server master di destinazione</span><span class="sxs-lookup"><span data-stu-id="6ccd8-289">Install VMware tools on the master target server</span></span>

<span data-ttu-id="6ccd8-290">È necessario installare gli strumenti VMware per consentire al server di destinazione master di rilevare gli archivi dati.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-290">You need to install VMware tools on the master target so that it can discover the data stores.</span></span> <span data-ttu-id="6ccd8-291">Se non sono installati gli strumenti, la schermata di riprotezione non viene elencata negli archivi dati.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-291">If the tools are not installed, the reprotect screen isn't listed in the data stores.</span></span> <span data-ttu-id="6ccd8-292">Dopo l'installazione degli strumenti VMware è necessario riavviare il computer.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-292">After installation of the VMware tools, you need to restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ccd8-293">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ccd8-293">Next steps</span></span>
<span data-ttu-id="6ccd8-294">Al termine dell'installazione e della registrazione del server, quest'ultimo viene visualizzato nella sezione del **server di destinazione master** della pagina **Infrastruttura di Site Recovery**, nella panoramica del server di configurazione.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-294">After the installation and registration of the master target has finsihed, you can see the master target appear on the **Master Target** section in **Site Recovery Infrastructure**, under the configuration server overview.</span></span>

<span data-ttu-id="6ccd8-295">È ora possibile procedere con la [riprotezione](site-recovery-how-to-reprotect.md), seguita dal failback.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-295">You can now proceed with [reprotection](site-recovery-how-to-reprotect.md), followed by failback.</span></span>

## <a name="common-issues"></a><span data-ttu-id="6ccd8-296">Problemi comuni</span><span class="sxs-lookup"><span data-stu-id="6ccd8-296">Common issues</span></span>

* <span data-ttu-id="6ccd8-297">Verificare che Storage vMotion non sia abilitato in alcun componente di gestione, ad esempio il server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-297">Make sure you do not turn on Storage vMotion on any management components such as a master target.</span></span> <span data-ttu-id="6ccd8-298">Se il server di destinazione master viene spostato dopo una riprotezione con esito positivo, non è possibile scollegare i dischi della macchina virtuale (VMDK).</span><span class="sxs-lookup"><span data-stu-id="6ccd8-298">If the master target moves after a successful reprotect, the virtual machine disks (VMDKs) cannot be detached.</span></span> <span data-ttu-id="6ccd8-299">In questo caso, il failback avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-299">In this case, failback fails.</span></span>

* <span data-ttu-id="6ccd8-300">Il server di destinazione master non deve includere snapshot nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-300">The master target should not have any snapshots on the virtual machine.</span></span> <span data-ttu-id="6ccd8-301">Se sono presenti snapshot, il failback avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-301">If there are snapshots, failback fails.</span></span>

* <span data-ttu-id="6ccd8-302">Per via delle configurazioni personalizzate della scheda di interfaccia di rete presso alcuni clienti, l'interfaccia di rete viene disabilitata durante l'avvio e non è possibile inizializzare l'agente del server di destinazione master.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-302">Due to some custom NIC configurations at some customers, the network interface is disabled during startup, and the master target agent cannot initialize.</span></span> <span data-ttu-id="6ccd8-303">Verificare che le proprietà seguenti siano impostate correttamente.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-303">Make sure that the following properties are correctly set.</span></span> <span data-ttu-id="6ccd8-304">Verificare le proprietà nei file della scheda Ethernet /etc/sysconfig/network-scripts/ifcfg-eth*.</span><span class="sxs-lookup"><span data-stu-id="6ccd8-304">Check these properties in the Ethernet card file's /etc/sysconfig/network-scripts/ifcfg-eth*.</span></span>
    * <span data-ttu-id="6ccd8-305">BOOTPROTO=dhcp</span><span class="sxs-lookup"><span data-stu-id="6ccd8-305">BOOTPROTO=dhcp</span></span>
    * <span data-ttu-id="6ccd8-306">ONBOOT=yes</span><span class="sxs-lookup"><span data-stu-id="6ccd8-306">ONBOOT=yes</span></span>
