---
title: aaaSet di Oracle ASM in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Attivare e mettere in funzione rapidamente Oracle ASM nell'ambiente Azure.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="35cba-103">Configurare Oracle ASM su una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="35cba-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="35cba-104">Le macchine virtuali di Azure offrono un ambiente di elaborazione completamente configurabile e flessibile.</span><span class="sxs-lookup"><span data-stu-id="35cba-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="35cba-105">In questa esercitazione vengono illustrate la distribuzione di macchina virtuale di Azure basic combinata con hello installazione e configurazione di Oracle automatizzata Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="35cba-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="35cba-106">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="35cba-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="35cba-107">Creare e connettersi a Oracle Database VM tooan</span><span class="sxs-lookup"><span data-stu-id="35cba-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="35cba-108">Installare e configurare Oracle Automated Storage Management</span><span class="sxs-lookup"><span data-stu-id="35cba-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="35cba-109">Installare e configurare l'infrastruttura di Oracle Grid</span><span class="sxs-lookup"><span data-stu-id="35cba-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="35cba-110">Inizializzare l'installazione di Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35cba-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="35cba-111">Creare un database Oracle gestito da ASM</span><span class="sxs-lookup"><span data-stu-id="35cba-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="35cba-112">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="35cba-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="35cba-113">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="35cba-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="35cba-114">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="35cba-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="35cba-115">Preparare l'ambiente hello</span><span class="sxs-lookup"><span data-stu-id="35cba-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="35cba-116">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="35cba-116">Create a resource group</span></span>

<span data-ttu-id="35cba-117">toocreate un gruppo di risorse, utilizzare hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="35cba-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="35cba-118">Un gruppo di risorse di Azure è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite.</span><span class="sxs-lookup"><span data-stu-id="35cba-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="35cba-119">In questo esempio, un gruppo di risorse denominato *myResourceGroup* in hello *eastus* area.</span><span class="sxs-lookup"><span data-stu-id="35cba-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="35cba-120">Creare una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="35cba-120">Create a VM</span></span>

<span data-ttu-id="35cba-121">toocreate una macchina virtuale basata sull'immagine di Oracle Database hello e configurarlo toouse Oracle ASM, usare hello [creare vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="35cba-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="35cba-122">Hello seguente viene creata una macchina virtuale denominata myVM che è una dimensione Standard_DS2_v2 con quattro dischi dati collegati di 50 GB.</span><span class="sxs-lookup"><span data-stu-id="35cba-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="35cba-123">Se non esistono già nel percorso della chiave predefinita hello, crea anche le chiavi SSH.</span><span class="sxs-lookup"><span data-stu-id="35cba-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="35cba-124">toouse uno specifico set di chiavi, utilizzare hello `--ssh-key-value` opzione.</span><span class="sxs-lookup"><span data-stu-id="35cba-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="35cba-125">Dopo aver creato una macchina virtuale hello, CLI di Azure consente di visualizzare informazioni toohello simile esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="35cba-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="35cba-126">Si noti il valore di hello per `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="35cba-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="35cba-127">Utilizzare questo hello tooaccess indirizzo macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="35cba-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="35cba-128">Connettersi toohello VM</span><span class="sxs-lookup"><span data-stu-id="35cba-128">Connect toohello VM</span></span>

<span data-ttu-id="35cba-129">toocreate una sessione SSH con hello VM e configurare impostazioni aggiuntive, usare hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="35cba-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="35cba-130">Sostituire l'indirizzo IP hello con hello `publicIpAddress` valore per la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="35cba-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="35cba-131">Installare Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35cba-131">Install Oracle ASM</span></span>

<span data-ttu-id="35cba-132">tooinstall Oracle ASM, hello completo alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="35cba-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="35cba-133">Per altre informazioni sull'installazione di Oracle ASM, vedere [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html) (Download di Oracle ASMLib per Oracle Linux 6).</span><span class="sxs-lookup"><span data-stu-id="35cba-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="35cba-134">È necessario toologin come radice in ordine toocontinue con installazione ASM:</span><span class="sxs-lookup"><span data-stu-id="35cba-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="35cba-135">Eseguire questi comandi aggiuntivi componenti Oracle ASM tooinstall:</span><span class="sxs-lookup"><span data-stu-id="35cba-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="35cba-136">Verificare che Oracle ASM sia installato:</span><span class="sxs-lookup"><span data-stu-id="35cba-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="35cba-137">output di Hello di questo comando deve includere hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="35cba-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="35cba-138">ASM richiede specifici utenti e ruoli in ordine toofunction correttamente.</span><span class="sxs-lookup"><span data-stu-id="35cba-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="35cba-139">Hello seguenti comandi di Crea gruppi e account utente prerequisito hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="35cba-140">Verificare che utenti e gruppi siano stati creati correttamente:</span><span class="sxs-lookup"><span data-stu-id="35cba-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="35cba-141">Hello output di questo comando deve includere seguente hello utenti e gruppi:</span><span class="sxs-lookup"><span data-stu-id="35cba-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="35cba-142">Creare una cartella per l'utente *griglia* e modificare il proprietario di hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="35cba-143">Configurare Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35cba-143">Set up Oracle ASM</span></span>

<span data-ttu-id="35cba-144">Per questa esercitazione, è l'utente predefinito hello *griglia* e il gruppo predefinito hello è *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="35cba-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="35cba-145">Verificare che hello *oracle* l'utente faccia parte del gruppo asmadmin hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="35cba-146">tooset installazione Oracle ASM, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="35cba-147">Impostazione dei driver di hello Oracle ASM libreria include la definizione utente predefinito hello (griglia) e il gruppo predefinito (asmadmin) nonché configurazione toostart unità hello all'avvio del sistema (selezione y) e tooscan per i dischi di avvio (selezione y).</span><span class="sxs-lookup"><span data-stu-id="35cba-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="35cba-148">È necessario tooanswer hello richieste da hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="35cba-149">output di Hello di questo comando dovrebbe essere simile toohello seguente, l'arresto con richieste toobe ha risposto.</span><span class="sxs-lookup"><span data-stu-id="35cba-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="35cba-150">Configurazione del disco Visualizza hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="35cba-151">output di Hello di questo comando dovrebbe essere simile toohello seguente elenco di dischi disponibili</span><span class="sxs-lookup"><span data-stu-id="35cba-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="35cba-152">Formattare il disco *dev/sdc* eseguendo hello comando seguente e rispondere alle hello prompt con:</span><span class="sxs-lookup"><span data-stu-id="35cba-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="35cba-153">*n* per una nuova partizione</span><span class="sxs-lookup"><span data-stu-id="35cba-153">*n* for new partition</span></span>
   - <span data-ttu-id="35cba-154">*p* per una partizione primaria</span><span class="sxs-lookup"><span data-stu-id="35cba-154">*p* for primary partition</span></span>
   - <span data-ttu-id="35cba-155">*1* partizione prima di hello tooselect</span><span class="sxs-lookup"><span data-stu-id="35cba-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="35cba-156">Premere `enter` per primo cilindro di hello predefinito</span><span class="sxs-lookup"><span data-stu-id="35cba-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="35cba-157">Premere `enter` per ultimo cilindro di hello predefinito</span><span class="sxs-lookup"><span data-stu-id="35cba-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="35cba-158">Premere *w* tabella di partizione toohello toowrite hello modifiche</span><span class="sxs-lookup"><span data-stu-id="35cba-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="35cba-159">Utilizza le risposte hello riportate sopra, output di hello per comando fdisk hello dovrebbe essere simile hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="35cba-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="35cba-160">Ripetizione hello precedente comando fdisk per `/dev/sdd`, `/dev/sde`, e `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="35cba-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="35cba-161">Controllare la configurazione disco hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="35cba-162">output di Hello del comando hello dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="35cba-163">Controllare lo stato del servizio Oracle ASM hello e avviare il servizio Oracle ASM hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="35cba-164">output di Hello del comando hello dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="35cba-165">Creare dischi Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="35cba-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="35cba-166">output di Hello del comando hello dovrebbe essere simile hello seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="35cba-167">Elencare i dischi Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="35cba-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="35cba-168">output di Hello del comando hello deve includere off hello dischi ASM Oracle seguenti:</span><span class="sxs-lookup"><span data-stu-id="35cba-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="35cba-169">Modificare le password hello per gli utenti di radice, oracle e griglia hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="35cba-170">**Prendere nota di queste nuove password** come vengano utilizzati in un secondo momento durante l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="35cba-171">Modificare le autorizzazioni di cartella hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="35cba-172">Scaricare e preparare Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="35cba-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="35cba-173">toodownload e preparare il software Oracle griglia infrastruttura hello, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="35cba-174">Scaricare l'infrastruttura di griglia di Oracle da hello [pagina di download di Oracle ASM](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="35cba-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="35cba-175">Nell'area download di hello intitolato **Oracle Database 12C versione 1 griglia infrastruttura (12.1.0.2.0) per Linux x86-64**, scaricare i file con estensione zip hello due.</span><span class="sxs-lookup"><span data-stu-id="35cba-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="35cba-176">Dopo aver scaricato hello ZIP file tooyour client computer, è possibile utilizzare il protocollo Secure di copia (SCP) toocopy hello file tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="35cba-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="35cba-177">SSH nuovamente la macchina virtuale di Oracle in Azure in file con estensione zip ordine toomove hello in hello /OPT cartella.</span><span class="sxs-lookup"><span data-stu-id="35cba-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="35cba-178">Quindi, modificare il proprietario di hello del file hello:</span><span class="sxs-lookup"><span data-stu-id="35cba-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="35cba-179">Decomprimere i file hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-179">Unzip hello files.</span></span> <span data-ttu-id="35cba-180">(Installazione hello Linux decomprimere strumento se non è già installato)</span><span class="sxs-lookup"><span data-stu-id="35cba-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="35cba-181">Modificare l'autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="35cba-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="35cba-182">Aggiornare lo spazio di swapping configurato.</span><span class="sxs-lookup"><span data-stu-id="35cba-182">Update configured swap space.</span></span> <span data-ttu-id="35cba-183">Componenti di una griglia Oracle è necessario almeno 6,8 GB di spazio di swapping tooinstall griglia.</span><span class="sxs-lookup"><span data-stu-id="35cba-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="35cba-184">dimensioni file di scambio Hello predefinite per le immagini di Oracle Linux in Azure sono solo a 2048MB.</span><span class="sxs-lookup"><span data-stu-id="35cba-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="35cba-185">È necessario tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` riavviare servizio WALinuxAgent hello per effetto di tootake hello aggiornata le impostazioni e dei file.</span><span class="sxs-lookup"><span data-stu-id="35cba-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="35cba-186">Poiché si tratta di un file di sola lettura, è necessario l'accesso in scrittura tooenable autorizzazioni file toochange.</span><span class="sxs-lookup"><span data-stu-id="35cba-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="35cba-187">Cercare `ResourceDisk.SwapSizeMB` e modificare il valore di hello troppo**8192**.</span><span class="sxs-lookup"><span data-stu-id="35cba-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="35cba-188">Sarà necessario toopress `insert` tooenter modalità di inserimento, tipo di valore hello **8192** e quindi premere `esc` tooreturn toocommand modalità.</span><span class="sxs-lookup"><span data-stu-id="35cba-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="35cba-189">le modifiche di hello toowrite e file hello quit, digitare `:wq` e premere `enter`.</span><span class="sxs-lookup"><span data-stu-id="35cba-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="35cba-190">È consigliabile utilizzare sempre `WALinuxAgent` tooconfigure spazio di swapping in modo che viene sempre creato hello temporaneo disco locale (disco temporaneo) per ottenere prestazioni ottimali.</span><span class="sxs-lookup"><span data-stu-id="35cba-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="35cba-191">Per ulteriori informazioni, vedere [come tooadd uno scambio di file in macchine virtuali Linux Azure](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="35cba-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="35cba-192">Preparare il client locale e VM toorun x11</span><span class="sxs-lookup"><span data-stu-id="35cba-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="35cba-193">La configurazione di Oracle ASM richiede un'interfaccia grafica toocomplete hello installazione e configurazione.</span><span class="sxs-lookup"><span data-stu-id="35cba-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="35cba-194">Usiamo hello x11 protocollo toofacilitate questa installazione.</span><span class="sxs-lookup"><span data-stu-id="35cba-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="35cba-195">Se si utilizza un sistema client (Mac o Linux) che dispone già di X11 funzionalità abilitato e configurato, è possibile ignorare questa configurazione e tooWindows esclusivo macchine del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="35cba-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="35cba-196">[Scaricare PuTTY](http://www.putty.org/) e [scaricare Xming](https://xming.en.softonic.com/) tooyour computer di Windows.</span><span class="sxs-lookup"><span data-stu-id="35cba-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="35cba-197">Installazione di hello toocomplete di entrambe le applicazioni con i valori predefiniti di hello prima di procedere sarà necessario.</span><span class="sxs-lookup"><span data-stu-id="35cba-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="35cba-198">Dopo aver installato PuTTY, aprire un prompt dei comandi, modificare in hello PuTTY cartella (ad esempio, c:\Programmi\Microsoft Files\PuTTY) ed eseguire `puttygen.exe` in ordine toogenerate una chiave.</span><span class="sxs-lookup"><span data-stu-id="35cba-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="35cba-199">Nel generatore di chiavi PuTTY:</span><span class="sxs-lookup"><span data-stu-id="35cba-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="35cba-200">Generare una chiave selezionando hello `Generate` pulsante.</span><span class="sxs-lookup"><span data-stu-id="35cba-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="35cba-201">Copiare il contenuto di hello della chiave di hello (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="35cba-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="35cba-202">Seleziona hello `Save private key` pulsante.</span><span class="sxs-lookup"><span data-stu-id="35cba-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="35cba-203">Ignorare l'avviso hello sulla protezione chiave hello con una passphrase e quindi selezionare `OK`.</span><span class="sxs-lookup"><span data-stu-id="35cba-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Screenshot del generatore di chiavi PuTTY](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="35cba-205">Nella macchina virtuale eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="35cba-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="35cba-206">Creare un file denominato `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="35cba-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="35cba-207">Incollare il contenuto di hello della chiave di hello in questo file e quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35cba-208">chiave di Hello deve contenere la stringa hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="35cba-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="35cba-209">Inoltre, il contenuto di hello della chiave hello deve essere una singola riga di testo.</span><span class="sxs-lookup"><span data-stu-id="35cba-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="35cba-210">Nel sistema client, avviare PuTTY.</span><span class="sxs-lookup"><span data-stu-id="35cba-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="35cba-211">In hello **categoria** riquadro andare troppo**connessione** > **SSH** > **Auth**. In hello **file di chiave privata per l'autenticazione** passare toohello chiave generata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="35cba-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Schermata delle opzioni di autenticazione SSH hello](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="35cba-213">In hello **categoria** riquadro andare troppo**connessione** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="35cba-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="35cba-214">Seleziona hello **inoltro X11 Enable** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="35cba-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Schermata di hello SSH X11 opzioni di inoltro](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="35cba-216">In hello **categoria** riquadro andare troppo**sessione**.</span><span class="sxs-lookup"><span data-stu-id="35cba-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="35cba-217">Immettere la macchina virtuale ASM Oracle `<publicIPaddress>` nella hello host Nome finestra di dialogo, inserire un nuovo `Saved Session` nome e quindi fare clic su `Save`.</span><span class="sxs-lookup"><span data-stu-id="35cba-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="35cba-218">Dopo il salvataggio, fare clic su `open` macchina virtuale di Oracle ASM tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="35cba-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="35cba-219">Hello prima connessione è un avviso nel Registro di sistema non è stato memorizzato nella cache sistema remoto hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="35cba-220">Fare clic su `yes` tooadd e continuare.</span><span class="sxs-lookup"><span data-stu-id="35cba-220">Click on `yes` tooadd it and continue.</span></span>

   ![Schermata delle opzioni di sessione PuTTY hello](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="35cba-222">Installare Oracle Grid Infrastructure</span><span class="sxs-lookup"><span data-stu-id="35cba-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="35cba-223">tooinstall Oracle griglia infrastruttura, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="35cba-224">Accedere come utente **grid**.</span><span class="sxs-lookup"><span data-stu-id="35cba-224">Sign in as **grid**.</span></span> <span data-ttu-id="35cba-225">(Deve essere in grado di toosign in senza che venga richiesta una password.)</span><span class="sxs-lookup"><span data-stu-id="35cba-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="35cba-226">Se si esegue Windows, assicurarsi di che aver avviato Xming prima di iniziare l'installazione di hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="35cba-227">Verrà visualizzata la finestra Oracle Grid Infrastructure 12c Release 1 Installer (Programma di installazione di Oracle Grid Infrastructure 12c versione 1).</span><span class="sxs-lookup"><span data-stu-id="35cba-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="35cba-228">(Potrebbe richiedere alcuni minuti per hello installer toostart).</span><span class="sxs-lookup"><span data-stu-id="35cba-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="35cba-229">In hello **seleziona un'opzione di installazione** selezionare **installare e configurare Oracle griglia infrastruttura per un Server autonomo**.</span><span class="sxs-lookup"><span data-stu-id="35cba-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Schermata della pagina Selezionare opzione di installazione del programma di installazione di hello](./media/oracle-asm/install01.png)

3. <span data-ttu-id="35cba-231">In hello **selezionare lingue prodotto** assicurarsi **inglese** o lingua hello desiderata è selezionata.</span><span class="sxs-lookup"><span data-stu-id="35cba-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="35cba-232">Fare clic su `next`.</span><span class="sxs-lookup"><span data-stu-id="35cba-232">Click `next`.</span></span>

4. <span data-ttu-id="35cba-233">In hello **Crea gruppo di dischi ASM** pagina:</span><span class="sxs-lookup"><span data-stu-id="35cba-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="35cba-234">Immettere un nome per il gruppo di dischi hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="35cba-235">In **Redundancy** (Ridondanza) selezionare **External** (Esterna).</span><span class="sxs-lookup"><span data-stu-id="35cba-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="35cba-236">In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.</span><span class="sxs-lookup"><span data-stu-id="35cba-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35cba-237">In **Add Disks** (Aggiungi dischi) selezionare **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="35cba-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="35cba-238">Fare clic su `next`.</span><span class="sxs-lookup"><span data-stu-id="35cba-238">Click `next`.</span></span>

5. <span data-ttu-id="35cba-239">In hello **specificare Password ASM** pagina, seleziona hello **utilizzare stessa password per questi account** opzione e immettere una password.</span><span class="sxs-lookup"><span data-stu-id="35cba-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Schermata della pagina specificare Password ASM del programma di installazione di hello](./media/oracle-asm/install04.png)

6. <span data-ttu-id="35cba-241">In hello **specificare opzioni di gestione** pagina, si dispone di hello opzione tooconfigure controllo Cloud EM.</span><span class="sxs-lookup"><span data-stu-id="35cba-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="35cba-242">Questa opzione verrà ignorato: fare clic su `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35cba-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="35cba-243">In hello **gruppi con privilegi di sistema operativo** pagina, utilizzare le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="35cba-244">Fare clic su `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35cba-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="35cba-245">In hello **percorso di installazione specificare** pagina, utilizzare le impostazioni predefinite di hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="35cba-246">Fare clic su `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35cba-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="35cba-247">In hello **crea** pagina, modificare hello inventario Directory troppo`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="35cba-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="35cba-248">Fare clic su `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35cba-248">Click `next` toocontinue.</span></span>

   ![Schermata della pagina di creare l'inventario del programma di installazione di hello](./media/oracle-asm/install08.png)

10. <span data-ttu-id="35cba-250">In hello **configurazione di esecuzione di script radice** pagina, seleziona hello **automaticamente di eseguire gli script di configurazione** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="35cba-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="35cba-251">Selezionare quindi hello **vengono usate le credenziali utente "root"** opzione e immettere una password dell'utente root hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Schermata radice script esecuzione del programma di installazione di hello pagina di configurazione](./media/oracle-asm/install09.png)

11. <span data-ttu-id="35cba-253">In hello **eseguire controlli dei prerequisiti** pagina installazione corrente di hello avrà esito negativo con errori.</span><span class="sxs-lookup"><span data-stu-id="35cba-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="35cba-254">Si tratta di un comportamento previsto.</span><span class="sxs-lookup"><span data-stu-id="35cba-254">This is an expected behavior.</span></span> <span data-ttu-id="35cba-255">Selezionare `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="35cba-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="35cba-256">In hello **Script correzione** la finestra di dialogo, fare clic su `OK`.</span><span class="sxs-lookup"><span data-stu-id="35cba-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="35cba-257">In hello **riepilogo** pagina, rivedere le impostazioni selezionate e quindi fare clic su `Install`.</span><span class="sxs-lookup"><span data-stu-id="35cba-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Schermata della pagina di riepilogo dell'installazione guidata di hello](./media/oracle-asm/install12.png)

14. <span data-ttu-id="35cba-259">Una finestra di dialogo di avviso viene visualizzato per informare gli script di configurazione di è necessario toobe eseguito come utente con privilegi.</span><span class="sxs-lookup"><span data-stu-id="35cba-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="35cba-260">Fare clic su `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="35cba-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="35cba-261">In hello **fine** pagina, fare clic su `Close` installazione hello toofinish.</span><span class="sxs-lookup"><span data-stu-id="35cba-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="35cba-262">Configurare l'installazione di Oracle ASM</span><span class="sxs-lookup"><span data-stu-id="35cba-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="35cba-263">tooset installazione Oracle ASM, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="35cba-264">Verificare che si è ancora connessi come **grid** dalla sessione X11.</span><span class="sxs-lookup"><span data-stu-id="35cba-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="35cba-265">Potrebbe essere necessario toohit `enter` toorevive hello terminal.</span><span class="sxs-lookup"><span data-stu-id="35cba-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="35cba-266">Avviare quindi hello Oracle automatizzata Storage Management Configuration Assistant:</span><span class="sxs-lookup"><span data-stu-id="35cba-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="35cba-267">Verrà visualizzato ASM Configuration Assistant (Assistente alla configurazione di ASM).</span><span class="sxs-lookup"><span data-stu-id="35cba-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="35cba-268">In hello **configurare ASM: gruppi di dischi** finestra di dialogo fare clic su hello `Create` pulsante e quindi fare clic su `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="35cba-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="35cba-269">In hello **Crea gruppo di dischi** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="35cba-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="35cba-270">Immettere il nome del gruppo disco hello **dati**.</span><span class="sxs-lookup"><span data-stu-id="35cba-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="35cba-271">In **Select Member Disks** (Selezionare i dischi membri) selezionare **ORCL_DATA** e **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="35cba-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="35cba-272">In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.</span><span class="sxs-lookup"><span data-stu-id="35cba-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35cba-273">Fare clic su `ok` toocreate il gruppo di dischi hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="35cba-274">Fare clic su `ok` tooclose finestra di conferma hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Schermata della finestra di dialogo Crea gruppo di dischi hello](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="35cba-276">In hello **configurare ASM: gruppi di dischi** finestra di dialogo fare clic su hello `Create` pulsante e quindi fare clic su `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="35cba-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="35cba-277">In hello **Crea gruppo di dischi** la finestra di dialogo:</span><span class="sxs-lookup"><span data-stu-id="35cba-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="35cba-278">Immettere il nome del gruppo disco hello **francese**.</span><span class="sxs-lookup"><span data-stu-id="35cba-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="35cba-279">In **Redundancy** (Ridondanza) selezionare **External (none)** (Esterna (nessuna)).</span><span class="sxs-lookup"><span data-stu-id="35cba-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="35cba-280">In **Select Member Disks** (Selezionare i dischi membri) selezionare **ORCL_DATA**.</span><span class="sxs-lookup"><span data-stu-id="35cba-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="35cba-281">In **Allocation Unit Size** (Dimensioni dell'unità di allocazione) selezionare **4**.</span><span class="sxs-lookup"><span data-stu-id="35cba-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="35cba-282">Fare clic su `ok` toocreate il gruppo di dischi hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="35cba-283">Fare clic su `ok` tooclose finestra di conferma hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Schermata della finestra di dialogo Crea gruppo di dischi hello](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="35cba-285">Selezionare **uscita** tooclose ASM Configuration Assistant.</span><span class="sxs-lookup"><span data-stu-id="35cba-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Schermata di hello configurare ASM: la finestra di dialogo di gruppi di dischi con il pulsante di uscita](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="35cba-287">Creare database hello</span><span class="sxs-lookup"><span data-stu-id="35cba-287">Create hello database</span></span>

<span data-ttu-id="35cba-288">Hello software per database Oracle è già installato nell'immagine di Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="35cba-289">toocreate un database, hello completo alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="35cba-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="35cba-290">Passare come superuser Oracle toohello di utenti e quindi inizializzare listener di hello per la registrazione:</span><span class="sxs-lookup"><span data-stu-id="35cba-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="35cba-291">Si apre Configuration Assistant (Assistente alla configurazione).</span><span class="sxs-lookup"><span data-stu-id="35cba-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="35cba-292">In hello **operazione sul Database** pagina, fare clic su `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="35cba-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="35cba-293">In hello **la modalità di creazione** pagina:</span><span class="sxs-lookup"><span data-stu-id="35cba-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="35cba-294">Immettere un nome per il database di hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="35cba-295">Per **Storage Type** (tipo di archiviazione) assicurarsi che **Automatic Storage Management (ASM)** (Gestione archiviazione automatica, ASM) sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="35cba-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="35cba-296">Per **percorso file di Database**, utilizzare hello predefinito ASM suggerito percorso.</span><span class="sxs-lookup"><span data-stu-id="35cba-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="35cba-297">Per **rapida Area ripristino**, utilizzare hello predefinito ASM suggerito percorso.</span><span class="sxs-lookup"><span data-stu-id="35cba-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="35cba-298">Digitare una **Password amministratore** e **confermare la password**.</span><span class="sxs-lookup"><span data-stu-id="35cba-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="35cba-299">Verificare che `create as container database` sia selezionato.</span><span class="sxs-lookup"><span data-stu-id="35cba-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="35cba-300">Digitare un valore `pluggable database name`.</span><span class="sxs-lookup"><span data-stu-id="35cba-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="35cba-301">In hello **riepilogo** pagina, rivedere le impostazioni selezionate e quindi fare clic su `Finish` database hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="35cba-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Schermata della pagina di riepilogo hello](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="35cba-303">Hello Database è stato creato.</span><span class="sxs-lookup"><span data-stu-id="35cba-303">hello Database has been created.</span></span> <span data-ttu-id="35cba-304">In hello **fine** sono disponibili hello opzione toounlock altri account toouse questo database e modificare le password hello.</span><span class="sxs-lookup"><span data-stu-id="35cba-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="35cba-305">Se si desidera toodo scopo, selezionare **la gestione delle Password** -in caso contrario, fare clic su `close`.</span><span class="sxs-lookup"><span data-stu-id="35cba-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="35cba-306">Eliminare hello VM</span><span class="sxs-lookup"><span data-stu-id="35cba-306">Delete hello VM</span></span>

<span data-ttu-id="35cba-307">È stata configurata correttamente Gestione archiviazione automatica Oracle sull'immagine di Oracle DB hello da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="35cba-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="35cba-308">Quando non è più necessario questa macchina virtuale, è possibile utilizzare hello seguente gruppo di risorse di comando tooremove hello, macchina virtuale e tutte le relative risorse:</span><span class="sxs-lookup"><span data-stu-id="35cba-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="35cba-309">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="35cba-309">Next steps</span></span>

[<span data-ttu-id="35cba-310">Esercitazione: Configurare Oracle DataGuard</span><span class="sxs-lookup"><span data-stu-id="35cba-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="35cba-311">Esercitazione: Configurare Oracle GoldenGate</span><span class="sxs-lookup"><span data-stu-id="35cba-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="35cba-312">Revisione: [Definire l'architettura di un database Oracle](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="35cba-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
