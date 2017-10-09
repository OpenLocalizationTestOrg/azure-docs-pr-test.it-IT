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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Come toolog eventi tooAzure hub eventi in Gestione API di Azure
Hub eventi di Azure è un servizio in ingresso dati altamente scalabili in grado di acquisire milioni di eventi al secondo in modo che sia possibile elaborare e analizzare hello enormi quantità di dati prodotti da applicazioni e dispositivi connessi. Hub eventi funge da hello "porta principale" per una pipeline di eventi e una volta in un hub eventi vengono raccolti i dati possono essere trasformato e archiviate utilizzando qualsiasi provider analitica in tempo reale o schede dell'invio in batch o dell'archiviazione. Hub eventi separa produzione hello di un flusso di eventi dal consumo hello di tali eventi, in modo che i consumer di eventi può accedere agli eventi di hello in una pianificazione personalizzata.

Questo articolo è una toohello complementare [integrare gestione API di Azure con hub eventi](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video e viene descritto come gli eventi di gestione API toolog tramite hub di eventi di Azure.

## <a name="create-an-azure-event-hub"></a>Creare un Hub di eventi di Azure
un nuovo Hub eventi, accedi toohello toocreate [portale di Azure classico](https://manage.windowsazure.com) e fare clic su **New**->**servizi App**->**Bus di servizio**  -> **Hub eventi**->**creazione rapida**. Immettere un nome e un'area per l'hub eventi, selezionare una sottoscrizione e quindi uno spazio dei nomi. Se in precedenza è ancora stato creato uno spazio dei nomi è possibile crearne uno digitando un nome in hello **Namespace** casella di testo. Dopo aver configurate tutte le proprietà, fare clic su **creare un nuovo Hub eventi** toocreate hello Hub eventi.

![Creare un hub eventi][create-event-hub]

Passare toohello **configura** scheda per il nuovo Hub eventi e creare due **criteri di accesso condiviso**. Nome hello come primo **invio** e assegnargli **inviare** autorizzazioni.

![Criterio Invio][sending-policy]

Nome hello secondo **ricezione**, assegnargli **ascolto** le autorizzazioni e fare clic su **salvare**.

![Criterio Ricezione][receiving-policy]

Tutti i criteri di accesso condiviso consente applicazioni toosend e ricevere eventi tooand da hello Hub eventi. stringhe di connessione di hello tooaccess per questi criteri, passare toohello **Dashboard** hello Hub eventi e fare clic su scheda **informazioni di connessione**.

![Stringa di connessione][event-hub-dashboard]

Hello **invio** stringa di connessione viene utilizzata durante la registrazione eventi, hello e **ricezione** stringa di connessione viene utilizzata durante il download di eventi da hello Hub eventi.

![Stringa di connessione][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Creare un logger di Gestione API
Dopo aver creato un Hub eventi, passaggio successivo hello è tooconfigure un [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) l'API di gestione del servizio in modo da potere registrare eventi toohello Hub eventi.

Logger di gestione API vengono configurati utilizzando hello [API REST gestione API](http://aka.ms/smapi). Prima di utilizzare hello API REST per hello prima volta, esaminare hello [prerequisiti](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e assicurarsi di aver [abilitato toohello accesso API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate un logger, effettuare una richiesta HTTP PUT con hello segue il modello di URL.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Sostituire `{your service}` con nome hello dell'istanza del servizio Gestione API.
* Sostituire `{new logger name}` con il nome desiderato per il nuovo logger hello. Si farà riferimento questo nome quando si configura hello [log-a-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) criteri

Aggiungere hello seguito intestazioni toohello richiesta.

* Content-Type: application/json
* Authorization : SharedAccessSignature 58...
  * Per istruzioni sulla generazione di hello `SharedAccessSignature` vedere [autenticazione di API REST di gestione di Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Specificare il corpo di richiesta hello utilizzando hello seguente modello.

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

* `type`deve essere impostato troppo`AzureEventHub`.
* `description`fornisce una descrizione facoltativa del logger hello e può essere una stringa di lunghezza zero, se necessario.
* `credentials`contiene hello `name` e `connectionString` di Hub di eventi di Azure.

Quando si effettua la richiesta di hello, se il logger hello viene creato un codice di stato `201 Created` viene restituito.

> [!NOTE]
> Per altri possibili codici restituiti e i relativi motivi, vedere [Creare un logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee come eseguire altre operazioni come elenco, update e delete, vedere hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentazione di entità.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Configurare i criteri log-to-eventhubs
Dopo aver configurato il logger in Gestione API, è possibile configurare gli eventi di log-a-eventhubs criteri toolog hello desiderato. Hello log-a-eventhubs criterio può essere utilizzato in entrambi hello sezione criteri in ingresso o in uscita criteri hello.

criteri tooconfigure, accedi toohello [portale di Azure](https://portal.azure.com), passare il servizio di gestione API tooyour e fare clic su **portale di pubblicazione** tooaccess hello portale di pubblicazione.

![Portale di pubblicazione][publisher-portal]

Fare clic su **criteri** hello gestione API dal menu a sinistra di hello, selezionare prodotto desiderato hello e API e fare clic su **aggiungere criteri**. In questo esempio stiamo aggiungendo un criterio toohello **API Echo** in hello **Unlimited** prodotto.

![Aggiungi criteri][add-policy]

Posizionare il cursore nel hello `inbound` criteri sezione e fare clic su hello **Log tooEventHub** hello tooinsert criteri `log-to-eventhub` modello di criteri di istruzione.

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Sostituire `logger-id` con nome hello del logger di gestione API hello configurato nel passaggio precedente hello.

È possibile utilizzare qualsiasi espressione che restituisce una stringa come valore hello hello `log-to-eventhub` elemento. In questo esempio viene registrata una stringa contenente data hello e l'ora, nome del servizio, id richiesta, indirizzo ip di richiesta e il nome dell'operazione.

Fare clic su **salvare** toosave hello aggiornata la configurazione dei criteri. Non appena viene salvato criteri hello sono attivo e gli eventi sono registrato toohello designato Hub eventi.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull'Hub eventi di Azure
  * [Introduzione all'Hub eventi](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Ricevere messaggi con EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guida alla programmazione di Hub eventi](../event-hubs/event-hubs-programming-guide.md)
* Altre informazioni sull'integrazione di Gestione API e Hub eventi
  * [Informazioni di riferimento per l'entità logger](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [Informazioni di riferimento per i criteri log-to-event](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Monitorare le API con Gestione API di Azure, Hub eventi e Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Guardare un video con la procedura dettagliata
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
