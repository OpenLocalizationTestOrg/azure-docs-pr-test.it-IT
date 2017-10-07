---
title: l'esplorazione dei dati aaaAdvanced e modellazione con Spark | Documenti Microsoft
description: Utilizzare l'esplorazione dei dati di toodo HDInsight Spark ed eseguirne il training modelli di classificazione e regressione binari con l'ottimizzazione della convalida incrociata e hyperparameter.
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
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="49da0-103">Esplorazione e modellazione avanzate dei dati con Spark</span><span class="sxs-lookup"><span data-stu-id="49da0-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="49da0-104">Questa procedura dettagliata Usa HDInsight Spark toodo train ed esplorazione dei binaria e classificazione dei dati utilizzando la convalida incrociata di modelli di regressione e ottimizzazione hyperparameter su un campione di hello NYC taxi di andata e ritorno e presentare set di dati 2013.</span><span class="sxs-lookup"><span data-stu-id="49da0-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="49da0-105">Contiene passaggi hello di hello [il processo di analisi scientifica dei dati](http://aka.ms/datascienceprocess), end-to-end, utilizzando un HDInsight Spark cluster per l'elaborazione e i modelli di dati e hello hello toostore oggetti BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="49da0-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="49da0-106">processo Hello analizza e visualizza i dati importati da un Blob di archiviazione di Azure e quindi prepara hello dati toobuild modelli predittivi.</span><span class="sxs-lookup"><span data-stu-id="49da0-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="49da0-107">Python è stato utilizzato toocode hello soluzione e tooshow hello rilevanti tracciati.</span><span class="sxs-lookup"><span data-stu-id="49da0-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="49da0-108">Questi modelli sono compilazione mediante classificazione binaria toodo toolkit Spark MLlib hello e modellazione di attività di regressione.</span><span class="sxs-lookup"><span data-stu-id="49da0-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="49da0-109">Hello **classificazione binaria** attività è toopredict un suggerimento è pagato viaggi hello o meno.</span><span class="sxs-lookup"><span data-stu-id="49da0-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="49da0-110">Hello **regressione** attività è quantità hello toopredict del suggerimento hello in base alle altre funzionalità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="49da0-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="49da0-111">i passaggi di modellazione Hello inoltre contenere codice che illustra come tootrain, valutare e salvare ogni tipo di modello.</span><span class="sxs-lookup"><span data-stu-id="49da0-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="49da0-112">Hello argomento vengono illustrate alcune delle hello stesso messa a terra come hello [l'esplorazione dei dati e modellazione con Spark](machine-learning-data-science-spark-data-exploration-modeling.md) argomento.</span><span class="sxs-lookup"><span data-stu-id="49da0-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="49da0-113">Ma più "avanzato" che usa anche la convalida incrociata con hyperparameter sweep tootrain modelli di classificazione e regressione in modo ottimale accurati.</span><span class="sxs-lookup"><span data-stu-id="49da0-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="49da0-114">**La convalida incrociata (CV)** è una tecnica che consente di valutare un modello sottoposto a training su un set di dati noto anche come consente di generalizzare toopredicting hello funzionalità dei set di dati in cui si è ancora stato eseguito.</span><span class="sxs-lookup"><span data-stu-id="49da0-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="49da0-115">Un'implementazione comune utilizzata in questo argomento è toodivide un set di dati in sezioni di K e quindi eseguire il training del modello di hello in uno schema round robin su almeno una delle sezioni hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="49da0-116">viene valutato il possibilità Hello di hello modello tooprediction in modo accurato quando testato hello indipendente dal set di dati in questo modello di hello tootrain riduzione non usato.</span><span class="sxs-lookup"><span data-stu-id="49da0-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="49da0-117">**Ottimizzazione Hyperparameter** hello problema della scelta di un set di iperparametri per un algoritmo di apprendimento, in genere con l'obiettivo di hello ottimizzare una misura delle prestazioni dell'algoritmo hello in un set di dati indipendente.</span><span class="sxs-lookup"><span data-stu-id="49da0-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="49da0-118">**Iperparametri** sono valori che devono essere specificati all'esterno di procedure training modello di hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="49da0-119">Presupposti relativi questi valori possono influire flessibilità hello e accuratezza dei modelli di hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="49da0-120">Gli alberi delle decisioni hanno iperparametri, ad esempio, come lo si desidera hello profondità e numero di foglie nell'albero di hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="49da0-121">Le macchine a vettori di supporto (SVM, Support Vector Machine) richiedono l'impostazione di una penalità per errata classificazione.</span><span class="sxs-lookup"><span data-stu-id="49da0-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="49da0-122">Un'ottimizzazione comune delle modalità tooperform hyperparameter utilizzata in questo argomento è una ricerca di griglia, o un **sweep di parametri**.</span><span class="sxs-lookup"><span data-stu-id="49da0-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="49da0-123">Si tratta di eseguendo una ricerca completa tramite i valori hello un subset di spazio hyperparameter hello specificato per un algoritmo di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="49da0-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="49da0-124">Convalida incrociata può fornire un toosort metrica prestazioni out ottimale hello prodotto dall'algoritmo di ricerca di hello griglia.</span><span class="sxs-lookup"><span data-stu-id="49da0-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="49da0-125">CV utilizzato con hyperparameter sweep problemi di limite consente l'overfitting di un dati tootraining del modello in modo che hello modello consente di mantenere hello capacità tooapply toohello generale set di dati dalla quale hello sono stati estratti i dati di training.</span><span class="sxs-lookup"><span data-stu-id="49da0-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="49da0-126">i modelli di Hello che utilizziamo includono la regressione logistica e lineare, foreste casuali e sfumati alberi con Boosting:</span><span class="sxs-lookup"><span data-stu-id="49da0-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="49da0-127">[La regressione lineare con SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) è un modello di regressione lineare che utilizza un metodo dei valori descent con sfumatura Stocastica (SGD, Virtual Private Network) e gli importi di suggerimento hello toopredict la scalabilità a pagamento per l'ottimizzazione e funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49da0-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="49da0-128">[La regressione logistica con LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) o regressione "logit", è un modello di regressione che può essere utilizzato quando variabile dipendente hello è organizzato per categorie toodo classificazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="49da0-129">LBFGS è un algoritmo di ottimizzazione quasi Newton che offre un'approssimazione algoritmo di Broyden – Fletcher – Goldfarb – Shanno (BFGS) hello utilizzando una quantità limitata di memoria del computer e che è ampiamente usati in machine learning.</span><span class="sxs-lookup"><span data-stu-id="49da0-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="49da0-130">[foreste casuali](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="49da0-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="49da0-131">Combinano molti decision trees tooreduce hello rischio di overfitting.</span><span class="sxs-lookup"><span data-stu-id="49da0-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="49da0-132">Foreste casuali vengono utilizzate per la classificazione e regressione e possono gestire funzioni categoriche e possono essere esteso l'impostazione di classificazione multiclasse toohello.</span><span class="sxs-lookup"><span data-stu-id="49da0-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="49da0-133">Non richiedono funzionalità scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49da0-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="49da0-134">Foreste casuali sono uno dei hello riuscito più modelli di machine learning per la classificazione e regressione.</span><span class="sxs-lookup"><span data-stu-id="49da0-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="49da0-135">[Alberi con boosting a gradienti](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT, Gradient boosted tree) sono insiemi di alberi delle decisioni.</span><span class="sxs-lookup"><span data-stu-id="49da0-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="49da0-136">GBTs train alberi delle decisioni in modo iterativo toominimize una funzione di perdita.</span><span class="sxs-lookup"><span data-stu-id="49da0-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="49da0-137">GBTs vengono utilizzati per la classificazione e regressione e può gestire funzioni categoriche, non richiedono la funzionalità di scalabilità e sono in grado di toocapture non linearità e interazioni di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49da0-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="49da0-138">Possono anche essere usati in un'impostazione di classificazione multiclasse.</span><span class="sxs-lookup"><span data-stu-id="49da0-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="49da0-139">Esempi di utilizzo CV e Hyperparameter di modellazione durante lo sweep vengono visualizzati per il problema di classificazione binaria hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="49da0-140">Più semplici (senza parametro sweep) sono illustrati esempi dell'argomento principale di hello per le attività di regressione.</span><span class="sxs-lookup"><span data-stu-id="49da0-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="49da0-141">Tuttavia, nell'appendice hello, viene presentata anche la convalida tramite net elastico per la regressione lineare e CV con parametro durante lo sweep di regressione di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="49da0-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="49da0-142">Hello **elastica net** è un metodo di regressione regolarizzata per la regressione lineare di adattamento modelli in modo lineare combina metriche di tipo L1 e L2 hello come sanzioni di hello [lazo](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) e [bordo in rilievo](https://en.wikipedia.org/wiki/Tikhonov_regularization) metodi.</span><span class="sxs-lookup"><span data-stu-id="49da0-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="49da0-143">Anche se hello Spark MLlib toolkit è progettato toowork su grandi set di dati, un campione di dimensioni relativamente ridotte (circa 30 Mb utilizzando K 170 righe, circa 0,1% del set di dati NYC originale hello) viene usato per motivi di praticità.</span><span class="sxs-lookup"><span data-stu-id="49da0-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="49da0-144">esercizio Hello indicato qui viene eseguito in modo efficiente (in circa 10 minuti) in un cluster di HDInsight con 2 nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="49da0-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="49da0-145">Hello stesso codice, con modifiche minori, può essere utilizzato tooprocess maggiore-set di dati, con le modifiche appropriate per la memorizzazione nella cache dei dati in memoria e la modifica delle dimensioni del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="49da0-146">Configurazione: notebook e cluster Spark</span><span class="sxs-lookup"><span data-stu-id="49da0-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="49da0-147">La procedura di installazione e il codice forniti in questa procedura dettagliata sono per l'uso di un HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="49da0-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="49da0-148">Ma vengono forniti i notebook di Jupyter per i cluster HDInsight sia Spark 1.6 sia Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="49da0-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="49da0-149">Vengono forniti una descrizione di hello blocchi appunti e collegamenti toothem in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) per il repository di GitHub hello che li contengono.</span><span class="sxs-lookup"><span data-stu-id="49da0-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="49da0-150">Inoltre, codice hello qui e i notebook hello collegato è generico e dovrebbe funzionare in un cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="49da0-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="49da0-151">Se non si utilizza HDInsight Spark, passaggi di configurazione e gestione di cluster hello potrebbero essere leggermente diversi rispetto a quanto mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="49da0-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="49da0-152">Per praticità, di seguito sono notebook Jupyter di hello collegamenti toohello per 1.6 Spark e 2.0 toobe eseguito nel kernel pyspark hello del server Jupyter Notebook hello:</span><span class="sxs-lookup"><span data-stu-id="49da0-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="49da0-153">Notebook Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="49da0-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="49da0-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): include gli argomenti nel notebook numero 1 e modella lo sviluppo usando l'ottimizzazione degli iperparametri e la convalida incrociata.</span><span class="sxs-lookup"><span data-stu-id="49da0-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="49da0-155">Notebook Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="49da0-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="49da0-156">[Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): questo file fornisce informazioni su come l'esplorazione dei dati tooperform, modellazione e assegnazione dei punteggi in Spark 2.0 cluster.</span><span class="sxs-lookup"><span data-stu-id="49da0-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="49da0-157">Il programma di installazione: hello, librerie e percorsi di archiviazione predefinito contesto Spark</span><span class="sxs-lookup"><span data-stu-id="49da0-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="49da0-158">Spark è in grado di tooAzure tooread e di scrittura Blob di archiviazione (noto anche come WASB).</span><span class="sxs-lookup"><span data-stu-id="49da0-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="49da0-159">Pertanto, i dati esistenti archiviate possono essere elaborati utilizzando Spark e hello risultati WASB archiviato nuovamente in.</span><span class="sxs-lookup"><span data-stu-id="49da0-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="49da0-160">modelli toosave o file in WASB, percorso hello deve toobe specificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="49da0-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="49da0-161">Hello del cluster Spark toohello contenitore collegato predefinito possibile farvi riferimento tramite un che inizia con: "wasb: / / /".</span><span class="sxs-lookup"><span data-stu-id="49da0-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="49da0-162">"wasb://" fa riferimento ad altri percorsi.</span><span class="sxs-lookup"><span data-stu-id="49da0-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="49da0-163">Impostare percorsi di directory per i percorsi di archiviazione in WASB</span><span class="sxs-lookup"><span data-stu-id="49da0-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="49da0-164">esempio di codice seguente Hello Specifica percorso hello di hello dati toobe leggere e hello percorso per l'output di hello modello archiviazione directory toowhich hello modello viene salvato:</span><span class="sxs-lookup"><span data-stu-id="49da0-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="49da0-165">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-165">**OUTPUT**</span></span>

<span data-ttu-id="49da0-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="49da0-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="49da0-167">Importare le librerie</span><span class="sxs-lookup"><span data-stu-id="49da0-167">Import libraries</span></span>
<span data-ttu-id="49da0-168">Importare le librerie necessarie con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="49da0-168">Import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="49da0-169">Contesto di Spark preimpostato e magic di PySpark</span><span class="sxs-lookup"><span data-stu-id="49da0-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="49da0-170">kernel PySpark Hello forniti con i notebook Jupyter dispone di un contesto predefinito.</span><span class="sxs-lookup"><span data-stu-id="49da0-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="49da0-171">Pertanto, non è necessario contesti di Spark o Hive hello tooset in modo esplicito prima di iniziare con un'applicazione hello che si sta sviluppando.</span><span class="sxs-lookup"><span data-stu-id="49da0-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="49da0-172">Questi contesti sono disponibili per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="49da0-172">These contexts are available for you by default.</span></span> <span data-ttu-id="49da0-173">Questi contesti sono:</span><span class="sxs-lookup"><span data-stu-id="49da0-173">These contexts are:</span></span>

* <span data-ttu-id="49da0-174">sc per Spark</span><span class="sxs-lookup"><span data-stu-id="49da0-174">sc - for Spark</span></span> 
* <span data-ttu-id="49da0-175">sqlContext per Hive</span><span class="sxs-lookup"><span data-stu-id="49da0-175">sqlContext - for Hive</span></span>

<span data-ttu-id="49da0-176">Hello kernel PySpark fornisce alcuni predefinite "magics", che sono comandi speciale che è possibile chiamare con % %.</span><span class="sxs-lookup"><span data-stu-id="49da0-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="49da0-177">Negli esempi di codice seguenti sono usati due comandi di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="49da0-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="49da0-178">**% % locale** specifica che il codice hello nelle righe successive toobe eseguite localmente.</span><span class="sxs-lookup"><span data-stu-id="49da0-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="49da0-179">Deve trattarsi di codice Python valido.</span><span class="sxs-lookup"><span data-stu-id="49da0-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="49da0-180">**% % sql -o <variable name>**  esegue una query Hive sqlContext hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="49da0-181">Se viene passato il parametro -o hello, il risultato di hello di hello query è persistente nel hello % % contesto Python locale come un frame di dati Pandas.</span><span class="sxs-lookup"><span data-stu-id="49da0-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="49da0-182">Per ulteriori informazioni su kernel hello per notebook Jupyter e hello predefiniti "magics" che forniscono, vedere [cluster kernel disponibile per i server Jupyter notebook con Linux di HDInsight Spark in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="49da0-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="49da0-183">Inserimento di dati dal BLOB pubblico:</span><span class="sxs-lookup"><span data-stu-id="49da0-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="49da0-184">Hello primo passaggio nel processo di analisi scientifica dei dati hello è tooingest hello dati toobe analizzati da origini in cui si trova nell'ambiente di esplorazione e modellazione di dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="49da0-185">In questa procedura dettagliata l'ambiente è Spark.</span><span class="sxs-lookup"><span data-stu-id="49da0-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="49da0-186">In questa sezione contiene toocomplete codice hello una serie di attività:</span><span class="sxs-lookup"><span data-stu-id="49da0-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="49da0-187">inserimento hello dati esempio toobe modellata</span><span class="sxs-lookup"><span data-stu-id="49da0-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="49da0-188">leggere nel set di input dati hello (archiviati come file tsv)</span><span class="sxs-lookup"><span data-stu-id="49da0-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="49da0-189">formato e dati hello pulita</span><span class="sxs-lookup"><span data-stu-id="49da0-189">format and clean hello data</span></span>
* <span data-ttu-id="49da0-190">Creazione di oggetti, RDD o frame di dati, e memorizzazione nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="49da0-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="49da0-191">Registrazione come tabella temporanea in un contesto SQL.</span><span class="sxs-lookup"><span data-stu-id="49da0-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="49da0-192">Ecco il codice hello per l'inserimento di dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-192">Here is hello code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-193">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-193">**OUTPUT**</span></span>

<span data-ttu-id="49da0-194">Tempo impiegato tooexecute di sopra di: 276.62 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="49da0-195">Visualizzazione ed esplorazione dei dati</span><span class="sxs-lookup"><span data-stu-id="49da0-195">Data exploration & visualization</span></span>
<span data-ttu-id="49da0-196">Dopo aver inseriti dati hello in Spark, hello il passaggio successivo nel processo di analisi scientifica dei dati hello è toogain comprensione più approfondita dei dati di hello tramite l'esplorazione e la visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="49da0-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="49da0-197">In questa sezione è esaminare i dati di taxi hello utilizzando le query SQL e le variabili di destinazione di tracciato hello e funzionalità potenziali per l'esame visivo.</span><span class="sxs-lookup"><span data-stu-id="49da0-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="49da0-198">Nello specifico, abbiamo tracciare frequenza hello dei conteggi di passeggeri in taxi trip, hello della frequenza degli importi di suggerimento e come suggerimenti variano a seconda del tipo e la quantità di pagamento.</span><span class="sxs-lookup"><span data-stu-id="49da0-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="49da0-199">Tracciare un istogramma che mostra le frequenze di conteggio di passeggeri nell'esempio hello di trip taxi</span><span class="sxs-lookup"><span data-stu-id="49da0-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="49da0-200">Questo codice e i successivi frammenti di codice è possibile utilizzare SQL tooquery magic hello dati di esempio e locale tooplot magic hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="49da0-201">**Chiave SQL (`%%sql`)** HDInsight PySpark kernel hello supporta hello sqlContext query HiveQL facile inline.</span><span class="sxs-lookup"><span data-stu-id="49da0-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="49da0-202">Hello (-o VARIABLE_NAME) argomento mantiene l'output di hello di query SQL hello sotto forma di un frame di dati Pandas server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="49da0-203">Ciò significa che è disponibile in modalità locale hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="49da0-204">Hello  **`%%local` magic** viene utilizzato codice toorun localmente nel server di Jupyter hello, ovvero hello nodo head del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="49da0-205">In genere, si utilizza `%%local` magic dopo hello `%%sql -o` magic è toorun utilizzata una query.</span><span class="sxs-lookup"><span data-stu-id="49da0-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="49da0-206">il parametro -o Hello sarebbe ancora valide output di hello di query SQL hello in locale.</span><span class="sxs-lookup"><span data-stu-id="49da0-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="49da0-207">Quindi hello `%%local` trigger magic hello set successivo di toorun frammenti di codice in locale sull'output di hello delle query SQL hello che ha reso persistente in locale.</span><span class="sxs-lookup"><span data-stu-id="49da0-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="49da0-208">output di Hello viene automaticamente visualizzato dopo l'esecuzione di codice hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="49da0-209">Questa query recupera trip hello dal conteggio di passeggeri.</span><span class="sxs-lookup"><span data-stu-id="49da0-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="49da0-210">Questo codice crea un frame di dati locale dall'output di hello query e vengono tracciati dati hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="49da0-211">Hello `%%local` magic crea un frame di dati locale, `sqlResults`, che può essere usato per il tracciato con matplotlib.</span><span class="sxs-lookup"><span data-stu-id="49da0-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="49da0-212">Tale magic PySpark viene usato più volte in questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="49da0-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="49da0-213">Se è grande quantità di hello di dati, si deve esempio toocreate un frame di dati che può adattarsi alla memoria locale.</span><span class="sxs-lookup"><span data-stu-id="49da0-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="49da0-214">Ecco trip di hello tooplot codice hello da passeggero conteggi</span><span class="sxs-lookup"><span data-stu-id="49da0-214">Here is hello code tooplot hello trips by passenger counts</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="49da0-215">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-215">**OUTPUT**</span></span>

![Frequenza delle corse per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="49da0-217">È possibile scegliere tra diversi tipi di visualizzazioni (tabella, a torta, linea, Area o barra) utilizzando hello **tipo** pulsanti di menu in blocco per Appunti hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="49da0-218">tracciato barra Hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="49da0-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="49da0-219">Tracciare un istogramma dell'importo delle mance e della relativa variazione in base al numero di passeggeri e all'importo delle corse.</span><span class="sxs-lookup"><span data-stu-id="49da0-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="49da0-220">Utilizzare una data di toosample query SQL...</span><span class="sxs-lookup"><span data-stu-id="49da0-220">Use a SQL query toosample data..</span></span>

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


<span data-ttu-id="49da0-221">Questa cella codice utilizza hello SQL query toocreate tre vengono tracciati hello dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="49da0-222">**OUTPUT:**</span><span class="sxs-lookup"><span data-stu-id="49da0-222">**OUTPUT:**</span></span> 

![Distribuzione dell'importo delle mance](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Importo della mancia per numero di passeggeri](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Importo della mancia per importo della corsa](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="49da0-226">Progettazione di funzionalità, trasformazione e preparazione dei dati per la modellazione</span><span class="sxs-lookup"><span data-stu-id="49da0-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="49da0-227">In questa sezione descrive e fornisce codice hello per le procedure utilizzate tooprepare dati per la modellazione di ML.</span><span class="sxs-lookup"><span data-stu-id="49da0-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="49da0-228">Viene illustrato come hello toodo seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="49da0-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="49da0-229">Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="49da0-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="49da0-230">Indicizzare funzionalità categoriche e applicare la codifica one-hot</span><span class="sxs-lookup"><span data-stu-id="49da0-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="49da0-231">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="49da0-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="49da0-232">Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing</span><span class="sxs-lookup"><span data-stu-id="49da0-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="49da0-233">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="49da0-233">Feature scaling</span></span>
* <span data-ttu-id="49da0-234">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="49da0-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="49da0-235">Creare una nuova funzionalità dalla partizione di contenitori per gli orari di trasporto</span><span class="sxs-lookup"><span data-stu-id="49da0-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="49da0-236">Questo codice viene illustrato come toocreate sempre una nuova funzionalità suddividendo il traffico in bin e come toocache hello risultante frame di dati in memoria.</span><span class="sxs-lookup"><span data-stu-id="49da0-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="49da0-237">La memorizzazione nella cache comporta il tempo di esecuzione tooimproved dove resilienti Distributed set di dati (RDDs) e frame di dati vengono utilizzati più volte.</span><span class="sxs-lookup"><span data-stu-id="49da0-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="49da0-238">RDD e frame di dati vengono quindi memorizzati nella cache in varie fasi di questa procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="49da0-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="49da0-239">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-239">**OUTPUT**</span></span>

<span data-ttu-id="49da0-240">126050</span><span class="sxs-lookup"><span data-stu-id="49da0-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="49da0-241">Indicizzare funzionalità categoriche e applicare la codifica one-hot</span><span class="sxs-lookup"><span data-stu-id="49da0-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="49da0-242">Questa sezione viene illustrato come tooindex o codificare categorica funzionalità per l'input nel hello funzioni di modellazione.</span><span class="sxs-lookup"><span data-stu-id="49da0-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="49da0-243">Hello modellazione e stimare le funzioni di MLlib richiedono che funzionalità organizzato per categorie dei dati di input deve essere indicizzata o codificata toouse precedente.</span><span class="sxs-lookup"><span data-stu-id="49da0-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="49da0-244">A seconda del modello di hello, è necessario tooindex o codificarli in modi diversi.</span><span class="sxs-lookup"><span data-stu-id="49da0-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="49da0-245">Ad esempio, modelli Logistic e regressione lineare richiedono hot una codifica, in cui, ad esempio, una funzionalità costituita da tre categorie può essere espanso in tre colonne di funzionalità, con ogni contiene 0 o 1 a seconda della categoria di hello di un'osservazione.</span><span class="sxs-lookup"><span data-stu-id="49da0-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="49da0-246">Fornisce MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) funzione toodo hot una codifica.</span><span class="sxs-lookup"><span data-stu-id="49da0-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="49da0-247">Questo codificatore esegue il mapping di una colonna della colonna di etichetta indici tooa di vettori binari, con al massimo uno a valore singolo.</span><span class="sxs-lookup"><span data-stu-id="49da0-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="49da0-248">Questa codifica consente di utilizzare gli algoritmi che prevedono le funzionalità di valori numeriche, ad esempio la regressione logistica, funzionalità toocategorical toobe applicato.</span><span class="sxs-lookup"><span data-stu-id="49da0-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="49da0-249">Ecco hello tooindex codice e codificare funzionalità organizzato per categorie:</span><span class="sxs-lookup"><span data-stu-id="49da0-249">Here is hello code tooindex and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="49da0-250">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-250">**OUTPUT**</span></span>

<span data-ttu-id="49da0-251">Tempo impiegato tooexecute di sopra di: 3,14 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="49da0-252">Creare oggetti punto etichettato per l'inserimento in funzioni di apprendimento automatico</span><span class="sxs-lookup"><span data-stu-id="49da0-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="49da0-253">In questa sezione contiene codice che illustra come tipo di dati di testo categorico tooindex come etichetta punto dati e come tooencode è.</span><span class="sxs-lookup"><span data-stu-id="49da0-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="49da0-254">Questa funzione Prepara, toobe utilizzato tootrain test MLlib la regressione logistica ed e altri modelli di classificazione.</span><span class="sxs-lookup"><span data-stu-id="49da0-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="49da0-255">Gli oggetti punto etichettato sono RDD (Resilient Distributed Dataset) formattati come richiesto per i dati di input dalla maggior parte degli algoritmi di apprendimento automatico in MLlib.</span><span class="sxs-lookup"><span data-stu-id="49da0-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="49da0-256">Un [punto etichettato](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) è un vettore locale, che può essere denso o sparso, associato a un'etichetta o a una risposta.</span><span class="sxs-lookup"><span data-stu-id="49da0-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="49da0-257">Ecco hello tooindex codice e codificare le funzionalità di testo per la classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="49da0-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="49da0-258">Ecco il codice hello tooencode indice testo categorico funzionalità per l'analisi di regressione lineare.</span><span class="sxs-lookup"><span data-stu-id="49da0-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="49da0-259">Creare un campionamento secondario casuale dei dati hello e dividere il set di training e set di testing</span><span class="sxs-lookup"><span data-stu-id="49da0-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="49da0-260">Questo codice crea un campionamento casuale dei dati di hello (25% viene utilizzato qui).</span><span class="sxs-lookup"><span data-stu-id="49da0-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="49da0-261">Anche se non sono richiesto per questo esempio a causa delle dimensioni toohello di hello set di dati, viene illustrato come è possibile campionare i dati hello qui.</span><span class="sxs-lookup"><span data-stu-id="49da0-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="49da0-262">Si può stabilire come toouse per il proprio problema se necessario.</span><span class="sxs-lookup"><span data-stu-id="49da0-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="49da0-263">Nei campioni di grandi dimensioni questa operazione permette di risparmiare molto tempo durante il training dei modelli.</span><span class="sxs-lookup"><span data-stu-id="49da0-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="49da0-264">Successivamente è suddivisa: esempio hello una parte di training (75%) e un test toouse parte (25 %)) nella classificazione e creazione di modelli di regressione.</span><span class="sxs-lookup"><span data-stu-id="49da0-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="49da0-265">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-265">**OUTPUT**</span></span>

<span data-ttu-id="49da0-266">Tempo impiegato tooexecute di sopra di: 0,31 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="49da0-267">Ridimensionamento di funzionalità</span><span class="sxs-lookup"><span data-stu-id="49da0-267">Feature scaling</span></span>
<span data-ttu-id="49da0-268">Funzionalità di scalabilità, noto anche come normalizzazione dei dati, si assicura che le funzionalità con ampiamente i valori sono non specificato un numero eccessivo pesare nella funzione obiettivo hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="49da0-269">codice per la funzionalità scalabilità Hello Usa hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) varianza di toounit tooscale hello funzionalità.</span><span class="sxs-lookup"><span data-stu-id="49da0-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="49da0-270">Viene fornito da MLlib per l'uso nella regressione lineare con Stochastic Gradient Descent (SGD).</span><span class="sxs-lookup"><span data-stu-id="49da0-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="49da0-271">SGD è un algoritmo molto diffuso per il training di una vasta gamma di modelli di apprendimento automatico, come la regressione regolarizzata o le macchine a vettori di supporto (SVM).</span><span class="sxs-lookup"><span data-stu-id="49da0-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="49da0-272">È stato trovato il ridimensionamento di hello LinearRegressionWithSGD algoritmo toobe toofeature sensibili.</span><span class="sxs-lookup"><span data-stu-id="49da0-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="49da0-273">Ecco le variabili di tooscale codice hello per l'utilizzo con l'algoritmo SGD lineare di regolarizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="49da0-274">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-274">**OUTPUT**</span></span>

<span data-ttu-id="49da0-275">Tempo impiegato tooexecute di sopra di: 11.67 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="49da0-276">Memorizzazione nella cache di oggetti in memoria</span><span class="sxs-lookup"><span data-stu-id="49da0-276">Cache objects in memory</span></span>
<span data-ttu-id="49da0-277">tempo per il training e testing di algoritmi di Machine Learning Hello può essere ridotto limitando la memorizzazione nella cache i frame di dati di input hello gli oggetti utilizzati per la classificazione di regressione e, con funzionalità di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="49da0-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="49da0-278">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-278">**OUTPUT**</span></span> 

<span data-ttu-id="49da0-279">Tempo impiegato tooexecute di sopra di: 0,13 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="49da0-280">Uso di modelli di classificazione binaria per prevedere se viene lasciata o meno una mancia</span><span class="sxs-lookup"><span data-stu-id="49da0-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="49da0-281">In questa sezione viene illustrato come utilizzare tre modelli per attività di classificazione binaria hello di stima di un suggerimento viene pagato per un itinerario taxi o meno.</span><span class="sxs-lookup"><span data-stu-id="49da0-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="49da0-282">modelli di Hello presentati sono:</span><span class="sxs-lookup"><span data-stu-id="49da0-282">hello models presented are:</span></span>

* <span data-ttu-id="49da0-283">Regressione logistica</span><span class="sxs-lookup"><span data-stu-id="49da0-283">Logistic regression</span></span> 
* <span data-ttu-id="49da0-284">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="49da0-284">Random forest</span></span>
* <span data-ttu-id="49da0-285">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="49da0-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="49da0-286">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="49da0-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="49da0-287">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="49da0-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="49da0-288">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="49da0-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="49da0-289">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="49da0-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="49da0-290">Viene illustrato come toodo convalida incrociata (CV) con il parametro sweep in due modi:</span><span class="sxs-lookup"><span data-stu-id="49da0-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="49da0-291">Utilizzando **generico** codice personalizzato che può essere applicato tooany algoritmo nel parametro MLlib e tooany imposta in un algoritmo.</span><span class="sxs-lookup"><span data-stu-id="49da0-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="49da0-292">Utilizzo di hello **pySpark funzione pipeline CrossValidator**.</span><span class="sxs-lookup"><span data-stu-id="49da0-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="49da0-293">Si noti che CrossValidator presenta alcune limitazioni per Spark 1.5.0:</span><span class="sxs-lookup"><span data-stu-id="49da0-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="49da0-294">I modelli di pipeline non possono essere salvati/resi persistenti per un utilizzo futuro.</span><span class="sxs-lookup"><span data-stu-id="49da0-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="49da0-295">Non può essere usato per ogni parametro in un modello.</span><span class="sxs-lookup"><span data-stu-id="49da0-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="49da0-296">Non può essere usato per ogni algoritmo MLlib.</span><span class="sxs-lookup"><span data-stu-id="49da0-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="49da0-297">Generico tra la convalida e lo sweep hyperparameter utilizzati con l'algoritmo di regressione logistica hello per la classificazione binaria</span><span class="sxs-lookup"><span data-stu-id="49da0-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="49da0-298">codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet.</span><span class="sxs-lookup"><span data-stu-id="49da0-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="49da0-299">Training del modello Hello tra la convalida (CV) e lo sweep hyperparameter implementato con codice personalizzato che può essere applicato tooany di hello in MLlib algoritmi di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="49da0-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="49da0-300">esecuzione di Hello del codice personalizzato CV può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="49da0-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="49da0-301">**Training modello di regressione logistica hello utilizzando CV e hyperparameter sweep**</span><span class="sxs-lookup"><span data-stu-id="49da0-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-302">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-302">**OUTPUT**</span></span>

<span data-ttu-id="49da0-303">Coefficienti: [0,0082065285375, -0,0223675576104, -0,0183812028036, -3,48124578069e-05, -0,00247646947233, -0,00165897881503, 0,0675394837328, -0,111823113101, -0,324609912762, -0,204549780032, -1,36499216354, 0,591088507921, -0,664263411392, -1,00439726852, 3,46567827545, -3,51025855172, -0,0471341112232, -0,043521833294, 0,000243375810385, 0,054518719222]</span><span class="sxs-lookup"><span data-stu-id="49da0-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="49da0-304">Intercetta: -0,0111216486893</span><span class="sxs-lookup"><span data-stu-id="49da0-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="49da0-305">Tempo impiegato tooexecute di sopra di: 14.43 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="49da0-306">**Valutazione del modello di classificazione binaria hello con le metriche standard**</span><span class="sxs-lookup"><span data-stu-id="49da0-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="49da0-307">codice Hello in questa sezione viene illustrato come tooevaluate una regressione logistica del modello su un test-set di dati, tra cui un tracciato di hello curva ROC.</span><span class="sxs-lookup"><span data-stu-id="49da0-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-308">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-308">**OUTPUT**</span></span>

<span data-ttu-id="49da0-309">Area in PR = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="49da0-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="49da0-310">Area in ROC = 0,983383274312</span><span class="sxs-lookup"><span data-stu-id="49da0-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="49da0-311">Statistiche di riepilogo</span><span class="sxs-lookup"><span data-stu-id="49da0-311">Summary Stats</span></span>

<span data-ttu-id="49da0-312">Precisione = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="49da0-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="49da0-313">Richiamo = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="49da0-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="49da0-314">Punteggio F1 = 0,984174341679</span><span class="sxs-lookup"><span data-stu-id="49da0-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="49da0-315">Tempo impiegato tooexecute di sopra di: 2.67 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="49da0-316">**Tracciare una curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="49da0-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="49da0-317">Hello *predictionAndLabelsDF* viene registrato come una tabella, *tmp_results*, nella cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="49da0-318">*tmp_results* possibile toodo utilizzato query e restituire i risultati in hello sqlResults-frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="49da0-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="49da0-319">Ecco il codice hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="49da0-320">Ecco le stime di toomake codice hello e hello tracciato curva ROC.</span><span class="sxs-lookup"><span data-stu-id="49da0-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="49da0-321">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-321">**OUTPUT**</span></span>

![Curva ROC di regressione logistica per approccio generico](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="49da0-323">**Rendere persistente il modello in un BLOB per l'utilizzo in futuro**</span><span class="sxs-lookup"><span data-stu-id="49da0-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="49da0-324">codice Hello in questa sezione viene illustrato come la regressione logistica toosave hello del modello per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="49da0-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="49da0-325">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-325">**OUTPUT**</span></span>

<span data-ttu-id="49da0-326">Tempo impiegato tooexecute di sopra di: 34.57 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="49da0-327">Usare la funzione della pipeline CrossValidator di MLlib con il modello di regressione logistica (regressione elastica)</span><span class="sxs-lookup"><span data-stu-id="49da0-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="49da0-328">codice Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di regressione logistica con [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) che esegue una stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa DataSet.</span><span class="sxs-lookup"><span data-stu-id="49da0-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="49da0-329">Training del modello Hello utilizzando la convalida incrociata (CV) e hyperparameter sweep con hello MLlib CrossValidator pipeline funzione implementata per CV con sweep di parametri.</span><span class="sxs-lookup"><span data-stu-id="49da0-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="49da0-330">esecuzione di Hello del codice MLlib CV può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="49da0-330">hello execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="49da0-331">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-331">**OUTPUT**</span></span>

<span data-ttu-id="49da0-332">Tempo impiegato tooexecute di sopra di: 107.98 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="49da0-333">**Tracciare una curva ROC hello.**</span><span class="sxs-lookup"><span data-stu-id="49da0-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="49da0-334">Hello *predictionAndLabelsDF* viene registrato come una tabella, *tmp_results*, nella cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="49da0-335">*tmp_results* possibile toodo utilizzato query e restituire i risultati in hello sqlResults-frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="49da0-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="49da0-336">Ecco il codice hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="49da0-337">Di seguito è riportata la curva ROC hello codice tooplot hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-337">Here is hello code tooplot hello ROC curve.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="49da0-338">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-338">**OUTPUT**</span></span>

![Curva ROC di regressione logistica con CrossValidator di MLlib](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="49da0-340">Classificazione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="49da0-340">Random forest classification</span></span>
<span data-ttu-id="49da0-341">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare una regressione foresta casuale che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT tooPRING TREES
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


<span data-ttu-id="49da0-342">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-342">**OUTPUT**</span></span>

<span data-ttu-id="49da0-343">Area in ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="49da0-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="49da0-344">Tempo impiegato tooexecute di sopra di: 26.72 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="49da0-345">Classificazione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="49da0-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="49da0-346">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima o meno un suggerimento viene pagato per un itinerario hello NYC taxi di andata e ritorno e tariffa set di dati.</span><span class="sxs-lookup"><span data-stu-id="49da0-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="49da0-347">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-347">**OUTPUT**</span></span>

<span data-ttu-id="49da0-348">Area in ROC = 0,985336538462</span><span class="sxs-lookup"><span data-stu-id="49da0-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="49da0-349">Tempo impiegato tooexecute di sopra di: 28.13 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="49da0-350">Prevedere l'importo delle mance con di modelli di regressione (senza usare la convalida incrociata)</span><span class="sxs-lookup"><span data-stu-id="49da0-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="49da0-351">Questa sezione viene illustrato come utilizzare tre modelli per attività di regressione hello: stimare hello suggerimento quantità pagata per un itinerario taxi basato sulle altre funzionalità di suggerimento.</span><span class="sxs-lookup"><span data-stu-id="49da0-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="49da0-352">modelli di Hello presentati sono:</span><span class="sxs-lookup"><span data-stu-id="49da0-352">hello models presented are:</span></span>

* <span data-ttu-id="49da0-353">Regressione lineare regolarizzata</span><span class="sxs-lookup"><span data-stu-id="49da0-353">Regularized linear regression</span></span>
* <span data-ttu-id="49da0-354">Foresta casuale</span><span class="sxs-lookup"><span data-stu-id="49da0-354">Random forest</span></span>
* <span data-ttu-id="49da0-355">Alberi con boosting a gradienti.</span><span class="sxs-lookup"><span data-stu-id="49da0-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="49da0-356">Questi modelli sono stati descritti introduzione hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-356">These models were described in hello introduction.</span></span> <span data-ttu-id="49da0-357">Ogni sezione di codice di compilazione del modello è suddivisa in passaggi:</span><span class="sxs-lookup"><span data-stu-id="49da0-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="49da0-358">**training del modello** con un set di parametri</span><span class="sxs-lookup"><span data-stu-id="49da0-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="49da0-359">**Valutazione del modello** su un set di dati di test con metriche</span><span class="sxs-lookup"><span data-stu-id="49da0-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="49da0-360">**Salvataggio del modello** in un BLOB per l'uso in futuro</span><span class="sxs-lookup"><span data-stu-id="49da0-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="49da0-361">AZURE Nota: La convalida incrociata non viene usata con hello tre i modelli di regressione in questa sezione, poiché questa operazione è stata illustrata in dettaglio per i modelli di regressione logistica hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="49da0-362">Un esempio che illustra come toouse CV con elastico netto per la regressione lineare viene fornito in hello appendice di questo argomento.</span><span class="sxs-lookup"><span data-stu-id="49da0-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="49da0-363">AZURE Nota: Nella nostra esperienza, possono esserci problemi con la convergenza dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="49da0-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="49da0-364">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="49da0-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="49da0-365">Regressione net elastica, illustrata nell'argomento toothis appendice hello nonché anziché LinearRegressionWithSGD.</span><span class="sxs-lookup"><span data-stu-id="49da0-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="49da0-366">Regressione lineare con SGD</span><span class="sxs-lookup"><span data-stu-id="49da0-366">Linear regression with SGD</span></span>
<span data-ttu-id="49da0-367">Hello codice in questa sezione viene illustrato come toouse scalato funzionalità tootrain una regressione lineare che usa descent con sfumatura stocastica (SGD) per l'ottimizzazione, e come tooscore, valutare e salvare il modello di hello in archiviazione Blob di Azure (WASB).</span><span class="sxs-lookup"><span data-stu-id="49da0-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="49da0-368">Nella nostra esperienza, si possono verificare problemi con convergenza hello dei modelli LinearRegressionWithSGD e parametri necessario toobe modificato/ottimizzata con attenzione per ottenere un modello valido.</span><span class="sxs-lookup"><span data-stu-id="49da0-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="49da0-369">Il ridimensionamento delle variabili può essere molto utile per la convergenza.</span><span class="sxs-lookup"><span data-stu-id="49da0-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="49da0-370">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-370">**OUTPUT**</span></span>

<span data-ttu-id="49da0-371">Coefficienti: [0,0141707753435, -0,0252930927087, -0,0231442517137, 0,247070902996, 0,312544147152, 0,360296120645, 0,0122079566092, -0,00456498588241, -0,0898228505177, 0,0714046248793, 0,102171263868, 0,100022455632, -0,00289545676449, -0,00791124681938, 0,54396316518, -0,536293513569, 0,0119076553369, -0,0173039244582, 0,0119632796147, 0,00146764882502]</span><span class="sxs-lookup"><span data-stu-id="49da0-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="49da0-372">Intercetta: 0,854507624459</span><span class="sxs-lookup"><span data-stu-id="49da0-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="49da0-373">RMSE = 1,23485131376</span><span class="sxs-lookup"><span data-stu-id="49da0-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="49da0-374">R-sqr = 0,597963951127</span><span class="sxs-lookup"><span data-stu-id="49da0-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="49da0-375">Tempo impiegato tooexecute di sopra di: 38.62 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="49da0-376">Regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="49da0-376">Random Forest regression</span></span>
<span data-ttu-id="49da0-377">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di foresta casuale che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="49da0-378">La convalida incrociata con parametro sweep con codice personalizzato viene fornita nell'appendice hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT tooPRING TREES
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="49da0-379">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-379">**OUTPUT**</span></span>

<span data-ttu-id="49da0-380">RMSE = 0,931981967875</span><span class="sxs-lookup"><span data-stu-id="49da0-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="49da0-381">R-sqr = 0,733445485802</span><span class="sxs-lookup"><span data-stu-id="49da0-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="49da0-382">Tempo impiegato tooexecute di sopra di: 25.98 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="49da0-383">Regressione tramite alberi con boosting a gradienti</span><span class="sxs-lookup"><span data-stu-id="49da0-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="49da0-384">codice di Hello in questa sezione viene illustrato come tootrain, valutare e salvare un modello di alberi boosting sfumatura che stima quantità suggerimento per dati di andata e ritorno taxi NYC hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="49da0-385">**Eseguire il training e valutare**</span><span class="sxs-lookup"><span data-stu-id="49da0-385">**Train and evaluate **</span></span>

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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-386">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-386">**OUTPUT**</span></span>

<span data-ttu-id="49da0-387">RMSE = 0,928172197114</span><span class="sxs-lookup"><span data-stu-id="49da0-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="49da0-388">R-sqr = 0,732680354389</span><span class="sxs-lookup"><span data-stu-id="49da0-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="49da0-389">Tempo impiegato tooexecute di sopra di: 20,9 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="49da0-390">**Grafico**</span><span class="sxs-lookup"><span data-stu-id="49da0-390">**Plot**</span></span>

<span data-ttu-id="49da0-391">*tmp_results* viene registrato come una tabella Hive in una cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="49da0-392">I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="49da0-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="49da0-393">Ecco il codice hello</span><span class="sxs-lookup"><span data-stu-id="49da0-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="49da0-394">Ecco dati hello tooplot codice hello utilizzando server Jupyter hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="49da0-396">Appendice: Attività di regressione aggiuntive tramite convalida incrociata con sweep di parametri</span><span class="sxs-lookup"><span data-stu-id="49da0-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="49da0-397">Questa appendice contiene una visualizzazione di codice come CV toodo tramite net elastico per la regressione lineare e come CV toodo con parametro sweep con codice personalizzato per la regressione di foresta casuale.</span><span class="sxs-lookup"><span data-stu-id="49da0-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="49da0-398">Convalida incrociata con Elastic Net per la regressione lineare</span><span class="sxs-lookup"><span data-stu-id="49da0-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="49da0-399">codice di Hello in questa sezione viene illustrato come toodo superano la convalida utilizzando elastica netto per la regressione lineare e come tooevaluate hello modello rispetto a dati di test.</span><span class="sxs-lookup"><span data-stu-id="49da0-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

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
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-400">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-400">**OUTPUT**</span></span>

<span data-ttu-id="49da0-401">Tempo impiegato tooexecute di sopra di: 161.21 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="49da0-402">**Eseguire la valutazione con la metrica R-SQR**</span><span class="sxs-lookup"><span data-stu-id="49da0-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="49da0-403">*tmp_results* viene registrato come una tabella Hive in una cella precedente hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="49da0-404">I risultati dalla tabella hello vengono visualizzati in hello *sqlResults* frame di dati per il tracciato.</span><span class="sxs-lookup"><span data-stu-id="49da0-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="49da0-405">Ecco il codice hello</span><span class="sxs-lookup"><span data-stu-id="49da0-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="49da0-406">Di seguito è toocalculate codice hello sqr di R.</span><span class="sxs-lookup"><span data-stu-id="49da0-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="49da0-407">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-407">**OUTPUT**</span></span>

<span data-ttu-id="49da0-408">R-sqr = 0,619184907088</span><span class="sxs-lookup"><span data-stu-id="49da0-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="49da0-409">Convalida incrociata con sweep di parametri usando codice personalizzato per la regressione tramite foresta casuale</span><span class="sxs-lookup"><span data-stu-id="49da0-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="49da0-410">codice di Hello in questa sezione viene illustrato come toodo convalida incrociata con lo sweep di parametri con codice personalizzato per la regressione di foreste casuali e come tooevaluate hello modello rispetto a dati di test.</span><span class="sxs-lookup"><span data-stu-id="49da0-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
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
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="49da0-411">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-411">**OUTPUT**</span></span>

<span data-ttu-id="49da0-412">RMSE = 0,906972198262</span><span class="sxs-lookup"><span data-stu-id="49da0-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="49da0-413">R-sqr = 0,740751197012</span><span class="sxs-lookup"><span data-stu-id="49da0-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="49da0-414">Tempo impiegato tooexecute di sopra di: 69.17 secondi</span><span class="sxs-lookup"><span data-stu-id="49da0-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="49da0-415">Pulire gli oggetti dalla memoria e stampare i percorsi dei modelli</span><span class="sxs-lookup"><span data-stu-id="49da0-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="49da0-416">Utilizzare `unpersist()` toodelete oggetti memorizzati nella cache in memoria.</span><span class="sxs-lookup"><span data-stu-id="49da0-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


<span data-ttu-id="49da0-417">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-417">**OUTPUT**</span></span>

<span data-ttu-id="49da0-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="49da0-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="49da0-419">* * Stampa percorso toomodel file toobe utilizzato in blocco per Appunti consumo hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="49da0-420">* * tooconsume e punteggio indipendente-set di dati, è necessario toocopy e incollare questi nomi di file in "Notebook consumo" hello.</span><span class="sxs-lookup"><span data-stu-id="49da0-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="49da0-421">**OUTPUT**</span><span class="sxs-lookup"><span data-stu-id="49da0-421">**OUTPUT**</span></span>

<span data-ttu-id="49da0-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="49da0-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="49da0-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="49da0-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="49da0-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="49da0-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="49da0-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="49da0-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="49da0-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="49da0-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="49da0-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="49da0-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="49da0-428">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="49da0-428">What's next?</span></span>
<span data-ttu-id="49da0-429">Dopo aver creato i modelli di classificazione e regressione con MlLib Spark hello, si è toolearn pronto come tooscore e valutare questi modelli.</span><span class="sxs-lookup"><span data-stu-id="49da0-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="49da0-430">**Utilizzo del modello:** toolearn come tooscore e valutare i modelli di classificazione e regressione hello creati in questo argomento, vedere [punteggio e valutare i modelli di apprendimento macchina compilato Spark](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="49da0-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

