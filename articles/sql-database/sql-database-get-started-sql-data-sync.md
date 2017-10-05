---
title: Introduzione all'anteprima di sincronizzazione dati SQL di Azure | Documentazione Microsoft
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
ms.openlocfilehash: 2d0f9d7f32ad79f49d58165d734b9df4af862835
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="246dd-103">Introduzione all'anteprima di sincronizzazione dati di SQL Azure</span><span class="sxs-lookup"><span data-stu-id="246dd-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="246dd-104">In questa esercitazione si imparerà a configurare sincronizzazione dati SQL di Azure creando un gruppo di sincronizzazione ibrido che contiene sia istanze del database SQL di Azure che istanze di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-104">In this tutorial, you learn how to set up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="246dd-105">Il nuovo gruppo di sincronizzazione ha una configurazione completa ed esegue la sincronizzazione in base alla pianificazione impostata.</span><span class="sxs-lookup"><span data-stu-id="246dd-105">The new sync group is fully configured and synchronizes on the schedule you set.</span></span>

<span data-ttu-id="246dd-106">Per questa esercitazione è necessario avere già un certo livello di esperienza precedente con il database SQL di Azure e SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="246dd-107">Per una panoramica di sincronizzazione dati SQL, vedere [Sincronizzare i dati](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="246dd-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="246dd-108">Per esempi di PowerShell completi che illustrano come configurare la sincronizzazione dati SQL, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="246dd-108">For complete PowerShell examples that show how to configure SQL Data Sync, see the following articles:</span></span>
-   [<span data-ttu-id="246dd-109">Usare PowerShell per sincronizzare più database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="246dd-109">Use PowerShell to sync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="246dd-110">Usare PowerShell per la sincronizzazione tra un database SQL di Azure e un database locale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="246dd-110">Use PowerShell to sync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="246dd-111">La documentazione tecnica completa impostata per la sincronizzazione dati SQL di Azure, che si trovava in precedenza su MSDN, è ora disponibile in formato PDF.</span><span class="sxs-lookup"><span data-stu-id="246dd-111">The complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="246dd-112">Scaricarla [qui](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="246dd-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="246dd-113">Passaggio 1 - Creare un gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="246dd-113">Step 1 - Create sync group</span></span>

### <a name="locate-the-data-sync-settings"></a><span data-ttu-id="246dd-114">Individuare le impostazioni di sincronizzazione dati</span><span class="sxs-lookup"><span data-stu-id="246dd-114">Locate the Data Sync settings</span></span>

1.  <span data-ttu-id="246dd-115">Nel browser passare al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="246dd-115">In your browser, navigate to the Azure portal.</span></span>

2.  <span data-ttu-id="246dd-116">Nel portale individuare i database SQL dal dashboard o dall'icona Database SQL sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="246dd-116">In the portal, locate your SQL databases from your Dashboard or from the SQL Databases icon on the toolbar.</span></span>

    ![Elenco dei database SQL di Azure](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="246dd-118">Nel pannello **Database SQL** selezionare il database SQL esistente da usare come database hub per la sincronizzazione dati. Verrà aperto il pannello del database SQL.</span><span class="sxs-lookup"><span data-stu-id="246dd-118">On the **SQL databases** blade, select the existing SQL database that you want to use as the hub database for Data Sync. The SQL database blade opens.</span></span>

4.  <span data-ttu-id="246dd-119">Nel pannello del database SQL per il database selezionato selezionare **Sincronizza con altri database**.</span><span class="sxs-lookup"><span data-stu-id="246dd-119">On the SQL database blade for the selected database, select **Sync to other databases**.</span></span> <span data-ttu-id="246dd-120">Verrà aperto il pannello di sincronizzazione dati.</span><span class="sxs-lookup"><span data-stu-id="246dd-120">The Data Sync blade opens.</span></span>

    ![Opzione Sincronizza con altri database](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="246dd-122">Creare un nuovo gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="246dd-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="246dd-123">Nel pannello di sincronizzazione dati selezionare **Nuovo gruppo di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-123">On the Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="246dd-124">Verrà aperto il pannello **Nuovo gruppo di sincronizzazione** con evidenziato il passaggio 1 **Crea gruppo di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-124">The **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="246dd-125">Verrà aperto anche il pannello **Crea gruppo di sincronizzazione dati**.</span><span class="sxs-lookup"><span data-stu-id="246dd-125">The **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="246dd-126">Nel pannello **Crea gruppo di sincronizzazione dati** eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="246dd-126">On the **Create Data Sync Group** blade, do the following things:</span></span>

    1.  <span data-ttu-id="246dd-127">Nel campo **Nome gruppo di sincronizzazione** immettere un nome per il nuovo gruppo di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="246dd-127">In the **Sync Group Name** field, enter a name for the new sync group.</span></span>

    2.  <span data-ttu-id="246dd-128">Nella sezione **Database dei metadati di sincronizzazione** scegliere se creare un nuovo database (scelta consigliata) o usare un database esistente.</span><span class="sxs-lookup"><span data-stu-id="246dd-128">In the **Sync Metadata Database** section, choose whether to create a new database (recommended) or to use an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="246dd-129">Microsoft consiglia di creare un nuovo database vuoto da usare come database dei metadati di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="246dd-129">Microsoft recommends that you create a new, empty database to use as the Sync Metadata Database.</span></span> <span data-ttu-id="246dd-130">La sincronizzazione dati crea tabelle in questo database ed esegue un carico di lavoro frequente.</span><span class="sxs-lookup"><span data-stu-id="246dd-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="246dd-131">Questo database viene automaticamente condiviso come database dei metadati di sincronizzazione per tutti i gruppi di sincronizzazione nell'area selezionata.</span><span class="sxs-lookup"><span data-stu-id="246dd-131">This database is automatically shared as the Sync Metadata Database for all of your Sync groups in the selected region.</span></span> <span data-ttu-id="246dd-132">È possibile modificare il database dei metadati di sincronizzazione, il relativo nome o il relativo livello di servizio senza eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="246dd-132">You can't change the Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="246dd-133">Se si sceglie **Nuovo database** selezionare **Crea nuovo database**.</span><span class="sxs-lookup"><span data-stu-id="246dd-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="246dd-134">Verrà aperto il pannello **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="246dd-134">The **SQL Database** blade opens.</span></span> <span data-ttu-id="246dd-135">Nel pannello **Database SQL** specificare un nome per il nuovo database e configurarlo.</span><span class="sxs-lookup"><span data-stu-id="246dd-135">On the **SQL Database** blade, name and configure the new database.</span></span> <span data-ttu-id="246dd-136">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="246dd-136">Then select **OK**.</span></span>

        <span data-ttu-id="246dd-137">Se si sceglie **Utilizza database esistente**, selezionare il database nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="246dd-137">If you chose **Use existing database**, select the database from the list.</span></span>

    3.  <span data-ttu-id="246dd-138">Nella sezione **Sincronizzazione automatica** selezionare innanzitutto **Sì** o **No**.</span><span class="sxs-lookup"><span data-stu-id="246dd-138">In the **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="246dd-139">Se si sceglie **Sì**, nella sezione **Frequenza sincronizzazione** immettere un numero e selezionare Secondi, Minuti, Ore o Giorni.</span><span class="sxs-lookup"><span data-stu-id="246dd-139">If you chose **On**, in the **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Specificare la frequenza di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="246dd-141">Nella sezione **Risoluzione dei conflitti** selezionare "Priorità hub" o "Priorità client".</span><span class="sxs-lookup"><span data-stu-id="246dd-141">In the **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Specificare come vengono risolti i conflitti](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="246dd-143">Selezionare **OK** e attendere che il nuovo gruppo di sincronizzazione venga creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="246dd-143">Select **OK** and wait for the new sync group to be created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="246dd-144">Passaggio 2 - Aggiungere i membri di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="246dd-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="246dd-145">Al termine della creazione e distribuzione del nuovo gruppo di sincronizzazione, nel pannello **Nuovo gruppo di sincronizzazione** viene evidenziato il passaggio 2 **Aggiungi membri di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-145">After the new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in the **New sync group** blade.</span></span>

<span data-ttu-id="246dd-146">Nella sezione **Database hub** immettere le credenziali esistenti per il server di database SQL in cui si trova il database hub.</span><span class="sxs-lookup"><span data-stu-id="246dd-146">In the **Hub Database** section, enter the existing credentials for the SQL Database server on which the hub database is located.</span></span> <span data-ttu-id="246dd-147">Non immettere *nuove* credenziali in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="246dd-147">Don't enter *new* credentials in this section.</span></span>

![Database hub aggiunto al gruppo di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="246dd-149">Aggiungere un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="246dd-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="246dd-150">Nella sezione **Database membro** aggiungere facoltativamente un database SQL di Azure al gruppo di sincronizzazione selezionando **Aggiungi un database di Azure**.</span><span class="sxs-lookup"><span data-stu-id="246dd-150">In the **Member Database** section, optionally add an Azure SQL Database to the sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="246dd-151">Verrà aperto il pannello **Configura database di Azure**.</span><span class="sxs-lookup"><span data-stu-id="246dd-151">The **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="246dd-152">Nel pannello **Configura database di Azure** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="246dd-152">On the **Configure Azure Database** blade, do the following things:</span></span>

1.  <span data-ttu-id="246dd-153">Nel campo **Nome membro di sincronizzazione** specificare un nome per il nuovo membro di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="246dd-153">In the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="246dd-154">Questo nome è distinto dal nome del database stesso.</span><span class="sxs-lookup"><span data-stu-id="246dd-154">This name is distinct from the name of the database itself.</span></span>

2.  <span data-ttu-id="246dd-155">Nel campo **Sottoscrizione** selezionare la sottoscrizione di Azure associata per la fatturazione.</span><span class="sxs-lookup"><span data-stu-id="246dd-155">In the **Subscription** field, select the associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="246dd-156">Nel campo **Server di Azure SQL** selezionare il server di database SQL esistente.</span><span class="sxs-lookup"><span data-stu-id="246dd-156">In the **Azure SQL Server** field, select the existing SQL database server.</span></span>

4.  <span data-ttu-id="246dd-157">Nel campo **Database SQL di Azure** selezionare il database SQL esistente.</span><span class="sxs-lookup"><span data-stu-id="246dd-157">In the **Azure SQL Database** field, select the existing SQL database.</span></span>

5.  <span data-ttu-id="246dd-158">Nel campo **Direzioni sincronizzazione** selezionare Sincronizzazione bidirezionale, Verso l'hub e Dall'hub.</span><span class="sxs-lookup"><span data-stu-id="246dd-158">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

    ![Aggiungere un nuovo membro di sincronizzazione del database SQL](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="246dd-160">Nei campi **Nome utente** e **Password** immettere le credenziali esistenti per il server di database SQL in cui si trova il database membro.</span><span class="sxs-lookup"><span data-stu-id="246dd-160">In the **Username** and **Password** fields, enter the existing credentials for the SQL Database server on which the member database is located.</span></span> <span data-ttu-id="246dd-161">Non immettere *nuove* credenziali in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="246dd-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="246dd-162">Selezionare **OK** e attendere che il nuovo membro di sincronizzazione venga creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="246dd-162">Select **OK** and wait for the new sync member to be created and deployed.</span></span>

    ![Il nuovo membro di sincronizzazione del database SQL è stato aggiunto](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="246dd-164">Aggiungere un database di SQL Server locale</span><span class="sxs-lookup"><span data-stu-id="246dd-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="246dd-165">Nella sezione **Database membro** aggiungere facoltativamente un'istanza di SQL Server locale al gruppo di sincronizzazione selezionando **Aggiungi un database locale**.</span><span class="sxs-lookup"><span data-stu-id="246dd-165">In the **Member Database** section, optionally add an on-premises SQL Server to the sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="246dd-166">Verrà aperto il pannello **Configurare database locale**.</span><span class="sxs-lookup"><span data-stu-id="246dd-166">The **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="246dd-167">Nel pannello **Configura database locale** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="246dd-167">On the **Configure On-Premises** blade, do the following things:</span></span>

1.  <span data-ttu-id="246dd-168">Selezionare **Scegliere il gateway dell'agente di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-168">Select **Choose the Sync Agent Gateway**.</span></span> <span data-ttu-id="246dd-169">Verrà aperto il pannello **Seleziona agente di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-169">The **Select Sync Agent** blade opens.</span></span>

    ![Scegliere il gateway dell'agente di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="246dd-171">Nel pannello **Scegliere il gateway dell'agente di sincronizzazione** specificare se si vuole usare un agente esistente o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="246dd-171">On the **Choose the Sync Agent Gateway** blade, choose whether to use an existing agent or create a new agent.</span></span>

    <span data-ttu-id="246dd-172">Se si sceglie **Agenti esistenti**, selezionare l'agente esistente nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="246dd-172">If you chose **Existing agents**, select the existing agent from the list.</span></span>

    <span data-ttu-id="246dd-173">Se si sceglie **Consente di creare un nuovo agente**, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="246dd-173">If you chose **Create a new agent**, do the following things:</span></span>

    1.  <span data-ttu-id="246dd-174">Scaricare il software dell'agente di sincronizzazione client dal collegamento specificato e installarlo nel computer in cui si trova SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-174">Download the client sync agent software from the link provided and install it on the computer where the SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="246dd-175">È necessario aprire la porta TCP 1433 in uscita nel firewall per consentire all'agente client di comunicare con il server.</span><span class="sxs-lookup"><span data-stu-id="246dd-175">You have to open outbound TCP port 1433 in the firewall to let the client agent communicate with the server.</span></span>


    2.  <span data-ttu-id="246dd-176">Immettere un nome per l'agente.</span><span class="sxs-lookup"><span data-stu-id="246dd-176">Enter a name for the agent.</span></span>

    3.  <span data-ttu-id="246dd-177">Selezionare **Crea e genera chiave**.</span><span class="sxs-lookup"><span data-stu-id="246dd-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="246dd-178">Copiare la chiave dell'agente negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="246dd-178">Copy the agent key to the clipboard.</span></span>
        
        ![Creazione di un nuovo agente di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="246dd-180">Selezionare **OK** per chiudere il pannello **Seleziona agente di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-180">Select **OK** to close the **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="246dd-181">Nel computer SQL Server individuare ed eseguire l'app dell'agente di sincronizzazione client.</span><span class="sxs-lookup"><span data-stu-id="246dd-181">On the SQL Server computer, locate and run the Client Sync Agent app.</span></span>

        ![App dell'agente client di sincronizzazione dati](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="246dd-183">Nell'app dell'agente di sincronizzazione selezionare **Submit Agent Key** (Invia chiave agente).</span><span class="sxs-lookup"><span data-stu-id="246dd-183">In the sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="246dd-184">Verrà aperta la finestra di dialogo **Sync Metadata Database Configuration** (Configurazione del database dei metadati di sincronizzazione).</span><span class="sxs-lookup"><span data-stu-id="246dd-184">The **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="246dd-185">Nella finestra di dialogo **Sync Metadata Database Configuration** (Configurazione del database dei metadati di sincronizzazione) incollare la chiave dell'agente copiata dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="246dd-185">In the **Sync Metadata Database Configuration** dialog box, paste in the agent key copied from the Azure portal.</span></span> <span data-ttu-id="246dd-186">Specificare anche le credenziali esistenti per il server di database SQL di Azure in cui si trova il database dei metadati.</span><span class="sxs-lookup"><span data-stu-id="246dd-186">Also provide the existing credentials for the Azure SQL Database server on which the metadata database is located.</span></span> <span data-ttu-id="246dd-187">(Se è stato creato un nuovo database dei metadati, il database si trova nello stesso server del database hub.) Selezionare **OK** e attendere che la configurazione venga completata.</span><span class="sxs-lookup"><span data-stu-id="246dd-187">(If you created a new metadata database, this database is on the same server as the hub database.) Select **OK** and wait for the configuration to finish.</span></span>

        ![Immettere la chiave dell'agente e le credenziali del server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="246dd-189">Se viene visualizzato un errore del firewall a questo punto, è necessario creare una regola del firewall in Azure per consentire il traffico in ingresso dal computer SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-189">If you get a firewall error at this point, you have to create a firewall rule on Azure to allow incoming traffic from the SQL Server computer.</span></span> <span data-ttu-id="246dd-190">È possibile creare manualmente la regola nel portale, ma può risultare più semplice crearla in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="246dd-190">You can create the rule manually in the portal, but you may find it easier to create it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="246dd-191">In SSMS provare a connettersi al database hub in Azure.</span><span class="sxs-lookup"><span data-stu-id="246dd-191">In SSMS, try to connect to the hub database on Azure.</span></span> <span data-ttu-id="246dd-192">Immettere il nome nel formato \<nome_database_hub\>.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="246dd-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="246dd-193">Seguire i passaggi nella finestra di dialogo per configurare la regola del firewall di Azure.</span><span class="sxs-lookup"><span data-stu-id="246dd-193">Follow the steps in the dialog box to configure the Azure firewall rule.</span></span> <span data-ttu-id="246dd-194">Tornare quindi all'app dell'agente di sincronizzazione client.</span><span class="sxs-lookup"><span data-stu-id="246dd-194">Then return to the Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="246dd-195">Nell'app dell'agente di sincronizzazione client fare clic su **Registra** per registrare un database di SQL Server con l'agente.</span><span class="sxs-lookup"><span data-stu-id="246dd-195">In the Client Sync Agent app, click **Register** to register a SQL Server database with the agent.</span></span> <span data-ttu-id="246dd-196">Verrà aperta la finestra di dialogo **Configurazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="246dd-196">The **SQL Server Configuration** dialog box opens.</span></span>

        ![Aggiungere e configurare un database di SQL Server](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="246dd-198">Nella finestra di dialogo **Configurazione di SQL Server** scegliere se effettuare la connessione mediante l'autenticazione di SQL Server o l'autenticazione di Windows.</span><span class="sxs-lookup"><span data-stu-id="246dd-198">In the **SQL Server Configuration** dialog box, choose whether to connect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="246dd-199">Se si sceglie l'autenticazione di SQL Server, immettere le credenziali esistenti.</span><span class="sxs-lookup"><span data-stu-id="246dd-199">If you chose SQL Server authentication, enter the existing credentials.</span></span> <span data-ttu-id="246dd-200">Specificare il nome dell'istanza di SQL Server e il nome del database che si vuole sincronizzare. Fare clic su **Test connessione** per testare le impostazioni.</span><span class="sxs-lookup"><span data-stu-id="246dd-200">Provide the SQL Server name and the name of the database that you want to sync. Select **Test connection** to test your settings.</span></span> <span data-ttu-id="246dd-201">Selezionare quindi **Salva**.</span><span class="sxs-lookup"><span data-stu-id="246dd-201">Then select **Save**.</span></span> <span data-ttu-id="246dd-202">Il database registrato verrà visualizzato nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="246dd-202">The registered database appears in the list.</span></span>

        ![Il database di SQL Server è ora registrato](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="246dd-204">È ora possibile chiudere l'app dell'agente di sincronizzazione client.</span><span class="sxs-lookup"><span data-stu-id="246dd-204">You can now close the Client Sync Agent app.</span></span>

    12. <span data-ttu-id="246dd-205">Nel pannello **Configura database locale** del portale selezionare **Selezionare il database**.</span><span class="sxs-lookup"><span data-stu-id="246dd-205">In the portal, on the **Configure On-Premises** blade, select **Select the Database.**</span></span> <span data-ttu-id="246dd-206">Verrà aperto il pannello **Seleziona database**.</span><span class="sxs-lookup"><span data-stu-id="246dd-206">The **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="246dd-207">Nel pannello **Seleziona database**, nel campo **Nome membro di sincronizzazione**, specificare un nome per il nuovo membro di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="246dd-207">On the **Select Database** blade, in the **Sync Member Name** field, provide a name for the new sync member.</span></span> <span data-ttu-id="246dd-208">Questo nome è distinto dal nome del database stesso.</span><span class="sxs-lookup"><span data-stu-id="246dd-208">This name is distinct from the name of the database itself.</span></span> <span data-ttu-id="246dd-209">Selezionare il database nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="246dd-209">Select the database from the list.</span></span> <span data-ttu-id="246dd-210">Nel campo **Direzioni sincronizzazione** selezionare Sincronizzazione bidirezionale, Verso l'hub e Dall'hub.</span><span class="sxs-lookup"><span data-stu-id="246dd-210">In the **Sync Directions** field, select Bi-directional Sync, To the Hub, or From the Hub.</span></span>

        ![Selezionare il database locale](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="246dd-212">Selezionare **OK** per chiudere il pannello **Seleziona database**.</span><span class="sxs-lookup"><span data-stu-id="246dd-212">Select **OK** to close the **Select Database** blade.</span></span> <span data-ttu-id="246dd-213">Selezionare quindi **OK** per chiudere il pannello **Configura database locale** e attendere che il nuovo membro di sincronizzazione venga creato e distribuito.</span><span class="sxs-lookup"><span data-stu-id="246dd-213">Then select **OK** to close the **Configure On-Premises** blade and wait for the new sync member to be created and deployed.</span></span> <span data-ttu-id="246dd-214">Fare infine clic su **OK** per chiudere il pannello **Selezionare i membri di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-214">Finally, click **OK** to close the **Select sync members** blade.</span></span>

        ![Database locale aggiunto al gruppo di sincronizzazione](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="246dd-216">Per connettersi a sincronizzazione dati SQL e all'agente locale, aggiungere il proprio nome utente al ruolo `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="246dd-216">To connect to SQL Data Sync and the local agent, add your user name to the role `DataSync_Executor`.</span></span> <span data-ttu-id="246dd-217">Sincronizzazione dati crea questo ruolo nell'istanza di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-217">Data Sync creates this role on the SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="246dd-218">Passaggio 3 - Configurare il gruppo di sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="246dd-218">Step 3 - Configure sync group</span></span>

<span data-ttu-id="246dd-219">Dopo avere creato e distribuito i nuovi membri del gruppo di sincronizzazione, nel pannello **Nuovo gruppo di sincronizzazione** viene evidenziato il passaggio 3 **Configura gruppo di sincronizzazione**.</span><span class="sxs-lookup"><span data-stu-id="246dd-219">After the new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in the **New sync group** blade.</span></span>

1.  <span data-ttu-id="246dd-220">Nel pannello **Tabelle** selezionare un database nell'elenco dei membri del gruppo di sincronizzazione e quindi selezionare **Aggiorna schema**.</span><span class="sxs-lookup"><span data-stu-id="246dd-220">On the **Tables** blade, select a database from the list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="246dd-221">Nell'elenco delle tabelle disponibili selezionare le tabelle che si vuole sincronizzare.</span><span class="sxs-lookup"><span data-stu-id="246dd-221">From the list of available tables, select the tables that you want to sync.</span></span>

    ![Selezionare le tabelle da sincronizzare](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="246dd-223">Per impostazione predefinita vengono selezionate tutte le colonne nella tabella.</span><span class="sxs-lookup"><span data-stu-id="246dd-223">By default, all columns in the table are selected.</span></span> <span data-ttu-id="246dd-224">Se non si vogliono sincronizzare tutte le colonne, disabilitare la casella di controllo per le colonne che non si vuole sincronizzare. Assicurarsi di lasciare selezionata la colonna chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="246dd-224">If you don't want to sync all the columns, disable the checkbox for the columns that you don't want to sync. Be sure to leave the primary key column selected.</span></span>

    ![Selezionare i campi da sincronizzare](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="246dd-226">Infine, selezionare **Salva**.</span><span class="sxs-lookup"><span data-stu-id="246dd-226">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="246dd-227">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="246dd-227">Next steps</span></span>
<span data-ttu-id="246dd-228">A questo punto</span><span class="sxs-lookup"><span data-stu-id="246dd-228">Congratulations.</span></span> <span data-ttu-id="246dd-229">è stato creato un gruppo di sincronizzazione che include sia un'istanza di database SQL che un database di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="246dd-229">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="246dd-230">Per altre informazioni sul database SQL e la sincronizzazione dati SQL, vedere:</span><span class="sxs-lookup"><span data-stu-id="246dd-230">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="246dd-231">Scaricare la documentazione tecnica completa di sincronizzazione dati SQL</span><span class="sxs-lookup"><span data-stu-id="246dd-231">Download the complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="246dd-232">Scaricare la documentazione dell'API REST di sincronizzazione dati SQL</span><span class="sxs-lookup"><span data-stu-id="246dd-232">Download the SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="246dd-233">Panoramica del database SQL</span><span class="sxs-lookup"><span data-stu-id="246dd-233">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="246dd-234">Gestione del ciclo di vita del database</span><span class="sxs-lookup"><span data-stu-id="246dd-234">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
