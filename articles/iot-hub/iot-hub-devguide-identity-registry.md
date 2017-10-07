---
title: "Registro di sistema aaaUnderstand hello Azure IoT Hub identità | Documenti Microsoft"
description: "Guida per sviluppatori - descrizione del Registro di identità IoT Hub hello e come toouse, toomanage i dispositivi. Include informazioni su hello importazione ed esportazione di identità di dispositivi in blocco."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0706eccd-e84c-4ae7-bbd4-2b1a22241147
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c9fe3730a4608e28c47807ecb42e13e73f6a2e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-hello-identity-registry-in-your-iot-hub"></a>Comprendere hello identità nel Registro di sistema dell'hub IoT

Ogni hub IoT è un registro di sistema di identità che archivia le informazioni sui dispositivi hello consentito tooconnect toohello IoT hub. Prima di un dispositivo possa connettersi tooan IoT hub, deve essere presente una voce per il dispositivo nel Registro di sistema dell'hub IoT hello identità. Un dispositivo deve autenticare anche con l'hub IoT hello in base alle credenziali archiviate nel Registro di identità hello.

ID dispositivo Hello archiviate nel Registro di identità hello è tra maiuscole e minuscole.

In generale, Registro di sistema di hello identità è una raccolta di risorse di identità di dispositivi con supporto per REST. Quando si aggiunge una voce nel Registro di sistema identità hello, IoT Hub consente di creare un set di risorse per ogni dispositivo, ad esempio coda hello che contiene i messaggi in transito cloud a dispositivo.

### <a name="when-toouse"></a>Quando toouse

Utilizzare il Registro di identità hello quando è necessario:

* Il provisioning dei dispositivi che si connettono tooyour IoT hub.
* Controllare gli endpoint che utilizzano il dispositivo dell'hub tooyour accesso di ogni dispositivo.

> [!NOTE]
> Registro di identità Hello non contiene i metadati specifici dell'applicazione.

## <a name="identity-registry-operations"></a>Operazioni del registro delle identità

Hello del Registro di sistema di IoT Hub identity espone hello seguenti operazioni:

* Creare l'identità del dispositivo
* Aggiornare l'identità del dispositivo
* Recuperare l'identità del dispositivo tramite ID
* Eliminare l'identità del dispositivo
* Elenco di identità too1000
* Esportare tutti gli archivi blob tooAzure di identità
* Importare le identità nell'Archiviazione BLOB di Azure

Tutte queste operazioni possono usare la concorrenza ottimistica, come specificato in [RFC7232][lnk-rfc7232].

> [!IMPORTANT]
> Hello solo modo tooretrieve tutte le identità nel Registro di identità di un hub IoT è hello toouse [esportare] [ lnk-export] funzionalità.

Un registro delle identità di un hub IoT:

* Non contiene metadati delle applicazioni.
* È possibile accedere come un dizionario, utilizzando hello **deviceId** come chiave hello.
* Non supporta le query espressive.

Una soluzione IoT include in genere un archivio separato specifico della soluzione che contiene metadati specifici dell'applicazione. Ad esempio, hello archivio specifici della soluzione in una soluzione di compilazione smart registrerà chat hello in cui viene distribuito un sensore di temperatura.

> [!IMPORTANT]
> Utilizzare solo il Registro di identità hello per le operazioni di provisioning e gestione dei dispositivi. Le operazioni ad alta velocità effettiva in fase di esecuzione non devono dipendere l'esecuzione di operazioni nel Registro di sistema di hello identità. Ad esempio, il controllo dello stato di connessione di hello di un dispositivo prima di inviare un comando non è un modello supportato. Verificare che hello toocheck [tassi di limitazione] [ lnk-quotas] per il Registro di identità hello e hello [heartbeat dispositivo] [ lnk-guidance-heartbeat] modello.

## <a name="disable-devices"></a>Disabilitare i dispositivi

È possibile disabilitare i dispositivi aggiornando hello **stato** proprietà di un'identità nel Registro di sistema di hello identità. Questa proprietà viene in genere usata in due scenari:

* Durante un processo di orchestrazione di provisioning. Per altre informazioni, vedere [Provisioning di dispositivi][lnk-guidance-provisioning].
* Se, per qualsiasi motivo, si considera un dispositivo compromesso o non più autorizzato.

## <a name="import-and-export-device-identities"></a>Importare ed esportare le identità dei dispositivi

È possibile esportare le identità del dispositivo in blocco da Registro di sistema di identità di un hub IoT, utilizzando le operazioni asincrone in hello [endpoint del provider di risorse IoT Hub][lnk-endpoints]. Le esportazioni sono con esecuzione prolungata processi che utilizzano dati di identità dispositivo un blob dal cliente, contenitore toosave leggere dal Registro di sistema di hello identità.

È possibile importare le identità del dispositivo del Registro di sistema di identità dell'hub IoT tooan di massa, utilizzando le operazioni asincrone in hello [endpoint del provider di risorse IoT Hub][lnk-endpoints]. Le importazioni sono processi con esecuzione prolungata che utilizzano i dati in un blob dal cliente, contenitore toowrite dispositivo identità di dati nel Registro di sistema di hello identità.

* Per informazioni dettagliate su hello importazione ed esportazione API, vedere [il provider di risorse IoT Hub API REST][lnk-resource-provider-apis].
* toolearn informazioni sull'esecuzione di importazione e i processi di esportazione, vedere [Bulk di gestione delle identità del dispositivo IoT Hub][lnk-bulk-identity].

## <a name="device-provisioning"></a>Provisioning di dispositivi

dati del dispositivo Hello che archivia una determinata soluzione IoT dipendono dai requisiti di specifiche di hello di tale soluzione. Tuttavia, come minimo, una soluzione deve archiviare identità di dispositivo e chiavi di autenticazione. L'hub IoT di Azure include un registro delle identità in grado di archiviare i valori per ogni dispositivo, ad esempio ID, chiavi di autenticazione e codici di stato. Una soluzione possa utilizzare altri servizi di Azure quali archiviazione tabelle, archiviazione blob o toostore DB Cosmos dati aggiuntive del dispositivo.

*Provisioning dei dispositivi* hello processo di aggiunta di archivi toohello dati di hello iniziale del dispositivo nella soluzione. tooenable un nuovo hub tooyour tooconnect di dispositivo, è necessario aggiungere un dispositivo ID e le chiavi toohello del Registro di sistema di IoT Hub identità. Come parte del processo di provisioning hello, potrebbe essere necessario tooinitialize di dati specifico del dispositivo in altri archivi di soluzione.

## <a name="device-heartbeat"></a>Heartbeat dispositivo

Registro di sistema di IoT Hub identità Hello contiene un campo denominato **connectionState**. Utilizzare solo hello **connectionState** campo durante lo sviluppo e debug. Soluzioni IoT non devono eseguire query campo hello in fase di esecuzione. Ad esempio, non eseguire una query hello **connectionState** toocheck campo se un dispositivo è connesso prima di inviare un messaggio da cloud a dispositivo o un SMS.

Se la soluzione IoT deve tooknow se è connesso un dispositivo, è necessario implementare hello *criterio heartbeat*.

Nel modello di heartbeat hello, dispositivo hello invia i messaggi da dispositivo a cloud almeno una volta ogni periodo di tempo (ad esempio, almeno una volta ogni ora) stabilito. Pertanto, anche se un dispositivo non dispone di qualsiasi toosend di dati, ancora invia un messaggio vuoto da dispositivo a cloud (in genere con una proprietà che lo identifica come un heartbeat). Sul lato servizio hello, soluzione hello mantiene una mappa con ultimo heartbeat hello ricevuti per ogni dispositivo. Se la soluzione hello non riceve un messaggio di heartbeat entro il tempo di hello previsto dal dispositivo hello, si presuppone che si è verificato un problema con dispositivo hello.

Un'implementazione più complessa potrebbe includere informazioni hello [monitoraggio delle operazioni] [ lnk-devguide-opmon] tooidentify dispositivi che si sta tentando di tooconnect o comunicano ma esito negativo. Quando si implementa il pattern di heartbeat hello, assicurarsi che toocheck [IoT Hub quote e velocità][lnk-quotas].

> [!NOTE]
> Se una connessione di hello utilizza soluzione IoT stato toodetermine unicamente se i messaggi da cloud a dispositivo toosend, e i messaggi non broadcast toolarge set di dispositivi, è possibile utilizzare più semplice hello *breve ora di scadenza* modello. Questo modello consente di ottenere hello stesso risultato a quella di un dispositivo connessione lo stato del Registro di sistema utilizzando il modello di heartbeat hello, pur essendo più efficiente. Se richiesta l'acknowledgement dei messaggi, IoT Hub può inviare notifiche relative ai quali dispositivi sono in grado di tooreceive messaggi e non.

## <a name="device-lifecycle-notifications"></a>Notifiche del ciclo di vita dei dispositivi

L'hub IoT può inviare una notifica alla soluzione IoT quando un'identità dispositivo viene creata o eliminata inviando notifiche del ciclo di vita dei dispositivi. toodo in tal caso, la soluzione IoT deve toocreate una route e tooset hello origine dati uguale troppo*DeviceLifecycleEvents*. Per impostazione predefinita, non vengono inviate notifiche del ciclo di vita, il che significa che queste route non sono preesistenti. messaggio di notifica Hello include proprietà e corpo.

Proprietà: Proprietà di sistema di messaggi sono precedute dal prefisso hello `'$'` simbolo.

| Nome | Valore |
| --- | --- |
$content-type | application/json |
$iothub-enqueuedtime |  Ora di invio notifica hello |
$iothub-message-source | deviceLifecycleEvents |
$content-encoding | utf-8 |
opType | **createDeviceIdentity** o **deleteDeviceIdentity** |
hubName | Nome dell'hub IoT |
deviceId | ID del dispositivo hello |
operationTimestamp | Timestamp ISO8601 dell'operazione |
iothub-message-schema | deviceLifecycleNotification |

Corpo: In questa sezione è in formato JSON e rappresenta un doppio hello di hello creato l'identità del dispositivo. Ad esempio,

```json
{
    "deviceId":"11576-ailn-test-0-67333793211",
    "etag":"AAAAAAAAAAE=",
    "properties": {
        "desired": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        },
        "reported": {
            "$metadata": {
                "$lastUpdated": "2016-02-30T16:24:48.789Z"
            },
            "$version": 1
        }
    }
}
```

## <a name="reference-topics"></a>Argomenti di riferimento:

Hello argomenti di riferimento seguenti offrono altre informazioni del Registro di sistema di hello identità.

## <a name="device-identity-properties"></a>Proprietà delle identità dei dispositivi

Le identità del dispositivo sono rappresentate come documenti JSON con hello le proprietà seguenti:

| Proprietà | Opzioni | Descrizione |
| --- | --- | --- |
| deviceId |Obbligatoria, di sola lettura negli aggiornamenti |Specifica una stringa (backup too128 caratteri) di caratteri alfanumerici ASCII a 7 bit + `{'-', ':', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| generationId |Obbligatoria, di sola lettura |IoT hub generato, con distinzione tra maiuscole e stringa di caratteri too128. Questo valore è toodistinguish utilizzato per i dispositivi con hello stesso **deviceId**, quando sono stati eliminati e ricreati. |
| etag |Obbligatoria, di sola lettura |Stringa che rappresenta un ETag debole per l'identità del dispositivo hello, in base [RFC7232][lnk-rfc7232]. |
| auth |Facoltativa |Oggetto composito contenente le informazioni di autenticazione e i materiali di sicurezza. |
| auth.symkey |Facoltativa |Oggetto composito contenente una chiave primaria e una chiave secondaria, archiviate in formato Base 64. |
| status |Obbligatoria |Indicatore di accesso. Può essere **Enabled** o **Disabled**. Se **abilitato**, dispositivo hello è consentito tooconnect. Se è **Disabled**, il dispositivo non potrà accedere ad alcun endpoint per il dispositivo. |
| statusReason |Facoltativa |Un carattere lungo di 128 stringa tale motivo hello archivi hello identità dello stato del dispositivo. Sono consentiti tutti i caratteri UTF-8. |
| statusUpdateTime |Sola lettura |Un indicatore temporale che mostra hello data e ora dell'ultimo aggiornamento dello stato di hello. |
| connectionState |Sola lettura |Campo indicante lo stato della connessione: **Connected** o **Disconnected**. Questo campo rappresenta hello visualizzazione dell'IoT Hub hello connessione dello stato dei dispositivi. **Importante**: è consigliabile usare questo campo solo per scopi di sviluppo e di debug. stato di connessione Hello viene aggiornato solo per i dispositivi con MQTT o AMQP. Si basa anche su ping a livello di protocollo (ping MQTT o AMQP) e può avere un ritardo massimo di soli 5 minuti. Per questi motivi possono essere presenti falsi positivi, ad esempio dispositivi segnalati come connessi, ma in realtà disconnessi. |
| connectionStateUpdatedTime |Sola lettura |Un indicatore temporale che mostra hello data e l'ultimo stato di connessione hello ora è stato aggiornato. |
| lastActivityTime |Sola lettura |Un indicatore temporale che mostra hello data e l'ultimo hello dispositivo connesso, ricevuto o inviato un messaggio. |

> [!NOTE]
> Stato di connessione può rappresentare solo hello visualizzazione dello stato di hello della connessione hello dell'IoT Hub. Stato toothis aggiornamenti potrebbe essere ritardato, a seconda delle configurazioni e le condizioni della rete.

## <a name="additional-reference-material"></a>Materiale di riferimento

Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* [Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* [Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello e la limitazione di comportamenti che si applicano toohello servizio IoT Hub.
* [Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* [Il linguaggio di query di IoT Hub] [ lnk-query] descrive il linguaggio di query hello è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.
* [Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi

A questo punto si è appreso come toouse hello Hub IoT identità Registro di sistema, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:

* [Controllo accesso tooIoT Hub][lnk-devguide-security]
* [Utilizzare lo stato del dispositivo gemelli toosynchronize e configurazioni][lnk-devguide-device-twins]
* [Richiamare un metodo diretto in un dispositivo][lnk-devguide-directmethods]
* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:

* [Introduzione all'hub IoT di Azure][lnk-getstarted-tutorial]

<!-- Links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-guidance-provisioning]: iot-hub-devguide-identity-registry.md#device-provisioning
[lnk-guidance-heartbeat]: iot-hub-devguide-identity-registry.md#device-heartbeat
[lnk-rfc7232]: https://tools.ietf.org/html/rfc7232
[lnk-bulk-identity]: iot-hub-bulk-identity-mgmt.md
[lnk-export]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities
[lnk-devguide-opmon]: iot-hub-operations-monitoring.md

[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
