---
title: note sulla versione di Array virtuale aaaStorSimple | Documenti Microsoft
description: Descrive i problemi critici aperti e le risoluzioni hello Array virtuale StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Note sulla versione dell'array virtuale StorSimple
## <a name="overview"></a>Panoramica
note sulla versione seguenti Hello identificare hello problemi critici aperti per il rilascio di disponibilità generale (GA) di marzo 2016 hello di hello Microsoft Azure StorSimple Virtual Array (noto anche come dispositivo virtuale locale StorSimple hello o hello virtuale StorSimple dispositivo). Questa versione corrisponde toosoftware versione 10.0.10271.0.

note sulla versione di Hello vengono aggiornati continuamente e come vengono individuati problemi critici che richiedono una soluzione alternativa, vengono aggiunti. Prima di distribuire il dispositivo virtuale StorSimple, leggere attentamente le informazioni di hello contenute nelle note sulla versione di hello. 

Hello nella tabella seguente fornisce un riepilogo dei problemi noti in questa versione.

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

