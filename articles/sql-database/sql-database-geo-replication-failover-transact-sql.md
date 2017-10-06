---
title: Failover TSQL:Initiate per il database SQL di Azure | Microsoft Docs
description: Avviare un failover pianificato o non pianificato per il database SQL di Azure usando Transact-SQL
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5eb2d256-025d-4f5a-99d4-17f702b37f14
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 418953e044ba84ce758063d56a371af45d5cdfe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="initiate-a-planned-or-unplanned-failover-for-azure-sql-database-with-transact-sql"></a>Avviare un failover pianificato o non pianificato per il database SQL di Azure con Transact-SQL

In questo articolo illustra come tooinitiate failover tooa Database SQL secondario tramite Transact-SQL. tooconfigure-replica geografica, vedere [configurare la replica geografica per il Database di SQL Azure](sql-database-geo-replication-transact-sql.md).

tooinitiate failover, è necessario seguente hello:

* Un account di accesso DBManager su hello primario
* Avere db_ownership del database locale di hello che sia necessario abilitare la replica geografica
* Essere DBManager in toowhich server partner di hello verrà configurata la replica geografica
* La versione più recente di SQL Server Management Studio (SSMS)

> [!IMPORTANT]
> È consigliabile utilizzare sempre hello versione più recente di Management Studio tooremain sincronizzati con gli aggiornamenti tooMicrosoft Azure e il Database SQL. [Aggiornare SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).
>  

## <a name="initiate-a-planned-failover-promoting-a-secondary-database-toobecome-hello-new-primary"></a>Avviare un failover pianificato la promozione di un database secondario toobecome hello nuovo database primario
È possibile utilizzare hello **ALTER DATABASE** istruzione toopromote un database secondario toobecome hello nuovo database primario del database in modo pianificato toobecome primario esistente hello l'abbassamento di livello un database secondario. Questa istruzione viene eseguita nel database master hello il server logico di hello Database SQL di Azure in cui hello risiede database secondari con replica geografica che viene innalzato di livello. Questa funzionalità è progettata per il failover pianificato, ad esempio durante il drill di ripristino di emergenza hello e richiede che il database primario hello siano disponibili.

comando Hello esegue hello del flusso di lavoro seguente:

1. Temporaneamente in modalità toosynchronous replica commutatori, causando tutte le transazioni in sospeso toobe scaricate toohello secondario e il blocco di tutte le nuove transazioni;
2. Commutatori hello ruoli di database di due hello nella relazione di replica geografica hello.  

Questa sequenza garantisce che hello due database siano sincronizzati prima di passare i ruoli di hello e pertanto si verificherà alcuna perdita di dati. È un breve periodo durante il quale entrambi i database non sono disponibili (in ordine di hello di 0 secondi too25) durante il cambio di ruolo hello. Se il database primario hello dispone di più database secondari, il comando hello verrà automaticamente reconfigure hello altri database secondari tooconnect toohello nuovo database primario.  intera operazione Hello richiederà meno di un minuto toocomplete in circostanze normali. Per altre informazioni, vedere [ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) e [Livelli di servizio](sql-database-service-tiers.md).

Utilizzare hello seguendo i passaggi tooinitiate un failover pianificato.

1. In Management Studio, connettere il server logico di toohello Database SQL di Azure in cui risiede un database secondario di replica geografica.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare la seguente hello **ALTER DATABASE** ruolo primario di istruzione tooswitch hello database secondario toohello.
   
        ALTER DATABASE <MyDB> FAILOVER;
4. Fare clic su **Execute** query hello toorun.

> [!NOTE]
> In rari casi, è possibile che operazione hello non è possibile completare e che risulti bloccato. In questo caso, utente hello può eseguire il comando di failover forzato hello e accettare la perdita di dati.
> 
> 

## <a name="initiate-an-unplanned-failover-from-hello-primary-database-toohello-secondary-database"></a>Avviare un failover non pianificato da database secondario di hello database primario toohello
È possibile utilizzare hello **ALTER DATABASE** istruzione toopromote un database secondario toobecome hello nuovo database primario del database in modo non pianificato, imporre l'abbassamento di livello hello di toobecome primario esistente hello un database secondario in un momento quando hello database primario non è più disponibile. Questa istruzione viene eseguita nel database master hello il server logico di hello Database SQL di Azure in cui hello risiede database secondari con replica geografica che viene innalzato di livello.

Questa funzionalità è progettata per il ripristino di emergenza quando la disponibilità di ripristino del database hello è critico e perdita di dati è accettabile. Quando viene richiamato il failover forzato, hello specificato immediatamente database secondario diventa hello database primario e inizia ad accettare transazioni di scrittura. Come database primario originale hello è in grado di tooreconnect con questo nuovo database primario, un backup incrementale viene eseguito sul database primario originale hello e database primario precedente hello viene trasformata in un database secondario per hello nuovo database primario; Successivamente, è semplicemente una replica di sincronizzazione del nuovo database primario di hello.

Tuttavia, poiché ripristino temporizzato non è supportato nei database secondari hello, se desidera hello toorecover dati eseguito il commit toohello database primario precedente che non fosse stata replicata toohello nuovo database primario prima che si è verificato il failover forzato hello, Salve, sarà necessario utente tooengage supporto toorecover questa perdita di dati.

Se il database primario hello dispone di più database secondari, il comando hello verrà automaticamente reconfigure hello altri database secondari tooconnect toohello nuovo database primario.

Utilizzare hello seguendo i passaggi tooinitiate un failover non pianificato.

1. In Management Studio, connettere il server logico di toohello Database SQL di Azure in cui risiede un database secondario di replica geografica.
2. Aprire hello cartella del database, espandere hello **database di sistema** pulsante destro del mouse nella cartella **master**, quindi fare clic su **nuova Query**.
3. Utilizzare la seguente hello **ALTER DATABASE** ruolo primario di istruzione tooswitch hello database secondario toohello.
   
        ALTER DATABASE <MyDB>   FORCE_FAILOVER_ALLOW_DATA_LOSS;
4. Fare clic su **Execute** query hello toorun.

> [!NOTE]
> Se il comando hello viene emesso quando sia primario e secondario sono online primario precedente hello diventerà hello nuovo database secondario immediatamente senza la sincronizzazione dei dati. Se è hello primario possono verificarsi il commit delle transazioni quando il comando hello viene eseguito una perdita di dati.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Dopo il failover, verificare i requisiti di autenticazione hello per server e database sono configurati nel nuovo database primario di hello. Per tutti i dettagli, vedere l'articolo sulla [sicurezza del database SQL di Azure dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md).
* toolearn ripristino dopo un'emergenza mediante la replica geografica attiva, inclusi i passaggi di pre- ripristino di e post-ripristino e l'esecuzione di un'analisi di ripristino di emergenza, vedere [il ripristino di emergenza](sql-database-disaster-recovery.md)
* Per un post di blog di Sasha Nosov sulla replica geografica attiva, vedere [Spotlight on new Geo-Replication capabilities](https://azure.microsoft.com/blog/spotlight-on-new-capabilities-of-azure-sql-database-geo-replication/) (Le nuove capacità di replica geografica)
* Per informazioni sulla progettazione cloud applicazioni toouse replica geografica attiva, vedere [progettazione di applicazioni cloud per la continuità aziendale usando la replica geografica](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
* Per informazioni sulla replica geografica attiva con i pool elastici, vedere [Strategie di ripristino di emergenza con pool elastico](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md).
* Per un quadro generale, vedere la [panoramica della continuità aziendale](sql-database-business-continuity.md)

