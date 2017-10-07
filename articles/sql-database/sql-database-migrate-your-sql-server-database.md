---
title: aaaMigrate tooAzure di database di SQL Server Database SQL | Documenti Microsoft
description: Informazioni su toomigrate il tooAzure di database di SQL Server Database SQL.
services: sql-database
documentationcenter: 
author: janeng
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,load & move data
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/27/2017
ms.author: janeng
ms.openlocfilehash: d10ad1d26576194f1dd6858bae5c3e7c1ec4fb91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-sql-server-database-tooazure-sql-database"></a>Eseguire la migrazione del tooAzure di database di SQL Server Database SQL

Spostamento del Server SQL database tooAzure Database SQL è un processo in tre parti: preparare, quindi esportare e quindi importare il database di hello. In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Preparare un database in SQL Server per la migrazione tooAzure Database SQL tramite hello [dati Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA)
> * Esportare file BACPAC di hello database tooa
> * Importare file BACPAC hello in un Database di SQL Azure

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

- Versione più recente di hello installato di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). Versione più recente di hello di SQLPackage, un'utilità della riga di comando che può essere utilizzato tooautomate una gamma di attività di sviluppo del database viene installato anche l'installazione di SQL Server Management Studio. 
- Hello installato [dati Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595) (DMA).
- E si dispone di accesso tooa database toomigrate. Questa esercitazione viene utilizzato hello [SQL Server 2008 R2 database OLTP AdventureWorks](https://msftdbprodsamples.codeplex.com/releases/view/59211) in un'istanza di SQL Server 2008 R2 o versioni più recenti, ma è possibile utilizzare qualsiasi database di propria scelta. problemi di compatibilità toofix, utilizzare [SQL Server Data Tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)

## <a name="prepare-for-migration"></a>Preparare la migrazione

Si è pronti tooprepare per la migrazione. Seguire questi hello toouse passaggi  **[dati Migration Assistant](https://www.microsoft.com/download/details.aspx?id=53595)**  tooassess hello preparazione del database di migrazione tooAzure Database SQL.

1. Aprire hello **dati Migration Assistant**. È possibile eseguire DMA su qualsiasi computer con connettività toohello istanza contenente hello database di SQL Server che si prevede di toomigrate, non è necessario tooinstall sul computer che ospita hello hello istanza di SQL Server.

     ![aprire Data Migration Assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-open.png)

2. Scegliere dal menu a sinistra hello **+ nuovo** toocreate un **valutazione** progetto. Compilare il modulo hello con un **nome progetto** (tutti gli altri valori lasciare i valori predefiniti) e fare clic su **crea**. Hello **opzioni** verrà visualizzata la pagina.

     ![nuovo progetto di Data Migration Assistant](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-new-project.png)

3. In hello **opzioni** pagina, fare clic su **Avanti**. Hello **selezionare origini** verrà visualizzata la pagina.

     ![nuova migrazione di dati opzioni](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-options.png) 

4. In hello **selezionare origini** pagina, immettere il nome di hello dell'istanza di SQL Server che contiene server hello si prevede di toomigrate. Modifica hello altri valori in questa pagina, se necessario. Fare clic su **Connetti**.

     ![nuova migrazione di dati selezione delle origini](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources.png)

5. In hello **aggiungere origini** parte hello **selezionare origini** pagina, selezionare le caselle di controllo di hello per hello database toobe testate per la compatibilità. Fare clic su **Aggiungi**.

     ![nuova migrazione di dati selezione delle origini](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-sources-add.png)

6. Fare clic su **Start Assessment** (Avvia valutazione).

     ![nuova migrazione di dati avvio della valutazione](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-start-assessment.png)

7. Al termine della valutazione di hello, esaminare innanzitutto toosee se hello database toomigrate sufficientemente compatibili. Cercare hello segno di spunta in un cerchio verde.

     ![nuova migrazione di dati valutazione della compatibilità](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-compatible.png)

8. Esaminare i risultati di hello. Hello **parità di funzionalità di SQL Server** risultati sono tooreview di risultati predefinito hello. In particolare, esaminare le informazioni di hello sulle funzionalità non supportate o supportate parzialmente e le informazioni fornita hello sulle azioni consigliate. 

     ![nuova migrazione di dati valutazione della parità](./media/sql-database-migrate-your-sql-server-database/data-migration-assistant-assessment-results-parity.png)

9. Hello revisione **problemi di compatibilità** facendo clic su questa opzione in alto a sinistra di hello. In particolare hello informazioni sui blocchi di migrazione, le modifiche di comportamento e le funzionalità per ogni livello di compatibilità deprecate. Per il database AdventureWorks2008R2 hello, rivedere le modifiche di hello tooFull ricerca poiché SQL Server 2008 e hello cambia tooSERVERPROPERTY('LCID') rispetto a SQL Server 2000. Per i dettagli su queste modifiche sono disponibili alcuni collegamenti ad altre informazioni. Molte opzioni di ricerca e impostazioni per la ricerca Full-Text sono state modificate 

   > [!IMPORTANT] 
   > Dopo la migrazione del Database SQL di tooAzure database, è possibile scegliere il database hello toooperate al livello corrente compatibilità (livello 100 per il database AdventureWorks2008R2 hello) o a un livello superiore. Per ulteriori informazioni sulle opzioni per l'uso di un database a un livello di compatibilità e le implicazioni di hello, vedere [del livello di compatibilità di ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level). Vedere anche [ALTER DATABASE SCOPED CONFIGURATION](https://docs.microsoft.com/sql/t-sql/statements/alter-database-scoped-configuration-transact-sql) per informazioni sulle impostazioni a livello di database aggiuntive correlate toocompatibility livelli.
   >

10. Facoltativamente, fare clic su **esportare report** report hello toosave come un file JSON.
11. Chiude hello dati Migration Assistant.

## <a name="export-toobacpac-file"></a>File di esportazione tooBACPAC 

Un file BACPAC è un file ZIP con un'estensione di file BACPAC che contiene metadati hello e i dati da un database di SQL Server. Un file BACPAC può essere memorizzato nell'archiviazione blob di Azure o nell'archiviazione locale per l'archiviazione o per la migrazione, ad esempio dal tooAzure di SQL Server Database SQL. Per un toobe esportazione consistente, è non necessario assicurarsi che nessun scrittura è in corso attività durante l'esportazione di hello.

Seguire questi passaggi toouse hello SQLPackage utilità della riga di comando tooexport hello AdventureWorks2008R2 toolocal archiviazione del database.

1. Aprire un prompt dei comandi di Windows e modificare la cartella tooa directory in cui è hello **130** versione di SQLPackage, ad esempio **C:\Program Files (x86) \Microsoft SQL Server\130\DAC\bin**.

2. Eseguire hello SQLPackage comando al prompt dei comandi di prova tooexport prova seguente **AdventureWorks2008R2** del database di **localhost** troppo**AdventureWorks2008R2.bacpac**. Modificare uno di questi valori come ambiente tooyour appropriato.

    ```SQLPackage
    sqlpackage.exe /Action:Export /ssn:localhost /sdn:AdventureWorks2008R2 /tf:AdventureWorks2008R2.bacpac
    ```

    ![esportazione con sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-export.png)

Dopo il completamento dell'esecuzione di hello file BACPAC hello generato è archiviato nella directory hello sqlpackage hello eseguibile in cui si trova. In questo esempio C:\Programmi (x86)\Microsoft SQL Server\130\DAC\bin. 

## <a name="log-in-toohello-azure-portal"></a>Accedi toohello portale di Azure

Accedi toohello [portale di Azure](https://portal.azure.com/). L'accesso dal computer di hello da cui è in esecuzione l'utilità della riga di comando di hello SQLPackage semplifica la creazione di hello hello regola del firewall nel passaggio 5.

## <a name="create-a-sql-server-logical-server"></a>Creare un server logico SQL Server

Un [server logico SQL Server](sql-database-features.md) funge da punto di gestione centrale per più database. Seguire questi passaggi toocreate messaggi hello del server logico toocontain un SQL server eseguita la migrazione di database di SQL Server di Adventure Works OLTP. 

1. Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.

2. Tipo **sql server** nella finestra di ricerca hello in hello **New** pagina e selezionare **database SQL (server logico)** da hello elenco filtrato.

    ![Selezionare il server logico](./media/sql-database-migrate-your-sql-server-database/logical-server.png)

3. In hello **tutto** pagina, fare clic su **SQL server (server logico)** e quindi fare clic su **crea** su hello **SQL Server (server logico)** pagina .

    ![creare un server logico](./media/sql-database-migrate-your-sql-server-database/logical-server-create.png)

4. Compilare hello SQL server (server logico) modulo con hello le seguenti informazioni, come mostrato nella precedente immagine hello:     

   | Impostazione       | Valore consigliato | Descrizione | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | **Server name** (Nome server) | Inserire qualsiasi nome univoco globale | Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). | 
   | **Nome di accesso amministratore server** | Inserire qualsiasi nome valido | Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database). |
   | **Password** | Inserire qualsiasi password valida | La password deve contenere almeno 8 caratteri e deve contenere caratteri di tre delle seguenti categorie di hello: lettere maiuscole, lettere minuscole, numeri e caratteri non alfanumerici. |
   | **Sottoscrizione** | Selezionare una sottoscrizione | Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni). |
   | **Gruppo di risorse** | Scegliere un gruppo di risorse esistente o creare un nuovo gruppo, come **myResourceGroup** |  Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni). |
   | **Posizione** | Immettere un percorso valido per nuovo server hello | Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/). |

   ![modulo di creazione del server logico completato](./media/sql-database-migrate-your-sql-server-database/logical-server-create-completed.png)

5. Fare clic su **crea** tooprovision server logico di hello. Il provisioning richiede alcuni minuti. 

> [!IMPORTANT]
> Ricordare il nome del server, il nome dell'account di accesso amministratore server e la password. Più avanti in questa esercitazione saranno necessari questi valori.
>

## <a name="create-a-server-level-firewall-rule"></a>Creare una regola del firewall a livello di server

Hello servizio Database SQL crea una [firewall a livello di server hello](sql-database-firewall-configure.md) che impedisce la applicazioni esterne e gli strumenti connessione toohello server o da qualsiasi database nel server di hello solo una regola del firewall creata hello tooopen firewall per indirizzi IP specifici. Seguire questi toocreate passaggi una regola del firewall a livello di server di Database SQL per l'indirizzo IP di hello del computer di hello da cui è in esecuzione l'utilità della riga di comando di SQLPackage hello. In questo modo SQLPackage tooconnect toohello SQL serverDatabase server logico attraverso il firewall di Database SQL di Azure hello. 

1. Fare clic su **tutte le risorse** dal menu a sinistra di hello e fare clic sul nuovo server in hello **tutte le risorse** pagina. pagina di panoramica Hello del server consente di aprire e offre opzioni per un'ulteriore configurazione.

     ![panoramica del server logico](./media/sql-database-migrate-your-sql-server-database/logical-server-overview.png)

2. Fare clic su **Firewall** nel menu a sinistra, hello in **impostazioni** nella pagina di panoramica hello. Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello. 

3. Fare clic su **Aggiungi indirizzo IP del client** sull'indirizzo IP del computer hello hello barra degli strumenti tooadd hello attualmente in uso e quindi fare clic su **salvare**. Viene creata una regola del firewall a livello di server per questo indirizzo IP.

     ![Impostare la regola del firewall del server](./media/sql-database-migrate-your-sql-server-database/server-firewall-rule-set.png)

4. Fare clic su **OK**.

È ora possibile connettersi tooall database nel server mediante SQL Server Management Studio o un altro strumento di propria scelta da questo indirizzo IP utilizzando l'account amministratore di server hello creato in precedenza.

> [!NOTE]
> Il database SQL comunica attraverso la porta 1433. Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete. In questo caso, è possibile connettersi tooyour server di Database SQL di Azure, a meno che il reparto IT consente di aprire la porta 1433.
>

## <a name="import-a-bacpac-file-tooazure-sql-database"></a>Importare un tooAzure file BACPAC SQL Database 

le versioni più recenti di Hello di hello utilità della riga di comando SQLPackage forniscono supporto per la creazione di un database SQL di Azure per uno specifico [servizio a livello di prestazioni e](sql-database-service-tiers.md). Per prestazioni ottimali durante l'importazione, selezionare un livello di prestazioni e di servizio elevati e quindi scalare verso il basso al termine dell'importazione, se il livello di prestazioni e di servizio hello è supera a quello necessario immediatamente.

Seguire questi passaggi utilizzare hello SQLPackage utilità della riga di comando tooimport hello AdventureWorks2008R2 database tooAzure Database SQL. Sebbene sia possibile utilizzare SQL Server Management Studio per questa attività, SQLPackage è hello preferito per la maggior parte degli ambienti di produzione per offrire la massima flessibilità e prestazioni ottimali. Vedere [la migrazione da SQL Server tooAzure Database SQL tramite file BACPAC](https://blogs.msdn.microsoft.com/sqlcat/2016/10/20/migrating-from-sql-server-to-azure-sql-database-using-bacpac-files/).

- Eseguire hello SQLPackage comando al prompt dei comandi di prova tooimport prova seguente **AdventureWorks2008R2** del database di server logico di archiviazione locale toohello SQL server che si tooa creato in precedenza nuovo database, un servizio livello di **Premium**e un obiettivo di servizio di **P6**. Sostituire i valori hello tra parentesi quadre con i valori appropriati per il server logico in SQL server e specificare un nome per il nuovo database hello (anche sostituire hello angolari). Inoltre, è possibile scegliere valori hello toochange per l'edizione del database e servizio objectgive come ambiente tooyour appropriato. A scopo di hello di questa esercitazione, viene chiamato database migrato hello **myMigratedDatabase**.

    ```
    SqlPackage.exe /a:import /tcs:"Data Source=<your_server_name>.database.windows.net;Initial Catalog=<your_new_database_name>;User Id=<change_to_your_admin_user_account>;Password=<change_to_your_password>" /sf:AdventureWorks2008R2.bacpac /p:DatabaseEdition=Premium /p:DatabaseServiceObjective=P6
    ```

   ![importazione sqlpackage](./media/sql-database-migrate-your-sql-server-database/sqlpackage-import.png)

> [!IMPORTANT]
> Un server logico SQL Server è in ascolto sulla porta 1433. Se si sta tentando di tooconnect tooa SQL server server logico all'interno di un firewall aziendale, questa porta deve essere aperta nel firewall aziendale hello per la connessione è toosuccessfully.
>

## <a name="connect-using-sql-server-management-studio-ssms"></a>Eseguire la connessione usando SQL Server Management Studio (SSMS)

Utilizzare SQL Server Management Studio tooestablish un server di Database SQL di Azure tooyour di connessione e il database appena migrato, denominato **myMigratedDatabase** in questa esercitazione. Se si esegue SQL Server Management Studio in un computer diverso da cui è stato eseguito SQLPackage, creare una regola del firewall per questo computer attenendosi alla procedura di hello nella procedura precedente hello.

1. Aprire SQL Server Management Studio.

2. In hello **connettersi tooServer** finestra di dialogo immettere hello le seguenti informazioni:
   - **Tipo di server**: specificare il motore del database
   - **Nome server**: immettere il nome completo del server, ad esempio **mynewserver20170403.database.windows.net**
   - **Autenticazione**: specificare l'Autenticazione di SQL Server
   - **Accesso**: immettere l'account dell'amministratore del server
   - **Password**: immettere hello password per l'account di amministratore del server
 
    ![connessione con SSMS](./media/sql-database-migrate-your-sql-server-database/connect-ssms.png)

3. Fare clic su **Connetti**. verrà visualizzata la finestra di Esplora oggetti Hello. 

4. In Esplora oggetti espandere **database** e quindi espandere **myMigratedDatabase** oggetti hello tooview nel database di esempio hello.

## <a name="change-database-properties"></a>Cambiare le proprietà del database

È possibile modificare il livello di servizio hello, livello di prestazioni e il livello di compatibilità con SQL Server Management Studio. Durante la fase di importazione hello, è consigliabile che l'importazione di tooa superiori prestazioni livello database per ottenere prestazioni ottimali, ma scalare verso il basso termine hello importazione money toosave finché non si è pronti tooactively Usa hello importati database. Modifica il livello di compatibilità di hello può produrre migliori prestazioni e le funzionalità più recenti di accesso toohello di hello servizio Database SQL di Azure. Quando si esegue la migrazione di un database meno recente, il livello di compatibilità del database viene mantenuto a livello di hello supportato più basso che è compatibile con il database di hello importato. Per altre informazioni, vedere [Miglioramento delle prestazioni delle query con il livello di compatibilità 130 nel database SQL di Azure](sql-database-compatibility-level-query-performance-130.md).

1. In Esplora oggetti fare clic con il pulsante destro del mouse su **myMigratedDatabase** e scegliere **Nuova query**. Database tooyour connesso viene visualizzata una finestra di query.

2. Eseguire hello seguente livello di servizio hello tooset comando troppo**Standard** e hello livello di prestazioni troppo**S1**.

    ```
    ALTER DATABASE myMigratedDatabase 
    MODIFY 
        (
        EDITION = 'Standard'
        , MAXSIZE = 250 GB
        , SERVICE_OBJECTIVE = 'S1'
    );
    ```

    ![cambiare il livello di servizio](./media/sql-database-migrate-your-sql-server-database/service-tier.png)

3. Eseguire hello seguente livello di compatibilità del database del comando toochange hello troppo**130**.

    ```
    ALTER DATABASE myMigratedDatabase  
    SET COMPATIBILITY_LEVEL = 130;
    ```

   ![cambiare il livello di compatibilità](./media/sql-database-migrate-your-sql-server-database/compat-level.png)

## <a name="next-steps"></a>Passaggi successivi 
In questa esercitazione è stato illustrato come preparare, esportare e importare un database. Si è appreso come:

> [!div class="checklist"]
> * Preparare un database in SQL Server per la migrazione tooAzure Database SQL
> * Esportare file BACPAC di hello database tooa
> * Importare file BACPAC hello in un Database di SQL Azure

Spostare toolearn esercitazione successiva toohello come toosecure del database.

> [!div class="nextstepaction"]
> [Proteggere il database SQL di Azure](sql-database-security-tutorial.md)


