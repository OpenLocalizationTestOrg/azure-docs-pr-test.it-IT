---
title: Identificare scenari di analisi avanzata per Azure Machine Learning | Documentazione Microsoft
description: Selezionare gli scenari appropriati per eseguire analisi predittive avanzate con il Processo di analisi scientifica dei dati per i team.
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
ms.openlocfilehash: fe4f74f2e0602d13eedb6ca186480291a9a5724f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="d1b21-103">Scenari per l'analisi avanzata in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d1b21-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="d1b21-104">Questo articolo descrive le varie origini dati di esempio e gli scenari di destinazione che possono essere gestiti con il [Processo di analisi scientifica dei dati per i team (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1b21-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="d1b21-105">Il TDSP offre un approccio sistematico per consentire ai team di collaborare sulla compilazione di applicazioni intelligenti.</span><span class="sxs-lookup"><span data-stu-id="d1b21-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="d1b21-106">Gli scenari presentati illustrano le opzioni disponibili nel flusso di lavoro dell'elaborazione dei dati basato su caratteristiche dei dati, posizioni delle origini e repository di destinazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="d1b21-107">L’ **albero delle decisioni** per la scelta degli scenari di esempio appropriati per i dati dell’utente e l'obiettivo sono presentati nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="d1b21-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="d1b21-108">Ciascuna delle sezioni seguenti presenta uno scenario di esempio.</span><span class="sxs-lookup"><span data-stu-id="d1b21-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="d1b21-109">Per ogni scenario vengono elencati un flusso di dati scientifici o di analisi avanzata possibile e le risorse di Azure di supporto.</span><span class="sxs-lookup"><span data-stu-id="d1b21-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="d1b21-110">**Per tutti gli scenari seguenti, è necessario:**
> </span><span class="sxs-lookup"><span data-stu-id="d1b21-110">**For all of the following scenarios, you need to:**
</span></span><br/>
> 
> * <span data-ttu-id="d1b21-111">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md)
>   </span><span class="sxs-lookup"><span data-stu-id="d1b21-111">[Create a storage account](../storage/common/storage-create-storage-account.md)
</span></span><br/>
> * [<span data-ttu-id="d1b21-112">Creare un'area di lavoro di Machine Learning di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <span data-ttu-id="d1b21-113"><a name="smalllocal"></a>Scenario \#1: Set di dati tabulari medio-piccolo in un file locale</span><span class="sxs-lookup"><span data-stu-id="d1b21-113"><a name="smalllocal"></a>Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![File locali medio-piccoli][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="d1b21-115">Risorse di Azure aggiuntive: nessuna</span><span class="sxs-lookup"><span data-stu-id="d1b21-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="d1b21-116">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="d1b21-117">Caricare un set di dati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-117">Upload a dataset.</span></span>
3. <span data-ttu-id="d1b21-118">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="d1b21-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <span data-ttu-id="d1b21-119"><a name="smalllocalprocess"></a>Scenario \#2: Set di dati medio-piccolo in un file locale che richiede elaborazione</span><span class="sxs-lookup"><span data-stu-id="d1b21-119"><a name="smalllocalprocess"></a>Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![File locali medio piccoli con elaborazione][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="d1b21-121">Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-122">Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="d1b21-123">Caricare i dati in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="d1b21-124">Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dal contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="d1b21-125">Trasformare i dati in un formato tabulare pulito.</span><span class="sxs-lookup"><span data-stu-id="d1b21-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="d1b21-126">Salvare i dati trasformati in BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="d1b21-127">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="d1b21-128">Leggere i dati dai BLOB di Azure usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="d1b21-129">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="d1b21-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="d1b21-130"><a name="largelocal"></a>Scenario \#3: Set di dati di grandi dimensioni in file locali, con destinazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-130"><a name="largelocal"></a>Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![File locali di grandi dimensioni][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="d1b21-132">Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-133">Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="d1b21-134">Caricare i dati in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="d1b21-135">Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dai BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="d1b21-136">Trasformare i dati in un formato tabulare pulito, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d1b21-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="d1b21-137">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="d1b21-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="d1b21-138">Estrarre un campione di dati medio-piccolo.</span><span class="sxs-lookup"><span data-stu-id="d1b21-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="d1b21-139">Salvare i dati campionati in BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="d1b21-140">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="d1b21-141">Leggere i dati dai BLOB di Azure usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="d1b21-142">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="d1b21-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="d1b21-143"><a name="smalllocaltodb"></a>Scenario \#4: Set di dati di medie o piccole dimensioni in un file locale, con destinazione SQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-143"><a name="smalllocaltodb"></a>Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![File locali medio-piccoli al database SQL in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="d1b21-145">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-146">Creare una macchina virtuale di Azure Virtual Machine che esegue SQL Server e IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="d1b21-147">Caricare i dati in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="d1b21-148">Pre-elaborare e pulire i dati nel contenitore di archiviazione di Azure usando IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="d1b21-149">Trasformare i dati in un formato tabulare pulito, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d1b21-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="d1b21-150">Salvare i dati in file nella macchina virtuale locale (IPython Notebook è in esecuzione nella VM, le unità locali fanno riferimento alle unità della VM).</span><span class="sxs-lookup"><span data-stu-id="d1b21-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="d1b21-151">Caricare i dati nel database SQL Server in esecuzione in una VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="d1b21-152">Opzione \#1: Uso di SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="d1b21-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="d1b21-153">Accedere alla macchina virtuale di SQL Server</span><span class="sxs-lookup"><span data-stu-id="d1b21-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="d1b21-154">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d1b21-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="d1b21-155">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="d1b21-155">Create database and target tables.</span></span>
   * <span data-ttu-id="d1b21-156">Utilizzare uno dei metodi di importazione globale per caricare i dati dai file della macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="d1b21-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="d1b21-157">Opzione \#2: L'uso di IPython Notebook non è consigliabile per i set di dati di medie o grandi dimensioni</span><span class="sxs-lookup"><span data-stu-id="d1b21-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="d1b21-158">Utilizzare la stringa di connessione ODBC per accedere a SQL Server sulla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d1b21-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="d1b21-159">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="d1b21-159">Create database and target tables.</span></span>
   * <span data-ttu-id="d1b21-160">Utilizzare uno dei metodi di importazione globale per caricare i dati dai file della macchina virtuale locale.</span><span class="sxs-lookup"><span data-stu-id="d1b21-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="d1b21-161">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="d1b21-161">Explore data, create features as needed.</span></span> <span data-ttu-id="d1b21-162">Si noti che le funzionalità non devono essere materializzare nelle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="d1b21-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="d1b21-163">Notare solo la query necessaria per crearle.</span><span class="sxs-lookup"><span data-stu-id="d1b21-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="d1b21-164">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="d1b21-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="d1b21-165">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="d1b21-166">Leggere i dati direttamente da SQL Server usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="d1b21-167">Incollare la query richiesta che estrae i campi, crea le funzionalità ed esegue il campionamento dei dati, se necessario, direttamente nella query di [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="d1b21-168">Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.</span><span class="sxs-lookup"><span data-stu-id="d1b21-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <span data-ttu-id="d1b21-169"><a name="largelocaltodb"></a>Scenario \#5: Set di dati di grandi dimensioni in file locali, con destinazione SQL Server in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-169"><a name="largelocaltodb"></a>Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![File locali di grandi dimensioni al database SQL in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="d1b21-171">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-172">Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="d1b21-173">Caricare i dati in un contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="d1b21-174">(Facoltativo) Pre-elaborare e pulire i dati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="d1b21-175">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-175">a.</span></span>  <span data-ttu-id="d1b21-176">Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="d1b21-177">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-177">b.</span></span>  <span data-ttu-id="d1b21-178">Trasformare i dati in un formato tabulare pulito, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d1b21-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="d1b21-179">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-179">c.</span></span>  <span data-ttu-id="d1b21-180">Salvare i dati in file nella macchina virtuale locale (IPython Notebook è in esecuzione nella VM, le unità locali fanno riferimento alle unità della VM).</span><span class="sxs-lookup"><span data-stu-id="d1b21-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="d1b21-181">Caricare i dati nel database SQL Server in esecuzione in una VM di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="d1b21-182">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-182">a.</span></span>  <span data-ttu-id="d1b21-183">Accedere alla macchina virtuale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1b21-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="d1b21-184">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-184">b.</span></span>  <span data-ttu-id="d1b21-185">Se i dati non sono ancora stati salvati, scaricare i file di dati da Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="d1b21-186">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-186">c.</span></span>  <span data-ttu-id="d1b21-187">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d1b21-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="d1b21-188">d.</span><span class="sxs-lookup"><span data-stu-id="d1b21-188">d.</span></span>  <span data-ttu-id="d1b21-189">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="d1b21-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="d1b21-190">e.</span><span class="sxs-lookup"><span data-stu-id="d1b21-190">e.</span></span>  <span data-ttu-id="d1b21-191">Usare uno dei metodi di importazione in blocco per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="d1b21-192">f.</span><span class="sxs-lookup"><span data-stu-id="d1b21-192">f.</span></span>  <span data-ttu-id="d1b21-193">Se sono richiesti join di tabella, creare gli indici per velocizzarli.</span><span class="sxs-lookup"><span data-stu-id="d1b21-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1b21-194">Per caricare più velocemente i dati di grandi dimensioni, si consiglia di creare tabelle partizionate e importare in blocco i dati in parallelo.</span><span class="sxs-lookup"><span data-stu-id="d1b21-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="d1b21-195">Per altre informazioni, vedere l'articolo relativo all' [importazione parallela di dati in tabelle partizionale di SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d1b21-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="d1b21-196">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="d1b21-196">Explore data, create features as needed.</span></span> <span data-ttu-id="d1b21-197">Si noti che le funzionalità non devono essere materializzare nelle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="d1b21-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="d1b21-198">Notare solo la query necessaria per crearle.</span><span class="sxs-lookup"><span data-stu-id="d1b21-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="d1b21-199">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="d1b21-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="d1b21-200">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="d1b21-201">Leggere i dati direttamente da SQL Server usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="d1b21-202">Incollare la query richiesta che estrae i campi, crea le funzionalità ed esegue il campionamento dei dati, se necessario, direttamente nella query di [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="d1b21-203">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato</span><span class="sxs-lookup"><span data-stu-id="d1b21-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <span data-ttu-id="d1b21-204"><a name="largedbtodb"></a>Scenario \#6: Set di dati di grandi dimensioni in un database SQL Server locale, con destinazione SQL Server nella macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-204"><a name="largedbtodb"></a>Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Database SQL locale di grandi dimensioni  al database SQL locale in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="d1b21-206">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-207">Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="d1b21-208">Usare uno dei metodi di esportazione dei dati per esportare i dati da SQL Server in file di dump.</span><span class="sxs-lookup"><span data-stu-id="d1b21-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1b21-209">Se si decide di spostare tutti i dati dal database locale, un metodo alternativo più rapido consiste nello spostamento dell'intero database nell'istanza di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="d1b21-210">Ignorare i passaggi per esportare i dati, creare il database e caricare/importare i dati nel database di destinazione e seguire il metodo alternativo.</span><span class="sxs-lookup"><span data-stu-id="d1b21-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="d1b21-211">Caricare file di dump nel contenitore di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="d1b21-212">Caricare i dati in un database di SQL Server in esecuzione in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="d1b21-213">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-213">a.</span></span>  <span data-ttu-id="d1b21-214">Accedere alla macchina virtuale di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d1b21-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="d1b21-215">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-215">b.</span></span>  <span data-ttu-id="d1b21-216">Scaricare i file di dati dal contenitore di archiviazione di Azure nella cartella della VM locale.</span><span class="sxs-lookup"><span data-stu-id="d1b21-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="d1b21-217">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-217">c.</span></span>  <span data-ttu-id="d1b21-218">Eseguire SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d1b21-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="d1b21-219">d.</span><span class="sxs-lookup"><span data-stu-id="d1b21-219">d.</span></span>  <span data-ttu-id="d1b21-220">Creare tabelle di database e di destinazione</span><span class="sxs-lookup"><span data-stu-id="d1b21-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="d1b21-221">e.</span><span class="sxs-lookup"><span data-stu-id="d1b21-221">e.</span></span>  <span data-ttu-id="d1b21-222">Usare uno dei metodi di importazione in blocco per caricare i dati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="d1b21-223">f.</span><span class="sxs-lookup"><span data-stu-id="d1b21-223">f.</span></span>  <span data-ttu-id="d1b21-224">Se sono richiesti join di tabella, creare gli indici per velocizzarli.</span><span class="sxs-lookup"><span data-stu-id="d1b21-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1b21-225">Per caricare più velocemente dati di grandi dimensioni, creare tabelle partizionate e importare in blocco i dati in parallelo.</span><span class="sxs-lookup"><span data-stu-id="d1b21-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="d1b21-226">Per altre informazioni, vedere l'articolo relativo all' [importazione parallela di dati in tabelle partizionale di SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="d1b21-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="d1b21-227">Esaminare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="d1b21-227">Explore data, create features as needed.</span></span> <span data-ttu-id="d1b21-228">Si noti che le funzionalità non devono essere materializzare nelle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="d1b21-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="d1b21-229">Notare solo la query necessaria per crearle.</span><span class="sxs-lookup"><span data-stu-id="d1b21-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="d1b21-230">Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.</span><span class="sxs-lookup"><span data-stu-id="d1b21-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="d1b21-231">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="d1b21-232">Leggere i dati direttamente da SQL Server usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="d1b21-233">Incollare la query richiesta che estrae i campi, crea le funzionalità ed esegue il campionamento dei dati, se necessario, direttamente nella query di [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="d1b21-234">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="d1b21-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="d1b21-235">Metodo alternativo per copiare un intero database da un server SQL locale al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Scollegare il database locale e collegarlo al database SQL in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="d1b21-237">Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="d1b21-238">Per replicare l'intero database SQL Server nella macchina virtuale di SQL Server, è necessario copiare un database da un percorso/server a un altro, supponendo che il database possa essere portato temporaneamente offline.</span><span class="sxs-lookup"><span data-stu-id="d1b21-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="d1b21-239">Eseguire questa operazione in SQL Server Management Studio, oppure utilizzando i comandi Transact-SQL equivalenti.</span><span class="sxs-lookup"><span data-stu-id="d1b21-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="d1b21-240">Scollegare il database nel percorso di origine.</span><span class="sxs-lookup"><span data-stu-id="d1b21-240">Detach the database at the source location.</span></span> <span data-ttu-id="d1b21-241">Per altre informazioni, vedere [Scollegamento di un database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="d1b21-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="d1b21-242">In Esplora risorse o nella finestra del prompt dei comandi di Windows  copiare il file o i file del database scollegato nel percorso di destinazione della macchina virtuale di SQL Server in Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="d1b21-243">Collegare i file copiati all'istanza di SQL Server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="d1b21-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="d1b21-244">Per altre informazioni, vedere [Collegare un database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="d1b21-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="d1b21-245">[Spostamento di un database tramite la funzionalità di scollegamento e collegamento (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="d1b21-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <span data-ttu-id="d1b21-246"><a name="largedbtohive"></a>Scenario \#7: Big Data nei file locali, con destinazione il database Hive nei cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1b21-246"><a name="largedbtohive"></a>Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big Data nell'Hive di destinazione locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="d1b21-248">Risorse di Azure aggiuntive: cluster Hadoop di Azure HDInsight e macchina virtuale di Azure (server IPython Notebook)</span><span class="sxs-lookup"><span data-stu-id="d1b21-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="d1b21-249">Creare una macchina virtuale di Azure che esegue il server IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d1b21-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="d1b21-250">Creare un cluster Hadoop di Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1b21-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="d1b21-251">(Facoltativo) Pre-elaborare e pulire i dati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="d1b21-252">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-252">a.</span></span>  <span data-ttu-id="d1b21-253">Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure</span><span class="sxs-lookup"><span data-stu-id="d1b21-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="d1b21-254">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-254">b.</span></span>  <span data-ttu-id="d1b21-255">Trasformare i dati in un formato tabulare pulito, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d1b21-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="d1b21-256">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-256">c.</span></span>  <span data-ttu-id="d1b21-257">Salvare i dati in file nella macchina virtuale locale (IPython Notebook è in esecuzione nella VM, le unità locali fanno riferimento alle unità della VM).</span><span class="sxs-lookup"><span data-stu-id="d1b21-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="d1b21-258">Caricare i dati nel contenitore predefinito del cluster Hadoop selezionato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="d1b21-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="d1b21-259">Caricare i dati nel database di Hive del cluster Hadoop di HDInsight di Azure.</span><span class="sxs-lookup"><span data-stu-id="d1b21-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="d1b21-260">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-260">a.</span></span>  <span data-ttu-id="d1b21-261">Accedere al nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="d1b21-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="d1b21-262">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-262">b.</span></span>  <span data-ttu-id="d1b21-263">Aprire la riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1b21-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="d1b21-264">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-264">c.</span></span>  <span data-ttu-id="d1b21-265">Immettere la directory radice di Hive con il comando `cd %hive_home%\bin` nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1b21-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="d1b21-266">d.</span><span class="sxs-lookup"><span data-stu-id="d1b21-266">d.</span></span>  <span data-ttu-id="d1b21-267">Eseguire le query Hive per creare tabelle e database e caricare i dati dall'archivio BLOB nelle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="d1b21-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d1b21-268">Se i dati sono di grandi dimensioni, gli utenti possono creare la tabella Hive con partizioni.</span><span class="sxs-lookup"><span data-stu-id="d1b21-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="d1b21-269">Gli utenti possono quindi usare un ciclo `for` nella riga di comando di Hadoop nel nodo head per caricare dati nella tabella Hive partizionata in base alla partizione.</span><span class="sxs-lookup"><span data-stu-id="d1b21-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="d1b21-270">Esaminare i dati e creare le funzionalità necessarie nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1b21-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="d1b21-271">Si noti che le funzionalità non devono essere materializzare nelle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="d1b21-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="d1b21-272">Notare solo la query necessaria per crearle.</span><span class="sxs-lookup"><span data-stu-id="d1b21-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="d1b21-273">a.</span><span class="sxs-lookup"><span data-stu-id="d1b21-273">a.</span></span>  <span data-ttu-id="d1b21-274">Accedere al nodo head del cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="d1b21-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="d1b21-275">b.</span><span class="sxs-lookup"><span data-stu-id="d1b21-275">b.</span></span>  <span data-ttu-id="d1b21-276">Aprire la riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1b21-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="d1b21-277">c.</span><span class="sxs-lookup"><span data-stu-id="d1b21-277">c.</span></span>  <span data-ttu-id="d1b21-278">Immettere la directory radice di Hive con il comando `cd %hive_home%\bin` nella riga di comando di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d1b21-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="d1b21-279">d.</span><span class="sxs-lookup"><span data-stu-id="d1b21-279">d.</span></span>  <span data-ttu-id="d1b21-280">Eseguire le query Hive nella riga di comando di Hadoop nel nodo head del cluster Hadoop per esplorare i dati e creare le funzionalità necessarie.</span><span class="sxs-lookup"><span data-stu-id="d1b21-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="d1b21-281">Se necessario e/o lo si desidera, campionare i dati in modo da adattarli a Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="d1b21-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="d1b21-282">Accedere a [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="d1b21-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="d1b21-283">Leggere i dati direttamente da `Hive Queries` usando il modulo [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="d1b21-284">Incollare la query richiesta che estrae i campi, crea le funzionalità ed esegue il campionamento dei dati, se necessario, direttamente nella query di [Import Data][import-data] (Importa dati).</span><span class="sxs-lookup"><span data-stu-id="d1b21-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="d1b21-285">Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.</span><span class="sxs-lookup"><span data-stu-id="d1b21-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <span data-ttu-id="d1b21-286"><a name="decisiontree"></a>Albero delle decisioni per la scelta degli scenari</span><span class="sxs-lookup"><span data-stu-id="d1b21-286"><a name="decisiontree"></a>Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="d1b21-287">Nel diagramma seguente sono riepilogati gli scenari descritti in precedenza e il processo di analisi avanzata e le scelte di tecnologia effettuate che conducono l’utente a ciascuno degli scenari elencati.</span><span class="sxs-lookup"><span data-stu-id="d1b21-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="d1b21-288">Tenere presente che l'elaborazione dei dati, l'esplorazione, la progettazione delle funzionalità e il campionamento potrebbero avvenire in uno o più metodi/ambienti, ad esempio nell'ambiente di origine, intermedio e/o di destinazione, e potrebbero procedere in modo iterativo, se necessario.</span><span class="sxs-lookup"><span data-stu-id="d1b21-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="d1b21-289">Il diagramma è solo un'illustrazione di alcuni dei possibili flussi e non fornisce un'enumerazione completa.</span><span class="sxs-lookup"><span data-stu-id="d1b21-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Scenari della procedura dettagliata del processo di analisi scientifica][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="d1b21-291">Analisi avanzata in esempi di azioni</span><span class="sxs-lookup"><span data-stu-id="d1b21-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="d1b21-292">Per procedure dettagliate end-to-end di Azure Machine Learning che usano ADAPT tramite set di dati pubblici, vedere:</span><span class="sxs-lookup"><span data-stu-id="d1b21-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="d1b21-293">[Processo di analisi scientifica dei dati per i team in azione: uso di SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d1b21-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="d1b21-294">[Processo di analisi scientifica dei dati per i team in azione: uso dei cluster Hadoop di HDInsight](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d1b21-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

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
