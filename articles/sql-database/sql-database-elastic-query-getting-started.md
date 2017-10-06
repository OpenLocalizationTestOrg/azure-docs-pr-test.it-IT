---
title: "aaaReport tra i database di cloud di scalabilità orizzontale (partizionamento orizzontale) | Documenti Microsoft"
description: come toouse tra le query di database di database
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Creare report in database cloud con numero maggiore di istanze (anteprima)
È possibile creare report da più database SQL di Azure da un unico punto di connessione usando una [query elastica](sql-database-elastic-query-overview.md). Hello database deve essere partizionata orizzontalmente (anche noto come "partizionati").

Se si dispone di un database esistente, vedere [esistente migrazione database database tooscaled-out](sql-database-elastic-convert-to-use-elastic-tools.md).

gli oggetti SQL hello toounderstand necessari tooquery, vedere [Query tra database partizionati orizzontalmente](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Prerequisiti
Scaricare ed eseguire hello [Guida introduttiva a esempio di strumenti di Database elastico](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Creare una mappa partizioni gestione tramite app di esempio hello
Di seguito si creerà una mappa partizioni manager insieme a diverse partizioni, seguita dall'inserimento di dati in partizioni hello. Se si è verificata tooalready con l'installazione di partizioni con dati partizionati, è possibile passare alla procedura seguente hello e spostare toohello nella sezione successiva.

1. Compilare ed eseguire hello **Introduzione agli strumenti di Database elastico** applicazione di esempio. Seguire i passaggi di hello fino al passaggio 7 nella sezione hello [scaricare ed eseguire app di esempio hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Al fine di hello del passaggio 7, verrà visualizzato un hello prompt dei comandi seguenti:

    ![Aprire il prompt dei comandi.][1]
2. Nella finestra di comando hello, digitare "1" e premere **invio**. Questo gestore mappe partizioni di hello crea e aggiunge due partizioni toohello server. Quindi digitare "3" e premere **invio**; ripetere azione hello quattro volte. Consente di inserire righe di dati di esempio nelle partizioni.
3. Hello [portale di Azure](https://portal.azure.com) devono essere visualizzati tre nuovi database nel server:

   ![Conferma di Visual Studio][2]

   Query tra database a questo punto, sono supportate tramite le librerie client di Database elastico hello. Nella finestra di comando hello, ad esempio, utilizzare l'opzione 4. Hello risultati da una query su più partizioni sono sempre un **UNION ALL** dei risultati di hello da tutte le partizioni.

   Nella sezione successiva hello, si crea un endpoint di database di esempio che supporta più l'esecuzione di query di dati hello tra partizioni.

## <a name="create-an-elastic-query-database"></a>Creare un database di query elastico
1. Aprire hello [portale di Azure](https://portal.azure.com) ed effettuare l'accesso.
2. Creare un nuovo database SQL di Azure in hello nello stesso server di configurazione del partizionamento. Nome database hello "ElasticDBQuery".

    ![Portale di Azure e il livello di prezzo][3]

    > [!NOTE]
    > È possibile usare un database esistente. Se è possibile farlo, non deve essere una delle partizioni hello che si desidera tooexecute nella query. Questo database verrà utilizzato per la creazione di oggetti di metadati per una query di database elastico hello.
    >

## <a name="create-database-objects"></a>Creare oggetti di database
### <a name="database-scoped-master-key-and-credentials"></a>Chiave master con ambito database e credenziali
Si tratta di gestore mappe partizioni di toohello tooconnect utilizzato e partizioni hello:

1. Apri SQL Server Management Studio e SQL Server Data Tools in Visual Studio
2. La connessione a database tooElasticDBQuery ed eseguire hello comandi T-SQL seguente:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "nomeutente" e "password" deve essere hello stesso come informazioni di accesso utilizzate nel passaggio 6 di [scaricare ed eseguire app di esempio hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) in [Introduzione agli strumenti di database elastico](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>DROP EXTERNAL DATA SOURCE
toocreate un'origine dati esterna, eseguire comando seguente sul database ElasticDBQuery hello hello:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 "CustomerIDShardMap" è il nome di hello della mappa partizioni hello, se è stato creato mappa partizioni hello e mappa partizioni manager utilizzando l'esempio di strumenti di database elastico hello. Tuttavia, se si utilizza il programma di installazione personalizzato per questo esempio, deve essere nome mappa partizioni di hello che scelto nell'applicazione.

### <a name="external-tables"></a>Tabelle esterne
Creare una tabella esterna corrispondente tabella Customers hello su partizioni hello eseguendo hello comando seguente sul database ElasticDBQuery:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Eseguire una query di esempio elastica database T-SQL
Dopo aver definito l'origine dati esterna e le tabelle esterne è ora possibile utilizzare T-SQL completa tramite le tabelle esterne.

Eseguire la query sul database ElasticDBQuery hello:

    select count(CustomerId) from [dbo].[Customers]

Si noterà che eseguono query hello aggrega i risultati di tutte le partizioni hello e offre hello seguente output:

![Dettagli dell'output][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Importare tooExcel risultati query di database elastico
 È possibile importare i risultati di hello da di un file di Excel tooan query.

1. Avviare Excel 2013.
2. Passare toohello **dati** della barra multifunzione.
3. Fare clic su **Da altre origini** e quindi su **Da SQL Server**.

   ![Importazione di Excel da altre origini][5]
4. In hello **connessione guidata dati** digitare le credenziali di nome e l'account di accesso server hello. Quindi fare clic su **Next**.
5. Nella finestra di dialogo hello **database selezionare hello che contiene dati hello da**selezionare hello **ElasticDBQuery** database.
6. Seleziona hello **clienti** tabella nella visualizzazione elenco hello e fare clic su **Avanti**. Fare clic su **Fine**.
7. In hello **l'importazione dei dati** del modulo **selezionare la modalità tooview questi dati nella cartella di lavoro**selezionare **tabella** e fare clic su **OK**.

Tutte le righe di hello **clienti** tabella, archiviata in partizioni diverse popolare un foglio di Excel hello.

È ora possibile utilizzare funzioni di visualizzazione avanzata dei dati di Excel. È possibile utilizzare la stringa di connessione hello con il nome del server, nome del database e credenziali tooconnect BI e dati integrazione strumenti toohello elastico query database. Assicurarsi che SQL Server sia supportato come origine dati per lo strumento. È possibile fare riferimento a database elastico query toohello e le tabelle esterne come qualsiasi altro database di SQL Server e le tabelle di SQL Server si connetterà toowith lo strumento.

### <a name="cost"></a>Costi
Non è senza costi aggiuntivi per l'utilizzo di funzionalità di Query di Database elastico hello.

Per informazioni sui prezzi, vedere [Dettagli prezzi del database SQL](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Passaggi successivi

* Per un approfondimento, vedere [Panoramica delle query elastiche](sql-database-elastic-query-overview.md).
* Per un'esercitazione sul partizionamento verticale, vedere [Introduzione alle query tra database (partizionamento verticale)](sql-database-elastic-query-getting-started-vertical.md).
* Per le query di esempio e sintassi per i dati con partizionamento verticale, vedere [Eseguire query su dati con partizionamento verticale](sql-database-elastic-query-vertical-partitioning.md)
* Per le query di esempio e sintassi per i dati con partizionamento orizzontale, vedere [Eseguire query su dati con partizionamento orizzontale](sql-database-elastic-query-horizontal-partitioning.md)
* Vedere [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) per una stored procedure che esegue un'istruzione Transact-SQL su un singolo database SQL di Azure remoto o un set di database che fungono da partizioni in uno schema di partizionamento orizzontale.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
