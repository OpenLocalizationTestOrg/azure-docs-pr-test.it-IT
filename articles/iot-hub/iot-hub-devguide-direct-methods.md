---
title: metodi di indirizzare aaaUnderstand IoT Hub di Azure | Documenti Microsoft
description: Guida per sviluppatori - utilizzare metodi diretti tooinvoke codice nei dispositivi da un'applicazione di servizio.
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a>Comprendere e richiamare metodi diretti dall'hub IoT
## <a name="overview"></a>Panoramica
IoT Hub offre metodi diretti di possibilità tooinvoke sui dispositivi dal cloud hello. Metodi diretti rappresentano un'interazione richiesta-risposta con un tooan simili dispositivi HTTP chiamare in quanto essi esito positivo o negativo (dopo un timeout specificato dall'utente). Ciò è utile per scenari in cui il corso hello di un'azione immediata è diverso a seconda se il dispositivo hello è stato in grado di toorespond, ad esempio l'invio di un dispositivo di riattivazione tooa SMS se un dispositivo è offline (SMS molto più costoso rispetto a una chiamata al metodo).

Ogni metodo del dispositivo è destinato a un unico dispositivo. [I processi] [ lnk-devguide-jobs] forniscono un modo tooinvoke metodi diretti su più dispositivi e pianificare la chiamata di metodo per i dispositivi disconnessi.

Chiunque abbia autorizzazioni di **connessione servizio** per l'hub IoT può richiamare un metodo in un dispositivo.

### <a name="when-toouse"></a>Quando toouse
Metodi diretti seguono un modello di richiesta-risposta e disponibili solo per le comunicazioni che richiedono la conferma immediata dei relativi risultati, in genere interattivo il controllo di hello dispositivo, ad esempio tooturn su una ventola.

Fare riferimento troppo[indicazioni di comunicazione Cloud a dispositivo] [ lnk-c2d-guidance] in caso di dubbio tra l'utilizzo di proprietà desiderate, indirizzare i metodi o i messaggi da cloud a dispositivo.

## <a name="method-lifecycle"></a>Ciclo di vita dei metodi
Metodi diretti sono implementati nel dispositivo hello e possono richiedere zero o più input in hello metodo payload toocorrectly creare un'istanza. Per richiamare un metodo diretto è possibile usare un URI per il servizio (`{iot hub}/twins/{device id}/methods/`). Il dispositivo riceve i metodi diretti tramite un argomento MQTT specifico del dispositivo (`$iothub/methods/POST/{method name}/`). Si potrebbe supporta i metodi diretti su protocolli di rete sul lato dispositivo aggiuntivi in hello future.

> [!NOTE]
> Quando si richiama un metodo diretto in un dispositivo, i valori e nomi di proprietà possono contenere solo US-ASCII stampabili caratteri alfanumerici, ad eccezione di quelli hello seguente insieme: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.
> 
> 

Indirizzare i metodi sono sincroni e l'esito positivo o esito negativo dopo il periodo di timeout di hello (impostazione predefinita: 30 secondi, impostabile backup too3600 secondi). Metodi diretti sono utili negli scenari interattivi in cui si desidera tooact un dispositivo solo se il dispositivo di hello è online e riceventi comandi, ad esempio l'attivazione chiaro da un telefono. In questi scenari, si desidera toosee un immediato esito positivo o negativo in modo servizio cloud hello può agire sul risultato di hello appena possibile. dispositivo Hello può restituire un corpo del messaggio in seguito a metodo hello, ma non è necessario per toodo metodo hello in modo. Nelle chiamate ai metodi non esiste alcuna garanzia di ordinamento o semantica di concorrenza.

Metodo diretto sono solo per HTTP dal lato cloud hello e MQTT solo dal lato dispositivo hello.

il payload per il metodo richieste e risposte Hello è un documento JSON backup too8KB.

## <a name="reference-topics"></a>Argomenti di riferimento:
Hello argomenti di riferimento seguenti offrono ulteriori informazioni sull'utilizzo di metodi diretti.

## <a name="invoke-a-direct-method-from-a-back-end-app"></a>Richiamare un metodo diretto da un'app back-end
### <a name="method-invocation"></a>Chiamata al metodo
Le chiamate a metodi diretti in un dispositivo sono chiamate HTTP e includono:

* Hello *URI* toohello specifico dispositivo (`{iot hub}/twins/{device id}/methods/`)
* Hello POST *(metodo)*
* *Intestazioni* , che contengono hello authorization, richiedere l'ID, tipo di contenuto e la codifica del contenuto
* JSON trasparente *corpo* in hello seguente formato:

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

Il timeout è espresso in secondi. Se non è stato impostato alcun timeout, il valore predefinito too30 secondi.

### <a name="response"></a>Response
applicazione di back-end Hello riceve una risposta che comprende:

* *Codice di stato HTTP*, che viene utilizzata per errori provenienti da hello IoT Hub, tra cui un errore 404 per i dispositivi non è attualmente connesso
* *Intestazioni* , che contengono hello ETag, richiedere l'ID, tipo di contenuto e la codifica del contenuto
* Un formato JSON *corpo* in hello seguente formato:

```
{
    "status" : 201,
    "payload" : {...}
}
```

   Entrambi `status` e `body` sono forniti dal dispositivo hello e usate toorespond con codice di stato del dispositivo hello e/o descrizione.

## <a name="handle-a-direct-method-on-a-device"></a>Gestire un metodo diretto in un dispositivo
### <a name="method-invocation"></a>Chiamata al metodo
I dispositivi ricevono richieste dirette del metodo su un argomento MQTT hello:`$iothub/methods/POST/{method name}/?$rid={request id}`

corpo Hello quale dispositivo hello riceve si hello seguente formato:

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

Le richieste di metodo sono QoS 0.

### <a name="response"></a>Response
dispositivo Hello invia risposte troppo`$iothub/methods/res/{status}/?$rid={request id}`, dove:

* Hello `status` proprietà è stato fornito dal dispositivo hello di esecuzione del metodo.
* Hello `$rid` proprietà è l'ID richiesta hello dalla chiamata al metodo hello ricevuta dall'IoT Hub.

corpo Hello viene impostato dal dispositivo hello e può essere qualsiasi stato.

## <a name="additional-reference-material"></a>Materiale di riferimento
Altri argomenti di riferimento nella Guida per sviluppatori di IoT Hub hello includono:

* [Gli endpoint IoT Hub] [ lnk-endpoints] descrive hello vari endpoint che espone ogni hub IoT per le operazioni in fase di esecuzione e gestione.
* [Limitazione delle richieste e le quote] [ lnk-quotas] descrive le quote di hello che si applicano toohello servizio IoT Hub e hello limitazione tooexpect comportamento quando si utilizza servizio hello.
* [Gli SDK di dispositivi e servizi di Azure IoT] [ lnk-sdks] elenchi hello language vari SDK è possibile utilizzare quando si sviluppano applicazioni di servizio sia sul dispositivo che interagiscono con l'IoT Hub.
* [Il linguaggio di query IoT Hub per gemelli di dispositivo, processi e il routing dei messaggi] [ lnk-query] descrive hello linguaggio di query IoT Hub è possibile utilizzare tooretrieve informazioni dall'IoT Hub sul gemelli di dispositivo e i processi.
* [Supporto di IoT Hub MQTT] [ lnk-devguide-mqtt] fornisce ulteriori informazioni sul supporto di IoT Hub per protocollo MQTT hello.

## <a name="next-steps"></a>Passaggi successivi
A questo punto si è appreso come metodi diretti toouse, potrebbe risultare interessante nel seguente argomento della Guida alla developer IoT Hub hello:

* [Pianificare processi in più dispositivi][lnk-devguide-jobs]

Se si desidera tootry alcuni dei concetti di hello descritti in questo articolo, si potrebbero essere interessati hello segue esercitazione IoT Hub:

* [Usare metodi diretti][lnk-methods-tutorial]

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
