---
title: aaaGetting avviato con l'archiviazione delle code e Visual Studio (progetti processi Web) di servizi connessi | Documenti Microsoft
description: Come tooget iniziare a usare l'archiviazione delle code di Azure in un progetto processo Web dopo la connessione di account di archiviazione tooa utilizzando Visual Studio di servizi connessi.
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 5c3ef267-2a67-44e9-ab4a-1edd7015034f
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 47a446aa5c6bbf25526339823db4952ac1a8802f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-webjob-projects"></a>Introduzione all'archiviazione di accodamento di Azure e ai servizi relativi a Visual Studio (progetti WebJob)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Panoramica
Questo articolo viene descritto come ottenere avviato mediante Azure coda di archiviazione in un progetto processo Web di Visual Studio Azure dopo aver creato o riferimento a un account di archiviazione di Azure tramite hello Visual Studio **aggiungere servizi connessi** la finestra di dialogo. Quando si aggiunge un progetto di processo Web tooa account di archiviazione usando Visual Studio hello **aggiungere servizi connessi** finestra di dialogo, sono installati pacchetti NuGet di archiviazione di Azure appropriati hello, riferimenti .NET appropriati hello vengono aggiuntivo toohello progetto e stringhe di connessione per l'account di archiviazione hello vengono aggiornate nel file app. config hello.  

In questo articolo vengono forniti esempi di codice c# che mostrano come toouse hello Azure WebJobs SDK versione 1. x con il servizio di archiviazione di Azure coda hello.

Archiviazione delle code di Azure è un servizio per l'archiviazione di un numero elevato di messaggi che è possibile accedere da qualsiasi in HelloWorld tramite chiamate autenticate tramite HTTP o HTTPS. Può essere un messaggio nella coda singola too64 KB di dimensioni e una coda può contenere milioni di messaggi, il limite di capacità totale toohello di un account di archiviazione. Per altre informazioni, vedere [Introduzione all'archiviazione code di Azure con .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) . Per ulteriori informazioni su ASP.NET, vedere [ASP.NET](http://www.asp.net).

## <a name="how-tootrigger-a-function-when-a-queue-message-is-received"></a>Come tootrigger una funzione quando viene ricevuto un messaggio nella coda
chiama una funzione che hello WebJobs SDK toowrite quando viene ricevuto un messaggio nella coda, utilizzare hello **QueueTrigger** attributo. costruttore di attributo Hello accetta un parametro di stringa che specifica il nome di hello di hello coda toopoll. toosee come tooset hello nome della coda in modo dinamico, estrarre [come opzioni di configurazione tooset](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Messaggi stringa in coda
Nell'esempio seguente di hello, hello coda contiene una stringa di messaggio, pertanto **QueueTrigger** tooa applicato parametro di stringa denominato **logMessage** che comprende il contenuto di hello del messaggio della coda. funzione Hello [scrive un toohello messaggio log Dashboard](#how-to-write-logs).

        public static void ProcessQueueMessage([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            logger.WriteLine(logMessage);
        }

Oltre a **stringa**, il parametro hello può essere una matrice di byte, un **CloudQueueMessage** oggetto o un POCO definiti.

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Nell'esempio seguente di hello, messaggio della coda contiene JSON per un **BlobInformation** oggetto che include un **BlobName** proprietà. Hello SDK deserializza automaticamente oggetto hello.

        public static void WriteLogPOCO([QueueTrigger("logqueue")] BlobInformation blobInfo, TextWriter logger)
        {
            logger.WriteLine("Queue message refers tooblob: " + blobInfo.BlobName);
        }

Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi. Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "log.txt" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

### <a name="async-functions"></a>Funzioni asincrone
Hello seguente funzione async [scrive un toohello log Dashboard](#how-to-write-logs).

        public async static Task ProcessQueueMessageAsync([QueueTrigger("logqueue")] string logMessage, TextWriter logger)
        {
            await logger.WriteLineAsync(logMessage);
        }

Le funzioni asincrone potrebbero richiedere un [token di annullamento](http://www.asp.net/mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4#CancelToken), come illustrato nell'esempio che consente di copiare un blob seguente hello. (Per una spiegazione di hello **queueTrigger** segnaposto, vedere hello [BLOB](#how-to-read-and-write-blobs-and-tables-while-processing-a-queue-message) sezione.)

        public async static Task ProcessQueueMessageAsyncCancellationToken(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput,
            CancellationToken token)
        {
            await blobInput.CopyToAsync(blobOutput, 4096, token);
        }

## <a name="types-hello-queuetrigger-attribute-works-with"></a>Attributo di tipi hello QueueTrigger funziona con
È possibile utilizzare **QueueTrigger** con hello seguenti tipi:

* **string**
* Tipo POCO serializzato come JSON
* **byte[]**
* **CloudQueueMessage**

## <a name="polling-algorithm"></a>Algoritmo di polling
Hello SDK implementa un effetto di hello esponenziale Backoff algoritmo casuali tooreduce di inattività della coda del polling sui costi delle transazioni di archiviazione.  Quando viene trovato un messaggio, hello SDK attende due secondi e ne controlla la presenza di un altro messaggio. Quando viene trovato alcun messaggio rimane in attesa circa quattro secondi prima di riprovare. Dopo i tentativi non riusciti successivi tooget un messaggio nella coda, il tempo di attesa hello continua tooincrease finché raggiunge il tempo di attesa massimo hello, il minuto tooone valori predefiniti. [Hello tempo di attesa massimo è configurabile](#how-to-set-configuration-options).

## <a name="multiple-instances"></a>Più istanze
Se l'app web viene eseguito su più istanze, viene eseguito un processi Web continui in ogni computer e ogni computer tenterà di attesa per i trigger e funzioni toorun. Funzioni toosome elaborazione hello due volte, in alcuni scenari, che questo può causare stessi dati funzioni devono essere idempotenti (scritto in modo che chiama ripetutamente con stessi dati di input non producono hello duplicare risultati).  

## <a name="parallel-execution"></a>Esecuzione parallela
Se si dispongono di più funzioni in attesa in code diverse, hello SDK verrà chiamarli in parallelo quando vengono ricevuti i messaggi contemporaneamente.

Hello stesso vale quando vengono ricevuti più messaggi per una singola coda. Per impostazione predefinita, hello SDK riceve un batch di messaggi in coda 16 alla volta ed esegue funzione hello elaborarli in parallelo. [dimensioni del batch Hello sono configurabile](#how-to-set-configuration-options). Quando il numero di hello elaborato Ottiene verso il basso toohalf della dimensione di batch di hello, hello SDK riceve un altro batch e inizia l'elaborazione di tali messaggi. Numero massimo di hello simultanee messaggi vengano elaborati per ogni funzione pertanto è dimensioni di batch di una volta e mezza hello. Questo limite si applica separatamente tooeach funzione che ha un **QueueTrigger** attributo. Se non si desidera l'esecuzione parallela per i messaggi ricevuti su una coda, impostare too1 dimensioni di batch hello.

## <a name="get-queue-or-queue-message-metadata"></a>Ottenere i metadati della coda o del messaggio in coda
È possibile ottenere hello seguenti proprietà di messaggio mediante l'aggiunta di firma del metodo toohello parametri:

* **DateTimeOffset** expirationTime
* **DateTimeOffset** insertionTime
* **DateTimeOffset** nextVisibleTime
* **string** queueTrigger (contiene il testo del messaggio)
* **string** id
* **string** popReceipt
* **int** dequeueCount

Se si desidera toowork direttamente con hello API di archiviazione di Azure, è inoltre possibile aggiungere un **CloudStorageAccount** parametro.

Hello nell'esempio seguente vengono tutti il registro applicazioni di metadati tooan INFO. Nell'esempio hello logMessage sia queueTrigger contenuto hello di messaggio della coda hello.

        public static void WriteLog([QueueTrigger("logqueue")] string logMessage,
            DateTimeOffset expirationTime,
            DateTimeOffset insertionTime,
            DateTimeOffset nextVisibleTime,
            string id,
            string popReceipt,
            int dequeueCount,
            string queueTrigger,
            CloudStorageAccount cloudStorageAccount,
            TextWriter logger)
        {
            logger.WriteLine(
                "logMessage={0}\n" +
            "expirationTime={1}\ninsertionTime={2}\n" +
                "nextVisibleTime={3}\n" +
                "id={4}\npopReceipt={5}\ndequeueCount={6}\n" +
                "queue endpoint={7} queueTrigger={8}",
                logMessage, expirationTime,
                insertionTime,
                nextVisibleTime, id,
                popReceipt, dequeueCount,
                cloudStorageAccount.QueueEndpoint,
                queueTrigger);
        }

Di seguito è riportato un log di esempio scritto dal codice di esempio hello:

        logMessage=Hello world!
        expirationTime=10/14/2014 10:31:04 PM +00:00
        insertionTime=10/7/2014 10:31:04 PM +00:00
        nextVisibleTime=10/7/2014 10:41:23 PM +00:00
        id=262e49cd-26d3-4303-ae88-33baf8796d91
        popReceipt=AgAAAAMAAAAAAAAAfc9H0n/izwE=
        dequeueCount=1
        queue endpoint=https://contosoads.queue.core.windows.net/
        queueTrigger=Hello world!

## <a name="graceful-shutdown"></a>Arresto normale
Una funzione che viene eseguito in un processo Web continuo può accettare un **CancellationToken** parametro che consente di hello toonotify hello funzione del sistema operativo quando hello processo Web sta toobe terminato. È possibile utilizzare questo toomake di notifica che la funzione hello non causare l'interruzione imprevista in modo che i dati rimane in uno stato incoerente.

Hello seguente esempio viene illustrato come toocheck imminente chiusura processo Web in una funzione.

    public static void GracefulShutdownDemo(
                [QueueTrigger("inputqueue")] string inputText,
                TextWriter logger,
                CancellationToken token)
    {
        for (int i = 0; i < 100; i++)
        {
            if (token.IsCancellationRequested)
            {
                logger.WriteLine("Function was cancelled at iteration {0}", i);
                break;
            }
            Thread.Sleep(1000);
            logger.WriteLine("Normal processing for queue message={0}", inputText);
        }
    }

**Nota:** hello Dashboard potrebbe non visualizzare correttamente hello stato e l'output di funzioni che è stato arrestato.

Per altre informazioni, vedere l'articolo sull' [arresto normale dei processi Web](http://blog.amitapple.com/post/2014/05/webjobs-graceful-shutdown/#.VCt1GXl0wpR).   

## <a name="how-toocreate-a-queue-message-while-processing-a-queue-message"></a>Come toocreate una coda dei messaggi durante l'elaborazione di un messaggio nella coda
una funzione che crea un nuovo messaggio, utilizzare hello toowrite **coda** attributo. Ad esempio **QueueTrigger**, si passa il nome della coda hello sotto forma di stringa oppure è possibile [impostare dinamicamente il nome di coda hello](#how-to-set-configuration-options).

### <a name="string-queue-messages"></a>Messaggi stringa in coda
Hello non asincrona nell'esempio di codice seguente crea un nuovo messaggio nella coda di hello denominato "outputqueue" con stesso contenuto sotto forma di messaggio della coda di hello ricevuto nella coda di hello denominata "inputqueue" hello. Per le funzioni asincrone, usare **IAsyncCollector<T>** come illustrato più avanti in questa sezione.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] out string outputQueueMessage )
        {
            outputQueueMessage = queueMessage;
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
tipo di un messaggio nella coda che contiene un POCO anziché una stringa, passata hello POCO toocreate come un toohello di parametro di output **coda** costruttore di attributo.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] BlobInformation blobInfoInput,
            [Queue("outputqueue")] out BlobInformation blobInfoOutput )
        {
            blobInfoOutput = blobInfoInput;
        }

Hello SDK serializza automaticamente tooJSON oggetto hello. Viene sempre creato un messaggio nella coda, anche se l'oggetto hello è null.

### <a name="create-multiple-messages-or-in-async-functions"></a>Creare più messaggi o in funzioni asincrone
toocreate più messaggi, rendere il tipo di parametro hello per coda di output di hello **ICollector<T>**  o **IAsyncCollector<T>**, come illustrato nell'esempio seguente hello.

        public static void CreateQueueMessages(
            [QueueTrigger("inputqueue")] string queueMessage,
            [Queue("outputqueue")] ICollector<string> outputQueueMessage,
            TextWriter logger)
        {
            logger.WriteLine("Creating 2 messages in outputqueue");
            outputQueueMessage.Add(queueMessage + "1");
            outputQueueMessage.Add(queueMessage + "2");
        }

Ogni messaggio della coda viene creato immediatamente quando hello **Aggiungi** metodo viene chiamato.

### <a name="types-that-hello-queue-attribute-works-with"></a>Tipi di attributo coda hello funziona con
È possibile utilizzare hello **coda** attributo hello seguenti tipi di parametro:

* **stringa** (Crea messaggio della coda se il valore del parametro è diverso da null quando la funzione hello termina)
* **out byte** (funziona come **string**)
* **out CloudQueueMessage** (funziona come **string**)
* **out POCO** (un tipo serializzabile, crea un messaggio con un oggetto null, se il parametro hello è null quando la funzione hello termina)
* **ICollector**
* **IAsyncCollector**
* **CloudQueue** (per la creazione di messaggi manualmente utilizzando hello API di archiviazione di Azure direttamente)

### <a name="use-webjobs-sdk-attributes-in-hello-body-of-a-function"></a>Utilizzare gli attributi di WebJobs SDK nel corpo di hello di una funzione
Se è necessario toodo alcune funzionano nella funzione prima di utilizzare un attributo WebJobs SDK, ad esempio **coda**, **Blob**, o **tabella**, è possibile utilizzare hello **IBinder** interfaccia.

Hello di esempio seguente accetta un messaggio della coda di input e crea un nuovo messaggio con stesso contenuto in una coda di output di hello. nome della coda output Hello viene impostata dal codice nel corpo di hello della funzione hello.

        public static void CreateQueueMessage(
            [QueueTrigger("inputqueue")] string queueMessage,
            IBinder binder)
        {
            string outputQueueName = "outputqueue" + DateTime.Now.Month.ToString();
            QueueAttribute queueAttribute = new QueueAttribute(outputQueueName);
            CloudQueue outputQueue = binder.Bind<CloudQueue>(queueAttribute);
            outputQueue.AddMessage(new CloudQueueMessage(queueMessage));
        }

Hello **IBinder** interfaccia può essere utilizzata anche con hello **tabella** e **Blob** attributi.

## <a name="how-tooread-and-write-blobs-and-tables-while-processing-a-queue-message"></a>Come tooread e scrittura BLOB e tabelle durante l'elaborazione di un messaggio nella coda
Hello **Blob** e **tabella** gli attributi consentono di tooread e scrivere i BLOB e tabelle. esempi di Hello in questa sezione si applicano tooblobs. Per esempi di codice che mostrano come tootrigger elabora quando BLOB vengono creati o aggiornati, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)e per esempi di codice che leggono e scrivono le tabelle, vedere [come toouse tabelle di Azure archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-tables-how-to.md).

### <a name="string-queue-messages-triggering-blob-operations"></a>Messaggi di coda stringa che attivano operazioni BLOB
Per un messaggio nella coda che contiene una stringa, **queueTrigger** è un segnaposto che è possibile utilizzare in hello **Blob** dell'attributo **blobPath** parametro che contiene il contenuto di hello di messaggio Hello.

Hello seguente utilizza **flusso** oggetti BLOB tooread e di scrittura. messaggio della coda di Hello è il nome di hello di un blob nel contenitore textblobs hello. Una copia di blob hello con "-new" nome toohello accodato viene creato in hello stesso contenitore.

        public static void ProcessQueueMessage(
            [QueueTrigger("blobcopyqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}",FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new",FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello **Blob** attributo costruttore accetta un **blobPath** parametro che specifica il nome di blob e contenitore hello. Per ulteriori informazioni su questo segnaposto, vedere [toouse Azure come blob di archiviazione con hello WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md).

Quando attributo hello decora un **flusso** dell'oggetto, un altro parametro di costruttore specifica hello **FileAccess** modalità come lettura, scrittura o lettura/scrittura.

Hello esempio seguente viene utilizzato un **CloudBlockBlob** oggetto toodelete un blob. messaggio della coda di Hello è il nome di hello del blob hello.

        public static void DeleteBlob(
            [QueueTrigger("deleteblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}")] CloudBlockBlob blobToDelete)
        {
            blobToDelete.Delete();
        }

### <a name="poco-plain-old-clr-objecthttpenwikipediaorgwikiplainoldclrobject-queue-messages"></a>Messaggi di coda POCO [(Plain Old CLR Object](http://en.wikipedia.org/wiki/Plain_Old_CLR_Object))
Per POCO archiviato in formato JSON in messaggio hello in coda, è possibile utilizzare i segnaposto di nome di proprietà dell'oggetto hello in hello **coda** dell'attributo **blobPath** parametro. È anche possibile usare nomi di proprietà dei metadati di coda come segnaposto. Vedere [Ottenere i metadati della coda o del messaggio in coda](#get-queue-or-queue-message-metadata).

Hello esempio copia un blob tooa nuovo blob con un'estensione diversa. messaggio della coda di Hello è un **BlobInformation** oggetto che include **BlobName** e **BlobNameWithoutExtension** proprietà. i nomi delle proprietà Hello vengono utilizzati come segnaposto nel percorso blob hello per hello **Blob** attributi.

        public static void CopyBlobPOCO(
            [QueueTrigger("copyblobqueue")] BlobInformation blobInfo,
            [Blob("textblobs/{BlobName}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{BlobNameWithoutExtension}.txt", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

Hello SDK Usa hello [pacchetto NuGet newtonsoft. JSON](http://www.nuget.org/packages/Newtonsoft.Json) tooserialize e deserializzare i messaggi. Se si creano messaggi in coda in un programma che non utilizza hello WebJobs SDK, è possibile scrivere codice simile al seguente esempio toocreate un messaggio nella coda POCO hello che hello che SDK consente di analizzare.

        BlobInformation blobInfo = new BlobInformation() { BlobName = "boot.log", BlobNameWithoutExtension = "boot" };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        logQueue.AddMessage(queueMessage);

Se è necessario toodo alcuni nella funzione prima di associare un oggetto tooan blob, è possibile utilizzare attributo hello nel corpo di hello della funzione hello, come illustrato nella [attributi utilizzare WebJobs SDK nel corpo di una funzione di hello](#use-webjobs-sdk-attributes-in-the-body-of-a-function).

### <a name="types-you-can-use-hello-blob-attribute-with"></a>Tipi di dati hello Blob di attributo con
Hello **Blob** attributo può essere utilizzato con hello seguenti tipi:

* **Flusso** (lettura o scrittura, specificato utilizzando il parametro di costruttore FileAccess hello)
* **TextReader**
* **TextWriter**
* **string** (lettura)
* **stringa** (scrittura; crea un blob solo se il parametro di stringa hello è non null quando viene restituita la funzione hello)
* POCO (lettura)
* out POCO (scrivere; sempre creato un blob, come oggetto null se il parametro POCO è null quando viene restituita la funzione hello)
* **CloudBlobStream** (scrittura)
* **ICloudBlob** (lettura o scrittura)
* **CloudBlockBlob** (lettura o scrittura)
* **CloudPageBlob** (lettura o scrittura)

## <a name="how-toohandle-poison-messages"></a>Come messaggi non elaborabili toohandle
Messaggi il cui contenuto provoca un toofail funzione sono denominati *messaggi non elaborabili*. Quando la funzione hello non riesce, il messaggio di coda hello non viene eliminato e infine viene prelevato nuovamente, causando hello ciclo toobe ripetuto. Hello SDK automaticamente in grado di interrompere il ciclo di hello dopo un numero limitato di iterazioni o è possibile farlo manualmente.

### <a name="automatic-poison-message-handling"></a>Gestione automatica dei messaggi non elaborabili
Hello SDK chiama una funzione di too5 volte tooprocess un messaggio nella coda. Se non riesce try quinto hello, messaggio hello è la coda non elaborabile spostato tooa. È possibile vedere come tooconfigure hello numero massimo di tentativi in [come opzioni di configurazione tooset](#how-to-set-configuration-options).

coda non elaborabile Hello è denominata *{originalqueuename}*-messaggi non elaborabili. È possibile scrivere messaggi tooprocess un funzione dalla coda non elaborabile hello registrarle o inviando una notifica che è necessario un intervento manuale.

In seguito hello esempio hello **CopyBlob** function ha esito negativo quando un messaggio nella coda contiene il nome di hello di un blob che non esiste. In questo caso, il messaggio hello viene spostato dalla hello copyblobqueue toohello copyblobqueue poison coda. Hello **ProcessPoisonMessage** quindi registri hello messaggi non elaborabili.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput)
        {
            blobInput.CopyTo(blobOutput, 4096);
        }

        public static void ProcessPoisonMessage(
            [QueueTrigger("copyblobqueue-poison")] string blobName, TextWriter logger)
        {
            logger.WriteLine("Failed toocopy blob, name=" + blobName);
        }

Hello figura seguente Mostra output di console da queste funzioni durante l'elaborazione di un messaggio non elaborabile.

![Output di console per la gestione dei messaggi non elaborabili](./media/vs-storage-webjobs-getting-started-queues/poison.png)

### <a name="manual-poison-message-handling"></a>Gestione manuale dei messaggi non elaborabili
È possibile ottenere un numero di volte in cui è stato selezionato un messaggio per l'elaborazione di hello aggiungendo un **int** parametro denominato **dequeueCount** tooyour funzione. È possibile quindi controllo hello numero nel codice della funzione di rimozione dalla coda ed eseguire la propria gestione di messaggio non elaborabile quando il numero di hello supera una soglia, come illustrato nell'esempio seguente hello.

        public static void CopyBlob(
            [QueueTrigger("copyblobqueue")] string blobName, int dequeueCount,
            [Blob("textblobs/{queueTrigger}", FileAccess.Read)] Stream blobInput,
            [Blob("textblobs/{queueTrigger}-new", FileAccess.Write)] Stream blobOutput,
            TextWriter logger)
        {
            if (dequeueCount > 3)
            {
                logger.WriteLine("Failed toocopy blob, name=" + blobName);
            }
            else
            {
            blobInput.CopyTo(blobOutput, 4096);
            }
        }

## <a name="how-tooset-configuration-options"></a>Come le opzioni di configurazione tooset
È possibile utilizzare hello **JobHostConfiguration** hello tooset tipo le opzioni di configurazione seguenti:

* Impostare le stringhe di connessione SDK hello nel codice.
* Configurare le impostazioni di **QueueTrigger** , ad esempio il conteggio rimozione dalla coda.
* Ottenere i nomi delle code dalla configurazione.

### <a name="set-sdk-connection-strings-in-code"></a>Impostare le stringhe di connessione SDK nel codice
L'impostazione di stringhe di connessione SDK hello nel codice consente si toouse i propri nomi di stringa di connessione nel file di configurazione o le variabili di ambiente, come illustrato nell'esempio seguente hello.

        static void Main(string[] args)
        {
            var _storageConn = ConfigurationManager
                .ConnectionStrings["MyStorageConnection"].ConnectionString;

            var _dashboardConn = ConfigurationManager
                .ConnectionStrings["MyDashboardConnection"].ConnectionString;

            var _serviceBusConn = ConfigurationManager
                .ConnectionStrings["MyServiceBusConnection"].ConnectionString;

            JobHostConfiguration config = new JobHostConfiguration();
            config.StorageConnectionString = _storageConn;
            config.DashboardConnectionString = _dashboardConn;
            config.ServiceBusConnectionString = _serviceBusConn;
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="configure-queuetrigger--settings"></a>Configurare le impostazioni di QueueTrigger
È possibile configurare hello seguendo le impostazioni che si applicano toohello l'elaborazione del messaggio della coda:

* numero massimo di messaggi in coda che vengono prelevati contemporaneamente toobe eseguite in parallelo Hello (valore predefinito è 16).
* Hello numero massimo di tentativi prima che un messaggio nella coda venga inviato coda non elaborabile tooa (valore predefinito è 5).
* tempo di attesa massimo Hello prima polling nuovamente quando una coda è vuota (valore predefinito è 1 minuto).

Hello seguente esempio viene illustrato come tooconfigure queste impostazioni:

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.Queues.BatchSize = 8;
            config.Queues.MaxDequeueCount = 4;
            config.Queues.MaxPollingInterval = TimeSpan.FromSeconds(15);
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

### <a name="set-values-for-webjobs-sdk-constructor-parameters-in-code"></a>Impostare i valori per i parametri del costruttore WebJobs SDK nel codice
Talvolta si desidera toospecify un nome di coda, un nome di blob o contenitore o una tabella di nome in codice anziché a livello di codice. Ad esempio, è consigliabile toospecify hello nome della coda **QueueTrigger** in una variabile di ambiente o i file di configurazione.

È possibile farlo tramite il passaggio di un **NameResolver** oggetto toohello **JobHostConfiguration** tipo. Si includono segnaposto speciale racchiusi tra segni di percentuale (%) nei parametri di costruttore di attributo WebJobs SDK e **NameResolver** codice specifica toobe valori effettivi hello utilizzato al posto di questi segnaposto.

Ad esempio, si supponga che si desidera toouse una coda denominata logqueuetest nell'ambiente di test hello e uno denominato logqueueprod nell'ambiente di produzione. Anziché un nome di coda a livello di codice, si desidera nome hello toospecify di una voce in hello **appSettings** raccolta aventi il nome di coda effettivo hello. Se hello **appSettings** chiave logqueue, la funzione potrebbe essere analogo al seguente esempio hello.

        public static void WriteLog([QueueTrigger("%logqueue%")] string logMessage)
        {
            Console.WriteLine(logMessage);
        }

Il **NameResolver** classe quindi è stato possibile ottenere il nome della coda hello da **appSettings** come illustrato nell'esempio seguente hello:

        public class QueueNameResolver : INameResolver
        {
            public string Resolve(string name)
            {
                return ConfigurationManager.AppSettings[name].ToString();
            }
        }

Si passa hello **NameResolver** classe toohello **JobHost** come mostrato nel seguente esempio hello.

        static void Main(string[] args)
        {
            JobHostConfiguration config = new JobHostConfiguration();
            config.NameResolver = new QueueNameResolver();
            JobHost host = new JobHost(config);
            host.RunAndBlock();
        }

**Nota:** coda, tabella e i nomi di blob vengono risolti ogni volta che viene chiamata una funzione, ma i nomi dei contenitori blob vengono risolti solo quando viene avviata un'applicazione hello. È possibile modificare il nome di contenitore blob mentre è in esecuzione il processo di hello.

## <a name="how-tootrigger-a-function-manually"></a>Come una funzione tootrigger manualmente
una funzione tootrigger manualmente, utilizzare hello **chiamare** o **CallAsync** metodo hello **JobHost** oggetto e hello **NoAutomaticTrigger** attributo nella funzione hello, come illustrato nell'esempio seguente hello.

        public class Program
        {
            static void Main(string[] args)
            {
                JobHost host = new JobHost();
                host.Call(typeof(Program).GetMethod("CreateQueueMessage"), new { value = "Hello world!" });
            }

            [NoAutomaticTrigger]
            public static void CreateQueueMessage(
                TextWriter logger,
                string value,
                [Queue("outputqueue")] out string message)
            {
                message = value;
                logger.WriteLine("Creating queue message: ", message);
            }
        }

## <a name="how-toowrite-logs"></a>Modalità di registrazione toowrite
Hello Dashboard Mostra i registri in due posizioni: la pagina hello per processo Web hello e hello per una chiamata a un particolare processo Web.

![Log nella pagina del processo Web](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Output dei metodi di Console che si chiama una funzione o hello **Main ()** metodo verrà visualizzato nella pagina Dashboard hello per hello processo Web, non nella pagina hello per una chiamata di metodo specifico. Verrà visualizzato l'output dall'oggetto TextWriter hello che si ottiene da un parametro nella firma del metodo nella pagina Dashboard hello per una chiamata al metodo.

Output della console non può essere chiamata al metodo particolare tooa collegato perché hello Console è a thread singolo, mentre molte funzioni di processo potrebbero essere in esecuzione hello contemporaneamente. Per tale motivo hello SDK fornisce a ogni chiamata di funzione con il proprio oggetto writer di log univoco.

toowrite [registri di traccia delle applicazioni](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#logsoverview), utilizzare **console** (Crea registri contrassegnati come INFO) e **Console.Error** (Crea log contrassegnato come errore). In alternativa, è toouse [traccia o TraceSource](http://blogs.msdn.com/b/mcsuksoldev/archive/2014/09/04/adding-trace-to-azure-web-sites-and-web-jobs.aspx), che fornisce Verbose, avviso, e i livelli di tooInfo aggiunta e di errore critico. Registri di traccia delle applicazioni vengono visualizzati nel file di log di hello web app, le tabelle di Azure, o oggetti BLOB di Azure a seconda di come si configura l'app web di Azure. Come nel caso di tutti gli output di Console, i registri applicazione 100 più recente di hello vengono inoltre visualizzati nella pagina Dashboard hello hello processo Web, la pagina di hello non per una chiamata di funzione.

Output della console viene visualizzato in hello Dashboard solo se il programma hello è in esecuzione in un processo Web di Azure, non se il programma hello viene eseguito localmente o in altri ambienti di rete.

È possibile disabilitare la registrazione impostando hello Dashboard connessione stringa toonull. Per ulteriori informazioni, vedere [come opzioni di configurazione tooset](#how-to-set-configuration-options).

Hello esempio seguente vengono illustrati vari modi toowrite log:

        public static void WriteLog(
            [QueueTrigger("logqueue")] string logMessage,
            TextWriter logger)
        {
            Console.WriteLine("Console.Write - " + logMessage);
            Console.Out.WriteLine("Console.Out - " + logMessage);
            Console.Error.WriteLine("Console.Error - " + logMessage);
            logger.WriteLine("TextWriter - " + logMessage);
        }

Nel Dashboard di processi Web SDK hello, hello output di hello **TextWriter** viene visualizzato quando si passa toohello pagina per una particolare chiamata di funzione e selezionarla oggetti **attiva/disattiva Output**:

![Collegamento della chiamata](./media/vs-storage-webjobs-getting-started-queues/dashboardinvocations.png)

![Log nella pagina di una chiamata di funzione](./media/vs-storage-webjobs-getting-started-queues/dashboardlogs.png)

Nel Dashboard di processi Web SDK hello, righe hello 100 più recente della Console l'output Mostra backup quando accede pagina toohello per hello processo Web (non per la chiamata di funzione hello) e selezionare **attiva/disattiva Output**.

![Attiva/Disattiva Output](./media/vs-storage-webjobs-getting-started-queues/dashboardapplogs.png)

In un processo Web continuo, log applicazioni visualizzati nella/dati processi/continua/*{webjobname}*/job_log.txt nel file system di hello web app.

        [09/26/2014 21:01:13 > 491e54: INFO] Console.Write - Hello world!
        [09/26/2014 21:01:13 > 491e54: ERR ] Console.Error - Hello world!
        [09/26/2014 21:01:13 > 491e54: INFO] Console.Out - Hello world!

In un'applicazione hello blob di Azure registri simile al seguente: 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738373502,0,17404,17,Console.Write - Hello world!, 2014-09-26T21:01:13, errore, contosoadsnew, 491e54, 635473620738373502,0,17404,19,console.Error - Hello world!, 2014-09-26T21:01:13,Information,contosoadsnew,491e54,635473620738529920,0,17404,17,Console.Out - Hello world!,

In un hello tabella Azure **console** e **Console.Error** registri è simile al seguente:

![Log delle informazioni nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableinfo.png)

![Log degli errori nella tabella](./media/vs-storage-webjobs-getting-started-queues/tableerror.png)

## <a name="next-steps"></a>Passaggi successivi
In questo articolo ha fornito codice di esempio che mostrano come toohandle scenari comuni per l'utilizzo di code di Azure. Per ulteriori informazioni su come toouse processi Web di Azure e hello WebJobs SDK, vedere [risorse della documentazione di processi Web di Azure](http://go.microsoft.com/fwlink/?linkid=390226).

