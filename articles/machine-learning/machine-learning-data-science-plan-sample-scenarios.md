---
title: gli scenari di analitica avanzati per Azure Machine Learning aaaIdentify | Documenti Microsoft
description: Selezionare scenari appropriato di hello per questo avanzate analitica predittiva con hello processo di analisi scientifica dei dati del Team.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="5e752-103">Scenari per l'analisi avanzata in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5e752-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="5e752-104">Questo articolo vengono illustrati vari hello origini dati di esempio e scenari di destinazione che possono essere gestiti da hello [Team Data Science processo (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e752-104">This article outlines hello variety of sample data sources and target scenarios that can be handled by hello [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="5e752-105">Hello TDSP fornisce un approccio sistematico per i team toocollaborate sulla compilazione di applicazioni intelligenti.</span><span class="sxs-lookup"><span data-stu-id="5e752-105">hello TDSP provides a systematic approach for teams toocollaborate on building intelligent applications.</span></span> <span data-ttu-id="5e752-106">scenari di Hello forniti in questa sezione illustrano le opzioni disponibili nel flusso di lavoro di hello l'elaborazione dati che variano in base alle caratteristiche dei dati hello, percorsi di origine e il repository di destinazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-106">hello scenarios presented here illustrate options available in hello data processing workflow that depend on hello data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="5e752-107">Hello **albero delle decisioni** per scenari di esempio hello appropriata per i dati e l'obiettivo di selezione viene presentata nell'ultima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-107">hello **decision tree** for selecting hello sample scenarios that is appropriate for your data and objective is presented in hello last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="5e752-108">Ognuno di hello le sezioni seguenti viene presentato uno scenario di esempio.</span><span class="sxs-lookup"><span data-stu-id="5e752-108">Each of hello following sections presents a sample scenario.</span></span> <span data-ttu-id="5e752-109">Per ogni scenario vengono elencati un flusso di dati scientifici o di analisi avanzata possibile e le risorse di Azure di supporto.</span><span class="sxs-lookup"><span data-stu-id="5e752-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="5e752-110">**Per tutti i seguenti scenari hello, è necessario:**
> </span><span class="sxs-lookup"><span data-stu-id="5e752-110">**For all of hello following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="5e752-111">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="5e752-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="5e752-112">Creare un'area di lavoro di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="5e752-113"><a name="smalllocal"></a>Scenario \#1: toomedium piccoli set di dati tabulari in un file locale</span><span class="sxs-lookup"><span data-stu-id="5e752-113"><a name="smalllocal"></a>Scenario \#1: Small toomedium tabular dataset in a local files</span></span>
![File locali toomedium Small][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="5e752-115">Risorse di Azure aggiuntive: nessuna</span><span class="sxs-lookup"><span data-stu-id="5e752-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="5e752-116">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-116">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="5e752-117">Caricare un set di dati.</span><span class="sxs-lookup"><span data-stu-id="5e752-117">Upload a dataset.</span></span>
3. <span data-ttu-id="5e752-118">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="5e752-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="5e752-119"><a name="smalllocalprocess"></a>Scenario \#2: toomedium piccoli set di dati di file locali che richiedono l'elaborazione</span><span class="sxs-lookup"><span data-stu-id="5e752-119"><a name="smalllocalprocess"></a>Scenario \#2: Small toomedium dataset of local files that require processing</span></span>
![File locali toomedium di piccole dimensioni con l'elaborazione][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5e752-121">Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-122">Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="5e752-123">Caricare dati tooan contenitore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-123">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="5e752-124">Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dal contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="5e752-125">Trasformare dati toocleaned, sotto forma di tabella.</span><span class="sxs-lookup"><span data-stu-id="5e752-125">Transform data toocleaned, tabular form.</span></span>
5. <span data-ttu-id="5e752-126">Salvare i dati trasformati in BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="5e752-127">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-127">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="5e752-128">Leggere i dati di hello dal BLOB di Azure utilizzando hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-128">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="5e752-129">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="5e752-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5e752-130"><a name="largelocal"></a>Scenario \#3: Set di dati di grandi dimensioni in file locali, con destinazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![File locali di grandi dimensioni][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5e752-132">Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-133">Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="5e752-134">Caricare dati tooan contenitore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-134">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="5e752-135">Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dai BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="5e752-136">Trasformare dati toocleaned, tabulare, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5e752-136">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="5e752-137">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="5e752-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="5e752-138">Estrarre un campione di dati medio-piccolo.</span><span class="sxs-lookup"><span data-stu-id="5e752-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="5e752-139">Salvare i dati campionato hello in BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-139">Save hello sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="5e752-140">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-140">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="5e752-141">Leggere i dati di hello dal BLOB di Azure utilizzando hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-141">Read hello data from Azure blobs using hello [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="5e752-142">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="5e752-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5e752-143"><a name="smalllocaltodb"></a>Scenario \#4: toomedium piccoli set di dati di file locali, come destinazione di SQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-143"><a name="smalllocaltodb"></a>Scenario \#4: Small toomedium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Toomedium piccoli file locali tooSQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5e752-145">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-146">Creare una macchina virtuale di Azure Virtual Machine che esegue SQL Server e IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="5e752-147">Caricare dati tooan contenitore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-147">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="5e752-148">Pre-elaborare e pulire i dati nel contenitore di archiviazione di Azure usando IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="5e752-149">Trasformare dati toocleaned, tabulare, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5e752-149">Transform data toocleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="5e752-150">Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).</span><span class="sxs-lookup"><span data-stu-id="5e752-150">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
6. <span data-ttu-id="5e752-151">Caricare il database del Server tooSQL dati in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-151">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="5e752-152">Opzione \#1: Uso di SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5e752-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="5e752-153">Account di accesso tooSQL macchina virtuale Server</span><span class="sxs-lookup"><span data-stu-id="5e752-153">Login tooSQL Server VM</span></span>
   * <span data-ttu-id="5e752-154">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5e752-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="5e752-155">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e752-155">Create database and target tables.</span></span>
   * <span data-ttu-id="5e752-156">Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi dai file di macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="5e752-156">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
   
   <span data-ttu-id="5e752-157">Opzione \#2: L'uso di IPython Notebook non è consigliabile per i set di dati di medie o grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="5e752-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="5e752-158">Utilizzare tooaccess di stringa di connessione ODBC SQL Server nella macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="5e752-158">Use ODBC connection string tooaccess SQL Server on VM.</span></span>
   * <span data-ttu-id="5e752-159">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e752-159">Create database and target tables.</span></span>
   * <span data-ttu-id="5e752-160">Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi dai file di macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="5e752-160">Use one of hello bulk import methods tooload hello data from VM-local files.</span></span>
7. <span data-ttu-id="5e752-161">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="5e752-161">Explore data, create features as needed.</span></span> <span data-ttu-id="5e752-162">Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-162">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="5e752-163">Nota solo hello query necessaria toocreate li.</span><span class="sxs-lookup"><span data-stu-id="5e752-163">Only note hello necessary query toocreate them.</span></span>
8. <span data-ttu-id="5e752-164">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="5e752-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="5e752-165">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-165">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="5e752-166">Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-166">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="5e752-167">Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="5e752-167">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="5e752-168">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="5e752-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="5e752-169"><a name="largelocaltodb"></a>Scenario \#5: Set di dati di grandi dimensioni in file locali, con destinazione SQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![File locale di grandi dimensioni tooSQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5e752-171">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-172">Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="5e752-173">Caricare dati tooan contenitore di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-173">Upload data tooan Azure storage container.</span></span>
3. <span data-ttu-id="5e752-174">(Facoltativo) Pre-elaborare e pulire i dati.</span><span class="sxs-lookup"><span data-stu-id="5e752-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="5e752-175">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-175">a.</span></span>  <span data-ttu-id="5e752-176">Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="5e752-177">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-177">b.</span></span>  <span data-ttu-id="5e752-178">Trasformare dati toocleaned, tabulare, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5e752-178">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="5e752-179">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-179">c.</span></span>  <span data-ttu-id="5e752-180">Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).</span><span class="sxs-lookup"><span data-stu-id="5e752-180">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="5e752-181">Caricare il database del Server tooSQL dati in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-181">Load data tooSQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="5e752-182">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-182">a.</span></span>  <span data-ttu-id="5e752-183">Account di accesso tooSQL macchina virtuale di Server.</span><span class="sxs-lookup"><span data-stu-id="5e752-183">Login tooSQL Server VM.</span></span>
   
   <span data-ttu-id="5e752-184">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-184">b.</span></span>  <span data-ttu-id="5e752-185">Se i dati non sono ancora stati salvati, scaricare i file di dati da Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-185">If data not saved already, download data files from Azure</span></span>
   
       storage container toolocal-VM folder.
   
   <span data-ttu-id="5e752-186">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-186">c.</span></span>  <span data-ttu-id="5e752-187">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5e752-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="5e752-188">d.</span><span class="sxs-lookup"><span data-stu-id="5e752-188">d.</span></span>  <span data-ttu-id="5e752-189">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e752-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="5e752-190">e.</span><span class="sxs-lookup"><span data-stu-id="5e752-190">e.</span></span>  <span data-ttu-id="5e752-191">Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi.</span><span class="sxs-lookup"><span data-stu-id="5e752-191">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="5e752-192">f.</span><span class="sxs-lookup"><span data-stu-id="5e752-192">f.</span></span>  <span data-ttu-id="5e752-193">Se sono necessari i join di tabelle, creare indici tooexpedite join.</span><span class="sxs-lookup"><span data-stu-id="5e752-193">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e752-194">Per un caricamento più rapido delle dimensioni di dati di grandi dimensioni, è consigliabile creare tabelle partizionate e importazione bulk hello in parallelo.</span><span class="sxs-lookup"><span data-stu-id="5e752-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import hello data in parallel.</span></span> <span data-ttu-id="5e752-195">Per ulteriori informazioni, vedere [tooSQL importazione parallela dei dati le tabelle partizionate](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5e752-195">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5e752-196">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="5e752-196">Explore data, create features as needed.</span></span> <span data-ttu-id="5e752-197">Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-197">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="5e752-198">Nota solo hello query necessaria toocreate li.</span><span class="sxs-lookup"><span data-stu-id="5e752-198">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="5e752-199">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="5e752-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="5e752-200">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-200">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="5e752-201">Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-201">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="5e752-202">Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="5e752-202">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="5e752-203">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato</span><span class="sxs-lookup"><span data-stu-id="5e752-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="5e752-204"><a name="largedbtodb"></a>Scenario \#6: Set di dati di grandi dimensioni in un database SQL Server locale, con destinazione SQL Server nella macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Database di SQL Server locale tooSQL DB grandi dimensioni in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5e752-206">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-207">Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="5e752-208">Utilizzare uno dei dati hello esportare i dati di hello tooexport metodi dai file toodump di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e752-208">Use one of hello data export methods tooexport hello data from SQL Server toodump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e752-209">Se si decide di toomove tutti i dati dal database locale di hello, un'alternativa (più veloce) metodo toomove hello completo del database toothe istanza SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-209">If you decide toomove all data from hello on-prem database, an alternate (faster) method toomove hello full database toothe SQL Server instance in Azure.</span></span> <span data-ttu-id="5e752-210">Ignorare i dati di hello passaggi tooexport, creare database e database di destinazione / importazione a caricamento dati toohello e seguire il metodo alternativo di hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-210">Skip hello steps tooexport data, create database, and load/import data toohello target database and follow hello alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="5e752-211">Caricare contenitore di archiviazione tooAzure file dump.</span><span class="sxs-lookup"><span data-stu-id="5e752-211">Upload dump files tooAzure storage container.</span></span>
4. <span data-ttu-id="5e752-212">Caricare i dati di hello tooa database di SQL Server in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-212">Load hello data tooa SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="5e752-213">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-213">a.</span></span>  <span data-ttu-id="5e752-214">Account di accesso toohello macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5e752-214">Login toohello SQL Server VM.</span></span>
   
   <span data-ttu-id="5e752-215">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-215">b.</span></span>  <span data-ttu-id="5e752-216">Scaricare i file di dati da una cartella di archiviazione di Azure contenitore toohello-VM locale.</span><span class="sxs-lookup"><span data-stu-id="5e752-216">Download data files from an Azure storage container toohello local-VM folder.</span></span>
   
   <span data-ttu-id="5e752-217">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-217">c.</span></span>  <span data-ttu-id="5e752-218">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5e752-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="5e752-219">d.</span><span class="sxs-lookup"><span data-stu-id="5e752-219">d.</span></span>  <span data-ttu-id="5e752-220">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="5e752-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="5e752-221">e.</span><span class="sxs-lookup"><span data-stu-id="5e752-221">e.</span></span>  <span data-ttu-id="5e752-222">Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi.</span><span class="sxs-lookup"><span data-stu-id="5e752-222">Use one of hello bulk import methods tooload hello data.</span></span>
   
   <span data-ttu-id="5e752-223">f.</span><span class="sxs-lookup"><span data-stu-id="5e752-223">f.</span></span>  <span data-ttu-id="5e752-224">Se sono necessari i join di tabelle, creare indici tooexpedite join.</span><span class="sxs-lookup"><span data-stu-id="5e752-224">If table joins are required, create indexes tooexpedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e752-225">Per un caricamento più rapido delle dimensioni di dati di grandi dimensioni, creare le tabelle partizionate e l'importazione dei dati hello toobulk in parallelo.</span><span class="sxs-lookup"><span data-stu-id="5e752-225">For faster loading of large data sizes, create partitioned tables and toobulk import hello data in parallel.</span></span> <span data-ttu-id="5e752-226">Per ulteriori informazioni, vedere [tooSQL importazione parallela dei dati le tabelle partizionate](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5e752-226">For more information, see [Parallel Data Import tooSQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="5e752-227">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="5e752-227">Explore data, create features as needed.</span></span> <span data-ttu-id="5e752-228">Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-228">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="5e752-229">Nota solo hello query necessaria toocreate li.</span><span class="sxs-lookup"><span data-stu-id="5e752-229">Only note hello necessary query toocreate them.</span></span>
6. <span data-ttu-id="5e752-230">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="5e752-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="5e752-231">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-231">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="5e752-232">Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-232">Read hello data directly from hello SQL Server using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="5e752-233">Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="5e752-233">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="5e752-234">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="5e752-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a><span data-ttu-id="5e752-235">Metodo alternativo toocopy completo di un database da un tooAzure di SQL Server on-premise SQL Database</span><span class="sxs-lookup"><span data-stu-id="5e752-235">Alternate method toocopy a full database from an on-premises  SQL Server tooAzure SQL Database</span></span>
![Collegamento e scollegamento di local DB tooSQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="5e752-237">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="5e752-238">tooreplicate hello intero database di SQL Server nella macchina virtuale SQL Server, è necessario copiare un database da un server dei percorsi/tooanother, presupponendo che il database hello è possibile portare temporaneamente offline.</span><span class="sxs-lookup"><span data-stu-id="5e752-238">tooreplicate hello entire SQL Server database in your SQL Server VM, you should copy a database from one location/server tooanother, assuming that hello database can be taken temporarily offline.</span></span> <span data-ttu-id="5e752-239">A tale scopo, in Esplora oggetti di SQL Server Management Studio hello o utilizzando i comandi Transact-SQL equivalenti hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-239">You do this in hello SQL Server Management Studio Object Explorer, or using hello equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="5e752-240">Scollegare il database di hello nel percorso di origine hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-240">Detach hello database at hello source location.</span></span> <span data-ttu-id="5e752-241">Per altre informazioni, vedere [Scollegamento di un database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5e752-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="5e752-242">Nella finestra di Esplora risorse o prompt dei comandi di Windows hello copia scollegata i file di database o file e file di log o percorso di destinazione dei file toohello su hello macchina virtuale di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="5e752-242">In Windows Explorer or Windows Command Prompt window, copy hello detached database file or files and log file or files toohello target location on hello SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="5e752-243">Collegare l'istanza di SQL Server di destinazione di hello copiato i file toohello.</span><span class="sxs-lookup"><span data-stu-id="5e752-243">Attach hello copied files toohello target SQL Server instance.</span></span> <span data-ttu-id="5e752-244">Per altre informazioni, vedere [Collegare un database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="5e752-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="5e752-245">[Spostamento di un database tramite la funzionalità di scollegamento e collegamento (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="5e752-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="5e752-246"><a name="largedbtohive"></a>Scenario \#7: Big Data nei file locali, con destinazione il database Hive nei cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e752-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big Data nell'Hive di destinazione locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="5e752-248">Risorse di Azure aggiuntive: cluster Hadoop di Azure HDInsight e macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="5e752-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="5e752-249">Creare una macchina virtuale di Azure che esegue il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="5e752-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="5e752-250">Creare un cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e752-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="5e752-251">(Facoltativo) Pre-elaborare e pulire i dati.</span><span class="sxs-lookup"><span data-stu-id="5e752-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="5e752-252">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-252">a.</span></span>  <span data-ttu-id="5e752-253">Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure</span><span class="sxs-lookup"><span data-stu-id="5e752-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="5e752-254">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-254">b.</span></span>  <span data-ttu-id="5e752-255">Trasformare dati toocleaned, tabulare, se necessario.</span><span class="sxs-lookup"><span data-stu-id="5e752-255">Transform data toocleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="5e752-256">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-256">c.</span></span>  <span data-ttu-id="5e752-257">Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).</span><span class="sxs-lookup"><span data-stu-id="5e752-257">Save data tooVM-local files (IPython Notebook is running on VM, local drives refer tooVM drives).</span></span>
4. <span data-ttu-id="5e752-258">Caricare contenitore predefinito toohello di dati di un cluster Hadoop hello selezionato nel passaggio hello 2.</span><span class="sxs-lookup"><span data-stu-id="5e752-258">Upload data toohello default container of hello Hadoop cluster selected in hello step 2.</span></span>
5. <span data-ttu-id="5e752-259">Caricamento dati tooHive database cluster Azure HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e752-259">Load data tooHive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="5e752-260">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-260">a.</span></span>  <span data-ttu-id="5e752-261">Accedi toohello nodo head del cluster Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="5e752-261">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="5e752-262">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-262">b.</span></span>  <span data-ttu-id="5e752-263">Aprire hello Hadoop della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="5e752-263">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5e752-264">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-264">c.</span></span>  <span data-ttu-id="5e752-265">Immettere una directory radice di Hive hello dal comando `cd %hive_home%\bin` nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e752-265">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5e752-266">d.</span><span class="sxs-lookup"><span data-stu-id="5e752-266">d.</span></span>  <span data-ttu-id="5e752-267">Eseguire hello Hive query toocreate database e le tabelle e caricare i dati da tabelle tooHive di archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="5e752-267">Run hello Hive queries toocreate database and tables, and load data from blob storage tooHive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5e752-268">Se i dati di hello sono grandi, gli utenti possono creare tabella Hive hello con partizioni.</span><span class="sxs-lookup"><span data-stu-id="5e752-268">If hello data is big, users can create hello Hive table with partitions.</span></span> <span data-ttu-id="5e752-269">Quindi, gli utenti possono usare un `for` ciclo in hello riga di comando di Hadoop su dati di tooload hello nodo head in tabella Hive hello partizionata dalla partizione.</span><span class="sxs-lookup"><span data-stu-id="5e752-269">Then, users can use a `for` loop in hello Hadoop Command Line on hello head node tooload data into hello Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="5e752-270">Esaminare i dati e creare le funzionalità necessarie nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e752-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="5e752-271">Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-271">Note that hello features do not need toobe materialized in hello database tables.</span></span> <span data-ttu-id="5e752-272">Nota solo hello query necessaria toocreate li.</span><span class="sxs-lookup"><span data-stu-id="5e752-272">Only note hello necessary query toocreate them.</span></span>
   
   <span data-ttu-id="5e752-273">a.</span><span class="sxs-lookup"><span data-stu-id="5e752-273">a.</span></span>  <span data-ttu-id="5e752-274">Accedi toohello nodo head del cluster Hadoop hello</span><span class="sxs-lookup"><span data-stu-id="5e752-274">Log in toohello head node of hello Hadoop cluster</span></span>
   
   <span data-ttu-id="5e752-275">b.</span><span class="sxs-lookup"><span data-stu-id="5e752-275">b.</span></span>  <span data-ttu-id="5e752-276">Aprire hello Hadoop della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="5e752-276">Open hello Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5e752-277">c.</span><span class="sxs-lookup"><span data-stu-id="5e752-277">c.</span></span>  <span data-ttu-id="5e752-278">Immettere una directory radice di Hive hello dal comando `cd %hive_home%\bin` nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5e752-278">Enter hello Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="5e752-279">d.</span><span class="sxs-lookup"><span data-stu-id="5e752-279">d.</span></span>  <span data-ttu-id="5e752-280">Eseguire le query Hive hello nella riga di comando di Hadoop nel nodo head di hello di dati di hello tooexplore cluster Hadoop hello e creare le funzionalità in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5e752-280">Run hello Hive queries in Hadoop Command Line on hello head node of hello Hadoop cluster tooexplore hello data and create features as needed.</span></span>
7. <span data-ttu-id="5e752-281">Se necessario e/o lo si desidera, esempio hello toofit di dati in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5e752-281">If needed and/or desired, sample hello data toofit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="5e752-282">Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="5e752-282">Sign in toohello [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="5e752-283">Leggere dati hello direttamente da hello `Hive Queries` utilizzando hello [l'importazione dei dati] [ import-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="5e752-283">Read hello data directly from hello `Hive Queries` using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="5e752-284">Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.</span><span class="sxs-lookup"><span data-stu-id="5e752-284">Paste hello necessary query which extracts fields, creates features, and samples data if needed directly in hello [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="5e752-285">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="5e752-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="5e752-286"><a name="decisiontree"></a>Albero delle decisioni per la scelta degli scenari</span><span class="sxs-lookup"><span data-stu-id="5e752-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="5e752-287">Hello diagramma seguente sono riepilogati gli scenari di hello descritti in precedenza e hello avanzate processo Analitica e la tecnologia le scelte effettuate che consentono di accedere tooeach degli scenari indicati in modo dettagliato hello.</span><span class="sxs-lookup"><span data-stu-id="5e752-287">hello following diagram summarizes hello scenarios described above and hello Advanced Analytics Process and Technology choices made that take you tooeach of hello itemized scenarios.</span></span> <span data-ttu-id="5e752-288">Si noti che potrebbe richiedere l'elaborazione dati, l'esplorazione, progettazione di funzionalità e campionamento inserire in uno o più metodo/ambiente - origine hello, intermedio, e/o ambienti di destinazione e possono essere eseguite in modo iterativo, in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="5e752-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at hello source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="5e752-289">diagramma di Hello solo funge da un'illustrazione di alcune delle possibili flussi e non fornisce un'enumerazione completa.</span><span class="sxs-lookup"><span data-stu-id="5e752-289">hello diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Scenari della procedura dettagliata del processo di analisi scientifica][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="5e752-291">Analisi avanzata in esempi di azioni</span><span class="sxs-lookup"><span data-stu-id="5e752-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="5e752-292">Per procedure dettagliate di Azure Machine Learning end-to-end che impiegano hello avanzate processo Analitica e la tecnologia utilizzano set di dati pubblici, vedere:</span><span class="sxs-lookup"><span data-stu-id="5e752-292">For end-to-end Azure Machine Learning walkthroughs that employ hello Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="5e752-293">[Processo di analisi scientifica dei dati per i team in azione: uso di SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5e752-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="5e752-294">[Processo di analisi scientifica dei dati per i team in azione: uso dei cluster Hadoop di HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="5e752-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
