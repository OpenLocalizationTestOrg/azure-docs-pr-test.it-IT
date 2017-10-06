---
title: 'T-SQL: gestire un pool elastico di database SQL di Azure | Microsoft Docs'
description: Utilizzare T-SQL toomanage un pool elastico del Database SQL di Azure.
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: 666f131b2c88849a1a9ea83381bbc27548e93599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a>Monitorare e gestire un pool elastico con Transact-SQL
In questo argomento illustra come toomanage scalabile [pool elastici](sql-database-elastic-pool.md) con Transact-SQL.  È anche possibile creare e gestire un hello Azure pool elastico [portale di Azure](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), hello l'API REST o [c#](sql-database-elastic-pool-manage-csharp.md). È anche possibile creare e spostare database verso e dai pool elastici usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).


Hello utilizzare [Create Database (Database SQL di Azure)](https://msdn.microsoft.com/library/dn268335.aspx) e [Database(Azure SQL Database) Alter](https://msdn.microsoft.com/library/mt574871.aspx) comandi toocreate e spostamento di database in e da un pool elastico. pool elastico Hello deve essere presente prima di poter usare questi comandi. che hanno effetto solo sui database. Impossibile modificare la creazione di nuovi pool e hello dell'impostazione della proprietà di pool di applicazioni (ad esempio min e max Edtu) con i comandi T-SQL.

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Creare un nuovo database in pool in un pool elastico
Comando CREATE DATABASE hello con opzione di SERVICE_OBJECTIVE hello.   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

Tutti i database in un pool elastico ereditano il livello di servizio hello del pool elastico di hello (Basic, Standard e Premium). 

## <a name="move-a-database-between-elastic-pools"></a>Spostare un database tra pool elastici
Comando ALTER DATABASE hello con hello modifica e impostare servizio\_opzione obiettivo come ELASTICA\_POOL. Impostare toohello nome hello del pool di destinazione hello.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move hello database named db1 tooan elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a>Spostare un database in un pool elastico
Comando ALTER DATABASE hello con hello modifica e impostare servizio\_opzione obiettivo come ELASTIC_POOL. Impostare toohello nome hello del pool di destinazione hello.

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move hello database named db1 tooan elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a>Spostare un database da un pool elastico
Utilizzare il comando di ALTER DATABASE hello e impostare hello SERVICE_OBJECTIVE tooone hello livelli di prestazioni (ad esempio S0 o S1).

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes hello database into a stand-alone database with hello service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a>Elencare i database in un pool elastico
Hello utilizzare [sys\_servizio \_visualizzazione obiettivi](https://msdn.microsoft.com/library/mt712619) toolist tutti hello database in un pool elastico. Visualizzazione del log nel database master toohello database tooquery hello.

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Ottenere i dati di utilizzo delle risorse per un pool elastico
Hello utilizzare [sys.elastic\_pool \_risorse \_Visualizza statistiche](https://msdn.microsoft.com/library/mt280062.aspx) statistiche di utilizzo delle risorse di tooexamine hello di un pool elastico in un server logico. Visualizzazione del log nel database master toohello database tooquery hello.

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a>Ottenere l'utilizzo delle risorse per un database in pool
Hello utilizzare [sys.dm\_ db\_ risorse\_Visualizza statistiche](https://msdn.microsoft.com/library/dn800981.aspx) o [sys.resource \_Visualizza statistiche](https://msdn.microsoft.com/library/dn269979.aspx) statistiche di utilizzo delle risorse di tooexamine hello di un database in un pool elastico. Questo processo è simile tooquerying utilizzo delle risorse per un singolo database.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato un pool elastico, è possibile gestire i database elastici nel pool di hello creando processi elastici. Elastici processi facilitano l'esecuzione di script T-SQL rispetto a qualsiasi numero di database nel pool di hello. Per ulteriori informazioni, vedere [Panoramica dei processi di database elastici](sql-database-elastic-jobs-overview.md). 

Vedere [scalabilità orizzontale con Database SQL di Azure](sql-database-elastic-scale-introduction.md): utilizzare tooscale strumenti di database elastico out, spostare i dati, eseguire una query o creare transazioni.

