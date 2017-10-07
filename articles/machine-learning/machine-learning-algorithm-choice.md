---
title: aaaHow toochoose algoritmi di machine learning | Documenti Microsoft
description: Come toochoose Azure Machine Learning algoritmi per l'apprendimento con e senza supervisione relative al clustering di classificazione o regressione esperimenti.
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a3b23d7f-f083-49c4-b6b1-3911cd69f1b4
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/25/2017
ms.author: garye
ms.openlocfilehash: 367b2278acc2435f27f9d24ead8199db58aca283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-algorithms-for-microsoft-azure-machine-learning"></a>Come algoritmi toochoose per Microsoft Azure Machine Learning
Hello domanda toohello "quali computer algoritmo di apprendimento deve usare?" è sempre "Dipende". Dipende dimensioni hello, la qualità e natura dei dati di hello. Dipende si desidera toodo con risposte hello. Dipende dalla modalità di conversione di matematica hello dell'algoritmo hello in istruzioni per il computer di hello in uso. E dipende dal tempo a disposizione. Anche gli esperti di dati si è verificato più hello è possono stabilire quale algoritmo eseguirà migliore prima di eseguirli.

## <a name="hello-machine-learning-algorithm-cheat-sheet"></a>Machine Learning algoritmo irregolarità foglio Hello
Hello **Microsoft Azure Machine Learning algoritmo irregolarità foglio** consente di scegliere destra hello algoritmo di apprendimento per le soluzioni analitica predittiva dalla libreria di Microsoft Azure Machine Learning hello degli algoritmi di machine.
In questo articolo viene descritta la procedura toouse è.

> [!NOTE]
> foglio informativo di toodownload hello e seguirlo con questo articolo, andare troppo[computer foglio informativo algoritmo di apprendimento per Microsoft Azure Machine Learning Studio](machine-learning-algorithm-cheat-sheet.md).
> 
> 

Questo foglio informativo dispone di un gruppo di destinatari molto specifico in considerazione: un esperto di dati iniziale con livello di età universitaria machine learning, durante il tentativo toochoose toostart un algoritmo con in Azure Machine Learning Studio. Ciò significa che fa alcune generalizzazioni e semplificazioni eccessive, ma indicherà una direzione sicura. Significa inoltre che esistono molti algoritmi non elencati qui. Quando Azure Machine Learning aumenta tooencompass un set più completo dei metodi disponibili, essi verrà aggiunto.

Queste indicazioni sono commenti e suggerimenti compilati da parte di scienziati dei dati ed esperti di Machine Learning. È non concordano tutti gli elementi, ma si è tentato tooharmonize nostri opinioni in consenso approssimativo. La maggior parte delle istruzioni hello di disaccordo iniziano con "a seconda dei casi..."

### <a name="how-toouse-hello-cheat-sheet"></a>Come toouse hello schede di riferimento rapido
Leggere le etichette di percorso e l'algoritmo hello grafico hello come "per  *&lt;etichetta percorso&gt;*, utilizzare  *&lt;algoritmo&gt;*." Ad esempio, "Per *velocità* usare *regressione logistica a due classi*". A volte è possibile applicare più di una branca.
A volte nessuno di essi sarà la scelta perfetta. Sono previsti toobe di regola indicazioni, pertanto non è importante che sia esatto.
È parlato con più esperti di dati ha dichiarato tale che solo modo trovare l'algoritmo migliore hello è tootry hello tutti gli elementi.

Di seguito è riportato un esempio di hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) di un esperimento che tenta di diversi algoritmi contro hello stessi dati e le confronta hello risultati: [Compare multi-class Classifiers: Letter recognition ](http://gallery.cortanaintelligence.com/Details/a635502fc98b402a890efe21cec65b92).

> [!TIP]
> toodownload e stampare un diagramma che offra una panoramica delle funzionalità di hello di Machine Learning Studio, vedere [diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).
> 
> 

## <a name="flavors-of-machine-learning"></a>Varianti di Machine Learning
### <a name="supervised"></a>Supervisionato
Gli algoritmi di apprendimento supervisionato fanno previsioni in base a un set di esempi. Ad esempio, quotazioni cronologici possono essere utilizzato toohazard ipotesi prezzi future. Ogni esempio viene utilizzato per il training è etichettata con valore hello di interesse, in questo caso hello prezzo azionario. Un algoritmo di apprendimento supervisionato cerca modelli ripetitivi nelle etichette dei valori. È possibile utilizzare tutte le informazioni potrebbero essere rilevanti, ovvero giorno hello della settimana hello, stagione hello, dati finanziari dell'azienda hello, tipo di hello del settore, presenza hello di arresto improvviso eventi geopolitici, e ogni algoritmo esegue la ricerca di tipi diversi di modelli. Dopo l'algoritmo hello ha individuato ottimale hello possibile, viene utilizzata che stime toomake modello per senza etichetta dati di test, i prezzi di domani.

L'apprendimento supervisionato è un tipo di Machine Learning è utile e diffuso. Con un'unica eccezione, tutti i moduli di hello in Azure Machine Learning sotto la supervisione algoritmi di apprendimento. Sono presenti diversi tipi specifici di apprendimento supervisionato rappresentati all'interno di Azure Machine Learning: classificazione, regressione e rilevamento di anomalie.

* **Classificazione**. Quando i dati hello vengono utilizzati toopredict una categoria, apprendimento supervisionato è l'acronimo di classificazione. Questo è il caso di hello quando si assegna un'immagine come immagine di 'gatto' o a 'dog". Quando sono disponibili solo due opzioni, è chiamato **a due classi** o **classificazione binomiale**. Quando sono presenti più categorie, come per la stima di riga confermata hello tournament basket NCAA hello, questo problema è noto come **classificazione multiclasse**.
* **Regressione**. Quando un valore viene previsto, come con i prezzi dei titoli, l’apprendimento supervisionato viene chiamato regressione.
* **Rilevamento delle anomalie**. A volte hello obiettivo è tooidentify i punti dati che sono semplicemente insoliti. Nel rilevamento delle frodi, ad esempio, i modelli di spesa della carta di credito altamente insoliti sono sospetti. le possibili varianti Hello sono numerosi e hello esempi di training pertanto alcuni, che è non fattibile toolearn quali attività illecite è simile. L'approccio che accetta il rilevamento di anomalie è toosimply apprendere le attività normali simile (utilizzando delle transazioni non fraudolenti cronologia) e identificare tutto ciò che è molto diverso.

### <a name="unsupervised"></a>Non supervisionato
Nell'apprendimento non supervisionato, ai punti dati non sono associate etichette. Al contrario, obiettivo hello di un non supervisionato apprendimento algoritmo consiste nell'organizzare i dati di hello in alcune o di toodescribe relativa struttura. Questo può significare il raggruppamento dei dati in cluster o l'individuazione di modi diversi con cui osservare dati complessi, in modo che appaiano più semplici o più organizzati.

### <a name="reinforcement-learning"></a>Apprendimento per rinforzo
Scoprire amplificazione, algoritmo hello Ottiene toochoose un'azione nel punto di dati di risposta tooeach. algoritmo di apprendimento Hello anche riceve un segnale di benefici è stato un breve periodo in un secondo momento, che indica la qualità delle decisioni hello.
In base a questa, algoritmo hello modifica la propria strategia in benefici ottenuti dalla più alta di hello tooachieve ordine. Attualmente in Azure Machine Learning non sono disponibili moduli di algoritmi di apprendimento per rinforzo. Apprendimento amplificazione è comune in robotica, in cui set di lettura dei sensori in un determinato punto nel tempo hello è un punto dati e algoritmo hello necessario scegliere l'azione successiva del robot hello. Questo approccio è ideale anche per applicazioni "Internet delle cose" (Internet of Things, IoT).

## <a name="considerations-when-choosing-an-algorithm"></a>Considerazioni relative alla scelta di un algoritmo
### <a name="accuracy"></a>Precisione
Ottenere risposte più accurate hello possibili non è sempre necessario.
Talvolta un'approssimazione è sufficiente, a seconda di ciò per cui si desidera utilizzarla. Se è questo caso di hello, potrebbe essere in grado di toocut il tempo di elaborazione in modo significativo da trovarsi bene con altri metodi approssimativi. Un altro vantaggio di metodi più approssimativi è la tendenza naturale a evitare il [sovradattamento](https://youtu.be/DQWI1kvmwRg).

### <a name="training-time"></a>Tempo di formazione
numero di minuti o ore tootrain necessario che un modello varia notevolmente tra gli algoritmi di Hello. I tempi di training sono spesso strettamente legato all'accuratezza, uno in genere accompagna hello altri. Inoltre, alcuni algoritmi sono più sensibili toohello numerosi punti dati rispetto ad altri.
Quando il tempo è limitato può risultare utile scelta hello dell'algoritmo, soprattutto quando il set di dati di hello è elevato.

### <a name="linearity"></a>Linearità
Un numero elevato di algoritmi di Machine Learning utilizza la linearità. Gli algoritmi di classificazione lineare ipotizzano che le classi possano essere separate da una linea retta (o dal suo equivalente della dimensione superiore). Queste includono la regressione logistica e le macchine a vettori di supporto (come implementate in Azure Machine Learning).
Gli algoritmi di regressione lineare ipotizzano che le tendenze dei dati seguano una linea retta. Queste ipotesi non sono errate per alcuni problemi, ma per altri riducono la precisione.

![Limite di classe non lineare][1]

***Limite di classe non lineare****: basarsi su un algoritmo di classificazione lineare produce una precisione ridotta*

![Dati con una tendenza non lineare][2]

***Dati con una tendenza non lineare*** *: l'uso di un metodo di regressione lineare genera errori più grandi del necessario*

Nonostante i loro pericoli, gli algoritmi lineari sono molto popolari come prima linea di attacco. Sono in genere toobe modo algoritmico semplice e veloce per eseguire il training.

### <a name="number-of-parameters"></a>Numero di parametri
I parametri sono manopole hello un esperto di dati ottiene tooturn quando si configura un algoritmo. Sono numeri che influiscono sul comportamento dell'algoritmo di hello, ad esempio la tolleranza di errore o un numero di iterazioni o opzioni tra le varianti del comportamento di algoritmo hello. tempi di training Hello e sull'accuratezza dell'algoritmo hello può talvolta risultare impostazioni corrette di hello solo toogetting molto sensibili. In genere, gli algoritmi con i parametri di un numero elevato richiedono hello più versione di valutazione e errore toofind una combinazione valida.

In alternativa, in Azure Machine Learning è disponibile un blocco di moduli per lo [sweep dei parametri](machine-learning-algorithm-parameters-optimize.md) che prova automaticamente tutte le combinazioni di parametri alla granularità scelta. Mentre questo è un ottimo modo toomake che è stato eseguito lo spanning spazio parametro hello, hello tempi tootrain un modello aumenta in modo esponenziale con numero di hello di parametri.

Hello rivolta è che con un numero di parametri in genere indica che un algoritmo ha una maggiore flessibilità. Può raggiungere spesso un’alta precisione. Fornito che è possibile trovare giusta combinazione di hello impostazioni dei parametri.

### <a name="number-of-features"></a>Numero di caratteristiche
Per determinati tipi di dati, il numero di hello di funzionalità può essere toohello confrontati molto grande numero di punti dati. Questo accade spesso hello con genetics o dati di testo. Alcuni algoritmi di apprendimento, rendendo training ora unfeasibly lungo possibile costringe a Hello numerose funzionalità. Macchine a vettori di supporto sono particolarmente adatta toothis case (vedere sotto).

### <a name="special-cases"></a>Casi speciali
Alcuni algoritmi di apprendimento è determinato supposizioni sulla struttura hello di hello dati o i risultati di hello desiderato. Se è possibile trovarne uno adatto alle proprie esigenze, può fornire risultati più utili, previsioni più accurate o tempi di addestramento più rapidi.

| **Algoritmo** | **Precisione** | **Tempo di addestramento** | **Linearità** | **Parametri** | **Note** |
| --- |:---:|:---:|:---:|:---:| --- |
| **Classificazione a due classi** | | | | | |
| [regressione logistica](https://msdn.microsoft.com/library/azure/dn905994.aspx) | |● |● |5 | |
| [foresta delle decisioni](https://msdn.microsoft.com/library/azure/dn906008.aspx) |● |○ | |6 | |
| [giungla delle decisioni](https://msdn.microsoft.com/library/azure/dn905976.aspx) |● |○ | |6 |Footprint della memoria ridotto |
| [albero delle decisioni con boosting scalabile](https://msdn.microsoft.com/library/azure/dn906025.aspx) |● |○ | |6 |Footprint della memoria di grandi dimensioni |
| [rete neurale](https://msdn.microsoft.com/library/azure/dn905947.aspx) |● | | |9 |[È possibile un’ulteriore personalizzazione](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [percezione media](https://msdn.microsoft.com/library/azure/dn906036.aspx) |○ |○ |● |4 | |
| [macchina a vettori di supporto](https://msdn.microsoft.com/library/azure/dn905835.aspx) | |○ |● |5 |Particolarmente valido per set di funzioni di grandi dimensioni |
| [macchina a vettori di supporto localmente approfondito](https://msdn.microsoft.com/library/azure/dn913070.aspx) |○ | | |8 |Particolarmente valido per set di funzioni di grandi dimensioni |
| [Bayes Point Machine](https://msdn.microsoft.com/library/azure/dn905930.aspx) | |○ |● |3 | |
| **Classificazione multiclasse** | | | | | |
| [regressione logistica](https://msdn.microsoft.com/library/azure/dn905853.aspx) | |● |● |5 | |
| [foresta delle decisioni](https://msdn.microsoft.com/library/azure/dn906015.aspx) |● |○ | |6 | |
| [giungla delle decisioni ](https://msdn.microsoft.com/library/azure/dn905963.aspx) |● |○ | |6 |Footprint della memoria ridotto |
| [rete neurale](https://msdn.microsoft.com/library/azure/dn906030.aspx) |● | | |9 |[È possibile un’ulteriore personalizzazione](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [one-v-all](https://msdn.microsoft.com/library/azure/dn905887.aspx) |- |- |- |- |Vedere le proprietà del metodo di due classi hello selezionato |
| **Regressionee** | | | | | |
| [lineare](https://msdn.microsoft.com/library/azure/dn905978.aspx) | |● |● |4 | |
| [Regressione lineare Bayesiana](https://msdn.microsoft.com/library/azure/dn906022.aspx) | |○ |● |2 | |
| [foresta delle decisioni](https://msdn.microsoft.com/library/azure/dn905862.aspx) |● |○ | |6 | |
| [albero delle decisioni con boosting scalabile](https://msdn.microsoft.com/library/azure/dn905801.aspx) |● |○ | |5 |Footprint della memoria di grandi dimensioni |
| [Quantile della foresta rapida](https://msdn.microsoft.com/library/azure/dn913093.aspx) |● |○ | |9 |Distribuzioni invece di previsioni punti |
| [rete neurale](https://msdn.microsoft.com/library/azure/dn905924.aspx) |● | | |9 |[È possibile un’ulteriore personalizzazione](http://go.microsoft.com/fwlink/?LinkId=402867) |
| [Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx) | | |● |5 |Tecnicamente logaritmica-lineare. Per la previsione di conteggi. |
| [Ordinale](https://msdn.microsoft.com/library/azure/dn906029.aspx) | | | |0 |Per la previsione dell'ordinamento delle classificazioni |
| **Rilevamento anomalie** | | | | | |
| [macchina a vettori di supporto](https://msdn.microsoft.com/library/azure/dn913103.aspx) |○ |○ | |2 |Particolarmente valido per set di funzioni di grandi dimensioni |
| [Rilevamento delle anomalie basato su PCA](https://msdn.microsoft.com/library/azure/dn913102.aspx) | |○ |● |3 | |
| [K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/) | |○ |● |4 |Algoritmo di clustering |

**Proprietà algoritmo:**

**●** -Mostra accuratezza, tempi di training veloci e utilizzare hello di linearità

**○** : mostra buona precisione e tempi di addestramento moderati

## <a name="algorithm-notes"></a>Note algoritmo
### <a name="linear-regression"></a>Linear regression
Come accennato in precedenza, [regressione lineare](https://msdn.microsoft.com/library/azure/dn905978.aspx) si inserisce un set di dati toohello riga (o piano o iperpiano). È un ottimo strumento di lavoro, semplice e veloce, ma potrebbe essere troppo semplicistica per alcuni problemi.
Qui è disponibile un' [esercitazione sulla regressione lineare](machine-learning-linear-regression-in-azure.md).

![Dati con una tendenza lineare][3]

***Dati con una tendenza lineare***

### <a name="logistic-regression"></a>Regressione logistica
Sebbene molte include 'regressione' nel nome hello, la regressione logistica è effettivamente un potente strumento per [due classi](https://msdn.microsoft.com/library/azure/dn905994.aspx) e [multiclass](https://msdn.microsoft.com/library/azure/dn905853.aspx) classificazione. È semplice e veloce. Hello fatto che usa un '-forma curva anziché una linea retta rende una scelta naturale per dividere i dati in gruppi. La regressione logistica fornisce limiti della classe lineari, pertanto quando la si utilizza, assicurarsi che un'approssimazione lineare sia accettabile.

![Dati tootwo-classe di regressione logistica con una sola funzionalità][4]

***Dati tootwo-classe della regressione logistica con una sola funzionalità*** *-il limite di classe è hello punto in cui hello curva logistica classi tooboth semplicemente più vicino*

### <a name="trees-forests-and-jungles"></a>Alberi, foreste e giungle
Le foreste delle decisioni ([regressione](https://msdn.microsoft.com/library/azure/dn905862.aspx), [a due classi](https://msdn.microsoft.com/library/azure/dn906008.aspx) e [multiclasse](https://msdn.microsoft.com/library/azure/dn906015.aspx)), le giungle delle decisioni ([a due classi](https://msdn.microsoft.com/library/azure/dn905976.aspx) e [multiclasse](https://msdn.microsoft.com/library/azure/dn905963.aspx)) e gli alberi delle decisioni con boosting ([regressione](https://msdn.microsoft.com/library/azure/dn905801.aspx) e [a due classi](https://msdn.microsoft.com/library/azure/dn906025.aspx)) sono tutti basati sugli alberi delle decisioni, un concetto fondamentale del Machine Learning. Esistono molte varianti di alberi delle decisioni, ma eseguono tutti lo stesso significato, suddividere lo spazio di funzioni hello in aree con principalmente hello stessa etichetta. Possono essere aree di una categoria coerente o di un valore costante, a seconda che si esegua la classificazione o la regressione.

![L’albero delle decisioni suddivide uno spazio di caratteristiche][5]

***Un albero delle decisioni suddivide uno spazio di elementi in aree di valori approssimativamente uniformi***

Poiché uno spazio di funzione può essere suddivisa in aree arbitrario piccole, è facile tooimagine dividendolo precisione sufficiente toohave un punto dati per ogni area. un esempio estremo di sovradattamento. In ordine tooavoid questa operazione, un ampio set di strutture ad albero vengono costruiti con particolare attenzione matematiche prese che alberi hello non sono correlati. Media di Hello di foresta delle decisioni"" è una struttura ad albero che consente di evitare l'overfitting. Le foreste delle decisioni possono utilizzare molta memoria. Giungle delle decisioni sono un valore variant che utilizza meno memoria spese hello di un tempo di training leggermente superiore.

Gli alberi delle decisioni con boosting consentono di evitare il sovradattamento limitando il numero di volte in cui possono suddividersi e il modo in cui pochi punti dati sono consentiti in ogni area. L'algoritmo costruisce una sequenza di alberi, ognuno dei quali apprende per compensare errori hello dalla struttura ad albero hello prima a sinistra. il risultato di Hello è uno strumento di apprendimento estremamente accurato che tende toouse una grande quantità di memoria. Per la descrizione tecnica hello, estrarre [documento originale di test di Friedman](http://www-stat.stanford.edu/~jhf/ftp/trebst.pdf).

[Fast regressione quantile foresta](https://msdn.microsoft.com/library/azure/dn913093.aspx) è una variante di alberi delle decisioni per caso speciale di hello in cui si desidera conoscere non solo hello tipico () valore mediano di dati di hello all'interno di un'area, ma anche la distribuzione nel formato hello di quantili.

### <a name="neural-networks-and-perceptrons"></a>Reti neurali e percezione
Le reti neurali sono algoritmi di apprendimento ispirati al cervello che coprono problemi [multiclasse](https://msdn.microsoft.com/library/azure/dn906030.aspx), [a due classi](https://msdn.microsoft.com/library/azure/dn905947.aspx) e di [regressione](https://msdn.microsoft.com/library/azure/dn905924.aspx). E sono disponibili per un'infinita varietà, ma le reti neurali hello all'interno di Azure Machine Learning sono tutti della forma hello di grafici aciclici diretti. Ciò significa che le caratteristiche di input vengono passate in avanti (mai indietro) tramite una sequenza di livelli prima di essere convertiti in output. In ogni livello, gli input vengono ponderati in varie combinazioni, sommato e passato al livello successivo hello. Questa combinazione di risultati di calcoli semplici in toolearn il possibilità sofisticate le tendenze dei dati e i limiti di classe, apparentemente rapida. Reti di molti livelli di questo tipo eseguono hello "formazione" che combustibili così tanto tech reporting e fantascienza.

Queste alte prestazioni non sono però possibili senza un costo. Reti neurali possono richiedere un tootrain molto tempo, in particolare per grandi set di dati con un numero elevato di funzionalità. Hanno inoltre la maggior parte degli algoritmi, il che significa che lo sweep dei parametri si espande notevolmente i tempi di training hello più parametri.
E per tali overachievers che desiderano troppo[specificare la propria struttura di rete](http://go.microsoft.com/fwlink/?LinkId=402867), i valori possibili sono inexhaustible.

![Limiti di apprendere le reti neurali][6]
***limiti hello appresi le reti neurali possono essere complessi e irregolare***

Hello [due classi Media perceptron](https://msdn.microsoft.com/library/azure/dn906036.aspx) è tempi di training tooskyrocketing risposta reti neurali. Utilizza una struttura di rete che fornisce limiti di classe lineari. È quasi primitivo da standard attuali, ma presenta una lunga storia di lavorare in modo affidabile ed è sufficientemente piccolo toolearn rapidamente.

### <a name="svms"></a>SVM
Macchine a vettori di supporto (macchine SVM) trovare limite hello che separa le classi da come livello margine possibili. Quando due classi hello non possono essere chiaramente separate, gli algoritmi di hello trovare limite migliore di hello che possono essere utilizzate. Come è scritto in Azure Machine Learning, hello [SVM a due classi](https://msdn.microsoft.com/library/azure/dn905835.aspx) ciò avviene solo una linea retta. (Nel linguaggio dell’SVM, utilizza un kernel lineare). In quanto rende l'approssimazione lineare, è in grado di toorun abbastanza rapidamente. Dove eccelle davvero è con dati ricchi di caratteristiche, come testi o genomica. In questi casi macchine SVM sono in grado di tooseparate classi più rapidamente e con meno l'overfitting rispetto ad altri la maggior parte degli algoritmi, inoltre toorequiring solo una singola quantità di memoria.

![Limite di classe della macchina a vettori di supporto ][7]

***Un limite di classe di supporto tipico vettore macchina Ottimizza margine hello separare due classi***

Un altro prodotto di Microsoft Research, hello [SVM avanzato a livello locale a due classi](https://msdn.microsoft.com/library/azure/dn913070.aspx) è una variante di SVM che mantiene la maggior parte di efficienza di memoria e velocità hello della versione di hello lineare non lineare. È ideale per i casi in cui approccio lineare hello non fornisce le risposte sufficientemente accurate. gli sviluppatori di Hello è stato eliminato fast suddividendo problema hello in una serie di piccoli problemi SVM lineare. Hello lettura [completo descrizione](http://research.microsoft.com/um/people/manik/pubs/Jose13.pdf) per informazioni dettagliate di hello su come vengono estratti disattivare questo accorgimento.

Utilizza un'estensione intelligente di macchine SVM non lineare, hello [SVM a una classe](https://msdn.microsoft.com/library/azure/dn913103.aspx) Disegna un limite che delinea strettamente hello intero set di dati. È utile per il rilevamento delle anomalie. Eventuali nuovi punti dati che rientrano molto di fuori di tale limite sono sufficientemente insolito toobe degno di nota.

### <a name="bayesian-methods"></a>Metodi bayesiani
I metodi bayesiani hanno una qualità estremamente utile: evitare il sovradattamento. A tal eseguendo alcuni presupposti in anticipo sulla distribuzione di probabilità hello delle risposte hello. Un altro risultato di questo approccio è che dispongono di parametri in numero molto ridotto. Azure Machine Learning ha algoritmi bayesiani per entrambe le classificazioni ([la Bayes Point Machine a due classi](https://msdn.microsoft.com/library/azure/dn905930.aspx)) e la regressione ([regressione lineare bayesiana](https://msdn.microsoft.com/library/azure/dn906022.aspx)).
Si noti che questi si presuppone che è possibile suddividere i dati di hello o adatta con una linea retta.

Dal punto di vista storico, le Bayes Point Machine sono state sviluppate presso Microsoft Research. Si basano su un lavoro teorico estremamente interessante. studente interessati Hello è diretto toohello [articolo originale in JMLR](http://jmlr.org/papers/volume1/herbrich01a/herbrich01a.pdf) e [dettagliati post di blog di Chris Bishop](http://blogs.technet.com/b/machinelearning/archive/2014/10/30/embracing-uncertainty-probabilistic-inference.aspx).

### <a name="specialized-algorithms"></a>Algoritmi specializzati
Se si dispone di un obiettivo molto specifico si potrebbe essere fortunati. All'interno di hello raccolta di Azure Machine Learning, sono disponibili algoritmi specializzate in:

- stima di classificazione ([regressione ordinale](https://msdn.microsoft.com/library/azure/dn906029.aspx)),
- stima di conteggio ([regressione Poisson](https://msdn.microsoft.com/library/azure/dn905988.aspx)),
- rilevamento di anomalie (uno basato sull'[analisi dei componenti principali](https://msdn.microsoft.com/library/azure/dn913102.aspx) e l'altro basato sulle [macchine a vettori di supporto](https://msdn.microsoft.com/library/azure/dn913103.aspx))
- Clustering ([K-means](https://msdn.microsoft.com/library/azure/5049a09b-bd90-4c4e-9b46-7c87e3a36810/))

![Rilevamento delle anomalie basato su PCA][8]

***Rilevamento di anomalie basato su PCA*** *-hello gran parte dei dati hello rientra in una distribuzione stereotypical; punti di allontanarsi notevolmente da tale distribuzione sono sospetti*

![Set di dati raggruppati utilizzando K-means][9]

***Un set di dati viene raggruppato in 5 cluster usando K-means***

È inoltre disponibile un insieme [one-v-all multiclass classifier](https://msdn.microsoft.com/library/azure/dn905887.aspx), quale problema di classificazione hello N classe interruzioni dei problemi di classificazione a due classi di n-1. accuratezza Hello, tempi di training e linearità proprietà sono determinate da classificatori di due classi hello utilizzati.

![Classificatori due classi combinate tooform un classificatore tre classi][10]

***Una coppia di due classi classificatori combinare tooform un classificatore tre classi***

Azure Machine Learning include anche framework potente tooa apprendimento accesso sotto il titolo di hello [Vowpal Wabbit](https://msdn.microsoft.com/library/azure/8383eb49-c0a3-45db-95c8-eb56a1fef5bf).
VW sfugge alla categorizzazione in questo caso, poiché può apprendere problemi sia di classificazione che di regressione e può apprendere anche dati parzialmente senza etichetta. È possibile configurarlo toouse uno qualsiasi di un numero di apprendimento algoritmi, perdita funzioni e algoritmi di ottimizzazione. È stato progettato da hello messa a terra backup toobe efficiente, estremamente veloce e parallela. Consente di gestire insiemi di caratteristiche estremamente grandi con uno sforzo minimo.
Avviato e condotto da John Langford di Microsoft Research, VW è un elemento da Formula Uno in un campo di algoritmi pari a vetture di serie. Non tutti i problemi rientra VW, ma in questo caso, quelle in uso, potrebbe essere la pena tooclimb la curva di apprendimento dell'interfaccia. È inoltre disponibile come [codice open source autonomo](https://github.com/JohnLangford/vowpal_wabbit) in diverse lingue.

## <a name="more-help-with-algorithms"></a>Altre informazioni sugli algoritmi
* Per ottenere una descrizione degli algoritmi e alcuni esempi, vedere [Infografica scaricabile: nozioni fondamentali di Machine Learning con esempi di algoritmi](machine-learning-basics-infographic-with-algorithm-examples.md).
* Per un elenco in base alla categoria di algoritmi di apprendimento hello tutti disponibili in Azure Machine Learning Studio, vedere [inizializzare modello] [ initialize-model] hello algoritmo di Machine Learning Studio e modulo della Guida.
* Per un elenco alfabetico completo degli algoritmi e dei moduli disponibili in Azure Machine Learning Studio, vedere [A-Z list of Machine Learning Studio modules][a-z-list] (Elenco alfabetico dei moduli di Machine Learning Studio) nella Guida degli algoritmi e dei moduli di Machine Learning Studio.
* toodownload e stampare un diagramma che offra una panoramica delle funzionalità di hello di Azure Machine Learning Studio, vedere [diagramma della panoramica delle funzionalità di Azure Machine Learning Studio](machine-learning-studio-overview-diagram.md).


<!-- Reference links -->
[initialize-model]: https://msdn.microsoft.com/library/azure/dn905812.aspx
[a-z-list]: https://msdn.microsoft.com/library/azure/dn906033.aspx

<!-- Media -->

[1]: ./media/machine-learning-algorithm-choice/image1.png
[2]: ./media/machine-learning-algorithm-choice/image2.png
[3]: ./media/machine-learning-algorithm-choice/image3.png
[4]: ./media/machine-learning-algorithm-choice/image4.png
[5]: ./media/machine-learning-algorithm-choice/image5.png
[6]: ./media/machine-learning-algorithm-choice/image6.png
[7]: ./media/machine-learning-algorithm-choice/image7.png
[8]: ./media/machine-learning-algorithm-choice/image8.png
[9]: ./media/machine-learning-algorithm-choice/image9.png
[10]: ./media/machine-learning-algorithm-choice/image10.png
