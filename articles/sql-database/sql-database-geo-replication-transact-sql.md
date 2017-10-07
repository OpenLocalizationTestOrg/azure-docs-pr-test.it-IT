---
title: replica geografica aaaConfigure per Database SQL di Azure con Transact-SQL | Documenti Microsoft
description: Configurare la replica geografica per il database SQL di Azure con Transact-SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d94d89a6-3234-46c5-8279-5eb8daad10ac
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: carlrab
ms.openlocfilehash: 295b6b12f257dfb15131d5ee28fbe65c6476352d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-with-transact-sql"></a>Configurare la replica geografica attiva per il database SQL di Azure con Transact-SQL

In questo articolo illustra come tooconfigure replica geografica attiva per un Database di SQL Azure con Transact-SQL.

failover tooinitiate utilizzando Transact-SQL, vedere [avviare un failover pianificato o per il Database di SQL Azure con Transact-SQL](sql-database-geo-replication-failover-transact-sql.md).

> [!NOTE]
> Quando si utilizza la replica geografica attiva (repliche secondarie leggibili) per il ripristino di emergenza è necessario configurare un gruppo di failover per tutti i database all'interno di un failover automatico e trasparente tooenable dell'applicazione. Questa funzionalità è in anteprima. Per altre informazioni vedere [Panoramica: Replica geografica attiva per il database SQL di Azure](sql-database-geo-replication-overview.md).
> 
> 

replica geografica tooconfigure attiva tramite Transact-SQL, è necessario seguente hello:

* Una sottoscrizione di Azure.
* Un server logico di Database SQL di Azure <MyLocalServer> e un database SQL <MyDB> -database primario di hello che si desidera tooreplicate
* Uno o più Database SQL di Azure server logici < MySecondaryServer(n) > - hello server logici che fungerà da server partner hello in cui si creerà un database secondario
* Un account di accesso DBManager su hello primario
* Avere db_ownership del database locale di hello che sia necessario abilitare la replica geografica
* Essere DBManager in toowhich server partner di hello verrà configurata la replica geografica
* versione più recente Hello di SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
> 
> 

## <a name="add-secondary-database"></a>Aggiungere un database secondario
È possibile utilizzare hello **ALTER DATABASE** istruzione toocreate un database secondario in un server partner di replica geografica. Eseguire questa istruzione nel database master hello hello server contiene hello database toobe replicati. Hello database di replica geografica (Buongiorno "database primario") sarà necessario hello stesso nome di database hello in corso la replica e che, per impostazione predefinita, dispone di hello stesso livello di servizio come database primario hello. Hello database secondario può essere leggibile o non leggibile e può essere un singolo database o in un pool elastico. Per altre informazioni, vedere [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Livelli di servizio](sql-database-service-tiers.md).
Dopo aver creato e sottoposto a seeding, database secondario hello dati verranno avviata la replica in modo asincrono dal database primario hello. Hello riportato di seguito viene descritta la modalità replica geografica tooconfigure utilizzando Management Studio. Vengono forniti passaggi toocreate non leggibile e leggibili database secondari, come un singolo database o in un pool elastico.

> [!NOTE]
> Se è presente un database nel server partner specificato hello con hello stesso nome come hello database primario hello comando avrà esito negativo.
> 

### <a name="add-readable-secondary-single-database"></a>Aggiungere un database secondario accessibile in lettura (database singolo)
Utilizzare hello seguendo i passaggi toocreate un database secondario leggibile come un singolo database.

1. In Management Studio, connettersi tooyour server logico di Database SQL di Azure.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare la seguente hello **ALTER DATABASE** istruzione toomake un database locale in un database primario-replica geografica con un database secondario leggibile in un server secondario.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer2> WITH (ALLOW_CONNECTIONS = ALL);
4. Fare clic su **Execute** query hello toorun.

### <a name="add-readable-secondary-elastic-pool"></a>Aggiungere un database secondario leggibile (pool elastico)
Utilizzare i seguenti passaggi toocreate un database secondario leggibile di un pool elastico hello.

1. In Management Studio, connettersi tooyour server logico di Database SQL di Azure.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare la seguente hello **ALTER DATABASE** istruzione toomake un database locale in un database primario-replica geografica con un database secondario leggibile in un server secondario in un pool elastico.
   
        ALTER DATABASE <MyDB>
           ADD SECONDARY ON SERVER <MySecondaryServer4> WITH (ALLOW_CONNECTIONS = ALL
           , SERVICE_OBJECTIVE = ELASTIC_POOL (name = MyElasticPool2));
4. Fare clic su **Execute** query hello toorun.

## <a name="remove-secondary-database"></a>Rimuovere un database secondario
È possibile utilizzare hello **ALTER DATABASE** istruzione toopermanently terminare la relazione di replica hello tra un database secondario e principale. Questa istruzione viene eseguita nel database master di hello in cui hello risiede il database primario. Dopo la terminazione di relazione hello, database secondario hello diventa un database di lettura / scrittura normale. Se il database di toosecondary hello connettività è interrotta hello comando ha esito positivo ma hello secondario diventeranno di lettura / scrittura dopo il ripristino della connettività. Per altre informazioni, vedere [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Livelli di servizio](sql-database-service-tiers.md).

Utilizzare hello seguente secondario di replica geografica tooremove passaggi da una relazione di replica geografica.

1. In Management Studio, connettersi tooyour server logico di Database SQL di Azure.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare la seguente hello **ALTER DATABASE** secondario tooremove replica geografica di istruzione.
   
        ALTER DATABASE <MyDB>
           REMOVE SECONDARY ON SERVER <MySecondaryServer1>;
4. Fare clic su **Execute** query hello toorun.

## <a name="monitor-active-geo-replication-configuration-and-health"></a>Monitorare l'integrità e la configurazione della replica geografica attiva

Attività di monitoraggio includono il monitoraggio della configurazione di replica geografica hello e monitoraggio dello stato di replica di dati.  È possibile utilizzare hello **sys.dm_geo_replication_links** vista a gestione dinamica hello database master tooreturn informazioni su tutti i collegamenti di replica esistente per ogni database nel server logico di Database SQL di Azure hello. Questa vista contiene una riga per ogni hello collegamento di replica tra database primario e secondari. È possibile utilizzare hello **sys.dm_replication_link_status** vista a gestione dinamica tooreturn una riga per ogni Database di SQL Azure è attualmente occupato in un collegamento di replica di replica. Sono inclusi il database primario e i database secondari. Se è presente più di un collegamento di replica continua per un determinato database primario, questa tabella contiene una riga per ognuna delle relazioni hello. visualizzazione di Hello viene creato in tutti i database, tra cui master logico hello. Tuttavia, l'esecuzione di query in questa vista nel database master logico hello restituisce un set vuoto. È possibile utilizzare hello **Sys.dm operation_status** stato hello tooshow vista a gestione dinamica per tutte le operazioni, incluso lo stato di hello hello dei collegamenti di replica di database. Per altre informazioni, vedere [sys.geo_replication_links (database SQL di Azure)](https://msdn.microsoft.com/library/mt575501.aspx), [sys.dm_geo_replication_link_status (database SQL di Azure)](https://msdn.microsoft.com/library/mt575504.aspx) e [sys.dm_operation_status (database SQL di Azure)](https://msdn.microsoft.com/library/dn270022.aspx).

Utilizzare hello partnership toomonitor una replica geografica attiva i passaggi seguenti.

1. In Management Studio, connettersi tooyour server logico di Database SQL di Azure.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare hello seguente istruzione tooshow tutti i database con i collegamenti di replica geografica.
   
        SELECT database_id, start_date, modify_date, partner_server, partner_database, replication_state_desc, role, secondary_allow_connections_desc FROM sys.geo_replication_links;
4. Fare clic su **Execute** query hello toorun.
5. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **MyDB**, quindi fare clic su **nuova Query**.
6. Hello utilizzo dopo la replica di hello tooshow istruzione rimane passo indietro e l'ultimo tempo di replica di database secondari di MyDB.
   
        SELECT link_guid, partner_server, last_replication, replication_lag_sec FROM sys.dm_geo_replication_link_status
7. Fare clic su **Execute** query hello toorun.
8. Utilizzare hello seguente istruzione tooshow hello più recente operazioni di replica geografica associate al database MyDB.
   
        SELECT * FROM sys.dm_operation_status where major_resource_id = 'MyDB'
        ORDER BY start_time DESC
9. Fare clic su **Execute** query hello toorun.

## <a name="next-steps"></a>Passaggi successivi
* toolearn ulteriori informazioni sui gruppi di failover e di replica geografica attiva, vedere - [gruppi di Failover](sql-database-geo-replication-overview.md)
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md)

