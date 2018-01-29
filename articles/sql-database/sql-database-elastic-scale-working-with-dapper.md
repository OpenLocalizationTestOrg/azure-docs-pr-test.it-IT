---
title: Uso della libreria client di database elastico con Dapper | Microsoft Docs
description: Utilizzo della libreria client dei database elastici con Dapper.
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: Inactive
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c258b1859e14d9783a3dfa75431b69bef4d640fd
ms.sourcegitcommit: dfd49613fce4ce917e844d205c85359ff093bb9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/31/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Utilizzo della libreria client dei database elastici con Dapper
Questo documento è rivolto agli sviluppatori che si basano su Dapper per creare applicazioni, ma desiderano avvalersi degli [strumenti dei database elastici](sql-database-elastic-scale-introduction.md) per creare applicazioni che implementano il partizionamento per la scalabilità orizzontale del livello dati.  Questo documento illustra le modifiche da apportare nelle applicazioni basate su Dapper per l'integrazione con gli strumenti dei database elastici. L'obiettivo è comporre la gestione delle partizioni dei database elastici e il routing dipendente dai dati con Dapper. 

**Codice di esempio**: [Strumenti dei database elastici per il database SQL di Azure - Integrazione con Dapper](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

L'integrazione di **Dapper** e **DapperExtensions** con la libreria client dei database elastici per il database SQL di Azure è semplice. Le applicazioni possono usare il routing dipendente dai dati modificando la creazione e l'apertura di nuovi oggetti [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) per usare la chiamata a [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) dalla [libreria client](http://msdn.microsoft.com/library/azure/dn765902.aspx). Questo limita le modifiche nell'applicazione solo ai punti in cui vengono create e aperte nuove connessioni. 

## <a name="dapper-overview"></a>Informazioni generali su Dapper
**Dapper** è un mapper object-relational. Esegue il mapping degli oggetti .NET dell'applicazione con un database relazionale e viceversa. La prima parte del codice di esempio illustra come integrare la libreria client dei database elastici con applicazioni basate su Dapper. La seconda parte del codice di esempio illustra come eseguire l’integrazione quando si usano Dapper e DapperExtensions.  

La funzionalità di mapper in Dapper fornisce metodi di estensione per le connessioni di database che semplificano l'invio di istruzioni T-SQL per l'esecuzione o per l'esecuzione di query del database. Ad esempio, Dapper consente di eseguire il mapping tra gli oggetti .NET e i parametri delle istruzioni SQL per le chiamate **Execute** o di usare i risultati delle query SQL negli oggetti .NET mediante chiamate **Query** da Dapper. 

Quando si usa DapperExtensions, non è più necessario fornire le istruzioni SQL. I metodi di estensione, ad esempio **GetList** o **Insert** per la connessione di database, creano le istruzioni SQL dietro le quinte.

Un altro vantaggio offerto da Dapper e anche da DapperExtensions è il controllo della creazione della connessione di database da parte dell'applicazione. Ciò consente di interagire con la libreria client dei database elastici che negozia le connessioni di database in base al mapping tra shardlet e database.

Per ottenere gli assembly Dapper, vedere la pagina relativa a [Dapper dot net](http://www.nuget.org/packages/Dapper/). Per le estensioni Dapper, vedere la pagina relativa a [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-the-elastic-database-client-library"></a>Panoramica della libreria client dei database elastici
Con libreria client dei database elastici è possibile definire partizioni di dati di applicazione denominate *shardlet*, eseguirne il mapping con i database e identificarli in base a *chiavi di partizionamento orizzontale*. È possibile disporre di tutti i database desiderati e distribuire gli shardlet su tali database. Il mapping dei valori delle chiavi di partizionamento orizzontale ai database è archiviato in una mappa partizioni fornita dalle API della libreria. Questa funzionalità è denominata **gestione mappe partizioni**. La mappa partizioni funge anche da gestore delle connessioni di database per le richieste che contengono una chiave di partizionamento orizzontale. Questa funzionalità è indicata come **routing dipendente dai dati**.

![Mappe di partizione e routing dipendente dai dati][1]

Il gestore mappe partizioni protegge gli utenti da visualizzazioni non coerenti in dati di shardlet che possono verificarsi quando vengono eseguite operazioni di gestione shardlet simultanee nei database. A tale scopo, le mappe partizioni gestiscono le connessioni al database per un'applicazione compilata con la libreria. Se esiste il rischio che le operazioni di gestione delle partizioni abbiano impatto sullo shardlet, in questo modo la funzionalità delle mappe di partizioni può terminare automaticamente una connessione al database. 

Anziché usare il sistema tradizionale per creare connessioni per Dapper, è necessario usare il [metodo OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn824099.aspx). Ciò garantisce che vengano eseguite tutte le convalide e vengano gestite correttamente le connessioni durante lo spostamento di dati tra le partizioni.

### <a name="requirements-for-dapper-integration"></a>Requisiti per l'integrazione con Dapper
Quando si usano sia la libreria client dei database elastici che le API di Dapper, si desidera mantenere le seguenti proprietà:

* **Scalabilità orizzontale**: si desidera aggiungere o rimuovere database dal livello dati dell'applicazione partizionata a seconda delle necessità per soddisfare le esigenze di capacità dell'applicazione. 
* **Coerenza**: poiché nell'applicazione viene implementata la scalabilità orizzontale con il partizionamento orizzontale, è necessario eseguire il routing dipendente dai dati. A tale scopo, è possibile usare le funzionalità di routing dipendente dai dati della libreria. In particolare, si desidera mantenere le garanzie di convalida e coerenza fornite dalle connessioni negoziate tramite il gestore mappe partizioni per evitare problemi di danneggiamento o di risultati di query non corretti. Ciò garantisce che le connessioni a un determinato shardlet vengano rifiutate o arrestate se ad esempio lo shardlet è attualmente spostato in una partizione diversa tramite API di suddivisione/unione.
* **Mapping degli oggetti**: si desidera mantenere i vantaggi dei mapping forniti da Dapper per la conversione tra le classi nell'applicazione e le strutture di database sottostanti. 

La seguente sezione fornisce indicazioni per tali requisiti per le applicazioni basate su **Dapper** e **DapperExtensions**.

## <a name="technical-guidance"></a>Indicazioni tecniche
### <a name="data-dependent-routing-with-dapper"></a>Routing dipendente dai dati con Dapper
Con Dapper l'applicazione è in genere responsabile della creazione e l'apertura delle connessioni al database sottostante. Sulla base di un tipo T fornito dall'applicazione, Dapper restituisce risultati di query come raccolte .NET di tipo T. Dapper esegue il mapping tra le righe di risultati di T-SQL e gli oggetti di tipo T. Analogamente, Dapper esegue il mapping tra oggetti .NET e parametri o valori SQL per istruzioni Data Manipulation Language (DML). Dapper offre questa funzionalità tramite i metodi di estensione nel normale oggetto [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) delle librerie client SQL ADO.NET. Anche la connessione SQL restituita dalle API di scalabilità elastica per record dei dati di individuazione sono normali oggetti [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx). In questo modo è possibile usare direttamente le estensioni Dapper sul tipo restituito dall'API di record dei dati della libreria client, perché anche in questo caso si tratta di una semplice connessione client SQL.

Queste osservazioni semplificano l'utilizzo delle connessioni negoziate dalla libreria client dei database elastici per Dapper.

Questo esempio di codice (dall'esempio di accompagnamento) illustra il metodo in cui la chiave di partizionamento viene fornita dall'applicazione alla libreria per negoziare la connessione al partizionamento corretto.   

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

La chiamata all'API [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) sostituisce la creazione predefinita e l'apertura di una connessione client SQL. La chiamata a [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) accetta gli argomenti necessari per il routing dipendente dai dati: 

* La mappa partizioni per l'accesso alle interfacce di routing dipendente dai dati
* La chiave di partizionamento orizzontale per l'identificazione dello shardlet
* Le credenziali (nome utente e password) per la connessione alla partizione

L'oggetto mappa partizioni crea una connessione alla partizione che contiene lo shardlet per la chiave di partizionamento orizzontale specificata. Le API della libreria client dei database elastici aggiungono inoltre un tag alla connessione per implementare le garanzie di coerenza. Poiché la chiamata a [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) restituisce un normale oggetto di connessione client SQL, la chiamata successiva al metodo di estensione **Execute** da Dapper segue la procedura Dapper standard.

Le query funzionano in modo molto simile: si apre innanzitutto la connessione usando [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) dall'API client. Si usano quindi i normali metodi di estensione Dapper per il mapping tra i risultati della query SQL negli oggetti .NET:

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

Si noti che il blocco **using** con la connessione di record di dati di individuazione definisce l'ambito di tutte le operazioni di database all'interno del blocco per la partizione in cui viene mantenuto tenantId1. La query restituisce solo blog archiviati nella partizione corrente, ma non quelli archiviati nelle altre partizioni. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Routing dipendente dai dati con Dapper e DapperExtensions
Dapper viene fornito con un ecosistema di estensioni aggiuntive che garantiscono praticità e astrazione dal database durante lo sviluppo di applicazioni di database. Un esempio è rappresentato da DapperExtensions. 

L'uso di DapperExtensions nell'applicazione non comporta la modifica della modalità di creazione e gestione delle connessioni di database. È comunque responsabilità dell'applicazione aprire le connessioni e sono previsti normali oggetti di connessione client SQL dai metodi di estensione. È possibile basarsi sul metodo [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) come illustrato in precedenza. Come mostrato nei seguenti esempi di codice, come unica differenza non è necessario scrivere le istruzioni T-SQL:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

Questo è l'esempio di codice per la query: 

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
Il team Microsoft Patterns & Practices ha pubblicato un articolo relativo al [blocco di applicazioni per la gestione degli errori temporanei](http://msdn.microsoft.com/library/hh680934.aspx) per consentire agli sviluppatori di applicazioni di attenuare le comuni condizioni di errori temporanei rilevate durante l'esecuzione nel cloud. Per ulteriori informazioni, vedere [Perseveranza, il segreto di tutti i successi: uso del Blocco di applicazioni per la gestione degli errori temporanei](http://msdn.microsoft.com/library/dn440719.aspx).

L'esempio di codice si basa sulla libreria di errori temporanei per proteggersi da questo tipo di errori. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** nel codice precedente viene definito come **SqlDatabaseTransientErrorDetectionStrategy** con un numero di tentativi pari a 10 e un tempo di attesa tra i tentativi pari a 5 secondi. Se si usano le transazioni, assicurarsi che l'ambito delle ripetizioni risalga all'inizio della transazione in caso di errore temporaneo.

## <a name="limitations"></a>Limitazioni
Gli approcci descritti in questo documento implicano due limitazioni:

* Il codice di esempio per questo documento non illustra come gestire lo schema tra partizioni.
* Data una richiesta, si presuppone che tutta la relativa elaborazione di database sia contenuta in una singola partizione identificata dalla chiave di partizionamento orizzontale fornita dalla richiesta. Tuttavia, questo presupposto non ha sempre valore, ad esempio quando non è possibile rendere disponibile una chiave di partizionamento orizzontale. Per risolvere questo problema, la libreria client dei database elastici include la [classe MultiShardQuery](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). Questa classe implementa un'astrazione di connessione per l'esecuzione di query su più partizioni. L'uso di MultiShardQuery in combinazione con Dapper esula dall'ambito di questo documento.

## <a name="conclusion"></a>Conclusioni
Le applicazioni che usano Dapper e DapperExtensions possono trarre vantaggio facilmente dagli strumenti dei database elastici del database SQL di Azure. Tramite le procedure descritte in questo documento, tali applicazioni possono usare la funzionalità dello strumento per il routing dipendente dai dati modificando la creazione e l'apertura di nuovi oggetti [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) per usare la chiamata a [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) della libreria client dei database elastici. In questo modo si limitano le modifiche dell'applicazione ai punti in cui vengono create e aperte nuove connessioni. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
