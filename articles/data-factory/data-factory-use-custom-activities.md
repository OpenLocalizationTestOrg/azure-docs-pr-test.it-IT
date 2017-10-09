---
title: "aaaUse attività personalizzate in una pipeline di Data Factory di Azure"
description: "Informazioni su come le attività personalizzate toocreate e utilizzarli in una pipeline di Data Factory di Azure."
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
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="1a5d6-103">Usare attività personalizzate in una pipeline di Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1a5d6-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="1a5d6-104">Attività Hive</span><span class="sxs-lookup"><span data-stu-id="1a5d6-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="1a5d6-105">Attività di Pig</span><span class="sxs-lookup"><span data-stu-id="1a5d6-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="1a5d6-106">Attività MapReduce</span><span class="sxs-lookup"><span data-stu-id="1a5d6-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="1a5d6-107">Attività di Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="1a5d6-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="1a5d6-108">Attività Spark</span><span class="sxs-lookup"><span data-stu-id="1a5d6-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="1a5d6-109">Attività di esecuzione batch di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a5d6-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="1a5d6-110">Attività della risorsa di aggiornamento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1a5d6-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="1a5d6-111">Attività stored procedure</span><span class="sxs-lookup"><span data-stu-id="1a5d6-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="1a5d6-112">Attività U-SQL di Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="1a5d6-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="1a5d6-113">Attività personalizzata di .NET</span><span class="sxs-lookup"><span data-stu-id="1a5d6-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="1a5d6-114">In una pipeline di Azure Data Factory è possibile usare due tipi di attività.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="1a5d6-115">[Le attività di spostamento dati](data-factory-data-movement-activities.md) dati toomove tra [archivi di dati di origine e sink supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="1a5d6-116">[Attività di trasformazione dei dati](data-factory-data-transformation-activities.md) tootransform dati utilizzando i servizi, ad esempio HDInsight di Azure, il Batch di Azure e Azure Machine Learning di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="1a5d6-117">i dati toomove in o da un archivio dati che non supporta la Data Factory, creare un **attività personalizzata** con la propria spostamento logica e utilizzare hello attività di dati in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="1a5d6-118">Analogamente, tootransform/elaborare i dati in modo che non è supportato da Data Factory, creare un'attività personalizzata con la logica di trasformazione di dati e utilizzare attività hello in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="1a5d6-119">È possibile configurare un toorun di attività personalizzata in un **Azure Batch** pool di macchine virtuali o basato su Windows **Azure HDInsight** cluster.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="1a5d6-120">Quando si usa Azure Batch, è possibile usare solo un pool esistente di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="1a5d6-121">Quando invece si usa HDInsight, è possibile usare un cluster HDInsight esistente o un cluster creato automaticamente su richiesta in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="1a5d6-122">Hello procedura riportata di seguito vengono fornite istruzioni dettagliate per la creazione di un'attività personalizzata di .NET e l'utilizzo di attività personalizzata hello in una pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="1a5d6-123">procedura dettagliata Hello viene utilizzato un **Azure Batch** servizio collegato.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="1a5d6-124">toouse HDInsight di Azure un servizio collegato, invece, si crea un servizio collegato di tipo **HDInsight** (il propria cluster HDInsight) o **HDInsightOnDemand** (Data Factory crea un cluster HDInsight su richiesta).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="1a5d6-125">Configurare quindi hello toouse attività personalizzata del servizio collegato di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="1a5d6-126">Vedere [servizi collegati HDInsight di Azure usare](#use-hdinsight-compute-service) per ulteriori informazioni sull'utilizzo di attività personalizzata hello toorun di Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="1a5d6-127">attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1a5d6-128">Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1a5d6-129">Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="1a5d6-130">Non è possibile toouse un Gateway di gestione di dati da origini dati locali tooaccess attività personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="1a5d6-131">Attualmente, [Gateway di gestione dati](data-factory-data-management-gateway.md) supporta solo attività di copia hello e attività di stored procedure nella Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="1a5d6-132">Procedura dettagliata: creare un'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="1a5d6-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="1a5d6-133">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1a5d6-133">Prerequisites</span></span>
* <span data-ttu-id="1a5d6-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="1a5d6-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="1a5d6-135">Scaricare e installare [.NET SDK di Azure](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1a5d6-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="1a5d6-136">Prerequisiti di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="1a5d6-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="1a5d6-137">In questa procedura dettagliata hello, vengono eseguite attività .NET personalizzate usando Azure Batch come una risorsa di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="1a5d6-138">**Azure Batch** è una piattaforma di servizio per l'esecuzione parallela su larga scala e ad alte prestazioni (HPC) applicazioni in modo efficiente nel cloud di hello di elaborazione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="1a5d6-139">Azure Batch pianifica toorun di lavoro a utilizzo intensivo di calcolo in un oggetto gestito **raccolta di macchine virtuali**, e possa automaticamente la scala di calcolo esigenze hello toomeet di risorse dei processi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="1a5d6-140">Vedere [nozioni di base di Azure Batch] [ batch-technical-overview] articolo per una panoramica dettagliata di hello servizio Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="1a5d6-141">Per l'esercitazione hello, creare un account Azure Batch con un pool di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="1a5d6-142">Ecco i passaggi di hello:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-142">Here are hello steps:</span></span>

1. <span data-ttu-id="1a5d6-143">Creare un **account Azure Batch** utilizzando hello [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="1a5d6-144">Per istruzioni, vedere l'articolo su come [creare e gestire un account Azure Batch][batch-create-account].</span><span class="sxs-lookup"><span data-stu-id="1a5d6-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="1a5d6-145">Annotando il nome dell'account Azure Batch hello, chiave dell'account, URI e nome del pool.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="1a5d6-146">È necessario toocreate un servizio collegato Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="1a5d6-147">Nella home page a hello per account Azure Batch, viene visualizzato un **URL** in hello seguente formato: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="1a5d6-148">In questo esempio, **myaccount** nome hello di hello account Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="1a5d6-149">URI è utilizzato nella definizione di servizio collegato hello è hello URL senza nome hello dell'account di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="1a5d6-150">Ad esempio: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="1a5d6-151">Fare clic su **chiavi** nel menu a sinistra di hello e hello copia **chiave di accesso primaria**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="1a5d6-152">toouse un pool esistente, fare clic su **pool** menu hello e annotare hello **ID** del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="1a5d6-153">Se non si dispone di un pool esistente, è possibile spostare toohello successivo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="1a5d6-154">Creare un **pool di Azure Batch**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="1a5d6-155">In hello [portale di Azure](https://portal.azure.com), fare clic su **Sfoglia** in hello menu a sinistra, quindi fare clic su **account Batch**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="1a5d6-156">Selezionare il hello tooopen di account Azure Batch **Account Batch** blade.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="1a5d6-157">Fare clic sul riquadro **Pool** .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="1a5d6-158">In hello **pool** pannello, fare clic su Aggiungi pulsante nella barra degli strumenti di hello tooadd un pool.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="1a5d6-159">Immettere un ID per il pool di hello (ID pool di applicazioni).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="1a5d6-160">Hello nota **ID del pool di hello**; è necessario durante la creazione di soluzioni di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="1a5d6-161">Specificare **Windows Server 2012 R2** per l'impostazione di hello famiglia di sistemi operativi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="1a5d6-162">Selezionare un **piano tariffario per il nodo**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="1a5d6-163">Immettere **2** come valore per hello **destinazione dedicato** impostazione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="1a5d6-164">Immettere **2** come valore per hello **Max attività per ogni nodo** impostazione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="1a5d6-165">Fare clic su **OK** pool hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="1a5d6-166">Annotare hello **ID** del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="1a5d6-167">Procedure generali</span><span class="sxs-lookup"><span data-stu-id="1a5d6-167">High-level steps</span></span>
<span data-ttu-id="1a5d6-168">Di seguito sono hello due operazioni eseguite come parte di questa procedura dettagliata:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="1a5d6-169">Creare un'attività personalizzata contenente una semplice logica di trasformazione/elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="1a5d6-170">Creare una data factory di Azure con una pipeline che utilizza l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="1a5d6-171">Creare un'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="1a5d6-171">Create a custom activity</span></span>
<span data-ttu-id="1a5d6-172">creare un'attività personalizzata di .NET, toocreate un **libreria di classi .NET** progetto con una classe che implementa che **IDotNetActivity** interfaccia.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="1a5d6-173">Questa interfaccia ha un solo metodo, [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) , e la relativa firma è:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="1a5d6-174">metodo Hello accetta quattro parametri:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="1a5d6-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-175">**linkedServices**.</span></span> <span data-ttu-id="1a5d6-176">Questa proprietà è un elenco enumerabile di servizi di archiviazione di dati collegato a cui fa riferimento dal set di dati di input/output per l'attività hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="1a5d6-177">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-177">**datasets**.</span></span> <span data-ttu-id="1a5d6-178">Questa proprietà è un elenco di set di dati di input/output per l'attività hello enumerabile.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="1a5d6-179">È possibile utilizzare questo percorsi hello tooget di parametro e gli schemi definiti dal set di dati di input e output.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="1a5d6-180">**activity**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-180">**activity**.</span></span> <span data-ttu-id="1a5d6-181">Questa proprietà rappresenta l'attività corrente hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-181">This property represents hello current activity.</span></span> <span data-ttu-id="1a5d6-182">Può essere utilizzato tooaccess le proprietà estese associate attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="1a5d6-183">Per i dettagli, vedere [Accedere a tutte le proprietà estese](#access-extended-properties).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="1a5d6-184">**logger**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-184">**logger**.</span></span> <span data-ttu-id="1a5d6-185">Questo oggetto consente di scrivere commenti di debug di tale area nel Registro di hello utente per la pipeline di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="1a5d6-186">metodo Hello restituisce un dizionario che può essere attività personalizzate toochain utilizzati insieme in futuro hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="1a5d6-187">Questa funzionalità non ancora implementata, pertanto restituire un dizionario vuoto da metodo hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="1a5d6-188">Procedura</span><span class="sxs-lookup"><span data-stu-id="1a5d6-188">Procedure</span></span>
1. <span data-ttu-id="1a5d6-189">Creare un progetto **Libreria di classi .NET** .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="1a5d6-190">Avviare <b>Visual Studio 2017</b>, <b>Visual Studio 2015</b>, <b>Visual Studio 2013</b> oppure <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="1a5d6-191">Fare clic su <b>File</b>, punto troppo<b>New</b>, fare clic su <b>progetto</b>.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="1a5d6-192">Espandere <b>Modelli</b> e quindi selezionare <b>Visual C#</b>.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="1a5d6-193">In questa procedura dettagliata, si utilizza c#, ma è possibile utilizzare qualsiasi attività personalizzate .NET language toodevelop hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="1a5d6-194">Selezionare <b>libreria di classi</b> dall'elenco di hello dei tipi di progetto su hello destra.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="1a5d6-195">In Visual Studio 2017, scegliere <b>Libreria di classi (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="1a5d6-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="1a5d6-196">Immettere <b>MyDotNetActivity</b> per hello <b>nome</b>.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="1a5d6-197">Selezionare <b>C:\ADFGetStarted</b> per hello <b>percorso</b>.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="1a5d6-198">Fare clic su <b>OK</b> progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="1a5d6-199">
2.Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="1a5d6-200">3.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-200">3.</span></span> <span data-ttu-id="1a5d6-201">Nella Console di gestione pacchetti hello, eseguire hello successivo comando tooimport **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="1a5d6-202">Hello importazione **di archiviazione di Azure** pacchetto NuGet nel progetto toohello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1a5d6-203">Utilità di avvio del servizio Data Factory richiede la versione di hello 4.3 di Windowsazure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="1a5d6-204">Se si aggiunge un riferimento tooa ultima versione di assembly di archiviazione di Azure nel progetto di attività personalizzata, viene visualizzato un errore durante l'esecuzione di attività hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="1a5d6-205">Errore di hello tooresolve, vedere [isolamento](#appdomain-isolation) sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="1a5d6-206">Aggiungere il seguente hello **utilizzando** istruzioni toohello file sorgente hello progetto.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-206">Add hello following **using** statements toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="1a5d6-207">Modifica nome hello di hello **dello spazio dei nomi** troppo**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="1a5d6-208">Modificare il nome di hello della classe hello troppo**MyDotNetActivity** ed eseguirne la derivazione da hello **IDotNetActivity** interfaccia come illustrato nel seguente frammento di codice hello:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="1a5d6-209">Hello implementare (Aggiungi) **Execute** metodo hello **IDotNetActivity** interfaccia toohello **MyDotNetActivity** classe e copia hello metodo toohello codice di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="1a5d6-210">Hello seguente conta hello numero di occorrenze del termine di ricerca hello ("Microsoft") in ogni blob associato a una sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
        // toolog information, use hello logger object
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

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
        string folderPath = GetFolderPath(inputDataset);
        string output = string.Empty; // for use later.
    
        // create storage client for input. Pass hello connection string.
        CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
        CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
        // initialize hello continuation token before using it in hello do-while loop.
        BlobContinuationToken continuationToken = null;
        do
        {   // get hello list of input blobs from hello input storage client object.
            BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                     true,
                                     BlobListingDetails.Metadata,
                                     null,
                                     continuationToken,
                                     null,
                                     null);
    
            // Calculate method returns hello number of occurrences of
            // hello search term (“Microsoft”) in each blob associated
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
        logger.Write("output blob URI: {0}", outputBlobUri.ToString());

        // create a blob and upload hello output text.
        CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
        logger.Write("Writing {0} toohello output blob", output);
        outputBlob.UploadText(output);
    
        // hello dictionary can be used toochain custom activities together in hello future.
        // This feature is not implemented yet, so just return an empty dictionary.  
    
        return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="1a5d6-211">Aggiungere hello dei seguenti metodi di supporto:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-211">Add hello following helper methods:</span></span> 

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
    /// </summary>
    
    private static string GetFolderPath(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
        return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets hello fileName value from hello input/output dataset.   
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
        if (dataArtifact == null || dataArtifact.Properties == null)
        {
            return null;
        }
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
        return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
                output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
            }
        }
        return output;
    }
    ```

    <span data-ttu-id="1a5d6-212">Hello GetFolderPath metodo restituisce hello percorso toohello cartella hello set di dati punta tooand hello GetFileName restituisce hello nome del metodo hello/file blob hello per i punti di set di dati.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="1a5d6-213">Se si havefolderPath definisce l'utilizzo di variabili, ad esempio {Year}, {Month,} restituisce {Day} e così via, il metodo hello hello stringa perché è senza sostituirli con i valori di runtime.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="1a5d6-214">Per i dettagli sull'accesso a SliceStart, SliceEnd e così via, vedere [Accedere a tutte le proprietà estese](#access-extended-properties) .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="1a5d6-215">metodo Calculate Hello calcola il numero di hello di istanze della parola chiave Microsoft nei file di input hello (BLOB nella cartella hello).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="1a5d6-216">il termine di ricerca Hello ("Microsoft") è hardcoded nel codice hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="1a5d6-217">Compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-217">Compile hello project.</span></span> <span data-ttu-id="1a5d6-218">Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1a5d6-219">Versione set 4.5.2 di .NET Framework come framework di destinazione hello per il progetto: progetto hello di mouse e scegliere **proprietà** framework di destinazione tooset hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="1a5d6-220">Data factory non supporta le attività personalizzate compilate in versioni di .NET Framework successive alla 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="1a5d6-221">Avviare **Esplora**e passare troppo**bin\debug** o **bin\release** cartella in base al tipo di hello di compilazione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="1a5d6-222">Creare un file zip **MyDotNetActivity.zip** che contiene tutti i file binari hello in hello <project folder>nella cartella \bin\Debug.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="1a5d6-223">Includere hello **MyDotNetActivity.pdb** file in modo che sia possibile ottenere ulteriori dettagli, ad esempio il numero di riga nel codice sorgente hello che ha causato il problema di hello se si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="1a5d6-224">Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** con nessun le sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![File di output binari](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="1a5d6-226">Se non è già presente, creare un contenitore BLOB denominato **customactivitycontainer**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="1a5d6-227">Caricare MyDotNetActivity.zip come un customactivitycontainer toohello blob in un **generica** archiviazione blob di Azure (archiviazione Blob non hot/cool) che fa riferimento AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1a5d6-228">Se si aggiunge questa soluzione di tooa progetto attività .NET in Visual Studio contenente un progetto di Data Factory e aggiunta un progetto di attività too.NET riferimento dal progetto di applicazione hello Data Factory, non è necessario tooperform hello ultimi due passaggi per la creazione manuale file zip Hello e caricarlo nell'archiviazione blob di Azure generico toohello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="1a5d6-229">Quando si pubblicano le entità di Data Factory utilizzando Visual Studio, questi passaggi vengono eseguiti automaticamente dal processo di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="1a5d6-230">Per altre informazioni, vedere la sezione [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) (Progetto Data Factory in Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="1a5d6-231">Creare una pipeline con attività personalizzate</span><span class="sxs-lookup"><span data-stu-id="1a5d6-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="1a5d6-232">Aver creato un'attività personalizzata e caricato il file zip hello con il contenitore di blob tooa i file binari in un **generica** Account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="1a5d6-233">In questa sezione creare una data factory di Azure con una pipeline che utilizza l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="1a5d6-234">set di dati input Hello per attività personalizzata hello rappresenta BLOB (file) nella cartella customactivityinput hello del contenitore adftutorial nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="1a5d6-235">set di dati per l'attività hello output di Hello rappresenta il BLOB di output nella cartella customactivityoutput hello del contenitore adftutorial nell'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="1a5d6-236">Creare **file.txt** file con hello seguente il contenuto e caricarla troppo**customactivityinput** cartella di hello **adftutorial** contenitore.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="1a5d6-237">Creare il contenitore di adftutorial hello se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="1a5d6-238">cartella input Hello corrisponde sezione tooa nella Data Factory di Azure, anche se la cartella hello dispone di due o più file.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="1a5d6-239">Quando ogni sezione venga elaborato dalla pipeline di hello, attività personalizzata hello scorre tutti i BLOB hello nella cartella di input hello per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="1a5d6-240">Viene visualizzato un file con nella cartella adftutorial\customactivityoutput hello di output con una o più righe (uguale al numero di BLOB nella cartella input hello):</span><span class="sxs-lookup"><span data-stu-id="1a5d6-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="1a5d6-241">Di seguito sono descritte hello che operazioni in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="1a5d6-242">Creare una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="1a5d6-243">Creare **servizi collegati** per pool di applicazioni Azure Batch hello di macchine virtuali in cui hello attività personalizzata viene eseguita e hello archiviazione di Azure che contiene il BLOB di input/output di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="1a5d6-244">Creazione di input e output **set di dati** che rappresentano l'input e output di attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="1a5d6-245">Creare un **pipeline** che usa l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="1a5d6-246">Creare hello **file.txt** e caricare il contenitore di blob tooa se non è già fatto.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="1a5d6-247">Vedere le istruzioni nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="1a5d6-248">Passaggio 1: Creare hello data factory</span><span class="sxs-lookup"><span data-stu-id="1a5d6-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="1a5d6-249">Dopo l'accesso toohello portale di Azure, hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="1a5d6-250">Fare clic su **NEW** nel menu di sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="1a5d6-251">Fare clic su **dati + Analitica** in hello **New** blade.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="1a5d6-252">Fare clic su **Data Factory** su hello **analitica dati** blade.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Menu Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="1a5d6-254">In hello **nuova data factory** pannello immettere **CustomActivityFactory** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="1a5d6-255">nome Hello di hello Azure data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="1a5d6-256">Se viene visualizzato l'errore hello: **"CustomActivityFactory" nome della Data factory non è disponibile**, modificare il nome di hello della data factory di hello (ad esempio, **yournameCustomActivityFactory**) e provare a creare nuovo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Pannello Nuova Azure Data Factory](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="1a5d6-258">Fare clic su **NOME DEL GRUPPO DI RISORSE**e selezionare un gruppo di risorse esistente o crearne uno.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="1a5d6-259">Verificare che si sta utilizzando hello corretto **sottoscrizione** e **area** in cui si desidera hello data factory toobe creato.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="1a5d6-260">Fare clic su **crea** su hello **nuova data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="1a5d6-261">Vedrai data factory di hello viene creato nel hello **Dashboard** di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="1a5d6-262">Dopo l'hello data factory è stata creata correttamente, vengono visualizzati pannello Data Factory di hello, che mostra contenuto della data factory di hello hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Pannello Data factory](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="1a5d6-264">Passaggio 2: Creare servizi collegati</span><span class="sxs-lookup"><span data-stu-id="1a5d6-264">Step 2: Create linked services</span></span>
<span data-ttu-id="1a5d6-265">Servizi collegati collegano archivi dati o servizi tooan data factory di Azure di calcolo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="1a5d6-266">In questo passaggio è collegare l'account di archiviazione di Azure e la data factory di Azure Batch account tooyour.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="1a5d6-267">Creare il servizio collegato Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1a5d6-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="1a5d6-268">Fare clic su hello **autore e distribuire** riquadro hello **DATA FACTORY** pannello **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="1a5d6-269">Vedrai hello Editor delle Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="1a5d6-270">Fare clic su **nuovo archivio dati** hello barra dei comandi e scegliere **archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="1a5d6-271">Dovrebbe essere hello script JSON per la creazione di una risorsa di archiviazione di Azure il servizio nell'editor di hello collegato.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Nuovo archivio dati - Archiviazione di Azure](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="1a5d6-273">Sostituire `<accountname>` con il nome dell'account di archiviazione di Azure e `<accountkey>` con la chiave di accesso di hello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="1a5d6-274">toolearn modalità di accesso di archiviazione di tooget chiave, vedere [visualizzazione, copia e l'archiviazione di rigenerare le chiavi di accesso](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Servizio collegato Archiviazione di Azure](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="1a5d6-276">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="1a5d6-277">Creare il servizio collegato Azure Batch</span><span class="sxs-lookup"><span data-stu-id="1a5d6-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="1a5d6-278">Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo calcolo**, quindi selezionare **Azure Batch** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Nuovo calcolo - Azure Batch](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="1a5d6-280">Apportare hello modifiche toohello JSON script seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="1a5d6-281">Specificare il nome di account Azure Batch per hello **accountName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="1a5d6-282">Hello **URL** da hello **pannello account Azure Batch** in hello seguente formato: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="1a5d6-283">Per hello **batchUri** proprietà hello JSON, è necessario tooremove `accountname.` da hello URL e l'utilizzo di hello `accountname` per hello `accountName` proprietà JSON.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="1a5d6-284">Specificare una chiave dell'account Azure Batch hello per hello **accessKey** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="1a5d6-285">Specificare il nome di hello del pool di hello creato come parte dei prerequisiti per hello **poolName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="1a5d6-286">È anche possibile specificare ID hello del pool di hello anziché il nome di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="1a5d6-287">Specificare l'URI del Batch di Azure per hello **batchUri** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="1a5d6-288">Esempio: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="1a5d6-289">Specificare hello **AzureStorageLinkedService** per hello **linkedServiceName** proprietà.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

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

       <span data-ttu-id="1a5d6-290">Per hello **poolName** proprietà, è inoltre possibile specificare l'ID di hello del pool di hello anziché il nome di hello del pool di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="1a5d6-291">Hello servizio Data Factory non supporta un'opzione su richiesta per il Batch di Azure a quanto accade per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="1a5d6-292">È possibile usare solo il proprio pool di Batch di Azure in una data factory di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="1a5d6-293">Passaggio 3: Creare set di dati</span><span class="sxs-lookup"><span data-stu-id="1a5d6-293">Step 3: Create datasets</span></span>
<span data-ttu-id="1a5d6-294">In questo passaggio, creare set di dati toorepresent input e i dati di output.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="1a5d6-295">Creare set di dati di input</span><span class="sxs-lookup"><span data-stu-id="1a5d6-295">Create input dataset</span></span>
1. <span data-ttu-id="1a5d6-296">In hello **Editor** per hello Data Factory, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**, quindi selezionare **archiviazione Blob di Azure** dal menu a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="1a5d6-297">Sostituire hello JSON nel riquadro di destra hello con hello frammento di codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

   <span data-ttu-id="1a5d6-298">Più avanti in questa procedura dettagliata viene creata una pipeline con ora di inizio: 2016-11-16T00:00:00Z e ora di fine: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="1a5d6-299">È pianificato tooproduce dati ogni ora, pertanto vi sono cinque intervalli di input/output (tra **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="1a5d6-300">Hello **frequenza** e **intervallo** per hello di un set di dati dell'input è troppo**ora** e **1**, il che significa che hello input sezione è disponibile ogni ora.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="1a5d6-301">In questo esempio, è hello stesso file (file. txt) in intputfolder hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="1a5d6-302">Di seguito sono ora di inizio hello per ogni sezione, rappresentata dalla variabile di sistema SliceStart in hello sopra il frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="1a5d6-303">Fare clic su **Distribuisci** hello toocreate barra degli strumenti e distribuire hello **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="1a5d6-304">Assicurarsi di visualizzare hello **tabella CREATA correttamente** messaggio sulla barra del titolo hello di hello Editor.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="1a5d6-305">Creare un set di dati di output</span><span class="sxs-lookup"><span data-stu-id="1a5d6-305">Create an output dataset</span></span>
1. <span data-ttu-id="1a5d6-306">In hello **editor Data Factory**, fare clic su **... Ulteriori** nella barra dei comandi di hello, fare clic su **nuovo set di dati**, quindi selezionare **archiviazione Blob di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="1a5d6-307">Sostituire script JSON hello nel riquadro di destra hello con hello lo script JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

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

     <span data-ttu-id="1a5d6-308">Percorso di output è **adftutorial/customactivityoutput/** e nome file di output è aaaa-MM-GG-HH.txt, dove AAAA-MM-GG-HH è hello anno, mese, data e ora della sezione hello in fase di produzione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="1a5d6-309">Per informazioni dettagliate, vedere la [guida di riferimento per gli sviluppatori][adf-developer-reference].</span><span class="sxs-lookup"><span data-stu-id="1a5d6-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="1a5d6-310">Un BLOB o file di output viene generato per ogni sezione di input.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="1a5d6-311">Ecco come viene denominato il file di output per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="1a5d6-312">Tutti i file di output di hello vengono generati in una cartella di output: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="1a5d6-313">Sezione</span><span class="sxs-lookup"><span data-stu-id="1a5d6-313">Slice</span></span> | <span data-ttu-id="1a5d6-314">Ora di inizio</span><span class="sxs-lookup"><span data-stu-id="1a5d6-314">Start time</span></span> | <span data-ttu-id="1a5d6-315">File di output</span><span class="sxs-lookup"><span data-stu-id="1a5d6-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="1a5d6-316">1</span><span class="sxs-lookup"><span data-stu-id="1a5d6-316">1</span></span> |<span data-ttu-id="1a5d6-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="1a5d6-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="1a5d6-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="1a5d6-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="1a5d6-319">2</span><span class="sxs-lookup"><span data-stu-id="1a5d6-319">2</span></span> |<span data-ttu-id="1a5d6-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="1a5d6-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="1a5d6-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="1a5d6-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="1a5d6-322">3</span><span class="sxs-lookup"><span data-stu-id="1a5d6-322">3</span></span> |<span data-ttu-id="1a5d6-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="1a5d6-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="1a5d6-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="1a5d6-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="1a5d6-325">4</span><span class="sxs-lookup"><span data-stu-id="1a5d6-325">4</span></span> |<span data-ttu-id="1a5d6-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="1a5d6-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="1a5d6-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="1a5d6-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="1a5d6-328">5</span><span class="sxs-lookup"><span data-stu-id="1a5d6-328">5</span></span> |<span data-ttu-id="1a5d6-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="1a5d6-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="1a5d6-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="1a5d6-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="1a5d6-331">Tenere presente che tutti i file hello in una cartella di input sono parte di una sezione con ora di inizio hello indicato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="1a5d6-332">Durante l'elaborazione di questa sezione, attività personalizzata hello esamina ogni file e produce una riga nel file di output di hello con numero di hello di occorrenze del termine di ricerca ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="1a5d6-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="1a5d6-333">Se sono presenti tre file in CartellaInput hello, sono presenti tre righe nel file di output di hello per ogni sezione oraria: 2016-11-16-00.txt 2016-11-16:01:00:00.txt, e così via.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="1a5d6-334">hello toodeploy **OutputDataset**, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="1a5d6-335">Creare ed eseguire una pipeline che utilizza l'attività personalizzata hello</span><span class="sxs-lookup"><span data-stu-id="1a5d6-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="1a5d6-336">Nell'Editor delle Data Factory hello, fare clic su **... Ulteriori**, quindi selezionare **nuova pipeline** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="1a5d6-337">Sostituire hello JSON nel riquadro di destra hello con hello lo script JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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

    <span data-ttu-id="1a5d6-338">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-338">Note hello following points:</span></span>

   * <span data-ttu-id="1a5d6-339">**Concorrenza** è troppo**2** in modo che le due sezioni vengono elaborate in parallelo da 2 macchine virtuali nel pool di hello Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="1a5d6-340">È un'attività nella sezione attività hello ed è di tipo: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="1a5d6-341">**AssemblyName** è impostato il nome toohello di hello DLL: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="1a5d6-342">**Punto di ingresso** è troppo**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="1a5d6-343">**PackageLinkedService** è troppo**AzureStorageLinkedService** che punta toohello archiviazione di blob che contiene i file zip di attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="1a5d6-344">Se si utilizza input/output di diversi account di archiviazione di Azure per file e hello file zip di attività personalizzata, si crea un altro servizio collegato di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="1a5d6-345">Questo articolo si presuppone che si sta utilizzando hello stesso account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="1a5d6-346">**PackageFile** è troppo**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="1a5d6-347">È in formato hello: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="1a5d6-348">attività personalizzata Hello accetta **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="1a5d6-349">la proprietà linkedServiceName Hello di attività personalizzata hello punta toohello **AzureBatchLinkedService**, che indica Data Factory di Azure, tale attività personalizzata hello deve toorun nelle macchine virtuali di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="1a5d6-350">**isPaused** impostata troppo**false** per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="1a5d6-351">pipeline Hello verrà eseguito immediatamente in questo esempio perché l'inizio delle sezioni hello in hello precedente.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="1a5d6-352">È possibile impostare la pipeline di hello toopause tootrue proprietà e impostarla toorestart toofalse indietro.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="1a5d6-353">Hello **avviare** tempo e **fine** i tempi sono **cinque** ore separate e le sezioni vengono generate ogni ora, in modo da cinque sezioni vengono generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="1a5d6-354">pipeline di hello toodeploy, fare clic su **Distribuisci** hello barra dei comandi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="1a5d6-355">Pipeline hello monitoraggio</span><span class="sxs-lookup"><span data-stu-id="1a5d6-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="1a5d6-356">Nel Pannello di Data Factory hello in hello portale di Azure, fare clic su **diagramma**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Riquadro Diagramma](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="1a5d6-358">Hello vista diagramma, fare clic su hello OutputDataset.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Vista diagramma](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="1a5d6-360">Dovrebbe essere che le sezioni di output cinque hello sono nello stato Ready hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="1a5d6-361">Se non sono in stato pronto hello, non sono state prodotte ancora.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Sezioni di output](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="1a5d6-363">Verificare che il file di output di hello vengono generato nell'archiviazione blob hello in hello **adftutorial** contenitore.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![output dell'attività personalizzata][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="1a5d6-365">Se si apre il file di output di hello, dovrebbe essere hello output toohello simile seguente output:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="1a5d6-366">Hello utilizzare [portale di Azure] [ azure-preview-portal] toomonitor i cmdlet di Azure PowerShell o la data factory di pipeline e set di dati.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="1a5d6-367">È possibile visualizzare i messaggi da hello **ActivityLogger** nel codice hello di attività personalizzata hello nei registri di hello (in particolare 0.log utente) che è possibile scaricare dal portale di hello o utilizzo dei cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![scaricare i log dall'attività personalizzata][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="1a5d6-369">Vedere [Monitorare e gestire le pipeline](data-factory-monitor-manage-pipelines.md) per i passaggi dettagliati per il monitoraggio di set di dati e pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="1a5d6-370">Progetto Data Factory in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a5d6-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="1a5d6-371">È possibile creare e pubblicare le entità di Data Factory usando Visual Studio anziché il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="1a5d6-372">Per ulteriori informazioni sulla creazione e pubblicazione entità Data Factory con Visual Studio, vedere [compilare le pipeline prima con Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) e [copiare i dati da Blob di Azure tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articoli.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="1a5d6-373">Hello seguendo i passaggi aggiuntivi se si sta creando il progetto di Data Factory in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="1a5d6-374">Aggiungere hello Data Factory progetto toohello soluzione di Visual Studio contenente il progetto di attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="1a5d6-375">Aggiungere un progetto di attività .NET toohello riferimento dal progetto di Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="1a5d6-376">Fare clic sul progetto Data Factory, scegliere troppo**Aggiungi**, quindi fare clic su **riferimento**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="1a5d6-377">In hello **Aggiungi riferimento** la finestra di dialogo, seleziona hello **MyDotNetActivity** del progetto e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="1a5d6-378">Compilare e pubblicare la soluzione hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1a5d6-379">Quando si pubblicano le entità di Data Factory, un file zip viene creato automaticamente ed è il contenitore di blob caricato toohello: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="1a5d6-380">Se il contenitore di blob hello non esiste, viene automaticamente creato troppo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="1a5d6-381">Integrazione di Data Factory e Batch</span><span class="sxs-lookup"><span data-stu-id="1a5d6-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="1a5d6-382">Hello servizio Data Factory crea un processo in Batch di Azure con nome hello: **adf poolname: processo-xxx**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="1a5d6-383">Fare clic su **processi** dal menu a sinistra di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-383">Click **Jobs** from hello left menu.</span></span> 

![Azure Data Factory: processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="1a5d6-385">Per ogni esecuzione attività di una sezione viene creata un'attività.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="1a5d6-386">Se sono presenti toobe pronto cinque sezioni elaborate, cinque attività vengono create in questo processo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="1a5d6-387">Se sono presenti più nodi di calcolo in hello pool Batch, è possono eseguire due o più sezioni in parallelo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="1a5d6-388">Se il numero massimo di attività hello per ogni set di nodi di calcolo troppo > 1, è inoltre possibile avere più di una sezione in esecuzione su hello calcolo stesso.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Azure Data Factory: attività processi di Batch](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="1a5d6-390">Hello seguente diagramma illustra la relazione hello tra le attività di Azure Data Factory e Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Data Factory e Batch](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="1a5d6-392">Errori in fase di risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="1a5d6-392">Troubleshoot failures</span></span>
<span data-ttu-id="1a5d6-393">La risoluzione dei problemi implica alcune tecniche di base:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="1a5d6-394">Se viene visualizzato il seguente errore hello, si potrebbe utilizzando un'archiviazione blob Hot/Cool anziché un'archiviazione blob di Azure utilizzo generale.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="1a5d6-395">Caricare hello zip file tooa **generico Account di archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="1a5d6-396">Se viene visualizzato il seguente errore hello, confermare che il nome di hello del classe hello in hello CS corrispondenze hello nome di file specificato per hello **EntryPoint** proprietà in formato JSON della pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="1a5d6-397">In questa procedura dettagliata hello, nome della classe hello è: MyDotNetActivity e Ciao EntryPoint hello JSON è: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="1a5d6-398">Se i nomi dei hello corrispondono, verificare che tutti i file binari hello attiva hello **cartella radice** del file zip hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="1a5d6-399">Ovvero, quando si apre file zip hello, si dovrebbe essere tutti i file hello nella cartella radice hello, non in tutte le relative sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="1a5d6-400">Se sezione input hello non è stato impostato troppo**pronto**, verificare che sia corretta struttura di cartelle di input di hello e **file.txt** presente nelle cartelle di input hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="1a5d6-401">In hello **Execute** metodo dell'attività personalizzata, utilizzare hello **IActivityLogger** informazioni toolog oggetto che consente di risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="1a5d6-402">scaricare i messaggi Hello registrata nei file di log utente hello (uno o più file denominati: utente 0.log 1.log di utente, utente 2.log, ecc.).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="1a5d6-403">In hello **OutputDataset** pannello, fare clic su hello toosee di sezione hello **sezione dati** pannello per tale sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="1a5d6-404">Verranno visualizzate le **esecuzioni di attività** per quella sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="1a5d6-405">Verrà visualizzata un'attività eseguire per sezione hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="1a5d6-406">Se si fa clic su Esegui nella barra dei comandi di hello, è possibile avviare un'altra attività eseguita per hello stessa sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="1a5d6-407">Quando si sceglie di eseguire attività di hello, vedrai hello **Dettagli esecuzione attività** pannello con un elenco di file di log.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="1a5d6-408">Vedere i messaggi registrati nel file user_0.log hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="1a5d6-409">Quando si verifica un errore, vengono visualizzati tre esecuzioni di attività perché il numero di tentativi di hello è too3 nella pipeline/attività hello JSON.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="1a5d6-410">Quando si sceglie di eseguire attività di hello, vedrai che è possibile esaminare l'errore hello tootroubleshoot i file di log hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="1a5d6-411">Nell'elenco di hello dei file di log, fare clic su hello **utente 0.log**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="1a5d6-412">Nel riquadro di destra hello sono risultati hello dell'utilizzo di hello **IActivityLogger.Write** metodo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="1a5d6-413">Se non si vedono tutti i messaggi, controllare se ci sono altri file di log denominati: user_1.log, user_2.log e così via. In caso contrario, il codice hello potrebbe non essere riuscita dopo l'ultimo messaggio registrato hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="1a5d6-414">Cercare anche eventuali messaggi di errore di sistema ed eccezioni nel file **system-0.log**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="1a5d6-415">Includere hello **PDB** file nel file zip hello in modo che i dettagli dell'errore hello presentano informazioni ad esempio **stack di chiamate** quando si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="1a5d6-416">Tutti hello file nel file zip hello per attività personalizzata hello deve essere in hello **livello principale** con nessun le sottocartelle.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="1a5d6-417">Verificare che hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer / MyDotNetActivity.zip) e **packageLinkedService** (deve puntare toohello **generica**archiviazione blob di Azure che contiene i file zip hello) sono impostate toocorrect valori.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="1a5d6-418">Se è stata corretta una sezione di hello tooreprocess errore e si desidera, fare doppio clic su sezione hello hello **OutputDataset** pannello e fare clic su **eseguire**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="1a5d6-419">Se viene visualizzato il seguente errore hello, si utilizza il pacchetto di archiviazione di Azure hello di versione > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="1a5d6-420">Utilità di avvio del servizio Data Factory richiede la versione di hello 4.3 di Windowsazure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="1a5d6-421">Vedere [isolamento](#appdomain-isolation) sezione per risolvere se è necessario utilizzare hello versione più recente dell'assembly di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="1a5d6-422">Se è possibile utilizzare la versione 4.3.0 hello del pacchetto di archiviazione di Azure, è possibile rimuovere hello riferimento tooAzure archiviazione pacchetto esistente di versione > 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="1a5d6-423">Eseguire quindi il comando seguente dalla Console di gestione pacchetti NuGet hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="1a5d6-424">Compilare il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-424">Build hello project.</span></span> <span data-ttu-id="1a5d6-425">Eliminare assembly Azure.Storage di versione > 4.3.0 dalla cartella bin\Debug hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="1a5d6-426">Creare un file zip con i file binari e il file PDB hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="1a5d6-427">Sostituire il vecchio file zip di hello con nel contenitore blob hello (customactivitycontainer).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="1a5d6-428">Hello Riesegui sezioni che non è riuscita (fare clic sulla sezione e fare clic su Esegui).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="1a5d6-429">attività personalizzata Hello non utilizza hello **app** file dal pacchetto.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="1a5d6-430">Pertanto, se il codice legge tutte le stringhe di connessione dal file di configurazione di hello, non funziona in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="1a5d6-431">Hello consigliata quando si utilizza Azure Batch è toohold tutti i segreti in un **KeyVault Azure**, utilizzare un hello tooprotect principale di servizio basata su certificati **keyvault**e distribuire il certificato di hello tooAzure pool Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="1a5d6-432">attività personalizzate .NET Hello quindi possono accedere i segreti in hello KeyVault in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="1a5d6-433">Questa soluzione è una soluzione generica e può essere ridimensionato tooany tipo di chiave privata, non solo stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="1a5d6-434">È una soluzione più semplice (ma non consigliata): è possibile creare un **servizio collegato SQL Azure** con le impostazioni della stringa di connessione, creare un set di dati che utilizza hello servizio collegato e catena hello dataset come un set di dati di input fittizio attività di .NET toohello personalizzata.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="1a5d6-435">È possibile quindi hello accesso collegato stringa di connessione del servizio nel codice di attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="1a5d6-436">Aggiornare l'attività personalizzata</span><span class="sxs-lookup"><span data-stu-id="1a5d6-436">Update custom activity</span></span>
<span data-ttu-id="1a5d6-437">Se si aggiorna il codice hello per attività personalizzata hello, compilarlo e caricare il file zip hello che contiene l'archiviazione blob di nuovo i file binari toohello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="1a5d6-438">Isolamento di AppDomain</span><span class="sxs-lookup"><span data-stu-id="1a5d6-438">Appdomain isolation</span></span>
<span data-ttu-id="1a5d6-439">Vedere [Cross AppDomain esempio](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) che illustra come toocreate un'attività personalizzata che non è vincolato versioni tooassembly usate dal pulsante di visualizzazione della Data Factory hello (esempio: versione 4.3.0 Windowsazure v6.0.x newtonsoft. JSON, ecc.).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="1a5d6-440">Accedere a tutte le proprietà estese</span><span class="sxs-lookup"><span data-stu-id="1a5d6-440">Access extended properties</span></span>
<span data-ttu-id="1a5d6-441">È possibile dichiarare le proprietà estese in formato JSON dell'attività hello, come illustrato nel seguente esempio hello:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

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


<span data-ttu-id="1a5d6-442">Nell'esempio hello, sono disponibili due proprietà estese: **SliceStart** e **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="1a5d6-443">il valore di Hello per SliceStart si basa su una variabile di sistema SliceStart hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="1a5d6-444">Per un elenco delle variabili di sistema supportate, vedere [Pianificazione ed esecuzione con Data Factory](data-factory-functions-variables.md) .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="1a5d6-445">valore Hello DataFactoryName è tooCustomActivityFactory hardcoded.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="1a5d6-446">tooaccess queste proprietà in hello estese **Execute** metodo, utilizzare codice simile toohello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="1a5d6-447">Scalabilità automatica di Azure Batch</span><span class="sxs-lookup"><span data-stu-id="1a5d6-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="1a5d6-448">È anche possibile creare un pool di Azure Batch con la funzionalità **Scalabilità automatica** .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="1a5d6-449">Ad esempio, è possibile creare un pool di batch di azure con macchine virtuali dedicate 0 e una formula di scalabilità automatica in base al numero di hello di attività in sospeso.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="1a5d6-450">formula di esempio Hello qui si ottiene hello seguente comportamento: quando viene creato inizialmente pool hello, inizia con 1 macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="1a5d6-451">Metrica $PendingTasks definisce il numero di hello di attività in esecuzione + attivo (in coda) dello stato.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="1a5d6-452">formula Hello trova numero medio di hello attività in sospeso in hello ultimi 180 secondi e imposta TargetDedicated di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="1a5d6-453">Assicura che TargetDedicated non vada mai oltre 25 macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="1a5d6-454">In tal caso, come vengono inviate nuove attività, pool aumentano automaticamente e come attività di completamento, le macchine virtuali diventano disponibile uno alla volta e la scalabilità automatica hello compatta tali macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="1a5d6-455">startingNumberOfVMs e maxNumberofVMs può essere adattato tooyour esigenze.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="1a5d6-456">Formula di scalabilità automatica:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="1a5d6-457">Per i dettagli, vedere [Ridimensionare automaticamente i nodi di calcolo in un pool di Azure Batch](../batch/batch-automatic-scaling.md) .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="1a5d6-458">Se il pool di hello utilizza predefinito hello [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello servizio Batch può richiedere 15-30 minuti tooprepare hello VM prima di eseguire l'attività personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="1a5d6-459">Se il pool di hello sta utilizzando un diverso autoScaleEvaluationInterval, hello servizio Batch può assumere autoScaleEvaluationInterval + 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="1a5d6-460">Usare il servizio di calcolo di HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a5d6-460">Use HDInsight compute service</span></span>
<span data-ttu-id="1a5d6-461">In questa procedura dettagliata hello, è stato utilizzato attività personalizzata hello toorun calcolo di Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="1a5d6-462">È possibile anche utilizzare un cluster HDInsight basati su Windows o Data Factory di creare cluster HDInsight basati su Windows su richiesta e dispone di attività personalizzata hello in esecuzione nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="1a5d6-463">Ecco i passaggi di alto livello hello per l'utilizzo di un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a5d6-464">attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1a5d6-465">Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1a5d6-466">Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="1a5d6-467">Creare un servizio collegato Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="1a5d6-468">Servizio al posto di collegato di HDInsight utilizzare **AzureBatchLinkedService** in hello JSON di pipeline.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="1a5d6-469">Se si desidera tootest con questa procedura dettagliata hello, modifica **avviare** e **fine** ore per la pipeline di hello in modo che è possibile testare uno scenario di hello con hello servizio Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="1a5d6-470">Creare un servizio collegato Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="1a5d6-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="1a5d6-471">Hello servizio Data Factory di Azure supporta la creazione di un cluster su richiesta e usarlo come dati di output tooprocess tooproduce input.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="1a5d6-472">È inoltre possibile utilizzare un cluster personale tooperform hello stesso.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="1a5d6-473">Quando si usa il cluster HDInsight su richiesta, viene creato un cluster per ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="1a5d6-474">Considerando che, se si utilizza un cluster HDInsight, cluster hello è pronto tooprocess hello sezione immediatamente.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="1a5d6-475">Pertanto, quando si utilizza cluster su richiesta, si potrebbero non visualizzare dati di output di hello più rapidamente quando si utilizza un cluster personale.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="1a5d6-476">In fase di esecuzione, un'istanza di un'attività .NET viene eseguita solo su un nodo di lavoro nel cluster HDInsight hello. non può essere scalato toorun su più nodi.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="1a5d6-477">Più istanze di attività .NET è possono eseguire in parallelo in nodi diversi del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="1a5d6-478">toouse un cluster di HDInsight su richiesta</span><span class="sxs-lookup"><span data-stu-id="1a5d6-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="1a5d6-479">In hello **portale di Azure**, fare clic su **autore e distribuire** nella home page di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="1a5d6-480">Nell'Editor delle Data Factory hello, fare clic su **nuovo calcolo** dal comando hello barra e selezionare **cluster HDInsight su richiesta** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="1a5d6-481">Apportare hello modifiche toohello JSON script seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="1a5d6-482">Per hello **clusterSize** proprietà, specificare le dimensioni di hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="1a5d6-483">Per hello **timeToLive** proprietà, specificare quanto tempo cliente hello può essere inattivo prima che venga eliminato.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="1a5d6-484">Per hello **versione** proprietà, specificare la versione di HDInsight hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="1a5d6-485">Se si esclude questa proprietà, viene utilizzata la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="1a5d6-486">Per hello **linkedServiceName**, specificare **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

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
    > <span data-ttu-id="1a5d6-487">attività .NET personalizzata Hello eseguito solo in cluster HDInsight basati su Windows.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="1a5d6-488">Una soluzione alternativa per questa limitazione è hello toouse codice personalizzato Java mappa ridurre attività toorun in un cluster HDInsight basati su Linux.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="1a5d6-489">Un'altra opzione è toouse un pool di Azure Batch di attività personalizzate di macchine virtuali toorun invece di usare un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="1a5d6-490">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="1a5d6-491">toouse cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="1a5d6-492">In hello **portale di Azure**, fare clic su **autore e distribuire** nella home page di hello Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="1a5d6-493">In hello **Editor delle Data Factory**, fare clic su **nuovo calcolo** dal comando hello barra e selezionare **cluster HDInsight** dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="1a5d6-494">Apportare hello modifiche toohello JSON script seguente:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="1a5d6-495">Per hello **clusterUri** proprietà, immettere l'URL di hello per HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="1a5d6-496">Ad esempio: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="1a5d6-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="1a5d6-497">Per hello **UserName** proprietà, immettere nome utente hello che dispone di cluster di HDInsight toohello di accesso.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="1a5d6-498">Per hello **Password** proprietà, immettere la password di hello hello utente.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="1a5d6-499">Per hello **LinkedServiceName** proprietà, immettere **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="1a5d6-500">Fare clic su **Distribuisci** sul comando hello barra toodeploy hello collegato servizio.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="1a5d6-501">Per informazioni dettagliate, vedere [Servizi collegati di calcolo](data-factory-compute-linked-services.md) .</span><span class="sxs-lookup"><span data-stu-id="1a5d6-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="1a5d6-502">In hello **JSON di pipeline**, utilizzare HDInsight (su richiesta o la propria) il servizio collegato:</span><span class="sxs-lookup"><span data-stu-id="1a5d6-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

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

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="1a5d6-503">Creazione di un’attività personalizzata tramite .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1a5d6-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="1a5d6-504">In questa procedura dettagliata hello in questo articolo, creerai una data factory con una pipeline che utilizza l'attività personalizzata hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="1a5d6-505">Hello di codice seguente viene illustrato come toocreate hello data factory di utilizzando invece .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="1a5d6-506">È possibile trovare ulteriori informazioni sull'utilizzo di SDK tooprogrammatically creare pipeline in hello [creare una pipeline con attività di copia utilizzando l'API .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

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

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
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

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
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

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="1a5d6-507">Eseguire il debug di attività personalizzate in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1a5d6-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="1a5d6-508">Hello [Azure Data Factory - ambiente locale](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) esempio in GitHub include uno strumento che consente attività .NET personalizzate toodebug all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="1a5d6-509">Attività personalizzata di esempio su GitHub</span><span class="sxs-lookup"><span data-stu-id="1a5d6-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="1a5d6-510">Esempio</span><span class="sxs-lookup"><span data-stu-id="1a5d6-510">Sample</span></span> | <span data-ttu-id="1a5d6-511">Funzioni delle attività personalizzate</span><span class="sxs-lookup"><span data-stu-id="1a5d6-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="1a5d6-512">[HttpDataDownloaderSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample)(Esempio relativo al downloader dati HTTP).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="1a5d6-513">Scarica i dati da un archivio Blob utilizzando l'attività personalizzata in c# in Data Factory di tooAzure HTTP Endpoint.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="1a5d6-514">Esempio di analisi del sentimento su Twitter</span><span class="sxs-lookup"><span data-stu-id="1a5d6-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="1a5d6-515">Chiama un modello ML di Azure ed esegue l'analisi del sentimento, l'assegnazione dei punteggi, la stima e così via.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="1a5d6-516">[RunRScriptUsingADFSample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)(Esempio relativo all'esecuzione di script R con ADF).</span><span class="sxs-lookup"><span data-stu-id="1a5d6-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="1a5d6-517">Chiama lo script R eseguendo RScript.exe sul cluster HDInsight in cui è già installato R.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="1a5d6-518">Attività .NET per dominio app</span><span class="sxs-lookup"><span data-stu-id="1a5d6-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="1a5d6-519">Utilizza le versioni di assembly diverso da quelli utilizzati dalla visualizzazione della Data Factory di hello</span><span class="sxs-lookup"><span data-stu-id="1a5d6-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="1a5d6-520">Rielaborare un modello in Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a5d6-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="1a5d6-521">Rielabora un modello in Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="1a5d6-521">Reprocesses a model in Azure Analysis Services.</span></span> |

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
