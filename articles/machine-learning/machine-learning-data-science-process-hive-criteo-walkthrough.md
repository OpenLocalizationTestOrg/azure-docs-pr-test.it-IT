---
title: Processo di analisi scientifica dei dati di Team Ciao azione - utilizzando un Cluster di Azure HDInsight Hadoop in un set di dati di 1 TB | Documenti Microsoft
description: Utilizzando hello Team processo di analisi scientifica dei dati per uno scenario end-to-end che utilizza un HDInsight Hadoop toobuild del cluster e distribuire un modello usando un set di dati disponibili pubblicamente (1 TB) grandi dimensioni
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
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="524a1-103">Processo di analisi scientifica dei dati di Team Ciao azione - utilizzando un Cluster di Azure HDInsight Hadoop in un set di dati di 1 TB</span><span class="sxs-lookup"><span data-stu-id="524a1-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="524a1-104">In questa procedura dettagliata viene descritto come usare hello Team processo di analisi scientifica dei dati in uno scenario end-to-end con un [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, esplorare, funzionalità tecnico e verso il basso di dati di esempio da uno dei hello pubblicamente disponibile [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) set di dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="524a1-105">Utilizziamo Azure Machine Learning toobuild un modello di classificazione binaria per i dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="524a1-106">Vengono inoltre illustrati come toopublish uno di questi modelli come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="524a1-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="524a1-107">È inoltre possibile toouse un'attività di hello IPython notebook tooaccomplish presentati in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="524a1-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="524a1-108">Gli utenti che sarebbero ad esempio tootry deve consultare questo approccio hello [procedura dettagliata Criteo utilizzando una connessione ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) argomento.</span><span class="sxs-lookup"><span data-stu-id="524a1-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="524a1-109"><a name="dataset"></a>Descrizione del set di dati Criteo</span><span class="sxs-lookup"><span data-stu-id="524a1-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="524a1-110">Hello Criteo dati sono un set di stima fare clic su dati che è di circa 370GB dei file TSV compresso gzip (~1.3TB non compressi), che comprendono più 4.3 miliardi di record.</span><span class="sxs-lookup"><span data-stu-id="524a1-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="524a1-111">I valori sono ottenuti da 24 giorni di dati sui clic resi disponibili da [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="524a1-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="524a1-112">Per praticità hello di esperti di dati, è stato decompresso dati tooexperiment toous disponibile con.</span><span class="sxs-lookup"><span data-stu-id="524a1-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="524a1-113">Ogni record nel set di dati contiene 40 colonne:</span><span class="sxs-lookup"><span data-stu-id="524a1-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="524a1-114">Hello prima colonna è una colonna di etichetta che indica se un utente fa clic su un **aggiungere** (valore 1) o non fare clic su uno (valore 0)</span><span class="sxs-lookup"><span data-stu-id="524a1-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="524a1-115">le successive 13 colonne sono di tipo numerico</span><span class="sxs-lookup"><span data-stu-id="524a1-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="524a1-116">le ultime 26 colonne sono di tipo categorico</span><span class="sxs-lookup"><span data-stu-id="524a1-116">last 26 are categorical columns</span></span>

<span data-ttu-id="524a1-117">colonne di Hello sono rese anonime e utilizzare una serie di nomi enumerati: "Col1" (per la colonna di etichetta hello) troppo ' Col40 "(per la colonna categorica ultimo hello).</span><span class="sxs-lookup"><span data-stu-id="524a1-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="524a1-118">Di seguito è un estratto di hello innanzitutto 20 colonne di due osservazioni (righe) da questo set di dati:</span><span class="sxs-lookup"><span data-stu-id="524a1-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="524a1-119">Sono presenti valori mancanti in entrambe le colonne numeriche e categorico hello in questo set di dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="524a1-120">Viene descritto un metodo semplice per la gestione dei valori mancanti hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="524a1-121">Dettagli aggiuntivi su dati hello vengono esaminati quando è archiviarli in tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="524a1-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="524a1-122">**Definizione di:** *frequenza click-through (CTRL):* è hello percentuale di clic nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="524a1-123">In questo set di dati, Criteo hello CTR è circa 3.3% o 0.033.</span><span class="sxs-lookup"><span data-stu-id="524a1-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="524a1-124"><a name="mltasks"></a>Esempi di attività di stima</span><span class="sxs-lookup"><span data-stu-id="524a1-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="524a1-125">Questa procedura dettagliata illustra due problemi di stima di esempio:</span><span class="sxs-lookup"><span data-stu-id="524a1-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="524a1-126">**Classificazione binaria**: stima se un utente ha fatto clic su un annuncio:</span><span class="sxs-lookup"><span data-stu-id="524a1-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="524a1-127">Classe 0: nessun clic</span><span class="sxs-lookup"><span data-stu-id="524a1-127">Class 0: No Click</span></span>
   * <span data-ttu-id="524a1-128">Classe 1: clic</span><span class="sxs-lookup"><span data-stu-id="524a1-128">Class 1: Click</span></span>
2. <span data-ttu-id="524a1-129">**Regressione**: stima delle probabilità hello un fare clic su Active Directory dalla funzionalità dell'utente.</span><span class="sxs-lookup"><span data-stu-id="524a1-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="524a1-130"><a name="setup"></a>Configurare un cluster Hadoop di HDInsight per l'analisi scientifica</span><span class="sxs-lookup"><span data-stu-id="524a1-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="524a1-131">**Nota:** in genere, questa attività viene svolta da un **amministratore**.</span><span class="sxs-lookup"><span data-stu-id="524a1-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="524a1-132">Per configurare l'ambiente di analisi scientifica dei dati di Azure per la creazione di soluzioni di analisi predittiva con i cluster HDInsight, sono necessari tre passaggi:</span><span class="sxs-lookup"><span data-stu-id="524a1-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="524a1-133">[Creare un account di archiviazione](../storage/common/storage-create-storage-account.md): questo account di archiviazione è toostore utilizzati dati nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="524a1-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="524a1-134">Hello utilizzato nel cluster HDInsight vengono archiviati qui.</span><span class="sxs-lookup"><span data-stu-id="524a1-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="524a1-135">[Personalizzare i cluster Hadoop di Azure HDInsight per l'analisi scientifica dei dati](machine-learning-data-science-customize-hadoop-cluster.md): questo passaggio consente di creare un cluster Hadoop di Azure HDInsight con la versione a 64 bit di Anaconda Python 2.7 installata in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="524a1-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="524a1-136">Esistono due toocomplete passaggi importanti (descritti in questo argomento) per la personalizzazione del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="524a1-137">È necessario collegare l'account di archiviazione hello creato nel passaggio 1 con il cluster HDInsight quando viene creato.</span><span class="sxs-lookup"><span data-stu-id="524a1-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="524a1-138">Questo account di archiviazione viene utilizzato per accedere ai dati che possono essere elaborati all'interno di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="524a1-139">È necessario abilitare nodo head toohello di accesso remoto del cluster hello dopo averlo creato.</span><span class="sxs-lookup"><span data-stu-id="524a1-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="524a1-140">Memorizza le credenziali di accesso remoto hello è possibile specificare (diverse da quelle specificate per il cluster hello al momento della relativa creazione): sono necessari toocomplete hello procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="524a1-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="524a1-141">[Creare un'area di lavoro di Azure ML](machine-learning-create-workspace.md): area di lavoro questo Azure Machine Learning è utilizzata per la creazione di modelli di machine learning dopo un'esplorazione dei dati iniziali e campionamento nel cluster HDInsight hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="524a1-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="524a1-142"><a name="getdata"></a>Ottenere e utilizzare i dati da un'origine pubblica</span><span class="sxs-lookup"><span data-stu-id="524a1-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="524a1-143">Hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) set di dati è possibile accedere facendo clic sul collegamento hello, accettazione hello condizioni d'uso e fornire un nome.</span><span class="sxs-lookup"><span data-stu-id="524a1-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="524a1-144">Ecco uno snapshot di come appare:</span><span class="sxs-lookup"><span data-stu-id="524a1-144">A snapshot of what this looks like is shown here:</span></span>

![Accettazione delle condizioni Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="524a1-146">Fare clic su **continua tooDownload** tooread informazioni sul set di dati hello e la relativa disponibilità.</span><span class="sxs-lookup"><span data-stu-id="524a1-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="524a1-147">Hello dati risiedono in un pubblico [archiviazione blob di Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) percorso: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="524a1-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="524a1-148">"wasb" Hello fa riferimento il percorso di archiviazione Blob di tooAzure.</span><span class="sxs-lookup"><span data-stu-id="524a1-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="524a1-149">dati Hello in questa risorsa di archiviazione blob pubblico è costituito da tre sottocartelle della cartella dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="524a1-150">Hello sottocartella *non elaborati/count/* contiene hello prima 21 giorni di dati, dal giorno\_tooday 00\_20</span><span class="sxs-lookup"><span data-stu-id="524a1-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="524a1-151">Hello sottocartella *non elaborati/train/* è costituito da un solo giorno della data, giorno\_21</span><span class="sxs-lookup"><span data-stu-id="524a1-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="524a1-152">Hello sottocartella *non elaborati/test/* è costituito da due giorni di dati, giorno\_22 e giorno\_23</span><span class="sxs-lookup"><span data-stu-id="524a1-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="524a1-153">Per gli utenti che desiderano toostart con dati non elaborati gzip hello, questi sono anche disponibili nella cartella principale hello *non elaborati /* come day_NN.gz, in cui NN va da too23 00.</span><span class="sxs-lookup"><span data-stu-id="524a1-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="524a1-154">Tooaccess un approccio alternativo, esplorare e modellare i dati che non richiedono alcun download locale è illustrato più avanti in questa procedura dettagliata, quando si creano tabelle Hive.</span><span class="sxs-lookup"><span data-stu-id="524a1-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="524a1-155"><a name="login"></a>Accedere al nodo head del cluster toohello</span><span class="sxs-lookup"><span data-stu-id="524a1-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="524a1-156">nel nodo head toohello hello del cluster di, utilizzare hello toolog [portale di Azure](https://ms.portal.azure.com) cluster hello toolocate.</span><span class="sxs-lookup"><span data-stu-id="524a1-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="524a1-157">Fare clic sull'icona di elephant HDInsight hello in hello a sinistra e quindi fare doppio clic sul nome di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="524a1-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="524a1-158">Passare toohello **configurazione** scheda, fare doppio clic sull'icona CONNETTI hello nella parte inferiore di hello della pagina hello e immettere le credenziali di accesso remoto quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="524a1-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="524a1-159">Consente di procedere toohello nodo head del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="524a1-160">Ecco come appare un tipico primo log nel nodo head del cluster toohello:</span><span class="sxs-lookup"><span data-stu-id="524a1-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Accedi toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="524a1-162">A sinistra di hello, vediamo hello "Hadoop riga di comando", ovvero il componente di base per l'esplorazione dei dati di hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="524a1-163">Sono inoltre disponibili due utili URL, "Hadoop Yarn Status" e "Hadoop Name Node".</span><span class="sxs-lookup"><span data-stu-id="524a1-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="524a1-164">URL di Hello yarn stato Mostra lo stato del processo e l'URL del nodo nome hello fornisce informazioni dettagliate sulla configurazione del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="524a1-165">Ora è vengono impostate e pronto toobegin prima parte della procedura dettagliata hello: l'esplorazione dei dati utilizzando Hive e recupero di dati pronti per Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="524a1-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="524a1-166"><a name="hive-db-tables"></a> Creare il database e le tabelle Hive</span><span class="sxs-lookup"><span data-stu-id="524a1-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="524a1-167">toocreate Hive tabelle per il set di dati Criteo, aprire hello ***della riga di comando Hadoop*** hello desktop del nodo head hello e immettere una directory di Hive hello immettendo il comando hello</span><span class="sxs-lookup"><span data-stu-id="524a1-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="524a1-168">Eseguire tutti i comandi di Hive in questa procedura dettagliata da bin Hive hello / prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="524a1-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="524a1-169">In questo modo, eventuali problemi di percorso vengono risolti automaticamente.</span><span class="sxs-lookup"><span data-stu-id="524a1-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="524a1-170">Vengono utilizzati termini hello "Hive prompt dei comandi", "bin Hive / prompt dei comandi", "riga di comando Hadoop" e in modo intercambiabile.</span><span class="sxs-lookup"><span data-stu-id="524a1-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="524a1-171">tooexecute qualsiasi query Hive, è possibile utilizzare sempre hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="524a1-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="524a1-172">Dopo aver hello REPL Hive viene visualizzato con una "hive >" firmare, tagliare e incollare tooexecute query hello è.</span><span class="sxs-lookup"><span data-stu-id="524a1-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="524a1-173">Hello codice seguente viene creato un database "criteo" e quindi genera l'errore 4 tabelle:</span><span class="sxs-lookup"><span data-stu-id="524a1-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="524a1-174">un *tabella per la generazione di conteggi* compilato giorno giorni\_tooday 00\_20,</span><span class="sxs-lookup"><span data-stu-id="524a1-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="524a1-175">un *tabella per l'utilizzo come set di dati di training hello* compilato giorno\_21, e</span><span class="sxs-lookup"><span data-stu-id="524a1-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="524a1-176">due *set di dati di test di tabelle per l'utilizzo come hello* compilato giorno\_22 e giorno\_23 rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="524a1-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="524a1-177">Il set di dati di test verranno suddivise in due tabelle diverse perché uno dei giorni hello è un giorno festivo e vogliamo toodetermine se il modello di hello in grado di rilevare le differenze tra un giorno festivo e lavorativi dalla frequenza di hello click-through.</span><span class="sxs-lookup"><span data-stu-id="524a1-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="524a1-178">Hello script [hive esempio &#95; &#95; creare &#95; criteo &#95; database &#95; e &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) viene visualizzato di seguito per praticità:</span><span class="sxs-lookup"><span data-stu-id="524a1-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="524a1-179">È possibile notare che tutte queste tabelle sono esterne come abbiamo punto tooAzure semplicemente i percorsi di archiviazione Blob (wasb).</span><span class="sxs-lookup"><span data-stu-id="524a1-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="524a1-180">**Esistono due modi tooexecute Hive qualsiasi query che è importante tenere presente questo punto.**</span><span class="sxs-lookup"><span data-stu-id="524a1-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="524a1-181">**Utilizzo di hello Hive REPL della riga di comando**: hello prima di tutto è tooissue un comando "hive" e copiare e incollare una query alla hello Hive REPL della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="524a1-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="524a1-182">toodo questo, eseguire:</span><span class="sxs-lookup"><span data-stu-id="524a1-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="524a1-183">Ora in hello REPL della riga di comando, tagliare e incollare la query hello viene eseguito.</span><span class="sxs-lookup"><span data-stu-id="524a1-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="524a1-184">**Salvare una query tooa file ed eseguendo il comando di hello**: hello è secondo file di toosave hello query tooa .hql ([hive esempio &#95; &#95; creare &#95; criteo &#95; database &#95; e &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) e quindi segue hello problema comando query hello tooexecute:</span><span class="sxs-lookup"><span data-stu-id="524a1-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="524a1-185">Verificare la creazione del database e della tabella</span><span class="sxs-lookup"><span data-stu-id="524a1-185">Confirm database and table creation</span></span>
<span data-ttu-id="524a1-186">Successivamente, si conferma hello creazione database hello con hello comando seguente da bin Hive hello / prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="524a1-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="524a1-187">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="524a1-188">Questo errore conferma la creazione di hello del nuovo database hello, "criteo".</span><span class="sxs-lookup"><span data-stu-id="524a1-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="524a1-189">toosee le tabelle create, è sufficiente eseguire hello comando qui dal bin Hive hello / prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="524a1-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="524a1-190">Verrà quindi visualizzato hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="524a1-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="524a1-191"><a name="exploration"></a> Esplorazione dei dati in Hive</span><span class="sxs-lookup"><span data-stu-id="524a1-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="524a1-192">È ora pronto toodo alcune attività di esplorazione di dati di base nell'Hive.</span><span class="sxs-lookup"><span data-stu-id="524a1-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="524a1-193">È iniziare contando il numero di hello di esempi di training hello e tabelle di dati di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="524a1-194">Numero di esempi di training</span><span class="sxs-lookup"><span data-stu-id="524a1-194">Number of train examples</span></span>
<span data-ttu-id="524a1-195">contenuto di Hello [esempio &#95; hive &#95; conteggio &#95; train &#95; tabella &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) riportati di seguito:</span><span class="sxs-lookup"><span data-stu-id="524a1-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="524a1-196">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="524a1-197">In alternativa, uno può anche rilasciare hello comando seguente da bin Hive hello / prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="524a1-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="524a1-198">Numero di esempi di test nei set di dati di hello due test</span><span class="sxs-lookup"><span data-stu-id="524a1-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="524a1-199">È ora possibile contare il numero di hello di esempi in hello due set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="524a1-200">contenuto di Hello [esempio &#95; hive &#95; conteggio &#95; criteo &#95; test &#95; giorno &#95; 22 &#95; tabella &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) in questa sezione sono:</span><span class="sxs-lookup"><span data-stu-id="524a1-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="524a1-201">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="524a1-202">Come al solito, si potrebbe chiamare script hello da bin Hive hello / directory prompt dei comandi eseguendo il comando hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="524a1-203">Infine, verrà esaminato il numero di hello degli esempi di test nel set di dati di test hello in base a giorno\_23.</span><span class="sxs-lookup"><span data-stu-id="524a1-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="524a1-204">Hello toodo comando tratta toohello simile uno riportata solo (vedere troppo[esempio &#95; hive &#95; conteggio &#95; criteo &#95; test &#95; giorno &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="524a1-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="524a1-205">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="524a1-206">Etichetta distribuzione hello training set di dati</span><span class="sxs-lookup"><span data-stu-id="524a1-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="524a1-207">distribuzione di etichetta Hello hello training set di dati è di particolare interesse.</span><span class="sxs-lookup"><span data-stu-id="524a1-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="524a1-208">toosee, si visualizza contenuto [esempio &#95; hive &#95; criteo &#95; etichetta &#95; distribuzione &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="524a1-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="524a1-209">Ciò produce una distribuzione etichetta hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="524a1-210">Si noti che la percentuale hello delle etichette positivo 3.3% circa (coerente con set di dati originale hello).</span><span class="sxs-lookup"><span data-stu-id="524a1-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="524a1-211">Le distribuzioni di istogramma di alcune variabili numeriche in hello training set di dati</span><span class="sxs-lookup"><span data-stu-id="524a1-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="524a1-212">È possibile utilizzare nativo Hive "istogramma\_numerico" funzione toofind out è simile a quali distribuzione hello di variabili numeriche hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="524a1-213">Di seguito sono contenuti hello di [esempio &#95; hive &#95; criteo &#95; istogramma &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="524a1-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="524a1-214">In tal modo si ottiene seguente hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-214">This yields hello following:</span></span>

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

<span data-ttu-id="524a1-215">Hello laterale visualizzazione: esplosione di combinazione di Hive funge da tooproduce un output simile a SQL anziché elenco normale hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="524a1-216">Si noti che in hello questa tabella, la prima colonna hello corrisponde toohello bin center e hello secondo toohello bin frequenza.</span><span class="sxs-lookup"><span data-stu-id="524a1-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="524a1-217">Set di dati di training percentili approssimativi di alcune variabili numeriche in hello</span><span class="sxs-lookup"><span data-stu-id="524a1-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="524a1-218">È inoltre calcolo hello di percentili approssimativi di interesse con variabili numeriche.</span><span class="sxs-lookup"><span data-stu-id="524a1-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="524a1-219">A tale scopo, è disponibile la funzione "percentile\_approx" nativa di Hive.</span><span class="sxs-lookup"><span data-stu-id="524a1-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="524a1-220">contenuto di Hello [esempio &#95; hive &#95; criteo &#95; approssimativo &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) sono:</span><span class="sxs-lookup"><span data-stu-id="524a1-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="524a1-221">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="524a1-222">Abbiamo commento che la distribuzione di hello del percentili è in genere toohello strettamente correlati istogramma distribuzione di qualsiasi variabile numerica.</span><span class="sxs-lookup"><span data-stu-id="524a1-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="524a1-223">Trovare il numero di valori univoci per alcune colonne categoriche in hello training set di dati</span><span class="sxs-lookup"><span data-stu-id="524a1-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="524a1-224">Continuare l'esplorazione dei dati hello, sono ora disponibili, per alcune colonne di categoria, il numero di hello di valori univoci che accettano.</span><span class="sxs-lookup"><span data-stu-id="524a1-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="524a1-225">toodo, si visualizza contenuto [esempio &#95; hive &#95; criteo &#95; univoco &#95; valori &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="524a1-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="524a1-226">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="524a1-227">Si noti che Col15 ha 19 milioni di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="524a1-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="524a1-228">Utilizzando le tecniche di naïve come "hot una codifica" tooencode tali variabili di categoria elevata dimensionalità non è applicabile.</span><span class="sxs-lookup"><span data-stu-id="524a1-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="524a1-229">In particolare, viene spiegata e illustrata una tecnica avanzata e affidabile di [apprendimento in base ai conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) per affrontare il problema in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="524a1-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="524a1-230">Questa sottosezione è terminare analizzando hello numero di valori univoci per alcune altre colonne categoriche anche.</span><span class="sxs-lookup"><span data-stu-id="524a1-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="524a1-231">Hello contenuto di [esempio &#95; hive &#95; criteo &#95; univoco &#95; valori &#95; più &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) sono:</span><span class="sxs-lookup"><span data-stu-id="524a1-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="524a1-232">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="524a1-233">Nuovo vediamo che ad eccezione di Col20, tutti hello altre colonne hanno molti valori univoci.</span><span class="sxs-lookup"><span data-stu-id="524a1-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="524a1-234">Conteggi di CO-occorrenza delle coppie di variabili di categoria nelle hello training set di dati</span><span class="sxs-lookup"><span data-stu-id="524a1-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="524a1-235">conteggi di CO-occorrenza Hello delle coppie di variabili di categoria è anche di interesse.</span><span class="sxs-lookup"><span data-stu-id="524a1-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="524a1-236">Ciò può essere determinato mediante il codice hello in [esempio &#95; hive &#95; criteo &#95; abbinata &#95; categorico &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="524a1-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="524a1-237">Abbiamo invertire l'ordine hello conteggi da tali eventi ed esaminare in questo caso superiore hello 15.</span><span class="sxs-lookup"><span data-stu-id="524a1-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="524a1-238">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-238">This gives us:</span></span>

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

## <span data-ttu-id="524a1-239"><a name="downsample"></a>Verso il basso il set di dati di esempio hello per Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="524a1-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="524a1-240">Con i set di dati di consentirne hello e illustrato come è possibile eseguire questo tipo di esplorazione per eventuali variabili (incluse le combinazioni), è ora verso il basso il set di dati di esempio hello in modo che è possibile compilare modelli in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="524a1-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="524a1-241">Tenere presente è il problema di hello ci concentreremo invece sui: dato un set di attributi di esempio (i valori delle funzionalità da Col2 - Col40), è stimare se Col1 è 0 (nessun clic) o 1 (fare clic).</span><span class="sxs-lookup"><span data-stu-id="524a1-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="524a1-242">toodown campionare il training e di test % too1 set di dati della dimensione originale hello, utilizziamo funzione RAND () nativa Hive.</span><span class="sxs-lookup"><span data-stu-id="524a1-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="524a1-243">passare allo script successivo, Hello [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) esegue questa operazione per hello training set di dati:</span><span class="sxs-lookup"><span data-stu-id="524a1-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="524a1-244">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="524a1-245">Hello script [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; test &#95; giorno &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) non è per i dati di test, giorno\_22:</span><span class="sxs-lookup"><span data-stu-id="524a1-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="524a1-246">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="524a1-247">Infine, hello script [esempio &#95; hive &#95; criteo &#95; sottocampionamento &#95; test &#95; giorno &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) non è per i dati di test, giorno\_23:</span><span class="sxs-lookup"><span data-stu-id="524a1-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="524a1-248">Il risultato è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="524a1-249">Con questo siamo toouse pronto campionato il nostro giù eseguire il training e set di dati per la creazione di modelli in Azure Machine Learning di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="524a1-250">È un componente importante finale prima di proseguire tooAzure Machine Learning, che è una tabella di conteggio hello problemi.</span><span class="sxs-lookup"><span data-stu-id="524a1-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="524a1-251">Nella sottosezione successiva hello, questa operazione, illustrati in maggior dettaglio.</span><span class="sxs-lookup"><span data-stu-id="524a1-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="524a1-252"><a name="count"></a>Una breve descrizione nella tabella di conteggio hello</span><span class="sxs-lookup"><span data-stu-id="524a1-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="524a1-253">Come è stato visto, diverse variabili categoriche hanno una dimensionalità molto elevata.</span><span class="sxs-lookup"><span data-stu-id="524a1-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="524a1-254">In questa procedura dettagliata, è presente una tecnica potente denominata [Learning con conteggi](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode queste variabili in modo efficiente e affidabile.</span><span class="sxs-lookup"><span data-stu-id="524a1-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="524a1-255">Ulteriori informazioni su questa tecnica sono hello collegamento fornito.</span><span class="sxs-lookup"><span data-stu-id="524a1-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="524a1-256">In questa procedura dettagliata, esaminato l'utilizzo di rappresentazioni compact tooproduce tabelle di conteggio di funzioni categoriche elevata dimensionalità.</span><span class="sxs-lookup"><span data-stu-id="524a1-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="524a1-257">Non si tratta hello solo modo tooencode funzioni categoriche; Per ulteriori informazioni sulle tecniche di altri utenti interessati possono estrarre [uno-a caldo-encoding](http://en.wikipedia.org/wiki/One-hot) e [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="524a1-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="524a1-258">tabelle di conteggio toobuild sui dati di conteggio hello, utilizziamo dati hello hello raw/numero di cartelle.</span><span class="sxs-lookup"><span data-stu-id="524a1-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="524a1-259">Nella sezione di modellazione illustrare agli utenti di hello come toobuild queste funzioni conteggiano tabelle per le funzionalità categoriche da zero o, in alternativa, toouse una tabella di conteggio preesistente per le esplorazioni.</span><span class="sxs-lookup"><span data-stu-id="524a1-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="524a1-260">In cosa indicato di seguito, quando si fa riferimento troppo "pre-creato le tabelle di conteggio", si intende l'utilizzo di tabelle di conteggio hello fornito da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="524a1-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="524a1-261">Istruzioni dettagliate su come tooaccess queste tabelle vengono fornite nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="524a1-262"><a name="aml"></a> Creare un modello con Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="524a1-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="524a1-263">Il processo di creazione di un modello in Azure Machine Learning prevede i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="524a1-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="524a1-264">Ottenere dati hello dalle tabelle di Hive in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="524a1-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="524a1-265">Creare l'esperimento hello: pulire dati hello e trasformare con le tabelle di conteggio</span><span class="sxs-lookup"><span data-stu-id="524a1-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="524a1-266">Compilazione, eseguire il training e il modello di punteggio hello</span><span class="sxs-lookup"><span data-stu-id="524a1-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="524a1-267">Valutazione del modello di hello</span><span class="sxs-lookup"><span data-stu-id="524a1-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="524a1-268">Pubblicare il modello di hello come un servizio web</span><span class="sxs-lookup"><span data-stu-id="524a1-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="524a1-269">Ora siamo modelli toobuild pronto in Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="524a1-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="524a1-270">I dati campionati verso il basso viene salvati come tabelle Hive nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="524a1-271">Utilizziamo hello Azure Machine Learning **l'importazione dei dati** modulo tooread questi dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="524a1-272">Hello credenziali tooaccess hello account di archiviazione del cluster, vedere di seguito.</span><span class="sxs-lookup"><span data-stu-id="524a1-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="524a1-273"><a name="step1"></a>Passaggio 1: Ottenere dati da tabelle Hive in Azure Machine Learning usando il modulo di importazione dei dati hello e selezionarla per un esperimento di machine learning</span><span class="sxs-lookup"><span data-stu-id="524a1-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="524a1-274">Per iniziare, selezionare **+NEW** -> **EXPERIMENT** -> **Blank Experiment** (+NUOVO -> ESPERIMENTO -> Esperimento vuoto).</span><span class="sxs-lookup"><span data-stu-id="524a1-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="524a1-275">Quindi, dalla hello **ricerca** casella hello in alto a sinistra, cercare "Importazione di dati".</span><span class="sxs-lookup"><span data-stu-id="524a1-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="524a1-276">Trascinamento della selezione hello **l'importazione dei dati** modulo nel modulo toohello esperimento canvas (hello parte centrale di schermata Ciao) toouse hello per accedere ai dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="524a1-277">Si tratta di quali hello **l'importazione dei dati** aspetto durante il recupero di dati dalla tabella Hive hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Acquisizione di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="524a1-279">Per hello **l'importazione dei dati** modulo, i valori hello di parametro hello viene forniti in hello grafico sono soli alcuni esempi di hello sorta di valori è necessario tooprovide.</span><span class="sxs-lookup"><span data-stu-id="524a1-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="524a1-280">Ecco alcune linee guida generali sulla configurazione per hello toofill parametro hello out **l'importazione dei dati** modulo.</span><span class="sxs-lookup"><span data-stu-id="524a1-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="524a1-281">In **Data Source**</span><span class="sxs-lookup"><span data-stu-id="524a1-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="524a1-282">In hello **query database Hive** casella, un'istruzione SELECT semplice * FROM < il\_database\_name.your\_tabella\_nome >-è sufficiente.</span><span class="sxs-lookup"><span data-stu-id="524a1-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="524a1-283">**Hcatalog server URI** (URI del server Hcatalog): se il cluster è "abc", specificare semplicemente https://abc.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="524a1-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="524a1-284">**Nome dell'account utente Hadoop**: nome utente hello scelta in fase di hello entrata cluster hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="524a1-285">(Non hello accesso remoto nome utente!)</span><span class="sxs-lookup"><span data-stu-id="524a1-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="524a1-286">**Password dell'account utente Hadoop**: hello password hello utente al momento di hello entrata cluster hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="524a1-287">(Non hello password di accesso remoto!)</span><span class="sxs-lookup"><span data-stu-id="524a1-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="524a1-288">**Location of output data**: scegliere "Azure".</span><span class="sxs-lookup"><span data-stu-id="524a1-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="524a1-289">**Nome dell'account di archiviazione Azure**: hello account di archiviazione associato hello cluster</span><span class="sxs-lookup"><span data-stu-id="524a1-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="524a1-290">**Chiave dell'account di archiviazione di Azure**: chiave hello hello dell'account di archiviazione associato hello cluster.</span><span class="sxs-lookup"><span data-stu-id="524a1-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="524a1-291">**Nome del contenitore di Azure**: se il nome del cluster hello è "abc", quindi viene semplicemente "abc", in genere.</span><span class="sxs-lookup"><span data-stu-id="524a1-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="524a1-292">Una volta hello **l'importazione dei dati** al termine dell'acquisizione di dati (segno di spunta verde hello vedere nel modulo hello), salvare i dati come set di dati (con un nome di propria scelta).</span><span class="sxs-lookup"><span data-stu-id="524a1-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="524a1-293">L'aspetto è il seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-293">What this looks like:</span></span>

![Salvataggio di dati con Import Data](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="524a1-295">Porta di hello di output di hello rapida **l'importazione dei dati** modulo.</span><span class="sxs-lookup"><span data-stu-id="524a1-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="524a1-296">Verranno visualizzate le opzioni **Save as dataset** (Salva come set di dati) e **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="524a1-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="524a1-297">Hello **Visualizza** opzione, se selezionato, consente di visualizzare 100 righe di dati di hello, insieme a un pannello destro che è utile per alcune statistiche di riepilogo.</span><span class="sxs-lookup"><span data-stu-id="524a1-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="524a1-298">toosave dati, selezionare semplicemente **salvare come set di dati** e seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="524a1-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="524a1-299">il set di dati di tooselect hello salvato per l'utilizzo in un esperimento di apprendimento macchina, individuare hello DataSet utilizzando hello **ricerca** dialogo illustrata nella seguente illustrazione hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="524a1-300">Quindi è sufficiente specificare il nome assegnato al hello hello set di dati parzialmente tooaccess e trascinare hello set di dati in hello pannello principale.</span><span class="sxs-lookup"><span data-stu-id="524a1-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="524a1-301">Il trascinamento nella finestra Pannello principale hello viene selezionata per la modellazione di machine learning.</span><span class="sxs-lookup"><span data-stu-id="524a1-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Set di dati del trascinamento nel pannello principale hello](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="524a1-303">Eseguire questa operazione per eseguire il training hello e hello test set di dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="524a1-304">Ricordare inoltre il nome di database toouse hello e i nomi di tabella assegnato a questo scopo.</span><span class="sxs-lookup"><span data-stu-id="524a1-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="524a1-305">i valori Hello utilizzati nella figura hello sono esclusivamente per figura purposes.* *</span><span class="sxs-lookup"><span data-stu-id="524a1-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="524a1-306"><a name="step2"></a>Passaggio 2: Creare un semplice esperimento in Azure Machine Learning toopredict clic / non fa clic su</span><span class="sxs-lookup"><span data-stu-id="524a1-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="524a1-307">L'esperimento di Azure ML è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-307">Our Azure ML experiment looks like this:</span></span>

![Esperimento di Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="524a1-309">È ora possibile esaminare i componenti chiave hello di questo esperimento.</span><span class="sxs-lookup"><span data-stu-id="524a1-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="524a1-310">Come promemoria, dobbiamo toodrag nostri salvata di eseguire il training e di testare i set di dati nell'area di disegno esperimento tooour prima.</span><span class="sxs-lookup"><span data-stu-id="524a1-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="524a1-311">Pulire i dati mancanti</span><span class="sxs-lookup"><span data-stu-id="524a1-311">Clean Missing Data</span></span>
<span data-ttu-id="524a1-312">Hello **Clean Missing Data** modulo cosa suggerisce il nome: vengono puliti i dati mancanti in modi che possono essere specificate dall'utente.</span><span class="sxs-lookup"><span data-stu-id="524a1-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="524a1-313">Analizzando il modulo, è possibile vedere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="524a1-313">Looking into this module, we see this:</span></span>

![Pulire i dati mancanti](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="524a1-315">In questo caso, è stato scelto tooreplace tutti i valori mancanti con il valore 0.</span><span class="sxs-lookup"><span data-stu-id="524a1-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="524a1-316">Sono disponibili anche altre opzioni che possono essere visualizzati esaminando hello elenchi a discesa nel modulo hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="524a1-317">Progettazione di funzionalità sui dati hello</span><span class="sxs-lookup"><span data-stu-id="524a1-317">Feature engineering on hello data</span></span>
<span data-ttu-id="524a1-318">Per alcune funzioni categoriche di set di dati di grandi dimensioni possono esistere milioni di valori univoci.</span><span class="sxs-lookup"><span data-stu-id="524a1-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="524a1-319">Non è possibile usare metodi di base come la codifica one-hot per rappresentare funzioni categoriche con dimensionalità così elevata.</span><span class="sxs-lookup"><span data-stu-id="524a1-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="524a1-320">In questa procedura dettagliata viene illustrato come le funzioni di conteggio toouse usando incorporato toogenerate moduli di Azure Machine Learning compact rappresentazioni di queste variabili categoriche elevata dimensionalità.</span><span class="sxs-lookup"><span data-stu-id="524a1-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="524a1-321">Hello risultato finale è un piccolo modello, tempi di training e metriche delle prestazioni sono molto simili toousing altre tecniche.</span><span class="sxs-lookup"><span data-stu-id="524a1-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="524a1-322">Compilazione di trasformazioni conteggio</span><span class="sxs-lookup"><span data-stu-id="524a1-322">Building counting transforms</span></span>
<span data-ttu-id="524a1-323">funzionalità di conteggio toobuild, utilizziamo hello **compilare conteggio trasformare** modulo che è disponibile in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="524a1-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="524a1-324">modulo Hello è simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="524a1-324">hello module looks like this:</span></span>

<span data-ttu-id="524a1-325">![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Modulo Build Counting Transform](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="524a1-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="524a1-326">In hello **Conteggio colonne** casella, si immette le colonne che si desidera che il conteggio di tooperform.</span><span class="sxs-lookup"><span data-stu-id="524a1-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="524a1-327">Come indicato in precedenza, si tratta in genere di colonne categoriche con dimensionalità elevata.</span><span class="sxs-lookup"><span data-stu-id="524a1-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="524a1-328">All'avvio di hello, abbiamo detto set di dati Criteo hello è 26 colonne categoriche: da Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="524a1-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="524a1-329">In questo caso, si contare su tutti gli elementi e i relativi indici (da 15 too40 separati da virgole, come illustrato).</span><span class="sxs-lookup"><span data-stu-id="524a1-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="524a1-330">modulo hello toouse hello modalità MapReduce (appropriata per grandi set di dati), si base accesso cluster HDInsight Hadoop tooan (quello utilizzato per l'esplorazione delle funzionalità possa essere riutilizzato per questo scopo, nonché Buongiorno) e le relative credenziali.</span><span class="sxs-lookup"><span data-stu-id="524a1-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="524a1-331">figure precedenti Hello illustrano quali hello riempita valori aspetto (sostituire i valori hello forniti a scopo illustrativo con quelli appropriati per il propria caso di utilizzo).</span><span class="sxs-lookup"><span data-stu-id="524a1-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Parametri del modulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="524a1-333">In hello nella figura riportata sopra viene illustrato come tooenter hello input blob percorso.</span><span class="sxs-lookup"><span data-stu-id="524a1-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="524a1-334">Questa posizione è riservati per la creazione di tabelle di conteggio dati di hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="524a1-335">Al termine dell'esecuzione questo modulo, è possibile salvare in un secondo momento trasformazione hello per facendo modulo hello hello **salvare come trasformazione** opzione:</span><span class="sxs-lookup"><span data-stu-id="524a1-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Opzione "Save as Transform" (Salva come trasformazione)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="524a1-337">Nell'architettura esperimento illustrato in precedenza, set di dati hello "ytransform2" corrisponde esattamente tooa salvato trasformazione conteggio.</span><span class="sxs-lookup"><span data-stu-id="524a1-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="524a1-338">Resto hello di questo esperimento, si presuppone che lettore hello usato un **compilare conteggio trasformare** modulo alcuni dati toogenerate conteggi e possono quindi utilizzare tali funzioni di conteggio toogenerate conteggi su train hello e set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="524a1-339">Scelta di quali conteggio tooinclude funzionalità come parte del training hello e set di dati di test</span><span class="sxs-lookup"><span data-stu-id="524a1-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="524a1-340">Una volta che un numero di trasformare pronto, utente hello è possibile scegliere quali tooinclude funzionalità nella loro train e test set di dati tramite hello **modificare i parametri di tabella conteggio** modulo.</span><span class="sxs-lookup"><span data-stu-id="524a1-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="524a1-341">Questo modulo viene illustrato qui per completezza, ma per semplicità non viene effettivamente usato nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="524a1-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![Modulo Modify Count Table Parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="524a1-343">In questo caso, come si può notare, abbiamo scelto toouse hello solo log-odds e tooignore hello spostare la colonna.</span><span class="sxs-lookup"><span data-stu-id="524a1-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="524a1-344">È anche possibile impostare i parametri, ad esempio hello soglia Cestino, quanti tooadd pseudo-precedente esempi per l'arrotondamento, e se toouse qualsiasi Laplaciana del rumore o non.</span><span class="sxs-lookup"><span data-stu-id="524a1-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="524a1-345">Tutte queste funzionalità sono avanzate e risulta toobe notare che i valori predefiniti di hello rappresentano un buon punto di partenza per gli utenti che sono di nuovo tipo toothis della generazione di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="524a1-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="524a1-346">Trasformazione dei dati prima di generare le funzionalità di conteggio hello</span><span class="sxs-lookup"><span data-stu-id="524a1-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="524a1-347">È ora concentrarsi su un punto importante sulla trasformazione il training e test tooactually di dati precedente la generazione di funzioni di conteggio.</span><span class="sxs-lookup"><span data-stu-id="524a1-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="524a1-348">Si noti che sono disponibili due **Execute R Script** moduli utilizzati prima che si applicano hello conteggio trasformazione tooour dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Moduli Execute R Script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="524a1-350">Ecco lo script R prima hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-350">Here is hello first R script:</span></span>

![Primo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="524a1-352">In questo script R, rinominare il nostro toonames colonne "Col1" troppo "Col40".</span><span class="sxs-lookup"><span data-stu-id="524a1-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="524a1-353">Questo avviene perché hello conteggio trasformazione prevede che i nomi di questo formato.</span><span class="sxs-lookup"><span data-stu-id="524a1-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="524a1-354">Nel secondo script R di hello, abbiamo bilanciare distribuzione hello tra classi positive e negative (classi rispettivamente 1 e 0) dalla classe di sottocampionamento hello negativo.</span><span class="sxs-lookup"><span data-stu-id="524a1-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="524a1-355">Hello R script qui illustrato in che modo toodo questo:</span><span class="sxs-lookup"><span data-stu-id="524a1-355">hello R script here shows how toodo this:</span></span>

![Secondo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="524a1-357">In questo semplice script R, si usa "pos\_neg\_rapporto" quantità di hello tooset di equilibrio tra hello positivo e negativo classi di hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="524a1-358">Questo è importante toodo poiché miglioramento sbilanciamento di classe in genere presenta vantaggi di prestazioni per problemi di classificazione in cui la distribuzione di classe hello è sfasato (tenere presente che in questo caso, sono disponibili classi positivo 3.3% e % 96,7 negativo).</span><span class="sxs-lookup"><span data-stu-id="524a1-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="524a1-359">L'applicazione della trasformazione Conteggio hello sui nostri dati</span><span class="sxs-lookup"><span data-stu-id="524a1-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="524a1-360">Infine, è possibile utilizzare hello **Apply Transformation** tooapply modulo hello trasformazioni conteggio sul training e set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="524a1-361">Questo modulo accetta trasformazione Conteggio hello salvato come un input e hello training o il set di dati di test come hello altri tipi di input e restituisce i dati con le funzionalità di conteggio.</span><span class="sxs-lookup"><span data-stu-id="524a1-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="524a1-362">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="524a1-362">It is shown here:</span></span>

![Modulo Apply Transformation](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="524a1-364">Un estratto della funzionalità di conteggio hello aspetto</span><span class="sxs-lookup"><span data-stu-id="524a1-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="524a1-365">È utile toosee sulle funzionalità di conteggio hello simile in questo caso.</span><span class="sxs-lookup"><span data-stu-id="524a1-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="524a1-366">Eccone un estratto:</span><span class="sxs-lookup"><span data-stu-id="524a1-366">Here we show an excerpt of this:</span></span>

![Funzioni di conteggio](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="524a1-368">In questo estratto, verrà indicato che per le colonne hello conteggiati in totale, è ottenere il totale hello e Accedi disparità backoffs rilevanti tooany di addizione.</span><span class="sxs-lookup"><span data-stu-id="524a1-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="524a1-369">Ci sono ora pronti toobuild un modello di Azure Machine Learning usando questi set di dati trasformato.</span><span class="sxs-lookup"><span data-stu-id="524a1-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="524a1-370">Nella sezione successiva hello, ecco come questa operazione può essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="524a1-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="524a1-371"><a name="step3"></a>Passaggio 3: Compilazione, il training e assegnare un punteggio modello hello</span><span class="sxs-lookup"><span data-stu-id="524a1-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="524a1-372">Scelta dello strumento di apprendimento</span><span class="sxs-lookup"><span data-stu-id="524a1-372">Choice of learner</span></span>
<span data-ttu-id="524a1-373">Innanzitutto, è necessario toochoose uno strumento di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="524a1-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="524a1-374">È in corso toouse un albero delle decisioni con Boosting di due classi come questo strumento di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="524a1-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="524a1-375">Ecco le opzioni predefinite di hello per questo strumento di apprendimento:</span><span class="sxs-lookup"><span data-stu-id="524a1-375">Here are hello default options for this learner:</span></span>

![Parametri del modulo Two-Class Boosted Decision Tree](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="524a1-377">Per la sperimentazione, siamo i valori predefiniti di corso toochoose hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="524a1-378">È possibile notare che hello predefinite sono in genere significativo e un buon metodo tooget rapido le linee di base sulle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="524a1-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="524a1-379">È possibile migliorare sulle prestazioni da sweep di parametri se si sceglie tooonce che è una linea di base.</span><span class="sxs-lookup"><span data-stu-id="524a1-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="524a1-380">Modello di hello Train</span><span class="sxs-lookup"><span data-stu-id="524a1-380">Train hello model</span></span>
<span data-ttu-id="524a1-381">Per il training, è sufficiente richiamare un modulo **Train Model** (Modello di training).</span><span class="sxs-lookup"><span data-stu-id="524a1-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="524a1-382">Hello due input tooit sono dello strumento di apprendimento di hello Two-Class Boosted Decision Tree e il set di dati di training.</span><span class="sxs-lookup"><span data-stu-id="524a1-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="524a1-383">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="524a1-383">This is shown here:</span></span>

![Modulo Train Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="524a1-385">Modello di punteggio hello</span><span class="sxs-lookup"><span data-stu-id="524a1-385">Score hello model</span></span>
<span data-ttu-id="524a1-386">Dopo avere creato un modello con training, si è pronti tooscore su hello verifica set di dati e tooevaluate delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="524a1-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="524a1-387">Facciamo utilizzando hello **Score Model** modulo illustrato nella seguente illustrazione, insieme a hello un **Evaluate Model** modulo:</span><span class="sxs-lookup"><span data-stu-id="524a1-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![Modulo Score Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="524a1-389"><a name="step4"></a>Passaggio 4: Valutazione del modello di hello</span><span class="sxs-lookup"><span data-stu-id="524a1-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="524a1-390">Infine, desideriamo tooanalyze le prestazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="524a1-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="524a1-391">In genere, per due problemi di classificazione (binario) di classe, un'ottima misura è hello AUC.</span><span class="sxs-lookup"><span data-stu-id="524a1-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="524a1-392">toovisualize, abbiamo agganciare hello **Score Model** modulo tooan **Evaluate Model** modulo per questo oggetto.</span><span class="sxs-lookup"><span data-stu-id="524a1-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="524a1-393">Fare clic su **Visualizza** su hello **Evaluate Model** modulo produce un'immagine come segue quello hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Modulo di valutazione del modello per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="524a1-395">Nel file binario (o classe due) problemi di classificazione, un'ottima misura dell'accuratezza della stima è hello Area nella curva (AUC).</span><span class="sxs-lookup"><span data-stu-id="524a1-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="524a1-396">Di seguito sono illustrati i risultati dell'uso del modello sul set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="524a1-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="524a1-397">tooget, questa porta di output di hello rapida di hello **Evaluate Model** modulo e quindi **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="524a1-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Visualizzazione del modulo Evaluate Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="524a1-399"><a name="step5"></a>Passaggio 5: Pubblicare il modello di hello come un servizio Web</span><span class="sxs-lookup"><span data-stu-id="524a1-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="524a1-400">Hello possibilità toopublish un modello di Azure Machine Learning come servizi web con un minimo di confusione è una funzionalità utile per renderlo ampiamente disponibile.</span><span class="sxs-lookup"><span data-stu-id="524a1-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="524a1-401">Al termine dell'operazione, chiunque può creare chiamate toohello web servizio con dati di input che hanno bisogno di stime per e servizio web hello utilizza hello modello tooreturn tali stime.</span><span class="sxs-lookup"><span data-stu-id="524a1-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="524a1-402">toodo, è innanzitutto salvare il modello con training come un oggetto modello con training.</span><span class="sxs-lookup"><span data-stu-id="524a1-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="524a1-403">Questa operazione viene eseguita facendo clic su hello **Train Model** modulo e l'utilizzo di hello **Save as Trained Model** opzione.</span><span class="sxs-lookup"><span data-stu-id="524a1-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="524a1-404">È quindi necessario toocreate input e output porte per il servizio web:</span><span class="sxs-lookup"><span data-stu-id="524a1-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="524a1-405">Recupera i dati in hello stesso modulo come dati hello che si richiedono stime per una porta di input</span><span class="sxs-lookup"><span data-stu-id="524a1-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="524a1-406">una porta di output restituisce hello Scored Labels e le probabilità di hello associata.</span><span class="sxs-lookup"><span data-stu-id="524a1-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="524a1-407">Selezionare alcune righe di dati per la porta di input hello</span><span class="sxs-lookup"><span data-stu-id="524a1-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="524a1-408">È utile toouse un **Apply SQL Transformation** modulo tooselect solo 10 righe tooserve come hello specificati dati porta di input.</span><span class="sxs-lookup"><span data-stu-id="524a1-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="524a1-409">Selezionare solo le righe di dati per la porta di input tramite query SQL hello illustrata di seguito:</span><span class="sxs-lookup"><span data-stu-id="524a1-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Dati porta di input](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="524a1-411">Servizio Web</span><span class="sxs-lookup"><span data-stu-id="524a1-411">Web service</span></span>
<span data-ttu-id="524a1-412">Ora è pronto toorun un esperimento di piccole dimensioni che può essere utilizzati toopublish il servizio web.</span><span class="sxs-lookup"><span data-stu-id="524a1-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="524a1-413">Generare i dati di input per il servizio Web</span><span class="sxs-lookup"><span data-stu-id="524a1-413">Generate input data for webservice</span></span>
<span data-ttu-id="524a1-414">Come passaggio zero, poiché è grande, la tabella di conteggio hello è poche righe di dati di test e generare dati di output da esso con le funzionalità di conteggio.</span><span class="sxs-lookup"><span data-stu-id="524a1-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="524a1-415">Questo può essere usato come formato di dati di input hello per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="524a1-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="524a1-416">come illustrato qui:</span><span class="sxs-lookup"><span data-stu-id="524a1-416">This is shown here:</span></span>

![Creazione dati di input per l'albero delle decisioni con boosting](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="524a1-418">Per il formato di dati di input di hello, è possibile utilizzare l'OUTPUT di hello hello **Count Featurizer** modulo.</span><span class="sxs-lookup"><span data-stu-id="524a1-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="524a1-419">Dopo questo provare al termine dell'esecuzione, salvare l'output di hello da hello **Count Featurizer** modulo come un set di dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="524a1-420">Questo set di dati viene utilizzato per dati di input hello in webservice hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="524a1-421">Esperimento di assegnazione dei punteggi per la pubblicazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="524a1-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="524a1-422">Innanzitutto, viene illustrato l'aspetto.</span><span class="sxs-lookup"><span data-stu-id="524a1-422">First, we show what this looks like.</span></span> <span data-ttu-id="524a1-423">struttura essenziali Hello è un **Score Model** modulo che accetta l'oggetto modello sottoposto a training e alcune righe di dati di input generati in precedenza hello utilizzando hello **Count Featurizer** modulo.</span><span class="sxs-lookup"><span data-stu-id="524a1-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="524a1-424">Utilizziamo tooproject "Selezionare le colonne nel set di dati" hello Scored etichette e le probabilità di punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Select Columns in Dataset](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="524a1-426">Si noti come hello **selezionare le colonne nel set di dati** modulo può essere utilizzato per il 'filtro' dati da un set di dati.</span><span class="sxs-lookup"><span data-stu-id="524a1-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="524a1-427">Ecco contenuto hello qui:</span><span class="sxs-lookup"><span data-stu-id="524a1-427">We show hello contents here:</span></span>

![Applicazione di filtri con hello selezionare le colonne nel modulo di set di dati](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="524a1-429">porte di tooget hello blu di input e output, sufficiente fare clic su **preparare webservice** in basso a destra hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="524a1-430">Eseguendo questo esperimento consente inoltre di servizio web di hello toopublish: fare clic su hello **servizio WEB di pubblicare** icona qui destra, come illustrato nella parte inferiore di hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![PUBLISH WEB SERVICE](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="524a1-432">Dopo aver pubblicato webservice hello, si ottiene pagina tooa reindirizzato pertanto:</span><span class="sxs-lookup"><span data-stu-id="524a1-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Dashboard del servizio Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="524a1-434">Verrà visualizzato due collegamenti per i servizi Web sul lato sinistro hello:</span><span class="sxs-lookup"><span data-stu-id="524a1-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="524a1-435">Hello **richiesta/risposta** (o il servizio RR) è destinati a singole stime ed è ciò che si utilizzano per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="524a1-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="524a1-436">Hello **esecuzione BATCH** servizio (BES) viene utilizzato per le stime in batch e richiede che le stime toomake di dati di input utilizzati hello si trovino nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="524a1-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="524a1-437">Fare clic sul collegamento hello **richiesta/risposta** ci ha tooa pagina che consente di ottenere pre-predefinito codice c#, python e R. Questo codice può essere facilmente usato per effettuare chiamate toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="524a1-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="524a1-438">Si noti che la chiave API in questa pagina hello necessario toobe utilizzato per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="524a1-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="524a1-439">È utile toocopy questo python di codice su tooa nuova cella notebook IPython hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="524a1-440">Di seguito è illustrato un segmento di codice python con chiave API corretta hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-440">Here we show a segment of python code with hello correct API key.</span></span>

![Codice Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="524a1-442">Si noti che la chiave API predefinito hello pertanto abbiamo sostituito con la chiave API del nostro webservices.</span><span class="sxs-lookup"><span data-stu-id="524a1-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="524a1-443">Fare clic su **eseguire** su questa cella in un IPython notebook produce hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="524a1-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![Risposta IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="524a1-445">Vediamo che per hello due test esempi che abbiamo chiesto (nel framework JSON hello dello script python hello), otteniamo risposte in formato hello "Scored Labels, probabilità Scored".</span><span class="sxs-lookup"><span data-stu-id="524a1-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="524a1-446">Si noti che in questo caso, è stato scelto i valori predefiniti di hello che il codice predefinito hello fornisce (0 zero per tutte le colonne numeriche e stringa hello "value" per tutte le colonne categoriche).</span><span class="sxs-lookup"><span data-stu-id="524a1-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="524a1-447">Questa operazione conclude la procedura dettagliata end-to-end di mostrare come toohandle set di dati su larga scala con Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="524a1-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="524a1-448">Viene avviato con un terabyte di dati, costruito un modello di stima e distribuita come servizio web nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="524a1-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

