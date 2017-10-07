---
title: i database con schema diverso aaaQuery tra cloud | Documenti Microsoft
description: come tooset le query tra database in partizioni verticali
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Eseguire query in database cloud con schemi diversi (anteprima)
![Eseguire una query tra tabelle in vari database][1]

I database con partizionamento verticale usano set di tabelle diversi su database diversi. Ciò significa che lo schema hello è diverso in database diversi. Ad esempio, tutte le tabelle per l'inventario si trovano in un database, mentre le tabelle correlate alla contabilità si trovano in un altro database. 

## <a name="prerequisites"></a>Prerequisiti
* utente Hello deve disporre dell'autorizzazione ALTER ANY EXTERNAL DATA SOURCE. Questa autorizzazione è inclusa con l'autorizzazione ALTER DATABASE hello.
* Le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE sono necessari toorefer toohello origine dati sottostante.

## <a name="overview"></a>Panoramica

> [!NOTE]
> A differenza con partizionamento orizzontale, queste istruzioni DDL non basarsi sulla definizione di un livello dati con una mappa partizioni tramite libreria client di database elastico hello.
>

1. [CREATE MASTER KEY](https://msdn.microsoft.com/library/ms174382.aspx)
2. [CREATE DATABASE SCOPED CREDENTIAL](https://msdn.microsoft.com/library/mt270260.aspx)
3. [CREATE EXTERNAL DATA SOURCE](https://msdn.microsoft.com/library/dn935022.aspx)
4. [CREATE EXTERNAL TABLE](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Creare la chiave master e le credenziali con ambito database
Hello credenziali vengono utilizzate dal database remoti tooyour tooconnect query elastico hello.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Verificare che hello `<username>` non include alcun **"@servername"** suffisso. 
>

## <a name="create-external-data-sources"></a>Creare origini dati esterne
Sintassi:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> è necessario impostare il parametro di tipo Hello troppo**RDBMS**. 
>

### <a name="example"></a>Esempio
Hello seguente viene illustrato hello utilizzo dell'istruzione CREATE hello per le origini dati esterne. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

elenco di hello tooretrieve delle origini dati esterne corrente: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Tabelle esterne
Sintassi:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Esempio
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

Hello di esempio seguente viene illustrato come tooretrieve hello elenco di tabelle esterne dal database corrente hello: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Osservazioni
Query elastico estende hello tabella esterna sintassi toodefine esterno tabelle esistenti che utilizzano origini dati esterne di tipo RDBMS. Una definizione di tabella esterna per il partizionamento verticale copre hello seguenti aspetti: 

* **Schema**: tabella esterna hello DDL definisce uno schema che è possono utilizzare le query. schema di Hello fornito nella definizione della tabella esterna deve schema hello toomatch delle tabelle di hello nel database remoto di hello dove vengono archiviati dati effettivi hello. 
* **Riferimento al database remoto**: tabella esterna hello DDL fa riferimento l'origine dati esterna tooan. origine dati esterna Hello Specifica nome del server logico hello e nome del database remoto di hello dove vengono archiviati i dati di tabella effettiva hello. 

Le tabelle esterne hello sintassi toocreate utilizzando un'origine dati esterna, come descritto nella sezione precedente di hello, è come segue: 

clausola DATA_SOURCE Hello definisce l'origine dati esterna hello (ad esempio hello database remoto in caso di partizionamento verticale) che viene utilizzato per la tabella esterna hello.  

le clausole nome_schema e nome_oggetto Hello forniscono hello possibilità toomap hello tabella esterna tooa tabella per la definizione in un altro schema nel database remoto hello o tooa tabella con un nome diverso, rispettivamente. Ciò è utile se si desidera toodefine una vista del catalogo tooa tabella esterna o DMV del database remoto, o qualsiasi altra situazione in cui il nome di tabella remota hello è già in uso in locale.  

Hello istruzione DDL seguente elimina una definizione di tabella esterna esistente dal catalogo locale hello. Non influisce sulla database remoto hello. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**Le autorizzazioni per CREATE/DROP TABLE esterno**: sono necessarie le autorizzazioni ALTER ANY EXTERNAL DATA SOURCE per la tabella esterna DDL che è anche necessario toorefer toohello origine dei dati sottostante.  

## <a name="security-considerations"></a>Considerazioni relative alla sicurezza
Gli utenti con una tabella esterna toohello di accesso accedere automaticamente toohello tabelle remote sottostanti in credenziali hello specificata nella definizione dell'origine dati esterna hello. È consigliabile gestire attentamente tabella esterna di accesso toohello elevazione tooavoid indesiderati di ordine dei privilegi tramite credenziali hello dell'origine dati esterna hello. Regolare autorizzazioni SQL possono essere utilizzato tooGRANT o tabella esterna tooan di revocare l'accesso come se fosse una normale tabella.  

## <a name="example-querying-vertically-partitioned-databases"></a>Esempio: esecuzione di query su database partizionati verticalmente
Hello nella query seguente esegue un join a tre vie tra due tabelle locali hello per le righe dell'ordine e ordini e la tabella remota hello per i clienti. Questo è un esempio di hello caso d'uso di dati di riferimento per query elastico: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Stored procedure per l'esecuzione remota di T-SQL: sp\_execute_remote
Query elastico introduce inoltre una stored procedure che fornisce accesso diretto toohello partizioni. Hello stored procedure viene chiamata [sp\_eseguire \_remoto](https://msdn.microsoft.com/library/mt703714) e può essere utilizzato tooexecute stored procedure remote o il codice T-SQL nel database remoto hello. Avrà hello seguenti parametri: 

* Nome dell'origine dati (nvarchar): nome hello dell'origine dati esterna hello di tipo RDBMS. 
* Query (nvarchar): toobe query hello T-SQL eseguito su ogni partizione. 
* Dichiarazione di parametro (nvarchar) - facoltativa: stringa con definizioni dei tipi di dati per i parametri di hello utilizzati nel parametro di Query hello (ad esempio sp_executesql). 
* Elenco di valori dei parametri (facoltativo): elenco delimitato da virgole di valori dei parametri, ad esempio sp_executesql.

sp Hello\_eseguire\_remoto utilizza hello origine dati esterna cui hello chiamata parametri tooexecute hello dato istruzione T-SQL nel database remoto hello. Usa credenziali hello del database di gestione di hello dati esterni origine tooconnect toohello shardmap e database remoti hello.  

Esempio: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>Connettività per gli strumenti
È possibile utilizzare l'integrazione strumenti toodatabases di BI e i dati regolari tooconnect di stringhe di connessione SQL Server nel server di database di SQL Server hello con query elastico abilitato e le tabelle esterne definite. Assicurarsi che SQL Server sia supportato come origine dati per lo strumento. Fare riferimento a database elastico query toohello e le relative tabelle esterne come qualsiasi altro database di SQL Server si connetterà toowith dallo strumento. 

## <a name="best-practices"></a>Procedure consigliate
* Assicurarsi di che database elastico query endpoint hello ha database remoto di accesso toohello abilitando l'accesso per i servizi di Azure la configurazione di firewall di database di SQL Server. Assicurarsi inoltre che credenziali hello fornita in dati esterni hello definizione di origine può accedere senza problemi nel database remoto hello e ha una tabella remota hello tooaccess autorizzazioni hello.  
* Query elastico è ideale per le query in cui la maggior parte del calcolo hello possono essere eseguita nel database remoto hello. In genere, si ottiene hello migliori prestazioni di query con predicati di filtro selettivo che possono essere valutati sul database remoto hello o join che possono essere eseguite completamente nel database remoto hello. Altri modelli di query potrebbe essere necessario grandi quantità di tooload dei dati dal database remoto hello e potrebbero essere scarse. 

## <a name="next-steps"></a>Passaggi successivi

* Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).
* Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).
* Per un'esercitazione sul partizionamento orizzontale, vedere la [guida introduttiva alle query elastiche per il partizionamento orizzontale](sql-database-elastic-query-getting-started.md).
* Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)
* Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
