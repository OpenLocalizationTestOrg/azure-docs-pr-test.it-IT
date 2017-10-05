---
title: 'Processo di analisi scientifica dei dati per i team in azione: uso di un cluster Hadoop di Azure HDInsight su un set di dati da 1 TB | Documentazione Microsoft'
description: Uso del Processo di analisi scientifica dei dati per i team per uno scenario end-to-end in cui un cluster Hadoop di HDInsight viene usato per creare e distribuire un modello con un set di dati di grandi dimensioni (1 TB) disponibile pubblicamente
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="931ed-103">Processo di analisi scientifica dei dati per i team in azione: uso di un cluster Hadoop di Azure HDInsight su un set di dati da 1 TB</span><span class="sxs-lookup"><span data-stu-id="931ed-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="931ed-104">In questa procedura dettagliata viene descritto come usare in uno scenario end-to-end il Processo di analisi scientifica dei dati per i team con un [cluster Hadoop di Azure HDInsight](https://azure.microsoft.com/services/hdinsight/) per archiviare, esplorare e sottocampionare i dati, nonché progettare caratteristiche, da uno dei set di dati [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) disponibili pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="931ed-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="931ed-105">Viene usato Azure Machine Learning per creare un modello di classificazione binaria in questi dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="931ed-106">Viene inoltre illustrato come pubblicare uno di questi modelli come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="931ed-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="931ed-107">Per eseguire le attività presentate in questa procedura dettagliata, è anche possibile usare IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="931ed-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="931ed-108">Se si vuole provare questo approccio, vedere l'argomento [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) (Procedura dettagliata su Criteo con una connessione Hive ODBC).</span><span class="sxs-lookup"><span data-stu-id="931ed-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="931ed-109"><a name="dataset"></a>Descrizione del set di dati Criteo</span><span class="sxs-lookup"><span data-stu-id="931ed-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="931ed-110">I dati Criteo sono un set di dati di stima dei clic raccolti in file TSV compressi nel formato gzip con dimensioni di circa 370 GB (circa 1,3 TB non compressi) e includono più di 4,3 miliardi di record.</span><span class="sxs-lookup"><span data-stu-id="931ed-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="931ed-111">I valori sono ottenuti da 24 giorni di dati sui clic resi disponibili da [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="931ed-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="931ed-112">Per semplificare il lavoro dei data scientist, sono disponibili dati non compressi con cui eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="931ed-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="931ed-113">Ogni record nel set di dati contiene 40 colonne:</span><span class="sxs-lookup"><span data-stu-id="931ed-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="931ed-114">la prima colonna è una colonna di etichetta che indica se un utente fa clic su un **annuncio** (valore 1) o non fa clic (valore 0)</span><span class="sxs-lookup"><span data-stu-id="931ed-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="931ed-115">le successive 13 colonne sono di tipo numerico</span><span class="sxs-lookup"><span data-stu-id="931ed-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="931ed-116">le ultime 26 colonne sono di tipo categorico</span><span class="sxs-lookup"><span data-stu-id="931ed-116">last 26 are categorical columns</span></span>

<span data-ttu-id="931ed-117">Le colonne sono rese anonime e usano una serie di nomi enumerati: da "Col1" (per la colonna di etichetta) a "Col40" (per l'ultima colonna categorica).</span><span class="sxs-lookup"><span data-stu-id="931ed-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="931ed-118">Di seguito è riportato un estratto delle prime 20 colonne di due osservazioni (righe) di questo set di dati:</span><span class="sxs-lookup"><span data-stu-id="931ed-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="931ed-119">Il set di dati presenta valori mancanti sia nelle colonne numeriche sia in quelle categoriche.</span><span class="sxs-lookup"><span data-stu-id="931ed-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="931ed-120">Di seguito viene descritto un semplice metodo per la gestione dei valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="931ed-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="931ed-121">Altri dettagli relativi ai dati sono illustrati quando vengono archiviati nelle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="931ed-122">**Definizione:** *percentuale di click-through (CTR, Clickthrough Rate):* indica la percentuale di clic nei dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="931ed-123">In questo set di dati Criteo, il valore corrisponde circa al 3,3% o 0,033.</span><span class="sxs-lookup"><span data-stu-id="931ed-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="931ed-124"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="931ed-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="931ed-125">Questa procedura dettagliata illustra due problemi di stima di esempio:</span><span class="sxs-lookup"><span data-stu-id="931ed-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="931ed-126">**Classificazione binaria**: stima se un utente ha fatto clic su un annuncio:</span><span class="sxs-lookup"><span data-stu-id="931ed-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="931ed-127">Classe 0: nessun clic</span><span class="sxs-lookup"><span data-stu-id="931ed-127">Class 0: No Click</span></span>
   * <span data-ttu-id="931ed-128">Classe 1: clic</span><span class="sxs-lookup"><span data-stu-id="931ed-128">Class 1: Click</span></span>
2. <span data-ttu-id="931ed-129">**Regressione**: stima la probabilità di un clic su un annuncio in base alle caratteristiche dell'utente.</span><span class="sxs-lookup"><span data-stu-id="931ed-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="931ed-130"><a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi scientifica</span><span class="sxs-lookup"><span data-stu-id="931ed-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="931ed-131">**Nota:** in genere, questa attività viene svolta da un **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="931ed-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="931ed-132">Per configurare l'ambiente di analisi scientifica dei dati di Azure per la creazione di soluzioni di analisi predittiva con i cluster HDInsight, sono necessari tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="931ed-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="931ed-133">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): l'account di archiviazione viene usato per archiviare i dati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="931ed-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="931ed-134">I dati usati nei cluster HDInsight vengono archiviati in questa posizione.</span><span class="sxs-lookup"><span data-stu-id="931ed-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="931ed-135">[Personalizzare i cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md): questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="931ed-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="931ed-136">Quando si personalizza il cluster HDInsight, occorre completare due importanti passaggi descritti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="931ed-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="931ed-137">È necessario collegare l'account di archiviazione creato nel passaggio 1 al cluster HDInsight al momento della creazione.</span><span class="sxs-lookup"><span data-stu-id="931ed-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="931ed-138">Questo account di archiviazione viene usato per accedere ai dati che possono essere elaborati all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="931ed-139">È necessario abilitare l'accesso remoto al nodo head del cluster dopo la creazione.</span><span class="sxs-lookup"><span data-stu-id="931ed-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="931ed-140">Ricordare le credenziali di accesso remoto specificate qui, che sono diverse da quelle specificate durante la creazione del cluster, perché sono necessarie per completare le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="931ed-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="931ed-141">[Creare un'area di lavoro di Azure ML](machine-learning-create-workspace.md): l'area di lavoro di Azure Machine Learning viene usata per la creazione di modelli di Machine Learning dopo l'esplorazione iniziale dei dati e il loro sottocampionamento nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="931ed-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="931ed-142"><a name="getdata"></a>Ottenere e utilizzare i dati da un'origine pubblica</span><span class="sxs-lookup"><span data-stu-id="931ed-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="931ed-143">È possibile accedere al set di dati [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) facendo clic sul collegamento, accettando le condizioni per l'utilizzo e specificando un nome.</span><span class="sxs-lookup"><span data-stu-id="931ed-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="931ed-144">Ecco uno snapshot di come appare:</span><span class="sxs-lookup"><span data-stu-id="931ed-144">A snapshot of what this looks like is shown here:</span></span>

![Accettazione delle condizioni Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="931ed-146">Fare clic su **Continue to Download** (Continuare per il download) per leggere altre informazioni sul set di dati e sulla relativa disponibilità.</span><span class="sxs-lookup"><span data-stu-id="931ed-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="931ed-147">I dati si trovano in una posizione di [archiviazione BLOB di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) pubblico: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="931ed-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="931ed-148">La sintassi "wasb" indica la posizione di archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="931ed-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="931ed-149">I dati in questo archivio BLOB pubblico sono costituiti da tre sottocartelle di dati non compressi.</span><span class="sxs-lookup"><span data-stu-id="931ed-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="931ed-150">La sottocartella *raw/count/* contiene i primi 21 giorni di dati, da day\_00 a day\_20</span><span class="sxs-lookup"><span data-stu-id="931ed-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="931ed-151">La sottocartella *raw/train/* è costituita da un singolo giorno di dati, day\_21</span><span class="sxs-lookup"><span data-stu-id="931ed-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="931ed-152">La sottocartella *raw/test/* è costituita da due giorni di dati, day\_22 e day\_23</span><span class="sxs-lookup"><span data-stu-id="931ed-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="931ed-153">Se si vuole iniziare usando i dati in formato gzip non elaborati, questi sono disponibili nella cartella principale *raw/* e indicati come day_NN.gz, dove NN va da 00 a 23.</span><span class="sxs-lookup"><span data-stu-id="931ed-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="931ed-154">Un approccio alternativo per accedere ai dati, esplorarli e modellarli senza eseguire alcun download locale è descritto più avanti in questa procedura dettagliata, al momento della creazione delle tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="931ed-155"><a name="login"></a>Accedere al nodo head del cluster</span><span class="sxs-lookup"><span data-stu-id="931ed-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="931ed-156">Per accedere al nodo head del cluster, usare il [portale di Azure](https://ms.portal.azure.com) per individuare il cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="931ed-157">Fare clic sull'icona a forma di elefante di HDInsight a sinistra e quindi fare doppio clic sul nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="931ed-158">Passare alla scheda **Configurazione** , fare doppio clic sull'icona CONNETTI nella parte inferiore della pagina e immettere le credenziali di accesso remoto quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="931ed-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="931ed-159">In questo modo, verrà visualizzato il nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="931ed-160">Ecco la tipica finestra visualizzata al primo accesso al nodo head del cluster:</span><span class="sxs-lookup"><span data-stu-id="931ed-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Accesso al cluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="931ed-162">A sinistra è presente la "riga di comando di Hadoop", che viene usata per l'esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="931ed-163">Sono inoltre disponibili due utili URL, "Hadoop Yarn Status" e "Hadoop Name Node".</span><span class="sxs-lookup"><span data-stu-id="931ed-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="931ed-164">Il primo URL mostra lo stato del processo, mentre il secondo fornisce informazioni dettagliate sulla configurazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="931ed-165">Ora che la configurazione è stata completata, è possibile iniziare la prima parte della procedura dettagliata, ovvero l'esplorazione dei dati tramite Hive e la loro preparazione per Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="931ed-166"><a name="hive-db-tables"></a> Creare il database e le tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="931ed-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="931ed-167">Per creare le tabelle Hive per il set di dati Criteo, aprire la ***riga di comando di Hadoop*** sul desktop del nodo head e specificare la directory Hive immettendo il comando</span><span class="sxs-lookup"><span data-stu-id="931ed-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="931ed-168">Al prompt della directory bin/ Hive eseguire tutti i comandi di Hive riportati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="931ed-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="931ed-169">In questo modo, eventuali problemi di percorso vengono risolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="931ed-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="931ed-170">I termini "prompt della directory Hive", "prompt della directory bin/ Hive" e "riga di comando di Hadoop" vengono usati in modo intercambiabile.</span><span class="sxs-lookup"><span data-stu-id="931ed-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="931ed-171">Per eseguire qualsiasi query Hive, è sempre possibile usare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="931ed-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="931ed-172">Dopo che viene visualizzata la shell REPL Hive con l'indicazione "hive >", è sufficiente tagliare e incollare la query per eseguirla.</span><span class="sxs-lookup"><span data-stu-id="931ed-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="931ed-173">Il codice seguente crea un database "criteo" e quindi genera 4 tabelle:</span><span class="sxs-lookup"><span data-stu-id="931ed-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="931ed-174">una *tabella per la generazione di conteggi* compilata nei giorni compresi tra day\_00 e day\_20</span><span class="sxs-lookup"><span data-stu-id="931ed-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="931ed-175">una *tabella da usare come set di dati di training* compilata il giorno day\_21</span><span class="sxs-lookup"><span data-stu-id="931ed-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="931ed-176">due *tabelle da usare come set di dati di test* compilate rispettivamente nei giorni day\_22 e day\_23</span><span class="sxs-lookup"><span data-stu-id="931ed-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="931ed-177">Il set di dati di test è suddiviso in due diverse tabelle perché uno dei giorni è festivo e si vuole determinare se il modello è in grado di rilevare le differenze tra un giorno festivo e uno non festivo in base alla percentuale di click-through.</span><span class="sxs-lookup"><span data-stu-id="931ed-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="931ed-178">Lo script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) è visualizzato qui per praticità:</span><span class="sxs-lookup"><span data-stu-id="931ed-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="931ed-179">È possibile notare che queste tabelle sono tutte esterne in quanto si punta semplicemente a posizioni di archiviazione BLOB di Azure (wasb).</span><span class="sxs-lookup"><span data-stu-id="931ed-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="931ed-180">**Ci sono due modi per eseguire QUALSIASI query Hive, come viene spiegato di seguito.**</span><span class="sxs-lookup"><span data-stu-id="931ed-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="931ed-181">**Usando la riga di comando REPL Hive**: il primo modo consiste nell'eseguire un comando "hive" e copiare e incollare la query nella riga di comando REPL Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="931ed-182">A tale scopo, eseguire l'operazione seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="931ed-183">A questo punto, tagliando e incollando la query nella riga di comando REPL questa viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="931ed-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="931ed-184">**Salvando le query in un file ed eseguendo il comando**: il secondo modo consiste nel salvare le query in un file con estensione hql ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) e quindi eseguire il comando seguente per eseguire la query:</span><span class="sxs-lookup"><span data-stu-id="931ed-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="931ed-185">Verificare la creazione del database e della tabella</span><span class="sxs-lookup"><span data-stu-id="931ed-185">Confirm database and table creation</span></span>
<span data-ttu-id="931ed-186">Viene quindi verificata la creazione del database con il comando seguente al prompt della directory bin/ Hive:</span><span class="sxs-lookup"><span data-stu-id="931ed-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="931ed-187">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="931ed-188">Ciò conferma la creazione del nuovo database, "criteo".</span><span class="sxs-lookup"><span data-stu-id="931ed-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="931ed-189">Per vedere quali tabelle sono state create, è sufficiente eseguire il comando seguente al prompt della directory bin/ Hive:</span><span class="sxs-lookup"><span data-stu-id="931ed-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="931ed-190">Verrà quindi visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="931ed-191"><a name="exploration"></a> Esplorazione dei dati in Hive</span><span class="sxs-lookup"><span data-stu-id="931ed-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="931ed-192">A questo punto, è possibile passare ad alcune attività di base di esplorazione dei dati in Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="931ed-193">Innanzitutto, viene contato il numero di esempi nelle tabelle di dati di training e di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="931ed-194">Numero di esempi di training</span><span class="sxs-lookup"><span data-stu-id="931ed-194">Number of train examples</span></span>
<span data-ttu-id="931ed-195">Il contenuto di [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) è visualizzato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="931ed-196">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="931ed-197">In alternativa, è anche possibile eseguire questo comando al prompt della directory bin/ Hive:</span><span class="sxs-lookup"><span data-stu-id="931ed-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="931ed-198">Numero di esempi di test nei due set di dati di test</span><span class="sxs-lookup"><span data-stu-id="931ed-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="931ed-199">Viene ora contato il numero di esempi di test nei due set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="931ed-200">Il contenuto di [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) è visualizzato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="931ed-201">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="931ed-202">Come di consueto, è anche possibile chiamare lo script al prompt della directory bin/ Hive eseguendo questo comando:</span><span class="sxs-lookup"><span data-stu-id="931ed-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="931ed-203">Infine, viene esaminato il numero di esempi di test nel set di dati di test basato sul giorno 23 (day\_23).</span><span class="sxs-lookup"><span data-stu-id="931ed-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="931ed-204">Il comando per eseguire questa operazione è simile a quello illustrato in precedenza. Vedere [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql):</span><span class="sxs-lookup"><span data-stu-id="931ed-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="931ed-205">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="931ed-206">Distribuzione delle etichette nel set di dati di training</span><span class="sxs-lookup"><span data-stu-id="931ed-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="931ed-207">La distribuzione delle etichette nel set di dati di training è un aspetto interessante.</span><span class="sxs-lookup"><span data-stu-id="931ed-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="931ed-208">Per vederla, è necessario visualizzare il contenuto di [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="931ed-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="931ed-209">Il risultato sarà la distribuzione delle etichette:</span><span class="sxs-lookup"><span data-stu-id="931ed-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="931ed-210">Si noti che la percentuale di etichette positive equivale circa al 3,3% (coerente con il set di dati originale).</span><span class="sxs-lookup"><span data-stu-id="931ed-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="931ed-211">Distribuzioni nell'istogramma di alcune variabili numeriche nel set di dati di training</span><span class="sxs-lookup"><span data-stu-id="931ed-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="931ed-212">È possibile usare la funzione "histogram\_numeric" nativa di Hive per visualizzare la distribuzione delle variabili numeriche.</span><span class="sxs-lookup"><span data-stu-id="931ed-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="931ed-213">Ecco il contenuto di [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="931ed-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="931ed-214">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="931ed-215">La combinazione LATERAL VIEW - explode in Hive serve a produrre un output simile a quello di SQL anziché il solito elenco.</span><span class="sxs-lookup"><span data-stu-id="931ed-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="931ed-216">Si noti che in questa tabella la prima colonna corrisponde al valore di bin_center e la seconda alla relativa frequenza.</span><span class="sxs-lookup"><span data-stu-id="931ed-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="931ed-217">Percentili approssimativi di alcune variabili numeriche nel set di dati di training</span><span class="sxs-lookup"><span data-stu-id="931ed-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="931ed-218">Un altro aspetto interessante in relazione alle variabili numeriche è il calcolo dei percentili approssimativi.</span><span class="sxs-lookup"><span data-stu-id="931ed-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="931ed-219">A tale scopo, è disponibile la funzione "percentile\_approx" nativa di Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="931ed-220">Il contenuto di [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="931ed-221">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="931ed-222">Tenere presente che la distribuzione dei percentili è in genere strettamente correlata alla distribuzione nell'istogramma di qualsiasi variabile numerica.</span><span class="sxs-lookup"><span data-stu-id="931ed-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="931ed-223">Trovare il numero di valori univoci per alcune colonne categoriche nel set di dati di training</span><span class="sxs-lookup"><span data-stu-id="931ed-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="931ed-224">Continuando l'esplorazione dei dati viene ora trovato, per alcune colonne categoriche, il numero di valori univoci accettati.</span><span class="sxs-lookup"><span data-stu-id="931ed-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="931ed-225">A tale scopo, viene visualizzato il contenuto di [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="931ed-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="931ed-226">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="931ed-227">Si noti che Col15 ha 19 milioni di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="931ed-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="931ed-228">Non è possibile usare tecniche di base come la "codifica one-hot" per codificare variabili categoriche con dimensionalità così elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="931ed-229">In particolare, viene spiegata e illustrata una tecnica avanzata e affidabile di [apprendimento in base ai conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) per affrontare il problema in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="931ed-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="931ed-230">Come ultima operazione di questa sottosezione, viene esaminato il numero di valori univoci per altre colonne categoriche.</span><span class="sxs-lookup"><span data-stu-id="931ed-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="931ed-231">Il contenuto di [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="931ed-232">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="931ed-233">Anche in questo caso è possibile notare che, ad eccezione di Col20, tutte le altre colonne includono numerosi valori univoci.</span><span class="sxs-lookup"><span data-stu-id="931ed-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="931ed-234">Conteggio della co-occorrenza di coppie di variabili categoriche nel set di dati di training</span><span class="sxs-lookup"><span data-stu-id="931ed-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="931ed-235">Anche il conteggio della co-occorrenza di coppie di variabili categoriche è un aspetto interessante.</span><span class="sxs-lookup"><span data-stu-id="931ed-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="931ed-236">Per determinarlo, è possibile usare il codice in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="931ed-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="931ed-237">In questo caso, i conteggi vengono visualizzati in ordine inverso in base all'occorrenza e vengono osservati i primi 15 risultati.</span><span class="sxs-lookup"><span data-stu-id="931ed-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="931ed-238">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="931ed-239"><a name="downsample"></a> Sottocampionare i set di dati per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="931ed-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="931ed-240">Dopo avere esplorato i set di dati e avere visto come eseguire questo tipo di esplorazione per qualsiasi variabile (inclusione le combinazioni), è ora possibile sottocampionare i set di dati in modo da poter creare modelli in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="931ed-241">Tenere presente il problema centrale, ovvero dato un set di attributi di esempio (valori delle caratteristiche da Col2 a Col40), si deve stimare se Col1 è 0 (nessun clic) o 1 (clic).</span><span class="sxs-lookup"><span data-stu-id="931ed-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="931ed-242">Per sottocampionare i set di dati di training e di test riducendoli all'1% delle dimensioni originali, è possibile usare la funzione RAND() nativa di Hive.</span><span class="sxs-lookup"><span data-stu-id="931ed-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="931ed-243">Lo script successivo, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) consente di eseguire questa operazione per il set di dati di training:</span><span class="sxs-lookup"><span data-stu-id="931ed-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="931ed-244">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="931ed-245">Lo script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) esegue la stessa operazione per i dati di test del giorno 22 (day\_22):</span><span class="sxs-lookup"><span data-stu-id="931ed-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="931ed-246">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="931ed-247">Infine, lo script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) esegue l'operazione per i dati di test del giorno 23 (day\_23):</span><span class="sxs-lookup"><span data-stu-id="931ed-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="931ed-248">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="931ed-249">A questo punto, è possibile usare i set di dati di training e di test sottocampionati per creare modelli in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="931ed-250">Prima di passare ad Azure Machine Learning, c'è un importante componente finale, relativo alla tabella di conteggio.</span><span class="sxs-lookup"><span data-stu-id="931ed-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="931ed-251">Questo aspetto verrà analizzato in modo più dettagliato nella sottosezione successiva.</span><span class="sxs-lookup"><span data-stu-id="931ed-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="931ed-252"><a name="count"></a> Breve discussione sulla tabella di conteggio</span><span class="sxs-lookup"><span data-stu-id="931ed-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="931ed-253">Come è stato visto, diverse variabili categoriche hanno una dimensionalità molto elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="931ed-254">Nella procedura dettagliata viene presentata una tecnica avanzata, detta tecnica di [apprendimento in base ai conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) , che consente di codificare queste variabili in modo affidabile ed efficiente.</span><span class="sxs-lookup"><span data-stu-id="931ed-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="931ed-255">Altre informazioni su questa tecnica sono disponibili facendo clic sul relativo collegamento.</span><span class="sxs-lookup"><span data-stu-id="931ed-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="931ed-256">In questa procedura dettagliata viene esaminato l'uso di tabelle di conteggio per produrre rappresentazioni compatte di funzionalità di tipo categorico con dimensionalità elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="931ed-257">Questa tecnica non è l'unico modo disponibile per codificare le funzionalità categoriche. Per altre informazioni su tecniche diverse, è possibile vedere gli argomenti relativi alla [codifica one-hot](http://en.wikipedia.org/wiki/One-hot) e all'[hashing delle funzioni](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="931ed-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="931ed-258">Per creare tabelle di conteggio sui dati di conteggio, vengono usati i dati nella cartella raw/count.</span><span class="sxs-lookup"><span data-stu-id="931ed-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="931ed-259">Nella sezione relativa alla modellazione viene illustrato come creare da zero queste tabelle di conteggio per le caratteristiche categoriche oppure, in alternativa, come usare una tabella di conteggio preesistente per le analisi.</span><span class="sxs-lookup"><span data-stu-id="931ed-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="931ed-260">Con "tabelle di conteggio preesistenti" si intendono le tabelle fornite da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="931ed-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="931ed-261">Istruzioni dettagliate su come accedere a queste tabelle sono disponibili nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="931ed-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="931ed-262"><a name="aml"></a> Creare un modello con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="931ed-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="931ed-263">Il processo di creazione di un modello in Azure Machine Learning prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="931ed-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="931ed-264">Ottenere i dati dalle tabelle Hive in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="931ed-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="931ed-265">Creare l'esperimento: pulire i dati e definire le caratteristiche con le tabelle di conteggio</span><span class="sxs-lookup"><span data-stu-id="931ed-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="931ed-266">Compilare, eseguire il training e assegnare un punteggio al modello</span><span class="sxs-lookup"><span data-stu-id="931ed-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="931ed-267">Valutare il modello</span><span class="sxs-lookup"><span data-stu-id="931ed-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="931ed-268">Pubblicare il modello come servizio Web</span><span class="sxs-lookup"><span data-stu-id="931ed-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="931ed-269">È ora possibile creare modelli in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="931ed-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="931ed-270">I dati sottocampionati vengono salvati come tabelle Hive nel cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="931ed-271">Per leggere i dati viene usato il modulo **Import Data** (Importa dati) di Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="931ed-272">Le credenziali per accedere all'account di archiviazione del cluster sono indicate di seguito.</span><span class="sxs-lookup"><span data-stu-id="931ed-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="931ed-273"><a name="step1"></a> Passaggio 1: Ottenere i dati dalle tabelle Hive in Azure Machine Learning usando il modulo Import Data e selezionarli per un esperimento di Machine Learning</span><span class="sxs-lookup"><span data-stu-id="931ed-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="931ed-274">Per iniziare, selezionare **+NEW** -> **EXPERIMENT** -> **Blank Experiment** (+NUOVO -> ESPERIMENTO -> Esperimento vuoto).</span><span class="sxs-lookup"><span data-stu-id="931ed-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="931ed-275">Quindi, nella casella **Search** (Ricerca) in alto a sinistra cercare "Import Data".</span><span class="sxs-lookup"><span data-stu-id="931ed-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="931ed-276">Trascinare il modulo **Import Data** sull'area di disegno degli esperimenti (la parte centrale della schermata) per usare il modulo per l'accesso ai dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="931ed-277">Ecco l'aspetto del modulo **Import Data** durante il recupero dei dati dalla tabella Hive:</span><span class="sxs-lookup"><span data-stu-id="931ed-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Acquisizione di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="931ed-279">Per il modulo **Import Data** i valori dei parametri forniti nel grafico sono solo esempi del tipo di valori che è necessario specificare.</span><span class="sxs-lookup"><span data-stu-id="931ed-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="931ed-280">Di seguito sono illustrate alcune indicazioni generali su come compilare il set di parametri per il modulo **Import Data** .</span><span class="sxs-lookup"><span data-stu-id="931ed-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="931ed-281">In **Data Source**</span><span class="sxs-lookup"><span data-stu-id="931ed-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="931ed-282">Nella casella **Hive database query** (Query di database Hive) è sufficiente specificare l'istruzione SELECT * FROM <nome\_del\_database.nome\_della\_tabella>.</span><span class="sxs-lookup"><span data-stu-id="931ed-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="931ed-283">**Hcatalog server URI** (URI del server Hcatalog): se il cluster è "abc", specificare semplicemente https://abc.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="931ed-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="931ed-284">**Hadoop user account name** (Nome dell'account utente Hadoop): nome utente scelto al momento dell'autorizzazione del cluster</span><span class="sxs-lookup"><span data-stu-id="931ed-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="931ed-285">(NON il nome utente di accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="931ed-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="931ed-286">**Hadoop user account password** (Password dell'account utente Hadoop): password per il nome utente scelta al momento dell'autorizzazione del cluster</span><span class="sxs-lookup"><span data-stu-id="931ed-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="931ed-287">(NON la password di accesso remoto).</span><span class="sxs-lookup"><span data-stu-id="931ed-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="931ed-288">**Location of output data**: scegliere "Azure".</span><span class="sxs-lookup"><span data-stu-id="931ed-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="931ed-289">**Azure storage account name**: account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="931ed-290">**Azure storage account key**: chiave dell'account di archiviazione associato al cluster.</span><span class="sxs-lookup"><span data-stu-id="931ed-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="931ed-291">**Azure container name**: se il nome del cluster è "abc", in genere questo valore è semplicemente "abc".</span><span class="sxs-lookup"><span data-stu-id="931ed-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="931ed-292">Quando il modulo **Import Data** termina il recupero dei dati, il completamento è indicato da un segno di spunta verde nel modulo, salvarli come set di dati con un nome a propria scelta.</span><span class="sxs-lookup"><span data-stu-id="931ed-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="931ed-293">L'aspetto è il seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-293">What this looks like:</span></span>

![Salvataggio di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="931ed-295">Fare clic con il pulsante destro del mouse sulla porta di output del modulo **Import Data** .</span><span class="sxs-lookup"><span data-stu-id="931ed-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="931ed-296">Verranno visualizzate le opzioni **Save as dataset** (Salva come set di dati) e **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="931ed-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="931ed-297">Facendo clic sull'opzione **Visualize** vengono visualizzati 100 righe di dati e un pannello, sul lato destro, utile per le statistiche di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="931ed-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="931ed-298">Per salvare i dati, è sufficiente selezionare **Save as dataset** e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="931ed-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="931ed-299">Per selezionare il set di dati salvato per l'uso in un esperimento di Machine Learning, individuare il set di dati usando la casella **Search** (Ricerca) illustrata nella figura seguente.</span><span class="sxs-lookup"><span data-stu-id="931ed-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="931ed-300">Digitare quindi una parte del nome assegnato al set di dati per accedervi e trascinare il set di dati nel pannello principale.</span><span class="sxs-lookup"><span data-stu-id="931ed-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="931ed-301">Rilasciando il set di dati sul pannello principale, questo viene selezionato per la modellazione in Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Trascinare il set di dati nel pannello principale](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="931ed-303">Eseguire questa operazione per entrambi i set di dati, di training e di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="931ed-304">Ricordare anche di usare il nome database e i nomi delle tabelle assegnati a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="931ed-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="931ed-305">I valori usati nella figura hanno puramente scopo illustrativo.**</span><span class="sxs-lookup"><span data-stu-id="931ed-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="931ed-306"><a name="step2"></a> Passaggio 2: Creare un semplice esperimento in Azure Machine Learning per stimare i clic o l'assenza di clic</span><span class="sxs-lookup"><span data-stu-id="931ed-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="931ed-307">L'esperimento di Azure ML è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-307">Our Azure ML experiment looks like this:</span></span>

![Esperimento di Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="931ed-309">Ora si esamineranno i componenti chiave di questo esperimento.</span><span class="sxs-lookup"><span data-stu-id="931ed-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="931ed-310">Si ricordi che prima è necessario trascinare i set di dati di training e di test salvati sull'area di disegno degli esperimenti.</span><span class="sxs-lookup"><span data-stu-id="931ed-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="931ed-311">Pulire i dati mancanti</span><span class="sxs-lookup"><span data-stu-id="931ed-311">Clean Missing Data</span></span>
<span data-ttu-id="931ed-312">Il modulo **Clean Missing Data** (Pulisci dati mancanti) pulisce i dati mancanti in un modo che può essere specificato dall'utente.</span><span class="sxs-lookup"><span data-stu-id="931ed-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="931ed-313">Analizzando il modulo, è possibile vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="931ed-313">Looking into this module, we see this:</span></span>

![Pulire i dati mancanti](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="931ed-315">In questo caso, si sceglie di sostituire tutti i valori mancanti con 0.</span><span class="sxs-lookup"><span data-stu-id="931ed-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="931ed-316">Sono disponibili anche altre opzioni, che è possibile visualizzare aprendo gli elenchi a discesa nel modulo.</span><span class="sxs-lookup"><span data-stu-id="931ed-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="931ed-317">Progettazione di funzionalità per i dati</span><span class="sxs-lookup"><span data-stu-id="931ed-317">Feature engineering on the data</span></span>
<span data-ttu-id="931ed-318">Per alcune funzioni categoriche di set di dati di grandi dimensioni possono esistere milioni di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="931ed-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="931ed-319">Non è possibile usare metodi di base come la codifica one-hot per rappresentare funzioni categoriche con dimensionalità così elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="931ed-320">In questa procedura dettagliata, viene illustrato come usare le funzioni di conteggio con i moduli predefiniti di Azure Machine Learning per generare rappresentazioni compatte di queste funzioni categoriche con dimensionalità così elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="931ed-321">Come risultato finale si ottengono dimensioni minori per il modello, tempi di training più rapidi e metriche delle prestazioni abbastanza simili all'uso di altre tecniche.</span><span class="sxs-lookup"><span data-stu-id="931ed-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="931ed-322">Compilazione di trasformazioni conteggio</span><span class="sxs-lookup"><span data-stu-id="931ed-322">Building counting transforms</span></span>
<span data-ttu-id="931ed-323">Per compilare funzioni di conteggio, si usa il modulo **Build Counting Transform** disponibile in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="931ed-324">Il modulo è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-324">The module looks like this:</span></span>

<span data-ttu-id="931ed-325">![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="931ed-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="931ed-326">Nella casella **Count columns** (Colonne conteggio) si immettono le colonne su cui eseguire i conteggi.</span><span class="sxs-lookup"><span data-stu-id="931ed-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="931ed-327">Come indicato in precedenza, si tratta in genere di colonne categoriche con dimensionalità elevata.</span><span class="sxs-lookup"><span data-stu-id="931ed-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="931ed-328">All'inizio si è detto che il set di dati Criteo contiene 26 colonne categoriche: da Col15 a Col40.</span><span class="sxs-lookup"><span data-stu-id="931ed-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="931ed-329">Ora vengono tenute tutte in considerazione e si assegnano gli indici (da 15 a 40 separati da virgole, come nella figura).</span><span class="sxs-lookup"><span data-stu-id="931ed-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="931ed-330">Per usare il modulo in modalità MapReduce, appropriata per i set di dati di grandi dimensioni, è necessario accedere a un cluster Hadoop HDInsight (quello usato per esplorare le funzionalità può essere usato anche a questo scopo) e alle relative credenziali.</span><span class="sxs-lookup"><span data-stu-id="931ed-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="931ed-331">Le figure precedenti illustrano i valori inseriti. Sostituire i valori forniti a scopo illustrativo con quelli pertinenti al proprio caso d'uso.</span><span class="sxs-lookup"><span data-stu-id="931ed-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Parametri del modulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="931ed-333">Nella figura precedente, viene mostrato come immettere il percorso BLOB di input.</span><span class="sxs-lookup"><span data-stu-id="931ed-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="931ed-334">Questo percorso include i dati riservati per la compilazione delle tabelle di conteggio.</span><span class="sxs-lookup"><span data-stu-id="931ed-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="931ed-335">Dopo l'esecuzione di questo modulo, è possibile salvare la trasformazione per un uso successivo facendo clic con il pulsante destro del mouse sul modulo e scegliendo l'opzione **Save as Transform** (Salva come trasformazione):</span><span class="sxs-lookup"><span data-stu-id="931ed-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![Opzione "Save as Transform" (Salva come trasformazione)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="931ed-337">Nell'architettura dell'esperimento precedente, il set di dati "ytransform2" corrisponde esattamente a una trasformazione conteggio salvata.</span><span class="sxs-lookup"><span data-stu-id="931ed-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="931ed-338">Nella parte restante di questo esperimento, si presume che il lettore abbia usato un modulo **Build Counting Transform** su alcuni dati per generare i conteggi e possa quindi usare tali conteggi per generare le funzioni di conteggio nei set di dati di training e di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="931ed-339">Scelta delle funzioni di conteggio da includere nei set di dati di training e di test</span><span class="sxs-lookup"><span data-stu-id="931ed-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="931ed-340">Una volta disponibile una trasformazione conteggio, l'utente può scegliere quali funzioni includere nei set di dati di training e di test usando il modulo **Modify Count Table Parameters** .</span><span class="sxs-lookup"><span data-stu-id="931ed-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="931ed-341">Questo modulo viene illustrato qui per completezza, ma per semplicità non viene effettivamente usato nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="931ed-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modulo Modify Count Table Parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="931ed-343">In questo caso, come si può osservare, si è scelto di usare solo i log-odds e di ignorare la colonna backoff.</span><span class="sxs-lookup"><span data-stu-id="931ed-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="931ed-344">Si possono anche impostare parametri come la soglia cestino, il numero di pseudo esempi precedenti da aggiungere per lo smoothing (attenuazione) e se usare o meno la scala laplaciana del rumore.</span><span class="sxs-lookup"><span data-stu-id="931ed-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="931ed-345">Sono tutte funzioni avanzate e si deve osservare che i valori predefiniti sono un valido punto di partenza per gli utenti con poca familiarità con questo tipo di generazione di funzioni.</span><span class="sxs-lookup"><span data-stu-id="931ed-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="931ed-346">Trasformazione dei data prima di generare le funzioni conteggio</span><span class="sxs-lookup"><span data-stu-id="931ed-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="931ed-347">Ora verrà illustrata una fase importante della trasformazione dei dati di training e di test prima della generazione effettiva delle funzioni conteggio.</span><span class="sxs-lookup"><span data-stu-id="931ed-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="931ed-348">Si noti che vengono usati due moduli **Execute R Script** prima di applicare la trasformazione conteggio ai dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Moduli Execute R Script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="931ed-350">Ecco il primo script R:</span><span class="sxs-lookup"><span data-stu-id="931ed-350">Here is the first R script:</span></span>

![Primo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="931ed-352">In questo script R, si rinominano le colonne con nomi da "Col1" a "Col40".</span><span class="sxs-lookup"><span data-stu-id="931ed-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="931ed-353">Infatti i nomi devono avere questo formato nella trasformazione conteggio.</span><span class="sxs-lookup"><span data-stu-id="931ed-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="931ed-354">Nel secondo script R, si bilancia la distribuzione tra classi positive e negative, rispettivamente le classi 1 e 0, sottocampionando la classe negativa.</span><span class="sxs-lookup"><span data-stu-id="931ed-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="931ed-355">Lo script R seguente mostra come eseguire questa operazione:</span><span class="sxs-lookup"><span data-stu-id="931ed-355">The R script here shows how to do this:</span></span>

![Secondo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="931ed-357">In questo semplice script R si usa "pos\_neg\_ratio" per impostare la quantità di bilanciamento tra le classi positiva e negativa.</span><span class="sxs-lookup"><span data-stu-id="931ed-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="931ed-358">Questo è importante perché, riducendo lo sbilanciamento delle classi, si ottengono di solito vantaggi a livello delle prestazioni per i problemi di classificazione in cui la distribuzione delle classi è asimmetrica. Si ricordi che in questo caso la classe positiva è pari al 3,3% e la classe negativa al 96,7%.</span><span class="sxs-lookup"><span data-stu-id="931ed-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="931ed-359">Applicazione della trasformazione conteggio ai dati</span><span class="sxs-lookup"><span data-stu-id="931ed-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="931ed-360">Infine, si può usare il modulo **Apply Transformation** (Applica trasformazione) per applicare le trasformazioni conteggio ai set di dati di training e di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="931ed-361">Questo modulo accetta la trasformazione conteggio salvata come input e i set di dati di training o di test come secondo input e restituisce i dati con le funzioni conteggio,</span><span class="sxs-lookup"><span data-stu-id="931ed-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="931ed-362">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-362">It is shown here:</span></span>

![Modulo Apply Transformation](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="931ed-364">Estratto delle funzioni conteggio</span><span class="sxs-lookup"><span data-stu-id="931ed-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="931ed-365">È interessante osservare come appaiono le funzioni conteggio in questo caso.</span><span class="sxs-lookup"><span data-stu-id="931ed-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="931ed-366">Eccone un estratto:</span><span class="sxs-lookup"><span data-stu-id="931ed-366">Here we show an excerpt of this:</span></span>

![Funzioni di conteggio](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="931ed-368">In questo estratto, si nota che, per le colonne usate per i conteggi, si ottengono i conteggi e i log-odds oltre ai backoff pertinenti.</span><span class="sxs-lookup"><span data-stu-id="931ed-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="931ed-369">Ora si può compilare un modello di Azure Machine Learning usando questi set di dati trasformati.</span><span class="sxs-lookup"><span data-stu-id="931ed-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="931ed-370">Nella sezione successiva viene illustrato come effettuare questa operazione.</span><span class="sxs-lookup"><span data-stu-id="931ed-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="931ed-371"><a name="step3"></a>Passaggio 3: Compilare, eseguire il training e assegnare un punteggio al modello</span><span class="sxs-lookup"><span data-stu-id="931ed-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="931ed-372">Scelta dello strumento di apprendimento</span><span class="sxs-lookup"><span data-stu-id="931ed-372">Choice of learner</span></span>
<span data-ttu-id="931ed-373">Prima di tutto è necessario scegliere uno strumento di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="931ed-373">First, we need to choose a learner.</span></span> <span data-ttu-id="931ed-374">Verrà usato un albero delle decisioni con boosting a due classi.</span><span class="sxs-lookup"><span data-stu-id="931ed-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="931ed-375">Ecco le opzioni predefinite per questo strumento di apprendimento:</span><span class="sxs-lookup"><span data-stu-id="931ed-375">Here are the default options for this learner:</span></span>

![Parametri del modulo Two-Class Boosted Decision Tree](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="931ed-377">Per l'esperimento verranno scelti i valori predefiniti.</span><span class="sxs-lookup"><span data-stu-id="931ed-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="931ed-378">I valori predefiniti sono in genere significativi e consentono di ottenere previsioni rapide sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="931ed-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="931ed-379">È possibile migliorare le prestazioni con lo sweep dei parametri, una volta che si dispone di una previsione.</span><span class="sxs-lookup"><span data-stu-id="931ed-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="931ed-380">Eseguire il training del modello</span><span class="sxs-lookup"><span data-stu-id="931ed-380">Train the model</span></span>
<span data-ttu-id="931ed-381">Per il training, è sufficiente richiamare un modulo **Train Model** (Modello di training).</span><span class="sxs-lookup"><span data-stu-id="931ed-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="931ed-382">I due input sono lo strumento di apprendimento Two-Class Boosted Decision Tree e il set di dati di training,</span><span class="sxs-lookup"><span data-stu-id="931ed-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="931ed-383">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-383">This is shown here:</span></span>

![Modulo Train Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="931ed-385">Assegnare un punteggio al modello</span><span class="sxs-lookup"><span data-stu-id="931ed-385">Score the model</span></span>
<span data-ttu-id="931ed-386">Una volta disponibile un modello con training, è possibile assegnare un punteggio al set di dati di test e valutarne le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="931ed-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="931ed-387">A questo scopo, usare il modulo **Score Model** (Modello di punteggio) illustrato nella figura seguente, insieme a un modulo **Evaluate Model** (Modello di valutazione):</span><span class="sxs-lookup"><span data-stu-id="931ed-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![Modulo Score Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="931ed-389"><a name="step4"></a> Passaggio 4: Valutare il modello</span><span class="sxs-lookup"><span data-stu-id="931ed-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="931ed-390">Infine, si vogliono analizzare le prestazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="931ed-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="931ed-391">In genere, per i problemi di classificazione a due classi (binaria), un buon metodo di misurazione è costituito dall'area sottesa alla curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="931ed-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="931ed-392">Per visualizzare quest'area, è necessario collegare il modulo **Score Model** a un modulo **Evaluate Model**.</span><span class="sxs-lookup"><span data-stu-id="931ed-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="931ed-393">Fare clic su **Visualize** (Visualizza) nel modulo **Evaluate Model** per visualizzare un grafico simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Modulo di valutazione del modello per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="931ed-395">Per i problemi di classificazione binaria (o a due classi), un buon metodo di misurazione dell'accuratezza della stima è costituito dall'area sottesa alla curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="931ed-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="931ed-396">Di seguito sono illustrati i risultati dell'uso del modello sul set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="931ed-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="931ed-397">Per ottenere i risultati, fare clic con il pulsante destro del mouse sulla porta di output del modulo **Evaluate Model** e quindi fare clic su **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="931ed-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Visualizzazione del modulo Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="931ed-399"><a name="step5"></a> Passaggio 5: Pubblicare il modello come servizio Web</span><span class="sxs-lookup"><span data-stu-id="931ed-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="931ed-400">Per rendere disponibile su larga scala un modello di Azure Machine Learning, è possibile pubblicarlo come servizio Web in modo molto semplice.</span><span class="sxs-lookup"><span data-stu-id="931ed-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="931ed-401">Una volta fatto, chiunque può eseguire chiamate al servizio Web con i dati di input per cui è necessario ottenere delle stime e il servizio Web usa il modello per restituire tali stime.</span><span class="sxs-lookup"><span data-stu-id="931ed-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="931ed-402">A tale scopo, è innanzitutto necessario salvare il modello sottoposto a training come oggetto Trained Model.</span><span class="sxs-lookup"><span data-stu-id="931ed-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="931ed-403">Fare clic con il pulsante destro del mouse su **Train Model** e scegliere **Save as Trained Model** (Salva come modello sottoposto a training).</span><span class="sxs-lookup"><span data-stu-id="931ed-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="931ed-404">Successivamente, è necessario creare le porte di input e di output per il servizio Web:</span><span class="sxs-lookup"><span data-stu-id="931ed-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="931ed-405">una porta di input accetta i dati nello stesso formato dei dati per cui sono necessarie le stime</span><span class="sxs-lookup"><span data-stu-id="931ed-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="931ed-406">una porta di output restituisce le etichette con punteggi e le probabilità associate.</span><span class="sxs-lookup"><span data-stu-id="931ed-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="931ed-407">Selezionare alcune righe di dati per la porta di input</span><span class="sxs-lookup"><span data-stu-id="931ed-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="931ed-408">Per praticità, è possibile usare un modulo **Apply SQL Transformation** per selezionare solo 10 righe come dati della porta di input.</span><span class="sxs-lookup"><span data-stu-id="931ed-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="931ed-409">Selezionare solo queste righe di dati per la porta di input usando la query SQL visualizzata qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Dati porta di input](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="931ed-411">Servizio Web</span><span class="sxs-lookup"><span data-stu-id="931ed-411">Web service</span></span>
<span data-ttu-id="931ed-412">È ora possibile eseguire un piccolo esperimento che può essere usato per pubblicare il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="931ed-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="931ed-413">Generare i dati di input per il servizio Web</span><span class="sxs-lookup"><span data-stu-id="931ed-413">Generate input data for webservice</span></span>
<span data-ttu-id="931ed-414">Come passaggio iniziale, poiché la tabella di conteggio è grande, vengono prese poche righe di dati di test e da esse vengono generati i dati di output con le caratteristiche di conteggio.</span><span class="sxs-lookup"><span data-stu-id="931ed-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="931ed-415">Questo può essere il formato dei dati di input per il servizio Web,</span><span class="sxs-lookup"><span data-stu-id="931ed-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="931ed-416">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-416">This is shown here:</span></span>

![Creazione dati di input per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="931ed-418">Per il formato dati di input, viene ora usato l'OUTPUT del modulo **Count Featurizer** (Creazione funzionalità da conteggi).</span><span class="sxs-lookup"><span data-stu-id="931ed-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="931ed-419">Una volta terminata l'esecuzione dell'esperimento, salvare l'output del modulo **Count Featurizer** come set di dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="931ed-420">Il set di dati viene usato per i dati di input nel servizio Web.</span><span class="sxs-lookup"><span data-stu-id="931ed-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="931ed-421">Esperimento di assegnazione dei punteggi per la pubblicazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="931ed-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="931ed-422">Innanzitutto, viene illustrato l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="931ed-422">First, we show what this looks like.</span></span> <span data-ttu-id="931ed-423">La struttura essenziale è un modulo **Score Model** che accetta l'oggetto modello sottoposto a training e poche righe di dati di input generate nei passaggi precedenti usando il modulo **Count Featurizer** (Creazione funzionalità da conteggi).</span><span class="sxs-lookup"><span data-stu-id="931ed-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="931ed-424">Viene usato il modulo "Select Columns in Dataset" per ottenere le etichette con i punteggi e le probabilità di stima.</span><span class="sxs-lookup"><span data-stu-id="931ed-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Select Columns in Dataset](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="931ed-426">Si noti che modo è possibile utilizzare il modulo **Select Columns in Dataset** per filtrare i dati da escludere da un set di dati.</span><span class="sxs-lookup"><span data-stu-id="931ed-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="931ed-427">Il contenuto è illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-427">We show the contents here:</span></span>

![Applicazione di filtri con il modulo Select Columns in Dataset](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="931ed-429">Per ottenere le porte di input e di output indicate in blu, è sufficiente fare clic su **prepare webservice** in basso a destra.</span><span class="sxs-lookup"><span data-stu-id="931ed-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="931ed-430">L'esecuzione di questo esperimento consente anche di pubblicare il servizio Web facendo clic sull'icona **PUBLISH WEB SERVICE** (PUBBLICA SERVIZIO WEB) in basso a destra, illustrata qui:</span><span class="sxs-lookup"><span data-stu-id="931ed-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![PUBLISH WEB SERVICE](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="931ed-432">Dopo la pubblicazione del servizio Web, si viene reindirizzati a una pagina simile alla seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Dashboard del servizio Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="931ed-434">A sinistra sono presenti due collegamenti per i servizi Web:</span><span class="sxs-lookup"><span data-stu-id="931ed-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="931ed-435">Il collegamento **REQUEST/RESPONSE** (o RRS) serve per le stime singole e viene usato in questo workshop.</span><span class="sxs-lookup"><span data-stu-id="931ed-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="931ed-436">Il collegamento **BATCH EXECUTION** (BES) viene usato per le stime in batch e richiede che i dati di input usati per effettuare le stime si trovino in un archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="931ed-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="931ed-437">Facendo clic sul collegamento **REQUEST/RESPONSE** (RICHIESTA/RISPOSTA) viene visualizzata una pagina che fornisce codice predefinito in C#, Python ed R. Questo codice può essere usato in modo semplice per effettuare chiamate al servizio Web.</span><span class="sxs-lookup"><span data-stu-id="931ed-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="931ed-438">Si noti che la chiave API in questa pagina deve essere usata per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="931ed-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="931ed-439">È consigliabile copiare questo codice Python in una nuova cella di IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="931ed-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="931ed-440">Ecco un segmento di codice Python con la chiave API corretta.</span><span class="sxs-lookup"><span data-stu-id="931ed-440">Here we show a segment of python code with the correct API key.</span></span>

![Codice Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="931ed-442">Si noti che la chiave API predefinita è stata sostituita con la chiave API del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="931ed-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="931ed-443">Facendo clic su **Run** in questa cella di IPython Notebook, viene generata la risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="931ed-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![Risposta IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="931ed-445">Si noti che per i due esempi di test chiesti (nel framework JSON dello script Python) si ottengono le risposte nel formato "Scored Labels, Scored Probabilities".</span><span class="sxs-lookup"><span data-stu-id="931ed-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="931ed-446">In questo caso, sono stati scelti i valori predefiniti forniti dal codice predefinito (0 per tutte le colonne numeriche e la stringa "value" per tutte le colonne categoriche).</span><span class="sxs-lookup"><span data-stu-id="931ed-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="931ed-447">Con questa osservazione si conclude la procedura dettagliata end-to-end che mostra come gestire set di dati di grandi dimensioni con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="931ed-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="931ed-448">Partendo da un terabyte di dati, è stato creato un modello di previsione che è stato quindi distribuito come servizio Web nel cloud.</span><span class="sxs-lookup"><span data-stu-id="931ed-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

