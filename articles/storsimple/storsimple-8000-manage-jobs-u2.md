---
title: aaaView e gestire i processi per StorSimple serie 8000 | Documenti Microsoft
description: "Viene descritto pannello processi del servizio di gestione di dispositivi StorSimple hello e come toouse è tootrack recenti, corrente e pianificate i processi di backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Utilizzare tooview servizio di gestione di dispositivi StorSimple hello e gestire i processi (Update 3 e versioni successivo)

## <a name="overview"></a>Panoramica
Hello **processi** pannello fornisce un unico portale centralizzato per la visualizzazione e gestione di processi avviati nei dispositivi connessi tooyour servizio di gestione di dispositivi StorSimple. È possibile visualizzare i processi pianificati, in esecuzione, completati, annullati e non riusciti per più dispositivi. I risultati vengono presentati in un formato tabulare.

![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:

* **Stato**: i processi possono essere in corso, completati, annullati, non riusciti, annullati o completati con errori.
* **Intervallo di tempo** : i processi possono essere intervallo di filtrato hello in base a data e ora. gli intervalli hello sono oltre 1 ora, ultime 24 ore, negli ultimi 7 giorni, agli ultimi 30 giorni, l'anno o data personalizzato.
* **Tipo** : il tipo di processo hello può essere pianificati backup, backup manuale, backup di ripristino, clonare volume, eseguire il failover contenitori di volumi, creare volume aggiunto in locale, modifica del volume, installare gli aggiornamenti, raccogliere i log di supporto e creare appliance di cloud.
* **Dispositivi** : i processi vengono avviati in un determinato servizio tooyour di dispositivo connesso.
  
Hello processi filtrati possono quindi essere caratterizzati sulla base di hello della hello gli attributi seguenti:
  
* **Nome**: backup pianificato, backup manuale, backup di ripristino, volume clone, contenitori dei volumi con failover, volume aggiunto in locale, volume modificato, installazione di aggiornamenti, raccolta di log di supporto e creazione di appliance cloud.
* **Stato** : in esecuzione, completati, annullati, non riusciti, in fase di annullamento o completati con errori.
* **Entità** – processi hello possono essere associati a un volume, un criterio di backup o un dispositivo. Ad esempio, un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup. Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.
* **Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.
* **Avviato su** : ora di hello inizio processo hello.
* **Durata** : processo di hello hello timer toocomplete obbligatorio.

elenco di Hello dei processi viene aggiornato ogni 30 secondi.

È possibile eseguire hello seguenti le azioni correlate al processo in questa pagina:

* Visualizza i dettagli dei processi
* Annullare un processo

## <a name="view-job-details"></a>Visualizza i dettagli dei processi
Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.

#### <a name="tooview-job-details"></a>dettagli dei processi tooview
1. Il servizio di gestione di dispositivi StorSimple tooyour, quindi fare clic su **processi**.

2. In hello **processi** blade, visualizzazione hello processi desiderati eseguendo una query con filtri appropriati. È possibile cercare processi completati, in esecuzione o annullati.

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Selezionare e fare clic su un processo.

    ![Pannello Processi](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. Nel Pannello di dettagli processo hello, è possibile visualizzare lo stato di hello, dettagli, le statistiche temporali e le statistiche sui dati.
   
    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Annullare un processo
Eseguire hello seguendo i passaggi toocancel un processo in esecuzione.

> [!NOTE]
> Alcuni processi, ad esempio modifica di un tipo di volume hello toochange volume o espansione di un volume, non possono essere annullati.


### <a name="toocancel-a-job"></a>toocancel un processo
1. In hello **processi** pagina, visualizzare i processi in esecuzione di hello che si desidera toocancel eseguendo una query con filtri appropriati. Selezionare il processo di hello.

2. Fare clic sul menu di scelta rapida hello tooinvoke hello processo selezionato e fare clic su **Annulla**.

    ![Dettagli del processo](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Alla richiesta di conferma fare clic su **Sì**. Questo processo ora viene annullato.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[gestire i criteri di backup di StorSimple](storsimple-8000-manage-backup-policies-u2.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio di gestione di dispositivi StorSimple dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

