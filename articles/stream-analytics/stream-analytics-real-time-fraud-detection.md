# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Introduzione all’uso di Analisi di flusso di Azure: rilevamento di illeciti in tempo reale

In questa esercitazione viene illustrato end-to-end come toouse Analitica di flusso di Azure. Si apprenderà come: 

* Introdurre eventi di streaming in un'istanza degli hub eventi di Azure. In questa esercitazione si userà un'app che simula un flusso di record di metadati di un telefono cellulare.

* Scrivere Analitica flusso simile a SQL Query tootransform dati, aggregazione delle informazioni o per i modelli. Verrà visualizzato come toouse tooexamine una query hello flusso in ingresso e individuare le chiamate che potrebbero essere falsi.

* Inviare hello risultati tooan sink di output (archiviazione) che è possibile analizzare per informazioni aggiuntive. In questo caso, inviare archiviazione Blob di hello chiamata sospette dati tooAzure.

In questa esercitazione, si usa l'esempio hello di rilevazione delle frodi in tempo reale in base ai dati di chiamata telefonica. Ma tecnica hello che è illustrare è adatto anche per altri tipi di rilevare le frodi, ad esempio furto di frode o identità della carta di credito. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Scenario: telecomunicazioni e rilevamento di illecito relativo alle SIM in tempo reale

Un'azienda di telecomunicazioni dispone di un volume di dati elevato relativamente alle chiamate in ingresso. società di Hello vuole toodetect fraudolenti chiama in tempo reale in modo che possano inviare notifiche ai clienti o arrestare il servizio per un numero specifico. Un tipo di frode SIM comporta più chiamate da hello stessa identità intorno hello stesso tempo ma in posizioni diverse località geografiche. toodetect questo tipo di frode, hello società esigenze tooexamine phone i record in entrata e cercare modelli specifici, in questo caso, per le chiamate intorno hello contemporaneamente in diversi paesi. Qualsiasi record di telefono che rientrano in questa categoria vengono scritti toostorage per analisi successive.

## <a name="prerequisites"></a>Prerequisiti

In questa esercitazione si simuleranno i dati di una chiamata telefonica usando un'app client che genera metadati di esempio di chiamate. Alcuni record hello che hello app produce fraudolente chiamate è simile. 

Prima di iniziare, verificare di che aver seguito hello:

* Un account Azure.
* applicazione di generatore Hello evento di chiamata. È possibile ottenere questo scaricando hello [TelcoGenerator.zip file](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) da hello Microsoft Download Center. Decomprimere il pacchetto in una cartella nel computer. Se si desidera il codice sorgente toosee hello e dell'applicazione hello esecuzione di un debugger, è possibile ottenere il codice sorgente dell'applicazione hello dai [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows potrebbero bloccare file con estensione ZIP scaricato hello. Se non è possibile decomprimere il contenuto, fare clic sul file hello e selezionare **proprietà**. Se hello viene visualizzato il messaggio "il file proviene da un altro computer e potrebbero essere bloccati toohelp proteggere questo computer", seleziona hello **Unblock** opzione e quindi fare clic su **applica**.

Se si desidera che tooexamine hello risultati del processo di Streaming Analitica hello, è necessario uno strumento per la visualizzazione contenuto hello di un contenitore di archiviazione Blob di Azure. Se si usa Visual Studio, è possibile usare [Strumenti di Microsoft Azure per Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) o [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). In alternativa, è possibile installare strumenti autonomi come [Azure Storage Explorer](http://storageexplorer.com/) o [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Creare un evento Azure eventi tooingest hub

tooanalyze un flusso di dati, si *inserimento* in Azure. Tipico tooingest è presente un toouse [hub eventi di Azure](../event-hubs/event-hubs-what-is-event-hubs.md), che consente di inserire milioni di eventi al secondo e quindi elaborare e archiviare le informazioni sull'evento hello. Per questa esercitazione, creare un hub eventi e quindi chiedere di hello evento chiamata generatore app trasmissione chiamata dati toothat hub eventi. Per ulteriori informazioni sugli hub di eventi, vedere hello [documentazione di Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Per una versione più dettagliata di questa procedura, vedere [creare uno spazio dei nomi dell'hub eventi e un hub di eventi utilizzando hello Azure portal](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Creare uno spazio dei nomi e un hub eventi
In questa procedura, creare innanzitutto un spazio dei nomi dell'hub di eventi e quindi aggiungere un namepsace toothat hub di eventi. Vengono utilizzati gli spazi dei nomi di evento hub gruppo toologically relative istanze di bus di eventi. 

1. Accedere al portale di Azure hello e fare clic su **New** > **Internet of Things** > **Hub eventi**. 

2. In hello **Crea spazio dei nomi** pannello, immettere un nome di spazio dei nomi, ad esempio `<yourname>-eh-ns-demo`. È possibile utilizzare qualsiasi nome spazio dei nomi hello, ma il nome di hello deve essere valido per un URL e deve essere univoco in Azure. 
    
3. Selezionare una sottoscrizione, creare o scegliere un gruppo di risorse e quindi fare clic su **Crea**. 

    ![Creare uno spazio dei nomi dell'hub eventi](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Al termine dello spazio dei nomi hello distribuzione, è possibile trovare hello spazio dei nomi hub di eventi nell'elenco delle risorse di Azure. 

5. Fare clic su nuovo spazio dei nomi hello e nel Pannello di hello dello spazio dei nomi, fare clic su  **+ &nbsp;Hub eventi**. 

    ![pulsante Aggiungi Hub eventi Hello per la creazione di un nuovo hub eventi ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Nome hello nuovo hub eventi `sa-eh-frauddetection-demo`. È possibile usare un nome diverso. In caso contrario, prendere nota di esso, in quanto è necessario il nome di hello in un secondo momento. Non è necessario tooset tutte le altre opzioni per l'hub di eventi hello ora.

    ![Pannello per creare un nuovo hub eventi](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Fare clic su **Crea**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Concessione dell'hub di eventi di accesso toohello e ottenere una stringa di connessione

Prima di un processo può inviare hub di eventi di dati tooan, hub eventi hello deve disporre di criteri che consente l'accesso appropriato. i criteri di accesso Hello produce una stringa di connessione che include informazioni di autorizzazione.

1.  Nel Pannello di spazio dei nomi di evento hello, fare clic su **hub eventi** e quindi fare clic su nome hello del nuovo hub di eventi.

2.  Nel Pannello di hub eventi hello, fare clic su **criteri di accesso condiviso** e quindi fare clic su  **+ &nbsp;Aggiungi**.

    >[!NOTE]
    >Verificare che si lavora con hub eventi hello, non nomi di hub eventi hello.

3.  Aggiungere criteri denominati `sa-policy-manage-demo` e per **Attestazione** selezionare **Gestisci**.

    ![Pannello per creare nuovi criteri di accesso all'hub eventi](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Fare clic su **Crea**.

5.  Dopo la distribuzione di criteri di hello, selezionarla nell'elenco di hello di criteri di accesso condiviso.

6.  Casella Trova hello **chiave primaria di stringa di connessione** e fare clic su hello copia pulsante Avanti toohello stringa di connessione. 
    
    ![Copia chiave di stringa di connessione primaria hello dai criteri di accesso hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Incollare la stringa di connessione hello in un editor di testo. La stringa di connessione è necessario per la sezione successiva hello, dopo aver apportato tooit alcune piccole modifiche.

    stringa di connessione Hello è simile al seguente:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Si noti che la stringa di connessione hello contiene più coppie chiave-valore, separate da punti e virgola: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configurare e avviare un'applicazione hello evento generatore

Prima di iniziare hello TelcoGenerator app, è configurato in modo da invierà hub eventi di chiamata record toohello che appena creato.

### <a name="configure-hello-telcogeneratorapp"></a>Configurare hello TelcoGeneratorapp

1.  Nell'editor di hello dove è stata copiata la stringa di connessione hello, prendere nota di hello `EntityPath` valore e quindi rimuovere hello `EntityPath` coppia (non dimenticare tooremove hello un punto e virgola che lo precede). 

2.  Nella cartella hello in cui è stato decompresso file TelcoGenerator.zip hello, aprire il file telcodatagen.exe.config hello in un editor. (È presente più di un file con estensione config, pertanto è necessario assicurarsi che si apre il diritto di hello uno).

3.  In hello `<appSettings>` elemento, eseguire questa operazione:

    * Impostare il valore di hello di hello `EventHubName` nome hub di eventi chiave toohello (vale a dire toohello valore del percorso di entità hello).
    * Impostare il valore di hello di hello `Microsoft.ServiceBus.ConnectionString` toohello stringa di connessione della chiave. 

    Hello `<appSettings>` sezione avrà un aspetto simile hello di esempio seguente. (Per maggiore chiarezza, è stato eseguito il wrapping righe hello e rimossi alcuni caratteri dal token di autorizzazione hello.)

    ![File di configurazione app TelcoGenerator hello evento hub nome stringa di connessione e di visualizzazione](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Salvare il file hello. 

### <a name="start-hello-app"></a>Avviare l'applicazione hello
1.  Aprire una finestra di comando e modificare toohello cartella in cui app TelcoGenerator hello viene decompresso.
2.  Immettere hello comando seguente:

        telcodatagen.exe 1000 .2 2

    i parametri di Hello sono: 

    * Numero di CDR all'ora. 
    * Probabilità di frode scheda SIM: Frequenza, come una percentuale di tutte le chiamate, tale applicazione hello deve simulare una chiamata fraudolenta. il valore di Hello 2 alla penultima copia indica che circa il 20% dei record di chiamata hello avrà un aspetto fraudolenti.
    * Durata in ore. numero di Hello di ore che hello app deve essere eseguito. È anche possibile arrestare app hello qualsiasi momento premendo Ctrl + C nella riga di comando hello.

    Dopo alcuni secondi, hello app inizia la visualizzazione di record telefonata nella schermata di hello come inviarli toohello hub di eventi.

Alcuni dei campi chiave hello che verrà utilizzato in questa applicazione di rilevamento di frodi in tempo reale sono di hello seguenti:

|**Record**|**Definizione**|
|----------|--------------|
|`CallrecTime`|ora di inizio Hello timestamp per chiamata hello. |
|`SwitchNum`|telefonico Hello utilizzato chiamata hello tooconnect. Per questo esempio, le opzioni di hello sono stringhe che rappresentano il paese hello di origine (Stati Uniti, Cina, Regno Unito, Germania o Australia). |
|`CallingNum`|numero di telefono Hello del chiamante hello. |
|`CallingIMSI`|Hello International Mobile IMSI (Subscriber Identity). Si tratta hello identificatore univoco del chiamante hello. |
|`CalledNum`|numero di telefono Hello del destinatario chiamata hello. |
|`CalledIMSI`|Codice IMSI (International Mobile Subscriber Identity). Si tratta hello identificatore univoco del destinatario chiamata hello. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Creare un toomanage processo Analitica flusso dati di streaming

Dopo aver creato un flusso di eventi di chiamata, sarà possibile configurare un processo di Analisi di flusso. processo Hello leggerà i dati provenienti dall'hub di eventi hello impostati. 

### <a name="create-hello-job"></a>Creazione del processo di hello 

1. Nel portale di Azure hello, fare clic su **New** > **Internet of Things** > **processo flusso Analitica**.

2. Nome del processo hello `sa_frauddetection_job_demo`, specificare una sottoscrizione, un gruppo di risorse e un percorso.

    È una buona idea tooplace hello processo e hello hub eventi in hello stessa area per prestazioni ottimali e pertanto di non prestare tootransfer dati tra aree.

    ![Creare un nuovo processo di Analisi di flusso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Fare clic su **Crea**.

    viene creato il processo di Hello e portale hello Visualizza i dettagli dei processi. Non è ancora in esecuzione, tuttavia, è il processo di hello tooconfigure prima di poter essere avviato.

### <a name="configure-job-input"></a>Configurare l'input del processo

1. Nel dashboard di hello o hello **tutte le risorse** pannello, trovare e seleziona hello `sa_frauddetection_job_demo` processo flusso Analitica. 
2. In hello **processo topologia** di hello pannello processo Analitica di flusso, fare clic su hello **Input** casella.

    ![Casella di input in una topologia nel Pannello di processo di Streaming Analitica hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:

    * **Alias di input**: utilizza il nome di hello `CallStream`. Se si usa un nome diverso, tenerne traccia, poiché sarà necessario in un secondo momento.
    * **Tipo di origine**: selezionare **Flusso dati**. (**Dati di riferimento** fa riferimento a dati di ricerca toostatic, che non vengono utilizzati in questa esercitazione.)
    * **Origine**: selezionare **Hub eventi**.
    * **Opzioni di importazione**: selezionare **Usa l'hub eventi della sottoscrizione corrente**. 
    * **Spazio dei nomi di Service bus**: selezionare hello spazio dei nomi hub eventi creato in precedenza (`<yourname>-eh-ns-demo`).
    * **Hub eventi**: hub eventi selezionare hello creato in precedenza (`sa-eh-frauddetection-demo`).
    * **Nome criterio hub eventi**: selezionare i criteri di accesso hello creato in precedenza (`sa-policy-manage-demo`).

    ![Creare un nuovo input per il processo di Analisi di flusso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Fare clic su **Crea**.

## <a name="create-queries-tootransform-real-time-data"></a>Creare query di dati in tempo reale tootransform

A questo punto, aver configurato un processo di flusso Analitica tooread un flusso di dati in ingresso. passaggio successivo Hello è toocreate una trasformazione che analizza i dati di hello in tempo reale. A tale scopo, creare una query. Analisi di flusso supporta un semplice modello di query dichiarative che descrive le trasformazioni per l'elaborazione in tempo reale. le query di Hello utilizzano un linguaggio simile a SQL con alcuni analitica toostream specifiche estensioni. 

Una query molto semplice semplicemente potrebbe leggere tutti i dati in arrivo hello. Tuttavia, è spesso creare query che la ricerca per i dati specifici o per le relazioni nei dati hello. In questa sezione dell'esercitazione hello, creare e i test verranno toolearn query diversi modi in cui è possibile trasformare un flusso di input per l'analisi. 

le query Hello che qui creati solo visualizzano hello dati trasformati toohello schermata. In una sezione successiva, è possibile configurare un sink di output e una query che scrive hello dati trasformati toothat sink.

toolearn più sul linguaggio di hello, vedere hello [riferimenti al linguaggio di Query di Azure flusso Analitica](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Ottenere dati di esempio per testare le query

hub di eventi di chiamata record toohello invia Hello TelcoGenerator app e del processo di flusso Analitica è tooread configurato dall'hub di eventi di hello. È possibile utilizzare un assicurarsi che sta leggendo correttamente toomake query tootest hello processo. troppo test di una query in hello console Azure, è necessario che i dati di esempio. Questa procedura dettagliata, si saranno estrarre dati di esempio dal flusso di hello provenienti in hub eventi hello.

1. Verificare che tale app TelcoGenerator hello è in esecuzione e se producono chiamata vengono registrate.
2. Nel portale di hello restituiscono pannello processo di Streaming Analitica toohello. (Se è stata chiusa pannello hello, cercare `sa_frauddetection_job_demo` in hello **tutte le risorse** blade.)
3. Fare clic su hello **Query** casella. Azure Elenca gli input hello e output che sono configurati per il processo di hello e consente di creare una query che consente di trasformare flusso di input hello inviata toohello output.
4. In hello **Query** pannello, fare clic su Avanti toohello di hello punti `CallStream` di input e quindi selezionare **dati da un input di esempio**.

    ![Dal menu Opzioni toouse dati di esempio per hello voce processi di Streaming Analitica, con "Dati di input" selezionati](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Verrà aperto un pannello che consente di specificare la quantità tooget di dati di esempio, definito in termini di tempo hello tooread flusso di input.

5. Impostare **minuti** too3 e quindi fare clic su **OK**. 
    
    ![Opzioni di campionamento di flusso di input hello, con "3 minuti" selezionati.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure esempi relativi a 3 minuti dei dati dal flusso di input hello e invia una notifica quando i dati di esempio hello sono pronti. Questa operazione richiede un breve tempo. 

dati di esempio Hello vengono archiviati temporaneamente ed sono disponibili quando è aperta la finestra di query hello. Se si chiude la finestra di query hello, vengono eliminati i dati di esempio hello e sarà necessario toocreate un nuovo set di dati di esempio. 

In alternativa, è possibile ottenere un file con estensione JSON che contiene dati di esempio [da GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)e quindi caricare tale toouse file con estensione JSON come dati di esempio per hello `CallStream` input. 

### <a name="test-using-a-pass-through-query"></a>Test mediante una query pass-through

Se si desidera tooarchive ogni evento, è possibile utilizzare tutti i campi nel payload hello dell'evento hello hello tooread una query pass-through.

1. Nella finestra query hello, immettere la query:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Come con SQL, le parole chiave non effettuano distinzione tra maiuscole e minuscole e gli spazi non sono rilevanti.

    In questa query `CallStream` è hello alias specificato durante la creazione di input hello. In presenza di un alias diverso, usare questo nome.

2. Fare clic su **Test**.

    il processo di flusso Analitica Hello esegue hello query su dati di esempio hello e visualizza l'output di hello nella parte inferiore di hello della finestra hello. Indica che hub eventi hello e il processo di Streaming Analitica hello siano configurati correttamente. (Come già indicato, in seguito si creerà un sink di output di hello query può scrivere i dati.)

    ![Output del processo di Analisi di flusso con 73 record generati](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    numero esatto di Hello di record da visualizzare dipenderà dal numero di record sono stato acquisito nell'esempio 3 minuti.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Ridurre il numero di hello di campi utilizzando una proiezione di colonna

In molti casi, l'analisi non deve necessariamente tutte le colonne di hello hello flusso di input. È possibile utilizzare una query tooproject ridurre il numero di campi di restituiti nella query pass-through hello.

1. Modificare la query hello in hello codice editor toohello che segue:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Fare di nuovo clic su **Test**. 

    ![Output del processo di Analisi di flusso per la proiezione con 25 record generati](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Numero di chiamate in ingresso per area: finestra a cascata con aggregazione

Si supponga che si desidera toocount hello numero di chiamate in ingresso per ogni area. Nel flusso di dati, quando si desidera che le funzioni di aggregazione tooperform come il conteggio dei, è necessario toosegment hello flusso in unità temporali (poiché hello flusso di dati in modo efficace infinito). A tale scopo, usare una [funzione finestra](stream-analytics-window-functions.md) di Analisi di flusso. È quindi possibile utilizzare dati hello all'interno di tale finestra come unità.

Per questa trasformazione si intende creare una sequenza di finestre temporali che non si sovrappongano. Ogni finestra includerà un set distinto di dati che è possibile raggruppare e aggregare. Questo tipo di finestra è tooas di cui si fa riferimento un *finestra a cascata* . Nella finestra a cascata hello, è possibile ottenere un conteggio delle chiamate in ingresso di hello raggruppato `SwitchNum`, che rappresenta il paese hello in cui ha origine chiamata hello. 

1. Modificare la query hello in hello codice editor toohello che segue:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Questa query utilizza hello `Timestamp By` parola chiave in hello `FROM` toospecify clausola quale campo timestamp hello finestra a cascata hello toodefine toouse del flusso di input. In questo caso, finestra hello divide i dati hello in segmenti per hello `CallRecTime` campo in ogni record. (Se non viene specificato alcun campo, operazione di windowing hello utilizza ora hello che ogni evento arriva all'hub eventi hello. Vedere la sezione relativa a tempo di arrivo e tempo di applicazione in [Informazioni di riferimento sul linguaggio di query per l'analisi di flusso](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    proiezione Hello include `System.Timestamp`, che restituisce un timestamp di fine hello di ogni finestra. 

    toospecify che si desidera toouse una finestra a cascata, utilizzare hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) funzione hello `GROUP BY `clausola. Nella funzione hello, specificare un'unità di tempo (da un giorno tooa microsecondi) e una dimensione della finestra (il numero di unità). In questo esempio, finestra a cascata hello costituito da intervalli di 5 secondi, per ottenere un conteggio in base al paese per chiamate relativi a ogni 5 secondi.

2. Fare di nuovo clic su **Test**. Nei risultati di hello, si noti che i timestamp hello in **WindowEnd** in incrementi di 5 secondi.

    ![Output del processo di Analisi di flusso per l'aggregazione con 13 record generati](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Rilevare una frode SIM mediante self-join

Per questo esempio, è possibile prendere in considerazione utilizzo fraudolento toobe chiamate provenienti da hello stesso utente, ma in posizioni diverse all'interno di 5 secondi una da altra. Ad esempio, hello stesso utente legittimamente effettuare una chiamata da hello Stati Uniti e Australia in hello contemporaneamente. 

toocheck in questi casi, è possibile utilizzare un self join della hello streaming tooitself flusso di dati toojoin hello in base a hello `CallRecTime` valore. Sarà quindi possibile esaminare per chiamata registra dove hello `CallingIMSI` valore (Buongiorno originari numero) è hello stesso, ma hello `SwitchNum` valore (paese di origine) non è hello stesso.

Quando si utilizza un join con il flusso di dati, deve fornire join hello sono alcuni limiti per la misura hello corrispondenti alle righe possono essere separati in tempo. (Come indicato in precedenza, hello flusso di dati è effettivamente infinito). limiti di tempo Hello per relazione hello specificati all'interno di hello `ON` clausola join hello, utilizzando hello `DATEDIFF` (funzione). In questo caso, il join di hello è basato su un intervallo di 5 secondi di dati della chiamata.

1. Modificare la query hello in hello codice editor toohello che segue: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Questa query è simile a un join SQL, ad eccezione di hello `DATEDIFF` funzione join hello. Si tratta di una versione di `DATEDIFF` tooStreaming specifico Analitica e deve essere visualizzato in hello `ON...BETWEEN` clausola. i parametri di Hello sono un'unità di tempo (secondi in questo esempio) e gli alias di hello due origini di hello per il join hello. (Questo comportamento è diverso da hello SQL standard `DATEDIFF` (funzione).) 

    Hello `WHERE` clausola include condizione hello che contrassegna chiamata fraudolenti hello: opzioni origine hello non sono hello stesso. 

2. Fare di nuovo clic su **Test**. 

    ![Output del processo di Analisi di flusso per il self-join con 6 record generati](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Fare clic su **Salva**. Questa query di self join hello viene salvata come parte del processo di Streaming Analitica hello. (Non salva i dati di esempio hello).

    ![Salvare il processo di Analisi di flusso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Creare un sink di output trasformati toostore dati

Sono stati definiti un flusso di eventi, un input tooingest degli hub eventi e tooperform una query una trasformazione tramite flusso hello. ultimo passaggio Hello è toodefine sink di output per il processo di hello, vale a dire un hello toowrite sul posto trasformato flusso. 

È possibile usare molte risorse come sink di output: un database di SQL Server, un'archiviazione tabelle, un'archiviazione Data Lake, Power BI e addirittura un altro hub eventi. Per questa esercitazione, verrà scritto il flusso di hello tooAzure archiviazione Blob, che è una scelta tipica per raccogliere informazioni sull'evento per analisi successive, in quanto avviene per dati non strutturati.

Se esiste già un account di archiviazione BLOB, è possibile usarlo. Per questa esercitazione, vi mostreremo come toocreate account una nuova risorsa di archiviazione sufficiente per questa esercitazione.

### <a name="create-an-azure-blob-storage-account"></a>Creare un account Archiviazione BLOB di Azure

1. Nel portale di Azure hello, restituire pannello processo di Streaming Analitica toohello. (Se è stata chiusa pannello hello, cercare `sa_frauddetection_job_demo` in hello **tutte le risorse** blade.)
2. In hello **processo topologia** fare clic su hello **Output** casella. 
3. In hello **output** pannello, fare clic su  **+ &nbsp;Aggiungi** e compilare pannello hello con questi valori:

    * **Alias di output**: utilizza il nome di hello `CallStream-FraudulentCalls`. 
    * **Sink**: selezionare **Archivio BLOB**.
    * **Opzioni di importazione**: selezionare **Usa l'archiviazione BLOB della sottoscrizione corrente**.
    * **Account di archiviazione**. Selezionare **Crea un nuovo account di archiviazione**.
    * **Account di archiviazione** (seconda casella). Immettere `YOURNAMEsademo`, dove `YOURNAME` rappresenta il nome o un'altra stringa univoca. nome Hello può utilizzare solo lettere minuscole e numeri e deve essere univoco in Azure. 
    * **Contenitore**. Immettere `sa-fraudulentcalls-demo`.
    nome account di archiviazione Hello e nome del contenitore sono tooprovide insieme usato un URI per l'archiviazione blob di hello, simile al seguente: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Pannello "Nuovo output" per il processo di Analisi di flusso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Fare clic su **Crea**. 

    Azure crea account di archiviazione hello e genera automaticamente una chiave. 

5. Chiude hello **output** blade. 

## <a name="start-hello-streaming-analytics-job"></a>Avviare il processo di Streaming Analitica hello

il processo di Hello è ora configurato. È stato specificato un input (hub eventi hello), una trasformazione (toolook hello query per le chiamate fraudolente) e un output (archiviazione blob). È ora possibile avviare il processo di hello. 

1. Verificare che hello TelcoGenerator app è in esecuzione.

2. Nel Pannello di hello processo, fare clic su **avviare**.

    ![Avviare il processo di flusso Analitica hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. In hello **inizio processo** per processo output ora di inizio, seleziona pannello **ora**. 

4. Fare clic su **Avvia**. 

    ![Pannello "Avvia processo" per il processo di flusso Analitica hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure notifica che ha avviato il processo di hello e nel Pannello di processo hello, viene visualizzato stato hello **esecuzione**.

    ![Stato del processo di Analisi di flusso indicante "In esecuzione"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Esaminare i dati trasformato hello

È stato creato un processo di Analisi di flusso completo. processo Hello è esaminare un flusso di metadati di chiamata telefonica, cercando fraudolenti telefonate in tempo reale e scrivere le informazioni relative a tali toostorage chiamate fraudolenti. 

toocomplete questa esercitazione, è possibile toolook dati hello vengono acquisiti dal processo di Streaming Analitica hello. dati Hello viene scritto tooAzure archiviazione BLOB in blocchi (file). È possibile usare qualsiasi strumento che legga Archiviazione BLOB di Azure. Come indicato nella sezione Prerequisiti di hello, è possibile utilizzare le estensioni di Azure in Visual Studio o è possibile utilizzare uno strumento come [Azure Storage Explorer](http://storageexplorer.com/) o [Esplora Azure](http://www.cerebrata.com/products/azure-explorer/introduction). 

Quando si esamina il contenuto di hello di un file nell'archiviazione blob, vedere simile alla seguente hello:

![Archiviazione BLOB di Azure con output di Analisi di flusso](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Pulire le risorse

Sono disponibili ulteriori articoli che continuano con uno scenario di rilevamento di frodi hello e che usano risorse hello creati in questa esercitazione. Se si desidera toocontinue, vedere i suggerimenti di hello in **passaggi successivi** in un secondo momento.

Tuttavia, se completato e non è necessario aver creato le risorse di hello, è possibile eliminarle in modo che non si incorrere in costi di Azure non necessari. In tal caso, si consiglia di hello seguenti:

1. Arrestare il processo di Streaming Analitica hello. In hello **processi** pannello, fare clic su **arrestare** nella parte superiore di hello.
2. Arrestare l'app di telecomunicazioni generatore hello. Nella finestra di comando hello in cui è stato avviato app hello, premere Ctrl + C.
3. Se è stato creato un nuovo account di archiviazione BLOB solo per questa esercitazione, eliminarlo. 
4. Eliminare il processo di Streaming Analitica hello.
5. Eliminazione dell'hub eventi hello.
6. Elimina spazio dei nomi hub di eventi hello.

## <a name="get-support"></a>Supporto

Per ulteriore assistenza, provare il [Forum di Analisi dei flussi di Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Passaggi successivi

È possibile continuare questa esercitazione con hello seguenti articoli:

* [Analisi di flusso e Power BI: dashboard di analisi in tempo reale per lo streaming dei dati](stream-analytics-power-bi-dashboard.md). Questo articolo illustra come toosend hello telecomunicazioni output di hello Analitica flusso processo tooPower Business Intelligence per la visualizzazione in tempo reale e analisi.
* [Come dati toostore Analitica di flusso di Azure in una Cache di Redis di Azure utilizzando le funzioni di Azure](stream-analytics-functions-redis.md). Questo articolo illustra come toouse Azure funzioni toowrite fraudolenti chiama tooan cache Redis di Azure tramite una coda del Bus di servizio.

Per altre informazioni generiche su Analisi di flusso, provare questi articoli:

* [Introduzione tooAzure flusso Analitica](stream-analytics-introduction.md)
* [Ridimensionare i processi di Analisi dei flussi di Azure](stream-analytics-scale-jobs.md)
* [Informazioni di riferimento sul linguaggio di query di Analisi dei flussi di Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Informazioni di riferimento sulle API REST di gestione di Analisi di flusso di Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
