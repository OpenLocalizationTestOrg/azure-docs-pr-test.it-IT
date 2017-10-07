---
title: metadati di informazioni aaaDevice nella soluzione di monitoraggio remoto hello | Documenti Microsoft
description: Una descrizione di hello Azure IoT preconfigurato soluzione di monitoraggio remoto e la relativa architettura.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1b334769-103b-4eb0-a293-184f3d1ba9a3
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 8387b98b8b2ae4934b0c900bc4df37dc17337c60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="device-information-metadata-in-hello-remote-monitoring-preconfigured-solution"></a>Metadati informazioni del dispositivo nella soluzione preconfigurata di monitoraggio remoto hello

Hello Azure IoT Suite soluzione preconfigurata di monitoraggio remoto viene illustrato un approccio per la gestione dei metadati del dispositivo. Questo articolo vengono illustrati l'approccio di hello questa soluzione richiede tooenable toounderstand è:

* Soluzione di hello metadati quali dispositivi vengono archiviati.
* Come soluzione hello gestisce i metadati del dispositivo hello.

## <a name="context"></a>Context

Hello monitoraggio remoto preconfigurato soluzione utilizza [IoT Hub Azure] [ lnk-iot-hub] tooenable toohello di dati toosend i dispositivi cloud. soluzione Hello archivia informazioni sui dispositivi in tre percorsi diversi:

| Percorso | Informazioni archiviate | Implementazione |
| -------- | ------------------ | -------------- |
| Registro delle identità | ID del dispositivo, chiavi di autenticazione, stato di abilitazione | TooIoT incorporato Hub |
| Dispositivi gemelli | Metadati: proprietà segnalate, proprietà desiderate, tag | TooIoT incorporato Hub |
| Cosmos DB | Cronologia dei comandi e dei metodi | Personalizzato per la soluzione |

IoT Hub include un [registro identità dispositivo] [ lnk-identity-registry] toomanage accedere hub IoT tooan e utilizza [gemelli dispositivo] [ lnk-device-twin] toomanage metadati del dispositivo . È disponibile anche un *registro dei dispositivi* specifico della soluzione di monitoraggio remoto, che archivia la cronologia dei comandi e dei metodi. Hello remoto monitoraggio soluzione utilizza un [DB Cosmos] [ lnk-docdb] tooimplement database un archivio personalizzato per la cronologia del comando e il metodo.

> [!NOTE]
> Hello soluzione preconfigurata di monitoraggio remoto mantiene la sincronizzazione con le informazioni di hello del Registro di sistema di hello dispositivo identity nel database DB Cosmos hello. Entrambi utilizzano hello stesso dispositivo id toouniquely identificare ogni dispositivo connesso tooyour IoT hub.

## <a name="device-metadata"></a>Metadati del dispositivo

IoT Hub conserva un [doppi dispositivo] [ lnk-device-twin] per ogni dispositivo simulato e fisico connessi tooa soluzione di monitoraggio remoto. soluzione di Hello utilizza metadati del dispositivo gemelli toomanage hello associati ai dispositivi. Un doppio di un dispositivo è un documento JSON mantenuto dall'IoT Hub e soluzione hello utilizza hello API dell'Hub IoT toointeract con gemelli di dispositivo.

Un dispositivo gemello archivia tre tipi di metadati:

- *Proprietà segnalati* hub IoT tooan inviati da un dispositivo. Nella soluzione di monitoraggio remoto hello, simulati i dispositivi le inviano proprietà restituita all'avvio e in risposta troppo**modificare lo stato del dispositivo** comandi e i metodi. È possibile visualizzare le proprietà segnalate in hello **elenco dei dispositivi** e **dettagli dispositivo** nel portale di soluzione hello. Le proprietà segnalate sono di sola lettura.
- *Le proprietà desiderate* vengono recuperati dall'hub IoT hello dai dispositivi. È responsabilità di hello di hello dispositivo toomake modificare qualsiasi configurazione necessarie sul dispositivo hello. È anche la responsabilità di hello dell'hub di hello dispositivo tooreport hello modifica toohello indietro come proprietà segnalate. È possibile impostare un valore di proprietà desiderato tramite il portale di soluzione hello.
- *Tag* esiste solo in un doppio dispositivo hello e non vengono mai sincronizzata con un dispositivo. È possibile impostare i valori di tag nel portale di soluzione hello e possono essere utilizzati filtrare l'elenco di hello dei dispositivi. soluzione Hello utilizza anche un toodisplay di icona hello tooidentify tag per un dispositivo nel portale di soluzione hello.

Esempio segnalato proprietà dai dispositivi hello simulato includono produttore, il numero di modello, latitudine e longitudine. Dispositivi simulati anche restituiranno elenco hello dei metodi supportati come una proprietà segnalata.

> [!NOTE]
> Hello dispositivo simulato solo codice hello **Desired.Config.TemperatureMeanValue** e **Desired.Config.TelemetryInterval** hello tooupdate proprietà desiderate segnalati proprietà restituita tooIoT Hub. Tutte le altre richieste di modifica delle proprietà desiderate vengono ignorate.

Un documento JSON di dispositivo informazioni dei metadati archiviato nel database di DB Cosmos hello dispositivo del Registro di sistema ha hello seguente struttura:

```json
{
  "DeviceProperties": {
    "DeviceID": "deviceid1",
    "HubEnabledState": null,
    "CreatedTime": "2016-04-25T23:54:01.313802Z",
    "DeviceState": "normal",
    "UpdatedTime": null
    },
  "SystemProperties": {
    "ICCID": null
  },
  "Commands": [],
  "CommandHistory": [],
  "IsSimulatedDevice": false,
  "id": "fe81a81c-bcbc-4970-81f4-7f12f2d8bda8"
}
```

> [!NOTE]
> Informazioni sul dispositivo possono includere anche metadati toodescribe hello telemetria hello dispositivo invia tooIoT Hub. soluzione di monitoraggio remoto Hello utilizza questo toocustomize metadati telemetria la modalità di visualizzazione dashboard hello [telemetria dinamica][lnk-dynamic-telemetry].

## <a name="lifecycle"></a>Ciclo di vita

Quando si crea un dispositivo nel portale di soluzione hello, soluzione hello crea una voce nel comando di toostore database DB Cosmos hello e la cronologia di metodo. A questo punto, la soluzione hello crea anche una voce per il dispositivo hello hello dispositivo identità del Registro di sistema, che genera l'errore hello chiavi hello dispositivo utilizza tooauthenticate con l'IoT Hub. Viene creato anche un dispositivo gemello.

Quando un dispositivo si connette prima soluzione toohello, invia proprietà segnalate e un messaggio di informazioni del dispositivo. Hello riportati i valori delle proprietà vengono salvati automaticamente in un doppio dispositivo hello. Hello segnalato proprietà includono produttore del dispositivo hello, numero di modello, il numero di serie e un elenco dei metodi supportati. messaggio di informazioni del dispositivo Hello include elenco hello dei comandi di hello hello dispositivo supporta incluse informazioni relative a eventuali parametri di comando. Quando la soluzione hello riceve questo messaggio, aggiorna le informazioni sul dispositivo hello nel database DB Cosmos hello.

### <a name="view-and-edit-device-information-in-hello-solution-portal"></a>Visualizzare e modificare le informazioni sul dispositivo nel portale di soluzione hello

elenco dei dispositivi nel portale di soluzione hello Hello Visualizza hello seguenti delle proprietà del dispositivo come colonne per impostazione predefinita: **stato**, **DeviceId**, **produttore**, **Numero modello**, **numero di serie**, **Firmware**, **piattaforma**, **processore**e  **RAM installata**. È possibile personalizzare le colonne di hello facendo **editor colonna**. proprietà del dispositivo Hello **latitudine** e **longitudine** unità posizione hello hello mappa di Bing nel dashboard di hello.

![Editor di colonne nell'elenco di dispositivi][img-device-list]

In hello **dettagli dispositivo** riquadro nel portale di soluzione hello, è possibile modificare le proprietà desiderate e tag (indicato proprietà sono di sola lettura).

![Riquadro Dettagli dispositivo][img-device-edit]

È possibile utilizzare hello soluzione portale tooremove un dispositivo dalla soluzione. Quando si rimuove un dispositivo, la soluzione hello rimuove la voce di dispositivo hello dal Registro di sistema di identità ed elimina un doppio dispositivo hello. soluzione Hello rimuove anche dispositivo toohello correlati di informazioni dai database DB Cosmos hello. Prima di poter rimuovere un dispositivo, è necessario disabilitarlo.

![Rimuovere un dispositivo][img-device-remove]

## <a name="device-information-message-processing"></a>Elaborazione dei messaggi informativi sul dispositivo

I messaggi informativi sul dispositivo inviati da un dispositivo sono diversi dai messaggi di telemetria. I messaggi informativi dispositivo includono comandi hello a che un dispositivo può rispondere e la cronologia dei comandi. IoT Hub stessa non ha alcuna conoscenza di hello metadati contenuti in un messaggio di informazioni del dispositivo e i processi hello messaggio hello allo stesso modo elabora i messaggi da dispositivo a cloud. Nella soluzione, di monitoraggio remoto hello un [Azure flusso Analitica] [ lnk-stream-analytics] processo (ASA) legge messaggi hello dall'IoT Hub. Hello **DeviceInfo** analitica di flusso del processo i filtri per messaggi che contengono **"ObjectType": "DeviceInfo"** e li inoltra toohello **EventProcessorHost** host istanza in esecuzione in un processo web. Logica di hello **EventProcessorHost** istanza utilizza i record del dispositivo id toofind hello Cosmos DB hello per record hello dispositivo e di aggiornamento specifico hello.

> [!NOTE]
> Un messaggio informativo sul dispositivo è un messaggio standard inviato dal dispositivo al cloud. soluzione Hello viene fatta distinzione tra i messaggi informativi di dispositivo e i messaggi di dati di telemetria tramite query ASA.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver apprendere come personalizzare soluzioni hello preconfigurato, è possibile esplorare alcune hello altre caratteristiche e funzionalità di soluzioni di IoT Suite preconfigurato hello:

* [Panoramica della soluzione preconfigurata di manutenzione predittiva][lnk-predictive-overview]
* [Domande frequenti su IoT Suite][lnk-faq]
* [Sicurezza di IoT da hello messa a terra][lnk-security-groundup]

<!-- Images and links -->
[img-device-list]: media/iot-suite-remote-monitoring-device-info/image1.png
[img-device-edit]: media/iot-suite-remote-monitoring-device-info/image2.png
[img-device-remove]: media/iot-suite-remote-monitoring-device-info/image3.png

[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-docdb]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-stream-analytics]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
