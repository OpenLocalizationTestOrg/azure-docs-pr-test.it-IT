---
title: prestazioni del Database SQL aaaAzure indicazioni di ottimizzazione | Documenti Microsoft
description: "In questo articolo consente di determinare quali toochoose del livello di servizio per l'applicazione. Consiglia inoltre di modi tootune il hello tooget applicazione meglio le potenzialità di Database SQL di Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Ottimizzazione delle prestazioni del database SQL di Azure

Database SQL di Azure fornisce [indicazioni](sql-database-advisor.md) che è possibile utilizzare tooimprove delle prestazioni del database, o lasciare il Database di SQL Azure [si adattano automaticamente applicazione tooyour](sql-database-automatic-tuning.md) e applicare le modifiche che migliorerà le prestazioni del carico di lavoro.

È, non sono disponibili raccomandazioni applicabile e avere problemi di prestazioni, è possibile utilizzare hello prestazioni tooimprove metodi seguenti:
1. Aumentare [livelli di servizio](sql-database-service-tiers.md) e fornire ulteriori risorse tooyour database.
2. Ottimizzare l'applicazione e applicare alcune procedure consigliate che consentono di migliorare le prestazioni. 
3. Ottimizzare i database di hello modificando gli indici e query toomore utilizzo efficiente di dati.

Questi sono metodi manuali perché è necessario toodecide cosa [livelli di servizio](sql-database-service-tiers.md) scegliere o che sarebbero necessari toorewrite applicazione o del codice del database e di distribuire le modifiche di hello.

## <a name="increasing-performance-tier-of-your-database"></a>Aumento del livello di prestazioni del database

Il servizio Database SQL di Azure offre quattro [livelli di servizio](sql-database-service-tiers.md) tra cui scegliere: Basic, Standard, Premium e Premium RS (le prestazioni sono misurate in unità di trasmissione dati del database o [DTU](sql-database-what-is-a-dtu.md)). Ogni livello di servizio isola rigorosamente risorse hello, che è possibile utilizzare l'oggetto del database SQL e garantisce prestazioni prevedibili per il livello di servizio. In questo articolo è offrono informazioni aggiuntive che consentono di scegliere il livello di servizio hello per l'applicazione. Vengono anche illustrati modi che è possibile ottimizzare il hello tooget applicazione meglio le potenzialità di Database SQL di Azure.

> [!NOTE]
> Questo articolo è incentrato sulle indicazioni relative alle prestazioni per singoli database nel database SQL di Azure. Per linee guida sulle prestazioni pool tooelastic correlate, vedere l'articolo [prezzo e considerazioni sulle prestazioni per il pool elastico](sql-database-elastic-pool-guidance.md). Si noti, tuttavia, che è possibile applicare molte delle indicazioni nelle toodatabases articolo in un pool elastico di ottimizzazione hello e ottenere prestazioni simili.
> 

* **Base**: prevedibilità hello base del servizio livello offre buone prestazioni per ogni database, l'ora in ore. In un database Basic una quantità di risorse sufficiente supporta prestazioni ottimali in un database di piccole dimensioni senza richieste simultanee multiple. I casi di utilizzo tipici in cui si usa il livello di servizio Basic sono:
  * **Si sta iniziando a usare il database SQL di Azure**. Le applicazioni sottoposte spesso a sviluppo non necessitano di livelli di prestazioni elevati. I database Basic costituiscono un ambiente ideale per lo sviluppo o il test di database a una fascia di prezzo conveniente.
  * **È presente un database con un singolo utente**. Le applicazioni in cui un singolo utente è associato a un database non sono in genere caratterizzate da requisiti elevati per concorrenza e prestazioni. Queste applicazioni sono candidati per il livello di servizio Basic hello.
* **Standard**: livello di servizio Standard hello offre prestazioni migliorate prevedibilità e offre buone prestazioni per i database con più richieste simultanee, ad esempio applicazioni web e il gruppo di lavoro. Quando si sceglie un database con livello di servizio Standard, è possibile ridimensionare le applicazioni di database in base alle prestazioni prevedibili minuto per minuto.
  * **Il database presenta più richieste simultanee**. Le applicazioni che gestiscono più utenti contemporaneamente necessitano in genere di livelli di prestazioni più elevate. Ad esempio, gruppo di lavoro o web applicazioni con requisiti di traffico dei / o toomedium bassa che supporta più query contemporaneamente sono buoni candidati per il livello di servizio Standard hello.
* **Premium**: livello di servizio Premium hello offre prestazioni prevedibili, secondo, in secondo luogo, per ogni database Premium. Quando si sceglie il livello di servizio Premium hello, è possibile ridimensionare l'applicazione di database in base al carico di picco hello per quel database. piano Hello Elimina casi in cui la varianza di prestazioni può causare piccole query tootake più tempo del previsto in operazioni sensibili alla latenza. Questo modello può semplificare notevolmente i cicli di convalida di sviluppo e prodotto hello per le applicazioni che richiedono toomake dichiarazioni forti sulle esigenze di risorse di picco, varianza di prestazioni o la latenza delle query. La maggior parte dei casi d'uso del livello di servizio Premium presenta una o più di queste caratteristiche:
  * **Picchi di carico elevati**. Un'applicazione che richiede notevole CPU, memoria o input/output (i/o) toocomplete delle operazioni richiede un livello dedicato ad alte prestazioni. Più core CPU per un periodo di tempo prolungato, ad esempio, un'operazione di database noti tooconsume è un candidato per il livello di servizio Premium hello.
  * **Molte richieste simultanee**. Alcune applicazioni di database gestiscono molte richieste simultanee, ad esempio durante l'utilizzo di un sito Web con un elevato volume di traffico. Basic e Standard i livelli di servizio limitare il numero di hello di richieste simultanee per ogni database. Le applicazioni che richiedono ulteriori connessioni dovrebbero essere toochoose un prenotazione appropriate dimensioni toohandle hello numero massimo di richieste necessarie.
  * **Bassa latenza**. Alcune applicazioni richiedono una risposta dal database hello tooguarantee in tempi minimi. Se la stored procedure viene chiamata come parte di un'operazione più ampia del cliente, potrebbe essere un requisito toohave restituito dalla chiamata di una in non più di 20 millisecondi, 99 per cento di tempo hello. Questo tipo di prestazioni dell'applicazione dal livello di servizio Premium hello, verificare che tale hello potenza di elaborazione toomake è disponibile.
* **Premium RS**: hello livello RS Premium è progettato per i carichi di lavoro con utilizzo intensivo dei / o che non richiedono hello garanzie di disponibilità più elevate. Esempi di test ad alte prestazioni dei carichi di lavoro o un carico di lavoro analitico in database hello non sistema hello del record.

livello di servizio Hello che è necessario per il database SQL dipende dai requisiti di carico di picco di hello per ogni dimensione di risorsa. È possibile che alcune applicazioni usino quantità irrilevanti di una singola risorsa, ma abbiano requisiti significativi per altre.

### <a name="service-tier-capabilities-and-limits"></a>Limiti e funzionalità dei livelli di servizio

A ogni livello di servizio, impostare il livello di prestazioni hello, in modo che sia hello flessibilità toopay solo per la capacità di hello che è necessario. È possibile [regolare la capacità](sql-database-service-tiers.md), in base alle modifiche del carico di lavoro. Ad esempio, se il carico di lavoro del database è elevato durante hello back-a-acquisti scuola, è possibile aumentare il livello di prestazioni hello per database hello per un determinato periodo di tempo, luglio a settembre. È quindi possibile ridurlo al termine del picco stagionale. È possibile ridurre i costi ottimizzando la stagionalità toohello di ambiente cloud dell'azienda. Questo modello è adatto anche per i cicli di rilascio di prodotti software. Un team di test può allocare la capacità durante l'esecuzione di test e quindi rilasciare tale capacità al termine dei test. In un modello basato sulla richiesta di capacità, si paga la capacità necessaria, evitando i costi per risorse dedicate usate raramente.

### <a name="why-service-tiers"></a>Vantaggi dei livelli di servizio
Anche se ogni carico di lavoro di database può variare, scopo hello dei livelli di servizio è tooprovide prevedibilità di prestazioni a vari livelli di prestazioni. I clienti con requisiti di risorse di database su larga scala possono operare in un ambiente di calcolo più dedicato.

## <a name="tune-your-application"></a>Ottimizzare l'applicazione
In SQL Server on-premise tradizionale il processo di hello della pianificazione della capacità iniziale spesso è separato dal processo hello di esecuzione di un'applicazione nell'ambiente di produzione. Vengono acquistate prima di tutto le licenze per hardware e prodotti e l'ottimizzazione delle prestazioni viene eseguita in un secondo momento. Quando si utilizza Database SQL di Azure, è un processo di hello buona toointerweave di esecuzione di un'applicazione e l'ottimizzazione. Con il modello di hello di pagamento per la capacità su richiesta, è possibile ottimizzare le risorse dell'applicazione toouse hello minime necessarie a questo punto, invece di effettuare l'overprovisioning nell'hardware in base a ipotesi di piani di crescita futura per un'applicazione, che spesso non sono corrette. Alcuni clienti potrebbero scegliere di non tootune un'applicazione e scegliere invece toooverprovision risorse hardware. Se non si desidera toochange un'applicazione chiave in un periodo di tempo occupato, questo approccio può essere una buona idea. Tuttavia, l'ottimizzazione di un'applicazione consente di ridurre i requisiti di risorse e ridurre i costi mensili quando si usano livelli di servizio hello in Database SQL di Azure.

### <a name="application-characteristics"></a>Caratteristiche dell'applicazione
Anche se i livelli di servizio di Database SQL di Azure sono progettate tooimprove prestazioni stabilità e la prevedibilità per un'applicazione, alcune procedure consigliate consentono di ottimizzare l'applicazione toobetter sfruttare le risorse di hello con un livello di prestazioni. Sebbene molte applicazioni dispongono di miglioramenti significativi delle prestazioni semplicemente da cambio tooa maggiore livello di prestazioni o un servizio di livello, alcune applicazioni è necessario ulteriore ottimizzazione toobenefit da un livello superiore del servizio. Per ottenere un aumento delle prestazioni, prendere in considerazione operazioni di ottimizzazione aggiuntive per le applicazioni con queste caratteristiche:

* **Applicazioni con prestazioni ridotte a causa di un comportamento "eccessivamente comunicativo"**. Applicazioni "frammentate" eseguire operazioni di accesso di un numero eccessivo di dati che sono sensibili toonetwork latenza. Potrebbe essere necessario toomodify questi tipi di applicazioni tooreduce hello numerosi dati accesso operazioni toohello al database SQL. Ad esempio, è possibile migliorare le prestazioni dell'applicazione utilizzando tecniche come l'invio in batch di query ad hoc o lo spostamento di una query hello toostored procedure. Per altre informazioni, vedere [Invio di query in batch](#batch-queries).
* **Database con un carico di lavoro elevato che non possono essere supportati da una singola macchina virtuale intera**. Database che superano le risorse di hello del livello di prestazioni Premium più elevato hello potrebbero trarre vantaggio dalla scalabilità orizzontale del carico di lavoro di hello. Per altre informazioni, vedere [Partizionamento orizzontale tra database](#cross-database-sharding) e [Partizionamento funzionale](#functional-partitioning).
* **Applicazioni con query non ottimali**. Le applicazioni, specialmente quelle nel livello di accesso ai dati hello, che con query non ottimizzate non possono trarre vantaggio da un livello di prestazioni superiore. Tra queste sono incluse query prive della clausola WHERE, con indici mancanti o con statistiche obsolete. Queste applicazioni possono trarre vantaggio dalle tecniche standard di ottimizzazione delle prestazioni delle query. Per altre informazioni, vedere [Indici mancanti](#identifying-and-adding-missing-indexes) e [Hint/Ottimizzazione di query](#query-tuning-and-hinting).
* **Applicazioni con struttura di accesso ai dati non ottimale**. Le applicazioni con problemi intrinseci di concorrenza per l'accesso ai dati, ad esempio il deadlock, potrebbero non trarre vantaggio da un livello di prestazioni superiore. Provare a ridurre i round trip contro hello Database SQL di Azure per la memorizzazione dei dati sul lato client hello con hello del servizio di Caching di Azure o un'altra tecnologia di memorizzazione nella cache. Vedere [Memorizzazione nella cache a livello di applicazione](#application-tier-caching).

## <a name="tune-your-database"></a>Ottimizzare il database
In questa sezione verranno esaminate alcune tecniche che è possibile utilizzare tootune Database SQL di Azure toogain hello migliori prestazioni per l'applicazione ed eseguirla a livello di prestazioni più basso hello. Alcune di queste tecniche corrispondono consigliate di ottimizzazione tradizionali di SQL Server, mentre altre sono specifiche tooAzure Database SQL. In alcuni casi, è possibile esaminare le risorse di hello utilizzata per un'ottimizzazione di database toofind aree toofurther ed estendere toowork tecniche di SQL Server tradizionale in Database SQL di Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identificare i problemi di prestazioni usando il portale di Azure
Hello seguenti strumenti di hello portale di Azure consentono di analizzare e risolvere i problemi di prestazioni con il database SQL:

* [Query Performance Insight](sql-database-query-performance.md)
* [Advisor per database SQL](sql-database-advisor.md)

Hello portale di Azure dispone di ulteriori informazioni su entrambi gli strumenti e come toouse li. tooefficiently diagnosticare e correggere i problemi, è consigliabile innanzitutto provare gli strumenti di hello in hello portale di Azure. È consigliabile utilizzare manuale hello ottimizzazione approcci che è illustrato più avanti, per gli indici e ottimizzazione delle query, in casi particolari mancanti.

Altre informazioni sull'identificazione dei problemi in Database SQL di Azure sono disponibili nell'articolo sul [monitoraggio delle prestazioni](sql-database-single-database-monitor.md).

### <a name="identifying-and-adding-missing-indexes"></a>Identificazione e aggiunta di indici mancanti
Un problema comune nelle prestazioni del database OLTP è correlato toohello progettazione fisica del database. Spesso gli schemi di database vengono progettati e forniti senza verificare la scala (nel caricamento o nel volume di dati). Purtroppo, le prestazioni di hello di un piano di query potrebbero essere accettabili su scala ma peggiorare notevolmente in volumi di dati a livello di produzione. l'origine più comune di questo problema Hello è la mancanza di hello di filtri toosatisfy indici adatti o altre restrizioni in una query. La mancanza di indici si manifesta spesso con una scansione di tabella quando potrebbe essere sufficiente una ricerca dell'indice.

In questo esempio, il piano di query selezionato hello utilizza una scansione quando invece basterebbe una ricerca:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Piano di query con indici mancanti](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

Il database SQL di Azure può consentire di trovare e risolvere condizioni comuni di indici mancanti. Esaminare le compilazioni di query in cui un indice potrebbe ridurre in modo significativo toorun costo stimato hello una query DMV incorporate nel Database SQL di Azure. Durante l'esecuzione di query, Database SQL rileva la frequenza con cui viene eseguito ogni piano di query e hello tracce stimato gap tra l'esecuzione del piano di query e di hello hello immaginare uno in cui tale indice esistente. È possibile utilizzare queste ipotesi tooquickly DMV quali modifiche tooyour progettazione fisica del database potrà migliorare il costo complessivo del carico di lavoro per un database e il relativo carico di lavoro reale.

È possibile utilizzare questo potenziale tooevaluate query degli indici mancanti:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

In questo esempio, la query hello ha restituito il suggerimento:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Dopo la sua creazione, la stessa istruzione SELECT sceglie un piano diverso, che utilizza una ricerca anziché un'analisi e quindi esegue in modo più efficiente piano hello:

![Piano di query con indici corretti](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

informazione chiave Hello è la capacità dei / o di una scheda SCSI hello, sistema apposito è più limitato rispetto a quello di un computer dedicato. È un vantaggio nella riduzione inutili i/o tootake massimo i vantaggi del sistema hello in hello DTU di ciascun livello di prestazioni dei livelli di servizio di Database SQL di Azure hello. Scelte di progettazione fisica del database appropriato in modo significativo possono migliorare latenza hello per le singole query, migliorare la velocità effettiva di hello di richieste simultanee gestite per unità di scala e ridurre al minimo la query di hello hello costi toosatisfy obbligatorio. Per ulteriori informazioni su hello mancante DMV dell'indice, vedere [Sys.dm db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Hint/Ottimizzazione di query
Hello query optimizer nel Database di SQL Azure è simile toohello tradizionali query optimizer di SQL Server. La maggior parte delle procedure consigliate di hello per ottimizzare le query e hello comprensione ragionamento delle limitazioni del modello per query optimizer di hello anche applicare tooAzure Database SQL. Se è ottimizzare le query in Database SQL di Azure, è possibile ottenere l'ulteriore vantaggio di hello di ridurre le richieste di risorse aggregate. L'applicazione potrebbe essere in grado di toorun a un costo inferiore rispetto a un equivalente gli perché può essere eseguito in un livello di prestazioni inferiore.

Un esempio che è comune in SQL Server e che si applica anche tooAzure Database SQL è come hello query optimizer "analizza" parametri. Durante la compilazione, query optimizer di hello valuta hello corrente valore toodetermine un parametro, se è possibile generare un piano di query ottimale. Sebbene questa strategia, spesso può causare tooa piano di query notevolmente più veloce rispetto a un piano compilato senza i valori dei parametri noti, attualmente funziona presentare sia in SQL Server e Database SQL di Azure. In alcuni casi il parametro hello è trasmissioni non e talvolta viene rilevato la presenza di parametro hello piano generato hello è ottimale per il set completo di hello di valori di parametro in un carico di lavoro. Microsoft include l'hint per la query (direttive) in modo che è possibile specificare la finalità più deliberatamente ed eseguire l'override di comportamento predefinito hello lo sniffing dei parametri. Spesso, se si utilizzano parametri, è possibile risolvere i casi in cui il comportamento di SQL Server o Database SQL di Azure predefinito hello è perfetto per un carico di lavoro del cliente specifico.

Hello esempio successivo viene illustrato come hello query processor può generare un piano non ottimale sia per le prestazioni e requisiti di risorse. L'esempio mostra anche che l'uso di un hint di query può consentire di ridurre il tempo di esecuzione delle query e i requisiti delle risorse per il database SQL:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

il codice di installazione di Hello crea una tabella che è inclinata di distribuzione dei dati. query ottimale di Hello piano differisce basata sul quale parametro sia selezionato. Sfortunatamente, il piano di hello comportamento di memorizzazione nella cache non sempre Ricompila query hello in base al valore di parametro più comune di hello. In tal caso, è possibile che un toobe piani non ottimali memorizzati nella cache e usato per molti valori, anche quando un piano diverso potrebbe essere preferibile piano medio. Piano di query hello crea quindi due stored procedure che sono identiche, ad eccezione del fatto che uno è un hint per la query speciale.

**Esempio (parte 1)**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Esempio (parte 2)**

(È consigliabile attendere almeno 10 minuti prima di iniziare la parte 2 di esempio hello, in modo che i risultati di hello in sono distinti hello i dati di telemetria risultante).

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Ogni parte dell'esempio tenta toorun un'istruzione insert con parametri 1.000 volte (toogenerate un toouse carico sufficiente come set di dati di test). Durante l'esecuzione di stored procedure, hello query processor viene esaminato il valore parametro hello passato toohello procedure durante la prima compilazione ("sniffing dei parametri"). processore Hello memorizza nella cache piano risultante hello e viene utilizzato per le chiamate successive, anche se il valore di parametro hello è diverso. piano ottimale Hello potrebbe non essere usata in tutti i casi. Talvolta è necessario tooguide hello optimizer toopick un piano che è preferibile per metà dei casi hello anziché caso specifico di hello dalla query hello quando compilato prima. In questo esempio, il piano iniziale hello genera un piano "analisi" che legge tutte le righe toofind ciascun valore corrispondente parametro hello:

![Ottimizzazione delle query mediante un piano di analisi](./media/sql-database-performance-guidance/query_tuning_1.png)

Poiché è eseguito procedure hello utilizzando hello valore 1, piano risultante hello ottimale per il valore di hello 1 non è ottimale per tutti gli altri valori di tabella hello. non è risultato Hello probabile che potrebbe desiderare se fosse toopick ogni piano in modo casuale, poiché il piano di hello vengono eseguite più lentamente e utilizza più risorse.

Se si esegue il test di hello con `SET STATISTICS IO` impostare troppo`ON`, il lavoro di scansione logica hello in questo esempio viene eseguito in background hello. Si noterà che sono 1,148 letture eseguite dal piano hello (che è inefficiente, hello metà dei casi viene tooreturn una sola riga):

![Ottimizzazione delle query mediante un'analisi logica](./media/sql-database-performance-guidance/query_tuning_2.png)

seconda parte di Hello dell'esempio hello utilizza una query hint tootell hello optimizer toouse un valore specifico durante il processo di compilazione hello. In questo caso, viene forzato hello query processor tooignore hello valore passato come parametro hello, e invece tooassume `UNKNOWN`. Si riferisce valore tooa con frequenza media hello nella tabella hello (ignorando lo sfasamento dei segnali). piano risultante Hello è un piano basato su ricerca è più veloce e Usa meno risorse, in Media, rispetto al piano hello nella parte 1 di questo esempio:

![Ottimizzazione delle query mediante un hint di query](./media/sql-database-performance-guidance/query_tuning_3.png)

È possibile visualizzare l'effetto di hello in hello **resource_stats** tabella (si verifica un ritardo di hello esecuzione di test hello e quando dati hello popolano la tabella hello). Per questo esempio, parte 1 eseguite durante l'intervallo di tempo 22:25:00 hello e parte 2 eseguita alle 22:35:00. Hello intervallo di tempo precedente altre risorse utilizzate in tale intervallo di tempo di hello versione più recente (a causa dei miglioramenti di efficienza di piano).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Risultati di esempio di ottimizzazione delle query](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Anche se il volume di hello in questo esempio è intenzionalmente piccolo, effetto hello di parametri non ottimali può essere significativo, in particolare nel database di grandi dimensioni. differenza Hello, in casi estremi, può essere di secondi per i casi veloci e ore per i casi lenta.
> 
> 

È possibile esaminare **resource_stats** toodetermine se la risorsa hello per un test utilizza più o meno risorse rispetto a un altro test. Quando si confrontano i dati, separare la temporizzazione hello di test in modo che non si trovano in hello stessa finestra di 5 minuti in hello **resource_stats** visualizzazione. Hello obiettivo dell'esercizio hello è totale hello toominimize delle risorse usate e risorse non di toominimize hello punta. In genere, anche con l'ottimizzazione di una parte di codice per la latenza viene ridotto il consumo di risorse. Assicurarsi che le modifiche di hello apportate tooan applicazione sono necessari e che i hello cambiamenti non incidano negativamente analisi utilizzo software per un utente che potrebbero utilizzare hint per la query in un'applicazione hello hello.

Se un carico di lavoro dispone di un set di ripetizione delle query, spesso effettua senso toocapture e convalidare validità hello delle scelte piano perché l'unità di hello minima dimensione unità toohost obbligatorio hello database resource. Dopo la convalida, in alcuni casi il riesame piani hello che toohelp è assicurarsi che la validità. Per altre informazioni, vedere [Hint per la query (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Partizionamento orizzontale tra database
Poiché il Database SQL di Azure viene eseguito su hardware apposito, limiti della capacità hello per un singolo database sono inferiori a quelli di un'installazione di SQL Server locale tradizionali. Alcuni clienti di utilizzare operazioni di database toospread tecniche di partizionamento orizzontale in più database quando le operazioni di hello non rientrano hello limiti di un singolo database nel Database SQL di Azure. La maggior parte dei clienti che usa le tecniche di partizionamento orizzontale nel database SQL di Azure suddivide i dati di una singola dimensione in più database. Per questo approccio, è necessario che le applicazioni OLTP eseguono spesso le transazioni che si applicano tooonly una riga o tooa piccolo gruppo di righe dello schema di hello toounderstand.

> [!NOTE]
> Database SQL offre ora un tooassist libreria con il partizionamento orizzontale. Per altre informazioni, vedere [Panoramica della libreria client dei database elastici](sql-database-elastic-database-client-library.md).
> 
> 

Ad esempio, se un database include il nome del cliente, ordine e dettagli dell'ordine (ad esempio, hello database Northwind di esempio tradizionale fornito con SQL Server), è possibile suddividere questi dati in più database raggruppando un cliente con hello ordine e dettagli ordine correlati informazioni. È possibile garantire il recupero di che dati del cliente hello rimangono in un singolo database. un'applicazione Hello, diversi clienti verrà suddivisi tra database, estendendo di fatto hello carico tra più database. Con il partizionamento orizzontale, i clienti possono non solo evitare hello limite delle dimensioni massime del database, ma il Database di SQL Azure può elaborare anche i carichi di lavoro che sono significativamente maggiori a limiti di hello hello diversi livelli di prestazioni, purché ogni singolo database rientri nel relativo DTU.

Anche se non viene ridotto capacità di risorse aggregate hello per una soluzione di partizionamento orizzontale di database, è estremamente efficiente nel supportare soluzioni di grandi dimensioni che vengono distribuite in più database. Ogni database è possibile eseguire in un diverso prestazioni livello toosupport molto grande, "effettivo" database con requisiti di risorse elevato.

### <a name="functional-partitioning"></a>Partizionamento funzionale
Gli utenti di SQL Server combinano spesso molte funzioni all'interno di un singolo database. Ad esempio, se un'applicazione abbia un inventario toomanage logica per un archivio, che il database potrebbe essere logica associata a inventario, il rilevamento di ordini di acquisto, le stored procedure e viste indicizzate o materializzate che Gestione dei report di fine mese. Questa tecnica rende più semplice database di hello tooadminister per operazioni quali backup, ma richiede anche si toosize hello hardware toohandle hello carico massimo in tutte le funzioni di un'applicazione.

Se si utilizza un'architettura di scalabilità orizzontale nel Database di SQL Azure, è una buona toosplit varie funzioni di un'applicazione in database diversi. Se si usa questa tecnica, ogni applicazione viene ridimensionata in modo indipendente. Quando un'applicazione viene utilizzata con maggiore frequenza (e hello carico aumenta database hello), amministratore di hello può scegliere i livelli di prestazioni indipendente per ogni funzione in un'applicazione hello. In limite hello, con questa architettura, un'applicazione può essere maggiore di una singola macchina apposita è possibile gestire perché carico hello è suddiviso in più computer.

### <a name="batch-queries"></a>Invio di query in batch
Per le applicazioni che accedono ai dati con volumi elevati, frequenti, la query ad hoc, una notevole quantità di tempo di risposta viene impiegata per la comunicazione di rete tra il livello di applicazione hello e hello Database SQL di Azure. Anche se entrambi hello applicazione e Database SQL di Azure sono in hello elementi nello stesso data center, la latenza di rete tra due hello hello potrebbe essere aumentato da un numero elevato di operazioni di accesso ai dati. rete hello tooreduce arrotondamento di viaggi per i dati di hello operazioni di accesso, è possibile utilizzare le query ad hoc di hello opzione tooeither batch hello o toocompile come stored procedure. Se si batch di query ad hoc hello, è possibile inviare più query come un unico grande batch in tooAzure una singola operazione Database SQL. Se si esegue la compilazione di query ad hoc in una stored procedure, è possibile ottenere hello che stesso risultato, come se i batch di essi. L'utilizzo di una stored procedure inoltre offre hello vantaggio di aumentare la probabilità hello della memorizzazione nella cache i piani di query hello in Database SQL di Azure, è possibile utilizzare hello stored procedure di nuovo.

Alcune applicazioni comportano un utilizzo elevato di scrittura. In alcuni casi è possibile ridurre carico i/o totale hello in un database considerando come toobatch scrive insieme. Questa operazione è spesso semplice come l'uso di transazioni esplicite anziché di transazioni autocommit in stored procedure e batch ad hoc. Per una valutazione delle differenti tecniche che si possono usare, vedere [Tecniche di esecuzione in batch per applicazioni del database SQL in Azure](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Sperimentare il proprio carico di lavoro toofind hello del modello per l'invio in batch. Essere toounderstand assicurarsi che un modello potrebbe essere leggermente garantisce la coerenza transazionale diverse. Trovare hello giusto carico di lavoro che riduce l'utilizzo delle risorse, è necessario individuare hello corretta combinazione di prestazioni e coerenza compromessi.

### <a name="application-tier-caching"></a>Memorizzazione nella cache a livello di applicazione
Alcune applicazioni di database contengono carichi di lavoro con intensa attività di lettura. Livelli di memorizzazione nella cache potrebbe ridurre il carico hello sul database hello e potrebbe potenzialmente ridurre toosupport richiesto livello hello prestazioni un database con Database SQL di Azure. Con [Cache Redis di Azure](https://azure.microsoft.com/services/cache/), se si dispone di un carico di lavoro con intensa attività di lettura, è possibile leggere una sola volta dati hello (o forse una volta per ogni computer a livello di applicazione, a seconda del tipo di configurazione) e quindi archiviare i dati all'esterno del database SQL. Si tratta di un carico modo tooreduce database (CPU e lettura i/o), ma è un effetto sulla coerenza transazionale poiché i dati di hello da leggere dalla cache di hello potrebbero essere sincronizzati con i dati di hello nel database di hello. Anche se in molte applicazioni è accettabile un livello di incoerenza, ciò non rappresenta una soluzione valida per tutti i carichi di lavoro. È necessario conoscere bene tutti i requisiti delle applicazioni prima di implementare una strategia di caching a livello di applicazione.

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sui livelli di servizio, vedere [Opzioni e prestazioni disponibili in ogni livello di servizio del database SQL](sql-database-service-tiers.md)
* Per altre informazioni sui pool elastici, vedere [Informazioni sui pool elastici di Azure](sql-database-elastic-pool.md)
* Per informazioni sui pool elastico e prestazioni, vedere [quando tooconsider un pool elastico](sql-database-elastic-pool-guidance.md)

