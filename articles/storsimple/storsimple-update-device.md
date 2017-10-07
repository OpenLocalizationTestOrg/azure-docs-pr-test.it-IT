---
title: aaaUpdate dispositivo StorSimple | Documenti Microsoft
description: "Viene illustrato come toouse hello StorSimple Aggiorna funzionalità tooinstall regolari e gli aggiornamenti in modalità manutenzione e aggiornamenti rapidi."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Aggiornare il dispositivo StorSimple 8000 serie
## <a name="overview"></a>Panoramica
Hello StorSimple aggiornamenti consentono tooeasily mantenere aggiornato il dispositivo StorSimple. In base al tipo di aggiornamento hello, è possibile applicare il dispositivo toohello aggiornamenti hello portale di Azure classico o mediante l'interfaccia di Windows PowerShell hello. Questa esercitazione vengono descritti i tipi di aggiornamento hello e come tooinstall di essi.

È possibile applicare due tipi di aggiornamenti del dispositivo: 

* Aggiornamenti regolari (o in modalità normale)
* Aggiornamenti in modalità manutenzione

È possibile installare gli aggiornamenti periodici tramite Windows PowerShell o di hello portale di Azure classico Tuttavia, è necessario utilizzare Windows PowerShell tooinstall aggiornamenti in modalità manutenzione. 

Di seguito viene separatamente descritto ogni tipo di aggiornamento.

### <a name="regular-updates"></a>Aggiornamenti regolari
Gli aggiornamenti regolari sono aggiornamenti non comportano interruzioni del servizio che possono essere installati quando il dispositivo di hello è in modalità normale. Questi aggiornamenti vengono applicati tramite controller del dispositivo tooeach sito Web Microsoft Update hello. 

> [!IMPORTANT]
> Un failover del controller possono verificarsi durante il processo di aggiornamento hello. Tuttavia, questa operazione non modificherà la disponibilità o l'operatività del sistema.
> 
> 

* Per informazioni dettagliate su come tooinstall regular Aggiorna tramite hello portale di Azure classico, vedere [installare aggiornamenti periodici tramite hello portale di Azure classico](#install-regular-updates-via-the-azure-classic-portal).
* È anche possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple. Per dettagli, vedere [Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple)

### <a name="maintenance-mode-updates"></a>Aggiornamenti in modalità manutenzione
Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici, come gli aggiornamenti del firmware del disco. Questi aggiornamenti richiedono hello dispositivo toobe modalità manutenzione. Per altri dettagli, vedere [Passaggio 2: Attivare la modalità di manutenzione](#step2). Non è possibile utilizzare gli aggiornamenti in modalità manutenzione hello Azure tooinstall portale classico. Pertanto è necessario utilizzare Windows PowerShell per StorSimple. 

Per informazioni dettagliate sulla modalità di aggiornamento tooinstall la modalità di manutenzione, vedere [aggiornamenti in modalità manutenzione installare tramite Windows PowerShell per StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Modalità manutenzione gli aggiornamenti devono essere applicate separatamente tooeach controller. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Installare gli aggiornamenti periodici tramite hello portale di Azure classico
È possibile utilizzare il dispositivo StorSimple tooyour di hello Azure tooapply portale classico gli aggiornamenti.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple
In alternativa, è possibile utilizzare Windows PowerShell per gli aggiornamenti di StorSimple tooapply normale (modalità normale).

> [!IMPORTANT]
> Sebbene sia possibile installare gli aggiornamenti periodici tramite Windows PowerShell per StorSimple, è consigliabile installare gli aggiornamenti periodici tramite hello portale di Azure classico. A partire da Update 1, controlli preliminari saranno disponibili aggiornamenti tooinstalling precedenti eseguite dal portale hello. Questi controlli preliminari preverranno errori e garantiranno un'esperienza più uniforme. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple
Utilizzare Windows PowerShell per il dispositivo di StorSimple tooapply manutenzione modalità aggiornamenti tooyour StorSimple. In questa modalità, tutte le richieste I/O sono sospese. Inoltre vengono arrestati i servizi, ad esempio memoria ad accesso casuale non volatile (NVRAM) o hello servizio cluster. Entrambi i controller vengono riavviati quando si entra o esce dalla modalità. Quando si esce da questa modalità, tutti i servizi di hello riprenderanno e devono essere integri. L'operazione potrebbe richiedere alcuni minuti.

Se è necessario tooapply aggiornamenti in modalità manutenzione, si riceverà un avviso in presenza di aggiornamenti che devono essere installati tramite hello portale di Azure classico. Questo avviso include istruzioni per l'utilizzo di Windows PowerShell per gli aggiornamenti di StorSimple tooinstall hello. Dopo aver aggiornato il dispositivo, utilizzare hello stessa modalità di procedure toochange hello dispositivo tooRegular. Per istruzioni dettagliate, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](#step4).

> [!IMPORTANT]
> * Prima di passare alla modalità manutenzione, verificare che entrambi i controller di dispositivo sono integri controllando hello **stato Hardware** su hello **manutenzione** pagina hello portale di Azure classico. Se il controller di hello non è integro, contattare il supporto Microsoft per i passaggi successivi hello. Per ulteriori informazioni, visitare tooContact supporto Microsoft. 
> * Quando si è in modalità manutenzione, è necessario tooapply hello prima di aggiornamento su un controller e quindi su hello altro controller.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>Passaggio 1: Connettere la console seriale toohello<a name="step1">
Innanzitutto, utilizzare un'applicazione, ad esempio PuTTY tooaccess hello console seriale. Hello procedura riportata di seguito viene illustrato come console seriale di toouse tooconnect PuTTY toohello.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Passaggio 2: Attivare la modalità di manutenzione <a name="step2">
Dopo aver connesso toohello console, determinare se sono presenti aggiornamenti tooinstall e immettere tooinstall modalità manutenzione li.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>Passaggio 3: Installare gli aggiornamenti <a name="step3">
Successivamente, installare gli aggiornamenti.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>Passaggio 4: Uscire dalla modalità di manutenzione <a name="step4">
Per terminare, uscire dalla modalità manutenzione.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>Installare gli aggiornamenti rapidi tramite Windows PowerShell per StorSimple
A differenza degli aggiornamenti per Microsoft Azure StorSimple, gli aggiornamenti rapidi vengono installati da una cartella condivisa. Come con gli aggiornamenti, sono disponibili due tipi di aggiornamenti rapidi: 

* Aggiornamenti rapidi regolari 
* Aggiornamenti rapidi in modalità manutenzione  

Hello procedure seguenti illustrano come toouse Windows PowerShell per StorSimple tooinstall regolare e hotfix in modalità manutenzione.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Cosa accade tooupdates se si esegue una factory di reimpostazione del dispositivo hello?
Se un dispositivo è toofactory di ripristino delle impostazioni, quindi tutti gli aggiornamenti di hello andranno persi. Dopo che il dispositivo di ripristino delle impostazioni predefinite hello è registrato e configurato, sarà necessario toomanually installa gli aggiornamenti tramite hello portale di Azure classico e/o di Windows PowerShell per StorSimple. Per ulteriori informazioni sulle impostazioni di fabbrica, vedere [ripristinare le impostazioni predefinite di hello dispositivo toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni, vedere [tramite Windows PowerShell per StorSimple tooadminister dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Altre informazioni, vedere [utilizzando hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

