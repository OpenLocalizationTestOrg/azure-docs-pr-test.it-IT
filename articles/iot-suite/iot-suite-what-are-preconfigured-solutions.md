---
title: aaaAzure IoT preconfigurato soluzioni | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzioni e la relativa architettura con risorse tooadditional collegamenti.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Quali sono le soluzioni di Azure IoT Suite preconfigurato hello?

le soluzioni di Azure IoT Suite preconfigurato Hello sono implementazioni dei modelli di soluzione IoT comuni che è possibile distribuire tooAzure Usa la sottoscrizione. È possibile utilizzare soluzioni preconfigurata hello:

* Come punto di partenza per le proprie soluzioni IoT.
* toolearn sui modelli comuni di sviluppo e progettazione della soluzione IoT.

Ogni soluzione preconfigurata è un'implementazione completa, end-to-end che utilizza simulato telemetria toogenerate dispositivi.

È possibile scaricare toocustomize di codice sorgente completo hello ed estendere hello soluzione toomeet IoT requisiti specifici.

> [!NOTE]
> toodeploy di hello preconfigurato soluzioni, visitare [Microsoft Azure IoT Suite][lnk-azureiotsuite]. articolo Hello [Introduzione a soluzioni IoT preconfigurato hello] [ lnk-getstarted-preconfigured] fornisce ulteriori informazioni su come toodeploy e eseguire uno dei hello soluzioni.

Hello nella tabella seguente illustra le soluzioni hello mapping toospecific IoT funzionalità:

| Soluzione | Inserimento di dati | Identità del dispositivo | Gestione dei dispositivi | Comando e controllo | Regole e azioni | Analisi predittiva |
| --- | --- | --- | --- | --- | --- | --- |
| [Monitoraggio remoto][lnk-getstarted-preconfigured] |Sì |Sì |Sì |Sì |Sì |- |
| [Manutenzione predittiva][lnk-predictive-maintenance] |Sì |Sì |- |Sì |Sì |Sì |
| [Connected factory][lnk-getstarted-factory] |Sì |Sì |Sì |Sì |Sì |- |

* *Inserimento di dati*: in ingresso dei dati al cloud toohello scala.
* *Identità del dispositivo*: gestire le identità univoco del dispositivo e controllare toohello soluzione di accesso dei dispositivi.
* *Gestione dei dispositivi*: gestione dei metadati del dispositivo ed esecuzione delle operazioni quali il riavvio del dispositivo e gli aggiornamenti del firmware.
* *Comando e controllo*: toocause hello dispositivo tootake un'azione, inviare dispositivo tooa messaggi da cloud hello.
* *Le regole e le azioni*: tooact dati specifici di dispositivo a cloud, back-end di hello soluzione utilizza le regole.
* *Analitica predittiva*: hello soluzione back-end analizza i dati di dispositivo a cloud toopredict quando eseguire azioni specifiche. Ad esempio, l'analisi aereo motore telemetria toodetermine alla manutenzione di un motore scadenza.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Panoramica della soluzione preconfigurata per il monitoraggio remoto

Abbiamo scelto toodiscuss hello soluzione preconfigurata di monitoraggio remoto in questo articolo perché illustra molti elementi di progettazione comune che hello condivisione altre soluzioni.

Hello diagramma seguente illustra gli elementi chiave hello di hello soluzione di monitoraggio remoto. Hello nelle sezioni seguenti vengono forniscono ulteriori informazioni su questi elementi.

![Architettura della soluzione preconfigurata per il monitoraggio remoto][img-remote-monitoring-arch]

## <a name="devices"></a>Dispositivi

Quando si distribuisce una soluzione preconfigurata di monitoraggio remoto hello, quattro dispositivi simulati sono pre-provisioning nella soluzione hello che simula un dispositivo di raffreddamento. I dispositivi simulati hanno un modello di umidità e temperatura predefinito che genera i dati di telemetria. Vengono inclusi questi dispositivi simulati per:

- Viene illustrato il flusso end-to-end hello di dati attraverso la soluzione hello.
- Offrire un'utile origine di dati di telemetria.
- Se si è uno sviluppatore di back-end utilizzando la soluzione hello come punto di partenza per un'implementazione personalizzata, forniscono un obiettivo di metodi o i comandi.

dispositivi Hello simulato nella soluzione hello possono rispondere toohello comunicazioni cloud a dispositivo seguenti:

- *Metodi ([diretta metodi][lnk-direct-methods])*: un metodo di comunicazione bidirezionale in un dispositivo connesso è previsto toorespond immediatamente.
- *Comandi (cloud a dispositivo messaggi)*: un metodo di comunicazione unidirezionale in cui un dispositivo recupera comando hello da una coda durevole.

Per un confronto tra questi diversi approcci, vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].

Quando un dispositivo si connette innanzitutto tooIoT Hub nella soluzione hello preconfigurato, invia un hub di toohello messaggio informazioni dispositivo. Questo messaggio enumera i metodi di hello dispositivo hello può rispondere a. In hello soluzione preconfigurata di monitoraggio remoto, i dispositivi simulati supportano questi metodi:

* *Avviare l'aggiornamento del Firmware*: questo metodo avvia un'attività asincrona in hello dispositivo tooperform un aggiornamento del firmware. attività asincrona Hello Usa del dashboard di soluzione toohello proprietà segnalati toodeliver lo stato degli aggiornamenti.
* *Riavviare il computer*: questo metodo determina tooreboot dispositivo simulato hello.
* *FactoryReset*: questo metodo attiva delle impostazioni di fabbrica nel dispositivo simulato hello.

Quando un dispositivo si connette innanzitutto tooIoT Hub nella soluzione hello preconfigurato, invia un hub di toohello messaggio informazioni dispositivo. Questo messaggio enumera i comandi di hello dispositivo hello può rispondere a. In hello soluzione preconfigurata di monitoraggio remoto, i dispositivi simulati supportano questi comandi:

* *Dispositivo di ping*: dispositivo hello risponde toothis comando con un acknowledgement. Questo comando è utile per controllare che il dispositivo hello è ancora attivo e in attesa.
* *Avviare telemetria*: indica hello dispositivo toostart l'invio di dati di telemetria.
* *Arrestare i dati di telemetria*: indica hello dispositivo toostop l'invio di dati di telemetria.
* *Imposta punto di temperatura modificare*: controlli hello temperatura simulato telemetria valori hello dispositivo invia. Questo comando è utile per testare la logica di back-end.
* *Telemetria sulla diagnostica*: controlla se il dispositivo hello deve inviare temperatura esterno hello come dati di telemetria.
* *Modifica dello stato del dispositivo*: imposta la proprietà hello dispositivo lo stato dei metadati che hello report del dispositivo. Questo comando è utile per testare la logica di back-end.

È possibile aggiungere ulteriori soluzioni toohello simulati i dispositivi che generano hello stesso telemetria e la risposta toohello stessi metodi e comandi.

Inoltre tooresponding toocommands e i metodi, hello soluzione Usa [gemelli dispositivo][lnk-device-twin]. I dispositivi usano dispositivo gemelli tooreport proprietà valori toohello soluzione back-end. dashboard di soluzione Hello utilizza i valori delle proprietà dispositivo gemelli tooset toonew desiderato nei dispositivi. Ad esempio, durante i report di dispositivo hello simulato processo aggiornamento firmware hello stato hello di hello aggiornare utilizzando le proprietà segnalate.

## <a name="iot-hub"></a>Hub IoT

In questa soluzione preconfigurata hello istanza dell'IoT Hub corrisponde toohello *Gateway del Cloud* in una tipica [architettura della soluzione IoT][lnk-what-is-azure-iot].

Un hub IoT riceve i dati di telemetria dai dispositivi hello in un singolo endpoint. Un hub IoT gestisce anche gli endpoint specifici del dispositivo in cui ogni periferica può recuperare i comandi di hello inviati tooit.

hub IoT Hello rende disponibili hello lato servizio telemetria leggere endpoint telemetria hello ricevuto.

funzionalità di gestione di dispositivi Hello dell'IoT Hub consente toomanage è la proprietà del dispositivo da hello soluzione portale e pianificare i processi che eseguono operazioni, ad esempio:

- Riavvio dei dispositivi
- Modifica degli stati del dispositivo
- Aggiornamenti del firmware

## <a name="azure-stream-analytics"></a>Analisi di flusso di Azure

Hello preconfigurato soluzione utilizza tre [Azure flusso Analitica] [ lnk-asa] flusso (ASA) processi toofilter hello telemetria dai dispositivi hello:

* *Processo DeviceInfo* -output dati tooan hub eventi da cui esegue il routing del Registro di sistema di dispositivo i messaggi di registrazione specifiche toohello soluzione dispositivo. Questo Registro di sistema del dispositivo è un database di Azure Cosmos DB. Tali messaggi vengono inviati quando un dispositivo si connette prima di tutto o in risposta tooa **modificare lo stato del dispositivo** comando.
* *Il processo di telemetria* - invia tutti i dati di telemetria non elaborati tooAzure l'archivio blob per freddo archiviazione e calcolo delle aggregazioni di dati di telemetria che consentono di visualizzare nel dashboard di soluzione hello.
* *Il processo di regole* - filtri hello flusso di dati di telemetria per i valori che superano le soglie di qualsiasi regola e output hello hub eventi tooan di dati. Quando viene attivata una regola, hello soluzione dashboard del portale visualizzare questo evento come una nuova riga nella tabella di cronologia di allarme hello. Queste regole possono inoltre attivare un'azione in base alle impostazioni di hello definite in hello **regole** e **azioni** viste nel portale di soluzione hello.

In questa soluzione preconfigurata hello ASA processi fanno parte di toohello **back-end di soluzione IoT** in una tipica [architettura della soluzione IoT][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Processore di eventi

In questa soluzione preconfigurata, il processore di eventi di hello fa parte di hello **back-end di soluzione IoT** in una tipica [architettura della soluzione IoT][lnk-what-is-azure-iot].

Hello **DeviceInfo** e **regole** processi ASA inviare loro hub tooEvent di output per il recapito tooother servizi di back-end. soluzione Hello utilizza un [EventProcessorHost] [ lnk-event-processor] istanza, in esecuzione in un [processo Web][lnk-web-job], messaggi hello tooread dagli hub eventi. Hello **EventProcessorHost** utilizza:
- Hello **DeviceInfo** dati tooupdate hello dispositivo di dati nel database DB Cosmos hello.
- Hello **regole** dati tooinvoke hello logica app e aggiornamento hello vengono visualizzati avvisi nel portale di soluzione hello.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Registro delle identità dei dispositivi, dispositivo gemello e Cosmos DB

Ogni hub IoT include un [registro delle identità dei dispositivi][lnk-identity-registry] che archivia le chiavi del dispositivo. IoT Hub questa informazione viene utilizzata l'autenticazione dei dispositivi: un dispositivo deve essere registrato e presenta una chiave valida prima di connettere toohello hub.

Oggetto [doppi dispositivo] [ lnk-device-twin] è un documento JSON gestito da hello IoT Hub. Un gemello dispositivo di un dispositivo contiene:

- Proprietà segnalate inviate dall'hub di toohello dispositivo hello. È possibile visualizzare queste proprietà nel portale di soluzione hello.
- Proprietà desiderate che si desidera toosend toohello dispositivo. È possibile impostare queste proprietà nel portale di soluzione hello.
- Tag che esiste solo in un doppio dispositivo hello e non su dispositivo hello. È possibile usare questi elenchi toofilter tag dei dispositivi nel portale di soluzione hello.

Questa soluzione Usa metadati dispositivo toomanage gemelli del dispositivo. soluzione di Hello utilizza anche un database DB Cosmos toostore dati di dispositivo specifici della soluzione aggiuntivi, ad esempio hello comandi supportati da ogni dispositivo e hello cronologia del comando.

soluzione Hello dovrà conservare anche informazioni hello nel Registro di identità dispositivo hello sincronizzato con il contenuto di hello del database DB Cosmos hello. Hello **EventProcessorHost** utilizza hello dati da **DeviceInfo** sincronizzazione hello toomanage analitica di flusso del processo.

## <a name="solution-portal"></a>Portale della soluzione

![portale della soluzione][img-dashboard]

portale di soluzione hello è un'interfaccia utente basata sul web che viene distribuito toohello cloud come parte della soluzione hello preconfigurato. Consente di:

* Visualizzare la cronologia di avvisi e i dati di telemetria in un dashboard.
* Eseguire il provisioning di nuovi dispositivi.
* Gestire e monitorare i dispositivi.
* Inviare comandi toospecific dispositivi.
* Richiamare i metodi su dispositivi specifici.
* Gestire regole e azioni.
* Pianificare i processi toorun in uno o più dispositivi.

In questa soluzione preconfigurata portale soluzione hello fa parte di hello **back-end di soluzione IoT** e parte di hello **connettività per l'elaborazione e aziendale** in hello tipico [soluzione IoT architettura][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulle architetture delle soluzioni IoT, vedere il documento relativo all'[architettura di riferimento dei servizi IoT di Microsoft Azure][lnk-refarch].

Ora si è certi di quali una soluzione preconfigurata è, è possibile iniziare la distribuzione di hello *monitoraggio remoto* preconfigurato soluzione: [Introduzione a soluzioni hello preconfigurato] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
