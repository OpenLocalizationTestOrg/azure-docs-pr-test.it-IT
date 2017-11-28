---
title: aaaRestore una singola tabella da un backup di Database SQL di Azure | Documenti Microsoft
description: Informazioni su come toorestore una singola tabella da un backup di Database SQL di Azure.
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="dc171-103">Come toorestore una singola tabella da un backup di Database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="dc171-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="dc171-104">Può verificarsi una situazione in cui è stato accidentalmente modificati alcuni dati in un database SQL e si desidera ora toorecover hello singola interessati tabella.</span><span class="sxs-lookup"><span data-stu-id="dc171-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="dc171-105">In questo articolo viene descritto come toorestore una singola tabella in un database da uno dei Database SQL di hello [backup automatici](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="dc171-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="dc171-106">Passaggi di preparazione: rinominare la tabella hello e ripristinare una copia del database hello</span><span class="sxs-lookup"><span data-stu-id="dc171-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="dc171-107">Identificare hello tabella nel database SQL di Azure che si desidera tooreplace con copia hello ripristinato.</span><span class="sxs-lookup"><span data-stu-id="dc171-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="dc171-108">Utilizzare tabella hello toorename di Microsoft SQL Management Studio.</span><span class="sxs-lookup"><span data-stu-id="dc171-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="dc171-109">Ad esempio, rinominare la tabella hello come &lt;nome tabella&gt;old.</span><span class="sxs-lookup"><span data-stu-id="dc171-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc171-110">tooavoid bloccate, assicurarsi che non è presente alcuna attività in esecuzione in una tabella di hello che si sta rinominando.</span><span class="sxs-lookup"><span data-stu-id="dc171-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="dc171-111">In caso di problemi, accertarsi di eseguire questa procedura durante una finestra di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="dc171-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="dc171-112">Ripristinare un backup del punto di tooa database nel tempo che si desidera hello toousing toorecover [In_Timeconpunto di ripristino](sql-database-recovery-using-backups.md#point-in-time-restore) passaggi.</span><span class="sxs-lookup"><span data-stu-id="dc171-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc171-113">nome Hello del database ripristinato hello sarà nel formato DBName + TimeStamp hello. ad esempio, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="dc171-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="dc171-114">Questo passaggio non sovrascriverà nome del database nel server di hello esistente hello.</span><span class="sxs-lookup"><span data-stu-id="dc171-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="dc171-115">Si tratta di una misura di sicurezza e ha lo scopo tooallow tooverify hello database ripristinato prima di eliminare il database corrente e rinominare il database ripristinato hello per la produzione.</span><span class="sxs-lookup"><span data-stu-id="dc171-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="dc171-116">Copia della tabella hello da hello database ripristinato usando lo strumento di migrazione del Database SQL di hello</span><span class="sxs-lookup"><span data-stu-id="dc171-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="dc171-117">Scaricare e installare hello [migrazione guidata Database SQL](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="dc171-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="dc171-118">Aprire hello migrazione guidata Database SQL, in hello **Select Process** selezionare **Database di analisi/migrazione**e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dc171-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database Migration wizard - Select Process](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="dc171-120">In hello **connettersi tooServer** finestra di dialogo casella, applicare hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="dc171-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="dc171-121">Server name (Nome server): **server SQL**</span><span class="sxs-lookup"><span data-stu-id="dc171-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="dc171-122">Authentication: (Autenticazione): **autenticazione di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="dc171-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="dc171-123">Login (Account di accesso): **account di accesso**</span><span class="sxs-lookup"><span data-stu-id="dc171-123">Login: **Your login**</span></span>
   * <span data-ttu-id="dc171-124">Password: **password**</span><span class="sxs-lookup"><span data-stu-id="dc171-124">Password: **Your password**</span></span>
   * <span data-ttu-id="dc171-125">Database: **Master DB (List all databases)** (Database master - Elenca tutti i database)</span><span class="sxs-lookup"><span data-stu-id="dc171-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="dc171-126">Per impostazione predefinita la procedura guidata hello Salva le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="dc171-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="dc171-127">Per modificare tale impostazione, selezionare **Forget Login Information**(Ignora informazioni di accesso).</span><span class="sxs-lookup"><span data-stu-id="dc171-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database Migration wizard - Select Source - step 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="dc171-129">In hello **Seleziona origine** la finestra di dialogo, il nome del database selezionare hello ripristinato da hello **preparativi** sezione come origine e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dc171-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database Migration wizard - Select Source - step 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="dc171-131">In hello **Seleziona oggetti** la finestra di dialogo, seleziona hello **selezionare oggetti di database specifici** opzione e quindi selezionare table(or tables) hello che si desidera toomigrate toohello server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="dc171-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="dc171-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="dc171-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="dc171-133">In hello **riepilogo generazione guidata Script** pagina, fare clic su **Sì** quando verrà richiesto se si è pronti toogenerate uno script SQL.</span><span class="sxs-lookup"><span data-stu-id="dc171-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="dc171-134">È inoltre possibile hello toosave hello opzione Script TSQL per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="dc171-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="dc171-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="dc171-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="dc171-136">In hello **riepilogo dei risultati** pagina, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dc171-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="dc171-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="dc171-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="dc171-138">In hello **connessione al Server di destinazione installazione** pagina, fare clic su **connettersi tooServer**, quindi immettere i dettagli di hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="dc171-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="dc171-139">**Server Name**(Nome server): istanza del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="dc171-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="dc171-140">**Autenticazione**: **autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="dc171-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="dc171-141">Immettere le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="dc171-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="dc171-142">**Database**: **Master DB (List all databases)** (Database master (Elenca tutti i database)).</span><span class="sxs-lookup"><span data-stu-id="dc171-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="dc171-143">Questa opzione vengono elencati tutti i database nel server di destinazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="dc171-143">This option lists all hello databases on hello target server.</span></span>
     
     ![SQL Database Migration wizard - Setup Target Server Connection](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="dc171-145">Fare clic su **Connetti**, selezionare i database di destinazione hello che si desidera toomove hello tabella e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="dc171-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="dc171-146">Questo dovrebbe terminare l'esecuzione dello script generato in precedenza hello e dovrebbe essere hello appena spostato i database della tabella di destinazione toohello copiato.</span><span class="sxs-lookup"><span data-stu-id="dc171-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="dc171-147">Passaggio di verifica</span><span class="sxs-lookup"><span data-stu-id="dc171-147">Verification step</span></span>

- <span data-ttu-id="dc171-148">Eseguire una query e test toomake tabella hello appena copiato che dati hello sia intatti.</span><span class="sxs-lookup"><span data-stu-id="dc171-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="dc171-149">Dopo la conferma, è possibile eliminare il formato di tabella hello rinominato **preparativi** sezione.</span><span class="sxs-lookup"><span data-stu-id="dc171-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="dc171-150">Ad esempio, &lt;nome tabella&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="dc171-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc171-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc171-151">Next steps</span></span>
[<span data-ttu-id="dc171-152">Backup automatici del database SQL</span><span class="sxs-lookup"><span data-stu-id="dc171-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

