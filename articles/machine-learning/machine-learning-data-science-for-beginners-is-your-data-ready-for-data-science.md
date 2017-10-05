---
title: Sono pronti i dati per l'analisi scientifica? Valutazione dei dati con Azure Machine Learning | Microsoft Docs
description: I 4 criteri per rendere pronti i dati per l'analisi scientifica. Nel video 2 Analisi scientifica dei dati per principianti vengono illustrati esempi concreti per la valutazione dei dati di base.
keywords: "dati rilevanti, valutare i dati, preparare i dati, criteri dei dati, compatibilità con i dati"
services: machine-learning
documentationcenter: na
author: cjgronlund
manager: jhubbard
editor: cjgronlund
ms.assetid: d502062c-da70-4b21-9054-0bfd9902612e
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: cgronlun
ms.openlocfilehash: c4a8bc11aec2f71796f589c0af54cc92253e5180
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="23348-106">Sono pronti i dati per l'analisi scientifica?</span><span class="sxs-lookup"><span data-stu-id="23348-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="23348-107">Video 2: Analisi scientifica dei dati per principianti</span><span class="sxs-lookup"><span data-stu-id="23348-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="23348-108">Informazioni su come valutare i dati per assicurarsi che questo processo soddisfi i criteri di base per la preparazione per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="23348-108">Learn how to evaluate your data to make sure it meets basic criteria to be ready for data science.</span></span>

<span data-ttu-id="23348-109">Per trarre il meglio dalla serie è consigliabile guardare tutti i video.</span><span class="sxs-lookup"><span data-stu-id="23348-109">To get the most out of the series, watch them all.</span></span> <span data-ttu-id="23348-110">[L'elenco dei video è disponibile qui](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="23348-110">[Go to the list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="23348-111">Altri video della serie</span><span class="sxs-lookup"><span data-stu-id="23348-111">Other videos in this series</span></span>
<span data-ttu-id="23348-112">*Analisi scientifica dei dati per principianti* è una rapida introduzione all'analisi scientifica dei dati in cinque brevi video.</span><span class="sxs-lookup"><span data-stu-id="23348-112">*Data Science for Beginners* is a quick introduction to data science in five short videos.</span></span>

* <span data-ttu-id="23348-113">Video 1: [5 domande a cui può rispondere l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min e 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="23348-113">Video 1: [The 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="23348-114">Video 2: Verifica della preparazione dei dati per l'analisi scientifica dei dati</span><span class="sxs-lookup"><span data-stu-id="23348-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="23348-115">Video 3: [Porre una domanda a cui è possibile rispondere con i dati](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min e 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="23348-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="23348-116">Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="23348-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="23348-117">Video 5: [Copiare il lavoro di altre persone per l'analisi scientifica dei dati](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min e 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="23348-117">Video 5: [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="23348-118">Trascrizione: Sono pronti i dati per l'analisi scientifica?</span><span class="sxs-lookup"><span data-stu-id="23348-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="23348-119">Questo è il video "I tuoi dati sono pronti per l'analisi scientifica?",</span><span class="sxs-lookup"><span data-stu-id="23348-119">Welcome to "Is your data ready for data science?"</span></span> <span data-ttu-id="23348-120">il secondo della serie *Data Science for Beginners* (Analisi scientifica dei dati per principianti).</span><span class="sxs-lookup"><span data-stu-id="23348-120">the second video in the series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="23348-121">Per ottenere le risposte desiderate dall'analisi scientifica dei dati, è necessario fornire materiale non elaborato di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="23348-121">Before data science can give you the answers you want, you have to give it some high-quality raw materials to work with.</span></span> <span data-ttu-id="23348-122">Proprio come preparare una pizza: più buoni sono gli ingredienti usati, migliore sarà il risultato finale.</span><span class="sxs-lookup"><span data-stu-id="23348-122">Just like making a pizza, the better the ingredients you start with, the better the final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="23348-123">Criteri per i dati</span><span class="sxs-lookup"><span data-stu-id="23348-123">Criteria for data</span></span>
<span data-ttu-id="23348-124">Quindi, nel caso dell'analisi scientifica dei dati, esistono alcuni ingredienti che devono essere amalgamati insieme.</span><span class="sxs-lookup"><span data-stu-id="23348-124">So, in the case of data science, there are some ingredients that we need to pull together.</span></span>

<span data-ttu-id="23348-125">Sono fondamentali dati:</span><span class="sxs-lookup"><span data-stu-id="23348-125">We need data that is:</span></span>

* <span data-ttu-id="23348-126">Rilevanti</span><span class="sxs-lookup"><span data-stu-id="23348-126">Relevant</span></span>
* <span data-ttu-id="23348-127">Connesso</span><span class="sxs-lookup"><span data-stu-id="23348-127">Connected</span></span>
* <span data-ttu-id="23348-128">Accurati</span><span class="sxs-lookup"><span data-stu-id="23348-128">Accurate</span></span>
* <span data-ttu-id="23348-129">In quantità sufficiente</span><span class="sxs-lookup"><span data-stu-id="23348-129">Enough to work with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="23348-130">Sono rilevanti i dati?</span><span class="sxs-lookup"><span data-stu-id="23348-130">Is your data relevant?</span></span>
<span data-ttu-id="23348-131">Per prima cosa, i dati devono essere rilevanti.</span><span class="sxs-lookup"><span data-stu-id="23348-131">So the first ingredient - we need data that's relevant.</span></span>

![Dati rilevanti vs. dati irrilevanti, valutare i dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="23348-133">Osservando la tabella a sinistra,</span><span class="sxs-lookup"><span data-stu-id="23348-133">Look at the table on the left.</span></span> <span data-ttu-id="23348-134">si apprende che abbiamo incontrato sette persone fuori dai bar di Boston, misurato il livello di alcol nel sangue, la media battuta dalla Red Sox nell'ultimo match e il prezzo del latte nel negozio di comodità più vicino.</span><span class="sxs-lookup"><span data-stu-id="23348-134">We met seven people outside of Boston bars, measured their blood alcohol level, the Red Sox batting average in their last game, and the price of milk in the nearest convenience store.</span></span>

<span data-ttu-id="23348-135">Si tratta di dati del tutto legittimi.</span><span class="sxs-lookup"><span data-stu-id="23348-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="23348-136">L'unico inconveniente è che non sono rilevanti.</span><span class="sxs-lookup"><span data-stu-id="23348-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="23348-137">Non esiste alcuna relazione ovvia tra questi numeri.</span><span class="sxs-lookup"><span data-stu-id="23348-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="23348-138">Infatti, dati il prezzo attuale del latte e la media battuta dalla Red Sox, non vi è alcun modo per risalire al contenuto di alcol nel sangue.</span><span class="sxs-lookup"><span data-stu-id="23348-138">If I gave you the current price of milk and the Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="23348-139">Osservando la tabella a destra</span><span class="sxs-lookup"><span data-stu-id="23348-139">Now look at the table on the right.</span></span> <span data-ttu-id="23348-140">si apprende invece che è stata misurata la massa corporea di ciascun individuo ed è stato contato il numero di bevande ingerite.</span><span class="sxs-lookup"><span data-stu-id="23348-140">This time we measured each person’s body mass and counted the number of drinks they’ve had.</span></span>  <span data-ttu-id="23348-141">I numeri presenti su ogni riga sono adesso rilevanti l'uno per l'altro.</span><span class="sxs-lookup"><span data-stu-id="23348-141">The numbers in each row are now relevant to each other.</span></span> <span data-ttu-id="23348-142">Data la massa corporea di un individuo e il numero di margarita bevuti, è possibile stimare la quantità di alcol presente nel sangue.</span><span class="sxs-lookup"><span data-stu-id="23348-142">If I gave you my body mass and the number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="23348-143">I dati a disposizione sono connessi?</span><span class="sxs-lookup"><span data-stu-id="23348-143">Do you have connected data?</span></span>
<span data-ttu-id="23348-144">L'ingrediente successivo è rappresentato dai dati connessi.</span><span class="sxs-lookup"><span data-stu-id="23348-144">The next ingredient is connected data.</span></span>

![Dati connessi vs. dati disconnessi: criteri dei dati, preparazione dei dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="23348-146">Ecco alcuni dati rilevanti sulla qualità degli hamburger: temperatura della griglia, peso della carne e classificazione nella rivista sul cibo locale.</span><span class="sxs-lookup"><span data-stu-id="23348-146">Here is some relevant data on the quality of hamburgers: grill temperature, patty weight, and rating in the local food magazine.</span></span> <span data-ttu-id="23348-147">Si presti però attenzione agli spazi vuoti nella tabella a sinistra.</span><span class="sxs-lookup"><span data-stu-id="23348-147">But notice the gaps in the table on the left.</span></span>

<span data-ttu-id="23348-148">Alcuni valori non sono presenti nella maggior parte dei set di dati.</span><span class="sxs-lookup"><span data-stu-id="23348-148">Most data sets are missing some values.</span></span> <span data-ttu-id="23348-149">Accade spesso di avere buchi del genere ed esistono delle soluzioni per colmarli.</span><span class="sxs-lookup"><span data-stu-id="23348-149">It's common to have holes like this and there are ways to work around them.</span></span> <span data-ttu-id="23348-150">Tuttavia, se mancano diversi valori, i dati iniziano a somigliare a un formaggio svizzero.</span><span class="sxs-lookup"><span data-stu-id="23348-150">But if there's too much missing, your data begins to look like Swiss cheese.</span></span>

<span data-ttu-id="23348-151">Dalla tabella a sinistra si evince che la quantità di dati mancanti è talmente elevata da poter difficilmente ipotizzare qualsiasi tipo di relazione tra la temperatura della griglia e il peso della carne.</span><span class="sxs-lookup"><span data-stu-id="23348-151">If you look at the table on the left, there's so much missing data, it's hard to come up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="23348-152">Questo è un esempio di dati disconnessi.</span><span class="sxs-lookup"><span data-stu-id="23348-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="23348-153">La tabella a destra, invece, è interamente completa e rappresenta un esempio di dati connessi.</span><span class="sxs-lookup"><span data-stu-id="23348-153">The table on the right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="23348-154">Sono accurati i dati?</span><span class="sxs-lookup"><span data-stu-id="23348-154">Is your data accurate?</span></span>
<span data-ttu-id="23348-155">L'ingrediente successivo necessario è l'accuratezza.</span><span class="sxs-lookup"><span data-stu-id="23348-155">The next ingredient we need is accuracy.</span></span> <span data-ttu-id="23348-156">Qui sono illustrati quattro bersagli da colpire con le frecce.</span><span class="sxs-lookup"><span data-stu-id="23348-156">Here are four targets that we’d like to hit with arrows.</span></span>

![Dati accurati vs. dati non accurati - criteri di dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="23348-158">Si osservi il bersaglio in alto a destra.</span><span class="sxs-lookup"><span data-stu-id="23348-158">Look at the target in the upper right.</span></span> <span data-ttu-id="23348-159">Attorno al punto centrale vi è un raggruppamento stretto.</span><span class="sxs-lookup"><span data-stu-id="23348-159">We’ve got a tight grouping right around the bullseye.</span></span> <span data-ttu-id="23348-160">Quello è naturalmente accurato.</span><span class="sxs-lookup"><span data-stu-id="23348-160">That, of course, is accurate.</span></span> <span data-ttu-id="23348-161">Stranamente, nel linguaggio di analisi scientifica dei dati, anche le prestazioni poco al di sotto del centro del bersaglio sono considerate accurate.</span><span class="sxs-lookup"><span data-stu-id="23348-161">Oddly, in the language of data science, our performance on the target right below it is also considered accurate.</span></span>

<span data-ttu-id="23348-162">Se si tratteggiasse il centro di queste frecce, si vedrebbe che è molto vicino al centro del bersaglio.</span><span class="sxs-lookup"><span data-stu-id="23348-162">If you were to map out the center of these arrows, you'd see that it's very close to the bullseye.</span></span> <span data-ttu-id="23348-163">Le frecce sono distribuite attorno al bersaglio, quindi considerate imprecise, ma sono centrate attorno al centro del bersaglio, quindi considerate accurate.</span><span class="sxs-lookup"><span data-stu-id="23348-163">The arrows are spread out all around the target, so they're considered imprecise, but they're centered around the bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="23348-164">Osservando adesso il bersaglio in alto a sinistra,</span><span class="sxs-lookup"><span data-stu-id="23348-164">Now look at the upper-left target.</span></span> <span data-ttu-id="23348-165">le frecce sono molto vicine l'una all'altra, si tratta di un raggruppamento stretto.</span><span class="sxs-lookup"><span data-stu-id="23348-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="23348-166">Sono precise, ma non accurate perché il centro è fuori dal centro del bersaglio.</span><span class="sxs-lookup"><span data-stu-id="23348-166">They're precise, but they're inaccurate because the center is way off the bullseye.</span></span> <span data-ttu-id="23348-167">E, naturalmente, le frecce nel bersaglio in fondo a sinistra sono sia inaccurate sia imprecise.</span><span class="sxs-lookup"><span data-stu-id="23348-167">And, of course, the arrows in the bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="23348-168">Questo arciere deve fare più pratica.</span><span class="sxs-lookup"><span data-stu-id="23348-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-to-work-with"></a><span data-ttu-id="23348-169">La quantità dei dati a disposizione con cui lavorare è sufficiente?</span><span class="sxs-lookup"><span data-stu-id="23348-169">Do you have enough data to work with?</span></span>
<span data-ttu-id="23348-170">Infine, l'ingrediente numero 4 è rappresentato da una quantità di dati sufficiente.</span><span class="sxs-lookup"><span data-stu-id="23348-170">Finally, ingredient #4 - we need to have enough data.</span></span>

![La quantità dei dati a disposizione è sufficiente per l'analisi?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="23348-173">Si immagini che ciascun punto di dati nella tabella sia una pennellata in un dipinto.</span><span class="sxs-lookup"><span data-stu-id="23348-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="23348-174">Se le pennellate sono poche, il dipinto può apparire abbastanza confuso ed è difficile stabilire quale sia il soggetto.</span><span class="sxs-lookup"><span data-stu-id="23348-174">If you have only a few of them, the painting can be pretty fuzzy - it's hard to tell what it is.</span></span>

<span data-ttu-id="23348-175">Se si danno altre pennellate, il dipinto inizia quindi a essere più nitido.</span><span class="sxs-lookup"><span data-stu-id="23348-175">If you add some more brush strokes, then your painting starts to get a little sharper.</span></span>

<span data-ttu-id="23348-176">Quando i tratti sono appena sufficienti, è possibile vedere quanto basta per prendere alcune decisioni approssimative.</span><span class="sxs-lookup"><span data-stu-id="23348-176">When you have barely enough strokes, you can see just enough to make some broad decisions.</span></span> <span data-ttu-id="23348-177">Si tratta di un posto che mi piacerebbe visitare?</span><span class="sxs-lookup"><span data-stu-id="23348-177">Is it somewhere I might want to visit?</span></span> <span data-ttu-id="23348-178">C'è molta luce, l'acqua sembra limpida: sì, è il posto in cui andrò in vacanza.</span><span class="sxs-lookup"><span data-stu-id="23348-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="23348-179">Aggiungendo sempre più dati, l'immagine diventa più chiara ed è possibile prendere decisioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="23348-179">As you add more data, the picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="23348-180">Adesso guardando i tre hotel sulla riva sinistra,</span><span class="sxs-lookup"><span data-stu-id="23348-180">Now I can look at the three hotels on the left bank.</span></span> <span data-ttu-id="23348-181">è possibile ammirare le straordinarie caratteristiche architettoniche di quello in primo piano.</span><span class="sxs-lookup"><span data-stu-id="23348-181">You know, I really like the architectural features of the one in the foreground.</span></span> <span data-ttu-id="23348-182">Deciso: terzo piano.</span><span class="sxs-lookup"><span data-stu-id="23348-182">I’ll stay there, on the third floor.</span></span>

<span data-ttu-id="23348-183">Dati rilevanti, connessi, accurati e in quantità sufficiente rappresentano tutti gli ingredienti necessari per effettuare alcune analisi scientifiche dei dati di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="23348-183">With data that's relevant, connected, accurate, and enough, we have all the ingredients we need to do some high-quality data science.</span></span>

<span data-ttu-id="23348-184">Anche gli altri quattro video della serie *Data Science for Beginners* (Analisi scientifica dei dati per principianti) di Microsoft Azure Machine Learning meritano di essere visti.</span><span class="sxs-lookup"><span data-stu-id="23348-184">Be sure to check out the other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23348-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="23348-185">Next steps</span></span>
* [<span data-ttu-id="23348-186">Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="23348-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="23348-187">Leggere l'Introduzione all'apprendimento automatico in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="23348-187">Get an introduction to Machine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
