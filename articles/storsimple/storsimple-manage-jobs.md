---
title: aaaView e gestire i processi di StorSimple | Documenti Microsoft
description: "Descrive una pagina di processi del servizio StorSimple Manager hello e come toouse è tootrack recenti, corrente e pianificate i processi di backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 55922cd0-d490-48eb-938a-012a67c1c09e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: b7341270e37a9f2530a8da1fb7c54f6b699c699c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs"></a>Utilizzare tooview servizio StorSimple Manager di hello e gestire i processi di StorSimple
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Panoramica
Hello **processi** pagina fornisce un unico portale centralizzato per la visualizzazione e gestione di processi avviati nei dispositivi connessi servizio StorSimple Manager tooyour. È possibile visualizzare i processi pianificati, in esecuzione, completati e non riusciti per più dispositivi. I risultati vengono presentati in un formato tabulare. 

![Pagina dei processi](./media/storsimple-manage-jobs/HCS_JobsPage.png)

È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:

* **Stato** : i processi possono essere in esecuzione, pianificati, non riusciti, completati, in fase di annullamento o annullati.
* **Tipo**: i processi possono essere creati come risultato di un backup su richiesta o pianificato (**Esegui backup**), di una clonazione, di un ripristino del dispositivo o di un'operazione di aggiornamento.
* **Dispositivi** : i processi vengono avviati in un determinato servizio tooyour di dispositivo connesso.
* **Da e a** : i processi possono essere intervallo di filtrato hello in base a data e ora.

Hello processi filtrati possono quindi essere caratterizzati sulla base di hello della hello gli attributi seguenti:

* **Tipo** : backup, clonazione, ripristino, failover o aggiornamento.
* **Stato** : in esecuzione, pianificato, non è riuscito, completato, in fase di annullamento o annullato.
* **Entità** – processi hello possono essere associati a un volume, un criterio di backup o un dispositivo. Un processo di clonazione è associato a un volume, mentre un processo di backup pianificato è associato a un criterio di backup. Viene creato un processo di dispositivo a causa di un ripristino di emergenza (DR) o di un'operazione di ripristino.
* **Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.
* **Avvio** : ora di hello inizio processo hello.
* **Lo stato di avanzamento** : hello percentuale di completamento di un processo in esecuzione. Per un processo completato deve sempre essere 100%.

elenco di Hello dei processi viene aggiornato ogni 30 secondi.

È possibile eseguire hello seguenti le azioni correlate al processo in questa pagina:

* Visualizza i dettagli dei processi
* Annullare un processo

## <a name="view-job-details"></a>Visualizza i dettagli dei processi
Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.

#### <a name="tooview-job-details"></a>dettagli dei processi tooview
1. In hello **processi** pagina, visualizzare i processi di hello desiderati eseguendo una query con filtri appropriati. È possibile cercare processi completati, in esecuzione o annullati.
2. Selezionare un processo.
3. Nella parte inferiore di hello della pagina hello, fare clic su **dettagli**.
4. In hello **dettagli dei processi di Backup** nella finestra di dialogo è possibile visualizzare lo stato di hello, dettagli, le statistiche temporali e le statistiche sui dati.

## <a name="cancel-a-job"></a>Annullare un processo
Eseguire hello seguendo i passaggi toocancel un processo in esecuzione.

### <a name="toocancel-a-job"></a>toocancel un processo
1. In hello **processi** pagina, visualizzare i processi in esecuzione di hello che si desidera toocancel eseguendo una query con filtri appropriati.
2. Selezionare il processo di hello.
3. Nella parte inferiore di hello della pagina hello, fare clic su **Annulla**.
4. Alla richiesta di conferma fare clic su **Sì**.

Questo processo ora viene annullato.

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su come troppo[gestire i criteri di backup di StorSimple](storsimple-manage-backup-policies.md).
* Informazioni su come troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).

