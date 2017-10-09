---
title: "modalità del dispositivo StorSimple aaaChange | Documenti Microsoft"
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 058ca6cc38954bce3679cc21b39d341b10cb4dfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-device-mode-on-your-storsimple-device"></a><span data-ttu-id="d45e4-103">Modifica della modalità dispositivo hello nel dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="d45e4-103">Change hello device mode on your StorSimple device</span></span>

<span data-ttu-id="d45e4-104">In questo articolo fornisce una breve descrizione di hello varie modalità in cui può operare dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d45e4-104">This article provides a brief description of hello various modes in which your StorSimple device can operate.</span></span> <span data-ttu-id="d45e4-105">Il dispositivo StorSimple può funzionare in tre modalità: normale, manutenzione e ripristino.</span><span class="sxs-lookup"><span data-stu-id="d45e4-105">Your StorSimple device can function in three modes: normal, maintenance, and recovery.</span></span>

<span data-ttu-id="d45e4-106">Una volta letto l'articolo, si sarà in grado di:</span><span class="sxs-lookup"><span data-stu-id="d45e4-106">After reading this article, you will know:</span></span>

* <span data-ttu-id="d45e4-107">Quali sono le modalità di dispositivo StorSimple hello</span><span class="sxs-lookup"><span data-stu-id="d45e4-107">What hello StorSimple device modes are</span></span>
* <span data-ttu-id="d45e4-108">Come toofigure la modalità di hello dispositivo StorSimple è in</span><span class="sxs-lookup"><span data-stu-id="d45e4-108">How toofigure out which mode hello StorSimple device is in</span></span>
* <span data-ttu-id="d45e4-109">Modalità toochange dalla modalità normale toomaintenance e *viceversa*</span><span class="sxs-lookup"><span data-stu-id="d45e4-109">How toochange from normal toomaintenance mode and *vice versa*</span></span>

<span data-ttu-id="d45e4-110">Hello sopra l'attività di gestione può essere eseguita solo tramite l'interfaccia di Windows PowerShell hello del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d45e4-110">hello above management tasks can only be performed via hello Windows PowerShell interface of your StorSimple device.</span></span>

## <a name="about-storsimple-device-modes"></a><span data-ttu-id="d45e4-111">Informazioni sulle modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="d45e4-111">About StorSimple device modes</span></span>

<span data-ttu-id="d45e4-112">Il dispositivo StorSimple può funzionare in modalità normale, manutenzione o ripristino.</span><span class="sxs-lookup"><span data-stu-id="d45e4-112">Your StorSimple device can operate in normal, maintenance, or recovery mode.</span></span> <span data-ttu-id="d45e4-113">Ognuna di queste modalità viene brevemente descritta di seguito.</span><span class="sxs-lookup"><span data-stu-id="d45e4-113">Each of these modes is briefly described below.</span></span>

### <a name="normal-mode"></a><span data-ttu-id="d45e4-114">Modalità normale</span><span class="sxs-lookup"><span data-stu-id="d45e4-114">Normal mode</span></span>

<span data-ttu-id="d45e4-115">Ciò viene definito come modalità operativa normale hello per un dispositivo StorSimple completamente configurato.</span><span class="sxs-lookup"><span data-stu-id="d45e4-115">This is defined as hello normal operational mode for a fully configured StorSimple device.</span></span> <span data-ttu-id="d45e4-116">Per impostazione predefinita, il dispositivo deve essere in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="d45e4-116">By default, your device should be in normal mode.</span></span>

### <a name="maintenance-mode"></a><span data-ttu-id="d45e4-117">Modalità di manutenzione</span><span class="sxs-lookup"><span data-stu-id="d45e4-117">Maintenance mode</span></span>

<span data-ttu-id="d45e4-118">In alcuni casi hello dispositivo StorSimple potrebbe essere necessario toobe in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-118">Sometimes hello StorSimple device may need toobe placed into maintenance mode.</span></span> <span data-ttu-id="d45e4-119">Questa modalità consente tooperform manutenzione sul dispositivo hello e installare gli aggiornamenti di arresto improvviso, ad esempio quelle relative toodisk firmware.</span><span class="sxs-lookup"><span data-stu-id="d45e4-119">This mode allows you tooperform maintenance on hello device and install disruptive updates, such as those related toodisk firmware.</span></span>

<span data-ttu-id="d45e4-120">È possibile inserire sistema hello in modalità manutenzione solo tramite hello Windows PowerShell per StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d45e4-120">You can put hello system into maintenance mode only via hello Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="d45e4-121">In questa modalità, tutte le richieste I/O sono sospese.</span><span class="sxs-lookup"><span data-stu-id="d45e4-121">All I/O requests are paused in this mode.</span></span> <span data-ttu-id="d45e4-122">Inoltre vengono arrestati i servizi, ad esempio memoria ad accesso casuale non volatile (NVRAM) o hello servizio cluster.</span><span class="sxs-lookup"><span data-stu-id="d45e4-122">Services such as non-volatile random access memory (NVRAM) or hello clustering service are also stopped.</span></span> <span data-ttu-id="d45e4-123">Quando si immette o si disattiva questa modalità, entrambi i controller hello vengono riavviati.</span><span class="sxs-lookup"><span data-stu-id="d45e4-123">Both hello controllers are restarted when you enter or exit this mode.</span></span> <span data-ttu-id="d45e4-124">Quando si esce dalla modalità di manutenzione hello, tutti i servizi di hello riprenderanno e devono essere integri.</span><span class="sxs-lookup"><span data-stu-id="d45e4-124">When you exit hello maintenance mode, all hello services will resume and should be healthy.</span></span> <span data-ttu-id="d45e4-125">L'operazione potrebbe richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="d45e4-125">This may take a few minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="d45e4-126">**La modalità di manutenzione è supportata solo in un dispositivo che funziona correttamente. Non è supportata in un dispositivo in cui uno o entrambi i controller di hello non funzionano.**</span><span class="sxs-lookup"><span data-stu-id="d45e4-126">**Maintenance mode is only supported on a properly functioning device. It is not supported on a device in which one or both of hello controllers are not functioning.**</span></span>


### <a name="recovery-mode"></a><span data-ttu-id="d45e4-127">Modalità di ripristino</span><span class="sxs-lookup"><span data-stu-id="d45e4-127">Recovery mode</span></span>

<span data-ttu-id="d45e4-128">La modalità di ripristino può essere descritta come la "modalità provvisoria di Windows con supporto di rete".</span><span class="sxs-lookup"><span data-stu-id="d45e4-128">Recovery mode can be described as "Windows Safe Mode with network support".</span></span> <span data-ttu-id="d45e4-129">Modalità di ripristino coinvolga i team di supporto Microsoft hello e consente loro tooperform diagnostica nel sistema hello.</span><span class="sxs-lookup"><span data-stu-id="d45e4-129">Recovery mode engages hello Microsoft Support team and allows them tooperform diagnostics on hello system.</span></span> <span data-ttu-id="d45e4-130">obiettivo principale di Hello della modalità di ripristino è tooretrieve hello i registri di sistema.</span><span class="sxs-lookup"><span data-stu-id="d45e4-130">hello primary goal of recovery mode is tooretrieve hello system logs.</span></span>

<span data-ttu-id="d45e4-131">Se il sistema passa in modalità di ripristino, è necessario contattare il supporto tecnico Microsoft per i passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="d45e4-131">If your system goes into recovery mode, you should contact Microsoft Support for next steps.</span></span> <span data-ttu-id="d45e4-132">Per ulteriori informazioni, visitare troppo[contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d45e4-132">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d45e4-133">**È possibile inserire il dispositivo hello in modalità di ripristino. Se il dispositivo di hello è in uno stato non valido, la modalità ripristino prova dispositivo hello tooget in uno stato in cui il personale di supporto Microsoft possono esaminarlo.**</span><span class="sxs-lookup"><span data-stu-id="d45e4-133">**You cannot place hello device in recovery mode. If hello device is in a bad state, recovery mode tries tooget hello device into a state in which Microsoft Support personnel can examine it.**</span></span>

## <a name="determine-storsimple-device-mode"></a><span data-ttu-id="d45e4-134">Determinare la modalità del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="d45e4-134">Determine StorSimple device mode</span></span>

#### <a name="toodetermine-hello-current-device-mode"></a><span data-ttu-id="d45e4-135">modalità del dispositivo corrente toodetermine hello</span><span class="sxs-lookup"><span data-stu-id="d45e4-135">toodetermine hello current device mode</span></span>

1. <span data-ttu-id="d45e4-136">Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d45e4-136">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d45e4-137">Esaminare il messaggio banner hello nel menu della console seriale del dispositivo hello hello.</span><span class="sxs-lookup"><span data-stu-id="d45e4-137">Look at hello banner message in hello serial console menu of hello device.</span></span> <span data-ttu-id="d45e4-138">Questo messaggio indica in modo esplicito se il dispositivo hello è in modalità di manutenzione o ripristino.</span><span class="sxs-lookup"><span data-stu-id="d45e4-138">This message explicitly indicates whether hello device is in maintenance or recovery mode.</span></span> <span data-ttu-id="d45e4-139">Se il messaggio hello non contiene informazioni specifiche sulla modalità di sistema toohello, dispositivo hello è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="d45e4-139">If hello message does not contain any specific information pertaining toohello system mode, hello device is in normal mode.</span></span>

## <a name="change-hello-storsimple-device-mode"></a><span data-ttu-id="d45e4-140">Modalità di modifica hello del dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="d45e4-140">Change hello StorSimple device mode</span></span>

<span data-ttu-id="d45e4-141">È possibile inserire il dispositivo di StorSimple hello in manutenzione tooperform (dalla modalità normale) la modalità di manutenzione o installare gli aggiornamenti in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-141">You can place hello StorSimple device into maintenance mode (from normal mode) tooperform maintenance or install maintenance mode updates.</span></span> <span data-ttu-id="d45e4-142">Eseguire hello seguendo procedure tooenter o uscita la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-142">Perform hello following procedures tooenter or exit maintenance mode.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d45e4-143">Prima di passare alla modalità manutenzione, verificare che entrambi i controller dei dispositivi siano integri in hello **le impostazioni del dispositivo > lo stato di Hardware** per il dispositivo in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d45e4-143">Before entering maintenance mode, verify that both device controllers are healthy by accessing hello **Device settings > Hardware health** for your device in hello Azure portal.</span></span> <span data-ttu-id="d45e4-144">Se uno o entrambi i controller hello non sono integri, contattare il supporto Microsoft per i passaggi successivi hello.</span><span class="sxs-lookup"><span data-stu-id="d45e4-144">If one or both hello controllers are not healthy, contact Microsoft Support for hello next steps.</span></span> <span data-ttu-id="d45e4-145">Per ulteriori informazioni, visitare troppo[contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="d45e4-145">For more information, go too[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>
 

#### <a name="tooenter-maintenance-mode"></a><span data-ttu-id="d45e4-146">modalità di manutenzione tooenter</span><span class="sxs-lookup"><span data-stu-id="d45e4-146">tooenter maintenance mode</span></span>

1. <span data-ttu-id="d45e4-147">Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d45e4-147">Log on toohello device serial console by following hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="d45e4-148">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="d45e4-148">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="d45e4-149">Quando richiesto, specificare hello **password amministratore del dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="d45e4-149">When prompted, provide hello **device administrator password**.</span></span> <span data-ttu-id="d45e4-150">password predefinita Hello è: `Password1`.</span><span class="sxs-lookup"><span data-stu-id="d45e4-150">hello default password is: `Password1`.</span></span>
3. <span data-ttu-id="d45e4-151">Al prompt dei comandi di hello, digitare</span><span class="sxs-lookup"><span data-stu-id="d45e4-151">At hello command prompt, type</span></span> 
   
    `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="d45e4-152">Verrà visualizzato un messaggio di avviso indicante che la modalità manutenzione interrompere tutte le richieste dei / o server hello connessione toohello portale di Azure e verrà richiesto di confermare.</span><span class="sxs-lookup"><span data-stu-id="d45e4-152">You will see a warning message telling you that maintenance mode will disrupt all I/O requests and sever hello connection toohello Azure portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="d45e4-153">Tipo **Y** tooenter la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-153">Type **Y** tooenter maintenance mode.</span></span>
5. <span data-ttu-id="d45e4-154">Entrambi i controller verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="d45e4-154">Both controllers will restart.</span></span> <span data-ttu-id="d45e4-155">Una volta completato il riavvio di hello, banner console seriale hello indicherà che il dispositivo hello è in modalità manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-155">When hello restart is complete, hello serial console banner will indicate that hello device is in maintenance mode.</span></span> <span data-ttu-id="d45e4-156">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="d45e4-156">A sample output is shown below.</span></span>

```
    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Controller0>Enter-HcsMaintenanceMode
    Checking device state...

    In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Passive
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>

```

#### <a name="tooexit-maintenance-mode"></a><span data-ttu-id="d45e4-157">modalità di manutenzione tooexit</span><span class="sxs-lookup"><span data-stu-id="d45e4-157">tooexit maintenance mode</span></span>

1. <span data-ttu-id="d45e4-158">Accedere toohello console seriale del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d45e4-158">Log on toohello device serial console.</span></span> <span data-ttu-id="d45e4-159">Verificare dal messaggio banner hello che il dispositivo è in modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-159">Verify from hello banner message that your device is in maintenance mode.</span></span>
2. <span data-ttu-id="d45e4-160">Al prompt dei comandi di hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="d45e4-160">At hello command prompt, type:</span></span>
   
    `Exit-HcsMaintenanceMode`
3. <span data-ttu-id="d45e4-161">Verranno visualizzati un messaggio di avviso e un messaggio di conferma.</span><span class="sxs-lookup"><span data-stu-id="d45e4-161">A warning message and a confirmation message will appear.</span></span> <span data-ttu-id="d45e4-162">Tipo **Y** tooexit la modalità di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="d45e4-162">Type **Y** tooexit maintenance mode.</span></span>
4. <span data-ttu-id="d45e4-163">Entrambi i controller verranno riavviati.</span><span class="sxs-lookup"><span data-stu-id="d45e4-163">Both controllers will restart.</span></span> <span data-ttu-id="d45e4-164">Una volta completato il riavvio di hello, banner console seriale hello indica che il dispositivo hello è in modalità normale.</span><span class="sxs-lookup"><span data-stu-id="d45e4-164">When hello restart is complete, hello serial console banner indicates that hello device is in normal mode.</span></span> <span data-ttu-id="d45e4-165">Di seguito è riportato un output di esempio.</span><span class="sxs-lookup"><span data-stu-id="d45e4-165">A sample output is shown below.</span></span>

```
    -----------------------MAINTENANCE MODE------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0
    ---------------------------------------------------------------

    Controller0>Exit-HcsMaintenanceMode
    Checking device state...

    Before exiting maintenance mode, ensure that any updates that are required on both controllers have been applied. Failure tooinstall on each controller could result in data corruption. Exiting maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooexit maintenance mode?
    [Y] Yes [N] No (Default is "Y"): Y

    <BOTH CONTROLLERS RESTART>

    ---------------------------------------------------------------
    Microsoft Azure StorSimple Appliance Model 8100
    Name: 8100-SHX0991003G44MT
    Software Version: 6.3.9600.17820
    Copyright (C) 2014 Microsoft Corporation. All rights reserved.
    You are connected tooController0 - Active
    ---------------------------------------------------------------

    Serial Console Menu
    [1] Log in with full access
    [2] Log into peer controller with full access
    [3] Connect with limited access
    [4] Change language
    Please enter your choice>
```

## <a name="next-steps"></a><span data-ttu-id="d45e4-166">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d45e4-166">Next steps</span></span>

<span data-ttu-id="d45e4-167">Informazioni su come troppo[applicare gli aggiornamenti in modalità normale e manutenzione](storsimple-update-device.md) nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d45e4-167">Learn how too[apply normal and maintenance mode updates](storsimple-update-device.md) on your StorSimple device.</span></span>

