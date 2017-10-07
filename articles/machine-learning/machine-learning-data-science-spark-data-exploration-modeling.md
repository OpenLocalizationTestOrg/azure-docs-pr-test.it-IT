---
title: aaaData esplorazione e modellazione con Spark | Documenti Microsoft
description: "Apprendimento hello l'esplorazione dei dati e modellazione di funzionalità del toolkit di hello MLlib Spark in Azure."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="b8500-103">Modellazione ed esplorazione dei dati con Spark</span><span class="sxs-lookup"><span data-stu-id="b8500-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="b8500-104">Questa procedura dettagliata Usa l'esplorazione dei dati di HDInsight Spark toodo e classificazione binaria e modellazione di attività a un campione di hello NYC regressione taxi di andata e ritorno e presentare set di dati 2013.</span><span class="sxs-lookup"><span data-stu-id="b8500-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="b8500-105">Contiene passaggi hello di hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess), end-to-end, utilizzando un HDInsight Spark cluster per l'elaborazione e i modelli di dati e hello hello toostore oggetti BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8500-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="b8500-106">processo Hello analizza e visualizza i dati importati da un Blob di archiviazione di Azure e quindi prepara hello dati toobuild modelli predittivi.</span><span class="sxs-lookup"><span data-stu-id="b8500-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="b8500-107">Questi modelli sono compilazione mediante classificazione binaria toodo toolkit Spark MLlib hello e modellazione di attività di regressione.</span><span class="sxs-lookup"><span data-stu-id="b8500-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="b8500-108">Hello **classificazione binaria** attività è toopredict un suggerimento è pagato viaggi hello o meno.</span><span class="sxs-lookup"><span data-stu-id="b8500-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="b8500-109">Hello **regressione** attività è quantità hello toopredict del suggerimento hello in base alle altre funzionalità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="b8500-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="b8500-110">i modelli di Hello che utilizziamo includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting:</span><span class="sxs-lookup"><span data-stu-id="b8500-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="b8500-111">[La regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che utilizza un metodo dei valori descent con sfumatura Stocastica (SGD, Virtual Private Network) e gli importi di suggerimento hello toopredict la scalabilità a pagamento per l'ottimizzazione e funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8500-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="b8500-112">[La regressione logistica con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regressione "logit", è un modello di regressione che può essere utilizzato quando variabile dipendente hello è organizzato per categorie toodo classificazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="b8500-113">LBFGS è un algoritmo di ottimizzazione quasi Newton che offre un'approssimazione algoritmo di Broyden – Fletcher – Goldfarb – Shanno (BFGS) hello utilizzando una quantità limitata di memoria del computer e che è ampiamente usati in machine learning.</span><span class="sxs-lookup"><span data-stu-id="b8500-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="b8500-114">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="b8500-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="b8500-115">Combinano molti decision trees tooreduce hello rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="b8500-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="b8500-116">Foreste casuali vengono utilizzate per la classificazione e regressione e possono gestire funzioni categoriche e possono essere esteso l'impostazione di classificazione multiclasse toohello.</span><span class="sxs-lookup"><span data-stu-id="b8500-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="b8500-117">Non richiedono funzionalità scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8500-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="b8500-118">Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.</span><span class="sxs-lookup"><span data-stu-id="b8500-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="b8500-119">[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="b8500-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="b8500-120">GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita.</span><span class="sxs-lookup"><span data-stu-id="b8500-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="b8500-121">GBTs vengono utilizzati per la classificazione e regressione e può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8500-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="b8500-122">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="b8500-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="b8500-123">i passaggi di modellazione Hello inoltre contenere codice che illustra come tootrain, valutare e salvare ogni tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="b8500-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="b8500-124">Python è stato utilizzato toocode hello soluzione e tooshow hello rilevanti tracciati.</span><span class="sxs-lookup"><span data-stu-id="b8500-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="b8500-125">Anche se hello Spark MLlib toolkit è progettato toowork su grandi set di dati, un campione di dimensioni relativamente ridotte (circa 30 Mb utilizzando K 170 righe, circa 0,1% del set di dati NYC originale hello) viene usato per motivi di praticità.</span><span class="sxs-lookup"><span data-stu-id="b8500-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="b8500-126">esercizio Hello indicato qui viene eseguito in modo efficiente (in circa 10 minuti) in un cluster di HDInsight con 2 nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b8500-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="b8500-127">Hello stesso codice, con modifiche minori, può essere utilizzato tooprocess maggiore-set di dati, con le modifiche appropriate per la memorizzazione nella cache dei dati in memoria e la modifica delle dimensioni del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b8500-128">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b8500-128">Prerequisites</span></span>
<span data-ttu-id="b8500-129">È necessario un account Azure e Spark 1.6 (o 2.0 Spark) toocomplete cluster HDInsight in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b8500-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="b8500-130">Vedere hello [panoramica dell'analisi scientifica dei dati utilizzando Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md) per istruzioni su come toosatisfy questi requisiti.</span><span class="sxs-lookup"><span data-stu-id="b8500-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="b8500-131">Questo argomento contiene inoltre una descrizione di hello dati NYC 2013 Taxi utilizzati in questo argomento e per istruzioni su come il codice da un server Jupyter notebook nel cluster Spark hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="b8500-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="b8500-132">Notebook e cluster Spark</span><span class="sxs-lookup"><span data-stu-id="b8500-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="b8500-133">La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="b8500-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="b8500-134">Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b8500-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="b8500-135">Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono.</span><span class="sxs-lookup"><span data-stu-id="b8500-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="b8500-136">Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="b8500-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="b8500-137">Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b8500-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="b8500-138">Per praticità, di seguito sono collegamenti hello toohello Jupyter notebook per Spark 1.6 (toobe eseguito nel kernel pySpark hello di hello server Jupyter Notebook) e Spark 2.0 (toobe eseguito nel kernel pySpark3 hello di hello server Jupyter Notebook):</span><span class="sxs-lookup"><span data-stu-id="b8500-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="b8500-139">Notebook Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="b8500-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="b8500-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi con diversi algoritmi.</span><span class="sxs-lookup"><span data-stu-id="b8500-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="b8500-141">Notebook Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="b8500-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="b8500-142">attività di classificazione e regressione Hello implementate utilizzando un cluster Spark 2.0 sono separati blocchi appunti e notebook classificazione hello utilizza un set di dati diverso:</span><span class="sxs-lookup"><span data-stu-id="b8500-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="b8500-143">[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi in Spark 2.0 cluster tramite hello viaggi NYC Taxi e set di dati tariffa descritto [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="b8500-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="b8500-144">Questo blocco può essere un buon punto di partenza per esplorare rapidamente codice hello che è stato fornito per Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b8500-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="b8500-145">Per un blocco per Appunti più dettagliata analizza hello dati NYC Taxi, vedere notebook avanti di hello in questo elenco.</span><span class="sxs-lookup"><span data-stu-id="b8500-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="b8500-146">Vedere le note di hello seguendo questo elenco di confrontare questi notebook.</span><span class="sxs-lookup"><span data-stu-id="b8500-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="b8500-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello viaggi NYC Taxi e tariffa set di dati descritto [ qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="b8500-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="b8500-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): questo file viene illustrato come tooperform dati wrangling (operazioni Spark SQL e frame di dati), l'esplorazione, modellazione e assegnazione dei punteggi usando hello partenza in fase di Airline noto set di dati da 2011 e 2012.</span><span class="sxs-lookup"><span data-stu-id="b8500-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="b8500-149">È integrato hello airline dataset con hello aeroporto weather dati (ad esempio, velocità del vento, temperatura, altitudine e così via) precedenti toomodeling, in modo queste funzionalità weather possono essere incluso nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="b8500-150">set di dati airline Hello è stato aggiunto notebook toohello Spark 2.0 toobetter illustrano l'utilizzo di hello di algoritmi di classificazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="b8500-151">Vedere i seguenti collegamenti per informazioni sui set di dati in fase di partenza airline e set di dati meteo hello:</span><span class="sxs-lookup"><span data-stu-id="b8500-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="b8500-152">Dati sulle partenze puntuali dei voli della compagnia aerea: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="b8500-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="b8500-153">Dati sulle condizioni atmosferiche dell'aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="b8500-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="b8500-154">Appunti di Spark 2.0 Hello in hello taxi NYC e airline flight delay-set di dati può richiedere 10 minuti o più toorun (a seconda delle dimensioni di hello del cluster HDI).</span><span class="sxs-lookup"><span data-stu-id="b8500-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="b8500-155">primo notebook in hello sopra elenco Hello Mostra molti aspetti di esplorazione dei dati di hello, training in un blocco per Appunti che accetta toorun meno tempo con ridotti NYC set di dati, in cui hello sono stati già aggiunti a un file taxi e fare del modello di visualizzazione e ML: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) il blocco accetta un molto più breve tempo toofinish (2-3 minuti) e può essere un buon punto di partenza per esplorare rapidamente codice hello abbiamo fornito per Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="b8500-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="b8500-156">descrizioni di Hello riportate di seguito sono correlati toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="b8500-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="b8500-157">Per le versioni 2.0 Spark, utilizzare i notebook hello descritti e in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b8500-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="b8500-158">Il programma di installazione: hello, librerie e percorsi di archiviazione predefinito contesto Spark</span><span class="sxs-lookup"><span data-stu-id="b8500-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="b8500-159">Spark è in grado di tooAzure tooread e di scrittura Blob di archiviazione (noto anche come WASB).</span><span class="sxs-lookup"><span data-stu-id="b8500-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="b8500-160">Pertanto, i dati esistenti archiviate possono essere elaborati utilizzando Spark e hello risultati WASB archiviato nuovamente in.</span><span class="sxs-lookup"><span data-stu-id="b8500-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="b8500-161">modelli toosave o file in WASB, percorso hello deve toobe specificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b8500-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="b8500-162">Hello del cluster Spark toohello contenitore collegato predefinito possibile farvi riferimento tramite un che inizia con: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="b8500-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="b8500-163">"wasb://" fa riferimento ad altri percorsi.</span><span class="sxs-lookup"><span data-stu-id="b8500-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="b8500-164">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="b8500-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="b8500-165">esempio di codice seguente Hello Specifica percorso hello di hello dati toobe leggere e hello percorso per l'output di hello modello archiviazione directory toowhich hello modello viene salvato:</span><span class="sxs-lookup"><span data-stu-id="b8500-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="b8500-166">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="b8500-166">Import libraries</span></span>
<span data-ttu-id="b8500-167">Per la configurazione occorre anche importare le librerie necessarie.</span><span class="sxs-lookup"><span data-stu-id="b8500-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="b8500-168">Impostare il contesto di spark e importare le librerie necessarie con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b8500-168">Set spark context and import necessary libraries with hello following code:</span></span>

    # IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="b8500-169">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="b8500-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="b8500-170">kernel PySpark Hello forniti con i notebook Jupyter dispone di un contesto predefinito.</span><span class="sxs-lookup"><span data-stu-id="b8500-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="b8500-171">Pertanto, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con un'applicazione hello che si sta sviluppando.</span><span class="sxs-lookup"><span data-stu-id="b8500-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="b8500-172">Questi contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b8500-172">These contexts are available for you by default.</span></span> <span data-ttu-id="b8500-173">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="b8500-173">These contexts are:</span></span>

* <span data-ttu-id="b8500-174">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="b8500-174">sc - for Spark</span></span> 
* <span data-ttu-id="b8500-175">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="b8500-175">sqlContext - for Hive</span></span>

<span data-ttu-id="b8500-176">Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con % %.</span><span class="sxs-lookup"><span data-stu-id="b8500-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="b8500-177">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="b8500-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="b8500-178">**% % locale** specifica che il codice hello nelle righe successive toobe eseguite localmente.</span><span class="sxs-lookup"><span data-stu-id="b8500-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="b8500-179">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="b8500-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="b8500-180">**% % sql -o <variable name>**  esegue una query Hive sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="b8500-181">Se viene passato il parametro -o hello, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="b8500-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="b8500-182">Per ulteriori informazioni su kernel hello per notebook Jupyter e hello predefiniti "magics" che forniscono, vedere [cluster kernel disponibile per i server Jupyter notebook con Linux di HDInsight Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="b8500-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="b8500-183">Inserimento di dati dal BLOB pubblico</span><span class="sxs-lookup"><span data-stu-id="b8500-183">Data ingestion from public blob</span></span>
<span data-ttu-id="b8500-184">Hello primo passaggio nel processo di analisi scientifica dei dati hello consiste tooingest hello dati toobe analizzati da origini in cui è si trova nell'ambiente di esplorazione e modellazione di dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="b8500-185">ambiente di Hello è Spark in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b8500-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="b8500-186">In questa sezione contiene toocomplete codice hello una serie di attività:</span><span class="sxs-lookup"><span data-stu-id="b8500-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="b8500-187">inserimento hello dati esempio toobe modellata</span><span class="sxs-lookup"><span data-stu-id="b8500-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="b8500-188">leggere nel set di input dati hello (archiviati come file tsv)</span><span class="sxs-lookup"><span data-stu-id="b8500-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="b8500-189">formato e dati hello pulita</span><span class="sxs-lookup"><span data-stu-id="b8500-189">format and clean hello data</span></span>
* <span data-ttu-id="b8500-190">Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="b8500-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="b8500-191">Registrazione come tabella temporanea in un contesto SQL.</span><span class="sxs-lookup"><span data-stu-id="b8500-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="b8500-192">Ecco il codice hello per l'inserimento di dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-192">Here is hello code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b8500-193">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-193">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-194">Tempo impiegato tooexecute di sopra di: 51.72 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="b8500-195">Visualizzazione ed esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="b8500-195">Data exploration & visualization</span></span>
<span data-ttu-id="b8500-196">Dopo aver inseriti dati hello in Spark, hello il passaggio successivo nel processo di analisi scientifica dei dati hello è toogain comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="b8500-197">In questa sezione è esaminare i dati di taxi hello utilizzando le query SQL e le variabili di destinazione di tracciato hello e funzionalità potenziali per l'esame visivo.</span><span class="sxs-lookup"><span data-stu-id="b8500-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="b8500-198">Nello specifico, abbiamo tracciare frequenza hello dei conteggi di passeggeri in taxi trip, hello della frequenza degli importi di suggerimento e come suggerimenti variano a seconda del tipo e la quantità di pagamento.</span><span class="sxs-lookup"><span data-stu-id="b8500-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="b8500-199">Tracciare un istogramma che mostra le frequenze di conteggio di passeggeri nell'esempio hello di trip taxi</span><span class="sxs-lookup"><span data-stu-id="b8500-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="b8500-200">Questo codice e i successivi frammenti di codice è possibile utilizzare SQL tooquery magic hello dati di esempio e locale tooplot magic hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="b8500-201">**Chiave SQL (`%%sql`)** HDInsight PySpark kernel hello supporta hello sqlContext query HiveQL facile inline.</span><span class="sxs-lookup"><span data-stu-id="b8500-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="b8500-202">Hello (-o VARIABLE_NAME) argomento mantiene l'output di hello di query SQL hello sotto forma di un frame di dati Pandas server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="b8500-203">Ciò significa che è disponibile in modalità locale hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="b8500-204">Hello  **`%%local` magic** viene utilizzato codice toorun localmente nel server di Jupyter hello, ovvero hello nodo head del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="b8500-205">In genere, si utilizza `%%local` magic in combinazione con hello `%%sql` magic con parametro -o.</span><span class="sxs-lookup"><span data-stu-id="b8500-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="b8500-206">il parametro -o Hello sarebbe ancora valide output di hello di query SQL hello in locale e quindi % % magic locale Attiva set successivo di hello di toorun frammento di codice in locale sull'output di hello delle query SQL hello in modo permanente in locale</span><span class="sxs-lookup"><span data-stu-id="b8500-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="b8500-207">output di Hello viene automaticamente visualizzato dopo l'esecuzione di codice hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="b8500-208">Questa query recupera trip hello dal conteggio di passeggeri.</span><span class="sxs-lookup"><span data-stu-id="b8500-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="b8500-209">Questo codice crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="b8500-210">Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che può essere usato per il tracciato con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="b8500-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="b8500-211">Tale magic PySpark viene usato più volte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="b8500-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="b8500-212">Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.</span><span class="sxs-lookup"><span data-stu-id="b8500-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="b8500-213">Ecco trip di hello tooplot codice hello da passeggero conteggi</span><span class="sxs-lookup"><span data-stu-id="b8500-213">Here is hello code tooplot hello trips by passenger counts</span></span>

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="b8500-214">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-214">**OUTPUT:**</span></span>

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="b8500-216">È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, linea, Area o barra) utilizzando hello **tipo** pulsanti di menu in blocco per Appunti hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="b8500-217">tracciato barra Hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b8500-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="b8500-218">Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.</span><span class="sxs-lookup"><span data-stu-id="b8500-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="b8500-219">Utilizzare una data di toosample query SQL.</span><span class="sxs-lookup"><span data-stu-id="b8500-219">Use a SQL query toosample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped 
    FROM taxi_train 
    WHERE passenger_count > 0 
    AND passenger_count < 7 
    AND fare_amount > 0 
    AND fare_amount < 200 
    AND payment_type in ('CSH', 'CRD') 
    AND tip_amount > 0 
    AND tip_amount < 25


<span data-ttu-id="b8500-220">Questa cella codice utilizza hello SQL query toocreate tre vengono tracciati hello dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


<span data-ttu-id="b8500-221">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-221">**OUTPUT:**</span></span> 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="b8500-225">Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione</span><span class="sxs-lookup"><span data-stu-id="b8500-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="b8500-226">In questa sezione descrive e fornisce codice hello per le procedure utilizzate tooprepare dati per la modellazione di ML.</span><span class="sxs-lookup"><span data-stu-id="b8500-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="b8500-227">Viene illustrato come hello toodo seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="b8500-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="b8500-228">Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="b8500-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="b8500-229">Indicizzare e codificare funzionalità categoriche</span><span class="sxs-lookup"><span data-stu-id="b8500-229">Index and encode categorical features</span></span>
* <span data-ttu-id="b8500-230">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="b8500-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="b8500-231">Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing</span><span class="sxs-lookup"><span data-stu-id="b8500-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="b8500-232">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="b8500-232">Feature scaling</span></span>
* <span data-ttu-id="b8500-233">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="b8500-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="b8500-234">Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="b8500-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="b8500-235">Questo codice viene illustrato come una nuova funzionalità inserendo ore in fase di traffico toocreate bucket e quindi come toocache hello risultante frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="b8500-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="b8500-236">Quando sono utilizzati più volte resilienti distribuiti i set di dati (RDDs) e frame di dati, la memorizzazione nella cache comporta tempi di esecuzione tooimproved.</span><span class="sxs-lookup"><span data-stu-id="b8500-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="b8500-237">Di conseguenza, nella cache RDDs e frame di dati in varie fasi in questa procedura dettagliata hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="b8500-238">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-238">**OUTPUT:**</span></span> 

<span data-ttu-id="b8500-239">126050</span><span class="sxs-lookup"><span data-stu-id="b8500-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="b8500-240">Indicizzare e codificare funzionalità categoriche per l'inserimento in funzioni di modellazione</span><span class="sxs-lookup"><span data-stu-id="b8500-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="b8500-241">Questa sezione viene illustrato come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="b8500-242">modellazione Hello e funzioni di MLlib richiedono funzionalità con dati di input categorici toobe indicizzato o codificato toouse precedente di stima.</span><span class="sxs-lookup"><span data-stu-id="b8500-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="b8500-243">A seconda del modello di hello, è necessario tooindex o codificarli in modi diversi:</span><span class="sxs-lookup"><span data-stu-id="b8500-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="b8500-244">**Modellazione basata sulla struttura ad albero** richiede toobe categorie codificati come valori numerici (ad esempio, una funzionalità costituita da tre categorie potrebbe essere stata codificata con 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="b8500-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="b8500-245">Questo avviene tramite la funzione [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) di MLlib,</span><span class="sxs-lookup"><span data-stu-id="b8500-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="b8500-246">Questa funzione consente di codificare una colonna stringa della colonna di etichette tooa di indici di etichetta che sono ordinati per le frequenze di etichetta.</span><span class="sxs-lookup"><span data-stu-id="b8500-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="b8500-247">Sebbene indicizzato con i valori numerici per l'input e la gestione dei dati, algoritmi di hello basati sulla struttura ad albero possono essere tootreat specificato in modo appropriato come categorie.</span><span class="sxs-lookup"><span data-stu-id="b8500-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="b8500-248">**Modelli di regressione lineare e di Logistic** richiedono la scelta di una codifica, in cui, ad esempio, una funzionalità costituita da tre categorie può essere espanso in tre colonne di funzionalità, con ogni contiene 0 o 1 a seconda della categoria di hello di un'osservazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="b8500-249">Fornisce MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione toodo hot una codifica.</span><span class="sxs-lookup"><span data-stu-id="b8500-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="b8500-250">Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo.</span><span class="sxs-lookup"><span data-stu-id="b8500-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="b8500-251">Questa codifica consente di utilizzare gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, funzionalità toocategorical toobe applicato.</span><span class="sxs-lookup"><span data-stu-id="b8500-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="b8500-252">Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:</span><span class="sxs-lookup"><span data-stu-id="b8500-252">Here is hello code tooindex and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-253">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-253">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-254">Tempo impiegato tooexecute di sopra di: 1,28 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="b8500-255">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="b8500-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="b8500-256">In questa sezione contiene codice che illustra come di tipo di dati di testo categorico tooindex come etichetta punto dati e codificarli in modo che possano essere utilizzati tootrain e test MLlib regressione logistica e altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="b8500-257">Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="b8500-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="b8500-258">Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.</span><span class="sxs-lookup"><span data-stu-id="b8500-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="b8500-259">In questa sezione contiene codice che illustra come dati di testo categorico tooindex come un [etichetta punto](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) tipo di dati e la codifica in modo che possano essere utilizzati tootrain e test MLlib regressione logistica e altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="b8500-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="b8500-260">Gli oggetti punto etichettato RDD (Resilient Distributed Dataset) costituiti da un'etichetta, o variabile di destinazione/risposta, e da un vettore di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8500-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="b8500-261">Questo formato è richiesto come input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="b8500-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="b8500-262">Ecco hello tooindex codice e codificare le funzionalità di testo per la classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="b8500-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="b8500-263">Ecco il codice hello tooencode indice testo categorico funzionalità per l'analisi di regressione lineare.</span><span class="sxs-lookup"><span data-stu-id="b8500-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])

        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="b8500-264">Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing</span><span class="sxs-lookup"><span data-stu-id="b8500-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="b8500-265">Questo codice crea un campionamento casuale dei dati di hello (25% viene utilizzato qui).</span><span class="sxs-lookup"><span data-stu-id="b8500-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="b8500-266">Anche se non sono richiesto per questo esempio a causa delle dimensioni toohello di hello set di dati, viene illustrato come è possibile campionare qui a per sapere come toouse per il proprio problema quando necessario.</span><span class="sxs-lookup"><span data-stu-id="b8500-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="b8500-267">Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli.</span><span class="sxs-lookup"><span data-stu-id="b8500-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="b8500-268">Successivamente è suddivisa: esempio hello una parte di training (75%) e un test toouse parte (25 %)) nella classificazione e creazione di modelli di regressione.</span><span class="sxs-lookup"><span data-stu-id="b8500-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-269">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-269">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-270">Tempo impiegato tooexecute di sopra di: 0,24 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="b8500-271">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="b8500-271">Feature scaling</span></span>
<span data-ttu-id="b8500-272">Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="b8500-273">codice per la funzionalità scalabilità Hello Usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza di toounit tooscale hello funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b8500-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="b8500-274">Viene fornito da MLlib per l'uso nella regressione lineare con la discesa del gradiente stocastica (SGD), un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="b8500-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="b8500-275">È stato trovato il ridimensionamento di hello LinearRegressionWithSGD algoritmo toobe toofeature sensibili.</span><span class="sxs-lookup"><span data-stu-id="b8500-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="b8500-276">Ecco le variabili di tooscale codice hello per l'utilizzo con l'algoritmo SGD lineare di regolarizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

    # FEATURE SCALING

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-277">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-277">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-278">Tempo impiegato tooexecute di sopra di: 13.17 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="b8500-279">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="b8500-279">Cache objects in memory</span></span>
<span data-ttu-id="b8500-280">tempo di Hello impiegato per il training e il testing di algoritmi di Machine Learning è possibile ridurre la memorizzazione nella cache gli oggetti frame di dati di input hello utilizzati per la classificazione, regressione, e con funzionalità di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="b8500-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-281">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-281">**OUTPUT:**</span></span> 

<span data-ttu-id="b8500-282">Tempo impiegato tooexecute di sopra di: 0,15 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="b8500-283">Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia</span><span class="sxs-lookup"><span data-stu-id="b8500-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="b8500-284">In questa sezione viene illustrato come utilizzare tre modelli per attività di classificazione binaria hello di stima di un suggerimento viene pagato per un itinerario taxi o meno.</span><span class="sxs-lookup"><span data-stu-id="b8500-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="b8500-285">modelli di Hello presentati sono:</span><span class="sxs-lookup"><span data-stu-id="b8500-285">hello models presented are:</span></span>

* <span data-ttu-id="b8500-286">Regressione logistica regolarizzata.</span><span class="sxs-lookup"><span data-stu-id="b8500-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="b8500-287">Modello di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="b8500-287">Random forest model</span></span>
* <span data-ttu-id="b8500-288">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="b8500-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="b8500-289">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="b8500-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="b8500-290">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="b8500-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="b8500-291">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="b8500-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="b8500-292">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="b8500-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="b8500-293">Classificazione tramite regressione logistica</span><span class="sxs-lookup"><span data-stu-id="b8500-293">Classification using logistic regression</span></span>
<span data-ttu-id="b8500-294">codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet.</span><span class="sxs-lookup"><span data-stu-id="b8500-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="b8500-295">**Training modello di regressione logistica hello utilizzando CV e hyperparameter sweep**</span><span class="sxs-lookup"><span data-stu-id="b8500-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="b8500-296">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-296">**OUTPUT:**</span></span> 

<span data-ttu-id="b8500-297">Coefficienti: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="b8500-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="b8500-298">Intercetta: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="b8500-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="b8500-299">Tempo impiegato tooexecute di sopra di: 14.43 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="b8500-300">**Valutazione del modello di classificazione binaria hello con le metriche standard**</span><span class="sxs-lookup"><span data-stu-id="b8500-300">**Evaluate hello binary classification model with standard metrics**</span></span>

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="b8500-301">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-301">**OUTPUT:**</span></span> 

<span data-ttu-id="b8500-302">Area in PR = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="b8500-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="b8500-303">Area in ROC = 0,983714670256</span><span class="sxs-lookup"><span data-stu-id="b8500-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="b8500-304">Statistiche di riepilogo</span><span class="sxs-lookup"><span data-stu-id="b8500-304">Summary Stats</span></span>

<span data-ttu-id="b8500-305">Precisione = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="b8500-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="b8500-306">Richiamo = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="b8500-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="b8500-307">Punteggio F1 = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="b8500-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="b8500-308">Tempo impiegato tooexecute di sopra di: 57.61 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="b8500-309">**Tracciare una curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="b8500-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="b8500-310">Hello *predictionAndLabelsDF* viene registrato come una tabella, *tmp_results*, nella cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="b8500-311">*tmp_results* possibile toodo utilizzato query e restituire i risultati in hello sqlResults-frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="b8500-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="b8500-312">Ecco il codice hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="b8500-313">Ecco le stime di toomake codice hello e hello tracciato curva ROC.</span><span class="sxs-lookup"><span data-stu-id="b8500-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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


<span data-ttu-id="b8500-314">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="b8500-316">Classificazione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="b8500-316">Random forest classification</span></span>
<span data-ttu-id="b8500-317">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di foresta casuale che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-318">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-318">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-319">Area in ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="b8500-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="b8500-320">Tempo impiegato tooexecute di sopra di: 31.09 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="b8500-321">Classificazione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="b8500-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="b8500-322">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.</span><span class="sxs-lookup"><span data-stu-id="b8500-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="b8500-323">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-323">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-324">Area in ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="b8500-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="b8500-325">Tempo impiegato tooexecute di sopra di: 19.76 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="b8500-326">Uso di modelli regressivi per prevedere l'importo delle mance per le corse in taxi</span><span class="sxs-lookup"><span data-stu-id="b8500-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="b8500-327">In questa sezione viene illustrato come utilizzare tre modelli per attività di regressione hello di stima quantità hello del suggerimento hello a pagamento per un itinerario taxi basato sulle altre funzionalità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="b8500-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="b8500-328">modelli di Hello presentati sono:</span><span class="sxs-lookup"><span data-stu-id="b8500-328">hello models presented are:</span></span>

* <span data-ttu-id="b8500-329">Regressione lineare regolarizzata</span><span class="sxs-lookup"><span data-stu-id="b8500-329">Regularized linear regression</span></span>
* <span data-ttu-id="b8500-330">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="b8500-330">Random forest</span></span>
* <span data-ttu-id="b8500-331">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="b8500-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="b8500-332">Questi modelli sono stati descritti introduzione hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-332">These models were described in hello introduction.</span></span> <span data-ttu-id="b8500-333">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="b8500-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="b8500-334">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="b8500-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="b8500-335">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="b8500-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="b8500-336">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="b8500-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="b8500-337">Regressione lineare con SGD</span><span class="sxs-lookup"><span data-stu-id="b8500-337">Linear regression with SGD</span></span>
<span data-ttu-id="b8500-338">Hello codice in questa sezione viene illustrato come toouse scalato funzionalità tootrain una regressione lineare che usa descent con sfumatura stocastica (SGD) per l'ottimizzazione, e come tooscore, valutare e salvare il modello di hello in archiviazione Blob di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="b8500-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="b8500-339">Nella nostra esperienza, si possono verificare problemi con convergenza hello dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="b8500-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="b8500-340">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="b8500-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-341">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-341">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-342">Coefficienti: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="b8500-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="b8500-343">Intercetta: -0,853872718283</span><span class="sxs-lookup"><span data-stu-id="b8500-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="b8500-344">RMSE = 1,24190115863</span><span class="sxs-lookup"><span data-stu-id="b8500-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="b8500-345">R-sqr = 0,608017146081</span><span class="sxs-lookup"><span data-stu-id="b8500-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="b8500-346">Tempo impiegato tooexecute di sopra di: 58.42 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="b8500-347">Regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="b8500-347">Random Forest regression</span></span>
<span data-ttu-id="b8500-348">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare una regressione foresta casuale che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-349">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-349">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-350">RMSE = 0,891209218139</span><span class="sxs-lookup"><span data-stu-id="b8500-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="b8500-351">R-sqr = 0,759661334921</span><span class="sxs-lookup"><span data-stu-id="b8500-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="b8500-352">Tempo impiegato tooexecute di sopra di: 49.21 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="b8500-353">Regressione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="b8500-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="b8500-354">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="b8500-355">**Eseguire il training e valutare**</span><span class="sxs-lookup"><span data-stu-id="b8500-355">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="b8500-356">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-356">**OUTPUT:**</span></span>

<span data-ttu-id="b8500-357">RMSE = 0,908473148639</span><span class="sxs-lookup"><span data-stu-id="b8500-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="b8500-358">R-sqr = 0,753835096681</span><span class="sxs-lookup"><span data-stu-id="b8500-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="b8500-359">Tempo impiegato tooexecute di sopra di: 34.52 secondi</span><span class="sxs-lookup"><span data-stu-id="b8500-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="b8500-360">**Grafico**</span><span class="sxs-lookup"><span data-stu-id="b8500-360">**Plot**</span></span>

<span data-ttu-id="b8500-361">*tmp_results* viene registrato come una tabella Hive in una cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="b8500-362">I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="b8500-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="b8500-363">Ecco il codice hello</span><span class="sxs-lookup"><span data-stu-id="b8500-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="b8500-364">Ecco dati hello tooplot codice hello utilizzando server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="b8500-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


<span data-ttu-id="b8500-365">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="b8500-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="b8500-367">Pulire gli oggetti dalla memoria</span><span class="sxs-lookup"><span data-stu-id="b8500-367">Clean up objects from memory</span></span>
<span data-ttu-id="b8500-368">Utilizzare `unpersist()` toodelete oggetti memorizzati nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="b8500-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="b8500-369">Percorsi di archiviazione di record dei modelli di hello del consumo e assegnazione dei punteggi</span><span class="sxs-lookup"><span data-stu-id="b8500-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="b8500-370">tooconsume e punteggio di un set di dati indipendenti descritto in hello [punteggio e valutare i modelli di apprendimento compilato Spark](machine-learning-data-science-spark-model-consumption.md) argomento, è necessario toocopy e incollare i file i nomi che contiene i modelli di hello salvato creati qui in hello Notebook Jupyter consumo.</span><span class="sxs-lookup"><span data-stu-id="b8500-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="b8500-371">Di seguito è tooprint codice hello out hello percorsi toomodel file che è necessario non esiste.</span><span class="sxs-lookup"><span data-stu-id="b8500-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="b8500-372">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="b8500-372">**OUTPUT**</span></span>

<span data-ttu-id="b8500-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="b8500-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="b8500-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="b8500-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="b8500-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="b8500-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="b8500-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="b8500-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="b8500-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="b8500-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="b8500-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="b8500-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="b8500-379">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8500-379">What's next?</span></span>
<span data-ttu-id="b8500-380">Dopo aver creato i modelli di classificazione e regressione con MlLib Spark hello, si è toolearn pronto come tooscore e valutare questi modelli.</span><span class="sxs-lookup"><span data-stu-id="b8500-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="b8500-381">Ciao avanzate di esplorazione dei dati e modellazione dives notebook più approfondito in tra la convalida incrociata, hyper-parameter sweep e valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="b8500-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="b8500-382">**Utilizzo del modello:** toolearn come tooscore e valutare i modelli di classificazione e regressione hello creati in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="b8500-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="b8500-383">**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri</span><span class="sxs-lookup"><span data-stu-id="b8500-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

