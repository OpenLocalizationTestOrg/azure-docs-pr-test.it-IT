---
title: aaaView e gestire i processi di Array virtuale StorSimple | Documenti Microsoft
description: "Viene descritto pagina processi del servizio di gestione di dispositivi StorSimple hello e come toouse è tootrack recenti e corrente dei processi di hello Array virtuale StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Utilizzare processi tooview del servizio di gestione di dispositivi StorSimple hello per hello Array virtuale StorSimple
## <a name="overview"></a>Panoramica
Hello **processi** pannello fornisce un unico portale centralizzato per visualizzare e gestire i processi avviati su array virtuale che sono connessi tooyour servizio di gestione di dispositivi StorSimple. È possibile visualizzare i processi in esecuzione, completati e non riusciti per più dispositivi virtuali. I risultati vengono presentati in un formato tabulare.

![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

È possibile trovare rapidamente i processi di hello desiderati applicando filtri ai campi, ad esempio:

* **Intervallo di tempo** : i processi possono essere intervallo di filtrato hello in base a data e ora.
* **Dispositivi** : i processi vengono avviati in un servizio tooyour specifico dispositivo connesso. Hello processi filtrati possono quindi essere caratterizzati in base a hello gli attributi seguenti:
  
  * **Nome** : nome del processo hello può essere **tutti**, **Backup**, **Clone**, **failover**, **scaricare gli aggiornamenti** , o **installare gli aggiornamenti**.
  * **Stato**: i processi possono essere **Tutto**, **In corso**, **Riuscito**, **Operazione non riuscita** o **Annullato**.
  * **Entità** – processi hello possono essere associati a un volume, condivisione o dispositivo.
  * **Dispositivo** : hello nome di dispositivo hello in cui hello processo è stato avviato.
  * **Avviato su** : ora di hello inizio processo hello.
  * **Durata** : hello durata per il processo di hello è stata eseguita.
* **Stato** : è possibile cercare tutti i processi in esecuzione, completati o non riusciti.
* **Tipo di processo** : tipo di processo hello può essere all, eseguire il backup, ripristino failover, scaricare gli aggiornamenti o installare gli aggiornamenti.

elenco di Hello dei processi viene aggiornato ogni 30 secondi.

## <a name="view-job-details"></a>Visualizza i dettagli dei processi
Eseguire i seguenti passaggi tooview hello dettagli di qualsiasi processo hello.

#### <a name="tooview-job-details"></a>dettagli dei processi tooview
1. In hello **processi** blade, visualizzazione hello processi desiderati eseguendo una query con filtri appropriati. È possibile cercare processi completati o in esecuzione.
2. Selezionare un processo dall'elenco tabulare di hello dei processi.
   
    ![Pannello Processi](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. Nella parte inferiore di hello della pagina hello, fare clic su **dettagli**.
4. In hello **dettagli** nella finestra di dialogo è possibile visualizzare lo stato, dettagli e le statistiche temporali. Hello nella figura seguente viene illustrato un esempio di hello **dettagli dei processi di Backup** la finestra di dialogo.
   
    ![Dettagli del processo](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Errore del processo quando viene sospesa macchina virtuale hello nell'hypervisor hello
Quando un processo è in corso nel dispositivo hello (macchina virtuale in hypervisor provisioning) e Array virtuale StorSimple è sospeso per più di 15 minuti, hello processo non riesce. Questa scadenza ora Array virtuale StorSimple tooyour viene sincronizzata con il tempo di Microsoft Azure hello. 

Verrà visualizzato il seguente errore hello: "l'ora del dispositivo non è sincronizzato con il tempo di Microsoft Azure hello da più di 15 minuti. Verificare che hello hypervisor e tempi di hello dispositivo siano sincronizzati con un NTP si trova. Assicurarsi che non vi siano problemi di connettività. problemi di connettività tootroubleshoot, eseguire i test diagnostici da hello interfaccia web locale del dispositivo virtuale."

Questi errori si applicano i processi toobackup, ripristino, aggiornamento e il failover. Se viene eseguito il provisioning di macchina virtuale in Hyper-V, macchina hello infine Sincronizza ora con l'hypervisor. Quando ciò accade, è possibile riavviare il processo.

## <a name="next-steps"></a>Passaggi successivi
[Informazioni su come toouse hello tooadminister dell'interfaccia utente web locale l'Array virtuale StorSimple](storsimple-ova-web-ui-admin.md).

