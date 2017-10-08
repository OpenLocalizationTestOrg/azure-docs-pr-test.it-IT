---
title: note sulla versione di aggiornamento 5 di serie 8000 aaaStorSimple | Documenti Microsoft
description: "Descrive le nuove funzionalità hello, problemi e soluzioni alternative per StorSimple 8000 Series aggiornamento 5."
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
ms.date: 08/23/2017
ms.author: alkohli
ms.openlocfilehash: 9eb8ffb97b41ce3d4f1ffdf2975f904d0a2958e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-8000-series-update-5-release-notes"></a>Note sulla versione dell'aggiornamento 5 di StorSimple serie 8000

## <a name="overview"></a>Panoramica

Hello note sulla versione seguenti descrivono le nuove funzionalità di hello e identificare i problemi critici aperti di hello per StorSimple 8000 Series aggiornamento 5. Contengono inoltre un elenco degli aggiornamenti software di StorSimple hello inclusi in questa versione.

Aggiornamento 5 può essere dispositivo StorSimple tooany applicato esecuzione Update 0,1 tramite aggiornamento 4. versione del dispositivo Hello associata con aggiornamento 5 è 6.3.9600.17845.

Esaminare le informazioni di hello contenute in versione di hello note prima di distribuire hello aggiornare nella soluzione StorSimple.

> [!IMPORTANT]
> * L'aggiornamento 5 include software per dispositivi, firmware del disco, aggiornamenti di sicurezza del sistema operativo e altri aggiornamenti di sicurezza. Sono necessari circa 4 ore tooinstall questo aggiornamento. L'aggiornamento firmware del disco è problematico e comporta un tempo di inattività per il dispositivo. Si consiglia di applicare l'aggiornamento 5 tookeep dispositivo aggiornato.
> * Per le nuove versioni, non sarà possibile visualizzare gli aggiornamenti immediatamente perché è un'implementazione graduale dei hello aggiornamenti. Attendere alcuni giorni e provare a cercare nuovamente gli aggiornamenti, perché verranno presto resi disponibili.

## <a name="whats-new-in-update-5"></a>Novità dell'aggiornamento 5

Hello seguenti importanti miglioramenti e correzioni di bug sono state apportate in Update 5.

* **Utilizzo di Azure Active Directory (AAD) tooauthenticate con il servizio di gestione di dispositivi StorSimple** – dall'aggiornamento 5 in poi, Azure Active Directory è tooauthenticate utilizzato con il servizio di gestione di dispositivi StorSimple hello. il meccanismo di autenticazione precedente Hello sarà deprecato entro dicembre 2017. Tutti gli utenti di hello devono includere hello nuovi autenticazione URL le regole firewall. Per ulteriori informazioni, visitare troppo[URL autenticazione elencati in requisiti di rete per il dispositivo StorSimple hello](storsimple-8000-system-requirements.md#url-patterns-for-azure-portal).

    Se l'URL di hello autenticazione non è incluso nelle regole di firewall hello, hello verrà visualizzato un avviso critico che non è stato possibile autenticare il dispositivo StorSimple con servizio hello. Se agli utenti di hello visualizzare questo avviso, è necessario tooinclude hello nuova autenticazione URL. Per ulteriori informazioni, visitare troppo[StorSimple rete avvisi](storsimple-8000-manage-alerts.md#networking-alerts).

* **Nuova versione di StorSimple Snapshot Manager** -Con l'aggiornamento 5 viene rilasciata una nuova versione di StorSimple Snapshot Manager. È consigliabile che l'aggiornamento di versione toothis. Questa versione è compatibile con tutti i dispositivi StorSimple hello che eseguono l'aggiornamento 3 o versione successiva. Per ulteriori informazioni, visitare troppo[distribuire gestione Snapshot StorSimple](storsimple-snapshot-manager-deployment.md).


## <a name="issues-fixed-in-update-5"></a>Problemi risolti nell'aggiornamento 5

Hello nella tabella seguente fornisce un riepilogo dei problemi che sono stati risolti in aggiornamento 5.

| No | Funzionalità | Problema | Si applica toophysical dispositivo | Si applica toovirtual dispositivo |
| --- | --- | --- | --- | --- |
| 1 |Comunicazione remota di Windows PowerShell |Nella versione precedente di hello, un utente riceve un errore durante il tentativo di tooestablish toohello una connessione remota StorSimple Appliance di Cloud tramite Windows PowerShell. In questa versione il problema è stato corretto una volta individuata la causa radice. |No |Sì |
| 2 |Modelli di larghezza di banda |Nella versione precedente, si è verificato un problema con i modelli di larghezza di banda che ha comportato la larghezza di banda inferiore rispetto a quale dispositivo hello è stata configurata per. Questo problema è stato risolto in questa versione. |Sì |Sì |
| 3 |Failover |Nella versione precedente, quando un dispositivo con un numero elevato di volumi è stato eseguito il failover tooanother dispositivo che esegue l'aggiornamento 4, hello processo avrà esito negativo durante il tentativo di record di controllo di accesso hello tooapply. Tale problema è stato corretto in questa versione. |Sì |Sì |



## <a name="known-issues-in-update-5-from-previous-releases"></a>Problemi noti nell'aggiornamento 5 rispetto alle versioni precedenti

Nessun nuovo problema noto nell'aggiornamento 5. Per un elenco di problemi trasferito tooUpdate 5 rispetto alle versioni precedenti, andare troppo[note sulla versione Update 3](storsimple-update3-release-notes.md#known-issues-in-update-3).

## <a name="serial-attached-scsi-sas-controller-and-firmware-updates-in-update-5"></a>Aggiornamenti firmware e controller SAS (Serial-attached SCSI) presenti nell'aggiornamento 5

Questa versione dispone degli aggiornamenti del controller SAS e del firmware e driver LSI. Per ulteriori informazioni su come tooinstall questi aggiornamenti, vedere [installare aggiornamento 5](storsimple-8000-install-update-5.md) nel dispositivo StorSimple.

## <a name="storsimple-cloud-appliance-updates-in-update-5"></a>Aggiornamenti all'appliance cloud StorSimple presenti nell'aggiornamento 5

Questo aggiornamento non può essere applicato toohello StorSimple Appliance di Cloud (noto anche come hello dispositivo virtuale). Nuovi accessori di cloud necessario toobe creato utilizzando l'immagine di hello aggiornamento 5. Per informazioni su come un'applicazione Cloud StorSimple, toocreate andare troppo[distribuire e gestire un'applicazione Cloud StorSimple](storsimple-8000-cloud-appliance-u2.md).

## <a name="next-step"></a>Passaggio successivo

Informazioni su come troppo[installare aggiornamento 5](storsimple-8000-install-update-5.md) nel dispositivo StorSimple.

