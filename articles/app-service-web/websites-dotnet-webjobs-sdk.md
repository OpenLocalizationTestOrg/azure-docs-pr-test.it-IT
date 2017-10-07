---
title: "aaaWhat è hello Azure WebJobs SDK"
description: "Un'introduzione toohello Azure WebJobs SDK. Illustra quali hello SDK, gli scenari tipici, che è utile per, e gli esempi di codice."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Che cos'è Azure WebJobs SDK hello
## <a id="overview"></a>Panoramica
Questo articolo spiega cosa hello WebJobs SDK è, esamina alcuni scenari è utile per e fornisce una panoramica delle modalità di utilizzo nel codice.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Processi Web](websites-webjobs-resources.md) è una funzionalità di Azure App Service che consente di toorun un programma o script in hello stesso contesto di un'app web, l'app per le API o app per dispositivi mobili. scopo di hello Hello [WebJobs SDK](websites-webjobs-resources.md) è toosimplify hello codice scritto per attività comuni che possono eseguire un processo Web, ad esempio l'elaborazione di immagini, l'elaborazione della coda, aggregazione RSS, manutenzione di file e l'invio di messaggi di posta elettronica. Hello WebJobs SDK include funzionalità per l'utilizzo di archiviazione di Azure e Bus di servizio per la pianificazione di attività e la gestione degli errori e per molti altri scenari comuni. Inoltre, è progettato toobe estendibile. Hello [WebJobs SDK è open source](https://github.com/Azure/azure-webjobs-sdk/)ed è presente un [repository del codice sorgente aperta per le estensioni](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Hello WebJobs SDK include hello seguenti componenti:

* **Pacchetti NuGet**. I pacchetti NuGet aggiungere il progetto di applicazione Console di Visual Studio tooa forniscono un framework che il codice utilizza dichiarando i metodi con attributi WebJobs SDK.
* **Dashboard**. Parte di hello WebJobs SDK è incluso in Azure App Service e fornisce monitoraggio avanzato e diagnostica per programmi che utilizzano i pacchetti NuGet hello. Non è necessario toowrite codice toouse queste funzionalità di monitoraggio e diagnostica.

## <a id="scenarios"></a>Scenari
Ecco alcuni scenari tipici, che è possibile gestire più facilmente con hello Azure WebJobs SDK:

* Elaborazione di immagini o altre operazioni con un uso intensivo della CPU. Una funzionalità comune dei siti Web è hello possibilità tooupload immagini o video. Spesso si desidera contenuto hello toomanipulate dopo che è stato caricato, ma non si desidera toomake hello utente attesa durante tale scopo.
* Elaborazione di code. Un modo comune per un toocommunicate front-end web con un servizio back-end è toouse code. Sito Web di hello deve tooget lavoro svolto, inviare un messaggio in una coda. Un servizio back-end estrae i messaggi dalla coda hello e hello lavoro. È possibile utilizzare le code per l'elaborazione di immagini: ad esempio, dopo che l'utente di hello carica un numero di file, inserire i nomi di file hello in un toobe messaggio coda prelevati dal back-end hello per l'elaborazione. In alternativa, è possibile usare la velocità di risposta di code tooimprove del sito. Ad esempio, invece di scrivere direttamente il database SQL tooa, tooa coda di scrittura, informa l'utente di hello termine e consentire di lavorare database relazionale di hello back-end del servizio handle con latenza elevata. Per un esempio della coda di elaborazione con il processo di immagine, vedere hello [WebJobs SDK iniziare esercitazione](websites-dotnet-webjobs-sdk-get-started.md).
* Aggregazione RSS. Se si dispone di un sito che gestisce un elenco di feed RSS, è possibile effettuare il pull in tutti gli articoli di hello dai feed hello in un processo in background.
* Manutenzione di file, ad esempio aggregazione o pulizia di file di log.  Si possono avere file di log viene creati da più siti o per separato intervalli di tempo che si desidera toocombine in ordine toorun i processi di analisi su di essi. Oppure si potrebbe desiderare tooschedule un tooclean settimanale toorun di attività dei vecchi file di log.
* Ingresso alle tabelle di Azure. Si potrebbe disporre i file archiviati e i BLOB e si desidera tooparse li e archiviare i dati di hello nelle tabelle. funzione di Hello in ingresso può essere scritto un numero elevato di righe (in alcuni casi, milioni) e hello WebJobs SDK rende possibili tooimplement questa funzionalità con facilità. Hello SDK fornisce inoltre il monitoraggio in tempo reale degli indicatori di stato di avanzamento, ad esempio il numero di hello di righe scritte nella tabella hello.
* Altre attività a esecuzione prolungata che si desidera toorun in un thread in background, ad esempio [l'invio di messaggi di posta elettronica](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Le attività che si desidera toorun in una pianificazione, ad esempio eseguire un'operazione di backup ogni notte.

In molti di questi scenari è tooscale un toorun app web in più macchine virtuali, che è necessario eseguire contemporaneamente più processi Web. In alcuni scenari, ciò potrebbe causare hello stessi dati in fase di elaborazione più volte, ma questo non è un problema quando si usa coda incorporato hello, blob e trigger di Bus di servizio di hello WebJobs SDK. Hello SDK assicura che le funzioni verranno elaborate solo una volta per ogni messaggio o di un blob.

Hello WebJobs SDK rende facile toohandle scenari comuni di gestione degli errori. È possibile impostare avvisi toosend notifiche quando una funzione non riesce, ed è possibile impostare i timeout in modo che una funzione viene automaticamente annullata se non completata entro un limite di tempo specificato.

## <a id="code"></a> Esempi di codice
codice Hello per la gestione delle attività tipiche che funzionano con l'archiviazione di Azure è semplice. Nell'applicazione Console `Main` metodo crei un `JobHost` oggetto che coordina hello chiama toomethods si scrive. Hello WebJobs SDK framework conosce toocall i metodi e i valori di parametro toouse hello WebJobs SDK in base attributi quando si utilizza in essi contenuti. Hello SDK fornisce *trigger* che consente di specificare quali condizioni hanno causato toobe funzione hello chiamato, e *raccoglitori* che consente di specificare la modalità tooget informazioni da e verso i parametri di metodo.

Ad esempio, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) attributo causa toobe una funzione chiamata quando viene ricevuto un messaggio in una coda, e se il formato di messaggio hello JSON per una matrice di byte o un tipo personalizzato, il messaggio hello viene automaticamente deserializzato. Hello [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) attributo avvia un processo ogni volta che viene creato un nuovo blob in un account di archiviazione di Azure.

Ecco un semplice programma che esegue il polling di una coda e crea un BLOB per ogni messaggio in coda ricevuto:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

Hello `JobHost` oggetto è un contenitore per un set di funzioni di sfondo. Hello `JobHost` oggetto Monitor hello funzioni, controlla gli eventi che attivano le ed esegue le funzioni hello quando si verificano gli eventi del trigger. Si chiama un `JobHost` tooindicate metodo se si desidera hello contenitore processo toorun hello thread corrente o un thread in background. Nell'esempio hello hello `RunAndBlock` metodo esegue il processo di hello in modo continuo sul thread corrente hello.

Poiché hello `ProcessQueueMessage` metodo in questo esempio ha un `QueueTrigger` attributo trigger hello per tale funzione è la ricezione di hello di un nuovo messaggio nella coda. Hello `JobHost` oggetto verifica la presenza di nuovi messaggi in coda nella coda specificata hello ("webjobsqueue" in questo esempio) e quando ne viene trovato, chiama il metodo `ProcessQueueMessage`. 

Hello `QueueTrigger` attributo associa hello `inputText` toohello valore del parametro di messaggio della coda hello. Hello e `Blob` attributo associa un `TextWriter` oggetto tooa denominati "blobname" in un contenitore denominato "containername".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

funzione Hello utilizza quindi tale valore hello toowrite di parametri di un blob toohello coda messaggio hello:

        writer.WriteLine(inputText);

funzionalità di trigger e strumento di associazione di Hello di hello WebJobs SDK semplificano notevolmente codice hello è toowrite. Hello di basso livello di codice necessario tooprocess code, BLOB, o file o le attività tooinitiate pianificato, viene eseguita automaticamente da hello framework WebJobs SDK. Ad esempio, framework hello crea code che non esistono ancora, verrà visualizzata la coda di hello, operazioni di lettura coda di messaggi, eliminazioni accoda i messaggi durante l'elaborazione è stata completata, vengono creati i contenitori di blob che non esistono ancora, scrive tooblobs e così via.

Hello esempio di codice seguente viene illustrata un'ampia gamma di trigger in un processo Web: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, e `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a> Pianificazione
Hello `TimerTrigger` attributo offre hello possibilità tootrigger funzioni toorun in una pianificazione. È possibile pianificare un processo Web come un intero tramite Azure o pianificazione singole funzioni di un processo Web usando hello WebJobs SDK `TimerTrigger`. Ecco un esempio di codice.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Per ulteriori esempi di codice, vedere [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) nel repository di estensioni del sdk di processi Web azure hello in GitHub.com.

## <a name="extensibility"></a>Estensibilità
Non è limitati toobuilt-in - funzionalità hello WebJobs SDK consente trigger personalizzati toowrite e gestori di associazione.  Ad esempio, è possibile scrivere trigger per gli eventi della cache e le pianificazioni periodiche. Un [repository del codice sorgente aprire](https://github.com/Azure/azure-webjobs-sdk-extensions) contiene un [Guida dettagliata sulla extensibility WebJobs SDK](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) e toohelp codice di esempio consentono di iniziare la scrittura di trigger e gestori di associazione personalizzati.

## <a id="workerrole"></a>Utilizzo di hello WebJobs SDK di fuori di processi Web
Un programma che utilizza hello hello WebJobs SDK è un'applicazione Console standard e possono essere eseguite dovunque - toorun non dispone di un processo Web. È possibile testare il programma hello in locale nel computer di sviluppo e nell'ambiente di produzione che è possibile eseguirlo in un ruolo di lavoro del servizio Cloud o un servizio Windows se si preferisce uno di questi ambienti. 

Tuttavia, il dashboard di hello è disponibile solo come un'estensione per un'app web di servizio App di Azure. Se si desidera toorun di fuori di un processo Web e continuare a utilizzare hello Dashboard, è possibile configurare una web app toouse hello stesso account di archiviazione che si intende la stringa di connessione di processi Web SDK Dashboard e i Dashboard di processi Web dell'app web verranno quindi visualizzati i dati sulla funzione esecuzione dal programma di cui è in esecuzione in un'altra posizione. È possibile ottenere toohello Dashboard usando hello URL https://*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Per ulteriori informazioni, vedere [ottenere un dashboard per lo sviluppo locale con hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ma si noti che il post di blog di hello Mostra un nome di stringa di connessione precedente. 

## <a id="nostorage"></a>Funzionalità del dashboard
anche se non si usa WebJobs SDK trigger o gestori di associazione, Hello WebJobs SDK offre diversi vantaggi:

* È possibile richiamare funzioni da hello Dashboard.
* È possibile riprodurre le funzioni da hello Dashboard.
* È possibile visualizzare i registri nel Dashboard, toohello collegato hello processo Web particolare (scrittura dei log applicazioni, utilizzando la console, Console.Error, traccia e così via) o collegati toohello chiamata di funzione specifica che le ha generate (log scritto utilizzando un `TextWriter` oggetto che hello che SDK passa toohello funzione come parametro). 

Per ulteriori informazioni, vedere [come toomanually richiamare una funzione](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) e [modalità di registrazione toowrite](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Passaggi successivi
Per ulteriori informazioni su hello WebJobs SDK, vedere [risorse consigliato processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

Per informazioni più recenti miglioramenti toohello di hello WebJobs SDK, vedere hello [note sulla versione](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

