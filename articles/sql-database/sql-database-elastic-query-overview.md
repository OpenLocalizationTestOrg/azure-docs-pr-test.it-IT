---
title: Panoramica di query elastica di Database SQL aaaAzure | Documenti Microsoft
description: "Panoramica della funzionalità di query elastico hello"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: a8bf0e2c-bc74-44d0-9b1e-bcc9a6aa2e33
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: mlandzic
ms.openlocfilehash: db17f551882cfcae0da67fdda12708baeb6db81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-elastic-query-overview-preview"></a>Panoramica delle query elastiche del database SQL di Azure (anteprima)
funzionalità di query elastico Hello (in anteprima) permette di toorun una query Transact-SQL che si estende su più database nel Database di SQL Azure. Consente tabelle remote di tooperform query tra database tooaccess e tooquery di strumenti (Excel, Power BI, Tableau, e così via) di Microsoft e di terze parti tooconnect tra i livelli di dati con più database. Usare questa funzionalità, è possibile scalare orizzontalmente i livelli dati toolarge query nel Database SQL e visualizzare i risultati di hello in report di business intelligence (BI).


## <a name="why-use-elastic-queries"></a>Vantaggi dell'uso di query elastiche

**Database SQL di Azure**

Eseguire query su database SQL di Azure completamente in T-SQL. Ciò consente l'esecuzione di query di sola lettura sui database remoti Ciò fornisce un'opzione per locale corrente applicazioni toomigrate clienti di SQL Server utilizzando nomi di tre e quattro parti o il server collegato tooSQL DB.

**Disponibile nel livello Standard**

Query elastico è supportata nel livello di prestazioni Standard hello nel livello di prestazioni Premium toohello aggiunta. Vedere la sezione hello anteprima limitazioni indicate di seguito sui limiti delle prestazioni per i livelli di prestazioni inferiore.

**Push tooremote database**

Query elastica può ora eseguire il push database remoti toohello parametri SQL per l'esecuzione.

**Esecuzione di stored procedure**

Eseguire chiamate di stored procedure remote o funzioni remote mediante [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714).

**Flessibilità**

Le tabelle esterne con query elastico ora possono fare riferimento a tabelle tooremote con un nome di tabella o un altro schema.

## <a name="elastic-query-scenarios"></a>Scenari di query elastiche

obiettivo di Hello è toofacilitate scenari in cui più database contribuiscono righe in un singolo risultato complessivo di una query. query Hello possono essere composte sia da hello utente o applicazione direttamente o indirettamente tramite gli strumenti che sono connessi toohello database. Ciò è particolarmente utile quando si creano report, si usano strumenti commerciali di Business Intelligence o di integrazione dei dati o si usa qualsiasi applicazione che non può essere modificata. Con una query elastica, è possibile eseguire query su più database tramite consueta esperienza di connettività SQL Server hello in strumenti, ad esempio Excel, Power BI, Tableau o Cognos.
Una query elastica consente un facile accesso tooan tutto l'insieme di database tramite le query eseguite da SQL Server Management Studio o Visual Studio e facilita l'esecuzione di query tra database da Entity Framework o in altri ambienti di ORM. La figura 1 illustra uno scenario in cui un oggetto esistente del cloud di applicazione (che utilizza hello [libreria client di database elastico](sql-database-elastic-database-client-library.md)) compilazioni su dati di scalabilità orizzontale del livello e viene utilizzata una query flessibile per i report tra database.

**Figura 1** Query elastica usata su un livello di dati con scalabilità orizzontale

![Query elastica usata su un livello di dati con scalabilità orizzontale][1]

Scenari di clienti per query elastico sono caratterizzati da hello seguenti topologie:

* **Partizionamento verticale - query tra database** (topologia 1): hello i dati sono partizionati in senso verticale tra un numero di database in un livello di dati. In genere, diversi set di tabelle si trovano in diversi database. Ciò significa che lo schema hello è diverso in database diversi. Ad esempio, tutte le tabelle per l'inventario si trovano in un database, mentre le tabelle correlate alla contabilità si trovano in un altro database. Casi d'uso comuni con questa topologia richiedono uno tooquery tra o toocompile relazioni tra tabelle in più database.
* **Partizionamento orizzontale - partizionamento orizzontale** (topologia 2): dati vengono partizionati orizzontalmente toodistribute righe attraverso una scalabilità dati livello. Con questo approccio, schema hello è identico in tutti i database partecipanti. Questo approccio viene definito anche "partizionamento orizzontale". Partizionamento orizzontale può essere eseguita e gestite tramite le librerie strumenti di database elastico hello (1) o (2) partizionamento orizzontale automatico. Una query elastica è report tooquery o di compilazione utilizzati tra molte partizioni.

> [!NOTE]
> Query elastico è ideale per scenari di report occasionali in cui la maggior parte dell'elaborazione hello può essere eseguita nel livello dati hello. Per carichi di lavoro di creazione di report elevati o per scenari di data warehousing con query più complesse è possibile usare anche [Azure SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
>  

## <a name="vertical-partitioning---cross-database-queries"></a>Partizionamento verticale - Query tra database

toobegin nel codice, vedere [Guida introduttiva a query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).

Una query elastica può essere utilizzato toomake dati si trova in un database SQL tooother disponibili database SQL. In questo modo le query da un database toorefer tootables in qualsiasi altro database SQL remoto. primo passaggio Hello è toodefine un'origine dati esterna per ogni database remoto. origine dati esterna Hello è definita nel database locale di hello da cui si desidera toogain accesso tootables sul database remoto hello. Non sono necessarie modifiche nel database remoto hello. Per verticali partizionamento scenari tipici in database diversi contengono schemi diversi, elastica query possono essere tooimplement utilizzati casi d'uso comuni, ad esempio tooreference accedere ai dati e l'esecuzione di query tra database.

> [!IMPORTANT]
> L'utente deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE. Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello. Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.
>

**Dati di riferimento**: topologia hello viene utilizzata per la gestione dei dati di riferimento. Nella seguente figura hello due tabelle (T1 e T2) con dati di riferimento vengono mantenute in un database dedicato. Utilizzando una query elastica, è ora possibile accedere tabelle T1 e T2 in modalità remota da altri database, come illustrato nella figura hello. Usare la topologia 1 se le tabelle di riferimento hanno dimensioni ridotte o se le query nella tabella di riferimento hanno predicati selettivi.

**Figura 2** verticale partizionamento - utilizzando dati di riferimento tooquery query elastico

![Verticale partizionamento - utilizzando dati di riferimento tooquery query elastico][3]

**Query tra database**: le query elastiche consentono casi di utilizzo che richiedono l'esecuzione di query in diversi database SQL. La Figura 3 mostra quattro database diversi, ovvero CRM, Inventario, Risorse umane e Prodotti. Le query eseguite in uno dei database hello anche necessitano accedere tooone o tutti hello altri database. Utilizzando una query elastica, è possibile configurare il database in questo caso eseguendo alcuni semplici istruzioni DDL in ognuno dei quattro database hello. Dopo questa configurazione occasionale, è sufficiente che fa riferimento a tabella locale tooa dalla query T-SQL o dagli strumenti BI tabella remota tooa di accesso. Questo approccio è consigliato se le query remote hello non restituiscono risultati di grandi dimensioni.

**Figura 3** verticale partizionamento - utilizzo tooquery elastico query tra database diversi

![Verticale partizionamento - utilizzo tooquery elastico query tra database diversi][4]

Hello seguenti passaggi consentono di configurare le query di database elastici per scenari di partizionamento verticale che richiedono tabella tooa accesso si trova nel database SQL remoti con hello stesso schema:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource of type **RDBMS**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Dopo l'esecuzione di istruzioni DDL hello, è possibile accedere tabella remota hello "mytable" come se fosse una tabella locale. Database SQL di Azure apre automaticamente un database remoto toohello di connessione, elabora la richiesta nel database remoto hello e restituisce risultati hello.

## <a name="horizontal-partitioning---sharding"></a>Partizionamento orizzontale - Partizionamento orizzontale
L'utilizzo di query elastico tooperform le attività di reporting su un partizionato, ad esempio, in senso orizzontale partizionata, livello dati richiede un [mappa partizioni di database elastico](sql-database-elastic-scale-shard-map-management.md) database hello toorepresent del livello dati hello. In genere, in questo scenario viene utilizzata solo una mappa di singola partizione e un database dedicato con funzionalità di query elastico (nodo head) funge da punto di ingresso hello per le query di report. Solo tale database dedicato deve mappa partizioni toohello di accesso. Figura 4 illustra questa topologia e la relativa configurazione con mappa di database e partizioni query elastico hello. i database nel livello dati hello Hello possono essere di qualsiasi Database SQL di Azure versione o edizione. Per ulteriori informazioni sulla libreria client di database elastico hello e la creazione di mappe partizioni, vedere [gestione mappa partizioni](sql-database-elastic-scale-shard-map-management.md).

**Figura 4** Partizionamento orizzontale - Uso delle query elastiche per la creazione di report relativi ai livelli dati con partizionamento orizzontale

![Partizionamento orizzontale - Uso delle query elastiche per la creazione di report relativi ai livelli dati con partizionamento orizzontale][5]

> [!NOTE]
> Database Query elastico (nodo head) può essere un database separato o può essere hello stesso database che mappa partizioni hello di host. Indipendentemente dalla modalità di configurazione, assicurarsi che tale livello di servizio e le prestazioni del database è l'importo previsto hello toohandle sufficientemente elevato di richieste di accesso/query.

Hello passaggi seguenti configurare query di database elastico per orizzontale partizionamento gli scenari che richiedono accesso tooa set della tabella che si trovano su (in genere in) database SQL remoti diversi:

* [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx) mymasterkey
* [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx) mycredential
* Creare un [mappa partizioni](sql-database-elastic-scale-shard-map-management.md) che rappresenta il livello dati utilizzando una libreria client di database elastico hello.   
* [CREATE/DROP EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx) mydatasource di tipo **SHARD_MAP_MANAGER**
* [CREATE/DROP EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) mytable

Dopo aver eseguito questi passaggi, è possibile accedere tabella partizionata orizzontalmente hello "mytable" come se fosse una tabella locale. Database SQL di Azure automaticamente apre più connessioni parallelo toohello database remoti in cui sono archiviate fisicamente tabelle hello elabora le richieste di hello su database remoti hello e restituisce risultati hello.
Ulteriori informazioni sui passaggi di hello necessario per uno scenario di partizionamento orizzontale hello è reperibile [elastica query per il partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md).

toobegin nel codice, vedere [introduzione elastica query per il partizionamento orizzontale (partizionamento orizzontale)](sql-database-elastic-query-getting-started.md).

## <a name="t-sql-querying"></a>Query T-SQL
Dopo aver definito le origini dati esterne e le tabelle esterne, è possibile utilizzare regolare connessione stringhe tooconnect toohello i database SQL Server in cui è definito le tabelle esterne. È possibile eseguire le istruzioni T-SQL su tabelle esterne su tale connessione con limitazioni hello descritte di seguito. È possibile trovare ulteriori informazioni ed esempi di query T-SQL negli argomenti di documentazione hello per [il partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md) e [partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md).

## <a name="connectivity-for-tools"></a>Connettività per gli strumenti
Le applicazioni e BI o dati toodatabases strumenti di integrazione con le tabelle esterne, è possibile utilizzare regolare tooconnect di stringhe di connessione SQL Server. Assicurarsi che SQL Server sia supportato come origine dati per lo strumento. Una volta connessi, fare riferimento toohello query elastico del database e hello tabelle esterne nel database esattamente come si farebbe con qualsiasi altro database di SQL Server che si connette toowith lo strumento.

> [!IMPORTANT]
> L'autenticazione tramite Azure Active Directory con query elastiche non è attualmente supportata.
> 
> 

## <a name="cost"></a>Costi
Query elastico è inclusa nel costo hello dei database di Database SQL di Azure. Si noti che sono supportate le topologie in cui sono i database remoti in un data center diverso rispetto a hello endpoint elastico query, ma i dati in uscita dai database remoti vengono addebitate regular [tariffe Azure](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="preview-limitations"></a>Limiti di anteprima
* Esecuzione della prima query elastica può richiedere fino a tooa alcuni minuti a livello di prestazioni Standard hello. Questa volta è una funzionalità di query elastico hello tooload necessarie; prestazioni di caricamento migliorano con i livelli di prestazioni superiore.
* La creazione di script di origini dati esterne o tabelle esterne da SSMS o SSDT non è ancora supportata.
* L'importazione/esportazione per il database SQL non supporta ancora origini dati esterne e tabelle esterne. Se è necessario toouse importazione/esportazione, eliminare questi oggetti prima di esportare e quindi ricrearli dopo l'importazione.
* Query elastico supporta attualmente solo le tabelle tooexternal accesso in sola lettura. Tuttavia, è possibile utilizzare le funzionalità complete di T-SQL nel database di hello in cui la tabella esterna hello è definita. Questo può essere utile mantenere, ad esempio, risultati temporanei utilizzando, ad esempio, selezionare < column_list > in < local_table >, o toodefine stored procedure nel database di hello elastico query che fanno riferimento a tabelle tooexternal.
* Ad eccezione di nvarchar(max), i tipi LOB non sono supportati nelle definizioni di tabelle esterne. In alternativa, è possibile creare una vista nel database remoto hello che esegue il cast di tipo LOB hello in nvarchar (max), definire la tabella esterna sulla visualizzazione di hello anziché una tabella di base hello e quindi eseguirne il cast al tipo LOB originale hello nelle query.
* Le statistiche di colonna sulle tabelle esterne non sono attualmente supportate. Statistiche delle tabelle sono supportati, ma è necessario toobe creato manualmente.

## <a name="feedback"></a>Commenti e suggerimenti
. Condividere commenti e suggerimenti sull'esperienza con le query elastiche con noi Disqus riportato di seguito, i forum MSDN hello, o su Stackoverflow. Siamo interessati tutti i tipi di commenti e suggerimenti sul servizio hello (difetti, bordi approssimativo, il gap di funzionalità).

## <a name="next-steps"></a>Passaggi successivi

* Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).
* Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)
* Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).
* Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)
* Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.

<!--Image references-->
[1]: ./media/sql-database-elastic-query-overview/overview.png
[2]: ./media/sql-database-elastic-query-overview/topology1.png
[3]: ./media/sql-database-elastic-query-overview/vertpartrrefdata.png
[4]: ./media/sql-database-elastic-query-overview/verticalpartitioning.png
[5]: ./media/sql-database-elastic-query-overview/horizontalpartitioning.png

<!--anchors-->
