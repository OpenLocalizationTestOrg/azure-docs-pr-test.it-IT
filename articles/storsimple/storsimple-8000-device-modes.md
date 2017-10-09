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
# <a name="change-hello-device-mode-on-your-storsimple-device"></a>Modifica della modalità dispositivo hello nel dispositivo StorSimple

In questo articolo fornisce una breve descrizione di hello varie modalità in cui può operare dispositivo StorSimple. Il dispositivo StorSimple può funzionare in tre modalità: normale, manutenzione e ripristino.

Una volta letto l'articolo, si sarà in grado di:

* Quali sono le modalità di dispositivo StorSimple hello
* Come toofigure la modalità di hello dispositivo StorSimple è in
* Modalità toochange dalla modalità normale toomaintenance e *viceversa*

Hello sopra l'attività di gestione può essere eseguita solo tramite l'interfaccia di Windows PowerShell hello del dispositivo StorSimple.

## <a name="about-storsimple-device-modes"></a>Informazioni sulle modalità del dispositivo StorSimple

Il dispositivo StorSimple può funzionare in modalità normale, manutenzione o ripristino. Ognuna di queste modalità viene brevemente descritta di seguito.

### <a name="normal-mode"></a>Modalità normale

Ciò viene definito come modalità operativa normale hello per un dispositivo StorSimple completamente configurato. Per impostazione predefinita, il dispositivo deve essere in modalità normale.

### <a name="maintenance-mode"></a>Modalità di manutenzione

In alcuni casi hello dispositivo StorSimple potrebbe essere necessario toobe in modalità manutenzione. Questa modalità consente tooperform manutenzione sul dispositivo hello e installare gli aggiornamenti di arresto improvviso, ad esempio quelle relative toodisk firmware.

È possibile inserire sistema hello in modalità manutenzione solo tramite hello Windows PowerShell per StorSimple. In questa modalità, tutte le richieste I/O sono sospese. Inoltre vengono arrestati i servizi, ad esempio memoria ad accesso casuale non volatile (NVRAM) o hello servizio cluster. Quando si immette o si disattiva questa modalità, entrambi i controller hello vengono riavviati. Quando si esce dalla modalità di manutenzione hello, tutti i servizi di hello riprenderanno e devono essere integri. L'operazione potrebbe richiedere alcuni minuti.

> [!NOTE]
> **La modalità di manutenzione è supportata solo in un dispositivo che funziona correttamente. Non è supportata in un dispositivo in cui uno o entrambi i controller di hello non funzionano.**


### <a name="recovery-mode"></a>Modalità di ripristino

La modalità di ripristino può essere descritta come la "modalità provvisoria di Windows con supporto di rete". Modalità di ripristino coinvolga i team di supporto Microsoft hello e consente loro tooperform diagnostica nel sistema hello. obiettivo principale di Hello della modalità di ripristino è tooretrieve hello i registri di sistema.

Se il sistema passa in modalità di ripristino, è necessario contattare il supporto tecnico Microsoft per i passaggi successivi. Per ulteriori informazioni, visitare troppo[contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).

> [!NOTE]
> **È possibile inserire il dispositivo hello in modalità di ripristino. Se il dispositivo di hello è in uno stato non valido, la modalità ripristino prova dispositivo hello tooget in uno stato in cui il personale di supporto Microsoft possono esaminarlo.**

## <a name="determine-storsimple-device-mode"></a>Determinare la modalità del dispositivo StorSimple

#### <a name="toodetermine-hello-current-device-mode"></a>modalità del dispositivo corrente toodetermine hello

1. Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Esaminare il messaggio banner hello nel menu della console seriale del dispositivo hello hello. Questo messaggio indica in modo esplicito se il dispositivo hello è in modalità di manutenzione o ripristino. Se il messaggio hello non contiene informazioni specifiche sulla modalità di sistema toohello, dispositivo hello è in modalità normale.

## <a name="change-hello-storsimple-device-mode"></a>Modalità di modifica hello del dispositivo StorSimple

È possibile inserire il dispositivo di StorSimple hello in manutenzione tooperform (dalla modalità normale) la modalità di manutenzione o installare gli aggiornamenti in modalità manutenzione. Eseguire hello seguendo procedure tooenter o uscita la modalità di manutenzione.

> [!IMPORTANT]
> Prima di passare alla modalità manutenzione, verificare che entrambi i controller dei dispositivi siano integri in hello **le impostazioni del dispositivo > lo stato di Hardware** per il dispositivo in hello portale di Azure. Se uno o entrambi i controller hello non sono integri, contattare il supporto Microsoft per i passaggi successivi hello. Per ulteriori informazioni, visitare troppo[contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md).
 

#### <a name="tooenter-maintenance-mode"></a>modalità di manutenzione tooenter

1. Accedere alla procedura seguente hello in console seriale del dispositivo toohello [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).
2. Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**. Quando richiesto, specificare hello **password amministratore del dispositivo**. password predefinita Hello è: `Password1`.
3. Al prompt dei comandi di hello, digitare 
   
    `Enter-HcsMaintenanceMode`
4. Verrà visualizzato un messaggio di avviso indicante che la modalità manutenzione interrompere tutte le richieste dei / o server hello connessione toohello portale di Azure e verrà richiesto di confermare. Tipo **Y** tooenter la modalità di manutenzione.
5. Entrambi i controller verranno riavviati. Una volta completato il riavvio di hello, banner console seriale hello indicherà che il dispositivo hello è in modalità manutenzione. Di seguito è riportato un output di esempio.

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

#### <a name="tooexit-maintenance-mode"></a>modalità di manutenzione tooexit

1. Accedere toohello console seriale del dispositivo. Verificare dal messaggio banner hello che il dispositivo è in modalità di manutenzione.
2. Al prompt dei comandi di hello, digitare:
   
    `Exit-HcsMaintenanceMode`
3. Verranno visualizzati un messaggio di avviso e un messaggio di conferma. Tipo **Y** tooexit la modalità di manutenzione.
4. Entrambi i controller verranno riavviati. Una volta completato il riavvio di hello, banner console seriale hello indica che il dispositivo hello è in modalità normale. Di seguito è riportato un output di esempio.

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

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come troppo[applicare gli aggiornamenti in modalità normale e manutenzione](storsimple-update-device.md) nel dispositivo StorSimple.

