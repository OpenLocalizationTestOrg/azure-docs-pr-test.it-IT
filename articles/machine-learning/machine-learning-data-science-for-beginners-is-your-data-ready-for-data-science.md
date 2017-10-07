---
title: aaaIs dati pronti per l'analisi scientifica dei dati? Valutazione dei dati con Azure Machine Learning | Microsoft Docs
description: Informazioni su criteri hello 4 per dati toobe pronto per l'analisi scientifica dei dati. Analisi scientifica dei dati per i principianti video 2 include esempi concreti toohelp con la valutazione dei dati di base.
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
ms.openlocfilehash: ef6bb680ace771537157dbdd50a4ccce0a3eb7ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="is-your-data-ready-for-data-science"></a><span data-ttu-id="906c8-106">Sono pronti i dati per l'analisi scientifica?</span><span class="sxs-lookup"><span data-stu-id="906c8-106">Is your data ready for data science?</span></span>
## <a name="video-2-data-science-for-beginners-series"></a><span data-ttu-id="906c8-107">Video 2: Analisi scientifica dei dati per principianti</span><span class="sxs-lookup"><span data-stu-id="906c8-107">Video 2: Data Science for Beginners series</span></span>
<span data-ttu-id="906c8-108">Informazioni su come tooevaluate toomake i dati che vengano soddisfatti i criteri di base toobe pronto per l'analisi scientifica dei dati.</span><span class="sxs-lookup"><span data-stu-id="906c8-108">Learn how tooevaluate your data toomake sure it meets basic criteria toobe ready for data science.</span></span>

<span data-ttu-id="906c8-109">hello tooget meglio serie hello, guardare tutti.</span><span class="sxs-lookup"><span data-stu-id="906c8-109">tooget hello most out of hello series, watch them all.</span></span> <span data-ttu-id="906c8-110">[Passare l'elenco toohello di video](#other-videos-in-this-series)
</span><span class="sxs-lookup"><span data-stu-id="906c8-110">[Go toohello list of videos](#other-videos-in-this-series)
</span></span><br>

> [!VIDEO https://channel9.msdn.com/Shows/SupervisionNotRequired/9/player]
>
>

## <a name="other-videos-in-this-series"></a><span data-ttu-id="906c8-111">Altri video della serie</span><span class="sxs-lookup"><span data-stu-id="906c8-111">Other videos in this series</span></span>
<span data-ttu-id="906c8-112">*Analisi scientifica dei dati per i principianti* scienza di toodata una rapida introduzione in cinque brevi video.</span><span class="sxs-lookup"><span data-stu-id="906c8-112">*Data Science for Beginners* is a quick introduction toodata science in five short videos.</span></span>

* <span data-ttu-id="906c8-113">Video 1: [hello 5 domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span><span class="sxs-lookup"><span data-stu-id="906c8-113">Video 1: [hello 5 questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) *(5 min 14 sec)*</span></span>
* <span data-ttu-id="906c8-114">Video 2: Verifica della preparazione dei dati per l'analisi scientifica dei dati</span><span class="sxs-lookup"><span data-stu-id="906c8-114">Video 2: Is your data ready for data science?</span></span>
* <span data-ttu-id="906c8-115">Video 3: [Porre una domanda a cui è possibile rispondere con i dati](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min e 17 sec)*</span><span class="sxs-lookup"><span data-stu-id="906c8-115">Video 3: [Ask a question you can answer with data](machine-learning-data-science-for-beginners-ask-a-question-you-can-answer-with-data.md) *(4 min 17 sec)*</span></span>
* <span data-ttu-id="906c8-116">Video 4: [Prevedere una risposta con un modello semplice](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min e 42 sec)*</span><span class="sxs-lookup"><span data-stu-id="906c8-116">Video 4: [Predict an answer with a simple model](machine-learning-data-science-for-beginners-predict-an-answer-with-a-simple-model.md) *(7 min 42 sec)*</span></span>
* <span data-ttu-id="906c8-117">Video 5: [copiare analisi scientifica dei dati di altre persone lavoro toodo](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span><span class="sxs-lookup"><span data-stu-id="906c8-117">Video 5: [Copy other people's work toodo data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) *(3 min 18 sec)*</span></span>

## <a name="transcript-is-your-data-ready-for-data-science"></a><span data-ttu-id="906c8-118">Trascrizione: Sono pronti i dati per l'analisi scientifica?</span><span class="sxs-lookup"><span data-stu-id="906c8-118">Transcript: Is your data ready for data science?</span></span>
<span data-ttu-id="906c8-119">Benvenuto troppo "è dati pronto per l'analisi scientifica dei dati?"</span><span class="sxs-lookup"><span data-stu-id="906c8-119">Welcome too"Is your data ready for data science?"</span></span> <span data-ttu-id="906c8-120">Hello secondo video in serie hello *analisi scientifica dei dati per i principianti*.</span><span class="sxs-lookup"><span data-stu-id="906c8-120">hello second video in hello series *Data Science for Beginners*.</span></span>  

<span data-ttu-id="906c8-121">Prima di analisi scientifica dei dati è possibile assegnare si hello risposte desiderate, è necessario toogive alcuni toowork materie di alta qualità con.</span><span class="sxs-lookup"><span data-stu-id="906c8-121">Before data science can give you hello answers you want, you have toogive it some high-quality raw materials toowork with.</span></span> <span data-ttu-id="906c8-122">Esecuzione di una pizza, hello migliori hello gli ingredienti si avvia, hello meglio prodotto finale hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-122">Just like making a pizza, hello better hello ingredients you start with, hello better hello final product.</span></span> 

## <a name="criteria-for-data"></a><span data-ttu-id="906c8-123">Criteri per i dati</span><span class="sxs-lookup"><span data-stu-id="906c8-123">Criteria for data</span></span>
<span data-ttu-id="906c8-124">In tal caso, nel caso di hello di analisi scientifica dei dati, esistono alcuni ingredienti che è necessario toopull.</span><span class="sxs-lookup"><span data-stu-id="906c8-124">So, in hello case of data science, there are some ingredients that we need toopull together.</span></span>

<span data-ttu-id="906c8-125">Sono fondamentali dati:</span><span class="sxs-lookup"><span data-stu-id="906c8-125">We need data that is:</span></span>

* <span data-ttu-id="906c8-126">Rilevanti</span><span class="sxs-lookup"><span data-stu-id="906c8-126">Relevant</span></span>
* <span data-ttu-id="906c8-127">Connesso</span><span class="sxs-lookup"><span data-stu-id="906c8-127">Connected</span></span>
* <span data-ttu-id="906c8-128">Accurati</span><span class="sxs-lookup"><span data-stu-id="906c8-128">Accurate</span></span>
* <span data-ttu-id="906c8-129">Sufficiente toowork con</span><span class="sxs-lookup"><span data-stu-id="906c8-129">Enough toowork with</span></span>

## <a name="is-your-data-relevant"></a><span data-ttu-id="906c8-130">Sono rilevanti i dati?</span><span class="sxs-lookup"><span data-stu-id="906c8-130">Is your data relevant?</span></span>
<span data-ttu-id="906c8-131">In modo principio prima hello - è necessario che i dati rilevanti.</span><span class="sxs-lookup"><span data-stu-id="906c8-131">So hello first ingredient - we need data that's relevant.</span></span>

![Dati rilevanti vs. dati irrilevanti, valutare i dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/relevant-and-irrelevant-data.png)

<span data-ttu-id="906c8-133">Esaminare la tabella hello a sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-133">Look at hello table on hello left.</span></span> <span data-ttu-id="906c8-134">Viene soddisfatta sette persone all'esterno delle barre di Boston, misurato loro livello alcole sangue, hello Red Sox battuta Media di un gioco ultima e il prezzo di hello di latte in hello più vicino al punto vendita.</span><span class="sxs-lookup"><span data-stu-id="906c8-134">We met seven people outside of Boston bars, measured their blood alcohol level, hello Red Sox batting average in their last game, and hello price of milk in hello nearest convenience store.</span></span>

<span data-ttu-id="906c8-135">Si tratta di dati del tutto legittimi.</span><span class="sxs-lookup"><span data-stu-id="906c8-135">This is all perfectly legitimate data.</span></span> <span data-ttu-id="906c8-136">L'unico inconveniente è che non sono rilevanti.</span><span class="sxs-lookup"><span data-stu-id="906c8-136">It’s only fault is that it isn’t relevant.</span></span> <span data-ttu-id="906c8-137">Non esiste alcuna relazione ovvia tra questi numeri.</span><span class="sxs-lookup"><span data-stu-id="906c8-137">There's no obvious relationship between these numbers.</span></span> <span data-ttu-id="906c8-138">Se è stato assegnato hello prezzo corrente di latte e hello media battuta Red Sox, non è possibile si può immaginare contenuto alcole sangue.</span><span class="sxs-lookup"><span data-stu-id="906c8-138">If I gave you hello current price of milk and hello Red Sox batting average, there's no way you could guess my blood alcohol content.</span></span>

<span data-ttu-id="906c8-139">Esaminare ora tabella hello a destra hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-139">Now look at hello table on hello right.</span></span> <span data-ttu-id="906c8-140">Questo tempo è misurato corpo hello di massa e conteggiato svariate ogni persona avute bibite.</span><span class="sxs-lookup"><span data-stu-id="906c8-140">This time we measured each person’s body mass and counted hello number of drinks they’ve had.</span></span>  <span data-ttu-id="906c8-141">numeri di Hello in ogni riga sono ora rilevanti tooeach altri.</span><span class="sxs-lookup"><span data-stu-id="906c8-141">hello numbers in each row are now relevant tooeach other.</span></span> <span data-ttu-id="906c8-142">Se ha fornito il numero di massa e hello corpo di limetta fresca ho, è possibile apportare una probabilità my sangue alcole contenuto.</span><span class="sxs-lookup"><span data-stu-id="906c8-142">If I gave you my body mass and hello number of Margaritas I've had, you could make a guess at my blood alcohol content.</span></span>

## <a name="do-you-have-connected-data"></a><span data-ttu-id="906c8-143">I dati a disposizione sono connessi?</span><span class="sxs-lookup"><span data-stu-id="906c8-143">Do you have connected data?</span></span>
<span data-ttu-id="906c8-144">principio Avanti Hello è dati connessa.</span><span class="sxs-lookup"><span data-stu-id="906c8-144">hello next ingredient is connected data.</span></span>

![Dati connessi vs. dati disconnessi: criteri dei dati, preparazione dei dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/connected-vs-disconnected-data.png)

<span data-ttu-id="906c8-146">Ecco alcuni dati pertinenti qualità hello di hamburger: griglia temperatura peso ad e classificazione di cibo locale hello rivista.</span><span class="sxs-lookup"><span data-stu-id="906c8-146">Here is some relevant data on hello quality of hamburgers: grill temperature, patty weight, and rating in hello local food magazine.</span></span> <span data-ttu-id="906c8-147">Ma si noti il gap di hello nella tabella hello hello sinistra.</span><span class="sxs-lookup"><span data-stu-id="906c8-147">But notice hello gaps in hello table on hello left.</span></span>

<span data-ttu-id="906c8-148">Alcuni valori non sono presenti nella maggior parte dei set di dati.</span><span class="sxs-lookup"><span data-stu-id="906c8-148">Most data sets are missing some values.</span></span> <span data-ttu-id="906c8-149">È comune fori toohave simile al seguente e sono disponibili modi toowork attorno a esse.</span><span class="sxs-lookup"><span data-stu-id="906c8-149">It's common toohave holes like this and there are ways toowork around them.</span></span> <span data-ttu-id="906c8-150">Ma se è presente una quantità eccessiva mancante, i dati iniziano toolook come cheese Svizzera.</span><span class="sxs-lookup"><span data-stu-id="906c8-150">But if there's too much missing, your data begins toolook like Swiss cheese.</span></span>

<span data-ttu-id="906c8-151">Se si esamina la tabella hello a sinistra di hello, è pertanto quantità di dati mancanti, è toocome rigido backup con qualsiasi tipo di relazione tra griglia peso temperatura e ad.</span><span class="sxs-lookup"><span data-stu-id="906c8-151">If you look at hello table on hello left, there's so much missing data, it's hard toocome up with any kind of relationship between grill temperature and patty weight.</span></span> <span data-ttu-id="906c8-152">Questo è un esempio di dati disconnessi.</span><span class="sxs-lookup"><span data-stu-id="906c8-152">This is an example of disconnected data.</span></span>

<span data-ttu-id="906c8-153">Hello tabella a destra hello, tuttavia, è completo e un esempio di dati connessi - completo.</span><span class="sxs-lookup"><span data-stu-id="906c8-153">hello table on hello right, though, is full and complete - an example of connected data.</span></span>

## <a name="is-your-data-accurate"></a><span data-ttu-id="906c8-154">Sono accurati i dati?</span><span class="sxs-lookup"><span data-stu-id="906c8-154">Is your data accurate?</span></span>
<span data-ttu-id="906c8-155">Hello principio avanti che dobbiamo è la precisione.</span><span class="sxs-lookup"><span data-stu-id="906c8-155">hello next ingredient we need is accuracy.</span></span> <span data-ttu-id="906c8-156">Ecco quattro destinazioni che si desidera toohit con frecce.</span><span class="sxs-lookup"><span data-stu-id="906c8-156">Here are four targets that we’d like toohit with arrows.</span></span>

![Dati accurati vs. dati non accurati - criteri di dati](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/inaccurate-vs-accurate-data.png)

<span data-ttu-id="906c8-158">Esaminare la destinazione hello in alto a destra hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-158">Look at hello target in hello upper right.</span></span> <span data-ttu-id="906c8-159">Abbiamo un raggruppamento di una stretta attorno a bullseye hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-159">We’ve got a tight grouping right around hello bullseye.</span></span> <span data-ttu-id="906c8-160">Quello è naturalmente accurato.</span><span class="sxs-lookup"><span data-stu-id="906c8-160">That, of course, is accurate.</span></span> <span data-ttu-id="906c8-161">In modo anomalo, nella lingua hello dell'analisi scientifica dei dati, le prestazioni a destra di destinazione hello sottostanti vengano inoltre considerate accurate.</span><span class="sxs-lookup"><span data-stu-id="906c8-161">Oddly, in hello language of data science, our performance on hello target right below it is also considered accurate.</span></span>

<span data-ttu-id="906c8-162">Se toomap centro hello di queste frecce, si vedrà che è molto simile toohello bullseye.</span><span class="sxs-lookup"><span data-stu-id="906c8-162">If you were toomap out hello center of these arrows, you'd see that it's very close toohello bullseye.</span></span> <span data-ttu-id="906c8-163">frecce Hello si diffondono tutte intorno destinazione hello, in modo che si sono considerate non precise, ma è incentrate sul bullseye hello, in modo che si sono considerati accurati.</span><span class="sxs-lookup"><span data-stu-id="906c8-163">hello arrows are spread out all around hello target, so they're considered imprecise, but they're centered around hello bullseye, so they're considered accurate.</span></span>

<span data-ttu-id="906c8-164">Esaminare ora destinazione alto-sinistra hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-164">Now look at hello upper-left target.</span></span> <span data-ttu-id="906c8-165">le frecce sono molto vicine l'una all'altra, si tratta di un raggruppamento stretto.</span><span class="sxs-lookup"><span data-stu-id="906c8-165">Here our arrows hit very close together, a tight grouping.</span></span> <span data-ttu-id="906c8-166">Ma sono precisi, ma sono corrette perché center hello è fuori bullseye hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-166">They're precise, but they're inaccurate because hello center is way off hello bullseye.</span></span> <span data-ttu-id="906c8-167">E, naturalmente, frecce hello nella destinazione nella parte inferiore sinistra hello sono corrette e imprecisa.</span><span class="sxs-lookup"><span data-stu-id="906c8-167">And, of course, hello arrows in hello bottom-left target are both inaccurate and imprecise.</span></span> <span data-ttu-id="906c8-168">Questo arciere deve fare più pratica.</span><span class="sxs-lookup"><span data-stu-id="906c8-168">This archer needs more practice.</span></span>

## <a name="do-you-have-enough-data-toowork-with"></a><span data-ttu-id="906c8-169">È sufficiente toowork dati con</span><span class="sxs-lookup"><span data-stu-id="906c8-169">Do you have enough data toowork with?</span></span>
<span data-ttu-id="906c8-170">Infine, principio #4 - dobbiamo toohave dati sufficienti.</span><span class="sxs-lookup"><span data-stu-id="906c8-170">Finally, ingredient #4 - we need toohave enough data.</span></span>

![La quantità dei dati a disposizione è sufficiente per l'analisi?](./media/machine-learning-data-science-for-beginners-is-your-data-ready-for-data-science/barely-enough-data.png)

<span data-ttu-id="906c8-173">Si immagini che ciascun punto di dati nella tabella sia una pennellata in un dipinto.</span><span class="sxs-lookup"><span data-stu-id="906c8-173">Think of each data point in your table as being a brush stroke in a painting.</span></span> <span data-ttu-id="906c8-174">Se è installato solo alcuni di essi, disegno hello può essere piuttosto fuzzy - tootell disco rigido è ciò che è.</span><span class="sxs-lookup"><span data-stu-id="906c8-174">If you have only a few of them, hello painting can be pretty fuzzy - it's hard tootell what it is.</span></span>

<span data-ttu-id="906c8-175">Se si aggiungono alcuni altri tratti pennello, il disegno avvia tooget un più nitida minimo.</span><span class="sxs-lookup"><span data-stu-id="906c8-175">If you add some more brush strokes, then your painting starts tooget a little sharper.</span></span>

<span data-ttu-id="906c8-176">Quando si dispone di poco sufficiente tracce, è possibile visualizzare solo sufficiente toomake alcune decisioni ampie.</span><span class="sxs-lookup"><span data-stu-id="906c8-176">When you have barely enough strokes, you can see just enough toomake some broad decisions.</span></span> <span data-ttu-id="906c8-177">Si tratta di una posizione di che cui si desidera conoscere toovisit?</span><span class="sxs-lookup"><span data-stu-id="906c8-177">Is it somewhere I might want toovisit?</span></span> <span data-ttu-id="906c8-178">C'è molta luce, l'acqua sembra limpida: sì, è il posto in cui andrò in vacanza.</span><span class="sxs-lookup"><span data-stu-id="906c8-178">It looks bright, that looks like clean water – yes, that’s where I’m going on vacation.</span></span>

<span data-ttu-id="906c8-179">Quando si aggiungono più dati, immagine hello diventa più chiara e per prendere decisioni più dettagliate.</span><span class="sxs-lookup"><span data-stu-id="906c8-179">As you add more data, hello picture becomes clearer and you can make more detailed decisions.</span></span> <span data-ttu-id="906c8-180">Ora esaminare hello tre hotel banca sinistro hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-180">Now I can look at hello three hotels on hello left bank.</span></span> <span data-ttu-id="906c8-181">Si conosce, mi piace davvero caratteristiche correlate all'architettura di hello di hello in primo piano hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-181">You know, I really like hello architectural features of hello one in hello foreground.</span></span> <span data-ttu-id="906c8-182">Disponibile, rimangano piano terzo hello.</span><span class="sxs-lookup"><span data-stu-id="906c8-182">I’ll stay there, on hello third floor.</span></span>

<span data-ttu-id="906c8-183">Con i dati rilevanti, connesso, precisione, e sufficienti, si dispone di tutti gli ingredienti hello dobbiamo toodo alcune analisi scientifica dei dati di alta qualità.</span><span class="sxs-lookup"><span data-stu-id="906c8-183">With data that's relevant, connected, accurate, and enough, we have all hello ingredients we need toodo some high-quality data science.</span></span>

<span data-ttu-id="906c8-184">Essere certi toocheck out hello altri video di quattro *analisi scientifica dei dati per i principianti* da Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="906c8-184">Be sure toocheck out hello other four videos in *Data Science for Beginners* from Microsoft Azure Machine Learning.</span></span>

## <a name="next-steps"></a><span data-ttu-id="906c8-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="906c8-185">Next steps</span></span>
* [<span data-ttu-id="906c8-186">Effettuare il primo esperimento di analisi scientifica dei dati con Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="906c8-186">Try a first data science experiment with Machine Learning Studio</span></span>](machine-learning-create-experiment.md)
* [<span data-ttu-id="906c8-187">Ottenere un tooMachine introduzione di apprendimento in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="906c8-187">Get an introduction tooMachine Learning on Microsoft Azure</span></span>](machine-learning-what-is-machine-learning.md)
