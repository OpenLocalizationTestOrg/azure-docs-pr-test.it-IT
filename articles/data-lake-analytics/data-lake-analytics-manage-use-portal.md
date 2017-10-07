---
title: portale di Azure di hello aaaManage Azure Data Lake Analitica con | Documenti Microsoft
description: Informazioni su come toomanage acounts Data Lake Analitica, dati di origini, gli utenti e i processi.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="0f976-103">Gestire Azure Data Lake Analitica con hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f976-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="0f976-104">Informazioni su come gli account di Azure Data Lake Analitica toomanage, origini dati di account, gli utenti e i processi tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f976-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="0f976-105">argomenti relativi alla gestione toosee sull'uso di altri strumenti, fare clic su una scheda nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="0f976-106">Gestire gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f976-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="0f976-107">Creare un account</span><span class="sxs-lookup"><span data-stu-id="0f976-107">Create an account</span></span>

1. <span data-ttu-id="0f976-108">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f976-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f976-109">Fare clic su **Nuovo** > **Intelligence e analisi** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0f976-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="0f976-110">Selezionare i valori per hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0f976-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="0f976-111">**Nome**: nome hello di hello account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0f976-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="0f976-112">**Sottoscrizione**: hello sottoscrizione di Azure usata per l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="0f976-113">**Gruppo di risorse**: gruppo di risorse di Azure hello in quale account hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="0f976-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="0f976-114">**Percorso**: hello Data Center di Azure per l'account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="0f976-115">**Archivio Data Lake**: hello toobe archivio predefinito utilizzato per l'account Data Lake Analitica hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="0f976-116">account archivio Azure Data Lake Hello e hello Data Lake Analitica account deve trovarsi in hello nello stesso percorso.</span><span class="sxs-lookup"><span data-stu-id="0f976-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="0f976-117">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="0f976-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="0f976-118">Eliminare un account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f976-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="0f976-119">Prima di eliminare un account di Data Lake Analytics, eliminare il relativo account di Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="0f976-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="0f976-120">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-121">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="0f976-121">Click **Delete**.</span></span>
3. <span data-ttu-id="0f976-122">Nome account hello del tipo.</span><span class="sxs-lookup"><span data-stu-id="0f976-122">Type hello account name.</span></span>
4. <span data-ttu-id="0f976-123">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="0f976-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="0f976-124">Gestire le origini dati</span><span class="sxs-lookup"><span data-stu-id="0f976-124">Manage data sources</span></span>

<span data-ttu-id="0f976-125">Data Lake Analitica supporta le seguenti origini dati hello:</span><span class="sxs-lookup"><span data-stu-id="0f976-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="0f976-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0f976-126">Data Lake Store</span></span>
* <span data-ttu-id="0f976-127">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="0f976-127">Azure Storage</span></span>

<span data-ttu-id="0f976-128">È possibile usare Esplora dati toobrowse le origini dati ed eseguire operazioni di gestione di file di base.</span><span class="sxs-lookup"><span data-stu-id="0f976-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="0f976-129">Aggiungere un'origine dati</span><span class="sxs-lookup"><span data-stu-id="0f976-129">Add a data source</span></span>

1. <span data-ttu-id="0f976-130">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-131">Fare clic su **Origini dati**.</span><span class="sxs-lookup"><span data-stu-id="0f976-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="0f976-132">Fare clic su **Aggiungi origine dati**.</span><span class="sxs-lookup"><span data-stu-id="0f976-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="0f976-133">un account archivio Data Lake tooadd, è necessario hello account toohello nome e l'accesso tooquery in grado di toobe è.</span><span class="sxs-lookup"><span data-stu-id="0f976-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="0f976-134">tooadd archiviazione Blob di Azure, è necessario che account di archiviazione hello e hello chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="0f976-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="0f976-135">toofind account di archiviazione toohello usarle, andare nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="0f976-136">Configurare le regole del firewall</span><span class="sxs-lookup"><span data-stu-id="0f976-136">Set up firewall rules</span></span>

<span data-ttu-id="0f976-137">È possibile utilizzare Data Lake Analitica toofurther bloccare l'accesso tooyour account Data Lake Analitica a livello di rete hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="0f976-138">È possibile abilitare un firewall, specificare un indirizzo IP o definire un intervallo di indirizzi IP per i client attendibili.</span><span class="sxs-lookup"><span data-stu-id="0f976-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="0f976-139">Dopo aver abilitato queste misure, solo i client che dispongono degli indirizzi IP hello intervallo hello definito possono connettersi toohello store.</span><span class="sxs-lookup"><span data-stu-id="0f976-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="0f976-140">Se altri servizi di Azure, ad esempio Data Factory di Azure o le macchine virtuali, connettono l'account Data Lake Analitica toohello, verificare che **consentire servizi Azure** sia **su**.</span><span class="sxs-lookup"><span data-stu-id="0f976-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="0f976-141">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="0f976-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="0f976-142">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-143">Scegliere hello dal menu a sinistra di hello **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="0f976-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="0f976-144">Aggiungere un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="0f976-144">Add a new user</span></span>

<span data-ttu-id="0f976-145">È possibile utilizzare hello **Aggiunta guidata utente** tooeasily effettuare il provisioning di nuovi utenti Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0f976-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="0f976-146">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-147">In hello a sinistra, sotto **Introduzione**, fare clic su **Aggiunta guidata utente**.</span><span class="sxs-lookup"><span data-stu-id="0f976-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="0f976-148">Selezionare un utente e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0f976-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="0f976-149">Selezionare un ruolo e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0f976-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="0f976-150">tooset di un nuovo toouse sviluppatore Azure Data Lake, seleziona hello **Data Lake Analitica Developer** ruolo.</span><span class="sxs-lookup"><span data-stu-id="0f976-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="0f976-151">Selezionare hello elenchi di controllo accesso (ACL) per i database hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="0f976-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="0f976-152">Dopo aver completato le selezioni, fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0f976-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="0f976-153">Selezionare gli elenchi ACL hello per file.</span><span class="sxs-lookup"><span data-stu-id="0f976-153">Select hello ACLs for files.</span></span> <span data-ttu-id="0f976-154">Per l'archivio predefinito hello, non modificare hello ACL per la cartella radice hello "/" e per la cartella /system hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="0f976-155">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="0f976-155">Click **Select**.</span></span>
7. <span data-ttu-id="0f976-156">Esaminare tutte le modifiche selezionate e quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="0f976-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="0f976-157">Al termine procedura guidata hello, fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="0f976-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="0f976-158">Gestire il controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="0f976-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="0f976-159">Analogamente ad altri servizi Azure, è possibile utilizzare toocontrol di controllo di accesso basato sui ruoli (RBAC) come gli utenti interagiscono con il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="0f976-160">ruoli RBAC standard Hello hanno hello seguenti funzionalità:</span><span class="sxs-lookup"><span data-stu-id="0f976-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="0f976-161">**Proprietario**: può inviare i processi, monitorare i processi, annullare i processi da qualsiasi utente e configurare l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="0f976-162">**Collaboratore**: può inviare i processi, monitorare i processi, annullare i processi da qualsiasi utente e configurare l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="0f976-163">**Lettore**: può monitorare i processi.</span><span class="sxs-lookup"><span data-stu-id="0f976-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="0f976-164">Usare hello Data Lake Analitica Developer tooenable U-SQL sviluppatori toouse hello Data Lake Analitica servizio ruolo.</span><span class="sxs-lookup"><span data-stu-id="0f976-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="0f976-165">È possibile utilizzare il ruolo Data Lake Analitica Developer hello per:</span><span class="sxs-lookup"><span data-stu-id="0f976-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="0f976-166">Inviare processi.</span><span class="sxs-lookup"><span data-stu-id="0f976-166">Submit jobs.</span></span>
* <span data-ttu-id="0f976-167">Monitorare lo stato di stato e hello processo dei processi inviati da qualsiasi utente.</span><span class="sxs-lookup"><span data-stu-id="0f976-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="0f976-168">Vedere script U-SQL hello i processi inviati da qualsiasi utente.</span><span class="sxs-lookup"><span data-stu-id="0f976-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="0f976-169">Annullare solo i processi creati personalmente.</span><span class="sxs-lookup"><span data-stu-id="0f976-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="0f976-170">Aggiungere utenti o gruppi di sicurezza tooa account Data Lake Analitica</span><span class="sxs-lookup"><span data-stu-id="0f976-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="0f976-171">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-172">Fare clic su **Controllo di accesso (IAM)** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="0f976-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="0f976-173">Selezionare un ruolo.</span><span class="sxs-lookup"><span data-stu-id="0f976-173">Select a role.</span></span>
4. <span data-ttu-id="0f976-174">Aggiungere un utente.</span><span class="sxs-lookup"><span data-stu-id="0f976-174">Add a user.</span></span>
5. <span data-ttu-id="0f976-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f976-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="0f976-176">Se un utente o un gruppo di sicurezza deve toosubmit processi, devono anche l'autorizzazione nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="0f976-177">Per altre informazioni, vedere [Protezione dei dati presenti in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="0f976-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="0f976-178">Gestire i processi</span><span class="sxs-lookup"><span data-stu-id="0f976-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="0f976-179">Inviare un processo</span><span class="sxs-lookup"><span data-stu-id="0f976-179">Submit a job</span></span>

1. <span data-ttu-id="0f976-180">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="0f976-181">Fare clic su **Nuovo processo**.</span><span class="sxs-lookup"><span data-stu-id="0f976-181">Click **New Job**.</span></span> <span data-ttu-id="0f976-182">Per ogni processo, configurare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="0f976-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="0f976-183">**Nome del processo**: nome hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="0f976-184">**Priorità**: i numeri più bassi hanno maggiore priorità.</span><span class="sxs-lookup"><span data-stu-id="0f976-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="0f976-185">Se i due processi sono in coda, hello con valore di priorità inferiore viene eseguito per primo.</span><span class="sxs-lookup"><span data-stu-id="0f976-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="0f976-186">**Parallelismo**: numero massimo di hello di calcolo elabora tooreserve per questo processo.</span><span class="sxs-lookup"><span data-stu-id="0f976-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="0f976-187">Fare clic su **Submit Job**.</span><span class="sxs-lookup"><span data-stu-id="0f976-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="0f976-188">Monitorare i processi</span><span class="sxs-lookup"><span data-stu-id="0f976-188">Monitor jobs</span></span>

1. <span data-ttu-id="0f976-189">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-190">Fare clic su **Visualizza tutti i processi**.</span><span class="sxs-lookup"><span data-stu-id="0f976-190">Click **View All Jobs**.</span></span> <span data-ttu-id="0f976-191">Viene visualizzato un elenco di tutti i processi di hello attive e completate di recente nell'account hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="0f976-192">Facoltativamente, fare clic su **filtro** toohelp è trovare processi hello da **intervallo di tempo**, **nome del processo**, e **autore** valori.</span><span class="sxs-lookup"><span data-stu-id="0f976-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="0f976-193">Monitoraggio dei processi della pipeline</span><span class="sxs-lookup"><span data-stu-id="0f976-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="0f976-194">I processi che fanno parte di una pipeline di lavoro, in genere in sequenza, tooaccomplish uno scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="0f976-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="0f976-195">È ad esempio possibile avere una pipeline che esegue la pulizia, estrae, trasforma, e aggrega l'utilizzo per Customer Insights.</span><span class="sxs-lookup"><span data-stu-id="0f976-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="0f976-196">I processi di pipeline vengono identificati utilizzando proprietà "Pipeline" hello, quando è stato inviato il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="0f976-197">Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0f976-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="0f976-198">tooview un elenco di processi U-SQL che fanno parte della pipeline:</span><span class="sxs-lookup"><span data-stu-id="0f976-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="0f976-199">Nel portale di Azure hello, andare account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="0f976-200">Fare clic su **Informazioni dettagliate sul processo**.</span><span class="sxs-lookup"><span data-stu-id="0f976-200">Click **Job Insights**.</span></span> <span data-ttu-id="0f976-201">Hello che scheda "Tutti i processi" verrà automaticamente modificata, che mostra un elenco di esecuzione, in coda e i processi di fine.</span><span class="sxs-lookup"><span data-stu-id="0f976-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="0f976-202">Fare clic su hello **processi Pipeline** scheda. Verrà visualizzato un elenco di processi della pipeline, con statistiche aggregate per ogni pipeline.</span><span class="sxs-lookup"><span data-stu-id="0f976-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="0f976-203">Monitoraggio dei processi ricorrenti</span><span class="sxs-lookup"><span data-stu-id="0f976-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="0f976-204">Un processo ricorrente è quello che ha hello stessa logica di business ma utilizza dati di input diversi ogni volta che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="0f976-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="0f976-205">Idealmente, devono sempre avere esito positivo e i processi ricorrenti con tempo di esecuzione relativamente stabile; monitoraggio di questi comportamenti consente di verificare che il processo di hello sia integro.</span><span class="sxs-lookup"><span data-stu-id="0f976-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="0f976-206">I processi ricorrenti vengono identificati utilizzando proprietà di "Recurrence" hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="0f976-207">Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="0f976-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="0f976-208">un elenco di processi U-SQL che sono ricorrenti tooview:</span><span class="sxs-lookup"><span data-stu-id="0f976-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="0f976-209">Nel portale di Azure hello, andare account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="0f976-210">Fare clic su **Informazioni dettagliate sul processo**.</span><span class="sxs-lookup"><span data-stu-id="0f976-210">Click **Job Insights**.</span></span> <span data-ttu-id="0f976-211">Hello che scheda "Tutti i processi" verrà automaticamente modificata, che mostra un elenco di esecuzione, in coda e i processi di fine.</span><span class="sxs-lookup"><span data-stu-id="0f976-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="0f976-212">Fare clic su hello **processi ricorrenti** scheda. Verrà visualizzato un elenco di processi ricorrenti, con statistiche aggregate per ogni processo.</span><span class="sxs-lookup"><span data-stu-id="0f976-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="0f976-213">Gestire i criteri</span><span class="sxs-lookup"><span data-stu-id="0f976-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="0f976-214">Criteri a livello di account</span><span class="sxs-lookup"><span data-stu-id="0f976-214">Account-level policies</span></span>

<span data-ttu-id="0f976-215">Questi criteri si applicano i processi di tooall in un account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0f976-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="0f976-216">Numero massimo di unità di analisi in un account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f976-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="0f976-217">Un criterio hello indica quante unità Analitica (Australia) può utilizzare l'account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0f976-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="0f976-218">Per impostazione predefinita, il valore di hello è too250.</span><span class="sxs-lookup"><span data-stu-id="0f976-218">By default, hello value is set too250.</span></span> <span data-ttu-id="0f976-219">Ad esempio, se questo valore è impostato too250 Australia, è possibile fare un processo in esecuzione con 250 tooit AUs assegnato o 10 processi in esecuzione con 25 AUs ogni.</span><span class="sxs-lookup"><span data-stu-id="0f976-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="0f976-220">Processi aggiuntivi che vengono inviati vengono messe in coda finché non vengono completati i processi in esecuzione hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="0f976-221">Completamento dei processi in esecuzione, AUs vengono liberate per hello in coda toorun processi.</span><span class="sxs-lookup"><span data-stu-id="0f976-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="0f976-222">numero hello toochange di AUs per l'account Data Lake Analitica:</span><span class="sxs-lookup"><span data-stu-id="0f976-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="0f976-223">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-224">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0f976-224">Click **Properties**.</span></span>
3. <span data-ttu-id="0f976-225">In **AUs massimo**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="0f976-226">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0f976-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0f976-227">Se è necessario più di hello predefinito (250) Australia, nel portale di hello, fare clic su **+ supporto** toosubmit una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="0f976-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="0f976-228">numero di Hello di AUs disponibili nell'account Data Lake Analitica può essere aumentato.</span><span class="sxs-lookup"><span data-stu-id="0f976-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="0f976-229">Numero massimo di processi che possono essere eseguiti contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="0f976-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="0f976-230">Un criterio controlla il numero di processi è possibile eseguire in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="0f976-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="0f976-231">Per impostazione predefinita, questo valore è impostato too20.</span><span class="sxs-lookup"><span data-stu-id="0f976-231">By default, this value is set too20.</span></span> <span data-ttu-id="0f976-232">Se il Analitica Lake dati include AUs disponibili, nuovi processi sono pianificati toorun immediatamente finché il numero totale di hello di processi in esecuzione raggiunge il valore di hello dei criteri.</span><span class="sxs-lookup"><span data-stu-id="0f976-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="0f976-233">Quando si raggiunge hello il numero massimo di processi che possono essere eseguite contemporaneamente, i processi successivi vengono accodati in ordine di priorità fino al completamento di uno o più processi in esecuzione (a seconda della disponibilità di aggiornamenti automatici).</span><span class="sxs-lookup"><span data-stu-id="0f976-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="0f976-234">numero di hello toochange di processi che possono essere eseguite contemporaneamente:</span><span class="sxs-lookup"><span data-stu-id="0f976-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="0f976-235">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-236">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0f976-236">Click **Properties**.</span></span>
3. <span data-ttu-id="0f976-237">In **numero massimo di processi in esecuzione**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="0f976-238">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0f976-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="0f976-239">Se è necessario più di hello numero (20) predefinito dei processi, nel portale di hello, fare clic su toorun **+ supporto** toosubmit una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="0f976-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="0f976-240">numero di Hello dei processi che è possibile eseguire contemporaneamente l'account Data Lake Analitica può essere aumentato.</span><span class="sxs-lookup"><span data-stu-id="0f976-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="0f976-241">Quanto tempo i metadati del processo tookeep e risorse</span><span class="sxs-lookup"><span data-stu-id="0f976-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="0f976-242">Quando gli utenti eseguono processi U-SQL, il servizio Data Lake Analitica hello mantiene tutti i file correlati.</span><span class="sxs-lookup"><span data-stu-id="0f976-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="0f976-243">I file correlati includono script hello U-SQL, file DLL hello a cui fa riferimento in script hello U-SQL, risorse compilate e statistiche.</span><span class="sxs-lookup"><span data-stu-id="0f976-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="0f976-244">file Hello sono nella cartella /system/ hello dell'account di archiviazione di Azure Data Lake hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="0f976-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="0f976-245">Questo criterio controlla per quanto tempo queste risorse si trovano prima di essere eliminati automaticamente (valore predefinito di hello è 30 giorni).</span><span class="sxs-lookup"><span data-stu-id="0f976-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="0f976-246">È possibile utilizzare questi file per il debug e per ottimizzare le prestazioni dei processi che saranno nuovamente in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="0f976-247">toochange quanto tempo i metadati del processo tookeep e risorse:</span><span class="sxs-lookup"><span data-stu-id="0f976-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="0f976-248">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-249">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0f976-249">Click **Properties**.</span></span>
3. <span data-ttu-id="0f976-250">In **giorni tooRetain processo query**, spostare hello dispositivo di scorrimento tooselect un valore o immettere il valore di hello nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="0f976-251">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="0f976-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="0f976-252">Criteri a livello di processo</span><span class="sxs-lookup"><span data-stu-id="0f976-252">Job-level policies</span></span>
<span data-ttu-id="0f976-253">Con i criteri a livello di processo, è possibile controllare hello AUs massimo e hello priorità massima che singoli utenti (o i membri di gruppi di sicurezza specifici) è possono impostare per i processi che hanno inviato personalmente.</span><span class="sxs-lookup"><span data-stu-id="0f976-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="0f976-254">Questo consente di controllare i costi di hello sostenuti dagli utenti.</span><span class="sxs-lookup"><span data-stu-id="0f976-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="0f976-255">Consente inoltre di effetto hello controllo che i processi pianificati con priorità alta potrebbe essere processi di produzione che sono in esecuzione hello stesso account Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="0f976-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="0f976-256">Data Lake Analitica presenta due criteri che è possibile impostare a livello di processo hello:</span><span class="sxs-lookup"><span data-stu-id="0f976-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="0f976-257">**Limite massimo di aggiornamenti automatici per processo**: agli utenti di inviare solo i processi con numero toothis di Australia.</span><span class="sxs-lookup"><span data-stu-id="0f976-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="0f976-258">Per impostazione predefinita, questo limite è hello come hello Australia massimo per l'account di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="0f976-259">**Priorità**: agli utenti di inviare solo i processi che hanno un valore di priorità toothis inferiori o uguali.</span><span class="sxs-lookup"><span data-stu-id="0f976-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="0f976-260">Si noti che un numero più alto indica una priorità più bassa.</span><span class="sxs-lookup"><span data-stu-id="0f976-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="0f976-261">Per impostazione predefinita, questo viene impostato too1, hello più alto possibile di priorità.</span><span class="sxs-lookup"><span data-stu-id="0f976-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="0f976-262">Per ogni account è impostato un criterio predefinito</span><span class="sxs-lookup"><span data-stu-id="0f976-262">There is a default policy set on every account.</span></span> <span data-ttu-id="0f976-263">criteri predefiniti Hello applicano tooall gli utenti dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="0f976-264">È possibile impostare altri criteri per utenti e gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="0f976-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="0f976-265">I criteri a livello di account e quelli a livello di processo vengono applicati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="0f976-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="0f976-266">Aggiungere un criterio per un utente o un gruppo specifico</span><span class="sxs-lookup"><span data-stu-id="0f976-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="0f976-267">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-268">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0f976-268">Click **Properties**.</span></span>
3. <span data-ttu-id="0f976-269">In **limiti invio processo**, fare clic su hello **Aggiungi criterio** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0f976-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="0f976-270">Quindi, selezionare o immettere hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="0f976-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="0f976-271">**Nome del criterio di calcolo**: immettere un nome di criterio, tooremind di scopo hello del criterio di hello.</span><span class="sxs-lookup"><span data-stu-id="0f976-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="0f976-272">**Seleziona utente o gruppo**: selezionare utente hello o un gruppo a cui si applica questo criterio.</span><span class="sxs-lookup"><span data-stu-id="0f976-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="0f976-273">**Impostare hello processo Australia limite**: limite di hello Australia che applica toohello selezionato utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="0f976-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="0f976-274">**Impostare il limite di priorità hello**: hello priorità limite che applica toohello selezionato utente o gruppo.</span><span class="sxs-lookup"><span data-stu-id="0f976-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="0f976-275">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f976-275">Click **Ok**.</span></span>

5. <span data-ttu-id="0f976-276">il nuovo criterio di Hello è elencato nella hello **predefinito** in Criteri di tabella **limiti di processo di invio**.</span><span class="sxs-lookup"><span data-stu-id="0f976-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="0f976-277">Eliminare o modificare un criterio esistente</span><span class="sxs-lookup"><span data-stu-id="0f976-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="0f976-278">Nel portale di Azure hello, visitare l'account Data Lake Analitica tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f976-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="0f976-279">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="0f976-279">Click **Properties**.</span></span>
3. <span data-ttu-id="0f976-280">In **limiti invio processo**, criteri di ricerca hello desiderato tooedit.</span><span class="sxs-lookup"><span data-stu-id="0f976-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="0f976-281">hello toosee **eliminare** e **modifica** fare clic su Opzioni, nella colonna più a destra di hello della tabella di hello, **...** .</span><span class="sxs-lookup"><span data-stu-id="0f976-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="0f976-282">Risorse aggiuntive per i criteri dei processi</span><span class="sxs-lookup"><span data-stu-id="0f976-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="0f976-283">Post di blog con una panoramica dei criteri</span><span class="sxs-lookup"><span data-stu-id="0f976-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="0f976-284">Post di blog sui criteri a livello di account</span><span class="sxs-lookup"><span data-stu-id="0f976-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="0f976-285">Post di blog sui criteri a livello di processo</span><span class="sxs-lookup"><span data-stu-id="0f976-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="0f976-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f976-286">Next steps</span></span>

* [<span data-ttu-id="0f976-287">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f976-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0f976-288">Introduzione a Data Lake Analitica utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f976-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0f976-289">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f976-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

