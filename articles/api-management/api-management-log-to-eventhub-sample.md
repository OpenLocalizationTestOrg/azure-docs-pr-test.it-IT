---
title: le API di gestione API di Azure, gli hub di eventi e Runscope aaaMonitor | Documenti Microsoft
description: Applicazione di esempio che illustra i criteri di log-a-eventhub hello connessione gestione API di Azure, gli hub di eventi di Azure e Runscope per HTTP di registrazione e monitoraggio
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a>Monitorare le API con Gestione API di Azure, Hub eventi e Runscope
Hello [servizio Gestione API](api-management-key-concepts.md) fornisce molte funzionalità tooenhance hello elaborazione di HTTP le richieste inviate tooyour API HTTP. Hello, tuttavia, l'esistenza di hello richieste e risposte sono temporanee. viene richiesto di Hello e passano attraverso hello API Gestione servizio tooyour API back-end. L'API elabora la richiesta di hello e una risposta passa attraverso i consumer toohello API. Servizio gestione API Hello mantiene alcune importanti statistiche sulle hello API per la visualizzazione nel dashboard del portale hello server di pubblicazione, ma che vanno oltre, dettagli hello non sono più disponibili.

Utilizzando hello [log-a-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [criteri](api-management-howto-policies.md) nel servizio Gestione API hello è possibile inviare i dettagli da hello richiesta e risposta tooan [Hub di eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md). Esistono diversi motivi per cui è possibile toogenerate eventi dai messaggi HTTP inviati tooyour API. ad esempio per ottenere audit trail di aggiornamenti, analisi di utilizzo, avvisi relativi alle eccezioni e integrazioni di terze parti.   

In questo articolo viene illustrato come toocapture hello intera richiesta e risposta messaggio HTTP, inviarlo tooan Hub eventi e quindi tale servizio di terze parti di tooa messaggio che fornisce HTTP registrazione e monitoraggio dei servizi di inoltro.

## <a name="why-send-from-api-management-service"></a>Vantaggi dell'invio dal servizio Gestione API
È possibile toowrite HTTP middleware che può collegare API HTTP Framework toocapture richieste e risposte HTTP e li feed in di registrazione e monitoraggio dei sistemi. approccio di Hello svantaggio toothis è hello HTTP middleware deve toobe integrato nel back-end hello API e deve corrispondere a hello di hello API. Se sono presenti più API ciascuno di essi deve distribuire hello middleware. Spesso non è possibile aggiornare le API back-end.

Con l'infrastruttura di registrazione toointegrate servizio di gestione API di Azure hello offre una soluzione indipendente dalla piattaforma e centralizzata. È inoltre scalabile, in parte dovuto toohello [-replica geografica](api-management-howto-deploy-multi-region.md) funzionalità di gestione API di Azure.

## <a name="why-send-tooan-azure-event-hub"></a>È possibile inviare tooan Hub di eventi di Azure.
È un tooask ragionevole, motivo per cui creare un criterio che è l'hub di eventi specifici tooAzure? Esistono molte diverse posizioni in cui si desidera conoscere toolog richieste personali. Perché non è sufficiente inviare hello richiede direttamente la destinazione finale toohello?  è una delle opzioni disponibili. Tuttavia, quando si effettua le richieste di registrazione da un servizio Gestione API, è necessario tooconsider come messaggi di registrazione influirà sulle prestazioni di hello di hello API. Gli incrementi graduali nel carico possono essere gestiti da istanze a disponibilità crescente dei componenti di sistema o sfruttando i vantaggi della replica geografica. Tuttavia, brevi picchi del traffico possono causare richieste toobe ritardato in modo significativo se infrastruttura toologging richieste avvia tooslow sotto carico.

Hello hub eventi di Azure è progettato tooingress grandi volumi di dati, con capacità per la gestione di un numero superiore di eventi del numero di hello di HTTP richiede la maggior parte dei processo API. Hello Hub eventi funge da un tipo di buffer sofisticate tra l'API del servizio e hello infrastruttura di gestione che verrà archiviata e l'elaborazione dei messaggi hello. In questo modo si garantisce che le prestazioni di API non subiranno scadenza toohello dell'infrastruttura di registrazione.  

Una volta passati tooan Hub di eventi è persistente e rimarrà in attesa di tooprocess consumer di Hub eventi, dati hello. Hello Hub eventi non è rilevante come verrà elaborata, semplicemente cuore assicurandosi che il messaggio hello verrà recapitato correttamente.     

Hub eventi sono i gruppi di consumer toomultiple hello possibilità toostream eventi. In questo modo toobe eventi elaborati da sistemi completamente diversi. In questo modo, che supporta numerosi scenari di integrazione senza inserire ritardi di addizione su hello l'elaborazione della richiesta API hello all'interno del servizio Gestione API di hello quando sono necessari per un solo evento toobe generato.

## <a name="a-policy-toosend-applicationhttp-messages"></a>Un messaggio di applicazione/http toosend criteri
Un hub eventi accetta i dati evento sotto forma di semplice stringa. contenuto Hello di tale stringa è completamente backup tooyou. toopackage in grado di toobe fino a una richiesta HTTP e inviarla off tooEvent hub dobbiamo stringa hello tooformat con le informazioni di richiesta o risposta hello. In situazioni di questo tipo, se è presente un formato esistente, che è possibile riutilizzare, quindi potrebbe non essere toowrite nostro l'analisi codice. Inizialmente è considerato utilizzando hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) per l'invio di richieste e risposte HTTP. ma questo formato è ottimizzato per l'archiviazione di una sequenza di richieste HTTP in un formato basato su JSON. Contiene un numero di elementi obbligatori che aggiungere complessità superflua per uno scenario di hello del passaggio di un messaggio hello HTTP rete hello.  

Stato di un'opzione alternativa hello toouse `application/http` tipo di supporto come descritto nella specifica HTTP hello [7230 RFC](http://tools.ietf.org/html/rfc7230). Questo tipo di supporti utilizza hello esatta stesso formato di messaggi HTTP di trasmissione utilizzato tooactually rete hello, ma l'intero messaggio hello può essere inserito nel corpo di hello di un'altra richiesta HTTP. In questo caso ci limiteremo corpo hello toouse come nostro tooEvent toosend messaggio hub. Per praticità, è un parser che esiste nel [Client di Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) librerie che possono analizzare questo formato e convertirlo in hello nativo `HttpRequestMessage` e `HttpResponseMessage` oggetti.

toocreate in grado di toobe questo messaggio è necessario tootake sfruttare basato su c# [espressioni di criteri](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Gestione API di Azure. Ecco i criteri di hello che invia un tooAzure messaggio di richiesta HTTP hub eventi.

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a>Dichiarazione di criteri
È necessario evidenziare alcuni aspetti di questa espressione di criteri. criteri di log-a-eventhub Hello ha un attributo denominato id logger che fa riferimento toohello nome del logger che è stato creato all'interno di hello servizio Gestione API. dettagli della modalità toosetup un logger di Hub eventi del servizio Gestione API hello è reperibile nel documento hello Hello [come toolog eventi tooAzure hub eventi in Gestione API di Azure](api-management-howto-log-event-hubs.md). secondo attributo Hello è un parametro facoltativo che indica a messaggi hello toostore partizione nell'hub eventi. Hub eventi utilizzare partizioni tooenable scalabilty e richiede un minimo di due. recapito ordinato dei messaggi Hello è garantito solo all'interno di una partizione. Se non si indicare l'Hub eventi in messaggi hello tooplace partizione, utilizza un carico di hello toodistribute algoritmo round-robin. Tuttavia, che può causare alcuni dei nostri toobe i messaggi elaborati nell'ordine errato.  

### <a name="partitions"></a>Partitions
tooensure i messaggi vengono recapitati tooconsumers in ordine e usufruire delle funzionalità di distribuzione hello carico delle partizioni, si è deciso di partizione di tooone i messaggi di richiesta di toosend HTTP e HTTP risposta messaggi tooa seconda partizione. In questo modo si assicurerà una distribuzione uniforme del carico e sarà possibile garantire che tutte le richieste e le risposte vengano utilizzate nell'ordine stabilito. È possibile che un toobe risposta utilizzati prima della richiesta di hello corrispondente, ma che non è un problema perché è un meccanismo diverso per la correlazione delle richieste tooresponses e sappiamo che le richieste provengano sempre prima le risposte.

### <a name="http-payloads"></a>Payload HTTP
Dopo la compilazione di hello `requestLine` controlliamo toosee se il corpo della richiesta hello deve essere troncato. corpo della richiesta Hello è troncato tooonly 1024. Questo può essere aumentato, tuttavia i singoli messaggi Hub eventi sono too256KB limitato, dunque è probabile che alcune HTTP corpi verrà non rientrano in un singolo messaggio. Quando si esegue una quantità significativa di informazioni di registrazione e analitica può essere derivata da solo riga di richiesta HTTP hello e intestazioni. Inoltre, molte richieste API restituiranno solo i corpi di piccole dimensioni e pertanto la perdita di hello del valore di informazioni troncando i corpi di grandi dimensioni è piuttosto minima riduzione toohello confronto trasferimento, l'elaborazione e archiviazione costi tookeep tutto il contenuto del corpo. Una nota finale sull'elaborazione testo hello è toopass `true` toohello come<string>metodo () perché venga letto contenuto del corpo hello, ma è anche desidera hello API back-end toobe tooread in grado di hello corpo. Passando il metodo toothis true è causare hello corpo toobe memorizzato nel buffer in modo che possa essere letto una seconda volta. Questo è importante toobe considerare se è disponibile un'API che non il caricamento di file di dimensioni molto grandi o utilizza polling lungo. In questi casi, sarebbe migliore tooavoid durante la lettura del corpo hello affatto.   

### <a name="http-headers"></a>Intestazioni HTTP
Intestazioni HTTP possono semplicemente trasferite nel formato di messaggio hello in un formato di coppia chiave/valore semplice. Scelto toostrip out determinate sicurezza campi riservati, tooavoid inutilmente perdita di informazioni sulle credenziali. È poco probabile che le chiavi API e altre credenziali vengano usate per finalità analitiche. Se si desiderano toodo analisi per l'utente di hello e prodotto specifico hello in uso, quindi è stato possibile ottenere che da hello `context` e aggiungere tale messaggio toohello.     

### <a name="message-metadata"></a>Metadati del messaggio
Quando si compila l'hub di eventi di hello messaggio completo toosend toohello prima riga hello non è parte effettiva di hello `application/http` messaggio. prima riga Hello è metadati aggiuntivi costituito se il messaggio hello è un messaggio di richiesta o risposta e un id di messaggio che è usato toocorrelate richiede tooresponses. id messaggio Hello viene creato utilizzando un altro criterio simile al seguente:

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

Avremmo potuto creare messaggio di richiesta di hello, archiviato che in una variabile finché hello risposta è stata restituita e quindi semplicemente inviata hello richiesta e risposta come un singolo messaggio. Tuttavia, l'invio in modo indipendente, hello richiesta e risposta e utilizzando un toocorrelate id messaggio hello due, si ottiene una maggiore flessibilità per la dimensione del messaggio hello, hello possibilità tootake sfruttare più partizioni, mantenendo hello e ordine dei messaggi richiesta verrà visualizzato nel dashboard registrazione prima. Possono essere presenti anche alcuni scenari in cui una risposta valida non viene mai inviata hub eventi toohello, probabilmente a causa di errore irreversibile richiesta tooa nel servizio di gestione API hello, ma sarà ancora un record di richiesta di hello.

messaggio di Hello criteri toosend hello risposta HTTP esegue la ricerca richiesta toohello molto simili e pertanto hello completare la configurazione dei criteri è simile al seguente:

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

Hello `set-variable` criteri creano un valore che sia accessibile da entrambi hello `log-to-eventhub` criteri in hello `<inbound>` sezione e hello `<outbound>` sezione.  

## <a name="receiving-events-from-event-hubs"></a>Ricezione di eventi dall'Hub eventi
Gli eventi provenienti dall'Hub di eventi di Azure vengono ricevuti utilizzando hello [protocollo AMQP](http://www.amqp.org/). il team di Microsoft Service Bus Hello apportate client hello toomake disponibili librerie utilizzo di eventi più semplici. Esistono due approcci diversi è supportati, uno è in corso un *Consumer diretto* e altri hello utilizza hello `EventProcessorHost` classe. Esempi di questi due approcci sono disponibili in hello [Guida per programmatori hub eventi](../event-hubs/event-hubs-programming-guide.md). versione breve di Hello delle differenze di hello è, `Direct Consumer` offre controllo completo e hello `EventProcessorHost` non le attività di plumbing hello per si ma su alcuni presupposti come elaborare gli eventi.  

### <a name="eventprocessorhost"></a>EventProcessorHost
In questo esempio, si utilizzerà hello `EventProcessorHost` per semplicità, tuttavia potrebbe non hello ottimale per questo particolare scenario. `EventProcessorHost`hello lavoro assicurandosi che non si dispone di tooworry informazioni sul threading problemi all'interno di una classe di evento specifico del processore. Tuttavia, in questo scenario, stiamo semplicemente la conversione del formato tooanother messaggi hello e passarlo lungo tooanother servizio utilizzando un metodo asincrono. Non è necessario aggiornare lo stato condiviso e quindi non si rischia che si verifichino problemi di threading. Per la maggior parte degli scenari, `EventProcessorHost` costituisce probabilmente la scelta ideale hello e è certamente l'opzione più semplice hello.     

### <a name="ieventprocessor"></a>IEventProcessor
concetto fondamentale di Hello quando si utilizza `EventProcessorHost` è toocreate un un'implementazione di hello `IEventProcessor` interfaccia che contiene il metodo hello `ProcessEventAsync`. le tracce di Hello di tale metodo sono illustrata di seguito:

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

Un elenco di oggetti EventData vengono passati nel metodo hello e abbiamo scorrere tale elenco. byte Hello di ogni metodo di analisi in un oggetto HttpMessage e tale oggetto viene passato l'istanza tooan IHttpMessageProcessor.

### <a name="httpmessage"></a>HttpMessage
Hello `HttpMessage` istanza contiene tre tipi di dati:

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

Hello `HttpMessage` istanza contiene un `MessageId` GUID che consente di elaborare richieste hello HTTP tooconnect risposta HTTP corrispondente toohello e un valore booleano valore che indica se l'oggetto hello contiene un'istanza di un HttpRequestMessage e HttpResponseMessage. Utilizzando hello compilato nelle classi HTTP da `System.Net.Http`, è stato in grado di tootake sfruttare hello `application/http` l'analisi del codice che è incluso in `System.Net.Http.Formatting`.  

### <a name="ihttpmessageprocessor"></a>IHttpMessageProcessor
Hello `HttpMessage` istanza viene quindi inoltrata tooimplementation di `IHttpMessageProcessor` che è un'interfaccia creato ricezione hello toodecouple e interpretazione degli eventi hello da Hub di eventi di Azure e hello effettivi l'elaborazione di esso.

## <a name="forwarding-hello-http-message"></a>Inoltrare il messaggio hello HTTP
Per questo esempio, ho deciso sarebbe interessante toopush hello richiesta HTTP su troppo[Runscope](http://www.runscope.com). Runscope è un servizio basato sul cloud specializzato nel debug, nella registrazione e nel monitoraggio HTTP. Hanno un livello gratuito, è facile tootry e consentirà le richieste HTTP di hello toosee nel flusso in tempo reale tramite il servizio Gestione API.

Hello `IHttpMessageProcessor` implementazione è simile al seguente,

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

È stato in grado di tootake sfruttare un [libreria client esistente per Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) che rende facile toopush `HttpRequestMessage` e `HttpResponseMessage` istanze backup nel proprio servizio. In ordine tooaccess hello API Runscope sarà necessario un account e una chiave API. È possibile trovare istruzioni per ottenere una chiave API in hello [tooAccess la creazione di applicazioni API Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.

## <a name="complete-sample"></a>Esempio completo
Hello [codice sorgente](https://github.com/darrelmiller/ApimEventProcessor) e test dell'esempio hello sono su GitHub. È necessario un [servizio Gestione API](api-management-get-started.md), [un Hub eventi connesso](api-management-howto-log-event-hubs.md)e un [Account di archiviazione](../storage/common/storage-create-storage-account.md) toorun: esempio hello per se stessi.   

esempio Hello è sufficiente una semplice applicazione Console è in ascolto per gli eventi provenienti dall'Hub di eventi, li converte in un `HttpRequestMessage` e `HttpResponseMessage` oggetti e quindi li inoltra su toohello Runscope API.

Nella seguente immagine animata di hello, è possibile visualizzare una richiesta effettuata tooan API nel portale per sviluppatori, messaggio hello hello Console dell'applicazione che mostra la ricezione di hello elaborati e inoltrati e quindi hello richiesta e risposta visualizzati in hello Runscope traffico controllo.

![Dimostrazione della richiesta viene inoltrata tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a>Riepilogo
Servizio gestione API di Azure fornisce un traffico di hello HTTP toocapture ideale in viaggio tooand dalle API. Hub eventi di Azure è una soluzione a scalabilità elevata e costi ridotti per l'acquisizione e l'inserimento del traffico in sistemi di elaborazione secondari per operazioni di registrazione e monitoraggio e per altre analisi avanzate. Connessione a sistemi Runscope è un semplice come poche decine righe di codice di monitoraggio del traffico di terze parti too3rd.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sull'Hub eventi di Azure
  * [Introduzione all'Hub eventi](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Ricevere messaggi con EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guida alla programmazione di Hub eventi](../event-hubs/event-hubs-programming-guide.md)
* Altre informazioni sull'integrazione di Gestione API e Hub eventi
  * [Come toolog eventi tooAzure hub eventi in Gestione API di Azure](api-management-howto-log-event-hubs.md)
  * [Informazioni di riferimento per l'entità logger](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [Informazioni di riferimento per i criteri log-to-event](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
