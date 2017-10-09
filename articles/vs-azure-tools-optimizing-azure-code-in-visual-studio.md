---
title: code di Azure in Visual Studio aaaOptimizing | Documenti Microsoft
description: "Informazioni su come il codice di Azure come strumento di ottimizzazione in Visual Studio consente di rendere il codice più affidabile e migliorare le prestazioni."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Ottimizzare il codice Azure
Quando si programmano App che usano Microsoft Azure, esistono alcune procedure consigliate da seguire toohelp evitare problemi di scalabilità, comportamento e le prestazioni in un ambiente cloud. Microsoft fornisce uno strumento di analisi del codice di Azure che riconosce molti di questi problemi comunemente riscontrati e aiuta a risolverli. È possibile scaricare lo strumento hello in Visual Studio tramite NuGet.

## <a name="azure-code-analysis-rules"></a>Regole di analisi codice di Azure
strumento di analisi del codice di Azure Hello utilizza hello seguendo regole tooautomatically flag del codice di Azure quando rileva i problemi noti che influiscono sulle prestazioni. I problemi rilevati vengono visualizzati come avvisi o errori del compilatore. Codice avviso hello tooresolve correzioni o suggerimenti o errore vengono spesso forniti tramite un'icona lampadina.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Evitare di utilizzare la modalità stato sessione (in-process) predefinita
### <a name="id"></a>ID
AP0000

### <a name="description"></a>Descrizione
Se si Usa modalità stato sessione (in-process) predefinita di hello per le applicazioni cloud, è possibile perdere lo stato della sessione.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Per impostazione predefinita, modalità di stato sessione hello specificata nel file Web. config hello è in-process. Inoltre, se non vengono specificate voci nel file di configurazione di hello, hello modalità stato sessione predefinita tooin-process. modalità in-process Hello archivia lo stato della sessione in memoria nel server web hello. Quando un'istanza viene riavviata o una nuova istanza viene utilizzata per il bilanciamento del carico o il supporto di failover, non viene salvato lo stato della sessione hello archiviato in memoria nel server web hello. Questa situazione impedisce l'applicazione hello essere scalabile nel cloud hello.

Lo stato della sessione ASP.NET supporta diverse opzioni di archiviazione per i dati dello stato sessione: InProc, StateServer, SQLServer, personalizzato e Off. Si consiglia di utilizzare dati toohost in modalità personalizzata in un archivio di stato sessione esterno, ad esempio [provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Soluzione
Una soluzione consigliata è toostore lo stato della sessione in un servizio cache gestita. Informazioni su come toouse [provider di stato della sessione di Azure per Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore lo stato della sessione. È possibile inoltre archivio sessione indicare in altre posizioni di tooensure che l'applicazione sia scalabile nel cloud hello. altre informazioni sulle soluzioni alternative, vedere toolearn [modalità stato sessione](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>L’esecuzione del metodo non deve essere asincrona
### <a name="id"></a>ID
AP1000

### <a name="description"></a>Descrizione
Creare metodi asincroni (ad esempio [await](https://msdn.microsoft.com/library/hh156528.aspx)) di fuori di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (metodo) e quindi chiamare i metodi di async hello da [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Dichiarazione di hello [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) il metodo asincrono comporta lavoro hello ruolo tooenter un ciclo di riavvio.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
La chiamata di metodi asincroni all'interno di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo causa hello runtime toorecycle hello lavoro ruolo del servizio cloud. Quando viene avviato un ruolo di lavoro, l'intera esecuzione del programma ha luogo all'interno di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo. In fase di chiusura hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo fa sì che il lavoro hello toorestart ruolo. Quando runtime ruolo di lavoro hello raggiunge metodo async hello, invia tutte le operazioni dopo il metodo asincrono hello e lo restituisce. Questo comporta lavoro hello tooexit ruolo dallo hello [ [ [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) (metodo) e riavviare. Durante l'iterazione successiva di hello di esecuzione, il ruolo di lavoro hello raggiunge nuovamente metodo async hello e viene riavviato, causando lavoro hello nuovamente anche toorecycle ruolo.

### <a name="solution"></a>Soluzione
Posizionare tutte le operazioni asincrone di fuori di hello [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo. Quindi, chiamare il metodo asincrono hello sottoposta a refactoring all'interno di hello [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) metodo, ad esempio .wait di RunAsync (). strumento di analisi del codice di Azure Hello può aiutare a risolvere il problema.

Hello seguente frammento di codice mostra correzione del codice hello per questo problema:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Autenticazione della firma di accesso condiviso con il bus di servizio
### <a name="id"></a>ID
AP2000

### <a name="description"></a>Descrizione
Uso della firma di accesso condiviso per l’autenticazione. Il servizio di controllo di accesso (ACS) è deprecato per l'autenticazione di bus di servizio.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Per una sicurezza ottimale, Azure Active Directory consiste nella sostituzione dell’autenticazione ACS con l'autenticazione SAS. Vedere [Azure Active Directory è hello futuro di ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) per informazioni sul piano di transizione hello.

### <a name="solution"></a>Soluzione
Utilizzare l'autenticazione SAS nelle app. Hello di esempio seguente viene illustrato come toouse un tooaccess token SAS esistente un servizio del bus di spazio dei nomi o entità.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Hello seguenti argomenti per ulteriori informazioni, vedere.

* Per una panoramica, vedere [autenticazione della firma di accesso condiviso con il bus di servizio](https://msdn.microsoft.com/library/dn170477.aspx)
* [Come toouse autenticazione della firma di accesso condiviso con il Bus di servizio](https://msdn.microsoft.com/library/dn205161.aspx)
* Per un progetto di esempio, vedere l'articolo relativo all' [autenticazione tramite firma di accesso condiviso con le sottoscrizioni del bus di servizio](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>È consigliabile utilizzare tooavoid metodo OnMessage "ciclo di ricezione"
### <a name="id"></a>ID
AP2002

### <a name="description"></a>Descrizione
tooavoid verso un "ciclo di ricezione," hello chiamante **OnMessage** metodo è una soluzione migliore per la ricezione di messaggi rispetto a chiamata hello **ricezione** metodo. Tuttavia, se è necessario utilizzare hello **ricezione** (metodo) e specificare un tempo di attesa del server non predefinito, assicurarsi che il tempo di attesa hello sia più di un minuto.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Quando si chiama **OnMessage**, client hello avvia un message pump interno che esegue il polling costantemente hello coda o sottoscrizione. Il message pump di contiene un ciclo infinito che effettua una chiamata tooreceive messaggi. Se il timeout della chiamata di hello, genera una nuova chiamata. intervallo di timeout Hello è determinata dal valore hello di hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) proprietà di hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)che viene utilizzato.

Hello vantaggio dell'utilizzo di **OnMessage** confrontati troppo**ricezione** è che gli utenti non hanno toomanually eseguire il polling per i messaggi, gestione delle eccezioni, elaborare più messaggi in parallelo e completare hello messaggi.

Se si chiama **ricezione** senza utilizzare il valore predefinito, essere hello che *ServerWaitTime* valore è superiore a un minuto. Impostazione *ServerWaitTime* toomore di un minuto impedisce server hello scadere prima completa ricezione del messaggio hello.

### <a name="solution"></a>Soluzione
Vedere hello seguono esempi di codice per gli utilizzi consigliati. Per altre informazioni, vedere [metodo QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e [metodo QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

prestazioni hello tooimprove di hello infrastruttura di messaggistica di Azure, vedere il modello di progettazione di hello [Introduzione alla messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).

Hello seguito è riportato un esempio di utilizzo **OnMessage** tooreceive messaggi.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Hello seguito è riportato un esempio di utilizzo **ricezione** con server predefinito hello tempo di attesa.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Hello seguito è riportato un esempio di utilizzo **ricezione** tempo di attesa con un server non predefinito.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Si consideri l'utilizzo di metodi asincroni del Bus di servizio
### <a name="id"></a>ID
AP2003

### <a name="description"></a>Descrizione
Utilizzare prestazioni tooimprove metodi di Service Bus asincrono con la messaggistica negoziata.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Utilizzare i metodi asincroni consente concorrenza delle applicazioni perché l'esecuzione di ogni chiamata non blocca il thread principale di hello. Quando si utilizzano i metodi di messaggistica del Bus di servizio, l’esecuzione di un'operazione (inviare, ricevere, eliminare, ecc) richiede tempo. Questo tempo include l'elaborazione di hello dell'operazione hello dal servizio Bus di servizio hello latenza toohello aggiunta di hello richiesta e risposta di hello. numero di hello tooincrease di operazioni per volta, le operazioni vengano eseguite simultaneamente. Per ulteriori informazioni, vedere troppo[procedure consigliate per prestazioni miglioramenti tramite servizio di messaggistica negoziata del Bus](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Soluzione
Vedere [classe QueueClient (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) per informazioni su come toouse hello consigliato metodo asincrono.

prestazioni hello tooimprove di hello infrastruttura di messaggistica di Azure, vedere il modello di progettazione di hello [Introduzione alla messaggistica asincrona](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Prendere in considerazione il partizionamento delle code e degli argomenti del bus di servizio.
### <a name="id"></a>ID
AP2004

### <a name="description"></a>Descrizione
Esegue il partizionamento delle code e degli argomenti del bus di servizio per ottenere prestazioni migliori con la messaggistica del bus di servizio.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Partizionamento di code e argomenti Service Bus aumenta la disponibilità di velocità effettiva e il servizio delle prestazioni perché hello velocità effettiva complessiva di una coda o argomento partizionato non è più limitata dalle prestazioni hello di un singolo broker messaggi o archivio di messaggistica. Una interruzione temporanea di un archivio di messaggistica non influisce sulla disponibilità di code e argomenti partizionati. Per ulteriori informazioni, vedere [Partizionamento delle entità di messaggistica](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Soluzione
Hello seguente frammento di codice viene illustrato come toopartition entità di messaggistica.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Per ulteriori informazioni, vedere [argomenti e code del Bus di servizio partizionati | Blog di Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) ed estrarre hello [coda partizionata di Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) esempio.

## <a name="do-not-set-sharedaccessstarttime"></a>Non impostare SharedAccessStartTime
### <a name="id"></a>ID
AP3001

### <a name="description"></a>Descrizione
Evitare di usare SharedAccessStartTimeset toohello corrente avvio tooimmediately hello criterio di accesso condiviso. È necessario solo tooset questa proprietà se si desidera criteri di accesso condiviso di toostart hello in un secondo momento.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
La sincronizzazione dell'orologio comporta una differenza oraria lieve tra i Data Center. Ad esempio, si potrebbe pensare ora di inizio hello di impostazione di un criterio di archiviazione SAS perché hello ora corrente usando Now o un metodo simile causerà l'effetto di hello SAS criteri tootake immediatamente. Tuttavia, le differenze di orario hello tra Data Center possono causare problemi con questo, a poiché alcuni Data Center potrebbero essere leggermente successiva all'ora di inizio di hello, mentre altri in anticipo. Di conseguenza, hello criterio SAS può scadere velocemente (o anche immediatamente) se durata criteri hello impostata è troppo breve.

Per ulteriori informazioni sull'uso di firma di accesso condiviso in archiviazione di Azure, vedere [introduzione tabella firma di accesso condiviso (firma di accesso condiviso) SAS coda aggiornamento tooBlob SAS - Blog del Team Microsoft Azure Storage - del sito e Home - blog MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Soluzione
Rimuovere l'istruzione hello che imposta l'ora di inizio hello dei criteri di accesso condiviso hello. strumento di analisi del codice di Azure Hello viene fornita una correzione per questo problema. Per ulteriori informazioni sulla gestione della sicurezza, vedere il modello di struttura hello [passepartout](https://msdn.microsoft.com/library/dn568102.aspx).

Hello frammento di codice seguente viene illustrato correzione del codice hello per questo problema.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>L’ora di scadenza del criterio di accesso condiviso deve essere più di cinque minuti 
### <a name="id"></a>ID
AP3002

### <a name="description"></a>Descrizione
Possono esistere fino a cinque minuti una differenza di orologi tra i Data Center in posizioni diverse, a causa di tooa condizione è nota come "sfasamento." token del criterio SAS hello tooprevent di scadenza precedente alla data di impostare hello scadenza ora toobe più di cinque minuti.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Data Center in posizioni diverse in tutto il mondo hello sincronizzare un segnale di clock. Poiché il tempo per i percorsi toodifferent tootravel segnale di clock, può esserci uno sfasamento di orario tra i Data Center in località geografiche diverse Sebbene tutto sia sincronizzato. Questa differenza temporale può avere implicazioni di accesso condiviso criteri inizio ora e scadenza intervallo hello. Pertanto, tooensure criterio di accesso condiviso diventa effettiva immediatamente, non specificare l'ora di inizio hello. Assicurarsi, inoltre, ora di scadenza hello è superiore al timeout anticipato tooprevent di 5 minuti.

Per ulteriori informazioni sull'uso della firma di accesso condiviso in archiviazione di Azure, vedere [introduzione tabella firma di accesso condiviso (firma di accesso condiviso) SAS coda aggiornamento tooBlob SAS - Blog del Team Microsoft Azure Storage - del sito e Home - blog MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Soluzione
Per ulteriori informazioni sulla gestione della sicurezza, vedere il modello di progettazione di hello [passepartout](https://msdn.microsoft.com/library/dn568102.aspx).

Hello Ecco un esempio non viene specificata un'ora di inizio dei criteri di accesso condiviso.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Hello Ecco un esempio di specificare un'ora di inizio dei criteri di accesso condiviso con una scadenza del criterio maggiore di cinque minuti.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Per ulteriori informazioni, [Creare e usare una firma di accesso condiviso](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>Utilizzare CloudConfigurationManager
### <a name="id"></a>ID
AP4000

### <a name="description"></a>Descrizione
Utilizzo di hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe per i progetti, ad esempio sito Web di Azure e servizi mobili di Azure non genera problemi di runtime. Come procedura consigliata, tuttavia, è toouse una buona idea Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) come una modalità unificata di gestione delle configurazioni per tutte le applicazioni Cloud di Azure.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
CloudConfigurationManager legge l'ambiente dell'applicazione hello configurazione file toohello appropriato.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Soluzione
Effettuare il refactoring del hello toouse codice [CloudConfigurationManager classe](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Una correzione del codice per questo problema viene fornita dallo strumento di analisi del codice di Azure hello.

Hello frammento di codice seguente viene illustrato correzione del codice hello per questo problema. Replace

`var settings = ConfigurationManager.AppSettings["mySettings"];`

con

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Di seguito è riportato un esempio di come toostore hello impostazione di configurazione in un file app. config o Web. config. Aggiungere una sezione appSettings di hello impostazioni toohello hello del file di configurazione. di seguito Hello è Web. config per il precedente esempio di codice hello hello.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Evitare di utilizzare stringhe di connessione hardcoded
### <a name="id"></a>ID
AP4001

### <a name="description"></a>Descrizione
Se si utilizzano stringhe di connessione hardcoded ed è necessario tooupdate loro in un secondo momento, si sarà toomake modifiche tooyour del codice sorgente e ricompilare l'applicazione hello. Tuttavia, se si archiviano le stringhe di connessione in un file di configurazione, è possibile modificarle successivamente semplicemente aggiornando il file di configurazione di hello.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Impostare come hardcoded le stringhe di connessione è sconsigliata perché si verificano problemi quando le stringhe di connessione è necessario modificare rapidamente toobe. Inoltre, se il progetto hello deve toobe selezionato nel controllo toosource, le stringhe di connessione hardcoded introducono vulnerabilità della sicurezza perché hello stringhe possono essere visualizzate nel codice sorgente hello.

### <a name="solution"></a>Soluzione
Archiviare le stringhe di connessione nel file di configurazione hello o ambienti di Azure.

* Per le applicazioni autonome, utilizzare le impostazioni della stringa di connessione toostore app. config.
* Per le applicazioni web ospitate in IIS, utilizzare le stringhe di connessione toostore Web. config.
* Per le applicazioni vNext ASP.NET, utilizzare le stringhe di connessione toostore configuration.json.

Per informazioni sull'uso di file di configurazione, ad esempio web.config o app. config, vedere [Linee guida configurazione di ASP.NET Web](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Per informazioni su come funzionano le variabili di ambiente di Azure, vedere [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/) (Siti Web di Microsoft Azure sul funzionamento delle stringhe di applicazione e di connessione). Per informazioni sull'archiviazione della stringa di connessione nel codice sorgente, vedere [evitare di inserire informazioni riservate come le stringhe di connessione nei file archiviati nel repository del codice sorgente](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Utilizzo del file di configurazione di Diagnostica.
### <a name="id"></a>ID
AP5000

### <a name="description"></a>Descrizione
Anziché configurare le impostazioni di diagnostica nel codice, ad esempio tramite hello Microsoft.WindowsAzure.Diagnostics API di programmazione, è necessario configurare le impostazioni di diagnostica nel file Diagnostics wadcfg hello. (O, diagnostics.wadcfgx se si utilizza Azure SDK 2.5). In questo modo, è possibile modificare le impostazioni di diagnostica senza toorecompile il codice.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Prima di Azure SDK 2.5 (che usa diagnostica di Azure 1.3), la diagnostica di Azure (WAD) è stato possibile configurare utilizzando diversi metodi: aggiungendola toohello blob di configurazione nella risorsa di archiviazione usando codice imperativo, una configurazione dichiarativa o default hello configurazione. Tuttavia, hello preferito modo tooconfigure diagnostica è un file di configurazione XML (Diagnostics. wadcfg o wadcfgx per SDK 2.5 e versioni successive) nel progetto di applicazione hello toouse. In questo approccio, il file Diagnostics wadcfg hello completamente definisce la configurazione di hello e possono essere aggiornate e ridistribuito come desiderato. Combinazione utilizzare hello del file di configurazione Diagnostics. wadcfg hello con hello metodi a livello di codice di impostazione delle configurazioni tramite hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)o [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classi possono causare tooconfusion. Vedere [Avviare o modificare la configurazione della diagnostica di Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) per ulteriori informazioni.

A partire da 1.3 WAD (incluso in Azure SDK 2.5), non è più diagnostica tooconfigure del codice toouse possibili. Di conseguenza, è possibile specificare solo configurazione hello quando l'applicazione o l'aggiornamento dell'estensione diagnostica hello.

### <a name="solution"></a>Soluzione
Utilizzare hello diagnostica toomove Progettazione impostazioni strumenti diagnostici toohello diagnostica configurazione file di configurazione (wadcfg o wadcfgx per SDK 2.5 e versioni successive). È inoltre consigliabile installare [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) e utilizzo funzionalità di diagnostica più recenti hello.

1. Nel menu di scelta rapida hello ruolo hello che si desidera tooconfigure, scegliere Proprietà e quindi scegliere la scheda di configurazione hello.
2. In hello **diagnostica** sezione, assicurarsi che tale hello **Abilita diagnostica** casella di controllo è selezionata.
3. Scegliere hello **configura** pulsante.

   ![Accesso opzione Abilita diagnostica hello](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Vedere [Configurazione della diagnostica per i servizi cloud e le macchine virtuali di Azure](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) .per ulteriori informazioni.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>Evitare di dichiarare gli oggetti DbContext come static
### <a name="id"></a>ID
AP6000

### <a name="description"></a>Descrizione
memoria toosave, evitare di dichiarare gli oggetti DBContext come statici.

Condividere le idee e i suggerimenti nei [Commenti e suggerimenti dell'analisi del codice di Azure](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Motivo
Gli oggetti DBContext contengono hello risultati della query da ogni chiamata. Gli oggetti DBContext statici non vengono eliminati fino a quando non viene scaricato il dominio di applicazione hello. Pertanto, un oggetto DBContext statico può utilizzare grandi quantità di memoria.

### <a name="solution"></a>Soluzione
Dichiarare DBContext come una variabile locale o un campo di istanza non statico, utilizzarlo per un'attività e poi eliminarlo dopo l'uso.

Hello classe controller MVC di esempio seguente viene illustrato come toouse hello oggetto DBContext.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Passaggi successivi
toolearn più sull'ottimizzazione e risoluzione dei problemi di App di Azure, vedere [risolvere i problemi relativi a un'app web nel servizio App di Azure con Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
