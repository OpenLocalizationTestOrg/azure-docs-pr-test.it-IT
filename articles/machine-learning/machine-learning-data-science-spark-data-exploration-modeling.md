---
title: Modellazione ed esplorazione dei dati con Spark | Documentazione Microsoft
description: "Illustra le funzionalità di modellazione ed esplorazione dei dati del toolkit MLlib di Spark su Azure."
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
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="a26f5-103">Modellazione ed esplorazione dei dati con Spark</span><span class="sxs-lookup"><span data-stu-id="a26f5-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="a26f5-104">Questa procedura dettagliata usa HDInsight Spark per eseguire l'esplorazione dei dati e attività di classificazione binaria e modellazione basata sulla regressione su un campione del set di dati relativo alle corse e alle tariffe taxi della città di New York nel 2013.</span><span class="sxs-lookup"><span data-stu-id="a26f5-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="a26f5-105">Illustra i passaggi end-to-end del [processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess)usando un cluster HDInsight Spark per l'elaborazione e BLOB di Azure per l'archiviazione dei dati e dei modelli.</span><span class="sxs-lookup"><span data-stu-id="a26f5-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="a26f5-106">Il processo analizza e visualizza i dati ottenuti da un BLOB di Archiviazione di Azure e li prepara per la compilazione di modelli predittivi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="a26f5-107">I modelli vengono compilati con il toolkit MLlib di Spark per l'esecuzione di attività di classificazione binaria e modellazione basata sulla regressione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="a26f5-108">L'attività di **classificazione binaria** consente di prevedere se per la corsa viene lasciata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="a26f5-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="a26f5-109">L'attività di **regressione** consente di prevedere l'importo della mancia in base ad altre funzionalità relative alle mance.</span><span class="sxs-lookup"><span data-stu-id="a26f5-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="a26f5-110">I modelli proposti includono la regressione logistica e lineare, foreste casuali e alberi con boosting a gradienti:</span><span class="sxs-lookup"><span data-stu-id="a26f5-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="a26f5-111">[Regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che si serve di un metodo di discesa del gradiente stocastico (SGD, Stochastic Gradient Descent), usato per l'ottimizzazione e il ridimensionamento delle funzionalità allo scopo di prevedere l'importo delle mance pagate.</span><span class="sxs-lookup"><span data-stu-id="a26f5-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="a26f5-112">[Regressione logistica con L-BFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) , o regressione "logit", è un modello di regressione che può essere usato quando la variabile dipendente usata per la classificazione dei dati è categoriale.</span><span class="sxs-lookup"><span data-stu-id="a26f5-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="a26f5-113">L'algoritmo L-BFGS è un algoritmo di ottimizzazione quasi-Newton che approssima l'algoritmo di Broyden-Fletcher-Goldfarb-Shanno (BFGS) usando una quantità limitata di memoria del computer ed è ampiamente usato nell'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="a26f5-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="a26f5-114">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="a26f5-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="a26f5-115">Queste foreste combinano diversi alberi delle decisioni per ridurre il rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="a26f5-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="a26f5-116">Le foreste casuali vengono usate per la classificazione e la regressione, sono in grado di gestire funzionalità relative alle categorie e possono essere estese all'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="a26f5-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="a26f5-117">Non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a26f5-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="a26f5-118">Le foreste casuali sono tra i modelli di apprendimento automatico più diffusi per la classificazione e la regressione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="a26f5-119">[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="a26f5-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="a26f5-120">Gli alberi GBT eseguono il training degli alberi delle decisioni in modo iterativo per ridurre al minimo la perdita di funzioni.</span><span class="sxs-lookup"><span data-stu-id="a26f5-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="a26f5-121">Gli alberi GBT vengono usati per la classificazione e la regressione e possono gestire funzionalità categoriche, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a26f5-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="a26f5-122">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="a26f5-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="a26f5-123">La procedura di modellazione include anche codice che illustra come eseguire il training, la valutazione e il salvataggio di ogni tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="a26f5-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="a26f5-124">Per il codice della soluzione e per visualizzare i relativi tracciati è stato usato Python.</span><span class="sxs-lookup"><span data-stu-id="a26f5-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="a26f5-125">Anche se il toolkit Spark MLlib è progettato per funzionare con set di dati di grandi dimensioni, per maggiore praticità viene usato un campione relativamente ridotto, di circa 30 Mb con 170.000 righe, ovvero lo 0,1% circa del set di dati originale della città di New York.</span><span class="sxs-lookup"><span data-stu-id="a26f5-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="a26f5-126">L'esercizio qui proposto viene eseguito in modo efficiente in un cluster HDInsight con 2 nodi di lavoro, in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="a26f5-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="a26f5-127">Lo stesso codice può essere usato per elaborare set di dati di dimensioni maggiori, con poche modifiche appropriate per il caching dei dati in memoria e la modifica delle dimensioni del cluster.</span><span class="sxs-lookup"><span data-stu-id="a26f5-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a26f5-128">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a26f5-128">Prerequisites</span></span>
<span data-ttu-id="a26f5-129">Per completare questa procedura dettagliata sono necessari un account Azure e un cluster HDInsight Spark 1.6 o 2.0.</span><span class="sxs-lookup"><span data-stu-id="a26f5-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="a26f5-130">Per istruzioni su come soddisfare questi requisiti, vedere [Panoramica dell'analisi scientifica dei dati con Spark in Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a26f5-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="a26f5-131">Questo argomento contiene inoltre una descrizione dei dati dei taxi di NYC per il 2013 usati qui e istruzioni su come eseguire il codice da un notebook Jupyter nel cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="a26f5-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="a26f5-132">Notebook e cluster Spark</span><span class="sxs-lookup"><span data-stu-id="a26f5-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="a26f5-133">La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="a26f5-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="a26f5-134">Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a26f5-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="a26f5-135">+Vengono inoltre forniti una descrizione dei notebook e i relativi collegamenti nel [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository GitHub che li contiene.</span><span class="sxs-lookup"><span data-stu-id="a26f5-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="a26f5-136">Inoltre, il codice in questo esempio e nei notebook collegati è generico e funzionerà in qualsiasi cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="a26f5-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="a26f5-137">Se non si usa HDInsight Spark, i passaggi di configurazione e gestione del cluster possono essere leggermente diversi rispetto a quanto illustrato qui.</span><span class="sxs-lookup"><span data-stu-id="a26f5-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="a26f5-138">Per praticità, ecco i collegamenti per i notebook di Jupyter per Spark 1.6 (da eseguire nel kernek di pySpark del server Notebook di Jupyter) e Spark 2.0 (da eseguire nel kernel di pySpark3 del server Notebook di Jupyter):</span><span class="sxs-lookup"><span data-stu-id="a26f5-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="a26f5-139">Notebook Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="a26f5-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="a26f5-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornisce informazioni su come eseguire l'esplorazione dei dati, la modellazione e l'assegnazione del punteggio con diversi algoritmi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="a26f5-141">Notebook Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="a26f5-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="a26f5-142">Le attività di classificazione e regressione implementate con un cluster Spark 2.0 si trovano in notebook diversi e il notebook di classificazione usa un dataset diverso:</span><span class="sxs-lookup"><span data-stu-id="a26f5-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="a26f5-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come eseguire l'esplorazione dei dati, la modellazione e l'assegnazione del punteggio nei cluster Spark 2.0 usando i dati relativi alle corse e alle tariffe dei taxi di NYC descritti [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="a26f5-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="a26f5-144">Questo notebook può essere un buon punto di partenza per esplorare velocemente il codice fornito per Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a26f5-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="a26f5-145">Per un notebook più dettagliato che analizza i dati dei taxi di NYC, vedere il notebook successivo di questo elenco.</span><span class="sxs-lookup"><span data-stu-id="a26f5-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="a26f5-146">Vedere le note dopo l'elenco che confrontano questi notebook.</span><span class="sxs-lookup"><span data-stu-id="a26f5-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="a26f5-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): questo file mostra come eseguire la gestione dei dati (Spark SQL e operazioni del frame di dati), l'esplorazione, il modellamento e l'assegnazione del punteggio utilizzando il set di dati delle corse e delle tariffe dei taxi di NYC descritti [qui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="a26f5-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="a26f5-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): questo file mostra come eseguire la gestione dei dati (Spark SQL e operazioni del frame di dati), l'esplorazione, il modellamento e l'assegnazione del punteggio utilizzando il set di dati relativi alle partenze puntuali dei voli del 2011 e 2012 di una compagnia area.</span><span class="sxs-lookup"><span data-stu-id="a26f5-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="a26f5-149">Abbiamo integrato il set di dati della compagnia aerea con i dati delle condizioni atmosferiche dell'aeroporto (ad esempio, velocità del vento, temperatura, altitudine e così via) prima del modellamento, in modo da poterli includere nel modello.</span><span class="sxs-lookup"><span data-stu-id="a26f5-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="a26f5-150">Il set di dati della compagnia aerea è stato aggiunto ai notebook Spark 2.0 per illustrare al meglio l'uso degli algoritmi di classificazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="a26f5-151">Vedere i collegamenti seguenti per informazioni sul set di dati delle partenze puntuali dei voli della compagnia aerea e sul set di dati delle condizioni atmosferiche:</span><span class="sxs-lookup"><span data-stu-id="a26f5-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="a26f5-152">Dati sulle partenze puntuali dei voli della compagnia aerea: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="a26f5-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="a26f5-153">Dati sulle condizioni atmosferiche dell'aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="a26f5-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="a26f5-154">L'esecuzione dei notebook Spark 2.0 sui dati dei taxi di NYC e sui ritardi dei voli può impiegare 10 minuti o più (in base alla dimensione del cluster HDI).</span><span class="sxs-lookup"><span data-stu-id="a26f5-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="a26f5-155">Il primo notebook dell'elenco precedente illustra molti aspetti dell'esplorazione dei dati, della visualizzazione e dell'addestramento del modello ML in un notebook che richiede meno tempo di esecuzione con dataset di NYC ricampionati, in cui i file dei dati di taxi e tariffe sono stati precedentemente uniti: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) Questo notebook termina in un tempo molto più breve (2-3 minuti) e può essere un buon punto di partenza per esplorare rapidamente il codice fornito per Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="a26f5-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="a26f5-156">Le descrizioni riportate di seguito riguardano l'uso di Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="a26f5-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="a26f5-157">Per le versioni Spark 2.0 usare i notebook le cui descrizioni e collegamenti sono riportati sopra.</span><span class="sxs-lookup"><span data-stu-id="a26f5-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="a26f5-158">Configurazione: percorsi di archiviazione, librerie e contesto Spark preimpostato</span><span class="sxs-lookup"><span data-stu-id="a26f5-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="a26f5-159">Spark può eseguire operazioni di lettura e scrittura in BLOB di Archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="a26f5-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="a26f5-160">I dati esistenti archiviati in WASB possono essere elaborati con Spark e i relativi risultati possono essere memorizzati nuovamente in BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a26f5-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="a26f5-161">Per salvare file o modelli in WASB, è necessario specificare correttamente il percorso.</span><span class="sxs-lookup"><span data-stu-id="a26f5-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="a26f5-162">È possibile fare riferimento al contenitore predefinito collegato al cluster Spark usando un percorso che inizia con: "wasb///".</span><span class="sxs-lookup"><span data-stu-id="a26f5-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="a26f5-163">"wasb://" fa riferimento ad altri percorsi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="a26f5-164">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="a26f5-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="a26f5-165">L'esempio di codice seguente specifica il percorso dei dati da leggere e il percorso della directory di archiviazione del modello in cui viene salvato l'output del modello:</span><span class="sxs-lookup"><span data-stu-id="a26f5-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="a26f5-166">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="a26f5-166">Import libraries</span></span>
<span data-ttu-id="a26f5-167">Per la configurazione occorre anche importare le librerie necessarie.</span><span class="sxs-lookup"><span data-stu-id="a26f5-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="a26f5-168">Impostare il contesto Spark e importare le librerie necessarie usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="a26f5-168">Set spark context and import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="a26f5-169">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="a26f5-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="a26f5-170">I kernel PySpark forniti con i notebook di Jupyter hanno un contesto preimpostato,</span><span class="sxs-lookup"><span data-stu-id="a26f5-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="a26f5-171">quindi non è necessario impostare esplicitamente i contesti Spark o Hive prima di iniziare a usare l'applicazione in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="a26f5-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="a26f5-172">Questi contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="a26f5-172">These contexts are available for you by default.</span></span> <span data-ttu-id="a26f5-173">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="a26f5-173">These contexts are:</span></span>

* <span data-ttu-id="a26f5-174">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="a26f5-174">sc - for Spark</span></span> 
* <span data-ttu-id="a26f5-175">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="a26f5-175">sqlContext - for Hive</span></span>

<span data-ttu-id="a26f5-176">Il kernel PySpark offre alcuni “magic” predefiniti, ovvero comandi speciali che è possibile chiamare con %%.</span><span class="sxs-lookup"><span data-stu-id="a26f5-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="a26f5-177">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="a26f5-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="a26f5-178">**%%local**: specifica che il codice presente nelle righe successive deve essere eseguito localmente.</span><span class="sxs-lookup"><span data-stu-id="a26f5-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="a26f5-179">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="a26f5-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="a26f5-180">**%%sql -o <variable name>**: esegue una query Hive su sqlContext.</span><span class="sxs-lookup"><span data-stu-id="a26f5-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="a26f5-181">Se viene passato il parametro -o, il risultato della query viene salvato in modo permanente nel contesto Python %%local come frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="a26f5-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="a26f5-182">Per altre informazioni sui kernel per i notebook di Jupyter e i "magic" predefiniti messi a disposizione, vedere [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md) (Kernel disponibili per i notebook di Jupyter con cluster Apache Spark in HDInsight Linux).</span><span class="sxs-lookup"><span data-stu-id="a26f5-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="a26f5-183">Inserimento di dati dal BLOB pubblico</span><span class="sxs-lookup"><span data-stu-id="a26f5-183">Data ingestion from public blob</span></span>
<span data-ttu-id="a26f5-184">Il primo passaggio del processo di analisi scientifica dei dati consiste nel prelevare i dati da analizzare dalle origini in cui si trovano e inserirli nell'ambiente di modellazione ed esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="a26f5-185">In questa procedura dettagliata l'ambiente è Spark.</span><span class="sxs-lookup"><span data-stu-id="a26f5-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="a26f5-186">Questa sezione contiene il codice per completare una serie di attività:</span><span class="sxs-lookup"><span data-stu-id="a26f5-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="a26f5-187">Inserimento del campione di dati da modellare.</span><span class="sxs-lookup"><span data-stu-id="a26f5-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="a26f5-188">Lettura del set di dati di input archiviato come file TSV.</span><span class="sxs-lookup"><span data-stu-id="a26f5-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="a26f5-189">Formattazione e pulizia dei dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-189">format and clean the data</span></span>
* <span data-ttu-id="a26f5-190">Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="a26f5-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="a26f5-191">Registrazione come tabella temporanea in un contesto SQL.</span><span class="sxs-lookup"><span data-stu-id="a26f5-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="a26f5-192">Di seguito è riportato il codice per l'inserimento di dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="a26f5-193">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-193">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-194">Tempo impiegato per eseguire questa cella: 51,72 secondi</span><span class="sxs-lookup"><span data-stu-id="a26f5-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="a26f5-195">Visualizzazione ed esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="a26f5-195">Data exploration & visualization</span></span>
<span data-ttu-id="a26f5-196">Dopo aver inserito i dati in Spark, il passaggio successivo del processo di analisi scientifica dei dati consiste nell'esplorazione e nella visualizzazione dei dati per approfondirne la conoscenza.</span><span class="sxs-lookup"><span data-stu-id="a26f5-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="a26f5-197">In questa sezione vengono esaminati i dati relativi ai taxi tramite query SQL e vengono tracciate le variabili di destinazione e le funzionalità potenziali per l'esame visivo.</span><span class="sxs-lookup"><span data-stu-id="a26f5-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="a26f5-198">In particolare, viene tracciata la frequenza del numero di passeggeri nelle corse dei taxi, la frequenza dell'importo delle mance e la variazione delle mance in base al tipo e all'importo del pagamento.</span><span class="sxs-lookup"><span data-stu-id="a26f5-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="a26f5-199">Tracciare un istogramma delle frequenze del numero di passeggeri nel campione di corse dei taxi</span><span class="sxs-lookup"><span data-stu-id="a26f5-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="a26f5-200">Questo codice e i frammenti di codice successivi usano un magic SQL per eseguire una query sul campione e un magic local per tracciare i dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="a26f5-201">**Magic SQL (`%%sql`)**: il kernel HDInsight PySpark supporta l'esecuzione di query HiveQL inline semplici su sqlContext.</span><span class="sxs-lookup"><span data-stu-id="a26f5-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="a26f5-202">L'argomento (-o NOME_VARIABILE) salva in modo permanente l'output della query SQL come frame di dati Pandas nel server Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a26f5-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="a26f5-203">Questo significa che è disponibile in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="a26f5-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="a26f5-204">Il **`%%local`** viene usato per eseguire il codice in locale nel server Jupyter, che costituisce il nodo head del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a26f5-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="a26f5-205">In genere si usa il magic `%%local` in combinazione con il magic `%%sql` con il parametro -o.</span><span class="sxs-lookup"><span data-stu-id="a26f5-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="a26f5-206">Il parametro -o rende persistente l'output della query SQL a livello locale e quindi il magic %%local attiva il successivo set di frammenti di codice che viene eseguito localmente a fronte dell'output della query SQL persistente a livello locale.</span><span class="sxs-lookup"><span data-stu-id="a26f5-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="a26f5-207">L'output viene visualizzato automaticamente dopo aver eseguito il codice.</span><span class="sxs-lookup"><span data-stu-id="a26f5-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="a26f5-208">Questa query recupera le corse per numero di passeggeri.</span><span class="sxs-lookup"><span data-stu-id="a26f5-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="a26f5-209">Questo codice crea un frame di dati locale dall'output della query ed esegue il tracciato dei dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="a26f5-210">Il magic `%%local` crea un frame di dati locale, `sqlResults`, che può essere usato per eseguire tracciati con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="a26f5-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="a26f5-211">Tale magic PySpark viene usato più volte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="a26f5-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="a26f5-212">In caso di un'elevata quantità di dati, è consigliabile campionare i dati in modo da creare un frame che possa essere contenuto nella memoria locale.</span><span class="sxs-lookup"><span data-stu-id="a26f5-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="a26f5-213">Ecco il codice per eseguire il tracciato delle corse per numero di passeggeri</span><span class="sxs-lookup"><span data-stu-id="a26f5-213">Here is the code to plot the trips by passenger counts</span></span>

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

<span data-ttu-id="a26f5-214">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-214">**OUTPUT:**</span></span>

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="a26f5-216">È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, a linee, ad area o a barre) usando i pulsanti del menu **Type** (Tipo) nel notebook.</span><span class="sxs-lookup"><span data-stu-id="a26f5-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="a26f5-217">In questo caso è stato scelto un tracciato a barre.</span><span class="sxs-lookup"><span data-stu-id="a26f5-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="a26f5-218">Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.</span><span class="sxs-lookup"><span data-stu-id="a26f5-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="a26f5-219">Usare una query SQL per campionare i dati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
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


<span data-ttu-id="a26f5-220">Questa cella di codice usa la query SQL per creare tre tracciati.</span><span class="sxs-lookup"><span data-stu-id="a26f5-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
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


<span data-ttu-id="a26f5-221">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-221">**OUTPUT:**</span></span> 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="a26f5-225">Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione</span><span class="sxs-lookup"><span data-stu-id="a26f5-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="a26f5-226">Questa sezione descrive le procedure usate per preparare i dati da usare nella modellazione per l'apprendimento automatico, fornisce il relativo codice e</span><span class="sxs-lookup"><span data-stu-id="a26f5-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="a26f5-227">illustra come eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="a26f5-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="a26f5-228">Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="a26f5-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="a26f5-229">Indicizzare e codificare funzionalità categoriche</span><span class="sxs-lookup"><span data-stu-id="a26f5-229">Index and encode categorical features</span></span>
* <span data-ttu-id="a26f5-230">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="a26f5-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="a26f5-231">Creare un sottocampionamento casuale dei dati e dividerlo in set di training e di testing</span><span class="sxs-lookup"><span data-stu-id="a26f5-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="a26f5-232">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="a26f5-232">Feature scaling</span></span>
* <span data-ttu-id="a26f5-233">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="a26f5-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="a26f5-234">Ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="a26f5-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="a26f5-235">Questo codice illustra come ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto e come memorizzare nella cache il frame di dati risultante in memoria.</span><span class="sxs-lookup"><span data-stu-id="a26f5-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="a26f5-236">Quando si usano ripetutamente RDD (Resilient Distributed Dataset) e frame di dati, la memorizzazione nella cache consente di migliorare i tempi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="a26f5-237">RDD e frame di dati vengono quindi memorizzati nella cache in varie fasi di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="a26f5-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

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
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="a26f5-238">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-238">**OUTPUT:**</span></span> 

<span data-ttu-id="a26f5-239">126050</span><span class="sxs-lookup"><span data-stu-id="a26f5-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="a26f5-240">Indicizzare e codificare funzionalità categoriche per l'inserimento in funzioni di modellazione</span><span class="sxs-lookup"><span data-stu-id="a26f5-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="a26f5-241">Questa sezione illustra come indicizzare o codificare le funzionalità categoriche per l'inserimento nelle funzioni di modellazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="a26f5-242">Per poter usare le funzioni di modellazione e previsione di MLlib, è necessario prima indicizzare o codificare le funzionalità con dati di input categorici.</span><span class="sxs-lookup"><span data-stu-id="a26f5-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="a26f5-243">A seconda del modello, è necessario indicizzare o codificare tali funzioni in modi diversi:</span><span class="sxs-lookup"><span data-stu-id="a26f5-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="a26f5-244">**Modelli basati su albero**: richiedono la codifica delle categorie come valori numerici (ad esempio, una funzionalità con tre categorie può essere codificata con 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="a26f5-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="a26f5-245">Questo avviene tramite la funzione [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) di MLlib,</span><span class="sxs-lookup"><span data-stu-id="a26f5-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="a26f5-246">che codifica una colonna stringa di etichette in una colonna di indici etichetta ordinati in base alle frequenze di etichetta.</span><span class="sxs-lookup"><span data-stu-id="a26f5-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="a26f5-247">Anche se viene usata l'indicizzazione con valori numerici per l'input e la gestione dei dati, è possibile specificare gli algoritmi basati su albero affinché trattino questi elementi in modo appropriato come categorie.</span><span class="sxs-lookup"><span data-stu-id="a26f5-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="a26f5-248">I **modelli logistici e di regressione lineare** richiedono la codifica one-hot in cui, ad esempio, una funzionalità con tre categorie può essere espansa in tre colonne delle funzionalità, in cui ogni colonna contiene 0 o 1, a seconda della categoria di un'osservazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="a26f5-249">Per eseguire la codifica one-hot in MLlib è disponibile la funzione [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder).</span><span class="sxs-lookup"><span data-stu-id="a26f5-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="a26f5-250">Questo codificatore esegue il mapping di una colonna di indici etichetta a una colonna di vettori binari, con al massimo un singolo valore unico.</span><span class="sxs-lookup"><span data-stu-id="a26f5-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="a26f5-251">Questa codifica permette di applicare a funzionalità categoriche gli algoritmi che prevedono funzionalità con valori numerici, ad esempio la regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="a26f5-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="a26f5-252">Di seguito è riportato il codice per l'indicizzazione e la codifica delle funzionalità categoriche:</span><span class="sxs-lookup"><span data-stu-id="a26f5-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-253">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-253">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-254">Tempo impiegato per eseguire questa cella: 1,28 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="a26f5-255">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="a26f5-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="a26f5-256">Questa sezione contiene codice che illustra come indicizzare dati di testo categorici come tipo di dati punto etichettato e codificarli per l'uso per il training e il testing della regressione logistica MLlib e di altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="a26f5-257">Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="a26f5-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="a26f5-258">Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.</span><span class="sxs-lookup"><span data-stu-id="a26f5-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="a26f5-259">Questa sezione contiene un codice che illustra come indicizzare dati di testo categorici come dati di tipo [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) e codificarli per l'uso a scopo di training e testing della regressione logistica MLlib e di altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="a26f5-260">Gli oggetti punto etichettato RDD (Resilient Distributed Dataset) costituiti da un'etichetta, o variabile di destinazione/risposta, e da un vettore di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a26f5-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="a26f5-261">Questo formato è richiesto come input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="a26f5-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="a26f5-262">Ecco il codice per indicizzare e codificare le funzionalità di testo per la classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="a26f5-262">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="a26f5-263">Ecco il codice per codificare e indicizzare le funzionalità di testo categoriche per l'analisi di regressione lineare.</span><span class="sxs-lookup"><span data-stu-id="a26f5-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="a26f5-264">Creare un sottocampionamento casuale dei dati e dividerlo in set di training e di testing</span><span class="sxs-lookup"><span data-stu-id="a26f5-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="a26f5-265">Questo codice crea un campionamento casuale dei dati, qui viene usato il 25%.</span><span class="sxs-lookup"><span data-stu-id="a26f5-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="a26f5-266">Anche se non è necessario per questo esempio, date le dimensioni del set di dati, viene illustrato come eseguire il campionamento e come usarlo quando necessario.</span><span class="sxs-lookup"><span data-stu-id="a26f5-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="a26f5-267">Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli.</span><span class="sxs-lookup"><span data-stu-id="a26f5-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="a26f5-268">Successivamente il campione viene suddiviso in un set di training (75%) e un set di testing (25%) da usare nei modelli di regressione e classificazione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-269">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-269">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-270">Tempo impiegato per eseguire questa cella: 0,24 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="a26f5-271">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="a26f5-271">Feature scaling</span></span>
<span data-ttu-id="a26f5-272">Il ridimensionamento di funzionalità, noto anche come normalizzazione dei dati, permette di fare in modo che alle funzionalità con valori molto dispersi non venga attribuito un peso eccessivo nella funzione obiettivo.</span><span class="sxs-lookup"><span data-stu-id="a26f5-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="a26f5-273">Per ridimensionare le funzionalità alla varianza unitaria, il relativo codice usa [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) .</span><span class="sxs-lookup"><span data-stu-id="a26f5-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="a26f5-274">Viene fornito da MLlib per l'uso nella regressione lineare con la discesa del gradiente stocastica (SGD), un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="a26f5-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="a26f5-275">L'algoritmo LinearRegressionWithSGD è risultato sensibile al ridimensionamento di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="a26f5-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="a26f5-276">Ecco il codice per ridimensionare le variabili per l'uso con l'algoritmo SGD lineare regolarizzato.</span><span class="sxs-lookup"><span data-stu-id="a26f5-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-277">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-277">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-278">Tempo impiegato per eseguire questa cella: 13,17 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="a26f5-279">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="a26f5-279">Cache objects in memory</span></span>
<span data-ttu-id="a26f5-280">Il caching degli oggetti del frame di dati di input usati per la classificazione, la regressione e le funzionalità con ridimensionamento permette di ridurre il tempo impiegato per il training e il testing degli algoritmi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a26f5-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-281">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-281">**OUTPUT:**</span></span> 

<span data-ttu-id="a26f5-282">Tempo impiegato per eseguire questa cella: 0,15 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="a26f5-283">Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia</span><span class="sxs-lookup"><span data-stu-id="a26f5-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="a26f5-284">Questa sezione illustra come usare tre modelli per l'attività di classificazione binaria di previsione di una possibile mancia lasciata per una corsa in taxi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="a26f5-285">I modelli presentati sono:</span><span class="sxs-lookup"><span data-stu-id="a26f5-285">The models presented are:</span></span>

* <span data-ttu-id="a26f5-286">Regressione logistica regolarizzata.</span><span class="sxs-lookup"><span data-stu-id="a26f5-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="a26f5-287">Modello di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="a26f5-287">Random forest model</span></span>
* <span data-ttu-id="a26f5-288">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="a26f5-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="a26f5-289">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="a26f5-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="a26f5-290">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="a26f5-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="a26f5-291">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="a26f5-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="a26f5-292">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="a26f5-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="a26f5-293">Classificazione tramite regressione logistica</span><span class="sxs-lookup"><span data-stu-id="a26f5-293">Classification using logistic regression</span></span>
<span data-ttu-id="a26f5-294">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di regressione logistica con l'algoritmo [L-BFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo alle corse e tariffe dei taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="a26f5-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="a26f5-295">**Eseguire il training del modello di regressione logistica usando la convalida incrociata e lo sweep degli iperparametri**</span><span class="sxs-lookup"><span data-stu-id="a26f5-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="a26f5-296">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-296">**OUTPUT:**</span></span> 

<span data-ttu-id="a26f5-297">Coefficienti: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="a26f5-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="a26f5-298">Intercetta: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="a26f5-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="a26f5-299">Tempo impiegato per eseguire questa cella: 14,43 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="a26f5-300">**Valutare il modello di classificazione binaria con le metriche standard**</span><span class="sxs-lookup"><span data-stu-id="a26f5-300">**Evaluate the binary classification model with standard metrics**</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="a26f5-301">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-301">**OUTPUT:**</span></span> 

<span data-ttu-id="a26f5-302">Area in PR = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="a26f5-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="a26f5-303">Area in ROC = 0,983714670256</span><span class="sxs-lookup"><span data-stu-id="a26f5-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="a26f5-304">Statistiche di riepilogo</span><span class="sxs-lookup"><span data-stu-id="a26f5-304">Summary Stats</span></span>

<span data-ttu-id="a26f5-305">Precisione = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="a26f5-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="a26f5-306">Richiamo = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="a26f5-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="a26f5-307">Punteggio F1 = 0,984304060189</span><span class="sxs-lookup"><span data-stu-id="a26f5-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="a26f5-308">Tempo impiegato per eseguire questa cella: 57,61 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="a26f5-309">**Tracciare la curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="a26f5-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="a26f5-310">L'oggetto *predictionAndLabelsDF* viene registrato come tabella, *tmp_results*, nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="a26f5-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="a26f5-311">L'oggetto *tmp_results* può essere usato per eseguire query e restituire i risultati nel frame di dati sqlResults per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="a26f5-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="a26f5-312">Ecco il codice.</span><span class="sxs-lookup"><span data-stu-id="a26f5-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="a26f5-313">Ecco il codice per eseguire stime e tracciare la curva ROC.</span><span class="sxs-lookup"><span data-stu-id="a26f5-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="a26f5-314">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="a26f5-316">Classificazione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="a26f5-316">Random forest classification</span></span>
<span data-ttu-id="a26f5-317">Il codice riportato in questa sezione illustra come eseguire il training, la valutazione e il salvataggio di un modello di foresta casuale, che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo a corse e tariffe dei taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="a26f5-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-318">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-318">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-319">Area in ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="a26f5-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="a26f5-320">Tempo impiegato per eseguire questa cella: 31,09 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="a26f5-321">Classificazione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="a26f5-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="a26f5-322">Il codice riportato in questa sezione illustra come eseguire il training, la valutazione e il salvataggio di un modello di alberi con boosting a gradienti, che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo a corse e tariffe dei taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="a26f5-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="a26f5-323">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-323">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-324">Area in ROC = 0,985297691373</span><span class="sxs-lookup"><span data-stu-id="a26f5-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="a26f5-325">Tempo impiegato per eseguire questa cella: 19,76 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="a26f5-326">Uso di modelli regressivi per prevedere l'importo delle mance per le corse in taxi</span><span class="sxs-lookup"><span data-stu-id="a26f5-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="a26f5-327">Questa sezione illustra come usare tre modelli per l'attività di regressione relativa alla previsione dell'importo della mancia lasciata per una corsa in taxi in base ad altre funzionalità relative alle mance.</span><span class="sxs-lookup"><span data-stu-id="a26f5-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="a26f5-328">I modelli presentati sono:</span><span class="sxs-lookup"><span data-stu-id="a26f5-328">The models presented are:</span></span>

* <span data-ttu-id="a26f5-329">Regressione lineare regolarizzata</span><span class="sxs-lookup"><span data-stu-id="a26f5-329">Regularized linear regression</span></span>
* <span data-ttu-id="a26f5-330">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="a26f5-330">Random forest</span></span>
* <span data-ttu-id="a26f5-331">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="a26f5-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="a26f5-332">Questi modelli sono stati descritti nell'introduzione.</span><span class="sxs-lookup"><span data-stu-id="a26f5-332">These models were described in the introduction.</span></span> <span data-ttu-id="a26f5-333">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="a26f5-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="a26f5-334">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="a26f5-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="a26f5-335">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="a26f5-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="a26f5-336">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="a26f5-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="a26f5-337">Regressione lineare con SGD</span><span class="sxs-lookup"><span data-stu-id="a26f5-337">Linear regression with SGD</span></span>
<span data-ttu-id="a26f5-338">Il codice riportato in questa sezione illustra come usare le funzionalità con ridimensionamento per il training di una regressione lineare che usa la discesa del gradiente stocastica (SGD) per l'ottimizzazione e come assegnare punteggi, valutare e salvare il modello in BLOB di Archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="a26f5-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="a26f5-339">La convergenza di modelli LinearRegressionWithSGD può risultare problematica ed è necessario modificare oppure ottimizzare attentamente i parametri per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="a26f5-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="a26f5-340">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="a26f5-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-341">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-341">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-342">Coefficienti: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="a26f5-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="a26f5-343">Intercetta: -0,853872718283</span><span class="sxs-lookup"><span data-stu-id="a26f5-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="a26f5-344">RMSE = 1,24190115863</span><span class="sxs-lookup"><span data-stu-id="a26f5-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="a26f5-345">R-sqr = 0,608017146081</span><span class="sxs-lookup"><span data-stu-id="a26f5-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="a26f5-346">Tempo impiegato per eseguire questa cella: 58,42 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="a26f5-347">Regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="a26f5-347">Random Forest regression</span></span>
<span data-ttu-id="a26f5-348">Il codice riportato in questa sezione illustra come eseguire il training, la valutazione e il salvataggio di una regressione tramite foresta casuale, che consente di prevedere l'importo della mancia per i dati relativi alle corse in taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="a26f5-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-349">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-349">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-350">RMSE = 0,891209218139</span><span class="sxs-lookup"><span data-stu-id="a26f5-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="a26f5-351">R-sqr = 0,759661334921</span><span class="sxs-lookup"><span data-stu-id="a26f5-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="a26f5-352">Tempo impiegato per eseguire questa cella: 49,21 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="a26f5-353">Regressione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="a26f5-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="a26f5-354">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di alberi con boosting a gradienti, che consente di prevedere l'importo della mancia per il set di dati relativo alle corse in taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="a26f5-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="a26f5-355">* * Eseguire il training e valutare * *</span><span class="sxs-lookup"><span data-stu-id="a26f5-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="a26f5-356">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-356">**OUTPUT:**</span></span>

<span data-ttu-id="a26f5-357">RMSE = 0,908473148639</span><span class="sxs-lookup"><span data-stu-id="a26f5-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="a26f5-358">R-sqr = 0,753835096681</span><span class="sxs-lookup"><span data-stu-id="a26f5-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="a26f5-359">Tempo impiegato per eseguire questa cella: 34,52 secondi.</span><span class="sxs-lookup"><span data-stu-id="a26f5-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="a26f5-360">**Grafico**</span><span class="sxs-lookup"><span data-stu-id="a26f5-360">**Plot**</span></span>

<span data-ttu-id="a26f5-361">L'oggetto *tmp_results* viene registrato come tabella Hive nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="a26f5-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="a26f5-362">I risultati della tabella vengono restituiti nel frame di dati *sqlResults* per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="a26f5-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="a26f5-363">Ecco il codice</span><span class="sxs-lookup"><span data-stu-id="a26f5-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="a26f5-364">Ecco il codice per tracciare i dati usando il server Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a26f5-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="a26f5-365">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="a26f5-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="a26f5-367">Pulire gli oggetti dalla memoria</span><span class="sxs-lookup"><span data-stu-id="a26f5-367">Clean up objects from memory</span></span>
<span data-ttu-id="a26f5-368">Usare `unpersist()` per eliminare gli oggetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="a26f5-368">Use `unpersist()` to delete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="a26f5-369">Registrazione dei percorsi di archiviazione dei modelli per l'utilizzo e l'assegnazione di punteggi</span><span class="sxs-lookup"><span data-stu-id="a26f5-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="a26f5-370">Per l'assegnazione di punteggi e l'utilizzo di un set di dati indipendente descritto nell'argomento [Assegnare punteggi a modelli di apprendimento automatico compilati con Spark](machine-learning-data-science-spark-model-consumption.md), è necessario copiare e incollare questi nomi di file che contengono i modelli salvati, creati qui nel notebook di Jupyter.</span><span class="sxs-lookup"><span data-stu-id="a26f5-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="a26f5-371">Di seguito è riportato il codice per stampare i percorsi dei file di modello necessari.</span><span class="sxs-lookup"><span data-stu-id="a26f5-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="a26f5-372">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="a26f5-372">**OUTPUT**</span></span>

<span data-ttu-id="a26f5-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="a26f5-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="a26f5-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="a26f5-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="a26f5-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="a26f5-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="a26f5-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="a26f5-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="a26f5-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="a26f5-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="a26f5-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="a26f5-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="a26f5-379">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a26f5-379">What's next?</span></span>
<span data-ttu-id="a26f5-380">Dopo aver creato i modelli regressivi e di classificazione con MlLib di Spark, è possibile imparare a valutare e assegnare punteggi a questi modelli.</span><span class="sxs-lookup"><span data-stu-id="a26f5-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="a26f5-381">Il notebook per la modellazione e l'esplorazione avanzata dei dati approfondisce la convalida incrociata, lo sweep degli iperparametri e la valutazione del modello.</span><span class="sxs-lookup"><span data-stu-id="a26f5-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="a26f5-382">**Uso dei modelli:** per informazioni su come valutare e assegnare punteggi ai modelli di regressione e di classificazione creati in questo argomento, vedere [Assegnare punteggi a modelli di apprendimento automatico compilati con Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="a26f5-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="a26f5-383">**Convalida incrociata e sweep di iperparametri**: vedere [Esplorazione e modellazione avanzate dei dati con Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) per informazioni su come istruire i modelli sulla convalida incrociata e lo sweep di iperparametri</span><span class="sxs-lookup"><span data-stu-id="a26f5-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

