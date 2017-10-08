---
title: analisi del sentiment aaaReal ora Twitter con Analitica di flusso di Azure | Documenti Microsoft
description: Informazioni su come toouse Analitica di flusso per l'analisi di valutazione di Twitter in tempo reale. Istruzioni dettagliate da toodata di generazione di eventi in un dashboard in tempo reale.
keywords: analisi delle tendenze twitter in tempo reale, analisi del sentiment, analisi dei social media, esempio di analisi delle tendenze
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Analisi del sentiment su Twitter in tempo reale in Analisi di flusso di Azure

Informazioni su come una soluzione di analisi del sentiment per analitica di social networking mettendo in tempo reale toobuild Twitter eventi nell'hub eventi di Azure. È quindi possibile scrivere una query su Azure flusso Analitica tooanalyze hello dati e nessuno dei due archivi hello risultati per un utilizzo successivo o utilizzare un dashboard e [Power BI](https://powerbi.com/) insights tooprovide in tempo reale.

Gli strumenti di analisi dei social media permettono alle organizzazioni di determinare gli argomenti di tendenza, vale a dire gli argomenti e gli atteggiamenti che registrano un numero elevato di post nei social media. Analisi del sentiment, denominato anche *data mining parere*, Usa attitudini di social networking analitica strumenti toodetermine verso un prodotto, l'idea e così via. 

Analisi delle tendenze Twitter in tempo reale è un ottimo esempio di uno strumento analitica, perché hello hashtag sottoscrizione modello consente le parole chiave toospecific toolisten (hashtag) e lo sviluppo di analisi del sentiment di hello feed.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Scenario: analisi del sentiment su social media in tempo reale

Una società che ha un sito Web di notizie media è interessata a ottenere un vantaggio rispetto alla concorrenza con il contenuto del sito è lettori tooits immediatamente pertinente. la società Hello utilizza analisi social media negli argomenti pertinenti tooreaders eseguendo l'analisi del sentiment in tempo reale dei dati di Twitter.

argomenti relativi alle tendenze di tooidentify in tempo reale su Twitter, hello analitica in tempo reale di esigenze aziendali sul volume di tweet hello e sentiment per gli argomenti principali. In altre parole, hello necessità è un motore analitica di analisi di valutazione che si basa sul supporto social feed.

## <a name="prerequisites"></a>Prerequisiti
In questa esercitazione, utilizzare un'applicazione client che si connette tooTwitter e Cerca TWEET che hanno determinate hashtag (che è possibile impostare). In ordine toorun applicazione hello e analizzare hello TWEET utilizzando Azure Streaming Analitica, è necessario disporre delle seguenti hello:

* Una sottoscrizione di Azure.
* Un account Twitter 
* Un'applicazione di Twitter e hello [token di accesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) per tale applicazione. Si forniscono istruzioni generali sul toocreate un'applicazione di Twitter in un secondo momento.
* applicazione di TwitterWPFClient Hello, che legge hello Twitter feed. tooget questa applicazione, il download hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) file da GitHub e quindi decomprimere il pacchetto di hello in una cartella nel computer in uso. Se si desidera il codice sorgente toosee hello ed eseguire un'applicazione hello in un debugger, è possibile ottenere il codice sorgente hello da [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Creare un hub eventi per l'input di Analisi di flusso

applicazione di esempio Hello genera eventi e li inserisce tooan hub di eventi di Azure. Gli hub di eventi di Azure sono hello preferito come metodo di inserimento di eventi per Analitica di flusso. Per ulteriori informazioni, vedere hello [documentazione hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Creare uno spazio dei nomi dell'hub eventi e un hub eventi
In questa procedura, creare innanzitutto un spazio dei nomi dell'hub di eventi e quindi aggiungere uno spazio dei nomi toothat hub di eventi. Vengono utilizzati gli spazi dei nomi di evento hub gruppo toologically relative istanze di bus di eventi. 

1. Accedi toohello portale di Azure e fare clic su **New** > **Internet of Things** > **Hub eventi**. 

2. In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi, ad esempio `<yourname>-socialtwitter-eh-ns`. È possibile utilizzare qualsiasi nome spazio dei nomi hello, ma il nome di hello deve essere valido per un URL e deve essere univoco in Azure. 
    
3. Selezionare una sottoscrizione, creare o scegliere un gruppo di risorse e quindi fare clic su **Crea**. 

    ![Creare uno spazio dei nomi dell'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Al termine dello spazio dei nomi hello distribuzione, è possibile trovare hello spazio dei nomi hub di eventi nell'elenco delle risorse di Azure. 

5. Fare clic su nuovo spazio dei nomi hello e nel Pannello di hello dello spazio dei nomi, fare clic su  **+ &nbsp;Hub eventi**. 

    ![pulsante Aggiungi Hub eventi Hello per la creazione di un nuovo hub eventi ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Nome hello nuovo hub eventi `socialtwitter-eh`. È possibile usare un nome diverso. In caso contrario, prendere nota di esso, in quanto è necessario il nome di hello in un secondo momento. Non è necessario tooset tutte le altre opzioni per l'hub di eventi hello.

    ![Pannello per creare un nuovo hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Fare clic su **Crea**.


### <a name="grant-access-toohello-event-hub"></a>Hub di eventi di concedere accesso toohello

Prima di un processo può inviare hub di eventi di dati tooan, hub eventi hello deve disporre di criteri che consente l'accesso appropriato. i criteri di accesso Hello produce una stringa di connessione che include informazioni di autorizzazione.

1.  Nel Pannello di spazio dei nomi di evento hello, fare clic su **hub eventi** e quindi fare clic su nome hello del nuovo hub di eventi.

2.  Nel Pannello di hub eventi hello, fare clic su **criteri di accesso condiviso** e quindi fare clic su  **+ &nbsp;Aggiungi**.

    >[!NOTE]
    >Verificare che si lavora con hub eventi hello, non nomi di hub eventi hello.

3.  Aggiungere criteri denominati `socialtwitter-access` e per **Attestazione** selezionare **Gestisci**.

    ![Pannello per creare nuovi criteri di accesso all'hub eventi](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Fare clic su **Crea**.

5.  Dopo la distribuzione di criteri di hello, selezionarla nell'elenco di hello di criteri di accesso condiviso.

6.  Casella Trova hello **chiave primaria di stringa di connessione** e fare clic su hello copia pulsante Avanti toohello stringa di connessione. 
    
    ![Copia chiave di stringa di connessione primaria hello dai criteri di accesso hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Incollare la stringa di connessione hello in un editor di testo. La stringa di connessione è necessario per la sezione successiva hello, dopo aver apportato tooit alcune piccole modifiche.

    stringa di connessione Hello è simile al seguente:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Si noti che la stringa di connessione hello contiene più coppie chiave-valore, separate da punti e virgola: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.  

    > [!NOTE]
    > Per la sicurezza, sono state rimosse le parti della stringa di connessione hello nell'esempio hello.

8.  Nell'editor di testo hello, rimuovere hello `EntityPath` coppia dalla stringa di connessione hello (non dimenticare tooremove hello un punto e virgola che lo precede). Al termine, la stringa di connessione hello simile al seguente:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Configurare e avviare l'applicazione client di Twitter hello
un'applicazione Hello client ottiene gli eventi di tweet direttamente da Twitter. In ordine toodo questa operazione, è necessario hello toocall autorizzazione Twitter API di flusso. tooconfigure di autorizzazione, creare un'applicazione in Twitter, che genera l'errore credenziali univoche (ad esempio, un token OAuth). È quindi possibile configurare hello client applicazione toouse queste credenziali quando si effettua chiamate API. 

### <a name="create-a-twitter-application"></a>Creare un'applicazione Twitter
Se si ha già un'applicazione Twitter utilizzabile per questa esercitazione, è possibile crearne una. È necessario avere già un account Twitter.

> [!NOTE]
> il processo effettivo Hello in Twitter per la creazione di un'applicazione e l'acquisizione di token, i segreti e le chiavi di hello potrebbe cambiare. Se queste istruzioni non corrispondono a ciò che viene visualizzato nel sito di Twitter hello, consultare la documentazione per sviluppatori di toohello Twitter.

1. Passare toohello [pagina Gestione applicazioni di Twitter](https://apps.twitter.com/). 

2. Creare una nuova applicazione. 

    * Per l'URL del sito Web hello, specificare un URL valido. È toobe un sito in tempo reale. ma non è possibile specificare semplicemente `localhost`.
    * Lasciare vuoto il campo di callback hello. i callback non richiede l'applicazione Hello client in che uso per questa esercitazione.

    ![Creazione di un'applicazione in Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Facoltativamente, modificare le autorizzazioni dell'applicazione hello tooread sola.

4. Quando viene creata un'applicazione hello, visitare toohello **chiavi e i token di accesso** pagina.

5. Fare clic su hello pulsante toogenerate un token di accesso e segreto del token di accesso.

Mantenere queste informazioni utili, poiché sarà necessario hello procedura descritta di seguito.

>[!NOTE]
>Hello chiavi e segreti per un'applicazione hello Twitter forniscono l'account di accesso tooyour Twitter. Considerate queste informazioni riservate, hello stesso come avviene la password di Twitter. Ad esempio, evitare di incorporare queste informazioni in un'applicazione che è possibile assegnare tooothers. 


### <a name="configure-hello-client-application"></a>Configurare un'applicazione hello client
Abbiamo creato un'applicazione client che si connette utilizzando dati tooTwitter [API del Twitter di Streaming](https://dev.twitter.com/streaming/overview) eventi tweet toocollect su un set specifico di argomenti. un'applicazione Hello utilizza hello [Sentiment140](http://help.sentiment140.com/) strumento open source, che assegna hello tweet tooeach valore di valutazione seguenti:

* 0 = negativo
* 2 = neutrale
* 4 = positivo

Dopo gli eventi tweet hello sono stati assegnati un valore di sentiment, queste vengono inviate hub eventi toohello creato in precedenza.

Prima dell'esecuzione di un'applicazione hello richiede alcune informazioni da parte dell'utente, ad esempio le chiavi di Twitter hello e stringa di connessione hub eventi hello. È possibile fornire informazioni di configurazione hello nei modi seguenti:

* Eseguire un'applicazione hello e quindi usare dell'applicazione hello UI tooenter hello chiavi, i segreti e stringa di connessione. In questo caso, le informazioni di configurazione hello viene utilizzate per la sessione corrente, ma non viene salvato.
* Modifica file config dell'applicazione hello e impostare i valori hello non esiste. Questo approccio mantiene le informazioni di configurazione hello, ma significa inoltre che queste informazioni potenzialmente riservate vengono archiviate in testo normale nel computer.

Hello procedura riportata di seguito descritti entrambi gli approcci. 

1. Assicurarsi di aver scaricato e decompresso hello [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) applicazione, come indicato nei prerequisiti hello.

2. i valori di hello tooset in fase di esecuzione (e solo per la sessione corrente di hello), eseguire hello `TwitterWPFClient.exe` dell'applicazione. Quando un'applicazione hello viene richiesto, immettere hello seguenti valori:

    * Hello Twitter Consumer tasto (API).
    * Hello Twitter segreto del cliente (chiave privata API).
    * Token di accesso Twitter Hello.
    * Segreto Token di accesso Twitter Hello.
    * Hello stringa informazioni di connessione è stato salvato in precedenza. Assicurarsi di utilizzare una stringa di connessione hello che sia stato rimosso hello `EntityPath` coppia chiave-valore da.
    * parole chiave Twitter Hello che si desidera toodetermine valutazione.

   ![Applicazione TwitterWpfClient in esecuzione, con le impostazioni oscurate](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. i valori hello tooset in modo permanente, utilizzano un file di testo dell'editor tooopen hello TwitterWpfClient.exe.config. Quindi in hello `<appSettings>` elemento, eseguire questa operazione:

    * Impostare `oauth_consumer_key` toohello Twitter Consumer tasto (API). 
    * Impostare `oauth_consumer_secret` toohello Twitter segreto del cliente (chiave privata API).
    * Impostare `oauth_token` toohello Twitter Token di accesso.
    * Impostare `oauth_token_secret` toohello segreto Token di accesso Twitter.

    Più avanti in hello `<appSettings>` elemento apportare queste modifiche:

    * Impostare `EventHubName` nome hub di eventi toohello (vale a dire toohello valore del percorso di entità hello).
    * Impostare `EventHubNameConnectionString` toohello stringa di connessione. Assicurarsi di utilizzare una stringa di connessione hello che sia stato rimosso hello `EntityPath` coppia chiave-valore da.

    Hello `<appSettings>` sezione aspetto hello di esempio seguente. Per motivi di chiarezza e sicurezza, è stato applicato il ritorno a capo automatico ad alcune righe e sono stati rimossi alcuni caratteri.

    ![File di configurazione applicazione TwitterWpfClient in un editor di testo che mostra hello Twitter chiavi e segreti e sulle stringhe di connessione hub eventi hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Se è già stato avviato l'applicazione hello, eseguire TwitterWpfClient.exe. 

5. Fare clic su sentiment social toocollect di hello pulsante start verde. Visualizzare gli eventi di Tweet con hello **CreatedAt**, **argomento**, e **SentimentScore** valori inviati tooyour hub di eventi.

    ![Applicazione TwitterWpfClient in esecuzione, con l'elenco di tweet visualizzato](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Se si verificano errori, e non viene visualizzato un flusso di tweet visualizzato nella parte inferiore di hello della finestra hello, è necessario verificare attentamente i segreti e le chiavi di hello. Controllare inoltre la stringa di connessione hello (assicurarsi che non include hello `EntityPath` chiave e il valore.)


## <a name="create-a-stream-analytics-job"></a>Creare un processo di Analisi di flusso.

Ora che gli eventi tweet utilizza il flusso in tempo reale da Twitter, è possibile impostare un tooanalyze processo flusso Analitica questi eventi in tempo reale.

1. Nel portale di Azure hello, fare clic su **New** > **Internet of Things** > **processo flusso Analitica**.

2. Nome del processo hello `socialtwitter-sa-job` e specificare una sottoscrizione, un gruppo di risorse e un percorso.

    È una buona idea tooplace hello processo e hello hub eventi in hello stessa area per prestazioni ottimali e pertanto di non prestare tootransfer dati tra aree.

    ![Creazione di un nuovo processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Fare clic su **Crea**.

    viene creato il processo di Hello e portale hello Visualizza i dettagli dei processi.


## <a name="specify-hello-job-input"></a>Specificare l'input processo hello

1. Nel processo di flusso Analitica, in **processo topologia** centro hello del pannello processo hello, fare clic su **input**. 

2. In hello **input** pannello, fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:

    * **Alias di input**: utilizza il nome di hello `TwitterStream`. Se si usa un nome diverso, tenerne traccia, poiché sarà necessario in un secondo momento.
    * **Tipo di origine**: selezionare **Flusso dati**.
    * **Origine**: selezionare **Hub eventi**.
    * **Opzioni di importazione**: selezionare **Usa l'hub eventi della sottoscrizione corrente**. 
    * **Spazio dei nomi di Service bus**: selezionare hello spazio dei nomi hub eventi creato in precedenza (`<yourname>-socialtwitter-eh-ns`).
    * **Hub eventi**: hub eventi selezionare hello creato in precedenza (`socialtwitter-eh`).
    * **Nome criterio hub eventi**: selezionare i criteri di accesso hello creato in precedenza (`socialtwitter-access`).

    ![Creare un nuovo input per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Fare clic su **Crea**.


## <a name="specify-hello-job-query"></a>Specificare hello processo query

Analisi di flusso supporta un semplice modello di query dichiarativa per descrivere le trasformazioni. toolearn più sul linguaggio di hello, vedere hello [riferimenti al linguaggio di Query di Azure flusso Analitica](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Questa esercitazione permette di creare e testare diverse query su dati di Twitter.

numero di hello toocompare di menziona tra gli argomenti, è possibile utilizzare un [finestra a cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) conteggio hello tooget di menziona dall'argomento ogni cinque secondi.

1. Chiude hello **input** pannello se hai già fatto.

2. Nel Pannello di hello processo, fare clic su hello **Query** casella. Azure Elenca gli input hello e output che sono configurati per il processo di hello e consente di creare una query che consente di trasformare flusso di input hello inviata toohello output.

3. Verificare che tale applicazione TwitterWpfClient hello è in esecuzione. 

3. In hello **Query** pannello, fare clic su Avanti toohello di hello punti `TwitterStream` di input e quindi selezionare **dati da un input di esempio**.

    ![Dal menu Opzioni toouse dati di esempio per hello voce processi di Streaming Analitica, con "Dati di input" selezionati](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Verrà aperto un pannello che consente di specificare la quantità tooget di dati di esempio, definito in termini di tempo hello tooread flusso di input.

4. Impostare **minuti** too3 e quindi fare clic su **OK**. 
    
    ![Opzioni di campionamento di flusso di input hello, con "3 minuti" selezionati.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    Azure esempi relativi a 3 minuti dei dati dal flusso di input hello e invia una notifica quando i dati di esempio hello sono pronti. Questa operazione richiede un breve tempo. 

    dati di esempio Hello vengono archiviati temporaneamente ed sono disponibili quando è aperta la finestra di query hello. Se si chiude la finestra di query hello, vengono eliminati i dati di esempio hello e aver toocreate un nuovo set di dati di esempio. 

5. Modificare la query hello in hello codice editor toohello che segue:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Se non sono stati `TwitterStream` come hello alias di input hello, sostituire con l'alias per `TwitterStream` nella query hello.  

    Questa query utilizza hello **TIMESTAMP BY** toospecify (parola chiave) un campo timestamp hello payload toobe utilizzata nel calcolo temporale hello. Se questo campo non è specificato, utilizzando hello di ogni evento arriva all'hub eventi hello viene eseguita l'operazione di windowing hello. Altre informazioni nella sezione hello "ora di arrivo vs tempo applicazione" di [flusso Analitica Query riferimento](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    La query accede anche a un timestamp di fine hello di ogni finestra utilizzando hello **timestamp** proprietà.

5. Fare clic su **Test**. query di Hello viene eseguita sui dati hello è campionate.
    
6. Fare clic su **Salva**. Consente di salvare la query hello come parte del processo di Streaming Analitica hello. (Non salva i dati di esempio hello).


## <a name="experiment-using-different-fields-from-hello-stream"></a>Provare a utilizzare diversi campi dal flusso hello 

Hello nella tabella seguente elenca i campi di hello che fanno parte di hello dati flusso JSON. È possibile tooexperiment disponibile nell'editor di query hello.

|Proprietà JSON | Definizione|
|--- | ---|
|CreatedAt | tempo di Hello è stato creato tale tweet hello|
|Argomento | argomento Hello corrispondente hello specificato (parola chiave)|
|SentimentScore | punteggio sentiment Hello Sentiment140|
|Autore | handle Twitter hello inviati tweet hello|
|Text | corpo Hello della tweet hello|


## <a name="create-an-output-sink"></a>Creare un sink di output

È stata definita ora un flusso di eventi, un input tooingest degli hub eventi e tooperform una query una trasformazione tramite flusso hello. ultimo passaggio Hello è toodefine sink di output per il processo di hello.  

In questa esercitazione, scrivere eventi tweet hello aggregato da hello processo query tooAzure nell'archiviazione Blob.  È possibile distribuire anche i risultati tooAzure Database SQL, archiviazione tabelle di Azure, gli hub di eventi o Power BI, è necessario a seconda dell'applicazione.

## <a name="specify-hello-job-output"></a>Specificare l'output del processo hello

1. In hello **processo topologia** fare clic su hello **Output** casella. 

2. In hello **output** pannello, fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:

    * **Alias di output**: utilizza il nome di hello `TwitterStream-Output`. 
    * **Sink**: selezionare **Archivio BLOB**.
    * **Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.
    * **Account di archiviazione**. Selezionare **Crea un nuovo account di archiviazione**.
    * **Account di archiviazione** (seconda casella). Immettere `YOURNAMEsa`, dove `YOURNAME` rappresenta il nome o un'altra stringa univoca. nome Hello può utilizzare solo lettere minuscole e numeri e deve essere univoco in Azure. 
    * **Contenitore**. Immettere `socialtwitter`.
    nome account di archiviazione Hello e nome del contenitore sono tooprovide insieme usato un URI per l'archiviazione blob di hello, simile al seguente: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Pannello "Nuovo output" per il processo di Analisi di flusso](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Fare clic su **Crea**. 

    Azure crea account di archiviazione hello e genera automaticamente una chiave. 

5. Chiude hello **output** blade. 


## <a name="start-hello-job"></a>Avviare il processo di hello

Sono stati specificati l'input del processo, la query e l'output. Sono processi di flusso Analitica hello toostart pronto.

1. Verificare che tale applicazione TwitterWpfClient hello è in esecuzione. 

2. Nel Pannello di hello processo, fare clic su **avviare**.

    ![Avviare il processo di flusso Analitica hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. In hello **inizio processo** pannello per **ora di inizio di output del processo**selezionare **ora** e quindi fare clic su **avviare**. 

    ![Pannello "Avvia processo" per il processo di flusso Analitica hello](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure notifica che ha avviato il processo di hello e nel Pannello di processo hello, viene visualizzato stato hello **esecuzione**.

    ![Processo in esecuzione](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Visualizzare l'output per l'analisi del sentiment

Dopo il processo è iniziata l'esecuzione e sta elaborando il flusso Twitter in tempo reale di hello, è possibile visualizzare l'output di hello per l'analisi di valutazione.

È possibile utilizzare uno strumento come [Azure Storage Explorer](https://http://storageexplorer.com/) o [Esplora Azure](http://www.cerebrata.com/products/azure-explorer/introduction) tooview il processo di output in tempo reale. Da qui è possibile utilizzare [Power BI](https://powerbi.com/) hello di tooextend il tooinclude applicazione un dashboard personalizzato come illustrato nella seguente schermata hello:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Creare un'altra query argomenti relativi alle tendenze tooidentify

Un'altra query, è possibile utilizzare toounderstand Twitter sentiment si basa su un [finestra temporale scorrevole](https://msdn.microsoft.com/library/azure/dn835051.aspx). argomenti relativi alle tendenze tooidentify, esaminare gli argomenti che superano un valore di soglia per i riferimenti in un periodo di tempo specificato.

Ai fini di hello di questa esercitazione, è cercare argomenti che più di 20 volte menzionati nelle hello ultimi 5 secondi.

1. Nel Pannello di hello processo, fare clic su **arrestare** processo hello toostop. 

2. In hello **processo topologia** fare clic su hello **Query** casella. 

3. Modificare i seguenti toohello di hello query:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Fare clic su **Salva**.

5. Verificare che tale applicazione TwitterWpfClient hello è in esecuzione. 

6. Fare clic su **avviare** processo hello toorestart utilizzando hello nuova query.


## <a name="get-support"></a>Supporto
Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi
* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Introduzione all'uso di Analisi dei flussi di Azure](stream-analytics-real-time-fraud-detection.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
