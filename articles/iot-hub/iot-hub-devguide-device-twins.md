---
title: gemelli di dispositivi Azure IoT Hub aaaUnderstand | Documenti Microsoft
description: Guida per sviluppatori - dispositivo utilizzare gemelli toosynchronize stato e dati di configurazione tra l'IoT Hub e i dispositivi
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 8a3da072-a5bf-46e5-8de4-24cdbb2a03fa
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7dade18665108ed352ff3d18e864dc34f451bbf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-device-twins-in-iot-hub"></a>Comprendere e usare dispositivi gemelli nell'hub IoT
## <a name="overview"></a>Panoramica
I *dispositivi gemelli* sono documenti JSON nei quali vengono archiviate informazioni sullo stato dei dispositivi (metadati, configurazioni e condizioni). IoT Hub persiste doppi un dispositivo per ogni dispositivo che si connette tooIoT Hub. L'articolo illustra:

* struttura di un doppio dispositivo hello Hello: *tag*, *desiderato* e *segnalati proprietà*, e
* operazioni di Hello che App per dispositivi e back-end possono eseguire sui gemelli di dispositivo.

> [!NOTE]
> Attualmente, gemelli di dispositivo sono accessibili solo da dispositivi che si connettono tooIoT Hub utilizzando il protocollo MQTT hello. Fare riferimento toohello [supporto MQTT] [ lnk-devguide-mqtt] per istruzioni su come tooconvert esistente dispositivo app toouse MQTT.
> 
> 

### <a name="when-toouse"></a>Quando toouse
Usare i dispositivi gemelli per:

* Archiviare i metadati specifici del dispositivo nel cloud hello. Salve, ad esempio, il percorso di distribuzione di una macchina distributore.
* Segnalare informazioni sullo stato corrente, come funzionalità disponibili e condizioni dall'app per dispositivo. Ad esempio, un dispositivo è connesso tooyour IoT hub over cellulare o Wi-Fi.
* Sincronizzazione dello stato di hello dei flussi di lavoro a esecuzione prolungata tra app per dispositivi e app back-end. Ad esempio, quando esegue il backup di soluzione hello fine specifica hello nuovo tooinstall di versione del firmware e hello dispositivo app report hello varie fasi del processo di aggiornamento hello.
* Eseguire query sui metadati, la configurazione o lo stato dei dispositivi.

Fare riferimento troppo[materiale sussidiario per la comunicazione da dispositivo a cloud] [ lnk-d2c-guidance] per istruzioni sull'uso di proprietà restituita, i messaggi da dispositivo a cloud o caricamento del file.
Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] per istruzioni sull'uso delle proprietà desiderate, metodi diretti o messaggi da cloud a dispositivo.

## <a name="device-twins"></a>Dispositivi gemelli
I dispositivi gemelli consentono di archiviare informazioni sul dispositivo che possono essere usate:

* Dispositivo e back end è possibile utilizzare condizioni di dispositivo toosynchronize e configurazione.
* back-end di Hello soluzione possono utilizzare tooquery e operazioni a esecuzione prolungata di destinazione.

ciclo di vita di Hello di una coppia di dispositivo è collegato corrispondente toohello [identità del dispositivo][lnk-identity]. I dispositivi gemelli vengono creati ed eliminati implicitamente quando viene creata o eliminata una nuova identità del dispositivo nell'hub IoT.

Un dispositivo gemello è un documento JSON che include:

* **Tag**. Una sezione del documento JSON hello hello soluzione back-end può leggere e scrivere. Tag non sono visibili toodevice app.
* **Proprietà desiderate**. Usata con configurazione del dispositivo toosynchronize proprietà segnalato o condizioni. Le proprietà desiderate possono essere impostate solo dalla soluzione hello nuovamente finale e possono essere letto da app per dispositivi hello. Hello dispositivo app può anche ricevere notifiche in tempo reale delle modifiche nelle proprietà hello desiderato.
* **Proprietà segnalate**. Usata con configurazione del dispositivo toosynchronize proprietà desiderate o condizioni. Proprietà restituita può essere impostata solo per app per dispositivi hello e possano leggere e query hello soluzione back-end.

Radice hello hello dispositivo doppi JSON documento contiene inoltre le proprietà di sola lettura hello dall'identità periferica corrispondente hello archiviati in hello [Registro di sistema di identità][lnk-identity].

![][img-twin]

Hello di esempio seguente viene illustrato un documento JSON un doppio di dispositivo:

        {
            "deviceId": "devA",
            "generationId": "123",
            "status": "enabled",
            "statusReason": "provisioned",
            "connectionState": "connected",
            "connectionStateUpdatedTime": "2015-02-28T16:24:48.789Z",
            "lastActivityTime": "2015-02-30T16:24:48.789Z",

            "tags": {
                "$etag": "123",
                "deploymentLocation": {
                    "building": "43",
                    "floor": "1"
                }
            },
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata" : {...},
                    "$version": 1
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": 55,
                    "$metadata" : {...},
                    "$version": 4
                }
            }
        }

Nell'oggetto radice hello, è di proprietà di sistema hello e gli oggetti contenitore per `tags` e `reported` e `desired` proprietà. Hello `properties` contenitore contiene alcuni elementi di sola lettura (`$metadata`, `$etag`, e `$version`) descritto in hello [dispositivo doppi metadati] [ lnk-twin-metadata] e [ Concorrenza ottimistica] [ lnk-concurrency] sezioni.

### <a name="reported-property-example"></a>Esempio di proprietà segnalata
Nell'esempio precedente hello doppi dispositivo hello contiene un `batteryLevel` proprietà che viene segnalato da app per dispositivi hello. Questa proprietà rende possibili tooquery e operare sui dispositivi in base al livello di batteria segnalati ultimo hello. Altri esempi hello dispositivo app reporting funzionalità dei dispositivi o le opzioni di connettività.

> [!NOTE]
> Proprietà segnalate semplificare gli scenari in cui desidera back-end di hello soluzione hello noto ultimo valore di una proprietà. Utilizzare [messaggi da dispositivo a cloud] [ lnk-d2c] se hello soluzione back-end deve tooprocess telemetria del dispositivo nel modulo hello di sequenze di eventi impostati i timestamp, ad esempio serie temporale.

### <a name="desired-property-example"></a>Esempio di proprietà desiderata
Nell'esempio precedente hello hello `telemetryConfig` doppi dispositivo desiderato e le proprietà segnalate vengono utilizzate da hello soluzione back-end e configurazione del dispositivo app toosynchronize hello telemetria hello per questo dispositivo. ad esempio:

1. back-end di Hello soluzione hello desiderato impostata con il valore di configurazione di hello desiderato. Di seguito è parte di hello del documento hello con set di proprietà hello desiderato:
   
        ...
        "desired": {
            "telemetryConfig": {
                "sendFrequency": "5m"
            },
            ...
        },
        ...
2. app per dispositivi Hello riceve una notifica di modifica hello immediatamente se è connesso, o in hello riconnettersi. Hello dispositivo app quindi segnala hello aggiornata configurazione (o una condizione di errore utilizzando hello `status` proprietà). Di seguito è parte di hello hello segnalati proprietà:
   
        ...
        "reported": {
            "telemetryConfig": {
                "sendFrequency": "5m",
                "status": "success"
            }
            ...
        }
        ...
3. back-end di Hello soluzione possibile tenere traccia hello risultati dell'operazione di configurazione hello su più dispositivi, da [l'esecuzione di query] [ lnk-query] gemelli di dispositivo.

> [!NOTE]
> frammenti di codice precedente Hello sono riportati esempi, ottimizzata per migliorare la leggibilità, di un modo tooencode una configurazione del dispositivo e il relativo stato. IoT Hub non è previsto uno schema specifico per un doppio dispositivo hello desiderato e segnalati proprietà gemelli dispositivo hello.
> 
> 

È possibile utilizzare operazioni a esecuzione prolungata toosynchronize gemelli, ad esempio gli aggiornamenti del firmware. Per ulteriori informazioni su come toouse proprietà toosynchronize e tenere traccia di un'operazione a esecuzione prolungata su dispositivi, vedere [lo si desidera utilizzare i dispositivi di proprietà tooconfigure][lnk-twin-properties].

## <a name="back-end-operations"></a>Operazioni di back-end
back-end di Hello soluzione opera su un doppio dispositivo hello hello dopo operazioni atomiche, esposte tramite HTTP utilizzando:

1. **Recuperare un dispositivo gemello tramite ID**. Questa operazione restituisce hello doppi documento di periferica, inclusi i tag e lo si desidera, è stato segnalato e le proprietà di sistema.
2. **Aggiornare parzialmente il dispositivo gemello**. Questa operazione consente di tag di hello soluzione back-end toopartially aggiornamento hello o le proprietà desiderate in una coppia di dispositivo. aggiornamento parziale di Hello viene espresso come un documento JSON che aggiunge o aggiorna le proprietà. Le proprietà impostate troppo`null` vengono rimossi. Hello esempio seguente viene creata una nuova proprietà desiderata con valore `{"newProperty": "newValue"}`, sovrascrive hello valore esistente della `existingProperty` con `"otherNewValue"`e rimuove `otherOldProperty`. Altre modifiche non vengono apportate proprietà tooexisting desiderato o i tag:
   
        {
            "properties": {
                "desired": {
                    "newProperty": {
                        "nestedProperty": "newValue"
                    },
                    "existingProperty": "otherNewValue",
                    "otherOldProperty": null
                }
            }
        }
3. **Sostituzione di proprietà desiderate**. Questo toocompletely di back-end operazione attiva hello soluzione sovrascrivere tutte le proprietà desiderate esistenti e sostituire un nuovo documento JSON per `properties/desired`.
4. **Sostituzione di tag**. Questo toocompletely di back-end operazione attiva hello soluzione sovrascrivere tutti i tag esistenti e sostituire un nuovo documento JSON per `tags`.
5. **Ricezione di notifiche relative al dispositivo gemello**. Questa operazione consente hello soluzione back-end toobe una notifica quando viene modificato un doppio hello. toodo in tal caso, la soluzione IoT deve toocreate una route e tooset hello origine dati uguale troppo*twinChangeEvents*. Per impostazione predefinita, non viene inviata alcuna notifica, ovvero queste route non sono preesistenti. Se la frequenza hello di modifica è troppo elevata o per altri motivi, ad esempio gli errori interni, hello IoT Hub potrebbe inviare solo una notifica che contiene tutte le modifiche. Di conseguenza, se l'applicazione ha bisogno di controllo e registrazione affidabili di tutti gli stati intermedi, è consigliabile continuare a usare i messaggi D2C. messaggio di notifica doppi Hello include proprietà e corpo.

    - Proprietà

    | Nome | Valore |
    | --- | --- |
    $content-type | application/json |
    $iothub-enqueuedtime |  Ora di invio notifica hello |
    $iothub-message-source | twinChangeEvents |
    $content-encoding | utf-8 |
    deviceId | ID del dispositivo hello |
    hubName | Nome dell'hub IoT |
    operationTimestamp | Timestamp [ISO8601] dell'operazione |
    iothub-message-schema | deviceLifecycleNotification |
    opType | "replaceTwin" o "updateTwin" |

    Proprietà di sistema di messaggi sono precedute da hello `'$'` simbolo.

    - Corpo
        
    In questa sezione include tutte le modifiche di un doppio hello in formato JSON. Usa hello stesso formato come una patch, con la differenza hello che può contenere tutte le sezioni di un doppio: tag, properties.reported, properties.desired e che contenga elementi hello "$metadata". Ad esempio,
    ```
    {
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

Tutti hello precedente il supporto di operazioni [la concorrenza ottimistica] [ lnk-concurrency] e richiedono hello **ServiceConnect** autorizzazione, come definito in hello [sicurezza ] [ lnk-security] articolo.

Operazioni toothese, soluzione hello inoltre eseguire il backup finale può:

* Eseguire una query utilizzando hello gemelli di hello dispositivo simile a SQL [il linguaggio di query di IoT Hub][lnk-query].
* Eseguire operazioni su set di grandi dimensioni dei dispositivi gemelli usando i [processi][lnk-jobs].

## <a name="device-operations"></a>Operazioni del dispositivo
app per dispositivi Hello opera su un doppio dispositivo hello hello dopo operazioni atomiche utilizzando:

1. **Recuperare un dispositivo gemello**. Questa operazione restituisce documento gemelli di hello dispositivo (inclusi i tag e lo si desidera, segnalati e le proprietà di sistema) per hello è attualmente connesso dispositivo.
2. **Aggiornamento parziale delle proprietà segnalate**. Questo consente di operazione hello aggiornamento parziale di hello segnalate le proprietà del dispositivo di hello attualmente connesso. Questo hello utilizza operazione aggiornare JSON stesso formato che hello soluzione back-end viene utilizzato per un aggiornamento parziale di proprietà desiderato.
3. **Osservazione di proprietà desiderate**. dispositivo attualmente connesso Hello possibile toobe una notifica di proprietà desiderato toohello aggiornamenti quando si verificano. Hello riceve hello stessa forma di aggiornamento (sostituzione parziale o completa) eseguito da hello soluzione back-end.

Tutte le operazioni precedenti di hello richiedono hello **DeviceConnect** autorizzazione, come definito in hello [sicurezza] [ lnk-security] articolo.

Hello [dispositivo IoT di Azure SDK] [ lnk-sdks] renderlo hello toouse semplice che precede le operazioni da numerosi linguaggi e piattaforme. Ulteriori informazioni sui dettagli di hello di primitive di IoT Hub per la sincronizzazione di proprietà desiderato sono reperibile [flusso riconnessione dispositivo][lnk-reconnection].

> [!NOTE]
> Attualmente, gemelli di dispositivo sono accessibili solo da dispositivi che si connettono tooIoT Hub utilizzando il protocollo MQTT hello.
> 
> 

## <a name="reference-topics"></a>Argomenti di riferimento:
Hello argomenti di riferimento seguenti offrono ulteriori informazioni su controllo hub IoT tooyour di accesso.

## <a name="tags-and-properties-format"></a>Formato di tag e proprietà
I tag, le proprietà desiderate e verrà segnalate sono oggetti JSON con hello seguenti restrizioni:

* Tutte le chiavi negli oggetti JSON sono stringhe UTF-8 UNICODE da 64 caratteri con distinzione tra maiuscole e minuscole. I caratteri consentiti escludono i caratteri di controllo UNICODE (segmenti C0 e C1) e `'.'`, `' '`, `'$'`.
* Tutti i valori negli oggetti JSON possono essere dei seguenti tipi di JSON hello: valore booleano, numero, stringa, oggetto. Non sono consentite le matrici.
* Tutti gli oggetti JSON nei tag e nelle proprietà desiderate e segnalate possono avere una profondità massima di 5. Ad esempio, hello segue l'oggetto è valido:

        {
            ...
            "tags": {
                "one": {
                    "two": {
                        "three": {
                            "four": {
                                "five": {
                                    "property": "value"
                                }
                            }
                        }
                    }
                }
            },
            ...
        }

* Tutti i valori di stringa possono avere una lunghezza massima di 512 byte.

## <a name="device-twin-size"></a>Dimensioni del dispositivo gemello
IoT Hub impone un limite di dimensioni di 8KB valori hello di `tags`, `properties/desired`, e `properties/reported`, esclusione di elementi di sola lettura.
Hello dimensioni vengono calcolate contando tutti i caratteri UNICODE escludendo controllano caratteri (segmenti C0 e C1) e lo spazio `' '` quando viene visualizzato di fuori di una costante di stringa.
Rifiuta l'IoT Hub con un errore di tutte le operazioni che verrebbero aumenta hello tali documenti supera il limite di hello.

## <a name="device-twin-metadata"></a>Metadati del dispositivo gemello
IoT Hub conserva hello timestamp dell'ultimo aggiornamento di hello per ogni oggetto JSON in un doppio dispositivo desiderato e segnalati proprietà. Hello timestamp sono espressi in UTC e codificato nella hello [ISO8601] formato `YYYY-MM-DDTHH:MM:SS.mmmZ`.
ad esempio:

        {
            ...
            "properties": {
                "desired": {
                    "telemetryConfig": {
                        "sendFrequency": "5m"
                    },
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": {
                                "$lastUpdated": "2016-03-30T16:24:48.789Z"
                            },
                            "$lastUpdated": "2016-03-30T16:24:48.789Z"
                        },
                        "$lastUpdated": "2016-03-30T16:24:48.789Z"
                    },
                    "$version": 23
                },
                "reported": {
                    "telemetryConfig": {
                        "sendFrequency": "5m",
                        "status": "success"
                    }
                    "batteryLevel": "55%",
                    "$metadata": {
                        "telemetryConfig": {
                            "sendFrequency": "5m",
                            "status": {
                                "$lastUpdated": "2016-03-31T16:35:48.789Z"
                            },
                            "$lastUpdated": "2016-03-31T16:35:48.789Z"
                        }
                        "batteryLevel": {
                            "$lastUpdated": "2016-04-01T16:35:48.789Z"
                        },
                        "$lastUpdated": "2016-04-01T16:24:48.789Z"
                    },
                    "$version": 123
                }
            }
            ...
        }

Queste informazioni vengono conservate in ogni livello degli aggiornamenti toopreserve (foglie hello non solo di hello struttura JSON) per la rimozione di chiavi dell'oggetto.

## <a name="optimistic-concurrency"></a>Concorrenza ottimistica
I tag e le proprietà desiderate e segnalate supportano la concorrenza ottimistica.
Tag presentano un valore ETag, come per [RFC7232], che rappresenta una rappresentazione JSON del tag hello. È possibile utilizzare valori eTag nelle operazioni di aggiornamento condizionale da coerenza tooensure di hello soluzione back-end.

Doppi dispositivo desiderato e le proprietà dei report non dispone di eTag, ma hanno un `$version` valore di cui è garantita toobe incrementale. Analogamente tooan ETag, versione di hello possono essere usati da hello aggiornamento coerenza tooenforce parti degli aggiornamenti. Ad esempio, un'app di dispositivo per un segnalati proprietà o hello soluzione back-end per una proprietà desiderata.

Le versioni sono utili anche quando un agente di osservazione (ad esempio di app per dispositivi hello osservando le proprietà di hello desiderato) devono essere riconciliate race condition che tra il risultato di hello di un'operazione di recupero e di una notifica di aggiornamento. Hello sezione [flusso riconnessione dispositivo] [ lnk-reconnection] vengono fornite ulteriori informazioni.

## <a name="device-reconnection-flow"></a>Flusso di riconnessione del dispositivo
L'hub IoT non conserva le notifiche di aggiornamento delle proprietà desiderate dei dispositivi connessi. Ne consegue che un dispositivo che esegue la connessione deve recuperare documento completo di proprietà desiderato hello, in aggiunta toosubscribing per le notifiche di aggiornamento. Dato il possibilità hello di race condition che tra le notifiche di aggiornamento e il recupero completo, è necessario garantire hello seguendo flusso:

1. App del dispositivo si connette tooan IoT hub.
2. L'app per dispositivo esegue la sottoscrizione per le notifiche di aggiornamento delle proprietà desiderate.
3. App del dispositivo recupera documento completo di hello per le proprietà desiderate.

app per dispositivi Hello è possibile ignorare tutte le notifiche con `$version` minore o uguale alla versione di hello del documento recuperato completo hello. Questo approccio è possibile poiché l'hub IoT garantisce l'incremento delle versioni.

> [!NOTE]
> Questa logica è già implementata in hello [dispositivo IoT di Azure SDK][lnk-sdks]. Questa descrizione è utile solo se l'app del dispositivo hello non è possibile utilizzare uno dei dispositivi IoT di Azure SDK e devono essere programmati interfaccia MQTT hello direttamente.
> 
> 

## <a name="additional-reference-material"></a>Materiale di riferimento
Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* Hello [gli endpoint IoT Hub] [ lnk-endpoints] hello descritti vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* Hello [la limitazione delle richieste e le quote] [ lnk-quotas] articolo descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.
* Hello [Azure IoT dispositivo e il servizio SDK] [ lnk-sdks] articolo elenchi hello vari language SDK, è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* Hello [linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] articolo viene descritto il linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi di hello .
* Hello [supporto IoT Hub MQTT] [ lnk-devguide-mqtt] vengono fornite ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi
Ora è imparato gemelli di dispositivo, potrebbero essere interessati hello seguenti argomenti della Guida per sviluppatori IoT Hub:

* [Richiamare un metodo diretto in un dispositivo][lnk-methods]
* [Pianificare processi in più dispositivi][lnk-jobs]

Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello seguenti esercitazioni IoT Hub:

* [Come toouse hello gemelli di dispositivo][lnk-twin-tutorial]
* [Come dispositivo toouse doppio proprietà][lnk-twin-properties]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-identity]: iot-hub-devguide-identity-registry.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-security]: iot-hub-devguide-security.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[ISO8601]: https://en.wikipedia.org/wiki/ISO_8601
[RFC7232]: https://tools.ietf.org/html/rfc7232
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-twin-metadata]: iot-hub-devguide-device-twins.md#device-twin-metadata
[lnk-concurrency]: iot-hub-devguide-device-twins.md#optimistic-concurrency
[lnk-reconnection]: iot-hub-devguide-device-twins.md#device-reconnection-flow

[img-twin]: media/iot-hub-devguide-device-twins/twin.png
