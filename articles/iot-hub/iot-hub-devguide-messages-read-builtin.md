---
title: Informazioni sull'endpoint predefinito dell'hub IoT di Azure | Microsoft Docs
description: 'Guida per gli sviluppatori: descrizione dell''uso dell''endpoint predefinito compatibile con l''hub eventi per la lettura dei messaggi da dispositivo a cloud.'
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
ms.openlocfilehash: fcc3743028e369fdc42b71887d49fb41fba2c0dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="read-device-to-cloud-messages-from-the-built-in-endpoint"></a><span data-ttu-id="17ded-103">Leggere messaggi da dispositivo a cloud dall'endpoint predefinito</span><span class="sxs-lookup"><span data-stu-id="17ded-103">Read device-to-cloud messages from the built-in endpoint</span></span>

<span data-ttu-id="17ded-104">Per impostazione predefinita, i messaggi vengono instradati all'endpoint per servizi predefinito (**messaggi/eventi**) compatibile con [Hub eventi][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="17ded-104">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="17ded-105">Questo endpoint è attualmente esposto solo con il protocollo [AMQP][lnk-amqp] sulla porta 5671.</span><span class="sxs-lookup"><span data-stu-id="17ded-105">This endpoint is currently only exposed using the [AMQP][lnk-amqp] protocol on port 5671.</span></span> <span data-ttu-id="17ded-106">Un hub IoT espone le proprietà seguenti per consentire il controllo dell'endpoint di messaggistica predefinito **messages/events**, compatibile con Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="17ded-106">An IoT hub exposes the following properties to enable you to control the built-in Event Hub-compatible messaging endpoint **messages/events**.</span></span>

| <span data-ttu-id="17ded-107">Proprietà</span><span class="sxs-lookup"><span data-stu-id="17ded-107">Property</span></span>            | <span data-ttu-id="17ded-108">Descrizione</span><span class="sxs-lookup"><span data-stu-id="17ded-108">Description</span></span> |
| ------------------- | ----------- |
| <span data-ttu-id="17ded-109">**Numero di partizioni**</span><span class="sxs-lookup"><span data-stu-id="17ded-109">**Partition count**</span></span> | <span data-ttu-id="17ded-110">Impostare questa proprietà in fase di creazione per definire il numero di [partizioni][lnk-event-hub-partitions] per l'inserimento di eventi da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="17ded-110">Set this property at creation to define the number of [partitions][lnk-event-hub-partitions] for device-to-cloud event ingestion.</span></span> |
| <span data-ttu-id="17ded-111">**Tempo di conservazione**</span><span class="sxs-lookup"><span data-stu-id="17ded-111">**Retention time**</span></span>  | <span data-ttu-id="17ded-112">Questa proprietà specifica per quanti giorni i messaggi vengono conservati dall'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="17ded-112">This property specifies how long in days messages are retained by IoT Hub.</span></span> <span data-ttu-id="17ded-113">Il valore predefinito è un giorno, ma può essere aumentato a sette giorni.</span><span class="sxs-lookup"><span data-stu-id="17ded-113">The default is one day, but it can be increased to seven days.</span></span> |

<span data-ttu-id="17ded-114">L'hub IoT consente inoltre di gestire i gruppi di consumer nell'endpoint di ricezione predefinito da dispositivo a cloud.</span><span class="sxs-lookup"><span data-stu-id="17ded-114">IoT Hub also enables you to manage consumer groups on the built-in device-to-cloud receive endpoint.</span></span>

<span data-ttu-id="17ded-115">Per impostazione predefinita, tutti i messaggi che non corrispondono in modo esplicito a una regola di routing vengono scritti nell'endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="17ded-115">By default, all messages that do not explicitly match a message routing rule are written to the built-in endpoint.</span></span> <span data-ttu-id="17ded-116">Se si disattiva questa route di fallback, i messaggi che non corrispondono in modo esplicito a una regola di routing verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="17ded-116">If you disable this fallback route, messages that do not explicitly match any message routing rules are dropped.</span></span>

<span data-ttu-id="17ded-117">È possibile modificare il tempo di conservazione a livello di codice con le [API del provider di risorse dell'hub IoT di Azure][lnk-resource-provider-apis] oppure usando il [portale di Azure][lnk-management-portal].</span><span class="sxs-lookup"><span data-stu-id="17ded-117">You can modify the retention time, either programmatically through the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis], or by using the [Azure portal][lnk-management-portal].</span></span>

<span data-ttu-id="17ded-118">L'hub IoT espone l'endpoint **messaggi/eventi** predefinito per permettere ai servizi back-end di leggere i messaggi da dispositivo a cloud ricevuti dall'hub.</span><span class="sxs-lookup"><span data-stu-id="17ded-118">IoT Hub exposes the **messages/events** built-in endpoint for your back-end services to read the device-to-cloud messages received by your hub.</span></span> <span data-ttu-id="17ded-119">L'endpoint è compatibile con Hub eventi e consente quindi di usare uno dei meccanismi supportati da tale servizio per la lettura dei messaggi.</span><span class="sxs-lookup"><span data-stu-id="17ded-119">This endpoint is Event Hub-compatible, which enables you to use any of the mechanisms the Event Hubs service supports for reading messages.</span></span>

## <a name="read-from-the-built-in-endpoint"></a><span data-ttu-id="17ded-120">Eseguire la lettura dall'endpoint predefinito</span><span class="sxs-lookup"><span data-stu-id="17ded-120">Read from the built-in endpoint</span></span>

<span data-ttu-id="17ded-121">Quando si usa [Azure Service Bus SDK per .NET][lnk-servicebus-sdk] o [Hub eventi - Host processore di eventi][lnk-eventprocessorhost], è possibile usare qualsiasi stringa di connessione dell'hub IoT con le autorizzazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="17ded-121">When you use the [Azure Service Bus SDK for .NET][lnk-servicebus-sdk] or the [Event Hubs - Event Processor Host][lnk-eventprocessorhost], you can use any IoT Hub connection strings with the correct permissions.</span></span> <span data-ttu-id="17ded-122">Usare quindi **messaggi/eventi** come nome dell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="17ded-122">Then use **messages/events** as the Event Hub name.</span></span>

<span data-ttu-id="17ded-123">Quando si usano gli SDK o integrazioni del prodotto non compatibili con l'hub IoT, è necessario recuperare un endpoint e un nome compatibili con Hub eventi dalle impostazioni dell'hub IoT nel [portale di Azure][lnk-management-portal]:</span><span class="sxs-lookup"><span data-stu-id="17ded-123">When you use SDKs (or product integrations) that are unaware of IoT Hub, you must retrieve an Event Hub-compatible endpoint and Event Hub-compatible name from the IoT Hub settings in the [Azure portal][lnk-management-portal]:</span></span>

1. <span data-ttu-id="17ded-124">Nel pannello dell'hub IoT fare clic su **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="17ded-124">In the IoT hub blade, click **Endpoints**.</span></span>
1. <span data-ttu-id="17ded-125">Nella sezione **Endpoint predefiniti** fare clic su **Eventi**.</span><span class="sxs-lookup"><span data-stu-id="17ded-125">In the **Built-in endpoints** section, click **Events**.</span></span> <span data-ttu-id="17ded-126">Il pannello contiene i valori seguenti: **Endpoint compatibile con l'hub eventi**, **Nome compatibile con l'hub eventi**, **Partizioni**, **Tempo di conservazione** e **Gruppi di consumer**.</span><span class="sxs-lookup"><span data-stu-id="17ded-126">The blade contains the following values: **Event Hub-compatible endpoint**, **Event Hub-compatible name**, **Partitions**, **Retention time**, and **Consumer groups**.</span></span>

    ![Impostazioni da dispositivo a cloud][img-eventhubcompatible]

<span data-ttu-id="17ded-128">L'SDK dell'hub IoT richiede il nome dell'endpoint dell'hub IoT, ossia **messages/events** come mostrato nel pannello **Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="17ded-128">The IoT Hub SDK requires the IoT Hub endpoint name, which is **messages/events** as shown in the **Endpoints** blade.</span></span>

<span data-ttu-id="17ded-129">Se l'SDK usato richiede un valore **Nome host** o **Spazio dei nomi**, rimuovere lo schema da **Endpoint compatibile con l'hub eventi**.</span><span class="sxs-lookup"><span data-stu-id="17ded-129">If the SDK you are using requires a **Hostname** or **Namespace** value, remove the scheme from the **Event Hub-compatible endpoint**.</span></span> <span data-ttu-id="17ded-130">Ad esempio, se l'endpoint compatibile con l'hub eventi è **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, il **Nome host** sarà **iothub-ns-myiothub-1234.servicebus.windows.net** e lo **Spazio dei nomi** sarà **iothub-ns-myiothub-1234**.</span><span class="sxs-lookup"><span data-stu-id="17ded-130">For example, if your Event Hub-compatible endpoint is **sb://iothub-ns-myiothub-1234.servicebus.windows.net/**, the **Hostname** would be **iothub-ns-myiothub-1234.servicebus.windows.net**, and the **Namespace** would be **iothub-ns-myiothub-1234**.</span></span>

<span data-ttu-id="17ded-131">È quindi possibile usare qualsiasi criterio di accesso condiviso con autorizzazioni **ServiceConnect** per connettersi all'hub eventi specificato.</span><span class="sxs-lookup"><span data-stu-id="17ded-131">You can then use any shared access policy that has the **ServiceConnect** permissions to connect to the specified Event Hub.</span></span>

<span data-ttu-id="17ded-132">Se si deve compilare una stringa di connessione dell'hub eventi con le informazioni precedenti, è possibile usare il modello seguente:</span><span class="sxs-lookup"><span data-stu-id="17ded-132">If you need to build an Event Hub connection string by using the previous information, use the following pattern:</span></span>

`Endpoint={Event Hub-compatible endpoint};SharedAccessKeyName={iot hub policy name};SharedAccessKey={iot hub policy key}`

<span data-ttu-id="17ded-133">Di seguito sono elencati gli SDK e le integrazioni che è possibile usare con gli endpoint compatibili con l'hub eventi esposti dall'hub IoT:</span><span class="sxs-lookup"><span data-stu-id="17ded-133">The SDKs and integrations that you can use with Event Hub-compatible endpoints that IoT Hub exposes includes the items in the following list:</span></span>

* <span data-ttu-id="17ded-134">[Client Java di Hub eventi](https://github.com/hdinsight/eventhubs-client).</span><span class="sxs-lookup"><span data-stu-id="17ded-134">[Java Event Hubs client](https://github.com/hdinsight/eventhubs-client).</span></span>
* <span data-ttu-id="17ded-135">[Spout di Apache Storm](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="17ded-135">[Apache Storm spout](../hdinsight/hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span> <span data-ttu-id="17ded-136">È possibile visualizzare il [codice sorgente dello spout](https://github.com/apache/storm/tree/master/external/storm-eventhubs) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="17ded-136">You can view the [spout source](https://github.com/apache/storm/tree/master/external/storm-eventhubs) on GitHub.</span></span>
* <span data-ttu-id="17ded-137">[Integrazione Apache Spark](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span><span class="sxs-lookup"><span data-stu-id="17ded-137">[Apache Spark integration](../hdinsight/hdinsight-apache-spark-eventhub-streaming.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="17ded-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17ded-138">Next steps</span></span>

<span data-ttu-id="17ded-139">Per altre informazioni sugli endpoint dell'hub IoT, vedere [Endpoint dell'hub IoT][lnk-endpoints].</span><span class="sxs-lookup"><span data-stu-id="17ded-139">For more information about IoT Hub endpoints, see [IoT Hub endpoints][lnk-endpoints].</span></span>

<span data-ttu-id="17ded-140">Le [esercitazioni introduttive][lnk-get-started] illustrano come inviare messaggi da dispositivo a cloud da dispositivi simulati e leggere i messaggi dall'endpoint predefinito.</span><span class="sxs-lookup"><span data-stu-id="17ded-140">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from simulated devices and read the messages from the built-in endpoint.</span></span> <span data-ttu-id="17ded-141">Per altri dettagli, vedere l'esercitazione [Elaborare messaggi da dispositivo a cloud dell'hub IoT usando route][lnk-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="17ded-141">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

<span data-ttu-id="17ded-142">Per instradare i messaggi da dispositivo a cloud verso endpoint personalizzati, vedere [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom] (Usare route messaggi ed endpoint personalizzati per i messaggi da dispositivo a cloud).</span><span class="sxs-lookup"><span data-stu-id="17ded-142">If you want to route your device-to-cloud messages to custom endpoints, see [Use message routes and custom endpoints for device-to-cloud messages][lnk-custom].</span></span>

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
