---
title: failover aaaStorSimple, ripristino di emergenza tooa StorSimple Appliance di Cloud | Documenti Microsoft
description: Informazioni su cloud toofail tramite il tooa di dispositivo fisico StorSimple 8000 series appliance.
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
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a>Eseguire il failover tooyour StorSimple Appliance di Cloud

## <a name="overview"></a>Panoramica

Questa esercitazione descrive hello passaggi necessari toofail su un tooa di dispositivi fisici serie StorSimple 8000 StorSimple Appliance di Cloud se si verifica un'emergenza. StorSimple Usa dati toomigrate funzionalità hello dispositivo failover da un dispositivo fisico di origine nel dispositivo di hello datacenter tooa cloud in esecuzione in Azure. materiale sussidiario di Hello in questa esercitazione si applica a dispositivi fisici serie di tooStorSimple 8000 e Appliance di cloud con le versioni di software Update 3 e successive.

toolearn ulteriori informazioni su failover del dispositivo e la modalità di toorecover utilizzato da un'emergenza, andare troppo[Failover e ripristino di emergenza per i dispositivi della serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail su un dispositivo di fisica della tooanother dispositivo fisico del StorSimple, andare troppo[failover dispositivo fisico StorSimple tooa](storsimple-8000-device-failover-physical-device.md). toofail su tooitself un dispositivo, andare troppo[failover toohello stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-same-device.md).

## <a name="prerequisites"></a>Prerequisiti

- Assicurarsi di aver esaminato considerazioni hello per failover del dispositivo. Per ulteriori informazioni, visitare troppo[considerazioni comuni per il failover dispositivo](storsimple-8000-device-failover-disaster-recovery.md).

- Prima di eseguire questa procedura, è necessario disporre di un'appliance cloud StorSimple creata e configurata. Se in esecuzione Aggiorna versione 3 o versioni successive, è consigliabile utilizzare un accessorio 8020 cloud per hello ripristino di emergenza. modello 8020 Hello è 64 TB e utilizza l'archiviazione Premium. Per ulteriori informazioni, visitare troppo[distribuire e gestire un'applicazione Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="steps-toofail-over-tooa-cloud-appliance"></a>Passaggi toofail su dispositivo cloud tooa

Eseguire hello seguendo i passaggi toorestore hello tooa di destinazione del dispositivo StorSimple Appliance di Cloud.

1.  Verificare il contenitore del volume hello desiderato toofail siano associati snapshot nel cloud. Per ulteriori informazioni, visitare troppo[toocreate i backup del servizio di utilizzare Gestione periferiche di StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Il servizio di gestione di dispositivi StorSimple tooyour, fare clic su **dispositivi**. In hello **dispositivi** blade, andare toohello elenco di dispositivi connessi con il servizio.
    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)
3. Selezionare e fare clic sul dispositivo di origine. contenitori di volumi hello che si desidera toofail sulla periferica di origine di Hello. Andare troppo**Impostazioni > contenitori di volumi**.

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. Selezionare un contenitore di volumi di cui si desidera toofail su tooanother dispositivo. Fare clic su elenco hello toodisplay hello volumi contenitore di volumi all'interno del contenitore. Selezionare un volume, il pulsante destro del mouse e fare clic su **non in linea** tootake offline volume hello.

    ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. Ripetere questo processo per tutti i volumi di hello hello contenitore del volume.

     ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. Passaggio di ripetizione hello precedente per tutti i contenitori dei volumi di hello desideri toofail su tooanother dispositivo.

7. Tornare indietro toohello **dispositivi** blade. Dalla barra dei comandi di hello, fare clic su **failover**.

    ![Fare clic su Failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. In hello **failover** pannello eseguire hello alla procedura seguente:
   
    1. Fare clic su **Origine**. Selezionare hello volume contenitori toofail su. **Hello solo contenitori di volumi con snapshot cloud associati e i volumi offline sono visualizzati.**
        ![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png) (Seleziona origine)
    2. Fare clic su **Destinazione**. Selezionare un'applicazione cloud di destinazione dall'elenco a discesa hello dei dispositivi disponibili. **Solo i dispositivi di hello che dispongono di sufficiente capacità tooaccommodate origine i contenitori dei volumi vengono visualizzati nell'elenco di hello.**

        ![Selezionare la destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. Esaminare le impostazioni di failover hello in **riepilogo** e selezionare la casella di controllo di hello, che indica che i volumi hello nei contenitori di volumi selezionati sono offline. 

        ![Esaminare le impostazioni di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. Viene creato un processo di failover. failover hello toomonitor di processo, fare clic su notifica del processo hello.

    ![Monitorare il processo di failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. Dopo aver completato il failover hello, tornare indietro toohello **dispositivi** blade.

    1. Selezionare il dispositivo hello che è stato utilizzato come destinazione di hello per il failover hello.

       ![Selezionare il dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. Fare clic su **Contenitori di volume**. Tutti i contenitori di volumi di hello, insieme ai volumi hello dispositivo precedente hello, dovrebbero essere elencati.

       Se il contenitore del volume hello che è stato eseguito il failover ha aggiunto in locale i volumi, tali volumi vengono eseguiti il failover come volumi a livelli. I volumi aggiunti in locale non sono attualmente supportati in un'appliance cloud StorSimple.

       ![Visualizzare i contenitori dei volumi di destinazione](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a>Passaggi successivi

* Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

* Per informazioni su come toouse hello dispositivo StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

