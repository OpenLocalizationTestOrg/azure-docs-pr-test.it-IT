---
title: note sulla versione aggiornamenti Array virtuale aaaStorSimple | Documenti Microsoft
description: Descrive i problemi critici aperti e le risoluzioni hello StorSimple Virtual Array che eseguono l'aggiornamento 0,2 e 0,1.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Note sulla versione dell'Aggiornamento 0.2 e 0.1 per l'array virtuale StorSimple
## <a name="overview"></a>Panoramica
Hello note sulla versione seguenti identificano i problemi critici aperti di hello e hello problemi risolti per gli aggiornamenti di Microsoft Azure StorSimple Virtual Array. (Microsoft Azure StorSimple Virtual Array è noto anche come dispositivo virtuale locale StorSimple di hello o dispositivo virtuale StorSimple hello.) 

note sulla versione di Hello vengono aggiornati continuamente e come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire il dispositivo virtuale StorSimple, leggere attentamente le informazioni di hello contenute nelle note sulla versione di hello.

Aggiornamento 0,2 corrispondente versione di software toohello **10.0.10280.0**; Aggiornamento 0,1 è versione **10.0.10279.0**. Hello nelle sezioni seguenti vengono elencano le modifiche di hello per ogni aggiornamento. 

> [!NOTE]
> Gli aggiornamenti comportano il riavvio del dispositivo. Se i/o sono in corso, il dispositivo hello genererà tempo di inattività.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problemi risolti in hello aggiornamento 0,2
Aggiornamento 0,2 include tutte le modifiche apportate dall'aggiornamento 0,1 correzione toohello inoltre descritto in hello nella tabella seguente:

| Funzionalità | Problema |
| --- | --- |
| Aggiornamenti |Nella versione precedente di hello, gli aggiornamenti non sono stati rilevati automaticamente nel portale di Azure classico, hello in modo era toouse hello gli aggiornamenti di tooinstall dell'interfaccia utente Web locali. Tale problema è stato corretto in questa versione. Dopo aver installato l'aggiornamento 0,2, è possibile installare gli aggiornamenti futuri utilizzando hello portale di Azure classico. |

## <a name="whats-new-in-hello-update-01"></a>Novità di hello aggiornamento 0,1
Aggiornamento 0,1 contiene seguente hello miglioramenti e correzioni di bug. 

* **Resilienza migliorata per le interruzioni cloud**: questa versione include diverse correzioni di bug per il ripristino di emergenza, backup, ripristino e suddivisione in livelli nell'evento hello di un'interruzione di connettività cloud. 
* **Miglioramento delle prestazioni di ripristino**: questa versione contiene correzioni di bug che sono significativamente ridurre il tempo di completamento hello hello processi di ripristino.
* **Ottimizzazione dello spazio di recupero automatico**: durante l'eliminazione di dati in volumi con thin provisioning hello blocchi di archiviazione inutilizzato necessario toobe recuperato. Questa versione dispone del processo di recupero dello spazio hello migliorate dal cloud hello risultante in hello inutilizzato spazio diventa disponibile più rapidamente rispetto a come toohello le versioni precedenti.
* **Nuove immagini disco virtuale**: VMDK nuovo VHD e VHDX sono ora disponibili tramite hello portale di Azure classico. È possibile scaricare queste immagini tooprovision nuovo aggiornamento 0,1 i dispositivi.
* **Migliorare l'accuratezza di hello dello stato dei processi nel portale di hello**: hello versione precedente del software, stato del processo report nel portale di hello non granulare. Questo problema è stato risolto in questa versione.
* **Esperienza di aggiunta dominio**: correzioni di Bug relativi toodomain aggiunta e la ridenominazione del dispositivo hello.

## <a name="issues-fixed-in-hello-update-01"></a>Problemi risolti in hello aggiornamento 0,1
Hello nella tabella seguente fornisce un riepilogo dei problemi risolti in questa versione.

| No. | Funzionalità | Problema |
| --- | --- | --- |
| 1 |VMDK |In alcune versioni di VMware, è stata considerata disco del sistema operativo hello che causano avvisi di tipo sparse e compromettere il normale funzionamento. Questo bug è stato risolto in questa versione. |
| 2 |Server iSCSI |Nella versione precedente di hello, hello utente è stato richiesto toospecify un gateway per ogni interfaccia di rete del dispositivo virtuale StorSimple. Questo comportamento viene modificato in questa versione, in modo che l'utente hello è tooconfigure almeno un gateway per tutte le interfacce di rete hello abilitato. |
| 3 |Pacchetto di supporto |In hello versione precedente del software, il supporto di raccolta di pacchetti non riuscito quando le dimensioni dei pacchetti hello erano maggiore di 1 GB. Tale problema è stato corretto in questa versione. |
| 4 |Accesso al cloud |Nella versione precedente di hello, se hello Array virtuale StorSimple non dispone di connettività di rete ed è stato riavviato, hello dell'interfaccia utente locale avrebbe problemi di connettività. Questo problema è stato risolto in questa versione. |
| 5 |Grafici di monitoraggio |Nella versione precedente di hello, dopo un failover del dispositivo, grafici di utilizzo della capacità cloud hello visualizzati valori non corretti nel portale di Azure classico hello. Questo problema viene risolto nella versione corrente di hello. |

## <a name="known-issues-in-hello-update-01"></a>Problemi noti di hello aggiornamento 0,1
Hello nella tabella seguente fornisce un riepilogo dei problemi noti per hello Array virtuale StorSimple e include problemi hello indicato versione rispetto alle versioni precedenti hello. **Hello versione problemi indicati in questa versione sono contrassegnati con un asterisco. Quasi tutti i problemi di hello in questo elenco sono trasferito dalla versione di hello GA di Array virtuale StorSimple.**

| No. | Funzionalità | Problema | Soluzione alternativa/commenti |
| --- | --- | --- | --- |
| **1.** |Aggiornamenti |dispositivi di Hello virtuali creati nella versione di anteprima di hello non possono essere aggiornato tooa supportato disponibilità generale versione. |Questi dispositivi virtuali devono essere eseguire il failover per il rilascio di disponibilità generale utilizzando un flusso di lavoro di ripristino di emergenza di emergenza hello. |
| **2.** |Disco dati sottoposto a provisioning |Una volta è stato effettuato il provisioning un disco dati di una determinata dimensione specificato e creato dispositivo virtuale StorSimple corrispondente hello, è necessario non espandere o compattare il disco di dati hello. Il tentativo di toodo pertanto comporta una perdita di tutti i dati di hello nei livelli di locale hello del dispositivo hello. | |
| **3.** |Criteri di gruppo |Quando un dispositivo è aggiunto al dominio, l'applicazione di criteri di gruppo può influenzare negativamente operazione dispositivo hello. |Assicurarsi che l'array virtuale nella propria unità organizzativa (OU) di Active Directory e non oggetti Criteri di gruppo (GPO) vengono applicati tooit. |
| **4.** |Interfaccia utente Web locale |Se sono abilitate le funzionalità di sicurezza avanzate di Internet Explorer, alcune pagine dell'interfaccia utente Web locale come Risoluzione dei problemi o Manutenzione potrebbero non funzionare correttamente. Anche i pulsanti di queste pagine potrebbero non funzionare. |Disattivare le funzionalità di protezione avanzata di Internet Explorer. |
| **5.** |Interfaccia utente Web locale |In una macchina virtuale Hyper-V, hello interfacce di rete nel web hello dell'interfaccia utente vengono visualizzate come interfacce da 10 Gbps. |Questo comportamento è una reflection di Hyper-V. Hyper-V visualizza sempre 10 Gbps per le schede di rete virtuale. |
| **6.** |Volumi o condivisioni a livelli |L'intervallo di byte per le applicazioni che funzionano con hello StorSimple volumi a livelli di blocco non è supportata. Se il blocco dell'intervallo di byte è abilitato, la suddivisione in livelli di StorSimple non funziona. |Tra le misure consigliate:  <br></br>Disattivare il blocco dell'intervallo di byte nella logica dell'applicazione.<br></br>Scegliere tooput dati per questa applicazione in volumi aggiunti in locale anziché come tootiered volumi.<br></br>*Avvertenza*: se utilizzando locale aggiunto volumi e il blocco di intervallo di byte è abilitato, tenere presente che il volume aggiunto in locale hello può essere online anche prima hello ripristino è stato completato. In questi casi, se un ripristino in corso, quindi è necessario attendere toocomplete ripristino hello. |
| **7.** |Condivisioni a livelli |Lavorare con file di grandi dimensioni può comportare una suddivisione in livelli lenta. |Quando si utilizzano file di grandi dimensioni, è consigliabile che file più grande di hello è minore di 3% delle dimensioni della condivisione hello. |
| **8.** |Capacità usata per le condivisioni |Può vedere condividere consumo in assenza di hello di tutti i dati nella condivisione di hello. Questo avviene perché la capacità di hello utilizzato per le condivisioni include i metadati. | |
| **9.** |Ripristino di emergenza |È possibile eseguire solo il ripristino di emergenza hello di toohello di server un file nello stesso dominio del dispositivo di origine hello. Dispositivo di destinazione tooa di ripristino di emergenza in un altro dominio non è supportata in questa versione. |Questo aspetto sarà implementato in una versione successiva. |
| **10.** |Azure PowerShell |i dispositivi virtuali StorSimple di Hello non possono essere gestiti tramite hello Azure PowerShell in questa versione. |Gestione di hello tutti i dispositivi virtuali hello debba essere eseguita tramite hello portale di Azure classico e interfaccia utente web locale hello. |
| **11.** |Modifica della password |console del dispositivo virtuale matrice Hello accetta solo input in formato en-US della tastiera. | |
| **12.** |CHAP |Le credenziali di autenticazione CHAP create non possono essere rimosse. Inoltre, se si modificano le credenziali dell'autenticazione CHAP hello, sarà anche necessario offline i volumi di hello tootake e quindi attivare la modalità online per effetto di tootake modifica hello. |Questi problemi verranno risolti in una versione successiva. |
| **13.** |Server iSCSI |Hello 'Archiviazione utilizzato' visualizzato per un volume iSCSI potrebbe essere diverso nel servizio StorSimple Manager hello e host iSCSI hello. |host iSCSI Hello è visualizzazione filesystem hello.<br></br>dispositivo Hello vede blocchi hello allocati quando il volume di hello quando la dimensione massima di hello. |
| **14.** |File server* |Se un file in una cartella è un flusso a dati alternativo (ADS) associati, annunci hello non backup o ripristino tramite il ripristino di emergenza, clonazione e ripristino a livello di elemento. | |

## <a name="next-step"></a>Passaggio successivo
[Installare aggiornamenti](storsimple-ova-install-update-01.md) nell'array virtuale StorSimple

