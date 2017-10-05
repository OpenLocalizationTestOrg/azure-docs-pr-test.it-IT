---
title: Esperimento semplice in Machine Learning Studio | Documentazione di Microsoft
description: "Questa esercitazione di Machine Learning illustra un esperimento semplice di analisi scientifica dei dati. Verrà stimato il prezzo di un'automobile usando un algoritmo di regressione."
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
ms.openlocfilehash: 0539e9d04c61d35de56a29d350c07654c095c576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="b546e-105">Esercitazione di Machine Learning: Creare il primo esperimento di analisi scientifica dei dati in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b546e-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="b546e-106">Questa esercitazione è destinata agli utenti che non hanno mai usato **Azure Machine Learning Studio**.</span><span class="sxs-lookup"><span data-stu-id="b546e-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="b546e-107">In questa esercitazione verrà illustrato come usare per la prima volta Studio per creare un esperimento di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b546e-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="b546e-108">L'esperimento testerà un modello analitico che stima il prezzo di un'automobile in base a diverse variabili, ad esempio la marca e le specifiche tecniche.</span><span class="sxs-lookup"><span data-stu-id="b546e-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="b546e-109">Questa esercitazione offre le nozioni di base su come trascinare moduli nell'esperimento, connetterli, eseguire l'esperimento ed esaminare i risultati.</span><span class="sxs-lookup"><span data-stu-id="b546e-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="b546e-110">Non verrà invece illustrato l'argomento generale di Machine Learning o come selezionare e usare i numerosi algoritmi predefiniti (più di 100) e i moduli di gestione dei dati inclusi in Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="b546e-111">Se non si ha familiarità con Machine Learning, è consigliabile vedere la serie di video [Analisi scientifica dei dati per principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="b546e-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="b546e-112">Questa serie di video rappresenta un'introduzione completa a Machine Learning e usa linguaggio e concetti semplici.</span><span class="sxs-lookup"><span data-stu-id="b546e-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="b546e-113">Se si ha familiarità con Machine Learning, ma si vuole approfondire la conoscenza su Machine Learning Studio e sugli algoritmi inclusi, vedere:</span><span class="sxs-lookup"><span data-stu-id="b546e-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="b546e-114">Cos'è Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="b546e-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="b546e-115">: questa è una panoramica generale di Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="b546e-116">[Nozioni fondamentali di Machine Learning con esempi di algoritmi](machine-learning-basics-infographic-with-algorithm-examples.md): questa infografica è molto utile se si vuole acquisire una maggiore conoscenza sui diversi tipi di algoritmi di Machine Learning inclusi in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="b546e-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) (Guida di Machine Learning): questa guida offre informazioni simili all'infografica, ma in formato interattivo.</span><span class="sxs-lookup"><span data-stu-id="b546e-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="b546e-118">[Foglio informativo sugli algoritmi di Machine Learning](machine-learning-algorithm-cheat-sheet.md) e [Come scegliere gli algoritmi di Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md): questo poster scaricabile e l'articolo relativo illustrano in modo più approfondito gli algoritmi di Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="b546e-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) (Machine Learning Studio: Guida agli algoritmi e ai moduli): questa è una guida di riferimento completa sui moduli di Studio e include gli algoritmi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b546e-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="b546e-120">Vantaggi di Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b546e-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="b546e-121">Machine Learning Studio semplifica la configurazione di un esperimento grazie a moduli a trascinamento preprogrammati con tecniche di modellazione predittiva.</span><span class="sxs-lookup"><span data-stu-id="b546e-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="b546e-122">L'uso di un'area di lavoro interattiva grafica consente di selezionare e trascinare ***set di dati*** e ***moduli*** di analisi in un'area di disegno interattiva.</span><span class="sxs-lookup"><span data-stu-id="b546e-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="b546e-123">Questi vengono successivamente connessi per creare un ***esperimento*** da eseguire in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="b546e-124">È possibile ***creare un modello***, ***eseguire il training del modello***, ***assegnare un punteggio e testare il modello***.</span><span class="sxs-lookup"><span data-stu-id="b546e-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="b546e-125">È possibile anche scorrere la struttura del modello, modificare l'esperimento ed eseguirlo di nuovo fino a quando non restituisce i risultati appropriati.</span><span class="sxs-lookup"><span data-stu-id="b546e-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="b546e-126">Quando il modello è pronto, è possibile pubblicarlo come ***servizio Web*** in modo che altri utenti possano inviare nuovi dati e ottenere stime in cambio.</span><span class="sxs-lookup"><span data-stu-id="b546e-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="b546e-127">Aprire Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b546e-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="b546e-128">Per avviare Studio, andare a [https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="b546e-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="b546e-129">Se è già stato effettuato l'accesso a Machine Learning Studio in precedenza, fare clic su **Sign In** (Accedi).</span><span class="sxs-lookup"><span data-stu-id="b546e-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="b546e-130">In caso contrario fare clic su **Sign up here** (Effettuare l'iscrizione qui) e scegliere un'opzione gratuita o a pagamento.</span><span class="sxs-lookup"><span data-stu-id="b546e-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="b546e-131">![Accedere a Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="b546e-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="b546e-132">
***Accedere a Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="b546e-132">
***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="b546e-133">Cinque passaggi per la creazione di un esperimento</span><span class="sxs-lookup"><span data-stu-id="b546e-133">Five steps to create an experiment</span></span>

<span data-ttu-id="b546e-134">In questa esercitazione di Machine Learning, si seguiranno cinque passaggi di base per compilare un esperimento in Machine Learning Studio per creare un modello, eseguire il training e assegnare un punteggio:</span><span class="sxs-lookup"><span data-stu-id="b546e-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="b546e-135">**Creare un modello**</span><span class="sxs-lookup"><span data-stu-id="b546e-135">**Create a model**</span></span>
    - <span data-ttu-id="b546e-136">[Passaggio 1: Ottenere i dati]</span><span class="sxs-lookup"><span data-stu-id="b546e-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="b546e-137">[Passaggio 2: Preparare i dati]</span><span class="sxs-lookup"><span data-stu-id="b546e-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="b546e-138">[Passaggio 3: Definire le caratteristiche]</span><span class="sxs-lookup"><span data-stu-id="b546e-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="b546e-139">**Eseguire il training del modello**</span><span class="sxs-lookup"><span data-stu-id="b546e-139">**Train the model**</span></span>
    - <span data-ttu-id="b546e-140">[Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]</span><span class="sxs-lookup"><span data-stu-id="b546e-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="b546e-141">**Assegnare un punteggio e testare il modello**</span><span class="sxs-lookup"><span data-stu-id="b546e-141">**Score and test the model**</span></span>
    - <span data-ttu-id="b546e-142">[Passaggio 5: Stimare i prezzi delle nuove automobili]</span><span class="sxs-lookup"><span data-stu-id="b546e-142">[Step 5: Predict new automobile prices]</span></span>

<span data-ttu-id="b546e-143">[Passaggio 1: Ottenere i dati]: #step-1-get-data</span><span class="sxs-lookup"><span data-stu-id="b546e-143">[Step 1: Get data]: #step-1-get-data</span></span>
<span data-ttu-id="b546e-144">[Passaggio 2: Preparare i dati]: #step-2-prepare-the-data</span><span class="sxs-lookup"><span data-stu-id="b546e-144">[Step 2: Prepare the data]: #step-2-prepare-the-data</span></span>
<span data-ttu-id="b546e-145">[Passaggio 3: Definire le caratteristiche]: #step-3-define-features</span><span class="sxs-lookup"><span data-stu-id="b546e-145">[Step 3: Define features]: #step-3-define-features</span></span>
<span data-ttu-id="b546e-146">[Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]: #step-4-choose-and-apply-a-learning-algorithm</span><span class="sxs-lookup"><span data-stu-id="b546e-146">[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm</span></span>
<span data-ttu-id="b546e-147">[Passaggio 5: Stimare i prezzi delle nuove automobili]: #step-5-predict-new-automobile-prices</span><span class="sxs-lookup"><span data-stu-id="b546e-147">[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices</span></span>

> [!TIP] 
> <span data-ttu-id="b546e-148">Per una copia di lavoro dell'esperimento seguente, visitare il sito Web [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="b546e-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="b546e-149">Passare a **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** (Primo esperimento scientifico sui dati - stima dei prezzi delle automobili) e fare clic su **Open in Studio** (Apri in Studio) per scaricare una copia dell'esperimento nell'area di lavoro di Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="b546e-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="b546e-150">Passaggio 1: Ottenere i dati</span><span class="sxs-lookup"><span data-stu-id="b546e-150">Step 1: Get data</span></span>

<span data-ttu-id="b546e-151">La prima operazione per eseguire un esperimento in Machine Learning è ottenere i dati.</span><span class="sxs-lookup"><span data-stu-id="b546e-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="b546e-152">In Machine Learning Studio sono disponibili numerosi set di dati di esempio da usare oppure è possibile importare dati da molte altre origini.</span><span class="sxs-lookup"><span data-stu-id="b546e-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="b546e-153">Per questo esempio, verrà usato il set di dati di esempio **Automobile price data (Raw)** (Dati non elaborati sui prezzi delle automobili) incluso nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b546e-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="b546e-154">Questo set di dati include voci per diverse automobili e include informazioni su marca, modello, specifiche tecniche e prezzo.</span><span class="sxs-lookup"><span data-stu-id="b546e-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="b546e-155">Di seguito viene illustrato come ottenere il set di dati nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="b546e-156">Creare un nuovo esperimento facendo clic su **+NEW** (NUOVO) nella parte inferiore della finestra di Machine Learning Studio, selezionare **EXPERIMENT** (ESPERIMENTO) e scegliere **Blank Experiment** (Esperimento vuoto).</span><span class="sxs-lookup"><span data-stu-id="b546e-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="b546e-157">All'esperimento viene assegnato un nome predefinito visualizzato nella parte superiore dell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="b546e-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="b546e-158">Selezionare il testo e rinominarlo in modo significativo, ad esempio **Stima prezzi automobili**.</span><span class="sxs-lookup"><span data-stu-id="b546e-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="b546e-159">Il nome non deve essere univoco.</span><span class="sxs-lookup"><span data-stu-id="b546e-159">The name doesn't need to be unique.</span></span>

    ![Rinominare l'esperimento][rename-experiment]

2. <span data-ttu-id="b546e-161">A sinistra dell'area di disegno dell'esperimento è presente una tavolozza di set di dati e moduli.</span><span class="sxs-lookup"><span data-stu-id="b546e-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="b546e-162">Digitare **automobile** nella casella di ricerca nella parte superiore della tavolozza per trovare il set di dati denominato **Automobile price data (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="b546e-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="b546e-163">Trascinare il set di dati nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="b546e-164">![Individuare il set di dati delle automobili e trascinarlo nell'area di disegno dell'esperimento][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="b546e-165">***Individuare il set di dati di automobili e trascinarlo nell'area di disegno esperimento***</span><span class="sxs-lookup"><span data-stu-id="b546e-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="b546e-166">Per visualizzare l'aspetto dei dati, fare clic sulla porta di output nella parte inferiore del set di dati relativo alle automobili e selezionare **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="b546e-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="b546e-167">![Fare clic sulla porta di output e selezionare "Visualize"][select-visualize]
 (Visualizza)</span><span class="sxs-lookup"><span data-stu-id="b546e-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="b546e-168">
***Fare clic sulla porta di output e selezionare "Visualize"*** (Visualizza)</span><span class="sxs-lookup"><span data-stu-id="b546e-168">
***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="b546e-169">I set di dati e i moduli hanno porte di input e output rappresentate da piccoli cerchi: le porte di input nella parte superiore e le porte di output nella parte inferiore.</span><span class="sxs-lookup"><span data-stu-id="b546e-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="b546e-170">Per creare un flusso di dati nell'esperimento, connettere una porta di output di un modulo a una porta di input di un altro.</span><span class="sxs-lookup"><span data-stu-id="b546e-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="b546e-171">In qualsiasi momento, è possibile fare clic sulla porta di output di un set di dati o di un modulo per visualizzare l'aspetto dei dati in tale punto specifico del flusso di dati.</span><span class="sxs-lookup"><span data-stu-id="b546e-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="b546e-172">In questo set di dati di esempio, ogni istanza di un'automobile viene rappresentata da una riga e le variabili associate a ogni automobile vengono rappresentate da colonne.</span><span class="sxs-lookup"><span data-stu-id="b546e-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="b546e-173">In base alle variabili per un'automobile specifica, si proverà a stimare il prezzo nella colonna che si trova all'estrema destra, ovvero la colonna 26 denominata "price" (prezzo).</span><span class="sxs-lookup"><span data-stu-id="b546e-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="b546e-174">![Visualizzare i dati delle automobili nella finestra di visualizzazione dei dati][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="b546e-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="b546e-175">
***Visualizzare i dati delle automobili nella finestra di visualizzazione dei dati***</span><span class="sxs-lookup"><span data-stu-id="b546e-175">
***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="b546e-176">Chiudere la finestra di visualizzazione facendo clic sulla "**x**" nell'angolo superiore destro.</span><span class="sxs-lookup"><span data-stu-id="b546e-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="b546e-177">Passaggio 2: Preparare i dati</span><span class="sxs-lookup"><span data-stu-id="b546e-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="b546e-178">Prima di poter analizzare un set di dati è in genere necessario pre-elaborarlo.</span><span class="sxs-lookup"><span data-stu-id="b546e-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="b546e-179">Ad esempio, si potrebbe notare l'assenza di valori nelle colonne di diverse righe.</span><span class="sxs-lookup"><span data-stu-id="b546e-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="b546e-180">Per consentire al modello di analizzare correttamente i dati, è necessario eseguire la pulizia di questi valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="b546e-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="b546e-181">In questo caso verranno rimosse le righe con i valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="b546e-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="b546e-182">Inoltre, la colonna **normalized-losses** ha molti valori mancanti, pertanto verrà esclusa completamente dal modello.</span><span class="sxs-lookup"><span data-stu-id="b546e-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="b546e-183">La pulizia dei valori mancanti dai dati di input è un prerequisito all'uso della maggior parte dei moduli.</span><span class="sxs-lookup"><span data-stu-id="b546e-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="b546e-184">Si aggiunge prima un modulo che rimuove completamente la colonna **normalized-losses** (perdite normalizzate) e si aggiunge un altro modulo che rimuove tutte le righe con dati mancanti.</span><span class="sxs-lookup"><span data-stu-id="b546e-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="b546e-185">Digitare **select columns** (seleziona colonne) nella casella di ricerca nella parte superiore del pannello dei moduli per trovare il modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) e trascinarlo nell'area di disegno.</span><span class="sxs-lookup"><span data-stu-id="b546e-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="b546e-186">Questo modulo consente di selezionare le colonne di dati da includere o escludere nel modello.</span><span class="sxs-lookup"><span data-stu-id="b546e-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="b546e-187">Connettere la porta di output del set di dati **Automobile price data (Raw)** (Dati non elaborati sui prezzi delle automobili) alla porta di input del modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="b546e-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="b546e-188">![Aggiungere il modulo "Select Columns in Dataset" all'area di disegno dell'esperimento e connetterlo][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="b546e-189">***Aggiungere il modulo "Selezionare le colonne nel set di dati" per l'area di disegno di sperimentazione e connetterlo***</span><span class="sxs-lookup"><span data-stu-id="b546e-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="b546e-190">Fare clic su [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) e fare clic su **Launch column selector** (Avvia selettore di colonna) nel riquadro **Properties** (Proprietà).</span><span class="sxs-lookup"><span data-stu-id="b546e-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="b546e-191">A sinistra, fare clic su **With rules**</span><span class="sxs-lookup"><span data-stu-id="b546e-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="b546e-192">In **Begin With** (Inizia con), fare clic su **All columns** (Tutte le colonne).</span><span class="sxs-lookup"><span data-stu-id="b546e-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="b546e-193">In questo modo, [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) analizzerà tutte le colonne, ad eccezione di quelle che verranno escluse.</span><span class="sxs-lookup"><span data-stu-id="b546e-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="b546e-194">Negli elenchi a discesa selezionare **Escludi** e **nomi colonna**, quindi fare clic all'interno della casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b546e-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="b546e-195">Verrà visualizzato un elenco di colonne.</span><span class="sxs-lookup"><span data-stu-id="b546e-195">A list of columns is displayed.</span></span> <span data-ttu-id="b546e-196">Selezionare **normalized-losses** per aggiungere la colonna alla casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b546e-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="b546e-197">Fare clic sul pulsante del segno di spunta (OK) per chiudere il selettore di colonne (nella parte inferiore destra).</span><span class="sxs-lookup"><span data-stu-id="b546e-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="b546e-198">![Avviare il selettore di colonna ed escludere la colonna "normalized-losses"][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="b546e-199">***Avviare il selettore di colonna e di escludere la colonna "perdite normalizzato"***</span><span class="sxs-lookup"><span data-stu-id="b546e-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="b546e-200">Il riquadro delle proprietà del modulo **Select Columns in Dataset** indica ora che verranno analizzate tutte le colonne del set di dati, a eccezione di **normalized-losses**.</span><span class="sxs-lookup"><span data-stu-id="b546e-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="b546e-201">![Il riquadro delle proprietà visualizza che la colonna "normalized-losses" è stata esclusa][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="b546e-202">***Il riquadro Proprietà mostra che la colonna "perdite normalizzato" è stato escluso***</span><span class="sxs-lookup"><span data-stu-id="b546e-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="b546e-203">È possibile aggiungere un commento a un modulo facendo doppio clic sul modulo e immettendo del testo.</span><span class="sxs-lookup"><span data-stu-id="b546e-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="b546e-204">In tal modo sarà possibile individuare subito l'operazione eseguita dal modulo nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="b546e-205">In questo caso, fare doppio clic sul modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) e immettere il commento "Escludi perdite normalizzate".</span><span class="sxs-lookup"><span data-stu-id="b546e-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="b546e-206">![Fare doppio clic su un modulo per aggiungere un commento][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="b546e-207">***Fare doppio clic su un modulo per aggiungere un commento***</span><span class="sxs-lookup"><span data-stu-id="b546e-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="b546e-208">Trascinare il modulo [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti) nell'area di disegno dell'esperimento e connetterlo al modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="b546e-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="b546e-209">Nel riquadro delle **proprietà** selezionare **Remove entire row** (Rimuovi riga intera) in **modalità Cleaning** (Pulizia).</span><span class="sxs-lookup"><span data-stu-id="b546e-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="b546e-210">Questa operazione indica al modulo [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti) di pulire i dati rimuovendo le righe con valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="b546e-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="b546e-211">Fare doppio clic sul modulo e digitare il commento "Rimuovi righe valori mancanti".</span><span class="sxs-lookup"><span data-stu-id="b546e-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="b546e-212">![Impostare la modalità di pulizia a "Remove entire row" (Rimuovi riga intera) per il modulo "Clean Missing Data"][set-remove-entire-row]
     (Pulisci dati mancanti)</span><span class="sxs-lookup"><span data-stu-id="b546e-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="b546e-213">***Impostare la modalità di pulizia "Rimuovere l'intera riga" per il modulo "Clean Missing Data"***</span><span class="sxs-lookup"><span data-stu-id="b546e-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="b546e-214">Eseguire l'esperimento facendo clic su **RUN** (ESEGUI) nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="b546e-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="b546e-215">Al termine dell'esecuzione dell'esperimento, tutti i moduli saranno contraddistinti da un segno di spunta verde per indicarne il corretto completamento.</span><span class="sxs-lookup"><span data-stu-id="b546e-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="b546e-216">Si noti anche lo stato **Finished running** nell'angolo in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="b546e-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="b546e-217">![Dopo l'esecuzione, l'esperimento dovrebbe avere l'aspetto seguente][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="b546e-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="b546e-218">
***Dopo l'esecuzione, l'esperimento dovrebbe avere l'aspetto seguente***</span><span class="sxs-lookup"><span data-stu-id="b546e-218">
***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="b546e-219">Perché è stato eseguito l'esperimento ora?</span><span class="sxs-lookup"><span data-stu-id="b546e-219">Why did we run the experiment now?</span></span> <span data-ttu-id="b546e-220">Con l'esecuzione dell'esperimento, le definizioni delle colonne per i dati passano dal set di dati, attraverso i moduli [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) e [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti).</span><span class="sxs-lookup"><span data-stu-id="b546e-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="b546e-221">Ciò significa che tutti i moduli connessi a [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti) avranno anche queste stesse informazioni.</span><span class="sxs-lookup"><span data-stu-id="b546e-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="b546e-222">Fino a questo punto dell'esperimento sono stati solo puliti i dati.</span><span class="sxs-lookup"><span data-stu-id="b546e-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="b546e-223">Per visualizzare il set di dati pulito, fare clic sulla porta di output sinistra del modulo [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti) e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="b546e-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="b546e-224">Si noti che la colonna **normalized-losses** non è più inclusa e che non ci sono valori mancanti.</span><span class="sxs-lookup"><span data-stu-id="b546e-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="b546e-225">A questo punto, una volta puliti i dati è possibile specificare le caratteristiche da usare nel modello predittivo.</span><span class="sxs-lookup"><span data-stu-id="b546e-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="b546e-226">Passaggio 3: Definire le caratteristiche</span><span class="sxs-lookup"><span data-stu-id="b546e-226">Step 3: Define features</span></span>

<span data-ttu-id="b546e-227">In Machine Learning le *caratteristiche* sono singole proprietà misurabili di un elemento a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="b546e-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="b546e-228">Nel set di dati corrente ogni riga rappresenta un'automobile e ogni colonna è una caratteristica di tale automobile.</span><span class="sxs-lookup"><span data-stu-id="b546e-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="b546e-229">Per cercare un set di caratteristiche adeguato per creare un modello predittivo, è necessario sperimentare e conoscere approfonditamente il problema che si desidera risolvere.</span><span class="sxs-lookup"><span data-stu-id="b546e-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="b546e-230">Alcune caratteristiche sono infatti migliori di altre per le stime.</span><span class="sxs-lookup"><span data-stu-id="b546e-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="b546e-231">Alcune caratteristiche sono strettamente correlate ad altre e possono essere rimosse.</span><span class="sxs-lookup"><span data-stu-id="b546e-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="b546e-232">Ad esempio, city-mpg e highway-mpg sono strettamente correlate ed è possibile rimuoverne una senza influire in modo significativo sulla stima.</span><span class="sxs-lookup"><span data-stu-id="b546e-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="b546e-233">Verrà ora creato un modello che usa un sottoinsieme delle caratteristiche del set di dati.</span><span class="sxs-lookup"><span data-stu-id="b546e-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="b546e-234">È possibile tornare più tardi e selezionare caratteristiche diverse, eseguire di nuovo l'esperimento e verificare se i risultati ottenuti sono migliori.</span><span class="sxs-lookup"><span data-stu-id="b546e-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="b546e-235">Per iniziare verranno tuttavia provate le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="b546e-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="b546e-236">Trascinare un altro modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="b546e-237">Connettere la porta di output sinistra del modulo [Clean Missing Data][clean-missing-data] (Pulisci dati mancanti) alla porta di input del modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="b546e-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="b546e-238">![Connettere il modulo "Select Columns in Dataset" al modulo "Clean Missing Data"][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="b546e-239">***Collegare il modulo "Selezionare le colonne nel set di dati" per il modulo "Clean Missing Data"***</span><span class="sxs-lookup"><span data-stu-id="b546e-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="b546e-240">Fare doppio clic sul modulo e digitare "Selezionare le caratteristiche per la stima".</span><span class="sxs-lookup"><span data-stu-id="b546e-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="b546e-241">Fare clic su **Launch column selector** nel riquadro **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="b546e-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="b546e-242">Fare clic su **With rules**(Con regole).</span><span class="sxs-lookup"><span data-stu-id="b546e-242">Click **With rules**.</span></span>

4. <span data-ttu-id="b546e-243">In **Begin With** (Inizia con), fare clic su **No columns** (Nessuna colonna).</span><span class="sxs-lookup"><span data-stu-id="b546e-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="b546e-244">Nella riga del filtro, scegliere **Include** (Includi) e **i nomi delle colonne** e selezionare l'elenco dei nomi delle colonne nella casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b546e-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="b546e-245">Ciò indica al modulo di non analizzare le colonne (caratteristiche), a eccezione di quelle specificate.</span><span class="sxs-lookup"><span data-stu-id="b546e-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="b546e-246">Fare clic sul pulsante di segno di spunta (OK).</span><span class="sxs-lookup"><span data-stu-id="b546e-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="b546e-247">![Selezionare le colonne (caratteristiche) da includere nella stima][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="b546e-248">***Selezionare le colonne (funzionalità) da includere nella stima***</span><span class="sxs-lookup"><span data-stu-id="b546e-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="b546e-249">Questa operazione produce un set di dati filtrato contenente solo le caratteristiche che si vuole passare all'algoritmo di apprendimento che si userà nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="b546e-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="b546e-250">In seguito, è possibile tornare indietro e provare a selezionare caratteristiche diverse.</span><span class="sxs-lookup"><span data-stu-id="b546e-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="b546e-251">Passaggio 4: Scegliere e applicare un algoritmo di apprendimento</span><span class="sxs-lookup"><span data-stu-id="b546e-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="b546e-252">I dati sono pronti, di conseguenza la creazione del modello predittivo implica la fase di training e test.</span><span class="sxs-lookup"><span data-stu-id="b546e-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="b546e-253">Questi dati verranno usati per il training del modello e verrà testata la sua capacità di precisione per stimare i prezzi.</span><span class="sxs-lookup"><span data-stu-id="b546e-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="b546e-254">*Classificazione* e *regressione* sono due tipi di algoritmi di Machine Learning sottoposti a supervisione.</span><span class="sxs-lookup"><span data-stu-id="b546e-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="b546e-255">La classificazione stima una risposta da un set di categorie definito, ad esempio un colore (rosso, blu o verde).</span><span class="sxs-lookup"><span data-stu-id="b546e-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="b546e-256">La regressione viene usata per stimare un numero.</span><span class="sxs-lookup"><span data-stu-id="b546e-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="b546e-257">Poiché si vuole stimare il prezzo, ovvero un numero, si userà un algoritmo di regressione.</span><span class="sxs-lookup"><span data-stu-id="b546e-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="b546e-258">Per questo esempio, verrà usato un modello *a regressione lineare* semplice.</span><span class="sxs-lookup"><span data-stu-id="b546e-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="b546e-259">Per altre informazioni sui diversi tipi di algoritmi di Machine Learning e su quando usarli, è consigliabile vedere il primo video [Le cinque domande a cui risponde l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) della serie Analisi scientifica dei dati per principianti.</span><span class="sxs-lookup"><span data-stu-id="b546e-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="b546e-260">È anche possibile esaminare l'infografica [Nozioni fondamentali di Machine Learning con esempi di algoritmi](machine-learning-basics-infographic-with-algorithm-examples.md) oppure scaricare il [Foglio informativo sugli algoritmi di Machine Learning](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="b546e-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="b546e-261">Il training del modello viene eseguito tramite l'assegnazione di un set di dati che include i prezzi.</span><span class="sxs-lookup"><span data-stu-id="b546e-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="b546e-262">Il modello analizza i dati e cerca le correlazioni tra le caratteristiche di un'automobile e il prezzo.</span><span class="sxs-lookup"><span data-stu-id="b546e-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="b546e-263">Il modello viene quindi testato: viene assegnato un set di caratteristiche per le automobili di cui si ha familiarità e viene visualizzata la precisione con la quale il modello stima il prezzo noto.</span><span class="sxs-lookup"><span data-stu-id="b546e-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="b546e-264">Il training e il test del modello verranno eseguiti con dati separati in un set di dati per il training e in un set di dati per il test.</span><span class="sxs-lookup"><span data-stu-id="b546e-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="b546e-265">Selezionare e trascinare il modulo [Split Data][split] (Dividi dati) nell'area di disegno dell'esperimento e connetterlo all'output dell'ultimo modulo [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati).</span><span class="sxs-lookup"><span data-stu-id="b546e-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="b546e-266">Fare clic sul modulo [Split Data][split] (Dividi dati) per selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="b546e-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="b546e-267">Trovare l'opzione **Fraction of rows in the first output dataset** (Frazione di righe nel primo set di dati di output) nel riquadro delle **proprietà** a destra dell'area di disegno e impostarlo a 0,75.</span><span class="sxs-lookup"><span data-stu-id="b546e-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="b546e-268">In questo modo verrà usato il 75% dei dati per eseguire il training del modello e il 25% per il test. Successivamente è possibile sperimentare percentuali diverse.</span><span class="sxs-lookup"><span data-stu-id="b546e-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="b546e-269">![Impostare la frazione di divisione del modulo "Split Data" a 0,75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="b546e-270">***Impostare la frazione di divisione del modulo "Suddivisione dei dati" 0,75***</span><span class="sxs-lookup"><span data-stu-id="b546e-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="b546e-271">Modificando il parametro **Random seed** , è possibile ottenere esempi casuali diversi per training e test.</span><span class="sxs-lookup"><span data-stu-id="b546e-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="b546e-272">Questo parametro controlla il seeding del generatore di numeri pseudocasuali.</span><span class="sxs-lookup"><span data-stu-id="b546e-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="b546e-273">Eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-273">Run the experiment.</span></span> <span data-ttu-id="b546e-274">Durante l'esecuzione dell'esperimento, i moduli [Select Columns in Dataset][select-columns] (Seleziona colonne in set di dati) e [Split Data][split] (Dividi dati) passano le definizioni di colonna ai moduli che saranno aggiunti successivamente.</span><span class="sxs-lookup"><span data-stu-id="b546e-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="b546e-275">Per selezionare l'algoritmo di apprendimento, espandere la categoria **Machine Learning** nella tavolozza dei moduli a sinistra dell'area di disegno e quindi espandere **Initialize Model** (Inizializza modello).</span><span class="sxs-lookup"><span data-stu-id="b546e-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="b546e-276">Verranno visualizzate diverse categorie di moduli che possono essere usate per inizializzare gli algoritmi di Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="b546e-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="b546e-277">Per questo esperimento, selezionare il modulo [Linear Regression][linear-regression] (Regressione lineare) della categoria **Regression** (Regressione) e trascinarlo nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="b546e-278">È anche possibile trovare il modulo digitando "linear regression" nella casella di ricerca della tavolozza.</span><span class="sxs-lookup"><span data-stu-id="b546e-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="b546e-279">Trovare e trascinare il modulo [Train Model][train-model] (Training modello) nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="b546e-280">Connettere la porta di output del modulo [Linear Regression][linear-regression] (Regressione lineare) alla porta di input sinistra del modulo [Train Model][train-model] (Training modello) e connettere la porta di output sinistra dei dati per il training del modulo [Split Data][split] (Dividi dati) alla porta di input destra del modulo [Train Model][train-model] (Training modello).</span><span class="sxs-lookup"><span data-stu-id="b546e-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="b546e-281">![Connettere il modulo "Train Model" ai moduli "Linear Regression" e "Split Data"][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="b546e-282">***Connettere il modulo "Train Model" moduli "Linear Regression" sia "Suddivisione dei dati"***</span><span class="sxs-lookup"><span data-stu-id="b546e-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="b546e-283">Fare clic sul modulo [Train Model][train-model] (Training modello), fare clic su **Launch column selector** (Avvia selettore di colonna) nel riquadro **Properties** (Proprietà) e quindi selezionare la colonna **price** (prezzo).</span><span class="sxs-lookup"><span data-stu-id="b546e-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="b546e-284">Questo è il valore che si intende stimare con il modello.</span><span class="sxs-lookup"><span data-stu-id="b546e-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="b546e-285">Per selezionare la colonna **price** nel selettore delle colonne, spostarla dall'elenco **Available columns** (Colonne disponibili) all'elenco **Selected columns** (Colonne selezionate).</span><span class="sxs-lookup"><span data-stu-id="b546e-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="b546e-286">![Selezionare la colonna price per il modulo "Train Model"][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="b546e-287">***Selezionare la colonna di prezzo per il modulo "Train Model"***</span><span class="sxs-lookup"><span data-stu-id="b546e-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="b546e-288">Eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-288">Run the experiment.</span></span>

<span data-ttu-id="b546e-289">Il risultato è un modello di regressione, del quale è stato eseguito il training, che può essere usato per assegnare un punteggio ai nuovi dati delle automobili per effettuare stime sui prezzi.</span><span class="sxs-lookup"><span data-stu-id="b546e-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="b546e-290">![Dopo l'esecuzione, l'esperimento dovrebbe avere l'aspetto seguente][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="b546e-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="b546e-291">
***Dopo l'esecuzione, l'esperimento dovrebbe avere l'aspetto seguente***</span><span class="sxs-lookup"><span data-stu-id="b546e-291">
***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="b546e-292">Passaggio 5: Stimare i prezzi delle nuove automobili</span><span class="sxs-lookup"><span data-stu-id="b546e-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="b546e-293">Dopo aver eseguito il training del modello usando il 75% dei dati, è possibile usarlo per classificare il restante 25% e verificarne il funzionamento.</span><span class="sxs-lookup"><span data-stu-id="b546e-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="b546e-294">Trovare e trascinare il modulo [Score Model][score-model] (Modello di punteggio) nell'area di disegno dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="b546e-295">Connettere la porta di output del modulo [Train Model][train-model] (Training modello) alla porta di input sinistra del modulo [Score Model][score-model] (Modello di punteggio).</span><span class="sxs-lookup"><span data-stu-id="b546e-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="b546e-296">Connettere la porta di output dei dati di test (porta destra) del modulo [Split Data][split] alla porta di input destra [Score Model][score-model] (Modello di punteggio).</span><span class="sxs-lookup"><span data-stu-id="b546e-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="b546e-297">![Connettere il modulo "Score Model" ai moduli "Train Model" e "Split Data"][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="b546e-298">***Connettere il modulo "Score Model" moduli "Train Model" sia "Suddivisione dei dati"***</span><span class="sxs-lookup"><span data-stu-id="b546e-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="b546e-299">Eseguire l'esperimento e visualizzare l'output del modulo [Score Model][score-model] (Modello di punteggio), fare clic sulla porta di output di [Score Model][score-model] (Modello di punteggio) e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="b546e-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="b546e-300">L'output mostra i valori stimati per il prezzo e i valori noti dai dati di test.</span><span class="sxs-lookup"><span data-stu-id="b546e-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="b546e-301">![Output del modulo "Score Model"][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="b546e-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="b546e-302">***Output del modulo "Score Model"***</span><span class="sxs-lookup"><span data-stu-id="b546e-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="b546e-303">Alla fine viene testata la qualità dei risultati.</span><span class="sxs-lookup"><span data-stu-id="b546e-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="b546e-304">Selezionare e trascinare il modulo [Evaluate Model][evaluate-model] (Modello di valutazione) nell'area di disegno dell'esperimento e connettere la porta di output del modulo [Score Model][score-model] (Modello di punteggio) alla porta di input sinistra del modulo [Evaluate Model][evaluate-model] (Modello di valutazione).</span><span class="sxs-lookup"><span data-stu-id="b546e-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="b546e-305">Ci sono due porte di input nel modulo [Evaluate Model][evaluate-model] (Modello di punteggio) perché può essere usato per confrontare due modelli affiancati.</span><span class="sxs-lookup"><span data-stu-id="b546e-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="b546e-306">In un secondo momento, è possibile aggiungere un altro algoritmo all'esperimento e usare il modulo [Evaluate Model][evaluate-model] (Modello di punteggio) per vedere quale modello produce i risultati migliori.</span><span class="sxs-lookup"><span data-stu-id="b546e-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="b546e-307">Eseguire l'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-307">Run the experiment.</span></span>

<span data-ttu-id="b546e-308">Per visualizzare l'output del modulo [Evaluate Model][evaluate-model], fare clic sulla porta di output e selezionare **Visualize** (Visualizza).</span><span class="sxs-lookup"><span data-stu-id="b546e-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="b546e-309">![Risultati di valutazione dell'esperimento][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="b546e-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/><span data-ttu-id="b546e-310">
***Risultati di valutazione dell'esperimento***</span><span class="sxs-lookup"><span data-stu-id="b546e-310">
***Evaluation results for the experiment***</span></span>

<span data-ttu-id="b546e-311">Per il modello vengono visualizzate le seguenti statistiche:</span><span class="sxs-lookup"><span data-stu-id="b546e-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="b546e-312">**Mean Absolute Error** (MAE, errore assoluto medio): media degli errori assoluti (un *errore* è la differenza tra il valore stimato e quello effettivo).</span><span class="sxs-lookup"><span data-stu-id="b546e-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="b546e-313">**Root Mean Squared Error** (RMSE, radice errore quadratico medio): radice quadrata della media degli errori quadratici delle stime effettuate sul set di dati di test.</span><span class="sxs-lookup"><span data-stu-id="b546e-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="b546e-314">**Relative Absolute Error**(errore assoluto relativo): media degli errori assoluti relativamente alla differenza assoluta tra i valori effettivi e la media di tutti i valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="b546e-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="b546e-315">**Relative Squared Error**(errore quadratico relativo): media degli errori quadratici relativamente alla differenza quadratica tra i valori effettivi e la media di tutti i valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="b546e-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="b546e-316">**Coefficient of Determination** (coefficiente di determinazione): noto anche come **valore quadratico R**, è una metrica statistica che indica l'esattezza del modello rispetto ai dati.</span><span class="sxs-lookup"><span data-stu-id="b546e-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="b546e-317">Per ogni statistica di errore, sono preferibili i valori più piccoli.</span><span class="sxs-lookup"><span data-stu-id="b546e-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="b546e-318">Un valore più piccolo indica che le stime sono più vicine ai valori effettivi.</span><span class="sxs-lookup"><span data-stu-id="b546e-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="b546e-319">Per **Coefficient of Determination**più il valore si avvicina a uno (1,0) più le stime sono migliori.</span><span class="sxs-lookup"><span data-stu-id="b546e-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="b546e-320">Esperimento finale</span><span class="sxs-lookup"><span data-stu-id="b546e-320">Final experiment</span></span>

<span data-ttu-id="b546e-321">L'esperimento dovrebbe avere un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="b546e-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="b546e-322">![Esperimento finale][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="b546e-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="b546e-323">
***Esperimento finale***</span><span class="sxs-lookup"><span data-stu-id="b546e-323">
***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="b546e-324">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b546e-324">Next steps</span></span>

<span data-ttu-id="b546e-325">Dopo aver completato la prima esercitazione di Machine Learning e impostato l'esperimento, è possibile migliorare il modello e successivamente distribuirlo come servizio Web predittivo.</span><span class="sxs-lookup"><span data-stu-id="b546e-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="b546e-326">**Eseguire l'iterazione per migliorare il modello**: ad esempio, è possibile modificare le caratteristiche usate per la stima.</span><span class="sxs-lookup"><span data-stu-id="b546e-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="b546e-327">In alternativa, è possibile modificare le proprietà dell'algoritmo [Linear Regression][linear-regression] (Regressione lineare) oppure provare un algoritmo diverso.</span><span class="sxs-lookup"><span data-stu-id="b546e-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="b546e-328">È anche possibile aggiungere contemporaneamente più algoritmi di Machine Learning all'esperimento e confrontarne due usando il modulo [Evaluate Model][evaluate-model] (Modello di valutazione).</span><span class="sxs-lookup"><span data-stu-id="b546e-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="b546e-329">Per un esempio di come confrontare più modelli in un esperimento singolo, vedere [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) (Confrontare regressori) in [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="b546e-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="b546e-330">Usare il pulsante **SAVE AS** (SALVA CON NOME) nella parte inferiore della pagina per copiare eventuali iterazioni dell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="b546e-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="b546e-331">È possibile visualizzare tutte le iterazioni dell'esperimento facendo clic su **VIEW RUN HISTORY** (VISUALIZZA LA CRONOLOGIA DI ESECUZIONE) nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="b546e-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="b546e-332">Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="b546e-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="b546e-333">**Distribuire il modello come servizio Web predittivo**: se si è soddisfatti con i risultati del modello, è possibile distribuirlo come servizio Web per stimare prezzi di automobili usando dati nuovi.</span><span class="sxs-lookup"><span data-stu-id="b546e-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="b546e-334">Per altre informazioni dettagliate, vedere [Distribuire un servizio Web di Azure Machine Learning][publish].</span><span class="sxs-lookup"><span data-stu-id="b546e-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="b546e-335">Per altre informazioni:</span><span class="sxs-lookup"><span data-stu-id="b546e-335">Want to learn more?</span></span> <span data-ttu-id="b546e-336">Per una procedura più completa e dettagliata del processo di creazione, training, assegnazione di punteggi e distribuzione di un modello, vedere [Sviluppare una soluzione predittiva con Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="b546e-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

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

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
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
