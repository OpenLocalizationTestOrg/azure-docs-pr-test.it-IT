---
title: Eseguire la migrazione di un Azure Data Warehouse esistente all'archiviazione Premium | Microsoft Docs
description: Istruzioni per la migrazione di un data warehouse esistente all'archiviazione Premium
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: barbkess
editor: 
ms.assetid: 04b05dea-c066-44a0-9751-0774eb84c689
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 11/29/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 860e50b532b4b0a21d3be54f087730070b0e56bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-data-warehouse-to-premium-storage"></a><span data-ttu-id="45337-103">Eseguire la migrazione di un data warehouse proprio all'archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="45337-103">Migrate your data warehouse to premium storage</span></span>
<span data-ttu-id="45337-104">Azure SQL Data Warehouse ha recentemente introdotto l'[archiviazione Premium per una maggiore prevedibilità delle prestazioni][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="45337-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="45337-105">I data warehouse esistenti attualmente inclusi nell'archiviazione Standard possono essere migrati all'archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="45337-105">Existing data warehouses currently on standard storage can now be migrated to premium storage.</span></span> <span data-ttu-id="45337-106">È possibile sfruttare la migrazione automatica oppure, se si preferisce controllare quando eseguire la migrazione (che prevede tempi di inattività), è possibile eseguire la migrazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="45337-106">You can take advantage of automatic migration, or if you prefer to control when to migrate (which does involve some downtime), you can do the migration yourself.</span></span>

<span data-ttu-id="45337-107">Se si hanno più data warehouse, usare la [pianificazione della migrazione automatica][automatic migration schedule] per determinare quando verrà eseguita la relativa migrazione.</span><span class="sxs-lookup"><span data-stu-id="45337-107">If you have more than one data warehouse, use the [automatic migration schedule][automatic migration schedule] to determine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="45337-108">Determinare il tipo di archiviazione</span><span class="sxs-lookup"><span data-stu-id="45337-108">Determine storage type</span></span>
<span data-ttu-id="45337-109">Se il data warehouse è stato creato prima delle date riportate di seguito, si sta usando l'archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="45337-109">If you created a data warehouse before the following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="45337-110">**Area**</span><span class="sxs-lookup"><span data-stu-id="45337-110">**Region**</span></span> | <span data-ttu-id="45337-111">**Data warehouse creato prima di questa data**</span><span class="sxs-lookup"><span data-stu-id="45337-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="45337-112">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="45337-112">Australia East</span></span> |<span data-ttu-id="45337-113">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="45337-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="45337-114">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="45337-114">China East</span></span> |<span data-ttu-id="45337-115">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="45337-115">November 1, 2016</span></span> |
| <span data-ttu-id="45337-116">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="45337-116">China North</span></span> |<span data-ttu-id="45337-117">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="45337-117">November 1, 2016</span></span> |
| <span data-ttu-id="45337-118">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="45337-118">Germany Central</span></span> |<span data-ttu-id="45337-119">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="45337-119">November 1, 2016</span></span> |
| <span data-ttu-id="45337-120">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="45337-120">Germany Northeast</span></span> |<span data-ttu-id="45337-121">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="45337-121">November 1, 2016</span></span> |
| <span data-ttu-id="45337-122">India occidentale</span><span class="sxs-lookup"><span data-stu-id="45337-122">India West</span></span> |<span data-ttu-id="45337-123">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="45337-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="45337-124">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="45337-124">Japan West</span></span> |<span data-ttu-id="45337-125">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="45337-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="45337-126">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="45337-126">North Central US</span></span> |<span data-ttu-id="45337-127">10 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="45337-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="45337-128">Dettagli sulla migrazione automatica</span><span class="sxs-lookup"><span data-stu-id="45337-128">Automatic migration details</span></span>
<span data-ttu-id="45337-129">Per impostazione predefinita, la migrazione automatica del database verrà eseguita tra le 18.00 e le 06.00 ora locale dell'area di appartenenza, in base alla [pianificazione della migrazione automatica][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="45337-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during the [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="45337-130">Durante la migrazione non sarà possibile usare il data warehouse esistente.</span><span class="sxs-lookup"><span data-stu-id="45337-130">Your existing data warehouse will be unusable during the migration.</span></span> <span data-ttu-id="45337-131">La migrazione richiederà circa un'ora per TB di archiviazione per ogni data warehouse.</span><span class="sxs-lookup"><span data-stu-id="45337-131">The migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="45337-132">Durante il processo di migrazione automatica non verranno addebitati costi.</span><span class="sxs-lookup"><span data-stu-id="45337-132">You will not be charged during any portion of the automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="45337-133">Al termine della migrazione, il data warehouse sarà di nuovo online e potrà essere riutilizzato.</span><span class="sxs-lookup"><span data-stu-id="45337-133">When the migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="45337-134">Per completare la migrazione, Microsoft si atterrà alla seguente procedura (non è richiesto alcun intervento da parte dell'utente).</span><span class="sxs-lookup"><span data-stu-id="45337-134">Microsoft is taking the following steps to complete the migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="45337-135">In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".</span><span class="sxs-lookup"><span data-stu-id="45337-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="45337-136">Microsoft rinomina "MyDW" in "MyDW_DO_NOT_USE_[Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="45337-136">Microsoft renames “MyDW” to “MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="45337-137">Microsoft sospende "MyDW" in "MyDW_DO_NOT_USE_[Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="45337-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="45337-138">Nel mentre, viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="45337-138">During this time, a backup is taken.</span></span> <span data-ttu-id="45337-139">In caso di problemi, il processo potrebbe essere sospeso e riprendere più volte.</span><span class="sxs-lookup"><span data-stu-id="45337-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="45337-140">Microsoft crea un nuovo data warehouse denominato "MyDW" in archiviazione Premium dal backup eseguito al passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="45337-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from the backup taken in step 2.</span></span> <span data-ttu-id="45337-141">"MyDW" non viene visualizzato fino al termine del processo di ripristino.</span><span class="sxs-lookup"><span data-stu-id="45337-141">“MyDW” will not appear until after the restore is complete.</span></span>
4. <span data-ttu-id="45337-142">Dopo aver completato il ripristino, "MyDW" torna alle stesse unità data warehouse e allo stato (sospeso o attivo) in cui si trovava prima della migrazione.</span><span class="sxs-lookup"><span data-stu-id="45337-142">After the restore is complete, “MyDW” returns to the same data warehouse units and state (paused or active) that it was before the migration.</span></span>
5. <span data-ttu-id="45337-143">Al termine della migrazione, Microsoft elimina "MyDW_DO_NOT_USE_[Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="45337-143">After the migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="45337-144">Le impostazioni seguenti non vengono mantenute come parte della migrazione:</span><span class="sxs-lookup"><span data-stu-id="45337-144">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="45337-145">Il controllo a livello di database deve essere abilitato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45337-145">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="45337-146">Le regole del firewall a livello di database devono essere aggiunte nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45337-146">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="45337-147">Le regole del firewall a livello di server non sono interessate.</span><span class="sxs-lookup"><span data-stu-id="45337-147">Firewall rules at the server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="45337-148">pianificazione della migrazione automatica</span><span class="sxs-lookup"><span data-stu-id="45337-148">Automatic migration schedule</span></span>
<span data-ttu-id="45337-149">I processi di migrazione automatica vengono eseguiti tra le 18.00 e le 06.00 (ora locale per ogni area) durante la seguente pianificazione di interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="45337-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during the following outage schedule.</span></span>

| <span data-ttu-id="45337-150">**Area**</span><span class="sxs-lookup"><span data-stu-id="45337-150">**Region**</span></span> | <span data-ttu-id="45337-151">**Data di inizio prevista**</span><span class="sxs-lookup"><span data-stu-id="45337-151">**Estimated start date**</span></span> | <span data-ttu-id="45337-152">**Data di fine prevista**</span><span class="sxs-lookup"><span data-stu-id="45337-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="45337-153">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="45337-153">Australia East</span></span> |<span data-ttu-id="45337-154">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-154">Not determined yet</span></span> |<span data-ttu-id="45337-155">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-155">Not determined yet</span></span> |
| <span data-ttu-id="45337-156">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="45337-156">China East</span></span> |<span data-ttu-id="45337-157">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-157">January 9, 2017</span></span> |<span data-ttu-id="45337-158">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-158">January 13, 2017</span></span> |
| <span data-ttu-id="45337-159">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="45337-159">China North</span></span> |<span data-ttu-id="45337-160">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-160">January 9, 2017</span></span> |<span data-ttu-id="45337-161">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-161">January 13, 2017</span></span> |
| <span data-ttu-id="45337-162">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="45337-162">Germany Central</span></span> |<span data-ttu-id="45337-163">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-163">January 9, 2017</span></span> |<span data-ttu-id="45337-164">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-164">January 13, 2017</span></span> |
| <span data-ttu-id="45337-165">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="45337-165">Germany Northeast</span></span> |<span data-ttu-id="45337-166">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-166">January 9, 2017</span></span> |<span data-ttu-id="45337-167">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-167">January 13, 2017</span></span> |
| <span data-ttu-id="45337-168">India occidentale</span><span class="sxs-lookup"><span data-stu-id="45337-168">India West</span></span> |<span data-ttu-id="45337-169">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-169">Not determined yet</span></span> |<span data-ttu-id="45337-170">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-170">Not determined yet</span></span> |
| <span data-ttu-id="45337-171">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="45337-171">Japan West</span></span> |<span data-ttu-id="45337-172">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-172">Not determined yet</span></span> |<span data-ttu-id="45337-173">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="45337-173">Not determined yet</span></span> |
| <span data-ttu-id="45337-174">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="45337-174">North Central US</span></span> |<span data-ttu-id="45337-175">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-175">January 9, 2017</span></span> |<span data-ttu-id="45337-176">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="45337-176">January 13, 2017</span></span> |

## <a name="self-migration-to-premium-storage"></a><span data-ttu-id="45337-177">Migrazione self-service ad archiviazione Premium</span><span class="sxs-lookup"><span data-stu-id="45337-177">Self-migration to premium storage</span></span>
<span data-ttu-id="45337-178">Se si preferisce mantenere il controllo sui tempi di inattività, è possibile attenersi alla procedura seguente per eseguire la migrazione di un data warehouse esistente da archiviazione Standard ad archiviazione Premium.</span><span class="sxs-lookup"><span data-stu-id="45337-178">If you want to control when your downtime will occur, you can use the following steps to migrate an existing data warehouse on standard storage to premium storage.</span></span> <span data-ttu-id="45337-179">Se si sceglie questa opzione, è necessario completare la migrazione self-service prima che inizi la migrazione automatica in tale area.</span><span class="sxs-lookup"><span data-stu-id="45337-179">If you choose this option, you must complete the self-migration before the automatic migration begins in that region.</span></span> <span data-ttu-id="45337-180">Ciò consente di evitare che la migrazione automatica causi conflitti (vedere la [pianificazione della migrazione automatica][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="45337-180">This ensures that you avoid any risk of the automatic migration causing a conflict (refer to the [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="45337-181">Istruzioni per la migrazione self-service</span><span class="sxs-lookup"><span data-stu-id="45337-181">Self-migration instructions</span></span>
<span data-ttu-id="45337-182">Per migrare da sé il data warehouse, utilizzare le funzionalità di backup e ripristino.</span><span class="sxs-lookup"><span data-stu-id="45337-182">To migrate your data warehouse yourself, use the backup and restore features.</span></span> <span data-ttu-id="45337-183">La parte della migrazione relativa al ripristino dovrebbe richiedere circa un'ora per TB di archiviazione per ogni data warehouse.</span><span class="sxs-lookup"><span data-stu-id="45337-183">The restore portion of the migration is expected to take around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="45337-184">Per mantenere lo stesso nome dopo il completamento della migrazione, seguire la [procedura di ridenominazione durante la migrazione][steps to rename during migration].</span><span class="sxs-lookup"><span data-stu-id="45337-184">If you want to keep the same name after migration is complete, follow the [steps to rename during migration][steps to rename during migration].</span></span>

1. <span data-ttu-id="45337-185">[Sospendere][Pause] il data warehouse.</span><span class="sxs-lookup"><span data-stu-id="45337-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="45337-186">Questa operazione richiede un backup automatico.</span><span class="sxs-lookup"><span data-stu-id="45337-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="45337-187">[Eseguire il ripristino][Restore] dallo snapshot più recente.</span><span class="sxs-lookup"><span data-stu-id="45337-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="45337-188">Eliminare il data warehouse esistente in archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="45337-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="45337-189">**Se non viene eseguito questo passaggio, si riceverà l'addebito per entrambi i data warehouse.**</span><span class="sxs-lookup"><span data-stu-id="45337-189">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="45337-190">Le impostazioni seguenti non vengono mantenute come parte della migrazione:</span><span class="sxs-lookup"><span data-stu-id="45337-190">The following settings do not carry over as part of the migration:</span></span>
>
> * <span data-ttu-id="45337-191">Il controllo a livello di database deve essere abilitato nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45337-191">Auditing at the database level needs to be re-enabled.</span></span>
> * <span data-ttu-id="45337-192">Le regole del firewall a livello di database devono essere aggiunte nuovamente.</span><span class="sxs-lookup"><span data-stu-id="45337-192">Firewall rules at the database level need to be re-added.</span></span> <span data-ttu-id="45337-193">Le regole del firewall a livello di server non sono interessate.</span><span class="sxs-lookup"><span data-stu-id="45337-193">Firewall rules at the server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="45337-194">Rinominare il data warehouse durante la migrazione (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="45337-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="45337-195">Due database nello stesso server logico non possono avere lo stesso nome.</span><span class="sxs-lookup"><span data-stu-id="45337-195">Two databases on the same logical server cannot have the same name.</span></span> <span data-ttu-id="45337-196">SQL Data Warehouse ora supporta la possibilità di rinominare un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="45337-196">SQL Data Warehouse now supports the ability to rename a data warehouse.</span></span>

<span data-ttu-id="45337-197">In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".</span><span class="sxs-lookup"><span data-stu-id="45337-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="45337-198">Rinominare "MyDW" utilizzando il seguente comando ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="45337-198">Rename "MyDW" by using the following ALTER DATABASE command.</span></span> <span data-ttu-id="45337-199">(In questo esempio, è necessario rinominarlo "MyDW_BeforeMigration.")  Questo comando arresta tutte le transazioni esistenti e, per avere esito positivo, deve essere eseguito nel database master.</span><span class="sxs-lookup"><span data-stu-id="45337-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in the master database to succeed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="45337-200">[Sospendere][Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="45337-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="45337-201">Questa operazione richiede un backup automatico.</span><span class="sxs-lookup"><span data-stu-id="45337-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="45337-202">[Reimpostare][Restore] dallo snapshot più recente un nuovo database con il nome solito (es. "MyDW").</span><span class="sxs-lookup"><span data-stu-id="45337-202">[Restore][Restore] from your most recent snapshot a new database with the name it used to be (for example, "MyDW").</span></span>
4. <span data-ttu-id="45337-203">Eliminare "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="45337-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="45337-204">**Se non viene eseguito questo passaggio, si riceverà l'addebito per entrambi i data warehouse.**</span><span class="sxs-lookup"><span data-stu-id="45337-204">**If you fail to do this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="45337-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="45337-205">Next steps</span></span>
<span data-ttu-id="45337-206">Con il passaggio ad archiviazione Premium, il numero di file BLOB del database nell'architettura sottostante del data warehouse è aumentato.</span><span class="sxs-lookup"><span data-stu-id="45337-206">With the change to premium storage, you also have an increased number of database blob files in the underlying architecture of your data warehouse.</span></span> <span data-ttu-id="45337-207">Per ottenere il massimo dei vantaggi delle prestazioni per questa modifica, ricreare gli indici columnstore cluster usando il seguente script.</span><span class="sxs-lookup"><span data-stu-id="45337-207">To maximize the performance benefits of this change, rebuild your clustered columnstore indexes by using the following script.</span></span> <span data-ttu-id="45337-208">Lo script funziona forzando alcuni dei dati esistenti per i BLOB aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="45337-208">The script works by forcing some of your existing data to the additional blobs.</span></span> <span data-ttu-id="45337-209">Se non viene eseguita alcuna azione, i dati vengono ovviamente ridistribuiti nel tempo mentre si caricano più dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="45337-209">If you take no action, the data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="45337-210">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="45337-210">**Prerequisites:**</span></span>

- <span data-ttu-id="45337-211">È necessario eseguire il data warehouse con almeno 1.000 unità data warehouse (vedere [Ridimensionare la potenza di calcolo][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="45337-211">The data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="45337-212">L'utente che esegue lo script deve essere nel [ruolo mediumrc][mediumrc role] o superiore.</span><span class="sxs-lookup"><span data-stu-id="45337-212">The user executing the script should be in the [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="45337-213">Per aggiungere un utente a questo ruolo, eseguire questo codice: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="45337-213">To add a user to this role, execute the following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table to control index rebuild
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------
create table sql_statements
WITH (distribution = round_robin)
as select
    'alter index all on ' + s.name + '.' + t.NAME + ' rebuild;' as statement,
    row_number() over (order by s.name, t.name) as sequence
from
    sys.schemas s
    inner join sys.tables t
        on s.schema_id = t.schema_id
where
    is_external = 0
;
go

--------------------------------------------------------------------------------
-- Step 2: Execute index rebuilds. If script fails, the below can be re-run to restart where last left off.
-- Run as user in mediumrc or higher
--------------------------------------------------------------------------------

declare @nbr_statements int = (select count(*) from sql_statements)
declare @i int = 1
while(@i <= @nbr_statements)
begin
      declare @statement nvarchar(1000)= (select statement from sql_statements where sequence = @i)
      print cast(getdate() as nvarchar(1000)) + ' Executing... ' + @statement
      exec (@statement)
      delete from sql_statements where sequence = @i
      set @i += 1
end;
go
-------------------------------------------------------------------------------
-- Step 3: Clean up table created in Step 1
--------------------------------------------------------------------------------
drop table sql_statements;
go
````

<span data-ttu-id="45337-214">In caso di problemi con il data warehouse, [creare un ticket di supporto][create a support ticket] e specificare la migrazione ad archiviazione Premium come possibile causa.</span><span class="sxs-lookup"><span data-stu-id="45337-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration to premium storage” as the possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration to Premium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps to rename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
