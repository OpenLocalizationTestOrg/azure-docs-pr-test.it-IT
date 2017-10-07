---
title: supporto di Azure IoT Hub MQTT aaaUnderstand | Documenti Microsoft
description: Sviluppatore Guida - supporto per i dispositivi si connettono a endpoint che utilizzano il dispositivo di IoT Hub utilizzando tooan hello protocollo MQTT. Include informazioni sul supporto MQTT integrato in hello Azure IoT dispositivo SDK.
services: iot-hub
documentationcenter: .net
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 1d71c27c-b466-4a40-b95b-d6550cf85144
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e461687963138987acdf1f4e0e34c453744ea191
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="communicate-with-your-iot-hub-using-hello-mqtt-protocol"></a>Comunicare con l'hub IoT protocollo MQTT hello

IoT Hub consente toocommunicate dispositivi con hello Hub IoT dispositivo endpoint che utilizzano hello [MQTT v3.1.1] [ lnk-mqtt-org] protocollo sulla porta 8883 o v3.1.1 MQTT attraverso il protocollo WebSocket sulla porta 443. IoT Hub richiede tutti toobe di comunicazione dispositivo protetta tramite TLS/SSL (di conseguenza, IoT Hub non supporta le connessioni non sicure attraverso la porta 1883).

## <a name="connecting-tooiot-hub"></a>Connessione tooIoT Hub

Un dispositivo può usare hub IoT di hello MQTT protocollo tooconnect tooan tramite l'utilizzo delle librerie di hello in hello [Azure IoT SDK] [ lnk-device-sdks] o utilizzando il protocollo MQTT hello direttamente.

## <a name="using-hello-device-sdks"></a>Utilizzo di hello dispositivo SDK

[Dispositivo SDK] [ lnk-device-sdks] tale hello supporto protocollo MQTT sono disponibili per Java, Node.js, C, c# e Python. uso del dispositivo di Hello SDK hello standard IoT Hub connessione stringa tooestablish un hub IoT tooan di connessione. protocollo MQTT toouse hello, hello client protocollo parametro deve essere impostato troppo**MQTT**. Per impostazione predefinita, il dispositivo di hello SDK connettersi tooan IoT Hub con hello **CleanSession** flag impostato troppo**0** e utilizzare **1 QoS** per scambio di messaggi con l'hub IoT hello.

Quando un dispositivo è connesso tooan hub IoT, dispositivo hello SDK forniscono metodi che consentono di messaggi di toosend dispositivo hello tooand ricevere messaggi da un hub IoT.

Hello nella tabella seguente sono contenuti collegamenti toocode esempi per ogni lingua supportata e specifica hello parametro toouse tooestablish tooIoT una connessione Hub utilizzando il protocollo MQTT hello.

| Lingua | Parametro del protocollo |
| --- | --- |
| [Node.js][lnk-sample-node] |azure-iot-device-mqtt |
| [Java][lnk-sample-java] |IotHubClientProtocol.MQTT |
| [C][lnk-sample-c] |MQTT_Protocol |
| [C#][lnk-sample-csharp] |TransportType.Mqtt |
| [Python][lnk-sample-python] |IoTHubTransportProvider.MQTT |

### <a name="migrating-a-device-app-from-amqp-toomqtt"></a>Migrazione di un'app di dispositivo da tooMQTT AMQP

Se si utilizza hello [dispositivo SDK][lnk-device-sdks], il passaggio da Usa AMQP tooMQTT, è necessario modificare il parametro di protocollo hello nell'inizializzazione del client hello come indicato in precedenza.

In tal caso, verificare che hello toocheck seguenti elementi:

* AMQP restituisce gli errori per diverse condizioni, mentre MQTT termina la connessione hello. Di conseguenza, la logica di gestione delle eccezioni potrebbe richiedere alcune modifiche.
* Non supporta hello MQTT *rifiutare* operazioni durante la ricezione [messaggi da cloud a dispositivo][lnk-messaging]. Se l'app back-end deve tooreceive una risposta da app per dispositivi hello, è consigliabile utilizzare [diretta metodi][lnk-methods].

## <a name="using-hello-mqtt-protocol-directly"></a>Protocollo hello MQTT direttamente
Se un dispositivo non è possibile usare il dispositivo di hello SDK, è possibile connettersi ancora gli endpoint pubblici dispositivo toohello protocollo MQTT hello sulla porta 8883. In hello **CONNETTI** dispositivo hello pacchetto deve utilizzare hello seguenti valori:

* Per hello **ClientId** campo, utilizzare hello **deviceId**.
* Per hello **Username** campo, utilizzare `{iothubhostname}/{device_id}/api-version=2016-11-14`, dove {iothubhostname} è hello CName completo dell'hub IoT hello.

    Ad esempio, se hello nome dell'hub IoT è **contoso.azure devices.net** e nome hello del dispositivo è **MyDevice01**, hello completo **Username** campo deve contenere `contoso.azure-devices.net/MyDevice01/api-version=2016-11-14`.
* Per hello **Password** campo, utilizzare un token di firma di accesso condiviso. formato Hello del token di firma di accesso condiviso è hello hello stesso per entrambi hello HTTP e protocolli AMQP:<br/>`SharedAccessSignature sig={signature-string}&se={expiry}&sr={URL-encoded-resourceURI}`.

    Per ulteriori informazioni su come toogenerate i token di firma di accesso condiviso, vedere la sezione di dispositivo di hello della [i token di sicurezza tramite l'IoT Hub][lnk-sas-tokens].

    Durante il test, è inoltre possibile utilizzare hello [Esplora dispositivo] [ lnk-device-explorer] tooquickly strumento generare un token di firma di accesso condiviso che è possibile copiare e incollare nel codice:

  1. Passare toohello **Management** scheda **Esplora dispositivo**.
  2. Fare clic su **SAS Token** in alto a destra.
  3. In **SASTokenForm**, selezionare il dispositivo in hello **DeviceID** elenco a discesa. Impostare il valore **TTL**.
  4. Fare clic su **genera** toocreate il token.

     token di firma di accesso condiviso generata Hello ha questa struttura: `HostName={your hub name}.azure-devices.net;DeviceId=javadevice;SharedAccessSignature=SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

     parte di questo token toouse come hello Hello **Password** è tooconnect campo utilizzando MQTT: `SharedAccessSignature sr={your hub name}.azure-devices.net%2Fdevices%2FMyDevice01%2Fapi-version%3D2016-11-14&sig=vSgHBMUG.....Ntg%3d&se=1456481802`.

Per MQTT connettere e disconnettere i pacchetti, IoT Hub genera un evento su hello **operazioni di monitoraggio** canale con informazioni aggiuntive che consentono di problemi di connettività tootroubleshoot.

### <a name="sending-device-to-cloud-messages"></a>Invio di messaggi da dispositivo a cloud

Dopo aver apportato una connessione ha esito positivo, un dispositivo può inviare messaggi tooIoT Hub utilizzando `devices/{device_id}/messages/events/` o `devices/{device_id}/messages/events/{property_bag}` come un **il nome dell'argomento**. Hello `{property_bag}` elemento consente i messaggi di hello dispositivo toosend con proprietà aggiuntive in un formato con codifica url. ad esempio:

```
RFC 2396-encoded(<PropertyName1>)=RFC 2396-encoded(<PropertyValue1>)&RFC 2396-encoded(<PropertyName2>)=RFC 2396-encoded(<PropertyValue2>)…
```

> [!NOTE]
> Questo `{property_bag}` elemento Usa hello stessa codifica per le stringhe di query nel protocollo hello HTTP.
>
>

app per dispositivi Hello inoltre è possibile utilizzare `devices/{device_id}/messages/events/{property_bag}` come hello **il nome dell'argomento verrà** toodefine *i messaggi di* toobe inoltrati come un messaggio di dati di telemetria.

- L'hub IoT non supporta i messaggi di QoS 2. Se un'app dispositivo pubblica un messaggio con **QoS 2**, IoT Hub chiude la connessione di rete hello.
- L'hub IoT non rende persistenti i messaggi di mantenimento. Se un dispositivo invia un messaggio con hello **MANTIENI** too1 impostato, l'IoT Hub aggiunge hello **x-opt-conserva** messaggio toohello di proprietà dell'applicazione. In questo caso, anziché salvare in modo permanente hello mantenere messaggio, l'IoT Hub passa toohello back-end app.
- L'hub IoT supporta solo una connessione MQTT attiva per ogni dispositivo. Qualsiasi nuova connessione MQTT per conto di hello lo stesso ID dispositivo provoca l'IoT Hub toodrop hello esistente.

Per altre informazioni, vedere [Guida per gli sviluppatori sulla messaggistica][lnk-messaging].

### <a name="receiving-cloud-to-device-messages"></a>Ricezione di messaggi da cloud a dispositivo

i messaggi tooreceive dall'IoT Hub, un dispositivo deve eseguire la sottoscrizione con `devices/{device_id}/messages/devicebound/#` come un **filtro argomento**. carattere jolly a più livelli di Hello  **#**  in hello argomento filtro viene utilizzato solo tooallow hello proprietà aggiuntive del dispositivo tooreceive nel nome di argomento hello. IoT Hub non consente l'utilizzo di hello di hello  **#**  o **?** per il filtro di argomenti secondari. Poiché l'IoT Hub non è un broker di messaggistica di pubblicazione-sottoscrizione generale, supporta solo nomi di argomento hello documentato e filtri di argomento.

Hello dispositivo non ricevere messaggi dall'IoT Hub, fino a quando non completata che ha sottoscritto endpoint specifico del dispositivo tooits, rappresentato da hello `devices/{device_id}/messages/devicebound/#` filtro argomento. Dopo aver stabilito sottoscrizione ha esito positivo, il dispositivo di hello avvia la ricezione dei messaggi solo cloud a dispositivo che sono stati inviati tooit volta hello di sottoscrizione hello. Se si connette il dispositivo hello con **CleanSession** flag impostato troppo**0**, sottoscrizione hello viene mantenuto tra sessioni diverse. In questo caso, hello alla successiva connessione con **CleanSession 0** dispositivo hello riceve messaggi in sospeso che sono stati inviati tooit mentre è stato disconnesso. Se il dispositivo hello Usa **CleanSession** flag impostato troppo**1** , tuttavia, non riceve i messaggi dall'IoT Hub fino a quando non sottoscrive tooits dispositivo endpoint.

IoT Hub recapita i messaggi con hello **il nome dell'argomento** `devices/{device_id}/messages/devicebound/`, o `devices/{device_id}/messages/devicebound/{property_bag}` se sono presenti eventuali proprietà di messaggio. `{property_bag}` contiene coppie chiave/valore con codifica URL di proprietà dei messaggi. Solo le proprietà dell'applicazione e le proprietà di sistema definibile dall'utente (ad esempio **messageId** o **correlationId**) sono inclusi nel contenitore delle proprietà di hello. I nomi di proprietà di sistema hanno prefisso hello  **$** , le proprietà dell'applicazione utilizzano hello nome della proprietà originale senza il prefisso.

Quando un'app dispositivo sottoscrive argomento tooa con **QoS 2**, IoT Hub concede massima QoS livello 1 in hello **SUBACK** pacchetto. Successivamente, l'IoT Hub recapita dispositivo toohello messaggi con QoS 1.

### <a name="retrieving-a-device-twins-properties"></a>Recupero delle proprietà dei dispositivi gemelli

Innanzitutto, un dispositivo sottoscrive troppo`$iothub/twin/res/#`, le risposte dell'operazione di tooreceive hello. Quindi, invia un messaggio vuoto di tootopic `$iothub/twin/GET/?$rid={request id}`, con un valore popolato per **id richiesta**. servizio hello invia un messaggio di risposta contenente i dati di un doppio dispositivo hello in argomento `$iothub/twin/res/{status}/?$rid={request id}`, utilizzando hello stesso  **id richiesta** come richiesta hello.

L'ID richiesta può essere qualsiasi valore valido per la proprietà di un messaggio, come descritto nella [Guida per gli sviluppatori sulla messaggistica dell'hub IoT][lnk-messaging], e lo stato viene convalidato come valore intero.
corpo della risposta Hello contiene sezione proprietà hello doppi dispositivo hello:

corpo Hello della voce del Registro di sistema di identità hello limitata membro "proprietà" toohello, ad esempio:

        {
            "properties": {
                "desired": {
                    "telemetrySendFrequency": "5m",
                    "$version": 12
                },
                "reported": {
                    "telemetrySendFrequency": "5m",
                    "batteryLevel": 55,
                    "$version": 123
                }
            }
        }

Hello codici di stato possibili sono:

|Stato | Descrizione |
| ----- | ----------- |
| 200 | Success |
| 429 | Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas] |
| 5** | Errori server |

Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].

### <a name="update-device-twins-reported-properties"></a>Aggiornare le proprietà segnalate di un dispositivo gemello

Hello sequenza seguente descrive la modalità di aggiornamento hello in un dispositivo di proprietà in un doppio dispositivo hello nell'IoT Hub segnalato:

1. Un dispositivo deve prima sottoscrizione toohello `$iothub/twin/res/#` le risposte dell'operazione di argomento tooreceive hello dall'IoT Hub.

1. Un dispositivo invia un messaggio che contiene hello dispositivo un doppio update toohello `$iothub/twin/PATCH/properties/reported/?$rid={request id}` argomento. Questo messaggio include un valore **request id**.

1. Hello servizio, quindi invia un messaggio di risposta contenente hello nuovo valore ETag per la raccolta di proprietà riportato su un argomento di hello `$iothub/twin/res/{status}/?$rid={request id}`. Questo messaggio di risposta utilizza hello stesso **id richiesta** come richiesta hello.

corpo del messaggio Hello richiesta contiene un documento JSON, che fornisce nuovi valori per le proprietà segnalate (nessuna altra proprietà o metadati possono essere modificato).
Ogni membro nel documento JSON hello aggiorna o aggiunta un membro corrispondente hello documento del hello dispositivo disponibilità di una copia. Un membro è stato impostato troppo`null`, eliminazioni hello hello contenente l'oggetto membro. ad esempio:

        {
            "telemetrySendFrequency": "35m",
            "batteryLevel": 60
        }

Hello codici di stato possibili sono:

|Stato | Descrizione |
| ----- | ----------- |
| 200 | Success |
| 400 | Richiesta non valida. JSON non valido |
| 429 | Numero eccessivo di richieste (limitazione), come descritto in [Limitazione dell'hub IoT][lnk-quotas] |
| 5** | Errori server |

Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].

### <a name="receiving-desired-properties-update-notifications"></a>Ricezione delle notifiche di aggiornamento delle proprietà desiderate

Quando è connesso un dispositivo, l'IoT Hub invia argomento toohello notifiche `$iothub/twin/PATCH/properties/desired/?$version={new version}`, che includono il contenuto di hello di hello aggiornamento eseguita dal back-end di hello soluzione. ad esempio:

        {
            "telemetrySendFrequency": "5m",
            "route": null
        }

Come per gli aggiornamenti delle proprietà, `null` indica i valori che hello JSON dell'oggetto membro eliminato.


> [!IMPORTANT] 
> L'hub IoT genera notifiche di modifica solo quando i dispositivi sono connessi. Verificare che hello tooimplement [flusso riconnessione dispositivo] [ lnk-devguide-twin-reconnection] tookeep hello desiderato la sincronizzazione tra l'IoT Hub e hello app per dispositivi di proprietà.

Per altre informazioni, vedere la [Guida per gli sviluppatori sui dispositivi gemelli][lnk-devguide-twin].

### <a name="respond-tooa-direct-method"></a>Rispondere tooa dirette del metodo

Innanzitutto, un dispositivo ha toosubscribe troppo`$iothub/methods/POST/#`. IoT Hub invia l'argomento del metodo richieste toohello `$iothub/methods/POST/{method name}/?$rid={request id}`, con un corpo vuoto o un JSON valido.

toorespond, dispositivo hello invia un messaggio con un JSON valido o di un corpo vuoto toohello argomento `$iothub/methods/res/{status}/?$rid={request id}`, dove **id richiesta** è toomatch hello uno nel messaggio di richiesta, hello e **stato** ha toobe un numero intero .

Per altre informazioni, vedere la [Guida per gli sviluppatori sui metodi diretti][lnk-methods].

### <a name="additional-considerations"></a>Considerazioni aggiuntive

In considerazione finale, se è necessario comportamento del protocollo MQTT hello toocustomize sul lato cloud hello, è necessario rivedere hello [gateway del protocollo Azure IoT] [ lnk-azure-protocol-gateway] che consente ad alte prestazioni toodeploy gateway di protocollo personalizzato che interagisce direttamente con l'IoT Hub. gateway del protocollo Hello Azure IoT consente di toocustomize hello dispositivo protocollo tooaccommodate brownfield MQTT le distribuzioni o altri protocolli personalizzati. Questo approccio richiede tuttavia l'esecuzione e la gestione di un gateway di protocollo personalizzato.

## <a name="next-steps"></a>Passaggi successivi

toolearn ulteriori informazioni su protocollo MQTT hello, vedere hello [documentazione MQTT][lnk-mqtt-docs].

toolearn ulteriori informazioni sulla pianificazione della distribuzione di IoT Hub, vedere:

* [Catalogo dei dispositivi Azure Certified per IoT][lnk-devices]
* [Supportare protocolli aggiuntivi][lnk-protocols]
* [Eseguire il confronto con Hub eventi][lnk-compare]
* [Scalabilità, disponibilità elevata e ripristino di emergenza][lnk-scaling]

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Guida per gli sviluppatori dell'hub IoT][lnk-devguide]
* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-mqtt-org]: http://mqtt.org/
[lnk-mqtt-docs]: http://mqtt.org/documentation
[lnk-sample-node]: https://github.com/Azure/azure-iot-sdk-node/blob/master/device/samples/simple_sample_device.js
[lnk-sample-java]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device/samples/send-receive-sample/src/main/java/samples/com/microsoft/azure/iothub/SendReceive.java
[lnk-sample-c]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_client/samples/iothub_client_sample_mqtt
[lnk-sample-csharp]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device/samples
[lnk-sample-python]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device/samples
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-sas-tokens]: iot-hub-devguide-security.md#use-sas-tokens-in-a-device-app
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-devices]: https://catalog.azureiotsuite.com/
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md

[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-messaging]: iot-hub-devguide-messaging.md

[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-twin-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow
[lnk-devguide-twin]: iot-hub-devguide-device-twins.md
