---
title: i processi di IoT Hub Azure aaaUnderstand | Documenti Microsoft
description: "Guida per sviluppatori - pianificazione processi toorun su più dispositivi connessi tooyour IoT hub. I processi possono aggiornare i tag e le proprietà desiderate e richiamare metodi diretti su più dispositivi."
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a>Pianificare processi in più dispositivi
## <a name="overview"></a>Panoramica
Come descritto in articoli precedenti, l'hub IoT di Azure consente un numero di blocchi predefiniti ([tag e proprietà di dispositivi gemelli][lnk-twin-devguide] e [metodi diretti][lnk-dev-methods]).  In genere, le applicazioni back-end abilitare tooupdate amministratori e operatori di dispositivo e interagiscono con i dispositivi IoT in blocco e a un'ora pianificata.  I processi di incapsulano esecuzione hello di due aggiornamenti del dispositivo e metodi diretti rispetto a un set di dispositivi in una fase di pianificazione.  Ad esempio, un operatore utilizzerebbe un'app di back-end che avviano e tenere traccia di un tooreboot processo un set di dispositivi nella compilazione 43 e floor 3 in un momento che non sarebbe operazioni toohello comportano interruzioni del servizio di compilazione hello.

### <a name="when-toouse"></a>Quando toouse
È consigliabile utilizzare processi quando: una soluzione back-end esigenze tooschedule e tenere traccia dello stato delle seguenti attività su un set di dispositivi hello:

* Aggiornare le proprietà desiderate
* Aggiornare i tag
* Richiamare metodi diretti

## <a name="job-lifecycle"></a>Ciclo di vita dei processi
I processi sono avviati dal back-end di soluzione hello e mantenuti dall'IoT Hub.  È possibile avviare un processo tramite un URI del servizio (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) ed eseguire query riguardo allo stato di avanzamento in un processo in esecuzione tramite un URI del servizio (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).  Una volta che viene avviato un processo, l'esecuzione di query per i processi consente hello app back-end toorefresh hello stato processi in esecuzione.

> [!NOTE]
> Quando si avvia un processo, i valori e nomi di proprietà possono contenere solo US-ASCII stampabili caratteri alfanumerici, ad eccezione di quelli hello seguente insieme: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

## <a name="reference-topics"></a>Argomenti di riferimento:
Hello argomenti di riferimento seguenti offrono ulteriori informazioni sull'utilizzo di processi.

## <a name="jobs-tooexecute-direct-methods"></a>Metodi di processi tooexecute diretti
Hello Ecco i dettagli della richiesta hello HTTP 1.1 per l'esecuzione di un [metodo diretto] [ lnk-dev-methods] in un set di dispositivi tramite un processo:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
condizione di query Hello può anche essere in un singolo Id di dispositivo o in un elenco di ID come mostrato di seguito

**esempi**
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
[Linguaggio di query dell'hub IoT][lnk-query] illustra il linguaggio di query dell'hub IoT in maggiore dettaglio.

## <a name="jobs-tooupdate-device-twin-properties"></a>Proprietà dei processi tooupdate dispositivi doppi
Hello Ecco i dettagli della richiesta HTTP 1.1 hello per aggiornare le proprietà di un doppio dispositivo tramite un processo:

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a>Esecuzione di query sull'avanzamento dei processi
Hello Ecco hello i dettagli della richiesta HTTP 1.1 per [l'esecuzione di query per i processi][lnk-query]:

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

Hello continuationToken viene fornito dalla risposta hello.  

## <a name="jobs-properties"></a>Proprietà dei processi
Hello seguito è riportato un elenco di proprietà e le descrizioni corrispondente, che possono essere utilizzate quando si eseguono query per i processi o i risultati del processo.

| Proprietà | Description |
| --- | --- |
| **jobId** |ID dell'applicazione specificato per il processo di hello. |
| **startTime** |Ora di avvio di applicazioni fornito (ISO 8601) per processo hello. |
| **endTime** |Data (ISO 8601) IoT Hub previste quando hello processo completato. Valido solo quando il processo di hello raggiunge lo stato 'completato' hello. |
| **type** |Tipi di processi: |
| **scheduledUpdateTwin**: tooupdate un processo utilizzato un set di proprietà desiderata o i tag. | |
| **scheduledDeviceMethod**: tooinvoke un processo utilizzato un metodo di dispositivo in un set di gemelli di dispositivo. | |
| **Stato** |Stato corrente del processo di hello. Valori possibili per lo stato: |
| **in sospeso** : pianificata e in attesa toobe prelevato dal servizio processo hello. | |
| **pianificato** : pianificata per un'ora nel futuro hello. | |
| **running**: processo attualmente attivo. | |
| **cancelled**: processo annullato. | |
| **failed**: processo non riuscito. | |
| **completed**: processo completato. | |
| **deviceJobStatistics** |Statistiche sull'esecuzione del processo di hello. |

Proprietà **deviceJobStatistics**.

| Proprietà | Description |
| --- | --- |
| **deviceJobStatistics.deviceCount** |Numero di dispositivi nel processo di hello. |
| **deviceJobStatistics.failedCount** |Numero di dispositivi in cui il processo di hello non è riuscito. |
| **deviceJobStatistics.succeededCount** |Numero di dispositivi in cui il processo di hello ha avuto esito positivo. |
| **deviceJobStatistics.runningCount** |Numero di dispositivi che sono attualmente in esecuzione il processo di hello. |
| **deviceJobStatistics.pendingCount** |Numero di dispositivi che sono in attesa processo hello toorun. |

### <a name="additional-reference-material"></a>Materiale di riferimento
Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* [Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* [Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.
* [Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* [Il linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] descrive hello linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.
* [Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi
Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:

* [Pianificare e trasmettere processi][lnk-jobs-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
