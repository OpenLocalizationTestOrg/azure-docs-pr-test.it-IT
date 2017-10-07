---
title: aaaStorSimple virtuale matrice 0,4 note sulla versione Update | Documenti Microsoft
description: Viene aperta critico problemi e risoluzioni per l'esecuzione di StorSimple Virtual Array hello aggiornino 0,4.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/05/2017
ms.author: alkohli
ms.openlocfilehash: 1fd174ff483f4f7b1b4a7853c9d9573d1e948cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-04-release-notes"></a>Note sulla versione dell'aggiornamento 0.4 per l'array virtuale StorSimple

## <a name="overview"></a>Panoramica

Hello note sulla versione seguenti identificano i problemi critici aperti di hello e hello problemi risolti per gli aggiornamenti di Microsoft Azure StorSimple Virtual Array.

note sulla versione di Hello vengono aggiornati continuamente e come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire l'Array virtuale StorSimple, leggere attentamente le informazioni di hello contenute nelle note sulla versione di hello.

Aggiornamento 0,4 corrispondente versione di software toohello **10.0.10289.0**.

> [!NOTE]
> Gli aggiornamenti comportano il riavvio del dispositivo. Se i/o sono in corso, il dispositivo hello comporta tempi di inattività.


## <a name="whats-new-in-hello-update-04"></a>Novità di hello aggiornamento 0,4
L'aggiornamento 0.4 è principalmente una build di correzioni di bug a cui sono stati aggiunti alcuni miglioramenti. In questa versione, sono stati risolti diversi bug causando errori di backup in una versione precedente di hello. come indicato di seguito sono riportati i miglioramenti principali Hello e correzioni di bug:

- **Miglioramenti delle prestazioni di backup** -questa versione ha diversi miglioramenti delle prestazioni di backup hello tooimprove. Di conseguenza, i backup di hello che coinvolgono un numero elevato di file, vedere una riduzione significativa toocomplete ora hello, per i backup completi e incrementali.

- **Migliorate le prestazioni** -questa versione include miglioramenti che consentono di migliorare notevolmente le prestazioni hello quando si utilizza un numero elevato di file. Se si utilizza 2-4 milioni di file, è consigliabile che si esegua il provisioning di una matrice con i miglioramenti di 16 GB RAM toosee hello virtuale. Durante l'utilizzo dei file meno di 2 milioni, requisito minimo di hello per la macchina virtuale hello toobe 8 GB di RAM.

- **Pacchetto tooSupport miglioramenti** -miglioramenti hello includono la registrazione in statistiche hello per disco, CPU, memoria, rete e cloud nel pacchetto di supporto hello, migliorando di conseguenza il processo di hello di diagnosi e il debug di problemi dei dispositivi.

- **Limite localmente bloccato iSCSI volumi too200 GB** -per i volumi aggiunti in locale, è consigliabile limitare volume iSCSI di 200 GB tooa sull'Array virtuale StorSimple. prenotazione di locale Hello per i volumi a livelli continua toobe 10% di hello il provisioning di dimensioni del volume, ma è limitata a 200 GB. 

- **Correzioni di bug relativi al backup** -nelle versioni precedenti del software, sono presenti toobackups correlati problemi che potrebbe causare errori di backup. I bug sono stati risolti in questa versione.


## <a name="issues-fixed-in-hello-update-04"></a>Problemi risolti in hello aggiornamento 0,4

Hello nella tabella seguente fornisce un riepilogo dei problemi risolti in questa versione.

| No. | Funzionalità | Problema |
| --- | --- | --- |
| 1 |Prestazioni del backup|In hello versioni precedenti, che includono un numero elevato di file di backup di hello richiederebbe un toocomplete molto tempo (in ordine di hello di giorni). In questa versione, sia hello completo e incrementali, vedere una riduzione significativa toocompletion ora hello. |
| 2 |Pacchetto di supporto|Disco, CPU, memoria, rete e le statistiche di cloud ora vengono registrate nei log di supporto di toohello eseguendo pacchetti di supporto hello molto efficaci in risoluzione dei problemi di qualsiasi dispositivo.|
| 3 |Backup |Nelle versioni precedenti, i backup a esecuzione prolungata potrebbe causare un elaborare spazio nel dispositivo hello causando errori di backup. In questa versione viene risolto il bug, consentendo di backup non più di 5 tooqueue in una sola volta.|
| 4 |iSCSI | Nelle versioni precedenti, la prenotazione locale hello per i volumi aggiunti in locale o a più livelli è 10% delle dimensioni del volume hello il provisioning. In questa versione, la prenotazione di locale hello per tutti i volumi iSCSI (localmente bloccato o a livelli) è % too10 limitato con un massimo di fino a 200 GB (per i volumi a livelli superiori a 2 TB) in tal modo liberare più spazio sul disco locale hello. È consigliabile che i volumi hello aggiunto in locale in questa versione GB too200 limitato.|


## <a name="known-issues-in-hello-update-04"></a>Problemi noti di hello aggiornamento 0,4

Hello nella tabella seguente fornisce un riepilogo dei problemi noti per hello Array virtuale StorSimple e include problemi hello indicato versione rispetto alle versioni precedenti hello. 

| No. | Funzionalità | Problema | Soluzione alternativa/commenti |
| --- | --- | --- | --- |
| **1.** |Aggiornamenti |dispositivi di Hello virtuali creati nella versione di anteprima di hello non possono essere aggiornato tooa supportato disponibilità generale versione. |Questi dispositivi virtuali devono essere eseguire il failover per il rilascio di disponibilità generale utilizzando un flusso di lavoro di ripristino di emergenza di emergenza hello. |
| **2.** |Disco dati sottoposto a provisioning |Una volta è stato effettuato il provisioning un disco dati di una determinata dimensione specificato e creato dispositivo virtuale StorSimple corrispondente hello, è necessario non espandere o compattare il disco di dati hello. Il tentativo di toodo comporta una perdita di tutti i dati di hello nei livelli di locale hello del dispositivo hello. | |
| **3.** |Criteri di gruppo |Quando un dispositivo è aggiunto al dominio, l'applicazione di criteri di gruppo può influenzare negativamente operazione dispositivo hello. |Assicurarsi che l'array virtuale nella propria unità organizzativa (OU) di Active Directory e non oggetti Criteri di gruppo (GPO) vengono applicati tooit. |
| **4.** |Interfaccia utente Web locale |Se sono abilitate le funzionalità di sicurezza avanzate di Internet Explorer, alcune pagine dell'interfaccia utente Web locale come Risoluzione dei problemi o Manutenzione potrebbero non funzionare correttamente. Anche i pulsanti di queste pagine potrebbero non funzionare. |Disattivare le funzionalità di protezione avanzata di Internet Explorer. |
| **5.** |Interfaccia utente Web locale |In una macchina virtuale Hyper-V, hello interfacce di rete nel web hello dell'interfaccia utente vengono visualizzate come interfacce da 10 Gbps. |Questo comportamento è una reflection di Hyper-V. Hyper-V visualizza sempre 10 Gbps per le schede di rete virtuale. |
| **6.** |Volumi o condivisioni a livelli |L'intervallo di byte per le applicazioni che funzionano con hello StorSimple volumi a livelli di blocco non è supportata. Se il blocco dell'intervallo di byte è abilitato, la suddivisione in livelli di StorSimple non funziona. |Tra le misure consigliate:  <br></br>Disattivare il blocco dell'intervallo di byte nella logica dell'applicazione.<br></br>Scegliere tooput dati per questa applicazione in volumi aggiunti in locale anziché come tootiered volumi.<br></br>*Avvertenza*: quando è abilitato il blocco di intervallo di byte utilizzando locale aggiunto volumi, volume hello aggiunto in locale può essere online anche prima hello ripristino è stato completato. In questi casi, se un ripristino in corso, quindi è necessario attendere toocomplete ripristino hello. |
| **7.** |Condivisioni a livelli |Lavorare con file di grandi dimensioni può comportare una suddivisione in livelli lenta. |Quando si utilizzano file di grandi dimensioni, è consigliabile che file più grande di hello è minore di 3% delle dimensioni della condivisione hello. |
| **8.** |Capacità usata per le condivisioni |Può vedere condividere consumo quando non sono presenti dati nella condivisione di hello. Questo avviene perché la capacità di hello utilizzato per le condivisioni include i metadati. | |
| **9.** |Ripristino di emergenza |È possibile eseguire solo il ripristino di emergenza hello di toohello di server un file nello stesso dominio del dispositivo di origine hello. Dispositivo di destinazione tooa di ripristino di emergenza in un altro dominio non è supportata in questa versione. |L'implementazione è prevista per una versione futura. |
| **10.** |Azure PowerShell |i dispositivi virtuali StorSimple di Hello non possono essere gestiti tramite hello Azure PowerShell in questa versione. |Gestione di hello tutti i dispositivi virtuali hello debba essere eseguita tramite hello portale di Azure classico e interfaccia utente web locale hello. |
| **11.** |Modifica della password |console del dispositivo virtuale matrice Hello accetta solo input in formato en-US della tastiera. | |
| **12.** |CHAP |Le credenziali di autenticazione CHAP create non possono essere rimosse. Inoltre, se si modificano le credenziali dell'autenticazione CHAP hello, necessario offline i volumi di hello tootake e quindi portarli online per effetto di tootake modifica hello. |La risoluzione del problema è prevista per una versione futura. |
| **13.** |Server iSCSI |Hello 'Archiviazione utilizzato' visualizzato per un volume iSCSI potrebbe essere diverso nel servizio StorSimple Manager hello e host iSCSI hello. |host iSCSI Hello è visualizzazione filesystem hello.<br></br>dispositivo Hello vede blocchi hello allocati quando il volume di hello quando la dimensione massima di hello. |
| **14.** |File server |Se un file in una cartella è un flusso a dati alternativo (ADS) associati, annunci hello non backup o ripristino tramite il ripristino di emergenza, clonazione e ripristino a livello di elemento. | |
| **15.** |File server |I collegamenti simbolici non sono supportati. | |
| **16.** |File server |I file protetti da Windows Encrypting File System (EFS) quando copiate o archiviate in hello Array virtuale StorSimple file server di risultati in una configurazione non supportata.  | |

## <a name="next-step"></a>Passaggio successivo
[Installare l'aggiornamento 0.4](storsimple-virtual-array-install-update-04.md) nell'array virtuale StorSimple.

## <a name="references"></a>Riferimenti
Si desidera consultare le note su una versione precedente? Passare a: 

* [Note sulla versione dell'aggiornamento 0.3 per l'array virtuale StorSimple](storsimple-ova-update-03-release-notes.md)
* [Note sulla versione dell'Aggiornamento 0.1 e 0.2 per l'array virtuale StorSimple](storsimple-ova-update-01-release-notes.md)
* [Note sulla versione con disponibilità generale dell'array virtuale StorSimple](storsimple-ova-pp-release-notes.md)

