---
title: 'Analisi scientifica dei dati scalabile in Azure Data Lake: procedura dettagliata end-to-end | Documentazione Microsoft'
description: "Modalità toouse Azure Data Lake toodo l'esplorazione e binario classificazione dei dati di attività da un set di dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="5a7d4-103">Analisi scientifica dei dati scalabile in Azure Data Lake: procedura dettagliata end-to-end</span><span class="sxs-lookup"><span data-stu-id="5a7d4-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="5a7d4-104">Questa procedura dettagliata illustra come toouse Azure Data Lake toodo l'esplorazione dei dati e le attività di classificazione binaria a un campione di hello NYC taxi di andata e ritorno e tariffa toopredict set di dati da una tariffa verrà corrisposto un suggerimento o meno.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="5a7d4-105">Contiene passaggi hello di hello [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess), end-to-end, dalla formazione toomodel acquisizione di dati, quindi toohello distribuzione di un servizio web che pubblica il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="5a7d4-106">Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="5a7d4-107">Hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) ha tutti toomake necessarie di funzionalità hello è più facile per i dati toostore gli esperti di dati di qualsiasi dimensione, forma e velocità e tooconduct elaborazione dei dati avanzate analitica e modellazione di machine learning con elevata scalabilità in un modo economico.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="5a7d4-108">Il pagamento viene effettuato per i singoli processi, solo quando i dati vengono effettivamente elaborati.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="5a7d4-109">Azure Data Lake Analitica include U-SQL, un linguaggio che blend hello natura dichiarativa di SQL con la potenza espressiva hello di c# tooprovide scalabile distributed funzionalità di query.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="5a7d4-110">Abilita tooprocess dati non strutturati tramite l'applicazione dello schema in lettura, inserire la logica personalizzata e definiti dall'utente (UDF) funzioni e include estendibilità tooenable con granularità fine un controllo accurato sul modo in tooexecute su larga scala.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="5a7d4-111">toolearn ulteriori informazioni su filosofia di progettazione hello U-SQL, vedere [post di blog di Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="5a7d4-112">Analisi Data Lake è anche un componente chiave di Cortana Analytics Suite e si integra con Azure SQL Data Warehouse, Power BI e Data Factory,</span><span class="sxs-lookup"><span data-stu-id="5a7d4-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="5a7d4-113">per offrire una piattaforma completa per Big Data sul cloud e per le analisi avanzate.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="5a7d4-114">Questa procedura dettagliata inizia con la descrizione hello prerequisiti e risorse che sono necessari toocomplete hello attività con Data Lake Analitica che formano processo di analisi scientifica dei dati hello e come tooinstall li.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="5a7d4-115">Quindi vengono delineati i passaggi di elaborazione dei dati hello utilizzando U-SQL e si conclude con la visualizzazione come toouse Python e Hive con Azure Machine Learning Studio toobuild e distribuire modelli predittivi hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="5a7d4-116">U-SQL e Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a7d4-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="5a7d4-117">Questa procedura dettagliata consiglia l'utilizzo di set di dati di Visual Studio tooedit U-SQL script tooprocess hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="5a7d4-118">script U-SQL Hello sono descritti di seguito e fornite in un file separato.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="5a7d4-119">il processo di Hello include l'inserimento di esplorazione e il campionamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="5a7d4-120">Viene inoltre illustrato come toorun U-SQL nello script di processo da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="5a7d4-121">Hive tabelle vengono create per i dati di hello in una compilazione associata dell'hello toofacilitate del cluster HDInsight e la distribuzione di un modello di classificazione binaria in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="5a7d4-122">Python</span><span class="sxs-lookup"><span data-stu-id="5a7d4-122">Python</span></span>
<span data-ttu-id="5a7d4-123">Questa procedura dettagliata contiene inoltre una sezione che illustra come toobuild e distribuire un modello predittivo tramite Python con Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="5a7d4-124">Viene fornito un server Jupyter notebook con script Python hello per questi passaggi del processo.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="5a7d4-125">blocco appunti Hello includono il codice per alcuni passaggi di progettazione di funzionalità aggiuntive e la costruzione di modelli, ad esempio multiclasse classificazione e regressione modellazione inoltre il modello di classificazione binaria toohello descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="5a7d4-126">attività di regressione Hello è toopredict hello suggerimento hello in base alle altre funzionalità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="5a7d4-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a7d4-127">Azure Machine Learning</span></span>
<span data-ttu-id="5a7d4-128">Azure Machine Learning Studio è toobuild utilizzato e distribuire modelli predittivi hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="5a7d4-129">Queste operazioni possono essere eseguite adottando un duplice approccio: prima con gli script Python e quindi con le tabelle Hive in un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="5a7d4-130">Script</span><span class="sxs-lookup"><span data-stu-id="5a7d4-130">Scripts</span></span>
<span data-ttu-id="5a7d4-131">Solo i passaggi principali hello sono descritte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="5a7d4-132">È possibile scaricare hello completo **script U-SQL** e **server Jupyter Notebook** da [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a7d4-133">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5a7d4-133">Prerequisites</span></span>
<span data-ttu-id="5a7d4-134">Prima di iniziare a questi argomenti, è necessario disporre delle seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="5a7d4-135">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-135">An Azure subscription.</span></span> <span data-ttu-id="5a7d4-136">Se non è già disponibile, vedere l'articolo che illustra [come ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="5a7d4-137">[Consigliato] Visual Studio 2013 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="5a7d4-138">Se non è già installata una di queste versioni, è possibile scaricare una versione Community gratuita da [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="5a7d4-139">Invece di Visual Studio, è possibile utilizzare anche le query di Azure Data Lake toosubmit di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="5a7d4-140">È verranno fornite istruzioni su come toodo così con Visual Studio e nel portale di hello nella sezione hello intitolata **elaborano i dati con U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="5a7d4-141">Preparare un ambiente di analisi scientifica dei dati per Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5a7d4-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="5a7d4-142">ambiente di analisi scientifica dei dati hello tooprepare per questa procedura dettagliata, creare hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="5a7d4-143">Archivio Azure Data Lake (ADLS)</span><span class="sxs-lookup"><span data-stu-id="5a7d4-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="5a7d4-144">Analisi Azure Data Lake (ADLA)</span><span class="sxs-lookup"><span data-stu-id="5a7d4-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="5a7d4-145">Account di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5a7d4-145">Azure Blob storage account</span></span>
* <span data-ttu-id="5a7d4-146">Account di Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5a7d4-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="5a7d4-147">Azure Data Lake Tools per Visual Studio (consigliato)</span><span class="sxs-lookup"><span data-stu-id="5a7d4-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="5a7d4-148">In questa sezione vengono fornite istruzioni su come toocreate di queste risorse.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="5a7d4-149">Se si scelgono toouse tabelle Hive con Azure Machine Learning, invece di Python, toobuild un modello, è necessario anche tooprovision un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="5a7d4-150">In questa procedura alternativa descritta nella sezione appropriata a hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="5a7d4-151">Hello **archivio Azure Data Lake** è possibile creare separatamente o quando si crea hello **Azure Data Lake Analitica** come spazio di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="5a7d4-152">Le istruzioni fanno riferimento per la creazione di ciascuna di queste risorse separatamente di seguito, ma hello account archivio Data Lake non è necessario crearli separatamente.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="5a7d4-153">Creare un Archivio Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5a7d4-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="5a7d4-154">Creare un ADLS da hello [portale Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5a7d4-155">Per informazioni dettagliate, vedere [Creare un cluster HDInsight con Archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="5a7d4-156">Essere tooset che di identità AAD Cluster Ciao hello **DataSource** blade di hello **configurazione facoltativa** pannello descritto non esiste.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="5a7d4-158">Creare un account di Analisi Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="5a7d4-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="5a7d4-159">Creare un account ADLA da hello [portale Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5a7d4-160">Per informazioni dettagliate, vedere [Esercitazione: Introduzione ad Analisi Azure Data Lake con il portale di Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="5a7d4-162">Creare un account di archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="5a7d4-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="5a7d4-163">Creare un account di archiviazione Blob di Azure da hello [portale Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="5a7d4-164">Per informazioni dettagliate, vedere hello crea un account di archiviazione sezione [gli account di archiviazione di Azure su](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="5a7d4-166">Configurare un account di Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5a7d4-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="5a7d4-167">Accedere in Azure Machine Learning Studio da hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pagina.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="5a7d4-168">Fare clic su hello **iniziare** pulsante e quindi scegliere un' "Area di lavoro disponibile" o "Area di lavoro Standard".</span><span class="sxs-lookup"><span data-stu-id="5a7d4-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="5a7d4-169">In seguito sarà in grado di toocreate esperimenti in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="5a7d4-170">Installare Azure Data Lake Tools [consigliato]</span><span class="sxs-lookup"><span data-stu-id="5a7d4-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="5a7d4-171">Installare Azure Data Lake Tools per la versione di Visual Studio in uso da [Azure Data Lake Tools per Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="5a7d4-173">Dopo l'installazione di hello viene completata correttamente, aprire Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="5a7d4-174">Verrà visualizzato hello Data Lake scheda hello menu nella parte superiore di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="5a7d4-175">Quando si accede all'account Azure, le risorse di Azure dovrebbero essere visualizzato nel riquadro sinistro di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="5a7d4-177">set di dati NYC Taxi trip Hello</span><span class="sxs-lookup"><span data-stu-id="5a7d4-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="5a7d4-178">Hello set di dati è utilizzati qui è un set di dati disponibile pubblicamente, hello [NYC Taxi trip dataset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="5a7d4-179">dati di andata e ritorno Taxi NYC Hello è costituita da circa 20GB di file CSV compressi (~ 48GB non compressi), registrazione 173 milioni hello e singoli trip tariffe a pagamento per ogni itinerario.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="5a7d4-180">Ogni record di andata e ritorno include percorsi di ritiro e deposito hello e volte, resi anonimi hack numero di patente) (e hello numero medallion (id univoco del taxi).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="5a7d4-181">dati Hello copre tutti i percorsi nell'anno hello 2013 e viene forniti in hello dopo i due set di dati per ogni mese:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="5a7d4-182">Hello 'trip_data' CSV contiene i dettagli di andata e ritorno, ad esempio il numero di passeggeri, prelievo e dropoff punti, la durata del viaggio e lunghezza di andata e ritorno.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="5a7d4-183">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="5a7d4-184">Hello 'trip_fare' CSV contiene i dettagli della tariffa di hello pagata per ogni itinerario, ad esempio il tipo di pagamento, quantità tariffa, supplemento e le imposte, suggerimenti e pedaggio e hello totale pagato.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="5a7d4-185">Di seguito vengono forniti alcuni record di esempio:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="5a7d4-186">viaggi toojoin chiave univoca Hello\_dati e andata e ritorno\_tariffa è costituito da tre campi seguenti hello: medallion, le maggiori\_licenza e prelievo\_datetime.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="5a7d4-187">il file CSV non elaborati di Hello sono accessibili da un blob di archiviazione di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="5a7d4-188">Hello script U-SQL per il join è in hello [Join di tabelle di andata e ritorno e tariffa](#join) sezione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="5a7d4-189">Elaborare i dati con U-SQL</span><span class="sxs-lookup"><span data-stu-id="5a7d4-189">Process data with U-SQL</span></span>
<span data-ttu-id="5a7d4-190">le attività di elaborazione dei dati Hello illustrate in questa sezione includono l'inserimento, controllo della qualità, esplorazione e il campionamento dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="5a7d4-191">Vengono inoltre illustrati come tabelle di andata e ritorno e tariffa toojoin.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="5a7d4-192">la sezione finale Hello Mostra esecuzione un processo con script U-SQL da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="5a7d4-193">Di seguito sono riportati collegamenti sottosezione tooeach:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="5a7d4-194">Inserimento di dati: leggere dati dal BLOB pubblico</span><span class="sxs-lookup"><span data-stu-id="5a7d4-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="5a7d4-195">Controlli della qualità dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="5a7d4-196">Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="5a7d4-197">Unire le tabelle relative a corse e tariffe</span><span class="sxs-lookup"><span data-stu-id="5a7d4-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="5a7d4-198">Campionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="5a7d4-199">Eseguire processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="5a7d4-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="5a7d4-200">script U-SQL Hello sono descritti di seguito e fornite in un file separato.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="5a7d4-201">È possibile scaricare hello completo **script U-SQL** da [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="5a7d4-202">tooexecute U-SQL, aprire Visual Studio, fare clic su **File--> Nuovo--> progetto**, scegliere **progetto U-SQL**, denominare e salvare la cartella tooa.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="5a7d4-204">È possibile toouse hello Azure Portal tooexecute U-SQL anziché Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="5a7d4-205">È possibile esplorare risorse di Azure Data Lake Analitica toohello nel portale di hello e inviare query direttamente come illustrato nella seguente illustrazione hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="5a7d4-207"><a name="ingest"></a>Inserimento di dati: leggere dati dal BLOB pubblico</span><span class="sxs-lookup"><span data-stu-id="5a7d4-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="5a7d4-208">percorso Hello dati hello in hello blob di Azure viene fatto riferimento come  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  e possono essere estratte con **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="5a7d4-209">Sostituire il nome di contenitore e il nome di account di archiviazione negli script seguenti per container_name@blob_storage_account_name indirizzo wasb hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="5a7d4-210">Poiché i nomi di file hello sono nello stesso formato, è possibile utilizzare **viaggi\_data_ {\*\}CSV** tooread in tutti i file di andata e ritorno 12.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="5a7d4-211">Poiché sono presenti intestazioni nella prima riga hello, è necessario intestazioni hello tooremove e modificare i tipi di colonna in quelli appropriati.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="5a7d4-212">È possibile salvare hello elaborato dati tooAzure Data Lake di archiviazione usando **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**account tramite l'archiviazione Blob _ o tooAzure  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="5a7d4-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="5a7d4-213">Analogamente è possibile leggere hello tariffa ai set di dati.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="5a7d4-214">Fare clic con il pulsante destro archivio Azure Data Lake, è possibile scegliere toolook i dati in **portale di Azure--> Esplora dati** o **Esplora File** all'interno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="5a7d4-217"><a name="quality"></a>Controlli della qualità dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="5a7d4-218">Dopo che è stato letto di andata e ritorno e tariffa tabelle, i controlli di qualità dei dati possono essere eseguiti nel seguente modo hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="5a7d4-219">Hello file CSV risultante può essere archiviazione Blob di output tooAzure o archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="5a7d4-220">Trovare il numero di hello di medallions e un numero univoco di medallions:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-221">È possibile trovare le licenze associate a più di 100 corse:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-222">È possibile trovare i record non validi a livello di valore pickup_longitude:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-223">È possibile trovare i valori mancanti per alcune variabili:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="5a7d4-224"><a name="explore"></a>Esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="5a7d4-225">È possibile eseguire alcune tooget l'esplorazione dei dati come una migliore comprensione dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="5a7d4-226">Trovare la distribuzione hello di trip inclinato e non inclinato:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-227">Trovare la distribuzione hello della quantità di suggerimento con valori di taglio: 0,5,10 e 20 dollari.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-228">È possibile trovare le statistiche di base relative alla distanza della corsa:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="5a7d4-229">Trovare i percentili hello della distanza di andata e ritorno:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="5a7d4-230"><a name="join"></a>Unire le tabelle relative a corse e tariffe</span><span class="sxs-lookup"><span data-stu-id="5a7d4-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="5a7d4-231">Le tabelle relative alle corse e alle tariffe possono essere unite in base ai valori medallion, hack_license e pickup_time.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="5a7d4-232">Per ogni livello del conteggio di passeggeri, calcolare il numero di hello di record, quantità media di suggerimento, la varianza della quantità di suggerimento, percentuale di viaggi inclinati.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="5a7d4-233"><a name="sample"></a>Campionamento dei dati</span><span class="sxs-lookup"><span data-stu-id="5a7d4-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="5a7d4-234">È in modo casuale selezionare innanzitutto 0,1% dei dati hello tabella unita in join hello:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="5a7d4-235">Eseguire quindi un campionamento stratificato in base alla variabile binaria tip_class:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="5a7d4-236"><a name="run"></a>Eseguire processi U-SQL</span><span class="sxs-lookup"><span data-stu-id="5a7d4-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="5a7d4-237">Al termine della modifica di script U-SQL, è possibile inviarli toohello server con l'account di Azure Data Lake Analitica.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="5a7d4-238">Fare clic su **Data Lake**, **Invia processo**, selezionare il proprio **account Analisi**, scegliere **Parallelismo** e fare clic sul pulsante **Invia**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="5a7d4-240">Quando processo hello è compilato correttamente, in Visual Studio verrà visualizzato lo stato di hello del processo per il monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="5a7d4-241">Al termine dell'esecuzione processo hello, è possibile anche riproduzione hello esecuzione processo e scoprire hello creare colli di bottiglia passaggi tooimprove l'efficienza del processo.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="5a7d4-242">È anche possibile passare tooAzure portale toocheck hello stato dei processi di U-SQL.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="5a7d4-245">Ora è possibile controllare i file di output di hello in archiviazione Blob di Azure o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="5a7d4-246">Si utilizzerà i dati di esempio hello stratificato per la modellazione nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="5a7d4-249">Compilare e distribuire modelli in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a7d4-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="5a7d4-250">Viene descritto come due opzioni disponibili per i dati toopull in Azure Machine Learning toobuild e</span><span class="sxs-lookup"><span data-stu-id="5a7d4-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="5a7d4-251">Nella prima opzione hello, utilizzare i dati campionato hello che sono stato scritto tooan Blob di Azure (in hello **campionamento dei dati** passaggio precedente) e utilizzare toobuild Python e distribuire modelli da Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="5a7d4-252">Nella seconda opzione hello, viene eseguita una query hello in Azure Data Lake direttamente tramite una query Hive.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="5a7d4-253">Questa opzione richiede di creare un nuovo cluster di HDInsight o utilizzare un cluster HDInsight esistente in cui hello Hive tabelle dati NY Taxi toohello punto di archiviazione di Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="5a7d4-254">Entrambe le opzioni sono illustrate di seguito.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="5a7d4-255">Opzione 1: Usare Python toobuild e distribuire modelli di machine learning</span><span class="sxs-lookup"><span data-stu-id="5a7d4-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="5a7d4-256">toobuild e distribuire i modelli di machine learning Usa Python, creare un server Jupyter Notebook nel computer locale o in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="5a7d4-257">Hello Server Jupyter Notebook fornito in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contiene hello tooexplore di codice completo, visualizzare i dati, progettazione di funzionalità, modellazione e distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="5a7d4-258">In questo articolo viene illustrata solo modellazione hello e la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="5a7d4-259">Importare librerie Python</span><span class="sxs-lookup"><span data-stu-id="5a7d4-259">Import Python libraries</span></span>
<span data-ttu-id="5a7d4-260">In hello toorun ordine esempio server Jupyter Notebook o file di script Python hello, hello pacchetti Python seguenti sono necessari.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="5a7d4-261">Se si utilizza il servizio di Azure ml Notebook hello, questi pacchetti sono stati preinstallati.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="5a7d4-262">Leggere dati hello dal blob</span><span class="sxs-lookup"><span data-stu-id="5a7d4-262">Read in hello data from blob</span></span>
* <span data-ttu-id="5a7d4-263">Connection String</span><span class="sxs-lookup"><span data-stu-id="5a7d4-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="5a7d4-264">Leggere come testo</span><span class="sxs-lookup"><span data-stu-id="5a7d4-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="5a7d4-266">Aggiungere i nomi di colonna e separare le colonne</span><span class="sxs-lookup"><span data-stu-id="5a7d4-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="5a7d4-267">Modificare toonumeric alcune colonne</span><span class="sxs-lookup"><span data-stu-id="5a7d4-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="5a7d4-268">Compilare modelli di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a7d4-268">Build machine learning models</span></span>
<span data-ttu-id="5a7d4-269">Abbiamo creato un toopredict modello di classificazione binaria se un trip è inclinato o non.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="5a7d4-270">Nel server Jupyter Notebook hello è possibile trovare altri due modelli: classificazione multiclasse e i modelli di regressione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="5a7d4-271">È prima necessario variabili fittizio toocreate che possono essere usate in scikit-informazioni su modelli</span><span class="sxs-lookup"><span data-stu-id="5a7d4-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="5a7d4-272">Creare frame di dati per la modellazione hello</span><span class="sxs-lookup"><span data-stu-id="5a7d4-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="5a7d4-273">Training e test della suddivisione 60-40</span><span class="sxs-lookup"><span data-stu-id="5a7d4-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="5a7d4-274">Regressione logistica nel set di training</span><span class="sxs-lookup"><span data-stu-id="5a7d4-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="5a7d4-275">Assegnare un punteggio al set di dati di test</span><span class="sxs-lookup"><span data-stu-id="5a7d4-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="5a7d4-276">Calcolare le metriche di valutazione</span><span class="sxs-lookup"><span data-stu-id="5a7d4-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="5a7d4-277">Compilare l'API del servizio Web e utilizzarla in Python</span><span class="sxs-lookup"><span data-stu-id="5a7d4-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="5a7d4-278">Vogliamo toooperationalize hello modello di machine learning dopo che è stata creata.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="5a7d4-279">Qui è usare modello logistica binario hello come esempio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="5a7d4-280">Verificare che scikit hello-informazioni su versione nel computer locale è 0.15.1.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="5a7d4-281">Se si utilizza servizio di Azure ML studio, non è più necessario tooworry su questo argomento.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="5a7d4-282">Trovare le credenziali dell'area di lavoro dalle impostazioni di Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="5a7d4-283">In Azure Machine Learning Studio fare clic su **Impostazioni** --> **Nome** --> **Token di autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![c3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="5a7d4-285">Creare un servizio Web</span><span class="sxs-lookup"><span data-stu-id="5a7d4-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="5a7d4-286">Ottenere le credenziali del servizio Web</span><span class="sxs-lookup"><span data-stu-id="5a7d4-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="5a7d4-287">Chiamare un'API del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-287">Call Web service API.</span></span> <span data-ttu-id="5a7d4-288">È necessario toowait 5-10 secondi dopo il passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="5a7d4-289">Opzione 2: Creare e distribuire modelli direttamente in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5a7d4-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="5a7d4-290">Azure Machine Learning Studio può leggere i dati direttamente dall'archivio Azure Data Lake e quindi essere toocreate utilizzato e distribuire modelli.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="5a7d4-291">Questo approccio utilizza una tabella Hive che punta al hello archivio Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="5a7d4-292">Questa operazione richiede che un cluster Azure HDInsight separato eseguirne il provisioning, in cui hello Hive viene creata nella tabella.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="5a7d4-293">Hello seguente mostra sezioni come toodo questo.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="5a7d4-294">Creare un cluster HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="5a7d4-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="5a7d4-295">Creare un HDInsight Cluster (Linux) da hello [portale Azure](http://portal.azure.com). Per informazioni dettagliate, vedere hello **creare un cluster HDInsight con accesso tooAzure archivio Data Lake** sezione [creare un cluster HDInsight con archivio Data Lake tramite il portale di Azure](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a7d4-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="5a7d4-297">Creare una tabella Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a7d4-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="5a7d4-298">È ora possibile creare toobe tabelle Hive usate in Azure Machine Learning Studio in cluster di HDInsight hello usando i dati di hello archiviati nell'archivio Azure Data Lake nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="5a7d4-299">Passare toohello cluster HDInsight appena creato.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="5a7d4-300">Fare clic su **impostazioni** --> **proprietà** --> **Cluster identità AAD** --> **ADLS accesso**, Verificare che l'account archivio Azure Data Lake viene aggiunto nell'elenco di hello con lettura, scrittura e diritti di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="5a7d4-302">Quindi fare clic su **Dashboard** toohello Avanti **impostazioni** pulsante e una finestra viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="5a7d4-303">Fare clic su **visualizzazione Hive** hello angolo superiore destro della pagina hello e si visualizzeranno hello **Editor di Query**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="5a7d4-306">Incolla in seguito hello Hive toocreate gli script di una tabella.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="5a7d4-307">Hello dell'origine dati si trova nella Guida di riferimento in questo modo archivio Azure Data Lake: **adl://data_lake_store_name.azuredatalakestore.net:443 nome_cartella/file_name**.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="5a7d4-308">Al termine dell'esecuzione query hello, vengono visualizzati risultati hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="5a7d4-310">Compilare e distribuire modelli in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="5a7d4-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="5a7d4-311">Ci sono ora pronti toobuild e distribuire un modello che stima o meno un suggerimento viene pagato con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="5a7d4-312">dati di esempio stratificato Hello sono pronto toobe utilizzati in questa classificazione binaria (suggerimento o non) problema.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="5a7d4-313">Hello modelli predittivi con classificazione multiclasse (tip_class) e regressione (tip_amount) può anche essere compilata e distribuita con Azure Machine Learning Studio, ma qui solo illustrare come toohandle hello maiuscole con hello modello di classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="5a7d4-314">Ottenere dati hello in Azure ML utilizzando hello **l'importazione dei dati** modulo, disponibile in hello **dati di Input e Output** sezione.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="5a7d4-315">Per ulteriori informazioni, vedere hello [modulo Importa dati](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) pagina di riferimento.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="5a7d4-316">Selezionare **Query Hive** come hello **origine dati** in hello **proprietà** pannello.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="5a7d4-317">Hello incollare lo script Hive in hello seguente **query database Hive** editor</span><span class="sxs-lookup"><span data-stu-id="5a7d4-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="5a7d4-318">Immettere il cluster di URI di HDInsight hello (questo è reperibile nel portale di Azure), le credenziali di Hadoop, posizione dei dati di output e il nome di contenitore/nome/chiave account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="5a7d4-320">Un esempio di lettura dei dati dalla tabella Hive un esperimento di classificazione binaria è illustrato nella figura hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="5a7d4-322">Dopo aver creato l'esperimento hello, fare clic su **di servizio Web** --> **predittiva servizio Web**</span><span class="sxs-lookup"><span data-stu-id="5a7d4-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="5a7d4-324">Assegnazione dei punteggi esperimento, al termine, fare clic su esecuzione hello creato automaticamente **distribuzione servizio Web**</span><span class="sxs-lookup"><span data-stu-id="5a7d4-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="5a7d4-326">verrà visualizzato a breve dashboard del servizio web Hello:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="5a7d4-328">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="5a7d4-328">Summary</span></span>
<span data-ttu-id="5a7d4-329">Seguendo questa procedura dettagliata è stato creato un ambiente di analisi scientifica dei dati per la creazione di soluzioni end-to-end scalabili in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="5a7d4-330">Questo ambiente è stato utilizzato tooanalyze un ampio set di dati pubblici, portarlo passaggi canonico hello hello il processo di analisi scientifica dei dati, dall'acquisizione dati training del modello, e quindi distribuzione toohello di hello del modello come un servizio web.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="5a7d4-331">U-SQL è stato utilizzato tooprocess, esplorare e hello dati di esempio.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="5a7d4-332">Python e Hive venivano utilizzati con Azure Machine Learning Studio toobuild e distribuire modelli predittivi.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="5a7d4-333">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a7d4-333">What's next?</span></span>
<span data-ttu-id="5a7d4-334">percorso di apprendimento Hello il [Team Data Science processo (TDSP)](http://aka.ms/datascienceprocess) fornisce collegamenti tootopics che descrivono ogni passaggio nel hello avanzate processo analitica.</span><span class="sxs-lookup"><span data-stu-id="5a7d4-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="5a7d4-335">Esistono una serie di procedure dettagliate dettagliate su hello [procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md) pagina come tale showcase toouse risorse e i servizi in vari scenari analitica predittiva:</span><span class="sxs-lookup"><span data-stu-id="5a7d4-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="5a7d4-336">Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5a7d4-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="5a7d4-337">Processo di analisi scientifica dei dati del Team di Hello in azione: utilizzo dei cluster HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5a7d4-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="5a7d4-338">Processo di analisi scientifica dei dati di Team Hello: utilizzo di SQL Server</span><span class="sxs-lookup"><span data-stu-id="5a7d4-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="5a7d4-339">Panoramica dell'utilizzo di processo di analisi scientifica dei dati hello nascita in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a7d4-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

