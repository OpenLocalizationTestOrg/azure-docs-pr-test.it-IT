---
title: aaaMigrate i dati di Azure esistenti warehouse archiviazione toopremium | Documenti Microsoft
description: Istruzioni per la migrazione di un'archiviazione toopremium esistente del data warehouse
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
ms.openlocfilehash: 145199c2da1f6f1fb8898626cd04886c42d82204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-data-warehouse-toopremium-storage"></a><span data-ttu-id="2d0f7-103">Eseguire la migrazione di archiviazione del data warehouse toopremium</span><span class="sxs-lookup"><span data-stu-id="2d0f7-103">Migrate your data warehouse toopremium storage</span></span>
<span data-ttu-id="2d0f7-104">Azure SQL Data Warehouse ha recentemente introdotto l'[archiviazione Premium per una maggiore prevedibilità delle prestazioni][premium storage for greater performance predictability].</span><span class="sxs-lookup"><span data-stu-id="2d0f7-104">Azure SQL Data Warehouse recently introduced [premium storage for greater performance predictability][premium storage for greater performance predictability].</span></span> <span data-ttu-id="2d0f7-105">Dati esistenti magazzini attualmente nell'archivio standard è ora possibile eseguire la migrazione archiviazione toopremium.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-105">Existing data warehouses currently on standard storage can now be migrated toopremium storage.</span></span> <span data-ttu-id="2d0f7-106">È possibile sfruttare la migrazione automatica, oppure se si preferisce toocontrol quando toomigrate (che implicano tempi di inattività), è possibile eseguire hello migrazione manualmente.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-106">You can take advantage of automatic migration, or if you prefer toocontrol when toomigrate (which does involve some downtime), you can do hello migration yourself.</span></span>

<span data-ttu-id="2d0f7-107">Se si dispone di più di un data warehouse, utilizzare hello [pianificazione migrazione automatica] [ automatic migration schedule] toodetermine quando verranno inoltre migrato.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-107">If you have more than one data warehouse, use hello [automatic migration schedule][automatic migration schedule] toodetermine when it will also be migrated.</span></span>

## <a name="determine-storage-type"></a><span data-ttu-id="2d0f7-108">Determinare il tipo di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2d0f7-108">Determine storage type</span></span>
<span data-ttu-id="2d0f7-109">Se è stato creato un data warehouse prima hello seguenti date, archiviazione standard attualmente in uso.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-109">If you created a data warehouse before hello following dates, you are currently using standard storage.</span></span>

| <span data-ttu-id="2d0f7-110">**Area**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-110">**Region**</span></span> | <span data-ttu-id="2d0f7-111">**Data warehouse creato prima di questa data**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-111">**Data warehouse created before this date**</span></span> |
|:--- |:--- |
| <span data-ttu-id="2d0f7-112">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-112">Australia East</span></span> |<span data-ttu-id="2d0f7-113">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="2d0f7-113">Premium storage not yet available</span></span> |
| <span data-ttu-id="2d0f7-114">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-114">China East</span></span> |<span data-ttu-id="2d0f7-115">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="2d0f7-115">November 1, 2016</span></span> |
| <span data-ttu-id="2d0f7-116">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-116">China North</span></span> |<span data-ttu-id="2d0f7-117">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="2d0f7-117">November 1, 2016</span></span> |
| <span data-ttu-id="2d0f7-118">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-118">Germany Central</span></span> |<span data-ttu-id="2d0f7-119">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="2d0f7-119">November 1, 2016</span></span> |
| <span data-ttu-id="2d0f7-120">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-120">Germany Northeast</span></span> |<span data-ttu-id="2d0f7-121">1 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="2d0f7-121">November 1, 2016</span></span> |
| <span data-ttu-id="2d0f7-122">India occidentale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-122">India West</span></span> |<span data-ttu-id="2d0f7-123">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="2d0f7-123">Premium storage not yet available</span></span> |
| <span data-ttu-id="2d0f7-124">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-124">Japan West</span></span> |<span data-ttu-id="2d0f7-125">Archiviazione Premium non ancora disponibile</span><span class="sxs-lookup"><span data-stu-id="2d0f7-125">Premium storage not yet available</span></span> |
| <span data-ttu-id="2d0f7-126">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="2d0f7-126">North Central US</span></span> |<span data-ttu-id="2d0f7-127">10 novembre 2016</span><span class="sxs-lookup"><span data-stu-id="2d0f7-127">November 10, 2016</span></span> |

## <a name="automatic-migration-details"></a><span data-ttu-id="2d0f7-128">Dettagli sulla migrazione automatica</span><span class="sxs-lookup"><span data-stu-id="2d0f7-128">Automatic migration details</span></span>
<span data-ttu-id="2d0f7-129">Per impostazione predefinita, si verrà eseguita la migrazione del database è compreso tra 6:00 e le 6.00 nell'ora locale dell'area durante hello [pianificazione migrazione automatica][automatic migration schedule].</span><span class="sxs-lookup"><span data-stu-id="2d0f7-129">By default, we will migrate your database for you between 6:00 PM and 6:00 AM in your region's local time during hello [automatic migration schedule][automatic migration schedule].</span></span> <span data-ttu-id="2d0f7-130">Il data warehouse esistente non sarà utilizzabile durante la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-130">Your existing data warehouse will be unusable during hello migration.</span></span> <span data-ttu-id="2d0f7-131">migrazione Hello richiederà circa un'ora per terabyte di archiviazione per ogni del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-131">hello migration will take approximately one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="2d0f7-132">Non ti durante qualsiasi parte della migrazione automatica hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-132">You will not be charged during any portion of hello automatic migration.</span></span>

> [!NOTE]
> <span data-ttu-id="2d0f7-133">Una volta completata la migrazione di hello, il data warehouse sarà nuovamente online e utilizzabile.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-133">When hello migration is complete, your data warehouse will be back online and usable.</span></span>
>
>

<span data-ttu-id="2d0f7-134">Microsoft sta diventando hello passaggi toocomplete hello migrazione (questi non richiedono alcun intervento da parte dell'utente).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-134">Microsoft is taking hello following steps toocomplete hello migration (these do not require any involvement on your part).</span></span> <span data-ttu-id="2d0f7-135">In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-135">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="2d0f7-136">Microsoft Rinomina "MyDW" troppo "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-136">Microsoft renames “MyDW” too“MyDW_DO_NOT_USE_[Timestamp].”</span></span>
2. <span data-ttu-id="2d0f7-137">Microsoft sospende "MyDW" in "MyDW_DO_NOT_USE_[Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-137">Microsoft pauses “MyDW_DO_NOT_USE_[Timestamp].”</span></span> <span data-ttu-id="2d0f7-138">Nel mentre, viene eseguito il backup.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-138">During this time, a backup is taken.</span></span> <span data-ttu-id="2d0f7-139">In caso di problemi, il processo potrebbe essere sospeso e riprendere più volte.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-139">You may see multiple pauses and resumes if we encounter any issues during this process.</span></span>
3. <span data-ttu-id="2d0f7-140">Microsoft consente di creare un nuovo data warehouse, denominato "MyDW" in archiviazione premium da backup hello prese nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-140">Microsoft creates a new data warehouse named “MyDW” on premium storage from hello backup taken in step 2.</span></span> <span data-ttu-id="2d0f7-141">"MyDW" non verranno visualizzati fino a dopo il ripristino di hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-141">“MyDW” will not appear until after hello restore is complete.</span></span>
4. <span data-ttu-id="2d0f7-142">Dopo il ripristino di hello, "MyDW" restituisce toohello stessi dati del data warehouse di unità e sullo stato (sospesa o attiva) in cui si trovava prima della migrazione hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-142">After hello restore is complete, “MyDW” returns toohello same data warehouse units and state (paused or active) that it was before hello migration.</span></span>
5. <span data-ttu-id="2d0f7-143">Al termine della migrazione hello, Microsoft eliminerà "MyDW_DO_NOT_USE_ [Timestamp]".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-143">After hello migration is complete, Microsoft deletes “MyDW_DO_NOT_USE_[Timestamp]”.</span></span>

> [!NOTE]
> <span data-ttu-id="2d0f7-144">Hello seguenti impostazioni non vengono trasferiti durante la migrazione di hello:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-144">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="2d0f7-145">Il controllo a livello di database hello deve toobe nuovamente abilitata.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-145">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="2d0f7-146">Regole del firewall a livello di database hello necessario toobe aggiunto di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-146">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="2d0f7-147">Regole del firewall a livello di server hello non sono interessate.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-147">Firewall rules at hello server level are not affected.</span></span>
>
>

### <a name="automatic-migration-schedule"></a><span data-ttu-id="2d0f7-148">pianificazione della migrazione automatica</span><span class="sxs-lookup"><span data-stu-id="2d0f7-148">Automatic migration schedule</span></span>
<span data-ttu-id="2d0f7-149">Migrazioni automatiche durante hello base alla pianificazione di interruzione tra 6:00 e 6:00:00 (ora locale per ogni area).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-149">Automatic migrations occur between 6:00 PM and 6:00 AM (local time per region) during hello following outage schedule.</span></span>

| <span data-ttu-id="2d0f7-150">**Area**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-150">**Region**</span></span> | <span data-ttu-id="2d0f7-151">**Data di inizio prevista**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-151">**Estimated start date**</span></span> | <span data-ttu-id="2d0f7-152">**Data di fine prevista**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-152">**Estimated end date**</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="2d0f7-153">Australia orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-153">Australia East</span></span> |<span data-ttu-id="2d0f7-154">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-154">Not determined yet</span></span> |<span data-ttu-id="2d0f7-155">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-155">Not determined yet</span></span> |
| <span data-ttu-id="2d0f7-156">Cina orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-156">China East</span></span> |<span data-ttu-id="2d0f7-157">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-157">January 9, 2017</span></span> |<span data-ttu-id="2d0f7-158">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-158">January 13, 2017</span></span> |
| <span data-ttu-id="2d0f7-159">Cina settentrionale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-159">China North</span></span> |<span data-ttu-id="2d0f7-160">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-160">January 9, 2017</span></span> |<span data-ttu-id="2d0f7-161">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-161">January 13, 2017</span></span> |
| <span data-ttu-id="2d0f7-162">Germania centrale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-162">Germany Central</span></span> |<span data-ttu-id="2d0f7-163">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-163">January 9, 2017</span></span> |<span data-ttu-id="2d0f7-164">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-164">January 13, 2017</span></span> |
| <span data-ttu-id="2d0f7-165">Germania nord-orientale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-165">Germany Northeast</span></span> |<span data-ttu-id="2d0f7-166">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-166">January 9, 2017</span></span> |<span data-ttu-id="2d0f7-167">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-167">January 13, 2017</span></span> |
| <span data-ttu-id="2d0f7-168">India occidentale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-168">India West</span></span> |<span data-ttu-id="2d0f7-169">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-169">Not determined yet</span></span> |<span data-ttu-id="2d0f7-170">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-170">Not determined yet</span></span> |
| <span data-ttu-id="2d0f7-171">Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="2d0f7-171">Japan West</span></span> |<span data-ttu-id="2d0f7-172">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-172">Not determined yet</span></span> |<span data-ttu-id="2d0f7-173">Non ancora determinata</span><span class="sxs-lookup"><span data-stu-id="2d0f7-173">Not determined yet</span></span> |
| <span data-ttu-id="2d0f7-174">Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="2d0f7-174">North Central US</span></span> |<span data-ttu-id="2d0f7-175">9 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-175">January 9, 2017</span></span> |<span data-ttu-id="2d0f7-176">13 gennaio 2017</span><span class="sxs-lookup"><span data-stu-id="2d0f7-176">January 13, 2017</span></span> |

## <a name="self-migration-toopremium-storage"></a><span data-ttu-id="2d0f7-177">Archiviazione toopremium migrazione automatica</span><span class="sxs-lookup"><span data-stu-id="2d0f7-177">Self-migration toopremium storage</span></span>
<span data-ttu-id="2d0f7-178">Se si desidera toocontrol quando si verifica il tempo di inattività, è possibile utilizzare hello seguire passaggi toomigrate un data warehouse esistente di archiviazione toopremium archiviazione standard.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-178">If you want toocontrol when your downtime will occur, you can use hello following steps toomigrate an existing data warehouse on standard storage toopremium storage.</span></span> <span data-ttu-id="2d0f7-179">Se si sceglie questa opzione, è necessario completare la migrazione automatica hello prima di inizia la migrazione automatica hello in tale area.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-179">If you choose this option, you must complete hello self-migration before hello automatic migration begins in that region.</span></span> <span data-ttu-id="2d0f7-180">In questo modo di evitare i rischi della migrazione automatica di hello causando un conflitto (vedere toohello [pianificazione migrazione automatica][automatic migration schedule]).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-180">This ensures that you avoid any risk of hello automatic migration causing a conflict (refer toohello [automatic migration schedule][automatic migration schedule]).</span></span>

### <a name="self-migration-instructions"></a><span data-ttu-id="2d0f7-181">Istruzioni per la migrazione self-service</span><span class="sxs-lookup"><span data-stu-id="2d0f7-181">Self-migration instructions</span></span>
<span data-ttu-id="2d0f7-182">toomigrate i dati del warehouse manualmente, utilizzano hello backup e ripristino funzionalità.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-182">toomigrate your data warehouse yourself, use hello backup and restore features.</span></span> <span data-ttu-id="2d0f7-183">parte relativa al ripristino Hello della migrazione hello è previsto tootake circa un'ora per terabyte di archiviazione per data warehouse di.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-183">hello restore portion of hello migration is expected tootake around one hour per terabyte of storage per data warehouse.</span></span> <span data-ttu-id="2d0f7-184">Se si vuole hello tookeep stesso nome, al termine della migrazione, seguire hello [toorename passaggi durante la migrazione][steps toorename during migration].</span><span class="sxs-lookup"><span data-stu-id="2d0f7-184">If you want tookeep hello same name after migration is complete, follow hello [steps toorename during migration][steps toorename during migration].</span></span>

1. <span data-ttu-id="2d0f7-185">[Sospendere][Pause] il data warehouse.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-185">[Pause][Pause] your data warehouse.</span></span> <span data-ttu-id="2d0f7-186">Questa operazione richiede un backup automatico.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-186">This takes an automatic backup.</span></span>
2. <span data-ttu-id="2d0f7-187">[Eseguire il ripristino][Restore] dallo snapshot più recente.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-187">[Restore][Restore] from your most recent snapshot.</span></span>
3. <span data-ttu-id="2d0f7-188">Eliminare il data warehouse esistente in archiviazione Standard.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-188">Delete your existing data warehouse on standard storage.</span></span> <span data-ttu-id="2d0f7-189">**Se non si toodo questo passaggio, verrà addebitato entrambi i data warehouse.**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-189">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>

> [!NOTE]
> <span data-ttu-id="2d0f7-190">Hello seguenti impostazioni non vengono trasferiti durante la migrazione di hello:</span><span class="sxs-lookup"><span data-stu-id="2d0f7-190">hello following settings do not carry over as part of hello migration:</span></span>
>
> * <span data-ttu-id="2d0f7-191">Il controllo a livello di database hello deve toobe nuovamente abilitata.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-191">Auditing at hello database level needs toobe re-enabled.</span></span>
> * <span data-ttu-id="2d0f7-192">Regole del firewall a livello di database hello necessario toobe aggiunto di nuovo.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-192">Firewall rules at hello database level need toobe re-added.</span></span> <span data-ttu-id="2d0f7-193">Regole del firewall a livello di server hello non sono interessate.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-193">Firewall rules at hello server level are not affected.</span></span>
>
>

#### <a name="rename-data-warehouse-during-migration-optional"></a><span data-ttu-id="2d0f7-194">Rinominare il data warehouse durante la migrazione (facoltativa)</span><span class="sxs-lookup"><span data-stu-id="2d0f7-194">Rename data warehouse during migration (optional)</span></span>
<span data-ttu-id="2d0f7-195">Due database nella hello devono avere lo stesso server logico hello stesso nome.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-195">Two databases on hello same logical server cannot have hello same name.</span></span> <span data-ttu-id="2d0f7-196">SQL Data Warehouse supporta ora la possibilità di hello toorename un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-196">SQL Data Warehouse now supports hello ability toorename a data warehouse.</span></span>

<span data-ttu-id="2d0f7-197">In questo esempio, immaginare che il data warehouse esistente in archiviazione Standard sia attualmente denominato "MyDW".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-197">In this example, imagine that your existing data warehouse on standard storage is currently named “MyDW.”</span></span>

1. <span data-ttu-id="2d0f7-198">Rinominare "MyDW" utilizzando il comando ALTER DATABASE seguente hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-198">Rename "MyDW" by using hello following ALTER DATABASE command.</span></span> <span data-ttu-id="2d0f7-199">(In questo esempio, è possibile rinominarlo "MyDW_BeforeMigration.")  Questo comando Arresta tutte le transazioni esistenti e deve essere effettuato in hello toosucceed di database master.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-199">(In this example, we'll rename it "MyDW_BeforeMigration.")  This command stops all existing transactions, and must be done in hello master database toosucceed.</span></span>
   ```
   ALTER DATABASE CurrentDatabasename MODIFY NAME = NewDatabaseName;
   ```
2. <span data-ttu-id="2d0f7-200">[Sospendere][Pause] "MyDW_BeforeMigration."</span><span class="sxs-lookup"><span data-stu-id="2d0f7-200">[Pause][Pause] "MyDW_BeforeMigration."</span></span> <span data-ttu-id="2d0f7-201">Questa operazione richiede un backup automatico.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-201">This takes an automatic backup.</span></span>
3. <span data-ttu-id="2d0f7-202">[Ripristinare] [ Restore] dallo snapshot più recente di un nuovo database con nome hello e utilizzato toobe (ad esempio, "MyDW").</span><span class="sxs-lookup"><span data-stu-id="2d0f7-202">[Restore][Restore] from your most recent snapshot a new database with hello name it used toobe (for example, "MyDW").</span></span>
4. <span data-ttu-id="2d0f7-203">Eliminare "MyDW_BeforeMigration".</span><span class="sxs-lookup"><span data-stu-id="2d0f7-203">Delete "MyDW_BeforeMigration."</span></span> <span data-ttu-id="2d0f7-204">**Se non si toodo questo passaggio, verrà addebitato entrambi i data warehouse.**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-204">**If you fail toodo this step, you will be charged for both data warehouses.**</span></span>


## <a name="next-steps"></a><span data-ttu-id="2d0f7-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2d0f7-205">Next steps</span></span>
<span data-ttu-id="2d0f7-206">Con hello modificare toopremium archiviazione, è necessario anche un maggior numero di file di database blob nell'architettura sottostante di hello del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-206">With hello change toopremium storage, you also have an increased number of database blob files in hello underlying architecture of your data warehouse.</span></span> <span data-ttu-id="2d0f7-207">vantaggi per le prestazioni di questa modifica, toomaximize hello ricompilare gli indici columnstore cluster utilizzando lo script seguente hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-207">toomaximize hello performance benefits of this change, rebuild your clustered columnstore indexes by using hello following script.</span></span> <span data-ttu-id="2d0f7-208">script di Hello funziona forzando alcuni dei blob aggiuntive toohello di dati esistente.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-208">hello script works by forcing some of your existing data toohello additional blobs.</span></span> <span data-ttu-id="2d0f7-209">Se viene eseguita alcuna azione, dati hello naturalmente ridistribuire nel tempo quando si caricano più dati in tabelle.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-209">If you take no action, hello data will naturally redistribute over time as you load more data into your tables.</span></span>

<span data-ttu-id="2d0f7-210">**Prerequisiti:**</span><span class="sxs-lookup"><span data-stu-id="2d0f7-210">**Prerequisites:**</span></span>

- <span data-ttu-id="2d0f7-211">Hello del data warehouse deve essere eseguito con le unità di 1.000 data warehouse o versione successiva (vedere [potenza di calcolo di scala][scale compute power]).</span><span class="sxs-lookup"><span data-stu-id="2d0f7-211">hello data warehouse should run with 1,000 data warehouse units or higher (see [scale compute power][scale compute power]).</span></span>
- <span data-ttu-id="2d0f7-212">Hello utente l'esecuzione dello script hello deve trovarsi nella hello [mediumrc ruolo] [ mediumrc role] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-212">hello user executing hello script should be in hello [mediumrc role][mediumrc role] or higher.</span></span> <span data-ttu-id="2d0f7-213">un ruolo utente toothis tooadd eseguire hello:````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span><span class="sxs-lookup"><span data-stu-id="2d0f7-213">tooadd a user toothis role, execute hello following: ````EXEC sp_addrolemember 'xlargerc', 'MyUser'````</span></span>

````sql
-------------------------------------------------------------------------------
-- Step 1: Create table toocontrol index rebuild
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
-- Step 2: Execute index rebuilds. If script fails, hello below can be re-run toorestart where last left off.
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

<span data-ttu-id="2d0f7-214">Se si verificano problemi con il data warehouse, [creare un ticket di supporto] [ create a support ticket] e fare riferimento a "migrazione toopremium risorsa di archiviazione" causa possibile hello.</span><span class="sxs-lookup"><span data-stu-id="2d0f7-214">If you encounter any issues with your data warehouse, [create a support ticket][create a support ticket] and reference “migration toopremium storage” as hello possible cause.</span></span>

<!--Image references-->

<!--Article references-->
[automatic migration schedule]: #automatic-migration-schedule
[self-migration tooPremium Storage]: #self-migration-to-premium-storage
[create a support ticket]: sql-data-warehouse-get-started-create-support-ticket.md
[Azure paired region]: best-practices-availability-paired-regions.md
[main documentation site]: services/sql-data-warehouse.md
[Pause]: sql-data-warehouse-manage-compute-portal.md#pause-compute
[Restore]: sql-data-warehouse-restore-database-portal.md
[steps toorename during migration]: #optional-steps-to-rename-during-migration
[scale compute power]: sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[mediumrc role]: sql-data-warehouse-develop-concurrency.md

<!--MSDN references-->


<!--Other Web references-->
[Premium Storage for greater performance predictability]: https://azure.microsoft.com/en-us/blog/azure-sql-data-warehouse-introduces-premium-storage-for-greater-performance/
[Azure Portal]: https://portal.azure.com
