---
title: aaaRun un MariaDB (MySQL) del cluster in Azure | Documenti Microsoft
description: Creare un cluster MariaDB + Galera MySQL in macchine virtuali di Azure
services: virtual-machines-linux
documentationcenter: 
author: sabbour
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d0d21937-7aac-4222-8255-2fdc4f2ea65b
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/15/2015
ms.author: asabbour
ms.openlocfilehash: f9a4d6c45d76478a8a3526b407c7bbe6aeb40423
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="mariadb-mysql-cluster-azure-tutorial"></a><span data-ttu-id="99a54-103">Cluster MariaDB (MySQL) - Esercitazione su Azure</span><span class="sxs-lookup"><span data-stu-id="99a54-103">MariaDB (MySQL) cluster: Azure tutorial</span></span>
> [!IMPORTANT]
> <span data-ttu-id="99a54-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="99a54-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="99a54-105">Questo articolo descrive il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-105">This article covers hello classic deployment model.</span></span> <span data-ttu-id="99a54-106">Si consiglia di utilizzano il modello di gestione risorse di Azure hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="99a54-106">Microsoft recommends that most new deployments use hello Azure Resource Manager model.</span></span>

> [!NOTE]
> <span data-ttu-id="99a54-107">Cluster MariaDB Enterprise è ora disponibile in hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="99a54-107">MariaDB Enterprise cluster is now available in hello Azure Marketplace.</span></span> <span data-ttu-id="99a54-108">nuova offerta di Hello distribuirà automaticamente un cluster di MariaDB Galera in Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="99a54-108">hello new offering will automatically deploy a MariaDB Galera cluster on Azure Resource Manager.</span></span> <span data-ttu-id="99a54-109">È consigliabile utilizzare una nuova offerta di hello da [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span><span class="sxs-lookup"><span data-stu-id="99a54-109">You should use hello new offering from [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/partners/mariadb/cluster-maxscale/).</span></span>
>
>

<span data-ttu-id="99a54-110">In questo articolo illustra come un multimaster toocreate [Galera](http://galeracluster.com/products/) cluster di [MariaDBs](https://mariadb.org/en/about/) (una sostituzione più solida, scalabile e affidabile per MySQL) toowork in un ambiente a disponibilità elevata in Azure macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="99a54-110">This article shows you how toocreate a multi-Master [Galera](http://galeracluster.com/products/) cluster of [MariaDBs](https://mariadb.org/en/about/) (a robust, scalable, and reliable drop-in replacement for MySQL) toowork in a highly available environment on Azure virtual machines.</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="99a54-111">Panoramica dell'architettura</span><span class="sxs-lookup"><span data-stu-id="99a54-111">Architecture overview</span></span>
<span data-ttu-id="99a54-112">Questo articolo viene descritto come hello toocomplete seguenti passaggi:</span><span class="sxs-lookup"><span data-stu-id="99a54-112">This article describes how toocomplete hello following steps:</span></span>

- <span data-ttu-id="99a54-113">Creare un cluster a tre nodi.</span><span class="sxs-lookup"><span data-stu-id="99a54-113">Create a three-node cluster.</span></span>
- <span data-ttu-id="99a54-114">Dischi dati hello separato dal disco del sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-114">Separate hello data disks from hello OS disk.</span></span>
- <span data-ttu-id="99a54-115">Creare dischi dati hello in tooincrease RAID 0/striping impostazione IOPS.</span><span class="sxs-lookup"><span data-stu-id="99a54-115">Create hello data disks in RAID-0/striped setting tooincrease IOPS.</span></span>
- <span data-ttu-id="99a54-116">Utilizzare carico hello toobalance di bilanciamento del carico di Azure per i nodi di hello tre.</span><span class="sxs-lookup"><span data-stu-id="99a54-116">Use Azure Load Balancer toobalance hello load for hello three nodes.</span></span>
- <span data-ttu-id="99a54-117">toominimize ricorrenti di lavoro, creare un'immagine di macchina virtuale che contiene MariaDB + Galera e utilizzarlo toocreate hello altre macchine virtuali del cluster.</span><span class="sxs-lookup"><span data-stu-id="99a54-117">toominimize repetitive work, create a VM image that contains MariaDB + Galera and use it toocreate hello other cluster VMs.</span></span>

![Architettura di sistema](./media/mariadb-mysql-cluster/Setup.png)

> [!NOTE]
> <span data-ttu-id="99a54-119">In questo argomento utilizza hello [CLI di Azure](../../../cli-install-nodejs.md) strumenti, quindi è opportuno assicurarsi che toodownload li e connettere le istruzioni in base toohello di tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="99a54-119">This topic uses hello [Azure CLI](../../../cli-install-nodejs.md) tools, so make sure toodownload them and connect them tooyour Azure subscription according toohello instructions.</span></span> <span data-ttu-id="99a54-120">Se è necessario un comandi toohello di riferimento disponibili in hello CLI di Azure, vedere hello [riferimento sui comandi CLI di Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="99a54-120">If you need a reference toohello commands available in hello Azure CLI, see hello [Azure CLI command reference](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span> <span data-ttu-id="99a54-121">È inoltre necessario troppo[creare una chiave SSH per l'autenticazione] e prendere nota del percorso del file con estensione PEM hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-121">You will also need too[create an SSH key for authentication] and make note of hello .pem file location.</span></span>
>
>

## <a name="create-hello-template"></a><span data-ttu-id="99a54-122">Creare il modello di hello</span><span class="sxs-lookup"><span data-stu-id="99a54-122">Create hello template</span></span>
### <a name="infrastructure"></a><span data-ttu-id="99a54-123">Infrastruttura</span><span class="sxs-lookup"><span data-stu-id="99a54-123">Infrastructure</span></span>
1. <span data-ttu-id="99a54-124">Creare un gruppo di affinità di toohold hello risorse insieme.</span><span class="sxs-lookup"><span data-stu-id="99a54-124">Create an affinity group toohold hello resources together.</span></span>

        azure account affinity-group create mariadbcluster --location "North Europe" --label "MariaDB Cluster"
2. <span data-ttu-id="99a54-125">Creare una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="99a54-125">Create a virtual network.</span></span>

        azure network vnet create --address-space 10.0.0.0 --cidr 8 --subnet-name mariadb --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --affinity-group mariadbcluster mariadbvnet
3. <span data-ttu-id="99a54-126">Creare un toohost di account di archiviazione di tutti i dischi.</span><span class="sxs-lookup"><span data-stu-id="99a54-126">Create a storage account toohost all our disks.</span></span> <span data-ttu-id="99a54-127">Non inserire più di 40 dischi utilizzati molto frequentemente su hello stesso tooavoid di account di archiviazione raggiunge limite dell'account di archiviazione IOPS hello 20.000.</span><span class="sxs-lookup"><span data-stu-id="99a54-127">You shouldn't place more than 40 heavily used disks on hello same storage account tooavoid hitting hello 20,000 IOPS storage account limit.</span></span> <span data-ttu-id="99a54-128">In questo caso, è molto di sotto di tale limite, in modo che conterrà tutti gli elementi in hello stesso account per semplicità.</span><span class="sxs-lookup"><span data-stu-id="99a54-128">In this case, you're well below that limit, so you'll store everything on hello same account for simplicity.</span></span>

        azure storage account create mariadbstorage --label mariadbstorage --affinity-group mariadbcluster
4. <span data-ttu-id="99a54-129">Trovare il nome di hello dell'immagine di macchina virtuale CentOS 7 hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-129">Find hello name of hello CentOS 7 virtual machine image.</span></span>

        azure vm image list | findstr CentOS
   <span data-ttu-id="99a54-130">output di Hello sarà simile al seguente `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span><span class="sxs-lookup"><span data-stu-id="99a54-130">hello output will be something like `5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926`.</span></span>

   <span data-ttu-id="99a54-131">Utilizzare il nome nel hello riportata dopo il passaggio.</span><span class="sxs-lookup"><span data-stu-id="99a54-131">Use that name in hello following step.</span></span>
5. <span data-ttu-id="99a54-132">Creare il modello di macchina virtuale hello e sostituire /path/to/key.pem con percorso hello in cui è archiviata la chiave SSH PEM hello generato.</span><span class="sxs-lookup"><span data-stu-id="99a54-132">Create hello VM template and replace /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

        azure vm create --virtual-network-name mariadbvnet --subnet-names mariadb --blob-url "http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-os.vhd"  --vm-size Medium --ssh 22 --ssh-cert "/path/to/key.pem" --no-ssh-password mariadbtemplate 5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-70-20140926 azureuser
6. <span data-ttu-id="99a54-133">Collegare i quattro 500 GB di dati dischi toohello macchina virtuale per l'utilizzo in una configurazione RAID hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-133">Attach four 500-GB data disks toohello VM for use in hello RAID configuration.</span></span>

        FOR /L %d IN (1,1,4) DO azure vm disk attach-new mariadbhatemplate 512 http://mariadbstorage.blob.core.windows.net/vhds/mariadbhatemplate-data-%d.vhd
7. <span data-ttu-id="99a54-134">Usare SSH toosign toohello modello macchina virtuale creata in mariadbhatemplate.cloudapp.net:22 e connettersi usando la chiave privata.</span><span class="sxs-lookup"><span data-stu-id="99a54-134">Use SSH toosign in toohello template VM that you created at mariadbhatemplate.cloudapp.net:22, and connect by using your private key.</span></span>

### <a name="software"></a><span data-ttu-id="99a54-135">Software</span><span class="sxs-lookup"><span data-stu-id="99a54-135">Software</span></span>
1. <span data-ttu-id="99a54-136">Ottenere la radice hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-136">Get hello root.</span></span>

        sudo su

2. <span data-ttu-id="99a54-137">Installare il supporto RAID:</span><span class="sxs-lookup"><span data-stu-id="99a54-137">Install RAID support:</span></span>

    <span data-ttu-id="99a54-138">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-138">a.</span></span> <span data-ttu-id="99a54-139">Installare mdadm.</span><span class="sxs-lookup"><span data-stu-id="99a54-139">Install mdadm.</span></span>

              yum install mdadm

    <span data-ttu-id="99a54-140">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-140">b.</span></span> <span data-ttu-id="99a54-141">Creare una configurazione RAID0/stripe hello con un file system EXT4.</span><span class="sxs-lookup"><span data-stu-id="99a54-141">Create hello RAID0/stripe configuration with an EXT4 file system.</span></span>

              mdadm --create --verbose /dev/md0 --level=stripe --raid-devices=4 /dev/sdc /dev/sdd /dev/sde /dev/sdf
              mdadm --detail --scan >> /etc/mdadm.conf
              mkfs -t ext4 /dev/md0
    <span data-ttu-id="99a54-142">c.</span><span class="sxs-lookup"><span data-stu-id="99a54-142">c.</span></span> <span data-ttu-id="99a54-143">Creare una directory del punto di montaggio hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-143">Create hello mount point directory.</span></span>

              mkdir /mnt/data
    <span data-ttu-id="99a54-144">d.</span><span class="sxs-lookup"><span data-stu-id="99a54-144">d.</span></span> <span data-ttu-id="99a54-145">Recuperare hello UUID del dispositivo RAID hello appena creato.</span><span class="sxs-lookup"><span data-stu-id="99a54-145">Retrieve hello UUID of hello newly created RAID device.</span></span>

              blkid | grep /dev/md0
    <span data-ttu-id="99a54-146">e.</span><span class="sxs-lookup"><span data-stu-id="99a54-146">e.</span></span> <span data-ttu-id="99a54-147">Modificare /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="99a54-147">Edit /etc/fstab.</span></span>

              vi /etc/fstab
    <span data-ttu-id="99a54-148">f.</span><span class="sxs-lookup"><span data-stu-id="99a54-148">f.</span></span> <span data-ttu-id="99a54-149">Aggiunta automatica di tooenable dispositivo hello montaggio riavvio, sostituendo hello UUID con valore hello ottenuto dal precedente hello **ID blocco** comando.</span><span class="sxs-lookup"><span data-stu-id="99a54-149">Add hello device tooenable auto mounting on reboot, replacing hello UUID with hello value obtained from hello previous **blkid** command.</span></span>

              UUID=<UUID FROM PREVIOUS>   /mnt/data ext4   defaults,noatime   1 2
    <span data-ttu-id="99a54-150">g.</span><span class="sxs-lookup"><span data-stu-id="99a54-150">g.</span></span> <span data-ttu-id="99a54-151">Installare una nuova partizione hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-151">Mount hello new partition.</span></span>

              mount /mnt/data

3. <span data-ttu-id="99a54-152">Installare MariaDB.</span><span class="sxs-lookup"><span data-stu-id="99a54-152">Install MariaDB.</span></span>

    <span data-ttu-id="99a54-153">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-153">a.</span></span> <span data-ttu-id="99a54-154">Creare file MariaDB.repo hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-154">Create hello MariaDB.repo file.</span></span>

                vi /etc/yum.repos.d/MariaDB.repo

    <span data-ttu-id="99a54-155">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-155">b.</span></span> <span data-ttu-id="99a54-156">Riempire i file di repository hello con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="99a54-156">Fill hello repo file with hello following content:</span></span>

              [mariadb]
              name = MariaDB
              baseurl = http://yum.mariadb.org/10.0/centos7-amd64
              gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
              gpgcheck=1
    <span data-ttu-id="99a54-157">c.</span><span class="sxs-lookup"><span data-stu-id="99a54-157">c.</span></span> <span data-ttu-id="99a54-158">tooavoid conflitti, rimuovere il suffisso esistente e mariadb librerie.</span><span class="sxs-lookup"><span data-stu-id="99a54-158">tooavoid conflicts, remove existing postfix and mariadb-libs.</span></span>

           yum remove postfix mariadb-libs-*
    <span data-ttu-id="99a54-159">d.</span><span class="sxs-lookup"><span data-stu-id="99a54-159">d.</span></span> <span data-ttu-id="99a54-160">Installare MariaDB con Galera.</span><span class="sxs-lookup"><span data-stu-id="99a54-160">Install MariaDB with Galera.</span></span>

           yum install MariaDB-Galera-server MariaDB-client galera

4. <span data-ttu-id="99a54-161">Spostare hello MySQL directory toohello RAID blocco il dispositivo di dati.</span><span class="sxs-lookup"><span data-stu-id="99a54-161">Move hello MySQL data directory toohello RAID block device.</span></span>

    <span data-ttu-id="99a54-162">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-162">a.</span></span> <span data-ttu-id="99a54-163">Copiare directory MySQL corrente hello nella nuova posizione e rimuovere la directory di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="99a54-163">Copy hello current MySQL directory into its new location and remove hello old directory.</span></span>

           cp -avr /var/lib/mysql /mnt/data  
           rm -rf /var/lib/mysql
    <span data-ttu-id="99a54-164">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-164">b.</span></span> <span data-ttu-id="99a54-165">Impostare le autorizzazioni per una nuova directory hello di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="99a54-165">Set permissions for hello new directory accordingly.</span></span>

           chown -R mysql:mysql /mnt/data && chmod -R 755 /mnt/data/

    <span data-ttu-id="99a54-166">c.</span><span class="sxs-lookup"><span data-stu-id="99a54-166">c.</span></span> <span data-ttu-id="99a54-167">Creare un collegamento simbolico che punta hello precedente toohello nuovo percorso della directory in hello partizione RAID.</span><span class="sxs-lookup"><span data-stu-id="99a54-167">Create a symlink that points hello old directory toohello new location on hello RAID partition.</span></span>

           ln -s /mnt/data/mysql /var/lib/mysql

5. <span data-ttu-id="99a54-168">Poiché [SELinux interferisce con le operazioni del cluster di hello](http://galeracluster.com/documentation-webpages/configuration.html#selinux), è necessario toodisable per hello sessione corrente.</span><span class="sxs-lookup"><span data-stu-id="99a54-168">Because [SELinux interferes with hello cluster operations](http://galeracluster.com/documentation-webpages/configuration.html#selinux), it is necessary toodisable it for hello current session.</span></span> <span data-ttu-id="99a54-169">Modifica `/etc/selinux/config` toodisable per successivi riavvii.</span><span class="sxs-lookup"><span data-stu-id="99a54-169">Edit `/etc/selinux/config` toodisable it for subsequent restarts.</span></span>

            setenforce 0

            then editing `/etc/selinux/config` tooset `SELINUX=permissive`
6. <span data-ttu-id="99a54-170">Convalidare le esecuzioni di MySQL.</span><span class="sxs-lookup"><span data-stu-id="99a54-170">Validate MySQL runs.</span></span>

   <span data-ttu-id="99a54-171">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-171">a.</span></span> <span data-ttu-id="99a54-172">Avviare MySQL.</span><span class="sxs-lookup"><span data-stu-id="99a54-172">Start MySQL.</span></span>

           service mysql start
   <span data-ttu-id="99a54-173">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-173">b.</span></span> <span data-ttu-id="99a54-174">Proteggere l'installazione di MySQL hello, impostare la password radice hello, rimuovere account di accesso di utenti anonimi toodisable radice remota e rimuovere i database di prova hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-174">Secure hello MySQL installation, set hello root password, remove anonymous users toodisable remote root login, and remove hello test database.</span></span>

           mysql_secure_installation
   <span data-ttu-id="99a54-175">c.</span><span class="sxs-lookup"><span data-stu-id="99a54-175">c.</span></span> <span data-ttu-id="99a54-176">Creare un utente nel database di hello per le operazioni del cluster e, facoltativamente, per le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="99a54-176">Create a user on hello database for cluster operations, and optionally for your applications.</span></span>

           mysql -u root -p
           GRANT ALL PRIVILEGES ON *.* too'cluster'@'%' IDENTIFIED BY 'p@ssw0rd' WITH GRANT OPTION; FLUSH PRIVILEGES;
           exit

   <span data-ttu-id="99a54-177">d.</span><span class="sxs-lookup"><span data-stu-id="99a54-177">d.</span></span> <span data-ttu-id="99a54-178">Arrestare MySQL.</span><span class="sxs-lookup"><span data-stu-id="99a54-178">Stop MySQL.</span></span>

            service mysql stop
7. <span data-ttu-id="99a54-179">Creare un segnaposto di configurazione.</span><span class="sxs-lookup"><span data-stu-id="99a54-179">Create a configuration placeholder.</span></span>

   <span data-ttu-id="99a54-180">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-180">a.</span></span> <span data-ttu-id="99a54-181">Modificare hello MySQL configurazione toocreate un segnaposto per le impostazioni del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-181">Edit hello MySQL configuration toocreate a placeholder for hello cluster settings.</span></span> <span data-ttu-id="99a54-182">Non sostituire hello  **`<Variables>`**  o rimuovere il commento ora.</span><span class="sxs-lookup"><span data-stu-id="99a54-182">Do not replace hello **`<Variables>`** or uncomment now.</span></span> <span data-ttu-id="99a54-183">L'operazione va eseguita dopo la creazione di una macchina virtuale dal modello.</span><span class="sxs-lookup"><span data-stu-id="99a54-183">That will happen after you create a VM from this template.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="99a54-184">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-184">b.</span></span> <span data-ttu-id="99a54-185">Modifica hello  **[galera]**  sezione e deselezionarla.</span><span class="sxs-lookup"><span data-stu-id="99a54-185">Edit hello **[galera]** section and clear it out.</span></span>

   <span data-ttu-id="99a54-186">c.</span><span class="sxs-lookup"><span data-stu-id="99a54-186">c.</span></span> <span data-ttu-id="99a54-187">Modifica hello **[mariadb]** sezione.</span><span class="sxs-lookup"><span data-stu-id="99a54-187">Edit hello **[mariadb]** section.</span></span>

           wsrep_provider=/usr/lib64/galera/libgalera_smm.so
           binlog_format=ROW
           wsrep_sst_method=rsync
           bind-address=0.0.0.0 # When set too0.0.0.0, hello server listens tooremote connections
           default_storage_engine=InnoDB
           innodb_autoinc_lock_mode=2

           wsrep_sst_auth=cluster:p@ssw0rd # CHANGE: Username and password you created for hello SST cluster MySQL user
           #wsrep_cluster_name='mariadbcluster' # CHANGE: Uncomment and set your desired cluster name
           #wsrep_cluster_address="gcomm://mariadb1,mariadb2,mariadb3" # CHANGE: Uncomment and Add all your servers
           #wsrep_node_address='<ServerIP>' # CHANGE: Uncomment and set IP address of this server
           #wsrep_node_name='<NodeName>' # CHANGE: Uncomment and set hello node name of this server
8. <span data-ttu-id="99a54-188">Aprire le porte necessarie sul firewall hello utilizzando FirewallD in CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="99a54-188">Open required ports on hello firewall by using FirewallD on CentOS 7.</span></span>

   * <span data-ttu-id="99a54-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="99a54-189">MySQL: `firewall-cmd --zone=public --add-port=3306/tcp --permanent`</span></span>
   * <span data-ttu-id="99a54-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="99a54-190">GALERA: `firewall-cmd --zone=public --add-port=4567/tcp --permanent`</span></span>
   * <span data-ttu-id="99a54-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="99a54-191">GALERA IST: `firewall-cmd --zone=public --add-port=4568/tcp --permanent`</span></span>
   * <span data-ttu-id="99a54-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span><span class="sxs-lookup"><span data-stu-id="99a54-192">RSYNC: `firewall-cmd --zone=public --add-port=4444/tcp --permanent`</span></span>
   * <span data-ttu-id="99a54-193">Ricarica hello firewall:`firewall-cmd --reload`</span><span class="sxs-lookup"><span data-stu-id="99a54-193">Reload hello firewall: `firewall-cmd --reload`</span></span>

9. <span data-ttu-id="99a54-194">Ottimizzare il sistema hello per le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="99a54-194">Optimize hello system for performance.</span></span> <span data-ttu-id="99a54-195">Per altre informazioni, vedere la [strategia di ottimizzazione delle prestazioni](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="99a54-195">For more information, see [performance tuning strategy](optimize-mysql.md).</span></span>

   <span data-ttu-id="99a54-196">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-196">a.</span></span> <span data-ttu-id="99a54-197">Modificare di nuovo il file di configurazione di hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="99a54-197">Edit hello MySQL configuration file again.</span></span>

            vi /etc/my.cnf.d/server.cnf
   <span data-ttu-id="99a54-198">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-198">b.</span></span> <span data-ttu-id="99a54-199">Modifica hello **[mariadb]** sezione e accodare hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="99a54-199">Edit hello **[mariadb]** section and append hello following content:</span></span>

   > [!NOTE]
   > <span data-ttu-id="99a54-200">innodb\_buffer\_pool_size dovrebbe essere il 70% della memoria della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="99a54-200">We recommend that innodb\_buffer\_pool_size is 70 percent of your VM's memory.</span></span> <span data-ttu-id="99a54-201">In questo esempio è stata impostata 2,45 GB per Media hello macchina virtuale di Azure con 3,5 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="99a54-201">In this example, it has been set at 2.45 GB for hello medium Azure VM with 3.5 GB of RAM.</span></span>
   >
   >

           innodb_buffer_pool_size = 2508M # hello buffer pool contains buffered data and hello index. This is usually set too70 percent of physical memory.
           innodb_log_file_size = 512M #  Redo logs ensure that write operations are fast, reliable, and recoverable after a crash
           max_connections = 5000 # A larger value will give hello server more time toorecycle idled connections
           innodb_file_per_table = 1 # Speed up hello table space transmission and optimize hello debris management performance
           innodb_log_buffer_size = 128M # hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit
           innodb_flush_log_at_trx_commit = 2 # hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL cluster
           query_cache_size = 0
10. <span data-ttu-id="99a54-202">Arrestare MySQL, disabilitare il servizio MySQL esecuzione avvio tooavoid interrompere cluster hello quando si aggiunge un nodo e deprovisioning macchina hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-202">Stop MySQL, disable MySQL service from running on startup tooavoid disrupting hello cluster when adding a node, and deprovision hello machine.</span></span>

        service mysql stop
        chkconfig mysql off
        waagent -deprovision
11. <span data-ttu-id="99a54-203">Acquisire hello VM tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-203">Capture hello VM through hello portal.</span></span> <span data-ttu-id="99a54-204">(Attualmente [emettere &#1268; negli strumenti di Azure CLI hello](https://github.com/Azure/azure-xplat-cli/issues/1268) vengono descritti i fatti hello che le immagini acquisite dagli strumenti di Azure CLI hello si acquisiscono i dischi dati collegato hello.)</span><span class="sxs-lookup"><span data-stu-id="99a54-204">(Currently, [issue #1268 in hello Azure CLI tools](https://github.com/Azure/azure-xplat-cli/issues/1268) describes hello fact that images captured by hello Azure CLI tools do not capture hello attached data disks.)</span></span>

    <span data-ttu-id="99a54-205">a.</span><span class="sxs-lookup"><span data-stu-id="99a54-205">a.</span></span> <span data-ttu-id="99a54-206">Spegnere la macchina hello tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-206">Shut down hello machine through hello portal.</span></span>

    <span data-ttu-id="99a54-207">b.</span><span class="sxs-lookup"><span data-stu-id="99a54-207">b.</span></span> <span data-ttu-id="99a54-208">Fare clic su **acquisire** e specificare il nome immagine hello come **mariadb-galera-immagine**.</span><span class="sxs-lookup"><span data-stu-id="99a54-208">Click **Capture** and specify hello image name as **mariadb-galera-image**.</span></span> <span data-ttu-id="99a54-209">Fornire una descrizione e selezionare "Il comando waagent è stato eseguito."</span><span class="sxs-lookup"><span data-stu-id="99a54-209">Provide a description and check "I have run waagent."</span></span>
      
      ![Acquisire una macchina virtuale hello](./media/mariadb-mysql-cluster/Capture2.PNG)

## <a name="create-hello-cluster"></a><span data-ttu-id="99a54-211">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="99a54-211">Create hello cluster</span></span>
<span data-ttu-id="99a54-212">Creare tre macchine virtuali con il modello di hello creato, quindi configurare e avviare hello cluster.</span><span class="sxs-lookup"><span data-stu-id="99a54-212">Create three VMs with hello template you created, and then configure and start hello cluster.</span></span>

1. <span data-ttu-id="99a54-213">Creare hello prima CentOS 7 VM da hello mariadb-galera-immagine immagine è creata, fornendo hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="99a54-213">Create hello first CentOS 7 VM from hello mariadb-galera-image image you created, providing hello following information:</span></span>

 - <span data-ttu-id="99a54-214">Nome rete virtuale: mariadbvnet</span><span class="sxs-lookup"><span data-stu-id="99a54-214">Virtual network name: mariadbvnet</span></span>
 - <span data-ttu-id="99a54-215">Subnet: mariadb</span><span class="sxs-lookup"><span data-stu-id="99a54-215">Subnet: mariadb</span></span>
 - <span data-ttu-id="99a54-216">Dimensioni della macchina: medie</span><span class="sxs-lookup"><span data-stu-id="99a54-216">Machine size: medium</span></span>
 - <span data-ttu-id="99a54-217">Nome del servizio cloud: mariadbha (o qualsiasi nome con cui si desidera accedere tramite mariadbha.cloudapp.net toobe)</span><span class="sxs-lookup"><span data-stu-id="99a54-217">Cloud service name: mariadbha (or whatever name you want toobe accessed through mariadbha.cloudapp.net)</span></span>
 - <span data-ttu-id="99a54-218">Nome del computer: mariadb1</span><span class="sxs-lookup"><span data-stu-id="99a54-218">Machine name: mariadb1</span></span>
 - <span data-ttu-id="99a54-219">Nome utente: azureuser</span><span class="sxs-lookup"><span data-stu-id="99a54-219">Username: azureuser</span></span>
 - <span data-ttu-id="99a54-220">Accesso SSH: abilitato</span><span class="sxs-lookup"><span data-stu-id="99a54-220">SSH access: enabled</span></span>
 - <span data-ttu-id="99a54-221">Il passaggio di file con estensione PEM del certificato SSH hello e sostituendo /path/to/key.pem con percorso hello in cui è archiviata la chiave SSH PEM hello generato.</span><span class="sxs-lookup"><span data-stu-id="99a54-221">Passing hello SSH certificate .pem file and replacing /path/to/key.pem with hello path where you stored hello generated .pem SSH key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="99a54-222">Hello comandi riportati di seguito sono suddivisi in più righe per maggiore chiarezza, ma è necessario immettere ogni una sola riga.</span><span class="sxs-lookup"><span data-stu-id="99a54-222">hello following commands are split over multiple lines for clarity, but you should enter each as one line.</span></span>
   >
   >
        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 22
        --vm-name mariadb1
        mariadbha mariadb-galera-image azureuser
2. <span data-ttu-id="99a54-223">Creare due altre macchine virtuali mediante la connessione del servizio cloud di toohello mariadbha.</span><span class="sxs-lookup"><span data-stu-id="99a54-223">Create two more virtual machines by connecting them toohello mariadbha cloud service.</span></span> <span data-ttu-id="99a54-224">Nome della macchina virtuale modifica hello e hello porta tooa univoca porta SSH non è in conflitto con altre macchine virtuali in hello nello stesso servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="99a54-224">Change hello VM name and hello SSH port tooa unique port not conflicting with other VMs in hello same cloud service.</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 23
        --vm-name mariadb2
        --connect mariadbha mariadb-galera-image azureuser
  <span data-ttu-id="99a54-225">Per MariaDB3:</span><span class="sxs-lookup"><span data-stu-id="99a54-225">For MariaDB3:</span></span>

        azure vm create
        --virtual-network-name mariadbvnet
        --subnet-names mariadb
        --availability-set clusteravset
        --vm-size Medium
        --ssh-cert "/path/to/key.pem"
        --no-ssh-password
        --ssh 24
        --vm-name mariadb3
        --connect mariadbha mariadb-galera-image azureuser
3. <span data-ttu-id="99a54-226">È necessario per il passaggio successivo hello tooget hello indirizzo IP interno di ognuna delle macchine virtuali hello tre:</span><span class="sxs-lookup"><span data-stu-id="99a54-226">You will need tooget hello internal IP address of each of hello three VMs for hello next step:</span></span>

    ![Recupero dell'indirizzo IP virtuale](./media/mariadb-mysql-cluster/IP.png)
4. <span data-ttu-id="99a54-228">Nelle macchine virtuali toohello tre toosign SSH e modificare il file di configurazione hello in ognuna di esse.</span><span class="sxs-lookup"><span data-stu-id="99a54-228">Use SSH toosign in toohello three VMs and edit hello configuration file on each of them.</span></span>

        sudo vi /etc/my.cnf.d/server.cnf

    <span data-ttu-id="99a54-229">Rimuovere il commento  **`wsrep_cluster_name`**  e  **`wsrep_cluster_address`**  rimuovendo hello  **#**  all'inizio di hello della riga hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-229">Uncomment **`wsrep_cluster_name`** and **`wsrep_cluster_address`** by removing hello **#** at hello beginning of hello line.</span></span>
    <span data-ttu-id="99a54-230">Inoltre, sostituire  **`<ServerIP>`**  in  **`wsrep_node_address`**  e  **`<NodeName>`**  in  **`wsrep_node_name`**  con hello IP della VM indirizzo e il nome, rispettivamente, e rimuovere il commento le righe di codice.</span><span class="sxs-lookup"><span data-stu-id="99a54-230">Additionally, replace **`<ServerIP>`** in **`wsrep_node_address`** and **`<NodeName>`** in **`wsrep_node_name`** with hello VM's IP address and name, respectively, and uncomment those lines as well.</span></span>
5. <span data-ttu-id="99a54-231">Avviare il cluster hello su MariaDB1 e consentire l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="99a54-231">Start hello cluster on MariaDB1 and let it run at startup.</span></span>

        sudo service mysql bootstrap
        chkconfig mysql on
6. <span data-ttu-id="99a54-232">Avviare MySQL in MariaDB2 e MariaDB3 e lasciare che venga eseguito all'avvio.</span><span class="sxs-lookup"><span data-stu-id="99a54-232">Start MySQL on MariaDB2 and MariaDB3 and let it run at startup.</span></span>

        sudo service mysql start
        chkconfig mysql on

## <a name="load-balance-hello-cluster"></a><span data-ttu-id="99a54-233">Cluster di bilanciamento carico di hello</span><span class="sxs-lookup"><span data-stu-id="99a54-233">Load balance hello cluster</span></span>
<span data-ttu-id="99a54-234">Durante la creazione di macchine virtuali hello in cluster, sono stati aggiunti in un set di disponibilità denominato clusteravset tooensure e che sono stati inseriti in diversi domini di errore e di aggiornamento e che Azure mai non manutenzione in tutti i computer in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="99a54-234">When you created hello clustered VMs, you added them into an availability set called clusteravset tooensure that they were put on different fault and update domains and that Azure never does maintenance on all machines at once.</span></span> <span data-ttu-id="99a54-235">Questa configurazione soddisfa i requisiti di hello toobe supportati dal contratto di servizio di Azure (SLA) hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-235">This configuration meets hello requirements toobe supported by hello Azure service level agreement (SLA).</span></span>

<span data-ttu-id="99a54-236">Utilizzare le richieste di bilanciamento del carico di Azure toobalance tra tre nodi hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-236">Now use Azure Load Balancer toobalance requests between hello three nodes.</span></span>

<span data-ttu-id="99a54-237">Eseguire hello seguenti comandi nel computer in uso tramite hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="99a54-237">Run hello following commands on your machine by using hello Azure CLI.</span></span>

<span data-ttu-id="99a54-238">struttura di parametri di comando Hello è:`azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span><span class="sxs-lookup"><span data-stu-id="99a54-238">hello command parameters structure is: `azure vm endpoint create-multiple <MachineName> <PublicPort>:<VMPort>:<Protocol>:<EnableDirectServerReturn>:<Load Balanced Set Name>:<ProbeProtocol>:<ProbePort>`</span></span>

    azure vm endpoint create-multiple mariadb1 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb2 3306:3306:tcp:false:MySQL:tcp:3306
    azure vm endpoint create-multiple mariadb3 3306:3306:tcp:false:MySQL:tcp:3306

<span data-ttu-id="99a54-239">Hello CLI imposta hello carico bilanciamento probe intervallo too15 (secondi), che potrebbero essere un po' troppo lunghi.</span><span class="sxs-lookup"><span data-stu-id="99a54-239">hello CLI sets hello load balancer probe interval too15 seconds, which might be a bit too long.</span></span> <span data-ttu-id="99a54-240">Modificare le impostazioni in portale hello in **endpoint** per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="99a54-240">Change it in hello portal under **Endpoints** for any of hello VMs.</span></span>

![Modificare l'endpoint](./media/mariadb-mysql-cluster/Endpoint.PNG)

<span data-ttu-id="99a54-242">Selezionare **hello Reconfigure Load-Balanced impostare**.</span><span class="sxs-lookup"><span data-stu-id="99a54-242">Select **Reconfigure hello Load-Balanced Set**.</span></span>

![Riconfigurare hello con bilanciamento del carico Set](./media/mariadb-mysql-cluster/Endpoint2.PNG)

<span data-ttu-id="99a54-244">Modifica **intervallo Probe** too5 secondi e salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="99a54-244">Change **Probe Interval** too5 seconds and save your changes.</span></span>

![Modificare l'intervallo di probe](./media/mariadb-mysql-cluster/Endpoint3.PNG)

## <a name="validate-hello-cluster"></a><span data-ttu-id="99a54-246">Convalida cluster hello</span><span class="sxs-lookup"><span data-stu-id="99a54-246">Validate hello cluster</span></span>
<span data-ttu-id="99a54-247">Hello rigido lavoro.</span><span class="sxs-lookup"><span data-stu-id="99a54-247">hello hard work is done.</span></span> <span data-ttu-id="99a54-248">cluster Hello dovrebbe ora essere accessibili nel `mariadbha.cloudapp.net:3306`, quale riscontri di bilanciamento del carico hello e indirizzare le richieste tra hello tre macchine virtuali lineare ed efficiente.</span><span class="sxs-lookup"><span data-stu-id="99a54-248">hello cluster should be now accessible at `mariadbha.cloudapp.net:3306`, which hits hello load balancer and route requests between hello three VMs smoothly and efficiently.</span></span>

<span data-ttu-id="99a54-249">Utilizzare i Preferiti tooconnect client MySQL, oppure da uno dei hello tooverify di macchine virtuali che il cluster sia in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="99a54-249">Use your favorite MySQL client tooconnect, or connect from one of hello VMs tooverify that this cluster is working.</span></span>

     mysql -u cluster -h mariadbha.cloudapp.net -p

<span data-ttu-id="99a54-250">Creare quindi un nuovo database e popolarlo con una serie di dati.</span><span class="sxs-lookup"><span data-stu-id="99a54-250">Then create a database and populate it with some data.</span></span>

    CREATE DATABASE TestDB;
    USE TestDB;
    CREATE TABLE TestTable (id INT NOT NULL AUTO_INCREMENT PRIMARY KEY, value VARCHAR(255));
    INSERT INTO TestTable (value)  VALUES ('Value1');
    INSERT INTO TestTable (value)  VALUES ('Value2');
    SELECT * FROM TestTable;

<span data-ttu-id="99a54-251">database Hello creato restituisce hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="99a54-251">hello database you created returns hello following table:</span></span>

    +----+--------+
    | id | value  |
    +----+--------+
    |  1 | Value1 |
    |  4 | Value2 |
    +----+--------+
    2 rows in set (0.00 sec)

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="99a54-252">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99a54-252">Next steps</span></span>
<span data-ttu-id="99a54-253">In questo articolo è stato creato un cluster a disponibilità elevata MariaDB + Galera a tre nodi in macchine virtuali di Azure con CentOS 7.</span><span class="sxs-lookup"><span data-stu-id="99a54-253">In this article, you created a three-node MariaDB + Galera highly available cluster on Azure virtual machines running CentOS 7.</span></span> <span data-ttu-id="99a54-254">macchine virtuali Hello sono con carico bilanciato con bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="99a54-254">hello VMs are load balanced with Azure Load Balancer.</span></span>

<span data-ttu-id="99a54-255">Potrebbe essere necessario toolook in [un altro modo toocluster MySQL in Linux](mysql-cluster.md) e modalità troppo[ottimizzare e testare le prestazioni di MySQL in macchine virtuali Linux di Azure](optimize-mysql.md).</span><span class="sxs-lookup"><span data-stu-id="99a54-255">You might want toolook at [another way toocluster MySQL on Linux](mysql-cluster.md) and ways too[optimize and test MySQL performance on Azure Linux VMs](optimize-mysql.md).</span></span>

<!--Anchors-->
[Architecture overview]:#architecture-overview
[Creating hello template]:#creating-the-template
[Creating hello cluster]:#creating-the-cluster
[Load balancing hello cluster]:#load-balancing-the-cluster
[Validating hello cluster]:#validating-the-cluster
[Next steps]:#next-steps

<!--Image references-->

<!--Link references-->
[Galera]:http://galeracluster.com/products/
[MariaDBs]:https://mariadb.org/en/about/
[creare una chiave SSH per l'autenticazione]:http://www.jeff.wilcox.name/2013/06/secure-linux-vms-with-ssh-certificates/
[issue #1268 in hello Azure CLI]:https://github.com/Azure/azure-xplat-cli/issues/1268
