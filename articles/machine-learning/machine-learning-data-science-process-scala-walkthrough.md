---
title: aaaData scienza con Scala e Spark in Azure | Documenti Microsoft
description: "Come toouse Scala per supervisione di machine learning attività con hello Spark MLlib e Spark ML pacchetti scalabili in un cluster Azure HDInsight Spark."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="7a321-103">Analisi scientifica dei dati tramite Scala e Spark in Azure</span><span class="sxs-lookup"><span data-stu-id="7a321-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="7a321-104">Questo articolo illustra come toouse Scala per le attività di apprendimento supervisionato macchina con hello MLlib scalabile Spark e Spark ML pacchetti in un cluster Azure HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="7a321-105">Illustra le attività che costituiscono hello hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess): inserimento di dati e l'esplorazione, visualizzazione, progettazione di funzionalità, modellazione e il consumo di modello.</span><span class="sxs-lookup"><span data-stu-id="7a321-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="7a321-106">i modelli di Hello nell'articolo hello includono la regressione logistica e lineare, foreste casuali e alberi con Boosting sfumatura (GBTs), inoltre comune tootwo sotto la supervisione attività di machine learning:</span><span class="sxs-lookup"><span data-stu-id="7a321-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="7a321-107">Problema di regressione: stima della quantità di hello suggerimento ($) per un itinerario taxi</span><span class="sxs-lookup"><span data-stu-id="7a321-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="7a321-108">Classificazione binaria: stima di mancia o non mancia (1/0) per una corsa in taxi</span><span class="sxs-lookup"><span data-stu-id="7a321-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="7a321-109">processo di modellazione Hello richiede training e valutazione in un set di dati di test e la metrica di accuratezza pertinente.</span><span class="sxs-lookup"><span data-stu-id="7a321-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="7a321-110">In questo articolo, utili come toostore questi modelli in archiviazione Blob di Azure e come tooscore e valutare le prestazioni predittiva.</span><span class="sxs-lookup"><span data-stu-id="7a321-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="7a321-111">In questo articolo viene illustrata anche hello argomenti della modalità toooptimize modelli tramite la convalida incrociata e hyper-parameter sweep più avanzati.</span><span class="sxs-lookup"><span data-stu-id="7a321-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="7a321-112">dati Hello utilizzati sono un esempio di hello 2013 NYC taxi viaggi tariffa set di dati e disponibile in GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a321-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="7a321-113">[Scala](http://www.scala-lang.org/), un linguaggio basato su macchina virtuale Java hello integra concetti sul linguaggio funzionale e orientata agli oggetti.</span><span class="sxs-lookup"><span data-stu-id="7a321-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="7a321-114">È un linguaggio scalabile toodistributed adatta l'elaborazione nel cloud hello, che viene eseguito nei cluster Spark di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a321-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="7a321-115">[Spark](http://spark.apache.org/) è un framework di elaborazione parallela open source che supporta in memoria prestazioni di elaborazione tooboost hello delle applicazioni analitica dei dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="7a321-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="7a321-116">motore di elaborazione Spark Hello viene compilato per la velocità, semplicità di utilizzo e analitica sofisticate.</span><span class="sxs-lookup"><span data-stu-id="7a321-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="7a321-117">Le funzionalità di elaborazione distribuita in memoria rendono Spark uno strumento valido per l'esecuzione di algoritmi iterativi in calcoli grafici e di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7a321-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="7a321-118">Hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pacchetto fornisce un set di API di alto livello basate su dati frame che consentono di creare e ottimizzare pratiche di machine learning pipeline uniforme.</span><span class="sxs-lookup"><span data-stu-id="7a321-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="7a321-119">[MLlib](http://spark.apache.org/mllib/) è libreria di apprendimento scalabile di macchine di Spark, che offre funzionalità di modellazione toothis di ambiente distribuito.</span><span class="sxs-lookup"><span data-stu-id="7a321-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="7a321-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) è offerta ospitato da Azure hello di Spark open source.</span><span class="sxs-lookup"><span data-stu-id="7a321-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="7a321-121">Include inoltre il supporto per la Jupyter Scala notebook nel cluster Spark hello e può eseguire Spark SQL Query interattive tootransform, filtrare e visualizzare i dati archiviati nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a321-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="7a321-122">Hello Scala frammenti di codice in questo articolo che forniscono soluzioni hello e visualizzare grafici rilevanti hello dati hello toovisualize eseguiti in server Jupyter notebook installato nel cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="7a321-123">passaggi di modellazione Hello in questi argomenti contengono codice che mostra come tootrain, valutare, salvare e utilizzare ogni tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="7a321-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="7a321-124">passaggi di installazione Hello e il codice in questo articolo sono per Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="7a321-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="7a321-125">Tuttavia, hello codice in questo articolo e nel hello [Scala server Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) sono generici e dovrebbe funzionare in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="7a321-126">installazione del cluster di Hello e operazioni di gestione potrebbero essere leggermente diversi rispetto a quanto mostrato in questo articolo se non si utilizza HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="7a321-127">Per un argomento che illustra come toouse Python anziché Scala toocomplete attività per un processo di analisi scientifica dei dati end-to-end, vedere [analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a321-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="7a321-128">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7a321-128">Prerequisites</span></span>
* <span data-ttu-id="7a321-129">È necessario disporre di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a321-129">You must have an Azure subscription.</span></span> <span data-ttu-id="7a321-130">Se non è già disponibile, [ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7a321-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7a321-131">È necessario un hello di toocomplete cluster Azure HDInsight 3.4 Spark 1.6, seguire le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="7a321-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="7a321-132">toocreate un cluster, vedere le istruzioni di hello in [Introduzione: creare Apache Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7a321-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="7a321-133">Impostare il tipo di cluster hello e versione hello **Seleziona tipo di Cluster** menu.</span><span class="sxs-lookup"><span data-stu-id="7a321-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Configurazione del tipo di cluster HDInsight](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="7a321-135">Per una descrizione dei dati di andata e ritorno di hello NYC taxi e istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute, vedere le sezioni pertinenti hello in [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7a321-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="7a321-136">Eseguire il codice di Scala da un server Jupyter notebook nel cluster Spark hello</span><span class="sxs-lookup"><span data-stu-id="7a321-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="7a321-137">È possibile avviare un server Jupyter notebook da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a321-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="7a321-138">Trovare cluster Spark hello nel dashboard e quindi fare clic su, pagina di gestione di hello tooenter per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7a321-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="7a321-139">Successivamente, fare clic su **dashboard del Cluster**, quindi fare clic su **server Jupyter Notebook** notebook hello tooopen associato al cluster Spark hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Dashboard del cluster e notebook Jupyter](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="7a321-141">È anche possibile accedere ai notebook di Jupyter da https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="7a321-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="7a321-142">Sostituire *clustername* con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="7a321-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="7a321-143">È necessario password hello per amministratore account tooaccess hello Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="7a321-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Passare notebook tooJupyter utilizzando il nome del cluster hello](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="7a321-145">Selezionare **Scala** toosee una directory con alcuni esempi di predisporre notebook tale hello utilizzare API PySpark.</span><span class="sxs-lookup"><span data-stu-id="7a321-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="7a321-146">Hello modellazione di esplorazione e di punteggio usando notebook Scala.ipynb che contiene esempi di codice hello per questo gruppo di argomenti di Spark è disponibile in [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="7a321-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="7a321-147">È possibile caricare notebook hello direttamente da GitHub toohello server Jupyter Notebook nel cluster di Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="7a321-148">Nella home page Jupyter, fare clic su hello **caricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="7a321-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="7a321-149">In Esplora file hello incollare hello GitHub (contenuto non elaborato) URL di notebook Scala hello e quindi fare clic su **aprire**.</span><span class="sxs-lookup"><span data-stu-id="7a321-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="7a321-150">blocco appunti Scala Hello sono disponibile in hello URL seguente:</span><span class="sxs-lookup"><span data-stu-id="7a321-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="7a321-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="7a321-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="7a321-152">Installazione: contesti di Spark e Hive predefiniti, magic Spark e librerie Spark</span><span class="sxs-lookup"><span data-stu-id="7a321-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="7a321-153">Contesti predefiniti di Spark e Hive</span><span class="sxs-lookup"><span data-stu-id="7a321-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="7a321-154">kernel Spark Hello forniti con i notebook Jupyter sono preimpostati contesti.</span><span class="sxs-lookup"><span data-stu-id="7a321-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="7a321-155">Tooexplicitly set hello Spark Hive contesti o non è necessario prima di iniziare con un'applicazione hello che si sta sviluppando.</span><span class="sxs-lookup"><span data-stu-id="7a321-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="7a321-156">Hello contesti predefiniti sono:</span><span class="sxs-lookup"><span data-stu-id="7a321-156">hello preset contexts are:</span></span>

* <span data-ttu-id="7a321-157">`sc` per SparkContext</span><span class="sxs-lookup"><span data-stu-id="7a321-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="7a321-158">`sqlContext` per HiveContext</span><span class="sxs-lookup"><span data-stu-id="7a321-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="7a321-159">Magic di Spark</span><span class="sxs-lookup"><span data-stu-id="7a321-159">Spark magics</span></span>
<span data-ttu-id="7a321-160">Hello kernel Spark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con `%%`.</span><span class="sxs-lookup"><span data-stu-id="7a321-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="7a321-161">Due di questi comandi vengono utilizzati nei seguenti esempi di codice hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="7a321-162">`%%local`Specifica che il codice hello nelle righe successive verrà eseguito localmente.</span><span class="sxs-lookup"><span data-stu-id="7a321-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="7a321-163">codice Hello deve essere valido codice di Scala.</span><span class="sxs-lookup"><span data-stu-id="7a321-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="7a321-164">`%%sql -o <variable name>`: esegue una query Hive su `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="7a321-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="7a321-165">Se hello `-o` parametro viene passato, il risultato di hello di hello query è persistente nel hello `%%local` contesto Scala di un frame di dati di Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="7a321-166">Per ulteriori informazioni su kernel hello per server Jupyter notebook e i relativi predefiniti "magics" che è stata chiamata con `%%` (ad esempio, `%%local`), vedere [cluster kernel disponibile per i notebook Jupyter con HDInsight Spark Linux HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="7a321-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="7a321-167">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="7a321-167">Import libraries</span></span>
<span data-ttu-id="7a321-168">Importare hello Spark MLlib e altre librerie, occorre utilizzando hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="7a321-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a><span data-ttu-id="7a321-169">Inserimento di dati</span><span class="sxs-lookup"><span data-stu-id="7a321-169">Data ingestion</span></span>
<span data-ttu-id="7a321-170">Hello hello il processo di analisi scientifica dei dati è innanzitutto i dati di hello tooingest che si desidera tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="7a321-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="7a321-171">Hello dati trasferiti da origini esterne o sistemi in cui si trova nell'ambiente di esplorazione e modellazione di dati.</span><span class="sxs-lookup"><span data-stu-id="7a321-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="7a321-172">In questo articolo di inserimento dei dati di hello sono un esempio di 0,1% unita in join di hello taxi di andata e ritorno e tariffa file (archiviato come file tsv).</span><span class="sxs-lookup"><span data-stu-id="7a321-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="7a321-173">ambiente di esplorazione e modellazione di dati Hello è Spark.</span><span class="sxs-lookup"><span data-stu-id="7a321-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="7a321-174">In questa sezione contiene hello toocomplete di codice hello serie di attività:</span><span class="sxs-lookup"><span data-stu-id="7a321-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="7a321-175">Impostare i percorsi di directory per l'archiviazione di dati e modelli.</span><span class="sxs-lookup"><span data-stu-id="7a321-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="7a321-176">Lettura in hello set di dati input (archiviati come file tsv).</span><span class="sxs-lookup"><span data-stu-id="7a321-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="7a321-177">Definire uno schema di dati hello e hello pulita.</span><span class="sxs-lookup"><span data-stu-id="7a321-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="7a321-178">Creare un frame di dati puliti e memorizzarli nella cache.</span><span class="sxs-lookup"><span data-stu-id="7a321-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="7a321-179">Registrare dati hello come una tabella temporanea in SQLContext.</span><span class="sxs-lookup"><span data-stu-id="7a321-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="7a321-180">Una query sulla tabella hello e importare i risultati di hello in un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="7a321-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="7a321-181">Impostare percorsi di directory per i percorsi di archiviazione in archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="7a321-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="7a321-182">Spark possono leggere e scrivere tooAzure nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="7a321-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="7a321-183">È possibile utilizzare i dati esistenti tooprocess Spark e quindi archiviare nuovamente i risultati di hello nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="7a321-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="7a321-184">i modelli di toosave o file nell'archiviazione Blob, è necessario tooproperly specificare il percorso di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="7a321-185">Contenitore predefinito di hello riferimento collegato cluster Spark toohello utilizzando un percorso che inizia con `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="7a321-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="7a321-186">Fare riferimento ad altre posizioni usando `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="7a321-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="7a321-187">Hello nell'esempio di codice seguente specifica la posizione di hello di hello toobe di dati di input letti e hello percorso tooBlob spazio di archiviazione cluster Spark toohello collegati in cui verrà salvato il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="7a321-188">Importare i dati, creare un RDD e definire un frame di dati in base toohello schema</span><span class="sxs-lookup"><span data-stu-id="7a321-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-189">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-189">**Output:**</span></span>

<span data-ttu-id="7a321-190">Cella di tempo toorun hello: 8 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="7a321-191">Una query sulla tabella hello e importare i risultati in un frame di dati</span><span class="sxs-lookup"><span data-stu-id="7a321-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="7a321-192">Quindi, nella tabella query hello per tariffa passeggeri e il suggerimento dati. filtrare i dati danneggiati e americane; e stampa di più righe.</span><span class="sxs-lookup"><span data-stu-id="7a321-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="7a321-193">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-193">**Output:**</span></span>

| <span data-ttu-id="7a321-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="7a321-194">fare_amount</span></span> | <span data-ttu-id="7a321-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="7a321-195">passenger_count</span></span> | <span data-ttu-id="7a321-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="7a321-196">tip_amount</span></span> | <span data-ttu-id="7a321-197">tipped</span><span class="sxs-lookup"><span data-stu-id="7a321-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="7a321-198">13,5</span><span class="sxs-lookup"><span data-stu-id="7a321-198">13.5</span></span> |<span data-ttu-id="7a321-199">1.0</span><span class="sxs-lookup"><span data-stu-id="7a321-199">1.0</span></span> |<span data-ttu-id="7a321-200">2,9</span><span class="sxs-lookup"><span data-stu-id="7a321-200">2.9</span></span> |<span data-ttu-id="7a321-201">1.0</span><span class="sxs-lookup"><span data-stu-id="7a321-201">1.0</span></span> |
|        <span data-ttu-id="7a321-202">16,0</span><span class="sxs-lookup"><span data-stu-id="7a321-202">16.0</span></span> |<span data-ttu-id="7a321-203">2.0</span><span class="sxs-lookup"><span data-stu-id="7a321-203">2.0</span></span> |<span data-ttu-id="7a321-204">3.4</span><span class="sxs-lookup"><span data-stu-id="7a321-204">3.4</span></span> |<span data-ttu-id="7a321-205">1.0</span><span class="sxs-lookup"><span data-stu-id="7a321-205">1.0</span></span> |
|        <span data-ttu-id="7a321-206">10,5</span><span class="sxs-lookup"><span data-stu-id="7a321-206">10.5</span></span> |<span data-ttu-id="7a321-207">2.0</span><span class="sxs-lookup"><span data-stu-id="7a321-207">2.0</span></span> |<span data-ttu-id="7a321-208">1.0</span><span class="sxs-lookup"><span data-stu-id="7a321-208">1.0</span></span> |<span data-ttu-id="7a321-209">1.0</span><span class="sxs-lookup"><span data-stu-id="7a321-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="7a321-210">Visualizzazione ed esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="7a321-210">Data exploration and visualization</span></span>
<span data-ttu-id="7a321-211">Dopo aver portato dati hello in Spark, hello passaggio successivo per il processo di analisi scientifica dei dati hello è toogain una comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="7a321-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="7a321-212">In questa sezione è esaminare dati taxi hello tramite query SQL.</span><span class="sxs-lookup"><span data-stu-id="7a321-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="7a321-213">Quindi, Importa hello risultati in un tooplot frame di dati hello le variabili di destinazione e le funzionalità potenziali per l'esame visivo utilizzando hello auto-visualizzazione di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="7a321-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="7a321-214">Utilizzare locale e i dati di magic tooplot SQL</span><span class="sxs-lookup"><span data-stu-id="7a321-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="7a321-215">Per impostazione predefinita, è disponibile nel contesto di hello della sessione hello in modo permanente in nodi di lavoro hello output di hello di ogni frammento di codice da eseguire da un server Jupyter notebook.</span><span class="sxs-lookup"><span data-stu-id="7a321-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="7a321-216">Se si desidera toosave un nodi di lavoro di andata e ritorno toohello per ogni calcolo e, se tutti hello i dati necessari per il calcolo è disponibile in locale nel nodo del server Jupyter hello (ovvero nodo head hello), è possibile utilizzare hello `%%local` particolare codice hello toorun frammento di codice server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="7a321-217">**Magic SQL** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="7a321-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="7a321-218">Hello kernel HDInsight Spark supporta SQLContext query HiveQL facile inline.</span><span class="sxs-lookup"><span data-stu-id="7a321-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="7a321-219">Hello (`-o VARIABLE_NAME`) argomento persiste output di hello di query SQL hello come frame di dati Pandas server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="7a321-220">Ciò significa che sarà disponibile in modalità locale hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="7a321-221">`%%local` **magic**.</span><span class="sxs-lookup"><span data-stu-id="7a321-221">`%%local` **magic**.</span></span> <span data-ttu-id="7a321-222">Hello `%%local` magic esegue codice hello in locale nel server Jupyter hello hello nodo head del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="7a321-223">In genere, si utilizza `%%local` magic in combinazione con hello `%%sql` magic con hello `-o` parametro.</span><span class="sxs-lookup"><span data-stu-id="7a321-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="7a321-224">Hello `-o` parametro sarebbe mantenere l'output di hello di query SQL hello in locale, quindi `%%local` magic attiverà set successivo di hello di toorun frammento di codice in locale sull'output di hello delle query SQL hello in modo permanente in locale.</span><span class="sxs-lookup"><span data-stu-id="7a321-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="7a321-225">Eseguire query sui dati hello tramite SQL</span><span class="sxs-lookup"><span data-stu-id="7a321-225">Query hello data by using SQL</span></span>
<span data-ttu-id="7a321-226">Questa query recupera trip taxi hello tariffa quantità, conteggio passeggeri e quantità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="7a321-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="7a321-227">Nel seguente codice di hello, hello `%%local` magic crea un frame di dati locale, sqlResults.</span><span class="sxs-lookup"><span data-stu-id="7a321-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="7a321-228">È possibile utilizzare sqlResults tooplot usando matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7a321-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="7a321-229">Il magic local viene usato più volte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7a321-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="7a321-230">Se il set di dati è grande, per esempio toocreate un frame di dati che può adattarsi alla memoria locale.</span><span class="sxs-lookup"><span data-stu-id="7a321-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="7a321-231">Dati hello tracciato</span><span class="sxs-lookup"><span data-stu-id="7a321-231">Plot hello data</span></span>
<span data-ttu-id="7a321-232">È possibile tracciare utilizzando codice Python dopo il frame di dati hello è nel contesto locale come frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="7a321-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="7a321-233">kernel Spark Hello Visualizza automaticamente l'output di hello delle query SQL (HiveQL) dopo l'esecuzione di codice hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="7a321-234">È possibile scegliere tra diversi tipi di visualizzazioni:</span><span class="sxs-lookup"><span data-stu-id="7a321-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="7a321-235">Tabella</span><span class="sxs-lookup"><span data-stu-id="7a321-235">Table</span></span>
* <span data-ttu-id="7a321-236">Grafico a torta</span><span class="sxs-lookup"><span data-stu-id="7a321-236">Pie</span></span>
* <span data-ttu-id="7a321-237">Grafico a linee</span><span class="sxs-lookup"><span data-stu-id="7a321-237">Line</span></span>
* <span data-ttu-id="7a321-238">Area</span><span class="sxs-lookup"><span data-stu-id="7a321-238">Area</span></span>
* <span data-ttu-id="7a321-239">Grafico a barre</span><span class="sxs-lookup"><span data-stu-id="7a321-239">Bar</span></span>

<span data-ttu-id="7a321-240">Ecco i dati di hello tooplot codice hello:</span><span class="sxs-lookup"><span data-stu-id="7a321-240">Here's hello code tooplot hello data:</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


<span data-ttu-id="7a321-241">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-241">**Output:**</span></span>

![Istogramma degli importi delle mance](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="7a321-245">Creare le funzionalità e trasformare le funzionalità, quindi preparare i dati per l'input in funzioni di modellazione</span><span class="sxs-lookup"><span data-stu-id="7a321-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="7a321-246">Per le funzioni di modellazione basata sulla struttura ad albero da Spark ML e MLlib, è possibile tooprepare destinazione e le funzionalità usando varie tecniche, ad esempio binning, indicizzazione, hot una codifica e la vettorializzazione.</span><span class="sxs-lookup"><span data-stu-id="7a321-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="7a321-247">Di seguito sono toofollow procedure hello in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="7a321-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="7a321-248">Ottenere una nuova funzionalità dalla **creazione di contenitori** per gli orari di trasporto.</span><span class="sxs-lookup"><span data-stu-id="7a321-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="7a321-249">Applicare **l'indicizzazione e hot una codifica** toocategorical funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7a321-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="7a321-250">**Esempio e split hello set di dati** in frazioni di training e di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="7a321-251">**Specificare le funzionalità e la variabile di training**e creare RDD (resilient distributed dataset )o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.</span><span class="sxs-lookup"><span data-stu-id="7a321-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="7a321-252">Automaticamente **classificare e vettorizzare funzionalità e le destinazioni** toouse come input per i modelli di machine learning.</span><span class="sxs-lookup"><span data-stu-id="7a321-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="7a321-253">Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="7a321-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="7a321-254">Questo codice viene illustrato come una nuova funzionalità inserendo ore in fase di traffico toocreate bucket e come toocache hello risultante frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="7a321-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="7a321-255">In cui i frame RDDs e i dati vengono utilizzati più volte, la memorizzazione nella cache comporta tempi di esecuzione tooimproved.</span><span class="sxs-lookup"><span data-stu-id="7a321-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="7a321-256">Di conseguenza, si saranno memorizza nella cache di frame di dati e RDDs in fasi diverse dell'hello seguire le procedure seguenti.</span><span class="sxs-lookup"><span data-stu-id="7a321-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="7a321-257">Indicizzare e applicare la codifica one-hot per le funzionalità categoriche</span><span class="sxs-lookup"><span data-stu-id="7a321-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="7a321-258">modellazione Hello e funzioni di MLlib richiedono funzionalità con dati di input categorici toobe indicizzato o codificato toouse precedente di stima.</span><span class="sxs-lookup"><span data-stu-id="7a321-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="7a321-259">In questa sezione illustra come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione.</span><span class="sxs-lookup"><span data-stu-id="7a321-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="7a321-260">È necessario tooindex o codificare i modelli in modi diversi, a seconda del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="7a321-261">Ad esempio, i modelli di regressione logistica e lineare richiedono codifica one-hot.</span><span class="sxs-lookup"><span data-stu-id="7a321-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="7a321-262">Ad esempio, una funzionalità con tre categorie può essere espansa in tre colonne di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7a321-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="7a321-263">Ogni colonna contiene 0 o 1 a seconda della categoria di hello di un'osservazione.</span><span class="sxs-lookup"><span data-stu-id="7a321-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="7a321-264">MLlib fornisce hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione per la scelta di una codifica.</span><span class="sxs-lookup"><span data-stu-id="7a321-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="7a321-265">Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari con al massimo uno a valore singolo.</span><span class="sxs-lookup"><span data-stu-id="7a321-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="7a321-266">Con questa codifica, gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, possono essere applicato toocategorical funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7a321-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="7a321-267">Qui si trasforma esempi tooshow solo quattro variabili sono stringhe di caratteri.</span><span class="sxs-lookup"><span data-stu-id="7a321-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="7a321-268">È possibile indicizzare come variabili categoriche anche altre variabili, ad esempio il giorno della settimana, rappresentate da valori numerici.</span><span class="sxs-lookup"><span data-stu-id="7a321-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="7a321-269">Per l'indicizzazione usare la funzione `StringIndexer()` e per la codifica one-hot e le funzioni `OneHotEncoder()` di MLlib.</span><span class="sxs-lookup"><span data-stu-id="7a321-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="7a321-270">Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:</span><span class="sxs-lookup"><span data-stu-id="7a321-270">Here is hello code tooindex and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-271">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-271">**Output:**</span></span>

<span data-ttu-id="7a321-272">Cella di hello toorun ora: 4 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="7a321-273">Esempio e split hello set di dati in frazioni di training e di test</span><span class="sxs-lookup"><span data-stu-id="7a321-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="7a321-274">Questo codice crea un campionamento casuale dei dati hello (25%, in questo esempio).</span><span class="sxs-lookup"><span data-stu-id="7a321-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="7a321-275">Anche se il campionamento non è necessario per questo esempio a causa delle dimensioni toohello hello del set di dati, hello articolo illustra come è possibile campionare in modo da sapere come toouse per altri problemi quando necessario.</span><span class="sxs-lookup"><span data-stu-id="7a321-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="7a321-276">Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli.</span><span class="sxs-lookup"><span data-stu-id="7a321-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="7a321-277">Successivamente, suddividere l'esempio hello in una parte di training (75%, in questo esempio) e un test (25%, in questo esempio) toouse classificazione e la modellazione basata sulla parte.</span><span class="sxs-lookup"><span data-stu-id="7a321-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="7a321-278">Aggiungere una riga tooeach numero casuale (compreso tra 0 e 1) (in una colonna "rand") che può essere utilizzati tooselect convalida incrociata riduzioni durante il training.</span><span class="sxs-lookup"><span data-stu-id="7a321-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-279">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-279">**Output:**</span></span>

<span data-ttu-id="7a321-280">Cella di tempo toorun hello: 2 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="7a321-281">Specificare le funzionalità e la variabile di training e quindi creare RDD o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.</span><span class="sxs-lookup"><span data-stu-id="7a321-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="7a321-282">In questa sezione contiene codice che mostra come scegliere il tipo di dati, dati di testo categorico tooindex come un'etichetta e codificarli in modo è possibile utilizzare tootrain e test di regressione logistica MLlib e altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="7a321-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="7a321-283">Gli oggetti punto etichettato sono RDD formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di Machine Learning in MLlib.</span><span class="sxs-lookup"><span data-stu-id="7a321-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="7a321-284">Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.</span><span class="sxs-lookup"><span data-stu-id="7a321-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="7a321-285">In questo codice, specificare variabile (dipendente) di destinazione hello e hello funzionalità toouse tootrain modelli.</span><span class="sxs-lookup"><span data-stu-id="7a321-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="7a321-286">Creare quindi RDD o frame di dati con punti etichettati per training e test indicizzati o con codifica one-hot.</span><span class="sxs-lookup"><span data-stu-id="7a321-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-287">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-287">**Output:**</span></span>

<span data-ttu-id="7a321-288">Cella di hello toorun ora: 4 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="7a321-289">Classificare automaticamente e vettorizzare toouse funzionalità e le destinazioni come input per i modelli di machine learning</span><span class="sxs-lookup"><span data-stu-id="7a321-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="7a321-290">Usare Spark ML toocategorize hello destinazione e le funzionalità toouse nelle funzioni di modellazione basata sulla struttura ad albero.</span><span class="sxs-lookup"><span data-stu-id="7a321-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="7a321-291">codice Hello completa due attività:</span><span class="sxs-lookup"><span data-stu-id="7a321-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="7a321-292">Crea una destinazione per la classificazione binaria assegnando un valore pari a 0 o 1 punto dati tooeach compreso tra 0 e 1, utilizzando un valore di soglia di 0,5.</span><span class="sxs-lookup"><span data-stu-id="7a321-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="7a321-293">Classifica automaticamente le funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7a321-293">Automatically categorizes features.</span></span> <span data-ttu-id="7a321-294">Se il numero di hello di valori numerici distinti per tutte le funzionalità è minore di 32, tale funzionalità è stata categorizzata.</span><span class="sxs-lookup"><span data-stu-id="7a321-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="7a321-295">Ecco il codice hello per le attività.</span><span class="sxs-lookup"><span data-stu-id="7a321-295">Here's hello code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="7a321-296">Modello di classificazione binaria: prevede se deve essere lasciata una mancia</span><span class="sxs-lookup"><span data-stu-id="7a321-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="7a321-297">In questa sezione è creare tre tipi di toopredict di modelli di classificazione binaria o meno un suggerimento deve essere a pagamento:</span><span class="sxs-lookup"><span data-stu-id="7a321-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="7a321-298">Oggetto **modello di regressione logistica** utilizzando hello Spark ML `LogisticRegression()` (funzione)</span><span class="sxs-lookup"><span data-stu-id="7a321-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="7a321-299">Oggetto **il modello di classificazione di foresta casuale** utilizzando hello Spark ML `RandomForestClassifier()` (funzione)</span><span class="sxs-lookup"><span data-stu-id="7a321-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="7a321-300">A **sfumatura modello di classificazione albero boosting** utilizzando hello MLlib `GradientBoostedTrees()` (funzione)</span><span class="sxs-lookup"><span data-stu-id="7a321-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="7a321-301">Creare un modello di regressione logistica</span><span class="sxs-lookup"><span data-stu-id="7a321-301">Create a logistic regression model</span></span>
<span data-ttu-id="7a321-302">Successivamente, creare un modello di regressione logistica usando hello Spark ML `LogisticRegression()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="7a321-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="7a321-303">Si crea il modello di hello la compilazione di codice in una serie di passaggi:</span><span class="sxs-lookup"><span data-stu-id="7a321-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="7a321-304">**Modello di training hello** dati con un set di parametri.</span><span class="sxs-lookup"><span data-stu-id="7a321-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="7a321-305">**Valutazione del modello di hello** su un set di dati di test con le metriche.</span><span class="sxs-lookup"><span data-stu-id="7a321-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="7a321-306">**Salvare il modello di hello** nell'archiviazione Blob per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="7a321-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="7a321-307">**Modello di punteggio hello** rispetto ai dati di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="7a321-308">**Tracciare i risultati di hello** con ricevitore operativo curve caratteristica (ROC).</span><span class="sxs-lookup"><span data-stu-id="7a321-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="7a321-309">Ecco il codice hello per queste procedure:</span><span class="sxs-lookup"><span data-stu-id="7a321-309">Here's hello code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="7a321-310">Caricare, assegnare un punteggio e salvare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-310">Load, score, and save hello results.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="7a321-311">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-311">**Output:**</span></span>

<span data-ttu-id="7a321-312">ROC sui dati di test = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="7a321-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="7a321-313">Utilizzare Python locale Pandas frame tooplot hello ROC curva dei dati.</span><span class="sxs-lookup"><span data-stu-id="7a321-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


<span data-ttu-id="7a321-314">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-314">**Output:**</span></span>

![Curva ROC per mancia o non mancia](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="7a321-316">Creare un modello di classificazione di foresta casuale</span><span class="sxs-lookup"><span data-stu-id="7a321-316">Create a random forest classification model</span></span>
<span data-ttu-id="7a321-317">Successivamente, creare un modello di classificazione di foresta casuale usando hello Spark ML `RandomForestClassifier()` funzione e quindi valutare il modello di hello sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="7a321-318">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-318">**Output:**</span></span>

<span data-ttu-id="7a321-319">ROC sui dati di test = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="7a321-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="7a321-320">Creare un modello di classificazione GBT</span><span class="sxs-lookup"><span data-stu-id="7a321-320">Create a GBT classification model</span></span>
<span data-ttu-id="7a321-321">Successivamente, creare un modello di classificazione GBT utilizzando del MLlib `GradientBoostedTrees()` funzione e quindi valutare il modello di hello sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="7a321-322">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-322">**Output:**</span></span>

<span data-ttu-id="7a321-323">Area sotto la curva ROC = 0,9846895479241554</span><span class="sxs-lookup"><span data-stu-id="7a321-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="7a321-324">Modello di regressione: stimare l'importo della mancia</span><span class="sxs-lookup"><span data-stu-id="7a321-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="7a321-325">In questa sezione creare due tipi di quantità di regressione modelli toopredict hello Suggerimento:</span><span class="sxs-lookup"><span data-stu-id="7a321-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="7a321-326">Oggetto **modello di regressione lineare regolarizzata** utilizzando hello Spark ML `LinearRegression()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="7a321-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="7a321-327">Verranno salvate modello hello e valutare il modello di hello sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="7a321-328">A **modello di regressione dell'albero boosting sfumatura** utilizzando hello Spark ML `GBTRegressor()` (funzione).</span><span class="sxs-lookup"><span data-stu-id="7a321-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="7a321-329">Creare un modello di regressione lineare regolarizzata</span><span class="sxs-lookup"><span data-stu-id="7a321-329">Create a regularized linear regression model</span></span>
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-330">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-330">**Output:**</span></span>

<span data-ttu-id="7a321-331">Cella di tempo toorun hello: 13 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-331">Time toorun hello cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="7a321-332">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-332">**Output:**</span></span>

<span data-ttu-id="7a321-333">R-sqr sui dati di test = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="7a321-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="7a321-334">Query successiva, hello i risultati dei test come frame di dati e utilizzare toovisualize AutoVizWidget e matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7a321-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="7a321-335">codice Hello crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="7a321-336">Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che è possibile utilizzare tooplot con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="7a321-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="7a321-337">Questo magic Spark viene usato più volte in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="7a321-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="7a321-338">Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.</span><span class="sxs-lookup"><span data-stu-id="7a321-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="7a321-339">Creare tracciati usando matplotlib di Python.</span><span class="sxs-lookup"><span data-stu-id="7a321-339">Create plots by using Python matplotlib.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="7a321-340">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-340">**Output:**</span></span>

![Importo della mancia: effettivo rispetto a stimato](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="7a321-342">Creare un modello di regressione con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="7a321-342">Create a GBT regression model</span></span>
<span data-ttu-id="7a321-343">Creare un modello di regressione GBT utilizzando hello Spark ML `GBTRegressor()` funzione e quindi valutare il modello di hello sui dati di test.</span><span class="sxs-lookup"><span data-stu-id="7a321-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="7a321-344">[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="7a321-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="7a321-345">GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita.</span><span class="sxs-lookup"><span data-stu-id="7a321-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="7a321-346">È possibile usare GBT per la classificazione e la regressione.</span><span class="sxs-lookup"><span data-stu-id="7a321-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="7a321-347">Gli alberi GBT possono gestire funzionalità categoriche, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="7a321-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="7a321-348">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="7a321-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="7a321-349">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-349">**Output:**</span></span>

<span data-ttu-id="7a321-350">Il valore R-sqr del test è: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="7a321-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="7a321-351">Utilità di modellazione avanzate per l'ottimizzazione</span><span class="sxs-lookup"><span data-stu-id="7a321-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="7a321-352">In questa sezione, usare le utilità di Machine Learning che gli sviluppatori spesso usano per l'ottimizzazione del modello.</span><span class="sxs-lookup"><span data-stu-id="7a321-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="7a321-353">In particolare, è possibile ottimizzare i modelli di Machine Learning in tre diversi modi usando lo sweep dei parametri e la convalida incrociata:</span><span class="sxs-lookup"><span data-stu-id="7a321-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="7a321-354">Suddividere i dati di hello in set di training e la convalida, ottimizzare il modello di hello tramite hyper-parameter sweep in un set di training e valutare in un set di convalida (regressione)</span><span class="sxs-lookup"><span data-stu-id="7a321-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="7a321-355">Ottimizzare il modello di hello utilizzando la convalida incrociata e hyper-parameter sweep dalla funzione di Machine Learning Spark CrossValidator (classificazione binaria)</span><span class="sxs-lookup"><span data-stu-id="7a321-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="7a321-356">Ottimizzare il modello di hello tramite codice personalizzato di convalida incrociata e sweep di parametri toouse qualsiasi di machine learning set di funzioni e parametri (regressione)</span><span class="sxs-lookup"><span data-stu-id="7a321-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="7a321-357">**La convalida incrociata** è una tecnica che consente di valutare l'accuratezza, un modello sottoposto a training su un set di dati noto generalizzerà toopredict hello funzionalità dei set di dati in cui si è ancora stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="7a321-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="7a321-358">Hello idea generale di questa tecnica è che un modello è stato sottoposto a training su un set di dati di dati noti e hello accuratezza di esecuzione delle stime viene quindi testata in un set di dati indipendente.</span><span class="sxs-lookup"><span data-stu-id="7a321-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="7a321-359">Un'implementazione comune è toodivide un set di dati in *k*-Raggruppa e quindi eseguire il training del modello di hello in uno schema round robin su almeno una delle sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="7a321-360">**Ottimizzazione di Hyper-parametro** hello problema della scelta di un set di hyper-parametri per un algoritmo di apprendimento, in genere con l'obiettivo di hello ottimizzare una misura delle prestazioni dell'algoritmo hello in un set di dati indipendente.</span><span class="sxs-lookup"><span data-stu-id="7a321-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="7a321-361">Hyper-parameter è un valore che è necessario specificare all'esterno di routine di training modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="7a321-362">Presupposti sui valori dei parametri di hyper possono influire sulla flessibilità hello e sull'accuratezza del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="7a321-363">Gli alberi delle decisioni avere hyper-parametri, ad esempio, ad esempio hello desiderato profondità e numero di foglie nell'albero hello.</span><span class="sxs-lookup"><span data-stu-id="7a321-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="7a321-364">È necessario impostare un termine di penalità per errata classificazione per macchine a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="7a321-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="7a321-365">Un'ottimizzazione comune delle modalità tooperform hyper parametro è toouse una ricerca di griglia, detto anche un **sweep di parametri**.</span><span class="sxs-lookup"><span data-stu-id="7a321-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="7a321-366">In una ricerca di griglia, viene eseguita una ricerca completa tramite i valori hello di un subset specificato di spazio di hyper-parametro hello per un algoritmo di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="7a321-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="7a321-367">La convalida incrociata può fornire un toosort metrica prestazioni out ottimale hello prodotto dall'algoritmo di ricerca di hello griglia.</span><span class="sxs-lookup"><span data-stu-id="7a321-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="7a321-368">Se si utilizza lo sweep dei parametri di hyper convalida incrociata, è possibile consentire l'overfitting dati tootraining modello problemi di limite.</span><span class="sxs-lookup"><span data-stu-id="7a321-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="7a321-369">In questo modo, il modello di hello mantiene hello capacità tooapply toohello generale set di dati dalla quale hello sono stati estratti i dati di training.</span><span class="sxs-lookup"><span data-stu-id="7a321-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="7a321-370">Ottimizzare un modello di regressione lineare con sweep di iperparametri</span><span class="sxs-lookup"><span data-stu-id="7a321-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="7a321-371">Successivamente, suddividere i dati in set di training e la convalida, utilizzare hyper-parameter sweep in un training set modello hello toooptimize e valutare in un set di convalida (regressione lineare).</span><span class="sxs-lookup"><span data-stu-id="7a321-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="7a321-372">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-372">**Output:**</span></span>

<span data-ttu-id="7a321-373">Il valore R-sqr del test è: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="7a321-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="7a321-374">Ottimizzare il modello di classificazione binaria hello utilizzando la convalida incrociata e hyper-parameter sweep</span><span class="sxs-lookup"><span data-stu-id="7a321-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="7a321-375">In questa sezione viene illustrato come toooptimize una classificazione binaria del modello tramite la convalida incrociata e hyper-parameter sweep.</span><span class="sxs-lookup"><span data-stu-id="7a321-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="7a321-376">Questo metodo utilizza hello Spark ML `CrossValidator` (funzione).</span><span class="sxs-lookup"><span data-stu-id="7a321-376">This uses hello Spark ML `CrossValidator` function.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="7a321-377">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-377">**Output:**</span></span>

<span data-ttu-id="7a321-378">Cella di tempo toorun hello: 33 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="7a321-379">Ottimizzare il modello di regressione lineare di hello utilizzando codice personalizzato di convalida incrociata e sweep di parametri</span><span class="sxs-lookup"><span data-stu-id="7a321-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="7a321-380">Successivamente, ottimizzare il modello di hello utilizzando codice personalizzato e identificare i parametri del modello migliori hello tramite criterio hello di precisione più elevata.</span><span class="sxs-lookup"><span data-stu-id="7a321-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="7a321-381">Quindi, creare modello finale hello, valutare hello modello sui dati di test e salvare il modello di hello nell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="7a321-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="7a321-382">Infine, caricare il modello di hello, assegnare un punteggio dati di test e valutare l'accuratezza.</span><span class="sxs-lookup"><span data-stu-id="7a321-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="7a321-383">**Output:**</span><span class="sxs-lookup"><span data-stu-id="7a321-383">**Output:**</span></span>

<span data-ttu-id="7a321-384">Cella di tempo toorun hello: 61 secondi.</span><span class="sxs-lookup"><span data-stu-id="7a321-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="7a321-385">Usare automaticamente i modelli di Machine Learning compilati con Spark con Scala</span><span class="sxs-lookup"><span data-stu-id="7a321-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="7a321-386">Per una panoramica degli argomenti che consentono di eseguire attività di hello che costituiscono il processo di analisi scientifica dei dati hello in Azure, vedere [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="7a321-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="7a321-387">[Procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md) vengono descritte altre procedure dettagliate end-to-end che illustrano i passaggi hello in hello Team processo di analisi scientifica dei dati per scenari specifici.</span><span class="sxs-lookup"><span data-stu-id="7a321-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="7a321-388">procedure dettagliate di Hello anche illustrano come toocombine cloud e locali strumenti e servizi in un flusso di lavoro o la pipeline di toocreate un'applicazione intelligente.</span><span class="sxs-lookup"><span data-stu-id="7a321-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="7a321-389">[Assegnare un punteggio i modelli di apprendimento compilato Spark](machine-learning-data-science-spark-model-consumption.md) Mostra come toouse Scala codice tooautomatically caricare e assegnare un punteggio nuovi set di dati con i modelli di apprendimento compilato in Spark e salvata nell'archiviazione Blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a321-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="7a321-390">È possibile seguire le istruzioni di hello purché esista e sostituire semplicemente hello codice Python con codice di Scala in questo articolo per il consumo automatico.</span><span class="sxs-lookup"><span data-stu-id="7a321-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

