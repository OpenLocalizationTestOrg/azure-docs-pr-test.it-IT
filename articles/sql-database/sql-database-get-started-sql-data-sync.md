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
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="6517a-103">Introduzione all'anteprima di sincronizzazione dati di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="6517a-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="6517a-104">In questa esercitazione viene illustrato come tooset di sincronizzazione dati SQL Azure mediante la creazione di un gruppo di sincronizzazione ibrido che contiene le istanze di Database SQL di Azure e SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6517a-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="6517a-105">nuovo gruppo di sincronizzazione Hello è completamente configurata e Sincronizza pianificazione hello che è impostata.</span><span class="sxs-lookup"><span data-stu-id="6517a-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="6517a-106">Per questa esercitazione è necessario avere già un certo livello di esperienza precedente con il database SQL di Azure e SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6517a-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="6517a-107">Per una panoramica di sincronizzazione dati SQL, vedere [Sincronizzare i dati](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="6517a-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="6517a-108">Per esempi di PowerShell completi che illustrano come tooconfigure sincronizzazione dati SQL, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="6517a-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="6517a-109">Utilizzare PowerShell toosync tra più database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6517a-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="6517a-110">Utilizzare PowerShell toosync tra un Database SQL di Azure e un database locale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="6517a-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="6517a-111">Hello completo set di documentazione tecnica per la sincronizzazione dati SQL di Azure, in precedenza si trova nel sito Web MSDN, è disponibile come una. Documento PDF.</span><span class="sxs-lookup"><span data-stu-id="6517a-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="6517a-112">Scaricarla [qui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="6517a-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="6517a-113">Passaggio 1 - Creare un gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="6517a-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="6517a-114">Individuare le impostazioni di sincronizzazione dati hello</span><span class="sxs-lookup"><span data-stu-id="6517a-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="6517a-115">Nel browser passare toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="6517a-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="6517a-116">Nel portale di hello, individuare i database SQL dal Dashboard o dall'icona di database SQL di hello sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Elenco dei database SQL di Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="6517a-118">In hello **database SQL** blade, database SQL esistente selezionare hello che si desidera toouse come database hub hello per dati di sincronizzazione. pannello database SQL hello viene aperto.</span><span class="sxs-lookup"><span data-stu-id="6517a-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="6517a-119">Nel Pannello di database SQL hello per database selezionato hello, selezionare **sincronizzare database tooother**.</span><span class="sxs-lookup"><span data-stu-id="6517a-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="6517a-120">Apre il pannello di sincronizzazione dati Hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-120">hello Data Sync blade opens.</span></span>

    ![Opzione di database di sincronizzazione tooother](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="6517a-122">Creare un nuovo gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="6517a-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="6517a-123">Nel Pannello di sincronizzazione dati hello, selezionare **nuovo gruppo di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="6517a-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="6517a-124">Hello **nuovo gruppo di sincronizzazione** pannello viene aperto con il passaggio 1, **Crea gruppo di sincronizzazione**, evidenziata.</span><span class="sxs-lookup"><span data-stu-id="6517a-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="6517a-125">Hello **Crea gruppo di sincronizzazione dati** pannello verrà inoltre aperta.</span><span class="sxs-lookup"><span data-stu-id="6517a-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="6517a-126">In hello **Crea gruppo di sincronizzazione dati** pannello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6517a-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="6517a-127">In hello **nome gruppo di sincronizzazione** immettere un nome per il nuovo gruppo di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="6517a-128">In hello **Database dei metadati di sincronizzazione** , scegliere se toocreate un nuovo database (scelta consigliato) o toouse esistente del database.</span><span class="sxs-lookup"><span data-stu-id="6517a-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="6517a-129">Microsoft consiglia di creare un nuovo database vuoto di toouse come hello Database dei metadati di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="6517a-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="6517a-130">La sincronizzazione dati crea tabelle in questo database ed esegue un carico di lavoro frequente.</span><span class="sxs-lookup"><span data-stu-id="6517a-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="6517a-131">Questo database viene automaticamente condivisa come hello Database dei metadati di sincronizzazione per tutti i gruppi di sincronizzazione in un'area selezionata hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="6517a-132">È possibile modificare hello Database dei metadati di sincronizzazione, il nome o il relativo livello di servizio, senza rilasciarlo.</span><span class="sxs-lookup"><span data-stu-id="6517a-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="6517a-133">Se si sceglie **Nuovo database** selezionare **Crea nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="6517a-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="6517a-134">Hello **Database SQL** apre blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="6517a-135">In hello **Database SQL** pannello, assegnare un nome e configurare hello nuovo database.</span><span class="sxs-lookup"><span data-stu-id="6517a-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="6517a-136">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="6517a-136">Then select **OK**.</span></span>

        <span data-ttu-id="6517a-137">Se si sceglie **utilizza database esistente**selezionare database hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="6517a-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="6517a-138">In hello **sincronizzazione automatica** , selezionare innanzitutto **su** o **Off**.</span><span class="sxs-lookup"><span data-stu-id="6517a-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="6517a-139">Se si sceglie **su**, in hello **frequenza di sincronizzazione** sezione, immettere un numero e selezionare secondi, minuti, ore o giorni.</span><span class="sxs-lookup"><span data-stu-id="6517a-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Specificare la frequenza di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="6517a-141">In hello **risoluzione dei conflitti** , selezionare "Hub wins" o "Wins membro".</span><span class="sxs-lookup"><span data-stu-id="6517a-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Specificare come vengono risolti i conflitti](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="6517a-143">Selezionare **OK** e attendere hello nuova sincronizzazione gruppo toobe creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="6517a-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="6517a-144">Passaggio 2 - Aggiungere i membri di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="6517a-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="6517a-145">Dopo la creazione e distribuzione, il passaggio 2, il nuovo gruppo di sincronizzazione hello **aggiungere membri sincronizzazione**, viene evidenziato in hello **nuovo gruppo di sincronizzazione** blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="6517a-146">In hello **Database Hub** sezione, immettere le credenziali esistenti hello per il server di Database SQL hello in cui hello si trova il database hub.</span><span class="sxs-lookup"><span data-stu-id="6517a-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="6517a-147">Non immettere *nuove* credenziali in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6517a-147">Don't enter *new* credentials in this section.</span></span>

![Database hub è stato aggiunto a un gruppo toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="6517a-149">Aggiungere un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="6517a-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="6517a-150">In hello **Database membro** sezione, facoltativamente, aggiungere un gruppo di sincronizzazione di Database SQL di Azure toohello selezionando **aggiungere un Database di Azure**.</span><span class="sxs-lookup"><span data-stu-id="6517a-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="6517a-151">Hello **configurare il Database di Azure** apre blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="6517a-152">In hello **configurare il Database di Azure** pannello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6517a-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="6517a-153">In hello **nome membro sincronizzazione** campo, specificare un nome per il nuovo membro di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="6517a-154">Questo nome è diverso dal nome hello del database hello stesso.</span><span class="sxs-lookup"><span data-stu-id="6517a-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="6517a-155">In hello **sottoscrizione** hello seleziona il associata sottoscrizione di Azure ai fini della fatturazione.</span><span class="sxs-lookup"><span data-stu-id="6517a-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="6517a-156">In hello **Server SQL Azure** server di database SQL esistente hello campo, selezionare.</span><span class="sxs-lookup"><span data-stu-id="6517a-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="6517a-157">In hello **Database SQL di Azure** database SQL esistente hello campo, selezionare.</span><span class="sxs-lookup"><span data-stu-id="6517a-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="6517a-158">In hello **direzioni di sincronizzazione** campo, selezionare la sincronizzazione bidirezionale, toohello Hub, o da hello Hub.</span><span class="sxs-lookup"><span data-stu-id="6517a-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Aggiungere un nuovo membro di sincronizzazione del database SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="6517a-160">In hello **Username** e **Password** immettere le credenziali esistenti hello per il server di Database SQL hello in quale hello si trova il database membro.</span><span class="sxs-lookup"><span data-stu-id="6517a-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="6517a-161">Non immettere *nuove* credenziali in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="6517a-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="6517a-162">Selezionare **OK** e attendere hello nuova sincronizzazione membro toobe creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="6517a-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Il nuovo membro di sincronizzazione del database SQL è stato aggiunto](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="6517a-164">Aggiungere un database di SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="6517a-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="6517a-165">In hello **Database membro** sezione, facoltativamente, aggiungere un gruppo di sincronizzazione toohello di SQL Server on-premise selezionando **aggiungere un Database locale**.</span><span class="sxs-lookup"><span data-stu-id="6517a-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="6517a-166">Hello **configurare On-Premise** apre blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="6517a-167">In hello **configurare On-Premise** pannello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6517a-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="6517a-168">Selezionare **hello scegliere Gateway dell'agente di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="6517a-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="6517a-169">Hello **selezionare agente di sincronizzazione** apre blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Scegli gateway dell'agente di sincronizzazione hello](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="6517a-171">In hello **hello scegliere Gateway dell'agente di sincronizzazione** pannello, scegliere se toouse un agente esistente o creare un nuovo agente.</span><span class="sxs-lookup"><span data-stu-id="6517a-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="6517a-172">Se si sceglie **agenti esistenti**, selezionare hello agente esistente dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="6517a-173">Se si sceglie **creare un nuovo agente**, hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="6517a-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="6517a-174">Scaricare software dell'agente di sincronizzazione client hello dal collegamento hello fornito e installarlo nel computer di hello hello SQL Server in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="6517a-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="6517a-175">Si dispone di comunicare con server hello tooopen in uscita la porta TCP 1433 nell'agente client di hello firewall toolet hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="6517a-176">Immettere un nome per l'agente di hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="6517a-177">Selezionare **Crea e genera chiave**.</span><span class="sxs-lookup"><span data-stu-id="6517a-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="6517a-178">Copiare negli Appunti di toohello chiave agente hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Creazione di un nuovo agente di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="6517a-180">Selezionare **OK** tooclose hello **selezionare agente di sincronizzazione** blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="6517a-181">Nel computer di SQL Server hello, individuare ed eseguire app di agente di sincronizzazione Client hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![app di agente client di sincronizzazione dati di Hello](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="6517a-183">Nell'app dell'agente di sincronizzazione hello selezionare **Invia chiave agente**.</span><span class="sxs-lookup"><span data-stu-id="6517a-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="6517a-184">Hello **configurazione Database di sincronizzazione dei metadati** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6517a-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="6517a-185">In hello **configurazione Database di sincronizzazione dei metadati** nella finestra di dialogo Incolla nella chiave agente hello copiato dal portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="6517a-186">Anche fornire le credenziali esistenti di hello per il server di Database SQL di Azure hello in quali hello si trova il database dei metadati.</span><span class="sxs-lookup"><span data-stu-id="6517a-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="6517a-187">(Se è stato creato un nuovo database di metadati, il database è in hello stesso server come database hub hello.) Selezionare **OK** e attendere toofinish configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Immettere le credenziali di chiave e il server agente hello](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="6517a-189">Se si verifica un errore di firewall a questo punto, è necessario toocreate una regola del firewall tooallow Azure il traffico in ingresso dal computer di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="6517a-190">È possibile creare la regola hello manualmente nel portale di hello, ma può risultare più semplice toocreate che in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="6517a-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="6517a-191">In SQL Server Management Studio, provare a database hub di toohello tooconnect in Azure.</span><span class="sxs-lookup"><span data-stu-id="6517a-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="6517a-192">Immettere il nome nel formato \<nome_database_hub\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6517a-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="6517a-193">Seguire i passaggi di hello nella regola firewall di Azure di hello finestra di dialogo tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="6517a-194">Ritornare quindi toohello app di agente di sincronizzazione Client.</span><span class="sxs-lookup"><span data-stu-id="6517a-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="6517a-195">Nell'app di agente di sincronizzazione Client hello, fare clic su **registrare** tooregister un database di SQL Server con l'agente di hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="6517a-196">Hello **configurazione di SQL Server** verrà visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="6517a-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Aggiungere e configurare un database di SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="6517a-198">In hello **configurazione di SQL Server** finestra di dialogo, scegliere se tooconnect mediante l'autenticazione di SQL Server o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="6517a-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="6517a-199">Se si sceglie l'autenticazione di SQL Server, immettere le credenziali esistenti hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="6517a-200">Specificare il nome di hello del database hello che SQL Server hello che si desidera toosync.</span><span class="sxs-lookup"><span data-stu-id="6517a-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="6517a-201">Selezionare **Test della connessione** tootest le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6517a-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="6517a-202">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6517a-202">Then select **Save**.</span></span> <span data-ttu-id="6517a-203">database registrato Hello viene visualizzato nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-203">hello registered database appears in hello list.</span></span>

        ![Il database di SQL Server è ora registrato](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="6517a-205">È ora possibile chiudere l'applicazione di agente di sincronizzazione Client hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="6517a-206">Nel portale hello hello **configurare On-Premise** pannello seleziona **selezionare hello Database.**</span><span class="sxs-lookup"><span data-stu-id="6517a-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="6517a-207">Hello **seleziona Database** apre blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="6517a-208">In hello **seleziona Database** pannello in hello **nome membro sincronizzazione** campo, specificare un nome per il nuovo membro di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="6517a-209">Questo nome è diverso dal nome hello del database hello stesso.</span><span class="sxs-lookup"><span data-stu-id="6517a-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="6517a-210">Selezionare database hello hello elenco.</span><span class="sxs-lookup"><span data-stu-id="6517a-210">Select hello database from hello list.</span></span> <span data-ttu-id="6517a-211">In hello **direzioni di sincronizzazione** campo, selezionare la sincronizzazione bidirezionale, toohello Hub, o da hello Hub.</span><span class="sxs-lookup"><span data-stu-id="6517a-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Selezionare hello nel database locale](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="6517a-213">Selezionare **OK** tooclose hello **seleziona Database** blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="6517a-214">Selezionare quindi **OK** tooclose hello **configurare On-Premise** blade e attendere hello sincronizzazione nuovo membro toobe creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="6517a-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="6517a-215">Infine, fare clic su **OK** tooclose hello **selezionare i membri di sincronizzazione** blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![Nel database locale aggiunto toosync gruppo](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="6517a-217">tooconnect tooSQL sincronizzazione dati e l'agente locale hello, aggiungere il ruolo di utente nome toohello `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="6517a-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="6517a-218">Sincronizzazione dati crea questo ruolo nell'istanza di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="6517a-219">Passaggio 3 - Configurare il gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="6517a-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="6517a-220">Dopo avere creati e distribuiti, il passaggio 3, nuovi membri del gruppo sincronizzazione hello **Configura gruppo di sincronizzazione**, viene evidenziato in hello **nuovo gruppo di sincronizzazione** blade.</span><span class="sxs-lookup"><span data-stu-id="6517a-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="6517a-221">In hello **tabelle** pannello Seleziona un database dall'elenco di hello della sincronizzazione i membri del gruppo e quindi selezionare **aggiornare lo schema**.</span><span class="sxs-lookup"><span data-stu-id="6517a-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="6517a-222">Dall'elenco di hello delle tabelle disponibili, selezionare le tabelle di hello che si desidera toosync.</span><span class="sxs-lookup"><span data-stu-id="6517a-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Selezionare le tabelle toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="6517a-224">Per impostazione predefinita, vengono selezionate tutte le colonne nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="6517a-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="6517a-225">Se non si desidera toosync tutte le colonne di hello, disabilitare la casella di controllo di hello per le colonne di hello che non si desidera toosync.</span><span class="sxs-lookup"><span data-stu-id="6517a-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="6517a-226">Assicurarsi di colonna di chiave primaria hello tooleave selezionato.</span><span class="sxs-lookup"><span data-stu-id="6517a-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Selezionare i campi toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="6517a-228">Infine, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="6517a-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6517a-229">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6517a-229">Next steps</span></span>
<span data-ttu-id="6517a-230">A questo punto</span><span class="sxs-lookup"><span data-stu-id="6517a-230">Congratulations.</span></span> <span data-ttu-id="6517a-231">è stato creato un gruppo di sincronizzazione che include sia un'istanza di database SQL che un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="6517a-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="6517a-232">Per altre informazioni sul database SQL e la sincronizzazione dati SQL, vedere:</span><span class="sxs-lookup"><span data-stu-id="6517a-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="6517a-233">Scaricare la documentazione tecnica sincronizzazione dati SQL completezza hello</span><span class="sxs-lookup"><span data-stu-id="6517a-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="6517a-234">Scaricare la documentazione delle API REST di sincronizzazione dati SQL hello</span><span class="sxs-lookup"><span data-stu-id="6517a-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="6517a-235">Panoramica del database SQL</span><span class="sxs-lookup"><span data-stu-id="6517a-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="6517a-236">Gestione del ciclo di vita del database</span><span class="sxs-lookup"><span data-stu-id="6517a-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
