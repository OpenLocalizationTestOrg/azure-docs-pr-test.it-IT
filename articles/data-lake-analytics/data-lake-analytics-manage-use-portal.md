---
title: Gestire Azure Data Lake Analytics tramite il portale di Azure | Microsoft Docs
description: Informazioni su come gestire account, origini dati, utenti e processi di Data Lake Analytics.
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
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="da645-103">Gestire Azure Data Lake Analytics tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="da645-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="da645-104">Informazioni su come gestire gli account, le origini dati degli account, gli utenti e i processi di Azure Data Lake Analytics usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="da645-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="da645-105">Per visualizzare gli argomenti di gestione sull'uso di altri strumenti, fare clic su una scheda nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="da645-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="da645-106">Gestire gli account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da645-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="da645-107">Creare un account</span><span class="sxs-lookup"><span data-stu-id="da645-107">Create an account</span></span>

1. <span data-ttu-id="da645-108">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="da645-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="da645-109">Fare clic su **Nuovo** > **Intelligence e analisi** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="da645-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="da645-110">Selezionare i valori per gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="da645-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="da645-111">**Nome**: nome dell'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="da645-112">**Sottoscrizione**: sottoscrizione di Azure usata per l'account.</span><span class="sxs-lookup"><span data-stu-id="da645-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="da645-113">**Gruppo di risorse**: gruppo di risorse di Azure in cui creare l'account.</span><span class="sxs-lookup"><span data-stu-id="da645-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="da645-114">**Posizione**: data center di Azure per l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="da645-115">**Data Lake Store**: archivio predefinito da usare per l'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="da645-116">L'account di Azure Data Lake Store e quello di Data Lake Analytics devono trovarsi nella stessa posizione.</span><span class="sxs-lookup"><span data-stu-id="da645-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="da645-117">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="da645-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="da645-118">Eliminare un account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da645-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="da645-119">Prima di eliminare un account di Data Lake Analytics, eliminare il relativo account di Data Lake Store predefinito.</span><span class="sxs-lookup"><span data-stu-id="da645-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="da645-120">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-121">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="da645-121">Click **Delete**.</span></span>
3. <span data-ttu-id="da645-122">Digitare il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="da645-122">Type the account name.</span></span>
4. <span data-ttu-id="da645-123">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="da645-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="da645-124">Gestire le origini dati</span><span class="sxs-lookup"><span data-stu-id="da645-124">Manage data sources</span></span>

<span data-ttu-id="da645-125">Data Lake Analytics supporta le origini dati seguenti:</span><span class="sxs-lookup"><span data-stu-id="da645-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="da645-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="da645-126">Data Lake Store</span></span>
* <span data-ttu-id="da645-127">Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="da645-127">Azure Storage</span></span>

<span data-ttu-id="da645-128">Per esplorare le origini dati ed eseguire operazioni di gestione dei file di base è possibile usare Esplora dati.</span><span class="sxs-lookup"><span data-stu-id="da645-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="da645-129">Aggiungere un'origine dati</span><span class="sxs-lookup"><span data-stu-id="da645-129">Add a data source</span></span>

1. <span data-ttu-id="da645-130">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-131">Fare clic su **Origini dati**.</span><span class="sxs-lookup"><span data-stu-id="da645-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="da645-132">Fare clic su **Aggiungi origine dati**.</span><span class="sxs-lookup"><span data-stu-id="da645-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="da645-133">Per aggiungere un account di Data Lake Store, sono necessari il nome dell'account e i diritti di accesso all'account per poter eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="da645-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="da645-134">Per aggiungere una risorsa di archiviazione BLOB di Azure, sono necessari l'account di archiviazione e la chiave dell'account.</span><span class="sxs-lookup"><span data-stu-id="da645-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="da645-135">Per trovarli, passare all'account di archiviazione nel portale.</span><span class="sxs-lookup"><span data-stu-id="da645-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="da645-136">Configurare le regole del firewall</span><span class="sxs-lookup"><span data-stu-id="da645-136">Set up firewall rules</span></span>

<span data-ttu-id="da645-137">È possibile usare Data Lake Analytics per bloccare ulteriormente l'accesso all'account di Data Lake Analytics a livello di rete.</span><span class="sxs-lookup"><span data-stu-id="da645-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="da645-138">È possibile abilitare un firewall, specificare un indirizzo IP o definire un intervallo di indirizzi IP per i client attendibili.</span><span class="sxs-lookup"><span data-stu-id="da645-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="da645-139">Dopo aver configurato queste regole, solo i client con indirizzo IP compreso nell'intervallo definito potranno connettersi all'archivio.</span><span class="sxs-lookup"><span data-stu-id="da645-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="da645-140">Se altri servizi di Azure, come Azure Data Factory o Macchine virtuali, si connettono all'account di Data Lake Analytics, verificare che l'opzione **Consenti ai servizi di Azure di accedere al server** sia **attivata**.</span><span class="sxs-lookup"><span data-stu-id="da645-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="da645-141">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="da645-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="da645-142">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-143">Nel menu a sinistra fare clic su **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="da645-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="da645-144">Aggiungere un nuovo utente</span><span class="sxs-lookup"><span data-stu-id="da645-144">Add a new user</span></span>

<span data-ttu-id="da645-145">È possibile usare l'**Aggiunta guidata utente** per effettuare facilmente il provisioning di nuovi utenti di Data Lake.</span><span class="sxs-lookup"><span data-stu-id="da645-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="da645-146">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-147">A sinistra, sotto **Attività iniziali**, fare clic su **Aggiunta guidata utente**.</span><span class="sxs-lookup"><span data-stu-id="da645-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="da645-148">Selezionare un utente e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="da645-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="da645-149">Selezionare un ruolo e quindi fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="da645-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="da645-150">Per configurare un nuovo sviluppatore per Azure Data Lake, selezionare il ruolo **Sviluppatore di Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="da645-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="da645-151">Selezionare gli elenchi di controllo di accesso (ACL) per i database U-SQL.</span><span class="sxs-lookup"><span data-stu-id="da645-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="da645-152">Dopo aver completato le selezioni, fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="da645-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="da645-153">Selezionare gli elenchi ACL per i file.</span><span class="sxs-lookup"><span data-stu-id="da645-153">Select the ACLs for files.</span></span> <span data-ttu-id="da645-154">Per l'archivio predefinito, non modificare gli elenchi ACL per la cartella radice "/" e per la cartella /system.</span><span class="sxs-lookup"><span data-stu-id="da645-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="da645-155">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="da645-155">Click **Select**.</span></span>
7. <span data-ttu-id="da645-156">Esaminare tutte le modifiche selezionate e quindi fare clic su **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="da645-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="da645-157">Al termine della procedura guidata, fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="da645-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="da645-158">Gestire il controllo degli accessi in base al ruolo</span><span class="sxs-lookup"><span data-stu-id="da645-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="da645-159">Come per altri servizi di Azure, è possibile usare il controllo degli accessi in base al ruolo (RBAC, Role-Based Access Control) per controllare il modo con cui gli utenti interagiscono con il servizio.</span><span class="sxs-lookup"><span data-stu-id="da645-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="da645-160">I ruoli RBAC standard offrono le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="da645-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="da645-161">**Proprietario**: può inviare e monitorare i processi, annullarli da qualsiasi utente e configurare l'account.</span><span class="sxs-lookup"><span data-stu-id="da645-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="da645-162">**Collaboratore**: può inviare e monitorare i processi, annullarli da qualsiasi utente e configurare l'account.</span><span class="sxs-lookup"><span data-stu-id="da645-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="da645-163">**Lettore**: può monitorare i processi.</span><span class="sxs-lookup"><span data-stu-id="da645-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="da645-164">Usare il ruolo Sviluppatore di Data Lake Analytics per consentire agli sviluppatori di U-SQL di usare il servizio Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="da645-165">È possibile usare il ruolo Sviluppatore di Data Lake Analytics per eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="da645-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="da645-166">Inviare processi.</span><span class="sxs-lookup"><span data-stu-id="da645-166">Submit jobs.</span></span>
* <span data-ttu-id="da645-167">Monitorare lo stato e l'avanzamento dei processi inviati da qualsiasi utente.</span><span class="sxs-lookup"><span data-stu-id="da645-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="da645-168">Vedere gli script U-SQL relativi ai processi inviati da qualsiasi utente.</span><span class="sxs-lookup"><span data-stu-id="da645-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="da645-169">Annullare solo i processi creati personalmente.</span><span class="sxs-lookup"><span data-stu-id="da645-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="da645-170">Aggiungere utenti o gruppi di sicurezza a un account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da645-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="da645-171">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-172">Fare clic su **Controllo di accesso (IAM)** > **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="da645-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="da645-173">Selezionare un ruolo.</span><span class="sxs-lookup"><span data-stu-id="da645-173">Select a role.</span></span>
4. <span data-ttu-id="da645-174">Aggiungere un utente.</span><span class="sxs-lookup"><span data-stu-id="da645-174">Add a user.</span></span>
5. <span data-ttu-id="da645-175">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="da645-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="da645-176">Se un utente o un gruppo di sicurezza vuole inviare processi, deve disporre anche dell'autorizzazione sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="da645-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="da645-177">Per altre informazioni, vedere [Protezione dei dati presenti in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="da645-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="da645-178">Gestire i processi</span><span class="sxs-lookup"><span data-stu-id="da645-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="da645-179">Inviare un processo</span><span class="sxs-lookup"><span data-stu-id="da645-179">Submit a job</span></span>

1. <span data-ttu-id="da645-180">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="da645-181">Fare clic su **Nuovo processo**.</span><span class="sxs-lookup"><span data-stu-id="da645-181">Click **New Job**.</span></span> <span data-ttu-id="da645-182">Per ogni processo, configurare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="da645-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="da645-183">**Nome processo**: nome del processo.</span><span class="sxs-lookup"><span data-stu-id="da645-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="da645-184">**Priorità**: i numeri più bassi hanno maggiore priorità.</span><span class="sxs-lookup"><span data-stu-id="da645-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="da645-185">Se due processi sono in coda, verrà eseguito per primo quello con la priorità più bassa.</span><span class="sxs-lookup"><span data-stu-id="da645-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="da645-186">**Parallelismo**: numero massimo di processi di calcolo da riservare per il processo.</span><span class="sxs-lookup"><span data-stu-id="da645-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="da645-187">Fare clic su **Invia processo**.</span><span class="sxs-lookup"><span data-stu-id="da645-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="da645-188">Monitorare i processi</span><span class="sxs-lookup"><span data-stu-id="da645-188">Monitor jobs</span></span>

1. <span data-ttu-id="da645-189">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-190">Fare clic su **Visualizza tutti i processi**.</span><span class="sxs-lookup"><span data-stu-id="da645-190">Click **View All Jobs**.</span></span> <span data-ttu-id="da645-191">Viene visualizzato un elenco di tutti i processi attivi e completati di recente nell'account.</span><span class="sxs-lookup"><span data-stu-id="da645-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="da645-192">Facoltativamente, fare clic su **Filtra** per trovare i processi in base ai valori di **Intervallo di tempo**, **Nome processo** e **Autore**.</span><span class="sxs-lookup"><span data-stu-id="da645-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="da645-193">Monitoraggio dei processi della pipeline</span><span class="sxs-lookup"><span data-stu-id="da645-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="da645-194">I processi che fanno parte di una pipeline funzionano insieme, in genere in sequenza, per realizzare uno scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="da645-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="da645-195">È ad esempio possibile avere una pipeline che esegue la pulizia, estrae, trasforma, e aggrega l'utilizzo per Customer Insights.</span><span class="sxs-lookup"><span data-stu-id="da645-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="da645-196">I processi della pipeline vengono identificati mediante la proprietà "Pipeline" al momento dell'invio del processo.</span><span class="sxs-lookup"><span data-stu-id="da645-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="da645-197">Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="da645-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="da645-198">Per visualizzare un elenco di processi U-SQL che fanno parte delle pipeline:</span><span class="sxs-lookup"><span data-stu-id="da645-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="da645-199">Nel portale di Azure accedere agli account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="da645-200">Fare clic su **Informazioni dettagliate sul processo**.</span><span class="sxs-lookup"><span data-stu-id="da645-200">Click **Job Insights**.</span></span> <span data-ttu-id="da645-201">Verrà aperta per impostazione predefinita la scheda "Tutti i processi", che mostra un elenco di processi in esecuzione, in coda e terminati.</span><span class="sxs-lookup"><span data-stu-id="da645-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="da645-202">Fare clic sulla scheda **Processi della pipeline**. Verrà visualizzato un elenco di processi della pipeline, con statistiche aggregate per ogni pipeline.</span><span class="sxs-lookup"><span data-stu-id="da645-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="da645-203">Monitoraggio dei processi ricorrenti</span><span class="sxs-lookup"><span data-stu-id="da645-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="da645-204">Un processo ricorrente è un processo che ha la stessa logica di business, ma usa dati di input diversi ogni volta che viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="da645-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="da645-205">Idealmente, i processi ricorrenti devono avere sempre esito positivo e un tempo di esecuzione relativamente stabile. Il monitoraggio di questi comportamenti aiuta ad assicurarsi che il processo sia integro.</span><span class="sxs-lookup"><span data-stu-id="da645-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="da645-206">I processi ricorrenti vengono identificati mediante la proprietà "Recurrence".</span><span class="sxs-lookup"><span data-stu-id="da645-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="da645-207">Per i processi pianificati usando ADF V2 questa proprietà viene popolata automaticamente.</span><span class="sxs-lookup"><span data-stu-id="da645-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="da645-208">Per visualizzare un elenco di processi U-SQL ricorrenti:</span><span class="sxs-lookup"><span data-stu-id="da645-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="da645-209">Nel portale di Azure accedere agli account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="da645-210">Fare clic su **Informazioni dettagliate sul processo**.</span><span class="sxs-lookup"><span data-stu-id="da645-210">Click **Job Insights**.</span></span> <span data-ttu-id="da645-211">Verrà aperta per impostazione predefinita la scheda "Tutti i processi", che mostra un elenco di processi in esecuzione, in coda e terminati.</span><span class="sxs-lookup"><span data-stu-id="da645-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="da645-212">Fare clic sulla scheda **Processi ricorrenti**. Verrà visualizzato un elenco di processi ricorrenti, con statistiche aggregate per ogni processo.</span><span class="sxs-lookup"><span data-stu-id="da645-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="da645-213">Gestire i criteri</span><span class="sxs-lookup"><span data-stu-id="da645-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="da645-214">Criteri a livello di account</span><span class="sxs-lookup"><span data-stu-id="da645-214">Account-level policies</span></span>

<span data-ttu-id="da645-215">Questi criteri si applicano a tutti i processi in un account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="da645-216">Numero massimo di unità di analisi in un account di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da645-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="da645-217">Un criterio controlla il numero totale di unità di analisi (AU, Analytics Unit) che possono essere usate dall'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="da645-218">Per impostazione predefinita, il valore è impostato su 250.</span><span class="sxs-lookup"><span data-stu-id="da645-218">By default, the value is set to 250.</span></span> <span data-ttu-id="da645-219">Se ad esempio sono impostate 250 AU, è possibile eseguire un processo a cui sono assegnate 250 AU oppure 10 processi con 25 AU ciascuno.</span><span class="sxs-lookup"><span data-stu-id="da645-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="da645-220">Gli altri processi inviati vengono inseriti in coda finché i processi in esecuzione non vengono completati.</span><span class="sxs-lookup"><span data-stu-id="da645-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="da645-221">Al termine di questi processi, le AU vengono rese disponibili per consentire l'esecuzione dei processi in coda.</span><span class="sxs-lookup"><span data-stu-id="da645-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="da645-222">Per modificare il numero di AU per l'account di Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="da645-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="da645-223">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-224">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da645-224">Click **Properties**.</span></span>
3. <span data-ttu-id="da645-225">In **Numero massimo di AU** spostare il dispositivo di scorrimento per selezionare un valore o immettere il valore nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="da645-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="da645-226">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="da645-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="da645-227">Se è necessario impostare un numero di AU superiore al valore predefinito (250), nel portale fare clic su **Guida e supporto** per inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="da645-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="da645-228">Il numero di AU disponibili nell'account di Data Lake Analytics può essere incrementato.</span><span class="sxs-lookup"><span data-stu-id="da645-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="da645-229">Numero massimo di processi che possono essere eseguiti contemporaneamente</span><span class="sxs-lookup"><span data-stu-id="da645-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="da645-230">Un criterio controlla il numero di processi che possono essere eseguiti contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="da645-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="da645-231">Per impostazione predefinita, questo valore è impostato su 20.</span><span class="sxs-lookup"><span data-stu-id="da645-231">By default, this value is set to 20.</span></span> <span data-ttu-id="da645-232">Se in Data Lake Analytics sono presenti AU disponibili, viene pianificata l'esecuzione di nuovi processi finché il numero totale dei processi in esecuzione non raggiunge il valore di questo criterio.</span><span class="sxs-lookup"><span data-stu-id="da645-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="da645-233">Quando si raggiunge il numero massimo di processi che possono essere eseguiti contemporaneamente, i processi successivi vengono inseriti in coda, in ordine di priorità, finché uno o più processi non vengono completati (a seconda della disponibilità di AU).</span><span class="sxs-lookup"><span data-stu-id="da645-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="da645-234">Per modificare il numero di processi che possono essere eseguiti contemporaneamente:</span><span class="sxs-lookup"><span data-stu-id="da645-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="da645-235">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-236">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da645-236">Click **Properties**.</span></span>
3. <span data-ttu-id="da645-237">In **Numero massimo di processi in esecuzione** spostare il dispositivo di scorrimento per selezionare un valore o immettere il valore nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="da645-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="da645-238">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="da645-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="da645-239">Se è necessario eseguire un numero di processi superiore al valore predefinito (20), nel portale fare clic su **Guida e supporto** per inviare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="da645-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="da645-240">Il numero di processi che possono essere eseguiti contemporaneamente nell'account di Data Lake Analytics può essere incrementato.</span><span class="sxs-lookup"><span data-stu-id="da645-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="da645-241">Per quanto tempo mantenere le risorse e i metadati dei processi</span><span class="sxs-lookup"><span data-stu-id="da645-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="da645-242">Quando gli utenti eseguono processi U-SQL, il servizio Data Lake Analytics mantiene tutti i file correlati,</span><span class="sxs-lookup"><span data-stu-id="da645-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="da645-243">ovvero lo script U-SQL, i file DLL a cui viene fatto riferimento nello script U-SQL, le risorse compilate e le statistiche.</span><span class="sxs-lookup"><span data-stu-id="da645-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="da645-244">I file si trovano nella cartella /system/ dell'account di Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="da645-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="da645-245">Questo criterio controlla per quanto tempo le risorse rimangono archiviate prima di essere eliminate automaticamente. Il valore predefinito è 30 giorni.</span><span class="sxs-lookup"><span data-stu-id="da645-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="da645-246">È possibile usare questi file per il debug e per ottimizzare le prestazioni dei processi che si eseguiranno nuovamente in futuro.</span><span class="sxs-lookup"><span data-stu-id="da645-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="da645-247">Per modificare il tempo di archiviazione delle risorse e dei metadati dei processi:</span><span class="sxs-lookup"><span data-stu-id="da645-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="da645-248">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-249">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da645-249">Click **Properties**.</span></span>
3. <span data-ttu-id="da645-250">In **Giorni di conservazione delle query del processo** spostare il dispositivo di scorrimento per selezionare un valore o immettere il valore nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="da645-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="da645-251">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="da645-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="da645-252">Criteri a livello di processo</span><span class="sxs-lookup"><span data-stu-id="da645-252">Job-level policies</span></span>
<span data-ttu-id="da645-253">Con i criteri a livello di processo è possibile controllare il numero massimo di AU e la massima priorità che i singoli utenti (o i membri di specifici gruppi di sicurezza) possono impostare per i processi che inviano.</span><span class="sxs-lookup"><span data-stu-id="da645-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="da645-254">Ciò consente di controllare i costi sostenuti dagli utenti</span><span class="sxs-lookup"><span data-stu-id="da645-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="da645-255">e l'effetto che i processi pianificati possono avere sui processi di produzione ad alta priorità in esecuzione nello stesso account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="da645-256">In Data Lake Analytics è possibile impostare due criteri a livello di processo:</span><span class="sxs-lookup"><span data-stu-id="da645-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="da645-257">**AU limit per job** (Limite AU per processo): gli utenti possono inviare solo processi che hanno al massimo il numero di AU specificato.</span><span class="sxs-lookup"><span data-stu-id="da645-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="da645-258">Per impostazione predefinita, questo limite corrisponde a quello definito per l'account.</span><span class="sxs-lookup"><span data-stu-id="da645-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="da645-259">**Priorità**: gli utenti possono inviare solo processi che hanno una priorità inferiore o uguale a questo valore.</span><span class="sxs-lookup"><span data-stu-id="da645-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="da645-260">Si noti che un numero più alto indica una priorità più bassa.</span><span class="sxs-lookup"><span data-stu-id="da645-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="da645-261">Per impostazione predefinita, questo valore è impostato su 1, che corrisponde alla massima priorità possibile.</span><span class="sxs-lookup"><span data-stu-id="da645-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="da645-262">Per ogni account è impostato un criterio predefinito</span><span class="sxs-lookup"><span data-stu-id="da645-262">There is a default policy set on every account.</span></span> <span data-ttu-id="da645-263">che si applica a tutti gli utenti dell'account.</span><span class="sxs-lookup"><span data-stu-id="da645-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="da645-264">È possibile impostare altri criteri per utenti e gruppi specifici.</span><span class="sxs-lookup"><span data-stu-id="da645-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="da645-265">I criteri a livello di account e quelli a livello di processo vengono applicati contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="da645-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="da645-266">Aggiungere un criterio per un utente o un gruppo specifico</span><span class="sxs-lookup"><span data-stu-id="da645-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="da645-267">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-268">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da645-268">Click **Properties**.</span></span>
3. <span data-ttu-id="da645-269">In **Limiti di invio del processo** fare clic sul pulsante **Aggiungi criterio**.</span><span class="sxs-lookup"><span data-stu-id="da645-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="da645-270">Selezionare o immettere le impostazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="da645-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="da645-271">**Nome criteri di calcolo**: immettere un nome di criterio in modo da identificarne la finalità.</span><span class="sxs-lookup"><span data-stu-id="da645-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="da645-272">**Selezionare l'utente o il gruppo**: selezionare l'utente o il gruppo a cui si applica questo criterio.</span><span class="sxs-lookup"><span data-stu-id="da645-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="da645-273">**Impostare il limite AU del processo**: impostare il limite di AU che si applica all'utente o al gruppo selezionato.</span><span class="sxs-lookup"><span data-stu-id="da645-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="da645-274">**Impostare il limite di priorità del processo**: impostare il limite di priorità che si applica all'utente o al gruppo selezionato.</span><span class="sxs-lookup"><span data-stu-id="da645-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="da645-275">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="da645-275">Click **Ok**.</span></span>

5. <span data-ttu-id="da645-276">Il nuovo criterio viene elencato nella tabella dei criteri **Impostazioni predefinite** in **Limiti di invio del processo**.</span><span class="sxs-lookup"><span data-stu-id="da645-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="da645-277">Eliminare o modificare un criterio esistente</span><span class="sxs-lookup"><span data-stu-id="da645-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="da645-278">Nel portale di Azure accedere all'account di Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="da645-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="da645-279">Fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da645-279">Click **Properties**.</span></span>
3. <span data-ttu-id="da645-280">In **Limiti di invio del processo** trovare il criterio da modificare.</span><span class="sxs-lookup"><span data-stu-id="da645-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="da645-281">Per visualizzare le opzioni **Elimina** e **Modifica**, nella colonna all'estremità destra della tabella fare clic su **...**.</span><span class="sxs-lookup"><span data-stu-id="da645-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="da645-282">Risorse aggiuntive per i criteri dei processi</span><span class="sxs-lookup"><span data-stu-id="da645-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="da645-283">Post di blog con una panoramica dei criteri</span><span class="sxs-lookup"><span data-stu-id="da645-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="da645-284">Post di blog sui criteri a livello di account</span><span class="sxs-lookup"><span data-stu-id="da645-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="da645-285">Post di blog sui criteri a livello di processo</span><span class="sxs-lookup"><span data-stu-id="da645-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="da645-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da645-286">Next steps</span></span>

* [<span data-ttu-id="da645-287">Panoramica di Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="da645-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="da645-288">Introduzione a Data Lake Analytics con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="da645-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="da645-289">Gestire Azure Data Lake Analytics tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="da645-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

