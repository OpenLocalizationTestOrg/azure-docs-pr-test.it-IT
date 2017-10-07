---
title: aaaGetting avviato con sincronizzazione dati SQL di Azure (anteprima) | Documenti Microsoft
description: Questa esercitazione fornisce informazioni per iniziare a usare l'anteprima di sincronizzazione dati SQL di Azure.
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a>Introduzione all'anteprima di sincronizzazione dati di SQL Azure
In questa esercitazione viene illustrato come tooset di sincronizzazione dati SQL Azure mediante la creazione di un gruppo di sincronizzazione ibrido che contiene le istanze di Database SQL di Azure e SQL Server. nuovo gruppo di sincronizzazione Hello è completamente configurata e Sincronizza pianificazione hello che è impostata.

Per questa esercitazione è necessario avere già un certo livello di esperienza precedente con il database SQL di Azure e SQL Server. 

Per una panoramica di sincronizzazione dati SQL, vedere [Sincronizzare i dati](sql-database-sync-data.md).

Per esempi di PowerShell completi che illustrano come tooconfigure sincronizzazione dati SQL, vedere hello seguenti articoli:
-   [Utilizzare PowerShell toosync tra più database SQL di Azure](scripts/sql-database-sync-data-between-sql-databases.md)
-   [Utilizzare PowerShell toosync tra un Database SQL di Azure e un database locale di SQL Server](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> Hello completo set di documentazione tecnica per la sincronizzazione dati SQL di Azure, in precedenza si trova nel sito Web MSDN, è disponibile come una. Documento PDF. Scaricarla [qui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).

## <a name="step-1---create-sync-group"></a>Passaggio 1 - Creare un gruppo di sincronizzazione

### <a name="locate-hello-data-sync-settings"></a>Individuare le impostazioni di sincronizzazione dati hello

1.  Nel browser passare toohello portale di Azure.

2.  Nel portale di hello, individuare i database SQL dal Dashboard o dall'icona di database SQL di hello sulla barra degli strumenti hello.

    ![Elenco dei database SQL di Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  In hello **database SQL** blade, database SQL esistente selezionare hello che si desidera toouse come database hub hello per dati di sincronizzazione. pannello database SQL hello viene aperto.

4.  Nel Pannello di database SQL hello per database selezionato hello, selezionare **sincronizzare database tooother**. Apre il pannello di sincronizzazione dati Hello.

    ![Opzione di database di sincronizzazione tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a>Creare un nuovo gruppo di sincronizzazione

1.  Nel Pannello di sincronizzazione dati hello, selezionare **nuovo gruppo di sincronizzazione**. Hello **nuovo gruppo di sincronizzazione** pannello viene aperto con il passaggio 1, **Crea gruppo di sincronizzazione**, evidenziata. Hello **Crea gruppo di sincronizzazione dati** pannello verrà inoltre aperta.

2.  In hello **Crea gruppo di sincronizzazione dati** pannello hello seguenti operazioni:

    1.  In hello **nome gruppo di sincronizzazione** immettere un nome per il nuovo gruppo di sincronizzazione hello.

    2.  In hello **Database dei metadati di sincronizzazione** , scegliere se toocreate un nuovo database (scelta consigliato) o toouse esistente del database.

        > [!NOTE]
        > Microsoft consiglia di creare un nuovo database vuoto di toouse come hello Database dei metadati di sincronizzazione. La sincronizzazione dati crea tabelle in questo database ed esegue un carico di lavoro frequente. Questo database viene automaticamente condivisa come hello Database dei metadati di sincronizzazione per tutti i gruppi di sincronizzazione in un'area selezionata hello. È possibile modificare hello Database dei metadati di sincronizzazione, il nome o il relativo livello di servizio, senza rilasciarlo.

        Se si sceglie **Nuovo database** selezionare **Crea nuovo database**. Hello **Database SQL** apre blade. In hello **Database SQL** pannello, assegnare un nome e configurare hello nuovo database. Selezionare **OK**.

        Se si sceglie **utilizza database esistente**selezionare database hello hello elenco.

    3.  In hello **sincronizzazione automatica** , selezionare innanzitutto **su** o **Off**.

        Se si sceglie **su**, in hello **frequenza di sincronizzazione** sezione, immettere un numero e selezionare secondi, minuti, ore o giorni.

        ![Specificare la frequenza di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  In hello **risoluzione dei conflitti** , selezionare "Hub wins" o "Wins membro".

        ![Specificare come vengono risolti i conflitti](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  Selezionare **OK** e attendere hello nuova sincronizzazione gruppo toobe creato e distribuito.

## <a name="step-2---add-sync-members"></a>Passaggio 2 - Aggiungere i membri di sincronizzazione

Dopo la creazione e distribuzione, il passaggio 2, il nuovo gruppo di sincronizzazione hello **aggiungere membri sincronizzazione**, viene evidenziato in hello **nuovo gruppo di sincronizzazione** blade.

In hello **Database Hub** sezione, immettere le credenziali esistenti hello per il server di Database SQL hello in cui hello si trova il database hub. Non immettere *nuove* credenziali in questa sezione.

![Database hub è stato aggiunto a un gruppo toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a>Aggiungere un database SQL di Azure

In hello **Database membro** sezione, facoltativamente, aggiungere un gruppo di sincronizzazione di Database SQL di Azure toohello selezionando **aggiungere un Database di Azure**. Hello **configurare il Database di Azure** apre blade.

In hello **configurare il Database di Azure** pannello hello seguenti operazioni:

1.  In hello **nome membro sincronizzazione** campo, specificare un nome per il nuovo membro di sincronizzazione hello. Questo nome è diverso dal nome hello del database hello stesso.

2.  In hello **sottoscrizione** hello seleziona il associata sottoscrizione di Azure ai fini della fatturazione.

3.  In hello **Server SQL Azure** server di database SQL esistente hello campo, selezionare.

4.  In hello **Database SQL di Azure** database SQL esistente hello campo, selezionare.

5.  In hello **direzioni di sincronizzazione** campo, selezionare la sincronizzazione bidirezionale, toohello Hub, o da hello Hub.

    ![Aggiungere un nuovo membro di sincronizzazione del database SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  In hello **Username** e **Password** immettere le credenziali esistenti hello per il server di Database SQL hello in quale hello si trova il database membro. Non immettere *nuove* credenziali in questa sezione.

7.  Selezionare **OK** e attendere hello nuova sincronizzazione membro toobe creato e distribuito.

    ![Il nuovo membro di sincronizzazione del database SQL è stato aggiunto](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a>Aggiungere un database di SQL Server locale

In hello **Database membro** sezione, facoltativamente, aggiungere un gruppo di sincronizzazione toohello di SQL Server on-premise selezionando **aggiungere un Database locale**. Hello **configurare On-Premise** apre blade.

In hello **configurare On-Premise** pannello hello seguenti operazioni:

1.  Selezionare **hello scegliere Gateway dell'agente di sincronizzazione**. Hello **selezionare agente di sincronizzazione** apre blade.

    ![Scegli gateway dell'agente di sincronizzazione hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  In hello **hello scegliere Gateway dell'agente di sincronizzazione** pannello, scegliere se toouse un agente esistente o creare un nuovo agente.

    Se si sceglie **agenti esistenti**, selezionare hello agente esistente dall'elenco di hello.

    Se si sceglie **creare un nuovo agente**, hello seguenti operazioni:

    1.  Scaricare software dell'agente di sincronizzazione client hello dal collegamento hello fornito e installarlo nel computer di hello hello SQL Server in cui si trova.
 
        > [!IMPORTANT]
        > Si dispone di comunicare con server hello tooopen in uscita la porta TCP 1433 nell'agente client di hello firewall toolet hello.


    2.  Immettere un nome per l'agente di hello.

    3.  Selezionare **Crea e genera chiave**.

    4.  Copiare negli Appunti di toohello chiave agente hello.
        
        ![Creazione di un nuovo agente di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  Selezionare **OK** tooclose hello **selezionare agente di sincronizzazione** blade.

    6.  Nel computer di SQL Server hello, individuare ed eseguire app di agente di sincronizzazione Client hello.

        ![app di agente client di sincronizzazione dati di Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  Nell'app dell'agente di sincronizzazione hello selezionare **Invia chiave agente**. Hello **configurazione Database di sincronizzazione dei metadati** verrà visualizzata la finestra di dialogo.

    8.  In hello **configurazione Database di sincronizzazione dei metadati** nella finestra di dialogo Incolla nella chiave agente hello copiato dal portale di Azure hello. Anche fornire le credenziali esistenti di hello per il server di Database SQL di Azure hello in quali hello si trova il database dei metadati. (Se è stato creato un nuovo database di metadati, il database è in hello stesso server come database hub hello.) Selezionare **OK** e attendere toofinish configurazione hello.

        ![Immettere le credenziali di chiave e il server agente hello](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   Se si verifica un errore di firewall a questo punto, è necessario toocreate una regola del firewall tooallow Azure il traffico in ingresso dal computer di SQL Server hello. È possibile creare la regola hello manualmente nel portale di hello, ma può risultare più semplice toocreate che in SQL Server Management Studio (SSMS). In SQL Server Management Studio, provare a database hub di toohello tooconnect in Azure. Immettere il nome nel formato \<nome_database_hub\>.database.windows.net. Seguire i passaggi di hello nella regola firewall di Azure di hello finestra di dialogo tooconfigure hello. Ritornare quindi toohello app di agente di sincronizzazione Client.

    9.  Nell'app di agente di sincronizzazione Client hello, fare clic su **registrare** tooregister un database di SQL Server con l'agente di hello. Hello **configurazione di SQL Server** verrà visualizzata la finestra di dialogo.

        ![Aggiungere e configurare un database di SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. In hello **configurazione di SQL Server** finestra di dialogo, scegliere se tooconnect mediante l'autenticazione di SQL Server o l'autenticazione di Windows. Se si sceglie l'autenticazione di SQL Server, immettere le credenziali esistenti hello. Specificare il nome di hello del database hello che SQL Server hello che si desidera toosync. Selezionare **Test della connessione** tootest le impostazioni. Selezionare quindi **Salva**. database registrato Hello viene visualizzato nell'elenco di hello.

        ![Il database di SQL Server è ora registrato](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. È ora possibile chiudere l'applicazione di agente di sincronizzazione Client hello.

    12. Nel portale hello hello **configurare On-Premise** pannello seleziona **selezionare hello Database.** Hello **seleziona Database** apre blade.

    13. In hello **seleziona Database** pannello in hello **nome membro sincronizzazione** campo, specificare un nome per il nuovo membro di sincronizzazione hello. Questo nome è diverso dal nome hello del database hello stesso. Selezionare database hello hello elenco. In hello **direzioni di sincronizzazione** campo, selezionare la sincronizzazione bidirezionale, toohello Hub, o da hello Hub.

        ![Selezionare hello nel database locale](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. Selezionare **OK** tooclose hello **seleziona Database** blade. Selezionare quindi **OK** tooclose hello **configurare On-Premise** blade e attendere hello sincronizzazione nuovo membro toobe creato e distribuito. Infine, fare clic su **OK** tooclose hello **selezionare i membri di sincronizzazione** blade.

        ![Nel database locale aggiunto toosync gruppo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  tooconnect tooSQL sincronizzazione dati e l'agente locale hello, aggiungere il ruolo di utente nome toohello `DataSync_Executor`. Sincronizzazione dati crea questo ruolo nell'istanza di SQL Server hello.

## <a name="step-3---configure-sync-group"></a>Passaggio 3 - Configurare il gruppo di sincronizzazione

Dopo avere creati e distribuiti, il passaggio 3, nuovi membri del gruppo sincronizzazione hello **Configura gruppo di sincronizzazione**, viene evidenziato in hello **nuovo gruppo di sincronizzazione** blade.

1.  In hello **tabelle** pannello Seleziona un database dall'elenco di hello della sincronizzazione i membri del gruppo e quindi selezionare **aggiornare lo schema**.

2.  Dall'elenco di hello delle tabelle disponibili, selezionare le tabelle di hello che si desidera toosync.

    ![Selezionare le tabelle toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  Per impostazione predefinita, vengono selezionate tutte le colonne nella tabella hello. Se non si desidera toosync tutte le colonne di hello, disabilitare la casella di controllo di hello per le colonne di hello che non si desidera toosync. Assicurarsi di colonna di chiave primaria hello tooleave selezionato.

    ![Selezionare i campi toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  Infine, selezionare **Salva**.

## <a name="next-steps"></a>Passaggi successivi
A questo punto è stato creato un gruppo di sincronizzazione che include sia un'istanza di database SQL che un database di SQL Server.

Per altre informazioni sul database SQL e la sincronizzazione dati SQL, vedere:

-   [Scaricare la documentazione tecnica sincronizzazione dati SQL completezza hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [Scaricare la documentazione delle API REST di sincronizzazione dati SQL hello](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [Panoramica del database SQL](sql-database-technical-overview.md)
-   [Gestione del ciclo di vita del database](https://msdn.microsoft.com/library/jj907294.aspx)
