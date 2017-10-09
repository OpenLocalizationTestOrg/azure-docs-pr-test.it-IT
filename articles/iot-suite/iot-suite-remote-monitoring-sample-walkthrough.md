---
title: procedura dettagliata sulla soluzione di monitoraggio preconfigurato aaaRemote | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione di monitoraggio remoto e la relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 31fe13af-0482-47be-b4c8-e98e36625855
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57a336bd94938c2b9ee5d3456ea8e45446cf3d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="remote-monitoring-preconfigured-solution-walkthrough"></a>Procedura dettagliata della soluzione preconfigurata per il monitoraggio remoto

Hello IoT Suite di monitoraggio remoto [preconfigurato soluzione] [ lnk-preconfigured-solutions] è un'implementazione di un end-to-end monitoraggio soluzione per più macchine virtuali in esecuzione in posizioni remote. soluzione Hello combina servizi Azure chiave tooprovide un'implementazione generica di scenario aziendale hello. È possibile utilizzare la soluzione hello come punto di partenza per la propria implementazione e [personalizzare] [ lnk-customize] è toomeet i requisiti aziendali specifici.

Questo articolo vengono illustrati alcuni elementi chiave hello, di hello remoto monitoraggio soluzione tooenable toounderstand il funzionamento. Queste informazioni consentono di:

* Risolvere i problemi nella soluzione hello.
* Pianificare la modalità toocustomize toohello soluzione toomeet esigenze specifiche. 
* Progettare la propria soluzione IoT che usa i servizi di Azure.

## <a name="logical-architecture"></a>Architettura logica

Hello seguente diagramma illustra i componenti logici hello della soluzione preconfigurata hello:

![Architettura logica](media/iot-suite-remote-monitoring-sample-walkthrough/remote-monitoring-architecture.png)

## <a name="simulated-devices"></a>Dispositivi simulati

Nella soluzione hello preconfigurato, dispositivo simulato hello rappresenta un dispositivo di raffreddamento (ad esempio una compilazione condizionatore o unità di gestione delle funzionalità aria). Quando si distribuisce la soluzione hello preconfigurato, inoltre automaticamente il provisioning di quattro simulati dispositivi che vengono eseguiti in un [processo Web di Azure][lnk-webjobs]. dispositivi Hello simulato semplificano si tooexplore hello comportamento della soluzione hello senza hello necessità toodeploy eventuali dispositivi fisici. toodeploy un dispositivo fisico reale, vedere hello [connettersi toohello il dispositivo remoto monitoraggio soluzione preconfigurata] [ lnk-connect-rm] esercitazione.

### <a name="device-to-cloud-messages"></a>Messaggi da dispositivo a cloud

Ogni dispositivo simulato può inviare i seguenti tipi di messaggio tooIoT Hub hello:

| Message | Descrizione |
| --- | --- |
| Startup |Quando si avvia il dispositivo di hello, invia un **informazioni sul dispositivo** messaggio contenente informazioni su se stesso toohello back-end. Questi dati includono l'id dispositivo hello e un elenco di comandi hello e metodi hello supporta dispositivi. |
| Presenza |Un dispositivo invia periodicamente un **presenza** messaggio tooreport se dispositivo hello può rilevare la presenza hello di un sensore. |
| Telemetria |Un dispositivo invia periodicamente un **telemetria** messaggio che segnala simulati i valori di temperatura hello e l'umidità non raccolti dal dispositivo hello del simulato sensori. |

> [!NOTE]
> soluzione Hello archivia l'elenco di hello di comandi supportato dal dispositivo hello in un database DB Cosmos e non in un doppio dispositivo hello.

### <a name="properties-and-device-twins"></a>Proprietà e dispositivi gemelli

Hello simulati i dispositivi le inviano hello seguente dispositivo proprietà toohello [doppi] [ lnk-device-twins] nell'hub IoT hello come *segnalati proprietà*. dispositivo invia Hello segnalati proprietà all'avvio e risposta tooa **modifica dello stato del dispositivo** metodo o il comando.

| Proprietà | Scopo |
| --- | --- |
| Config.TelemetryInterval | Dispositivo hello frequenza (secondi) invia i dati di telemetria |
| Config.TemperatureMeanValue | Specifica il valore medio di hello per hello simulato temperatura telemetria |
| Device.DeviceID |ID che viene fornito o assegnato al momento della creazione di un dispositivo nella soluzione hello |
| Device.DeviceState | Stato segnalato dal dispositivo hello |
| Device.CreatedTime |Dispositivo hello ora è stato creato nella soluzione hello |
| Device.StartupTime |Dispositivo hello ora è stato avviato |
| Device.LastDesiredPropertyChange |modificare il numero di versione Hello della proprietà desiderata ultimo hello |
| Device.Location.Latitude |Posizione di latitudine di hello dispositivo |
| Device.Location.Longitude |Posizione di longitudine di hello dispositivo |
| System.Manufacturer |Produttore del dispositivo |
| System.ModelNumber |Numero di modello di dispositivo hello |
| System.SerialNumber |Numero di serie del dispositivo hello |
| System.FirmwareVersion |Versione corrente del firmware sul dispositivo hello |
| System.Platform |Architettura della piattaforma del dispositivo hello |
| System.Processor |Dispositivo hello in esecuzione processore |
| System.InstalledRAM |Quantità di RAM installato sul dispositivo hello |

simulatore Hello semi queste proprietà in dispositivi simulati con valori di esempio. Ogni volta che il simulatore hello Inizializza un dispositivo simulato, il dispositivo hello report hello metadati predefiniti tooIoT Hub come proprietà segnalate. Proprietà restituita può essere aggiornata solo dal dispositivo hello. una proprietà segnalata toochange, impostare la proprietà desiderata nel portale di soluzione. È responsabilità di hello del dispositivo hello per:

1. Dall'hub IoT hello recuperare periodicamente le proprietà desiderate.
2. Aggiornare la configurazione con valore della proprietà hello desiderato.
3. Inviare nuovo hub di back-toohello valore hello come una proprietà segnalata.

Dal dashboard di soluzione hello, è possibile utilizzare *le proprietà desiderate* tooset proprietà in un dispositivo utilizzando hello [doppi dispositivo][lnk-device-twins]. In genere, un dispositivo legge un valore della proprietà desiderata da hello hub tooupdate che il relativo stato interno e hello report modificare nuovamente come una proprietà segnalata.

> [!NOTE]
> Hello dispositivo simulato solo codice hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** hello tooupdate proprietà desiderate segnalati proprietà restituita tooIoT Hub. Nel dispositivo simulato hello, vengono ignorate tutte le altre richieste di modifica della proprietà desiderata.

### <a name="methods"></a>Metodi

Hello dispositivi simulati in grado di gestire hello dei seguenti metodi ([diretta metodi][lnk-direct-methods]) viene richiamato dal portale di soluzione hello tramite l'hub IoT hello:

| Metodo | Descrizione |
| --- | --- |
| InitiateFirmwareUpdate |Indica a hello dispositivo tooperform un aggiornamento del firmware |
| Reboot |Indica a hello dispositivo tooreboot |
| FactoryReset |Indica di Reimposta una factory di hello dispositivo tooperform |

Alcuni metodi utilizzano proprietà segnalati tooreport sullo stato di avanzamento. Ad esempio, hello **InitiateFirmwareUpdate** metodo Simula aggiornamento hello in esecuzione in modo asincrono sul dispositivo hello. metodo Hello restituisce immediatamente sul dispositivo hello, mentre l'attività asincrona hello continua toosend nuovamente gli aggiornamenti dello stato toohello soluzione dashboard usando segnalato proprietà.

### <a name="commands"></a>Comandi:

dispositivi Hello simulato è possono gestire hello comandi (cloud a dispositivo messaggi) inviati dal portale di soluzione hello tramite l'hub IoT hello seguenti:

| Comando | Descrizione |
| --- | --- |
| PingDevice |Invia un *ping* toohello toocheck di dispositivo è attivo |
| StartTelemetry |Dispositivo hello viene avviato l'invio di dati di telemetria |
| StopTelemetry |Interrompe l'invio di dati di telemetria di hello |
| ChangeSetPointTemp |Modifica il valore dell'imposta punto hello intorno al quale hello vengono generati dati casuali |
| DiagnosticTelemetry |I trigger hello toosend simulatore di dispositivo un valore di dati di telemetria aggiuntive (externalTemp) |
| ChangeDeviceState |Modifica una proprietà di stato esteso per il dispositivo hello e Invia messaggio di informazioni sul dispositivo di hello dal dispositivo hello |

> [!NOTE]
> Per un confronto tra questi comandi (messaggi da cloud a dispositivo) e i metodi (metodi diretti), vedere [Indicazioni sulle comunicazioni da cloud a dispositivo][lnk-c2d-guidance].

## <a name="iot-hub"></a>Hub IoT

Hello [hub IoT] [ lnk-iothub] inserisce i dati inviati da dispositivi hello in cloud hello e rende disponibili toohello i processi di Azure flusso Analitica (ASA). Ogni processo ASA flusso Usa IoT Hub consumer gruppo tooread hello flusso separato di messaggi dai dispositivi.

Hello anche hub IoT nella soluzione hello:

- Gestisce un registro di sistema di identità che archivia gli ID hello e chiavi di autenticazione di tutti i dispositivi di hello tooconnect toohello portale è consentiti. È possibile abilitare e disabilitare i dispositivi tramite il Registro di identità hello.
- Invia comandi tooyour dispositivi per conto di portale soluzione hello.
- Richiama i metodi nei dispositivi per conto di portale soluzione hello.
- Gestisce i dispositivi gemelli per tutti i dispositivi registrati. Un doppio di un dispositivo archivia i valori delle proprietà hello segnalati da un dispositivo. Un doppio di un dispositivo archivia anche le proprietà desiderate impostate nel portale di soluzione hello per hello dispositivo tooretrieve quando si connette quindi.
- Le pianificazioni dei processi di proprietà tooset per più dispositivi o chiamare metodi su più dispositivi.

## <a name="azure-stream-analytics"></a>Analisi di flusso di Azure

Nella soluzione, di monitoraggio remoto hello [Azure flusso Analitica] [ lnk-asa] (ASA) invia i messaggi di dispositivo ricevuti dai componenti hello IoT hub tooother back-end per l'elaborazione o di archiviazione. Diversi processi ASA eseguono operazioni specifiche in base al contenuto dei messaggi hello hello.

**Processo 1: Informazioni sul dispositivo** Filtra i messaggi informativi di dispositivo dal flusso di messaggi hello in arrivo e li invia a endpoint di Hub eventi tooan. Un dispositivo invia i messaggi informativi di dispositivo all'avvio e di risposta tooa **SendDeviceInfo** comando. Questo processo Usa hello seguente query definizione tooidentify **informazioni sul dispositivo** messaggi:

```
SELECT * FROM DeviceDataStream Partition By PartitionId WHERE  ObjectType = 'DeviceInfo'
```

Consente di inviare il tooan output Hub eventi per un'ulteriore elaborazione.

**Processo 2: Regole** restituisce valori di telemetria in entrata relativi a temperatura e umidità rispetto alle soglie per dispositivo. I valori di soglia vengono impostati nell'editor delle regole hello disponibile nel portale di soluzione hello. Ogni coppia dispositivo/valore viene archiviata in base al timestamp in un BLOB che viene letto in Analisi di flusso come **dati di riferimento**. qualsiasi valore non vuoto hello di soglia impostata per il dispositivo hello viene confrontato con il processo di Hello. Se il valore supera hello ' >' condizione, l'output del processo di hello un **allarme** evento che indica che tale soglia hello viene superato e fornisce dispositivo hello, valore e i valori di timestamp. Questo processo Usa hello seguente query definizione tooidentify telemetria messaggi devono attivare un allarme:

```
WITH AlarmsData AS 
(
SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Temperature' as ReadingType,
     Stream.Temperature as Reading,
     Ref.Temperature as Threshold,
     Ref.TemperatureRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature

UNION ALL

SELECT
     Stream.IoTHub.ConnectionDeviceId AS DeviceId,
     'Humidity' as ReadingType,
     Stream.Humidity as Reading,
     Ref.Humidity as Threshold,
     Ref.HumidityRuleOutput as RuleOutput,
     Stream.EventEnqueuedUtcTime AS [Time]
FROM IoTTelemetryStream Stream
JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
WHERE
     Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
)

SELECT *
INTO DeviceRulesMonitoring
FROM AlarmsData

SELECT *
INTO DeviceRulesHub
FROM AlarmsData
```

Hello processo invia relativo tooan output Hub eventi per un'ulteriore elaborazione e lo salva i dettagli di ogni archiviazione tooblob avviso da dove portale soluzione hello possa leggere informazioni sugli avvisi di hello.

**Processo 3: Telemetria** opera su hello flusso in ingresso dispositivo telemetria in due modi. Hello invia prima tutti i messaggi di dati di telemetria dall'archiviazione blob di toopersistent hello dispositivi per l'archiviazione a lungo termine. Hello secondo calcola umidità medio, minimo e massimo valori su una finestra temporale scorrevole di cinque minuti e invia l'archiviazione dei dati tooblob. portale di soluzione Hello legge i dati di telemetria hello da grafici di hello toopopulate archiviazione blob. Questo processo Usa hello dopo la definizione della query:

```
WITH 
    [StreamData]
AS (
    SELECT
        *
    FROM [IoTHubStream]
    WHERE
        [ObjectType] IS NULL -- Filter out device info and command responses
) 

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    Temperature,
    Humidity,
    ExternalTemperature,
    EventProcessedUtcTime,
    PartitionId,
    EventEnqueuedUtcTime,
    * 
INTO
    [Telemetry]
FROM
    [StreamData]

SELECT
    IoTHub.ConnectionDeviceId AS DeviceId,
    AVG (Humidity) AS [AverageHumidity],
    MIN(Humidity) AS [MinimumHumidity],
    MAX(Humidity) AS [MaxHumidity],
    5.0 AS TimeframeMinutes 
INTO
    [TelemetrySummary]
FROM [StreamData]
WHERE
    [Humidity] IS NOT NULL
GROUP BY
    IoTHub.ConnectionDeviceId,
    SlidingWindow (mi, 5)
```

## <a name="event-hubs"></a>Hub eventi

Hello **informazioni sul dispositivo** e **regole** processi ASA output i relativi dati tooEvent hub tooreliably rollforward in toohello **processore di eventi** in esecuzione in hello processo Web.

## <a name="azure-storage"></a>Archiviazione di Azure

soluzione Hello utilizza tutti i dati di telemetria non elaborati e riepilogati hello dai dispositivi hello toopersist di archiviazione blob di Azure nella soluzione hello. portale Hello legge i dati di telemetria hello da grafici di hello toopopulate archiviazione blob. avvisi toodisplay, portale soluzione hello legge dati hello dall'archiviazione blob che registra hello valori superati telemetria configurati i valori di soglia. soluzione Hello utilizza valori soglia blob archiviazione toorecord hello che è impostato nel portale di soluzione hello.

## <a name="webjobs"></a>WebJobs

Inoltre simulatori di dispositivo toohosting hello, hello processi Web nella soluzione hello anche hello host **processore di eventi** in esecuzione in un processo Web di Azure che gestisce le risposte di comando. Usa comando risposta messaggi tooupdate hello comando Cronologia dispositivo (archiviata nel database DB Cosmos hello).

## <a name="cosmos-db"></a>Cosmos DB

soluzione di Hello utilizza un DB Cosmos database toostore informazioni sulle hello dispositivi connessi toohello soluzione. Queste informazioni includono cronologia hello di comandi inviati toodevices dal portale di soluzione hello e i metodi richiamati dal portale di soluzione hello.

## <a name="solution-portal"></a>Portale della soluzione

portale di soluzione hello è un'app web distribuita come parte della soluzione hello preconfigurato. le pagine di chiave Hello nel portale di soluzione hello sono dashboard hello e l'elenco dei dispositivi hello.

### <a name="dashboard"></a>Dashboard

Questa pagina nell'app web hello utilizza controlli javascript Power BI (vedere [repository PowerBI-visuals](https://www.github.com/Microsoft/PowerBI-visuals)) toovisualize i dati di telemetria dai dispositivi hello hello. soluzione di Hello utilizza hello ASA telemetria processo toowrite hello telemetria tooblob archiviazione dei dati.

### <a name="device-list"></a>Elenco dei dispositivi

In questa pagina nel portale di soluzione hello è possibile:

* Effettuare il provisioning di un nuovo dispositivo. Questa azione imposta l'id univoco del dispositivo hello e genera la chiave di autenticazione hello. Scrive informazioni hello di tooboth dispositivo hello del Registro di sistema identità IoT Hub e il database di DB Cosmos hello specifici della soluzione.
* Gestire le proprietà dei dispositivi. Questa azione include la visualizzazione delle proprietà esistenti e l'aggiornamento con nuove proprietà.
* Invio dispositivo tooa comandi.
* Consente di visualizzare la cronologia dei comandi hello per un dispositivo.
* Abilitare e disabilitare i dispositivi.

## <a name="next-steps"></a>Passaggi successivi

Hello post di blog di TechNet seguenti forniscono ulteriori dettagli su hello soluzione preconfigurata di monitoraggio remoto:

* [Monitoraggio remoto di IoT Suite - Under hello quinte-](http://social.technet.microsoft.com/wiki/contents/articles/32941.iot-suite-under-the-hood-remote-monitoring.aspx)
* [Aggiunta di dispositivi veri e simulati per il monitoraggio remoto in IoT Suite](http://social.technet.microsoft.com/wiki/contents/articles/32975.iot-suite-remote-monitoring-adding-live-and-simulated-devices.aspx)

È possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:

* [Connettere la soluzione preconfigurata di monitoraggio remoto toohello di dispositivo][lnk-connect-rm]
* [Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]

[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-iothub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-webjobs]: https://azure.microsoft.com/documentation/articles/websites-webjobs-resources/
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twins]:  ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
