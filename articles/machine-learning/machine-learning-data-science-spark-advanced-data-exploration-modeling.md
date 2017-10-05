---
title: Esplorazione e modellazione avanzate dei dati con Spark | Documentazione Microsoft
description: Usare HDInsight Spark per eseguire l'esplorazione dei dati e il training dei modelli di classificazione binaria e regressione usando la convalida incrociata e l'ottimizzazione di iperparametri.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="99f0f-103">Esplorazione e modellazione avanzate dei dati con Spark</span><span class="sxs-lookup"><span data-stu-id="99f0f-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="99f0f-104">Questa procedura dettagliata usa HDInsight Spark per eseguire l'esplorazione dei dati e il training dei modelli di classificazione binaria e regressione usando la convalida incrociata e l'ottimizzazione di iperparametri su un campione del set di dati relativo alle corse e alle tariffe dei taxi della città di New York nel 2013.</span><span class="sxs-lookup"><span data-stu-id="99f0f-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="99f0f-105">Illustra i passaggi end-to-end del [processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess)usando un cluster HDInsight Spark per l'elaborazione e BLOB di Azure per l'archiviazione dei dati e dei modelli.</span><span class="sxs-lookup"><span data-stu-id="99f0f-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="99f0f-106">Il processo analizza e visualizza i dati ottenuti da un BLOB di Archiviazione di Azure e li prepara per la compilazione di modelli predittivi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="99f0f-107">Per il codice della soluzione e per visualizzare i relativi tracciati è stato usato Python.</span><span class="sxs-lookup"><span data-stu-id="99f0f-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="99f0f-108">I modelli vengono compilati con il toolkit MLlib di Spark per l'esecuzione di attività di classificazione binaria e modellazione basata sulla regressione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="99f0f-109">L'attività di **classificazione binaria** consente di prevedere se per la corsa viene lasciata o meno una mancia.</span><span class="sxs-lookup"><span data-stu-id="99f0f-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="99f0f-110">L'attività di **regressione** consente di prevedere l'importo della mancia in base ad altre funzionalità relative alle mance.</span><span class="sxs-lookup"><span data-stu-id="99f0f-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="99f0f-111">La procedura di modellazione include anche un codice che illustra come eseguire il training, valutare e salvare ogni tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="99f0f-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="99f0f-112">Nell'argomento vengono illustrati alcuni aspetti comuni all'argomento [Modellazione ed esplorazione dei dati con Spark](machine-learning-data-science-spark-data-exploration-modeling.md).</span><span class="sxs-lookup"><span data-stu-id="99f0f-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="99f0f-113">Tuttavia, questo argomento è più "avanzato" nel senso che usa anche la convalida incrociata con la ricerca di iperparametri per formare modelli precisi di classificazione e regressione in modo ottimale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="99f0f-114">La **convalida incrociata** è una tecnica che consente di valutare in che modo un modello con training eseguito su un set di dati noto viene generalizzato per stimare le funzionalità di set di dati su cui non è stato eseguito il training.</span><span class="sxs-lookup"><span data-stu-id="99f0f-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="99f0f-115">Un'implementazione comune usata qui consiste nel dividere un set di dati in K riduzioni e quindi eseguire il training del modello in base a uno schema round robin su tutte le riduzioni eccetto una.</span><span class="sxs-lookup"><span data-stu-id="99f0f-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="99f0f-116">Viene valutata la capacità del modello di eseguire una stima accurata quando testata in confronto con il set di dati indipendenti in questa sezione non usata per il training del modello.</span><span class="sxs-lookup"><span data-stu-id="99f0f-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="99f0f-117">**ottimizzazione degli iperparametri** consiste nello scegliere un set di iperparametri per un algoritmo di apprendimento, in genere con l'obiettivo di ottimizzare una misura delle prestazioni dell'algoritmo su un set di dati indipendente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="99f0f-118">**iperparametri** sono valori che devono essere specificati al di fuori della procedura di training del modello.</span><span class="sxs-lookup"><span data-stu-id="99f0f-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="99f0f-119">I presupposti di questi valori possono influire sulla flessibilità e l'accuratezza dei modelli.</span><span class="sxs-lookup"><span data-stu-id="99f0f-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="99f0f-120">Gli alberi delle decisioni includono, ad esempio, iperparametri come la profondità desiderata e il numero di foglie nell'albero.</span><span class="sxs-lookup"><span data-stu-id="99f0f-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="99f0f-121">Le macchine a vettori di supporto (SVM, Support Vector Machine) richiedono l'impostazione di una penalità per errata classificazione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="99f0f-122">Un modo comune per eseguire l'ottimizzazione degli iperparametri usato in questo articolo è una ricerca nella griglia o **sweep di parametri**.</span><span class="sxs-lookup"><span data-stu-id="99f0f-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="99f0f-123">Si tratta di eseguire una ricerca completa nei valori di un subset specificato dello spazio degli iperparametri per un algoritmo di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="99f0f-124">La convalida incrociata può fornire metriche delle prestazioni per selezionare i risultati ottimali generati dall'algoritmo di ricerca nella griglia.</span><span class="sxs-lookup"><span data-stu-id="99f0f-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="99f0f-125">La convalida incrociata usata con lo sweep di iperparametri limita i problemi come l'overfitting di un modello rispetto ai dati di training, in modo che il modello mantenga la capacità di essere applicato al set di dati generale da cui sono stati estratti i dati di training.</span><span class="sxs-lookup"><span data-stu-id="99f0f-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="99f0f-126">I modelli proposti includono la regressione logistica e lineare, foreste casuali e alberi con boosting a gradienti:</span><span class="sxs-lookup"><span data-stu-id="99f0f-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="99f0f-127">[Regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che si serve di un metodo di discesa del gradiente stocastico (SGD, Stochastic Gradient Descent), usato per l'ottimizzazione e il ridimensionamento delle funzionalità allo scopo di prevedere l'importo delle mance pagate.</span><span class="sxs-lookup"><span data-stu-id="99f0f-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="99f0f-128">[Regressione logistica con L-BFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) , o regressione "logit", è un modello di regressione che può essere usato quando la variabile dipendente usata per la classificazione dei dati è categoriale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="99f0f-129">L'algoritmo L-BFGS è un algoritmo di ottimizzazione quasi-Newton che approssima l'algoritmo di Broyden-Fletcher-Goldfarb-Shanno (BFGS) usando una quantità limitata di memoria del computer ed è ampiamente usato nell'apprendimento automatico.</span><span class="sxs-lookup"><span data-stu-id="99f0f-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="99f0f-130">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="99f0f-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="99f0f-131">Queste foreste combinano diversi alberi delle decisioni per ridurre il rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="99f0f-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="99f0f-132">Le foreste casuali vengono usate per la classificazione e la regressione, sono in grado di gestire funzionalità relative alle categorie e possono essere estese all'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="99f0f-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="99f0f-133">Non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="99f0f-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="99f0f-134">Le foreste casuali sono tra i modelli di apprendimento automatico più diffusi per la classificazione e la regressione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="99f0f-135">[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="99f0f-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="99f0f-136">Gli alberi GBT eseguono il training degli alberi delle decisioni in modo iterativo per ridurre al minimo la perdita di funzioni.</span><span class="sxs-lookup"><span data-stu-id="99f0f-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="99f0f-137">Gli alberi GBT vengono usati per la classificazione e la regressione e possono gestire funzionalità categoriche, non richiedono il ridimensionamento delle funzionalità e possono rilevare non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="99f0f-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="99f0f-138">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="99f0f-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="99f0f-139">Esempi di modelli che usano la convalida incrociata e sweep di iperparametri sono illustrati per il problema della classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="99f0f-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="99f0f-140">Esempi più semplici, senza sweep di parametri, sono illustrati nell'argomento principale per le attività di regressione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="99f0f-141">Nell'appendice sono tuttavia descritte anche la convalida con Elastic Net per la regressione lineare e la convalida incrociata con sweep dei parametri per la regressione tramite foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="99f0f-142">**elastic net** è un metodo di regressione regolarizzata per l'adattamento di modelli di regressione lineare che combina in modo lineare le metriche L1 e L2 come penalità dei metodi [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization).</span><span class="sxs-lookup"><span data-stu-id="99f0f-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="99f0f-143">Anche se il toolkit Spark MLlib è progettato per funzionare con set di dati di grandi dimensioni, per maggiore praticità viene usato un campione relativamente ridotto di circa 30 Mb che usa 170.000 righe, ovvero lo 0,1% circa del set di dati originale di NYC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="99f0f-144">L'esercizio qui proposto viene eseguito in modo efficiente in un cluster HDInsight con 2 nodi di lavoro, in circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="99f0f-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="99f0f-145">Lo stesso codice può essere usato per elaborare set di dati di dimensioni maggiori, con poche modifiche appropriate per il caching dei dati in memoria e la modifica delle dimensioni del cluster.</span><span class="sxs-lookup"><span data-stu-id="99f0f-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="99f0f-146">Configurazione: notebook e cluster Spark</span><span class="sxs-lookup"><span data-stu-id="99f0f-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="99f0f-147">La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="99f0f-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="99f0f-148">Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="99f0f-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="99f0f-149">+Vengono inoltre forniti una descrizione dei notebook e i relativi collegamenti nel [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository GitHub che li contiene.</span><span class="sxs-lookup"><span data-stu-id="99f0f-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="99f0f-150">Inoltre, il codice in questo esempio e nei notebook collegati è generico e funzionerà in qualsiasi cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="99f0f-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="99f0f-151">Se non si usa HDInsight Spark, i passaggi di configurazione e gestione del cluster possono essere leggermente diversi rispetto a quanto illustrato qui.</span><span class="sxs-lookup"><span data-stu-id="99f0f-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="99f0f-152">Per praticità, ecco i collegamenti per il notebook di Jupyter per Spark 1.6 e 2.0 da eseguire nel kernel pyspark del server del notebook di Jupyter:</span><span class="sxs-lookup"><span data-stu-id="99f0f-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="99f0f-153">Notebook Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="99f0f-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="99f0f-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): include gli argomenti nel notebook numero 1 e modella lo sviluppo usando l'ottimizzazione degli iperparametri e la convalida incrociata.</span><span class="sxs-lookup"><span data-stu-id="99f0f-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="99f0f-155">Notebook Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="99f0f-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="99f0f-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come eseguire l'esplorazione dei dati, la modellazione e l'assegnazione del punteggio nei cluster Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="99f0f-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="99f0f-157">Configurazione: percorsi di archiviazione, librerie e contesto Spark preimpostato</span><span class="sxs-lookup"><span data-stu-id="99f0f-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="99f0f-158">Spark può eseguire operazioni di lettura e scrittura in BLOB di Archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="99f0f-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="99f0f-159">I dati esistenti archiviati in WASB possono essere elaborati con Spark e i relativi risultati possono essere memorizzati nuovamente in BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="99f0f-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="99f0f-160">Per salvare file o modelli in WASB, è necessario specificare correttamente il percorso.</span><span class="sxs-lookup"><span data-stu-id="99f0f-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="99f0f-161">È possibile fare riferimento al contenitore predefinito collegato al cluster Spark usando un percorso che inizia con: "wasb///".</span><span class="sxs-lookup"><span data-stu-id="99f0f-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="99f0f-162">"wasb://" fa riferimento ad altri percorsi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="99f0f-163">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="99f0f-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="99f0f-164">L'esempio di codice seguente specifica il percorso dei dati da leggere e il percorso della directory di archiviazione del modello in cui viene salvato l'output del modello.</span><span class="sxs-lookup"><span data-stu-id="99f0f-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="99f0f-165">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-165">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="99f0f-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="99f0f-167">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="99f0f-167">Import libraries</span></span>
<span data-ttu-id="99f0f-168">Importare le librerie necessarie usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="99f0f-168">Import necessary libraries with the following code:</span></span>

    # LOAD PYSPARK LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="99f0f-169">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="99f0f-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="99f0f-170">I kernel PySpark forniti con i notebook di Jupyter hanno un contesto preimpostato,</span><span class="sxs-lookup"><span data-stu-id="99f0f-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="99f0f-171">quindi non è necessario impostare esplicitamente i contesti Spark o Hive prima di iniziare a usare l'applicazione in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="99f0f-172">Questi contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="99f0f-172">These contexts are available for you by default.</span></span> <span data-ttu-id="99f0f-173">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="99f0f-173">These contexts are:</span></span>

* <span data-ttu-id="99f0f-174">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="99f0f-174">sc - for Spark</span></span> 
* <span data-ttu-id="99f0f-175">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="99f0f-175">sqlContext - for Hive</span></span>

<span data-ttu-id="99f0f-176">Il kernel PySpark offre alcuni “magic” predefiniti, ovvero comandi speciali che è possibile chiamare con %%.</span><span class="sxs-lookup"><span data-stu-id="99f0f-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="99f0f-177">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="99f0f-178">**%%local**: specifica che il codice presente nelle righe successive deve essere eseguito localmente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="99f0f-179">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="99f0f-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="99f0f-180">**%%sql -o <variable name>**: esegue una query Hive su sqlContext.</span><span class="sxs-lookup"><span data-stu-id="99f0f-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="99f0f-181">Se viene passato il parametro -o, il risultato della query viene salvato in modo permanente nel contesto Python %%local come frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="99f0f-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="99f0f-182">Per altre informazioni sui kernel per i notebook di Jupyter e i "magic" predefiniti messi a disposizione, vedere [Kernel disponibili per i notebook di Jupyter con cluster Apache Spark in HDInsight Linux](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="99f0f-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="99f0f-183">Inserimento di dati dal BLOB pubblico:</span><span class="sxs-lookup"><span data-stu-id="99f0f-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="99f0f-184">Il primo passaggio del processo di analisi scientifica dei dati consiste nel prelevare i dati da analizzare dalle origini in cui risiedono e inserirli nell'ambiente di modellazione ed esplorazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="99f0f-185">In questa procedura dettagliata l'ambiente è Spark.</span><span class="sxs-lookup"><span data-stu-id="99f0f-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="99f0f-186">Questa sezione contiene il codice per completare una serie di attività:</span><span class="sxs-lookup"><span data-stu-id="99f0f-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="99f0f-187">Inserimento del campione di dati da modellare.</span><span class="sxs-lookup"><span data-stu-id="99f0f-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="99f0f-188">Lettura del set di dati di input archiviato come file TSV.</span><span class="sxs-lookup"><span data-stu-id="99f0f-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="99f0f-189">Formattazione e pulizia dei dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-189">format and clean the data</span></span>
* <span data-ttu-id="99f0f-190">Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="99f0f-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="99f0f-191">Registrazione come tabella temporanea in un contesto SQL.</span><span class="sxs-lookup"><span data-stu-id="99f0f-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="99f0f-192">Di seguito è riportato il codice per l'inserimento di dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-192">Here is the code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-193">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-193">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-194">Tempo impiegato per eseguire questa cella: 276,62 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="99f0f-195">Visualizzazione ed esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="99f0f-195">Data exploration & visualization</span></span>
<span data-ttu-id="99f0f-196">Dopo aver inserito i dati in Spark, il passaggio successivo del processo di analisi scientifica dei dati consiste nell'esplorazione e nella visualizzazione dei dati per approfondirne la conoscenza.</span><span class="sxs-lookup"><span data-stu-id="99f0f-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="99f0f-197">In questa sezione vengono esaminati i dati relativi ai taxi tramite query SQL e vengono tracciate le variabili di destinazione e le funzionalità potenziali per l'esame visivo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="99f0f-198">In particolare, viene tracciata la frequenza del numero di passeggeri nelle corse dei taxi, la frequenza dell'importo delle mance e la variazione delle mance in base al tipo e all'importo del pagamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="99f0f-199">Tracciare un istogramma delle frequenze del numero di passeggeri nel campione di corse dei taxi</span><span class="sxs-lookup"><span data-stu-id="99f0f-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="99f0f-200">Questo codice e i frammenti di codice successivi usano un magic SQL per eseguire una query sul campione e un magic local per tracciare i dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="99f0f-201">**Magic SQL (`%%sql`)**: il kernel HDInsight PySpark supporta l'esecuzione di query HiveQL inline semplici su sqlContext.</span><span class="sxs-lookup"><span data-stu-id="99f0f-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="99f0f-202">L'argomento (-o NOME_VARIABILE) salva in modo permanente l'output della query SQL come frame di dati Pandas nel server Jupyter.</span><span class="sxs-lookup"><span data-stu-id="99f0f-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="99f0f-203">Questo significa che è disponibile in modalità locale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="99f0f-204">Il **`%%local`** viene usato per eseguire il codice in locale nel server Jupyter, che costituisce il nodo head del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="99f0f-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="99f0f-205">In genere, si usa Magic `%%local` dopo il Magic `%%sql -o` per eseguire una query.</span><span class="sxs-lookup"><span data-stu-id="99f0f-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="99f0f-206">Il parametro -o salva in modo permanente l'output della query SQL in locale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="99f0f-207">Il Magic `%%local` attiva il set successivo di frammenti di codice per eseguire localmente l'output delle query SQL che è stato mantenuto in locale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="99f0f-208">L'output viene visualizzato automaticamente dopo aver eseguito il codice.</span><span class="sxs-lookup"><span data-stu-id="99f0f-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="99f0f-209">Questa query recupera le corse per numero di passeggeri.</span><span class="sxs-lookup"><span data-stu-id="99f0f-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="99f0f-210">Questo codice crea un frame di dati locale dall'output della query ed esegue il tracciato dei dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="99f0f-211">Il magic `%%local` crea un frame di dati locale, `sqlResults`, che può essere usato per eseguire tracciati con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="99f0f-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="99f0f-212">Tale magic PySpark viene usato più volte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="99f0f-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="99f0f-213">In caso di un'elevata quantità di dati, è consigliabile campionare i dati in modo da creare un frame che possa essere contenuto nella memoria locale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="99f0f-214">Ecco il codice per eseguire il tracciato delle corse per numero di passeggeri</span><span class="sxs-lookup"><span data-stu-id="99f0f-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

<span data-ttu-id="99f0f-215">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-215">**OUTPUT**</span></span>

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="99f0f-217">È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, a linee, ad area o a barre) usando i pulsanti del menu **Type** (Tipo) nel notebook.</span><span class="sxs-lookup"><span data-stu-id="99f0f-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="99f0f-218">In questo caso è stato scelto un tracciato a barre.</span><span class="sxs-lookup"><span data-stu-id="99f0f-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="99f0f-219">Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.</span><span class="sxs-lookup"><span data-stu-id="99f0f-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="99f0f-220">Usare una query SQL per campionare i dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-220">Use a SQL query to sample data..</span></span>

    # SQL SQUERY
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


<span data-ttu-id="99f0f-221">Questa cella di codice usa la query SQL per creare tre tracciati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


<span data-ttu-id="99f0f-222">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="99f0f-222">**OUTPUT:**</span></span> 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="99f0f-226">Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione</span><span class="sxs-lookup"><span data-stu-id="99f0f-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="99f0f-227">Questa sezione descrive le procedure usate per preparare i dati da usare nella modellazione per l'apprendimento automatico, fornisce il relativo codice e</span><span class="sxs-lookup"><span data-stu-id="99f0f-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="99f0f-228">illustra come eseguire queste attività:</span><span class="sxs-lookup"><span data-stu-id="99f0f-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="99f0f-229">Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="99f0f-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="99f0f-230">Indicizzare funzionalità categoriche e applicare la codifica one-hot</span><span class="sxs-lookup"><span data-stu-id="99f0f-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="99f0f-231">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="99f0f-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="99f0f-232">Creare un sottocampionamento casuale dei dati e dividerlo in set di training e di testing</span><span class="sxs-lookup"><span data-stu-id="99f0f-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="99f0f-233">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="99f0f-233">Feature scaling</span></span>
* <span data-ttu-id="99f0f-234">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="99f0f-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="99f0f-235">Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="99f0f-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="99f0f-236">Questo codice illustra come ottenere una nuova funzionalità dalla creazione di contenitori per gli orari di trasporto e come memorizzare nella cache il frame di dati risultante in memoria.</span><span class="sxs-lookup"><span data-stu-id="99f0f-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="99f0f-237">La memorizzazione nella cache consente di migliorare i tempi di esecuzione, quando si usano ripetutamente RDD (Resilient Distributed Dataset) e frame di dati.</span><span class="sxs-lookup"><span data-stu-id="99f0f-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="99f0f-238">RDD e frame di dati vengono quindi memorizzati nella cache in varie fasi di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="99f0f-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="99f0f-239">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-239">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-240">126050</span><span class="sxs-lookup"><span data-stu-id="99f0f-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="99f0f-241">Indicizzare funzionalità categoriche e applicare la codifica one-hot</span><span class="sxs-lookup"><span data-stu-id="99f0f-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="99f0f-242">Questa sezione illustra come indicizzare o codificare le funzionalità categoriche per l'inserimento nelle funzioni di modellazione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="99f0f-243">Per poter usare le funzioni di modellazione e previsione di MLlib, è necessario prima indicizzare o codificare le funzionalità con dati di input categorici.</span><span class="sxs-lookup"><span data-stu-id="99f0f-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="99f0f-244">A seconda del modello, è necessario indicizzare o codificare tali funzioni in modi diversi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="99f0f-245">Ad esempio, i modelli logistici e di regressione lineare richiedono la codifica one-hot in cui, ad esempio, una funzionalità con tre categorie può essere espansa in tre colonne di funzionalità, in cui ogni colonna contiene 0 o 1 a seconda della categoria di un'osservazione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="99f0f-246">Per eseguire la codifica one-hot in MLlib è disponibile la funzione [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder).</span><span class="sxs-lookup"><span data-stu-id="99f0f-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="99f0f-247">Questo codificatore esegue il mapping di una colonna di indici etichetta a una colonna di vettori binari, con al massimo un singolo valore unico.</span><span class="sxs-lookup"><span data-stu-id="99f0f-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="99f0f-248">Questa codifica permette di applicare a funzionalità categoriche gli algoritmi che prevedono funzionalità con valori numerici, ad esempio la regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="99f0f-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="99f0f-249">Di seguito è riportato il codice per l'indicizzazione e la codifica delle funzionalità categoriche:</span><span class="sxs-lookup"><span data-stu-id="99f0f-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="99f0f-250">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-250">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-251">Tempo impiegato per eseguire questa cella: 3,14 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="99f0f-252">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="99f0f-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="99f0f-253">Questa sezione contiene il codice che illustra come indicizzare i dati di testo suddivisi in categorie come tipo di dati come punto etichettato e come codificarlo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="99f0f-254">Consente di prepararlo ad essere usato per il training e test di regressione logistica MLlib e altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="99f0f-255">Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="99f0f-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="99f0f-256">Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.</span><span class="sxs-lookup"><span data-stu-id="99f0f-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="99f0f-257">Ecco il codice per indicizzare e codificare le funzionalità di testo per la classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="99f0f-257">Here is the code to index and encode text features for binary classification.</span></span>

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


<span data-ttu-id="99f0f-258">Ecco il codice per codificare e indicizzare le funzionalità di testo categoriche per l'analisi di regressione lineare.</span><span class="sxs-lookup"><span data-stu-id="99f0f-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="99f0f-259">Creare un sottocampionamento casuale dei dati e dividerlo in set di training e di testing</span><span class="sxs-lookup"><span data-stu-id="99f0f-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="99f0f-260">Questo codice crea un campionamento casuale dei dati, qui viene usato il 25%.</span><span class="sxs-lookup"><span data-stu-id="99f0f-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="99f0f-261">Anche se non è necessario per questo esempio, date le dimensioni del set di dati, viene illustrato come eseguire il campionamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="99f0f-262">Adesso si sa come usarlo per il proprio problema, se necessario.</span><span class="sxs-lookup"><span data-stu-id="99f0f-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="99f0f-263">Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli.</span><span class="sxs-lookup"><span data-stu-id="99f0f-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="99f0f-264">Successivamente il campione viene suddiviso in un set di training (75%) e un set di testing (25%) da usare nei modelli di regressione e classificazione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

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

<span data-ttu-id="99f0f-265">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-265">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-266">Tempo impiegato per eseguire questa cella: 0,31 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="99f0f-267">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="99f0f-267">Feature scaling</span></span>
<span data-ttu-id="99f0f-268">Il ridimensionamento di funzionalità, noto anche come normalizzazione dei dati, permette di fare in modo che alle funzionalità con valori molto dispersi non venga attribuito un peso eccessivo nella funzione obiettivo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="99f0f-269">Per ridimensionare le funzionalità alla varianza unitaria, il relativo codice usa [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) .</span><span class="sxs-lookup"><span data-stu-id="99f0f-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="99f0f-270">Viene fornito da MLlib per l'uso nella regressione lineare con Stochastic Gradient Descent (SGD).</span><span class="sxs-lookup"><span data-stu-id="99f0f-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="99f0f-271">SGD è un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="99f0f-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="99f0f-272">L'algoritmo LinearRegressionWithSGD è risultato sensibile al ridimensionamento di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="99f0f-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="99f0f-273">Ecco il codice per ridimensionare le variabili per l'uso con l'algoritmo SGD lineare regolarizzato.</span><span class="sxs-lookup"><span data-stu-id="99f0f-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="99f0f-274">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-274">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-275">Tempo impiegato per eseguire questa cella: 11,67 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="99f0f-276">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="99f0f-276">Cache objects in memory</span></span>
<span data-ttu-id="99f0f-277">Il caching degli oggetti del frame di dati di input usati per la classificazione, la regressione e le funzionalità con ridimensionamento permette di ridurre il tempo impiegato per il training e il testing degli algoritmi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="99f0f-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="99f0f-278">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-278">**OUTPUT**</span></span> 

<span data-ttu-id="99f0f-279">Tempo impiegato per eseguire questa cella: 0,13 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="99f0f-280">Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia</span><span class="sxs-lookup"><span data-stu-id="99f0f-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="99f0f-281">Questa sezione illustra come usare tre modelli per l'attività di classificazione binaria di previsione di una possibile mancia lasciata per una corsa in taxi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="99f0f-282">I modelli presentati sono:</span><span class="sxs-lookup"><span data-stu-id="99f0f-282">The models presented are:</span></span>

* <span data-ttu-id="99f0f-283">Regressione logistica</span><span class="sxs-lookup"><span data-stu-id="99f0f-283">Logistic regression</span></span> 
* <span data-ttu-id="99f0f-284">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="99f0f-284">Random forest</span></span>
* <span data-ttu-id="99f0f-285">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="99f0f-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="99f0f-286">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="99f0f-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="99f0f-287">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="99f0f-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="99f0f-288">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="99f0f-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="99f0f-289">**Salvataggio del modello** in un BLOB per l'utilizzo in futuro</span><span class="sxs-lookup"><span data-stu-id="99f0f-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="99f0f-290">Ecco due modi per eseguire la convalida incrociata con sweep di parametri:</span><span class="sxs-lookup"><span data-stu-id="99f0f-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="99f0f-291">Tramite codice **generico** personalizzato che può essere applicato a qualsiasi algoritmo in MLlib e a qualsiasi set di parametri in un algoritmo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="99f0f-292">Tramite la **funzione della pipeline CrossValidator pySpark**.</span><span class="sxs-lookup"><span data-stu-id="99f0f-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="99f0f-293">Si noti che CrossValidator presenta alcune limitazioni per Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="99f0f-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="99f0f-294">I modelli di pipeline non possono essere salvati/resi persistenti per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="99f0f-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="99f0f-295">Non può essere usato per ogni parametro in un modello.</span><span class="sxs-lookup"><span data-stu-id="99f0f-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="99f0f-296">Non può essere usato per ogni algoritmo MLlib.</span><span class="sxs-lookup"><span data-stu-id="99f0f-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="99f0f-297">Convalida incrociata generica e sweep di iperparametri usati con l'algoritmo di regressione logistica per la classificazione binaria</span><span class="sxs-lookup"><span data-stu-id="99f0f-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="99f0f-298">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di regressione logistica con l'algoritmo [L-BFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo alle corse e tariffe dei taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="99f0f-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="99f0f-299">Il training del modello viene eseguito con convalida incrociata e sweep di iperparametri implementati con codice personalizzato, che è possibile applicare a qualsiasi algoritmo di apprendimento in MLlib.</span><span class="sxs-lookup"><span data-stu-id="99f0f-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="99f0f-300">L'esecuzione del codice personalizzato di convalida incrociata può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="99f0f-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="99f0f-301">**Eseguire il training del modello di regressione logistica usando la convalida incrociata e lo sweep degli iperparametri**</span><span class="sxs-lookup"><span data-stu-id="99f0f-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-302">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-302">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-303">Coefficienti: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="99f0f-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="99f0f-304">Intercetta: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="99f0f-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="99f0f-305">Tempo impiegato per eseguire questa cella: 14,43 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="99f0f-306">**Valutare il modello di classificazione binaria con le metriche standard**</span><span class="sxs-lookup"><span data-stu-id="99f0f-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="99f0f-307">Il codice in questa sezione illustra come valutare un modello di regressione logistica su un set di dati di test, incluso un tracciato della curva ROC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

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

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-308">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-308">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-309">Area in PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="99f0f-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="99f0f-310">Area in ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="99f0f-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="99f0f-311">Statistiche di riepilogo</span><span class="sxs-lookup"><span data-stu-id="99f0f-311">Summary Stats</span></span>

<span data-ttu-id="99f0f-312">Precisione = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="99f0f-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="99f0f-313">Richiamo = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="99f0f-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="99f0f-314">Punteggio F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="99f0f-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="99f0f-315">Tempo impiegato per eseguire questa cella: 2,67 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="99f0f-316">**Tracciare la curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="99f0f-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="99f0f-317">L'oggetto *predictionAndLabelsDF* viene registrato come tabella, *tmp_results*, nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="99f0f-318">L'oggetto *tmp_results* può essere usato per eseguire query e restituire i risultati nel frame di dati sqlResults per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="99f0f-319">Ecco il codice.</span><span class="sxs-lookup"><span data-stu-id="99f0f-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="99f0f-320">Ecco il codice per eseguire stime e tracciare la curva ROC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


<span data-ttu-id="99f0f-321">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-321">**OUTPUT**</span></span>

![Curva ROC di regressione logistica per approccio generico](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="99f0f-323">**Rendere persistente il modello in un BLOB per l'utilizzo in futuro**</span><span class="sxs-lookup"><span data-stu-id="99f0f-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="99f0f-324">Il codice in questa sezione illustra come salvare il modello di regressione logistica per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="99f0f-325">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-325">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-326">Tempo impiegato per eseguire questa cella: 34,57 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="99f0f-327">Usare la funzione della pipeline CrossValidator di MLlib con il modello di regressione logistica (regressione elastica)</span><span class="sxs-lookup"><span data-stu-id="99f0f-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="99f0f-328">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di regressione logistica con l'algoritmo [L-BFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) , che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo alle corse e tariffe dei taxi della città di New York.</span><span class="sxs-lookup"><span data-stu-id="99f0f-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="99f0f-329">Il training del modello viene eseguito con convalida incrociata e sweep di iperparametri implementati con la funzione della pipeline CrossValidator MLlib per convalida incrociata con sweep di iperparametri.</span><span class="sxs-lookup"><span data-stu-id="99f0f-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="99f0f-330">L'esecuzione del codice di convalida incrociata MLlib può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="99f0f-330">The execution of this MLlib CV code can take several minutes.</span></span>
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="99f0f-331">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-331">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-332">Tempo impiegato per eseguire questa cella: 107,98 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="99f0f-333">**Tracciare la curva ROC.**</span><span class="sxs-lookup"><span data-stu-id="99f0f-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="99f0f-334">L'oggetto *predictionAndLabelsDF* viene registrato come tabella, *tmp_results*, nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="99f0f-335">L'oggetto *tmp_results* può essere usato per eseguire query e restituire i risultati nel frame di dati sqlResults per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="99f0f-336">Ecco il codice.</span><span class="sxs-lookup"><span data-stu-id="99f0f-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="99f0f-337">Ecco il codice per tracciare la curva ROC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


<span data-ttu-id="99f0f-338">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-338">**OUTPUT**</span></span>

![Curva ROC di regressione logistica con CrossValidator di MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="99f0f-340">Classificazione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="99f0f-340">Random forest classification</span></span>
<span data-ttu-id="99f0f-341">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare una regressione tramite foresta casuale, che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo alle corse e tariffe dei taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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


<span data-ttu-id="99f0f-342">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-342">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-343">Area in ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="99f0f-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="99f0f-344">Tempo impiegato per eseguire questa cella: 26,72 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="99f0f-345">Classificazione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="99f0f-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="99f0f-346">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di alberi con boosting a gradienti, che consente di prevedere se viene lasciata o meno una mancia per una corsa nel set di dati relativo alle corse e tariffe dei taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
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

<span data-ttu-id="99f0f-347">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-347">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-348">Area in ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="99f0f-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="99f0f-349">Tempo impiegato per eseguire questa cella: 28,13 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="99f0f-350">Prevedere l'importo delle mance con di modelli di regressione (senza usare la convalida incrociata)</span><span class="sxs-lookup"><span data-stu-id="99f0f-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="99f0f-351">Questa sezione illustra come usare tre modelli per l'attività di regressione relativa alla previsione dell'importo della mancia lasciata per una corsa in taxi in base ad altre funzionalità relative alle mance.</span><span class="sxs-lookup"><span data-stu-id="99f0f-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="99f0f-352">I modelli presentati sono:</span><span class="sxs-lookup"><span data-stu-id="99f0f-352">The models presented are:</span></span>

* <span data-ttu-id="99f0f-353">Regressione lineare regolarizzata</span><span class="sxs-lookup"><span data-stu-id="99f0f-353">Regularized linear regression</span></span>
* <span data-ttu-id="99f0f-354">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="99f0f-354">Random forest</span></span>
* <span data-ttu-id="99f0f-355">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="99f0f-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="99f0f-356">Questi modelli sono stati descritti nell'introduzione.</span><span class="sxs-lookup"><span data-stu-id="99f0f-356">These models were described in the introduction.</span></span> <span data-ttu-id="99f0f-357">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="99f0f-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="99f0f-358">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="99f0f-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="99f0f-359">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="99f0f-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="99f0f-360">**Salvataggio del modello** in un BLOB per l'utilizzo in futuro</span><span class="sxs-lookup"><span data-stu-id="99f0f-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="99f0f-361">NOTA PER AZURE: la convalida incrociata non viene usata con i tre modelli di regressione in questa sezione, in quanto è stata illustrata in dettaglio per i modelli di regressione logistica.</span><span class="sxs-lookup"><span data-stu-id="99f0f-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="99f0f-362">Nell'appendice di questo argomento viene fornito un esempio che illustra come usare la convalida incrociata con Elastic Net per la regressione lineare.</span><span class="sxs-lookup"><span data-stu-id="99f0f-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="99f0f-363">NOTA PER AZURE: la convergenza di modelli LinearRegressionWithSGD può risultare problematica ed è necessario modificare oppure ottimizzare attentamente i parametri per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="99f0f-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="99f0f-364">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="99f0f-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="99f0f-365">Al posto di LinearRegressionWithSGD è anche possibile usare la regressione Elastic Net illustrata nell'appendice di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="99f0f-366">Regressione lineare con SGD</span><span class="sxs-lookup"><span data-stu-id="99f0f-366">Linear regression with SGD</span></span>
<span data-ttu-id="99f0f-367">Il codice riportato in questa sezione illustra come usare le funzionalità con ridimensionamento per il training di una regressione lineare che usa la discesa del gradiente stocastica (SGD) per l'ottimizzazione e come assegnare punteggi, valutare e salvare il modello in BLOB di Archiviazione di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="99f0f-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="99f0f-368">La convergenza di modelli LinearRegressionWithSGD può risultare problematica ed è necessario modificare oppure ottimizzare attentamente i parametri per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="99f0f-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="99f0f-369">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="99f0f-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="99f0f-370">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-370">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-371">Coefficienti: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="99f0f-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="99f0f-372">Intercetta: 0,854507624459</span><span class="sxs-lookup"><span data-stu-id="99f0f-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="99f0f-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="99f0f-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="99f0f-374">R-sqr = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="99f0f-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="99f0f-375">Tempo impiegato per eseguire questa cella: 38,62 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="99f0f-376">Regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="99f0f-376">Random Forest regression</span></span>
<span data-ttu-id="99f0f-377">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di foresta casuale, che consente di prevedere l'importo della mancia per il set di dati relativo alle corse in taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="99f0f-378">Nell'appendice è illustrata la convalida incrociata con sweep di parametri tramite codice personalizzato.</span><span class="sxs-lookup"><span data-stu-id="99f0f-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT TO PRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

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

<span data-ttu-id="99f0f-379">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-379">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="99f0f-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="99f0f-381">R-sqr = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="99f0f-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="99f0f-382">Tempo impiegato per eseguire questa cella: 25,98 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="99f0f-383">Regressione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="99f0f-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="99f0f-384">Il codice riportato in questa sezione illustra come eseguire il training, valutare e salvare un modello di alberi con boosting a gradienti, che consente di prevedere l'importo della mancia per il set di dati relativo alle corse in taxi di NYC.</span><span class="sxs-lookup"><span data-stu-id="99f0f-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="99f0f-385">* * Eseguire il training e valutare * *</span><span class="sxs-lookup"><span data-stu-id="99f0f-385">**Train and evaluate **</span></span>

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-386">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-386">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="99f0f-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="99f0f-388">R-sqr = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="99f0f-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="99f0f-389">Tempo impiegato per eseguire questa cella: 20,9 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="99f0f-390">**Grafico**</span><span class="sxs-lookup"><span data-stu-id="99f0f-390">**Plot**</span></span>

<span data-ttu-id="99f0f-391">L'oggetto *tmp_results* viene registrato come tabella Hive nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="99f0f-392">I risultati della tabella vengono restituiti nel frame di dati *sqlResults* per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="99f0f-393">Ecco il codice</span><span class="sxs-lookup"><span data-stu-id="99f0f-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="99f0f-394">Ecco il codice per tracciare i dati usando il server Jupyter.</span><span class="sxs-lookup"><span data-stu-id="99f0f-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="99f0f-396">Appendice: Attività di regressione aggiuntive tramite convalida incrociata con sweep di parametri</span><span class="sxs-lookup"><span data-stu-id="99f0f-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="99f0f-397">Questa appendice contiene il codice che illustra come eseguire la convalida incrociata con Elastic Net per la regressione lineare e come eseguire la convalida incrociata con sweep di parametri usando codice personalizzato per la regressione tramite foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="99f0f-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="99f0f-398">Convalida incrociata con Elastic Net per la regressione lineare</span><span class="sxs-lookup"><span data-stu-id="99f0f-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="99f0f-399">Il codice in questa sezione illustra come eseguire la convalida incrociata usando Elastic Net per la regressione lineare e come valutare il modello rispetto a dati di test.</span><span class="sxs-lookup"><span data-stu-id="99f0f-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-400">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-400">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-401">Tempo impiegato per eseguire questa cella: 161,21 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="99f0f-402">**Eseguire la valutazione con la metrica R-SQR**</span><span class="sxs-lookup"><span data-stu-id="99f0f-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="99f0f-403">*tmp_results* viene registrato come una tabella Hive nella cella precedente.</span><span class="sxs-lookup"><span data-stu-id="99f0f-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="99f0f-404">I risultati della tabella vengono restituiti nel frame di dati *sqlResults* per il tracciamento.</span><span class="sxs-lookup"><span data-stu-id="99f0f-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="99f0f-405">Ecco il codice</span><span class="sxs-lookup"><span data-stu-id="99f0f-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="99f0f-406">Ecco il codice per calcolare R-sqr.</span><span class="sxs-lookup"><span data-stu-id="99f0f-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="99f0f-407">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-407">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-408">R-sqr = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="99f0f-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="99f0f-409">Convalida incrociata con sweep di parametri usando codice personalizzato per la regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="99f0f-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="99f0f-410">Il codice in questa sezione illustra come eseguire la convalida incrociata con sweep di parametri usando codice personalizzato per la regressione tramite foresta casuale e come valutare il modello rispetto a dati di test.</span><span class="sxs-lookup"><span data-stu-id="99f0f-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="99f0f-411">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-411">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="99f0f-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="99f0f-413">R-sqr = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="99f0f-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="99f0f-414">Tempo impiegato per eseguire questa cella: 69,17 secondi.</span><span class="sxs-lookup"><span data-stu-id="99f0f-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="99f0f-415">Pulire gli oggetti dalla memoria e stampare i percorsi dei modelli</span><span class="sxs-lookup"><span data-stu-id="99f0f-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="99f0f-416">Usare `unpersist()` per eliminare gli oggetti memorizzati nella cache.</span><span class="sxs-lookup"><span data-stu-id="99f0f-416">Use `unpersist()` to delete objects cached in memory.</span></span>

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

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


<span data-ttu-id="99f0f-417">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-417">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="99f0f-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="99f0f-419">* * Percorso di stampa per i file di modello da utilizzare nel blocco appunti consumo.</span><span class="sxs-lookup"><span data-stu-id="99f0f-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="99f0f-420">* * Per utilizzare e assegnare un punteggio un set di dati indipendente, è necessario copiare e incollare questi nomi di file "Raccoglitore di utilizzo".</span><span class="sxs-lookup"><span data-stu-id="99f0f-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="99f0f-421">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="99f0f-421">**OUTPUT**</span></span>

<span data-ttu-id="99f0f-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="99f0f-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="99f0f-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="99f0f-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="99f0f-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="99f0f-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="99f0f-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="99f0f-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="99f0f-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="99f0f-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="99f0f-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="99f0f-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="99f0f-428">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="99f0f-428">What's next?</span></span>
<span data-ttu-id="99f0f-429">Dopo aver creato i modelli regressivi e di classificazione con MlLib di Spark, è possibile imparare a valutare e assegnare punteggi a questi modelli.</span><span class="sxs-lookup"><span data-stu-id="99f0f-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="99f0f-430">**Uso dei modelli:** per informazioni su come valutare e assegnare punteggi ai modelli di regressione e di classificazione creati in questo argomento, vedere [Assegnare punteggi a modelli di apprendimento automatico compilati con Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="99f0f-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

