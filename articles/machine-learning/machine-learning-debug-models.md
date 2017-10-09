---
title: aaaDebug il modello in Azure Machine Learning | Documenti Microsoft
description: Gli errori di toodebug generati dal modello di training e il modello di punteggio come moduli in Azure Machine Learning.
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
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="179f0-103">Debug del modello in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="179f0-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="179f0-104">Questo articolo descrive le cause possibili di hello perché uno dei seguenti due errori hello potrebbero essere presenti durante l'esecuzione di un modello:</span><span class="sxs-lookup"><span data-stu-id="179f0-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="179f0-105">Hello [Train Model] [ train-model] modulo genera un errore</span><span class="sxs-lookup"><span data-stu-id="179f0-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="179f0-106">Hello [Score Model] [ score-model] modulo genera risultati non corretti</span><span class="sxs-lookup"><span data-stu-id="179f0-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="179f0-107">Il modulo Train Model genera un errore</span><span class="sxs-lookup"><span data-stu-id="179f0-107">Train Model Module produces an error</span></span>

![Immagine1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="179f0-109">Hello [Train Model] [ train-model] modulo prevede due input:</span><span class="sxs-lookup"><span data-stu-id="179f0-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="179f0-110">tipo di Hello del modello di machine learning dalla raccolta hello di modelli forniti da Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="179f0-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="179f0-111">dati di training con una colonna di etichetta specificata, che specifica Hello hello toopredict variabile (hello altre colonne vengono considerate toobe funzionalità).</span><span class="sxs-lookup"><span data-stu-id="179f0-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="179f0-112">Questo modulo può produrre un errore in hello seguenti casi:</span><span class="sxs-lookup"><span data-stu-id="179f0-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="179f0-113">colonna di etichetta Hello è stato specificato correttamente.</span><span class="sxs-lookup"><span data-stu-id="179f0-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="179f0-114">Questa situazione può verificarsi se è selezionata più di una colonna come etichetta hello o un indice di colonna non è selezionato.</span><span class="sxs-lookup"><span data-stu-id="179f0-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="179f0-115">Ad esempio, secondo caso hello verrà applicata se viene utilizzato un indice di colonna pari a 30 con un set di dati di input che ha solo 25 colonne.</span><span class="sxs-lookup"><span data-stu-id="179f0-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="179f0-116">Hello dataset non contiene tutte le colonne di funzionalità.</span><span class="sxs-lookup"><span data-stu-id="179f0-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="179f0-117">Ad esempio, se hello di un set di dati dell'input ha una sola colonna, che è contrassegnata come colonna di etichetta hello, non vi sarà alcuna funzionalità con il modello di hello toobuild.</span><span class="sxs-lookup"><span data-stu-id="179f0-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="179f0-118">In questo caso, hello [Train Model] [ train-model] modulo genera un errore.</span><span class="sxs-lookup"><span data-stu-id="179f0-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="179f0-119">Hello input set di dati (funzionalità o etichetta) contiene un numero infinito come valore.</span><span class="sxs-lookup"><span data-stu-id="179f0-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="179f0-120">Il modulo Classificazione del modello genera risultati non corretti</span><span class="sxs-lookup"><span data-stu-id="179f0-120">Score Model Module produces incorrect results</span></span>

![Immagine2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="179f0-122">In genere esperimento per l'apprendimento supervisionato training/test, hello [dati divisi] [ split] modulo suddivide hello set di dati originale in due parti: una parte è il modello di hello tootrain utilizzato e viene utilizzata una parte tooscore come modello con training hello prestazioni.</span><span class="sxs-lookup"><span data-stu-id="179f0-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="179f0-123">modello con training Hello è usato tooscore hello dati di test, dopo il quale i risultati di hello sono valutate toodetermine hello accuratezza del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="179f0-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="179f0-124">Hello [Score Model] [ score-model] modulo richiede due input:</span><span class="sxs-lookup"><span data-stu-id="179f0-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="179f0-125">Un output di un modello con Training da hello [Train Model] [ train-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="179f0-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="179f0-126">Un punteggio set di dati che è diverso dal set di dati hello utilizzato il modello di hello tootrain.</span><span class="sxs-lookup"><span data-stu-id="179f0-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="179f0-127">È possibile che, anche se ha esito positivo esperimento hello, hello del [Score Model] [ score-model] modulo genera risultati non corretti.</span><span class="sxs-lookup"><span data-stu-id="179f0-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="179f0-128">Diversi scenari possono generare questo toohappen:</span><span class="sxs-lookup"><span data-stu-id="179f0-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="179f0-129">Se hello specificato etichetta è categorica e un modello di regressione è sottoposto a training sui dati hello, verrà prodotto un output non corretto da hello [Score Model] [ score-model] modulo.</span><span class="sxs-lookup"><span data-stu-id="179f0-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="179f0-130">Questo si verifica perché la regressione richiede una variabile di risposta continua.</span><span class="sxs-lookup"><span data-stu-id="179f0-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="179f0-131">In questo caso, sarebbe più adatta toouse un modello di classificazione.</span><span class="sxs-lookup"><span data-stu-id="179f0-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="179f0-132">Analogamente, se un modello di classificazione viene eseguito il training su un set di dati con numeri a virgola mobile nella colonna di etichetta hello, può produrre risultati indesiderati.</span><span class="sxs-lookup"><span data-stu-id="179f0-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="179f0-133">Questo si verifica perché la classificazione richiede una variabile di risposta discreta che ammette solo valori all'interno di un set di classi finito e solitamente di dimensioni ridotte.</span><span class="sxs-lookup"><span data-stu-id="179f0-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="179f0-134">Se hello punteggio set di dati non contiene tutti i modelli di hello tootrain di funzionalità utilizzate hello, hello [Score Model] [ score-model] genera un errore.</span><span class="sxs-lookup"><span data-stu-id="179f0-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="179f0-135">Se una riga nel set di dati di punteggio hello contiene un valore mancante o un valore infinito per tutte le sue funzionalità, hello [Score Model] [ score-model] non produrrà qualsiasi riga di output corrispondente toothat.</span><span class="sxs-lookup"><span data-stu-id="179f0-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="179f0-136">Hello [Score Model] [ score-model] può produrre output identici per tutte le righe nel set di dati di punteggio hello.</span><span class="sxs-lookup"><span data-stu-id="179f0-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="179f0-137">Ciò può verificarsi, ad esempio, quando si tenta di classificazione utilizzando foreste delle decisioni, numero minimo di hello degli esempi per ogni nodo foglia sia toobe più hello numero di esempi di training disponibili.</span><span class="sxs-lookup"><span data-stu-id="179f0-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

