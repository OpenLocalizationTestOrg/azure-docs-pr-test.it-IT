---
title: aaaSQL Server database migrazione tooAzure Database SQL | Documenti Microsoft
description: "Informazioni per quanto riguarda il migrazione di database SQL Server tooAzure Database SQL nel cloud hello. Usare la migrazione di database migrazione strumenti tootest compatibilità toodatabase precedente."
keywords: migrazione di database, migrazione di database sql server, strumenti di migrazione del database, eseguire la migrazione di database, eseguire la migrazione di database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 9cf09000-87fc-4589-8543-a89175151bc2
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sqldb-migrate
ms.date: 02/08/2017
ms.author: carlrab
ms.openlocfilehash: 3a5e879404dd2da1dd5254a6134e3ee1517648db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-database-migration-toosql-database-in-hello-cloud"></a>TooSQL di migrazione di database SQL Server Database nel cloud hello
In questo articolo, conoscere hello due metodi principali per la migrazione di un SQL Server 2005 o successiva database tooAzure Database SQL. Hello primo metodo è più semplice, ma richiede una certa, possibilmente notevole, tempo di inattività durante la migrazione di hello. Hello secondo metodo è più complessa, ma elimina notevolmente i tempi di inattività durante la migrazione di hello.

In entrambi i casi, è necessario tooensure il database di origine hello è compatibile con i Database di SQL Azure mediante hello [dati Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595). Database SQL V12 si avvicina [nelle funzionalità](sql-database-features.md) con SQL Server, diverso da operazioni a livello di tooserver e tra database correlate problemi. Database e applicazioni che si basano su [parzialmente supportate o funzioni](sql-database-transact-sql-information.md) necessita di alcuni [riprogettazione toofix incompatibilità](sql-database-cloud-migrate.md#resolving-database-migration-compatibility-issues) prima hello SQL Server è possibile eseguire la migrazione di database.

> [!NOTE]
> toomigrate un database non SQL Server, tra cui Microsoft Access, Sybase, MySQL Oracle e DB2 tooAzure Database SQL, vedere [SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2016/12/22/released-sql-server-migration-assistant-ssma-v7-2/).
> 

## <a name="method-1-migration-with-downtime-during-hello-migration"></a>Metodo 1: Migrazione con tempi di inattività durante la migrazione di hello

 Usare questo metodo se si è disposti a tollerare tempi di inattività o se si esegue una migrazione di prova di un database di produzione per una migrazione successiva. Per un'esercitazione, vedere [Eseguire la migrazione di un database SQL Server](sql-database-migrate-your-sql-server-database.md).

Hello elenco seguente contiene hello generale del flusso di lavoro per la migrazione di un database di SQL Server utilizzando questo metodo.

  ![Diagramma di migrazione di VSSSDT](./media/sql-database-cloud-migrate/azure-sql-migration-sql-db.png)

1. Valutare database hello per garantire la compatibilità con hello versione più recente di [dati Migration Assistant (DMA)](https://www.microsoft.com/download/details.aspx?id=53595).
2. Preparare eventuali correzioni necessarie come script Transact-SQL.
3. Creare una copia del database di origine hello consistente migrato - e verificare le modifiche successive non diventano i database di origine toohello (o è possibile applicare manualmente tali modifiche dopo aver completato la migrazione hello). Sono disponibili molti metodi tooquiesce un database, la disabilitazione di toocreating di connettività client da un [snapshot del database](https://msdn.microsoft.com/library/ms175876.aspx).
4. Distribuire una copia di database di hello Transact-SQL script tooapply hello correzioni toohello.
5. [Esportare](sql-database-export.md) hello tooa copia di database. File BACPAC in un'unità locale.
6. [Importazione](sql-database-import.md) hello. Il file BACPAC come nuovo database SQL di Azure utilizzando uno dei diversi BACPAC importare strumenti, tramite SQLPackage.exe da hello consigliato strumento per ottimizzare le prestazioni.

### <a name="optimizing-data-transfer-performance-during-migration"></a>Ottimizzazione delle prestazioni di trasferimento dei dati durante la migrazione 

Hello seguente elenco contiene le indicazioni per ottimizzare le prestazioni durante il processo di importazione hello.

* Scegliere hello massimo livello di servizio e le prestazioni del livello che il budget consente prestazioni di trasferimento toomaximize hello. È possibile scalare verso il basso, dopo il completamento di migrazione hello toosave money. 
* Ridurre al minimo la distanza hello tra il. BACPAC file e hello destinazione centro dati.
* Disabilitare le statistiche automatiche durante la migrazione.
* Partizionare tabelle e indici.
* Eliminare le viste indicizzate e ricrearle al termine della migrazione.
* Rimuovere i dati cronologici raramente richiesto tooanother database ed eseguire la migrazione di questo database di SQL Azure separato tooa dati cronologici. Sarà quindi possibile eseguire query sui dati cronologici usando [query elastiche](sql-database-elastic-query-overview.md).

### <a name="optimize-performance-after-hello-migration-completes"></a>Ottimizzare le prestazioni, dopo aver completato la migrazione hello

[Aggiornare le statistiche](https://msdn.microsoft.com/library/ms187348.aspx) con l'analisi completa dopo aver completata la migrazione di hello.

## <a name="method-2-use-transactional-replication"></a>Metodo 2: Usare la replica transazionale

Quando ci si può permettere tooremove il database di SQL Server di produzione mentre è in corso la migrazione di hello, è possibile utilizzare la replica transazionale di SQL Server come soluzione di migrazione. toouse questo metodo, il database di origine hello deve soddisfa hello [requisiti per la replica transazionale](https://msdn.microsoft.com/library/mt589530.aspx) e compatibili per il Database SQL di Azure. Per informazioni sulla replica di SQL con AlwaysOn, vedere [Configurare la replica per i gruppi di disponibilità AlwaysOn (SQL Server)](/sql/database-engine/availability-groups/windows/configure-replication-for-always-on-availability-groups-sql-server).

toouse questa soluzione, di configurare il Database di SQL Azure come un'istanza di SQL Server toohello sottoscrittore che si desidera toomigrate. Hello Server di distribuzione di replica transazionale consente di sincronizzare dati da toobe database hello sincronizzati (server di pubblicazione hello) mentre le nuove transazioni continuano a verificarsi. 

Con la replica transazionale, tutte le modifiche tooyour dati o schema visualizzati nel Database SQL di Azure. Una volta hello sincronizzazione è stata completata e si è pronti toomigrate, modificare la stringa di connessione hello di toopoint le applicazioni li tooyour Database SQL di Azure. Dopo la replica transazionale Svuota tutte le modifiche a sinistra nel database di origine e di tutte le applicazioni scegliere tooAzure DB, è possibile disinstallare la replica transazionale. Il database SQL di Azure è ora il sistema di produzione.

 ![Diagramma di SeedCloudTR](./media/sql-database-cloud-migrate/SeedCloudTR.png)

> [!TIP]
> È possibile utilizzare anche la replica transazionale toomigrate un sottoinsieme del database di origine. pubblicazione di Hello replicare tooAzure Database SQL può essere limitato tooa subset di tabelle di hello nel database di hello in corso la replica. Per ogni tabella in corso la replica, è possibile limitare hello dati tooa sottoinsieme righe hello e/o un subset di colonne hello.
>

### <a name="migration-toosql-database-using-transaction-replication-workflow"></a>Migrazione tooSQL tramite flusso di lavoro di replica della transazione di Database

> [!IMPORTANT]
> Utilizzare hello più recente di SQL Server Management Studio tooremain sincronizzati con aggiornamenti tooMicrosoft Azure e il Database SQL. Le versioni precedenti di SQL Server Management Studio non sono in grado di impostare il database SQL come sottoscrittore. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 

1. Configurare la distribuzione
   -  [Usando SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_1)
   -  [Usando Transact-SQL](https://msdn.microsoft.com/library/ms151192.aspx#Anchor_2)
2. Creare la pubblicazione
   -  [Usando SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_1)
   -  [Usando Transact-SQL](https://msdn.microsoft.com/library/ms151160.aspx#Anchor_2)
3. Creare la sottoscrizione
   -  [Usando SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_0)
   -  [Usando Transact-SQL](https://msdn.microsoft.com/library/ms152566.aspx#Anchor_1)

### <a name="some-tips-and-differences-for-migrating-toosql-database"></a>Alcuni suggerimenti e le differenze per la migrazione di Database tooSQL

1. Usare un server di distribuzione locale. 
   - In questo modo un impatto sulle prestazioni nel server di hello. 
   - Se l'impatto sulle prestazioni di hello è accettabile, è possibile utilizzare un altro server, ma aumenta la complessità della gestione e amministrazione.
2. Quando la selezione di una cartella snapshot, la cartella hello assicurarsi di verificare che si seleziona è sufficientemente grande toohold una BCP di ogni tabella è opportuno tooreplicate. 
3. Blocchi di creazione di snapshot hello tabelle associate fino al completamento, pertanto, pianificare lo snapshot in modo appropriato. 
4. Nel database SQL di Azure sono supportate solo le sottoscrizioni push. È possibile aggiungere solo i sottoscrittori dal database di origine hello.

## <a name="resolving-database-migration-compatibility-issues"></a>Risoluzione dei problemi di compatibilità della migrazione di database
Sono disponibili un'ampia gamma di problemi di compatibilità che possono verificarsi, sia nella versione di hello di SQL Server che a seconda hello origine database e hello la complessità del database hello che si esegue la migrazione. Le versioni precedenti di SQL Server presentano più problemi di compatibilità. Utilizzare hello seguenti risorse, inoltre tooa destinazione ricerca Internet utilizzando il motore di ricerca di opzioni:

* [Funzionalità del database di SQL Server non supportate nel database SQL di Microsoft Azure](sql-database-transact-sql-information.md)
* [Funzionalità del motore di database sospese in SQL Server 2016](https://msdn.microsoft.com/library/ms144262%28v=sql.130%29)
* [Funzionalità del motore di database sospese in SQL Server 2014](https://msdn.microsoft.com/library/ms144262%28v=sql.120%29)
* [Funzionalità del motore di database sospese in SQL Server 2012](https://msdn.microsoft.com/library/ms144262%28v=sql.110%29)
* [Funzionalità del motore di database sospese in SQL Server 2008 R2](https://msdn.microsoft.com/library/ms144262%28v=sql.105%29)
* [Funzionalità del motore di database sospese in SQL Server 2005](https://msdn.microsoft.com/library/ms144262%28v=sql.90%29)

Inoltre toosearching hello Internet e l'utilizzo di queste risorse, utilizzare hello [forum della community MSDN di SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/home?category=sqlserver) o [StackOverflow](http://stackoverflow.com/).

## <a name="next-steps"></a>Passaggi successivi
* Utilizzare script hello sul blog di Azure SQL EMEA tecnici hello troppo[monitorare l'utilizzo di tempdb durante la migrazione](https://blogs.msdn.microsoft.com/azuresqlemea/2016/12/28/lesson-learned-10-monitoring-tempdb-usage/).
* Utilizzare script hello sul blog di Azure SQL EMEA tecnici hello troppo[monitorare lo spazio di log delle transazioni di hello del database mentre è in corso la migrazione](https://blogs.msdn.microsoft.com/azuresqlemea/2016/10/31/lesson-learned-7-monitoring-the-transaction-log-space-of-my-database/0).
* Per un Team di consulenza clienti di SQL Server tramite file BACPAC, vedere i blog sulla migrazione [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).
* Per informazioni sull'utilizzo di ora UTC dopo la migrazione, vedere [fuso orario di modifica hello predefinito per il fuso orario locale](https://blogs.msdn.microsoft.com/azuresqlemea/2016/07/27/lesson-learned-4-modifying-the-default-time-zone-for-your-local-time-zone/).
* Per informazioni sulla modifica di lingua predefinita hello di un database dopo la migrazione, vedere [come toochange hello lingua predefinita del Database SQL di Azure](https://blogs.msdn.microsoft.com/azuresqlemea/2017/01/13/lesson-learned-16-how-to-change-the-default-language-of-azure-sql-database/).


