---
title: aaaConfigure MPIO nell'host StorSimple Linux | Documenti Microsoft
description: Configurare MPIO nell'host di Linux tooa StorSimple connessi che eseguono 6.6 CentOS
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: tysonn
ms.assetid: ca289eed-12b7-4e2e-9117-adf7e2034f2f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: alkohli
ms.openlocfilehash: d9f7e02903243494c909313fb2c33ac690764274
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="9986a-103">Configurare MPIO in un host di StorSimple che esegue CentOS</span><span class="sxs-lookup"><span data-stu-id="9986a-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="9986a-104">Questo articolo spiega hello passaggi necessari tooconfigure Multipath i/o (MPIO) sul server host Centos 6.6.</span><span class="sxs-lookup"><span data-stu-id="9986a-104">This article explains hello steps required tooconfigure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="9986a-105">server host Hello è dispositivo Microsoft Azure StorSimple tooyour connessi per la disponibilità elevata tramite gli iniziatori iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-105">hello host server is connected tooyour Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="9986a-106">Vengono descritti in dettaglio hello l'individuazione automatica dei dispositivi a percorsi multipli e installazione specifiche di hello solo per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-106">It describes in detail hello automatic discovery of multipath devices and hello specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="9986a-107">Questa procedura è applicabile tooall i modelli di hello di dispositivi della serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="9986a-107">This procedure is applicable tooall hello models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="9986a-108">Questa procedura non può essere usata per un dispositivo virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="9986a-109">Per ulteriori informazioni, vedere come tooconfigure ospitano server per il dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="9986a-109">For more information, see how tooconfigure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="9986a-110">Informazioni sui percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-110">About multipathing</span></span>
<span data-ttu-id="9986a-111">Hello percorsi multipli consente tooconfigure più percorsi i/o tra un server host e un dispositivo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="9986a-111">hello multipathing feature allows you tooconfigure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="9986a-112">I percorsi I/O sono connessioni SAN fisiche che possono includere cavi, switch, interfacce di rete e controller separati.</span><span class="sxs-lookup"><span data-stu-id="9986a-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="9986a-113">Percorsi multipli aggrega i percorsi i/o di hello, tooconfigure un nuovo dispositivo associato a tutti i percorsi di hello aggregato.</span><span class="sxs-lookup"><span data-stu-id="9986a-113">Multipathing aggregates hello I/O paths, tooconfigure a new device that is associated with all of hello aggregated paths.</span></span>

<span data-ttu-id="9986a-114">scopo di Hello di percorsi multipli è duplice:</span><span class="sxs-lookup"><span data-stu-id="9986a-114">hello purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="9986a-115">**Disponibilità elevata**: fornisce un percorso alternativo se qualsiasi elemento del percorso dei / o hello (ad esempio un cavo, switch, l'interfaccia di rete o controller) ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9986a-115">**High availability**: It provides an alternate path if any element of hello I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="9986a-116">**Il bilanciamento del carico**: a seconda della configurazione di hello del dispositivo di archiviazione, è possibile migliorare le prestazioni di hello rilevando carichi nei percorsi di hello i/o e tali carichi il ribilanciamento in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="9986a-116">**Load balancing**: Depending on hello configuration of your storage device, it can improve hello performance by detecting loads on hello I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="9986a-117">Informazioni sui componenti dei percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-117">About multipathing components</span></span>
<span data-ttu-id="9986a-118">I percorsi multipli in Linux sono costituiti da componenti kernel e spazio utente come elencato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9986a-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="9986a-119">**Kernel**: il componente principale di hello è hello *dispositivo mapper* che reindirizza i/o e supporta il failover per i percorsi e i gruppi di percorso.</span><span class="sxs-lookup"><span data-stu-id="9986a-119">**Kernel**: hello main component is hello *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="9986a-120">**Spazio utente**: si tratta di *multipath strumenti* che gestiscono i dispositivi con percorsi multipli, indicando modulo a percorsi multipli di hello dispositivo mapper quali toodo.</span><span class="sxs-lookup"><span data-stu-id="9986a-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing hello device-mapper multipath module what toodo.</span></span> <span data-ttu-id="9986a-121">strumenti di Hello è costituito da:</span><span class="sxs-lookup"><span data-stu-id="9986a-121">hello tools consist of:</span></span>
   
   * <span data-ttu-id="9986a-122">**Multipath**: elenca e configura i dispositivi a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="9986a-123">**Multipathd**: daemon che esegue i percorsi di hello multipath e monitoraggi.</span><span class="sxs-lookup"><span data-stu-id="9986a-123">**Multipathd**: daemon that executes multipath and monitors hello paths.</span></span>
   * <span data-ttu-id="9986a-124">**Nome di Devmap**: offre un significativo tooudev nome del dispositivo per devmaps.</span><span class="sxs-lookup"><span data-stu-id="9986a-124">**Devmap-name**: provides a meaningful device-name tooudev for devmaps.</span></span>
   * <span data-ttu-id="9986a-125">**Kpartx**: devmaps lineare toodevice partizioni toomake multipath mappe partizionabile viene eseguito il mapping.</span><span class="sxs-lookup"><span data-stu-id="9986a-125">**Kpartx**: maps linear devmaps toodevice partitions toomake multipath maps partitionable.</span></span>
   * <span data-ttu-id="9986a-126">**Multipath.conf**: file di configurazione per percorsi multipli daemon che è usato toooverwrite hello configurazione incorporati tabella.</span><span class="sxs-lookup"><span data-stu-id="9986a-126">**Multipath.conf**: configuration file for multipath daemon that is used toooverwrite hello built-in configuration table.</span></span>

### <a name="about-hello-multipathconf-configuration-file"></a><span data-ttu-id="9986a-127">Sul file di configurazione multipath.conf hello</span><span class="sxs-lookup"><span data-stu-id="9986a-127">About hello multipath.conf configuration file</span></span>
<span data-ttu-id="9986a-128">file di configurazione Hello `/etc/multipath.conf` vengono apportate diverse hello Multipath funzionalità configurabile dall'utente.</span><span class="sxs-lookup"><span data-stu-id="9986a-128">hello configuration file `/etc/multipath.conf` makes many of hello multipathing features user-configurable.</span></span> <span data-ttu-id="9986a-129">Hello `multipath` comando e hello daemon kernel `multipathd` utilizzare informazioni contenute in questo file.</span><span class="sxs-lookup"><span data-stu-id="9986a-129">hello `multipath` command and hello kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="9986a-130">file Hello viene consultato solo durante la configurazione di hello di dispositivi a percorsi multipli hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-130">hello file is consulted only during hello configuration of hello multipath devices.</span></span> <span data-ttu-id="9986a-131">Assicurarsi che tutte le modifiche vengono apportate prima di eseguire hello `multipath` comando.</span><span class="sxs-lookup"><span data-stu-id="9986a-131">Make sure that all changes are made before you run hello `multipath` command.</span></span> <span data-ttu-id="9986a-132">Se si modifica il file hello in seguito, sarà anche necessario toostop e avviare multipathd nuovamente per effetto di tootake modifiche hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-132">If you modify hello file afterwards, you will need toostop and start multipathd again for hello changes tootake effect.</span></span>

<span data-ttu-id="9986a-133">Hello multipath.conf include cinque sezioni:</span><span class="sxs-lookup"><span data-stu-id="9986a-133">hello multipath.conf has five sections:</span></span>

- <span data-ttu-id="9986a-134">**System level defaults***(defaults)*: è possibile ignorare i valori predefiniti a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="9986a-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="9986a-135">**Disattivato dispositivi** *(nera)*: È possibile specificare hello elenco di dispositivi che non devono essere controllati da BizTalk mapper di dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9986a-135">**Blacklisted devices** *(blacklist)*: You can specify hello list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="9986a-136">**Disattivare le eccezioni** *(blacklist_exceptions)*: È possibile identificare considerati i dispositivi a percorsi multipli, anche se è elencato nella blacklist hello toobe di dispositivi specifici.</span><span class="sxs-lookup"><span data-stu-id="9986a-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices toobe treated as multipath devices even if listed in hello blacklist.</span></span>
- <span data-ttu-id="9986a-137">**Impostazioni specifiche di controller di archiviazione** *(dispositivi)*: È possibile specificare le impostazioni di configurazione che verrà applicato toodevices che le informazioni di prodotto e fornitore.</span><span class="sxs-lookup"><span data-stu-id="9986a-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied toodevices that have Vendor and Product information.</span></span>
- <span data-ttu-id="9986a-138">**Impostazioni specifiche di dispositivo** *(multipaths)*: È possibile utilizzare le impostazioni di configurazione hello toofine ottimizzare questa sezione per singoli LUN.</span><span class="sxs-lookup"><span data-stu-id="9986a-138">**Device specific settings** *(multipaths)*: You can use this section toofine-tune hello configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-toolinux-host"></a><span data-ttu-id="9986a-139">Configurare percorsi multipli sull'host connesso tooLinux StorSimple</span><span class="sxs-lookup"><span data-stu-id="9986a-139">Configure multipathing on StorSimple connected tooLinux host</span></span>
<span data-ttu-id="9986a-140">Un host di Linux tooa dispositivo connesso StorSimple può essere configurato per la disponibilità elevata e bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="9986a-140">A StorSimple device connected tooa Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="9986a-141">Ad esempio, se host Linux hello ha due interfacce toohello connesso SAN e hello dispositivo ha due interfacce connessi toohello SAN ad presenti queste interfacce hello stessa subnet, quindi esisterà 4 percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9986a-141">For example, if hello Linux host has two interfaces connected toohello SAN and hello device has two interfaces connected toohello SAN such that these interfaces are on hello same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="9986a-142">Tuttavia, se ogni interfaccia di dati nell'interfaccia di dispositivi e host hello in un'altra subnet IP (e non instradabili), quindi solo 2 i percorsi saranno disponibili.</span><span class="sxs-lookup"><span data-stu-id="9986a-142">However, if each DATA interface on hello device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="9986a-143">È possibile configurare percorsi multipli tooautomatically individuare tutti i percorsi disponibili hello, scegliere un algoritmo di bilanciamento del carico per tali percorsi, applicare impostazioni di configurazione specifiche per i volumi StorSimple-only, abilitare e verificare i percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-143">You can configure multipathing tooautomatically discover all hello available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="9986a-144">Hello procedura riportata di seguito viene descritto come percorsi multipli tooconfigure quando un dispositivo StorSimple con due interfacce di rete viene connessa tooa host con due interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="9986a-144">hello following procedure describes how tooconfigure multipathing when a StorSimple device with two network interfaces is connected tooa host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9986a-145">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9986a-145">Prerequisites</span></span>
<span data-ttu-id="9986a-146">Questa sezione descrive i prerequisiti di configurazione hello per server CentOS e il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-146">This section details hello configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="9986a-147">Sull'host CentOS</span><span class="sxs-lookup"><span data-stu-id="9986a-147">On CentOS host</span></span>
1. <span data-ttu-id="9986a-148">Assicurarsi che l'host CentOS abbia due interfacce di rete abilitate.</span><span class="sxs-lookup"><span data-stu-id="9986a-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="9986a-149">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="9986a-150">Hello riportato di seguito output di hello quando due interfacce di rete (`eth0` e `eth1`) sono presenti nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-150">hello following example shows hello output when two network interfaces (`eth0` and `eth1`) are present on hello host.</span></span>
   
        [root@centosSS ~]# ifconfig
        eth0  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:41  
          inet addr:10.126.162.65  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3341/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3341/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
         RX packets:36536 errors:0 dropped:0 overruns:0 frame:0
          TX packets:6312 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:13994127 (13.3 MiB)  TX bytes:645654 (630.5 KiB)
   
        eth1  Link encap:Ethernet  HWaddr 00:15:5D:A2:33:42  
          inet addr:10.126.162.66  Bcast:10.126.163.255  Mask:255.255.252.0
          inet6 addr: 2001:4898:4010:3012:215:5dff:fea2:3342/64 Scope:Global
          inet6 addr: fe80::215:5dff:fea2:3342/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:25962 errors:0 dropped:0 overruns:0 frame:0
          TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:2597350 (2.4 MiB)  TX bytes:754 (754.0 b)
   
        loLink encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:12 errors:0 dropped:0 overruns:0 frame:0
          TX packets:12 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:720 (720.0 b)  TX bytes:720 (720.0 b)
2. <span data-ttu-id="9986a-151">Installare *iSCSI-initiator-utils* sul server CentOS.</span><span class="sxs-lookup"><span data-stu-id="9986a-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="9986a-152">Eseguire i seguenti passaggi tooinstall hello *utilità di iniziatore iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="9986a-152">Perform hello following steps tooinstall *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="9986a-153">Accedere come `root` all'host CentOS.</span><span class="sxs-lookup"><span data-stu-id="9986a-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="9986a-154">Installare hello *utilità di iniziatore iSCSI*.</span><span class="sxs-lookup"><span data-stu-id="9986a-154">Install hello *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="9986a-155">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="9986a-156">Dopo aver hello *utilità di iniziatore iSCSI* è stato installato, avviare il servizio iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-156">After hello *iSCSI-Initiator-utils* is successfully installed, start hello iSCSI service.</span></span> <span data-ttu-id="9986a-157">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="9986a-158">In alcuni casi, `iscsid` possono avviare e non è effettivamente hello `--force` opzione potrebbe essere necessaria.</span><span class="sxs-lookup"><span data-stu-id="9986a-158">On occasions, `iscsid` may not actually start and hello `--force` option may be needed</span></span>
   4. <span data-ttu-id="9986a-159">che l'iniziatore iSCSI è abilitato durante la fase di avvio, utilizzare hello tooensure `chkconfig` servizio hello tooenable di comando.</span><span class="sxs-lookup"><span data-stu-id="9986a-159">tooensure that your iSCSI initiator is enabled during boot time, use hello `chkconfig` command tooenable hello service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="9986a-160">tooverify che è stato corretto del programma di installazione, eseguire il comando di hello:</span><span class="sxs-lookup"><span data-stu-id="9986a-160">tooverify that that it was properly setup, run hello command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="9986a-161">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="9986a-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="9986a-162">Da hello esempio precedente, si noterà che l'ambiente iSCSI verrà eseguito in fase di avvio su livelli fase 2, 3, 4 e 5.</span><span class="sxs-lookup"><span data-stu-id="9986a-162">From hello above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="9986a-163">Installare *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="9986a-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="9986a-164">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="9986a-165">verrà avviata l'installazione di Hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-165">hello installation will start.</span></span> <span data-ttu-id="9986a-166">Tipo **Y** toocontinue alla richiesta di conferma.</span><span class="sxs-lookup"><span data-stu-id="9986a-166">Type **Y** toocontinue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="9986a-167">Sul dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="9986a-167">On StorSimple device</span></span>
<span data-ttu-id="9986a-168">Il dispositivo StorSimple deve avere:</span><span class="sxs-lookup"><span data-stu-id="9986a-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="9986a-169">Almeno due interfacce abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="9986a-170">tooverify che due interfacce siano abilitate per iSCSI sul dispositivo StorSimple, eseguire hello nel portale di Azure classico per il dispositivo StorSimple hello come segue:</span><span class="sxs-lookup"><span data-stu-id="9986a-170">tooverify that two interfaces are iSCSI-enabled on your StorSimple device, perform hello following steps in hello Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="9986a-171">Accedere al portale classico di hello per il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-171">Log into hello classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="9986a-172">Selezionare il servizio StorSimple Manager, fare clic su **dispositivi** e scegliere il dispositivo StorSimple specifico di hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-172">Select your StorSimple Manager service, click **Devices** and choose hello specific StorSimple device.</span></span> <span data-ttu-id="9986a-173">Fare clic su **configura** e verificare le impostazioni dell'interfaccia di rete hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-173">Click **Configure** and verify hello network interface settings.</span></span> <span data-ttu-id="9986a-174">Di seguito è riportata una schermata con due interfacce di rete abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="9986a-175">Entrambe le interfacce di rete da 10 GbE, DATA 2 e DATA 3, sono abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configurazione DATA 2 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configurazione DATA 3 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="9986a-178">In hello **configura** pagina</span><span class="sxs-lookup"><span data-stu-id="9986a-178">In hello **Configure** page</span></span>
     
     1. <span data-ttu-id="9986a-179">Assicurarsi che entrambe le interfacce di rete siano abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="9986a-180">Hello **abilitato per iSCSI** campo deve essere impostato troppo**Sì**.</span><span class="sxs-lookup"><span data-stu-id="9986a-180">hello **iSCSI enabled** field should be set too**Yes**.</span></span>
     2. <span data-ttu-id="9986a-181">Verificare che le interfacce di rete hello abbiano hello stessa velocità, entrambi devono essere da 1 GbE o 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="9986a-181">Ensure that hello network interfaces have hello same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="9986a-182">Si noti indirizzi IPv4 hello delle interfacce abilitate per iSCSI hello e salvare per un utilizzo successivo nell'host di hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-182">Note hello IPv4 addresses of hello iSCSI-enabled interfaces and save for later use on hello host.</span></span>
* <span data-ttu-id="9986a-183">interfacce iSCSI Hello nel dispositivo StorSimple devono essere raggiungibile dal server CentOS hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-183">hello iSCSI interfaces on your StorSimple device should be reachable from hello CentOS server.</span></span>
      <span data-ttu-id="9986a-184">tooverify, gli indirizzi IP di hello tooprovide le interfacce di rete abilitate per iSCSI StorSimple è necessario nel server host.</span><span class="sxs-lookup"><span data-stu-id="9986a-184">tooverify this, you need tooprovide hello IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="9986a-185">i comandi usati Hello e hello output corrispondente con DATA2 (10.126.162.25) e DATA3 (10.126.162.26) è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9986a-185">hello commands used and hello corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="9986a-186">Configurazione hardware</span><span class="sxs-lookup"><span data-stu-id="9986a-186">Hardware configuration</span></span>
<span data-ttu-id="9986a-187">È consigliabile connettersi hello due iSCSI interfacce di rete su percorsi diversi per la ridondanza.</span><span class="sxs-lookup"><span data-stu-id="9986a-187">We recommend that you connect hello two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="9986a-188">Hello seguente figura configurazione hardware consigliata hello per la disponibilità elevata e bilanciamento del carico percorsi multipli per il server di CentOS e un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-188">hello figure below shows hello recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configurazione hardware di MPIO per StorSimple tooLinux host](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="9986a-190">Come illustrato nella figura precedente hello:</span><span class="sxs-lookup"><span data-stu-id="9986a-190">As shown in hello preceding figure:</span></span>

* <span data-ttu-id="9986a-191">Il dispositivo StorSimple ha una configurazione attiva-passiva con due controller.</span><span class="sxs-lookup"><span data-stu-id="9986a-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="9986a-192">Due commutatori di rete SAN sono connessi tooyour controller del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9986a-192">Two SAN switches are connected tooyour device controllers.</span></span>
* <span data-ttu-id="9986a-193">Due iniziatori iSCSI sono abilitati nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="9986a-194">Due interfacce di rete sono abilitate sull'host CentOS.</span><span class="sxs-lookup"><span data-stu-id="9986a-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="9986a-195">Se le interfacce di hello host e i dati siano instradabili, Hello sopra configurazione genererà 4 percorsi separati tra l'host del dispositivo e hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-195">hello above configuration will yield 4 separate paths between your device and hello host if hello host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="9986a-196">È consigliabile non combinare interfacce di rete da 1 GbE e da 10 GbE per i percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="9986a-197">Quando si usano due interfacce di rete, entrambe le interfacce hello devono essere hello stesso tipo.</span><span class="sxs-lookup"><span data-stu-id="9986a-197">When using two network interfaces, both hello interfaces should be hello identical type.</span></span>
> * <span data-ttu-id="9986a-198">Sul dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 sono interfacce da 1 GbE mentre DATA2 e DATA3 sono interfacce di rete da 10 GbE.|</span><span class="sxs-lookup"><span data-stu-id="9986a-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="9986a-199">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="9986a-199">Configuration steps</span></span>
<span data-ttu-id="9986a-200">passaggi di configurazione Hello per percorsi multipli implicano i percorsi disponibili per l'individuazione automatica, specificare hello bilanciamento del carico algoritmo toouse, consentendo a percorsi multipli e infine verifica configurazione hello hello di configurazione.</span><span class="sxs-lookup"><span data-stu-id="9986a-200">hello configuration steps for multipathing involve configuring hello available paths for automatic discovery, specifying hello load-balancing algorithm toouse, enabling multipathing and finally verifying hello configuration.</span></span> <span data-ttu-id="9986a-201">Ognuno di questi passaggi è illustrato in dettaglio nelle sezioni che seguono hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-201">Each of these steps is discussed in detail in hello following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="9986a-202">Passaggio 1: Configurare percorsi multipli per il rilevamento automatico</span><span class="sxs-lookup"><span data-stu-id="9986a-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="9986a-203">i dispositivi supportati multipath Hello possono essere individuati automaticamente e configurati.</span><span class="sxs-lookup"><span data-stu-id="9986a-203">hello multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="9986a-204">Inizializzare il file `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="9986a-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="9986a-205">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="9986a-206">Hello sopra comando creerà un `sample/etc/multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="9986a-206">hello above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="9986a-207">Avviare il servizio a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-207">Start multipath service.</span></span> <span data-ttu-id="9986a-208">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="9986a-209">Verrà visualizzato hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="9986a-209">You will see hello following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="9986a-210">Abilitare il rilevamento automatico dei percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="9986a-211">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="9986a-212">Verrà modificato hello sezione Impostazioni predefinite del `multipath.conf` come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9986a-212">This will modify hello defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="9986a-213">Passaggio 2: Configurare i percorsi multipli per volumi StorSimple</span><span class="sxs-lookup"><span data-stu-id="9986a-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="9986a-214">Per impostazione predefinita, tutti i dispositivi sono elencati nel file multipath.conf hello neri e verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="9986a-214">By default, all devices are black listed in hello multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="9986a-215">È necessario toocreate blacklist eccezioni tooallow Multipath per volumi da dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-215">You will need toocreate blacklist exceptions tooallow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="9986a-216">Modifica hello `/etc/mulitpath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="9986a-216">Edit hello `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="9986a-217">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="9986a-218">Nella sezione hello blacklist_exceptions nel file multipath.conf hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-218">Locate hello blacklist_exceptions section in hello multipath.conf file.</span></span> <span data-ttu-id="9986a-219">Il dispositivo StorSimple deve toobe elencato come eccezione blacklist in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9986a-219">Your StorSimple device needs toobe listed as a blacklist exception in this section.</span></span> <span data-ttu-id="9986a-220">È possibile rimuovere il commento rilevanti righe toomodify questo file, come illustrato di seguito (utilizzare solo hello modello specifico di dispositivo hello in uso):</span><span class="sxs-lookup"><span data-stu-id="9986a-220">You can uncomment relevant lines in this file toomodify it as shown below (use only hello specific model of hello device you are using):</span></span>
   
        blacklist_exceptions {
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8100*"
            }
            device {
                       vendor  "MSFT"
                       product "STORSIMPLE 8600*"
            }
           }

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="9986a-221">Passaggio 3: Configurare percorsi multipli round robin</span><span class="sxs-lookup"><span data-stu-id="9986a-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="9986a-222">Questo algoritmo di bilanciamento del carico utilizza tutti i controller attivo di hello toohello multipaths disponibile in modo bilanciato e round robin.</span><span class="sxs-lookup"><span data-stu-id="9986a-222">This load-balancing algorithm uses all hello available multipaths toohello active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="9986a-223">Modifica hello `/etc/multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="9986a-223">Edit hello `/etc/multipath.conf` file.</span></span> <span data-ttu-id="9986a-224">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="9986a-225">In hello `defaults` sezione, hello set `path_grouping_policy` troppo`multibus`.</span><span class="sxs-lookup"><span data-stu-id="9986a-225">Under hello `defaults` section, set hello `path_grouping_policy` too`multibus`.</span></span> <span data-ttu-id="9986a-226">Hello `path_grouping_policy` multipaths toounspecified hello predefinito percorso raggruppamento criteri tooapply specifica.</span><span class="sxs-lookup"><span data-stu-id="9986a-226">hello `path_grouping_policy` specifies hello default path grouping policy tooapply toounspecified multipaths.</span></span> <span data-ttu-id="9986a-227">sezione Impostazioni predefinite di Hello apparirà come illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9986a-227">hello defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="9986a-228">valori più comuni di Hello `path_grouping_policy` includono:</span><span class="sxs-lookup"><span data-stu-id="9986a-228">hello most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="9986a-229">failover = 1 percorso per ogni gruppo prioritario</span><span class="sxs-lookup"><span data-stu-id="9986a-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="9986a-230">multibus = tutti i percorsi validi in 1 gruppo prioritario</span><span class="sxs-lookup"><span data-stu-id="9986a-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="9986a-231">Passaggio 4: Abilitare i percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="9986a-232">Riavviare hello `multipathd` daemon.</span><span class="sxs-lookup"><span data-stu-id="9986a-232">Restart hello `multipathd` daemon.</span></span> <span data-ttu-id="9986a-233">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="9986a-234">output di Hello saranno come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9986a-234">hello output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="9986a-235">Passaggio 5: Verificare i percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="9986a-236">Assicurarsi innanzitutto che viene stabilita la connessione iSCSI con dispositivo StorSimple hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9986a-236">First make sure that iSCSI connection is established with hello StorSimple device as follows:</span></span>
   
   <span data-ttu-id="9986a-237">a.</span><span class="sxs-lookup"><span data-stu-id="9986a-237">a.</span></span> <span data-ttu-id="9986a-238">Trovare il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-238">Discover your StorSimple device.</span></span> <span data-ttu-id="9986a-239">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on hello device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="9986a-240">output di Hello quando l'indirizzo IP DATA0 è 10.126.162.25 e porta 3260 viene aperta nel dispositivo StorSimple hello per il traffico in uscita iSCSI è come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9986a-240">hello output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on hello StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="9986a-241">Hello Copia nome IQN del dispositivo StorSimple `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, da hello output precedente.</span><span class="sxs-lookup"><span data-stu-id="9986a-241">Copy hello IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from hello preceding output.</span></span>

   <span data-ttu-id="9986a-242">b.</span><span class="sxs-lookup"><span data-stu-id="9986a-242">b.</span></span> <span data-ttu-id="9986a-243">Collegare il dispositivo di toohello tramite iSCSI di destinazione.</span><span class="sxs-lookup"><span data-stu-id="9986a-243">Connect toohello device using target IQN.</span></span> <span data-ttu-id="9986a-244">dispositivo StorSimple Hello è una destinazione iSCSI di hello qui.</span><span class="sxs-lookup"><span data-stu-id="9986a-244">hello StorSimple device is hello iSCSI target here.</span></span> <span data-ttu-id="9986a-245">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="9986a-246">Hello esempio seguente viene illustrato l'output con una nome qualificato iSCSI di destinazione di `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="9986a-246">hello following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="9986a-247">output di Hello indica che sono stati connessi toohello due interfacce di rete abilitate per iSCSI sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9986a-247">hello output indicates that you have successfully connected toohello two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login too[iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login too[iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="9986a-248">Se viene visualizzato un solo host interfaccia e i due percorsi, è necessario tooenable entrambe le interfacce hello nell'host per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="9986a-248">If you see only one host interface and two paths here, then you need tooenable both hello interfaces on host for iSCSI.</span></span> <span data-ttu-id="9986a-249">È possibile seguire hello [dettagliate nella documentazione di Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="9986a-249">You can follow hello [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="9986a-250">Server CentOS toohello esposto dal dispositivo StorSimple hello è un volume.</span><span class="sxs-lookup"><span data-stu-id="9986a-250">A volume is exposed toohello CentOS server from hello StorSimple device.</span></span> <span data-ttu-id="9986a-251">Per ulteriori informazioni, vedere [passaggio 6: creare un volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) tramite hello portale di Azure classico nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via hello Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="9986a-252">Verificare i percorsi disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-252">Verify hello available paths.</span></span> <span data-ttu-id="9986a-253">Digitare:</span><span class="sxs-lookup"><span data-stu-id="9986a-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="9986a-254">Hello di esempio seguente viene illustrato l'output di hello per le due interfacce di rete su un'interfaccia di rete StorSimple dispositivo connesso tooa singolo host con due percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9986a-254">hello following example shows hello output for two network interfaces on a StorSimple device connected tooa single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        hello following example shows hello output for two network interfaces on a StorSimple device connected tootwo host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After hello paths are configured, refer toohello specific instructions on your host operating system (Centos 6.6) toomount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="9986a-255">Risoluzione dei problemi relativi ai percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="9986a-256">Questa sezione contiene alcuni suggerimenti utili in caso di problemi durante la configurazione dei percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="9986a-257">D:</span><span class="sxs-lookup"><span data-stu-id="9986a-257">Q.</span></span> <span data-ttu-id="9986a-258">Non vengono visualizzati le modifiche di hello in `multipath.conf` file diventino effettive.</span><span class="sxs-lookup"><span data-stu-id="9986a-258">I do not see hello changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="9986a-259">R.</span><span class="sxs-lookup"><span data-stu-id="9986a-259">A.</span></span> <span data-ttu-id="9986a-260">Se sono state apportate toohello eventuali modifiche `multipath.conf` file, sarà necessario del servizio di toorestart hello percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="9986a-260">If you have made any changes toohello `multipath.conf` file, you will need toorestart hello multipathing service.</span></span> <span data-ttu-id="9986a-261">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9986a-261">Type hello following command:</span></span>

    service multipathd restart

<span data-ttu-id="9986a-262">D:</span><span class="sxs-lookup"><span data-stu-id="9986a-262">Q.</span></span> <span data-ttu-id="9986a-263">È stata attivata due interfacce di rete nel dispositivo StorSimple hello e due interfacce di rete sull'host hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-263">I have enabled two network interfaces on hello StorSimple device and two network interfaces on hello host.</span></span> <span data-ttu-id="9986a-264">Quando elencano i percorsi disponibili hello, viene visualizzato solo due percorsi.</span><span class="sxs-lookup"><span data-stu-id="9986a-264">When I list hello available paths, I see only two paths.</span></span> <span data-ttu-id="9986a-265">Previsto toosee quattro percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="9986a-265">I expected toosee four available paths.</span></span>

<span data-ttu-id="9986a-266">R.</span><span class="sxs-lookup"><span data-stu-id="9986a-266">A.</span></span> <span data-ttu-id="9986a-267">Assicurarsi che siano percorsi hello due su hello stessa subnet e instradabile.</span><span class="sxs-lookup"><span data-stu-id="9986a-267">Make sure that hello two paths are on hello same subnet and routable.</span></span> <span data-ttu-id="9986a-268">Se sono interfacce di rete hello su VLAN diversi e non è instradabile, verrà visualizzato solo due percorsi.</span><span class="sxs-lookup"><span data-stu-id="9986a-268">If hello network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="9986a-269">Unidirezionale tooverify equivale toomake assicurarsi che entrambe le interfacce host hello da un'interfaccia di rete nel dispositivo StorSimple hello può raggiungere.</span><span class="sxs-lookup"><span data-stu-id="9986a-269">One way tooverify this is toomake sure that you can reach both hello host interfaces from a network interface on hello StorSimple device.</span></span> <span data-ttu-id="9986a-270">È necessario troppo[contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) come questa verifica può essere eseguita solo tramite una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="9986a-270">You will need too[contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="9986a-271">D:</span><span class="sxs-lookup"><span data-stu-id="9986a-271">Q.</span></span> <span data-ttu-id="9986a-272">Nell'elenco dei percorsi disponibili non è visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="9986a-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="9986a-273">R.</span><span class="sxs-lookup"><span data-stu-id="9986a-273">A.</span></span> <span data-ttu-id="9986a-274">In genere, non possono visualizzare tutti i percorsi con percorsi multipli suggerisce un problema con il daemon di percorsi multipli hello ed è probabile che qualsiasi problema risiede nella hello `multipath.conf` file.</span><span class="sxs-lookup"><span data-stu-id="9986a-274">Typically, not seeing any multipathed paths suggests a problem with hello multipathing daemon, and it’s most likely that any problem here lies in hello `multipath.conf` file.</span></span>

<span data-ttu-id="9986a-275">Sarebbe inoltre controllare che è possibile visualizzare alcuni dischi dopo la connessione di destinazione, toohello come alcuna risposta da elenchi di percorsi multipli hello non potrebbe inoltre risultare che non includa alcun disco.</span><span class="sxs-lookup"><span data-stu-id="9986a-275">It would also be worth checking that you can actually see some disks after connecting toohello target, as no response from hello multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="9986a-276">Utilizzare hello bus SCSI hello toorescan di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9986a-276">Use hello following command toorescan hello SCSI bus:</span></span>
  
    <span data-ttu-id="9986a-277">`$ rescan-scsi-bus.sh `(parte del pacchetto sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="9986a-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="9986a-278">Digitare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9986a-278">Type hello following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="9986a-279">Or</span><span class="sxs-lookup"><span data-stu-id="9986a-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="9986a-280">Verranno restituite informazioni dettagliate sui dischi aggiunti di recente.</span><span class="sxs-lookup"><span data-stu-id="9986a-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="9986a-281">Se si tratta di un disco di StorSimple, toodetermine utilizzare hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="9986a-281">toodetermine whether it is a StorSimple disk, use hello following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="9986a-282">Verrà restituita una stringa, che determinerà se si tratta di un disco StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="9986a-283">Una causa meno probabile, ma possibile, potrebbe anche essere un PID iSCSI non aggiornato.</span><span class="sxs-lookup"><span data-stu-id="9986a-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="9986a-284">Utilizzare hello successivo comando toolog off da sessioni iSCSI hello:</span><span class="sxs-lookup"><span data-stu-id="9986a-284">Use hello following command toolog off from hello iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="9986a-285">Ripetere questo comando per tutte le interfacce di rete connessa hello in destinazione iSCSI hello, che è il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9986a-285">Repeat this command for all hello connected network interfaces on hello iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="9986a-286">Dopo aver eseguito l'accesso da tutte le sessioni iSCSI di hello, utilizzare una sessione iSCSI hello iSCSI destinazione IQN tooreestablish hello.</span><span class="sxs-lookup"><span data-stu-id="9986a-286">Once you have logged off from all hello iSCSI sessions, use hello iSCSI target IQN tooreestablish hello iSCSI session.</span></span> <span data-ttu-id="9986a-287">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9986a-287">Type hello following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="9986a-288">D:</span><span class="sxs-lookup"><span data-stu-id="9986a-288">Q.</span></span> <span data-ttu-id="9986a-289">Come è possibile verificare che il dispositivo sia incluso nell'elenco dei dispositivi consentiti?</span><span class="sxs-lookup"><span data-stu-id="9986a-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="9986a-290">R.</span><span class="sxs-lookup"><span data-stu-id="9986a-290">A.</span></span> <span data-ttu-id="9986a-291">Se il dispositivo è abilitata, tooverify utilizzare hello comando interattivo sulla risoluzione dei problemi seguente:</span><span class="sxs-lookup"><span data-stu-id="9986a-291">tooverify whether your device is whitelisted, use hello following troubleshooting interactive command:</span></span>

    multipathd –k
    multipathd> show devices
    available block devices:
    ram0 devnode blacklisted, unmonitored
    ram1 devnode blacklisted, unmonitored
    ram2 devnode blacklisted, unmonitored
    ram3 devnode blacklisted, unmonitored
    ram4 devnode blacklisted, unmonitored
    ram5 devnode blacklisted, unmonitored
    ram6 devnode blacklisted, unmonitored
    ram7 devnode blacklisted, unmonitored
    ram8 devnode blacklisted, unmonitored
    ram9 devnode blacklisted, unmonitored
    ram10 devnode blacklisted, unmonitored
    ram11 devnode blacklisted, unmonitored
    ram12 devnode blacklisted, unmonitored
    ram13 devnode blacklisted, unmonitored
    ram14 devnode blacklisted, unmonitored
    ram15 devnode blacklisted, unmonitored
    loop0 devnode blacklisted, unmonitored
    loop1 devnode blacklisted, unmonitored
    loop2 devnode blacklisted, unmonitored
    loop3 devnode blacklisted, unmonitored
    loop4 devnode blacklisted, unmonitored
    loop5 devnode blacklisted, unmonitored
    loop6 devnode blacklisted, unmonitored
    loop7 devnode blacklisted, unmonitored
    sr0 devnode blacklisted, unmonitored
    sda devnode whitelisted, monitored
    dm-0 devnode blacklisted, unmonitored
    dm-1 devnode blacklisted, unmonitored
    dm-2 devnode blacklisted, unmonitored
    sdb devnode whitelisted, monitored
    sdc devnode whitelisted, monitored
    dm-3 devnode blacklisted, unmonitored


<span data-ttu-id="9986a-292">Per ulteriori informazioni, visitare troppo[utilizzare risoluzione dei problemi di un comando interattivo per percorsi multipli](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="9986a-292">For more information, go too[use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="9986a-293">Elenco di comandi utili</span><span class="sxs-lookup"><span data-stu-id="9986a-293">List of useful commands</span></span>
| <span data-ttu-id="9986a-294">Digitare </span><span class="sxs-lookup"><span data-stu-id="9986a-294">Type</span></span> | <span data-ttu-id="9986a-295">Comando</span><span class="sxs-lookup"><span data-stu-id="9986a-295">Command</span></span> | <span data-ttu-id="9986a-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="9986a-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9986a-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="9986a-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="9986a-298">Avviare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="9986a-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="9986a-299">Arrestare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="9986a-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="9986a-300">Riavviare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="9986a-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="9986a-301">Individuare le destinazioni disponibili in hello specificato indirizzo</span><span class="sxs-lookup"><span data-stu-id="9986a-301">Discover available targets on hello specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="9986a-302">Accedere alla destinazione iSCSI toohello</span><span class="sxs-lookup"><span data-stu-id="9986a-302">Log in toohello iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="9986a-303">Disconnettersi dalla destinazione iSCSI hello</span><span class="sxs-lookup"><span data-stu-id="9986a-303">Log out from hello iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="9986a-304">Stampare il nome dell'iniziatore iSCSI</span><span class="sxs-lookup"><span data-stu-id="9986a-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="9986a-305">Controllare lo stato di hello di sessione iSCSI hello e volume individuato nell'host di hello</span><span class="sxs-lookup"><span data-stu-id="9986a-305">Check hello state of hello iSCSI session and volume discovered on hello host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="9986a-306">Mostra tutte le sessioni iSCSI hello stabilite tra host hello e il dispositivo StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="9986a-306">Shows all hello iSCSI sessions established between hello host and hello StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="9986a-307">**Percorsi multipli**</span><span class="sxs-lookup"><span data-stu-id="9986a-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="9986a-308">Avviare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="9986a-309">Arrestare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="9986a-310">Riavviare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="9986a-311">OPPURE</span><span class="sxs-lookup"><span data-stu-id="9986a-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="9986a-312">Abilitare toostart daemon a percorsi multipli in fase di avvio</span><span class="sxs-lookup"><span data-stu-id="9986a-312">Enable multipath daemon toostart at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="9986a-313">Avviare la console interattiva di hello per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="9986a-313">Start hello interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="9986a-314">Elencare le connessioni e i dispositivi a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="9986a-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="9986a-315">Creare un file mulitpath.conf di esempio in `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="9986a-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="9986a-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9986a-316">Next steps</span></span>
<span data-ttu-id="9986a-317">Come si configura MPIO nell'host di Linux, è necessario anche toohello toorefer CentoS 6.6 documenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="9986a-317">As you are configuring MPIO on Linux host, you may also need toorefer toohello following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="9986a-318">Configurazione di MPIO su CentOS</span><span class="sxs-lookup"><span data-stu-id="9986a-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="9986a-319">Guida alla formazione Linux</span><span class="sxs-lookup"><span data-stu-id="9986a-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

