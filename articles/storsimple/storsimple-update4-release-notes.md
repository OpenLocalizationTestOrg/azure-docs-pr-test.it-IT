---
title: note sulla versione di aggiornamento 4 di serie 8000 aaaStorSimple | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series aggiornamento 4."
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
ms.date: 04/04/2017
ms.author: alkohli
ms.openlocfilehash: 4bca8ca222e6706fd6eaf56b702b0d34b6ffd1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-4-release-notes"></a>Note sulla versione dell'aggiornamento 4 di StorSimple serie 8000

## <a name="overview"></a>Panoramica

Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series aggiornamento 4. Contengono inoltre un elenco degli aggiornamenti software di StorSimple hello inclusi in questa versione. 

È possibile dispositivo StorSimple tooany applicato esegue versione (GA) o 0,1 aggiornamento-aggiornamento 3.1 Update 4. versione del dispositivo Hello associata con l'aggiornamento 4 è 6.3.9600.17820.

Esaminare informazioni hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.

> [!IMPORTANT]
> * L'aggiornamento 4 include software per dispositivi, firmware USM, firmware e driver LSI, firmware del disco, Storport e Spaceport, aggiornamenti di sicurezza e una serie di altri aggiornamenti del sistema operativo. Sono necessari circa 4 ore tooinstall questo aggiornamento. L'aggiornamento firmware del disco è problematico e comporta un tempo di inattività per il dispositivo. Si consiglia di applicare l'aggiornamento 4 tookeep dispositivo aggiornato. 
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Attendere alcuni giorni e quindi provare a cercare nuovamente gli aggiornamenti, perché verranno presto resi disponibili.

## <a name="whats-new-in-update-4"></a>Novità dell'aggiornamento 4

Hello seguenti importanti miglioramenti e correzioni di bug sono state apportate nell'aggiornamento 4.

* **Prontezza automatizzata algoritmi di recupero di spazio** – nell'aggiornamento 4, hello algoritmi di recupero automatico dello spazio vengono migliorate tooadjust hello recupero di spazio in base a hello previsto cicli recuperato spazio disponibile nel cloud hello. 

* **Miglioramenti delle prestazioni per i volumi aggiunti in locale** – aggiornamento 4 dispone di miglioramento delle prestazioni di hello di volumi aggiunti in locale in scenari con inserimento di dati elevata (dimensione toovolume confrontabili dati).

* **Ripristino basato su Heatmap** : hello precedenti versioni, dopo un ripristino di emergenza (ripristino di emergenza), dati hello è state ripristinate dal cloud hello in base ai modelli di accesso hello causando un rallentamento delle prestazioni. 

    Una nuova funzionalità viene implementata nell'aggiornamento 4 che tiene traccia si accede di frequente dati toocreate un heatmap quando hello dispositivo è in uso precedente tooDR (utilizzati più blocchi di dati con elevato calore mentre minore utilizzato blocchi sono calore basso). Dopo il ripristino di emergenza, StorSimple Usa hello heatmap tooautomatically ripristino e riattivare dati hello dal cloud hello. 

    Tutti hello ripristini eseguiti sono ora basati su heatmap. Per ulteriori informazioni su come heatmap tooquery e Annulla basata i processi di ripristino e riattivazione, andare troppo[di Windows PowerShell per StorSimple cmdlet riferimento](https://technet.microsoft.com/library/dn688168.aspx).

* **Lo strumento di diagnostica di StorSimple** : aggiornamento 4, una diagnostica StorSimple strumento viene rilasciato tooallow per la diagnosi di facile e risoluzione dei problemi di relativi integrità componente toosystem, rete, le prestazioni e dell'hardware. Questo strumento viene eseguito tramite hello Windows PowerShell per StorSimple. Per ulteriori informazioni, visitare troppo[risoluzione dei problemi mediante lo strumento di diagnostica di StorSimple](storsimple-8000-diagnostics.md).

* **Basato su interfaccia utente dello strumento di migrazione di StorSimple** -toothis precedente versione, migrazione dei dati dalla serie 5000 7000 necessari hello utenti tooexecute una parte del flusso di lavoro di migrazione hello utilizzando l'interfaccia di hello Azure PowerShell. In questa versione, un semplice da utilizzare migrazione StorSimple basato su interfaccia utente dello strumento viene reso disponibile per il supporto toofacilitate hello stesso flusso di lavoro di migrazione. Questo strumento consentirà inoltre per il consolidamento di hello di bucket di ripristino. 

* **Le modifiche correlate a FIPS** : questa versione successiva, FIPS è abilitata per impostazione predefinita su tutti i dispositivi della serie StorSimple 8000 hello per entrambi hello Microsoft Azure per enti pubblici e gli account di cloud pubblico di Azure.

* **Aggiornare le modifiche** : In questa versione, i bug di tooupdate correlati sono stati corretti gli errori.

* **Avviso per gli errori del disco** -viene aggiunto un nuovo avviso che avvisa l'utente hello imminente di errori del disco in questa versione. Se si verifica questo avviso, contattare il supporto Microsoft tooship un disco di sostituzione. Per ulteriori informazioni, visitare troppo[avvisi relativi all'hardware sul dispositivo StorSimple](storsimple-manage-alerts.md#hardware-alerts).

* **Modifiche di sostituzione controller** -viene aggiunto un cmdlet che consente di hello utente tooquery hello stato processo di sostituzione del controller hello in questa versione. Per ulteriori informazioni, visitare toohello [stato sostituzione del controller cmdlet tooquery](https://technet.microsoft.com/library/dn688168.aspx).


## <a name="issues-fixed-in-update-4"></a>Problemi risolti nell'aggiornamento 4

Hello nella tabella seguente fornisce un riepilogo dei problemi che sono stati risolti nell'aggiornamento 4.    

| No | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Failover |In hello versione precedente, dopo il failover hello, vi è stato un problema correlato toocleanup osservati presso il cliente hello. Tale problema è stato corretto in questa versione. |Sì |Sì |
| 2 |Volumi aggiunti in locale |Nella versione precedente di hello, durante la creazione del volume un toorelated problema per i volumi aggiunti in locale che può determinare errori di creazione dei volumi. In questa versione il problema è stato corretto una volta individuata la causa radice. |Sì |No |
| 3 |Pacchetto di supporto |Nella versione precedente, sono stati pacchetto tooSupport correlati problemi che comporta un'eccezione System.OutOfMemory o altri errori risultanti in un errore durante la creazione del pacchetto di supporto. Tali bug sono stati risolti in questa versione. |Sì |Sì |
| 4 |Monitoraggio |Nella versione precedente, non esiste un problema correlato grafici toomonitoring per i volumi aggiunti in locale in cui è stato visualizzato consumo EB. Questo bug è stato risolto in questa versione. |Sì |Sì |
| 5 |Migrazione |Nella versione precedente, sono stati affidabilità di toohello correlati diversi problemi di migrazione da dispositivi della serie too8000 serie 5000 7000. I problemi sono stati risolti in questa versione. |Sì |Sì |
| 6 |Aggiornare |Nelle versioni precedenti, se si è verificato un errore di aggiornamento, i controller di hello verrebbero in modalità di ripristino e pertanto utente hello non è possibile procedere con l'aggiornamento di hello e sarebbe necessario toocontact supporto Microsoft. <br> In questa versione il comportamento è stato modificato. Se l'utente hello dispone di un errore di aggiornamento dopo che entrambi i controller hello sono in esecuzione hello stessa versione di aggiornamento 4, hello controller non passi alla modalità di ripristino. Se l'utente hello si verifica questo errore, è consigliabile che attendere un bit e quindi ripetere l'aggiornamento di hello. Riprova Hello potrebbe avere esito positivo. Se i tentativi di hello non riesce, quindi contattare il supporto Microsoft. |Sì |Sì |


## <a name="known-issues-in-update-4-from-previous-releases"></a>Problemi noti nell'aggiornamento 4 rispetto alle versioni precedenti

Nessun nuovo problema noto nell'aggiornamento 4. Per un elenco di problemi trasferito tooUpdate 4 rispetto alle versioni precedenti, andare troppo[note sulla versione Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-4"></a>Aggiornamenti firmware e controller SAS presenti nell'aggiornamento 4

Questa versione dispone degli aggiornamenti del controller SAS e del firmware e driver LSI. Per ulteriori informazioni su come tooinstall questi aggiornamenti, vedere [installare l'aggiornamento 4](storsimple-install-update-4.md) nel dispositivo StorSimple.

## <a name="virtual-device-updates-in-update-4"></a>Aggiornamenti del dispositivo virtuale nell'aggiornamento 4

Questo aggiornamento non può essere applicato toohello StorSimple Appliance di Cloud (noto anche come hello dispositivo virtuale). Nuovi dispositivi virtuali saranno necessario toobe creato. 

## <a name="next-step"></a>Passaggio successivo

Informazioni su come troppo[installare l'aggiornamento 4](storsimple-install-update-4.md) nel dispositivo StorSimple.

