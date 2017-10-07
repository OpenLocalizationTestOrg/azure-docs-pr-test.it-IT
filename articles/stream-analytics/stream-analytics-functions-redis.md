---
title: l'elaborazione in tempo reale aaaStream Analitica per le funzioni di Azure | Documenti Microsoft
description: "Informazioni su modalità di connessione di una coda del Bus di servizio, una Cache Redis di Azure dall'output di hello di un processo di flusso Analitica toopopulate toouse una funzione di Azure."
keywords: flusso di dati, cache redis, coda bus di servizio
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: 
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: 5ef4fe76c2cadf896a80eeaf421f010c315918af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toostore-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a>Come dati toostore Analitica di flusso di Azure in una Cache di Redis di Azure utilizzando le funzioni di Azure
Analitica di flusso di Azure consente di sviluppare e distribuire informazioni in tempo reale di soluzioni a basso costo toogain da dispositivi, sensori, infrastruttura e le applicazioni o qualsiasi flusso di dati rapidamente. Ciò consente vari casi di utilizzo, tra cui: monitoraggio e gestione in tempo reale, comando e controllo, rilevamento di frodi, automobili connesse e molti altri. In molti scenari, è consigliabile toostore dati restituiti da Azure Analitica di flusso in un archivio dati distribuiti, ad esempio una cache Redis di Azure.

Immaginare di far parte di una società di telecomunicazioni. Si sta tentando di frode SIM toodetect in più chiamate provenienti da hello stessa identità, in hello stesso tempo, ma in diverse località geografiche percorsi. Si desidera archiviare tutti hello potenzialmente illecite telefonate in una cache Redis di Azure. In questo blog, vengono fornite le indicazioni su come è possibile completare tale operazione. 

## <a name="prerequisites"></a>Prerequisiti
Hello completo [in tempo reale la rilevazione di frodi] [ fraud-detection] procedura dettagliata per ASA

## <a name="architecture-overview"></a>Panoramica dell'architettura
![Schermata dell'architettura](./media/stream-analytics-functions-redis/architecture-overview.png)

Come illustrato nella figura precedente hello, Analitica di flusso consente il flusso di dati di input toobe eseguire una query e inviati tooan output. Basati sull'output di hello, funzioni di Azure può quindi attivare un tipo di evento. 

In questo blog, è lo stato attivo sulla parte di Azure funzioni hello della pipeline o hello in particolare l'attivazione di un evento che archivia i dati fraudolenti nella cache di hello.
Dopo aver completato hello [in tempo reale la rilevazione di frodi] [ fraud-detection] esercitazione, è un input (un hub di eventi), una query e un output (archiviazione blob) già configurato e in esecuzione. In questo blog, abbiamo modificare hello output toouse una coda del Bus di servizio. Successivamente, la connessione è una coda di toothis della funzione di Azure. 

## <a name="create-and-connect-a-service-bus-queue-output"></a>Creare e collegare un output della coda di del bus di servizio
toocreate una coda del Bus di servizio, seguire i passaggi 1 e 2 della sezione .NET hello [Introduzione a code di Service Bus][servicebus-getstarted].
Ora si connettono hello coda toohello Analitica flusso processo è stato creato in hello precedente procedura dettagliata di rilevamento di frodi.

1. Nel portale di Azure hello, passare toohello **output** pannello del processo e selezionare **Aggiungi** nella parte superiore di hello della pagina hello.
   
    ![Aggiunta di output](./media/stream-analytics-functions-redis/adding-outputs.png)
2. Scegliere **coda di Service Bus** come hello **Sink** e seguire le istruzioni di hello nella schermata di hello. Che toochoose hello uno spazio dei nomi di hello coda del Bus di servizio è stato creato in [Introduzione a code di Service Bus][servicebus-getstarted]. Al termine, fare clic su pulsante "right" hello.
3. Specificare i seguenti valori hello:
   
   * **Formato serializzatore eventi**: JSON
   * **Codifica**: UTF8
   * **FORMATO**: riga separata
4. Fare clic su hello **crea** pulsante tooadd l'origine ed tooverify Analitica di flusso che può connettersi toohello account di archiviazione.
5. In hello **Query** scheda, sostituire la query corrente hello con hello seguente. Sostituire * YOUR NAME BUS di servizio * con il nome di output di hello creato nel passaggio 3. 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a>Creare una cache Redis di Azure
Creare una cache Redis di Azure eseguendo la seguente sezione .NET hello [come tooUse Cache Redis di Azure] [ use-rediscache] fino alla sezione hello ***configurare i client della cache di hello***.
Al termine dell'operazione, è disponibile una nuova cache Redis. In **tutte le impostazioni**selezionare **le chiavi di accesso** e annotare hello ***stringa di connessione primaria***.

![Schermata dell'architettura](./media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a>Creare una funzione di Azure
Seguire [creare la prima funzione Azure] [ functions-getstarted] tooget esercitazione introduttiva funzioni di Azure. Se si dispone già di una funzione di Azure viene ad esempio toouse, quindi andare troppo[tooRedis Cache di scrittura](#Writing-to-Redis-Cache)

1. Nel portale di hello, selezionare servizi App dal riquadro di spostamento a sinistra hello, quindi fare clic su sito Web di app la funzione Azure app nome tooget toohello della funzione.
    ![Schermata dell'elenco di funzioni dei servizi app](./media/stream-analytics-functions-redis/app-services-function-list.png)
2. Fare clic su **Nuova funzione > ServiceBusQueueTrigger – C#**. Per hello campi seguenti, seguire queste istruzioni:
   
   * **Nome della coda**: hello stesso nome come nome di hello immesso al momento della creazione della coda di hello in [Introduzione a code di Service Bus] [ servicebus-getstarted] (non nome hello del bus di servizio hello). Assicurarsi di utilizzare coda hello toohello connesso Analitica di flusso di output.
   * **Connessione del bus di servizio**: selezionare **Aggiungere una stringa di connessione**. stringa di connessione hello toofind, andare toohello portale classico, selezionare **Bus di servizio**, bus di servizio è stato creato, hello e **informazioni di connessione** in basso hello hello. Verificare che la schermata principale hello, in questa pagina. Copiare e incollare la stringa di connessione hello. È gratuito tooenter qualsiasi nome di connessione.
     
       ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/servicebus-connection.png)
   * **AccessRights**: scegliere **Gestisci**
3. Fare clic su **Crea**

## <a name="writing-tooredis-cache"></a>TooRedis scrittura Cache
A questo punto è stata creata una funzione di Azure leggibile dalla coda del bus di servizio. Tutto ciò che viene lasciato toodo è utilizzare la funzione toowrite questo toohello dati Cache Redis. 

1. Selezionare il nuovo **ServiceBusQueueTrigger**, fare clic su **funzione impostazioni app** su hello angolo superiore destro. Selezionare **Vai tooApp servizio impostazioni > Impostazioni > Impostazioni applicazione**
2. Nella sezione delle stringhe di connessione hello, creare un nome in hello **nome** sezione. Incollare una stringa di connessione primaria hello trovato in hello **creare una Cache Redis** Esegui istruzione hello **valore** sezione. Selezionare **Personalizzato** per **Database SQL**.
3. Fare clic su **salvare** nella parte superiore di hello.
   
    ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/function-connection-string.png)
4. Tornare toohello impostazioni di servizio App e selezionare **strumenti > Editor di servizio App (anteprima) > su > passare**.
   
    ![Schermata di connessione al bus di servizio](./media/stream-analytics-functions-redis/app-service-editor.png)
5. In un editor di propria scelta, creare un file JSON denominato **Project** con hello seguente e salvarlo su disco locale tooyour.
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. Caricare il file nella directory radice hello della funzione (non WWWROOT). Dovrebbe essere un file denominato **lock** vengono visualizzati automaticamente, per confermare che hello Nuget pacchetti "Stackexchange" e "Newtonsoft. JSON" sono stati importati.
7. In hello **run.csx** file, sostituire codice generati in precedenza hello con hello seguente codice. Nella funzione lazyConnection hello, sostituire "CONN NAME" con il nome di hello creato nel passaggio 2 di **archiviare i dati nella cache di hello Redis**.

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers tooa property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract hello time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using hello cache object...
        // Simple put of integral data types into hello cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from hello cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect toohello Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-hello-stream-analytics-job"></a>Avviare il processo di flusso Analitica hello
1. Avviare un'applicazione hello telcodatagen.exe. utilizzo di Hello è come segue:````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````
2. Dal Pannello di processo di flusso Analitica hello nel portale di hello, fare clic su **avviare** nella parte superiore di hello della pagina hello.
   
    ![Schermata del processo di avvio](./media/stream-analytics-functions-redis/starting-job.png)
3. In hello **inizio processo** pannello viene visualizzato, selezionare **ora** e quindi fare clic su hello **avviare** pulsante in basso hello hello. stato del processo di Hello diventa tooStarting e tardi tooRunning le modifiche.
   
    ![Schermata di selezione dell'ora del processo di avvio](./media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a>Eseguire la soluzione e verificarne i risultati
Se si torna indietro tooyour **ServiceBusQueueTrigger** pagina, dovrebbe essere istruzioni di log. Questi log indicano che un elemento ottenuto dal hello coda di Service Bus, inserirlo nel database di hello e viene recuperato utilizzando ora hello come chiave hello!

tooverify che i dati sono in cache Redis, Vai a pagina di cache Redis tooyour nel nuovo portale di hello (come mostrato nella precedente hello [creare una Cache Redis di Azure](#Create-an-Azure-Redis-Cache) passaggio) e selezionare Console.

È ora possibile scrivere Redis comandi tooconfirm che siano effettivamente nella cache di hello.

![Schermata della console Redis](./media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a>Passaggi successivi
Siamo entusiasti di nuovi elementi di hello Azure funzioni analitica di flusso è possibile eseguire insieme e ci auguriamo che questa operazione sblocca nuove possibilità per l'utente. Se si dispone di commenti al successivo come si desidera, è possibile toouse libero hello [sito UserVoice Azure](https://feedback.azure.com/forums/270577-stream-analytics).

Nel caso di nuova versione di Microsoft Azure, la invitiamo tootry out per registrarsi per un [senza account di valutazione Azure](https://azure.microsoft.com/pricing/free-trial/). Se si è nuovo tooStream Analitica, quindi vi invitiamo troppo[creare il primo processo di flusso Analitica](stream-analytics-create-a-job.md).

In caso di domande o per ricevere assistenza, pubblicare un messaggio nel forum [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) o [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics). 

È inoltre possibile visualizzare hello seguenti risorse:

* [Guida di riferimento per gli sviluppatori di Funzioni di Azure](../azure-functions/functions-reference.md)
* [Guida di riferimento per gli sviluppatori C# di Funzioni di Azure](../azure-functions/functions-reference-csharp.md)
* [Guida di riferimento per gli sviluppatori di Funzioni di Azure in F#](../azure-functions/functions-reference-fsharp.md)
* [Guida di riferimento per gli sviluppatori NodeJS di Funzioni di Azure](../azure-functions/functions-reference.md)
* [Trigger e associazioni di Funzioni di Azure](../azure-functions/functions-triggers-bindings.md)
* [La modalità di Cache Redis di Azure di toomonitor](../redis-cache/cache-how-to-monitor.md)

Seguire toostay aggiornate tutte le notizie più recenti hello e funzionalità, [ @AzureStreaming ](https://twitter.com/AzureStreaming) su Twitter.

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md
