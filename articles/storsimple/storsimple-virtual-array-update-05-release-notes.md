---
title: aaaStorSimple virtuale matrice 0,5 note sulla versione Update | Documenti Microsoft
description: Viene aperta critico problemi e risoluzioni per l'esecuzione di StorSimple Virtual Array hello aggiornino 0,5.
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
ms.date: 05/08/2017
ms.author: alkohli
ms.openlocfilehash: a249e2e8f0105dcf6cc02d3136dfa3e37ea615d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-05-release-notes"></a>Note sulla versione dell'aggiornamento 0.5 per l'array virtuale StorSimple

## <a name="overview"></a>Panoramica

Hello note sulla versione seguenti identificano i problemi critici aperti di hello e hello problemi risolti per gli aggiornamenti di Microsoft Azure StorSimple Virtual Array.

note sulla versione di Hello vengono aggiornati continuamente e come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire l'Array virtuale StorSimple, leggere attentamente le informazioni di hello contenute nelle note sulla versione di hello.

Aggiornamento 0,5 corrisponde versione software toohello **10.0.10290.0**.

> [!NOTE]
> Gli aggiornamenti comportano il riavvio del dispositivo. Se i/o sono in corso, il dispositivo hello comporta tempi di inattività. Per istruzioni dettagliate su come tooapply hello aggiornamento, visitare troppo[installare l'aggiornamento 0,5](storsimple-virtual-array-install-update-05.md).


## <a name="whats-new-in-hello-update-05"></a>Novità di hello aggiornamento 0,5
L'aggiornamento 0.5 è principalmente una build per la correzione di bug. come indicato di seguito sono riportati i miglioramenti principali Hello e correzioni di bug:

- **Miglioramenti della resilienza backup** -questa versione contiene correzioni che consentono di migliorare la flessibilità di backup hello. In hello ritentate versioni precedenti, i backup solo per determinate eccezioni. Questa versione Ritenta tutte le eccezioni di backup hello e rende hello backup più flessibile.

- **Gli aggiornamenti per il monitoraggio dell'utilizzo di archiviazione** -a partire da 30 giugno 2017, hello archiviazione monitoraggio dell'utilizzo per serie di dispositivi virtuali StorSimple verrà ritirata. Si applica toohello grafici su tutte le matrici virtuale hello esecuzione Update 0,4 o inferiore di monitoraggio. Questo aggiornamento contiene modifiche hello obbligatoria per si toocontinue hello dell'uso dell'archiviazione di monitoraggio in hello portale di Azure. Installare questo aggiornamento critico prima del 30 giugno 2017 toocontinue utilizzando hello funzionalità di monitoraggio.


## <a name="issues-fixed-in-hello-update-05"></a>Problemi risolti in hello aggiornamento 0,5

Hello nella tabella seguente fornisce un riepilogo dei problemi risolti in questa versione.

| No. | Funzionalità | Problema |
| --- | --- | --- |
| 1 |Resilienza dei backup| In hello ritentate versioni precedenti, i backup solo per determinate eccezioni. Questa versione include un backup di correzione toomake più flessibile con un nuovo tentativo di tutte le eccezioni di backup hello.|
| 2 |Monitoraggio| Hello archiviazione monitoraggio dell'utilizzo per la serie di dispositivi virtuali StorSimple verrà deprecato a partire dal 30 giugno 2017. Questa azione influisce su hello monitoraggio grafici nel servizio di gestione di dispositivi StorSimple hello in esecuzione su StorSimple Virtual Array (modello a 1200). Questa versione è disponibili aggiornamenti che consentono l'uso di hello utente toocontinue hello di monitoraggio utilizzo dell'archiviazione per le matrici virtuale hello oltre 30 giugno 2017.|
| 3 |File server| In hello versioni precedenti, un utente è stato possibile copiare erroneamente array virtuale toohello di file crittografati. Questa versione include una correzione che non consente la copia della matrice toovirtual file crittografati. Se il dispositivo è esistente toohello precedente di file crittografati di aggiornamento, i backup continuerà toofail fino a quando non vengono eliminati tutti i file crittografato hello dal sistema hello. |


## <a name="known-issues-in-hello-update-05"></a>Problemi noti di hello aggiornamento 0,5

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
| **8.** |Capacità usata per le condivisioni |Può vedere condividere consumo quando non sono presenti dati nella condivisione di hello. Questo utilizzo è perché la capacità di hello utilizzato per le condivisioni include i metadati. | |
| **9.** |Ripristino di emergenza |È possibile eseguire solo il ripristino di emergenza hello di toohello di server un file nello stesso dominio del dispositivo di origine hello. Dispositivo di destinazione tooa di ripristino di emergenza in un altro dominio non è supportata in questa versione. |L'implementazione è prevista per una versione futura. Per ulteriori informazioni, visitare troppo[Failover e ripristino di emergenza per l'Array virtuale StorSimple](storsimple-virtual-array-failover-dr.md) |
| **10.** |Azure PowerShell |i dispositivi virtuali StorSimple di Hello non possono essere gestiti tramite hello Azure PowerShell in questa versione. |Tutti i management hello di dispositivi virtuali hello devono essere eseguiti tramite hello Azure portal e hello interfaccia utente web locale. |
| **11.** |Modifica della password |Hello console del dispositivo virtuale matrice accetta solo input en-us formato della tastiera. | |
| **12.** |CHAP |Le credenziali di autenticazione CHAP create non possono essere rimosse. Inoltre, se si modificano le credenziali dell'autenticazione CHAP hello, necessario offline i volumi di hello tootake e quindi portarli online per effetto di tootake modifica hello. |La risoluzione del problema è prevista per una versione futura. |
| **13.** |Server iSCSI |Hello 'Archiviazione utilizzato' visualizzato per un volume iSCSI potrebbe essere diverso nel servizio di gestione di dispositivi StorSimple hello e host iSCSI hello. |host iSCSI Hello è visualizzazione filesystem hello.<br></br>dispositivo Hello vede blocchi hello allocati quando il volume di hello quando la dimensione massima di hello. |
| **14.** |File server |Se un file in una cartella è un flusso a dati alternativo (ADS) associati, annunci hello non backup o ripristino tramite il ripristino di emergenza, clonazione e ripristino a livello di elemento. | |
| **15.** |File server |I collegamenti simbolici non sono supportati. | |
| **16.** |File server |I file protetti da Windows Encrypting File System (EFS) quando copiate o archiviate in hello Array virtuale StorSimple file server di risultati in una configurazione non supportata.  | |

## <a name="next-step"></a>Passaggio successivo
[Installare l'aggiornamento 0.5](storsimple-virtual-array-install-update-05.md) nell'array virtuale StorSimple.

## <a name="references"></a>Riferimenti
Si desidera consultare le note su una versione precedente? Passare a:

* [Note sulla versione dell'aggiornamento 0.4 per l'array virtuale StorSimple](storsimple-virtual-array-update-04-release-notes.md)
* [Note sulla versione dell'aggiornamento 0.3 per l'array virtuale StorSimple](storsimple-ova-update-03-release-notes.md)
* [Note sulla versione dell'Aggiornamento 0.1 e 0.2 per l'array virtuale StorSimple](storsimple-ova-update-01-release-notes.md)
* [Note sulla versione con disponibilità generale dell'array virtuale StorSimple](storsimple-ova-pp-release-notes.md)

