---
title: Eseguire il debug del modello in Azure Machine Learning | Documentazione Microsoft
description: Come eseguire il debug di errori generati dai moduli dal training e dalla classificazione del modello in Azure Machine Learning.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="62d99-103">Debug del modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="62d99-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="62d99-104">In questo articolo vengono spiegati i potenziali motivi per i quali possono verificarsi i due errori indicati di seguito durante l'esecuzione di un modello:</span><span class="sxs-lookup"><span data-stu-id="62d99-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="62d99-105">il modulo [Train Model][train-model] genera un errore</span><span class="sxs-lookup"><span data-stu-id="62d99-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="62d99-106">il modulo [Score Model][score-model] genera risultati non corretti</span><span class="sxs-lookup"><span data-stu-id="62d99-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="62d99-107">Il modulo Train Model genera un errore</span><span class="sxs-lookup"><span data-stu-id="62d99-107">Train Model Module produces an error</span></span>

![Immagine1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="62d99-109">Il modulo [Training del modello][train-model] prevede i due valori di input seguenti:</span><span class="sxs-lookup"><span data-stu-id="62d99-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="62d99-110">Il tipo di modello di Machine Learning della raccolta di modelli forniti da Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="62d99-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="62d99-111">I dati di training con una colonna Etichetta specifica che indica la variabile da stimare (le altre colonne vengono considerate funzionalità).</span><span class="sxs-lookup"><span data-stu-id="62d99-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="62d99-112">Questo modulo può generare un errore nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="62d99-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="62d99-113">La colonna Etichetta è stata specificata in modo errato.</span><span class="sxs-lookup"><span data-stu-id="62d99-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="62d99-114">Questo può succedere se è selezionata più di una colonna come Etichetta oppure se è selezionato un indice di colonna non corretto.</span><span class="sxs-lookup"><span data-stu-id="62d99-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="62d99-115">Ad esempio, il secondo caso è applicabile se è stato usato un indice di colonna pari a 30 con un set di dati di input dotato di 25 colonne soltanto.</span><span class="sxs-lookup"><span data-stu-id="62d99-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="62d99-116">Il set di dati non contiene nessuna colonna per le caratteristiche.</span><span class="sxs-lookup"><span data-stu-id="62d99-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="62d99-117">Se ad esempio il set di dati di input dispone solo di una colonna, contrassegnata come colonna Etichetta, non sono presenti caratteristiche con cui creare il modello.</span><span class="sxs-lookup"><span data-stu-id="62d99-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="62d99-118">In questo caso, il modulo [Train Model][train-model] genera un errore.</span><span class="sxs-lookup"><span data-stu-id="62d99-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="62d99-119">Il set di dati di input (caratteristiche o etichetta) contiene Infinity come valore.</span><span class="sxs-lookup"><span data-stu-id="62d99-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="62d99-120">Il modulo Classificazione del modello genera risultati non corretti</span><span class="sxs-lookup"><span data-stu-id="62d99-120">Score Model Module produces incorrect results</span></span>

![Immagine2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="62d99-122">In un tipico esperimento di training/testing per l'apprendimento supervisionato, il modulo [Divisione dei dati][split] separa il set di dati originale in due parti: una usata per eseguire il training del modello e l'altra riservata alla classificazione delle prestazioni del modello.</span><span class="sxs-lookup"><span data-stu-id="62d99-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="62d99-123">Il modello sottoposto a training viene quindi usato per calcolare il punteggio dei dati di test, dopo il quale vengono valutati i risultati per determinare la precisione del modello.</span><span class="sxs-lookup"><span data-stu-id="62d99-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="62d99-124">Il modulo [Score Model][score-model] richiede due input:</span><span class="sxs-lookup"><span data-stu-id="62d99-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="62d99-125">Output del modello sottoposto a training dal modulo [Training modello][train-model].</span><span class="sxs-lookup"><span data-stu-id="62d99-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="62d99-126">Un set di dati per la classificazione diverso da quello usato per il training del modello.</span><span class="sxs-lookup"><span data-stu-id="62d99-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="62d99-127">Può accadere che, nonostante il buon esito dell'esperimento, il modulo [Classificazione modello][score-model] produca risultati non corretti.</span><span class="sxs-lookup"><span data-stu-id="62d99-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="62d99-128">Ciò può essere dovuto a diversi scenari:</span><span class="sxs-lookup"><span data-stu-id="62d99-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="62d99-129">Se l'etichetta specificata è categorica e un modello di regressione è sottoposto a training sui dati, può essere prodotto un output errato dal modulo [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="62d99-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="62d99-130">Questo si verifica perché la regressione richiede una variabile di risposta continua.</span><span class="sxs-lookup"><span data-stu-id="62d99-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="62d99-131">In questo caso sarebbe più opportuno usare un modello di classificazione.</span><span class="sxs-lookup"><span data-stu-id="62d99-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="62d99-132">Analogamente, se un modello di classificazione è sottoposto a training su un set di dati con numeri a virgola mobile nella colonna Etichetta, tale modello può produrre risultati indesiderati.</span><span class="sxs-lookup"><span data-stu-id="62d99-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="62d99-133">Questo si verifica perché la classificazione richiede una variabile di risposta discreta che ammette solo valori all'interno di un set di classi finito e solitamente di dimensioni ridotte.</span><span class="sxs-lookup"><span data-stu-id="62d99-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="62d99-134">Se il set di dati non contiene tutte le caratteristiche usate per eseguire il training del modello, il modulo [Score Model][score-model] genera un errore.</span><span class="sxs-lookup"><span data-stu-id="62d99-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="62d99-135">Il modulo [Score Model][score-model] non genera alcun output corrispondente a una riga nel set di dati di punteggio contenente un valore mancante o infinito per una delle proprie caratteristiche.</span><span class="sxs-lookup"><span data-stu-id="62d99-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="62d99-136">Il modulo [Score Model][score-model] può generare output identici per tutte le righe nel set di dati di punteggio.</span><span class="sxs-lookup"><span data-stu-id="62d99-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="62d99-137">Ciò potrebbe verificarsi, ad esempio, quando si tenta di eseguire una classificazione usando insiemi di decisioni se il numero minimo di esempi per nodo foglia viene scelto per superare il numero di esempi di training disponibili.</span><span class="sxs-lookup"><span data-stu-id="62d99-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

