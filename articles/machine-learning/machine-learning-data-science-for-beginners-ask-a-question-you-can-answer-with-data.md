---
title: Formulare una domanda a cui i dati possono rispondere - Problemi di data science - Azure Machine Learning | Microsoft Docs
description: Informazioni su come formulare una domanda mirata sull'analisi scientifica dei dati in Analisi scientifica dei dati per principianti, video 3. Include un confronto delle domande di classificazione e regressione.
keywords: problemi di analisi scientifica dei dati, domande di analisi scientifica dei dati, formulare domande, domande di regressione, domande di classificazione, domanda ben strutturata
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: 5b9501e3-9964-417a-8ffc-8913103da77b
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: 0495dbab72024e504ae33d35f16a212a2084bc10
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="854ac-105">Porre una domanda a cui è possibile rispondere con i dati</span><span class="sxs-lookup"><span data-stu-id="854ac-105">Ask a question you can answer with data</span></span>
## <a name="video-3-data-science-for-beginners-series"></a><span data-ttu-id="854ac-106">Video 3: Analisi scientifica dei dati per principianti</span><span class="sxs-lookup"><span data-stu-id="854ac-106">Video 3: Data Science for Beginners series</span></span>
<span data-ttu-id="854ac-107">Informazioni su come formulare un problema come domanda sull'analisi scientifica dei dati in Analisi scientifica dei dati per principianti, video 3.</span><span class="sxs-lookup"><span data-stu-id="854ac-107">Learn how to formulate a data science problem into a question in Data Science for Beginners video 3.</span></span> <span data-ttu-id="854ac-108">Questo video include un confronto di domande per gli algoritmi di classificazione e regressione.</span><span class="sxs-lookup"><span data-stu-id="854ac-108">This video includes a comparison of questions for classification and regression algorithms.</span></span>

<span data-ttu-id="854ac-109">Per trarre il meglio dalla serie è consigliabile guardare tutti i video.</span><span class="sxs-lookup"><span data-stu-id="854ac-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="854ac-110">[L'elenco dei video è disponibile qui](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="854ac-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Data-science-for-beginners-Ask-a-question-you-can-answer-with-data/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="854ac-111">Altri video della serie</span><span class="sxs-lookup"><span data-stu-id="854ac-111">Other videos in this series</span></span>
<span data-ttu-id="854ac-112">*Analisi scientifica dei dati per principianti* è una rapida introduzione all'analisi scientifica dei dati in cinque brevi video.</span><span class="sxs-lookup"><span data-stu-id="854ac-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="854ac-113">Video 1: [5 domande a cui può rispondere l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min e 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="854ac-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="854ac-114">Video 2: [Verifica della preparazione dei dati per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span><span class="sxs-lookup"><span data-stu-id="854ac-114">Video 2: [Is your data ready for data science?](machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science.md)</span></span> <span data-ttu-id="854ac-115">*(4 min e 56 sec)*</span><span class="sxs-lookup"><span data-stu-id="854ac-115">*(4 min 56 sec)*</span></span>
* <span data-ttu-id="854ac-116">Video 3: Porre una domanda a cui è possibile rispondere con i dati</span><span class="sxs-lookup"><span data-stu-id="854ac-116">Video 3: Ask a question you can answer with data</span></span>
* <span data-ttu-id="854ac-117">Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="854ac-117">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="854ac-118">Video 5: [Copiare il lavoro di altre persone per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min e 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="854ac-118">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-ask-a-question-you-can-answer-with-data"></a><span data-ttu-id="854ac-119">Trascrizione: Porre una domanda a cui è possibile rispondere con i dati</span><span class="sxs-lookup"><span data-stu-id="854ac-119">Transcript: Ask a question you can answer with data</span></span>
<span data-ttu-id="854ac-120">Questo è il terzo video della serie "Analisi scientifica dei dati per principianti".</span><span class="sxs-lookup"><span data-stu-id="854ac-120">Welcome to the third video in the series "Data Science for Beginners."</span></span>  

<span data-ttu-id="854ac-121">In questo video vengono forniti suggerimenti per formulare una domanda a cui è possibile rispondere con i dati.</span><span class="sxs-lookup"><span data-stu-id="854ac-121">In this one, you'll get some tips for formulating a question you can answer with data.</span></span>

<span data-ttu-id="854ac-122">È possibile sfruttare al meglio questo video guardando prima i due video precedenti di questa serie: "Le 5 domande a cui l'analisi scientifica dei dati può rispondere" e "Sono pronti i dati per l'analisi scientifica?"</span><span class="sxs-lookup"><span data-stu-id="854ac-122">You might get more out of this video, if you first watch the two earlier videos in this series: "The 5 questions data science can answer" and "Is your data is ready for data science?"</span></span>

## <a name="ask-a-sharp-question"></a><span data-ttu-id="854ac-123">Porre una domanda ben strutturata</span><span class="sxs-lookup"><span data-stu-id="854ac-123">Ask a sharp question</span></span>
<span data-ttu-id="854ac-124">È stato spiegato come l'analisi scientifica dei dati sia il processo d'uso di nomi, detti anche categorie o etichette, e di numeri per prevedere una risposta a una domanda.</span><span class="sxs-lookup"><span data-stu-id="854ac-124">We've talked about how data science is the process of using names (also called categories or labels) and numbers to predict an answer to a question.</span></span> <span data-ttu-id="854ac-125">Non può però essere una domanda qualsiasi, deve essere una *domanda ben strutturata*</span><span class="sxs-lookup"><span data-stu-id="854ac-125">But it can't be just any question; it has to be a *sharp question.*</span></span>

<span data-ttu-id="854ac-126">A una domanda vaga non è necessario rispondere con un nome o un numero,</span><span class="sxs-lookup"><span data-stu-id="854ac-126">A vague question doesn't have to be answered with a name or a number.</span></span> <span data-ttu-id="854ac-127">mentre lo è per una domanda ben strutturata.</span><span class="sxs-lookup"><span data-stu-id="854ac-127">A sharp question must.</span></span>

<span data-ttu-id="854ac-128">Si immagini di trovare una lampada magica con un genio che risponde puntualmente a qualsiasi domanda.</span><span class="sxs-lookup"><span data-stu-id="854ac-128">Imagine you found a magic lamp with a genie who will truthfully answer any question you ask.</span></span> <span data-ttu-id="854ac-129">Ma è un genio dispettoso, che tenta di rendere la risposta quanto più vaga e confusa possibile.</span><span class="sxs-lookup"><span data-stu-id="854ac-129">But it's a mischievous genie, and he'll try to make his answer as vague and confusing as he can get away with.</span></span> <span data-ttu-id="854ac-130">Si vuole costringerlo con una domanda così precisa a cui non potrà fare a meno di dare la risposta che si vuole ottenere.</span><span class="sxs-lookup"><span data-stu-id="854ac-130">You want to pin him down with a question so airtight that he can't help but tell you what you want to know.</span></span>

<span data-ttu-id="854ac-131">Se si pone una domanda vaga, come "Cosa accadrà al mio titolo azionario?", il genio potrebbe rispondere "Cambierà il prezzo".</span><span class="sxs-lookup"><span data-stu-id="854ac-131">If you were to ask a vague question, like "What's going to happen with my stock?", the genie might answer, "The price will change".</span></span> <span data-ttu-id="854ac-132">È una risposta vera, ma non è molto utile.</span><span class="sxs-lookup"><span data-stu-id="854ac-132">That's a truthful answer, but it's not very helpful.</span></span>

<span data-ttu-id="854ac-133">Se però si pone una domanda ben strutturata, ad esempio "Quale sarà il prezzo di vendita del mio titolo la prossima settimana?", il genio non potrà fare a meno di fornire una risposta specifica e prevedere un prezzo di vendita.</span><span class="sxs-lookup"><span data-stu-id="854ac-133">But if you were to ask a sharp question, like "What will my stock's sale price be next week?", the genie can't help but give you a specific answer and predict a sale price.</span></span>

## <a name="examples-of-your-answer-target-data"></a><span data-ttu-id="854ac-134">Esempi di risposta: dati di destinazione</span><span class="sxs-lookup"><span data-stu-id="854ac-134">Examples of your answer: Target data</span></span>
<span data-ttu-id="854ac-135">Una volta formulata la domanda, verificare se sono disponibili esempi di risposta nei dati.</span><span class="sxs-lookup"><span data-stu-id="854ac-135">Once you formulate your question, check to see whether you have examples of the answer in your data.</span></span>

<span data-ttu-id="854ac-136">Se la domanda è "Quale sarà il prezzo di vendita del mio titolo la prossima settimana?",</span><span class="sxs-lookup"><span data-stu-id="854ac-136">If our question is "What will my stock's sale price be next week?"</span></span> <span data-ttu-id="854ac-137">è necessario assicurarsi che i dati includano la cronologia dei prezzi dei titoli azionari.</span><span class="sxs-lookup"><span data-stu-id="854ac-137">then we have to make sure our data includes the stock price history.</span></span>

<span data-ttu-id="854ac-138">Se la domanda è "Quale auto del mio parco macchine avrà per prima un guasto?",</span><span class="sxs-lookup"><span data-stu-id="854ac-138">If our question is "Which car in my fleet is going to fail first?"</span></span> <span data-ttu-id="854ac-139">sarà necessario assicurarsi che i dati includano informazioni sui guasti precedenti.</span><span class="sxs-lookup"><span data-stu-id="854ac-139">then we have to make sure our data includes information about previous failures.</span></span>

![Dati di destinazione: esempi di risposta.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/target-data.png)

<span data-ttu-id="854ac-142">Questi esempi di risposte sono detti destinazione.</span><span class="sxs-lookup"><span data-stu-id="854ac-142">These examples of answers are called a target.</span></span> <span data-ttu-id="854ac-143">Una destinazione è ciò che si sta tentando di stimare in relazione ai punti dati futuri, se si tratta di una categoria o di un numero.</span><span class="sxs-lookup"><span data-stu-id="854ac-143">A target is what we are trying to predict about future data points, whether it's a category or a number.</span></span>

<span data-ttu-id="854ac-144">Se non sono disponibili dati di destinazione, è necessario ottenerne alcuni.</span><span class="sxs-lookup"><span data-stu-id="854ac-144">If you don't have any target data, you'll need to get some.</span></span> <span data-ttu-id="854ac-145">Non sarà possibile rispondere alla domanda senza questi dati.</span><span class="sxs-lookup"><span data-stu-id="854ac-145">You won't be able to answer your question without it.</span></span>

## <a name="reformulate-your-question"></a><span data-ttu-id="854ac-146">Riformulare la domanda</span><span class="sxs-lookup"><span data-stu-id="854ac-146">Reformulate your question</span></span>
<span data-ttu-id="854ac-147">In alcuni casi è possibile riformulare la domanda per ottenere una risposta più utile.</span><span class="sxs-lookup"><span data-stu-id="854ac-147">Sometimes you can reword your question to get a more useful answer.</span></span>

<span data-ttu-id="854ac-148">La domanda "Il punto dati è A o B?"</span><span class="sxs-lookup"><span data-stu-id="854ac-148">The question "Is this data point A or B?"</span></span> <span data-ttu-id="854ac-149">stima la categoria (o nome o etichetta) di un elemento.</span><span class="sxs-lookup"><span data-stu-id="854ac-149">predicts the category (or name or label) of something.</span></span> <span data-ttu-id="854ac-150">Per rispondere si userà un *algoritmo di classificazione*.</span><span class="sxs-lookup"><span data-stu-id="854ac-150">To answer it, we use a *classification algorithm*.</span></span>

<span data-ttu-id="854ac-151">La domanda "Quanto?"</span><span class="sxs-lookup"><span data-stu-id="854ac-151">The question "How much?"</span></span> <span data-ttu-id="854ac-152">o "Quanti?"</span><span class="sxs-lookup"><span data-stu-id="854ac-152">or "How many?"</span></span> <span data-ttu-id="854ac-153">prevede una quantità.</span><span class="sxs-lookup"><span data-stu-id="854ac-153">predicts an amount.</span></span> <span data-ttu-id="854ac-154">Per rispondere si userà un *algoritmo di regressione*.</span><span class="sxs-lookup"><span data-stu-id="854ac-154">To answer it we use a *regression algorithm*.</span></span>

<span data-ttu-id="854ac-155">Per vedere come è possibile trasformare questi dati, si osserverà la domanda "Quale notizia è più interessante per questo lettore?"</span><span class="sxs-lookup"><span data-stu-id="854ac-155">To see how we can transform these, let's look at the question, "Which news story is the most interesting to this reader?"</span></span> <span data-ttu-id="854ac-156">Richiede una stima di una singola opzione tra molte possibilità, in altre parole "È A o B o C o D?"</span><span class="sxs-lookup"><span data-stu-id="854ac-156">It asks for a prediction of a single choice from many possibilities - in other words "Is this A or B or C or D?"</span></span> <span data-ttu-id="854ac-157">e si userà un algoritmo di classificazione.</span><span class="sxs-lookup"><span data-stu-id="854ac-157">- and would use a classification algorithm.</span></span>

<span data-ttu-id="854ac-158">La risposta a questa domanda può tuttavia essere semplice se la si riformula in "Quanto è interessante ogni notizia in questo elenco per il lettore?"</span><span class="sxs-lookup"><span data-stu-id="854ac-158">But, this question may be easier to answer if you reword it as "How interesting is each story on this list to this reader?"</span></span> <span data-ttu-id="854ac-159">A questo punto è possibile assegnare a ogni articolo un punteggio numerico e quindi è facile identificare quello con il punteggio più elevato.</span><span class="sxs-lookup"><span data-stu-id="854ac-159">Now you can give each article a numerical score, and then it's easy to identify the highest-scoring article.</span></span> <span data-ttu-id="854ac-160">Si tratta di una riformulazione della domanda di classificazione in una domanda di regressione o di quantità.</span><span class="sxs-lookup"><span data-stu-id="854ac-160">This is a rephrasing of the classification question into a regression question or How much?</span></span>

![Riformulare la domanda.](./media/machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data/classification-question-vs-regression-question.png)

<span data-ttu-id="854ac-163">Come si pone una domanda è un'indicazione per individuare l'algoritmo che può fornire una risposta.</span><span class="sxs-lookup"><span data-stu-id="854ac-163">How you ask a question is a clue to which algorithm can give you an answer.</span></span>

<span data-ttu-id="854ac-164">Si noterà che alcune famiglie di algoritmi, come quelli nell'esempio relativo alle notizie, sono strettamente correlate.</span><span class="sxs-lookup"><span data-stu-id="854ac-164">You'll find that certain families of algorithms - like the ones in our news story example - are closely related.</span></span> <span data-ttu-id="854ac-165">È possibile riformulare la domanda per usare l'algoritmo che fornisce la risposta più utile.</span><span class="sxs-lookup"><span data-stu-id="854ac-165">You can reformulate your question to use the algorithm that gives you the most useful answer.</span></span>

<span data-ttu-id="854ac-166">La cosa più importante, tuttavia, è porre una domanda ben strutturata, quella a cui è possibile fornire una risposta con i dati.</span><span class="sxs-lookup"><span data-stu-id="854ac-166">But, most important, ask that sharp question - the question that you can answer with data.</span></span> <span data-ttu-id="854ac-167">Occorre anche assicurarsi di avere i dati corretti per rispondere.</span><span class="sxs-lookup"><span data-stu-id="854ac-167">And be sure you have the right data to answer it.</span></span>

<span data-ttu-id="854ac-168">Sono stati trattati alcuni principi di base per porre una domanda a cui è possibile rispondere con i dati.</span><span class="sxs-lookup"><span data-stu-id="854ac-168">We've talked about some basic principles for asking a question you can answer with data.</span></span>

<span data-ttu-id="854ac-169">Anche gli altri video della serie "Analisi scientifica dei dati per principianti" di Microsoft Azure Machine Learning meritano di essere visti.</span><span class="sxs-lookup"><span data-stu-id="854ac-169">Be sure to check out the other videos in "Data Science for Beginners" from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="854ac-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="854ac-170">Next steps</span></span>
* [<span data-ttu-id="854ac-171">Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="854ac-171">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="854ac-172">Leggere l'Introduzione all'apprendimento automatico in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="854ac-172">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
