---
title: aaaA semplice esperimento in Machine Learning Studio | Documenti Microsoft
description: "Questa esercitazione di Machine Learning illustra un esperimento semplice di analisi scientifica dei dati. Si sarà stimare prezzo hello di un'automobile usando un algoritmo di regressione."
keywords: esperimento,regressione lineare,algoritmi di machine learning,esercitazione su machine learning,tecniche di modellazione predittiva,esperimento di analisi scientifica dei dati
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="4a9c8-105">Esercitazione di Machine Learning: Creare il primo esperimento di analisi scientifica dei dati in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4a9c8-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="4a9c8-106">Questa esercitazione è destinata agli utenti che non hanno mai usato **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="4a9c8-107">In questa esercitazione verranno esaminati come toouse Studio hello per la prima volta toocreate un esperimento di machine learning.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="4a9c8-108">sperimentazione Hello testerà un modello analitico che stima il prezzo di hello di un'automobile in base alle diverse variabili, ad esempio le specifiche tecniche e verificare.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="4a9c8-109">Questa esercitazione Mostra nozioni fondamentali di hello dei moduli come toodrag e rilascio nell'esperimento, collegarli, eseguire l'esperimento hello e visualizzare risultati hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="4a9c8-110">Non verrà toodiscuss hello argomento generale di machine learning o come tooselect e utilizzare hello 100 + dati e algoritmi manipolazione dei moduli predefiniti inclusi in Studio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="4a9c8-111">Se si è nuovo learning toomachine, hello serie di video [analisi scientifica dei dati per i principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) potrebbe essere toostart un buon punto.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="4a9c8-112">Questa serie di video è un learning toomachine introduzione grande utilizzando concetti e il linguaggio naturale.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="4a9c8-113">Se si ha familiarità con machine learning, ma si sta cercando le informazioni di carattere generale su Machine Learning Studio e hello algoritmi di machine learning che contiene, di seguito sono riportate alcune risorse validi:</span><span class="sxs-lookup"><span data-stu-id="4a9c8-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="4a9c8-114">Cos'è Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="4a9c8-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="4a9c8-115">: questa è una panoramica generale di Studio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="4a9c8-116">[Nozioni di base con esempi di algoritmi di apprendimento computer](machine-learning-basics-infographic-with-algorithm-examples.md) -questo infografica è utile se si desidera toolearn informazioni sui diversi tipi di hello algoritmi di machine learning inclusi in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="4a9c8-117">[Machine Learning Guida](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -questa guida vengono fornite le informazioni simili di hello infografica precedente, ma in un formato interattivo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="4a9c8-118">[Machine learning foglio informativo algoritmo](machine-learning-algorithm-cheat-sheet.md) e [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) -questo articolo e il poster scaricabile discutere algoritmi Studio hello in profondità.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="4a9c8-119">[Machine Learning Studio: Algoritmo e modulo della Guida](https://msdn.microsoft.com/library/azure/dn905974.aspx) -si tratta di hello riferimento completo di tutti i moduli di Studio, inclusi gli algoritmi di machine learning,</span><span class="sxs-lookup"><span data-stu-id="4a9c8-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="4a9c8-120">Vantaggi di Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4a9c8-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="4a9c8-121">Machine Learning Studio rende facile tooset di un esperimento usando i moduli di trascinamento e rilascio preprogrammati con le tecniche di modellazione predittiva.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="4a9c8-122">L'uso di un'area di lavoro interattiva grafica consente di selezionare e trascinare ***set di dati*** e ***moduli*** di analisi in un'area di disegno interattiva.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="4a9c8-123">Si connette tooform insieme un ***sperimentare*** che vengono eseguiti in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="4a9c8-124">Si ***creare un modello***, ***Training modello di hello***, e ***punteggio e test hello modello***.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="4a9c8-125">È possibile eseguire l'iterazione sulla struttura del modello, la modifica di sperimentazione hello e si esegue fino a quando offre hello risultati che si sta cercando.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="4a9c8-126">Quando il modello è pronto, è possibile pubblicarlo come ***servizio Web*** in modo che altri utenti possano inviare nuovi dati e ottenere stime in cambio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="4a9c8-127">Aprire Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="4a9c8-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="4a9c8-128">tooget introduttiva Studio, andare troppo[https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="4a9c8-129">Se è già stato effettuato l'accesso a Machine Learning Studio in precedenza, fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="4a9c8-130">In caso contrario fare clic su **Sign up here** (Effettuare l'iscrizione qui) e scegliere un'opzione gratuita o a pagamento.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="4a9c8-131">![Accedi tooMachine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="4a9c8-132">
***Accedi tooMachine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="4a9c8-133">Cinque passaggi toocreate un esperimento</span><span class="sxs-lookup"><span data-stu-id="4a9c8-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="4a9c8-134">In questa esercitazione machine learning sarà seguire cinque passaggi di base toobuild un esperimento di Machine Learning Studio toocreate, eseguire il training e assegnare un punteggio del modello:</span><span class="sxs-lookup"><span data-stu-id="4a9c8-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="4a9c8-135">**Creare un modello**</span><span class="sxs-lookup"><span data-stu-id="4a9c8-135">**Create a model**</span></span>
    - <span data-ttu-id="4a9c8-136">[Passaggio 1: Ottenere i dati]</span><span class="sxs-lookup"><span data-stu-id="4a9c8-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="4a9c8-137">[Passaggio 2: Preparare i dati di hello]</span><span class="sxs-lookup"><span data-stu-id="4a9c8-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="4a9c8-138">[Passaggio 3: Definire le caratteristiche]</span><span class="sxs-lookup"><span data-stu-id="4a9c8-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="4a9c8-139">**Modello di hello Train**</span><span class="sxs-lookup"><span data-stu-id="4a9c8-139">**Train hello model**</span></span>
    - <span data-ttu-id="4a9c8-140">[Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]</span><span class="sxs-lookup"><span data-stu-id="4a9c8-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="4a9c8-141">**Punteggio e test hello modello**</span><span class="sxs-lookup"><span data-stu-id="4a9c8-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="4a9c8-142">[Passaggio 5: Stimare i prezzi delle nuove automobili]</span><span class="sxs-lookup"><span data-stu-id="4a9c8-142">[Step 5: Predict new automobile prices]</span></span>

[Passaggio 1: Ottenere i dati]: #step-1-get-data
[Passaggio 2: Preparare i dati di hello]: #step-2-prepare-the-data
[Passaggio 3: Definire le caratteristiche]: #step-3-define-features
[Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]: #step-4-choose-and-apply-a-learning-algorithm
[Passaggio 5: Stimare i prezzi delle nuove automobili]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="4a9c8-148">È possibile trovare una copia di lavoro di hello seguente esperimento nella hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="4a9c8-149">Andare troppo**[l'analisi scientifica dei dati prima di provare - stima prezzo Automobile](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  e fare clic su **Open in Studio** toodownload una copia dell'esperimento hello nel Machine Learning Area di lavoro di Studio.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="4a9c8-150">Passaggio 1: Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="4a9c8-150">Step 1: Get data</span></span>

<span data-ttu-id="4a9c8-151">Hello occorre innanzitutto tooperform l'apprendimento è dati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="4a9c8-152">In Machine Learning Studio sono disponibili numerosi set di dati di esempio da usare oppure è possibile importare dati da molte altre origini.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="4a9c8-153">In questo esempio utilizzeremo i set di dati campione hello, **dati prezzo Automobile (Raw)**, che è incluso nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="4a9c8-154">Questo set di dati include voci per diverse automobili e include informazioni su marca, modello, specifiche tecniche e prezzo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="4a9c8-155">Ecco come tooget hello set di dati nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="4a9c8-156">Creare un nuovo esperimento facendo **+ nuovo** nella parte inferiore di hello della finestra di Machine Learning Studio hello, selezionare **SPERIMENTARE**, quindi selezionare **sperimentare vuoto**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="4a9c8-157">sperimentazione Hello viene assegnato un nome predefinito visualizzato nella parte superiore di hello dell'area di disegno hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="4a9c8-158">Selezionare il testo e rinominarlo toosomething significativo, ad esempio, **stima prezzo Automobile**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="4a9c8-159">nome Hello non deve necessariamente toobe univoco.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-159">hello name doesn't need toobe unique.</span></span>

    ![Rinominare l'esperimento hello][rename-experiment]

2. <span data-ttu-id="4a9c8-161">toohello a sinistra dell'area di disegno esperimento hello è una tavolozza dei moduli e dei set di dati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="4a9c8-162">Tipo **automobile** nella casella di ricerca hello nella parte superiore di hello del dataset hello toofind tavolozza con etichettato **dati prezzo Automobile (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="4a9c8-163">Trascinare l'area di disegno di set di dati toohello esperimento.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="4a9c8-164">![Trovare set di dati automobili hello e trascinarlo nell'area di disegno esperimento hello][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="4a9c8-165">***Trovare set di dati automobili hello e trascinarlo nell'area di disegno esperimento hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="4a9c8-166">toosee questo aspetto dati like, fare clic sulla porta di output di hello nella parte inferiore di hello del set di dati automobili hello e quindi selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="4a9c8-167">![Fare clic sulla porta di output di hello e selezionare "Visualizza"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="4a9c8-168">
***Fare clic sulla porta di output di hello e selezionare "Visualizza"***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="4a9c8-169">Set di dati e i moduli con input e le porte di output rappresentate da cerchi piccoli - porte di input nella parte superiore di hello, porte nella parte inferiore di hello di output.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="4a9c8-170">toocreate un flusso di dati attraverso l'esperimento, si accede di una porta di output della porta di input tooan un modulo di un altro.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="4a9c8-171">In qualsiasi momento, è possibile scegliere quali dati hello sono simile a questo punto nel flusso di dati hello porta di output di hello del toosee set di dati o un modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="4a9c8-172">In questo set di dati di esempio, ogni istanza di un'automobile viene visualizzato come una riga e le variabili di hello associate a ogni automobile vengono visualizzati come colonne.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="4a9c8-173">Dato variabili hello di un'automobile specifica, verrà tootry toopredict hello prezzo colonna estrema destra "(price colonna 26, intitolata").</span><span class="sxs-lookup"><span data-stu-id="4a9c8-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="4a9c8-174">![Visualizzare i dati di un'automobile hello nella finestra di visualizzazione dati hello][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="4a9c8-175">
***Visualizzare i dati di un'automobile hello nella finestra di visualizzazione dati hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="4a9c8-176">Finestra di visualizzazione hello Chiudi facendo hello "**x**" nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="4a9c8-177">Passaggio 2: Preparare i dati di hello</span><span class="sxs-lookup"><span data-stu-id="4a9c8-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="4a9c8-178">Prima di poter analizzare un set di dati è in genere necessario pre-elaborarlo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="4a9c8-179">Ad esempio, è possibile aver notato hello i valori presenti nelle colonne di hello delle varie righe mancanti.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="4a9c8-180">Questi valori mancanti necessario toobe puliti quindi modello hello è possibile analizzare dati hello correttamente.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="4a9c8-181">In questo caso verranno rimosse le righe con i valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="4a9c8-182">Inoltre, hello **perdite normalizzato** colonna ha una proporzione elevata di valori mancanti, che dunque verrà escluso tale colonna dal modello hello completamente.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="4a9c8-183">Pulizia hello mancano i valori dei dati di input è un prerequisito per utilizzando la maggior parte dei moduli di hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="4a9c8-184">Si aggiunge un modulo che rimuove hello **perdite normalizzato** colonna completamente, quindi è aggiungere un altro modulo che rimuove tutte le righe che mancano alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="4a9c8-185">Tipo **selezionare colonne** nella casella di ricerca hello nella parte superiore di hello di hello toofind tavolozza di hello modulo [selezionare le colonne nel set di dati] [ select-columns] modulo, quindi trascinarlo toohello esperimento canvas .</span><span class="sxs-lookup"><span data-stu-id="4a9c8-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="4a9c8-186">Questo modulo consente tooselect quali colonne di dati si desidera tooinclude o escludere hello modello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="4a9c8-187">Connettere hello porta di output di hello **dati prezzo Automobile (Raw)** toohello set di dati di input porta hello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="4a9c8-188">![Aggiungere l'area di disegno hello "Selezionare le colonne nel set di dati" modulo toohello sperimentazione e connetterla][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="4a9c8-189">***Aggiungere l'area di disegno hello "Selezionare le colonne nel set di dati" modulo toohello sperimentazione e connetterla***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="4a9c8-190">Fare clic su hello [selezionare le colonne nel set di dati] [ select-columns] modulo e fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="4a9c8-191">A sinistra di hello, fare clic su **con regole**</span><span class="sxs-lookup"><span data-stu-id="4a9c8-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="4a9c8-192">In **Begin With** (Inizia con), fare clic su **All columns** (Tutte le colonne).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="4a9c8-193">In questo modo [selezionare le colonne nel set di dati] [ select-columns] toopass tramite tutte le colonne di hello (tranne le colonne siamo su tooexclude).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="4a9c8-194">Hello elenchi a discesa, selezionare **escludere** e **i nomi delle colonne**e quindi fare clic nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="4a9c8-195">Verrà visualizzato un elenco di colonne.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-195">A list of columns is displayed.</span></span> <span data-ttu-id="4a9c8-196">Selezionare **perdite normalizzato**, e è aggiunto toohello casella di testo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="4a9c8-197">Fare clic sul selettore di colonna hello per la tooclose pulsante hello segno di spunta (OK) (in basso a destra hello).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="4a9c8-198">![Avvia selettore di colonna hello ed escludere la colonna "perdite normalizzato" hello][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="4a9c8-199">***Avvia selettore di colonna hello ed escludere la colonna "perdite normalizzato" hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="4a9c8-200">Riquadro delle proprietà ora hello per **selezionare le colonne nel set di dati** indica il passaggio attraverso tutte le colonne dal set di dati di hello tranne **perdite normalizzato**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="4a9c8-201">![riquadro Proprietà Hello mostra che colonna hello "perdite normalizzato" viene escluso][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="4a9c8-202">***riquadro Proprietà Hello mostra che colonna hello "perdite normalizzato" viene escluso***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="4a9c8-203">È possibile aggiungere un modulo tooa commento facendo doppio clic su modulo hello e immissione di testo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="4a9c8-204">Ciò consente di visualizzare a colpo d'occhio esegue il modulo hello nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="4a9c8-205">In questo caso fare doppio clic su hello [selezionare le colonne nel set di dati] [ select-columns] modulo e il tipo hello commento "Exclude normalizzato perdite".</span><span class="sxs-lookup"><span data-stu-id="4a9c8-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="4a9c8-206">![Fare doppio clic su un tooadd modulo un commento][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="4a9c8-207">***Fare doppio clic su un tooadd modulo un commento***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="4a9c8-208">Hello trascinare [Clean Missing Data] [ clean-missing-data] toohello modulo provare l'area di disegno e connetterla toohello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="4a9c8-209">In hello **proprietà** riquadro, selezionare **Rimuovi intera riga** in **modalità di pulizia**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="4a9c8-210">In questo modo [Clean Missing Data] [ clean-missing-data] dati hello tooclean rimuovendo le righe che contengono i valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="4a9c8-211">Fare doppio clic sul modulo hello e digitare il commento hello "Rimuovi righe valore mancante".</span><span class="sxs-lookup"><span data-stu-id="4a9c8-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="4a9c8-212">![Impostare la modalità di pulizia hello troppo "Rimuovi intera riga" per il modulo "Clean Missing Data" hello][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="4a9c8-213">***Impostare la modalità di pulizia hello troppo "Rimuovi intera riga" per il modulo "Clean Missing Data" hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="4a9c8-214">Eseguire l'esperimento hello facendo **eseguire** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="4a9c8-215">Al termine dell'esecuzione esperimento hello, tutti i moduli di hello hanno tooindicate un segno di spunta verde che è state completata.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="4a9c8-216">Si noti inoltre hello **al termine dell'esecuzione** stato nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="4a9c8-217">![Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="4a9c8-218">
***Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="4a9c8-219">Motivo per cui è stata eseguiamo esperimento hello ora?</span><span class="sxs-lookup"><span data-stu-id="4a9c8-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="4a9c8-220">Per esperimento hello in esecuzione, le definizioni di colonna hello per i dati passano dal set di dati hello tramite hello [selezionare le colonne nel set di dati] [ select-columns] modulo e tramite hello [Clean Missing Data] [ clean-missing-data] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="4a9c8-221">Ciò significa che tutti i moduli la connessione è troppo[Clean Missing Data] [ clean-missing-data] anche avrà le stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="4a9c8-222">Svolto nella sperimentazione hello punto toothis è dati hello pulita.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="4a9c8-223">Se si desidera tooview hello pulito set di dati, fare clic su hello lasciato la porta di output di hello [Clean Missing Data] [ clean-missing-data] modulo e selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="4a9c8-224">Si noti che hello **perdite normalizzato** colonna non viene più fornita e non sono presenti valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="4a9c8-225">Ora che i dati di hello sono puliti, si è pronti toospecify quali funzionalità è archivieranno toouse nel modello predittivo hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="4a9c8-226">Passaggio 3: Definire le caratteristiche</span><span class="sxs-lookup"><span data-stu-id="4a9c8-226">Step 3: Define features</span></span>

<span data-ttu-id="4a9c8-227">In Machine Learning le *caratteristiche* sono singole proprietà misurabili di un elemento a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="4a9c8-228">Nel set di dati corrente ogni riga rappresenta un'automobile e ogni colonna è una caratteristica di tale automobile.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="4a9c8-229">Ricerca di un set ottimo di funzionalità per la creazione di un modello predittivo richiede informazioni sui problemi di hello e sperimentazione desiderate toosolve.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="4a9c8-230">Alcune funzionalità sono migliori per la stima destinazione hello rispetto ad altri.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="4a9c8-231">Alcune caratteristiche sono strettamente correlate ad altre e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="4a9c8-232">Ad esempio, città mpg e autostrada mpg sono strettamente correlati in modo da poter mantenere uno e rimuovere altri hello senza stima hello in maniera significativa.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="4a9c8-233">Creare ora un modello che utilizza un sottoinsieme di funzionalità hello nel set di dati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="4a9c8-234">È possibile tornare più avanti e selezionare diverse funzionalità, eseguire nuovamente l'esperimento hello e vedere se si ottengono risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="4a9c8-235">Toostart, ma si proverà hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="4a9c8-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="4a9c8-236">Trascinare un'altra [selezionare le colonne nel set di dati] [ select-columns] toohello modulo provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="4a9c8-237">Connettersi a sinistra sulla porta di output di hello hello [Clean Missing Data] [ clean-missing-data] input toohello modulo di hello [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="4a9c8-238">![Connettersi hello "Selezionare le colonne nel set di dati" toohello "Clean Missing Data" modulo][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="4a9c8-239">***Connettersi hello "Selezionare le colonne nel set di dati" toohello "Clean Missing Data" modulo***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="4a9c8-240">Fare doppio clic sul modulo hello e digitare "Selezionare le funzionalità per la stima."</span><span class="sxs-lookup"><span data-stu-id="4a9c8-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="4a9c8-241">Fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="4a9c8-242">Fare clic su **With rules**(Con regole).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-242">Click **With rules**.</span></span>

4. <span data-ttu-id="4a9c8-243">In **Begin With** (Inizia con), fare clic su **No columns** (Nessuna colonna).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="4a9c8-244">Nella riga di filtro hello, selezionare **Include** e **i nomi delle colonne** e selezionare l'elenco di nomi di colonna nella casella di testo hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="4a9c8-245">In questo modo hello modulo toonot iterazione (funzionalità) tutte le colonne tranne quelle che si specificano hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="4a9c8-246">Fare clic su hello segno di spunta (OK).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="4a9c8-247">![Selezionare tooinclude colonne (funzionalità) hello nella stima hello][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="4a9c8-248">***Selezionare tooinclude colonne (funzionalità) hello nella stima hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="4a9c8-249">Ciò produce un set di dati filtrato contenente solo le funzioni hello che desideriamo toohello toopass verrà usato nel passaggio successivo hello algoritmo di apprendimento.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="4a9c8-250">In seguito, è possibile tornare indietro e provare a selezionare caratteristiche diverse.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="4a9c8-251">Passaggio 4: Scegliere e applicare un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="4a9c8-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="4a9c8-252">Ora che i dati di hello sono pronti, la costruzione di un modello predittivo costituito training e test.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="4a9c8-253">Verrà usato il modello di dati tootrain hello e quindi verrà eseguito un test hello modello toosee la misura è in grado di toopredict prezzi.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="4a9c8-254">*Classificazione* e *regressione* sono due tipi di algoritmi di Machine Learning sottoposti a supervisione.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="4a9c8-255">La classificazione stima una risposta da un set di categorie definito, ad esempio un colore (rosso, blu o verde).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="4a9c8-256">La regressione è toopredict usato un numero.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="4a9c8-257">Dal momento che il prezzo toopredict, che è un numero, verrà utilizzato un algoritmo di regressione.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="4a9c8-258">Per questo esempio, verrà usato un modello *a regressione lineare* semplice.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="4a9c8-259">Se si desidera toolearn informazioni sui diversi tipi di algoritmi di machine learning e quando toouse loro, si potrebbe visualizzare video prima hello in hello analisi scientifica dei dati per serie di utenti meno esperti, [hello cinque domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="4a9c8-260">È anche possibile consultare hello infografica [computer nozioni di base con esempi di algoritmi di apprendimento](machine-learning-basics-infographic-with-algorithm-examples.md), o estrarlo hello [Machine learning foglio informativo algoritmo](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="4a9c8-261">Abbiamo Training modello di hello mediante l'assegnazione di un set di dati che include il prezzo di hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="4a9c8-262">modello Hello analizza dati hello e cercare le correlazioni tra le funzionalità di un'automobile e il prezzo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="4a9c8-263">Quindi verrà eseguito un test del modello di hello - verrà assegnargli un set di funzionalità per automobili che si ha familiarità con e vedere come chiudere hello prevede prezzo di toopredicting hello noti.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="4a9c8-264">Si userà i dati per il training del modello di hello e testarlo suddividendo dati hello in training e il testing di set di dati separato.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="4a9c8-265">Selezionare e trascinare hello [dati divisi] [ split] toohello modulo provare l'area di disegno e connetterla toohello ultima [selezionare le colonne nel set di dati] [ select-columns] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="4a9c8-266">Fare clic su hello [dati divisi] [ split] tooselect modulo è.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="4a9c8-267">Trovare hello **frazione di righe in hello set di dati di output prima** (in hello **proprietà** toohello riquadro a destra dell'area di disegno hello) e impostarlo too0.75.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="4a9c8-268">In questo modo, verrà usata al 75% hello tootrain hello di modello di data e contenere il 25% per il testing (in un secondo momento, è possibile sperimentare con diverse percentuali).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="4a9c8-269">![Set hello dividere frazione di hello "Suddivisione dei dati" modulo too0.75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="4a9c8-270">***Set hello dividere frazione di hello "Suddivisione dei dati" modulo too0.75***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="4a9c8-271">Modificando hello **Random seed** parametro, è possibile produrre diversi campioni casuale per il training e testing.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="4a9c8-272">Questo parametro controlla il seeding del generatore di numeri pseudo-casuali hello hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="4a9c8-273">Eseguire l'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-273">Run hello experiment.</span></span> <span data-ttu-id="4a9c8-274">Quando viene eseguito l'esperimento hello, hello [selezionare le colonne nel set di dati] [ select-columns] e [dati divisi] [ split] moduli passare toohello le definizioni di colonna moduli che verranno aggiunte successivamente.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="4a9c8-275">hello tooselect, algoritmo di apprendimento espandere hello **Machine Learning** categoria hello modulo tavolozza toohello a sinistra di hello area di disegno e quindi espandere **inizializzare modello**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="4a9c8-276">Consente di visualizzare diverse categorie di moduli che possono essere algoritmi utilizzati tooinitialize machine learning.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="4a9c8-277">Per questo esercizio, selezionare hello [Linear Regression] [ linear-regression] modulo in hello **regressione** categoria e trascinarlo toohello esperimento canvas.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="4a9c8-278">(È possibile anche trovare hello modulo digitando "linear regression" nella casella di ricerca tavolozza hello.)</span><span class="sxs-lookup"><span data-stu-id="4a9c8-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="4a9c8-279">Individuare e trascinare hello [Train Model] [ train-model] toohello modulo provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="4a9c8-280">Connettere l'output di hello di hello [Linear Regression] [ linear-regression] toohello modulo lasciato input di hello [Train Model] [ train-model] modulo e connettersi hello la formazione di output dei dati (porta a sinistra) di hello [dati divisi] [ split] input di destra toohello modulo di hello [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="4a9c8-281">![Connettersi hello "Train Model" modulo tooboth hello "Linear Regression" e "Suddivisione dei dati" moduli][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="4a9c8-282">***Connettersi hello "Train Model" modulo tooboth hello "Linear Regression" e "Suddivisione dei dati" moduli***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="4a9c8-283">Fare clic su hello [Train Model] [ train-model] modulo, fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro e quindi seleziona hello **prezzo** colonna.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="4a9c8-284">Questo è il valore di hello che il modello è toopredict continua.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="4a9c8-285">Si seleziona hello **prezzo** colonna nel selettore di colonna hello spostandola hello **colonne disponibili** elenco toohello **colonne selezionate** elenco.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="4a9c8-286">![Selezionare una colonna prezzo hello per il modulo "Train Model" hello][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="4a9c8-287">***Selezionare una colonna prezzo hello per il modulo "Train Model" hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="4a9c8-288">Eseguire l'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-288">Run hello experiment.</span></span>

<span data-ttu-id="4a9c8-289">È ora disponibile un modello di regressione con training che può essere utilizzato tooscore nuove automobili dati toomake prezzo stime.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="4a9c8-290">![Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="4a9c8-291">
***Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="4a9c8-292">Passaggio 5: Stimare i prezzi delle nuove automobili</span><span class="sxs-lookup"><span data-stu-id="4a9c8-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="4a9c8-293">Ora che è stata Training modello di hello utilizzando pari al 75% dei dati, è possibile usarlo tooscore hello altri 25 percento hello dati toosee prestazioni nostri funzioni del modello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="4a9c8-294">Individuare e trascinare hello [Score Model] [ score-model] toohello modulo provare l'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="4a9c8-295">Connettere l'output di hello di hello [Train Model] [ train-model] toohello modulo porta di input di sinistra [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="4a9c8-296">Connettersi hello test output dei dati (porta a destra) di hello [dati divisi] [ split] porta di input destra toohello modulo [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="4a9c8-297">![Connettersi hello "Score Model" modulo tooboth hello "Train Model" e "Suddivisione dei dati" moduli][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="4a9c8-298">***Connettersi hello "Score Model" modulo tooboth hello "Train Model" e "Suddivisione dei dati" moduli***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="4a9c8-299">Eseguire l'esperimento hello e visualizzare l'output di hello di hello [Score Model] [ score-model] modulo (fare clic sulla porta di output di hello del [Score Model] [ score-model] e selezionare **Visualizzare**).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="4a9c8-300">Mostra output di Hello hello valori stimati per prezzo e hello valori noti hello dei dati dei test.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="4a9c8-301">![Output di hello "Score Model" modulo][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="4a9c8-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="4a9c8-302">***Output di hello "Score Model" modulo***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="4a9c8-303">Infine, verranno testate qualità hello dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="4a9c8-304">Selezionare e trascinare hello [Evaluate Model] [ evaluate-model] toohello modulo provare l'area di disegno e connettere l'output di hello di hello [Score Model] [ score-model] modulo toohello input di sinistra [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="4a9c8-305">Non sono presenti due porte di input in hello [Evaluate Model] [ evaluate-model] modulo poiché può essere utilizzato toocompare due modelli side-by.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="4a9c8-306">In un secondo momento, è possibile aggiungere un altro esperimento toohello di algoritmo e usare [Evaluate Model] [ evaluate-model] toosee quello che offre risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="4a9c8-307">Eseguire l'esperimento hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-307">Run hello experiment.</span></span>

<span data-ttu-id="4a9c8-308">output di hello tooview da hello [Evaluate Model] [ evaluate-model] modulo, fare clic sulla porta di output di hello e quindi selezionare **Visualizza**.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="4a9c8-309">![Risultati della valutazione per esperimento hello][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="4a9c8-310">
***Risultati della valutazione per esperimento hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="4a9c8-311">Hello seguendo le statistiche viene visualizzato per il nostro modello:</span><span class="sxs-lookup"><span data-stu-id="4a9c8-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="4a9c8-312">**Errore assoluto medio** (MAE): hello media degli errori assoluti (un *errore* hello differenze hello previsto valore e il valore effettivo hello).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="4a9c8-313">**Errore quadratico medio radice** (RMSE): hello di radice quadrata della media hello di errori al quadrato di stime effettuate nel set di dati di hello test.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="4a9c8-314">**Errore assoluto relativo**: hello Media errori assoluto relativo toohello assoluto basso tra i valori effettivi e Media hello di tutti i valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="4a9c8-315">**Errore quadratico relativo**: Media hello di errori al quadrato relativo toohello al quadrato differenza tra i valori effettivi hello e Media hello di tutti i valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="4a9c8-316">**Coefficiente di determinazione**: anche noto come hello **R al quadrato valore**, si tratta di una metrica statistica che indica l'idoneità un modello di rapporto dati hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="4a9c8-317">Per ogni errore hello statistiche, più piccolo sono consigliabile.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="4a9c8-318">Un valore inferiore indica che le stime hello corrispondano maggiormente i valori effettivi hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="4a9c8-319">Per **coefficiente di determinazione**, hello più vicino il relativo valore è tooone (1.0), stime hello migliori hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="4a9c8-320">Esperimento finale</span><span class="sxs-lookup"><span data-stu-id="4a9c8-320">Final experiment</span></span>

<span data-ttu-id="4a9c8-321">sperimentazione finale Hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="4a9c8-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="4a9c8-322">![sperimentazione finale Hello][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="4a9c8-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="4a9c8-323">
***sperimentazione finale Hello***</span><span class="sxs-lookup"><span data-stu-id="4a9c8-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a9c8-324">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4a9c8-324">Next steps</span></span>

<span data-ttu-id="4a9c8-325">Ora che si aver completato l'esercitazione di hello prima machine learning e imposta esperimento, è possibile continuare il modello di hello tooimprove e quindi distribuirla come servizio web predittivo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="4a9c8-326">**Eseguire l'iterazione del modello di hello tooimprove tootry** -ad esempio, è possibile modificare le funzionalità di hello è utilizzare la stima.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="4a9c8-327">Oppure è possibile modificare le proprietà di hello di hello [Linear Regression] [ linear-regression] algoritmo o tenta di tutto un algoritmo diverso.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="4a9c8-328">È anche possibile aggiungere più esperimento di machine learning algoritmi tooyour in una sola volta e confrontare i due di essi utilizzando hello [Evaluate Model] [ evaluate-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="4a9c8-329">Per un esempio di come toocompare più modelli in un esperimento singolo, vedere [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="4a9c8-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="4a9c8-330">toocopy qualsiasi iterazione dell'esperimento, utilizzare hello **SAVE AS** pulsante nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="4a9c8-331">È possibile visualizzare tutte le iterazioni di hello dell'esperimento facendo **Visualizza cronologia di esecuzione** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="4a9c8-332">Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="4a9c8-333">**Distribuire il modello di hello come un servizio web predittivo** : quando si è soddisfatti del modello, è possibile distribuire un toobe di servizio web utilizzato prezzi delle automobili toopredict utilizzando nuovi dati.</span><span class="sxs-lookup"><span data-stu-id="4a9c8-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="4a9c8-334">Per altre informazioni dettagliate, vedere [Distribuire un servizio Web di Azure Machine Learning][publish].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="4a9c8-335">Desidera toolearn altre?</span><span class="sxs-lookup"><span data-stu-id="4a9c8-335">Want toolearn more?</span></span> <span data-ttu-id="4a9c8-336">Per una procedura dettagliata più ampia e dettagliata del processo di hello di creazione, training, valutazione e distribuzione di un modello, vedere [sviluppare una soluzione predittiva mediante Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="4a9c8-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
