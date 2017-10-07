---
title: aaaStore i backup di Database SQL di Azure per backup anni too10 | Documenti Microsoft
description: Informazioni su come Database SQL di Azure supporta l'archiviazione di backup per backup too10 anni.
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
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="833c4-103">Archiviare i backup del Database SQL di Azure per backup too10 anni</span><span class="sxs-lookup"><span data-stu-id="833c4-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="833c4-104">Molte applicazioni hanno normativi, conformità o altre attività che richiedono i backup di database tooretain oltre hello 7-35 giorni forniti dal Database SQL di Azure a scopo [backup automatici](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="833c4-105">Tramite funzionalità di conservazione dei backup a lungo termine hello, è possibile archiviare i backup dei database SQL in un insieme di credenziali di servizi di ripristino di Azure per backup too10 anni.</span><span class="sxs-lookup"><span data-stu-id="833c4-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="833c4-106">È possibile archiviare backup too1, 000 database per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="833c4-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="833c4-107">È quindi possibile selezionare qualsiasi backup hello insieme di credenziali toorestore come un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="833c4-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="833c4-108">Conservazione dei backup a lungo termine è attualmente in anteprima e disponibile in hello seguenti aree: Australia orientale, Australia sudorientale, Brasile meridionale, Stati Uniti centrali, Asia orientale, Stati Uniti orientali, Stati Uniti orientali 2, India centrale, India meridionale, Giappone orientale, Giappone occidentale, North Central US, settentrionale Europa, Stati Uniti centro-meridionali, Asia sudorientale, Europa occidentale e Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="833c4-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="833c4-109">È possibile abilitare dei database too200 per ogni insieme di credenziali durante un periodo di 24 ore.</span><span class="sxs-lookup"><span data-stu-id="833c4-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="833c4-110">È consigliabile utilizzare un archivio separato per ogni impatto hello toominimize di server di questo limite.</span><span class="sxs-lookup"><span data-stu-id="833c4-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="833c4-111">Funzionamento della conservazione a lungo termine dei backup del database SQL</span><span class="sxs-lookup"><span data-stu-id="833c4-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="833c4-112">La conservazione a lungo termine dei backup consente di associare un server del database SQL a un insieme di credenziali di Servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="833c4-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="833c4-113">È necessario creare l'insieme di credenziali hello in hello stessa sottoscrizione Azure creata hello SQL server e in hello stesso gruppo risorse e area geografico.</span><span class="sxs-lookup"><span data-stu-id="833c4-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="833c4-114">È quindi possibile configurare un criterio di conservazione per qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="833c4-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="833c4-115">Hello criteri cause hello settimanale completo del database backup toobe copiati insieme di credenziali di servizi di ripristino toohello e conservati per il periodo di memorizzazione specificato hello (backup too10 anni).</span><span class="sxs-lookup"><span data-stu-id="833c4-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="833c4-116">È quindi possibile ripristinare il database di hello da uno qualsiasi di questi backup tooa nuovo database in qualsiasi server nella sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="833c4-117">Archiviazione di Azure crea una copia di backup esistenti e copia hello non ha alcun impatto sulle prestazioni per il database esistente di hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="833c4-118">Per una procedura-tooguide, vedere [Configura e il ripristino da conservazione dei backup di Database SQL di Azure a lungo termine](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="833c4-119">Abilitare la conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="833c4-119">Enable long-term backup retention</span></span>

<span data-ttu-id="833c4-120">tooconfigure a lungo termine conservazione dei backup per un database:</span><span class="sxs-lookup"><span data-stu-id="833c4-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="833c4-121">Creare un insieme di credenziali di servizi di ripristino di Azure in hello stesso gruppo di area, sottoscrizione e delle risorse del server di database SQL.</span><span class="sxs-lookup"><span data-stu-id="833c4-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="833c4-122">Registrare l'insieme di credenziali di hello server toohello.</span><span class="sxs-lookup"><span data-stu-id="833c4-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="833c4-123">Creare un criterio di protezione per i servizi di ripristino di Azure.</span><span class="sxs-lookup"><span data-stu-id="833c4-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="833c4-124">Applicare i database toohello criteri di protezione hello che richiedono di conservazione dei backup a lungo termine.</span><span class="sxs-lookup"><span data-stu-id="833c4-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="833c4-125">tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure, effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="833c4-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="833c4-126">Tramite il portale di Azure di hello: fare clic su **conservazione dei backup a lungo termine**, selezionare un database e quindi fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="833c4-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selezionare un database per la conservazione backup a lungo termine](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="833c4-128">Utilizzo di PowerShell: Andare troppo[Configura e il ripristino da conservazione dei backup di Database SQL di Azure a lungo termine](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="833c4-129">Ripristinare un database che viene archiviato con funzionalità di conservazione dei backup a lungo termine hello</span><span class="sxs-lookup"><span data-stu-id="833c4-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="833c4-130">toorecover da un backup di conservazione dei backup a lungo termine:</span><span class="sxs-lookup"><span data-stu-id="833c4-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="833c4-131">Elenco hello insieme di credenziali in cui è memorizzato il backup di hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="833c4-132">Elenco hello contenitore server logico tooyour mappato.</span><span class="sxs-lookup"><span data-stu-id="833c4-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="833c4-133">Origine dati dell'elenco hello all'interno dell'insieme di credenziali hello che è mappata tooyour database.</span><span class="sxs-lookup"><span data-stu-id="833c4-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="833c4-134">Elenco hello dei punti di ripristino sono disponibili toorestore.</span><span class="sxs-lookup"><span data-stu-id="833c4-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="833c4-135">Ripristinare il database di hello dal server di destinazione toohello punto di ripristino hello nella sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="833c4-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="833c4-136">tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure, effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="833c4-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="833c4-137">Utilizzando hello portale di Azure: passare troppo[con conservazione dei backup a lungo termine Gestisci hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="833c4-138">Utilizzo di PowerShell: Andare troppo[gestire la conservazione di backup a lungo termine tramite PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="833c4-139">Trovare i prezzi per la conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="833c4-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="833c4-140">Conservazione dei backup a lungo termine di un database SQL viene addebitato in base toohello [servizi di Azure backup prezzi tariffe](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="833c4-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="833c4-141">Dopo aver registrato toohello insieme di credenziali server di database SQL di hello, vengono addebitati i hello spazio di archiviazione totale utilizzato da backup settimanale di hello archiviati nell'insieme di credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="833c4-142">Visualizzare i backup disponibili archiviati nella conservazione dei backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="833c4-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="833c4-143">tooconfigure, gestire e ripristinare un database da conservazione dei backup a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure tramite hello portale di Azure, effettuare una delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="833c4-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="833c4-144">Utilizzando hello portale di Azure: passare troppo[con conservazione dei backup a lungo termine Gestisci hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="833c4-145">Utilizzo di PowerShell: Andare troppo[gestire la conservazione di backup a lungo termine tramite PowerShell](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="833c4-146">Disabilitare la conservazione a lungo termine</span><span class="sxs-lookup"><span data-stu-id="833c4-146">Disable long-term retention</span></span>

<span data-ttu-id="833c4-147">il servizio di ripristino Hello gestisce automaticamente la pulizia di hello di backup in base a hello fornito criteri di conservazione.</span><span class="sxs-lookup"><span data-stu-id="833c4-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="833c4-148">backup hello l'invio di toostop per un insieme di credenziali toohello database specifico, rimuovere i criteri di conservazione hello per il database.</span><span class="sxs-lookup"><span data-stu-id="833c4-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="833c4-149">i backup di Hello che sono già nell'insieme di credenziali hello non sono interessati.</span><span class="sxs-lookup"><span data-stu-id="833c4-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="833c4-150">Vengono automaticamente eliminati dal servizio di ripristino hello quando scade il periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="833c4-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="833c4-151">Domande frequenti sulla conservazione del backup a lungo termine</span><span class="sxs-lookup"><span data-stu-id="833c4-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="833c4-152">**È possibile manualmente eliminare backup specifici nell'insieme di credenziali hello?**</span><span class="sxs-lookup"><span data-stu-id="833c4-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="833c4-153">No, per il momento.</span><span class="sxs-lookup"><span data-stu-id="833c4-153">Not currently.</span></span> <span data-ttu-id="833c4-154">insieme di credenziali Hello pulisce automaticamente i backup quando è scaduto il periodo di memorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="833c4-155">**È possibile registrare il toomore di backup server toostore rispetto a un insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="833c4-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="833c4-156">No, è attualmente possibile archiviare backup tooonly due insiemi di credenziali alla volta.</span><span class="sxs-lookup"><span data-stu-id="833c4-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="833c4-157">**È possibile disporre di un insieme di credenziali e un server in sottoscrizioni diverse?**</span><span class="sxs-lookup"><span data-stu-id="833c4-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="833c4-158">No, attualmente insieme di credenziali hello e server devono trovarsi in hello stesso gruppo di risorse e di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="833c4-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="833c4-159">**È possibile usare un insieme di credenziali creato in un'area diversa rispetto all'area del mio server?**</span><span class="sxs-lookup"><span data-stu-id="833c4-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="833c4-160">No, deve essere l'insieme di credenziali hello e server hello toominimize area stessa ora di copiare ed evitare addebiti per il traffico.</span><span class="sxs-lookup"><span data-stu-id="833c4-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="833c4-161">**Quanti database è possibile archiviare in un insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="833c4-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="833c4-162">Attualmente supporta backup too1, 000 database per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="833c4-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="833c4-163">**Quanti insiemi di credenziali è possibile creare per ogni sottoscrizione?**</span><span class="sxs-lookup"><span data-stu-id="833c4-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="833c4-164">È possibile creare backup too25 gli insiemi di credenziali per ogni sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="833c4-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="833c4-165">**Quanti database è possibile configurare al giorno per ogni insieme di credenziali?**</span><span class="sxs-lookup"><span data-stu-id="833c4-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="833c4-166">È possibile configurare 200 database al giorno per ogni insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="833c4-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="833c4-167">**La conservazione dei backup a lungo termine funziona con i pool elastici?**</span><span class="sxs-lookup"><span data-stu-id="833c4-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="833c4-168">Sì.</span><span class="sxs-lookup"><span data-stu-id="833c4-168">Yes.</span></span> <span data-ttu-id="833c4-169">Qualsiasi database nel pool di hello può essere configurato con criteri di conservazione hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="833c4-170">**È possibile scegliere l'ora di hello in corrispondenza del quale viene creato il backup di hello?**</span><span class="sxs-lookup"><span data-stu-id="833c4-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="833c4-171">No, il Database SQL controlla hello pianificazione del backup toominimize hello impatto sulle prestazioni dei database.</span><span class="sxs-lookup"><span data-stu-id="833c4-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="833c4-172">**Per il database è attiva Transparent Data Encryption . È possibile usarli insieme di credenziali hello.**</span><span class="sxs-lookup"><span data-stu-id="833c4-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="833c4-173">Sì, Transparent Data Encryption è supportata.</span><span class="sxs-lookup"><span data-stu-id="833c4-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="833c4-174">È possibile ripristinare il database di hello dall'insieme di credenziali hello anche se il database originale di hello non esiste più.</span><span class="sxs-lookup"><span data-stu-id="833c4-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="833c4-175">**Cosa accade con backup hello nell'insieme di credenziali hello se la sottoscrizione è sospesa.**</span><span class="sxs-lookup"><span data-stu-id="833c4-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="833c4-176">Se la sottoscrizione è sospesa, è conservare i backup e i database esistenti di hello.</span><span class="sxs-lookup"><span data-stu-id="833c4-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="833c4-177">I nuovi backup non sono toohello copiati insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="833c4-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="833c4-178">Dopo aver riattivato sottoscrizione hello, servizio hello riprende la copia di backup toohello insieme di credenziali.</span><span class="sxs-lookup"><span data-stu-id="833c4-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="833c4-179">L'insieme di credenziali diventa accessibile toohello operazioni di ripristino tramite backup di hello che sono stati copiati in tale posizione prima sottoscrizione hello è stata sospesa.</span><span class="sxs-lookup"><span data-stu-id="833c4-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="833c4-180">**È possibile ottenere accesso toohello file di backup del database SQL in modo è possibile scaricare o ripristinarli toohello SQL server?**</span><span class="sxs-lookup"><span data-stu-id="833c4-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="833c4-181">No, non attualmente.</span><span class="sxs-lookup"><span data-stu-id="833c4-181">No, not currently.</span></span>

<span data-ttu-id="833c4-182">**È possibile toohave più pianificazioni (giornaliera, settimanale, mensile, annuale) all'interno di un criterio di conservazione SQL.**</span><span class="sxs-lookup"><span data-stu-id="833c4-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="833c4-183">No, le pianificazioni multiple sono attualmente disponibili solo per i backup della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="833c4-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="833c4-184">**Cosa accade se si configura la conservazione dei backup a lungo termine in un database che è una replica geografica attiva secondaria?**</span><span class="sxs-lookup"><span data-stu-id="833c4-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="833c4-185">Attualmente non vengono eseguiti backup sulle repliche e pertanto non è possibile la conservazione dei backup a lungo termine nei database secondari.</span><span class="sxs-lookup"><span data-stu-id="833c4-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="833c4-186">Tuttavia, è importante per gli utenti tooset di conservazione dei backup a lungo termine in un database secondario di replica geografica attiva per i motivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="833c4-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="833c4-187">Quando si verifica un failover e database hello diventa un database primario, si esegue il backup completo, ovvero toovault caricato.</span><span class="sxs-lookup"><span data-stu-id="833c4-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="833c4-188">Non vi è alcun extra costi toohello cliente per l'impostazione di conservazione dei backup a lungo termine in un database secondario.</span><span class="sxs-lookup"><span data-stu-id="833c4-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="833c4-189">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="833c4-189">Next steps</span></span>
<span data-ttu-id="833c4-190">Poiché i backup dei database proteggono i dati da danneggiamenti o eliminazioni accidentali, sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="833c4-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="833c4-191">toolearn circa hello altre soluzioni di continuità aziendale del Database SQL, vedere [Panoramica di continuità aziendale](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="833c4-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
