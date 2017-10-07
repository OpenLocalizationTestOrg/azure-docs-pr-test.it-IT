---
title: batteria aaaReplace nel dispositivo StorSimple di Microsoft Azure | Documenti Microsoft
description: Descrive come sostituire tooremove e mantenere hello modulo batteria di backup nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a>Sostituire il modulo batteria di backup hello nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
enclosure principale Hello alimentazione e raffreddamento modulo PCM () sul dispositivo Microsoft Azure StorSimple è un gruppo batterie aggiuntivo. Questo Service pack assicura l'alimentazione in modo che hello dispositivo StorSimple può salvare i dati nel caso di perdita di enclosure principale toohello di alimentazione CA. Questo gruppo batterie sono hello tooas cui *modulo batteria di backup*. modulo batteria di backup Hello esiste solo per l'enclosure principale di hello del dispositivo StorSimple (hello enclosure EBOD non contiene un modulo batteria di backup). 

In questa esercitazione viene illustrato come:

* Rimuovere hello modulo batteria di backup 
* Installare un nuovo modulo della batteria di backup
* Gestisci hello modulo batteria di backup

> [!IMPORTANT]
> Prima di rimozione e sostituzione di un modulo batteria di backup, rivedere le informazioni sulla sicurezza hello in hello [sostituzione dei componenti hardware tooStorSimple Introduzione](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-backup-battery-module"></a>Rimuovere hello modulo batteria di backup
Hello modulo batteria di backup per il dispositivo StorSimple è un'unità sostituibile sul campo. Prima di installarla in hello PCM, il modulo di batteria hello deve essere conservato nella confezione originale. Eseguire hello batteria di backup hello tooremove i passaggi seguenti.

#### <a name="tooremove-hello-backup-battery-module"></a>modulo batteria di backup di hello tooremove
1. Nel portale di Azure classico hello, andare troppo**dispositivi** > **manutenzione** > **stato Hardware**. In **componenti condivisi**, esaminare lo stato di hello di batteria hello.
2. Identificare il PCM hello in cui hello batteria non funzionante. Figura 1 mostra hello parte posteriore di dispositivo StorSimple hello.
   
    ![Backplane dei moduli dello chassis principale del dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    **Figura 1** Parte posteriore del dispositivo principale in cui vengono mostrati il PCM e i moduli del controller
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |PCM 0 |
   | 2 |PCM 1 |
   | 3 |Controller 0 |
   | 4 |Controller 1 |
   
    Come illustrato nella figura 2 hello numero 3, hello monitoraggio indicatore LED sul PCM 0 corrispondente troppo**guasto alla batteria** deve essere acceso.
   
    ![Backplane degli indicatori LED di monitoraggio del PCM del dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    **Figura 2** hello di parte posteriore del PCM con indicatori LED di monitoraggio
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Guasto dell’alimentazione CA |
   | 2 |Guasto alla ventola |
   | 3 |Guasto alla batteria |
   | 4 |PCM OK |
   | 5 |Guasto dell'alimentazione CC |
   | 6 |Integrità della batteria |
3. tooremove hello PCM con batteria non funzionante, seguire i passaggi hello [rimuovere un PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).
4. Con hello PCM rimosso, accuratezza e batteria hello ruota modulo gestire verso l'alto, come indicato nella seguente illustrazione hello ed estrarla batteria hello tooremove.
   
    ![Rimozione della batteria dal PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    **Figura 3** rimozione hello batteria dal PCM hello
5. Inserire il modulo di hello in unità sostituibile sul campo di hello creazione del pacchetto.
6. Restituire hello unità difettosa tooMicrosoft per la gestione e manutenzione corretto.

## <a name="install-a-new-backup-battery-module"></a>Installare un nuovo modulo della batteria di backup
Eseguire hello seguente modulo batteria sostitutivo passaggi tooinstall hello in hello PCM nell'enclosure principale di hello del dispositivo StorSimple.

#### <a name="tooinstall-hello-battery-module"></a>modulo batteria di hello tooinstall
1. Inserire l'orientamento corretto hello in hello PCM hello modulo batteria di backup.
2. Premere la freccia giù modulo batteria hello gestire connettore di hello tooseat hello modo tutti.
3. Sostituire hello PCM nell'enclosure principale hello seguendo le linee guida hello in [sostituire un Power and Cooling Module nel dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).
4. Una volta completata la sostituzione hello, andare troppo**dispositivi** > **manutenzione** > **stato Hardware** nel portale di Azure classico hello. Verificare lo stato di hello di hello batteria toomake assicurarsi della corretta installazione hello. Stato verde indica che la batteria hello è integra.

## <a name="maintain-hello-backup-battery-module"></a>Gestisci hello modulo batteria di backup
Nel dispositivo StorSimple hello modulo batteria di backup fornisce controller toohello power durante un evento di perdita di alimentazione. Consente di hello StorSimple dispositivo toosave dati critici precedente tooshutting verso il basso in modo controllato. Con due batterie completamente in hello PCM, il sistema di hello può gestire due interruzioni consecutive della fornitura.

Nel portale di Azure classico hello, hello **stato Hardware** su hello **manutenzione** pagina indica se batteria hello non funziona correttamente o se si sta avvicinando hello ciclo di vita. stato della batteria Hello è indicato da **batteria in PCM 0** o **batteria in PCM 1** in **componenti condivisi**. In questa pagina verrà visualizzato lo stato **DANNEGGIATO** per indicare l'avvicinarsi della fine del ciclo di vita e **NON RIUSCITO** per indicare che è stata raggiunta la fine del ciclo di vita. 

> [!NOTE]
> batteria Hello può segnalare **FAILED** quando è necessario semplicemente toobe addebitati.
> 
> 

Se hello **danneggiato** viene visualizzato lo stato, è consigliabile hello seguente linea di condotta:

* sistema Hello che si sia verificata un'interruzione dell'alimentazione recente o batterie hello potrebbero essere in fase di manutenzione periodica. Osservare il sistema hello per 12 ore prima di procedere.
  
  * Se lo stato di hello è ancora **danneggiato** dopo 12 ore di energia elettrica tooAC connessione continua con hello controller e i PCM in esecuzione, quindi hello batteria deve toobe sostituito. [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) per un modulo della batteria di backup sostitutivo.
  * Se lo stato di hello diventa OK dopo 12 ore, hello batteria è operativa ed era soltanto necessario un costo di manutenzione.
* Se non si è verificata un'interruzione di alimentazione e hello PCM è acceso e connesso power tooAC, toobe sostituito batteria hello. [Contattare il supporto Microsoft](storsimple-contact-microsoft-support.md) tooorder un modulo batteria di backup sostitutivo.

> [!IMPORTANT]
> Dispose di hello non riuscita della batteria in base toonational e alle normative locali. 
> 
> 

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).

