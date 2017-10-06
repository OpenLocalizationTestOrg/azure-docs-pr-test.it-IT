---
title: toouse aaaHow tooimprove le prestazioni dell'applicazione di Database SQL di Azure batch
description: "Hello argomento fornisce una prova che l'invio in batch le operazioni del database notevolmente imroves hello velocità e la scalabilità delle applicazioni di Database SQL di Azure. Sebbene queste tecniche di invio in batch di lavoro per qualsiasi database di SQL Server, è incentrata hello articolo hello in Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Come l'invio in batch le prestazioni dell'applicazione di Database SQL tooimprove toouse
Invio in batch di operazioni tooAzure Database SQL in modo significativo migliora hello prestazioni e scalabilità delle applicazioni. Vantaggi di hello toounderstand ordine, prima parte di hello di questo articolo descrive alcuni risultati del test di esempio che consentono di confrontare le richieste in batch e sequenziale tooa Database SQL. Hello resto dell'articolo hello Mostra le tecniche di hello, scenari e considerazioni toohelp toouse batch correttamente nelle applicazioni Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Perché l'invio in batch è importante per il database SQL?
Servizio remoto di chiamate tooa il batch è una ben nota strategia per migliorare le prestazioni e scalabilità. Fissi di elaborazione delle interazioni tooany costi con un servizio remoto, ad esempio la serializzazione, trasferimento tramite rete e la deserializzazione. Il raggruppamento di più transazioni distinte in un singolo batch consente di ridurre al minimo questi costi.

In questo documento, è necessario tooexamine diversi scenari e strategie di invio in batch di Database SQL. Sebbene tali strategie siano importanti anche per applicazioni locali che utilizzano SQL Server, esistono diversi motivi per evidenziare l'uso di hello del raggruppamento per il Database SQL:

* È potenzialmente maggiore latenza di rete durante l'accesso al Database SQL, in particolare se si accede a Database SQL da hello esterno stesso Data Center di Microsoft Azure.
* caratteristiche di multi-tenant Hello indica che il Database SQL che hello l'efficienza dei dati hello accedere livello correlata toohello scalabilità generale del database hello. Database SQL devono evitare qualsiasi singolo tenant/utente monopolizzi dannosa toohello risorse di database di altri tenant. Nella risposta toousage eccesso di quote predefinite, Database SQL può compromettono la velocità effettiva oppure rispondere con eccezioni di limitazione. Maggiore efficienza, ad esempio l'invio in batch, Abilita si toodo più lavoro nel Database SQL prima di raggiungere questi limiti. 
* L'invio in batch è efficace anche per le architetture che usano più database (partizionamento orizzontale). Hello l'efficienza dell'interazione con ogni unità di database è ancora un fattore chiave per la scalabilità complessiva. 

Uno dei vantaggi di hello dell'utilizzo del Database SQL è che non sono toomanage hello server database hello host. Tuttavia, questa infrastruttura gestita implica anche la presenza di toothink in modo diverso sull'ottimizzazione di database. Non è possibile esaminare tooimprove hello hardware o rete dell'infrastruttura di database. Gli ambienti sono controllati da Microsoft Azure. Hello principale che è possibile controllare è rappresentata come l'applicazione interagisce con il Database SQL. L'invio in batch è una di queste ottimizzazioni. 

prima parte di Hello del documento hello esamina varie tecniche di invio in batch per le applicazioni .NET che utilizzano il Database SQL. Hello ultime due sezioni illustrano batch linee guida e scenari.

## <a name="batching-strategies"></a>Strategie di invio in batch
### <a name="note-about-timing-results-in-this-topic"></a>Nota sui risultati della tempistica in questo argomento
> [!NOTE]
> Risultati non sono benchmark ma intendono tooshow **prestazioni relative**. Le tempistiche si basano su una media di almeno 10 esecuzioni del test. Le operazioni sono inserimenti in una tabella vuota. Questi test sono stati misurati pre-V12 e non corrispondono necessariamente toothroughput che potrebbero verificarsi in un database V12 usando hello [livelli di servizio](sql-database-service-tiers.md). vantaggio relativo di Hello di hello tecnica di invio in batch dovrebbe essere simile.
> 
> 

### <a name="transactions"></a>Transazioni
Sembra strano toobegin una revisione dell'invio in batch parlando di transazioni. Ma utilizzare hello delle transazioni lato client dispone di un leggero effetto di invio in batch sul lato server che consente di migliorare le prestazioni. E le transazioni possono essere aggiunti con poche righe di codice, in modo che un modo rapido tooimprove di offrire prestazioni operazioni sequenziali.

Si consideri hello dopo il codice c# che contiene una sequenza di inserimento e operazioni update in una tabella semplice.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Queste operazioni vengono eseguite Hello seguente di codice ADO.NET in sequenza.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Hello toooptimize modo migliore questo codice è tooimplement qualche forma di invio in batch sul lato client di queste chiamate. Tuttavia, vi sia un modo semplice tooincrease hello delle prestazioni del codice semplicemente eseguendo il wrapping sequenza hello di chiamate in una transazione. Ecco hello stesso codice che utilizza una transazione.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Le transazioni vengono in effetti usate in entrambi questi esempi. Nel primo esempio hello, ogni singola chiamata è una transazione implicita. Nel secondo esempio hello, una transazione esplicita esegue il wrapping di tutte le chiamate di hello. Per la documentazione di hello per hello [log delle transazioni write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), i record del log sono disco toohello scaricato quando si esegue il commit delle transazioni hello. Pertanto, includendo più chiamate in una transazione, hello log delle transazioni di scrittura toohello possibile ritardare fino a quando non viene eseguito il commit delle transazioni hello. In effetti, si abilita l'invio in batch per il log delle transazioni del server di hello scritture toohello.

Hello nella tabella seguente mostra alcuni risultati di test ad hoc. eseguire i test di Hello hello che stesso sequenziale inserisce con e senza transazioni. Per maggiore chiarezza, hello primo set di test è stato eseguito in modalità remota da un database toohello portatile in Microsoft Azure. Hello secondo set di test è stato eseguito da un servizio cloud e un database entrambi residenti nello hello stesso Data Center di Microsoft Azure (Stati Uniti occidentali). Hello nella tabella seguente mostra la durata di hello in millisecondi di operazioni sequenziali di inserimento con e senza transazioni.

**On-premise tooAzure**:

| Operazioni | Senza transazione (ms) | Con transazione (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**Azure tooAzure (medesimo datacenter)**:

| Operazioni | Senza transazione (ms) | Con transazione (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

In base ai risultati dei test precedenti hello, il wrapping di una singola operazione in una transazione effettivamente riduce le prestazioni. Ma quando si aumenta il numero di hello di operazioni in una singola transazione, miglioramento delle prestazioni hello diventa più evidente. è inoltre più significativa differenza nelle prestazioni Hello quando tutte le operazioni si verificano nel Data Center di Microsoft Azure hello. Hello un aumento della latenza di utilizzo dal Data Center di Microsoft Azure hello all'esterno del Database SQL leggibile miglioramento delle prestazioni hello utilizzo delle transazioni.

Sebbene l'utilizzo di hello delle transazioni può migliorare le prestazioni, continuare troppo[osservare le procedure consigliate per le connessioni e transazioni](https://msdn.microsoft.com/library/ms187484.aspx). Mantenere transazioni hello più brevi connessione al database hello possibili e di chiusura dopo hello lavoro viene completato. istruzione using nell'esempio precedente hello Hello assicura la chiusura connessione hello termine del blocco di codice successivo hello.

Hello precedente esempio viene illustrato che è possibile aggiungere un codice ADO.NET tooany transazione locale con due righe. Le transazioni rappresentano un modo rapido le prestazioni di hello tooimprove di codice che effettua sequenza di inserimento e aggiornamento e le operazioni di eliminazione. Tuttavia, per prestazioni più veloci hello, provare a modificare hello codice tootake vantaggio dell'invio in batch sul lato client, quali i parametri con valori di tabella.

Per altre informazioni sulle transazioni in ADO.NET, vedere [Transazioni locali in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Parametri con valori di tabella
I parametri con valori di tabella supportano tipi di tabella definiti dall'utente come parametri nelle funzioni, nelle stored procedure e nelle istruzioni Transact-SQL. Questa tecnica di invio in batch sul lato client consente toosend più righe di dati all'interno di parametro con valori di tabella hello. toouse parametri con valori di tabella, innanzitutto definire un tipo di tabella. Hello istruzione Transact-SQL seguente crea un tipo di tabella denominato **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


Nel codice, si crea un **DataTable** con hello esatta stessi nomi e tipi hello del tipo di tabella. Passare l'oggetto **DataTable** in un parametro in una chiamata di stored procedure o query di testo. Hello seguente illustra questa tecnica:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

Nell'esempio precedente hello hello **SqlCommand** oggetto inserisce righe da un parametro con valori di tabella,  **@TestTvp** . Hello creato in precedenza **DataTable** oggetto viene assegnato il parametro toothis con hello **SqlCommand.Parameters.Add** metodo. Batch hello inserimenti in una chiamano in modo significativo aumenta le prestazioni di hello su operazioni sequenziali di inserimento.

tooimprove hello precedente esempio, inoltre, utilizzare una stored procedure anziché un comando basata su testo. Hello comando Transact-SQL seguente crea una stored procedure che accetta hello **SimpleTestTableType** parametro con valori di tabella.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Modificare quindi hello **SqlCommand** dichiarazione seguente toohello esempio hello precedente codice dell'oggetto.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

Nella maggior parte dei casi i parametri con valori di tabella hanno prestazioni equivalenti o superiori rispetto ad altre tecniche di invio in batch. I parametri con valori di tabella sono spesso preferibili perché più flessibili di altre opzioni. Ad esempio, altre tecniche come la copia bulk di SQL, consentono solo inserimento hello di nuove righe. Ma con i parametri con valori di tabella, è possibile utilizzare la logica in hello stored procedure toodetermine le righe da aggiornare e quelle da inserire. tipo di tabella Hello può essere modificato toocontain una colonna "Operation" che indica se hello specificata riga deve essere inserita, aggiornata o eliminata.

Hello nella tabella seguente mostra i risultati dei test ad hoc per l'utilizzo di hello di parametri con valori di tabella in millisecondi.

| Operazioni | On-premise tooAzure (ms) | Azure stesso data center (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

miglioramento delle prestazioni Hello dall'invio in batch è immediatamente evidente. Nel test sequenziale precedente hello, 1000 operazioni hanno richiesto 129 secondi hello esterno datacenter e 21 secondi all'interno di hello datacenter. Ma con i parametri con valori di tabella, 1000 operazioni richiedono invece solo 2,6 secondi all'esterno di hello datacenter e 0,4 secondi all'interno di hello datacenter.

Per altre informazioni sui parametri con valori di tabella, vedere [Usare parametri con valori di tabella (motore di database)](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Copia bulk di SQL
Copia bulk di SQL è un altro modo tooinsert grandi quantità di dati in un database di destinazione. Applicazioni .NET possono usare hello **SqlBulkCopy** operazioni di inserimento bulk tooperform di classe. **SqlBulkCopy** è simile nello strumento da riga di comando di funzione toohello, **Bcp.exe**, o istruzione Transact-SQL, hello **BULK INSERT**. Hello esempio di codice seguente viene illustrato come hello copia toobulk righe nell'origine hello **DataTable**, table, tabella di destinazione toohello in SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

In alcuni casi la copia bulk è preferibile rispetto ai parametri con valori di tabella. Vedere la tabella di confronto hello dei parametri con valori di tabella rispetto alle operazioni BULK INSERT in argomento hello [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).

risultati dei test ad hoc seguenti Hello mostrano prestazioni hello dell'invio in batch con **SqlBulkCopy** in millisecondi.

| Operazioni | On-premise tooAzure (ms) | Azure stesso data center (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

Nel batch di dimensioni minori, i parametri con valori di tabella di utilizzo hello buoni hello **SqlBulkCopy** classe. Tuttavia, **SqlBulkCopy** eseguita 12-31% più rapida rispetto ai parametri con valori di tabella per i test hello di 1.000 e 10.000 righe. Come i parametri con valori di tabella, **SqlBulkCopy** è un'opzione valida per inserimenti batch, in particolare quando confrontati toohello le prestazioni delle operazioni non in batch.

Per altre informazioni sulla copia bulk in ADO.NET, vedere [Operazioni di copia bulk in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Istruzioni INSERT con parametri a più righe
Un'alternativa per i batch di piccole dimensioni è un grande tooconstruct istruzione INSERT per inserire più righe con parametri. Hello esempio di codice seguente viene illustrata questa tecnica.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Questo esempio è ideato tooshow concetti di base hello. Uno scenario più realistico sarebbe ciclo stringa di query hello tooconstruct entità hello necessarie e i parametri del comando hello contemporaneamente. Si è limitati totale tooa 2100 parametri di query, il che limita il numero totale di hello di righe che possono essere elaborati in questo modo.

Hello seguente ad hoc testare risultati Mostra hello le prestazioni di questo tipo di istruzione insert in millisecondi.

| Operazioni | Parametri con valori di tabella (ms) | Singola istruzione INSERT (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

Questo approccio può essere leggermente più veloce per i batch minori di 100 righe. Benché miglioramento hello è piccolo, questa tecnica è un'altra opzione che potrebbe rivelarsi utile in specifici scenari applicativi.

### <a name="dataadapter"></a>DataAdapter
Hello **DataAdapter** classe consente toomodify un **DataSet** dell'oggetto e quindi inviare le modifiche di hello come operazioni INSERT, UPDATE e DELETE. Se si utilizza hello **DataAdapter** in questo modo, è importante toonote che separano le chiamate vengono eseguite per ogni distinta operazione. prestazioni tooimprove, utilizzare hello **UpdateBatchSize** numero di operazioni che devono essere raggruppate in un momento toohello della proprietà. Per altre informazioni, vedere [Esecuzione di operazioni batch usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity Framework
Entity Framework non supporta attualmente l'invio in batch. Diversi sviluppatori della community di hello sono provato a soluzioni alternative toodemonstrate, ad esempio hello override **SaveChanges** metodo. Ma hello soluzioni sono in genere applicazioni complesse e personalizzate toohello e modello di dati. progetto codeplex di Entity Framework Hello dispone attualmente di una pagina di discussione sulla richiesta di funzionalità. tooview questa discussione, vedere [Design Meeting Notes - 2 agosto 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Per motivi di completezza, riteniamo che è importante tootalk informazioni XML come strategia di invio in batch. Tuttavia, utilizzare hello di XML ha non offre vantaggi rispetto ad altri metodi e presenta numerosi svantaggi. approccio Hello è simile tootable parametri con valori di un file XML o una stringa viene passato tooa stored procedure anziché una tabella definita dall'utente. procedura Hello archiviato analizza i comandi di hello nella procedura hello archiviato.

Esistono diversi svantaggi toothis approccio:

* L'uso di XML può risultare complesso e soggetto a errori.
* Analisi hello XML nel database di hello può essere elevato della CPU.
* Nella maggior parte dei casi questo metodo è più lento rispetto ai parametri con valori di tabella.

Per questi motivi, non è invece consigliabile usare hello XML per query in batch.

## <a name="batching-considerations"></a>Considerazioni sull'invio in batch
Hello le sezioni seguenti fornisce informazioni aggiuntive per l'utilizzo di hello dell'invio in batch nelle applicazioni di Database SQL.

### <a name="tradeoffs"></a>Compromessi
A seconda dell'architettura, l'invio in batch può comportare un compromesso tra prestazioni e resilienza. Ad esempio, si consideri uno scenario di hello in cui il ruolo viene inaspettatamente disattivato. Se si perde una riga di dati, l'impatto di hello è minore di impatto hello di perdere un batch di grandi dimensioni di righe non inviate. È un rischio maggiore quando si buffer di riga prima di inviarli toohello database in un intervallo di tempo specificato.

Considerando questo compromesso, valutare il tipo di hello di operazioni da eseguire in batch. Usare più ampiamente i batch, con dimensioni maggiori e finestre temporali più ampie, per i dati meno critici.

### <a name="batch-size"></a>Dimensioni dei batch
Nei test, si è verificato in genere batch di grandi dimensioni toobreaking alcun vantaggio in blocchi più piccoli. In effetti, questa suddivisione ha causato spesso prestazioni inferiori rispetto all'invio di un singolo batch di grandi dimensioni. Ad esempio, si consideri uno scenario in cui si desidera tooinsert 1000 righe. Hello nella tabella seguente mostra il tempo impiegato parametri con valori di tabella toouse tooinsert 1000 righe divise in batch più piccoli.

| Dimensioni dei batch | Iterazioni | Parametri con valori di tabella (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

È possibile vedere che le prestazioni migliori di hello per 1000 righe sono toosubmit tutti contemporaneamente. In altri test (non mostrato qui) si è verificato un toobreak di miglioramento delle prestazioni di piccole dimensioni un batch di 10000 righe in due batch da 5000. Ma schema della tabella hello per questi test è relativamente semplice, pertanto è consigliabile eseguire test sul tooverify le dimensioni di batch e dati specifici questi risultati.

Un altro fattore tooconsider è che se il batch complessivo hello diventa troppo grande, Database SQL potrebbe applicare limitazioni e rifiutarne di batch hello toocommit. Per ottenere risultati ottimali hello, testare il toodetermine uno scenario specifico nel caso di dimensioni ideali dei batch. Rendi hello batch configurabili al runtime tooenable modifiche rapide in base alle prestazioni o gli errori.

Infine, bilanciare dimensioni hello di batch di hello con hello rischi con l'invio in batch. Se si verificano errori temporanei o ruolo hello ha esito negativo, considerare hello conseguenze di ripetere l'operazione di hello o di perdita di dati hello in batch hello.

### <a name="parallel-processing"></a>Elaborazione parallela
Cosa accade se si ha impiegato approccio hello di riduzione delle dimensioni di batch hello ma utilizzati più thread tooexecute hello lavoro? Anche in questo caso, i test indicano che diversi batch multithreading di dimensioni ridotte producono prestazioni generalmente inferiori a un singolo batch di dimensioni maggiori. Hello test seguente tenta tooinsert 1000 righe in una o più batch paralleli. Questo test indica come più batch simultanei causino in effetti una riduzione delle prestazioni.

| Dimensioni dei batch [iterazioni] | Due thread (ms) | Quattro thread (ms) | Sei thread (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> I risultati non sono benchmark. Vedere hello [nota sui risultati di temporizzazione in questo argomento](#note-about-timing-results-in-this-topic).
> 
> 

Esistono diverse potenziali cause delle prestazioni hello tooparallelism scadenza:

* Sono presenti più chiamate di rete simultanee invece di una.
* L'esecuzione di più operazioni su una singola tabella può determinare contese e blocchi.
* Il multithreading implica overhead.
* costo di Hello dell'apertura di più connessioni supera il vantaggio di hello dell'elaborazione parallela.

Se la destinazione è più tabelle o database, è possibile toosee miglioramento alcune delle prestazioni con questa strategia. Il partizionamento orizzontale o le federazioni di database rappresentano uno scenario possibile per questo approccio. Partizionamento orizzontale utilizza più database e database tooeach di route dati diversi. Se ogni piccolo batch verrà tooa diversi database, quindi l'esecuzione di operazioni di hello in parallelo può essere più efficiente. Tuttavia, miglioramento delle prestazioni di hello non è sufficientemente elevato toouse base hello per il partizionamento orizzontale di database toouse una decisione nella soluzione.

In alcune progettazioni, l'esecuzione parallela di batch di piccole dimensioni può produrre un miglioramento della velocità effettiva delle richieste in un sistema sotto carico. In questo caso, anche se è più veloce tooprocess un singolo batch di dimensioni maggiori, l'elaborazione di più batch in parallelo potrebbero risultare più efficiente.

Se si usa l'esecuzione parallela, prendere in considerazione controllo hello di numero massimo di thread di lavoro. Un numero più piccolo potrebbe ridurre il rischio di contese e i tempi di esecuzione. Inoltre, prendere in considerazione hello ulteriori carichi di lavoro che si inserisce nel database di destinazione hello sia le connessioni e transazioni.

### <a name="related-performance-factors"></a>Fattori correlati alle prestazioni
Le indicazioni tipiche relative alle prestazioni dei database influiscono anche sull'invio in batch. Le prestazioni delle operazioni di inserimento, ad esempio, risultano ridotte per le tabelle con chiave primaria di grandi dimensioni o con numerosi indici non cluster.

Se i parametri con valori di tabella utilizzano una stored procedure, è possibile utilizzare il comando hello **SET NOCOUNT ON** all'inizio di hello della procedura hello. Questa istruzione rimuove restituito hello del conteggio hello di righe interessata hello nella procedura hello. Tuttavia, nei test eseguiti, uso di hello **SET NOCOUNT ON** non aveva alcun effetto o una diminuzione delle prestazioni. Hello stored procedure di test è semplice con un singolo **inserire** dal parametro con valori di tabella hello. È possibile che stored procedure più complesse possano trarre vantaggio da questa istruzione. Non si presuppone che l'aggiunta tuttavia **SET NOCOUNT ON** tooyour stored procedure migliori automaticamente le prestazioni. toounderstand hello effetto, testare la stored procedure con e senza hello **SET NOCOUNT ON** istruzione.

## <a name="batching-scenarios"></a>Scenari di invio in batch
Hello sezioni seguenti descrivono come parametri con valori di tabella toouse in tre scenari di applicazione. Hello primo scenario illustra come la memorizzazione nel buffer e l'invio in batch possono essere usati insieme. il secondo scenario di Hello migliora le prestazioni eseguendo operazioni master / dettaglio in una chiamata a singola stored procedure. Hello nello scenario finale illustra come parametri con valori di tabella toouse in un'operazione "UPSERT".

### <a name="buffering"></a>Buffering
Sebbene alcuni scenari siano particolarmente adatti all'invio in batch, ne esistono numerosi che potrebbero trarre vantaggio da questo tipo di operazione grazie all'elaborazione ritardata. Tuttavia, anche l'elaborazione ritardata comporta un rischio maggiore hello dati vengono persi in caso di hello di un errore imprevisto. È importante toounderstand questo rischio e hello conseguenze.

Ad esempio, si consideri un'applicazione web che tiene traccia della cronologia di navigazione hello di ogni utente. In ogni richiesta di pagina, un'applicazione hello esegua visualizzazione pagina database chiamata toorecord hello dell'utente. Ma, è possibile ottenere prestazioni e scalabilità buffering delle attività di navigazione degli utenti hello e quindi invia questo database toohello dati in batch. È possibile attivare l'aggiornamento del database hello dal tempo trascorso e/o dimensione del buffer. Ad esempio, una regola è possibile specificare che tale batch hello deve essere elaborato dopo 20 secondi o quando il buffer di hello raggiunge i 1000 elementi.

codice Hello seguente viene utilizzato [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess memorizzato nel buffer gli eventi generati da una classe di monitoraggio. Quando hello riempimenti buffer o viene raggiunto un timeout, batch hello dei dati utente viene inviato toohello database con un parametro con valori di tabella.

Hello seguenti NavHistoryData classe modelli hello utente navigazione dettagli. Contiene informazioni di base, ad esempio l'identificatore utente hello, hello URL accessibili e hello tempo di accesso.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

classe NavHistoryDataMonitor Hello è responsabile del buffering database toohello di hello utente spostamento dati. Contiene un metodo RecordUserNavigationEntry che risponde generando un evento **OnAdded** . Hello codice seguente illustra la logica del costruttore hello che utilizza Rx toocreate una raccolta osservabile in base all'evento hello. Viene quindi sottoscritta la raccolta osservabile toothis con metodo hello del Buffer. overload di Hello specifica che buffer hello deve essere inviato ogni 20 secondi o 1000 voci.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

gestore Hello converte tutti gli elementi memorizzati nel buffer hello in un tipo con valori di tabella e quindi passa questa procedura tooa archiviato di tipo batch hello processi. Hello codice seguente viene illustrato definizione completa di hello per le classi NavHistoryDataMonitor hello e hello NavHistoryDataEventArgs.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse questa classe di buffering, un'applicazione hello crea un oggetto NavHistoryDataMonitor statico. Ogni volta che un utente accede a una pagina, un'applicazione hello chiama il metodo NavHistoryDataMonitor.RecordUserNavigationEntry hello. Hello logica di buffering continua tootake cure l'invio di questi database toohello voci in batch.

### <a name="master-detail"></a>Master/dettaglio
I parametri con valori di tabella sono utili per gli scenari INSERT semplici. Tuttavia, può essere più impegnativo inserimenti toobatch che coinvolgono più di una tabella. scenario "master-details" Hello è un buon esempio. la tabella master di Hello identifica l'entità primaria hello. Uno o più tabelle dettagli archiviano altri dati sull'entità hello. In questo scenario, relazioni di chiave esterna applicano relazione hello di entità master univoca di dettagli tooa. Si consideri una versione semplificata di una tabella PurchaseOrder e la tabella associata OrderDetail. Hello Transact-SQL seguente crea tabella PurchaseOrder hello con quattro colonne: lo stato, OrderDate, CustomerID e OrderID.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Ogni ordine contiene uno o più acquisti di prodotti. Queste informazioni vengono acquisite nella tabella PurchaseOrderDetail hello. Hello Transact-SQL seguente crea tabella PurchaseOrderDetail hello con cinque colonne: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

colonna OrderID Hello nella tabella PurchaseOrderDetail hello deve fare riferimento a un ordine dalla tabella PurchaseOrder hello. Hello seguente definizione di una chiave esterna applica il vincolo.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

In parametri con valori di tabella toouse di ordine, è necessario disporre di un tipo di tabella definito dall'utente per ogni tabella di destinazione.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Definire quindi una stored procedure che accetti tabelle di questi tipi. Questa procedura consente a un batch di toolocally applicazione un set di ordini e dettagli ordine in una singola chiamata. Hello Transact-SQL seguente fornisce hello dichiarazione di stored procedure completa per questo esempio di ordine di acquisto.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

In questo esempio hello definite localmente @IdentityLink tabella archivia hello OrderID i valori effettivi dalle righe appena inserita hello. Questi identificatori di ordine sono diversi dai valori OrderID temporanei hello in hello @orders e @details parametri con valori di tabella. Per questo motivo, hello @IdentityLink tabella collega quindi i valori OrderID hello in hello @orders toohello reale OrderID valori dei parametri per le nuove righe hello nella tabella PurchaseOrder hello. Dopo questo passaggio, hello @IdentityLink tabella può facilitare l'inserimento dei dettagli ordine hello con hello OrderID effettivo che soddisfa il vincolo di chiave esterna di hello.

Questa stored procedure può essere utilizzata dal codice o da altre chiamate Transact-SQL. Nella sezione hello parametri con valori di tabella di questo articolo per un esempio di codice. Hello Transact-SQL seguente viene illustrato come toocall hello sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Questa soluzione consente a un set di valori OrderID che iniziano da 1 toouse ogni batch. Questi valori OrderID temporanei descrivono le relazioni di hello in batch hello ma hello effettivo OrderID valori vengono determinati in fase di hello dell'operazione di inserimento hello. È possibile eseguire hello stesse istruzioni nell'esempio precedente hello ripetutamente e generare gli ordini univoci nel database di hello. Per questo motivo, considerare l'aggiunta di più logica di database o di codice che impedisca gli ordini duplicati quando si usa questa tecnica di invio in batch.

In questo esempio viene spiegato che è possibile eseguire in batch anche operazioni di database più complesse, ad esempio operazioni master/dettaglio, usando i parametri con valori di tabella.

### <a name="upsert"></a>UPSERT
Un altro scenario di invio in batch prevede l'aggiornamento simultaneo di righe esistenti e l'inserimento di nuove righe. Questa operazione è talvolta tooas cui un'operazione "UPSERT" (aggiornamento + inserimento). Anziché eseguire chiamate separate tooINSERT e l'aggiornamento, istruzione MERGE hello è più adatta toothis attività. Hello istruzione MERGE può eseguire sia insert e operazioni in una singola chiamata di aggiornamento.

Parametri con valori di tabella possono essere utilizzati con hello MERGE istruzione tooperform aggiornamenti e inserimenti. Si consideri ad esempio una tabella Employee semplificata contenente hello seguenti colonne: EmployeeID, FirstName, LastName, SocialSecurityNumber:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

In questo esempio, è possibile utilizzare hello fatto tale hello SocialSecurityNumber univoco tooperform un'unione di più dipendenti. Creare innanzitutto il tipo di tabella definito dall'utente hello:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Successivamente, creare una stored procedure oppure scrivere codice che usa hello aggiornamento hello tooperform istruzione di tipo MERGE e insert. Hello esempio seguente viene utilizzata hello istruzione MERGE in un parametro con valori di tabella, @employees, di tipo EmployeeTableType. contenuto di hello Hello @employees tabella non vengono visualizzati qui.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Per ulteriori informazioni, vedere la documentazione di hello ed esempi per l'istruzione MERGE hello. Sebbene hello stessa operazione possa essere eseguita in più passaggi chiamata alla stored procedure con operazioni INSERT e UPDATE separate, hello istruzione MERGE è più efficiente. Codice del database è inoltre possibile creare chiamate Transact-SQL che utilizzano l'istruzione MERGE hello direttamente senza richiedere due chiamate di database per INSERT e UPDATE.

## <a name="recommendation-summary"></a>Riepilogo delle indicazioni
Hello elenco riportato di seguito viene fornito un riepilogo di hello batch raccomandazioni descritte in questo argomento:

* Utilizzare la memorizzazione nel buffer e l'invio in batch tooincrease hello prestazioni e scalabilità delle applicazioni di Database SQL.
* Comprendere i compromessi hello tra l'invio in batch/buffering e resilienza. Durante un errore di ruolo, il rischio di hello di perdere un batch non elaborato di dati aziendali critici superiore a quello previsto miglioramento delle prestazioni hello dell'invio in batch.
* Tentativo tookeep tutti i database toohello chiamate all'interno di una latenza tooreduce singolo Data Center.
* Se si sceglie una tecnica di invio in batch singola, i parametri con valori di tabella offrono flessibilità e prestazioni ottimali hello.
* Per più veloce hello inserire le prestazioni, seguire queste linee guida generali ma testare lo scenario:
  * Per < 100 righe, usare un singolo comando INSERT con parametri.
  * Per < 1000 righe usare parametri con valori di tabella.
  * Per >= 1000 righe usare SqlBulkCopy.
* Per aggiornare e le operazioni di eliminazione, utilizzare i parametri con valori di tabella con logica della stored procedure che determina il corretto funzionamento di hello in ogni riga nel parametro tabella hello.
* Linee guida sulle dimensioni dei batch:
  * Utilizzare hello più grande le dimensioni di batch in base allo scopo dell'applicazione e i requisiti aziendali.
  * Il miglioramento delle prestazioni di hello saldo di batch di grandi dimensioni con rischio di hello di errori temporanei o irreversibili. Qual è la conseguenza hello di tentativi o perdita di dati hello in batch hello? 
  * Test hello più grande batch dimensioni tooverify che il Database SQL non li respinga.
  * Creare le impostazioni di configurazione di tale controllo invio in batch, ad esempio la dimensione del batch hello o finestra temporale di buffering hello. Queste impostazioni offrono flessibilità. È possibile modificare l'invio in batch comportamento nell'ambiente di produzione senza ridistribuire il servizio di cloud hello hello.
* Evitare l'esecuzione parallela di batch che operano su una singola tabella in un database. Se si sceglie un singolo batch toodivide tra più thread di lavoro, eseguire test toodetermine hello numero ideale di thread. Dopo una soglia non specificata, più thread determinano una riduzione delle prestazioni invece di un aumento.
* Considerare il buffering in base a dimensioni e tempo come modalità di implementazione dell'invio in batch per più scenari.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo attivando la modalità progettazione di database e le tecniche di codifica correlati toobatching può migliorare le prestazioni dell'applicazione e la scalabilità. Questo è però solo uno dei fattori della strategia complessiva. Per altre prestazioni tooimprove modi e scalabilità, vedere [linee guida sulle prestazioni di Database SQL di Azure per singoli database](sql-database-performance-guidance.md) e [prezzo e considerazioni sulle prestazioni per un pool elastico](sql-database-elastic-pool-guidance.md).

