---
title: aaaClusterize MySQL con set con carico bilanciato | Documenti Microsoft
description: "Impostare una bilanciamento del carico, la disponibilità elevata cluster Linux MySQL creato con il modello di distribuzione classica hello in Azure"
services: virtual-machines-linux
documentationcenter: 
author: bureado
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6c413a16-e9b5-4ffe-a8a3-ae67046bbdf3
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/14/2015
ms.author: jparrel
ms.openlocfilehash: 1829fd877c4b0ed177b23a8e3404dbb3db746561
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-load-balanced-sets-tooclusterize-mysql-on-linux"></a><span data-ttu-id="7aa2c-103">Utilizzare set con carico bilanciato tooclusterize MySQL in Linux</span><span class="sxs-lookup"><span data-stu-id="7aa2c-103">Use load-balanced sets tooclusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7aa2c-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="7aa2c-105">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-105">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="7aa2c-106">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="7aa2c-107">Oggetto [modello Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) è disponibile se è necessario toodeploy un cluster di MySQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need toodeploy a MySQL cluster.</span></span>

<span data-ttu-id="7aa2c-108">In questo articolo viene esaminata e illustra hello diversi approcci disponibili toodeploy servizi a disponibilità elevata basate su Linux in Microsoft Azure, l'esplorazione di MySQL Server a elevata disponibilità come nozioni di base.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-108">This article explores and illustrates hello different approaches available toodeploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="7aa2c-109">Su [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)è disponibile un video che illustra questo approccio.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="7aa2c-110">Sarà descritta una soluzione con disponibilità elevata MySQL a master singolo, con due nodi e nessuna condivisione, basata su DRBD, Corosync e Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="7aa2c-111">MySQL viene eseguito solo su un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="7aa2c-112">Lettura e scrittura da risorse DRBD hello è anche un nodo tooonly limitato alla volta.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-112">Reading and writing from hello DRBD resource is also limited tooonly one node at a time.</span></span>

<span data-ttu-id="7aa2c-113">Non è necessario per una soluzione VIP come LVS, poiché verrà utilizzato il set di bilanciamento del carico nella possibilità di recupero di hello VIP, il rilevamento di funzionalità e l'endpoint round-robin tooprovide e la rimozione di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure tooprovide round-robin functionality and endpoint detection, removal, and graceful recovery of hello VIP.</span></span> <span data-ttu-id="7aa2c-114">Hello VIP è un indirizzo IPv4 instradabile assegnato da Microsoft Azure al momento della creazione del servizio cloud hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-114">hello VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create hello cloud service.</span></span>

<span data-ttu-id="7aa2c-115">È possibile usare altre architetture per MySQL inclusi NBD Cluster, Percona, Galera e varie soluzioni middleware, di cui almeno una disponibile come VM su [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="7aa2c-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="7aa2c-116">Purché queste soluzioni possono essere replicati in unicast e multicast o broadcast e non fare affidamento sull'archiviazione condivisa o più interfacce di rete, gli scenari di hello devono essere facile toodeploy in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, hello scenarios should be easy toodeploy on Microsoft Azure.</span></span>

<span data-ttu-id="7aa2c-117">Queste architetture di clustering possono essere estesi tooother prodotti come PostgreSQL e OpenLDAP in modo simile.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-117">These clustering architectures can be extended tooother products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="7aa2c-118">Questa procedura di bilanciamento del carico senza condivisione è stata ad esempio testata con OpenLDAP multimaster ed è possibile vederne i risultati sul blog di Channel 9.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="7aa2c-119">Preparazione</span><span class="sxs-lookup"><span data-stu-id="7aa2c-119">Get ready</span></span>
<span data-ttu-id="7aa2c-120">È necessario hello segue le risorse e funzionalità:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-120">You need hello following resources and abilities:</span></span>

  - <span data-ttu-id="7aa2c-121">Account di un Microsoft Azure con una sottoscrizione valida, in grado di toocreate almeno due macchine virtuali (XS è stato utilizzato in questo esempio)</span><span class="sxs-lookup"><span data-stu-id="7aa2c-121">A Microsoft Azure account with a valid subscription, able toocreate at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="7aa2c-122">Una rete e una subnet</span><span class="sxs-lookup"><span data-stu-id="7aa2c-122">A network and a subnet</span></span>
  - <span data-ttu-id="7aa2c-123">Un gruppo di affinità</span><span class="sxs-lookup"><span data-stu-id="7aa2c-123">An affinity group</span></span>
  - <span data-ttu-id="7aa2c-124">Un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="7aa2c-124">An availability set</span></span>
  - <span data-ttu-id="7aa2c-125">Hello possibilità toocreate dischi rigidi virtuali nella stessa area del servizio cloud hello hello e allegarli le macchine virtuali Linux toohello</span><span class="sxs-lookup"><span data-stu-id="7aa2c-125">hello ability toocreate VHDs in hello same region as hello cloud service and attach them toohello Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="7aa2c-126">Ambiente testato</span><span class="sxs-lookup"><span data-stu-id="7aa2c-126">Tested environment</span></span>
* <span data-ttu-id="7aa2c-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="7aa2c-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="7aa2c-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="7aa2c-128">DRBD</span></span>
  * <span data-ttu-id="7aa2c-129">Server MySQL</span><span class="sxs-lookup"><span data-stu-id="7aa2c-129">MySQL Server</span></span>
  * <span data-ttu-id="7aa2c-130">Corosync e Pacemaker</span><span class="sxs-lookup"><span data-stu-id="7aa2c-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="7aa2c-131">Gruppo di affinità</span><span class="sxs-lookup"><span data-stu-id="7aa2c-131">Affinity group</span></span>
<span data-ttu-id="7aa2c-132">Creare un gruppo di affinità per la soluzione hello effettuando l'accesso al portale di Azure classico, toohello selezionando **impostazioni**e la creazione di un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-132">Create an affinity group for hello solution by signing in toohello Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="7aa2c-133">Le risorse allocate create in un secondo momento verranno assegnate il gruppo di affinità toothis.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-133">Allocated resources created later will be assigned toothis affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="7aa2c-134">Reti</span><span class="sxs-lookup"><span data-stu-id="7aa2c-134">Networks</span></span>
<span data-ttu-id="7aa2c-135">Viene creata una nuova rete e una subnet viene creata all'interno di rete hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-135">A new network is created, and a subnet is created inside hello network.</span></span> <span data-ttu-id="7aa2c-136">Questo esempio usa una rete 10.10.10.0/24 contenente una sola subnet /24.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="7aa2c-137">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="7aa2c-137">Virtual machines</span></span>
<span data-ttu-id="7aa2c-138">Hello prima Ubuntu 13.10 VM viene creato utilizzando un'immagine della raccolta Ubuntu Endorsed e viene chiamato `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-138">hello first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="7aa2c-139">Nel processo di hello, denominato hadb, viene creato un nuovo servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-139">A new cloud service is created in hello process, called hadb.</span></span> <span data-ttu-id="7aa2c-140">Questo nome viene condiviso, hello natura con bilanciamento del carico che servizio hello avrà quando vengono aggiunte più risorse.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-140">This name illustrates hello shared, load-balanced nature that hello service will have when more resources are added.</span></span> <span data-ttu-id="7aa2c-141">creazione di Hello `hadb01` è completata e se tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-141">hello creation of `hadb01` is uneventful and completed by using hello portal.</span></span> <span data-ttu-id="7aa2c-142">Viene creato automaticamente un endpoint per SSH e hello nuova rete sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-142">An endpoint for SSH is automatically created, and hello new network is selected.</span></span> <span data-ttu-id="7aa2c-143">È ora possibile creare un set di disponibilità per le macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-143">Now you can create an availability set for hello VMs.</span></span>

<span data-ttu-id="7aa2c-144">Dopo aver hello prima macchina virtuale viene creato (tecnicamente, quando viene creato il servizio di cloud hello), creare hello seconda macchina virtuale, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-144">After hello first VM is created (technically, when hello cloud service is created), create hello second VM, `hadb02`.</span></span> <span data-ttu-id="7aa2c-145">Per hello secondo VM, utilizzare Ubuntu 13.10 VM da hello raccolta tramite il portale di hello, ma utilizzare un servizio cloud esistente, `hadb.cloudapp.net`, anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-145">For hello second VM, use Ubuntu 13.10 VM from hello Gallery by using hello portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="7aa2c-146">Hello rete e set di disponibilità deve essere selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-146">hello network and availability set should be automatically selected.</span></span> <span data-ttu-id="7aa2c-147">Verrà anche creato un endpoint SSH.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="7aa2c-148">Dopo aver create entrambe le macchine virtuali, prendere nota della porta SSH hello per `hadb01` (TCP 22) e `hadb02` (assegnato automaticamente da Azure).</span><span class="sxs-lookup"><span data-stu-id="7aa2c-148">After both VMs have been created, take note of hello SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="7aa2c-149">Archivio collegato</span><span class="sxs-lookup"><span data-stu-id="7aa2c-149">Attached storage</span></span>
<span data-ttu-id="7aa2c-150">Collegare un nuovo tooboth disco macchine virtuali e creare i dischi di 5 GB nel processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-150">Attach a new disk tooboth VMs and create 5-GB disks in hello process.</span></span> <span data-ttu-id="7aa2c-151">dischi Hello sono ospitati nel contenitore di disco rigido virtuale hello in uso per i dischi del sistema operativo principale.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-151">hello disks are hosted in hello VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="7aa2c-152">Dopo che i dischi vengono creati e collegati, non si verifica alcun toorestart necessità Linux poiché kernel hello verrà visualizzato il nuovo dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-152">After disks are created and attached, there is no need toorestart Linux because hello kernel will see hello new device.</span></span> <span data-ttu-id="7aa2c-153">Questo dispositivo è in genere `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="7aa2c-154">Controllare `dmesg` per l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-154">Check `dmesg` for hello output.</span></span>

<span data-ttu-id="7aa2c-155">In ogni macchina virtuale, creare una partizione utilizzando `cfdisk` (partizione principale, di Linux) e scrittura hello nuova tabella di partizione.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write hello new partition table.</span></span> <span data-ttu-id="7aa2c-156">Non creare un file system in questa partizione.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-hello-cluster"></a><span data-ttu-id="7aa2c-157">Configurazione di cluster hello</span><span class="sxs-lookup"><span data-stu-id="7aa2c-157">Set up hello cluster</span></span>
<span data-ttu-id="7aa2c-158">Scegliere entrambe le macchine virtuali Ubuntu APT tooinstall Corosync Pacemaker e DRBD.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-158">Use APT tooinstall Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="7aa2c-159">toodo con `apt-get`, eseguire hello il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-159">toodo so with `apt-get`, run hello following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="7aa2c-160">Non installare MySQL a questo punto.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="7aa2c-161">Debian e Ubuntu gli script di installazione verranno inizializzato una directory di dati di MySQL in `/var/lib/mysql`, ma poiché la directory hello verrà essere sostituita da un file system DRBD, è necessario tooinstall MySQL in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because hello directory will be superseded by a DRBD file system, you need tooinstall MySQL later.</span></span>

<span data-ttu-id="7aa2c-162">Verificare (tramite `/sbin/ifconfig`) che entrambe le macchine virtuali utilizzano indirizzi nella subnet 10.10.10.0/24 hello e che è possibile eseguire il ping tra loro in base al nome.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in hello 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="7aa2c-163">È inoltre possibile utilizzare `ssh-keygen` e `ssh-copy-id` toomake che entrambe le macchine virtuali possono comunicare tramite SSH senza richiedere una password.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-163">You can also use `ssh-keygen` and `ssh-copy-id` toomake sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="7aa2c-164">Configurare DRBD</span><span class="sxs-lookup"><span data-stu-id="7aa2c-164">Set up DRBD</span></span>
<span data-ttu-id="7aa2c-165">Creare una risorsa DRBD che utilizza hello sottostante `/dev/sdc1` tooproduce partizionare un `/dev/drbd1` risorse che possono essere formattate usando ext3 e utilizzate nei nodi primari e secondari.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-165">Create a DRBD resource that uses hello underlying `/dev/sdc1` partition tooproduce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="7aa2c-166">Aprire `/etc/drbd.d/r0.res` e hello copia seguente definizione di risorsa in entrambe le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-166">Open `/etc/drbd.d/r0.res` and copy hello following resource definition on both VMs:</span></span>

        resource r0 {
          on `hadb01` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.4:7789;
            meta-disk internal;
          }
          on `hadb02` {
            device  /dev/drbd1;
            disk   /dev/sdc1;
            address  10.10.10.5:7789;
            meta-disk internal;
          }
        }

2. <span data-ttu-id="7aa2c-167">Inizializzare la risorsa hello usando `drbdadm` in entrambe le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-167">Initialize hello resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="7aa2c-168">Nella macchina virtuale primaria hello (`hadb01`), forzare la proprietà (primaria) della risorsa DRBD hello:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-168">On hello primary VM (`hadb01`), force ownership (primary) of hello DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="7aa2c-169">Se si esamina il contenuto di hello di proc/drbd (`sudo cat /proc/drbd`) su entrambe le macchine virtuali, dovrebbe essere `Primary/Secondary` su `hadb01` e `Secondary/Primary` su `hadb02`, coerente con la soluzione hello a questo punto.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-169">If you examine hello contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with hello solution at this point.</span></span> <span data-ttu-id="7aa2c-170">disco di 5 GB Hello verrà sincronizzato tramite rete 10.10.10.0/24 hello toocustomers alcun addebito.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-170">hello 5-GB disk is synchronized over hello 10.10.10.0/24 network at no charge toocustomers.</span></span>

<span data-ttu-id="7aa2c-171">Dopo la sincronizzazione disco hello, è possibile creare il sistema di file hello in `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-171">After hello disk is synchronized, you can create hello file system on `hadb01`.</span></span> <span data-ttu-id="7aa2c-172">A scopo di test, abbiamo utilizzato ext2, ma hello seguente codice verrà creato un file system ext3:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-172">For testing purposes, we used ext2, but hello following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-hello-drbd-resource"></a><span data-ttu-id="7aa2c-173">Montare hello DRBD risorsa</span><span class="sxs-lookup"><span data-stu-id="7aa2c-173">Mount hello DRBD resource</span></span>
<span data-ttu-id="7aa2c-174">Si è ora pronto toomount risorse DRBD hello `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-174">You're now ready toomount hello DRBD resources on `hadb01`.</span></span> <span data-ttu-id="7aa2c-175">Debian e i derivati usano `/var/lib/mysql` come directory dei dati di MySQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="7aa2c-176">Poiché non è stato installato MySQL, creare directory hello e montare hello DRBD risorsa.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-176">Because you haven't installed MySQL, create hello directory and mount hello DRBD resource.</span></span> <span data-ttu-id="7aa2c-177">tooperform questa opzione, eseguire hello seguendo codice `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-177">tooperform this option, run hello following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="7aa2c-178">Configurare MySQL</span><span class="sxs-lookup"><span data-stu-id="7aa2c-178">Set up MySQL</span></span>
<span data-ttu-id="7aa2c-179">A questo punto è pronti tooinstall MySQL in `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-179">Now you're ready tooinstall MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="7aa2c-180">Per `hadb02`sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="7aa2c-181">È possibile installare mysql server, che crea /var/lib/mysql, compilarlo con una nuova directory dei dati e quindi rimuovere il contenuto di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove hello contents.</span></span> <span data-ttu-id="7aa2c-182">tooperform questa opzione, eseguire hello seguendo codice `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-182">tooperform this option, run hello following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="7aa2c-183">seconda opzione Hello è toofailover troppo`hadb02` e quindi installare mysql-server non esiste.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-183">hello second option is toofailover too`hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="7aa2c-184">Gli script di installazione noteranno installazione esistente di hello e non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-184">Installation scripts will notice hello existing installation and won't touch it.</span></span>

<span data-ttu-id="7aa2c-185">Esecuzione hello il seguente codice in `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-185">Run hello following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="7aa2c-186">Esecuzione hello il seguente codice in `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-186">Run hello following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="7aa2c-187">Se a questo punto non si intende toofailover DRBD, hello prima opzione è più semplice, anche se probabilmente sia meno elegante.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-187">If you don't plan toofailover DRBD now, hello first option is easier although arguably less elegant.</span></span> <span data-ttu-id="7aa2c-188">Al termine della configurazione, è possibile iniziare a lavorare sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="7aa2c-189">Esecuzione hello il seguente codice in `hadb02` (o qualsiasi uno dei server hello è attivo, in base tooDRBD):</span><span class="sxs-lookup"><span data-stu-id="7aa2c-189">Run hello following code on `hadb02` (or whichever one of hello servers is active, according tooDRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* tooroot;

> [!WARNING]
> <span data-ttu-id="7aa2c-190">L'ultima istruzione disabilita in modo efficace l'autenticazione per l'utente root hello in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-190">This last statement effectively disables authentication for hello root user in this table.</span></span> <span data-ttu-id="7aa2c-191">È consigliabile sostituirla con istruzioni GRANT di livello di produzione ed è inclusa solo per scopi esplicativi.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="7aa2c-192">Se si desidera toomake query da macchine virtuali di hello esterno (ovvero scopo hello di questa Guida), è necessario anche tooenable di rete per MySQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-192">If you want toomake queries from outside hello VMs (which is hello purpose of this guide), you also need tooenable networking for MySQL.</span></span> <span data-ttu-id="7aa2c-193">In entrambe le macchine virtuali, aprire `/etc/mysql/my.cnf` e andare troppo`bind-address`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-193">On both VMs, open `/etc/mysql/my.cnf` and go too`bind-address`.</span></span> <span data-ttu-id="7aa2c-194">Modificare indirizzo hello da 127.0.0.1 too0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-194">Change hello address from 127.0.0.1 too0.0.0.0.</span></span> <span data-ttu-id="7aa2c-195">Dopo aver salvato il file hello, emettere un `sudo service mysql restart` sul server principale corrente.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-195">After saving hello file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-hello-mysql-load-balanced-set"></a><span data-ttu-id="7aa2c-196">Creare set di bilanciamento del carico di hello MySQL</span><span class="sxs-lookup"><span data-stu-id="7aa2c-196">Create hello MySQL load-balanced set</span></span>
<span data-ttu-id="7aa2c-197">Tornare indietro toohello portal, andare troppo`hadb01`e scegliere **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-197">Go back toohello portal, go too`hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="7aa2c-198">toocreate un endpoint, scegliere di MySQL (porta TCP 3306) dall'elenco a discesa hello e selezionare **set con bilanciamento del carico di nuova creazione**.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-198">toocreate an endpoint, choose MySQL (TCP 3306) from hello drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="7aa2c-199">Endpoint con bilanciamento del carico di nome hello `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-199">Name hello load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="7aa2c-200">Impostare **ora** too5 secondi minimi.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-200">Set **Time** too5 seconds, minimum.</span></span>

<span data-ttu-id="7aa2c-201">Dopo aver creato endpoint hello, andare troppo`hadb02`, scegliere **endpoint**e creare un endpoint.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-201">After you create hello endpoint, go too`hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="7aa2c-202">Scegliere `lb-mysql`, quindi selezionare MySQL dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-202">Choose `lb-mysql`, and then select MySQL from hello drop-down list.</span></span> <span data-ttu-id="7aa2c-203">È inoltre possibile utilizzare hello CLI di Azure per questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-203">You can also use hello Azure CLI for this step.</span></span>

<span data-ttu-id="7aa2c-204">È ora disponibile tutto il che necessario per l'operazione manuale del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-204">You now have everything you need for manual operation of hello cluster.</span></span>

### <a name="test-hello-load-balanced-set"></a><span data-ttu-id="7aa2c-205">Testare il set di bilanciamento del carico hello</span><span class="sxs-lookup"><span data-stu-id="7aa2c-205">Test hello load-balanced set</span></span>
<span data-ttu-id="7aa2c-206">I test possono essere eseguiti da un computer esterno usando qualsiasi client MySQL oppure con alcune applicazioni come phpMyAdmin in esecuzione come sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="7aa2c-207">In questo caso è stato usato lo strumento da riga di comando di MySQL su un'altra casella di Linux:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="7aa2c-208">Failover manuale</span><span class="sxs-lookup"><span data-stu-id="7aa2c-208">Manually failing over</span></span>
<span data-ttu-id="7aa2c-209">È possibile simulare il failover chiudendo MySQL, passando al nodo primario di DRBD e riavviando MySQL.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="7aa2c-210">tooperform questa attività esegue hello seguendo hadb01 codice:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-210">tooperform this task, run hello following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="7aa2c-211">Quindi, in hadb02:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="7aa2c-212">Dopo aver eseguito il failover manuale, è possibile ripetere la query remota, che dovrebbe funzionare perfettamente.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="7aa2c-213">Configurare Corosync</span><span class="sxs-lookup"><span data-stu-id="7aa2c-213">Set up Corosync</span></span>
<span data-ttu-id="7aa2c-214">Corosync è hello un'infrastruttura di cluster sottostante per Pacemaker toowork.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-214">Corosync is hello underlying cluster infrastructure required for Pacemaker toowork.</span></span> <span data-ttu-id="7aa2c-215">Per Heartbeat (e altri metodi come Ultramonkey) Corosync è una suddivisione delle funzionalità CRM hello, mentre il Pacemaker rimane tooHeartbeat più simile nella funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of hello CRM functionalities, while Pacemaker remains more similar tooHeartbeat in functionality.</span></span>

<span data-ttu-id="7aa2c-216">vincolo principale per Corosync Hello in Azure è che Corosync privilegia multicast broadcast unicast comunicazioni, ma la rete di Microsoft Azure supporta solo unicast.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-216">hello main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="7aa2c-217">Fortunatamente Corosync include una modalità di lavoro unicast.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="7aa2c-218">vincolo solo reale Hello è che, poiché tutti i nodi non comunicano tra loro, è necessario nodi hello toodefine nei file di configurazione, inclusi gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-218">hello only real constraint is that because all nodes are not communicating among themselves, you need toodefine hello nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="7aa2c-219">È possibile utilizzare file di esempio hello Corosync per Unicast e Modifica binding di indirizzo, elenchi di nodi e le directory di registrazione (Ubuntu Usa `/var/log/corosync` mentre utilizzato dai file di esempio hello `/var/log/cluster`) e consentire agli strumenti di quorum.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-219">We can use hello Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while hello example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="7aa2c-220">Utilizzare la seguente hello `transport: udpu` direttiva e hello definiti manualmente gli indirizzi IP per entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-220">Use hello following `transport: udpu` directive and hello manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="7aa2c-221">Esecuzione hello il seguente codice in `/etc/corosync/corosync.conf` per entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-221">Run hello following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

    totem {
      version: 2
      crypto_cipher: none
      crypto_hash: none
      interface {
        ringnumber: 0
        bindnetaddr: 10.10.10.0
        mcastport: 5405
        ttl: 1
      }
      transport: udpu
    }

    logging {
      fileline: off
      to_logfile: yes
      to_syslog: yes
      logfile: /var/log/corosync/corosync.log
      debug: off
      timestamp: on
      logger_subsys {
        subsys: QUORUM
        debug: off
        }
      }

    nodelist {
      node {
        ring0_addr: 10.10.10.4
        nodeid: 1
      }

      node {
        ring0_addr: 10.10.10.5
        nodeid: 2
      }
    }

    quorum {
      provider: corosync_votequorum
    }

<span data-ttu-id="7aa2c-222">Copiare il file di configurazione in entrambe le VM e avviare Corosync in entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="7aa2c-223">Subito dopo l'avvio del servizio di hello, è necessario stabilire cluster hello anello corrente hello e quorum deve essere costituito.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-223">Shortly after starting hello service, hello cluster should be established in hello current ring, and quorum should be constituted.</span></span> <span data-ttu-id="7aa2c-224">Revisione dei registri o eseguendo hello seguente di codice, è possibile controllare questa funzionalità:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-224">We can check this functionality by reviewing logs or by running hello following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="7aa2c-225">Si noterà toohello simili di output seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-225">You will see output similar toohello following image:</span></span>

![output di esempio di corosync-quorumtool -l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="7aa2c-227">Configurare Pacemaker</span><span class="sxs-lookup"><span data-stu-id="7aa2c-227">Set up Pacemaker</span></span>
<span data-ttu-id="7aa2c-228">Usa pacemaker hello toomonitor cluster per le risorse, definisce quando diminuisce primari e passa toosecondaries tali risorse.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-228">Pacemaker uses hello cluster toomonitor for resources, define when primaries go down, and switch those resources toosecondaries.</span></span> <span data-ttu-id="7aa2c-229">Le risorse possono essere definite da un set di script disponibili o da script LSB (simili all'inizializzazione), tra le altre possibilità.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="7aa2c-230">Vogliamo Pacemaker risorsa DRBD hello troppo "un" punto di montaggio hello e servizio MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-230">We want Pacemaker too"own" hello DRBD resource, hello mount point, and hello MySQL service.</span></span> <span data-ttu-id="7aa2c-231">Se il Pacemaker può attivare e disattivare DRBD, montare e smontare, quindi avviare e arrestare MySQL in hello destra ordine quando un'operazione non valida si verifica con hello primario, il programma di installazione è stata completata.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in hello right order when something bad happens with hello primary, setup is complete.</span></span>

<span data-ttu-id="7aa2c-232">Quando si installa Pacemaker per la prima volta, la configurazione dovrebbe essere molto semplice, come:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="7aa2c-233">Controllare la configurazione di hello eseguendo `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-233">Check hello configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="7aa2c-234">Quindi creare un file (ad esempio `/tmp/cluster.conf`) con hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-234">Then create a file (like `/tmp/cluster.conf`) with hello following resources:</span></span>

        primitive drbd_mysql ocf:linbit:drbd \
              params drbd_resource="r0" \
              op monitor interval="29s" role="Master" \
              op monitor interval="31s" role="Slave"

        ms ms_drbd_mysql drbd_mysql \
              meta master-max="1" master-node-max="1" \
                clone-max="2" clone-node-max="1" \
                notify="true"

        primitive fs_mysql ocf:heartbeat:Filesystem \
              params device="/dev/drbd/by-res/r0" \
              directory="/var/lib/mysql" fstype="ext3"

        primitive mysqld lsb:mysql

        group mysql fs_mysql mysqld

        colocation mysql_on_drbd \
               inf: mysql ms_drbd_mysql:Master

        order mysql_after_drbd \
               inf: ms_drbd_mysql:promote mysql:start

        property stonith-enabled=false

        property no-quorum-policy=ignore

3. <span data-ttu-id="7aa2c-235">Caricare il file hello in configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-235">Load hello file into hello configuration.</span></span> <span data-ttu-id="7aa2c-236">È necessario solo toodo questo in uno dei nodi.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-236">You only need toodo this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="7aa2c-237">Controllare che Pacemaker si avvii al momento giusto in entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="7aa2c-238">Utilizzando `sudo crm_mon –L`, verificare che uno dei nodi è diventato master hello per cluster hello e che è in esecuzione tutte le risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-238">By using `sudo crm_mon –L`, verify that one of your nodes has become hello master for hello cluster and is running all hello resources.</span></span> <span data-ttu-id="7aa2c-239">È possibile utilizzare montaggio e ps toocheck risorse hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-239">You can use mount and ps toocheck that hello resources are running.</span></span>

<span data-ttu-id="7aa2c-240">Hello seguente schermata mostra `crm_mon` con un solo nodo arrestato (uscita selezionando Ctrl + C):</span><span class="sxs-lookup"><span data-stu-id="7aa2c-240">hello following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![Nodo crm_mon arrestato](./media/mysql-cluster/image002.png)

<span data-ttu-id="7aa2c-242">Questa schermata mostra entrambi i nodi, uno master e uno slave:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-242">This screenshot shows both nodes, one master and one slave:</span></span>

![Master/slave operativo crm_mon](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="7aa2c-244">Test</span><span class="sxs-lookup"><span data-stu-id="7aa2c-244">Testing</span></span>
<span data-ttu-id="7aa2c-245">Ora è possibile eseguire una simulazione del failover automatico.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="7aa2c-246">Esistono due modi toodo questo: software e hardware.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-246">There are two ways toodo this: soft and hard.</span></span>

<span data-ttu-id="7aa2c-247">Hello soft viene utilizzata la funzione di arresto del cluster hello: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-247">hello soft way uses hello cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="7aa2c-248">Se si utilizza questa sul master hello, slave hello assume.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-248">If you use this on hello master, hello slave takes over.</span></span> <span data-ttu-id="7aa2c-249">Tenere presente che tooset questo toooff indietro.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-249">Remember tooset this back toooff.</span></span> <span data-ttu-id="7aa2c-250">In caso contrario, crm_mon mostrerà un solo nodo in standby.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="7aa2c-251">Hello complicata è in corso l'arresto verso il basso hello macchina virtuale primaria (hadb01) tramite il portale di hello o modificando hello /RL. su hello VM (ovvero, arresto, arresto).</span><span class="sxs-lookup"><span data-stu-id="7aa2c-251">hello hard way is shutting down hello primary VM (hadb01) via hello portal or by changing hello runlevel on hello VM (that is, halt, shutdown).</span></span> <span data-ttu-id="7aa2c-252">In questo modo Corosync e Pacemaker tramite segnalazioni corso della pagina master che hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-252">This helps Corosync and Pacemaker by signaling that hello master's going down.</span></span> <span data-ttu-id="7aa2c-253">È possibile testare questo (utile per le finestre di manutenzione), ma è anche possibile forzare scenario hello bloccando hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-253">You can test this (useful for maintenance windows), but you can also force hello scenario by freezing hello VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="7aa2c-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="7aa2c-254">STONITH</span></span>
<span data-ttu-id="7aa2c-255">Dovrebbe essere possibile tooissue un arresto della macchina virtuale tramite hello CLI di Azure anziché uno script STONITH che controlla un dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-255">It should be possible tooissue a VM shutdown via hello Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="7aa2c-256">È possibile utilizzare `/usr/lib/stonith/plugins/external/ssh` come base e abilitare STONITH nella configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in hello cluster's configuration.</span></span> <span data-ttu-id="7aa2c-257">CLI di Azure deve essere installato a livello globale e le impostazioni di pubblicazione hello e profilo deve essere caricato per l'utente del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-257">Azure CLI should be globally installed, and hello publish settings and profile should be loaded for hello cluster's user.</span></span>

<span data-ttu-id="7aa2c-258">È disponibile nel codice di esempio per la risorsa hello [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="7aa2c-258">Sample code for hello resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="7aa2c-259">Modificare la configurazione del cluster hello aggiungendo hello seguente troppo`sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-259">Change hello cluster's configuration by adding hello following too`sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="7aa2c-260">script Hello non esegue controlli su/giù.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-260">hello script doesn't perform up/down checks.</span></span> <span data-ttu-id="7aa2c-261">risorsa SSH originale Hello aveva 15 verifica ping, ma il tempo di recupero per una macchina virtuale di Azure potrebbe essere più variabile.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-261">hello original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="7aa2c-262">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="7aa2c-262">Limitations</span></span>
<span data-ttu-id="7aa2c-263">si applica Hello limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-263">hello following limitations apply:</span></span>

* <span data-ttu-id="7aa2c-264">script di risorsa DRBD linbit che gestisce DRBD come risorsa in Usa Pacemaker Hello `drbdadm down` durante l'arresto di un nodo, anche se il nodo hello solo in modalità standby.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-264">hello linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if hello node is just going on standby.</span></span> <span data-ttu-id="7aa2c-265">Questo non è ideale perché slave hello verrà non sincronizzati risorsa DRBD hello mentre master hello Ottiene scritture.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-265">This is not ideal because hello slave will not be synchronizing hello DRBD resource while hello master gets writes.</span></span> <span data-ttu-id="7aa2c-266">Se non viene eseguito gentilmente master hello, slave hello può richiedere più di un file system uno stato precedente.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-266">If hello master does not fail graciously, hello slave can take over an older file system state.</span></span> <span data-ttu-id="7aa2c-267">Per questo problema sono possibili due soluzioni:</span><span class="sxs-lookup"><span data-stu-id="7aa2c-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="7aa2c-268">Applicare un `drbdadm up r0` in tutti i nodi del cluster tramite un watchdog locale (non appartenente al cluster) oppure</span><span class="sxs-lookup"><span data-stu-id="7aa2c-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="7aa2c-269">Modifica di script di hello linbit DRBD, assicurandosi che `down` non viene chiamato in`/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="7aa2c-269">Editing hello linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="7aa2c-270">servizio di bilanciamento del carico Hello deve toorespond almeno cinque secondi, in modo che le applicazioni devono essere compatibile con cluster e più tolleranti di timeout.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-270">hello load balancer needs at least five seconds toorespond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="7aa2c-271">Possono essere utili anche altre architetture, quali le code in-app e i middleware di query.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="7aa2c-272">Ottimizzazione di MySQL è necessario tooensure scrittura eseguita a un ritmo gestibile e memorizza nella cache è stati scaricati toodisk con una frequenza toominimize possibili perdite di memoria.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-272">MySQL tuning is necessary tooensure that writing is done at a manageable pace and caches are flushed toodisk as frequently as possible toominimize memory loss.</span></span>
* <span data-ttu-id="7aa2c-273">Scrivere le prestazioni sono dipendenti in una macchina virtuale nel commutatore virtuale hello sono collegati perché questo è il meccanismo di hello utilizzato da DRBD tooreplicate hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7aa2c-273">Write performance is dependent in VM interconnect in hello virtual switch because this is hello mechanism used by DRBD tooreplicate hello device.</span></span>
