---
title: aaaHow toolog eventi tooAzure hub eventi in Gestione API di Azure | Documenti Microsoft
description: Informazioni su come toolog eventi tooAzure hub eventi in Gestione API di Azure.
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
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="a3cfb-103">Come toolog eventi tooAzure hub eventi in Gestione API di Azure</span><span class="sxs-lookup"><span data-stu-id="a3cfb-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="a3cfb-104">Hub eventi di Azure è un servizio in ingresso dati altamente scalabili in grado di acquisire milioni di eventi al secondo in modo che sia possibile elaborare e analizzare hello enormi quantità di dati prodotti da applicazioni e dispositivi connessi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a3cfb-105">Hub eventi funge da hello "porta principale" per una pipeline di eventi e una volta in un hub eventi vengono raccolti i dati possono essere trasformato e archiviate utilizzando qualsiasi provider analitica in tempo reale o schede dell'invio in batch o dell'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="a3cfb-106">Hub eventi separa produzione hello di un flusso di eventi dal consumo hello di tali eventi, in modo che i consumer di eventi può accedere agli eventi di hello in una pianificazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="a3cfb-107">Questo articolo è una toohello complementare [integrare gestione API di Azure con hub eventi](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video e viene descritto come gli eventi di gestione API toolog tramite hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="a3cfb-108">Creare un Hub di eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="a3cfb-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="a3cfb-109">un nuovo Hub eventi, accedi toohello toocreate [portale di Azure classico](https://manage.windowsazure.com) e fare clic su **New**->**servizi App**->**Bus di servizio**  -> **Hub eventi**->**creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="a3cfb-110">Immettere un nome e un'area per l'hub eventi, selezionare una sottoscrizione e quindi uno spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="a3cfb-111">Se in precedenza è ancora stato creato uno spazio dei nomi è possibile crearne uno digitando un nome in hello **Namespace** casella di testo.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="a3cfb-112">Dopo aver configurate tutte le proprietà, fare clic su **creare un nuovo Hub eventi** toocreate hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Creare un hub eventi][create-event-hub]

<span data-ttu-id="a3cfb-114">Passare toohello **configura** scheda per il nuovo Hub eventi e creare due **criteri di accesso condiviso**.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="a3cfb-115">Nome hello come primo **invio** e assegnargli **inviare** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Criterio Invio][sending-policy]

<span data-ttu-id="a3cfb-117">Nome hello secondo **ricezione**, assegnargli **ascolto** le autorizzazioni e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Criterio Ricezione][receiving-policy]

<span data-ttu-id="a3cfb-119">Tutti i criteri di accesso condiviso consente applicazioni toosend e ricevere eventi tooand da hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="a3cfb-120">stringhe di connessione di hello tooaccess per questi criteri, passare toohello **Dashboard** hello Hub eventi e fare clic su scheda **informazioni di connessione**.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Stringa di connessione][event-hub-dashboard]

<span data-ttu-id="a3cfb-122">Hello **invio** stringa di connessione viene utilizzata durante la registrazione eventi, hello e **ricezione** stringa di connessione viene utilizzata durante il download di eventi da hello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Stringa di connessione][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="a3cfb-124">Creare un logger di Gestione API</span><span class="sxs-lookup"><span data-stu-id="a3cfb-124">Create an API Management logger</span></span>
<span data-ttu-id="a3cfb-125">Dopo aver creato un Hub eventi, passaggio successivo hello è tooconfigure un [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) l'API di gestione del servizio in modo da potere registrare eventi toohello Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="a3cfb-126">Logger di gestione API vengono configurati utilizzando hello [API REST gestione API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="a3cfb-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="a3cfb-127">Prima di utilizzare hello API REST per hello prima volta, esaminare hello [prerequisiti](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e assicurarsi di aver [abilitato toohello accesso API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="a3cfb-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="a3cfb-128">toocreate un logger, effettuare una richiesta HTTP PUT con hello segue il modello di URL.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="a3cfb-129">Sostituire `{your service}` con nome hello dell'istanza del servizio Gestione API.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="a3cfb-130">Sostituire `{new logger name}` con il nome desiderato per il nuovo logger hello.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="a3cfb-131">Si farà riferimento questo nome quando si configura hello [log-a-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) criteri</span><span class="sxs-lookup"><span data-stu-id="a3cfb-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="a3cfb-132">Aggiungere hello seguito intestazioni toohello richiesta.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="a3cfb-133">Content-Type: application/json</span><span class="sxs-lookup"><span data-stu-id="a3cfb-133">Content-Type : application/json</span></span>
* <span data-ttu-id="a3cfb-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="a3cfb-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="a3cfb-135">Per istruzioni sulla generazione di hello `SharedAccessSignature` vedere [autenticazione di API REST di gestione di Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="a3cfb-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="a3cfb-136">Specificare il corpo di richiesta hello utilizzando hello seguente modello.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-136">Specify hello request body using hello following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="a3cfb-137">`type`deve essere impostato troppo`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="a3cfb-138">`description`fornisce una descrizione facoltativa del logger hello e può essere una stringa di lunghezza zero, se necessario.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="a3cfb-139">`credentials`contiene hello `name` e `connectionString` di Hub di eventi di Azure.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="a3cfb-140">Quando si effettua la richiesta di hello, se il logger hello viene creato un codice di stato `201 Created` viene restituito.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="a3cfb-141">Per altri possibili codici restituiti e i relativi motivi, vedere [Creare un logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="a3cfb-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="a3cfb-142">toosee come eseguire altre operazioni come elenco, update e delete, vedere hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentazione di entità.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="a3cfb-143">Configurare i criteri log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="a3cfb-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="a3cfb-144">Dopo aver configurato il logger in Gestione API, è possibile configurare gli eventi di log-a-eventhubs criteri toolog hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="a3cfb-145">Hello log-a-eventhubs criterio può essere utilizzato in entrambi hello sezione criteri in ingresso o in uscita criteri hello.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="a3cfb-146">criteri tooconfigure, accedi toohello [portale di Azure](https://portal.azure.com), passare il servizio di gestione API tooyour e fare clic su **portale di pubblicazione** tooaccess hello portale di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portale di pubblicazione][publisher-portal]

<span data-ttu-id="a3cfb-148">Fare clic su **criteri** hello gestione API dal menu a sinistra di hello, selezionare prodotto desiderato hello e API e fare clic su **aggiungere criteri**.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="a3cfb-149">In questo esempio stiamo aggiungendo un criterio toohello **API Echo** in hello **Unlimited** prodotto.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Aggiungi criteri][add-policy]

<span data-ttu-id="a3cfb-151">Posizionare il cursore nel hello `inbound` criteri sezione e fare clic su hello **Log tooEventHub** hello tooinsert criteri `log-to-eventhub` modello di criteri di istruzione.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="a3cfb-153">Sostituire `logger-id` con nome hello del logger di gestione API hello configurato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="a3cfb-154">È possibile utilizzare qualsiasi espressione che restituisce una stringa come valore hello hello `log-to-eventhub` elemento.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="a3cfb-155">In questo esempio viene registrata una stringa contenente data hello e l'ora, nome del servizio, id richiesta, indirizzo ip di richiesta e il nome dell'operazione.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="a3cfb-156">Fare clic su **salvare** toosave hello aggiornata la configurazione dei criteri.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="a3cfb-157">Non appena viene salvato criteri hello sono attivo e gli eventi sono registrato toohello designato Hub eventi.</span><span class="sxs-lookup"><span data-stu-id="a3cfb-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3cfb-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3cfb-158">Next steps</span></span>
* <span data-ttu-id="a3cfb-159">Altre informazioni sull'Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="a3cfb-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="a3cfb-160">Introduzione all'Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a3cfb-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="a3cfb-161">Ricevere messaggi con EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="a3cfb-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="a3cfb-162">Guida alla programmazione di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a3cfb-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="a3cfb-163">Altre informazioni sull'integrazione di Gestione API e Hub eventi</span><span class="sxs-lookup"><span data-stu-id="a3cfb-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="a3cfb-164">Informazioni di riferimento per l'entità logger</span><span class="sxs-lookup"><span data-stu-id="a3cfb-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="a3cfb-165">Informazioni di riferimento per i criteri log-to-event</span><span class="sxs-lookup"><span data-stu-id="a3cfb-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="a3cfb-166">Monitorare le API con Gestione API di Azure, Hub eventi e Runscope</span><span class="sxs-lookup"><span data-stu-id="a3cfb-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="a3cfb-167">Guardare un video con la procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="a3cfb-167">Watch a video walkthrough</span></span>
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
