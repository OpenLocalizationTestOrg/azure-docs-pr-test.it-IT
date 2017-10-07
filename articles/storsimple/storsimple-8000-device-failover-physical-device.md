---
title: failover aaaStorSimple, dispositivo fisico serie StorSimple 8000 tooa ripristino d'emergenza | Documenti Microsoft
description: Informazioni su come toofail tramite il dispositivo fisico StorSimple 8000 series dispositivo fisico tooanother.
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
ms.date: 05/03/2017
ms.author: alkohli
ms.openlocfilehash: 29d2576a96c446ff5ffcd98dcd0f5a07f1ab08ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooa-storsimple-8000-series-physical-device"></a>Eseguire il failover al dispositivo fisico di tooa StorSimple 8000 series

## <a name="overview"></a>Panoramica

In questa esercitazione viene hello passaggi necessari toofail su un dispositivo StorSimple serie 8000 dispositivo fisico tooanother StorSimple fisico, se una situazione di emergenza. StorSimple Usa dati toomigrate funzionalità hello dispositivo failover da un dispositivo fisico di origine nel dispositivo fisico di hello datacenter tooanother. materiale sussidiario Hello in questa esercitazione si applica a dispositivi fisici serie 8000 tooStorSimple con le versioni di software Update 3 e successive.

toolearn ulteriori informazioni su failover del dispositivo e la modalità di toorecover utilizzato da un'emergenza, andare troppo[Failover e ripristino di emergenza per i dispositivi della serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail su un tooa dispositivo fisico StorSimple Appliance di Cloud di StorSimple, andare troppo[failover tooa StorSimple Appliance di Cloud](storsimple-8000-device-failover-cloud-appliance.md). toofail su tooitself un dispositivo fisico, andare troppo[failover toohello stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-same-device.md).


## <a name="prerequisites"></a>Prerequisiti

- Assicurarsi di aver esaminato considerazioni hello per failover del dispositivo. Per ulteriori informazioni, visitare troppo[considerazioni comuni per il failover dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- È necessario disporre di un dispositivo StorSimple serie 8000 fisico distribuito nel Data Center hello. dispositivo Hello è necessario eseguire Update 3 o versione successiva di software. Per ulteriori informazioni, visitare troppo[distribuire il dispositivo StorSimple locale](storsimple-8000-deployment-walkthrough-u2.md).


## <a name="steps-toofail-over-tooa-physical-device"></a>Passaggi toofail sul dispositivo fisico tooa

Eseguire hello seguendo i passaggi toorestore il dispositivo di destinazione di tooa dispositivo fisico.

1. Verificare il contenitore del volume hello desiderato toofail siano associati snapshot nel cloud. Per ulteriori informazioni, visitare troppo[toocreate i backup del servizio di utilizzare Gestione periferiche di StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Tooyour dispositivo StorSimple Manager, quindi fare clic su **dispositivi**. In hello **dispositivi** blade, andare toohello elenco di dispositivi connessi con il servizio.
    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev1.png)
3. Selezionare e fare clic sul dispositivo di origine. contenitori di volumi hello che si desidera toofail sulla periferica di origine di Hello. Andare troppo**Impostazioni > contenitori di volumi**.
4. Selezionare un contenitore di volumi di cui si desidera toofail su tooanother dispositivo. Fare clic su elenco hello toodisplay hello volumi contenitore di volumi all'interno del contenitore. Selezionare un volume, il pulsante destro del mouse e fare clic su **non in linea** tootake offline volume hello. Ripetere questo processo per tutti i volumi di hello hello contenitore del volume.
5. Passaggio di ripetizione hello precedente per tutti i contenitori dei volumi di hello desideri toofail su tooanother dispositivo.
6. Tornare indietro toohello **dispositivi** blade. Dalla barra dei comandi di hello, fare clic su **failover**.
    ![Fare clic su failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev2.png)
    
7. In hello **failover** pannello eseguire hello alla procedura seguente:
   
   1. Fare clic su **Origine**. vengono visualizzati i contenitori dei volumi Hello con volumi associati snapshot nel cloud. Solo i contenitori di hello visualizzati sono idonei per il failover. Nell'elenco di hello dei contenitori di volumi, selezionare i contenitori di volumi hello desiderato toofail su. **Hello solo contenitori di volumi con snapshot cloud associati e i volumi offline sono visualizzati.**

       ![Selezionare l'origine](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev5.png)
   2. Fare clic su **Destinazione**. Per i contenitori di volumi hello selezionati nel passaggio precedente hello, selezionare un dispositivo di destinazione dall'elenco a discesa hello dei dispositivi disponibili. Solo i dispositivi di hello che dispongono di sufficiente capacità tooaccommodate origine i contenitori dei volumi vengono visualizzati nell'elenco di hello.

        ![Selezionare la destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev6.png)

   3. Esaminare infine tutte le impostazioni di failover hello in **riepilogo**. Dopo avere esaminato le impostazioni di hello, selezionare la casella di controllo di hello, che indica che i volumi hello nei contenitori di volumi selezionati sono offline. Fare clic su **OK**.

       ![Esaminare le impostazioni di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev8.png)
  
8. StorSimple crea un processo di failover. Fare clic su hello processo notifica toomonitor hello il processo di failover tramite hello **processi** blade.

    Se il contenitore del volume hello che è stato eseguito il failover con volumi locali, vedrai i processi di ripristino di singole per ogni volume locale (non per i volumi a livelli) nel contenitore hello. I processi di ripristino potrebbe richiedere toocomplete un certo tempo. È probabile che il processo di failover hello può essere completata in precedenza. Questi volumi avrà garanzie locale solo dopo il completamento dei processi di ripristino hello.

    ![Monitorare il processo di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

9. Dopo aver completato il failover hello, visitare toohello **dispositivi** blade.
   
   1. Selezionare il dispositivo hello che è stato usato come dispositivo di destinazione hello per il processo di failover di hello.

       ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

   2. Passare toohello **contenitori di volumi** blade. Tutti i contenitori di volumi di hello, insieme ai volumi hello dispositivo precedente hello, dovrebbero essere elencati.

       ![Visualizzare i contenitori dei volumi di destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev16.png)


## <a name="next-steps"></a>Passaggi successivi

* Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Per informazioni su come toouse hello dispositivo StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

