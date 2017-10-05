---
title: Ripristinare una singola tabella dal backup del database SQL di Azure | Documentazione Microsoft
description: Learn how to restore a single table from Azure SQL Database backup.
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
ms.openlocfilehash: 8c750c503d10ea63b9665958b96db2dfea3d9a3c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="43b6e-103">Come ripristinare una singola tabella nel backup del database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="43b6e-103">How to restore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="43b6e-104">Potrebbe verificarsi una situazione in cui alcuni dati sono stati modificati accidentalmente in un database SQL e ora si desidera ripristinare la singola tabella interessata.</span><span class="sxs-lookup"><span data-stu-id="43b6e-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table.</span></span> <span data-ttu-id="43b6e-105">Questo articolo descrive come ripristinare una singola tabella in un database da uno dei [backup automatici](sql-database-automated-backups.md)del database SQL.</span><span class="sxs-lookup"><span data-stu-id="43b6e-105">This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a><span data-ttu-id="43b6e-106">Passaggi preliminari: rinominare la tabella e ripristinare una copia del database</span><span class="sxs-lookup"><span data-stu-id="43b6e-106">Preparation steps: Rename the table and restore a copy of the database</span></span>
1. <span data-ttu-id="43b6e-107">Identificare la tabella nel database SQL di Azure che si desidera sostituire con la copia ripristinata.</span><span class="sxs-lookup"><span data-stu-id="43b6e-107">Identify the table in your Azure SQL database that you want to replace with the restored copy.</span></span> <span data-ttu-id="43b6e-108">Utilizzare Microsoft SQL Management Studio per rinominare la tabella.</span><span class="sxs-lookup"><span data-stu-id="43b6e-108">Use Microsoft SQL Management Studio to rename the table.</span></span> <span data-ttu-id="43b6e-109">Ad esempio, rinominare la tabella &lt;nometabella&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="43b6e-109">For example, rename the table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43b6e-110">Per evitare il blocco, assicurarsi che non vi sia alcuna attività in esecuzione nella tabella che si sta rinominando.</span><span class="sxs-lookup"><span data-stu-id="43b6e-110">To avoid being blocked, make sure that there's no activity running on the table that you are renaming.</span></span> <span data-ttu-id="43b6e-111">In caso di problemi, accertarsi di eseguire questa procedura durante una finestra di manutenzione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="43b6e-112">Ripristinare un backup del database al momento specifico desiderato usando i passaggi di [Ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore).</span><span class="sxs-lookup"><span data-stu-id="43b6e-112">Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43b6e-113">Il nome del database ripristinato sarà nel formato NomeDB+Timestamp. Ad esempio, **Adventureworks2012_2016-01-01T22-12Z**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-113">The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="43b6e-114">Questo passaggio non sovrascrive il nome del database esistente nel server.</span><span class="sxs-lookup"><span data-stu-id="43b6e-114">This step doesn't overwrite the existing database name on the server.</span></span> <span data-ttu-id="43b6e-115">Si tratta di una misura di sicurezza che consente all'utente di verificare il database ripristinato prima di eliminare il database corrente e rinominare il database ripristinato per l'uso in produzione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-115">This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.</span></span>
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a><span data-ttu-id="43b6e-116">Copia della tabella dal database ripristinato tramite lo strumento di migrazione del database SQL</span><span class="sxs-lookup"><span data-stu-id="43b6e-116">Copying the table from the restored database by using the SQL Database Migration tool</span></span>

1. <span data-ttu-id="43b6e-117">Scaricare e installare la [Migrazione guidata database SQL di Microsoft Azure](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="43b6e-117">Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="43b6e-118">Aprire la Migrazione guidata database SQL. Nella pagina **Seleziona processo** selezionare **Database in Analyze/Migrate** (Database in corso di analisi/migrazione) e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-118">Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![SQL Database Migration wizard - Select Process](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="43b6e-120">Nella finestra di dialogo **Connect to Server** (Connetti al server) immettere i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="43b6e-120">In the **Connect to Server** dialog box, apply the following settings:</span></span>

   * <span data-ttu-id="43b6e-121">Server name (Nome server): **server SQL**</span><span class="sxs-lookup"><span data-stu-id="43b6e-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="43b6e-122">Authentication: (Autenticazione): **autenticazione di SQL Server**</span><span class="sxs-lookup"><span data-stu-id="43b6e-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="43b6e-123">Login (Account di accesso): **account di accesso**</span><span class="sxs-lookup"><span data-stu-id="43b6e-123">Login: **Your login**</span></span>
   * <span data-ttu-id="43b6e-124">Password: **password**</span><span class="sxs-lookup"><span data-stu-id="43b6e-124">Password: **Your password**</span></span>
   * <span data-ttu-id="43b6e-125">Database: **Master DB (List all databases)** (Database master - Elenca tutti i database)</span><span class="sxs-lookup"><span data-stu-id="43b6e-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43b6e-126">Per impostazione predefinita, la procedura guidata salva le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="43b6e-126">By default the wizard saves your login information.</span></span> <span data-ttu-id="43b6e-127">Per modificare tale impostazione, selezionare **Forget Login Information**(Ignora informazioni di accesso).</span><span class="sxs-lookup"><span data-stu-id="43b6e-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![SQL Database Migration wizard - Select Source - step 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="43b6e-129">Nella finestra di dialogo **Seleziona origine** selezionare il nome del database ripristinato nella sezione **Preparation steps** (Passaggi preliminari) come origine e quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-129">In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![SQL Database Migration wizard - Select Source - step 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="43b6e-131">Nella finestra di dialogo **Seleziona oggetti** selezionare l'opzione **Seleziona oggetti di database specifici** e quindi scegliere una o più tabelle di cui eseguire la migrazione al server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-131">In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.</span></span>
   <span data-ttu-id="43b6e-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="43b6e-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="43b6e-133">Nella pagina **Riepilogo Generazione guidata script** fare clic su **Sì** quando verrà richiesto se si è pronti a generare uno script SQL.</span><span class="sxs-lookup"><span data-stu-id="43b6e-133">On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script.</span></span> <span data-ttu-id="43b6e-134">È anche possibile salvare lo script TSQL per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="43b6e-134">You also have the option to save the TSQL Script for later use.</span></span>
   <span data-ttu-id="43b6e-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="43b6e-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="43b6e-136">Nella pagina **Results Summary** (Riepilogo risultati) fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-136">On the **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="43b6e-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="43b6e-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="43b6e-138">Nella pagina **Setup Target Server Connection** (Configura connessione a server di destinazione) fare clic su **Connetti al server** e quindi immettere i dettagli seguenti:</span><span class="sxs-lookup"><span data-stu-id="43b6e-138">On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:</span></span>
   
   * <span data-ttu-id="43b6e-139">**Server Name**(Nome server): istanza del server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="43b6e-140">**Autenticazione**: **autenticazione di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="43b6e-141">Immettere le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="43b6e-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="43b6e-142">**Database**: **Master DB (List all databases)** (Database master (Elenca tutti i database)).</span><span class="sxs-lookup"><span data-stu-id="43b6e-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="43b6e-143">Questa opzione consente di elencare tutti i database nel server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-143">This option lists all the databases on the target server.</span></span>
     
     ![SQL Database Migration wizard - Setup Target Server Connection](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="43b6e-145">Fare clic su **Connetti**, selezionare il database di destinazione in cui si vuole spostare la tabella e fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="43b6e-145">Click **Connect**, select the target database that you want to move the table to, and then click **Next**.</span></span> <span data-ttu-id="43b6e-146">In tal modo si dovrebbe interrompere l'esecuzione dello script generato in precedenza e dovrebbe essere visualizzata la tabella appena spostata copiata nel database di destinazione.</span><span class="sxs-lookup"><span data-stu-id="43b6e-146">This should finish running the previously generated script, and you should see the newly moved table copied to the target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="43b6e-147">Passaggio di verifica</span><span class="sxs-lookup"><span data-stu-id="43b6e-147">Verification step</span></span>

- <span data-ttu-id="43b6e-148">Eseguire query e verificare la tabella appena copiata per assicurarsi che i dati siano inalterati.</span><span class="sxs-lookup"><span data-stu-id="43b6e-148">Query and test the newly copied table to make sure that the data is intact.</span></span> <span data-ttu-id="43b6e-149">Dopo la conferma, è possibile rimuovere la tabella rinominata nella sezione **Preparation steps** (Passaggi preliminari).</span><span class="sxs-lookup"><span data-stu-id="43b6e-149">Upon confirmation, you can drop the renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="43b6e-150">Ad esempio, &lt;nome tabella&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="43b6e-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="43b6e-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="43b6e-151">Next steps</span></span>
[<span data-ttu-id="43b6e-152">Backup automatici del database SQL</span><span class="sxs-lookup"><span data-stu-id="43b6e-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

