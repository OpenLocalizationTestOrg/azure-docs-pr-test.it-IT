---
title: "Usare attività personalizzate in una pipeline di Azure Data Factory"
description: "Informazioni su come creare attività personalizzate e usarle in una pipeline di Azure Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f3d265f31cb653d32076747e586383d67bbccc41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="2dbae-103">Usare attività personalizzate in una pipeline di Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="2dbae-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="2dbae-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="2dbae-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="2dbae-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="2dbae-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="2dbae-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="2dbae-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="2dbae-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="2dbae-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="2dbae-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="2dbae-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="2dbae-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2dbae-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="2dbae-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="2dbae-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="2dbae-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="2dbae-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="2dbae-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="2dbae-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="2dbae-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="2dbae-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="2dbae-114">In una pipeline di Azure Data Factory è possibile usare due tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="2dbae-115">[Attività di spostamento dei dati](data-factory-data-movement-activities.md) per spostare i dati fra [archivi dati supportati di origine e sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="2dbae-115">[Data Movement Activities](data-factory-data-movement-activities.md) to move data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="2dbae-116">[Attività di trasformazione dei dati](data-factory-data-transformation-activities.md) per trasformare i dati usando servizi di calcolo come Azure HDInsight, Azure Batch e Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="2dbae-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="2dbae-117">Per spostare dati da e verso un archivio dati non supportato da Azure Data Factory, creare un'**attività personalizzata** contenente la logica di spostamento dei dati richiesta e usarla in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-117">To move data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use the activity in a pipeline.</span></span> <span data-ttu-id="2dbae-118">Analogamente, per trasformare o elaborare dati in un modo non supportato dalla Data Factory, creare un'attività personalizzata contenente la logica di trasformazione dei dati richiesta e usarla in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-118">Similarly, to transform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use the activity in a pipeline.</span></span> 

<span data-ttu-id="2dbae-119">È possibile configurare un'attività personalizzata per l'esecuzione in un pool di macchine virtuali di **Azure Batch** o in un cluster di **Azure HDInsight** basato su Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbae-119">You can configure a custom activity to run on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="2dbae-120">Quando si usa Azure Batch, è possibile usare solo un pool esistente di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="2dbae-121">Quando invece si usa HDInsight, è possibile usare un cluster HDInsight esistente o un cluster creato automaticamente su richiesta in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="2dbae-122">La procedura dettagliata seguente riporta le istruzioni complete per creare un'attività .NET personalizzata e usarla in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-122">The following walkthrough provides step-by-step instructions for creating a custom .NET activity and using the custom activity in a pipeline.</span></span> <span data-ttu-id="2dbae-123">La procedura dettagliata usa il servizio collegato **Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-123">The walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="2dbae-124">Per usare invece un servizio collegato Azure HDInsight, si crea un servizio collegato di tipo **HDInsight** (il proprio cluster HDInsight) o **HDInsightOnDemand** (Data Factory crea un cluster di HDInsight su richiesta).</span><span class="sxs-lookup"><span data-stu-id="2dbae-124">To use an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="2dbae-125">Configurare quindi l'attività personalizzata per usare il servizio collegato HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-125">Then, configure custom activity to use the HDInsight linked service.</span></span> <span data-ttu-id="2dbae-126">Per i dettagli sull’uso di Azure HDInsight per eseguire l’attività personalizzata vedere [Usare i servizi collegati Azure HDInsight](#use-hdinsight-compute-service) .</span><span class="sxs-lookup"><span data-stu-id="2dbae-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight to run the custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="2dbae-127">Le attività .NET personalizzate sono eseguite solo su cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbae-127">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2dbae-128">Una soluzione alternativa a questa limitazione consiste nell'utilizzare l'attività MapReduce per eseguire codice Java personalizzato su un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="2dbae-128">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2dbae-129">Un'altra opzione è utilizzare un pool di macchine virtuali di Azure Batch per eseguire attività personalizzate anziché utilizzare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-129">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="2dbae-130">Non è possibile usare il gateway di gestione dati da un'attività personalizzata per accedere alle origini dati locali.</span><span class="sxs-lookup"><span data-stu-id="2dbae-130">It is not possible to use a Data Management Gateway from a custom activity to access on-premises data sources.</span></span> <span data-ttu-id="2dbae-131">Attualmente il [Gateway di gestione dati](data-factory-data-management-gateway.md) supporta solo le attività di copia e di stored procedure in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only the copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="2dbae-132">Procedura dettagliata: creare un'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="2dbae-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="2dbae-133">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2dbae-133">Prerequisites</span></span>
* <span data-ttu-id="2dbae-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="2dbae-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="2dbae-135">Scaricare e installare [.NET SDK di Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="2dbae-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="2dbae-136">Prerequisiti di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2dbae-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="2dbae-137">In questa procedura dettagliata vengono eseguite attività .NET personalizzate usando Azure Batch come risorsa di calcolo.</span><span class="sxs-lookup"><span data-stu-id="2dbae-137">In the walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="2dbae-138">**Azure Batch** è un servizio di piattaforma per eseguire in modo efficiente applicazioni parallele e HPC (High Performance Computing) su larga scala nel cloud.</span><span class="sxs-lookup"><span data-stu-id="2dbae-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="2dbae-139">Azure Batch pianifica l'esecuzione del lavoro a elevato utilizzo di calcolo su una **raccolta di macchine virtuali** gestita e può ridimensionare automaticamente le risorse di calcolo in base alle esigenze dei processi.</span><span class="sxs-lookup"><span data-stu-id="2dbae-139">Azure Batch schedules compute-intensive work to run on a managed **collection of virtual machines**, and can automatically scale compute resources to meet the needs of your jobs.</span></span> <span data-ttu-id="2dbae-140">Vedere l'articolo [Nozioni di base di Azure Batch][batch-technical-overview] per una panoramica dettagliata del servizio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of the Azure Batch service.</span></span>

<span data-ttu-id="2dbae-141">Per l'esercitazione creare un account Batch di Azure con un pool di VM.</span><span class="sxs-lookup"><span data-stu-id="2dbae-141">For the tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="2dbae-142">Di seguito sono riportati i passaggi necessari:</span><span class="sxs-lookup"><span data-stu-id="2dbae-142">Here are the steps:</span></span>

1. <span data-ttu-id="2dbae-143">Creare un **account di Azure Batch** tramite il [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2dbae-143">Create an **Azure Batch account** using the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="2dbae-144">Per istruzioni, vedere l'articolo su come [creare e gestire un account Azure Batch][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="2dbae-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="2dbae-145">Annotare il nome dell'account Azure Batch, la chiave account, l'URI e il nome del pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-145">Note down the Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="2dbae-146">È necessario creare un servizio collegato Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-146">You need them to create an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="2dbae-147">Nella home page per l'account Azure Batch, l'**URL** avrà il formato seguente: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="2dbae-147">On the home page for Azure Batch account, you see a **URL** in the following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="2dbae-148">In questo esempio, **myaccount** è il nome dell'account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-148">In this example, **myaccount** is the name of the Azure Batch account.</span></span> <span data-ttu-id="2dbae-149">L'URI usato nella definizione del servizio collegato è l'URL senza il nome dell'account.</span><span class="sxs-lookup"><span data-stu-id="2dbae-149">URI you use in the linked service definition is the URL without the name of the account.</span></span> <span data-ttu-id="2dbae-150">Ad esempio: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="2dbae-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="2dbae-151">Fare clic su **Chiavi** nel menu a sinistra e copiare la **CHIAVE DI ACCESSO PRIMARIA**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-151">Click **Keys** on the left menu, and copy the **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="2dbae-152">Per usare un pool esistente, fare clic su **Pool** nel menu e annotare l'**ID** del pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-152">To use an existing pool, click **Pools** on the menu, and note down the **ID** of the pool.</span></span> <span data-ttu-id="2dbae-153">Se non è disponibile un pool esistente, andare al passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="2dbae-153">If you don't have an existing pool, move to the next step.</span></span>     
2. <span data-ttu-id="2dbae-154">Creare un **pool di Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="2dbae-155">Nel menu a sinistra del [portale di Azure](https://portal.azure.com) fare clic su **Esplora** e quindi su **Account Batch**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-155">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="2dbae-156">Selezionare il proprio account Azure Batch per aprire il pannello **Account Batch** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-156">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
   3. <span data-ttu-id="2dbae-157">Fare clic sul riquadro **Pool** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="2dbae-158">Nel riquadro **pool** fare clic sul pulsante Aggiungi nella barra degli strumenti per aggiungere un pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-158">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
      1. <span data-ttu-id="2dbae-159">Immettere un ID per il pool (ID pool).</span><span class="sxs-lookup"><span data-stu-id="2dbae-159">Enter an ID for the pool (Pool ID).</span></span> <span data-ttu-id="2dbae-160">Prendere nota dell' **ID del pool**perché sarà necessario durante la creazione della soluzione Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-160">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
      2. <span data-ttu-id="2dbae-161">Specificare **Windows Server 2012 R2** per l'impostazione Famiglia di sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="2dbae-161">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
      3. <span data-ttu-id="2dbae-162">Selezionare un **piano tariffario per il nodo**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="2dbae-163">Immettere **2** come valore per l'impostazione **Pool dedicati di destinazione**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-163">Enter **2** as value for the **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="2dbae-164">Immettere **2** come valore per l'impostazione **Numero massimo attività per nodo**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-164">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="2dbae-165">Fare clic su **OK** per creare il pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-165">Click **OK** to create the pool.</span></span>
   6. <span data-ttu-id="2dbae-166">Annotare l'**ID** del pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-166">Note down the **ID** of the pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="2dbae-167">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="2dbae-167">High-level steps</span></span>
<span data-ttu-id="2dbae-168">Eseguire i seguenti due passaggi di alto livello come parte di questa procedura dettagliata:</span><span class="sxs-lookup"><span data-stu-id="2dbae-168">Here are the two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="2dbae-169">Creare un'attività personalizzata contenente una semplice logica di trasformazione/elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2dbae-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="2dbae-170">Creare una data factory di Azure con una pipeline che usa l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-170">Create an Azure data factory with a pipeline that uses the custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="2dbae-171">Creare un'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="2dbae-171">Create a custom activity</span></span>
<span data-ttu-id="2dbae-172">Per creare un'attività personalizzata .NET, è necessario creare un progetto **Libreria di classi .NET** con una classe che implementa l'**interfaccia IDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-172">To create a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="2dbae-173">Questa interfaccia ha un solo metodo, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , e la relativa firma è:</span><span class="sxs-lookup"><span data-stu-id="2dbae-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="2dbae-174">Il metodo accetta quattro parametri:</span><span class="sxs-lookup"><span data-stu-id="2dbae-174">The method takes four parameters:</span></span>

- <span data-ttu-id="2dbae-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-175">**linkedServices**.</span></span> <span data-ttu-id="2dbae-176">Questa proprietà è un elenco enumerabile di servizi collegati di archiviazione dati a cui fanno riferimento i set di dati di input/output per l'attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for the activity.</span></span>   
- <span data-ttu-id="2dbae-177">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-177">**datasets**.</span></span> <span data-ttu-id="2dbae-178">Questa proprietà è un elenco enumerabile di set di dati di input/output per l'attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-178">This property is an enumerable list of input/output datasets for the activity.</span></span> <span data-ttu-id="2dbae-179">È possibile usare questo parametro per ottenere le posizioni e gli schemi definiti da set di dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="2dbae-179">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="2dbae-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-180">**activity**.</span></span> <span data-ttu-id="2dbae-181">Questa proprietà rappresenta l'attività corrente.</span><span class="sxs-lookup"><span data-stu-id="2dbae-181">This property represents the current activity.</span></span> <span data-ttu-id="2dbae-182">Può essere usata per accedere alle proprietà estese associate all'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-182">It can be used to access extended properties associated with the custom activity.</span></span> <span data-ttu-id="2dbae-183">Per i dettagli, vedere [Accedere a tutte le proprietà estese](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="2dbae-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="2dbae-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-184">**logger**.</span></span> <span data-ttu-id="2dbae-185">Questo oggetto consente di scrivere commenti di debug che verranno visualizzati nel log dell'utente per la pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-185">This object lets you write debug comments that surface in the user log for the pipeline.</span></span>

<span data-ttu-id="2dbae-186">Il metodo restituisce un dizionario che può essere usato per concatenare le attività personalizzate in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2dbae-186">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="2dbae-187">Questa funzionalità non è ancora implementata, quindi il metodo restituisce un dizionario vuoto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-187">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="2dbae-188">Procedura</span><span class="sxs-lookup"><span data-stu-id="2dbae-188">Procedure</span></span>
1. <span data-ttu-id="2dbae-189">Creare un progetto **Libreria di classi .NET** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="2dbae-190">Avviare <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> oppure <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="2dbae-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="2dbae-191">Fare clic su <b>File</b>, scegliere <b>Nuovo</b> e quindi fare clic su <b>Progetto</b>.</span><span class="sxs-lookup"><span data-stu-id="2dbae-191">Click <b>File</b>, point to <b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="2dbae-192">Espandere <b>Modelli</b> e quindi selezionare <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="2dbae-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="2dbae-193">In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET per sviluppare l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-193">In this walkthrough, you use C#, but you can use any .NET language to develop the custom activity.</span></span></li>
     <li><span data-ttu-id="2dbae-194">Selezionare la <b>libreria di classi</b> dall'elenco relativo ai tipi di progetto visualizzato a destra.</span><span class="sxs-lookup"><span data-stu-id="2dbae-194">Select <b>Class Library</b> from the list of project types on the right.</span></span> <span data-ttu-id="2dbae-195">In Visual Studio 2017, scegliere <b>Libreria di classi (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="2dbae-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="2dbae-196">Immettere <b>MyDotNetActivity</b> per <b>Nome</b>.</span><span class="sxs-lookup"><span data-stu-id="2dbae-196">Enter <b>MyDotNetActivity</b> for the <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="2dbae-197">Selezionare <b>C:\ADFGetStarted</b> per <b>Percorso</b>.</span><span class="sxs-lookup"><span data-stu-id="2dbae-197">Select <b>C:\ADFGetStarted</b> for the <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="2dbae-198">Fare clic su <b>OK</b> per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-198">Click <b>OK</b> to create the project.</span></span></li>
   </ol><span data-ttu-id="2dbae-199">
2. Fare clic su **Strumenti**, scegliere **Gestione pacchetti NuGet** e quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-199">
2. Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="2dbae-200">3.</span><span class="sxs-lookup"><span data-stu-id="2dbae-200">3.</span></span> <span data-ttu-id="2dbae-201">In Console di Gestione pacchetti eseguire il comando seguente per importare **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-201">In the Package Manager Console, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="2dbae-202">Importare nel progetto il pacchetto NuGet **Azure Storage** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-202">Import the **Azure Storage** NuGet package in to the project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="2dbae-203">L'utilità di avvio del servizio Data Factory richiede la versione 4.3 di WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="2dbae-203">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="2dbae-204">Se si aggiunge un riferimento a una versione successiva dell'assembly di Archiviazione di Azure nel progetto di attività personalizzato, viene visualizzato un errore durante l'esecuzione dell'attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-204">If you add a reference to a later version of Azure Storage assembly in your custom activity project, you see an error when the activity executes.</span></span> <span data-ttu-id="2dbae-205">Per risolvere l'errore, vedere la sezione [Isolamento di AppDomain](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="2dbae-205">To resolve the error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="2dbae-206">Aggiungere le seguenti istruzioni **using** al file di origine nel progetto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-206">Add the following **using** statements to the source file in the project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="2dbae-207">Modificare il nome dello **spazio dei nomi** in **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-207">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="2dbae-208">Modificare il nome della classe in **MyDotNetActivity** e derivarlo dall'interfaccia **IDotNetActivity** come illustrato nel frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2dbae-208">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown in the following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="2dbae-209">Implementare (aggiungere) il metodo **Execute** dell'interfaccia **IDotNetActivity** nella classe **MyDotNetActivity** e copiare il seguente codice di esempio nel metodo.</span><span class="sxs-lookup"><span data-stu-id="2dbae-209">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span>

    <span data-ttu-id="2dbae-210">Nell’esempio seguente si conta il numero di occorrenze del termine di ricerca (“Microsoft”) in ogni BLOB associato con una sezione dei dati.</span><span class="sxs-lookup"><span data-stu-id="2dbae-210">The following sample counts the number of occurrences of the search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    
    public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
    {
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // to log information, use the logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get the input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables to hold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from the dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and the other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get the first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using the same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get the connection string in the linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get the folder path from the input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass the connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize the continuation token before using it in the do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get the list of input blobs from the input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns the number of occurrences of
            // the search term (“Microsoft”) in each blob associated
               // with the data slice. definition of the method is shown in the next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for the output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get the folder path from the output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log the output folder path   
        logger.Write("Writing blob to the folder: {0}", folderPath);
    
        // create a storage object for the output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write the name of the file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log the output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload the output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} to the output blob", output);
        outputBlob.UploadText(output);
    
        // The dictionary can be used to chain custom activities together in the future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="2dbae-211">Aggiungere i seguenti metodi helper:</span><span class="sxs-lookup"><span data-stu-id="2dbae-211">Add the following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of the dataset   
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the folder path found in the type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of the dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return the blob/file name in the type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
        string output = string.Empty;
        logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
        foreach (IListBlobItem listBlobItem in Bresult.Results)
        {
            CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
            if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
            {
                string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
                logger.Write("input blob text: {0}", blobText);
                string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
                var matchQuery = from word in source
                                 where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                 select word;
                int wordCount = matchQuery.Count();
                output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="2dbae-212">Il metodo GetFolderPath restituisce il percorso della cartella a cui punta il set di dati e il metodo GetFileName restituisce il nome del BLOB o del file a cui punta il set di dati.</span><span class="sxs-lookup"><span data-stu-id="2dbae-212">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span> <span data-ttu-id="2dbae-213">Se sono presenti definizioni folderPath che usano variabili come {Year}, {Month}, {Day} e così via, il metodo restituisce la stringa così com’è, senza sostituirla con i valori di runtime.</span><span class="sxs-lookup"><span data-stu-id="2dbae-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., the method returns the string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="2dbae-214">Per i dettagli sull'accesso a SliceStart, SliceEnd e così via, vedere [Accedere a tutte le proprietà estese](#access-extended-properties) .</span><span class="sxs-lookup"><span data-stu-id="2dbae-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="2dbae-215">Il metodo Calculate calcola il numero di istanze della parola chiave "Microsoft" nei file di input (BLOB nella cartella).</span><span class="sxs-lookup"><span data-stu-id="2dbae-215">The Calculate method calculates the number of instances of keyword Microsoft in the input files (blobs in the folder).</span></span> <span data-ttu-id="2dbae-216">Il termine di ricerca ("Microsoft") è hardcoded nel codice.</span><span class="sxs-lookup"><span data-stu-id="2dbae-216">The search term (“Microsoft”) is hard-coded in the code.</span></span>
10. <span data-ttu-id="2dbae-217">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-217">Compile the project.</span></span> <span data-ttu-id="2dbae-218">Fare clic su **Compila** dal menu e scegliere **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-218">Click **Build** from the menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2dbae-219">Impostare la versione 4.5.2 di .NET Framework come framework di destinazione per il progetto: fare clic con il pulsante destre sul progetto e quindi su **Proprietà** per impostare il framework di destinazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-219">Set 4.5.2 version of .NET Framework as the target framework for your project: right-click the project, and click **Properties** to set the target framework.</span></span> <span data-ttu-id="2dbae-220">Data factory non supporta le attività personalizzate compilate in versioni di .NET Framework successive alla 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="2dbae-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="2dbae-221">Avviare **Esplora risorse** e passare alla cartella **bin\debug** o **bin\release**, a seconda del tipo di compilazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-221">Launch **Windows Explorer**, and navigate to **bin\debug** or **bin\release** folder depending on the type of build.</span></span>
12. <span data-ttu-id="2dbae-222">Creare un file ZIP **MyDotNetActivity.zip** che contiene tutti i file binari disponibili nella cartella <project folder>\bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="2dbae-222">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="2dbae-223">Includere il file **MyDotNetActivity.pdb** per ottenere altri dettagli, ad esempio il numero della riga nel codice sorgente che ha causato il problema in caso di errore.</span><span class="sxs-lookup"><span data-stu-id="2dbae-223">Include the **MyDotNetActivity.pdb** file so that you get additional details such as line number in the source code that caused the issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="2dbae-224">Tutti i file contenuti nel file con estensione zip dell'attività personalizzata devono trovarsi nel **livello principale** senza sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="2dbae-224">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>

    ![File di output binari](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="2dbae-226">Se non è già presente, creare un contenitore BLOB denominato **customactivitycontainer**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="2dbae-227">Caricare MyDotNetActivity.zip come BLOB in customactivitycontainer in un'Archiviazione BLOB di Azure **di uso generico**, non ad accesso frequente/sporadico, a cui si fa riferimento da AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="2dbae-227">Upload MyDotNetActivity.zip as a blob to the customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="2dbae-228">Se si aggiunge questo progetto di attività .NET a una soluzione in Visual Studio che contiene un progetto Data Factory e si aggiunge un riferimento al progetto dell'attività .NET dal progetto dell'applicazione Data Factory, non è necessario eseguire gli ultimi due passaggi, ovvero creare manualmente il file ZIP e caricarlo nell'Archiviazione BLOB di Azure di uso generico.</span><span class="sxs-lookup"><span data-stu-id="2dbae-228">If you add this .NET activity project to a solution in Visual Studio that contains a Data Factory project, and add a reference to .NET activity project from the Data Factory application project, you do not need to perform the last two steps of manually creating the zip file and uploading it to the general-purpose Azure blob storage.</span></span> <span data-ttu-id="2dbae-229">Quando si pubblicano entità Data Factory utilizzando Visual Studio, questi passaggi vengono eseguiti automaticamente dal processo di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by the publishing process.</span></span> <span data-ttu-id="2dbae-230">Per altre informazioni, vedere la sezione [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) (Progetto Data Factory in Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="2dbae-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="2dbae-231">Creare una pipeline con attività personalizzate</span><span class="sxs-lookup"><span data-stu-id="2dbae-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="2dbae-232">È stata creata un'attività personalizzata ed è stato caricato il file zip con file binari in un contenitore BLOB in un account di Archiviazione di Azure **di uso generico**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-232">You have created a custom activity and uploaded the zip file with binaries to a blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="2dbae-233">Questa sezione illustra come creare una data factory di Azure con una pipeline che usa l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-233">In this section, you create an Azure data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="2dbae-234">Il set di dati di input per l'attività personalizzata rappresenta i BLOB (file) nella cartella customactivityinput del contenitore adftutorial nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="2dbae-234">The input dataset for the custom activity represents blobs (files) in the customactivityinput folder of adftutorial container in the blob storage.</span></span> <span data-ttu-id="2dbae-235">Il set di dati di output per l'attività rappresenta i BLOB di output nella cartella customactivityoutput del contenitore adftutorial nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="2dbae-235">The output dataset for the activity represents output blobs in the customactivityoutput folder of adftutorial container in the blob storage.</span></span>

<span data-ttu-id="2dbae-236">Creare il file **file.txt** con il contenuto seguente e caricarlo nella cartella **customactivityinput** del contenitore **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-236">Create **file.txt** file with the following content and upload it to **customactivityinput** folder of the **adftutorial** container.</span></span> <span data-ttu-id="2dbae-237">Se non esiste ancora, creare il contenitore adftutorial.</span><span class="sxs-lookup"><span data-stu-id="2dbae-237">Create the adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="2dbae-238">La cartella di input corrisponde a una sezione in Azure Data Factory, anche se la cartella contiene due o più file.</span><span class="sxs-lookup"><span data-stu-id="2dbae-238">The input folder corresponds to a slice in Azure Data Factory even if the folder has two or more files.</span></span> <span data-ttu-id="2dbae-239">Quando ogni sezione viene elaborata dalla pipeline, l'attività personalizzata esegue l'iterazione di tutti i BLOB nella cartella di input per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-239">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="2dbae-240">Verrà visualizzato un file di output nella cartella adftutorial\customactivityoutput con una o più righe, pari al numero di BLOB nella cartella di input:</span><span class="sxs-lookup"><span data-stu-id="2dbae-240">You see one output file with in the adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in the input folder):</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="2dbae-241">Di seguito sono elencati i passaggi da eseguire in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="2dbae-241">Here are the steps you perform in this section:</span></span>

1. <span data-ttu-id="2dbae-242">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="2dbae-243">Creare **servizi collegati** per il pool di VM di Azure Batch in cui viene eseguita l'attività personalizzata e l'Archiviazione di Azure che contiene i BLOB di input e di output.</span><span class="sxs-lookup"><span data-stu-id="2dbae-243">Create **Linked services** for the Azure Batch pool of VMs on which the custom activity runs and the Azure Storage that holds the input/output blobs.</span></span>
3. <span data-ttu-id="2dbae-244">Creare i **set di dati** di input e di output che rappresentano l'input e l'output dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-244">Create input and output **datasets** that represent input and output of the custom activity.</span></span>
4. <span data-ttu-id="2dbae-245">Creare una **pipeline** che usa l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-245">Create a **pipeline** that uses the custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="2dbae-246">Creare il file **file.txt** e caricarlo in un contenitore BLOB, se l'operazione non è ancora stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="2dbae-246">Create the **file.txt** and upload it to a blob container if you haven't already done so.</span></span> <span data-ttu-id="2dbae-247">Vedere le istruzioni nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="2dbae-247">See instructions in the preceding section.</span></span>   

### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="2dbae-248">Passaggio 1: Creare la data factory</span><span class="sxs-lookup"><span data-stu-id="2dbae-248">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="2dbae-249">Dopo l'accesso al portale di Azure, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2dbae-249">After logging in to the Azure portal, do the following steps:</span></span>
   1. <span data-ttu-id="2dbae-250">Fare clic su **Nuovo** nel menu a sinistra.</span><span class="sxs-lookup"><span data-stu-id="2dbae-250">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="2dbae-251">Fare clic su **Dati e analisi** nel pannello **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-251">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="2dbae-252">Fare clic su **Data factory** nel pannello **Analisi dei dati**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-252">Click **Data Factory** on the **Data analytics** blade.</span></span>
   
    ![Menu Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="2dbae-254">Nel pannello **Nuova data factory** immettere **CustomActivityFactory** come Nome.</span><span class="sxs-lookup"><span data-stu-id="2dbae-254">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="2dbae-255">È necessario specificare un nome univoco globale per l'istanza di Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-255">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="2dbae-256">Se viene visualizzato l'errore **Il nome "CustomActivityFactory" per la data factory non è disponibile**, cambiare il nome della data factory, ad esempio, **nomeutenteCustomActivityFactory**, e provare di nuovo a crearla.</span><span class="sxs-lookup"><span data-stu-id="2dbae-256">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Pannello Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="2dbae-258">Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="2dbae-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="2dbae-259">Verificare se la **sottoscrizione** e l'**area** in cui si vuole creare la data factory sono quelle corrette.</span><span class="sxs-lookup"><span data-stu-id="2dbae-259">Verify that you are using the correct **subscription** and **region** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="2dbae-260">Fare clic su **Crea** nel pannello **Nuova data factory**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-260">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="2dbae-261">Nel **Dashboard** del portale di Azure verrà visualizzata la data factory in fase di creazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-261">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="2dbae-262">Dopo aver creato la data factory, verrà visualizzato il pannello corrispondente con elencato il contenuto della data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-262">After the data factory has been created successfully, you see the Data Factory blade, which shows you the contents of the data factory.</span></span>
    
    ![Pannello Data factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="2dbae-264">Passaggio 2: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="2dbae-264">Step 2: Create linked services</span></span>
<span data-ttu-id="2dbae-265">I servizi collegati collegano archivi dati o servizi di calcolo a una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-265">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="2dbae-266">In questo passaggio si collegheranno l'account di archiviazione di Azure e l'account Azure Batch alla data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-266">In this step, you link your Azure Storage account and Azure Batch account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="2dbae-267">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2dbae-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="2dbae-268">Fare clic sul riquadro **Creare e distribuire** nel pannello **DATA FACTORY** per **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-268">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="2dbae-269">Viene visualizzato l'editor di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-269">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="2dbae-270">Fare clic su **Nuovo archivio dati** sulla barra dei comandi e scegliere **Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-270">Click **New data store** on the command bar and choose **Azure storage**.</span></span> <span data-ttu-id="2dbae-271">Nell'editor verrà visualizzato lo script JSON per la creazione di un servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-271">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>
    
    ![Nuovo archivio dati - Archiviazione di Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="2dbae-273">Sostituire `<accountname>` con il nome dell'account di archiviazione di Azure e `<accountkey>` con la chiave di accesso dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of the Azure storage account.</span></span> <span data-ttu-id="2dbae-274">Per informazioni su come ottenere la chiave di accesso alle risorse di archiviazione, vedere la sezione [Visualizzare, copiare e rigenerare le chiavi di accesso nelle risorse di archiviazione](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="2dbae-274">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Servizio collegato Archiviazione di Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="2dbae-276">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-276">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="2dbae-277">Creare il servizio collegato Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2dbae-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="2dbae-278">Nell'editor di Data Factory fare clic su **... Altro** sulla barra dei comandi, fare clic su **Nuovo calcolo** e quindi selezionare **Azure Batch** dal menu.</span><span class="sxs-lookup"><span data-stu-id="2dbae-278">In the Data Factory Editor, click **... More** on the command bar, click **New compute**, and then select **Azure Batch** from the menu.</span></span>

    ![Nuovo calcolo - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="2dbae-280">Apportare le modifiche seguenti allo script JSON:</span><span class="sxs-lookup"><span data-stu-id="2dbae-280">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="2dbae-281">Specificare il nome dell'account Azure Batch per la proprietà **accountName** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-281">Specify Azure Batch account name for the **accountName** property.</span></span> <span data-ttu-id="2dbae-282">L'**URL** nel **pannello dell'account Azure Batch** è nel formato seguente: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="2dbae-282">The **URL** from the **Azure Batch account blade** is in the following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="2dbae-283">Per la proprietà **batchUri** nel JSON è necessario rimuovere `accountname.` dall'URL e usare il `accountname` per la `accountName` proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="2dbae-283">For the **batchUri** property in the JSON, you need to remove `accountname.` from the URL and use the `accountname` for the `accountName` JSON property.</span></span>
   2. <span data-ttu-id="2dbae-284">Specificare la chiave dell'account Azure Batch per la proprietà **accessKey** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-284">Specify the Azure Batch account key for the **accessKey** property.</span></span>
   3. <span data-ttu-id="2dbae-285">Specificare il nome del pool che è stato creato come parte dei prerequisiti per la proprietà **poolName** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-285">Specify the name of the pool you created as part of prerequisites for the **poolName** property.</span></span> <span data-ttu-id="2dbae-286">È anche possibile specificare l'ID del pool anziché il nome del pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-286">You can also specify the ID of the pool instead of the name of the pool.</span></span>
   4. <span data-ttu-id="2dbae-287">Specificare l'URI di Azure Batch per la proprietà **batchUri** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-287">Specify Azure Batch URI for the **batchUri** property.</span></span> <span data-ttu-id="2dbae-288">Esempio: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="2dbae-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="2dbae-289">Per la proprietà **AzureStorageLinkedService** for the **linkedServiceName** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-289">Specify the **AzureStorageLinkedService** for the **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="2dbae-290">Per la proprietà **poolName** è anche possibile specificare l'ID del pool anziché il nome del pool.</span><span class="sxs-lookup"><span data-stu-id="2dbae-290">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="2dbae-291">Il servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure come accade per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-291">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="2dbae-292">È possibile usare solo il proprio pool di Batch di Azure in una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="2dbae-293">Passaggio 3: Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="2dbae-293">Step 3: Create datasets</span></span>
<span data-ttu-id="2dbae-294">In questo passaggio vengono creati set di dati per rappresentare i dati di input e di output.</span><span class="sxs-lookup"><span data-stu-id="2dbae-294">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="2dbae-295">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="2dbae-295">Create input dataset</span></span>
1. <span data-ttu-id="2dbae-296">Nell'**editor** della data factory fare clic su **... Altro** sulla barra dei comandi, fare clic su **Nuovo set di dati** e quindi selezionare **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-296">In the **Editor** for the Data Factory, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="2dbae-297">Sostituire il codice JSON nel riquadro a destra con il frammento JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="2dbae-297">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
         },
         "availability": {
             "frequency": "Hour",
             "interval": 1
         },
         "external": true,
         "policy": {}
     }
    }
    ```

   <span data-ttu-id="2dbae-298">Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2016-11-16T00:00:00Z e ora di fine: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="2dbae-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="2dbae-299">Viene pianificata per produrre dati ogni ora, in modo da ottenere cinque sezioni di input/output tra **00**:00:00 -> **05**:00:00.</span><span class="sxs-lookup"><span data-stu-id="2dbae-299">It is scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="2dbae-300">La **frequenza** e l'**intervallo** per il set di dati di input sono impostati su **Ora** e **1**. Ciò significa che la sezione di input è disponibile ogni ora.</span><span class="sxs-lookup"><span data-stu-id="2dbae-300">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span> <span data-ttu-id="2dbae-301">In questo esempio si tratta dello stesso file (file.txt) che si trova nella cartella di input.</span><span class="sxs-lookup"><span data-stu-id="2dbae-301">In this sample, it is the same file (file.txt) in the intputfolder.</span></span>

   <span data-ttu-id="2dbae-302">Sono indicate le ore di inizio per ogni sezione, rappresentate dalla variabile di sistema SliceStart nel precedente frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="2dbae-302">Here are the start times for each slice, which is represented by SliceStart system variable in the above JSON snippet.</span></span>
3. <span data-ttu-id="2dbae-303">Fare clic su **Distribuisci** sulla barra degli strumenti per creare e distribuire **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-303">Click **Deploy** on the toolbar to create and deploy the **InputDataset**.</span></span> <span data-ttu-id="2dbae-304">Controllare che sulla barra del titolo dell'editor sia visualizzato un messaggio simile a **LA CREAZIONE DELLA TABELLA È STATA COMPLETATA** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-304">Confirm that you see the **TABLE CREATED SUCCESSFULLY** message on the title bar of the Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="2dbae-305">Creare un set di dati di output</span><span class="sxs-lookup"><span data-stu-id="2dbae-305">Create an output dataset</span></span>
1. <span data-ttu-id="2dbae-306">Nell'**editor di Data Factory** fare clic su **... Altro** sulla barra dei comandi, fare clic su **Nuovo set di dati** e quindi selezionare **Archivio BLOB di Azure**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-306">In the **Data Factory editor**, click **... More** on the command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="2dbae-307">Sostituire lo script JSON nel riquadro a destra con il seguente script JSON:</span><span class="sxs-lookup"><span data-stu-id="2dbae-307">Replace the JSON script in the right pane with the following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
                "partitionedBy": [
                    {
                        "name": "slice",
                        "value": {
                            "type": "DateTime",
                            "date": "SliceStart",
                            "format": "yyyy-MM-dd-HH"
                        }
                    }
                ]
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```

     <span data-ttu-id="2dbae-308">Il percorso di output è **adftutorial/customactivityoutput/** e il nome del file di output è yyyy-MM-dd-HH.txt, dove yyyy-MM-dd-HH indica anno, mese, giorno e ora della sezione che viene generata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is the year, month, date, and hour of the slice being produced.</span></span> <span data-ttu-id="2dbae-309">Per informazioni dettagliate, vedere la [guida di riferimento per gli sviluppatori][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="2dbae-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="2dbae-310">Un BLOB o file di output viene generato per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="2dbae-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="2dbae-311">Ecco come viene denominato il file di output per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="2dbae-312">Tutti i file di output vengono generati in una cartella di output: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-312">All the output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="2dbae-313">Sezione</span><span class="sxs-lookup"><span data-stu-id="2dbae-313">Slice</span></span> | <span data-ttu-id="2dbae-314">Ora di inizio</span><span class="sxs-lookup"><span data-stu-id="2dbae-314">Start time</span></span> | <span data-ttu-id="2dbae-315">File di output</span><span class="sxs-lookup"><span data-stu-id="2dbae-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="2dbae-316">1</span><span class="sxs-lookup"><span data-stu-id="2dbae-316">1</span></span> |<span data-ttu-id="2dbae-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="2dbae-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="2dbae-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="2dbae-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="2dbae-319">2</span><span class="sxs-lookup"><span data-stu-id="2dbae-319">2</span></span> |<span data-ttu-id="2dbae-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="2dbae-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="2dbae-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="2dbae-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="2dbae-322">3</span><span class="sxs-lookup"><span data-stu-id="2dbae-322">3</span></span> |<span data-ttu-id="2dbae-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="2dbae-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="2dbae-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="2dbae-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="2dbae-325">4</span><span class="sxs-lookup"><span data-stu-id="2dbae-325">4</span></span> |<span data-ttu-id="2dbae-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="2dbae-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="2dbae-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="2dbae-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="2dbae-328">5</span><span class="sxs-lookup"><span data-stu-id="2dbae-328">5</span></span> |<span data-ttu-id="2dbae-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="2dbae-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="2dbae-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="2dbae-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="2dbae-331">Tenere presente che tutti i file in una cartella di input fanno parte di una sezione con le ore di inizio indicate in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2dbae-331">Remember that all the files in an input folder are part of a slice with the start times mentioned above.</span></span> <span data-ttu-id="2dbae-332">Quando la sezione viene elaborata, l'attività personalizzata esamina ogni file e produce una riga nel file di output con il numero di occorrenze del termine di ricerca ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="2dbae-332">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="2dbae-333">Se sono presenti tre file nella cartella di input, ci saranno tre righe nel file di output per ogni sezione oraria: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt e così via.</span><span class="sxs-lookup"><span data-stu-id="2dbae-333">If there are three files in the inputfolder, there are three lines in the output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="2dbae-334">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-334">To deploy the **OutputDataset**, click **Deploy** on the command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-the-custom-activity"></a><span data-ttu-id="2dbae-335">Creare ed eseguire una pipeline che usi l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="2dbae-335">Create and run a pipeline that uses the custom activity</span></span>
1. <span data-ttu-id="2dbae-336">Nell'editor di Data Factory fare clic su **... Altro** e quindi selezionare **Nuova pipeline** sulla barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2dbae-336">In the Data Factory Editor, click **... More**, and then select **New pipeline** on the command bar.</span></span> 
2. <span data-ttu-id="2dbae-337">Sostituire lo script JSON nel riquadro a destra con lo script JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="2dbae-337">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="2dbae-338">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="2dbae-338">Note the following points:</span></span>

   * <span data-ttu-id="2dbae-339">**Concorrenza** è impostata su **2** in modo che due sezioni siano elaborate in parallelo da 2 VM nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-339">**Concurrency** is set to **2** so that two slices are processed in parallel by 2 VMs in the Azure Batch pool.</span></span>
   * <span data-ttu-id="2dbae-340">Nella sezione delle attività esiste una sola attività, di tipo **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-340">There is one activity in the activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="2dbae-341">**AssemblyName** è impostato sul nome della DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-341">**AssemblyName** is set to the name of the DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="2dbae-342">**EntryPoint** è impostato su **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-342">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="2dbae-343">**PackageLinkedService** è impostato su **AzureStorageLinkedService** che punta all'archiviazione BLOB contenente il file ZIP dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-343">**PackageLinkedService** is set to **AzureStorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="2dbae-344">Se vengono usati account di archiviazione di Azure diversi per i file di input/output e per il file ZIP dell'attività personalizzata, è necessario creare un altro servizio collegato Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-344">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="2dbae-345">Questo articolo presuppone che venga usato lo stesso account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-345">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="2dbae-346">**PackageFile** è impostato su **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-346">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="2dbae-347">Ha il formato: contenitoreperlozip/nomedellozip.zip.</span><span class="sxs-lookup"><span data-stu-id="2dbae-347">It is in the format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="2dbae-348">L'attività personalizzata accetta **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="2dbae-348">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="2dbae-349">La proprietà linkedServiceName dell'attività personalizzata punta ad **AzureBatchLinkedService**per indicare ad Azure Data Factory che l'attività personalizzata deve essere eseguita nelle VM di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-349">The linkedServiceName property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch VMs.</span></span>
   * <span data-ttu-id="2dbae-350">La proprietà **isPaused** è impostata su **false** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2dbae-350">**isPaused** property is set to **false** by default.</span></span> <span data-ttu-id="2dbae-351">In questo esempio la pipeline viene eseguita immediatamente perché le sezioni hanno inizio nel passato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-351">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="2dbae-352">È possibile impostare questa proprietà su true per sospendere la pipeline e reimpostarla su false per riavviare la pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-352">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>
   * <span data-ttu-id="2dbae-353">L'ora di **inizio** e l'ora di **fine** hanno **cinque** ore di differenza e le sezioni vengono prodotte ogni ora, quindi la pipeline genera cinque sezioni.</span><span class="sxs-lookup"><span data-stu-id="2dbae-353">The **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>
3. <span data-ttu-id="2dbae-354">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire la pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-354">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-the-pipeline"></a><span data-ttu-id="2dbae-355">Monitorare la pipeline</span><span class="sxs-lookup"><span data-stu-id="2dbae-355">Monitor the pipeline</span></span>
1. <span data-ttu-id="2dbae-356">Nel pannello Data factory del portale di Azure fare clic su **Diagramma**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-356">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

    ![Riquadro Diagramma](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="2dbae-358">Nella vista Diagramma fare clic su OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="2dbae-358">In the Diagram View, now click the OutputDataset.</span></span>

    ![Vista diagramma](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="2dbae-360">Le cinque sezioni di output si trovano nello stato Ready.</span><span class="sxs-lookup"><span data-stu-id="2dbae-360">You should see that the five output slices are in the Ready state.</span></span> <span data-ttu-id="2dbae-361">Se non sono nello stato Ready, non sono state ancora generate.</span><span class="sxs-lookup"><span data-stu-id="2dbae-361">If they are not in the Ready state, they haven't been produced yet.</span></span> 

   ![Sezioni di output](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="2dbae-363">Verificare che i file di output vengano generati nell'archiviazione BLOB nel contenitore **adftutorial** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-363">Verify that the output files are generated in the blob storage in the **adftutorial** container.</span></span>

   ![output dell'attività personalizzata][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="2dbae-365">Se si apre il file di output, l'output visualizzato dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2dbae-365">If you open the output file, you should see the output similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="2dbae-366">Usare il [portale di Azure][azure-preview-portal] o i cmdlet di Azure PowerShell per monitorare l'istanza di Data Factory, le pipeline e i set di dati.</span><span class="sxs-lookup"><span data-stu-id="2dbae-366">Use the [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets to monitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="2dbae-367">I messaggi possono essere visualizzati da **ActivityLogger** nel codice per l'attività personalizzata nei log (specifically user-0.log) scaricabili dal portale o con i cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2dbae-367">You can see messages from the **ActivityLogger** in the code for the custom activity in the logs (specifically user-0.log) that you can download from the portal or using cmdlets.</span></span>

   ![scaricare i log dall'attività personalizzata][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="2dbae-369">Vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) per i passaggi dettagliati per il monitoraggio di set di dati e pipeline.</span><span class="sxs-lookup"><span data-stu-id="2dbae-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="2dbae-370">Progetto Data Factory in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2dbae-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="2dbae-371">È possibile creare e pubblicare le entità di Data Factory usando Visual Studio anziché il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="2dbae-372">Vedere gli articoli [Creare la prima pipeline con Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) e [Copiare dati da BLOB di Azure a SQL Azure](data-factory-copy-activity-tutorial-using-visual-studio.md) per altre informazioni sulla creazione e pubblicazione di entità di Data factory con Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dbae-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob to Azure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="2dbae-373">Se si sta creando il progetto Data Factory in Visual Studio, eseguire i passaggi aggiuntivi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2dbae-373">Do the following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="2dbae-374">Aggiungere il progetto Data Factory alla soluzione di Visual Studio che contiene il progetto dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-374">Add the Data Factory project to the Visual Studio solution that contains the custom activity project.</span></span> 
2. <span data-ttu-id="2dbae-375">Aggiungere un riferimento al progetto di attività .NET dal progetto Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-375">Add a reference to the .NET activity project from the Data Factory project.</span></span> <span data-ttu-id="2dbae-376">Fare clic con il pulsante destro del mouse sul progetto Data Factory, scegliere **Aggiungi**, quindi fare clic su **Riferimento**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-376">Right-click Data Factory project, point to **Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="2dbae-377">Nella finestra di dialogo **Aggiungi riferimento** selezionare il progetto **MyDotNetActivity** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-377">In the **Add Reference** dialog box, select the **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="2dbae-378">Creare e pubblicare la soluzione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-378">Build and publish the solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2dbae-379">Quando si pubblica l'entità Data Factory, viene creato automaticamente un file zip e caricato nel contenitore BLOB: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="2dbae-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded to the blob container: customactivitycontainer.</span></span> <span data-ttu-id="2dbae-380">Se il contenitore BLOB non esiste, anche questo viene automaticamente creato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-380">If the blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="2dbae-381">Integrazione di Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="2dbae-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="2dbae-382">Il servizio Data Factory crea un processo in Azure Batch denominato **adf-poolname: job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-382">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="2dbae-383">Fare clic su **Processi** nel menu di sinistra.</span><span class="sxs-lookup"><span data-stu-id="2dbae-383">Click **Jobs** from the left menu.</span></span> 

![Azure Data Factory: processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="2dbae-385">Per ogni esecuzione attività di una sezione viene creata un'attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="2dbae-386">Se cinque sezioni sono pronte per l'elaborazione, in questo processo vengono create cinque attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-386">If there are five slices ready to be processed, five tasks are created in this job.</span></span> <span data-ttu-id="2dbae-387">Se sono presenti più nodi di calcolo nel pool di batch, è possibile eseguire due o più sezioni in parallelo.</span><span class="sxs-lookup"><span data-stu-id="2dbae-387">If there are multiple compute nodes in the Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="2dbae-388">È anche possibile eseguire più sezioni nello stesso nodo di calcolo se l'impostazione per il numero massimo di attività per nodo di calcolo è > 1.</span><span class="sxs-lookup"><span data-stu-id="2dbae-388">If the maximum tasks per compute node is set to > 1, you can also have more than one slice running on the same compute.</span></span>

![Azure Data Factory: attività processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="2dbae-390">Il diagramma seguente illustra il rapporto tra attività di Azure Data Factory e Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-390">The following diagram illustrates the relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory e Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="2dbae-392">Errori in fase di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2dbae-392">Troubleshoot failures</span></span>
<span data-ttu-id="2dbae-393">La risoluzione dei problemi implica alcune tecniche di base:</span><span class="sxs-lookup"><span data-stu-id="2dbae-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="2dbae-394">Se viene visualizzato l'errore seguente, è possibile che si stia usando un'archiviazione BLOB ad accesso frequente/sporadico anziché usare un'Archiviazione BLOB di Azure di uso generico.</span><span class="sxs-lookup"><span data-stu-id="2dbae-394">If you see the following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="2dbae-395">Caricare il file zip in un **account di archiviazione di Azure di uso generico**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-395">Upload the zip file to a **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of the specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="2dbae-396">Se viene visualizzato l'errore seguente, verificare che il nome della classe nel file CS corrisponda al nome specificato per la proprietà **EntryPoint** nella pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="2dbae-396">If you see the following error, confirm that the name of the class in the CS file matches the name you specified for the **EntryPoint** property in the pipeline JSON.</span></span> <span data-ttu-id="2dbae-397">Nella procedura dettagliata il nome della classe è MyDotNetActivity e la proprietà EntryPoint nella pipeline JSON è MyDotNetActivityNS.**MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-397">In the walkthrough, name of the class is: MyDotNetActivity, and the EntryPoint in the JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement the type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="2dbae-398">Se i nomi corrispondono, verificare che tutti i file binari si trovino nella **cartella radice** del file ZIP.</span><span class="sxs-lookup"><span data-stu-id="2dbae-398">If the names do match, confirm that all the binaries are in the **root folder** of the zip file.</span></span> <span data-ttu-id="2dbae-399">Quando si apre il file ZIP, in altre parole, tutti i file devono trovarsi nella cartella radice, non nelle sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="2dbae-399">That is, when you open the zip file, you should see all the files in the root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="2dbae-400">Se la sezione di input non è impostata su **Ready**, verificare che la struttura di cartelle di input sia corretta e che **file.txt** sia presente nelle cartelle di input.</span><span class="sxs-lookup"><span data-stu-id="2dbae-400">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and **file.txt** exists in the input folders.</span></span>
3. <span data-ttu-id="2dbae-401">Nel metodo **Execute** dell'attività personalizzata usare l'oggetto **IActivityLogger** per registrare informazioni utili per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="2dbae-401">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="2dbae-402">I messaggi registrati vengono visualizzati nei file di log dell'utente, ovvero uno o più file denominati user-0.log, user-1.log, user-2.log e così via.</span><span class="sxs-lookup"><span data-stu-id="2dbae-402">The logged messages show up in the user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="2dbae-403">Nel pannello **OutputDataset** fare clic sulla sezione per visualizzare il relativo pannello **SEZIONE DATI**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-403">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="2dbae-404">Verranno visualizzate le **esecuzioni di attività** per quella sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="2dbae-405">Dovrebbe essere visualizzata una esecuzione attività per questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-405">You should see one activity run for the slice.</span></span> <span data-ttu-id="2dbae-406">Facendo clic su Esegui sulla barra dei comandi è possibile avviare un'altra esecuzione attività per la stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-406">If you click Run in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="2dbae-407">Quando si fa clic sull'esecuzione attività viene visualizzato il pannello **DETTAGLI ESECUZIONE ATTIVITÀ** con un elenco di file di log.</span><span class="sxs-lookup"><span data-stu-id="2dbae-407">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="2dbae-408">I messaggi registrati verranno visualizzati nel file user_0.log.</span><span class="sxs-lookup"><span data-stu-id="2dbae-408">You see logged messages in the user_0.log file.</span></span> <span data-ttu-id="2dbae-409">Quando si verifica un errore vengono visualizzate tre esecuzioni attività perché il numero di tentativi è impostato su 3 nel codice JSON della pipeline/attività.</span><span class="sxs-lookup"><span data-stu-id="2dbae-409">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="2dbae-410">Quando si fa clic sull'esecuzione attività vengono visualizzati i file di log che è possibile esaminare per risolvere l'errore.</span><span class="sxs-lookup"><span data-stu-id="2dbae-410">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   <span data-ttu-id="2dbae-411">Nell'elenco dei file di log fare clic su **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-411">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="2dbae-412">Nel riquadro destro sono riportati i risultati dell'uso del metodo **IActivityLogger.Write** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-412">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span> <span data-ttu-id="2dbae-413">Se non si vedono tutti i messaggi, controllare se ci sono altri file di log denominati: user_1.log, user_2.log e così via. Altrimenti il codice potrebbe essersi bloccato dopo l’ultimo messaggio registrato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, the code may have failed after the last logged message.</span></span>

   <span data-ttu-id="2dbae-414">Cercare anche eventuali messaggi di errore di sistema ed eccezioni nel file **system-0.log**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="2dbae-415">Includere il file **PDB** nel file ZIP in modo che i dettagli dell'errore contengano informazioni come lo **stack di chiamate** quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="2dbae-415">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="2dbae-416">Tutti i file contenuti nel file con estensione zip dell'attività personalizzata devono trovarsi nel **livello principale** senza sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="2dbae-416">All the files in the zip file for the custom activity must be at the **top level** with no sub folders.</span></span>
6. <span data-ttu-id="2dbae-417">Assicurarsi che **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip) e **packageLinkedService** (deve fare riferimento all'Archiviazione BLOB di Azure **di uso generico** che contiene il file ZIP) siano impostati su valori corretti.</span><span class="sxs-lookup"><span data-stu-id="2dbae-417">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the **general-purpose**Azure blob storage that contains the zip file) are set to correct values.</span></span>
7. <span data-ttu-id="2dbae-418">Se è stato risolto un errore e si vuole rielaborare la sezione, fare clic con il pulsante destro del mouse sulla sezione nel pannello **OutputDataset**, quindi scegliere **Esegui**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-418">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="2dbae-419">Se viene visualizzato l'errore seguente, si usa il pacchetto di Archiviazione di Azure con una versione > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="2dbae-419">If you see the following error, you are using the Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="2dbae-420">L'utilità di avvio del servizio Data Factory richiede la versione 4.3 di WindowsAzure.Storage.</span><span class="sxs-lookup"><span data-stu-id="2dbae-420">Data Factory service launcher requires the 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="2dbae-421">Per informazioni su una soluzione alternativa nel caso in cui sia necessario usare una versione più recente dell'assembly di Archiviazione di Azure, vedere la sezione [Isolamento di AppDomain](#appdomain-isolation).</span><span class="sxs-lookup"><span data-stu-id="2dbae-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use the later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="2dbae-422">Se è possibile usare la versione 4.3.0 del pacchetto di Archiviazione di Azure, rimuovere il riferimento esistente al pacchetto di Archiviazione di Azure con versione > 4.3.0</span><span class="sxs-lookup"><span data-stu-id="2dbae-422">If you can use the 4.3.0 version of Azure Storage package, remove the existing reference to Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="2dbae-423">ed eseguire il comando seguente dalla console di Gestione pacchetti NuGet.</span><span class="sxs-lookup"><span data-stu-id="2dbae-423">Then, run the following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="2dbae-424">Compilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-424">Build the project.</span></span> <span data-ttu-id="2dbae-425">Eliminare l'assembly Azure.Storage con versione > 4.3.0 dalla cartella bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="2dbae-425">Delete Azure.Storage assembly of version > 4.3.0 from the bin\Debug folder.</span></span> <span data-ttu-id="2dbae-426">Creare un file ZIP con i file binari e il file PDB.</span><span class="sxs-lookup"><span data-stu-id="2dbae-426">Create a zip file with binaries and the PDB file.</span></span> <span data-ttu-id="2dbae-427">Sostituire il file ZIP precedente con questo nel contenitore BLOB (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="2dbae-427">Replace the old zip file with this one in the blob container (customactivitycontainer).</span></span> <span data-ttu-id="2dbae-428">Eseguire di nuovo le sezioni non riuscite, facendo clic sul pulsante destro del mouse sulla sezione e scegliendo Esegui.</span><span class="sxs-lookup"><span data-stu-id="2dbae-428">Rerun the slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="2dbae-429">L'attività personalizzata non usa il file **app** dal pacchetto.</span><span class="sxs-lookup"><span data-stu-id="2dbae-429">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="2dbae-430">Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione, l'attività non funzionerà in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-430">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="2dbae-431">La procedura consigliata quando si usa Azure Batch consiste nell'inserire tutti i segreti in un **insieme di credenziali delle chiavi di Azure**, usare un'entità servizio basata su certificato per proteggere l'**insieme di credenziali** e distribuire il certificato nel pool di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="2dbae-431">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the **keyvault**, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="2dbae-432">L'attività personalizzata .NET può quindi accedere ai segreti dall'insieme di credenziali delle chiavi in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-432">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="2dbae-433">Questa è una soluzione generica e può essere ridimensionata per qualsiasi tipo di segreto, non solo per una stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-433">This solution is a generic solution and can scale to any type of secret, not just connection string.</span></span>

   <span data-ttu-id="2dbae-434">Esiste una soluzione più semplice, ma non consigliata: è possibile creare un **servizio collegato di Azure SQL** con le impostazioni della stringa di connessione, creare un set di dati che usa il servizio collegato e concatenare tale set di dati come set di dati di input fittizio all'attività .NET personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="2dbae-435">È quindi possibile accedere alla stringa di connessione del servizio collegato nel codice dell'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-435">You can then access the linked service's connection string in the custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="2dbae-436">Aggiornare l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="2dbae-436">Update custom activity</span></span>
<span data-ttu-id="2dbae-437">Per aggiornare il codice dell'attività personalizzata, compilarlo e caricare il file ZIP contenente i nuovi file binari nell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="2dbae-437">If you update the code for the custom activity, build it, and upload the zip file that contains new binaries to the blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="2dbae-438">Isolamento di AppDomain</span><span class="sxs-lookup"><span data-stu-id="2dbae-438">Appdomain isolation</span></span>
<span data-ttu-id="2dbae-439">Vedere l' [esempio sul passaggio fra AppDomain](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) che illustra come creare un'attività personalizzata che non sia vincolata alle versioni assembly usate dal servizio di avvio di Azure Data Factory, ad esempio WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x e così via.</span><span class="sxs-lookup"><span data-stu-id="2dbae-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how to create a custom activity that is not constrained to assembly versions used by the Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="2dbae-440">Accedere a tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="2dbae-440">Access extended properties</span></span>
<span data-ttu-id="2dbae-441">È possibile dichiarare estese le proprietà presenti nel codice JSON dell'attività come nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2dbae-441">You can declare extended properties in the activity JSON as shown in the following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="2dbae-442">Nell'esempio sono presenti due proprietà estese: **SliceStart** e **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-442">In the example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="2dbae-443">Il valore di SliceStart si basa sulla variabile di sistema SliceStart.</span><span class="sxs-lookup"><span data-stu-id="2dbae-443">The value for SliceStart is based on the SliceStart system variable.</span></span> <span data-ttu-id="2dbae-444">Per un elenco delle variabili di sistema supportate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="2dbae-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="2dbae-445">Il valore di DataFactoryName è hardcoded su CustomActivityFactory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-445">The value for DataFactoryName is hard-coded to CustomActivityFactory.</span></span>

<span data-ttu-id="2dbae-446">Per accedere alle proprietà estese nel metodo **Execute**, usare codice simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2dbae-446">To access these extended properties in the **Execute** method, use code similar to the following code:</span></span>

```csharp
// to get extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// to log all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="2dbae-447">Scalabilità automatica di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="2dbae-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="2dbae-448">È anche possibile creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** .</span><span class="sxs-lookup"><span data-stu-id="2dbae-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="2dbae-449">Ad esempio, è possibile creare un pool di Azure Batch con 0 VM dedicate e una formula di scalabilità basata sul numero di attività in sospeso.</span><span class="sxs-lookup"><span data-stu-id="2dbae-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="2dbae-450">La formula di esempio seguente consente di ottenere il comportamento seguente: quando il pool viene creato inizialmente, inizia con 1 macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="2dbae-450">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="2dbae-451">La metrica $PendingTasks definisce il numero di attività in esecuzione e quelle in coda.</span><span class="sxs-lookup"><span data-stu-id="2dbae-451">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="2dbae-452">La formula trova il numero medio di attività in sospeso negli ultimi 180 secondi e imposta TargetDedicated di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="2dbae-452">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="2dbae-453">Assicura che TargetDedicated non vada mai oltre 25 macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="2dbae-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="2dbae-454">Pertanto, quando vengono inviate nuove attività, il pool si espande automaticamente e al completamento delle attività le macchine virtuali diventano disponibili una alla volta e la scalabilità automatica le riduce.</span><span class="sxs-lookup"><span data-stu-id="2dbae-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="2dbae-455">È possibile regolare startingNumberOfVMs e maxNumberofVMs in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="2dbae-455">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="2dbae-456">Formula di scalabilità automatica:</span><span class="sxs-lookup"><span data-stu-id="2dbae-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="2dbae-457">Per i dettagli, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="2dbae-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="2dbae-458">Se il pool usa il valore predefinito [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), possono essere necessari 15-30 minuti perché il servizio Batch prepari la VM prima di eseguire l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-458">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="2dbae-459">Se il pool usa un valore autoScaleEvaluationInterval diverso, il servizio Batch può richiedere un valore autoScaleEvaluationInterval + 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="2dbae-459">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="2dbae-460">Usare il servizio di calcolo di HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dbae-460">Use HDInsight compute service</span></span>
<span data-ttu-id="2dbae-461">Nella procedura dettagliata è stato usato il calcolo Azure Batch per eseguire l'attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2dbae-461">In the walkthrough, you used Azure Batch compute to run the custom activity.</span></span> <span data-ttu-id="2dbae-462">È anche possibile usare il proprio cluster HDInsight basato su Windows o fare in modo che Data Factory crei un cluster HDInsight basato su Windows su richiesta ed esegua l'attività personalizzata sul cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have the custom activity run on the HDInsight cluster.</span></span> <span data-ttu-id="2dbae-463">Di seguito sono riportati i passaggi generali per usare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-463">Here are the high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dbae-464">Le attività .NET personalizzate sono eseguite solo su cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbae-464">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2dbae-465">Una soluzione alternativa a questa limitazione consiste nell'utilizzare l'attività MapReduce per eseguire codice Java personalizzato su un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="2dbae-465">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2dbae-466">Un'altra opzione è utilizzare un pool di macchine virtuali di Azure Batch per eseguire attività personalizzate anziché utilizzare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-466">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="2dbae-467">Creare un servizio collegato Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="2dbae-468">Usare il servizio collegato HDInsight al posto di **AzureBatchLinkedService** nella pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="2dbae-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in the pipeline JSON.</span></span>

<span data-ttu-id="2dbae-469">Se si vuole eseguire il test con la procedura dettagliata, modificare l'ora di **inizio** e **fine** per la pipeline per poter testare lo scenario con il servizio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-469">If you want to test it with the walkthrough, change **start** and **end** times for the pipeline so that you can test the scenario with the Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="2dbae-470">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="2dbae-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="2dbae-471">Il servizio Azure Data Factory supporta la creazione di un cluster su richiesta e lo usa per elaborare l'input per generare i dati di output.</span><span class="sxs-lookup"><span data-stu-id="2dbae-471">The Azure Data Factory service supports creation of an on-demand cluster and use it to process input to produce output data.</span></span> <span data-ttu-id="2dbae-472">È anche possibile usare il proprio cluster per eseguire la stessa operazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-472">You can also use your own cluster to perform the same.</span></span> <span data-ttu-id="2dbae-473">Quando si usa il cluster HDInsight su richiesta, viene creato un cluster per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="2dbae-474">Invece, se si usa il proprio cluster HDInsight, il cluster è pronto per elaborare immediatamente la sezione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-474">Whereas, if you use your own HDInsight cluster, the cluster is ready to process the slice immediately.</span></span> <span data-ttu-id="2dbae-475">Quindi, quando si usa un cluster su richiesta, i dati di output potrebbero non essere visualizzati tanto rapidamente quanto i dati nel proprio cluster.</span><span class="sxs-lookup"><span data-stu-id="2dbae-475">Therefore, when you use on-demand cluster, you may not see the output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2dbae-476">Al runtime, un'istanza di un'attività .NET viene eseguita solo in un nodo di lavoro nel cluster HDInsight, ma non può essere scalata al fine di essere eseguita in più nodi.</span><span class="sxs-lookup"><span data-stu-id="2dbae-476">At runtime, an instance of a .NET activity runs only on one worker node in the HDInsight cluster; it cannot be scaled to run on multiple nodes.</span></span> <span data-ttu-id="2dbae-477">È possibile eseguire più istanze di attività .NET contemporaneamente su diversi nodi del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-477">Multiple instances of .NET activity can run in parallel on different nodes of the HDInsight cluster.</span></span>
>
>

##### <a name="to-use-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="2dbae-478">Per usare un cluster HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="2dbae-478">To use an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="2dbae-479">Nel menu a sinistra del **portale di Azure**fare clic su **Creare e distribuire** nella home page di Data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-479">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="2dbae-480">Nell'editor di Data Factory fare clic su **Nuovo calcolo** sulla barra dei comandi, quindi scegliere **Cluster HDInsight su richiesta** dal menu.</span><span class="sxs-lookup"><span data-stu-id="2dbae-480">In the Data Factory Editor, click **New compute** from the command bar and select **On-demand HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="2dbae-481">Apportare le modifiche seguenti allo script JSON:</span><span class="sxs-lookup"><span data-stu-id="2dbae-481">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="2dbae-482">Per la proprietà **clusterSize** , specificare le dimensioni del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-482">For the **clusterSize** property, specify the size of the HDInsight cluster.</span></span>
   2. <span data-ttu-id="2dbae-483">Per la proprietà **timeToLive** specificare il tempo di inattività consentito per il cliente prima dell'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="2dbae-483">For the **timeToLive** property, specify how long the customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="2dbae-484">Per la proprietà **version** , specificare la versione di HDInsight da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="2dbae-484">For the **version** property, specify the HDInsight version you want to use.</span></span> <span data-ttu-id="2dbae-485">Se si esclude questa proprietà, verrà usata la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="2dbae-485">If you exclude this property, the latest version is used.</span></span>  
   4. <span data-ttu-id="2dbae-486">Per **linkedServiceName** specificare **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="2dbae-486">For the **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="2dbae-487">Le attività .NET personalizzate sono eseguite solo su cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="2dbae-487">The custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2dbae-488">Una soluzione alternativa a questa limitazione consiste nell'utilizzare l'attività MapReduce per eseguire codice Java personalizzato su un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="2dbae-488">A workaround for this limitation is to use the Map Reduce Activity to run custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="2dbae-489">Un'altra opzione è utilizzare un pool di macchine virtuali di Azure Batch per eseguire attività personalizzate anziché utilizzare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-489">Another option is to use an Azure Batch pool of VMs to run custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="2dbae-490">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-490">Click **Deploy** on the command bar to deploy the linked service.</span></span>

##### <a name="to-use-your-own-hdinsight-cluster"></a><span data-ttu-id="2dbae-491">Per usare il proprio cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2dbae-491">To use your own HDInsight cluster:</span></span>
1. <span data-ttu-id="2dbae-492">Nel menu a sinistra del **portale di Azure**fare clic su **Creare e distribuire** nella home page di Data factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-492">In the **Azure portal**, click **Author and Deploy** in the Data Factory home page.</span></span>
2. <span data-ttu-id="2dbae-493">Nell**editor di Data Factory** fare clic su **Nuovo calcolo** sulla barra dei comandi, quindi scegliere **Cluster HDInsight** dal menu.</span><span class="sxs-lookup"><span data-stu-id="2dbae-493">In the **Data Factory Editor**, click **New compute** from the command bar and select **HDInsight cluster** from the menu.</span></span>
3. <span data-ttu-id="2dbae-494">Apportare le modifiche seguenti allo script JSON:</span><span class="sxs-lookup"><span data-stu-id="2dbae-494">Make the following changes to the JSON script:</span></span>

   1. <span data-ttu-id="2dbae-495">Per la proprietà **clusterUri** , immettere l'URL di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-495">For the **clusterUri** property, enter the URL for your HDInsight.</span></span> <span data-ttu-id="2dbae-496">Ad esempio: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="2dbae-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="2dbae-497">Per la proprietà **UserName** , immettere il nome dell'utente che ha accesso al cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dbae-497">For the **UserName** property, enter the user name who has access to the HDInsight cluster.</span></span>
   3. <span data-ttu-id="2dbae-498">Per la proprietà **Password** , immettere la password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="2dbae-498">For the **Password** property, enter the password for the user.</span></span>
   4. <span data-ttu-id="2dbae-499">Per la proprietà **LinkedServiceName**, immettere **AzureStorageLinkedService**,</span><span class="sxs-lookup"><span data-stu-id="2dbae-499">For the **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="2dbae-500">Fare clic su **Distribuisci** sulla barra dei comandi per distribuire il servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="2dbae-500">Click **Deploy** on the command bar to deploy the linked service.</span></span>

<span data-ttu-id="2dbae-501">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="2dbae-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="2dbae-502">Nella **pipeline JSON**usare il servizio collegato HDInsight, proprio o su richiesta:</span><span class="sxs-lookup"><span data-stu-id="2dbae-502">In the **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="2dbae-503">Creazione di un’attività personalizzata tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2dbae-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="2dbae-504">Nella procedura dettagliata di questo articolo, si crea una data factory con una pipeline che usa l'attività personalizzata tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbae-504">In the walkthrough in this article, you create a data factory with a pipeline that uses the custom activity by using the Azure portal.</span></span> <span data-ttu-id="2dbae-505">Il codice seguente illustra invece come creare la data factory con .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2dbae-505">The following code shows you how to create the data factory by using .NET SDK instead.</span></span> <span data-ttu-id="2dbae-506">È possibile trovare altre informazioni sull'uso di SDK per creare pipeline a livello di codice nell'articolo sulla [creazione di una pipeline con attività di copia tramite API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md).</span><span class="sxs-lookup"><span data-stu-id="2dbae-506">You can find more details about using SDK to programmatically create pipelines in the [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with the name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need to set slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed to acquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="2dbae-507">Eseguire il debug di attività personalizzate in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2dbae-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="2dbae-508">L'esempio relativo all'[ambiente locale di Azure Data Factory](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) su GitHub include uno strumento che consente di eseguire il debug di attività .NET personalizzate all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dbae-508">The [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you to debug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="2dbae-509">Attività personalizzata di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="2dbae-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="2dbae-510">Esempio</span><span class="sxs-lookup"><span data-stu-id="2dbae-510">Sample</span></span> | <span data-ttu-id="2dbae-511">Funzioni delle attività personalizzate</span><span class="sxs-lookup"><span data-stu-id="2dbae-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="2dbae-512">[HttpDataDownloaderSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)(Esempio relativo al downloader dati HTTP).</span><span class="sxs-lookup"><span data-stu-id="2dbae-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="2dbae-513">Scarica i dati da un endpoint HTTP per l'archivio BLOB di Azure usando l'attività personalizzata C# in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2dbae-513">Downloads data from an HTTP Endpoint to Azure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="2dbae-514">Esempio di analisi del sentimento su Twitter</span><span class="sxs-lookup"><span data-stu-id="2dbae-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="2dbae-515">Chiama un modello ML di Azure ed esegue l'analisi del sentimento, l'assegnazione dei punteggi, la stima e così via.</span><span class="sxs-lookup"><span data-stu-id="2dbae-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="2dbae-516">[RunRScriptUsingADFSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Esempio relativo all'esecuzione di script R con ADF).</span><span class="sxs-lookup"><span data-stu-id="2dbae-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="2dbae-517">Chiama lo script R eseguendo RScript.exe sul cluster HDInsight in cui è già installato R.</span><span class="sxs-lookup"><span data-stu-id="2dbae-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="2dbae-518">Attività .NET per dominio app</span><span class="sxs-lookup"><span data-stu-id="2dbae-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="2dbae-519">Usa versioni di assembly diverse da quelle usate dal servizio di avvio di Data Factory</span><span class="sxs-lookup"><span data-stu-id="2dbae-519">Uses different assembly versions from ones used by the Data Factory launcher</span></span> |
| [<span data-ttu-id="2dbae-520">Rielaborare un modello in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="2dbae-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="2dbae-521">Rielabora un modello in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="2dbae-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
