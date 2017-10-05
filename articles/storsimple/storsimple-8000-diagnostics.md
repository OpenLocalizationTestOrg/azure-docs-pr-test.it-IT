---
title: Strumento di diagnostica per la risoluzione dei problemi del dispositivo StorSimple 8000 | Microsoft Docs
description: "Vengono descritte le modalità del dispositivo StorSimple e viene illustrato come utilizzare Windows PowerShell per StorSimple per modificare la modalità del dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 8fae7bb357f8e5e8eff249edfe3a2aaafe04283c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-storsimple-diagnostics-tool-to-troubleshoot-8000-series-device-issues"></a><span data-ttu-id="0b7ce-103">Usare lo strumento di diagnostica StorSimple per risolvere i problemi dei dispositivi della serie 8000</span><span class="sxs-lookup"><span data-stu-id="0b7ce-103">Use the StorSimple Diagnostics Tool to troubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="0b7ce-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="0b7ce-104">Overview</span></span>

<span data-ttu-id="0b7ce-105">Lo strumento di diagnostica StorSimple permette di eseguire la diagnosi dei problemi legati al sistema, alle prestazioni, alla rete e all'integrità dei componenti hardware per un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-105">The StorSimple Diagnostics tool diagnoses issues related to system, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="0b7ce-106">È possibile usare lo strumento di diagnostica in vari scenari,</span><span class="sxs-lookup"><span data-stu-id="0b7ce-106">The diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="0b7ce-107">che includono la pianificazione del carico di lavoro, la distribuzione di un dispositivo StorSimple, la valutazione dell'ambiente di rete e il calcolo delle prestazioni di un dispositivo operativo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-107">These scenarios include workload planning, deploying a StorSimple device, assessing the network environment, and determining the performance of an operational device.</span></span> <span data-ttu-id="0b7ce-108">Questo articolo offre una panoramica sullo strumento di diagnostica e ne illustra l'uso con un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-108">This article provides an overview of the diagnostics tool and describes how the tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="0b7ce-109">L'uso dello strumento di diagnostica è destinato principalmente a dispositivi StorSimple locali della serie 8000 (8100 e 8600).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-109">The diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="0b7ce-110">Eseguire lo strumento di diagnostica</span><span class="sxs-lookup"><span data-stu-id="0b7ce-110">Run diagnostics tool</span></span>

<span data-ttu-id="0b7ce-111">Per eseguire questo strumento è possibile usare l'interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-111">This tool can be run via the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="0b7ce-112">Per accedere all'interfaccia locale del dispositivo è possibile procedere in due modi:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-112">There are two ways to access the local interface of your device:</span></span>

* <span data-ttu-id="0b7ce-113">[Usare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-113">[Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="0b7ce-114">[Accedere in remoto allo strumento tramite Windows PowerShell per StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-114">[Remotely access the tool via the Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="0b7ce-115">In questo articolo si presuppone che la connessione alla console seriale del dispositivo sia stata stabilita tramite PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-115">In this article, we assume that you have connected to the device serial console via PuTTY.</span></span>

#### <a name="to-run-the-diagnostics-tool"></a><span data-ttu-id="0b7ce-116">Per eseguire lo strumento di diagnostica</span><span class="sxs-lookup"><span data-stu-id="0b7ce-116">To run the diagnostics tool</span></span>

<span data-ttu-id="0b7ce-117">Dopo aver stabilito la connessione all'interfaccia di Windows PowerShell del dispositivo, seguire questa procedura seguente per eseguire il cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-117">Once you have connected to the Windows PowerShell interface of the device, perform the following steps to run the cmdlet.</span></span>
1. <span data-ttu-id="0b7ce-118">Accedere alla console seriale del dispositivo seguendo i passaggi riportati in [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-118">Log on to the device serial console by following the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="0b7ce-119">Digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-119">Type the following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="0b7ce-120">Se il parametro di ambito non è specificato, il cmdlet esegue tutti i test di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-120">If the scope parameter is not specified, the cmdlet executes all the diagnostic tests.</span></span> <span data-ttu-id="0b7ce-121">I test riguardano il sistema, l'integrità dei componenti hardware, la rete e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="0b7ce-122">Per eseguire solo un determinato test, è necessario specificare il parametro di ambito.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-122">To run only a specific test, specify the scope parameter.</span></span> <span data-ttu-id="0b7ce-123">Ad esempio, per eseguire solo il test della rete, digitare:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-123">For instance, to run only the network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="0b7ce-124">Selezionare e copiare l'output dalla finestra PuTTY in un file di testo per analizzarlo ulteriormente.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-124">Select and copy the output from the PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-to-use-the-diagnostics-tool"></a><span data-ttu-id="0b7ce-125">Scenari per l'uso dello strumento di diagnostica</span><span class="sxs-lookup"><span data-stu-id="0b7ce-125">Scenarios to use the diagnostics tool</span></span>

<span data-ttu-id="0b7ce-126">Usare lo strumento di diagnostica per risolvere i problemi relativi alla rete, alle prestazioni, al sistema e all'integrità dei componenti hardware del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-126">Use the diagnostics tool to troubleshoot the network, performance, system, and hardware health of the system.</span></span> <span data-ttu-id="0b7ce-127">Di seguito sono riportati alcuni scenari possibili:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="0b7ce-128">**Dispositivo offline**: il dispositivo StorSimple serie 8000 è offline.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="0b7ce-129">Tuttavia, dall'interfaccia di Windows PowerShell sembra che entrambi i controller siano operativi.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-129">However, from the Windows PowerShell interface, it seems that both the controllers are up and running.</span></span>
    * <span data-ttu-id="0b7ce-130">È possibile usare lo strumento di diagnostica per determinare lo stato della rete.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-130">You can use this tool to then determine the network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="0b7ce-131">Non usare lo strumento per valutare le impostazioni delle prestazioni e della rete in un dispositivo prima della registrazione o della configurazione tramite l'installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-131">Do not use this tool to assess performance and network settings on a device before the registration (or configuring via setup wizard).</span></span> <span data-ttu-id="0b7ce-132">Durante la registrazione e l'installazione guidata, al dispositivo viene assegnato un indirizzo IP valido.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-132">A valid IP is assigned to the device during setup wizard and registration.</span></span> <span data-ttu-id="0b7ce-133">In un dispositivo non registrato è possibile eseguire questo cmdlet per valutare il sistema e l'integrità dell'hardware.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="0b7ce-134">Usare il parametro di ambito, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-134">Use the scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="0b7ce-135">**Problemi persistenti del dispositivo**: i problemi del dispositivo sembrano persistere.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-135">**Persistent device issues** - You are experiencing device issues that seem to persist.</span></span> <span data-ttu-id="0b7ce-136">Ad esempio, la registrazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-136">For instance, registration is failing.</span></span> <span data-ttu-id="0b7ce-137">I problemi possono verificarsi anche dopo che il dispositivo è stato registrato e ha funzionato per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-137">You could also be experiencing device issues after the device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="0b7ce-138">In tal caso, è possibile usare lo strumento di diagnostica per risolvere i problemi prima di inviare una richiesta di servizio al supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="0b7ce-139">È consigliabile eseguire lo strumento e acquisirne l'output,</span><span class="sxs-lookup"><span data-stu-id="0b7ce-139">We recommend that you run this tool and capture the output of this tool.</span></span> <span data-ttu-id="0b7ce-140">per inviarlo al supporto tecnico e accelerare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-140">You can then provide this output to Support to expedite troubleshooting.</span></span>
    * <span data-ttu-id="0b7ce-141">In caso di problemi relativi ai componenti hardware o ai cluster, è necessario inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="0b7ce-142">**Prestazioni ridotte del dispositivo**: il dispositivo StorSimple è lento.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="0b7ce-143">In tal caso, eseguire il cmdlet con il parametro di ambito impostato sulle prestazioni</span><span class="sxs-lookup"><span data-stu-id="0b7ce-143">In this case, run this cmdlet with scope parameter set to performance.</span></span> <span data-ttu-id="0b7ce-144">e analizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-144">Analyze the output.</span></span> <span data-ttu-id="0b7ce-145">Vengono restituite le latenze di lettura/scrittura nel cloud.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-145">You get the cloud read-write latencies.</span></span> <span data-ttu-id="0b7ce-146">Usare le latenze segnalate come obiettivo massimo raggiungibile, tenere conto dell'overhead per l'elaborazione dei dati interna e quindi distribuire i carichi di lavoro nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-146">Use the reported latencies as maximum achievable target, factor in some overhead for the internal data processing, and then deploy the workloads on the system.</span></span> <span data-ttu-id="0b7ce-147">Per altre informazioni, vedere la sezione [Test della rete](#network-test).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-147">For more information, go to [Use the network test to troubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="0b7ce-148">Test di diagnostica e output di esempio</span><span class="sxs-lookup"><span data-stu-id="0b7ce-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="0b7ce-149">Test dell'hardware</span><span class="sxs-lookup"><span data-stu-id="0b7ce-149">Hardware test</span></span>

<span data-ttu-id="0b7ce-150">Questo test determina lo stato dei componenti hardware, del firmware USM e del firmware del disco in esecuzione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-150">This test determines the status of the hardware components, the USM firmware, and the disk firmware running on your system.</span></span>

* <span data-ttu-id="0b7ce-151">I componenti hardware segnalati sono quelli che non hanno superato il test o non sono presenti nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-151">The hardware components reported are those components that failed the test or are not present in the system.</span></span>
* <span data-ttu-id="0b7ce-152">Le versioni del firmware USM e del firmware del disco vengono segnalate per il Controller 0, il Controller 1 e i componenti condivisi nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-152">The USM firmware and disk firmware versions are reported for the Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="0b7ce-153">Per un elenco completo dei componenti hardware, vedere:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="0b7ce-154">Componenti nello chassis principale</span><span class="sxs-lookup"><span data-stu-id="0b7ce-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="0b7ce-155">Componenti nello chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="0b7ce-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="0b7ce-156">Se il test dell'hardware segnala componenti con errori, [inviare una richiesta di servizio al supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-156">If the hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="0b7ce-157">Output di esempio del test dell'hardware per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="0b7ce-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="0b7ce-158">Di seguito è riportato un output di esempio per un dispositivo StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="0b7ce-159">Nel dispositivo modello 8100, lo chassis EBOD non è presente.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-159">In the 8100 model device, the EBOD enclosure is not present.</span></span> <span data-ttu-id="0b7ce-160">Di conseguenza, i componenti del controller EBOD non vengono segnalati.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-160">Hence, the EBOD controller components are not reported.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Hardware
Running hardware diagnostics ...
--------------------------------------------------
Hardware components failed or not present
----------------------

           Type           State      Controller           Index     EnclosureId
           ----           -----      ----------           -----     -----------
...rVipResource      NotPresent            None               1            None
...rVipResource      NotPresent            None               2            None
...rVipResource      NotPresent            None               3            None
...rVipResource      NotPresent            None               4            None
...rVipResource      NotPresent            None               5            None
...rVipResource      NotPresent            None               6            None
...rVipResource      NotPresent            None               7            None
...rVipResource      NotPresent            None               8            None
...rVipResource      NotPresent            None               9            None
...rVipResource      NotPresent            None              10            None
...rVipResource      NotPresent            None              11            None

Firmware information
----------------------
TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

TalladegaController : ActiveBIOS:0.45.0010
                      BackupBIOS:0.45.0006
                      MainCPLD:17.0.000b
                      ActiveBMCRoot:2.0.001F
                      BackupBMCRoot:2.0.001F
                      BMCBoot:2.0.0002
                      LsiFirmware:20.00.04.00
                      LsiBios:07.37.00.00
                      Battery1Firmware:06.2C
                      Battery2Firmware:06.2C
                      DomFirmware:X231600
                      CanisterFirmware:3.5.0.56
                      CanisterBootloader:5.03
                      CanisterConfigCRC:0x9134777A
                      CanisterVPDStructure:0x06
                      CanisterGEMCPLD:0x19
                      CanisterVPDCRC:0x142F7DC2
                      MidplaneVPDStructure:0x0C
                      MidplaneVPDCRC:0xA6BD4F64
                      MidplaneCPLD:0x10
                      PCM1Firmware:1.00|1.05
                      PCM1VPDStructure:0x05
                      PCM1VPDCRC:0x41BEF99C
                      PCM2Firmware:1.00|1.05
                      PCM2VPDStructure:0x05
                      PCM2VPDCRC:0x41BEF99C

EbodController      :
DisksFirmware       : SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      SmrtStor:TXA2D20400GA6XYR:KZ50
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08
                      WD:WD4001FYYG-01SL3:VR08

--------------------------------------------------
```

### <a name="system-test"></a><span data-ttu-id="0b7ce-161">Test del sistema</span><span class="sxs-lookup"><span data-stu-id="0b7ce-161">System test</span></span>

<span data-ttu-id="0b7ce-162">Questo test restituisce informazioni sul sistema, sul cluster e sul servizio per il dispositivo, nonché gli aggiornamenti disponibili.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-162">This test reports the system information, the updates available, the cluster information, and the service information for your device.</span></span>

* <span data-ttu-id="0b7ce-163">Le informazioni sul sistema includono il modello, il numero di serie del dispositivo, il fuso orario, lo stato del controller e i dettagli sulla versione del software in esecuzione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-163">The system information includes the model, device serial number, time zone, controller status, and the detailed software version running on the system.</span></span> <span data-ttu-id="0b7ce-164">Per comprendere i vari parametri di sistema segnalati come output, vedere l'[Appendice: interpretazione delle informazioni sul sistema](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-164">To understand the various system parameters reported as the output, go to [Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="0b7ce-165">La disponibilità di aggiornamenti segnala se la modalità normale e la modalità di manutenzione sono disponibili e i relativi nomi di pacchetto associati.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-165">The update availability reports whether the regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="0b7ce-166">Se `RegularUpdates` e `MaintenanceModeUpdates` sono `false`, non sono disponibili aggiornamenti</span><span class="sxs-lookup"><span data-stu-id="0b7ce-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that the updates are not available.</span></span> <span data-ttu-id="0b7ce-167">e il dispositivo è già aggiornato.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="0b7ce-168">Le informazioni sul cluster contengono informazioni su vari componenti logici di tutti i gruppi di cluster HCS e i rispettivi stati.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-168">The cluster information contains the information on various logical components of all the HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="0b7ce-169">Se in questa sezione del report è presente un gruppo di cluster offline, [contattare il supporto tecnico Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-169">If you see an offline cluster group in this section of the report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="0b7ce-170">Le informazioni sul servizio includono i nomi e gli stati di tutti i servizi CiS e HCS in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-170">The service information includes the names and statuses of all the HCS and CiS services running on your device.</span></span> <span data-ttu-id="0b7ce-171">Queste informazioni sono utili per il supporto tecnico Microsoft nella risoluzione dei problemi del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-171">This information is helpful for the Microsoft Support in troubleshooting the device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="0b7ce-172">Output di esempio del test del sistema per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="0b7ce-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="0b7ce-173">Di seguito è riportato un output di esempio del test del sistema per un dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-173">Here is a sample output of the system test run on an 8100 device.</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope System
Running system diagnostics ...
--------------------------------------------------

System information
----------------------
Controller0:

InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                : (UTC-08:00) Pacific Time (US & Canada)
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : Disabled
FipsMode                : Enabled

Controller1:
InstanceId              : 7382407f-a56b-4622-8f3f-756fe04cfd38
Name                    : 8100-SHX0991003G467K
Model                   : 8100
SerialNumber            : SHX0991003G467K
TimeZone                :
CurrentController       : Controller0
ActiveController        : Controller0
Controller0Status       : Normal
Controller1Status       : Normal
SystemMode              : Normal
FriendlySoftwareVersion : StorSimple 8000 Series Update 4.0
HcsSoftwareVersion      : 6.3.9600.17820
ApiVersion              : 9.0.0.0
VhdVersion              : 6.3.9600.17759
OSVersion               : 6.3.9600.0
CisAgentVersion         : 1.0.9441.0
MdsAgentVersion         : 35.2.2.0
Lsisas2Version          : 2.0.78.0
Capacity                : 219902325555200
RemoteManagementMode    : HttpsAndHttpEnabled
FipsMode                : Enabled

Update availability
----------------------
RegularUpdates              : False
MaintenanceModeUpdates      : False
RegularUpdatesTitle         : {}
MaintenanceModeUpdatesTitle : {}

Cluster information
----------------------
Name                          State OwnerGroup
----                          ----- ----------
ApplicationHostRLUA           Online HCS Cluster Group
Data0v4                       Online HCS Cluster Group
HCS Vnic Resource             Online HCS Cluster Group
hcs_cloud_connectivity_...    Online HCS Cluster Group
hcs_controller_replacement    Online HCS Cluster Group
hcs_datapath_service          Online HCS Cluster Group
hcs_management_servic         Online HCS Cluster Group
hcs_nvram_service             Online HCS Cluster Group
hcs_passive_datapath          Online HCS Passive Cluster Group
hcs_platform_service          Online HCS Cluster Group
hcs_saas_agent_service        Online HCS Cluster Group
HddDataClusterDisk            Online HCS Cluster Group
HddMgmtClusterDisk            Online HCS Cluster Group
HddReplClusterDisk            Online HCS Cluster Group
iSCSI Target Server           Online HCS Cluster Group
NvramClusterDisk              Online HCS Cluster Group
SSAdminRLUA                   Online HCS Cluster Group
SsdDataClusterDisk            Online HCS Cluster Group
SsdNvramClusterDisk           Online HCS Cluster Group

Service information
----------------------
Name                                          Status DisplayName
----                                          ------ -----------
CiSAgentSvc                                   Stopped CiS Service Agent
hcs_cloud_connectivity_...                    Running hcs_cloud_connectivity...
hcs_controller_replacement                    Running HCS Controller Replace...
hcs_datapath_service                          Running HCS Datapath Service
hcs_management_service                        Running HCS Management Service
hcs_minishell                                 Running hcs_minishell
HCS_NVRAM_Service                             Running HCS NVRAM Service
hcs_passive_datapath                          Stopped HCS Passive Datapath S...
hcs_platform_service                          Running HCS Platform Monitor S...
hcs_saas_agent_service                        Running hcs_saas_agent_service
hcs_startup                                   Stopped hcs_startup
--------------------------------------------------
```

### <a name="network-test"></a><span data-ttu-id="0b7ce-174">Test della rete</span><span class="sxs-lookup"><span data-stu-id="0b7ce-174">Network test</span></span>

<span data-ttu-id="0b7ce-175">Questo test verifica lo stato di interfacce di rete, porte, connettività del server NTP e DNS, certificato SSL, credenziali dell'account di archiviazione, connettività ai server di aggiornamento e connettività del proxy Web nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-175">This test validates the status of the network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity to the Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="0b7ce-176">Esempio di output del test della rete quando è abilitata solo l'interfaccia di rete DATA0</span><span class="sxs-lookup"><span data-stu-id="0b7ce-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="0b7ce-177">Di seguito è riportato un output di esempio per il dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-177">Here is a sample output of the 8100 device.</span></span> <span data-ttu-id="0b7ce-178">L'output mostra quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-178">You can see in the output that:</span></span>
* <span data-ttu-id="0b7ce-179">Solo le interfacce di rete DATA0 e DATA1 sono abilitate e configurate.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="0b7ce-180">Le interfacce da DATA2 a DATA5 non sono abilitate nel portale.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-180">DATA 2 - 5 are not enabled in the portal.</span></span>
* <span data-ttu-id="0b7ce-181">La configurazione del server DNS è valida e il dispositivo può connettersi tramite il server DNS.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-181">The DNS server configuration is valid and the device can connect via the DNS server.</span></span>
* <span data-ttu-id="0b7ce-182">La connettività del server NTP è valida.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-182">The NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="0b7ce-183">Le porte 80 e 443 sono aperte,</span><span class="sxs-lookup"><span data-stu-id="0b7ce-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="0b7ce-184">ma la porta 9354 è bloccata.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="0b7ce-185">In base ai [requisiti di rete del sistema](storsimple-system-requirements.md), questa porta deve essere aperta per la comunicazione del bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-185">Based on the [system network requirements](storsimple-system-requirements.md), you need to open this port for the service bus communication.</span></span>
* <span data-ttu-id="0b7ce-186">Il certificato SSL è valido.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-186">The SSL certification is valid.</span></span>
* <span data-ttu-id="0b7ce-187">Il dispositivo può connettersi all'account di archiviazione _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-187">The device can connect to the storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="0b7ce-188">La connettività ai server di aggiornamento è valida.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-188">The connectivity to Update servers is valid.</span></span>
* <span data-ttu-id="0b7ce-189">Il proxy Web non è configurato in questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-189">The web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="0b7ce-190">Esempio di output del test della rete quando sono abilitate le interfacce di rete DATA0 e DATA1</span><span class="sxs-lookup"><span data-stu-id="0b7ce-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Network
Running network diagnostics ....
--------------------------------------------------
Validating networks .....
Name                Entity              Result              Details
----                ------              ------              -------
Network interface   Data0               Valid
Network interface   Data1               Valid
Network interface   Data2               Not enabled
Network interface   Data3               Not enabled
Network interface   Data4               Not enabled
Network interface   Data5               Not enabled
DNS                 10.222.118.154      Valid
NTP                 time.windows.com    Valid
Port                80                  Open
Port                443                 Open
Port                9354                Blocked
SSL certificate     https://myss8000... Valid
Storage account ... myss8000storageacct Valid
URL                 http://download.... Valid
URL                 http://download.... Valid
Web proxy                               Not enabled         Web proxy is not...
--------------------------------------------------
```

### <a name="performance-test"></a><span data-ttu-id="0b7ce-191">Test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="0b7ce-191">Performance test</span></span>

<span data-ttu-id="0b7ce-192">Questo test restituisce le prestazioni del cloud tramite le latenze di lettura/scrittura nel cloud per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-192">This test reports the cloud performance via the cloud read-write latencies for your device.</span></span> <span data-ttu-id="0b7ce-193">È possibile usare lo strumento di diagnostica per stabilire una baseline per le prestazioni del cloud raggiungibili con StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-193">This tool can be used to establish a baseline of the cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="0b7ce-194">Lo strumento indica le prestazioni massime, ovvero lo scenario migliore per le latenze di lettura/scrittura, che è possibile ottenere per la connessione.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-194">The tool reports the maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="0b7ce-195">Dal momento che lo strumento segnala le prestazioni massime raggiungibili, è possibile usare le latenze di lettura/scrittura indicate come obiettivo nella distribuzione dei carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-195">As the tool reports the maximum achievable performance, we can use the reported read-write latencies as targets when deploying the workloads.</span></span>

<span data-ttu-id="0b7ce-196">Il test simula le dimensioni dei BLOB associati ai vari tipi di volume nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-196">The test simulates the blob sizes associated with the different volume types on the device.</span></span> <span data-ttu-id="0b7ce-197">I normali volumi a livelli e i backup dei volumi aggiunti in locale usano dimensioni del BLOB pari a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="0b7ce-198">I volumi a livelli con l'opzione di archiviazione selezionata usano dimensioni del BLOB pari a 512 KB.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="0b7ce-199">Se il dispositivo contiene volumi a livelli e volumi aggiunti in locale configurati, viene eseguito solo il test corrispondente alle dimensioni del BLOB di 64 KB.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-199">If your device has tiered and locally pinned volumes configured, only the test corresponding to 64 KB blob data size is run.</span></span>

<span data-ttu-id="0b7ce-200">Per usare lo strumento di diagnostica, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-200">To use this tool, perform the following steps:</span></span>

1.  <span data-ttu-id="0b7ce-201">Creare prima di tutto una combinazione di volumi a livelli e volumi a livelli con l'opzione di archiviazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="0b7ce-202">Questa azione assicura l'esecuzione dei test per entrambe le dimensioni del BLOB, 64 KB e 512 KB.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-202">This action ensures that the tool runs the tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="0b7ce-203">Eseguire il cmdlet dopo aver creato e configurato i volumi.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-203">Run the cmdlet after you have created and configured the volumes.</span></span> <span data-ttu-id="0b7ce-204">Digitare:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="0b7ce-205">Annotare le latenze di lettura/scrittura segnalate dallo strumento.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-205">Make a note of the read-write latencies reported by the tool.</span></span> <span data-ttu-id="0b7ce-206">Con questo test possono essere necessari alcuni minuti prima che vengano restituiti i risultati.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-206">This test can take several minutes to run before it reports the results.</span></span>

4. <span data-ttu-id="0b7ce-207">Se le latenze di connessione sono tutte comprese nell'intervallo previsto, è possibile usare le latenze segnalate dallo strumento come obiettivo massimo raggiungibile nella distribuzione dei carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-207">If the connection latencies are all under the expected range, then the latencies reported by the tool can be used as maximum achievable target when deploying the workloads.</span></span> <span data-ttu-id="0b7ce-208">Tenere conto dell'overhead per l'elaborazione dei dati interna.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="0b7ce-209">Se le latenze di lettura/scrittura segnalate dallo strumento di diagnostica sono elevate:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-209">If the read-write latencies reported by the diagnostics tool are high:</span></span>

    1. <span data-ttu-id="0b7ce-210">Configurare Analisi archiviazione per i servizi BLOB e analizzare l'output per ottenere informazioni sulle latenze per l'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-210">Configure Storage Analytics for blob services and analyze the output to understand the latencies for the Azure storage account.</span></span> <span data-ttu-id="0b7ce-211">Per istruzioni dettagliate, vedere come [abilitare e configurare Analisi archiviazione](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-211">For detailed instructions, go to [enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="0b7ce-212">Se anche tali latenze sono elevate, con valori analoghi a quelli restituiti dallo strumento di diagnostica StorSimple, è necessario inviare una richiesta di servizio tramite Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-212">If those latencies are also high and comparable to the numbers you received from the StorSimple Diagnostics tool, then you need to log a service request with Azure storage.</span></span>

    2. <span data-ttu-id="0b7ce-213">Se le latenze dell'account di archiviazione sono basse, contattare l'amministratore di rete per indagare su eventuali problemi di latenza della rete.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-213">If the storage account latencies are low, contact your network administrator to investigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="0b7ce-214">Output di esempio del test delle prestazioni per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="0b7ce-214">Sample output of performance test run on an 8100 device</span></span>

```
Controller0>Invoke-HcsDiagnostics -Scope Performance
Running performance diagnostics...
--------------------------------------------------
Cloud performance: writing blobs
Cloud write latency: 194 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: reading blobs..
Cloud read latency: 544 ms using credential 'myss8000storageacct', blob size '64KB'
Cloud performance: writing blobs.
Cloud write latency: 369 ms using credential 'myss8000storageacct', blob size '512KB'
Cloud performance: reading blobs...
Cloud read latency: 4924 ms using credential 'myss8000storageacct', blob size '512KB'
--------------------------------------------------
Controller0>
```

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="0b7ce-215">Appendice: interpretazione delle informazioni sul sistema</span><span class="sxs-lookup"><span data-stu-id="0b7ce-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="0b7ce-216">La tabella riportata di seguito illustra il mapping dei vari parametri di Windows PowerShell alle informazioni sul sistema.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-216">Here is a table describing what the various Windows PowerShell parameters in the system information map to.</span></span> 

| <span data-ttu-id="0b7ce-217">Parametro di PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b7ce-217">PowerShell Parameter</span></span>    | <span data-ttu-id="0b7ce-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="0b7ce-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="0b7ce-219">ID istanza</span><span class="sxs-lookup"><span data-stu-id="0b7ce-219">Instance ID</span></span>             | <span data-ttu-id="0b7ce-220">Ogni controller è associato a un identificatore univoco o un GUID.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="0b7ce-221">Nome</span><span class="sxs-lookup"><span data-stu-id="0b7ce-221">Name</span></span>                    | <span data-ttu-id="0b7ce-222">Nome descrittivo del dispositivo configurato tramite il portale di Azure durante la distribuzione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-222">The friendly name of the device as configured through the Azure portal during device deployment.</span></span> <span data-ttu-id="0b7ce-223">Il nome descrittivo predefinito è il numero di serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-223">The default friendly name is the device serial number.</span></span> |
| <span data-ttu-id="0b7ce-224">Modello</span><span class="sxs-lookup"><span data-stu-id="0b7ce-224">Model</span></span>                   | <span data-ttu-id="0b7ce-225">Modello del dispositivo StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-225">The model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="0b7ce-226">Il modello può essere 8100 o 8600.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-226">The model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="0b7ce-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="0b7ce-227">SerialNumber</span></span>            | <span data-ttu-id="0b7ce-228">Numero di serie di 15 caratteri assegnato in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-228">The device serial number is assigned at the factory and is 15 characters long.</span></span> <span data-ttu-id="0b7ce-229">Ad esempio, 8600-SHX0991003G44HT indica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0b7ce-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="0b7ce-230">8600: modello del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-230">8600 – Is the device model.</span></span><br><span data-ttu-id="0b7ce-231">SHX: sito di produzione.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-231">SHX – Is the manufacturing site.</span></span><br> <span data-ttu-id="0b7ce-232">0991003: prodotto specifico.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="0b7ce-233">G44HT: ultime cinque cifre incrementate per creare numeri di serie univoci.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-233">G44HT- the last 5 digits are incremented to create unique serial numbers.</span></span> <span data-ttu-id="0b7ce-234">Questo potrebbe non essere un insieme sequenziale.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="0b7ce-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="0b7ce-235">TimeZone</span></span>                | <span data-ttu-id="0b7ce-236">Fuso orario del dispositivo configurato nel portale di Azure durante la distribuzione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-236">The device time zone as configured in the Azure portal during device deployment.</span></span>|
| <span data-ttu-id="0b7ce-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="0b7ce-237">CurrentController</span></span>       | <span data-ttu-id="0b7ce-238">Controller a cui si è connessi tramite l'interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-238">The controller that you are connected to through the Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="0b7ce-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="0b7ce-239">ActiveController</span></span>        | <span data-ttu-id="0b7ce-240">Controller attivo nel dispositivo che controlla tutte le operazioni di rete e sul disco.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-240">The controller that is active on your device and is controlling all the network and disk operations.</span></span> <span data-ttu-id="0b7ce-241">Può trattarsi del Controller 0 o del Controller 1.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="0b7ce-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="0b7ce-242">Controller0Status</span></span>       | <span data-ttu-id="0b7ce-243">Stato del Controller 0 nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-243">The status of Controller 0 on your device.</span></span> <span data-ttu-id="0b7ce-244">Lo stato del controller può essere normale, in modalità di ripristino o non raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-244">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="0b7ce-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="0b7ce-245">Controller1Status</span></span>       | <span data-ttu-id="0b7ce-246">Stato del Controller 1 nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-246">The status of Controller 1 on your device.</span></span>  <span data-ttu-id="0b7ce-247">Lo stato del controller può essere normale, in modalità di ripristino o non raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-247">The controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="0b7ce-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="0b7ce-248">SystemMode</span></span>              | <span data-ttu-id="0b7ce-249">Stato generale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-249">The overall status of your StorSimple device.</span></span> <span data-ttu-id="0b7ce-250">Lo stato del dispositivo può essere normale, manutenzione, o autorizzazioni rimosse, che corrisponde a disattivato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-250">The device status can be normal, maintenance, or decommissioned (corresponds to deactivated in the Azure portal).</span></span>|
| <span data-ttu-id="0b7ce-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="0b7ce-252">Stringa descrittiva che corrisponde alla versione del software del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-252">The friendly string that corresponds to the device software version.</span></span> <span data-ttu-id="0b7ce-253">Per un sistema che esegue l'aggiornamento 4, la stringa descrittiva del software sarà Aggiornamento 4.0 di StorSimple serie 8000.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-253">For a system running Update 4, the friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="0b7ce-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="0b7ce-255">Versione del software HCS in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-255">The HCS software version running on your device.</span></span> <span data-ttu-id="0b7ce-256">Ad esempio, la versione del software HCS corrispondente all'aggiornamento 4.0 di StorSimple serie 8000 è 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-256">For instance, the HCS software version corresponding to StorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="0b7ce-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-257">ApiVersion</span></span>              | <span data-ttu-id="0b7ce-258">Versione del software dell'API di Windows PowerShell nel dispositivo HCS.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-258">The software version of the Windows PowerShell API of the HCS device.</span></span>|
| <span data-ttu-id="0b7ce-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-259">VhdVersion</span></span>              | <span data-ttu-id="0b7ce-260">Versione del software dell'immagine produttore computer fornita con il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-260">The software version of the factory image that the device was shipped with.</span></span> <span data-ttu-id="0b7ce-261">Se si ripristinano le impostazioni predefinite del dispositivo, viene eseguita questa versione del software.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-261">If you reset your device to factory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="0b7ce-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-262">OSVersion</span></span>               | <span data-ttu-id="0b7ce-263">Versione del software del sistema operativo Windows Server in esecuzione nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-263">The software version of the Windows Server operating system running on the device.</span></span> <span data-ttu-id="0b7ce-264">Il dispositivo StorSimple si basa su Windows Server 2012 R2 che corrisponde a 6.3.9600.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-264">The StorSimple device is based off the Windows Server 2012 R2 that corresponds to 6.3.9600.</span></span>|
| <span data-ttu-id="0b7ce-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-265">CisAgentVersion</span></span>         | <span data-ttu-id="0b7ce-266">Versione dell'agente CiS in esecuzione nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-266">The version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="0b7ce-267">Questo agente consente di comunicare con il servizio StorSimple Manager in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-267">This agent helps communicate with the StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="0b7ce-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="0b7ce-268">MdsAgentVersion</span></span>         | <span data-ttu-id="0b7ce-269">Versione corrispondente all'agente MDS in esecuzione nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-269">The version corresponding to the Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="0b7ce-270">Questo agente sposta i dati verso il servizio di monitoraggio e diagnostica (MDS).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-270">This agent moves data to the Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="0b7ce-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="0b7ce-271">Lsisas2Version</span></span>          | <span data-ttu-id="0b7ce-272">Versione corrispondente ai driver LSI nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-272">The version corresponding to the LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="0b7ce-273">Capacità</span><span class="sxs-lookup"><span data-stu-id="0b7ce-273">Capacity</span></span>                | <span data-ttu-id="0b7ce-274">Capacità totale del dispositivo espressa in byte.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-274">The total capacity of the device in bytes.</span></span>|
| <span data-ttu-id="0b7ce-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="0b7ce-275">RemoteManagementMode</span></span>    | <span data-ttu-id="0b7ce-276">Indica se il dispositivo può essere gestito in remoto tramite la relativa interfaccia di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-276">Indicates whether the device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="0b7ce-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="0b7ce-277">FipsMode</span></span>                | <span data-ttu-id="0b7ce-278">Indica se la modalità FIPS (Federal Information Processing Standard per gli Stati Uniti) è abilitata nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-278">Indicates whether the United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="0b7ce-279">Lo standard FIPS 140 definisce gli algoritmi di crittografia approvati per l'uso da parte dei sistemi del governo federale degli Stati Uniti per la protezione dei dati sensibili.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-279">The FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for the protection of sensitive data.</span></span> <span data-ttu-id="0b7ce-280">Per i dispositivi che eseguono l'aggiornamento 4 o versione successiva, la modalità FIPS è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b7ce-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0b7ce-281">Next steps</span></span>

* <span data-ttu-id="0b7ce-282">Informazioni sulla [sintassi del cmdlet Invoke-HcsDiagnostics](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b7ce-282">Learn the [syntax of the Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="0b7ce-283">Altre informazioni sulla [risoluzione dei problemi di distribuzione](storsimple-troubleshoot-deployment.md) nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0b7ce-283">Learn more about how to [troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
