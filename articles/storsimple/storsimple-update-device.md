---
title: Aggiornare il dispositivo StorSimple | Documentazione Microsoft
description: "Viene illustrato come utilizzare la funzionalità di aggiornamento StorSimple per installare gli aggiornamenti rapidi in modalità normale e manutenzione."
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
ms.openlocfilehash: 8490110942741b049b6d44ac93697303cef40e8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>Aggiornare il dispositivo StorSimple 8000 serie
## <a name="overview"></a>Panoramica
La funzionalità di aggiornamento StorSimple consentono di tenere aggiornato il dispositivo StorSimple. A seconda del tipo di aggiornamento, è possibile applicare gli aggiornamenti al dispositivo tramite il portale di Azure classico o tramite l'interfaccia Windows PowerShell. In questa esercitazione vengono descritti i tipi di aggiornamento e come installarli.

È possibile applicare due tipi di aggiornamenti del dispositivo: 

* Aggiornamenti regolari (o in modalità normale)
* Aggiornamenti in modalità manutenzione

È possibile installare aggiornamenti regolari tramite il portale di Azure classico o Windows PowerShell; tuttavia, è necessario utilizzare Windows PowerShell per installare gli aggiornamenti in modalità manutenzione. 

Di seguito viene separatamente descritto ogni tipo di aggiornamento.

### <a name="regular-updates"></a>Aggiornamenti regolari
Gli aggiornamenti regolari sono aggiornamenti senza interruzioni che possono essere installati quando il dispositivo è in modalità normale. Questi aggiornamenti vengono applicati tramite il sito Web Microsoft Update per ogni controller del dispositivo. 

> [!IMPORTANT]
> Durante il processo di aggiornamento può verificarsi un failover del controller. Tuttavia, questa operazione non modificherà la disponibilità o l'operatività del sistema.
> 
> 

* Per informazioni dettagliate su come installare aggiornamenti regolari con il portale di Azure classico, vedere [Installare gli aggiornamenti regolari tramite il portale di Azure classico](#install-regular-updates-via-the-azure-classic-portal).
* È anche possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple. Per dettagli, vedere [Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple](#install-regular-updates-via-windows-powershell-for-storsimple)

### <a name="maintenance-mode-updates"></a>Aggiornamenti in modalità manutenzione
Gli aggiornamenti in modalità manutenzione sono aggiornamenti problematici, come gli aggiornamenti del firmware del disco. Questi aggiornamenti richiedono che il dispositivo sia in modalità manutenzione. Per altri dettagli, vedere [Passaggio 2: Attivare la modalità di manutenzione](#step2). Per installare gli aggiornamenti in modalità manutenzione, non è possibile usare il portale di Azure classico. Pertanto è necessario utilizzare Windows PowerShell per StorSimple. 

Per informazioni dettagliate su come installare gli aggiornamenti in modalità manutenzione, vedere [Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Gli aggiornamenti in modalità manutenzione devono essere applicati separatamente a ogni controller. 
> 
> 

## <a name="install-regular-updates-via-the-azure-classic-portal"></a>Installare gli aggiornamenti regolari tramite il portale di Azure classico
È possibile usare il portale di Azure classico per applicare gli aggiornamenti al dispositivo StorSimple.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>Installare aggiornamenti regolari tramite Windows PowerShell per StorSimple
In alternativa, è possibile utilizzare Windows PowerShell per StorSimple per applicare gli aggiornamenti regolari (modalità normale).

> [!IMPORTANT]
> Sebbene sia possibile installare aggiornamenti regolari tramite Windows PowerShell per StorSimple, è consigliabile installare gli aggiornamenti periodici tramite il portale di Azure classico. A partire dall’aggiornamento 1, verranno eseguiti controlli preliminari prima di installare gli aggiornamenti dal portale. Questi controlli preliminari preverranno errori e garantiranno un'esperienza più uniforme. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>Installare gli aggiornamenti in modalità manutenzione tramite Windows PowerShell per StorSimple
Utilizzare Windows PowerShell per StorSimple per applicare gli aggiornamenti in modalità manutenzione al dispositivo StorSimple. In questa modalità, tutte le richieste I/O sono sospese. Inoltre vengono arrestati servizi come la memoria ad accesso casuale non volatile (NVRAM) o il servizio cluster. Entrambi i controller vengono riavviati quando si entra o esce dalla modalità. Quando si esce da questa modalità, tutti i servizi vengono ripresi e devono essere integri. L'operazione potrebbe richiedere alcuni minuti.

Se è necessario applicare gli aggiornamenti in modalità manutenzione, si riceverà un avviso tramite il portale di Azure classico riguardo gli aggiornamenti che devono essere installati. Questo avviso include le istruzioni sull'utilizzo di Windows PowerShell per StorSimple per installare gli aggiornamenti. Dopo aver aggiornato il dispositivo, utilizzare la stessa procedura per modificare il dispositivo alla modalità normale. Per istruzioni dettagliate, vedere [Passaggio 4: Uscire dalla modalità di manutenzione](#step4).

> [!IMPORTANT]
> * Prima di entrare in modalità manutenzione, verificare che entrambi i controller di dispositivi siano integri controllando lo **Stato Hardware** sulla pagina **Manutenzione** nel portale di Azure classico. Se il controller non è integro, contattare il supporto tecnico Microsoft per i passaggi successivi. Per altre informazioni, contattare il supporto tecnico Microsoft. 
> * In modalità manutenzione, è necessario applicare l’aggiornamento rapido prima in un controller e poi nell’altro.
> 
> 

### <a name="step-1-connect-to-the-serial-console-a-namestep1"></a>Passaggio 1: Connettersi alla console seriale <a name="step1">
In primo luogo, utilizzare un'applicazione come PuTTY per accedere alla console seriale. La procedura seguente illustra come utilizzare PuTTY per connettersi alla console seriale.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>Passaggio 2: Attivare la modalità di manutenzione <a name="step2">
Dopo la connessione alla console, determinare se sono presenti aggiornamenti da installare e attivare la modalità manutenzione per installarli.

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

Nelle procedure seguenti viene illustrato come utilizzare Windows PowerShell per StorSimple per installare aggiornamenti rapidi regolari e di modalità manutenzione.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-to-updates-if-you-perform-a-factory-reset-of-the-device"></a>Cosa accade agli aggiornamenti se si esegue un ripristino delle impostazioni predefinite?
Se il dispositivo viene ripristinato alle impostazioni predefinite, tutti gli aggiornamenti vengono persi. Dopo aver registrato e configurato il dispositivo ripristinato alle impostazioni predefinite, sarà necessario installare manualmente gli aggiornamenti tramite il portale di Azure classico e/o Windows PowerShell per StorSimple. Per altre informazioni sul ripristino delle impostazioni predefinite, vedere [Ripristinare le impostazioni di fabbrica del dispositivo](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull' [utilizzo di Windows PowerShell per StorSimple per amministrare il dispositivo StorSimple](storsimple-windows-powershell-administration.md).
* Altre informazioni sull’ [utilizzo del servizio StorSimple Manager per amministrare il dispositivo StorSimple](storsimple-manager-service-administration.md).

