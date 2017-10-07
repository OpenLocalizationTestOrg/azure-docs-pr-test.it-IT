---
title: libreria client di database elastico aaaUsing con Dapper | Documenti Microsoft
description: Utilizzo della libreria client dei database elastici con Dapper.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Utilizzo della libreria client dei database elastici con Dapper
Questo documento è destinata agli sviluppatori che si basano sulle applicazioni toobuild Dapper, ma desidera anche tooembrace [degli strumenti di database elastico](sql-database-elastic-scale-introduction.md) toocreate applicazioni che implementano tooscale partizionamento orizzontale in orizzontale il livello dati.  Questo documento vengono illustrate le modifiche di hello nelle applicazioni basate su Dapper che sono necessarie toointegrate con gli strumenti di database elastico. L'obiettivo è la composizione di gestione di partizioni di database elastico hello e dipendente dai dati di routing con Dapper. 

**Codice di esempio**: [Strumenti dei database elastici per il database SQL di Azure - Integrazione con Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

L'integrazione **Dapper** e **DapperExtensions** hello libreria client di database elastici per Database SQL di Azure in modo semplice. L'applicazione può utilizzare dati routing modificando la creazione di hello e l'apertura di nuovi dipendenti [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello toouse oggetti [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chiamare da hello [client libreria](http://msdn.microsoft.com/library/azure/dn765902.aspx). Consente di limitare le modifiche in tooonly l'applicazione in cui le nuove connessioni vengono create e aperto. 

## <a name="dapper-overview"></a>Informazioni generali su Dapper
**Dapper** è un mapper object-relational. Eseguire il mapping di oggetti .NET dai database relazionali di tooa dell'applicazione (e viceversa). prima parte di Hello hello del codice di esempio viene illustrato come integrare libreria client di database elastico hello con le applicazioni basate su Dapper. seconda parte di Hello hello del codice di esempio viene illustrato come toointegrate quando si utilizza Dapper sia DapperExtensions.  

funzionalità di BizTalk mapper Hello Dapper fornisce metodi di estensione per le connessioni di database che semplificano l'invio di istruzioni T-SQL per l'esecuzione o l'esecuzione di query database hello. Ad esempio, Dapper rende facile toomap tra gli oggetti di .NET e i parametri hello delle istruzioni SQL per **Execute** chiamate o tooconsume hello risultati delle query SQL in oggetti .NET utilizzando **Query**chiamate da Dapper. 

Quando si utilizza DapperExtensions, non è più necessario istruzioni SQL di tooprovide hello. Metodi di estensione, ad esempio **GetList** o **inserire** su connessione al database hello creare istruzioni SQL in background hello hello.

Un altro vantaggio della Dapper, nonché DapperExtensions è che i controlli dell'applicazione hello hello creazione della connessione al database hello. Ciò consente di interagire con una libreria client di database elastico hello che le connessioni basate su mapping hello di shardlet toodatabases Broker del database.

assembly di hello tooget Dapper, vedere [Dapper punto net](http://www.nuget.org/packages/Dapper/). Per le estensioni di Dapper hello, vedere [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Una libreria client di database elastico hello sintesi
Libreria client di database elastico hello definire le partizioni di dati dell'applicazione denominati *shardlet* , eseguirne il mapping toodatabases e identificarli da *chiavi di partizionamento orizzontale*. È possibile disporre di tutti i database desiderati e distribuire gli shardlet su tali database. mapping di Hello dei database toohello valori di chiave di partizionamento orizzontale vengono archiviati per una mappa partizioni fornita dalle API della libreria hello. Questa funzionalità è denominata **gestione mappe partizioni**. mappa partizioni Hello funge anche da Service broker hello di connessioni di database per le richieste che contengono una chiave di partizionamento orizzontale. Questa funzionalità è denominata tooas **routing dipendente dai dati**.

![Mappe di partizione e routing dipendente dai dati][1]

gestore mappe partizioni di Hello protegge gli utenti da visualizzazioni incoerenti nei dati di shardlet che possono verificarsi quando vengono eseguite operazioni di gestione di shardlet simultanee sui database hello. toodo hello in tal caso, partizioni mappe broker hello connessioni al database per un'applicazione compilata con la libreria hello. Quando le operazioni di gestione di partizioni potrebbe influire sulla hello shardlet, in questo modo kill tooautomatically funzionalità di hello partizioni mappa una connessione al database. 

Anziché utilizzare le connessioni di hello modalità tradizionale toocreate per Dapper, dobbiamo hello toouse [OpenConnectionForKey metodo](http://msdn.microsoft.com/library/azure/dn824099.aspx). Ciò garantisce che tutte le convalide hello viene eseguita e le connessioni vengono gestite correttamente quando si sposta tutti i dati tra le partizioni.

### <a name="requirements-for-dapper-integration"></a>Requisiti per l'integrazione con Dapper
Quando si utilizza la libreria di client di database elastico hello e hello API Dapper, desideriamo hello tooretain le proprietà seguenti:

* **Scalabilità orizzontale**: si desidera tooadd o rimuovere i database dal livello dati hello applicazione partizionati hello necessarie per le esigenze di capacità hello di un'applicazione hello. 
* **Coerenza**: poiché l'applicazione è scalabilità tramite il partizionamento orizzontale, è necessario tooperform routing dipendente dai dati. È necessario pertanto toouse hello dati dipendenti funzionalità di routing di hello libreria toodo. In particolare, si desidera la convalida di hello tooretain e garanzie di coerenza per le connessioni che sono negoziate mediante gestore mappe partizioni di hello danneggiamento tooavoid ordine o risultati di query non corretto. Ciò garantisce che tooa di connessioni specificato shardlet vengono rifiutati o arrestato se (per l'istanza) shardlet hello è attualmente spostato tooa partizione diversa utilizzando le API di suddivisione/unione.
* **Mapping degli oggetti**: vogliamo praticità hello tooretain di mapping hello fornito da Dapper tootranslate tra le classi in un'applicazione hello e hello strutture di database sottostanti. 

Hello seguente sezione vengono fornite linee guida per i seguenti requisiti per le applicazioni basate su **Dapper** e **DapperExtensions**.

## <a name="technical-guidance"></a>Indicazioni tecniche
### <a name="data-dependent-routing-with-dapper"></a>Routing dipendente dai dati con Dapper
Con Dapper, un'applicazione hello è in genere responsabile della creazione e l'apertura di hello connessioni toohello database sottostante. Dato un tipo T da un'applicazione hello, Dapper restituisce risultati della query come raccolte di .NET di tipo T. Dapper esegue il mapping di hello da oggetti toohello righe hello T-SQL risultato di tipo T. Analogamente, Dapper esegue il mapping di oggetti .NET in valori SQL o i parametri per istruzioni data manipulation language (DML). Dapper offre questa funzionalità tramite i metodi di estensione in hello regolare [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) oggetto dalle librerie Client di SQL ADO .NET hello. connessione SQL restituita dall'API di scalabilità elastica hello per DDR Hello sono anche regolare [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) oggetti. In questo modo toodirectly utilizzano le estensioni Dapper su hello tipo restituito dall'API di DDR della libreria client hello, perché è anche una semplice connessione a SQL Client.

Queste osservazioni rendono semplice toouse connessioni negoziate dalla libreria client di database elastico hello per Dapper.

Questo esempio di codice (da hello che accompagna esempio) di seguito viene illustrato l'approccio hello in cui la chiave di partizionamento orizzontale hello viene fornita da hello applicazione toohello libreria toobroker hello connessione toohello destra partizioni.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Hello chiamata toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API sostituisce creazione predefinita hello e apertura di una connessione SQL Client. Hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chiamata accetta argomenti di hello necessari per il routing dipendente dai dati: 

* Hello partizioni mappa tooaccess hello interfacce di routing dipendente di dati
* Hello shardlet hello tooidentify chiave di partizionamento orizzontale
* partizioni toohello tooconnect di Hello credenziali (nome utente e password)

oggetto mappa partizioni di Hello crea una partizione toohello connessione che contiene shardlet hello per hello data chiave di partizionamento orizzontale. API client di database elastico Hello tag anche tooimplement connessione hello garantisce la consistenza. Poiché hello chiamare troppo[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) restituisce un oggetto di connessione SQL Client regolare, hello chiamata successiva toohello **Execute** metodo di estensione da segue Dapper hello Dapper standard procedure consigliate.

Le query molto lavoro hello stesso modo - Apertura connessione hello usando [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) da client hello API. È quindi utilizzare risultati hello estensione Dapper regolare metodi toomap hello della query SQL in oggetti .NET:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Si noti che hello **utilizzando** blocco con gli ambiti di connessione DDR hello tutte le operazioni di database all'interno di hello blocco toohello una partizione in cui è stato conservato tenantId1. query Hello restituisce solo i blog archiviati nella partizione corrente hello, ma non hello quelli memorizzati su eventuali altre partizioni. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Routing dipendente dai dati con Dapper e DapperExtensions
Dapper dotato di un ecosistema di estensioni aggiuntive che possono fornire ulteriori motivi di praticità e astrazione dal database hello durante lo sviluppo di applicazioni di database. Un esempio è rappresentato da DapperExtensions. 

L'uso di DapperExtensions nell'applicazione non comporta la modifica della modalità di creazione e gestione delle connessioni di database. È comunque connessioni tooopen di responsabilità dell'applicazione hello e oggetti di connessione SQL Client normali previsti da metodi di estensione hello. È possibile affidarsi hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) come illustrato in precedenza. Hello esempi di codice seguenti illustrano, hello unica differenza sarà che non è più disponibile istruzioni T-SQL hello toowrite:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

E l'esempio di codice hello per query hello: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Gestione degli errori temporanei
Hello Microsoft Patterns & Practices team hello pubblicato [Transient Fault Handling Application Block](http://msdn.microsoft.com/library/hh680934.aspx) gli sviluppatori di applicazioni toohelp attenuare condizioni comuni di errori temporanei durante l'esecuzione nel cloud hello. Per ulteriori informazioni, vedere [Perseverance, segreto tutti luogo: hello Transient Fault Handling Application Block utilizzando](http://msdn.microsoft.com/library/dn440719.aspx).

Nell'esempio di codice Hello si basa su hello errori temporanei della libreria tooprotect contro gli errori temporanei. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** in hello codice precedente viene definito come un **SqlDatabaseTransientErrorDetectionStrategy** con un numero di tentativi di 10 e 5 secondi di attesa tra i tentativi. Se si utilizzano transazioni, assicurarsi che l'ambito di tentativi viene reimpostato toohello dall'inizio della transazione hello in caso di hello di un errore temporaneo.

## <a name="limitations"></a>Limitazioni
approcci Hello descritti nel presente documento comportano un paio di limitazioni:

* codice di esempio Hello per questo documento viene illustrato come schema toomanage tra partizioni.
* Data una richiesta, si presuppone che l'elaborazione di tutti i relativi database è contenuto all'interno di una singola partizione come identificato dalla chiave di partizionamento orizzontale hello fornita dalla richiesta hello. Tuttavia, questo presupposto non sempre contenere, ad esempio, quando non è possibile toomake una chiave di partizionamento orizzontale disponibile. tooaddress, hello libreria client di database elastico include hello [MultiShardQuery classe](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). classe Hello implementa un'astrazione di connessione per l'esecuzione di query su più partizioni. Utilizzo di MultiShardQuery in combinazione con Dapper esula dall'ambito di hello di questo documento.

## <a name="conclusion"></a>Conclusioni
Le applicazioni che usano Dapper e DapperExtensions possono trarre vantaggio facilmente dagli strumenti dei database elastici del database SQL di Azure. Passaggi hello descritte nel presente documento, tali applicazioni possono utilizzare funzionalità dello strumento hello per dipendenti routing modificando la creazione di hello e aprire i nuovi dati [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello toouse oggetti [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) chiamata della libreria client di database elastico hello. Questo limita hello applicazione le modifiche necessarie toothose posizioni in cui le nuove connessioni vengono create e aperto. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
