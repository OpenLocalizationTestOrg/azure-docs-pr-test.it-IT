---
title: Come registrare gli eventi in Hub eventi di Azure in Gestione API di Azure | Microsoft Docs
description: Informazioni su come registrare eventi nell'Hub eventi di Azure in Gestione API di Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="8834c-103">Come registrare eventi nell'Hub eventi di Azure in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="8834c-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="8834c-104">Hub di eventi di Azure è un servizio di ingresso dati altamente scalabile che può inserire milioni di eventi al secondo in modo che è possibile elaborare e analizzare enormi quantità di dati generati per i dispositivi connessi e le applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8834c-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="8834c-105">Gli hub di eventi fungono da "porta principale" per una pipeline di eventi e una volta che i dati vengono raccolti in un hub di eventi, possono essere trasformati e archiviati con qualsiasi provider di analisi in tempo reale o adattatori di invio in batch/archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8834c-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="8834c-106">Gli hub di eventi separano la produzione di un flusso di eventi dal consumo di questi eventi, in modo che i consumer di eventi può accedere agli eventi in base a una pianificazione.</span><span class="sxs-lookup"><span data-stu-id="8834c-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="8834c-107">Questo articolo è complementare al video su come [Integrare la Gestione API di Azure con gli Hub di eventi](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) e descrive come registrare gli eventi di gestione API mediante gli hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8834c-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="8834c-108">Creare un Hub di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="8834c-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="8834c-109">Per creare un nuovo hub eventi, accedere al [portale di Azure classico](https://manage.windowsazure.com), quindi fare clic su **Nuovo**->**Servizi app**->**Bus di servizio**->**Hub eventi**->**Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="8834c-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="8834c-110">Immettere un nome e un'area per l'hub eventi, selezionare una sottoscrizione e quindi uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="8834c-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="8834c-111">Se non è ancora stato creato uno spazio dei nomi, è possibile crearne uno immettendo un nome nella casella di testo **Spazio dei nomi** .</span><span class="sxs-lookup"><span data-stu-id="8834c-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="8834c-112">Al termine della configurazione di tutte le proprietà, fare clic su **Crea un nuovo hub eventi** per creare l'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8834c-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Creare un hub eventi][create-event-hub]

<span data-ttu-id="8834c-114">Passare quindi alla scheda **Configura** per il nuovo hub eventi e creare due tipi di **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="8834c-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="8834c-115">Denominare il primo tipo di criteri **Invio** e assegnare ad essi le autorizzazioni di **invio**.</span><span class="sxs-lookup"><span data-stu-id="8834c-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Criterio Invio][sending-policy]

<span data-ttu-id="8834c-117">Denominare il secondo criterio **Ricezione**, assegnare al criterio le autorizzazioni **Listen**, quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8834c-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Criterio Ricezione][receiving-policy]

<span data-ttu-id="8834c-119">Ogni tipo di criteri di accesso condiviso consente alle applicazioni di inviare e ricevere eventi verso e dall'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8834c-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="8834c-120">Per accedere alle stringhe di connessione relative a questi criteri, passare alla scheda **Dashboard** dell'hub eventi e fare clic su **Informazioni di connessione**.</span><span class="sxs-lookup"><span data-stu-id="8834c-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Stringa di connessione][event-hub-dashboard]

<span data-ttu-id="8834c-122">La stringa di connessione di **invio** viene usata durante la registrazione di eventi, mentre la stringa di connessione di **ricezione** viene usata durante il download di eventi dall'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8834c-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Stringa di connessione][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="8834c-124">Creare un logger di Gestione API</span><span class="sxs-lookup"><span data-stu-id="8834c-124">Create an API Management logger</span></span>
<span data-ttu-id="8834c-125">Dopo aver creato un hub eventi, è necessario configurare un [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) nel servizio Gestione API, in modo che possa registrare eventi nell'hub eventi.</span><span class="sxs-lookup"><span data-stu-id="8834c-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="8834c-126">I logger di Gestione API vengono configurati mediante l' [API REST Gestione API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="8834c-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="8834c-127">Prima di usare l'API REST per la prima volta, vedere i [prerequisiti](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e assicurarsi di avere [abilitato l'accesso all'API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="8834c-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="8834c-128">Per creare un logger, effettuare una richiesta HTTP PUT usando il seguente modello URL.</span><span class="sxs-lookup"><span data-stu-id="8834c-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="8834c-129">Sostituire `{your service}` con il nome dell'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="8834c-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="8834c-130">Sostituire `{new logger name}` con il nome desiderato per il nuovo logger.</span><span class="sxs-lookup"><span data-stu-id="8834c-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="8834c-131">Si farà riferimento a questo nome al momento di configurare i criteri [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) .</span><span class="sxs-lookup"><span data-stu-id="8834c-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="8834c-132">Aggiungere le intestazioni seguenti alla richiesta.</span><span class="sxs-lookup"><span data-stu-id="8834c-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="8834c-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="8834c-133">Content-Type : application/json</span></span>
* <span data-ttu-id="8834c-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="8834c-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="8834c-135">Per istruzioni sulla generazione di `SharedAccessSignature` , vedere [Autenticazione dell'API REST Gestione API di Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="8834c-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="8834c-136">Specificare il corpo della richiesta usando il modello seguente.</span><span class="sxs-lookup"><span data-stu-id="8834c-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="8834c-137">`type` deve essere impostato su `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="8834c-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="8834c-138">`description` fornisce una descrizione facoltativa del logger e può essere una stringa di lunghezza zero, se lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="8834c-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="8834c-139">`credentials` contiene i valori `name` e `connectionString` di Hub eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="8834c-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="8834c-140">Quando si esegue la richiesta, se viene creato il logger, verrà visualizzato un codice di stato `201 Created` .</span><span class="sxs-lookup"><span data-stu-id="8834c-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="8834c-141">Per altri possibili codici restituiti e i relativi motivi, vedere [Creare un logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="8834c-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="8834c-142">Per informazioni su come eseguire altre operazioni, ad esempio elencare, aggiornare o eliminare, vedere la documentazione relativa all'entità [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) .</span><span class="sxs-lookup"><span data-stu-id="8834c-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="8834c-143">Configurare i criteri log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="8834c-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="8834c-144">Dopo la configurazione del logger in Gestione API, è possibile configurare i criteri log-to-eventhubs in modo da registrare gli eventi desiderati.</span><span class="sxs-lookup"><span data-stu-id="8834c-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="8834c-145">I criteri log-to-eventhubs possono essere usati nella sezione relativa ai criteri in ingresso o in quella relativa ai criteri in uscita.</span><span class="sxs-lookup"><span data-stu-id="8834c-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="8834c-146">Per configurare i criteri, accedere al [portale di Azure](https://portal.azure.com), passare al servizio Gestione API e fare clic su **Portale di pubblicazione** per accedervi.</span><span class="sxs-lookup"><span data-stu-id="8834c-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Portale di pubblicazione][publisher-portal]

<span data-ttu-id="8834c-148">Scegliere **Criteri** dal menu di Gestione API a sinistra, selezionare il prodotto e l'API desiderati e quindi fare clic su **Aggiungi criteri**.</span><span class="sxs-lookup"><span data-stu-id="8834c-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="8834c-149">In questo esempio si aggiungono dei criteri all'**API Echo** nel prodotto **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="8834c-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Aggiungi criteri][add-policy]

<span data-ttu-id="8834c-151">Posizionare il cursore nella sezione dei criteri `inbound` e fare clic sui criteri **Accedi a Hub eventi** per inserire il modello di istruzione dei criteri `log-to-eventhub`.</span><span class="sxs-lookup"><span data-stu-id="8834c-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="8834c-153">Sostituire `logger-id` con il nome del logger di Gestione API configurato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="8834c-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="8834c-154">È possibile usare qualsiasi espressione che restituisce una stringa come valore dell'elemento `log-to-eventhub` .</span><span class="sxs-lookup"><span data-stu-id="8834c-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="8834c-155">In questo esempio viene registrata una stringa contenente data e ora, nome del servizio, ID richiesta, indirizzo IP della richiesta e nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="8834c-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="8834c-156">Fare clic su **Salva** per salvare la configurazione aggiornata dei criteri.</span><span class="sxs-lookup"><span data-stu-id="8834c-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="8834c-157">Il criterio risulta attivo immediatamente dopo il salvataggio e gli eventi vengono registrati nell'hub eventi designato.</span><span class="sxs-lookup"><span data-stu-id="8834c-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8834c-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8834c-158">Next steps</span></span>
* <span data-ttu-id="8834c-159">Altre informazioni sull'Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="8834c-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="8834c-160">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="8834c-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="8834c-161">Ricevere messaggi con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="8834c-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="8834c-162">Guida alla programmazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="8834c-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="8834c-163">Altre informazioni sull'integrazione di Gestione API e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="8834c-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="8834c-164">Informazioni di riferimento per l'entità logger</span><span class="sxs-lookup"><span data-stu-id="8834c-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="8834c-165">Informazioni di riferimento per i criteri log-to-event</span><span class="sxs-lookup"><span data-stu-id="8834c-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="8834c-166">Monitorare le API con Gestione API di Azure, Hub eventi e Runscope</span><span class="sxs-lookup"><span data-stu-id="8834c-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="8834c-167">Guardare un video con la procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="8834c-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
