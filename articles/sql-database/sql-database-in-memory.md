---
title: tecnologie di Database SQL In memoria aaaAzure | Documenti Microsoft
description: Tecnologie In memoria del Database SQL Azure migliorare notevolmente le prestazioni di hello delle transazioni e i carichi di lavoro analitica. Informazioni su come tootake sfruttare tali tecnologie.
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Ottimizzare le prestazioni tramite le tecnologie in memoria nel database SQL

Tramite le tecnologie in memoria del database SQL di Azure, è possibile migliorare le prestazioni di diversi carichi di lavoro: transazionale (elaborazione transazionale online o OLTP), analitica (elaborazione analitica online o OLAP) e mista (elaborazione ibrida transazione/analitica o HTAP). A causa di hello query più efficienti e l'elaborazione delle transazioni, le tecnologie In memoria consentono anche di costo tooreduce. In genere non occorre hello tooupgrade tariffario hello database tooachieve dei miglioramenti delle prestazioni. In alcuni casi, potrebbe anche essere possibile ridurre hello tariffario, mentre ancora osservare i miglioramenti delle prestazioni con le tecnologie In memoria.

Di seguito sono riportati due esempi di come OLTP In memoria consentito toosignificantly migliorare le prestazioni:

- Con OLTP In memoria, [Quorum soluzioni di Business è stato in grado di toodouble relativo carico di lavoro migliorando Dtu del 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU significa *unità di velocità effettiva database* e include una misurazione del consumo di risorse.
- Hello video seguente viene illustrato un miglioramento significativo del consumo di risorse con un carico di lavoro di esempio: [OLTP In memoria in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Per ulteriori informazioni, vedere hello post di blog: [OLTP In memoria in cui il Post di Blog di Azure SQL Database](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Tecnologie in memoria sono disponibili in tutti i database nel livello Premium hello, inclusi i database nel pool elastico Premium.

Hello video seguente viene illustrato potenziali miglioramenti delle prestazioni con le tecnologie In memoria nel Database di SQL Azure. Tenere presente che miglioramento delle prestazioni di hello che viene visualizzato sempre dipende da molti fattori, tra cui natura hello del carico di lavoro di hello e dati, il criterio di accesso del database di hello e così via.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Database SQL di Azure è hello seguenti tecnologie In memoria:

- *OLTP in memoria*: aumenta la velocità effettiva e riduce la latenza per l'elaborazione delle transazioni. Gli scenari che beneficiano dell'OLTP in memoria sono: elaborazione transazionale ad alta velocità di elaborazione, come l'inserimento di dati commerciali e da videogiochi, da eventi o dispositivi IoT, il caching, il caricamento di dati, le tabelle temporanee e gli scenari con variabili di tabella.
- *Indici columnstore cluster* ridurre il footprint di memoria (i tempi di too10) e migliorare le prestazioni per le query di creazione di report e analitica. È possibile utilizzarlo con le tabelle dei fatti in toofit di data mart i dati più dati nel database e migliorare le prestazioni. Inoltre, è possibile utilizzarlo con i dati cronologici in tooarchive il database operativo ed essere in grado di tooquery too10 ore di più dati.
- *Indici columnstore non cluster* per help HTAP si toogain approfondite in tempo reale dell'azienda tramite l'esecuzione di query hello operational database direttamente, senza hello necessità toorun un'estrazione dispendiosa, trasformazione e il processo di caricamento (ETL) e in attesa per hello dati warehouse toobe popolato. Indici columnstore non cluster consentono l'esecuzione molto rapida delle query analitica nel database OLTP di hello, riducendo l'impatto di hello sul carico di lavoro operativo hello.
- È anche possibile combinazione di hello di una tabella con ottimizzazione per la memoria con un indice columnstore. Questa combinazione consente tooperform molto rapida elaborazione delle transazioni e troppo*contemporaneamente* fase analitica esegue una query molto rapidamente sul hello stessi dati.

Sia gli indici columnstore e OLTP In memoria sono stati parte del prodotto SQL Server hello sin 2012 e 2014, rispettivamente. Database SQL di Azure e SQL Server condividono hello stessa implementazione delle tecnologie In memoria. In futuro, le nuove funzionalità per queste tecnologie verranno integrate prima nel database SQL di Azure e poi in SQL Server.

In questo argomento vengono descritti gli aspetti di OLTP In memoria e columnstore indici tooAzure specifico Database SQL e vengono forniti esempi di:
- Si noterà impatto hello di queste tecnologie, sui limiti di dimensioni di archiviazione e i dati.
- Verrà visualizzato come toomanage hello lo spostamento di database che utilizzano queste tecnologie tra hello livelli di prezzo diverso.
- Si noterà due esempi che illustrano l'utilizzo di hello di OLTP In memoria, nonché gli indici columnstore in Database SQL di Azure.

Hello seguenti risorse per ulteriori informazioni, vedere.

Informazioni dettagliate sulle tecnologie di hello:

- [Panoramica di OLTP in memoria e scenari di utilizzo](https://msdn.microsoft.com/library/mt774593.aspx) (include riferimenti toocustomer case study e informazioni tooget avviato)
- [OLTP in memoria](http://msdn.microsoft.com/library/dn133186.aspx)
- [Descrizione degli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx)
- L'elaborazione analitica e transazionale ibrida (HTAP), anche nota come [analisi operativa in tempo reale](https://msdn.microsoft.com/library/dn817827.aspx)

Riportata una breve spiegazione su OLTP In memoria: [avvio rapido 1: tecnologie OLTP In memoria per più rapidamente le prestazioni di T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (un altro articolo toohelp iniziare)

Video dettagliate sulle tecnologie di hello:

- [OLTP in memoria nel Database di SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (che contiene una dimostrazione delle prestazioni vantaggi e i passaggi tooreproduce questi risultati manualmente)
- [Video OLTP in memoria: Che cos'è e quando e come toouse,](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Indice ColumnStore: Video sull'analisi in memoria da Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Dimensioni di archiviazione e dati

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Limite su dimensioni dei dati e archiviazione per OLTP in memoria

OLTP in memoria include tabelle con ottimizzazione per la memoria, che vengono usate per archiviare i dati utente. Queste tabelle sono necessarie toofit in memoria. Perché vengono gestiti memoria direttamente nel servizio di Database SQL di hello, abbiamo concetto hello di una quota per i dati utente. Questo concetto è noto tooas *archiviazione OLTP In memoria*.

Ogni piano tariffario relativo a database autonomi e pool elastici supportati include una certa quantità di spazio di archiviazione OLTP in memoria. In fase di hello di scrittura, si ottiene un gigabyte di spazio di archiviazione per ogni unità di transazione database (Dtu) 125 o di un database elastico (Edtu) di unità di transazione.

Hello [livelli di servizio di Database SQL](sql-database-service-tiers.md) articolo ha elenco ufficiale di hello hello OLTP In memoria di archiviazione di disponibili per ogni database autonomo e il pool elastico piano tariffario.

Hello dopo il numero di elementi verso l'estremità di archiviazione di OLTP In memoria:

- Righe di dati utente attive nelle tabelle con ottimizzazione per la memoria e variabili di tabella. Si noti che le versioni precedenti di riga non conteggiati per cap hello.
- Indici nelle tabelle con ottimizzazione per la memoria.
- Costi operativi delle operazioni ALTER TABLE.

Se si raggiunge il limite di hello, viene visualizzato un errore di quota di uscita e, non sarà più in grado di tooinsert o aggiornamento di dati. toomitigate questo errore, eliminare i dati o aumentare hello a livello di database hello o un pool di prezzo.

Per informazioni dettagliate sul monitoraggio di utilizzo di spazio di archiviazione di OLTP In memoria e la configurazione degli avvisi quando quasi raggiunto limite massimo di hello, vedere [archiviazione di monitoraggio In memoria](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Informazioni sui pool elastici

Il pool elastico, hello archiviazione OLTP In memoria è condivisa tra tutti i database nel pool di hello. Pertanto, utilizzo di hello in un database può influire altri database. Esistono due metodi per la risoluzione di questo problema:

- Consente di configurare un numero massimo-eDTU per database che è inferiore al numero di eDTU hello per il pool di hello nel suo complesso. Questo valore massimo per le coperture spazio di archiviazione OLTP In memoria hello, in qualsiasi database nel pool di hello, dimensioni toohello corrispondente numero di eDTU toohello.
- Configurare Min-eDTU su un valore maggiore di 0. Questo modo si garantisce che ogni database nel pool di hello quantità hello di archiviazione di OLTP In memoria disponibile corrispondente toohello minimo configurato Min eDTU.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Dimensioni dei dati e archiviazione per gli indici columnstore

Gli indici ColumnStore non sono necessari toofit in memoria. Pertanto, hello solo limite dimensione hello degli indici hello è hello dimensione massima complessiva del database, che è documentato in hello [livelli di servizio di Database SQL](sql-database-service-tiers.md) articolo.

Quando si utilizzano gli indici columnstore cluster, la compressione a colonne viene utilizzata per l'archiviazione di tabelle di base hello. Questo tipo di compressione può ridurre notevolmente il footprint di memoria hello dei dati utente, il che significa che è possibile inserire più dati nel database di hello. E la compressione di hello può essere ulteriormente aumentata con [la compressione dell'archivio colonne](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). quantità di Hello della compressione che è possibile ottenere dipende dalla natura hello dei dati di hello, ma la compressione di 10 volte hello non è insolita.

Ad esempio, se si dispone di un database con una dimensione massima di 1 terabyte (TB) e per ottenere la compressione di 10 volte hello utilizzare gli indici columnstore, è possibile adattare un totale di 10 TB di dati dell'utente nel database di hello.

Quando si utilizzano gli indici columnstore non cluster, tabella di base hello è ancora archiviata in formato rowstore tradizionali hello. Pertanto, hello risparmi di archiviazione non sono grandi come con gli indici columnstore cluster. Tuttavia, se si desidera sostituire un numero di indici non cluster tradizionale con un indice columnstore singolo, è possibile visualizzare ancora un risparmio in footprint di memoria hello per tabella hello complessivo.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Spostamento dei database tra i piani tariffari tramite tecnologie in memoria

Esistono mai eventuali incompatibilità o altri problemi quando si esegue l'aggiornamento tooa superiore tariffario, ad esempio da tooPremium Standard. risorse e funzionalità disponibili hello solo aumentano.

Ma hello downgrade tariffario può influire negativamente del database. impatto di Hello è particolarmente evidente quando esegue il downgrade da Premium tooStandard o di base per il database contiene oggetti di OLTP In memoria. Le tabelle con ottimizzazione per la memoria e gli indici columnstore, sono disponibili dopo il downgrade di hello (anche se rimangono visibili). Hello stesse considerazioni si applicano quando si sta riducendo hello a livello di un pool elastico di prezzo o spostamento di un database con le tecnologie In memoria, in uno Standard o Basic pool elastico.

### <a name="in-memory-oltp"></a>OLTP in memoria

*Downgrade tooBasic/Standard*: OLTP In memoria non è supportato nei database di livello Standard o Basic hello. Inoltre, non è possibile toomove un database che include qualsiasi toohello oggetti OLTP In memoria livello Standard o Basic.

Prima effettuare il downgrade hello database tooStandard/Basic, rimuovere tutte le tabelle con ottimizzazione per la memoria e i tipi di tabella, nonché tutti i moduli T-SQL compilati in modo nativo.

Se un determinato database supporta OLTP In memoria è toounderstand un livello di codice. È possibile eseguire hello query Transact-SQL seguente:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Se la query hello restituisce **1**, OLTP In memoria è supportato in questo database.


*Il downgrade di livello Premium inferiore tooa*: dati nelle tabelle con ottimizzazione per la memoria devono essere contenuta in archiviazione di OLTP In memoria hello che è associato a hello piano tariffario del database hello o nel pool elastico hello è disponibile. Se si tenta di hello toolower livello di prezzo o spostare database hello in un pool che non dispone di sufficiente spazio di archiviazione di OLTP In memoria disponibile, hello operazione ha esito negativo.

### <a name="columnstore-indexes"></a>Indici Columnstore

*Downgrade Standard o tooBasic*: gli indici sono supportati solo nel piano tariffario Premium hello e non in Columnstore hello livelli Standard o Basic. Quando si esegue il downgrade del database tooStandard o Basic, l'indice columnstore non è più disponibile. sistema di Hello mantiene l'indice columnstore, ma mai sfrutta indice hello. Se si aggiorna in un secondo momento tooPremium indietro, l'indice columnstore è immediatamente pronto toobe utilizzati nuovamente.

Se dispone di un **cluster** indice columnstore, intera tabella hello diventa disponibile dopo il downgrade di livello. Pertanto è consigliabile eliminare tutti *cluster* di indici columnstore prima effettuare il downgrade del database di sotto di livello Premium hello.

*Il downgrade di livello Premium inferiore tooa*: questa operazione ha esito positivo se l'intero database hello rientra nelle dimensioni massime del database hello per destinazione hello livello di prezzo o all'interno dell'archiviazione disponibile nel pool elastico hello hello. Non ha alcun impatto determinato dagli indici columnstore hello.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Installare l'esempio di OLTP In memoria hello

È possibile creare il database di esempio AdventureWorksLT hello con pochi clic nel hello [portale di Azure](https://portal.azure.com/). Quindi, hello passaggi in questa sezione illustrano come è possibile arricchire il database AdventureWorksLT con gli oggetti di OLTP In memoria e illustrano i vantaggi delle prestazioni.

Per una dimostrazione più semplice e visivamente più interessante sulle prestazioni di OLTP in memoria, vedere:

- Versione: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Codice sorgente: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Procedura di installazione

1. In hello [portale di Azure](https://portal.azure.com/), creare un database Premium in un server. Set hello **origine** toohello database di esempio AdventureWorksLT. Per istruzioni dettagliate, vedere [Creare il primo database SQL di Azure](sql-database-get-started-portal.md).

2. La connessione a database toohello con SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Hello copia [script Transact-SQL di In-Memory OLTP](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour Appunti. Hello script T-SQL hello crea oggetti In memoria necessarie nel database di esempio AdventureWorksLT hello creato nel passaggio 1.

4. Incollare lo script T-SQL di hello in SQL Server Management Studio e quindi eseguire script hello. Hello `MEMORY_OPTIMIZED = ON` istruzioni CREATE TABLE sono fondamentali. ad esempio:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Errore 40536


Se viene visualizzato l'errore 40536 quando si esegue script hello T-SQL, eseguire hello seguente tooverify script T-SQL se il database di hello supporta In memoria:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Se il risultato è **0**, le funzionalità in memoria non sono supportate, mentre **1** indica che sono supportate. problema di hello toodiagnose, assicurarsi che il database hello sia a livello di servizio Premium hello.


#### <a name="about-hello-created-memory-optimized-items"></a>Sui hello creata articoli con ottimizzazione per la memoria

**Tabelle**: esempio hello contiene hello le tabelle con ottimizzazione per la memoria seguenti:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


È possibile esaminare le tabelle con ottimizzazione per la memoria tramite hello **Esplora oggetti** in SQL Server Management Studio. Fare doppio clic su **Tabelle** > **Filtro** > **Impostazioni filtro** > **Con ottimizzazione per la memoria**. il valore di Hello è uguale a 1.


In alternativa, è possibile eseguire query viste del catalogo hello, ad esempio:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Stored procedure compilata in modo nativo**: è possibile esaminare SalesLT.usp_InsertSalesOrder_inmem usando una query delle viste del catalogo.


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Eseguire il carico di lavoro di hello esempio OLTP

l'unica differenza tra i due seguenti hello Hello *stored procedure* che prima procedura hello utilizza le versioni con ottimizzazione per la memoria delle tabelle di hello, hello durante la seconda procedura utilizza tabelle su disco normali hello:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


In questa sezione viene visualizzato come toouse hello utile **ostress.exe** tooexecute utilità hello due stored procedure senza livelli. È possibile confrontare il tempo impiegato per hello due stress esecuzioni toofinish.


Quando si esegue ostress.exe, è consigliabile passare valori di parametro progettate per entrambi i seguenti hello:

- Eseguire un numero elevato di connessioni simultanee, usando -n100.
- Ripetere ogni ciclo di connessione centinaia di volte, usando -r500.


Tuttavia, è consigliabile toostart con valori inferiori come - tooensure n10 e - r50 che funzionino.


### <a name="script-for-ostressexe"></a>Script per ostress.exe


In questa sezione Visualizza script T-SQL hello incorporato della linea di comando ostress.exe. script di Hello utilizza gli elementi creati da hello script T-SQL che è installato in precedenza.


Hello lo script seguente inserisce un ordine di vendita di esempio con cinque voci seguenti hello con ottimizzazione per la memoria *tabelle*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


hello toomake *ondisk* versione di hello precedente script T-SQL per ostress.exe, si devono sostituire entrambe le occorrenze di hello *inmem* substring con *ondisk*. Queste sostituzioni interessano nomi hello delle tabelle e stored procedure.


### <a name="install-rml-utilities-and-ostress"></a>Installare le utilità RML e ostress


Idealmente, è possibile pianificare toorun ostress.exe in una macchina virtuale di Azure (VM). Si creerà un [macchina virtuale di Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello stessa area geografica Azure in cui risiede il database AdventureWorksLT. È possibile eseguire ostress.exe sul computer portatile.


In hello macchina virtuale o in qualsiasi host è scegliere, installare le utilità di hello riproduzione Markup Language (RML). utilità di Hello includono ostress.exe.

Per altre informazioni, vedere:
- Hello discussione ostress.exe in [Database di esempio per OLTP In memoria](http://msdn.microsoft.com/library/mt465764.aspx).
- [Database di esempio per OLTP in memoria](http://msdn.microsoft.com/library/mt465764.aspx).
- Hello [blog per l'installazione ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Eseguire hello *inmem* stress prima del carico di lavoro


È possibile utilizzare un *prompt comandi RML* toorun finestra la riga di comando ostress.exe. i parametri della riga di comando Hello diretta ostress per:

- Eseguire 100 connessioni simultaneamente (-n100).
- Ogni connessione eseguire script T-SQL hello 50 volte (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


hello toorun ostress.exe della riga di comando precedente:


1. Reimpostare il contenuto di dati di hello database tramite l'esecuzione di tutti i dati che è stati inseriti da tutte le esecuzioni precedenti hello hello in SSMS, toodelete comando seguente:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Copiare il testo hello di hello precedente ostress.exe riga di comando tooyour Appunti.

3. Sostituire hello `<placeholders>` per hello parametri -S - U -P -d con hello correggere i valori reali.

4. Eseguire la riga di comando modificata in una finestra dei comandi RML.


#### <a name="result-is-a-duration"></a>Il risultato è un intervallo di tempo


Al termine, ostress.exe scrive hello durata di esecuzione come riga finale di output nella finestra Cmd RML hello. Ad esempio, per un'esecuzione dei test più breve, durata circa 1,5 minuti:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Reimpostare, modificare per l'esecuzione *_ondisk* ed eseguire di nuovo il test


Dopo aver risultato hello hello *inmem* esecuzione, eseguire hello alla procedura seguente per hello *ondisk* eseguire:


1. Ripristina database hello mediante l'esecuzione di tutti i dati che è stati inseriti da hello precedente esecuzione hello hello in SSMS toodelete comando seguente:
```
EXECUTE Demo.usp_DemoReset;
```

2. Modifica hello ostress.exe riga di comando tooreplace tutti *inmem* con *ondisk*.

3. Eseguire di nuovo ostress.exe per hello seconda volta e acquisire i risultati di durata hello.

4. Nuovamente, reimpostare hello (per l'eliminazione in modo responsabile di ciò che può essere una grande quantità di dati di test).


#### <a name="expected-comparison-results"></a>Risultati previsti per il confronto

I test In memoria hanno dimostrato che le prestazioni migliorate **nove volte** per questo carico di lavoro semplice, con ostress in esecuzione in una macchina virtuale di Azure in hello stessa regione di Azure come database hello.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Installare: esempio hello Analitica In memoria


In questa sezione è confrontare hello IO e risultati delle statistiche quando si utilizza un indice columnstore e un indice albero b tradizionale.


Per analitica in tempo reale in un carico di lavoro OLTP, spesso è migliore toouse un indice columnstore non cluster. Per informazioni dettagliate, vedere [Descrizione degli indici columnstore](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Preparare hello columnstore analitica test


1. Utilizzare hello toocreate portale Azure un nuovo database AdventureWorksLT tratto dall'esempio hello.
 - Usare esattamente questo nome.
 - Scegliere qualsiasi livello di servizio Premium.

2. Hello copia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour Appunti.
 - Hello script T-SQL hello crea oggetti In memoria necessarie nel database di esempio AdventureWorksLT hello creato nel passaggio 1.
 - script di Hello Crea tabella della dimensione hello e due tabelle dei fatti. le tabelle dei fatti Hello vengono popolate con 3,5 milioni di righe ognuno.
 - script Hello potrebbe richiedere toocomplete 15 minuti.

3. Incollare lo script T-SQL di hello in SQL Server Management Studio e quindi eseguire script hello. Hello **COLUMNSTORE** parola chiave in hello **CREATE INDEX** istruzione è fondamentale, come in:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Impostare il livello di toocompatibility AdventureWorksLT 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Livello 130 non funzionalità memoria tooIn direttamente correlati. ma offre in genere prestazioni delle query più veloci rispetto al livello 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tabelle e indici columnstore fondamentali


- dbo. FactResellerSalesXL_CCI è una tabella che include un indice columnstore cluster, che offre avanzati per la compressione a hello *dati* livello.

- dbo. FactResellerSalesXL_PageCompressed è una tabella con un equivalente regolare indice cluster, che è compressi solo a hello *pagina* livello.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Indice di chiave di query toocompare hello columnstore


Esistono [diversi tipi di query T-SQL che è possibile eseguire](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee miglioramenti delle prestazioni. Nel passaggio 2 in hello script T-SQL, si paga coppia toothis attenzione di query. Le due query differiscono per una sola riga:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Un indice columnstore cluster è in hello FactResellerSalesXL\_tabella CCI.

Hello estratto di script T-SQL seguente stampa le statistiche dei / o e l'ora di query hello di ogni tabella.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

In un database con livello di prezzo hello P2, è possibile prevedere circa nove volte hello miglioramento delle prestazioni per la query utilizzando l'indice columnstore cluster hello confrontato con un indice tradizionale hello. Con P15, è possibile prevedere miglioramento delle prestazioni di hello circa 57 volte utilizzando l'indice columnstore hello.



## <a name="next-steps"></a>Passaggi successivi

- [Avvio rapido 1: Tecnologie OLTP in memoria per ottimizzare le prestazioni di T-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.](sql-database-in-memory-oltp-migration.md)

- [Monitoraggio dell'archiviazione OLTP in memoria](sql-database-in-memory-oltp-monitoring.md) per OLTP in memoria.


## <a name="additional-resources"></a>Risorse aggiuntive

#### <a name="deeper-information"></a>Approfondimenti

- [Informazioni in Learn how Quorum doubles key database's workload while lowering DTU by 70% with In-Memory OLTP in SQL Databas](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database) (Il quorum raddoppia il carico di lavoro del database principale riducendo il DTU del 70% con OLTP in memoria nel database SQL)

- [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/) (Post di blog su OLTP nel database SQL di Azure)

- [Informazioni su OLTP in memoria](http://msdn.microsoft.com/library/dn133186.aspx)

- [Informazioni sugli indici columnstore](https://msdn.microsoft.com/library/gg492088.aspx)

- [Informazioni sulle analisi operative in tempo reale](http://msdn.microsoft.com/library/dn817827.aspx)

- Vedere l'articolo sui [modelli comuni dei carichi di lavoro e considerazioni relative alla migrazione](http://msdn.microsoft.com/library/dn673538.aspx), che descrive modelli di carico di lavoro in cui OLTP in memoria fornisce in genere miglioramenti significativi delle prestazioni

#### <a name="application-design"></a>Progettazione di applicazioni

- [OLTP in memoria (ottimizzazione in memoria)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Usare OLTP in memoria in un'applicazione esistente del database SQL di Azure.](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Strumenti

- [Portale di Azure](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SQL Server Data Tools (SSDT)](http://msdn.microsoft.com/library/mt204009.aspx)
