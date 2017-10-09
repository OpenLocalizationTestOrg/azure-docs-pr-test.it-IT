---
title: endpoint predefinito di aaaUnderstand hello IoT Hub di Azure | Documenti Microsoft
description: Guida per sviluppatori - viene descritto come toouse hello incorporato, i messaggi di Hub eventi compatibile con endpoint per leggere da dispositivo a cloud.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 15484c1b1828151ffcae5f4a1407264374223da1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a>Leggere messaggi da dispositivo a cloud da endpoint predefiniti hello

Per impostazione predefinita, i messaggi vengono indirizzati toohello incorporato orientati ai servizi endpoint (**messaggi di eventi**), che è compatibile con [hub eventi][lnk-event-hubs]. Questo endpoint è attualmente solo esposte tramite hello [AMQP] [ lnk-amqp] protocollo sulla porta 5671. Un hub IoT espone hello seguenti proprietà tooenable è toocontrol hello endpoint di messaggistica compatibile con Hub eventi predefiniti **messaggi di eventi**.

| Proprietà            | Descrizione |
| ------------------- | ----------- |
| **Numero di partizioni** | Impostare questa proprietà al numero di hello creazione toodefine di [partizioni] [ lnk-event-hub-partitions] per l'inserimento di eventi da dispositivo a cloud. |
| **Tempo di conservazione**  | Questa proprietà specifica per quanti giorni i messaggi vengono conservati dall'hub IoT. valore predefinito di Hello è un giorno, ma può essere maggiore di tooseven giorni. |

IoT Hub consente anche gruppi di consumer toomanage su hello predefinite dispositivo a cloud endpoint di ricezione.

Per impostazione predefinita, tutti i messaggi che non corrispondono in modo esplicito una regola di routing del messaggio vengono scritti toohello endpoint predefiniti. Se si disattiva questa route di fallback, i messaggi che non corrispondono in modo esplicito a una regola di routing verranno eliminati.

È possibile modificare l'ora di memorizzazione hello, a livello di programmazione tramite hello [il provider di risorse IoT Hub API REST][lnk-resource-provider-apis], oppure utilizzando hello [portale di Azure] [ lnk-management-portal].

IoT Hub espone hello **messaggi di eventi** i messaggi da dispositivo a cloud di hello tooread ricevuti dall'hub di servizi di endpoint predefiniti per il back-end. Si tratta di eventi compatibile con Hub, che consentono di toouse qualsiasi servizio hub eventi di hello meccanismi hello supporta per la lettura dei messaggi.

## <a name="read-from-hello-built-in-endpoint"></a>Leggere da endpoint predefiniti hello

Quando si utilizza hello [Azure Service Bus SDK per .NET] [ lnk-servicebus-sdk] o hello [hub eventi - eventi processore Host][lnk-eventprocessorhost], è possibile usare qualsiasi connessione IoT Hub stringhe con le autorizzazioni corrette hello. Utilizzare quindi **messaggi di eventi** come nome Hub eventi hello.

Quando si utilizza gli SDK (o le integrazioni dei prodotti) che non sono consapevoli dell'IoT Hub, è necessario recuperare un endpoint compatibile con Hub eventi e il nome Hub eventi compatibile con impostazioni Hub IoT hello in hello [portale di Azure] [ lnk-management-portal]:

1. Nel Pannello di hub IoT hello, fare clic su **endpoint**.
1. In hello **gli endpoint predefiniti** fare clic su **eventi**. Pannello Hello contiene hello seguenti valori: **endpoint compatibile con Hub eventi**, **nome compatibile con Hub eventi**, **partizioni**, **il periodo di conservazione**, e **gruppi di Consumer**.

    ![Impostazioni da dispositivo a cloud][img-eventhubcompatible]

Hello IoT Hub SDK richiede il nome dell'endpoint IoT Hub, ovvero hello **messaggi di eventi** come illustrato nell'hello **endpoint** blade.

Se hello SDK in uso richiede una **Hostname** o **Namespace** valore, rimuovere lo schema di hello hello **endpoint compatibile con Hub eventi**. Ad esempio, se l'endpoint compatibile con Hub eventi è **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** sarebbe  **l'hub IOT-ns-myiothub-1234.servicebus.windows.net**, hello e **Namespace** sarebbe **l'hub IOT-ns-myiothub-1234**.

È quindi possibile utilizzare qualsiasi criterio di accesso condiviso hello **ServiceConnect** toohello tooconnect di autorizzazioni specificato Hub eventi.

Se è necessario toobuild una stringa di connessione Hub eventi con le informazioni precedenti hello, utilizzare hello seguente motivo:

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

SDK di Hello e integrazioni per cui è possibile utilizzare con gli endpoint compatibile con Hub eventi che espone l'IoT Hub sono inclusi gli elementi di hello hello seguente elenco:

* [Client Java di Hub eventi](https://github.com/hdinsight/eventhubs-client).
* [Spout di Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md). È possibile visualizzare hello [spout origine](https://github.com/apache/storm/tree/master/external/storm-eventhubs) su GitHub.
* [Integrazione Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-endpoints].

Hello [iniziare] [ lnk-get-started] le esercitazioni illustrano come i messaggi da dispositivo a cloud toosend da simulati i dispositivi e leggere messaggi hello da endpoint predefiniti hello. Per ulteriori dettagli, vedere hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione.

Se si desidera tooroute il dispositivo a cloud messaggi toocustom endpoint, vedere [utilizzare route dei messaggi e gli endpoint personalizzati per i messaggi da dispositivo a cloud][lnk-custom].

[img-eventhubcompatible]: ./media/iot-hub-devguide-messages-read-builtin/eventhubcompatible.png

[lnk-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-management-portal]: https://portal.azure.com
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-event-hub-partitions]: ../event-hubs/event-hubs-features.md#partitions
[lnk-servicebus-sdk]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-eventprocessorhost]: http://blogs.msdn.com/b/servicebus/archive/2015/01/16/event-processor-host-best-practices-part-1.aspx
[lnk-amqp]: https://www.amqp.org/
