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
# <a name="read-device-to-cloud-messages-from-hello-built-in-endpoint"></a><span data-ttu-id="8ff38-103">Leggere messaggi da dispositivo a cloud da endpoint predefiniti hello</span><span class="sxs-lookup"><span data-stu-id="8ff38-103">Read device-to-cloud messages from hello built-in endpoint</span></span>

<span data-ttu-id="8ff38-104">Per impostazione predefinita, i messaggi vengono indirizzati toohello incorporato orientati ai servizi endpoint (**messaggi di eventi**), che è compatibile con [hub eventi][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="8ff38-104">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="8ff38-105">Questo endpoint è attualmente solo esposte tramite hello [AMQP] [ lnk-amqp] protocollo sulla porta 5671.</span><span class="sxs-lookup"><span data-stu-id="8ff38-105">This endpoint is currently only exposed using hello [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="8ff38-106">Un hub IoT espone hello seguenti proprietà tooenable è toocontrol hello endpoint di messaggistica compatibile con Hub eventi predefiniti **messaggi di eventi**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-106">An IoT hub exposes hello following properties tooenable you toocontrol hello built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="8ff38-107">Proprietà</span><span class="sxs-lookup"><span data-stu-id="8ff38-107">Property</span></span>            | <span data-ttu-id="8ff38-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="8ff38-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="8ff38-109">**Numero di partizioni**</span><span class="sxs-lookup"><span data-stu-id="8ff38-109">**Partition count**</span></span> | <span data-ttu-id="8ff38-110">Impostare questa proprietà al numero di hello creazione toodefine di [partizioni] [ lnk-event-hub-partitions] per l'inserimento di eventi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="8ff38-110">Set this property at creation toodefine hello number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="8ff38-111">**Tempo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="8ff38-111">**Retention time**</span></span>  | <span data-ttu-id="8ff38-112">Questa proprietà specifica per quanti giorni i messaggi vengono conservati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8ff38-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="8ff38-113">valore predefinito di Hello è un giorno, ma può essere maggiore di tooseven giorni.</span><span class="sxs-lookup"><span data-stu-id="8ff38-113">hello default is one day, but it can be increased tooseven days.</span></span> |

<span data-ttu-id="8ff38-114">IoT Hub consente anche gruppi di consumer toomanage su hello predefinite dispositivo a cloud endpoint di ricezione.</span><span class="sxs-lookup"><span data-stu-id="8ff38-114">IoT Hub also enables you toomanage consumer groups on hello built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="8ff38-115">Per impostazione predefinita, tutti i messaggi che non corrispondono in modo esplicito una regola di routing del messaggio vengono scritti toohello endpoint predefiniti.</span><span class="sxs-lookup"><span data-stu-id="8ff38-115">By default, all messages that do not explicitly match a message routing rule are written toohello built-in endpoint.</span></span> <span data-ttu-id="8ff38-116">Se si disattiva questa route di fallback, i messaggi che non corrispondono in modo esplicito a una regola di routing verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="8ff38-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="8ff38-117">È possibile modificare l'ora di memorizzazione hello, a livello di programmazione tramite hello [il provider di risorse IoT Hub API REST][lnk-resource-provider-apis], oppure utilizzando hello [portale di Azure] [ lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="8ff38-117">You can modify hello retention time, either programmatically through hello [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using hello [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="8ff38-118">IoT Hub espone hello **messaggi di eventi** i messaggi da dispositivo a cloud di hello tooread ricevuti dall'hub di servizi di endpoint predefiniti per il back-end.</span><span class="sxs-lookup"><span data-stu-id="8ff38-118">IoT Hub exposes hello **messages/events** built-in endpoint for your back-end services tooread hello device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="8ff38-119">Si tratta di eventi compatibile con Hub, che consentono di toouse qualsiasi servizio hub eventi di hello meccanismi hello supporta per la lettura dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="8ff38-119">This endpoint is Event Hub-compatible, which enables you toouse any of hello mechanisms hello Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-hello-built-in-endpoint"></a><span data-ttu-id="8ff38-120">Leggere da endpoint predefiniti hello</span><span class="sxs-lookup"><span data-stu-id="8ff38-120">Read from hello built-in endpoint</span></span>

<span data-ttu-id="8ff38-121">Quando si utilizza hello [Azure Service Bus SDK per .NET] [ lnk-servicebus-sdk] o hello [hub eventi - eventi processore Host][lnk-eventprocessorhost], è possibile usare qualsiasi connessione IoT Hub stringhe con le autorizzazioni corrette hello.</span><span class="sxs-lookup"><span data-stu-id="8ff38-121">When you use hello [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or hello [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with hello correct permissions.</span></span> <span data-ttu-id="8ff38-122">Utilizzare quindi **messaggi di eventi** come nome Hub eventi hello.</span><span class="sxs-lookup"><span data-stu-id="8ff38-122">Then use **messages/events** as hello Event Hub name.</span></span>

<span data-ttu-id="8ff38-123">Quando si utilizza gli SDK (o le integrazioni dei prodotti) che non sono consapevoli dell'IoT Hub, è necessario recuperare un endpoint compatibile con Hub eventi e il nome Hub eventi compatibile con impostazioni Hub IoT hello in hello [portale di Azure] [ lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="8ff38-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from hello IoT Hub settings in hello [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="8ff38-124">Nel Pannello di hub IoT hello, fare clic su **endpoint**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-124">In hello IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="8ff38-125">In hello **gli endpoint predefiniti** fare clic su **eventi**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-125">In hello **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="8ff38-126">Pannello Hello contiene hello seguenti valori: **endpoint compatibile con Hub eventi**, **nome compatibile con Hub eventi**, **partizioni**, **il periodo di conservazione**, e **gruppi di Consumer**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-126">hello blade contains hello following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Impostazioni da dispositivo a cloud][img-eventhubcompatible]

<span data-ttu-id="8ff38-128">Hello IoT Hub SDK richiede il nome dell'endpoint IoT Hub, ovvero hello **messaggi di eventi** come illustrato nell'hello **endpoint** blade.</span><span class="sxs-lookup"><span data-stu-id="8ff38-128">hello IoT Hub SDK requires hello IoT Hub endpoint name, which is **messages/events** as shown in hello **Endpoints** blade.</span></span>

<span data-ttu-id="8ff38-129">Se hello SDK in uso richiede una **Hostname** o **Namespace** valore, rimuovere lo schema di hello hello **endpoint compatibile con Hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-129">If hello SDK you are using requires a **Hostname** or **Namespace** value, remove hello scheme from hello **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="8ff38-130">Ad esempio, se l'endpoint compatibile con Hub eventi è **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** sarebbe  **l'hub IOT-ns-myiothub-1234.servicebus.windows.net**, hello e **Namespace** sarebbe **l'hub IOT-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="8ff38-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, hello **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and hello **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="8ff38-131">È quindi possibile utilizzare qualsiasi criterio di accesso condiviso hello **ServiceConnect** toohello tooconnect di autorizzazioni specificato Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8ff38-131">You can then use any shared access policy that has hello **ServiceConnect** permissions tooconnect toohello specified Event Hub.</span></span>

<span data-ttu-id="8ff38-132">Se è necessario toobuild una stringa di connessione Hub eventi con le informazioni precedenti hello, utilizzare hello seguente motivo:</span><span class="sxs-lookup"><span data-stu-id="8ff38-132">If you need toobuild an Event Hub connection string by using hello previous information, use hello following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="8ff38-133">SDK di Hello e integrazioni per cui è possibile utilizzare con gli endpoint compatibile con Hub eventi che espone l'IoT Hub sono inclusi gli elementi di hello hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="8ff38-133">hello SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes hello items in hello following list:</span></span>

* <span data-ttu-id="8ff38-134">[Client Java di Hub eventi](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="8ff38-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="8ff38-135">[Spout di Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8ff38-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="8ff38-136">È possibile visualizzare hello [spout origine](https://github.com/apache/storm/tree/master/external/storm-eventhubs) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ff38-136">You can view hello [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="8ff38-137">[Integrazione Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="8ff38-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ff38-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8ff38-138">Next steps</span></span>

<span data-ttu-id="8ff38-139">Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="8ff38-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="8ff38-140">Hello [iniziare] [ lnk-get-started] le esercitazioni illustrano come i messaggi da dispositivo a cloud toosend da simulati i dispositivi e leggere messaggi hello da endpoint predefiniti hello.</span><span class="sxs-lookup"><span data-stu-id="8ff38-140">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from simulated devices and read hello messages from hello built-in endpoint.</span></span> <span data-ttu-id="8ff38-141">Per ulteriori dettagli, vedere hello [messaggi da dispositivo a cloud IoT Hub processo mediante route] [ lnk-d2c-tutorial] esercitazione.</span><span class="sxs-lookup"><span data-stu-id="8ff38-141">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="8ff38-142">Se si desidera tooroute il dispositivo a cloud messaggi toocustom endpoint, vedere [utilizzare route dei messaggi e gli endpoint personalizzati per i messaggi da dispositivo a cloud][lnk-custom].</span><span class="sxs-lookup"><span data-stu-id="8ff38-142">If you want tooroute your device-to-cloud messages toocustom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
