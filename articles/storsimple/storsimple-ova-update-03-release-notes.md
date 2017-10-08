---
title: note sulla versione aggiornamenti Array virtuale aaaStorSimple | Documenti Microsoft
description: Viene aperta critico 0,3 aggiornino i problemi e risoluzioni per l'esecuzione di hello Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: b197651a-3c40-4185-b23d-4c8f22cfa8f4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/15/2016
ms.author: alkohli
ms.openlocfilehash: 305e6419b248fde134abae65f3d2c241d72ffa18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-03-release-notes"></a>Note sulla versione dell'aggiornamento 0.3 per l'array virtuale StorSimple
## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti identificano i problemi critici aperti di hello e hello problemi risolti per gli aggiornamenti di Microsoft Azure StorSimple Virtual Array.

note sulla versione di Hello vengono aggiornati continuamente e come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire l'Array virtuale StorSimple, leggere attentamente le informazioni di hello contenute nelle note sulla versione di hello.

Aggiornamento 0.3 corrispondente versione di software toohello **10.0.10288.0**.

> [!NOTE]
> Gli aggiornamenti comportano il riavvio del dispositivo. Se i/o sono in corso, il dispositivo hello comporta tempi di inattività.
> 
> 

## <a name="whats-new-in-hello-update-03"></a>Novità di hello aggiornamento 0.3
L'aggiornamento 0.3 è principalmente una build per la correzione di bug. In questa versione, sono stati risolti diversi bug causando errori di backup in una versione precedente di hello.

## <a name="issues-fixed-in-hello-update-03"></a>Problemi risolti in hello aggiornamento 0.3
Hello nella tabella seguente fornisce un riepilogo dei problemi risolti in questa versione.

| No. | Funzionalità | Problema |
| --- | --- | --- |
| 1 |Backup |Un problema è stato individuato in hello versione precedente in cui i backup hello avrà esito negativo toocomplete per una condivisione file. Se si è verificato il problema, è stato generato un avviso critico sull'utente che hello toonotify servizio StorSimple Manager hello hello processo di backup avrà esito negativo. Questo problema non influisce sui dati hello nelle condivisioni hello o accedere ai dati toohello. causa radice di Hello è stato identificato e risolto in questa versione. <br></br> correzione di Hello non si applica modo retroattivo tooshares che è già visualizzato questo problema. I clienti che vengono visualizzato questo problema devono innanzitutto applicare aggiornamento 0,3, quindi contattare il supporto Microsoft tooperform un problema di hello toofix backup completo del sistema. Anziché contattando il supporto Microsoft, i clienti inoltre possono ripristinare tooa nuova condivisione da una copia di backup per le condivisioni hello interessata. |
| 2 |iSCSI |È stato rilevato un problema in hello versione precedente in cui volumi hello scompare quando si copiano i volumi di tooa dati hello Array virtuale StorSimple. In questa versione il problema è stato corretto. <br></br> correzioni di Hello diventano effettive solo in nuovi volumi. correzioni di Hello non si applicano modo retroattivo toovolumes che è già visualizzato questo problema. Toobring hello interessata volumi online tramite hello portale di Azure classico, eseguono un backup per questi volumi e quindi ripristino i volumi di toonew, si consiglia ai clienti. |

## <a name="known-issues-in-hello-update-03"></a>Problemi noti di hello aggiornamento 0.3
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

## <a name="next-step"></a>Passaggio successivo
[Installare l'aggiornamento 0.3](storsimple-ova-install-update-01.md) sull'array virtuale StorSimple.

## <a name="references"></a>Riferimenti
Si desidera consultare le note su una versione precedente? Passare a: 

* [Note sulla versione dell'Aggiornamento 0.1 e 0.2 per l'array virtuale StorSimple](storsimple-ova-update-01-release-notes.md)
* [Note sulla versione con disponibilità generale dell'array virtuale StorSimple](storsimple-ova-pp-release-notes.md)

