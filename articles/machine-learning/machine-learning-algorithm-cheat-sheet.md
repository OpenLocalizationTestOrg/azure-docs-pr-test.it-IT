---
title: aaaMachine foglio informativo algoritmo di apprendimento | Documenti Microsoft
description: Una macchina stampabile foglio informativo algoritmo di apprendimento consente di scegliere l'algoritmo appropriato di hello per il modello predittivo in Azure Machine Learning Studio.
keywords: foglio informativo sugli algoritmi, foglio informatico, algoritmo di machine learning
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: e1dc31ec-1acb-463f-ba77-de565d4ddf4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: garye
ms.openlocfilehash: 2bedd77bfc65128a90c6128743016415dd8609d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-algorithm-cheat-sheet-for-microsoft-azure-machine-learning-studio"></a>Foglio informativo sugli algoritmi di Machine Learning per Microsoft Azure Machine Learning Studio
Hello **Microsoft Azure Machine Learning algoritmo irregolarità foglio** consente di scegliere l'algoritmo di destra hello per un modello predittivo analitica.

[Azure Machine Learning Studio](https://studio.azureml.net/) ha un'ampia libreria di algoritmi da hello ***regressione***, ***classificazione***, ***clustering***e ***il rilevamento di anomalie*** famiglie. Ognuno è progettato tooaddress un diverso tipo di problema di machine learning.

## <a name="download-machine-learning-algorithm-cheat-sheet"></a>Download: foglio informativo sugli algoritmi di Machine Learning
**Scaricare hello il foglio informativo qui: [Machine Learning algoritmo irregolarità foglio (11 x 17 in)](http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet-v6.pdf)**

![Foglio informativo di algoritmo di apprendimento macchina: informazioni su come toochoose un algoritmo di Machine Learning.][cheat-sheet]

[cheat-sheet]: ./media/machine-learning-algorithm-cheat-sheet/machine-learning-algorithm-cheat-sheet-small_v_0_6-01.png

Scaricare e stampare Ciao Machine Learning algoritmo irregolarità foglio tookeep dimensioni tabloid poterla e Guida scelta di un algoritmo.

> [!NOTE]
> Vedere l'articolo hello [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) per una Guida dettagliata di toousing questo foglio informativo.
> 
> 

## <a name="more-help-with-algorithms"></a>Altre informazioni sugli algoritmi
* Per informazioni sull'utilizzo di questo foglio informativo per la scelta di algoritmo appropriato hello e una discussione più approfondita di diversi tipi di hello di algoritmi di machine learning e modalità di utilizzo, vedere [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).
* Per ottenere una descrizione degli algoritmi e alcuni esempi, vedere [Infografica scaricabile: nozioni fondamentali di Machine Learning con esempi di algoritmi](machine-learning-basics-infographic-with-algorithm-examples.md).
* Per un elenco in base alla categoria tutti hello algoritmi di machine learning disponibili in Machine Learning Studio, vedere [inizializzare modello] [ initialize-model] hello algoritmo di Machine Learning Studio e modulo della Guida.
* Per un elenco alfabetico completo degli algoritmi e dei moduli disponibili in Machine Learning Studio, vedere l'argomento relativo all'[elenco alfabetico dei moduli di Machine Learning Studio][a-z-list] nella Guida degli algoritmi e dei moduli di Machine Learning Studio.
* toodownload e stampare un diagramma che offra una panoramica delle funzionalità di hello di Machine Learning Studio, vedere [diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="notes-and-terminology-definitions-for-hello-machine-learning-algorithm-cheat-sheet"></a>Note e le definizioni di terminologia per hello algoritmo di machine learning schede di riferimento rapido

* i suggerimenti di Hello disponibili in questo foglio informativo algoritmo sono le regole di thumb approssimativo. Alcuni possono essere modificati, altri totalmente ignorati. Si tratta di toosuggest previsto un punto di partenza. Non essere toorun termine della lezione una concorrenza combattimenti testa a testa tra diversi algoritmi sui dati. Non è semplicemente alcuna sostituzione per comprendere i principi di hello di ogni algoritmo e la comprensione di sistema hello che ha generato i dati.

* Ogni algoritmo di apprendimento automatico ha il proprio stile o *bias induttivo*. Per un problema specifico, possono essere appropriati diversi algoritmi, uno dei quali può rivelarsi una scelta più adatta rispetto agli altri. Ma non è sempre possibile tooknow in anticipo hello migliore adattamento. In questi casi diversi algoritmi sono elencati insieme nel foglio informativo hello. Una strategia appropriata sarebbe tootry un algoritmo e se hello risultati non sono ancora soddisfacenti, riprovare hello ad altri utenti. Di seguito è riportato un esempio di hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) di un esperimento che tenta di diversi algoritmi contro hello stessi dati e le confronta hello risultati: [Compare multi-class Classifiers: Letter recognition ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

* L'apprendimento automatico si divide in tre categorie principali: **apprendimento supervisionato**, **apprendimento non supervisionato** e **apprendimento per rinforzo**.

  * Nell'**apprendimento supervisionato** ogni punto dati è etichettato con o associato a una categoria o un valore di interesse.  Un esempio di un'etichetta di categoria è l'assegnazione di un'immagine come "gatto" o "cane".  Un esempio di un valore dell'etichetta è il prezzo di vendita hello associato a un'auto usata. obiettivo di apprendimento supervisionati Hello è toostudy molti etichettate esempi come queste e quindi toobe toomake in grado di stime sui punti dati futuri. Ad esempio, identificare nuove foto con hello corretto animale o l'assegnazione di tooother i prezzi di vendita accurate utilizzato automobili. Questo tipo di Machine Learning è utile e diffuso. Tutti i moduli di hello in Azure Machine Learning sotto la supervisione algoritmi, ad eccezione di apprendimento [Clustering K-Means][k-means-clustering].

  * Nell'**apprendimento non supervisionato** ai punti dati non sono associate etichette. Hello, invece, l'obiettivo di un algoritmo di apprendimento non supervisionato sono la struttura di dati hello tooorganize in alcune modalità o toodescribe. Questo può significare il raggruppamento dei dati in cluster, come fa K-Means, o l'individuazione di modi diversi in cui osservare dati complessi perché appaiano semplici.

  * In **learning amplificazione**, algoritmo hello Ottiene toochoose un'azione nel punto di dati di risposta tooeach. È un approccio comune in robotica, in cui set di lettura dei sensori in un determinato punto nel tempo hello è un punto dati e algoritmo hello necessario scegliere l'azione successiva del robot hello. Questo approccio è ideale anche per applicazioni "Internet delle cose" (Internet of Things, IoT). algoritmo di apprendimento Hello anche riceve un segnale di benefici è stato un breve periodo in un secondo momento, che indica la qualità delle decisioni hello. In base a questa, algoritmo hello modifica la propria strategia in benefici ottenuti dalla più alta di hello tooachieve ordine. Attualmente in Azure ML non sono disponibili moduli di algoritmi di apprendimento per rinforzo.

* **Metodi di Bayes** fare ipotesi hello di dati statisticamente indipendenti. Ciò significa che hello unmodeled variabilità in un punto dati è non correlato con altri utenti, vale a dire, non è possibile prevedere. Ad esempio, se i dati di hello registrati hello numero di minuti fino a quando non arriva train metropolitana Avanti hello, due misure smontate un giorno sono statisticamente indipendenti. Tuttavia, due misure smontate un minuto non sono statisticamente indipendenti: valore hello uno elevata predittiva del valore di hello di hello altri.

* La **regressione con alberi delle decisioni con boosting** sfrutta la sovrapposizione delle caratteristiche o l'interazione tra caratteristiche. Che significa che, in tutti i dati determinati punto, hello valore di una funzionalità viene in qualche modo predittiva del valore di hello di un altro. Ad esempio, nei dati di alta o bassa temperatura giornaliera, conoscere bassa temperatura hello per giorno hello consente toomake un ragionevole in hello elevata. informazioni di Hello in due funzionalità hello sono piuttosto ridondante.

* La classificazione di dati in più di due categorie può essere eseguita usando un classificatore essenzialmente multiclasse o combinando un set di classificatori a due classi in un **insieme**. Nell'approccio insieme hello, vi è un classificatore a due classi separato per ogni classe - ciascuno di essi hello i dati vengono separati in due categorie: "questa classe" e "non questa classe." Quindi questi classificatori votano corretta assegnazione di hello del punto dati hello. Si tratta di hello principio operativo dietro [One-vs-All Multiclass][one-vs-all-multiclass].

* Si supponga di diversi metodi, incluse la regressione logistica e i computer del punto di Bayes hello, **limiti di classe lineare**. Ovvero, si presuppone che hello limiti tra le classi sono circa linee rette (o hyperplanes nel caso più generale di hello). Spesso si tratta di una caratteristica dei dati hello che non si conosce fino a dopo che hai tentato tooseparate, ma si è un elemento che in genere possono essere appresi da visualizzare in anticipo. Se i limiti di classe hello aspetto molto irregolari, utilizzare gli alberi delle decisioni, giungle delle decisioni, supportano le macchine a vettori, o reti neurali.

* Reti neurali sono utilizzabile con variabili di categoria creando un **variabile fittizia** per ogni categoria, impostarlo too1 nei casi in cui si applica la categoria hello, in caso contrario 0.


<!-- This is how you can embed a link in an image in HTML. Don't know how toodo this in markdown.
<a href="http://download.microsoft.com/download/A/6/1/A613E11E-8F9C-424A-B99D-65344785C288/microsoft-machine-learning-algorithm-cheat-sheet.pdf">
<img src="C:\Users\garye\azure-docs-pr\articles\media\machine-learning-algorithm-cheat-sheet\cheat-sheet-small.png">
</a>
-->

<!-- Module References -->
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx
[initialize-model]: https://msdn.microsoft.com/library/azure/0c67013c-bfbc-428b-87f3-f552d8dd41f6/
[k-means-clustering]: https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/
[one-vs-all-multiclass]: https://msdn.microsoft.com/library/azure/7191efae-b4b1-4d03-a6f8-7205f87be664/
