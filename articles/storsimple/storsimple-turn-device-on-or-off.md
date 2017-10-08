---
title: aaaTurn il dispositivo StorSimple serie 8000 o disattivare | Documenti Microsoft
description: "Viene illustrato come attivare un dispositivo che è stato arrestato o un'interruzione dell'alimentazione, tooturn in un nuovo dispositivo di StorSimple e disattivare un dispositivo in esecuzione."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 8e9c6e6c-965c-4a81-81bd-e1c523a14c82
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 85434bde9377e330cd6ba4797fd5fd68bcee944d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="turn-on-or-turn-off-your-storsimple-8000-series-device"></a>Attivare o disattivare il dispositivo StorSimple serie 8000
## <a name="overview"></a>Panoramica
L’arresto di un dispositivo Microsoft Azure StorSimple non è necessario nel normale funzionamento del sistema. Tuttavia, potrebbe essere necessario tooturn in un nuovo dispositivo o un dispositivo che è stato arrestato toobe. In genere, un arresto è necessario nei casi in cui bisogna sostituire l'hardware non riuscito, spostare fisicamente un'unità o mettere fuori servizio un dispositivo. In questa esercitazione descrive hello necessario per l'attivazione e l'arresto del dispositivo StorSimple in diversi scenari.

## <a name="turn-on-a-new-device"></a>Attivare un nuovo dispositivo
Hello passaggi per l'attivazione in un dispositivo StorSimple per hello prima volta variano a seconda se il dispositivo hello è un 8100 o un modello 8600. Hello 8100 ha una sola enclosure principale, mentre hello 8600 è un dispositivo di due enclosure con una enclosure principale e una EBOD. Hello passaggi dettagliati per entrambi i modelli vengono trattati in hello le sezioni seguenti.

* [Nuovo dispositivo con soltanto un’enclosure principale](#new-device-with-primary-enclosure-only)
* [Nuovo dispositivo con enclosure EBOD](#new-device-with-ebod-enclosure)

### <a name="new-device-with-primary-enclosure-only"></a>Nuovo dispositivo con soltanto un’enclosure principale
modello di Hello StorSimple 8100 è un dispositivo a enclosure singola. Il dispositivo include moduli PCM (Power and Cooling Modules) Entrambi i PCM devono essere installati e connesso toodifferent power origini tooensure la disponibilità elevata.

Eseguire hello seguendo i passaggi toocable il dispositivo per l'alimentazione.

[!INCLUDE [storsimple-cable-8100-for-power](../../includes/storsimple-cable-8100-for-power.md)]

> [!NOTE]
> Per l'installazione completa del dispositivo e i cavi di istruzioni, visitare troppo[installare il dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md). Assicurarsi di seguire le istruzioni di hello esattamente.
> 
> 

### <a name="new-device-with-ebod-enclosure"></a>Nuovo dispositivo con enclosure EBOD
modello Hello 8600 StorSimple include una enclosure principale e un'enclosure EBOD. Questa operazione richiede hello unità toobe cablate insieme per la connettività SAS Serial Attached SCSI () e l'alimentazione.

Quando si imposta questo dispositivo per hello prima volta, eseguire hello del cablaggio SAS innanzitutto e passaggi hello quindi completo per il collegamento all'alimentazione.

[!INCLUDE [storsimple-sas-cable-8600](../../includes/storsimple-sas-cable-8600.md)]

[!INCLUDE [storsimple-cable-8600-for-power](../../includes/storsimple-cable-8600-for-power.md)]

> [!NOTE]
> Per l'installazione completa del dispositivo e i cavi di istruzioni, visitare troppo[installare del dispositivo 8600 StorSimple](storsimple-8600-hardware-installation.md). Assicurarsi di seguire le istruzioni di hello esattamente.

## <a name="turn-on-a-device-after-shutdown"></a>Attivare un dispositivo dopo l'arresto
Hello passaggi per l'attivazione di un dispositivo StorSimple dopo che è stato arrestato sono diversi a seconda se il dispositivo hello è un 8100 o un modello 8600. Hello 8100 ha una sola enclosure principale, mentre hello 8600 è un dispositivo di due enclosure con una enclosure principale e una EBOD.

* [Dispositivo con soltanto un’enclosure principale](#device-with-primary-enclosure-only)
* [Dispositivo con enclosure EBOD](#device-with-ebod-enclosure)

### <a name="device-with-primary-enclosure-only"></a>Dispositivo con soltanto un’enclosure principale
Dopo un arresto, utilizzare hello seguendo procedure tooturn in un dispositivo StorSimple con una enclosure principale e nessuna enclosure EBOD.

#### <a name="tooturn-on-a-device-with-a-primary-enclosure-only"></a>tooturn in un dispositivo con solo una enclosure principale
1. Assicurarsi che sia Power interruttori di alimentazione di hello e moduli raffreddamento (PCM) siano in posizione OFF hello. Se hello opzioni non sono in posizione OFF hello, quindi invertite in posizione OFF toohello e attendere hello luci toogo off.
2. Accendere il dispositivo hello girando hello interruttori di alimentazione su entrambi i PCM in posizione on toohello. dispositivo Hello dovrebbe accendersi.
3. Controllo hello seguente tooverify che hello dispositivo sia acceso completamente:
   
   1. Hello LED OK di entrambi i moduli PCM sono di colore verde.
   2. LED di stato Hello in entrambi i controller sono di colore verde.
   3. Hello LED blu su uno dei controller hello è lampeggiante, che indica che tale controller hello è attiva.
      
      Se una di queste condizioni non vengono soddisfatte, il dispositivo non è integro. [Contattare il supporto Microsoft](storsimple-8000-contact-microsoft-support.md).

### <a name="device-with-ebod-enclosure"></a>Dispositivo con enclosure EBOD
Dopo un arresto, utilizzare hello seguendo procedure tooturn in un dispositivo StorSimple con una enclosure principale e una EBOD. Eseguire ogni passaggio esattamente come descritto nella sequenza. Errore toodo così potrebbe causare la perdita di dati.

#### <a name="tooturn-on-a-device-with-a-primary-and-an-ebod-enclosure"></a>tooturn in un dispositivo con un database primario e un'enclosure EBOD
1. Verificare che tale enclosure EBOD hello è enclosure principale toohello connesso. Per ulteriori informazioni, vedere [Installare il dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md).
2. Verificare che tale hello Power Cooling Module (PCM) sia hello EBOD ed enclosure principale sono in posizione OFF hello. Se hello opzioni non sono in posizione OFF hello, quindi invertite in posizione OFF toohello e attendere hello luci toogo off.
3. Attivare in hello enclosure EBOD girando hello interruttori di alimentazione su entrambi i PCM in posizione on toohello. LED PCM Hello deve essere di colore verde. Un controller di EBOD LED verde in questa unità indica che in enclosure EBOD hello.
4. Accendere l'enclosure principale hello girando hello interruttori di alimentazione su entrambi i PCM in posizione on toohello. intero sistema Hello dovrebbe ora essere in.
5. Verificare che hello LED SAS siano di colore verde, che assicura la connessione di hello tra hello enclosure EBOD e l'enclosure principale hello è valido.

## <a name="turn-on-a-device-after-a-power-loss"></a>Attivare un dispositivo dopo un'interruzione dell'alimentazione
Un guasto o un'interruzione dell'alimentazione può causare l'arresto di un dispositivo StorSimple. interruzione dell'alimentazione Hello possono essere eseguiti su uno degli alimentatori hello o entrambi gli alimentatori. passaggi di ripristino Hello sono diversi a seconda se il dispositivo hello è un 8100 o un modello 8600. Hello 8100 ha una sola enclosure principale, mentre hello 8600 è un dispositivo di due enclosure con una enclosure principale e una EBOD. Questa sezione descrive la procedura di ripristino hello per ogni scenario.

* [Dispositivo con soltanto un’enclosure principale](#8100)
* [Dispositivo con enclosure EBOD](#8600)

### <a name="device-with-primary-enclosure-only-a-name8100"></a>Dispositivo con soltanto un’enclosure principale <a name="8100">
sistema Hello possibile se continuare a funzionare normalmente power perdita tooone degli alimentatori. Tuttavia, la disponibilità elevata del dispositivo hello, ripristino power toohello tooensure alimentatore appena possibile.

Se è presente un'interruzione dell'alimentazione o l'interruzione dell'alimentazione su entrambi gli alimentatori, il sistema hello verrà arrestato in modo ordinato e controllato. Quando power hello viene ripristinato, il sistema hello verrà attivata automaticamente.

### <a name="device-with-ebod-enclosure-a-name8600"></a>Dispositivo con enclosure EBOD <a name="8600">
#### <a name="power-loss-on-one-power-supply"></a>Interruzione dell'alimentazione su un solo alimentatore
Se power perdita tooone degli alimentatori enclosure principale hello o enclosure EBOD hello sistema Hello possibile continuare il normale funzionamento. Tuttavia, tooensure un'elevata disponibilità dispositivo hello, ripristinare alimentatore toohello power appena possibile.

#### <a name="power-loss-on-both-power-supplies-on-primary-and-ebod-enclosures"></a>Perdita di energia su entrambi gli alimentatori dell’enclosure principale e dell’enclosure EBOD
Se è presente un'interruzione di alimentazione o di un'interruzione dell'alimentazione per entrambi gli alimentatori, hello enclosure EBOD verrà arrestata immediatamente e l'enclosure principale hello verrà arrestato in modo ordinato e controllato. Quando viene ripristinata l'alimentazione, accessorio hello verrà avviato automaticamente.

Se power hello è disattivato manualmente, quindi intraprendere hello sistema toohello power toorestore di passaggi seguenti.

1. Accendere l'enclosure EBOD hello.
2. Dopo hello enclosure EBOD, accendere l'enclosure principale hello.

### <a name="power-loss-on-both-power-supplies-on-ebod-enclosure"></a>Perdita di energia su entrambi gli alimentatori dell’enclosure EBOD
Quando configurano i cavi, è necessario assicurarsi che hello EBOD non è mai connessi solo tooa separare PDU. Se hello EBOD e principale non riuscire in hello contemporaneamente, sistema di hello verrà ripristinato.

Se solo hello enclosure EBOD non riesce per entrambi gli alimentatori, il sistema di hello non verrà ripristinato automaticamente. Accettano hello seguendo i passaggi tooturn sistema hello e ripristinarlo tooa integro:

1. Se è attivata l'enclosure principale hello, spegnere entrambi Power and Cooling Module (PCM).
2. Attendere alcuni minuti per hello sistema tooshut verso il basso.
3. Accendere l'enclosure EBOD hello.
4. Dopo hello enclosure EBOD, accendere l'enclosure principale hello.

## <a name="turn-on-a-device-after-hello-primary-and-ebod-enclosure-connection-is-lost"></a>Attivare un dispositivo dopo hello primario e il collegamento di enclosure EBOD viene interrotto
Se hello connessione si interrompe tra i controller in standby hello e controller EBOD corrispondente hello, dispositivo hello continua toowork. Se la connessione hello tra controller di sistema attivo hello e il corrispondente controller EBOD di hello viene persa, failover dovrebbe verificarsi e dispositivo hello deve continuare toowork come di consueto.

Quando vengono rimossi entrambi i cavi SAS Serial Attached SCSI () o connessione hello tra hello enclosure EBOD ed enclosure principale hello viene interrotto, il dispositivo hello smetterà di funzionare. A questo punto, eseguire hello alla procedura seguente.

### <a name="tooturn-on-hello-device-after-connection-is-lost"></a>tooturn sul dispositivo hello dopo la connessione viene persa
1. Hello accesso parte posteriore dispositivo hello.
2. Se hello cavo SAS tra hello EBOD hello enclosure principale ed è interrotto, tutti i terminali del cavo SAS LED sul hello enclosure EBOD saranno spenti.
3. Arrestare entrambi Power and Cooling Module (PCM) sulle enclosure EBOD di hello e hello primario.
4. Attendere che tutte le luci hello in hello parte posteriore di entrambe le enclosure hello disattivare.
5. Reinserire i cavi SAS hello e verificare che sia presente un collegamento tra hello EBOD hello enclosure principale ed.
6. Attivare hello enclosure EBOD prima girando entrambi PCM commutatori toohello in posizione.
7. Verificare che l'enclosure EBOD hello sia su controllando che il LED verde hello è impostata su ON.
8. Accendere l'enclosure principale hello.
9. Verificare che l'enclosure principale hello sia su verificando che i LED verde del controller hello sia in.
10. Verificare che hello connessione enclosure EBOD con enclosure principale hello buona controllando che hello SAS LED terminali del cavo (quattro per controller EBOD) si trovano tutti in.

> [!IMPORTANT]
> Se i cavi SAS hello sono difettosi o connessione hello tra hello enclosure EBOD ed enclosure principale hello è non valida, quando si attiva il sistema di hello, passerà alla modalità di ripristino. Se ciò accade, [contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md) .


## <a name="turn-off-a-running-device"></a>Spegnere un dispositivo in esecuzione
Un dispositivo StorSimple in esecuzione potrebbe essere necessario toobe arrestato se è stato spostato, messo fuori servizio, o è un componente non funzionante toobe sostituito. Hello passaggi sono diversi a seconda se il dispositivo StorSimple hello sia un 8100 o un modello 8600. Hello 8100 ha una sola enclosure principale, mentre hello 8600 è un dispositivo di due enclosure con una enclosure principale e una EBOD. In questa sezione illustra in dettaglio hello passaggi tooshut verso il basso un dispositivo in esecuzione.

* [Dispositivo con enclosure principale](#8100a)
* [Dispositivo con enclosure EBOD](#8600a)

### <a name="device-with-primary-enclosure-a-name8100a"></a>Dispositivo con enclosure principale <a name="8100a">
tooshut verso il basso il dispositivo hello in modo ordinato e controllato, è possibile farlo tramite hello portale di Azure classico o hello Windows PowerShell per StorSimple. 

> [!IMPORTANT]
> Non arrestare un dispositivo in esecuzione con il pulsante di alimentazione hello in hello parte posteriore dispositivo hello.
> 
> Prima di arrestare il dispositivo di hello, assicurarsi che tutti i componenti del dispositivo hello siano integri. Nel portale di Azure classico hello, passare troppo**dispositivi** > **manutenzione** > **stato Hardware**e verificare lo stato di tutti i hello i componenti sia di colore verde. Questo vale solo per un sistema integro. Se il sistema hello è l'arresto tooreplace un componente non funzionante, verrà visualizzato un errore (rosso) o danneggiato (giallo) dello stato per componente hello in hello **stato Hardware**.
> 
> 

Dopo l'accesso hello Windows PowerShell per StorSimple o hello portale di Azure classico, seguire i passaggi hello [arrestare un dispositivo StorSimple](storsimple-manage-device-controller.md#shut-down-a-storsimple-device). 

### <a name="device-with-ebod-enclosure-a-name8600a"></a>Dispositivo con enclosure EBOD <a name="8600a">
> [!IMPORTANT]
> Prima di arrestare hello primario e hello EBOD, assicurarsi che tutti i componenti del dispositivo hello siano integri. Nel portale di Azure hello, passare troppo**dispositivi** > **monitoraggio** > **lo stato di Hardware**e verificare che tutti i componenti di hello siano integri.


#### <a name="tooshut-down-a-running-device-with-ebod-enclosure"></a>tooshut verso il basso un dispositivo con enclosure EBOD in esecuzione
1. Eseguire tutti i passaggi di hello elencati in [arrestare un dispositivo StorSimple](storsimple-8000-manage-device-controller.md#shut-down-a-storsimple-device) per enclosure principale hello.
2. Dopo aver hello enclosure principale è stato arrestato, arrestare hello EBOD girando disattivare Opzioni risparmio energia sia modulo di raffreddamento (PCM).
3. arresto tooverify che hello EBOD, verificare che tutti diventa su hello parte posteriore dell'enclosure EBOD hello sono disattivate.

> [!NOTE]
> i cavi SAS Hello che vengono utilizzati tooconnect hello EBOD toohello enclosure principale enclosure non devono essere rimosso fino a dopo l'arresto del sistema hello.

## <a name="next-steps"></a>Passaggi successivi
[Contattare il supporto tecnico Microsoft](storsimple-8000-contact-microsoft-support.md) se si riscontrano problemi durante l'attivazione o l'arresto di un dispositivo StorSimple.

