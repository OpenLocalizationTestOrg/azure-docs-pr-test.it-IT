---
title: Archiviare i backup del database SQL di Azure per un massimo di 10 anni | Microsoft Docs
description: Informazioni sul supporto del database SQL di Azure dell'archiviazione dei backup per un massimo di 10 anni.
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="f559b-103">Archiviare i backup del database SQL di Azure per un massimo di 10 anni</span><span class="sxs-lookup"><span data-stu-id="f559b-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="f559b-104">Molte applicazioni sono vincolate da ragioni normative, di conformità o altri scopi aziendali che richiedono di conservare i backup del database oltre i 7-35 giorni offerti dai [backup automatici](sql-database-automated-backups.md) del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="f559b-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="f559b-105">La funzionalità di conservazione dei backup a lungo termine consente di archiviare i backup del database SQL in un insieme di credenziali dei servizi di ripristino di Azure fino a 10 anni.</span><span class="sxs-lookup"><span data-stu-id="f559b-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="f559b-106">È possibile archiviare fino a 1.000 database per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="f559b-107">È possibile quindi selezionare qualsiasi backup nell'insieme di credenziali per ripristinarlo come nuovo database.</span><span class="sxs-lookup"><span data-stu-id="f559b-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f559b-108">La conservazione dei backup a lungo termine è attualmente in anteprima ed è disponibile nelle aree seguenti: Australia orientale, Australia sud-orientale, Brasile meridionale, Stati Uniti centrali, Asia orientale, Stati Uniti orientali, Stati Uniti orientali 2, India centrale, India meridionale, Giappone orientale, Giappone occidentale, Stati Uniti centro-settentrionali, Europa settentrionale, Stati Uniti centro-meridionali, Asia sud-orientale, Europa occidentale e Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="f559b-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="f559b-109">È possibile abilitare fino a 200 database per ogni insieme di credenziali in un periodo di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="f559b-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="f559b-110">È consigliabile usare insiemi di credenziali separati per ogni server al fine di ridurre al minimo l'impatto di questo limite.</span><span class="sxs-lookup"><span data-stu-id="f559b-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="f559b-111">Funzionamento della conservazione a lungo termine dei backup del database SQL</span><span class="sxs-lookup"><span data-stu-id="f559b-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="f559b-112">La conservazione a lungo termine dei backup consente di associare un server del database SQL a un insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="f559b-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="f559b-113">L'insieme di credenziali deve essere creato nella stessa sottoscrizione di Azure in cui è stato creato il server SQL, nonché nella stessa area geografica e gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f559b-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="f559b-114">È quindi possibile configurare un criterio di conservazione per qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="f559b-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="f559b-115">Il criterio consente di copiare i backup settimanali del database completo nell'insieme di credenziali dei servizi di ripristino e di conservare i backup per il periodo di memorizzazione specificato, ovvero fino a 10 anni.</span><span class="sxs-lookup"><span data-stu-id="f559b-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="f559b-116">Sarà quindi possibile ripristinare il database da una copia di questi backup in un nuovo database in qualsiasi server nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f559b-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="f559b-117">Partendo da backup esistenti Archiviazione di Azure crea una copia che non ha alcun impatto sulle prestazioni del database esistente.</span><span class="sxs-lookup"><span data-stu-id="f559b-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="f559b-118">Per informazioni di guida, vedere [Configurare e ripristinare dalla conservazione dei backup a lungo termine del database SQL di Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="f559b-119">Abilitare la conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-119">Enable long-term backup retention</span></span>

<span data-ttu-id="f559b-120">Per configurare la conservazione a lungo termine dei backup per un database:</span><span class="sxs-lookup"><span data-stu-id="f559b-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="f559b-121">Creare un insieme di credenziali dei servizi di ripristino di Azure nella stessa area, sottoscrizione e gruppo di risorse in cui si trova il server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="f559b-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="f559b-122">Registrare il server nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="f559b-123">Creare un criterio di protezione per i servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="f559b-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="f559b-124">Applicare il criterio di protezione ai database che richiedono la conservazione dei backup a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="f559b-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="f559b-125">Per configurare, gestire e ripristinare un database dalla conservazione a lungo termine di backup automatici in un insieme di credenziali di Servizi di ripristino di Azure, eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f559b-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="f559b-126">Tramite il portale di Azure: fare clic su **Conservazione backup a lungo termine**, selezionare un database e quindi fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="f559b-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selezionare un database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="f559b-128">Tramite PowerShell: passare a [Configurare e ripristinare dalla conservazione dei backup a lungo termine del database SQL di Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="f559b-129">Ripristinare un database archiviato con la funzionalità di conservazione dei backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="f559b-130">Per ripristinare un database da un backup di conservazione a lungo termine:</span><span class="sxs-lookup"><span data-stu-id="f559b-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="f559b-131">Elencare l'insieme di credenziali in cui è archiviato il backup.</span><span class="sxs-lookup"><span data-stu-id="f559b-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="f559b-132">Elencare il contenitore in cui viene eseguito il mapping al server logico.</span><span class="sxs-lookup"><span data-stu-id="f559b-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="f559b-133">Elencare l'origine dei dati all'interno dell'insieme di credenziali in cui viene eseguito il mapping al database.</span><span class="sxs-lookup"><span data-stu-id="f559b-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="f559b-134">Elencare i punti di ripristino disponibili per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="f559b-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="f559b-135">Eseguire il ripristino dal punto di ripristino verso il server di destinazione all'interno della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f559b-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="f559b-136">Per configurare, gestire e ripristinare un database dalla conservazione a lungo termine di backup automatici in un insieme di credenziali di Servizi di ripristino di Azure, eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f559b-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="f559b-137">Tramite il portale di Azure: passare a [Gestire la conservazione del backup a lungo termine usando il portale di Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="f559b-138">Tramite PowerShell: passare a [Gestire la conservazione del backup a lungo termine usando PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="f559b-139">Trovare i prezzi per la conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="f559b-140">Il costo della conservazione dei backup a lungo termine di un database SQL dipende dalle [tariffe dei servizi di backup di Azure](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="f559b-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="f559b-141">Dopo che il server del database SQL viene registrato nell'insieme di credenziali, viene addebitata l'archiviazione totale usata per i backup settimanali archiviati nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="f559b-142">Visualizzare i backup disponibili archiviati nella conservazione dei backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="f559b-143">Per configurare, gestire e ripristinare un database dalla conservazione a lungo termine di backup automatici in un insieme di credenziali di Servizi di ripristino di Azure tramite il portale di Azure, eseguire una delle operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f559b-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="f559b-144">Tramite il portale di Azure: passare a [Gestire la conservazione del backup a lungo termine usando il portale di Azure](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="f559b-145">Tramite PowerShell: passare a [Gestire la conservazione del backup a lungo termine usando PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="f559b-146">Disabilitare la conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-146">Disable long-term retention</span></span>

<span data-ttu-id="f559b-147">Il servizio di ripristino gestisce in automatico l'eliminazione dei backup in base ai criteri di conservazione specificati.</span><span class="sxs-lookup"><span data-stu-id="f559b-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="f559b-148">Per interrompere l'invio di backup di un database specifico all'insieme di credenziali, rimuovere i criteri di conservazione relativi al database specifico.</span><span class="sxs-lookup"><span data-stu-id="f559b-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="f559b-149">I backup che sono già nell'insieme di credenziali non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="f559b-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="f559b-150">Questi vengono automaticamente eliminati dal servizio di ripristino alla scadenza del periodo di conservazione.</span><span class="sxs-lookup"><span data-stu-id="f559b-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="f559b-151">Domande frequenti sulla conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="f559b-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="f559b-152">**È possibile eliminare manualmente backup specifici nell'insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="f559b-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="f559b-153">No, per il momento.</span><span class="sxs-lookup"><span data-stu-id="f559b-153">Not currently.</span></span> <span data-ttu-id="f559b-154">L'insieme di credenziali pulisce automaticamente i backup quando il periodo di conservazione è scaduto.</span><span class="sxs-lookup"><span data-stu-id="f559b-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="f559b-155">**È possibile registrare un server per archiviare backup di più di un insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="f559b-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="f559b-156">No, attualmente è possibile archiviare solo i backup di un insieme di credenziali per volta.</span><span class="sxs-lookup"><span data-stu-id="f559b-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="f559b-157">**È possibile disporre di un insieme di credenziali e un server in sottoscrizioni diverse?**</span><span class="sxs-lookup"><span data-stu-id="f559b-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="f559b-158">No, attualmente l'insieme di credenziali e il server devono trovarsi nella stessa sottoscrizione e nello stesso gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f559b-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="f559b-159">**È possibile usare un insieme di credenziali creato in un'area diversa rispetto all'area del mio server?**</span><span class="sxs-lookup"><span data-stu-id="f559b-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="f559b-160">No, l'insieme di credenziali e il server devono trovarsi nella stessa area per ridurre al minimo il tempo di copia ed evitare costi di traffico.</span><span class="sxs-lookup"><span data-stu-id="f559b-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="f559b-161">**Quanti database è possibile archiviare in un insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="f559b-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="f559b-162">Attualmente è supportato un massimo di 1.000 database per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="f559b-163">**Quanti insiemi di credenziali è possibile creare per ogni sottoscrizione?**</span><span class="sxs-lookup"><span data-stu-id="f559b-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="f559b-164">È possibile creare fino a 25 insiemi di credenziali per sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f559b-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="f559b-165">**Quanti database è possibile configurare al giorno per ogni insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="f559b-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="f559b-166">È possibile configurare 200 database al giorno per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="f559b-167">**La conservazione dei backup a lungo termine funziona con i pool elastici?**</span><span class="sxs-lookup"><span data-stu-id="f559b-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="f559b-168">Sì.</span><span class="sxs-lookup"><span data-stu-id="f559b-168">Yes.</span></span> <span data-ttu-id="f559b-169">Qualsiasi database nel pool può essere configurato con i criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="f559b-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="f559b-170">**È possibile scegliere l'ora di creazione del backup?**</span><span class="sxs-lookup"><span data-stu-id="f559b-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="f559b-171">No, il database SQL controlla la pianificazione dei backup per ridurre al minimo l'impatto sulle prestazioni dei database.</span><span class="sxs-lookup"><span data-stu-id="f559b-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="f559b-172">**Per il database è attiva Transparent Data Encryption . È possibile usarla nell'insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="f559b-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="f559b-173">Sì, Transparent Data Encryption è supportata.</span><span class="sxs-lookup"><span data-stu-id="f559b-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="f559b-174">Anche se il database originale non esiste più, è possibile ripristinare il database dall'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="f559b-175">**Cosa succede ai backup nell'insieme di credenziali se la mia sottoscrizione viene sospesa?**</span><span class="sxs-lookup"><span data-stu-id="f559b-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="f559b-176">Se la sottoscrizione viene sospesa, vengono mantenuti i database e i backup esistenti.</span><span class="sxs-lookup"><span data-stu-id="f559b-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="f559b-177">I nuovi backup non vengono copiati nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="f559b-178">Dopo la riattivazione della sottoscrizione, il servizio riprende la copia dei backup nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="f559b-179">L'insieme di credenziali diventa inaccessibile per le operazioni di ripristino che usano i backup copiati prima della sospensione della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="f559b-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="f559b-180">**È possibile accedere ai file di backup del database SQL per scaricarli o ripristinarli nel server di SQL?**</span><span class="sxs-lookup"><span data-stu-id="f559b-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="f559b-181">No, non attualmente.</span><span class="sxs-lookup"><span data-stu-id="f559b-181">No, not currently.</span></span>

<span data-ttu-id="f559b-182">**È possibile disporre di più pianificazioni, ad esempio giornaliere, settimanali, mensili, annuali, in un criterio di conservazione SQL?**</span><span class="sxs-lookup"><span data-stu-id="f559b-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="f559b-183">No, le pianificazioni multiple sono attualmente disponibili solo per i backup della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f559b-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="f559b-184">**Cosa accade se si configura la conservazione dei backup a lungo termine in un database che è una replica geografica attiva secondaria?**</span><span class="sxs-lookup"><span data-stu-id="f559b-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="f559b-185">Attualmente non vengono eseguiti backup sulle repliche e pertanto non è possibile la conservazione dei backup a lungo termine nei database secondari.</span><span class="sxs-lookup"><span data-stu-id="f559b-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="f559b-186">Tuttavia, è importante per un utente configurare la conservazione dei backup a lungo termine in un database secondario della replica geografica attivo per questi motivi:</span><span class="sxs-lookup"><span data-stu-id="f559b-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="f559b-187">Quando si verifica un failover e il database diventa un database primario, viene eseguito un backup completo, che verrà caricato nell'insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="f559b-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="f559b-188">La configurazione della conservazione dei backup a lungo termine in un database secondario non prevede alcun costo aggiuntivo per il cliente.</span><span class="sxs-lookup"><span data-stu-id="f559b-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f559b-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f559b-189">Next steps</span></span>
<span data-ttu-id="f559b-190">Poiché i backup dei database proteggono i dati da danneggiamenti o eliminazioni accidentali, sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="f559b-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="f559b-191">Per informazioni sulle altre soluzioni di continuità aziendale del database SQL, vedere [Panoramica della continuità aziendale](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="f559b-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
