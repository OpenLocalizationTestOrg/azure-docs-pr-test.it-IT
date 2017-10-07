---
title: failover aaaStorSimple, il ripristino di emergenza per i dispositivi 8000 serie | Documenti Microsoft
description: Informazioni su come toofail tramite il toohello dispositivo StorSimple stesso dispositivo.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a>Eseguire il failover del dispositivo di toosame dispositivo fisico StorSimple

## <a name="overview"></a>Panoramica

In questa esercitazione descrive hello passaggi necessari toofail su un tooitself di dispositivo fisico StorSimple 8000 series se si verifica un'emergenza. StorSimple Usa dati toomigrate funzionalità hello dispositivo failover da un dispositivo fisico di origine nel dispositivo fisico di hello datacenter tooanother. materiale sussidiario Hello in questa esercitazione si applica a dispositivi fisici serie 8000 tooStorSimple con le versioni di software Update 3 e successive.

toolearn ulteriori informazioni su failover del dispositivo e la modalità di toorecover utilizzato da un'emergenza, andare troppo[Failover e ripristino di emergenza per i dispositivi della serie StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).

toofail su un dispositivo fisico tooanother dispositivo fisico, andare troppo[failover toohello stesso dispositivo fisico StorSimple](storsimple-8000-device-failover-physical-device.md). toofail su un tooa dispositivo fisico StorSimple Appliance di Cloud di StorSimple, andare troppo[failover tooa StorSimple Appliance di Cloud](storsimple-8000-device-failover-cloud-appliance.md).


## <a name="prerequisites"></a>Prerequisiti

- Assicurarsi di aver esaminato considerazioni hello per failover del dispositivo. Per ulteriori informazioni, visitare troppo[considerazioni comuni per il failover dispositivo](storsimple-8000-device-failover-disaster-recovery.md).


## <a name="steps-toofail-over-toohello-same-device"></a>Passaggi toofail su toohello stesso dispositivo

Eseguire operazioni se è necessario toofail su toohello hello stesso dispositivo.

1. Creare snapshot cloud di tutti i volumi di hello nel dispositivo. Per ulteriori informazioni, visitare troppo[toocreate i backup del servizio di utilizzare Gestione periferiche di StorSimple](storsimple-8000-manage-backup-policies-u2.md).
2. Reimpostare le impostazioni predefinite del dispositivo toofactory. Seguire hello dettagliate in [come impostazioni predefinite tooreset un toofactory dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).
3. Il servizio di gestione di dispositivi StorSimple toohello go e quindi selezionare **dispositivi**. In hello **dispositivi** pannello dispositivo precedente hello dovrebbe risultare **Offline**.

    ![Dispositivo di origine offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. Configurare il dispositivo e registrarlo di nuovo nel servizio Gestione dispositivi StorSimple. Hello dispositivo appena registrato dovrebbe risultare **pronto tooset backup**. nome del dispositivo per il nuovo dispositivo di hello Hello è hello stesso dispositivo precedente hello ma aggiunto con una numerazione tooindicate dispositivo hello stato reimpostazione toofactory predefinito e registrati nuovamente.

    ![Dispositivo appena registrato tooset pronto backup](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. Per una nuova periferica hello, completare la configurazione di dispositivo hello. Per ulteriori informazioni, visitare troppo[passaggio 4: completare l'installazione minima del dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup). In hello **dispositivi** pannello stato hello del dispositivo hello diventa troppo**Online**.

   > [!IMPORTANT]
   > **Completare la configurazione minima di hello prima o il ripristino di emergenza potrebbe non riuscire.**

    ![Dispositivo appena registrato online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. Selezionare il dispositivo precedente hello (stato non in linea) e dalla barra dei comandi di hello, fare clic su **failover**. In hello **failover** pannello selezionare dispositivo precedente come origine di hello e specificare il dispositivo di destinazione hello hello appena registrato dispositivo.

    ![Riepilogo del failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    Per istruzioni dettagliate, vedere troppo[failover dispositivo fisico tooanother](#fail-over-to-another-physical-device).

7. Viene creato un processo di ripristino di dispositivo che è possibile monitorare da hello **processi** blade.

8. Al termine il processo di hello, accedere di nuovo dispositivo hello e passare toohello **contenitori di volumi** blade. Verificare che tutti i contenitori di volumi di hello dispositivo precedente hello siano stati migrati toohello nuovo dispositivo.

   ![Migrazione dei contenitori dei volumi eseguita](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. Al termine del failover hello, è possibile disattivare ed eliminare dispositivo precedente hello dal portale hello. Selezionare hello precedente dispositivo (offline), pulsante destro del mouse, quindi **disattiva**. Dopo la disattivazione di dispositivo hello, hello del dispositivo hello viene aggiornato.

     ![Dispositivo di origine disattivato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. Seleziona hello disattivato dispositivo pulsante destro del mouse e quindi selezionare **eliminare**. Ciò elimina dispositivo hello dall'elenco di hello dei dispositivi.

    ![Dispositivo di origine eliminato](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a>Passaggi successivi

* Dopo aver eseguito un failover, potrebbe essere troppo[disattivare o eliminare il dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).
* Per informazioni su come toouse hello dispositivo StorSimple Manager service, andare troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

