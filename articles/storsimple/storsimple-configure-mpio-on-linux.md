---
title: Configurare MPIO sull'host Linux StorSimple | Microsoft Docs
description: Configurare MPIO in dispositivi StorSimple connessi all'host Linux che esegue CentOS 6.6
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
ms.openlocfilehash: add539351066f9ff94febeebfd5334773b360e8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-mpio-on-a-storsimple-host-running-centos"></a><span data-ttu-id="6986d-103">Configurare MPIO in un host di StorSimple che esegue CentOS</span><span class="sxs-lookup"><span data-stu-id="6986d-103">Configure MPIO on a StorSimple host running CentOS</span></span>
<span data-ttu-id="6986d-104">Questo articolo illustra i passaggi necessari a configurare l'I/O a percorsi multipli (MPIO) nel server host CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="6986d-104">This article explains the steps required to configure Multipathing IO (MPIO) on your Centos 6.6 host server.</span></span> <span data-ttu-id="6986d-105">Il server host è connesso al dispositivo Microsoft Azure StorSimple per la disponibilità elevata attraverso gli iniziatori iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-105">The host server is connected to your Microsoft Azure StorSimple device for high availability via iSCSI initiators.</span></span> <span data-ttu-id="6986d-106">L'articolo descrive in dettaglio il rilevamento automatico dei dispositivi con percorsi multipli e la configurazione specifica solo per i volumi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-106">It describes in detail the automatic discovery of multipath devices and the specific setup only for StorSimple volumes.</span></span>

<span data-ttu-id="6986d-107">Questa procedura è applicabile a tutti i modelli di dispositivi della serie StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="6986d-107">This procedure is applicable to all the models of StorSimple 8000 series devices.</span></span>

> [!NOTE]
> <span data-ttu-id="6986d-108">Questa procedura non può essere usata per un dispositivo virtuale StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-108">This procedure cannot be used for a StorSimple virtual device.</span></span> <span data-ttu-id="6986d-109">Per altre informazioni, vedere Come configurare i server host per il dispositivo virtuale.</span><span class="sxs-lookup"><span data-stu-id="6986d-109">For more information, see how to configure host servers for your virtual device.</span></span>
> 
> 

## <a name="about-multipathing"></a><span data-ttu-id="6986d-110">Informazioni sui percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-110">About multipathing</span></span>
<span data-ttu-id="6986d-111">La funzionalità di percorsi multipli consente di configurare più percorsi I/O tra un server host e un dispositivo di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="6986d-111">The multipathing feature allows you to configure multiple I/O paths between a host server and a storage device.</span></span> <span data-ttu-id="6986d-112">I percorsi I/O sono connessioni SAN fisiche che possono includere cavi, switch, interfacce di rete e controller separati.</span><span class="sxs-lookup"><span data-stu-id="6986d-112">These I/O paths are physical SAN connections that can include separate cables, switches, network interfaces, and controllers.</span></span> <span data-ttu-id="6986d-113">I percorsi multipli aggregano i percorsi I/O per configurare un nuovo dispositivo associato a tutti i percorsi aggregati.</span><span class="sxs-lookup"><span data-stu-id="6986d-113">Multipathing aggregates the I/O paths, to configure a new device that is associated with all of the aggregated paths.</span></span>

<span data-ttu-id="6986d-114">Lo scopo dei percorsi multipli è duplice:</span><span class="sxs-lookup"><span data-stu-id="6986d-114">The purpose of multipathing is two-fold:</span></span>

* <span data-ttu-id="6986d-115">**Disponibilità elevata**: fornisce un percorso alternativo se qualsiasi elemento del percorso I/O (ad esempio un cavo, uno switch, l'interfaccia di rete o il controller) non riesce.</span><span class="sxs-lookup"><span data-stu-id="6986d-115">**High availability**: It provides an alternate path if any element of the I/O path (such as a cable, switch, network interface, or controller) fails.</span></span>
* <span data-ttu-id="6986d-116">**Bilanciamento del carico**: a seconda della configurazione del dispositivo di archiviazione, è possibile migliorare le prestazioni rilevando carichi sui percorsi I/O e in modo dinamico con il ribilanciamento di tali carichi.</span><span class="sxs-lookup"><span data-stu-id="6986d-116">**Load balancing**: Depending on the configuration of your storage device, it can improve the performance by detecting loads on the I/O paths and dynamically rebalancing those loads.</span></span>

### <a name="about-multipathing-components"></a><span data-ttu-id="6986d-117">Informazioni sui componenti dei percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-117">About multipathing components</span></span>
<span data-ttu-id="6986d-118">I percorsi multipli in Linux sono costituiti da componenti kernel e spazio utente come elencato di seguito.</span><span class="sxs-lookup"><span data-stu-id="6986d-118">Multipathing in Linux consists of kernel components and user-space components as tabulated below.</span></span>

* <span data-ttu-id="6986d-119">**Kernel**: il componente principale è il *mapper dei dispositivi* che reindirizza l'I/O e supporta il failover per i percorsi e i gruppi di percorsi.</span><span class="sxs-lookup"><span data-stu-id="6986d-119">**Kernel**: The main component is the *device-mapper* that reroutes I/O and supports failover for paths and path groups.</span></span>

* <span data-ttu-id="6986d-120">**Spazio utente**: si tratta di *strumenti per percorsi multipli* che gestiscono i dispositivi a percorsi multipli, indicando il modulo a percorsi multipli del mapper dei dispositivi le operazioni da eseguire.</span><span class="sxs-lookup"><span data-stu-id="6986d-120">**User-space**: These are *multipath-tools* that manage multipathed devices by instructing the device-mapper multipath module what to do.</span></span> <span data-ttu-id="6986d-121">Questi strumenti sono:</span><span class="sxs-lookup"><span data-stu-id="6986d-121">The tools consist of:</span></span>
   
   * <span data-ttu-id="6986d-122">**Multipath**: elenca e configura i dispositivi a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-122">**Multipath**: lists and configures multipathed devices.</span></span>
   * <span data-ttu-id="6986d-123">**Multipathd**: daemon che esegue i percorsi multipli e monitora i percorsi.</span><span class="sxs-lookup"><span data-stu-id="6986d-123">**Multipathd**: daemon that executes multipath and monitors the paths.</span></span>
   * <span data-ttu-id="6986d-124">**Devmap-name**: fornisce un nome significativo del dispositivo a udev per devmap.</span><span class="sxs-lookup"><span data-stu-id="6986d-124">**Devmap-name**: provides a meaningful device-name to udev for devmaps.</span></span>
   * <span data-ttu-id="6986d-125">**Kpartx**: mappa devmap lineari alle partizioni del dispositivo per rendere partizionabili le mappe a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-125">**Kpartx**: maps linear devmaps to device partitions to make multipath maps partitionable.</span></span>
   * <span data-ttu-id="6986d-126">**Multipath.conf**: file di configurazione per daemon a percorsi multipli usato per sovrascrivere la tabella di configurazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="6986d-126">**Multipath.conf**: configuration file for multipath daemon that is used to overwrite the built-in configuration table.</span></span>

### <a name="about-the-multipathconf-configuration-file"></a><span data-ttu-id="6986d-127">Informazioni sul file di configurazione multipath.conf</span><span class="sxs-lookup"><span data-stu-id="6986d-127">About the multipath.conf configuration file</span></span>
<span data-ttu-id="6986d-128">Il file di configurazione `/etc/multipath.conf` rende configurabili dall'utente molte delle funzionalità dei percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-128">The configuration file `/etc/multipath.conf` makes many of the multipathing features user-configurable.</span></span> <span data-ttu-id="6986d-129">Il comando `multipath` e il daemon kernel `multipathd` usano le informazioni ricavate da questo file.</span><span class="sxs-lookup"><span data-stu-id="6986d-129">The `multipath` command and the kernel daemon `multipathd` use information found in this file.</span></span> <span data-ttu-id="6986d-130">Il file viene consultato solo durante la configurazione dei dispositivi a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-130">The file is consulted only during the configuration of the multipath devices.</span></span> <span data-ttu-id="6986d-131">Assicurarsi che tutte le modifiche vengano apportate prima di eseguire il comando `multipath` .</span><span class="sxs-lookup"><span data-stu-id="6986d-131">Make sure that all changes are made before you run the `multipath` command.</span></span> <span data-ttu-id="6986d-132">Se successivamente si modifica il file, è necessario arrestare e avviare multipathd nuovamente per rendere effettive le modifiche.</span><span class="sxs-lookup"><span data-stu-id="6986d-132">If you modify the file afterwards, you will need to stop and start multipathd again for the changes to take effect.</span></span>

<span data-ttu-id="6986d-133">Il file multipath.conf è composto da cinque sezioni:</span><span class="sxs-lookup"><span data-stu-id="6986d-133">The multipath.conf has five sections:</span></span>

- <span data-ttu-id="6986d-134">**System level defaults** *(defaults)*: è possibile ignorare i valori predefiniti a livello di sistema.</span><span class="sxs-lookup"><span data-stu-id="6986d-134">**System level defaults** *(defaults)*: You can override system level defaults.</span></span>
- <span data-ttu-id="6986d-135">**Blacklisted devices** *(blacklist)*: è possibile specificare l'elenco dei dispositivi che il mapper dei dispositivi non deve controllare.</span><span class="sxs-lookup"><span data-stu-id="6986d-135">**Blacklisted devices** *(blacklist)*: You can specify the list of devices that should not be controlled by device-mapper.</span></span>
- <span data-ttu-id="6986d-136">**Blacklist exceptions** *(blacklist_exceptions)*: è possibile identificare i dispositivi specifici da considerare come dispositivi a percorsi multipli anche se elencati nella blacklist.</span><span class="sxs-lookup"><span data-stu-id="6986d-136">**Blacklist exceptions** *(blacklist_exceptions)*: You can identify specific devices to be treated as multipath devices even if listed in the blacklist.</span></span>
- <span data-ttu-id="6986d-137">**Storage controller specific settings** *(devices)*: è possibile specificare impostazioni di configurazione che verranno applicate ai dispositivi con informazioni sul fornitore e sul prodotto.</span><span class="sxs-lookup"><span data-stu-id="6986d-137">**Storage controller specific settings** *(devices)*: You can specify configuration settings that will be applied to devices that have Vendor and Product information.</span></span>
- <span data-ttu-id="6986d-138">**Device specific settings** *(multipaths)*: è possibile usare questa sezione per ottimizzare le impostazioni di configurazione per le singole unità logiche.</span><span class="sxs-lookup"><span data-stu-id="6986d-138">**Device specific settings** *(multipaths)*: You can use this section to fine-tune the configuration settings for individual LUNs.</span></span>

## <a name="configure-multipathing-on-storsimple-connected-to-linux-host"></a><span data-ttu-id="6986d-139">Configurare percorsi multipli in dispositivi StorSimple connessi all'host Linux</span><span class="sxs-lookup"><span data-stu-id="6986d-139">Configure multipathing on StorSimple connected to Linux host</span></span>
<span data-ttu-id="6986d-140">Un dispositivo StorSimple connesso a un host Linux può essere configurato per l'elevata disponibilità e il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="6986d-140">A StorSimple device connected to a Linux host can be configured for high availability and load balancing.</span></span> <span data-ttu-id="6986d-141">Ad esempio, se l'host Linux ha due interfacce connesse alla SAN e il dispositivo ha due interfacce connesse alla SAN in modo che queste interfacce siano tutte nella stessa subnet, saranno disponibili quattro percorsi.</span><span class="sxs-lookup"><span data-stu-id="6986d-141">For example, if the Linux host has two interfaces connected to the SAN and the device has two interfaces connected to the SAN such that these interfaces are on the same subnet, then there will be 4 paths available.</span></span> <span data-ttu-id="6986d-142">Tuttavia, se ogni interfaccia DATA sull'interfaccia del dispositivo e dell'host si trova in una diversa subnet IP (non instradabile), saranno disponibili solo due percorsi.</span><span class="sxs-lookup"><span data-stu-id="6986d-142">However, if each DATA interface on the device and host interface are on a different IP subnet (and not routable), then only 2 paths will be available.</span></span> <span data-ttu-id="6986d-143">È possibile configurare percorsi multipli per trovare automaticamente tutti i percorsi disponibili, scegliere un algoritmo di bilanciamento del carico per tali percorsi, applicare impostazioni di configurazione specifiche per i volumi solo StorSimple, quindi abilitare e verificare i percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-143">You can configure multipathing to automatically discover all the available paths, choose a load-balancing algorithm for those paths, apply specific configuration settings for StorSimple-only volumes, and then enable and verify multipathing.</span></span>

<span data-ttu-id="6986d-144">La procedura seguente descrive come configurare i percorsi multipli quando un dispositivo StorSimple con due interfacce di rete viene connesso a un host con due interfacce di rete.</span><span class="sxs-lookup"><span data-stu-id="6986d-144">The following procedure describes how to configure multipathing when a StorSimple device with two network interfaces is connected to a host with two network interfaces.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6986d-145">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6986d-145">Prerequisites</span></span>
<span data-ttu-id="6986d-146">Questa sezione illustra nel dettaglio i prerequisiti di configurazione per il server CentOS e il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-146">This section details the configuration prerequisites for CentOS server and your StorSimple device.</span></span>

### <a name="on-centos-host"></a><span data-ttu-id="6986d-147">Sull'host CentOS</span><span class="sxs-lookup"><span data-stu-id="6986d-147">On CentOS host</span></span>
1. <span data-ttu-id="6986d-148">Assicurarsi che l'host CentOS abbia due interfacce di rete abilitate.</span><span class="sxs-lookup"><span data-stu-id="6986d-148">Make sure that your CentOS host has 2 network interfaces enabled.</span></span> <span data-ttu-id="6986d-149">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-149">Type:</span></span>
   
    `ifconfig`
   
    <span data-ttu-id="6986d-150">L'esempio seguente mostra l'output che si ottiene quando sull'host sono presenti due interfacce di rete (`eth0` e `eth1`).</span><span class="sxs-lookup"><span data-stu-id="6986d-150">The following example shows the output when two network interfaces (`eth0` and `eth1`) are present on the host.</span></span>
   
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
2. <span data-ttu-id="6986d-151">Installare *iSCSI-initiator-utils* sul server CentOS.</span><span class="sxs-lookup"><span data-stu-id="6986d-151">Install *iSCSI-initiator-utils* on your CentOS server.</span></span> <span data-ttu-id="6986d-152">Seguire questa procedura per installare *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="6986d-152">Perform the following steps to install *iSCSI-initiator-utils*.</span></span>
   
   1. <span data-ttu-id="6986d-153">Accedere come `root` all'host CentOS.</span><span class="sxs-lookup"><span data-stu-id="6986d-153">Log on as `root` into your CentOS host.</span></span>
   2. <span data-ttu-id="6986d-154">Installare *iSCSI-initiator-utils*.</span><span class="sxs-lookup"><span data-stu-id="6986d-154">Install the *iSCSI-initiator-utils*.</span></span> <span data-ttu-id="6986d-155">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-155">Type:</span></span>
      
       `yum install iscsi-initiator-utils`
   3. <span data-ttu-id="6986d-156">Dopo aver correttamente installato *iSCSI-initiator-utils* , avviare il servizio iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-156">After the *iSCSI-Initiator-utils* is successfully installed, start the iSCSI service.</span></span> <span data-ttu-id="6986d-157">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-157">Type:</span></span>
      
       `service iscsid start`
      
       <span data-ttu-id="6986d-158">A volte, `iscsid` potrebbe non avviarsi e può rendersi necessaria l'opzione `--force`</span><span class="sxs-lookup"><span data-stu-id="6986d-158">On occasions, `iscsid` may not actually start and the `--force` option may be needed</span></span>
   4. <span data-ttu-id="6986d-159">Per assicurarsi che l'iniziatore iSCSI sia abilitato durante la fase di avvio, usare il comando `chkconfig` per abilitare il servizio.</span><span class="sxs-lookup"><span data-stu-id="6986d-159">To ensure that your iSCSI initiator is enabled during boot time, use the `chkconfig` command to enable the service.</span></span>
      
       `chkconfig iscsi on`
   5. <span data-ttu-id="6986d-160">Per verificare che sia stato correttamente configurato, eseguire il comando:</span><span class="sxs-lookup"><span data-stu-id="6986d-160">To verify that that it was properly setup, run the command:</span></span>
      
       `chkconfig --list | grep iscsi`
      
       <span data-ttu-id="6986d-161">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="6986d-161">A sample output is shown below.</span></span>
      
           iscsi   0:off   1:off   2:on3:on4:on5:on6:off
           iscsid  0:off   1:off   2:on3:on4:on5:on6:off
      
       <span data-ttu-id="6986d-162">Nell'esempio precedente, è possibile vedere che l'ambiente iSCSI verrà eseguito in fase di avvio su livelli di esecuzione 2, 3, 4 e 5.</span><span class="sxs-lookup"><span data-stu-id="6986d-162">From the above example, you can see that your iSCSI environment will run on boot time on run levels 2, 3, 4, and 5.</span></span>
3. <span data-ttu-id="6986d-163">Installare *device-mapper-multipath*.</span><span class="sxs-lookup"><span data-stu-id="6986d-163">Install *device-mapper-multipath*.</span></span> <span data-ttu-id="6986d-164">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-164">Type:</span></span>
   
    `yum install device-mapper-multipath`
   
    <span data-ttu-id="6986d-165">Viene avviata l'installazione.</span><span class="sxs-lookup"><span data-stu-id="6986d-165">The installation will start.</span></span> <span data-ttu-id="6986d-166">Digitare **Y** per continuare quando viene richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="6986d-166">Type **Y** to continue when prompted for confirmation.</span></span>

### <a name="on-storsimple-device"></a><span data-ttu-id="6986d-167">Sul dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="6986d-167">On StorSimple device</span></span>
<span data-ttu-id="6986d-168">Il dispositivo StorSimple deve avere:</span><span class="sxs-lookup"><span data-stu-id="6986d-168">Your StorSimple device should have:</span></span>

* <span data-ttu-id="6986d-169">Almeno due interfacce abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-169">A minimum of two interfaces enabled for iSCSI.</span></span> <span data-ttu-id="6986d-170">Per verificare che le due interfacce siano abilitate per iSCSI sul dispositivo StorSimple, seguire questa procedura nel portale di Azure classico del dispositivo StorSimple:</span><span class="sxs-lookup"><span data-stu-id="6986d-170">To verify that two interfaces are iSCSI-enabled on your StorSimple device, perform the following steps in the Azure classic portal for your StorSimple device:</span></span>
  
  1. <span data-ttu-id="6986d-171">Accedere al portale classico del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-171">Log into the classic portal for your StorSimple device.</span></span>
  2. <span data-ttu-id="6986d-172">Selezionare il servizio StorSimple Manager, fare clic su **Dispositivi** e scegliere lo specifico dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-172">Select your StorSimple Manager service, click **Devices** and choose the specific StorSimple device.</span></span> <span data-ttu-id="6986d-173">Fare clic su **Configura** e verificare le impostazioni di interfaccia di rete.</span><span class="sxs-lookup"><span data-stu-id="6986d-173">Click **Configure** and verify the network interface settings.</span></span> <span data-ttu-id="6986d-174">Di seguito è riportata una schermata con due interfacce di rete abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-174">A screenshot with two iSCSI-enabled network interfaces is shown below.</span></span> <span data-ttu-id="6986d-175">Entrambe le interfacce di rete da 10 GbE, DATA 2 e DATA 3, sono abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-175">Here DATA 2 and DATA 3, both 10 GbE interfaces are enabled for iSCSI.</span></span>
     
      ![Configurazione DATA 2 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761347.png)
     
      ![Configurazione DATA 3 StorSimple MPIO](./media/storsimple-configure-mpio-on-linux/IC761348.png)
     
      <span data-ttu-id="6986d-178">Nella pagina **Configura**</span><span class="sxs-lookup"><span data-stu-id="6986d-178">In the **Configure** page</span></span>
     
     1. <span data-ttu-id="6986d-179">Assicurarsi che entrambe le interfacce di rete siano abilitate per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-179">Ensure that both network interfaces are iSCSI-enabled.</span></span> <span data-ttu-id="6986d-180">Il campo **Abilitato per iSCSI** deve essere impostato su **Sì**.</span><span class="sxs-lookup"><span data-stu-id="6986d-180">The **iSCSI enabled** field should be set to **Yes**.</span></span>
     2. <span data-ttu-id="6986d-181">Assicurarsi che le interfacce di rete abbiano la stessa velocità, cioè 1 GbE o 10 GbE.</span><span class="sxs-lookup"><span data-stu-id="6986d-181">Ensure that the network interfaces have the same speed, both should be 1 GbE or 10 GbE.</span></span>
     3. <span data-ttu-id="6986d-182">Prendere nota degli indirizzi IPv4 delle interfacce abilitate per iSCSI e salvarli per un uso successivo nell'host.</span><span class="sxs-lookup"><span data-stu-id="6986d-182">Note the IPv4 addresses of the iSCSI-enabled interfaces and save for later use on the host.</span></span>
* <span data-ttu-id="6986d-183">Le interfacce iSCSI sul dispositivo StorSimple devono essere raggiungibili dal server CentOS.</span><span class="sxs-lookup"><span data-stu-id="6986d-183">The iSCSI interfaces on your StorSimple device should be reachable from the CentOS server.</span></span>
      <span data-ttu-id="6986d-184">Per verificarlo, è necessario fornire gli indirizzi IP delle interfacce di rete abilitate per iSCSI StorSimple nel server host.</span><span class="sxs-lookup"><span data-stu-id="6986d-184">To verify this, you need to provide the IP addresses of your StorSimple iSCSI-enabled network interfaces on your host server.</span></span> <span data-ttu-id="6986d-185">I comandi usati e l'output corrispondente con DATA2 (10.126.162.25) e DATA3 (10.126.162.26) sono illustrati di seguito:</span><span class="sxs-lookup"><span data-stu-id="6986d-185">The commands used and the corresponding output with DATA2 (10.126.162.25) and DATA3 (10.126.162.26) is shown below:</span></span>
  
        [root@centosSS ~]# iscsiadm -m discovery -t sendtargets -p 10.126.162.25:3260
        10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target
        10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g44mt-target

### <a name="hardware-configuration"></a><span data-ttu-id="6986d-186">Configurazione hardware</span><span class="sxs-lookup"><span data-stu-id="6986d-186">Hardware configuration</span></span>
<span data-ttu-id="6986d-187">Si consiglia di connettere le due interfacce di rete iSCSI in percorsi distinti per la ridondanza.</span><span class="sxs-lookup"><span data-stu-id="6986d-187">We recommend that you connect the two iSCSI network interfaces on separate paths for redundancy.</span></span> <span data-ttu-id="6986d-188">La figura seguente illustra la configurazione hardware consigliata per la disponibilità elevata e il bilanciamento del carico dei percorsi multipli per il server CentOS e il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-188">The figure below shows the recommended hardware configuration for high availability and load-balancing multipathing for your CentOS server and StorSimple device.</span></span>

![Configurazione hardware MPIO per StorSimple all'host Linux](./media/storsimple-configure-mpio-on-linux/MPIOHardwareConfigurationStorSimpleToLinuxHost2M.png)

<span data-ttu-id="6986d-190">Come illustrato nella figura precedente:</span><span class="sxs-lookup"><span data-stu-id="6986d-190">As shown in the preceding figure:</span></span>

* <span data-ttu-id="6986d-191">Il dispositivo StorSimple ha una configurazione attiva-passiva con due controller.</span><span class="sxs-lookup"><span data-stu-id="6986d-191">Your StorSimple device is in an active-passive configuration with two controllers.</span></span>
* <span data-ttu-id="6986d-192">Due commutatori SAN sono connesse ai controller dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="6986d-192">Two SAN switches are connected to your device controllers.</span></span>
* <span data-ttu-id="6986d-193">Due iniziatori iSCSI sono abilitati nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-193">Two iSCSI initiators are enabled on your StorSimple device.</span></span>
* <span data-ttu-id="6986d-194">Due interfacce di rete sono abilitate sull'host CentOS.</span><span class="sxs-lookup"><span data-stu-id="6986d-194">Two network interfaces are enabled on your CentOS host.</span></span>

<span data-ttu-id="6986d-195">La configurazione sopra indicata restituirà 4 percorsi separati tra il dispositivo e l'host se l'host e le interfacce di dati sono instradabili.</span><span class="sxs-lookup"><span data-stu-id="6986d-195">The above configuration will yield 4 separate paths between your device and the host if the host and data interfaces are routable.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="6986d-196">È consigliabile non combinare interfacce di rete da 1 GbE e da 10 GbE per i percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-196">We recommend that you do not mix 1 GbE and 10 GbE network interfaces for multipathing.</span></span> <span data-ttu-id="6986d-197">Quando si usano due interfacce di rete, devono essere di tipo identico.</span><span class="sxs-lookup"><span data-stu-id="6986d-197">When using two network interfaces, both the interfaces should be the identical type.</span></span>
> * <span data-ttu-id="6986d-198">Sul dispositivo StorSimple, DATA0, DATA1, DATA4 e DATA5 sono interfacce da 1 GbE mentre DATA2 e DATA3 sono interfacce di rete da 10 GbE.|</span><span class="sxs-lookup"><span data-stu-id="6986d-198">On your StorSimple device, DATA0, DATA1, DATA4 and DATA5 are 1 GbE interfaces whereas DATA2 and DATA3 are 10 GbE network interfaces.|</span></span>
> 
> 

## <a name="configuration-steps"></a><span data-ttu-id="6986d-199">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="6986d-199">Configuration steps</span></span>
<span data-ttu-id="6986d-200">La procedura di configurazione per i percorsi multipli implica la configurazione dei percorsi disponibili per il rilevamento automatico, specificando l'algoritmo di bilanciamento del carico da usare, abilitando i percorsi multipli e infine verificando la configurazione.</span><span class="sxs-lookup"><span data-stu-id="6986d-200">The configuration steps for multipathing involve configuring the available paths for automatic discovery, specifying the load-balancing algorithm to use, enabling multipathing and finally verifying the configuration.</span></span> <span data-ttu-id="6986d-201">Ognuno dei passaggi precedenti viene illustrato nel dettaglio nelle sezioni seguenti.</span><span class="sxs-lookup"><span data-stu-id="6986d-201">Each of these steps is discussed in detail in the following sections.</span></span>

### <a name="step-1-configure-multipathing-for-automatic-discovery"></a><span data-ttu-id="6986d-202">Passaggio 1: Configurare percorsi multipli per il rilevamento automatico</span><span class="sxs-lookup"><span data-stu-id="6986d-202">Step 1: Configure multipathing for automatic discovery</span></span>
<span data-ttu-id="6986d-203">I dispositivi supportati da percorsi multipli possono essere individuati e configurati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6986d-203">The multipath-supported devices can be automatically discovered and configured.</span></span>

1. <span data-ttu-id="6986d-204">Inizializzare il file `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="6986d-204">Initialize `/etc/multipath.conf` file.</span></span> <span data-ttu-id="6986d-205">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-205">Type:</span></span>
   
     `mpathconf --enable`
   
    <span data-ttu-id="6986d-206">Il comando precedente creerà un file `sample/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="6986d-206">The above command will create a `sample/etc/multipath.conf` file.</span></span>
2. <span data-ttu-id="6986d-207">Avviare il servizio a percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-207">Start multipath service.</span></span> <span data-ttu-id="6986d-208">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-208">Type:</span></span>
   
    `service multipathd start`
   
    <span data-ttu-id="6986d-209">Viene visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="6986d-209">You will see the following output:</span></span>
   
    `Starting multipathd daemon:`
3. <span data-ttu-id="6986d-210">Abilitare il rilevamento automatico dei percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-210">Enable automatic discovery of multipaths.</span></span> <span data-ttu-id="6986d-211">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-211">Type:</span></span>
   
    `mpathconf --find_multipaths y`
   
    <span data-ttu-id="6986d-212">Verrà modificata la sezione delle impostazioni predefinite del file `multipath.conf` , come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6986d-212">This will modify the defaults section of your `multipath.conf` as shown below:</span></span>
   
        defaults {
        find_multipaths yes
        user_friendly_names yes
        path_grouping_policy multibus
        }

### <a name="step-2-configure-multipathing-for-storsimple-volumes"></a><span data-ttu-id="6986d-213">Passaggio 2: Configurare i percorsi multipli per volumi StorSimple</span><span class="sxs-lookup"><span data-stu-id="6986d-213">Step 2: Configure multipathing for StorSimple volumes</span></span>
<span data-ttu-id="6986d-214">Per impostazione predefinita, tutti i dispositivi sono elencati nella blacklist del file multipath.conf neri e verranno ignorati.</span><span class="sxs-lookup"><span data-stu-id="6986d-214">By default, all devices are black listed in the multipath.conf file and will be bypassed.</span></span> <span data-ttu-id="6986d-215">È necessario creare eccezioni di blacklist per consentire percorsi multipli per volumi dai dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-215">You will need to create blacklist exceptions to allow multipathing for volumes from StorSimple devices.</span></span>

1. <span data-ttu-id="6986d-216">Modificare il file `/etc/mulitpath.conf` .</span><span class="sxs-lookup"><span data-stu-id="6986d-216">Edit the `/etc/mulitpath.conf` file.</span></span> <span data-ttu-id="6986d-217">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-217">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="6986d-218">Trovare la sezione blacklist_exceptions nel file multipath.conf.</span><span class="sxs-lookup"><span data-stu-id="6986d-218">Locate the blacklist_exceptions section in the multipath.conf file.</span></span> <span data-ttu-id="6986d-219">Il dispositivo StorSimple deve essere elencato come eccezione di blacklist in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6986d-219">Your StorSimple device needs to be listed as a blacklist exception in this section.</span></span> <span data-ttu-id="6986d-220">È possibile rimuovere il commento dalle righe pertinenti in questo file per modificarlo, come mostrato di seguito (usare solo il modello specifico del dispositivo in uso):</span><span class="sxs-lookup"><span data-stu-id="6986d-220">You can uncomment relevant lines in this file to modify it as shown below (use only the specific model of the device you are using):</span></span>
   
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

### <a name="step-3-configure-round-robin-multipathing"></a><span data-ttu-id="6986d-221">Passaggio 3: Configurare percorsi multipli round robin</span><span class="sxs-lookup"><span data-stu-id="6986d-221">Step 3: Configure round-robin multipathing</span></span>
<span data-ttu-id="6986d-222">Questo algoritmo di bilanciamento del carico usa tutti i percorsi multipli disponibili per il controller attivo in modo bilanciato e round robin.</span><span class="sxs-lookup"><span data-stu-id="6986d-222">This load-balancing algorithm uses all the available multipaths to the active controller in a balanced, round-robin fashion.</span></span>

1. <span data-ttu-id="6986d-223">Modificare il file `/etc/multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="6986d-223">Edit the `/etc/multipath.conf` file.</span></span> <span data-ttu-id="6986d-224">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-224">Type:</span></span>
   
    `vi /etc/multipath.conf`
2. <span data-ttu-id="6986d-225">Nella sezione `defaults` impostare `path_grouping_policy` su `multibus`.</span><span class="sxs-lookup"><span data-stu-id="6986d-225">Under the `defaults` section, set the `path_grouping_policy` to `multibus`.</span></span> <span data-ttu-id="6986d-226">`path_grouping_policy` specifica il criterio di raggruppamento dei percorsi predefinito da applicare ai percorsi multipli non specificati.</span><span class="sxs-lookup"><span data-stu-id="6986d-226">The `path_grouping_policy` specifies the default path grouping policy to apply to unspecified multipaths.</span></span> <span data-ttu-id="6986d-227">La sezione delle impostazioni predefinite avrà l'aspetto seguente.</span><span class="sxs-lookup"><span data-stu-id="6986d-227">The defaults section will look as shown below.</span></span>
   
        defaults {
                user_friendly_names yes
                path_grouping_policy multibus
        }

> [!NOTE]
> <span data-ttu-id="6986d-228">I valori più comuni di `path_grouping_policy` includono:</span><span class="sxs-lookup"><span data-stu-id="6986d-228">The most common values of `path_grouping_policy` include:</span></span>
> 
> * <span data-ttu-id="6986d-229">failover = 1 percorso per ogni gruppo prioritario</span><span class="sxs-lookup"><span data-stu-id="6986d-229">failover = 1 path per priority group</span></span>
> * <span data-ttu-id="6986d-230">multibus = tutti i percorsi validi in 1 gruppo prioritario</span><span class="sxs-lookup"><span data-stu-id="6986d-230">multibus = all valid paths in 1 priority group</span></span>
> 
> 

### <a name="step-4-enable-multipathing"></a><span data-ttu-id="6986d-231">Passaggio 4: Abilitare i percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-231">Step 4: Enable multipathing</span></span>
1. <span data-ttu-id="6986d-232">Riavviare il daemon `multipathd` .</span><span class="sxs-lookup"><span data-stu-id="6986d-232">Restart the `multipathd` daemon.</span></span> <span data-ttu-id="6986d-233">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-233">Type:</span></span>
   
    `service multipathd restart`
2. <span data-ttu-id="6986d-234">Si otterrà un output come quello illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6986d-234">The output will be as shown below:</span></span>
   
        [root@centosSS ~]# service multipathd start
        Starting multipathd daemon:  [OK]

### <a name="step-5-verify-multipathing"></a><span data-ttu-id="6986d-235">Passaggio 5: Verificare i percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-235">Step 5: Verify multipathing</span></span>
1. <span data-ttu-id="6986d-236">Assicurarsi prima di tutto che venga stabilita la connessione iSCSI con il dispositivo StorSimple come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="6986d-236">First make sure that iSCSI connection is established with the StorSimple device as follows:</span></span>
   
   <span data-ttu-id="6986d-237">a.</span><span class="sxs-lookup"><span data-stu-id="6986d-237">a.</span></span> <span data-ttu-id="6986d-238">Trovare il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-238">Discover your StorSimple device.</span></span> <span data-ttu-id="6986d-239">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-239">Type:</span></span>
      
    ```
    iscsiadm -m discovery -t sendtargets -p  <IP address of network interface on the device>:<iSCSI port on StorSimple device>
    ```
    
    <span data-ttu-id="6986d-240">Quando l'indirizzo IP per DATA0 è 10.126.162.25 e viene aperta la porta 3260 sul dispositivo StorSimple per il traffico iSCSI in uscita, l'output è il seguente:</span><span class="sxs-lookup"><span data-stu-id="6986d-240">The output when IP address for DATA0 is 10.126.162.25 and port 3260 is opened on the StorSimple device for outbound iSCSI traffic is as shown below:</span></span>
    
    ```
    10.126.162.25:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    10.126.162.26:3260,1 iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target
    ```

    <span data-ttu-id="6986d-241">Copiare il nome qualificato iSCSI del dispositivo StorSimple, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, dall'output precedente.</span><span class="sxs-lookup"><span data-stu-id="6986d-241">Copy the IQN of your StorSimple device, `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`, from the preceding output.</span></span>

   <span data-ttu-id="6986d-242">b.</span><span class="sxs-lookup"><span data-stu-id="6986d-242">b.</span></span> <span data-ttu-id="6986d-243">Connettersi al dispositivo usando il nome qualificato iSCSI di destinazione.</span><span class="sxs-lookup"><span data-stu-id="6986d-243">Connect to the device using target IQN.</span></span> <span data-ttu-id="6986d-244">In questo caso, la destinazione iSCSI è il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-244">The StorSimple device is the iSCSI target here.</span></span> <span data-ttu-id="6986d-245">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-245">Type:</span></span>

    ```
    iscsiadm -m node --login -T <IQN of iSCSI target>
    ```

    <span data-ttu-id="6986d-246">La figura seguente mostra l'output con un nome qualificato iSCSI `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span><span class="sxs-lookup"><span data-stu-id="6986d-246">The following example shows output with a target IQN of `iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target`.</span></span> <span data-ttu-id="6986d-247">L'output indica che è stata effettuata la connessione alle due interfacce di rete abilitate per iSCSI sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="6986d-247">The output indicates that you have successfully connected to the two iSCSI-enabled network interfaces on your device.</span></span>

    ```
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] (multiple)
    Logging in to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Logging in to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] (multiple)
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.25,3260] successful.
    Login to [iface: eth0, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    Login to [iface: eth1, target: iqn.1991-05.com.microsoft:storsimple8100-shx0991003g00dv-target, portal: 10.126.162.26,3260] successful.
    ```

    <span data-ttu-id="6986d-248">Se in questo caso vengono visualizzati due percorsi e una sola interfaccia host, sarà necessario abilitare entrambe le interfacce sull'host per iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-248">If you see only one host interface and two paths here, then you need to enable both the interfaces on host for iSCSI.</span></span> <span data-ttu-id="6986d-249">Consultare le [istruzioni dettagliate nella documentazione Linux](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span><span class="sxs-lookup"><span data-stu-id="6986d-249">You can follow the [detailed instructions in Linux documentation](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/5/html/Online_Storage_Reconfiguration_Guide/iscsioffloadmain.html).</span></span>

2. <span data-ttu-id="6986d-250">Un volume viene esposto al server CentOS dal dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-250">A volume is exposed to the CentOS server from the StorSimple device.</span></span> <span data-ttu-id="6986d-251">Per altre informazioni, vedere la procedura [Passaggio 6: Creare un volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) nel portale di Azure classico dal dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-251">For more information, see [Step 6: Create a volume](storsimple-deployment-walkthrough.md#step-6-create-a-volume) via the Azure classic portal on your StorSimple device.</span></span>

3. <span data-ttu-id="6986d-252">Verificare i percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="6986d-252">Verify the available paths.</span></span> <span data-ttu-id="6986d-253">Digitare:</span><span class="sxs-lookup"><span data-stu-id="6986d-253">Type:</span></span>

      ```
      multipath –l
      ```

      <span data-ttu-id="6986d-254">L'esempio seguente illustra l'output di due interfacce di rete su un dispositivo StorSimple connesso a una singola interfaccia di rete host con due percorsi disponibili.</span><span class="sxs-lookup"><span data-stu-id="6986d-254">The following example shows the output for two network interfaces on a StorSimple device connected to a single host network interface with two available paths.</span></span>

        ```
        mpathb (36486fd20cc081f8dcd3fccb992d45a68) dm-3 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 7:0:0:1 sdc 8:32 active undef running
        `- 6:0:0:1 sdd 8:48 active undef running
        ```

        The following example shows the output for two network interfaces on a StorSimple device connected to two host network interfaces with four available paths.

        ```
        mpathb (36486fd27a23feba1b096226f11420f6b) dm-2 MSFT,STORSIMPLE 8100
        size=100G features='0' hwhandler='0' wp=rw
        `-+- policy='round-robin 0' prio=0 status=active
        |- 17:0:0:0 sdb 8:16 active undef running
        |- 15:0:0:0 sdd 8:48 active undef running
        |- 14:0:0:0 sdc 8:32 active undef running
        `- 16:0:0:0 sde 8:64 active undef running
        ```

        After the paths are configured, refer to the specific instructions on your host operating system (Centos 6.6) to mount and format this volume.

## <a name="troubleshoot-multipathing"></a><span data-ttu-id="6986d-255">Risoluzione dei problemi relativi ai percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-255">Troubleshoot multipathing</span></span>
<span data-ttu-id="6986d-256">Questa sezione contiene alcuni suggerimenti utili in caso di problemi durante la configurazione dei percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-256">This section provides some helpful tips if you run into any issues during multipathing configuration.</span></span>

<span data-ttu-id="6986d-257">D:</span><span class="sxs-lookup"><span data-stu-id="6986d-257">Q.</span></span> <span data-ttu-id="6986d-258">Le modifiche apportate al file `multipath.conf` non hanno effetto.</span><span class="sxs-lookup"><span data-stu-id="6986d-258">I do not see the changes in `multipath.conf` file taking effect.</span></span>

<span data-ttu-id="6986d-259">A.</span><span class="sxs-lookup"><span data-stu-id="6986d-259">A.</span></span> <span data-ttu-id="6986d-260">Se sono state apportate modifiche al file `multipath.conf` , è necessario riavviare il servizio di percorsi multipli.</span><span class="sxs-lookup"><span data-stu-id="6986d-260">If you have made any changes to the `multipath.conf` file, you will need to restart the multipathing service.</span></span> <span data-ttu-id="6986d-261">Digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="6986d-261">Type the following command:</span></span>

    service multipathd restart

<span data-ttu-id="6986d-262">D:</span><span class="sxs-lookup"><span data-stu-id="6986d-262">Q.</span></span> <span data-ttu-id="6986d-263">Sono state abilitate due interfacce di rete sul dispositivo StorSimple e due interfacce di rete sull'host.</span><span class="sxs-lookup"><span data-stu-id="6986d-263">I have enabled two network interfaces on the StorSimple device and two network interfaces on the host.</span></span> <span data-ttu-id="6986d-264">Nell'elenco dei percorsi disponibili sono visibili solo due percorsi,</span><span class="sxs-lookup"><span data-stu-id="6986d-264">When I list the available paths, I see only two paths.</span></span> <span data-ttu-id="6986d-265">mentre dovrebbero essercene quattro.</span><span class="sxs-lookup"><span data-stu-id="6986d-265">I expected to see four available paths.</span></span>

<span data-ttu-id="6986d-266">A.</span><span class="sxs-lookup"><span data-stu-id="6986d-266">A.</span></span> <span data-ttu-id="6986d-267">Assicurarsi che i due percorsi siano nella stessa subnet e instradabili.</span><span class="sxs-lookup"><span data-stu-id="6986d-267">Make sure that the two paths are on the same subnet and routable.</span></span> <span data-ttu-id="6986d-268">Se le interfacce di rete si trovano su VLAN diverse e non sono instradabili, verranno visualizzati solo due percorsi.</span><span class="sxs-lookup"><span data-stu-id="6986d-268">If the network interfaces are on different vLANs and not routable, you will see only two paths.</span></span> <span data-ttu-id="6986d-269">Un modo per verificare questa condizione è assicurarsi che sia possibile raggiungere entrambe le interfacce host da un'interfaccia di rete nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-269">One way to verify this is to make sure that you can reach both the host interfaces from a network interface on the StorSimple device.</span></span> <span data-ttu-id="6986d-270">Sarà necessario [contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md) perché questa verifica può essere eseguita solo in una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="6986d-270">You will need to [contact Microsoft Support](storsimple-contact-microsoft-support.md) as this verification can only be done via a support session.</span></span>

<span data-ttu-id="6986d-271">D:</span><span class="sxs-lookup"><span data-stu-id="6986d-271">Q.</span></span> <span data-ttu-id="6986d-272">Nell'elenco dei percorsi disponibili non è visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="6986d-272">When I list available paths, I do not see any output.</span></span>

<span data-ttu-id="6986d-273">A.</span><span class="sxs-lookup"><span data-stu-id="6986d-273">A.</span></span> <span data-ttu-id="6986d-274">In genere, la mancata visualizzazione di percorsi multipli suggerisce un problema con il daemon di percorsi multipli ed è probabile che qualsiasi problema riguardi il file `multipath.conf` .</span><span class="sxs-lookup"><span data-stu-id="6986d-274">Typically, not seeing any multipathed paths suggests a problem with the multipathing daemon, and it’s most likely that any problem here lies in the `multipath.conf` file.</span></span>

<span data-ttu-id="6986d-275">Potrebbe anche essere opportuno verificare che si possano visualizzare alcuni dischi dopo aver eseguito la connessione alla destinazione, perché se non si riceve alcuna risposta dagli elenchi dei percorsi multipli è probabile che non sia presente alcun disco.</span><span class="sxs-lookup"><span data-stu-id="6986d-275">It would also be worth checking that you can actually see some disks after connecting to the target, as no response from the multipath listings could also mean you don’t have any disks.</span></span>

* <span data-ttu-id="6986d-276">Per ripetere la scansione del bus iSCSI, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6986d-276">Use the following command to rescan the SCSI bus:</span></span>
  
    <span data-ttu-id="6986d-277">`$ rescan-scsi-bus.sh `(parte del pacchetto sg3_utils)</span><span class="sxs-lookup"><span data-stu-id="6986d-277">`$ rescan-scsi-bus.sh `(part of sg3_utils package)</span></span>
* <span data-ttu-id="6986d-278">Digitare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6986d-278">Type the following commands:</span></span>
  
    `$ dmesg | grep sd*`
     
     <span data-ttu-id="6986d-279">Oppure</span><span class="sxs-lookup"><span data-stu-id="6986d-279">Or</span></span>
  
    `$ fdisk –l`
  
    <span data-ttu-id="6986d-280">Verranno restituite informazioni dettagliate sui dischi aggiunti di recente.</span><span class="sxs-lookup"><span data-stu-id="6986d-280">These will return details of recently added disks.</span></span>
* <span data-ttu-id="6986d-281">Per determinare se si tratta di un disco StorSimple, usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="6986d-281">To determine whether it is a StorSimple disk, use the following commands:</span></span>
  
    `cat /sys/block/<DISK>/device/model`
  
    <span data-ttu-id="6986d-282">Verrà restituita una stringa, che determinerà se si tratta di un disco StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-282">This will return a string, which will determine if it’s a StorSimple disk.</span></span>

<span data-ttu-id="6986d-283">Una causa meno probabile, ma possibile, potrebbe anche essere un PID iSCSI non aggiornato.</span><span class="sxs-lookup"><span data-stu-id="6986d-283">A less likely but possible cause could also be stale iscsid pid.</span></span> <span data-ttu-id="6986d-284">Per disconnettersi dalle sessioni iSCSI usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6986d-284">Use the following command to log off from the iSCSI sessions:</span></span>

    iscsiadm -m node --logout -p <Target_IP>

<span data-ttu-id="6986d-285">Ripetere questo comando per tutte le interfacce di rete connesse nella destinazione iSCSI, ovvero il dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6986d-285">Repeat this command for all the connected network interfaces on the iSCSI target, which is your StorSimple device.</span></span> <span data-ttu-id="6986d-286">Dopo aver effettuato la disconnessione da tutte le sessioni iSCSI, usare il nome qualificato iSCSI di destinazione per ristabilire la sessione iSCSI.</span><span class="sxs-lookup"><span data-stu-id="6986d-286">Once you have logged off from all the iSCSI sessions, use the iSCSI target IQN to reestablish the iSCSI session.</span></span> <span data-ttu-id="6986d-287">Digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="6986d-287">Type the following command:</span></span>

    iscsiadm -m node --login -T <TARGET_IQN>


<span data-ttu-id="6986d-288">D:</span><span class="sxs-lookup"><span data-stu-id="6986d-288">Q.</span></span> <span data-ttu-id="6986d-289">Come è possibile verificare che il dispositivo sia incluso nell'elenco dei dispositivi consentiti?</span><span class="sxs-lookup"><span data-stu-id="6986d-289">I am not sure if my device is whitelisted.</span></span>

<span data-ttu-id="6986d-290">A.</span><span class="sxs-lookup"><span data-stu-id="6986d-290">A.</span></span> <span data-ttu-id="6986d-291">Per verificare che il dispositivo sia incluso nell'elenco dei dispositivi consentiti, usare il comando interattivo di risoluzione dei problemi seguente:</span><span class="sxs-lookup"><span data-stu-id="6986d-291">To verify whether your device is whitelisted, use the following troubleshooting interactive command:</span></span>

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


<span data-ttu-id="6986d-292">Per altre informazioni, vedere come [usare il comando interattivo di risoluzione dei problemi per i percorsi multipli](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span><span class="sxs-lookup"><span data-stu-id="6986d-292">For more information, go to [use troubleshooting interactive command for multipathing](http://www.centos.org/docs/5/html/5.1/DM_Multipath/multipath_config_confirm.html).</span></span>

## <a name="list-of-useful-commands"></a><span data-ttu-id="6986d-293">Elenco di comandi utili</span><span class="sxs-lookup"><span data-stu-id="6986d-293">List of useful commands</span></span>
| <span data-ttu-id="6986d-294">Digitare </span><span class="sxs-lookup"><span data-stu-id="6986d-294">Type</span></span> | <span data-ttu-id="6986d-295">Comando</span><span class="sxs-lookup"><span data-stu-id="6986d-295">Command</span></span> | <span data-ttu-id="6986d-296">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6986d-296">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6986d-297">**iSCSI**</span><span class="sxs-lookup"><span data-stu-id="6986d-297">**iSCSI**</span></span> |`service iscsid start` |<span data-ttu-id="6986d-298">Avviare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-298">Start iSCSI service</span></span> |
| &nbsp; |`service iscsid stop` |<span data-ttu-id="6986d-299">Arrestare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-299">Stop iSCSI service</span></span> |
| &nbsp; |`service iscsid restart` |<span data-ttu-id="6986d-300">Riavviare il servizio iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-300">Restart iSCSI service</span></span> |
| &nbsp; |`iscsiadm -m discovery -t sendtargets -p <TARGET_IP>` |<span data-ttu-id="6986d-301">Individuare le destinazioni disponibili all'indirizzo specificato</span><span class="sxs-lookup"><span data-stu-id="6986d-301">Discover available targets on the specified address</span></span> |
| &nbsp; |`iscsiadm -m node --login -T <TARGET_IQN>` |<span data-ttu-id="6986d-302">Accedere alla destinazione iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-302">Log in to the iSCSI target</span></span> |
| &nbsp; |`iscsiadm -m node --logout -p <Target_IP>` |<span data-ttu-id="6986d-303">Disconnettersi dalla destinazione iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-303">Log out from the iSCSI target</span></span> |
| &nbsp; |`cat /etc/iscsi/initiatorname.iscsi` |<span data-ttu-id="6986d-304">Stampare il nome dell'iniziatore iSCSI</span><span class="sxs-lookup"><span data-stu-id="6986d-304">Print iSCSI initiator name</span></span> |
| &nbsp; |`iscsiadm –m session –s <sessionid> -P 3` |<span data-ttu-id="6986d-305">Controllare lo stato della sessione e del volume iSCSI individuati nell'host</span><span class="sxs-lookup"><span data-stu-id="6986d-305">Check the state of the iSCSI session and volume discovered on the host</span></span> |
| &nbsp; |`iscsi –m session` |<span data-ttu-id="6986d-306">Mostra tutte le sessioni iSCSI stabilite tra l'host e il dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="6986d-306">Shows all the iSCSI sessions established between the host and the StorSimple device</span></span> |
|  | | |
| <span data-ttu-id="6986d-307">**Percorsi multipli**</span><span class="sxs-lookup"><span data-stu-id="6986d-307">**Multipathing**</span></span> |`service multipathd start` |<span data-ttu-id="6986d-308">Avviare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-308">Start multipath daemon</span></span> |
| &nbsp; |`service multipathd stop` |<span data-ttu-id="6986d-309">Arrestare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-309">Stop multipath daemon</span></span> |
| &nbsp; |`service multipathd restart` |<span data-ttu-id="6986d-310">Riavviare il daemon a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-310">Restart multipath daemon</span></span> |
| &nbsp; |`chkconfig multipathd on` </br> <span data-ttu-id="6986d-311">Oppure</span><span class="sxs-lookup"><span data-stu-id="6986d-311">OR</span></span> </br> `mpathconf –with_chkconfig y` |<span data-ttu-id="6986d-312">Abilitare l'avvio del daemon a percorsi multipli all'avvio del computer</span><span class="sxs-lookup"><span data-stu-id="6986d-312">Enable multipath daemon to start at boot time</span></span> |
| &nbsp; |`multipathd –k` |<span data-ttu-id="6986d-313">Avviare la console interattiva per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="6986d-313">Start the interactive console for troubleshooting</span></span> |
| &nbsp; |`multipath –l` |<span data-ttu-id="6986d-314">Elencare le connessioni e i dispositivi a percorsi multipli</span><span class="sxs-lookup"><span data-stu-id="6986d-314">List multipath connections and devices</span></span> |
| &nbsp; |`mpathconf --enable` |<span data-ttu-id="6986d-315">Creare un file mulitpath.conf di esempio in `/etc/mulitpath.conf`</span><span class="sxs-lookup"><span data-stu-id="6986d-315">Create a sample mulitpath.conf file in `/etc/mulitpath.conf`</span></span> |
|  | | |

## <a name="next-steps"></a><span data-ttu-id="6986d-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6986d-316">Next steps</span></span>
<span data-ttu-id="6986d-317">Nella configurazione di MPIO sull'host Linux può anche essere necessario consultare i seguenti documenti relativi a CentOS 6.6:</span><span class="sxs-lookup"><span data-stu-id="6986d-317">As you are configuring MPIO on Linux host, you may also need to refer to the following CentoS 6.6 documents:</span></span>

* [<span data-ttu-id="6986d-318">Configurazione di MPIO su CentOS</span><span class="sxs-lookup"><span data-stu-id="6986d-318">Setting up MPIO on CentOS</span></span>](http://www.centos.org/docs/5/html/5.1/DM_Multipath/setup_procedure.html)
* [<span data-ttu-id="6986d-319">Guida alla formazione Linux</span><span class="sxs-lookup"><span data-stu-id="6986d-319">Linux Training Guide</span></span>](http://linux-training.be/files/books/LinuxAdm.pdf)

