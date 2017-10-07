---
title: 'Portale di Azure: replica geografica di database SQL | Microsoft Docs'
description: Configurare la replica geografica per il Database SQL di Azure nel portale di Azure di hello e avviare il failover
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a>Configurare la replica geografica attiva per il Database SQL di Azure in hello portale di Azure e avviare il failover

In questo articolo illustra come tooconfigure replica geografica attiva per il Database SQL in hello [portale di Azure](http://portal.azure.com) e tooinitiate failover.

failover tooinitiate con hello portale di Azure, vedere [avviare un failover pianificato o per Database SQL di Azure con il portale di Azure hello](sql-database-geo-replication-portal.md).

tooconfigure replica geografica attiva utilizzando hello portale di Azure, è necessario hello seguenti risorse:

* Un database SQL di Azure: database primario di hello che si desidera area geografica di tooreplicate tooa diversa.

> [!Note]
Replica geografica attiva deve essere compreso tra i database di hello stessa sottoscrizione.

## <a name="add-a-secondary-database"></a>Aggiungere un database secondario
Hello seguente procedura consente di creare un nuovo database secondario in una relazione di replica geografica.  

tooadd un database secondario, è necessario essere proprietario della sottoscrizione hello o comproprietario.

database secondario Hello è hello stesso nome come database primario hello e ha, per impostazione predefinita, hello stesso livello di servizio. database secondario Hello può essere un singolo database o un database in un pool elastico. Per altre informazioni, vedere [Livelli di servizio](sql-database-service-tiers.md).
Dopo aver creato e sottoposto a seeding hello secondario, dati iniziano la replica dal database secondario nuovo toohello hello database primario.

> [!NOTE]
> Se esiste un database partner hello (ad esempio, in seguito a terminare una relazione di replica geografica precedente) comando hello ha esito negativo.
> 

1. In hello [portale di Azure](http://portal.azure.com), esplorare database toohello che si desidera tooset per la replica geografica.
2. Nella pagina di database SQL di hello, selezionare **-replica geografica**e quindi selezionare i database secondari di hello area toocreate hello. È possibile selezionare qualsiasi area diversa area hello che ospita il database primario hello, ma è consigliabile hello [area abbinata](../best-practices-availability-paired-regions.md).
   
    ![Configurare la replica geografica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Selezionare o configurare server hello e il piano tariffario per il database secondario hello.
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/create-secondary.png)
4. Facoltativamente, è possibile aggiungere un pool elastico tooan di database secondario. database secondario di hello toocreate in un pool, fare clic su **pool elastico** e selezionare un pool nel server di destinazione hello. Un pool deve esistere nel server di destinazione hello. Questo flusso di lavoro non crea un pool.
5. Fare clic su **crea** hello tooadd secondario.
6. creazione del database secondario Hello e inizia il processo di seeding hello.
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/seeding0.png)
7. Una volta completato il processo di seeding hello, database secondario hello consente di visualizzare il relativo stato.
   
    ![Seeding completo](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Avviare un failover

database secondario Hello può essere disattivati toobecome hello primario.  

1. In hello [portale di Azure](http://portal.azure.com), Sfoglia toohello database primario in una relazione di replica geografica hello.
2. Nel Pannello di Database SQL di hello, selezionare **tutte le impostazioni** > **-replica geografica**.
3. In hello **secondari** elenco, il database di hello selezionare da toobecome hello nuovo database primario e fare clic su **Failover**.
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Fare clic su **Sì** toobegin hello failover.

comando Hello passa immediatamente database secondario hello in ruolo primario hello. 

È un breve periodo durante il quale entrambi i database non sono disponibili (in ordine di hello di 0 secondi too25) durante il cambio di ruolo hello. Se il database primario hello dispone di più database secondari, il comando hello automaticamente la riconfigurazione hello altri database secondari tooconnect toohello nuovo database primario. intera operazione Hello richiederà meno di un minuto toocomplete in circostanze normali. 

> [!NOTE]
> Questo comando è progettato per il ripristino rapido dei database hello in caso di interruzione. e attiva il failover senza sincronizzazione dei dati (failover forzato).  Se il commit delle transazioni quando il comando hello viene eseguito una perdita di dati può verificarsi hello primario è online. 
> 
> 

## <a name="remove-secondary-database"></a>Rimuovere un database secondario
Questa operazione termina in modo permanente i database secondari di hello replica toohello e modifiche hello ruolo di database di lettura / scrittura hello tooa secondaria regolare. Se il database secondario di hello connettività toohello viene interrotto, il comando di hello ha esito positivo ma hello fa secondari non diventano lettura / scrittura fino a dopo il ripristino della connettività.  

1. In hello [portale di Azure](http://portal.azure.com), Sfoglia toohello database primario in una relazione di replica geografica hello.
2. Nella pagina di database SQL di hello, selezionare **-replica geografica**.
3. In hello **secondari** elenco, database selezionare hello da tooremove dalla relazione di replica geografica hello.
4. Fare clic su **Arresta replica**.
   
    ![Rimuovere un database secondario](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. Verrà visualizzata una finestra di conferma. Fare clic su **Sì** database hello tooremove dalla relazione di replica geografica hello. (Impostato il database di lettura / scrittura tooa non fa parte del processo di replica).

## <a name="next-steps"></a>Passaggi successivi
* toolearn più sulla replica geografica attiva, vedere [replica geografica attiva](sql-database-geo-replication-overview.md).
* Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).

