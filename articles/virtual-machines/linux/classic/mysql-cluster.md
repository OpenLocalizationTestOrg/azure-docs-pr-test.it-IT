---
title: Creare un cluster MySQL con set con carico bilanciato | Microsoft Docs
description: "Configurare un cluster MySQL di Linux con bilanciamento del carico e disponibilità elevata creato con il modello di distribuzione classica in Azure"
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
ms.openlocfilehash: 4eaf86c9ac3e4dc2b51b88383626eda774cab0e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-load-balanced-sets-to-clusterize-mysql-on-linux"></a><span data-ttu-id="9cbb3-103">Usare set con bilanciamento del carico per creare un cluster MySQL su Linux</span><span class="sxs-lookup"><span data-stu-id="9cbb3-103">Use load-balanced sets to clusterize MySQL on Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9cbb3-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e la distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="9cbb3-105">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-105">This article covers using the classic deployment model.</span></span> <span data-ttu-id="9cbb3-106">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="9cbb3-107">È disponibile un [modello di Resource Manager](https://azure.microsoft.com/documentation/templates/mysql-replication/) per la distribuzione di un cluster MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-107">A [Resource Manager template](https://azure.microsoft.com/documentation/templates/mysql-replication/) is available if you need to deploy a MySQL cluster.</span></span>

<span data-ttu-id="9cbb3-108">Questo articolo esplora e illustra i diversi approcci disponibili per distribuire servizi basati su Linux con disponibilità elevata su Microsoft Azure, esaminando principalmente l'elevata disponibilità del server MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-108">This article explores and illustrates the different approaches available to deploy highly available Linux-based services on Microsoft Azure, exploring MySQL Server high availability as a primer.</span></span> <span data-ttu-id="9cbb3-109">Su [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL)è disponibile un video che illustra questo approccio.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-109">A video illustrating this approach is available on [Channel 9](http://channel9.msdn.com/Blogs/Open/Load-balancing-highly-available-Linux-services-on-Windows-Azure-OpenLDAP-and-MySQL).</span></span>

<span data-ttu-id="9cbb3-110">Sarà descritta una soluzione con disponibilità elevata MySQL a master singolo, con due nodi e nessuna condivisione, basata su DRBD, Corosync e Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-110">We will outline a shared-nothing, two-node, single-master MySQL high availability solution based on DRBD, Corosync, and Pacemaker.</span></span> <span data-ttu-id="9cbb3-111">MySQL viene eseguito solo su un nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-111">Only one node runs MySQL at a time.</span></span> <span data-ttu-id="9cbb3-112">Anche la lettura e la scrittura dalla risorsa DRBD sono limitate a un solo nodo alla volta.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-112">Reading and writing from the DRBD resource is also limited to only one node at a time.</span></span>

<span data-ttu-id="9cbb3-113">Non è necessaria una soluzione IP virtuale come LVS, in quanto si useranno i set con carico bilanciato in Microsoft Azure per garantire la funzionalità round robin e il rilevamento dell'endpoint, la rimozione e il ripristino gestito automaticamente dell'indirizzo VIP.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-113">There's no need for a VIP solution like LVS, because you'll use load-balanced sets in Microsoft Azure to provide round-robin functionality and endpoint detection, removal, and graceful recovery of the VIP.</span></span> <span data-ttu-id="9cbb3-114">L'indirizzo VIP è un indirizzo IPv4 instradabile a livello globale assegnato da Microsoft Azure durante la creazione del servizio cloud.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-114">The VIP is a globally routable IPv4 address assigned by Microsoft Azure when you first create the cloud service.</span></span>

<span data-ttu-id="9cbb3-115">È possibile usare altre architetture per MySQL inclusi NBD Cluster, Percona, Galera e varie soluzioni middleware, di cui almeno una disponibile come VM su [VM Depot](http://vmdepot.msopentech.com).</span><span class="sxs-lookup"><span data-stu-id="9cbb3-115">There are other possible architectures for MySQL, including NBD Cluster, Percona, Galera, and several middleware solutions, including at least one available as a VM on [VM Depot](http://vmdepot.msopentech.com).</span></span> <span data-ttu-id="9cbb3-116">Se le soluzioni possono eseguire la replica su unicast piuttosto che su multicast o trasmissione e non si basano su un archivio condiviso o su più interfacce di rete, gli scenari dovrebbero risultare facili da distribuire su Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-116">As long as these solutions can replicate on unicast vs. multicast or broadcast and don't rely on shared storage or multiple network interfaces, the scenarios should be easy to deploy on Microsoft Azure.</span></span>

<span data-ttu-id="9cbb3-117">Queste architetture di clustering possono essere estese ad altri prodotti come PostgreSQL e OpenLDAP in modo simile.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-117">These clustering architectures can be extended to other products like PostgreSQL and OpenLDAP in a similar fashion.</span></span> <span data-ttu-id="9cbb3-118">Questa procedura di bilanciamento del carico senza condivisione è stata ad esempio testata con OpenLDAP multimaster ed è possibile vederne i risultati sul blog di Channel 9.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-118">For example, this load-balancing procedure with shared nothing was successfully tested with multi-master OpenLDAP, and you can watch it on our Channel 9 blog.</span></span>

## <a name="get-ready"></a><span data-ttu-id="9cbb3-119">Preparazione</span><span class="sxs-lookup"><span data-stu-id="9cbb3-119">Get ready</span></span>
<span data-ttu-id="9cbb3-120">Sono necessarie le risorse e funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-120">You need the following resources and abilities:</span></span>

  - <span data-ttu-id="9cbb3-121">Un account di Microsoft Azure con una sottoscrizione valida, in grado di creare almeno due VM (in questo esempio è stato usato XS)</span><span class="sxs-lookup"><span data-stu-id="9cbb3-121">A Microsoft Azure account with a valid subscription, able to create at least two VMs (XS was used in this example)</span></span>
  - <span data-ttu-id="9cbb3-122">Una rete e una subnet</span><span class="sxs-lookup"><span data-stu-id="9cbb3-122">A network and a subnet</span></span>
  - <span data-ttu-id="9cbb3-123">Un gruppo di affinità</span><span class="sxs-lookup"><span data-stu-id="9cbb3-123">An affinity group</span></span>
  - <span data-ttu-id="9cbb3-124">Un set di disponibilità</span><span class="sxs-lookup"><span data-stu-id="9cbb3-124">An availability set</span></span>
  - <span data-ttu-id="9cbb3-125">La possibilità di creare dischi rigidi virtuali nella stessa area del servizio cloud e collegarli alle VM Linux</span><span class="sxs-lookup"><span data-stu-id="9cbb3-125">The ability to create VHDs in the same region as the cloud service and attach them to the Linux VMs</span></span>

### <a name="tested-environment"></a><span data-ttu-id="9cbb3-126">Ambiente testato</span><span class="sxs-lookup"><span data-stu-id="9cbb3-126">Tested environment</span></span>
* <span data-ttu-id="9cbb3-127">Ubuntu 13.10</span><span class="sxs-lookup"><span data-stu-id="9cbb3-127">Ubuntu 13.10</span></span>
  * <span data-ttu-id="9cbb3-128">DRBD</span><span class="sxs-lookup"><span data-stu-id="9cbb3-128">DRBD</span></span>
  * <span data-ttu-id="9cbb3-129">Server MySQL</span><span class="sxs-lookup"><span data-stu-id="9cbb3-129">MySQL Server</span></span>
  * <span data-ttu-id="9cbb3-130">Corosync e Pacemaker</span><span class="sxs-lookup"><span data-stu-id="9cbb3-130">Corosync and Pacemaker</span></span>

### <a name="affinity-group"></a><span data-ttu-id="9cbb3-131">Gruppo di affinità</span><span class="sxs-lookup"><span data-stu-id="9cbb3-131">Affinity group</span></span>
<span data-ttu-id="9cbb3-132">Creare un gruppo di affinità per la soluzione accedendo al portale di Azure classico, selezionando **Impostazioni** e creando un gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-132">Create an affinity group for the solution by signing in to the Azure classic portal, selecting **Settings**, and creating an affinity group.</span></span> <span data-ttu-id="9cbb3-133">Le risorse allocate create in seguito verranno assegnate a questo gruppo di affinità.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-133">Allocated resources created later will be assigned to this affinity group.</span></span>

### <a name="networks"></a><span data-ttu-id="9cbb3-134">Reti</span><span class="sxs-lookup"><span data-stu-id="9cbb3-134">Networks</span></span>
<span data-ttu-id="9cbb3-135">Vengono create una nuova rete e una subnet all'interno della rete.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-135">A new network is created, and a subnet is created inside the network.</span></span> <span data-ttu-id="9cbb3-136">Questo esempio usa una rete 10.10.10.0/24 contenente una sola subnet /24.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-136">This example uses a 10.10.10.0/24 network with only one /24 subnet inside.</span></span>

### <a name="virtual-machines"></a><span data-ttu-id="9cbb3-137">Macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="9cbb3-137">Virtual machines</span></span>
<span data-ttu-id="9cbb3-138">La prima VM Ubuntu 13.10 viene creata con un'immagine della raccolta Ubuntu approvata ed è denominata `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-138">The first Ubuntu 13.10 VM is created by using an Endorsed Ubuntu Gallery image and is called `hadb01`.</span></span> <span data-ttu-id="9cbb3-139">Nel processo viene creato un nuovo servizio cloud, denominato hadb.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-139">A new cloud service is created in the process, called hadb.</span></span> <span data-ttu-id="9cbb3-140">Questo nome indica la natura condivisa e con bilanciamento del carico che il servizio avrà al momento dell'aggiunta di altre risorse.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-140">This name illustrates the shared, load-balanced nature that the service will have when more resources are added.</span></span> <span data-ttu-id="9cbb3-141">La creazione di `hadb01` è molto semplice e la si esegue mediante il portale.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-141">The creation of `hadb01` is uneventful and completed by using the portal.</span></span> <span data-ttu-id="9cbb3-142">Viene creato automaticamente un endpoint per SSH e viene selezionata la nuova rete.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-142">An endpoint for SSH is automatically created, and the new network is selected.</span></span> <span data-ttu-id="9cbb3-143">Ora è possibile creare un set di disponibilità per le VM.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-143">Now you can create an availability set for the VMs.</span></span>

<span data-ttu-id="9cbb3-144">Dopo aver creato la prima VM (tecnicamente quando viene creato il servizio cloud), creare la seconda VM, `hadb02`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-144">After the first VM is created (technically, when the cloud service is created), create the second VM, `hadb02`.</span></span> <span data-ttu-id="9cbb3-145">Anche per la seconda VM si userà una VM Ubuntu 13.10 della raccolta tramite il portale, ma si userà un servizio cloud esistente, `hadb.cloudapp.net`, anziché crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-145">For the second VM, use Ubuntu 13.10 VM from the Gallery by using the portal, but use an existing cloud service, `hadb.cloudapp.net`, instead of creating a new one.</span></span> <span data-ttu-id="9cbb3-146">La rete e il set di disponibilità dovrebbero essere selezionati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-146">The network and availability set should be automatically selected.</span></span> <span data-ttu-id="9cbb3-147">Verrà anche creato un endpoint SSH.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-147">An SSH endpoint will be created, too.</span></span>

<span data-ttu-id="9cbb3-148">Dopo aver creato entrambe le macchine virtuali, prendere nota della porta SSH per `hadb01` (TCP 22) e `hadb02` (assegnata automaticamente da Azure).</span><span class="sxs-lookup"><span data-stu-id="9cbb3-148">After both VMs have been created, take note of the SSH port for `hadb01` (TCP 22) and `hadb02` (automatically assigned by Azure).</span></span>

### <a name="attached-storage"></a><span data-ttu-id="9cbb3-149">Archivio collegato</span><span class="sxs-lookup"><span data-stu-id="9cbb3-149">Attached storage</span></span>
<span data-ttu-id="9cbb3-150">Collegare un nuovo disco a entrambe le VM e creare nuovi dischi da 5 GB durante il processo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-150">Attach a new disk to both VMs and create 5-GB disks in the process.</span></span> <span data-ttu-id="9cbb3-151">I dischi sono ospitati nel contenitore del disco rigido virtuale in uso per i dischi del sistema operativo principale.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-151">The disks are hosted in the VHD container in use for your main operating system disks.</span></span> <span data-ttu-id="9cbb3-152">Dopo la creazione e il collegamento dei dischi non è necessario riavviare Linux, in quanto il kernel rileva il nuovo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-152">After disks are created and attached, there is no need to restart Linux because the kernel will see the new device.</span></span> <span data-ttu-id="9cbb3-153">Questo dispositivo è in genere `/dev/sdc`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-153">This device is usually `/dev/sdc`.</span></span> <span data-ttu-id="9cbb3-154">Controllare l'output di `dmesg`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-154">Check `dmesg` for the output.</span></span>

<span data-ttu-id="9cbb3-155">In ogni VM creare una nuova partizione usando `cfdisk` (partizione primaria Linux) e scrivendo la nuova tabella di partizione.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-155">On each VM, create a partition by using `cfdisk` (primary, Linux partition) and write the new partition table.</span></span> <span data-ttu-id="9cbb3-156">Non creare un file system in questa partizione.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-156">Do not create a file system on this partition.</span></span>

## <a name="set-up-the-cluster"></a><span data-ttu-id="9cbb3-157">Configurazione del cluster</span><span class="sxs-lookup"><span data-stu-id="9cbb3-157">Set up the cluster</span></span>
<span data-ttu-id="9cbb3-158">Usare APT per installare Corosync, Pacemaker e DRBD su entrambe le VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-158">Use APT to install Corosync, Pacemaker, and DRBD on both Ubuntu VMs.</span></span> <span data-ttu-id="9cbb3-159">Per farlo con `apt-get`, eseguire il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-159">To do so with `apt-get`, run the following code:</span></span>

    sudo apt-get install corosync pacemaker drbd8-utils.

<span data-ttu-id="9cbb3-160">Non installare MySQL a questo punto.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-160">Do not install MySQL at this time.</span></span> <span data-ttu-id="9cbb3-161">Gli script di installazione Debian e Ubuntu inizializzeranno una directory di dati MySQL in `/var/lib/mysql`, ma poiché la directory verrà sostituita da un file system DRBD, è necessario installare MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-161">Debian and Ubuntu installation scripts will initialize a MySQL data directory on `/var/lib/mysql`, but because the directory will be superseded by a DRBD file system, you need to install MySQL later.</span></span>

<span data-ttu-id="9cbb3-162">Verificare (con `/sbin/ifconfig`) che entrambe le macchine virtuali usino indirizzi della subnet 10.10.10.0/24 e che siano in grado di eseguire il ping reciprocamente in base al nome.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-162">Verify (by using `/sbin/ifconfig`) that both VMs are using addresses in the 10.10.10.0/24 subnet and that they can ping each other by name.</span></span> <span data-ttu-id="9cbb3-163">È anche possibile usare `ssh-keygen` e `ssh-copy-id` per verificare che entrambe le macchine virtuali siano in grado di comunicare tramite SSH senza che sia necessaria una password.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-163">You can also use `ssh-keygen` and `ssh-copy-id` to make sure both VMs can communicate via SSH without requiring a password.</span></span>

### <a name="set-up-drbd"></a><span data-ttu-id="9cbb3-164">Configurare DRBD</span><span class="sxs-lookup"><span data-stu-id="9cbb3-164">Set up DRBD</span></span>
<span data-ttu-id="9cbb3-165">Creare una risorsa DRBD che usa la partizione `/dev/sdc1` sottostante per produrre una risorsa `/dev/drbd1` che possa essere formattata con ext3 e usata in nodi primari e secondari.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-165">Create a DRBD resource that uses the underlying `/dev/sdc1` partition to produce a `/dev/drbd1` resource that can be formatted by using ext3 and used in both primary and secondary nodes.</span></span>

1. <span data-ttu-id="9cbb3-166">Aprire `/etc/drbd.d/r0.res` e copiare la definizione di risorsa seguente in entrambe le VM:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-166">Open `/etc/drbd.d/r0.res` and copy the following resource definition on both VMs:</span></span>

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

2. <span data-ttu-id="9cbb3-167">Inizializzare la risorsa utilizzando `drbdadm` in entrambe le VM:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-167">Initialize the resource by using `drbdadm` on both VMs:</span></span>

        sudo drbdadm -c /etc/drbd.conf role r0
        sudo drbdadm up r0

3. <span data-ttu-id="9cbb3-168">Sulla VM primaria (`hadb01`) forzare la proprietà (primaria) della risorsa DRBD:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-168">On the primary VM (`hadb01`), force ownership (primary) of the DRBD resource:</span></span>

        sudo drbdadm primary --force r0

<span data-ttu-id="9cbb3-169">A questo punto, nel contenuto di /proc/drbd (`sudo cat /proc/drbd`) su entrambe le macchine virtuali, dovrebbe essere presente `Primary/Secondary` su `hadb01` e `Secondary/Primary` su `hadb02`, coerentemente con la soluzione.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-169">If you examine the contents of /proc/drbd (`sudo cat /proc/drbd`) on both VMs, you should see `Primary/Secondary` on `hadb01` and `Secondary/Primary` on `hadb02`, consistent with the solution at this point.</span></span> <span data-ttu-id="9cbb3-170">Il disco da 5 GB viene sincronizzato sulla rete 10.10.10.0/24 senza costi per i clienti.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-170">The 5-GB disk is synchronized over the 10.10.10.0/24 network at no charge to customers.</span></span>

<span data-ttu-id="9cbb3-171">Quando il disco è sincronizzato, è possibile creare il file system su `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-171">After the disk is synchronized, you can create the file system on `hadb01`.</span></span> <span data-ttu-id="9cbb3-172">Per le operazioni di test è stato usato ext2, ma il codice seguente crea un file system ext3:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-172">For testing purposes, we used ext2, but the following code will create an ext3 file system:</span></span>

    mkfs.ext3 /dev/drbd1

### <a name="mount-the-drbd-resource"></a><span data-ttu-id="9cbb3-173">Montare la risorsa DRBD</span><span class="sxs-lookup"><span data-stu-id="9cbb3-173">Mount the DRBD resource</span></span>
<span data-ttu-id="9cbb3-174">Ora è possibile montare le risorse DRBD in `hadb01`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-174">You're now ready to mount the DRBD resources on `hadb01`.</span></span> <span data-ttu-id="9cbb3-175">Debian e i derivati usano `/var/lib/mysql` come directory dei dati di MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-175">Debian and derivatives use `/var/lib/mysql` as MySQL's data directory.</span></span> <span data-ttu-id="9cbb3-176">Poiché MySQL non è installato, creare la directory e montare la risorsa DRBD.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-176">Because you haven't installed MySQL, create the directory and mount the DRBD resource.</span></span> <span data-ttu-id="9cbb3-177">Per eseguire questa opzione, eseguire il codice seguente su `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-177">To perform this option, run the following code on `hadb01`:</span></span>

    sudo mkdir /var/lib/mysql
    sudo mount /dev/drbd1 /var/lib/mysql

## <a name="set-up-mysql"></a><span data-ttu-id="9cbb3-178">Configurare MySQL</span><span class="sxs-lookup"><span data-stu-id="9cbb3-178">Set up MySQL</span></span>
<span data-ttu-id="9cbb3-179">A questo punto si può installare MySQL su `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-179">Now you're ready to install MySQL on `hadb01`:</span></span>

    sudo apt-get install mysql-server

<span data-ttu-id="9cbb3-180">Per `hadb02`sono disponibili due opzioni.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-180">For `hadb02`, you have two options.</span></span> <span data-ttu-id="9cbb3-181">È possibile installare mysql-server creando in questo modo /var/lib/mysql, inserirvi una nuova directory dati e poi rimuovere i contenuti.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-181">You can install mysql-server, which will create /var/lib/mysql, fill it with a new data directory, and then remove the contents.</span></span> <span data-ttu-id="9cbb3-182">Per eseguire questa opzione, eseguire il codice seguente su `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-182">To perform this option, run the following code on `hadb02`:</span></span>

    sudo apt-get install mysql-server
    sudo service mysql stop
    sudo rm –rf /var/lib/mysql/*

<span data-ttu-id="9cbb3-183">La seconda opzione è eseguire il failover su `hadb02` e quindi installare mysql-server là.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-183">The second option is to failover to `hadb02` and then install mysql-server there.</span></span> <span data-ttu-id="9cbb3-184">Gli script di installazione rileveranno l'installazione esistente e non la toccheranno.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-184">Installation scripts will notice the existing installation and won't touch it.</span></span>

<span data-ttu-id="9cbb3-185">Eseguire il codice seguente in `hadb01`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-185">Run the following code on `hadb01`:</span></span>

    sudo drbdadm secondary –force r0

<span data-ttu-id="9cbb3-186">Eseguire il codice seguente in `hadb02`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-186">Run the following code on `hadb02`:</span></span>

    sudo drbdadm primary –force r0
    sudo apt-get install mysql-server

<span data-ttu-id="9cbb3-187">Se non si prevede di eseguire il failover di DRBD a questo punto, la prima opzione è più semplice, anche se meno elegante.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-187">If you don't plan to failover DRBD now, the first option is easier although arguably less elegant.</span></span> <span data-ttu-id="9cbb3-188">Al termine della configurazione, è possibile iniziare a lavorare sul database MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-188">After you set this up, you can start working on your MySQL database.</span></span> <span data-ttu-id="9cbb3-189">Eseguire il codice seguente in `hadb02` (o su qualsiasi server attivo, in base a DRBD):</span><span class="sxs-lookup"><span data-stu-id="9cbb3-189">Run the following code on `hadb02` (or whichever one of the servers is active, according to DRBD):</span></span>

    mysql –u root –p
    CREATE DATABASE azureha;
    CREATE TABLE things ( id SERIAL, name VARCHAR(255) );
    INSERT INTO things VALUES (1, "Yet another entity");
    GRANT ALL ON things.\* TO root;

> [!WARNING]
> <span data-ttu-id="9cbb3-190">Quest'ultima istruzione disabilita in modo efficace l'autenticazione per l'utente ROOT in questa tabella.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-190">This last statement effectively disables authentication for the root user in this table.</span></span> <span data-ttu-id="9cbb3-191">È consigliabile sostituirla con istruzioni GRANT di livello di produzione ed è inclusa solo per scopi esplicativi.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-191">This should be replaced by your production-grade GRANT statements and is included only for illustrative purposes.</span></span>

<span data-ttu-id="9cbb3-192">Se si vuole eseguire query dall'esterno delle VM, che è lo scopo di questa guida, occorre anche abilitare le connessioni di rete per MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-192">If you want to make queries from outside the VMs (which is the purpose of this guide), you also need to enable networking for MySQL.</span></span> <span data-ttu-id="9cbb3-193">In entrambe le VM aprire `/etc/mysql/my.cnf` e passare a `bind-address`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-193">On both VMs, open `/etc/mysql/my.cnf` and go to `bind-address`.</span></span> <span data-ttu-id="9cbb3-194">Cambiare l'indirizzo da 127.0.0.1 in 0.0.0.0.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-194">Change the address from 127.0.0.1 to 0.0.0.0.</span></span> <span data-ttu-id="9cbb3-195">Dopo aver salvato il file, inviare un comando `sudo service mysql restart` al nodo primario corrente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-195">After saving the file, issue a `sudo service mysql restart` on your current primary.</span></span>

### <a name="create-the-mysql-load-balanced-set"></a><span data-ttu-id="9cbb3-196">Creare il set con carico bilanciato di MySQL</span><span class="sxs-lookup"><span data-stu-id="9cbb3-196">Create the MySQL load-balanced set</span></span>
<span data-ttu-id="9cbb3-197">Tornare al portale, passare a `hadb01` e scegliere **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-197">Go back to the portal, go to `hadb01`, and choose **Endpoints**.</span></span> <span data-ttu-id="9cbb3-198">Per creare un endpoint, scegliere MySQL (TCP 3306) dall'elenco a discesa e selezionare **Crea nuovo con carico bilanciato**.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-198">To create an endpoint, choose MySQL (TCP 3306) from the drop-down list and select **Create new load balanced set**.</span></span> <span data-ttu-id="9cbb3-199">Assegnare un nome all'endpoint con carico bilanciato `lb-mysql`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-199">Name the load-balanced endpoint `lb-mysql`.</span></span> <span data-ttu-id="9cbb3-200">Impostare **Tempo** su 5 secondi, come valore minimo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-200">Set **Time** to 5 seconds, minimum.</span></span>

<span data-ttu-id="9cbb3-201">Dopo aver creato l'endpoint, passare a `hadb02`, selezionare **Endpoint** e creare un endpoint.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-201">After you create the endpoint, go to `hadb02`, choose **Endpoints**, and create an endpoint.</span></span> <span data-ttu-id="9cbb3-202">Scegliere `lb-mysql`, quindi selezionare MySQL dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-202">Choose `lb-mysql`, and then select MySQL from the drop-down list.</span></span> <span data-ttu-id="9cbb3-203">È anche possibile usare CLI di Azure per questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-203">You can also use the Azure CLI for this step.</span></span>

<span data-ttu-id="9cbb3-204">Ora si ha tutto l'occorrente per il funzionamento manuale del cluster.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-204">You now have everything you need for manual operation of the cluster.</span></span>

### <a name="test-the-load-balanced-set"></a><span data-ttu-id="9cbb3-205">Eseguire test sul set con carico bilanciato</span><span class="sxs-lookup"><span data-stu-id="9cbb3-205">Test the load-balanced set</span></span>
<span data-ttu-id="9cbb3-206">I test possono essere eseguiti da un computer esterno usando qualsiasi client MySQL oppure con alcune applicazioni come phpMyAdmin in esecuzione come sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-206">Tests can be performed from an outside machine by using any MySQL client, or by using certain applications, like phpMyAdmin running as an Azure website.</span></span> <span data-ttu-id="9cbb3-207">In questo caso è stato usato lo strumento da riga di comando di MySQL su un'altra casella di Linux:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-207">In this case, you used MySQL's command-line tool on another Linux box:</span></span>

    mysql azureha –u root –h hadb.cloudapp.net –e "select * from things;"

### <a name="manually-failing-over"></a><span data-ttu-id="9cbb3-208">Failover manuale</span><span class="sxs-lookup"><span data-stu-id="9cbb3-208">Manually failing over</span></span>
<span data-ttu-id="9cbb3-209">È possibile simulare il failover chiudendo MySQL, passando al nodo primario di DRBD e riavviando MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-209">You can simulate failovers by shutting down MySQL, switching DRBD's primary, and starting MySQL again.</span></span>

<span data-ttu-id="9cbb3-210">Per eseguire questa attività, eseguire il codice seguente in hadb01:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-210">To perform this task, run the following code on hadb01:</span></span>

    service mysql stop && umount /var/lib/mysql ; drbdadm secondary r0

<span data-ttu-id="9cbb3-211">Quindi, in hadb02:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-211">Then, on hadb02:</span></span>

    drbdadm primary r0 ; mount /dev/drbd1 /var/lib/mysql && service mysql start

<span data-ttu-id="9cbb3-212">Dopo aver eseguito il failover manuale, è possibile ripetere la query remota, che dovrebbe funzionare perfettamente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-212">After you fail over manually, you can repeat your remote query and it should work perfectly.</span></span>

## <a name="set-up-corosync"></a><span data-ttu-id="9cbb3-213">Configurare Corosync</span><span class="sxs-lookup"><span data-stu-id="9cbb3-213">Set up Corosync</span></span>
<span data-ttu-id="9cbb3-214">Corosync è l'infrastruttura di cluster sottostante necessaria per il funzionamento di Pacemaker.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-214">Corosync is the underlying cluster infrastructure required for Pacemaker to work.</span></span> <span data-ttu-id="9cbb3-215">Per Heartbeat (e altre metodologie come Ultramonkey), Corosync è una parte delle funzionalità CRM, mentre Pacemaker rimane più simile ad Heartbeat per funzionalità.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-215">For Heartbeat (and other methodologies like Ultramonkey), Corosync is a split of the CRM functionalities, while Pacemaker remains more similar to Heartbeat in functionality.</span></span>

<span data-ttu-id="9cbb3-216">Il vincolo principale per Corosync su Azure sta nel fatto che Corosync preferisce il multicast alla trasmissione su comunicazioni unicast, mentre le reti Microsoft Azure supportano solo l'unicast.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-216">The main constraint for Corosync on Azure is that Corosync prefers multicast over broadcast over unicast communications, but Microsoft Azure networking only supports unicast.</span></span>

<span data-ttu-id="9cbb3-217">Fortunatamente Corosync include una modalità di lavoro unicast.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-217">Fortunately, Corosync has a working unicast mode.</span></span> <span data-ttu-id="9cbb3-218">L'unico vero vincolo è che, poiché i nodi non comunicano tutti tra loro, è necessario definire i nodi nei file di configurazione, incluso l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-218">The only real constraint is that because all nodes are not communicating among themselves, you need to define the nodes in your configuration files, including their IP addresses.</span></span> <span data-ttu-id="9cbb3-219">È possibile usare i file di esempio di Corosync per Unicast, cambiare l'indirizzo di associazione, l'elenco dei nodi e le directory di registrazione (Ubuntu usa `/var/log/corosync` mentre i file di esempio usano `/var/log/cluster`) e abilitare gli strumenti del quorum.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-219">We can use the Corosync example files for Unicast and change bind address, node lists, and logging directories (Ubuntu uses `/var/log/corosync` while the example files use `/var/log/cluster`), and enable quorum tools.</span></span>

> [!NOTE]
> <span data-ttu-id="9cbb3-220">Usare la seguente direttiva `transport: udpu` e gli indirizzi IP definiti manualmente per entrambi i nodi.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-220">Use the following `transport: udpu` directive and the manually defined IP addresses for both nodes.</span></span>

<span data-ttu-id="9cbb3-221">Eseguire il codice seguente in `/etc/corosync/corosync.conf` per entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-221">Run the following code on `/etc/corosync/corosync.conf` for both nodes:</span></span>

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

<span data-ttu-id="9cbb3-222">Copiare il file di configurazione in entrambe le VM e avviare Corosync in entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-222">Copy this configuration file on both VMs and start Corosync in both nodes:</span></span>

    sudo service start corosync

<span data-ttu-id="9cbb3-223">Poco dopo aver avviato il servizio, dovrebbe venire stabilito il cluster nell'anello corrente e il quorum dovrebbe essere costituito.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-223">Shortly after starting the service, the cluster should be established in the current ring, and quorum should be constituted.</span></span> <span data-ttu-id="9cbb3-224">Per verificare questa funzionalità, controllare i log oppure eseguire il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-224">We can check this functionality by reviewing logs or by running the following code:</span></span>

    sudo corosync-quorumtool –l

<span data-ttu-id="9cbb3-225">L'output sarà simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-225">You will see output similar to the following image:</span></span>

![output di esempio di corosync-quorumtool -l](./media/mysql-cluster/image001.png)

## <a name="set-up-pacemaker"></a><span data-ttu-id="9cbb3-227">Configurare Pacemaker</span><span class="sxs-lookup"><span data-stu-id="9cbb3-227">Set up Pacemaker</span></span>
<span data-ttu-id="9cbb3-228">Pacemaker usa il cluster per monitorare le risorse, definire quando i nodi primari diventano inattivi e passare le risorse ai nodi secondari.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-228">Pacemaker uses the cluster to monitor for resources, define when primaries go down, and switch those resources to secondaries.</span></span> <span data-ttu-id="9cbb3-229">Le risorse possono essere definite da un set di script disponibili o da script LSB (simili all'inizializzazione), tra le altre possibilità.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-229">Resources can be defined from a set of available scripts or from LSB (init-like) scripts, among other choices.</span></span>

<span data-ttu-id="9cbb3-230">Si vuole che Pacemaker "possegga" la risorsa DRBD, il punto di montaggio e il servizio MySQL.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-230">We want Pacemaker to "own" the DRBD resource, the mount point, and the MySQL service.</span></span> <span data-ttu-id="9cbb3-231">Se Pacemaker è in grado di attivare e disattivare DRBD, montarlo e smontarlo, quindi avviare e interrompere MySQL nell'ordine corretto in caso di errori del nodo primario, e la configurazione è completa.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-231">If Pacemaker can turn on and off DRBD, mount and unmount it, and then start and stop MySQL in the right order when something bad happens with the primary, setup is complete.</span></span>

<span data-ttu-id="9cbb3-232">Quando si installa Pacemaker per la prima volta, la configurazione dovrebbe essere molto semplice, come:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-232">When you first install Pacemaker, your configuration should be simple enough, something like:</span></span>

    node $id="1" hadb01
      attributes standby="off"
    node $id="2" hadb02
      attributes standby="off"

1. <span data-ttu-id="9cbb3-233">Controllare la configurazione eseguendo `sudo crm configure show`.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-233">Check the configuration by running `sudo crm configure show`.</span></span>
2. <span data-ttu-id="9cbb3-234">Quindi creare un file (ad esempio `/tmp/cluster.conf`) con le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-234">Then create a file (like `/tmp/cluster.conf`) with the following resources:</span></span>

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

3. <span data-ttu-id="9cbb3-235">Caricare il file nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-235">Load the file into the configuration.</span></span> <span data-ttu-id="9cbb3-236">È sufficiente eseguire questa operazione in un solo nodo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-236">You only need to do this in one node.</span></span>

        sudo crm configure
          load update /tmp/cluster.conf
          commit
          exit

4. <span data-ttu-id="9cbb3-237">Controllare che Pacemaker si avvii al momento giusto in entrambi i nodi:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-237">Make sure that Pacemaker starts at boot in both nodes:</span></span>

        sudo update-rc.d pacemaker defaults

5. <span data-ttu-id="9cbb3-238">Mediante `sudo crm_mon –L` verificare che uno dei nodi sia diventato il master del cluster, in cui sono eseguite tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-238">By using `sudo crm_mon –L`, verify that one of your nodes has become the master for the cluster and is running all the resources.</span></span> <span data-ttu-id="9cbb3-239">È possibile usare mount e ps per verificare che le risorse siano in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-239">You can use mount and ps to check that the resources are running.</span></span>

<span data-ttu-id="9cbb3-240">La schermata seguente mostra `crm_mon` con un nodo arrestato (uscire con CTRL+C):</span><span class="sxs-lookup"><span data-stu-id="9cbb3-240">The following screenshot shows `crm_mon` with one node stopped (exit by selecting Ctrl+C):</span></span>

![Nodo crm_mon arrestato](./media/mysql-cluster/image002.png)

<span data-ttu-id="9cbb3-242">Questa schermata mostra entrambi i nodi, uno master e uno slave:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-242">This screenshot shows both nodes, one master and one slave:</span></span>

![Master/slave operativo crm_mon](./media/mysql-cluster/image003.png)

## <a name="testing"></a><span data-ttu-id="9cbb3-244">Test</span><span class="sxs-lookup"><span data-stu-id="9cbb3-244">Testing</span></span>
<span data-ttu-id="9cbb3-245">Ora è possibile eseguire una simulazione del failover automatico.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-245">You're ready for an automatic failover simulation.</span></span> <span data-ttu-id="9cbb3-246">È possibile procedere in due modi: con un soft mount e con un hard mount.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-246">There are two ways to do this: soft and hard.</span></span>

<span data-ttu-id="9cbb3-247">Il metodo soft mount prevede l'uso della funzione di arresto del cluster: ``crm_standby -U `uname -n` -v on``.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-247">The soft way uses the cluster's shutdown function: ``crm_standby -U `uname -n` -v on``.</span></span> <span data-ttu-id="9cbb3-248">Se la si usa sul master, subentra lo slave.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-248">If you use this on the master, the slave takes over.</span></span> <span data-ttu-id="9cbb3-249">Ricordare di disattivarla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-249">Remember to set this back to off.</span></span> <span data-ttu-id="9cbb3-250">In caso contrario, crm_mon mostrerà un solo nodo in standby.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-250">If you don't, crm_mon will show one node on standby.</span></span>

<span data-ttu-id="9cbb3-251">Il metodo "forte" è arrestare la VM primaria (hadb01) mediante il portalr o cambiare il runlevel sulla VM (ovvero halt, shutdown).</span><span class="sxs-lookup"><span data-stu-id="9cbb3-251">The hard way is shutting down the primary VM (hadb01) via the portal or by changing the runlevel on the VM (that is, halt, shutdown).</span></span> <span data-ttu-id="9cbb3-252">Questo aiuta Corosync e Pacemaker segnalando che il master si sta arrestando.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-252">This helps Corosync and Pacemaker by signaling that the master's going down.</span></span> <span data-ttu-id="9cbb3-253">È possibile testare questa funzionalità (utile per le finestre di manutenzione) ma anche forzare lo scenario bloccando la VM.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-253">You can test this (useful for maintenance windows), but you can also force the scenario by freezing the VM.</span></span>

## <a name="stonith"></a><span data-ttu-id="9cbb3-254">STONITH</span><span class="sxs-lookup"><span data-stu-id="9cbb3-254">STONITH</span></span>
<span data-ttu-id="9cbb3-255">Dovrebbe risultare possibile causare la chiusura di una macchina virtuale tramite l'interfaccia della riga di comando di Azure per Linux anziché eseguire uno script STONITH che controlla un dispositivo fisico.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-255">It should be possible to issue a VM shutdown via the Azure CLI in lieu of a STONITH script that controls a physical device.</span></span> <span data-ttu-id="9cbb3-256">È possibile usare `/usr/lib/stonith/plugins/external/ssh` come base e abilitare STONITH nella configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-256">You can use `/usr/lib/stonith/plugins/external/ssh` as a base and enable STONITH in the cluster's configuration.</span></span> <span data-ttu-id="9cbb3-257">L'interfaccia della riga di comando di Azure deve essere installata a livello globale e le impostazioni e il profilo di pubblicazione devono essere caricati per l'utente del cluster.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-257">Azure CLI should be globally installed, and the publish settings and profile should be loaded for the cluster's user.</span></span>

<span data-ttu-id="9cbb3-258">Esempi di codice per la risorsa sono disponibili in [GitHub](https://github.com/bureado/aztonith).</span><span class="sxs-lookup"><span data-stu-id="9cbb3-258">Sample code for the resource is available on [GitHub](https://github.com/bureado/aztonith).</span></span> <span data-ttu-id="9cbb3-259">Modificare la configurazione del cluster aggiungendo il codice seguente a `sudo crm configure`:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-259">Change the cluster's configuration by adding the following to `sudo crm configure`:</span></span>

    primitive st-azure stonith:external/azure \
      params hostlist="hadb01 hadb02" \
      clone fencing st-azure \
      property stonith-enabled=true \
      commit

> [!NOTE]
> <span data-ttu-id="9cbb3-260">Lo script non esegue controlli up/down.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-260">The script doesn't perform up/down checks.</span></span> <span data-ttu-id="9cbb3-261">La risorsa SSH originale aveva 15 verifiche ping ma il tempo di ripristino per una macchina virtuale di Azure può variare maggiormente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-261">The original SSH resource had 15 ping checks, but recovery time for an Azure VM might be more variable.</span></span>

## <a name="limitations"></a><span data-ttu-id="9cbb3-262">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="9cbb3-262">Limitations</span></span>
<span data-ttu-id="9cbb3-263">Si applicano le limitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-263">The following limitations apply:</span></span>

* <span data-ttu-id="9cbb3-264">Lo script della risorsa DRBD linbit che gestisce DRBD come risorsa in Pacemaker usa `drbdadm down` per chiudere un nodo, anche se il nodo sta passando in modalità standby.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-264">The linbit DRBD resource script that manages DRBD as a resource in Pacemaker uses `drbdadm down` when shutting down a node, even if the node is just going on standby.</span></span> <span data-ttu-id="9cbb3-265">Questa situazione non è ideale perché lo slave non sincronizza la risorsa DRBD mentre il master riceve le scritture.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-265">This is not ideal because the slave will not be synchronizing the DRBD resource while the master gets writes.</span></span> <span data-ttu-id="9cbb3-266">Se l'arresto del master non avviene con grazia, lo slave può sostituire uno stato del file system meno recente.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-266">If the master does not fail graciously, the slave can take over an older file system state.</span></span> <span data-ttu-id="9cbb3-267">Per questo problema sono possibili due soluzioni:</span><span class="sxs-lookup"><span data-stu-id="9cbb3-267">There are two potential ways of solving this:</span></span>
  * <span data-ttu-id="9cbb3-268">Applicare un `drbdadm up r0` in tutti i nodi del cluster tramite un watchdog locale (non appartenente al cluster) oppure</span><span class="sxs-lookup"><span data-stu-id="9cbb3-268">Enforcing a `drbdadm up r0` in all cluster nodes via a local (not clusterized) watchdog</span></span>
  * <span data-ttu-id="9cbb3-269">Modificare lo script DRBD linbit per fare in modo che `down` non venga chiamato in `/usr/lib/ocf/resource.d/linbit/drbd`</span><span class="sxs-lookup"><span data-stu-id="9cbb3-269">Editing the linbit DRBD script, making sure that `down` is not called in `/usr/lib/ocf/resource.d/linbit/drbd`</span></span>
* <span data-ttu-id="9cbb3-270">Il bilanciamento del carico richiede almeno cinque secondi per rispondere, quindi le applicazioni devono essere compatibili con i cluster ed essere più tolleranti del timeout.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-270">The load balancer needs at least five seconds to respond, so applications should be cluster-aware and be more tolerant of timeout.</span></span> <span data-ttu-id="9cbb3-271">Possono essere utili anche altre architetture, quali le code in-app e i middleware di query.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-271">Other architectures, like in-app queues and query middlewares, can also help.</span></span>
* <span data-ttu-id="9cbb3-272">L'ottimizzazione di MySQL è necessaria per assicurare che la scrittura venga effettuata con la velocità adeguata e che le cache siano scaricate nel disco il più frequentemente possibile per ridurre al minimo le perdite di memoria.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-272">MySQL tuning is necessary to ensure that writing is done at a manageable pace and caches are flushed to disk as frequently as possible to minimize memory loss.</span></span>
* <span data-ttu-id="9cbb3-273">Le prestazioni delle operazioni di scrittura dipendono dall'interconnessione delle VM nel commutatore virtuale, in quanto questo è il meccanismo utilizzato da DRBD per replicare il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9cbb3-273">Write performance is dependent in VM interconnect in the virtual switch because this is the mechanism used by DRBD to replicate the device.</span></span>
