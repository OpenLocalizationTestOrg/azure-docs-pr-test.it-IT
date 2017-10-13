---
title: Indicatori di monitoraggio di StorSimple | Microsoft Docs
description: Descrive i diodi a emissione luminosa (LED) e gli avvisi sonori utilizzati per monitorare lo stato del dispositivo StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 59dee7b9-ca6d-4fd9-96e6-a0071e8d248e
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 0d44f94719bff0cb58b3727050598e55f4774e66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-monitoring-indicators-to-manage-your-device"></a>Utilizzare gli indicatori di monitoraggio StorSimple per gestire il dispositivo
## <a name="overview"></a>Panoramica
Il dispositivo StorSimple include diodi a emissione luminosa (LED) e allarmi che possono essere utilizzati per monitorare i moduli e lo stato generale del dispositivo StorSimple. Gli indicatori di monitoraggio possono trovarsi in componenti hardware dello chassis principale e dello chassis EBOD del dispositivo. Gli indicatori di monitoraggio possono essere LED o allarmi acustici.

Vengono utilizzate tre condizioni dei LED per indicare lo stato di un modulo: verde, intermittente da verde a rosso-ambra o rosso-ambra.  

* I LED verdi indicano uno stato operativo integro.  
* I LED intermittenti da verde a rosso-ambra indicano la presenza di condizioni non critiche che potrebbero richiedere l'intervento dell'utente.  
* I LED rosso-ambra indicano la presenza di un errore critico all'interno del modulo.  

Nel promemoria del presente articolo vengono descritti i vari indicatori LED di monitoraggio, le posizioni sul dispositivo StorSimple, lo stato del dispositivo in base alle condizioni dei LED ed eventuali allarmi acustici associati.

## <a name="front-panel-indicator-leds"></a>Indicatori LED sul pannello anteriore
Il pannello anteriore, noto anche come *pannello operativo* o *pannello delle operazioni*, visualizza lo stato aggregato di tutti i moduli del sistema. Il pannello anteriore è identico sia nell'alloggiamento principale sia in quello EBOD del dispositivo StorSimple e viene illustrato di seguito.  

   ![Pannello anteriore del dispositivo][1]

Il pannello anteriore include i seguenti indicatori:  

1. Pulsante di disattivazione audio
2. Indicatore LED (verde/rosso-ambra) di alimentazione
3. Indicatore LED di errore nel modulo (ACCESO rosso-ambra/SPENTO)
4. Indicatore LED di errore logico (ACCESO rosso-ambra/SPENTO)
5. Display ID unità  

La differenza principale tra i LED del pannello anteriore del dispositivo e quelli dello chassis EBOD è il **Numero identificativo dell'unità di sistema** visualizzato sul display a LED. L'ID unità predefinito visualizzato sul dispositivo è **00**, mentre l'ID unità predefinito visualizzato sullo chassis EBOD è **01**. In questo modo è possibile distinguere rapidamente tra il dispositivo e lo chassis EBOD quando il dispositivo è acceso. Se il dispositivo è disattivato, utilizzare le informazioni fornite in [Accensione di un nuovo dispositivo](storsimple-turn-device-on-or-off.md#turn-on-a-new-device) per differenziarlo dallo chassis EBOD.  

## <a name="front-panel-led-status"></a>Stato dei LED sul pannello anteriore
Utilizzare la seguente tabella per identificare lo stato indicato dai LED sul pannello anteriore per il dispositivo o lo chassis EBOD.  

| Alimentazione del sistema | Errore del modulo | Errore logico | Allarme | Stato |
| --- | --- | --- | --- | --- |
| Rosso-ambra |DISATTIVA |DISATTIVA |N/D |Alimentazione CA persa, funzionamento con alimentazione di backup oppure alimentazione CA ATTIVA con i moduli di controllo rimossi. |
| Verde |ATTIVA |ATTIVA |N/D |Stato del test di alimentazione del pannello delle operazioni acceso (5 sec) |
| Verde |DISATTIVA |DISATTIVA |N/D |Acceso, funzionamento corretto |
| Verde |ATTIVA |N/D |LED di errore PCM, LED di malfunzionamento ventola |Qualsiasi errore PCM, errore delle ventola oppure sotto o sovratemperatura |
| Verde |ATTIVA |N/D |LED modulo I/O |Qualsiasi errore del modulo controller |
| Verde |ATTIVA |N/D |N/D |Errore logico chassis |
| Verde |Lampeggiante |N/D |LED di stato del modulo sul modulo controller. LED di errore PCM, LED di malfunzionamento ventola |Tipo di modulo controller installato sconosciuto, errore del bus I2C, errore di configurazione del controller del modulo VPD (vital product data) |

## <a name="power-cooling-module-pcm-indicator-leds"></a>Indicatori LED del modulo di alimentazione e raffreddamento (PCM)
Gli indicatori LED del modulo di alimentazione e raffreddamento (PCM) sono disponibili nella parte posteriore dello chassis principale o nello chassis EBOD di ogni modulo PCM. In questo argomento viene descritto come utilizzare i seguenti LED per monitorare lo stato del dispositivo StorSimple.  

* LED PCM per lo chassis principale
* LED PCM per lo chassis EBOD

## <a name="pcm-leds-for-the-primary-enclosure"></a>LED PCM per lo chassis principale
Il dispositivo StorSimple dispone di un modulo PCM da 764 W con una batteria aggiuntiva. Nella figura seguente è illustrato il pannello LED per il dispositivo.  

   ![LED PCM per lo chassis principale][2]

Legenda dei LED:

1. Guasto dell’alimentazione CA
2. Guasto alla ventola
3. Guasto alla batteria
4. PCM OK
5. Guasto CC
6. Batteria integra  

Lo stato del PCM è indicato sul pannello dei LED. Il pannello dei LED PCM del dispositivo dispone di sei LED. Quattro di tali LED visualizzano lo stato dell’alimentatore e della ventola. Idue LED restanti indicano lo stato del modulo della batteria di backup nel PCM. È possibile utilizzare le tabelle riportate di seguito per determinare lo stato del PCM.  

### <a name="pcm-indicator-leds-for-power-supply-and-fan"></a>Indicatori LED del PCM per l'alimentatore e la ventola
| Stato | PCM OK (verde) | Guasto CA (ambra) | Guasto ventola (ambra) | Guasto CC (ambra) |
| --- | --- | --- | --- | --- |
| Alimentazione CA assente (allo chassis) |DISATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Alimentazione CA assente (solo questo PCM) |DISATTIVA |ATTIVA |DISATTIVA |ATTIVA |
| CA presente PCM ATTIVO - OK |ATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Guasto PCM (guasto ventola) |DISATTIVA |DISATTIVA |ATTIVA |N/D |
| Errore PCM (sovramperaggio, sovratensione, sovracorrente) |DISATTIVA |ATTIVA |ATTIVA |ATTIVA |
| PCM (ventola fuori tolleranza) |ATTIVA |DISATTIVA |DISATTIVA |ATTIVA |
| Modalità standby |Intermittente |DISATTIVA |DISATTIVA |DISATTIVA |
| Download firmware PCM |DISATTIVA |Intermittente |Intermittente |Intermittente |

### <a name="pcm-indicator-leds-for-the-backup-battery"></a>Indicatori LED del PCM per la batteria di backup
| Stato | Batteria integra (verde) | Errore batteria (ambra) |
| --- | --- | --- |
| Batteria assente |DISATTIVA |DISATTIVA |
| Batteria presente e carica |ATTIVA |DISATTIVA |
| Batteria in carica o scarica per manutenzione |Intermittente |DISATTIVA |
| Errore batteria "software" (recuperabile) |DISATTIVA |Intermittente |
| Errore batteria "hardware" (non recuperabile) |DISATTIVA |ATTIVA |
| Batteria disattivata |Intermittente |DISATTIVA |

## <a name="pcm-leds-for-the-ebod-enclosure"></a>LED PCM per lo chassis EBOD
Lo chassis EBOD dispone di un PCM da 580 W senza batteria aggiuntiva. Il pannello PCM per lo chassis EBOD dispone di indicatori LED esclusivi per gli alimentatori e la ventola. Nella figura seguente vengono illustrati tali LED.

   ![LED PCM per lo chassis EBOD][3] 

È possibile utilizzare la tabella riportata di seguito per determinare lo stato del PCM.  

| Stato | PCM OK (verde) | Guasto CA (ambra) | Guasto ventola (ambra) | Guasto CC (ambra) |
| --- | --- | --- | --- | --- |
| Alimentazione CA assente (allo chassis) |DISATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Alimentazione CA assente (solo questo PCM) |DISATTIVA |ATTIVA |DISATTIVA |ATTIVA |
| CA presente PCM ATTIVO - OK |ATTIVA |DISATTIVA |DISATTIVA |DISATTIVA |
| Guasto PCM (guasto ventola) |DISATTIVA |DISATTIVA |ATTIVA |X |
| Errore PCM (sovramperaggio, sovratensione, sovracorrente) |DISATTIVA |ATTIVA |ATTIVA |ATTIVA |
| PCM (ventola fuori tolleranza) |ATTIVA |DISATTIVA |DISATTIVA |ATTIVA |
| Modello standby |Intermittente |DISATTIVA |DISATTIVA |DISATTIVA |
| Download firmware PCM |DISATTIVA |Intermittente |Intermittente |Intermittente |

## <a name="controller-module-indicator-leds"></a>Indicatori LED del modulo controller
Il dispositivo StorSimple contiene LED per il controller primario e i moduli del controller EBOD.   

### <a name="monitoring-leds-for-the-primary-controller"></a>LED di monitoraggio per il controller primario
La figura seguente facilita l’identificazione dei LED sul controller primario. Per facilitare l’orientamento, vengono elencati tutti i componenti.  

   ![LED di monitoraggio - controller primario][4]

Utilizzare la tabella seguente per determinare se il modulo controller funziona correttamente.  

### <a name="controller-indicator-leds"></a>Indicatori LED del controller
| LED | Descrizione |
| --- | --- |
| LED ID (blu) |Indica che è in corso l’identificazione del modulo. Se su un controller in esecuzione, il LED blu lampeggia, significa che tale controller è attivo mentre l'altro è in standby. Per ulteriori informazioni, vedere [Identificare un controller attivo sul dispositivo](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| LED errore (ambra) |Indica un errore nel controller. |
| LED OK (verde) |Una luce verde continua indica che il controller è OK. Una luce verde intermittente indica un errore di configurazione del controller VPD. |
| LED attività SAS (verde) |Una luce verde continua indica una connessione senza attività corrente. Una luce verde intermittente indica un’attività in corso nella connessione. |
| LED stato Ethernet |Il lato destro indica un’attività di collegamento/rete: collegamento attivo (verde continuo), attività di rete (verde intermittente). Il lato sinistro indica la velocità di rete: 1000 Mb/s (giallo), 100 Mb/s (verde) e 10 Mb/s (SPENTA). In base al modello del componente, tale indicazione luminosa potrebbe lampeggiare anche se l'interfaccia di rete non è abilitata. |
| LED POST |Indica lo stato dell’avvio quando il controller è attivato. Se l’avvio del dispositivo StorSimple ha esito negativo, tale LED consente al supporto tecnico Microsoft di identificare il punto del processo di avvio in cui si è verificato l'errore. |

> [!IMPORTANT]
> Il LED di errore acceso indica un problema con il modulo controller che potrebbe essere risolto tramite riavvio. Se il riavvio del controller non consente di risolvere il problema, contattare il supporto tecnico Microsoft.  
> 
> 

### <a name="monitoring-leds-for-the-ebod-ebod-enclosure"></a>LED di monitoraggio per EBOD (chassis EBOD)
Ogni controller EBOD SAS 6 Gb/s dispone di LED che indicano lo stato, come illustrato nella figura seguente.  

  ![LED di monitoraggio - chassis EBOD][5]

Utilizzare la tabella seguente per determinare se il modulo controller EBOD funziona normalmente.  

### <a name="ebod-controller-module-indicator-leds"></a>Indicatori LED del modulo controller EBOD
| Stato | Modulo I/O OK (verde) | Errore modulo I/O (ambra) | Attività porta host (verde) |
| --- | --- | --- | --- |
| Modulo controller OK |ATTIVA |DISATTIVA |- |
| Errore del modulo controller |DISATTIVA |ATTIVA |- |
| Nessuna connessione porta host esterna |- |- |DISATTIVA |
| Connessione porta host esterna – Nessuna attività |- |- |ATTIVA |
| Connessione porta host esterna – Attività |- |- |Intermittente |
| Errore metadati modulo controller |Intermittente |- |- |

## <a name="disk-drive-indicator-leds-for-the-primary-enclosure-and-ebod-enclosure"></a>Indicatori LED unità disco per lo chassis principale e lo chassis EBOD
Le unità disco del dispositivo StorSimple sono collocate sia nello chassis principale che nello chassis EBOD. Come descritto in questa sezione, ogni unità disco contiene indicatori LED di monitoraggio. 

Per le unità disco, lo stato dell’unità è indicato da un LED verde e un LED rosso-ambra montati sulla parte anteriore di ogni modulo supporto unità. Nella figura seguente vengono illustrati tali LED.

  ![LED delle unità disco][6]

Utilizzare la tabella seguente per determinare lo stato di ogni unità disco che, a sua volta, influisce sullo stato generale del LED del pannello anteriore.  

### <a name="disk-drive-indicator-leds-for-the-ebod-enclosure"></a>Indicatori LED dell’unità disco per lo chassis EBOD
| Stato | LED attività OK (verde) | LED errore (rosso-ambra) | LED pannello delle operazioni associato |
| --- | --- | --- | --- |
| Nessuna unità installata |DISATTIVA |DISATTIVA |None |
| Unità installata e operativa |Intermittente acceso/spento in base all’attività |X |None |
| Set di identità del dispositivo servizi chassis SCSI (SES) |ATTIVA |Intermittenza 1 secondo accesa/1 secondo spenta |None |
| Set bit errore dispositivo SES |ATTIVA |ATTIVA |Errore logico (rosso) |
| Errore circuito di controllo alimentazione |DISATTIVA |ATTIVA |Errore del modulo (rosso) |

## <a name="audible-alarms"></a>Allarmi acustici
Un dispositivo StorSimple contiene allarmi acustici associati sia allo chassis principale che allo chassis EBOD. Un allarme acustico si trova sul pannello anteriore (noto anche come il pannello delle operazioni) di entrambi gli chassis. L’allarme acustico indica quando è presente una condizione di errore. L’allarme viene attivato dalle seguenti condizioni:  

* Guasto alla ventola o errore
* Voltaggio fuori misura
* Condizione di sovra o sottotemperatura
* Sovraccarico termico
* Errore di sistema
* Errore logico
* Errore di alimentazione
* Rimozione di un modulo di alimentazione e raffreddamento (PCM)  

Nella tabella seguente vengono descritti i vari stati di allarme.  

### <a name="alarm-states"></a>Stati di allarme
| Stato di allarme | Azione | Azione con il pulsante di disattivazione audio premuto |
| --- | --- | --- |
| S0 |Modalità normale: invisibile all'utente |Doppio segnale acustico |
| S1 |Modalità errore: 1 secondo accesa/1 secondo spenta |Passaggio da S2 a S3 (vedere le note) |
| S2 |Modalità promemoria: segnale acustico intermittente |None |
| S3 |Modalità disattivato: invisibile all'utente |None |
| S4 |Modalità errore critico: allarme continuo |Non disponibile: disattivazione non attiva |

> [!NOTE]
> * Nello stato di allarme S1, se non si preme Disattiva entro 2 minuti, lo stato passa automaticamente da S2 a S3.  
> * Dopo la risoluzione della condizione di errore, gli stati di allarme da S1 a S4 tornano a S0.  
> * Lo stato di errore critico S4 può essere immesso da qualunque altro stato.  


È possibile disattivare l'allarme acustico premendo l'apposito pulsante sul pannello delle operazioni. Se, dopo due minuti il commutatore di disattivazione non viene azionato manualmente, la disattivazione avviene in modo automatico. Quando l'allarme viene disattivato, continuerà a emettere brevi segnali acustici intermittenti per indicare che il problema ancora persiste. L’allarme non emetterà segnali acustici quando tutti i problemi vengono risolti.

Nella tabella seguente vengono descritte le varie condizioni di allarme.

### <a name="alarm-conditions"></a>Condizioni di allarme
| Stato | Gravità | Allarme | LED pannello delle operazioni |
| --- | --- | --- | --- |
| Avviso PCM - Interruzione dell'alimentazione CD da un singolo PCM |Errore – Perdita di ridondanza assente |S1 |Errore del modulo |
| Avviso PCM - Interruzione dell'alimentazione CD da un singolo PCM |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Guasto ventola del PCM |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Errore PCM rilevato dal modulo SBB |Errore |S1 |Errore del modulo |
| PCM rimosso |Errore di configurazione |None |Errore del modulo |
| Errore di configurazione dello chassis |Errore - Critico |S1 |Errore del modulo |
| Allerta temperatura di avviso bassa |Avviso |S1 |Errore del modulo |
| Allerta temperatura di avviso alta |Avviso |S1 |Errore del modulo |
| Allarme sovratemperatura |Errore - Critico |S1 |Errore del modulo |
| Errore del bus I2C |Errore – Perdita di ridondanza |S1 |Errore del modulo |
| Errore di comunicazione (I2C) del pannello delle operazioni |Errore - Critico |S1 |Errore del modulo |
| Errore del controller |Errore - Critico |S1 |Errore del modulo |
| Errore del modulo di interfaccia SBB |Errore - Critico |S1 |Errore del modulo |
| Errore del modulo di interfaccia SBB - Moduli funzionanti rimanenti non presenti |Errore - Critico |S4 |Errore del modulo |
| Modulo interfaccia SBB rimosso |Avviso |None |Errore del modulo |
| Errore di controllo dell’alimentazione dell’unità |Avviso - Interruzione dell'alimentazione dell’unità assente |S1 |Errore del modulo |
| Errore di controllo dell’alimentazione dell’unità |Errore - Critico; interruzione dell'alimentazione unità |S1 |Errore del modulo |
| Unità rimossa |Avviso |None |Errore del modulo |
| Disponibilità alimentazione insufficiente |Avviso |None |Errore del modulo |

## <a name="next-steps"></a>Passaggi successivi
Ulteriori informazioni sui [componenti hardware e sullo stato di StorSimple](storsimple-8000-monitor-hardware-status.md)

[1]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE01.png
[2]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE02.png
[3]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE03.png
[4]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE04.png
[5]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE05.png
[6]: ./media/storsimple-monitoring-indicators/storsimple-monitoring-indicators-IMAGE06.png


