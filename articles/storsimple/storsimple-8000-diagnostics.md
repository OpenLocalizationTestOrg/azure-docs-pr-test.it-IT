---
title: dispositivo di StorSimple 8000 tootroubleshoot strumento aaaDiagnostics | Documenti Microsoft
description: "Modalità del dispositivo StorSimple hello descrive e illustra come toouse Windows PowerShell per StorSimple toochange hello modalità del dispositivo."
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
ms.openlocfilehash: e8b7fdbc44d2533973b63da841335ba73ba0014b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-diagnostics-tool-tootroubleshoot-8000-series-device-issues"></a><span data-ttu-id="51624-103">Utilizzare hello lo strumento di diagnostica StorSimple tootroubleshoot 8000 series problemi dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="51624-103">Use hello StorSimple Diagnostics Tool tootroubleshoot 8000 series device issues</span></span>

## <a name="overview"></a><span data-ttu-id="51624-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="51624-104">Overview</span></span>

<span data-ttu-id="51624-105">lo strumento di diagnostica StorSimple Hello individua problemi correlati toosystem, prestazioni, rete e lo stato di componenti hardware per un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-105">hello StorSimple Diagnostics tool diagnoses issues related toosystem, performance, network, and hardware component health for a StorSimple device.</span></span> <span data-ttu-id="51624-106">strumento di diagnostica Hello può essere utilizzato in scenari diversi.</span><span class="sxs-lookup"><span data-stu-id="51624-106">hello diagnostics tool can be used in various scenarios.</span></span> <span data-ttu-id="51624-107">Questi scenari includono la pianificazione del carico di lavoro, la distribuzione di un dispositivo StorSimple, valutare l'ambiente di rete hello e determinare le prestazioni di un dispositivo operativo hello.</span><span class="sxs-lookup"><span data-stu-id="51624-107">These scenarios include workload planning, deploying a StorSimple device, assessing hello network environment, and determining hello performance of an operational device.</span></span> <span data-ttu-id="51624-108">In questo articolo viene fornita una panoramica dello strumento di diagnostica hello e viene descritto come utilizzare lo strumento hello con un dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-108">This article provides an overview of hello diagnostics tool and describes how hello tool can be used with a StorSimple device.</span></span>

<span data-ttu-id="51624-109">lo strumento di diagnostica Hello viene usata principalmente per i dispositivi locali serie StorSimple 8000 (8100 e 8600).</span><span class="sxs-lookup"><span data-stu-id="51624-109">hello diagnostics tool is primarily intended for StorSimple 8000 series on-premises devices (8100 and 8600).</span></span>

## <a name="run-diagnostics-tool"></a><span data-ttu-id="51624-110">Eseguire lo strumento di diagnostica</span><span class="sxs-lookup"><span data-stu-id="51624-110">Run diagnostics tool</span></span>

<span data-ttu-id="51624-111">Questo strumento può essere eseguito tramite l'interfaccia di Windows PowerShell hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-111">This tool can be run via hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="51624-112">Esistono due modi tooaccess hello interfaccia locale del dispositivo:</span><span class="sxs-lookup"><span data-stu-id="51624-112">There are two ways tooaccess hello local interface of your device:</span></span>

* <span data-ttu-id="51624-113">[Console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="51624-113">[Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
* <span data-ttu-id="51624-114">[Accedere in remoto lo strumento hello tramite hello Windows PowerShell per StorSimple](storsimple-remote-connect.md).</span><span class="sxs-lookup"><span data-stu-id="51624-114">[Remotely access hello tool via hello Windows PowerShell for StorSimple](storsimple-remote-connect.md).</span></span>

<span data-ttu-id="51624-115">In questo articolo si presuppone che si è connessi toohello console seriale del dispositivo tramite PuTTY.</span><span class="sxs-lookup"><span data-stu-id="51624-115">In this article, we assume that you have connected toohello device serial console via PuTTY.</span></span>

#### <a name="toorun-hello-diagnostics-tool"></a><span data-ttu-id="51624-116">strumento di diagnostica hello toorun</span><span class="sxs-lookup"><span data-stu-id="51624-116">toorun hello diagnostics tool</span></span>

<span data-ttu-id="51624-117">Dopo avere connesso toohello interfaccia di Windows PowerShell del dispositivo hello, eseguire hello seguendo i passaggi toorun hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="51624-117">Once you have connected toohello Windows PowerShell interface of hello device, perform hello following steps toorun hello cmdlet.</span></span>
1. <span data-ttu-id="51624-118">Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="51624-118">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>

2. <span data-ttu-id="51624-119">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="51624-119">Type hello following command:</span></span>

    `Invoke-HcsDiagnostics`

    <span data-ttu-id="51624-120">Se non è stato specificato il parametro di ambito hello, hello cmdlet esegue tutti i test diagnostici hello.</span><span class="sxs-lookup"><span data-stu-id="51624-120">If hello scope parameter is not specified, hello cmdlet executes all hello diagnostic tests.</span></span> <span data-ttu-id="51624-121">I test riguardano il sistema, l'integrità dei componenti hardware, la rete e le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="51624-121">These tests include system, hardware component health, network, and performance.</span></span> 
    
    <span data-ttu-id="51624-122">toorun solo un test specifico, specificare il parametro di ambito hello.</span><span class="sxs-lookup"><span data-stu-id="51624-122">toorun only a specific test, specify hello scope parameter.</span></span> <span data-ttu-id="51624-123">Ad esempio, toorun solo hello test di rete, tipo</span><span class="sxs-lookup"><span data-stu-id="51624-123">For instance, toorun only hello network test, type</span></span>

    `Invoke-HcsDiagnostics -Scope Network`

3. <span data-ttu-id="51624-124">Selezionare e copiare l'output di hello dal hello PuTTY finestra in un file di testo per un'ulteriore analisi.</span><span class="sxs-lookup"><span data-stu-id="51624-124">Select and copy hello output from hello PuTTY window into a text file for further analysis.</span></span>

## <a name="scenarios-toouse-hello-diagnostics-tool"></a><span data-ttu-id="51624-125">Strumento di diagnostica di scenari toouse hello</span><span class="sxs-lookup"><span data-stu-id="51624-125">Scenarios toouse hello diagnostics tool</span></span>

<span data-ttu-id="51624-126">Utilizzare hello diagnostica strumento tootroubleshoot hello rete, le prestazioni, sistema e hardware integrità del sistema hello.</span><span class="sxs-lookup"><span data-stu-id="51624-126">Use hello diagnostics tool tootroubleshoot hello network, performance, system, and hardware health of hello system.</span></span> <span data-ttu-id="51624-127">Di seguito sono riportati alcuni scenari possibili:</span><span class="sxs-lookup"><span data-stu-id="51624-127">Here are some possible scenarios:</span></span>

* <span data-ttu-id="51624-128">**Dispositivo offline**: il dispositivo StorSimple serie 8000 è offline.</span><span class="sxs-lookup"><span data-stu-id="51624-128">**Device offline** - Your StorSimple 8000 series device is offline.</span></span> <span data-ttu-id="51624-129">Tuttavia, dall'interfaccia di Windows PowerShell hello, ci risulta che entrambi i controller hello siano in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="51624-129">However, from hello Windows PowerShell interface, it seems that both hello controllers are up and running.</span></span>
    * <span data-ttu-id="51624-130">È possibile utilizzare questo strumento toothen determinare lo stato di rete hello.</span><span class="sxs-lookup"><span data-stu-id="51624-130">You can use this tool toothen determine hello network state.</span></span>
         
         > [!NOTE]
         > <span data-ttu-id="51624-131">Non utilizzare questo tooassess prestazioni e le impostazioni di rete in un dispositivo prima della registrazione hello (o la configurazione tramite installazione guidata).</span><span class="sxs-lookup"><span data-stu-id="51624-131">Do not use this tool tooassess performance and network settings on a device before hello registration (or configuring via setup wizard).</span></span> <span data-ttu-id="51624-132">Un indirizzo IP valido assegnato toohello dispositivo durante la registrazione e installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="51624-132">A valid IP is assigned toohello device during setup wizard and registration.</span></span> <span data-ttu-id="51624-133">In un dispositivo non registrato è possibile eseguire questo cmdlet per valutare il sistema e l'integrità dell'hardware.</span><span class="sxs-lookup"><span data-stu-id="51624-133">You can run this cmdlet, on a device that is not registered, for hardware health and system.</span></span> <span data-ttu-id="51624-134">Usare il parametro di ambito hello, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="51624-134">Use hello scope parameter, for example:</span></span>
         >
         > `Invoke-HcsDiagnostics -Scope Hardware`
         >
         > `Invoke-HcsDiagnostics -Scope System`

* <span data-ttu-id="51624-135">**Problemi dei dispositivi permanenti** -si verificano problemi di dispositivo che sembrano toopersist.</span><span class="sxs-lookup"><span data-stu-id="51624-135">**Persistent device issues** - You are experiencing device issues that seem toopersist.</span></span> <span data-ttu-id="51624-136">Ad esempio, la registrazione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="51624-136">For instance, registration is failing.</span></span> <span data-ttu-id="51624-137">Si può anche essere problemi dispositivo dopo dispositivo hello è operativo e registrati correttamente per un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="51624-137">You could also be experiencing device issues after hello device is successfully registered and operational for a while.</span></span>
    * <span data-ttu-id="51624-138">In tal caso, è possibile usare lo strumento di diagnostica per risolvere i problemi prima di inviare una richiesta di servizio al supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="51624-138">In this case, use this tool for preliminary troubleshooting before you log a service request with Microsoft Support.</span></span> <span data-ttu-id="51624-139">Ti consigliamo di eseguire l'output di hello strumento e acquisizione di questo strumento.</span><span class="sxs-lookup"><span data-stu-id="51624-139">We recommend that you run this tool and capture hello output of this tool.</span></span> <span data-ttu-id="51624-140">È quindi possibile fornire questo output tooSupport tooexpedite la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="51624-140">You can then provide this output tooSupport tooexpedite troubleshooting.</span></span>
    * <span data-ttu-id="51624-141">In caso di problemi relativi ai componenti hardware o ai cluster, è necessario inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="51624-141">If there are any hardware component or cluster failures, you should log in a Support request.</span></span>

* <span data-ttu-id="51624-142">**Prestazioni ridotte del dispositivo**: il dispositivo StorSimple è lento.</span><span class="sxs-lookup"><span data-stu-id="51624-142">**Low device performance** - Your StorSimple device is slow.</span></span>
    * <span data-ttu-id="51624-143">In questo caso, è possibile eseguire questo cmdlet con tooperformance set di parametri di ambito.</span><span class="sxs-lookup"><span data-stu-id="51624-143">In this case, run this cmdlet with scope parameter set tooperformance.</span></span> <span data-ttu-id="51624-144">Analizzare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-144">Analyze hello output.</span></span> <span data-ttu-id="51624-145">È possibile ottenere il cloud hello latenze di lettura / scrittura.</span><span class="sxs-lookup"><span data-stu-id="51624-145">You get hello cloud read-write latencies.</span></span> <span data-ttu-id="51624-146">Hello utilizzare segnalato latenze come destinazione raggiungibile massimo, fattore in un certo overhead per l'elaborazione dati interna hello e quindi distribuire i carichi di lavoro hello nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="51624-146">Use hello reported latencies as maximum achievable target, factor in some overhead for hello internal data processing, and then deploy hello workloads on hello system.</span></span> <span data-ttu-id="51624-147">Per ulteriori informazioni, visitare troppo[utilizzare le prestazioni del dispositivo hello rete test tootroubleshoot](#network-test).</span><span class="sxs-lookup"><span data-stu-id="51624-147">For more information, go too[Use hello network test tootroubleshoot device performance](#network-test).</span></span>


## <a name="diagnostics-test-and-sample-outputs"></a><span data-ttu-id="51624-148">Test di diagnostica e output di esempio</span><span class="sxs-lookup"><span data-stu-id="51624-148">Diagnostics test and sample outputs</span></span>

### <a name="hardware-test"></a><span data-ttu-id="51624-149">Test dell'hardware</span><span class="sxs-lookup"><span data-stu-id="51624-149">Hardware test</span></span>

<span data-ttu-id="51624-150">Questo test determina lo stato di hello di componenti hardware hello, al firmware USM hello e firmware del disco hello in esecuzione nel sistema.</span><span class="sxs-lookup"><span data-stu-id="51624-150">This test determines hello status of hello hardware components, hello USM firmware, and hello disk firmware running on your system.</span></span>

* <span data-ttu-id="51624-151">componenti hardware Hello segnalati sono i componenti di tale test hello non riuscito o non sono presenti nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="51624-151">hello hardware components reported are those components that failed hello test or are not present in hello system.</span></span>
* <span data-ttu-id="51624-152">versioni del firmware del disco e del firmware Hello USM vengono segnalate per Controller 0, 1 Controller, hello e i componenti condivisi nel sistema.</span><span class="sxs-lookup"><span data-stu-id="51624-152">hello USM firmware and disk firmware versions are reported for hello Controller 0, Controller 1, and shared components in your system.</span></span> <span data-ttu-id="51624-153">Per un elenco completo dei componenti hardware, vedere:</span><span class="sxs-lookup"><span data-stu-id="51624-153">For a complete list of hardware components, go to:</span></span>

    * [<span data-ttu-id="51624-154">Componenti nello chassis principale</span><span class="sxs-lookup"><span data-stu-id="51624-154">Components in primary enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-primary-enclosure-of-storsimple-device)
    * [<span data-ttu-id="51624-155">Componenti nello chassis EBOD</span><span class="sxs-lookup"><span data-stu-id="51624-155">Components in EBOD enclosure</span></span>](storsimple-monitor-hardware-status.md#component-list-for-ebod-enclosure-of-storsimple-device)

> [!NOTE]
> <span data-ttu-id="51624-156">Se il test dell'hardware hello segnala problemi dei componenti, [log in una richiesta di servizio con il supporto Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="51624-156">If hello hardware test reports failed components, [log in a service request with Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

#### <a name="sample-output-of-hardware-test-run-on-an-8100-device"></a><span data-ttu-id="51624-157">Output di esempio del test dell'hardware per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="51624-157">Sample output of hardware test run on an 8100 device</span></span>

<span data-ttu-id="51624-158">Di seguito è riportato un output di esempio per un dispositivo StorSimple 8100.</span><span class="sxs-lookup"><span data-stu-id="51624-158">Here is a sample output from a StorSimple 8100 device.</span></span> <span data-ttu-id="51624-159">Nel dispositivo di modello 8100 hello, hello enclosure EBOD non è presente.</span><span class="sxs-lookup"><span data-stu-id="51624-159">In hello 8100 model device, hello EBOD enclosure is not present.</span></span> <span data-ttu-id="51624-160">Di conseguenza, non vengono segnalati i componenti del controller EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="51624-160">Hence, hello EBOD controller components are not reported.</span></span>

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

### <a name="system-test"></a><span data-ttu-id="51624-161">Test del sistema</span><span class="sxs-lookup"><span data-stu-id="51624-161">System test</span></span>

<span data-ttu-id="51624-162">Questo test segnala le informazioni di sistema hello, hello gli aggiornamenti disponibili, informazioni sul cluster hello e informazioni hello del servizio per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-162">This test reports hello system information, hello updates available, hello cluster information, and hello service information for your device.</span></span>

* <span data-ttu-id="51624-163">informazioni di sistema Hello includono il modello di hello, numero di serie del dispositivo, fuso orario, lo stato del controller e versione del software dettagliate hello in esecuzione sul sistema hello.</span><span class="sxs-lookup"><span data-stu-id="51624-163">hello system information includes hello model, device serial number, time zone, controller status, and hello detailed software version running on hello system.</span></span> <span data-ttu-id="51624-164">hello toounderstand vari parametri di sistema segnalato come output di hello, andare troppo[interpretazione delle informazioni di sistema](#appendix-interpreting-system-information).</span><span class="sxs-lookup"><span data-stu-id="51624-164">toounderstand hello various system parameters reported as hello output, go too[Interpreting system information](#appendix-interpreting-system-information).</span></span>

* <span data-ttu-id="51624-165">disponibilità di aggiornamenti Hello segnala se sono disponibili le modalità normali e di manutenzione di hello e i relativi nomi di pacchetto associati.</span><span class="sxs-lookup"><span data-stu-id="51624-165">hello update availability reports whether hello regular and maintenance modes are available and their associated package names.</span></span> <span data-ttu-id="51624-166">Se `RegularUpdates` e `MaintenanceModeUpdates` sono `false`, ciò indica che non sono disponibili aggiornamenti di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-166">If `RegularUpdates` and `MaintenanceModeUpdates` are `false`, this indicates that hello updates are not available.</span></span> <span data-ttu-id="51624-167">e il dispositivo è già aggiornato.</span><span class="sxs-lookup"><span data-stu-id="51624-167">Your device is up-to-date.</span></span>
* <span data-ttu-id="51624-168">informazioni sul cluster Hello contiene informazioni di hello sui vari componenti logici di tutti i gruppi di cluster HCS hello e i relativi stati rispettivi.</span><span class="sxs-lookup"><span data-stu-id="51624-168">hello cluster information contains hello information on various logical components of all hello HCS cluster groups and their respective statuses.</span></span> <span data-ttu-id="51624-169">Se viene visualizzato un gruppo di cluster non in linea in questa sezione del report hello, [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="51624-169">If you see an offline cluster group in this section of hello report, [contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>
* <span data-ttu-id="51624-170">informazioni sul servizio Hello include nomi di hello e gli stati di hello tutti HCS e gli elementi di configurazione servizi in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-170">hello service information includes hello names and statuses of all hello HCS and CiS services running on your device.</span></span> <span data-ttu-id="51624-171">Queste informazioni sono utili per hello supporto Microsoft nella risoluzione dei problemi di dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="51624-171">This information is helpful for hello Microsoft Support in troubleshooting hello device issue.</span></span>

#### <a name="sample-output-of-system-test-run-on-an-8100-device"></a><span data-ttu-id="51624-172">Output di esempio del test del sistema per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="51624-172">Sample output of system test run on an 8100 device</span></span>

<span data-ttu-id="51624-173">Di seguito è riportato un esempio di output di hello sistema esecuzione dei test in un dispositivo 8100.</span><span class="sxs-lookup"><span data-stu-id="51624-173">Here is a sample output of hello system test run on an 8100 device.</span></span>

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

### <a name="network-test"></a><span data-ttu-id="51624-174">Test della rete</span><span class="sxs-lookup"><span data-stu-id="51624-174">Network test</span></span>

<span data-ttu-id="51624-175">Questo test consente di verificare lo stato di hello di interfacce di rete hello, porte, DNS e NTP connettività del server, SSL certificato, le credenziali dell'account di archiviazione, i server di aggiornamento toohello connettività e connettività proxy web nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-175">This test validates hello status of hello network interfaces, ports, DNS and NTP server connectivity, SSL certificate, storage account credentials, connectivity toohello Update servers, and web proxy connectivity on your StorSimple device.</span></span>

#### <a name="sample-output-of-network-test-when-only-data0-is-enabled"></a><span data-ttu-id="51624-176">Esempio di output del test della rete quando è abilitata solo l'interfaccia di rete DATA0</span><span class="sxs-lookup"><span data-stu-id="51624-176">Sample output of network test when only DATA0 is enabled</span></span>

<span data-ttu-id="51624-177">Di seguito è riportato un esempio di output del dispositivo 8100 hello.</span><span class="sxs-lookup"><span data-stu-id="51624-177">Here is a sample output of hello 8100 device.</span></span> <span data-ttu-id="51624-178">È possibile vedere nell'output di hello che:</span><span class="sxs-lookup"><span data-stu-id="51624-178">You can see in hello output that:</span></span>
* <span data-ttu-id="51624-179">Solo le interfacce di rete DATA0 e DATA1 sono abilitate e configurate.</span><span class="sxs-lookup"><span data-stu-id="51624-179">Only DATA 0 and DATA 1 network interfaces are enabled and configured.</span></span>
* <span data-ttu-id="51624-180">2-5 di dati non sono abilitati nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-180">DATA 2 - 5 are not enabled in hello portal.</span></span>
* <span data-ttu-id="51624-181">configurazione del server DNS Hello è valida e hello dispositivo possa connettersi attraverso il server DNS hello.</span><span class="sxs-lookup"><span data-stu-id="51624-181">hello DNS server configuration is valid and hello device can connect via hello DNS server.</span></span>
* <span data-ttu-id="51624-182">è inoltre Hello connettività del server NTP.</span><span class="sxs-lookup"><span data-stu-id="51624-182">hello NTP server connectivity is also fine.</span></span>
* <span data-ttu-id="51624-183">Le porte 80 e 443 sono aperte,</span><span class="sxs-lookup"><span data-stu-id="51624-183">Ports 80 and 443 are open.</span></span> <span data-ttu-id="51624-184">ma la porta 9354 è bloccata.</span><span class="sxs-lookup"><span data-stu-id="51624-184">However, port 9354 is blocked.</span></span> <span data-ttu-id="51624-185">In base a hello [requisiti di sistema di rete](storsimple-system-requirements.md), tooopen questa porta è necessaria per la comunicazione di hello service bus.</span><span class="sxs-lookup"><span data-stu-id="51624-185">Based on hello [system network requirements](storsimple-system-requirements.md), you need tooopen this port for hello service bus communication.</span></span>
* <span data-ttu-id="51624-186">certificazione SSL Hello è valido.</span><span class="sxs-lookup"><span data-stu-id="51624-186">hello SSL certification is valid.</span></span>
* <span data-ttu-id="51624-187">account di archiviazione toohello è possibile connettere il dispositivo di Hello: _myss8000storageacct_.</span><span class="sxs-lookup"><span data-stu-id="51624-187">hello device can connect toohello storage account: _myss8000storageacct_.</span></span>
* <span data-ttu-id="51624-188">i server tooUpdate connettività Hello è valido.</span><span class="sxs-lookup"><span data-stu-id="51624-188">hello connectivity tooUpdate servers is valid.</span></span>
* <span data-ttu-id="51624-189">Hello web proxy non è configurato su questo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-189">hello web proxy is not configured on this device.</span></span>

#### <a name="sample-output-of-network-test-when-data0-and-data1-are-enabled"></a><span data-ttu-id="51624-190">Esempio di output del test della rete quando sono abilitate le interfacce di rete DATA0 e DATA1</span><span class="sxs-lookup"><span data-stu-id="51624-190">Sample output of network test when DATA0 and DATA1 are enabled</span></span>

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

### <a name="performance-test"></a><span data-ttu-id="51624-191">Test delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="51624-191">Performance test</span></span>

<span data-ttu-id="51624-192">Questo test indica prestazioni cloud hello tramite latenze di lettura / scrittura hello cloud per il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-192">This test reports hello cloud performance via hello cloud read-write latencies for your device.</span></span> <span data-ttu-id="51624-193">Questo strumento può essere utilizzato tooestablish una linea di base delle prestazioni di cloud hello che è possibile ottenere con StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-193">This tool can be used tooestablish a baseline of hello cloud performance that you can achieve with StorSimple.</span></span> <span data-ttu-id="51624-194">Hello strumento report hello massimo delle prestazioni (scenario migliore per le latenze di lettura / scrittura) che è possibile ottenere per la connessione.</span><span class="sxs-lookup"><span data-stu-id="51624-194">hello tool reports hello maximum performance (best case scenario for read-write latencies) that you can get for your connection.</span></span>

<span data-ttu-id="51624-195">Come strumento hello segnala le massime prestazioni ottenibili hello, possiamo utilizzare hello segnalato le latenze di lettura / scrittura quando si distribuiscono le destinazioni hello carichi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="51624-195">As hello tool reports hello maximum achievable performance, we can use hello reported read-write latencies as targets when deploying hello workloads.</span></span>

<span data-ttu-id="51624-196">test di Hello simula le dimensioni di blob hello associate a tipi di volume diversa hello sul dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="51624-196">hello test simulates hello blob sizes associated with hello different volume types on hello device.</span></span> <span data-ttu-id="51624-197">I normali volumi a livelli e i backup dei volumi aggiunti in locale usano dimensioni del BLOB pari a 64 KB.</span><span class="sxs-lookup"><span data-stu-id="51624-197">Regular tiered and backups of locally pinned volumes use a 64 KB blob size.</span></span> <span data-ttu-id="51624-198">I volumi a livelli con l'opzione di archiviazione selezionata usano dimensioni del BLOB pari a 512 KB.</span><span class="sxs-lookup"><span data-stu-id="51624-198">Tiered volumes with archive option checked use 512 KB blob data size.</span></span> <span data-ttu-id="51624-199">Se il dispositivo dispone di volumi aggiunti in locale e a più livelli è configurato, solo hello test corrispondente too64 KB blob di dimensioni dei dati viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="51624-199">If your device has tiered and locally pinned volumes configured, only hello test corresponding too64 KB blob data size is run.</span></span>

<span data-ttu-id="51624-200">toouse questo strumento, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="51624-200">toouse this tool, perform hello following steps:</span></span>

1.  <span data-ttu-id="51624-201">Creare prima di tutto una combinazione di volumi a livelli e volumi a livelli con l'opzione di archiviazione selezionata.</span><span class="sxs-lookup"><span data-stu-id="51624-201">First, create a mix of tiered volumes and tiered volumes with archived option checked.</span></span> <span data-ttu-id="51624-202">Questa operazione assicura che lo strumento hello esegue i test di hello per 64 KB e 512 KB dimensioni blob.</span><span class="sxs-lookup"><span data-stu-id="51624-202">This action ensures that hello tool runs hello tests for both 64 KB and 512 KB blob sizes.</span></span>

2. <span data-ttu-id="51624-203">Dopo aver creato e configurato i volumi di hello, eseguire i cmdlet di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-203">Run hello cmdlet after you have created and configured hello volumes.</span></span> <span data-ttu-id="51624-204">Digitare:</span><span class="sxs-lookup"><span data-stu-id="51624-204">Type:</span></span>

    `Invoke-HcsDiagnostics -Scope Performance`

3. <span data-ttu-id="51624-205">Prendere nota della latenza di lettura / scrittura hello segnalati dallo strumento hello.</span><span class="sxs-lookup"><span data-stu-id="51624-205">Make a note of hello read-write latencies reported by hello tool.</span></span> <span data-ttu-id="51624-206">Questo test può richiedere diversi minuti toorun prima che riporti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-206">This test can take several minutes toorun before it reports hello results.</span></span>

4. <span data-ttu-id="51624-207">Se le latenze connessione hello sono tutti in hello intervallo previsto, quindi hello latenze segnalate dallo strumento hello utilizzabili come destinazione raggiungibile massimo quando si distribuiscono i carichi di lavoro di hello.</span><span class="sxs-lookup"><span data-stu-id="51624-207">If hello connection latencies are all under hello expected range, then hello latencies reported by hello tool can be used as maximum achievable target when deploying hello workloads.</span></span> <span data-ttu-id="51624-208">Tenere conto dell'overhead per l'elaborazione dei dati interna.</span><span class="sxs-lookup"><span data-stu-id="51624-208">Factor in some overhead for internal data processing.</span></span>

    <span data-ttu-id="51624-209">Se le latenze di lettura / scrittura hello segnalati lo strumento di diagnostica hello sono elevati:</span><span class="sxs-lookup"><span data-stu-id="51624-209">If hello read-write latencies reported by hello diagnostics tool are high:</span></span>

    1. <span data-ttu-id="51624-210">Configurare l'archiviazione Analitica per i servizi blob e analizzare hello output toounderstand hello latenze per hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="51624-210">Configure Storage Analytics for blob services and analyze hello output toounderstand hello latencies for hello Azure storage account.</span></span> <span data-ttu-id="51624-211">Per istruzioni dettagliate, vedere troppo[abilitare e configurare archiviazione Analitica](../storage/common/storage-enable-and-view-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="51624-211">For detailed instructions, go too[enable and configure Storage Analytics](../storage/common/storage-enable-and-view-metrics.md).</span></span> <span data-ttu-id="51624-212">Se le latenze sono anche numeri toohello elevata e comparabili ricevuto da hello lo strumento di diagnostica di StorSimple, è necessario toolog una richiesta di servizio con l'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="51624-212">If those latencies are also high and comparable toohello numbers you received from hello StorSimple Diagnostics tool, then you need toolog a service request with Azure storage.</span></span>

    2. <span data-ttu-id="51624-213">Se le latenze account di archiviazione hello sono basse, contattare il tooinvestigate di amministratore di rete problemi di latenza della rete.</span><span class="sxs-lookup"><span data-stu-id="51624-213">If hello storage account latencies are low, contact your network administrator tooinvestigate any latency issues in your network.</span></span>

#### <a name="sample-output-of-performance-test-run-on-an-8100-device"></a><span data-ttu-id="51624-214">Output di esempio del test delle prestazioni per un dispositivo 8100</span><span class="sxs-lookup"><span data-stu-id="51624-214">Sample output of performance test run on an 8100 device</span></span>

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

## <a name="appendix-interpreting-system-information"></a><span data-ttu-id="51624-215">Appendice: interpretazione delle informazioni sul sistema</span><span class="sxs-lookup"><span data-stu-id="51624-215">Appendix: interpreting system information</span></span>

<span data-ttu-id="51624-216">Di seguito è riportata una tabella che descrive quale hello per eseguire il mapping di diversi parametri di Windows PowerShell nelle informazioni di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="51624-216">Here is a table describing what hello various Windows PowerShell parameters in hello system information map to.</span></span> 

| <span data-ttu-id="51624-217">Parametro di PowerShell</span><span class="sxs-lookup"><span data-stu-id="51624-217">PowerShell Parameter</span></span>    | <span data-ttu-id="51624-218">Descrizione</span><span class="sxs-lookup"><span data-stu-id="51624-218">Description</span></span>  |
|-------------------------|------------------|
| <span data-ttu-id="51624-219">ID istanza</span><span class="sxs-lookup"><span data-stu-id="51624-219">Instance ID</span></span>             | <span data-ttu-id="51624-220">Ogni controller è associato a un identificatore univoco o un GUID.</span><span class="sxs-lookup"><span data-stu-id="51624-220">Every controller has a unique identifier or a GUID associated with it.</span></span>|
| <span data-ttu-id="51624-221">Nome</span><span class="sxs-lookup"><span data-stu-id="51624-221">Name</span></span>                    | <span data-ttu-id="51624-222">nome descrittivo di Hello del dispositivo hello in base alla configurazione hello portale di Azure durante la distribuzione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-222">hello friendly name of hello device as configured through hello Azure portal during device deployment.</span></span> <span data-ttu-id="51624-223">nome descrittivo predefinito Hello è hello numero di serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-223">hello default friendly name is hello device serial number.</span></span> |
| <span data-ttu-id="51624-224">Modello</span><span class="sxs-lookup"><span data-stu-id="51624-224">Model</span></span>                   | <span data-ttu-id="51624-225">modello di Hello del dispositivo StorSimple 8000 series.</span><span class="sxs-lookup"><span data-stu-id="51624-225">hello model of your StorSimple 8000 series device.</span></span> <span data-ttu-id="51624-226">è possibile modello Hello 8100 o 8600.</span><span class="sxs-lookup"><span data-stu-id="51624-226">hello model can be 8100 or 8600.</span></span>|
| <span data-ttu-id="51624-227">SerialNumber</span><span class="sxs-lookup"><span data-stu-id="51624-227">SerialNumber</span></span>            | <span data-ttu-id="51624-228">numero di serie Hello è assegnato alla factory hello e 15 caratteri.</span><span class="sxs-lookup"><span data-stu-id="51624-228">hello device serial number is assigned at hello factory and is 15 characters long.</span></span> <span data-ttu-id="51624-229">Ad esempio, 8600-SHX0991003G44HT indica quanto segue:</span><span class="sxs-lookup"><span data-stu-id="51624-229">For instance, 8600-SHX0991003G44HT indicates:</span></span><br> <span data-ttu-id="51624-230">8600: è un modello di dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="51624-230">8600 – Is hello device model.</span></span><br><span data-ttu-id="51624-231">SHX – è hello di produzione del sito.</span><span class="sxs-lookup"><span data-stu-id="51624-231">SHX – Is hello manufacturing site.</span></span><br> <span data-ttu-id="51624-232">0991003: prodotto specifico.</span><span class="sxs-lookup"><span data-stu-id="51624-232">0991003 - Is a specific product.</span></span> <br> <span data-ttu-id="51624-233">G44HT-hello ultimi 5 cifre vengono incrementati toocreate i numeri di serie univoco.</span><span class="sxs-lookup"><span data-stu-id="51624-233">G44HT- hello last 5 digits are incremented toocreate unique serial numbers.</span></span> <span data-ttu-id="51624-234">Questo potrebbe non essere un insieme sequenziale.</span><span class="sxs-lookup"><span data-stu-id="51624-234">This may not be a sequential set.</span></span>|
| <span data-ttu-id="51624-235">TimeZone</span><span class="sxs-lookup"><span data-stu-id="51624-235">TimeZone</span></span>                | <span data-ttu-id="51624-236">Hello fuso orario del dispositivo come configurato nella hello portale di Azure durante la distribuzione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-236">hello device time zone as configured in hello Azure portal during device deployment.</span></span>|
| <span data-ttu-id="51624-237">CurrentController</span><span class="sxs-lookup"><span data-stu-id="51624-237">CurrentController</span></span>       | <span data-ttu-id="51624-238">controller Hello che si è connessi toothrough interfaccia di Windows PowerShell hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-238">hello controller that you are connected toothrough hello Windows PowerShell interface of your StorSimple device.</span></span>|
| <span data-ttu-id="51624-239">ActiveController</span><span class="sxs-lookup"><span data-stu-id="51624-239">ActiveController</span></span>        | <span data-ttu-id="51624-240">controller Hello che è attivo sul dispositivo e controlla tutte le operazioni di rete e disco hello.</span><span class="sxs-lookup"><span data-stu-id="51624-240">hello controller that is active on your device and is controlling all hello network and disk operations.</span></span> <span data-ttu-id="51624-241">Può trattarsi del Controller 0 o del Controller 1.</span><span class="sxs-lookup"><span data-stu-id="51624-241">This can be Controller 0 or Controller 1.</span></span>  |
| <span data-ttu-id="51624-242">Controller0Status</span><span class="sxs-lookup"><span data-stu-id="51624-242">Controller0Status</span></span>       | <span data-ttu-id="51624-243">stato di Hello del Controller 0 sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-243">hello status of Controller 0 on your device.</span></span> <span data-ttu-id="51624-244">lo stato del controller Hello può essere normale, in modalità di ripristino o non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="51624-244">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="51624-245">Controller1Status</span><span class="sxs-lookup"><span data-stu-id="51624-245">Controller1Status</span></span>       | <span data-ttu-id="51624-246">Hello lo stato del Controller 1 nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-246">hello status of Controller 1 on your device.</span></span>  <span data-ttu-id="51624-247">lo stato del controller Hello può essere normale, in modalità di ripristino o non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="51624-247">hello controller status can be normal, in recovery mode, or unreachable.</span></span>|
| <span data-ttu-id="51624-248">SystemMode</span><span class="sxs-lookup"><span data-stu-id="51624-248">SystemMode</span></span>              | <span data-ttu-id="51624-249">Hello stato generale del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-249">hello overall status of your StorSimple device.</span></span> <span data-ttu-id="51624-250">stato del dispositivo Hello può essere normale, manutenzione, o non autorizzato (corrisponde toodeactivated in hello portale di Azure).</span><span class="sxs-lookup"><span data-stu-id="51624-250">hello device status can be normal, maintenance, or decommissioned (corresponds toodeactivated in hello Azure portal).</span></span>|
| <span data-ttu-id="51624-251">FriendlySoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="51624-251">FriendlySoftwareVersion</span></span> | <span data-ttu-id="51624-252">stringa descrittivo Hello corrispondente toohello versione software del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-252">hello friendly string that corresponds toohello device software version.</span></span> <span data-ttu-id="51624-253">Per un sistema che esegue l'aggiornamento 4, versione del software descrittivo hello sarebbe StorSimple 8000 Series Update 4.0.</span><span class="sxs-lookup"><span data-stu-id="51624-253">For a system running Update 4, hello friendly software version would be StorSimple 8000 Series Update 4.0.</span></span>|
| <span data-ttu-id="51624-254">HcsSoftwareVersion</span><span class="sxs-lookup"><span data-stu-id="51624-254">HcsSoftwareVersion</span></span>      | <span data-ttu-id="51624-255">versione del software HCS Hello in esecuzione sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="51624-255">hello HCS software version running on your device.</span></span> <span data-ttu-id="51624-256">Ad esempio, hello HCS software versione corrispondente tooStorSimple 8000 Series Update 4.0 è 6.3.9600.17820.</span><span class="sxs-lookup"><span data-stu-id="51624-256">For instance, hello HCS software version corresponding tooStorSimple 8000 Series Update 4.0 is 6.3.9600.17820.</span></span> |
| <span data-ttu-id="51624-257">ApiVersion</span><span class="sxs-lookup"><span data-stu-id="51624-257">ApiVersion</span></span>              | <span data-ttu-id="51624-258">versione del software Hello dell'API di Windows PowerShell del dispositivo HCS hello hello.</span><span class="sxs-lookup"><span data-stu-id="51624-258">hello software version of hello Windows PowerShell API of hello HCS device.</span></span>|
| <span data-ttu-id="51624-259">VhdVersion</span><span class="sxs-lookup"><span data-stu-id="51624-259">VhdVersion</span></span>              | <span data-ttu-id="51624-260">versione del software Hello dell'immagine del factory hello hello dispositivo è stata fornita con.</span><span class="sxs-lookup"><span data-stu-id="51624-260">hello software version of hello factory image that hello device was shipped with.</span></span> <span data-ttu-id="51624-261">Se si reimpostano le impostazioni predefinite del dispositivo toofactory, esegue questa versione del software.</span><span class="sxs-lookup"><span data-stu-id="51624-261">If you reset your device toofactory defaults, then it runs this software version.</span></span>|
| <span data-ttu-id="51624-262">OSVersion</span><span class="sxs-lookup"><span data-stu-id="51624-262">OSVersion</span></span>               | <span data-ttu-id="51624-263">versione del sistema operativo di Windows Server hello in esecuzione sul dispositivo hello software Hello.</span><span class="sxs-lookup"><span data-stu-id="51624-263">hello software version of hello Windows Server operating system running on hello device.</span></span> <span data-ttu-id="51624-264">Windows Server 2012 R2 corrispondente too6.3.9600 hello è basata sul dispositivo StorSimple Hello.</span><span class="sxs-lookup"><span data-stu-id="51624-264">hello StorSimple device is based off hello Windows Server 2012 R2 that corresponds too6.3.9600.</span></span>|
| <span data-ttu-id="51624-265">CisAgentVersion</span><span class="sxs-lookup"><span data-stu-id="51624-265">CisAgentVersion</span></span>         | <span data-ttu-id="51624-266">versione di Hello per l'agente di elementi di configurazione in esecuzione sul dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-266">hello version for your Cis agent running on your StorSimple device.</span></span> <span data-ttu-id="51624-267">Questo agente consente di comunicare con il servizio StorSimple Manager hello in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="51624-267">This agent helps communicate with hello StorSimple Manager service running in Azure.</span></span>|
| <span data-ttu-id="51624-268">MdsAgentVersion</span><span class="sxs-lookup"><span data-stu-id="51624-268">MdsAgentVersion</span></span>         | <span data-ttu-id="51624-269">Hello versione corrispondente toohello Mds agente in esecuzione nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-269">hello version corresponding toohello Mds agent running on your StorSimple device.</span></span> <span data-ttu-id="51624-270">Questo agente sposta dati toohello monitoraggio e diagnostica del servizio (MDS).</span><span class="sxs-lookup"><span data-stu-id="51624-270">This agent moves data toohello Monitoring and Diagnostics Service (MDS).</span></span>|
| <span data-ttu-id="51624-271">Lsisas2Version</span><span class="sxs-lookup"><span data-stu-id="51624-271">Lsisas2Version</span></span>          | <span data-ttu-id="51624-272">Hello driver versione corrispondente toohello LSI nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-272">hello version corresponding toohello LSI drivers on your StorSimple device.</span></span>|
| <span data-ttu-id="51624-273">Capacity</span><span class="sxs-lookup"><span data-stu-id="51624-273">Capacity</span></span>                | <span data-ttu-id="51624-274">capacità totale di Hello del dispositivo hello in byte.</span><span class="sxs-lookup"><span data-stu-id="51624-274">hello total capacity of hello device in bytes.</span></span>|
| <span data-ttu-id="51624-275">RemoteManagementMode</span><span class="sxs-lookup"><span data-stu-id="51624-275">RemoteManagementMode</span></span>    | <span data-ttu-id="51624-276">Indica se il dispositivo hello può essere gestito in modalità remota tramite l'interfaccia di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="51624-276">Indicates whether hello device can be remotely managed via its Windows PowerShell interface.</span></span> |
| <span data-ttu-id="51624-277">FipsMode</span><span class="sxs-lookup"><span data-stu-id="51624-277">FipsMode</span></span>                | <span data-ttu-id="51624-278">Indica se il dispositivo viene abilitata la modalità di hello United States elaborazione Standard FIPS (Federal Information).</span><span class="sxs-lookup"><span data-stu-id="51624-278">Indicates whether hello United States Federal Information Processing Standard (FIPS) mode is enabled on your device.</span></span> <span data-ttu-id="51624-279">standard di Hello FIPS 140 definisce gli algoritmi di crittografia approvati per l'utilizzo dai sistemi di computer governo federale US per la protezione dei dati sensibili hello.</span><span class="sxs-lookup"><span data-stu-id="51624-279">hello FIPS 140 standard defines cryptographic algorithms approved for use by US Federal government computer systems for hello protection of sensitive data.</span></span> <span data-ttu-id="51624-280">Per i dispositivi che eseguono l'aggiornamento 4 o versione successiva, la modalità FIPS è abilitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="51624-280">For devices running Update 4 or later, FIPS mode is enabled by default.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="51624-281">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="51624-281">Next steps</span></span>

* <span data-ttu-id="51624-282">Informazioni su hello [sintassi del cmdlet Invoke-HcsDiagnostics hello](https://technet.microsoft.com/library/mt795371.aspx).</span><span class="sxs-lookup"><span data-stu-id="51624-282">Learn hello [syntax of hello Invoke-HcsDiagnostics cmdlet](https://technet.microsoft.com/library/mt795371.aspx).</span></span>

* <span data-ttu-id="51624-283">Per ulteriori informazioni su troppo[risolvere i problemi di distribuzione](storsimple-troubleshoot-deployment.md) nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="51624-283">Learn more about how too[troubleshoot deployment issues](storsimple-troubleshoot-deployment.md) on your StorSimple device.</span></span>
