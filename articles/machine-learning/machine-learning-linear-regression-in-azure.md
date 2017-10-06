---
title: la regressione lineare in Machine Learning aaaUsing | Documenti Microsoft
description: Confronto tra i modelli di regressione lineare in Excel e in Azure Machine Learning Studio
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Uso della regressione lineare Azure Machine Learning
> *Kate Baroni* e *Ben Boatman* sono architetti di soluzioni aziendali in Microsoft Data Insights Center of Excellence. In questo articolo vengono descritte l'esperienza di migrazione una regressione analysis suite tooa basato su cloud soluzione esistente con Azure Machine Learning. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Obiettivo
Il progetto è iniziato con due obiettivi prefissati: 

1. Utilizzare analitica predittiva tooimprove hello precisione di proiezioni sui ricavi mensili dell'azienda 
2. Utilizzo di Azure Machine Learning tooconfirm, ottimizzare, aumentare la velocità e la scala i risultati. 

Come molte aziende, anche questa organizzazione esegue un processo di previsione dei ricavi mensile. Il team di piccole dimensioni di business analyst occupano mediante Azure Machine Learning toosupport hello processo e migliorare l'accuratezza della previsione. il team di Hello impiegato per la raccolta dei dati da più origini e l'esecuzione di attributi di hello dati tramite l'analisi statistica che identifica gli attributi chiave tooservices rilevanti le previsioni di vendita di diversi mesi. passaggio successivo Hello durante i modelli di regressione statistica di creazione di prototipi toobegin hello dati presenti in Excel. All'interno di alcune settimane, abbiamo un modello di regressione di Excel che è stata superando campo corrente hello e finanza previsione processi. Questo aspetto è diventato risultato di stima hello linea di base. 

È quindi impiegato hello successivo passaggio toomoving nostri analitica predittiva su tooAzure Machine Learning toofind out come Machine Learning suscettibili di miglioramento delle prestazioni predittiva.

## <a name="achieving-predictive-performance-parity"></a>Raggiungimento della parità delle prestazioni predittive
La priorità è tooachieve parità tra i modelli di regressione di Machine Learning ed Excel. Dato hello stessi dati e hello stesso suddividere i set di training e dati di testing, Desideravamo parità prestazioni predittive tooachieve tra Excel e Machine Learning. Inizialmente, l'obiettivo non è stato raggiunto. modello di Excel Hello ha superato il modello di Machine Learning hello. Errore di Hello: a causa di mancanza di tooa di conoscenza dello strumento base di hello impostazione in Machine Learning. Dopo una sincronizzazione con team del prodotto di Machine Learning hello, viene acquisita una migliore comprensione di hello base impostazione richiesta per il set di dati e ottenuto parità tra due modelli di hello. 

### <a name="create-regression-model-in-excel"></a>Creare un modello di regressione in Excel
La regressione di Excel utilizzato il modello di regressione lineare standard hello hello analisi di Excel, vedere. 

È stata calcolata *% assoluto medio errore* e utilizzata come misura delle prestazioni di hello per modello hello. Impiegato tooarrive 3 mesi in un modello di lavoro con Excel. È attivata la modalità gran parte dell'apprendimento hello in hello esperimento di Machine Learning Studio che infine è stata utile nelle informazioni sui requisiti.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Creare un esperimento confrontabile in Azure Machine Learning
Abbiamo adottato toocreate questi passaggi esperimento in Machine Learning Studio: 

1. Set di dati di hello caricato come un tooMachine file csv Learning Studio (file molto piccola)
2. Creazione di un esperimento di nuovo e utilizzato hello [selezionare le colonne nel set di dati] [ select-columns] tooselect modulo hello stesse funzionalità di dati utilizzata in Excel 
3. Hello utilizzato [dati divisi] [ split] modulo (con *espressione relativa* modalità) dati hello toodivide hello stessi set di dati di training, come era stato eseguito in Excel 
4. Sperimenta hello [Linear Regression] [ linear-regression] modulo (solo opzioni predefinito), documentati e confrontati modello di regressione hello risultati tooour Excel

### <a name="review-initial-results"></a>Rivedere i risultati iniziali
Inizialmente, il modello di Excel hello buoni chiaramente il modello di Machine Learning Studio hello: 

|  | Excel | Studio |
| --- |:---:|:---:|
| Prestazioni | | |
| <ul style="list-style-type: none;"><li>R-quadrato corretto</li></ul> |0,96 |N/D |
| <ul style="list-style-type: none;"><li>Coefficiente di <br />determinazione</li></ul> |N/D |0,78<br />(bassa precisione) |
| Errore assoluto medio |$ 9,5 milioni |$ 19,4 milioni |
| Errore assoluto medio (%) |6,03% |12,2% |

Quando è stato eseguito il processo e i risultati per gli sviluppatori di hello e gli esperti di dati su team Machine Learning hello, vengono rapidamente forniti alcuni suggerimenti utili. 

* Quando si utilizza hello [Linear Regression] [ linear-regression] modulo in Machine Learning Studio, vengono forniti due metodi:
  * Online Gradient Descent: più adatto a problemi su larga scala
  * Metodo dei minimi quadrati: Questo metodo hello la maggior parte delle persone considerano quando viene emesso di regressione lineare è. Per set di dati di piccole dimensioni, il metodo Ordinary Least Squares è solitamente la scelta ottimale.
* Provare a regolare le prestazioni di hello peso regolarizzazione L2 parametro tooimprove. Too0.001 è impostato per impostazione predefinita, ma per il piccolo set di dati è impostare la proprietà too0.005 tooimprove prestazioni. 

### <a name="mystery-solved"></a>Misero risolto
Quando si applica indicazioni hello, ottenuta hello stesse prestazioni di base in Machine Learning Studio, come in Excel: 

|  | Excel | Studio (iniziale) | Studio con Least Squares |
| --- |:---:|:---:|:---:|
| Valore etichettato |Valori effettivi (numerici) |uguale |uguale |
| Strumento di apprendimento |Excel -> Analisi dati -> Regressione |Regressione lineare. |Linear Regression |
| Opzioni strumento di apprendimento |N/D |Valori predefiniti |Ordinary Least Squares<br />L2 = 0,005 |
| Set di dati |26 righe, 3 funzionalità, 1 etichetta. Tutti valori numerici. |uguale |uguale |
| Divisione: training |Excel sottoposto a training sui hello innanzitutto 18 righe, testati su hello 8 ultime righe. |uguale |uguale |
| Divisione: test |Formula di regressione applicato di Excel toohello ultimo 8 righe |uguale |uguale |
| **Prestazioni** | | | |
| R-quadrato corretto |0,96 |N/D | |
| Coefficiente di determinazione |N/D |0,78 |0,952049 |
| Errore assoluto medio |$ 9,5 milioni |$ 19,4 milioni |$ 9,5 milioni |
| Errore assoluto medio (%) |<span style="background-color: 00FF00;"> 6,03%</span> |12,2% |<span style="background-color: 00FF00;"> 6,03%</span> |

Inoltre, i coefficienti di Excel hello rispetto anche toohello pesi delle funzioni in hello Azure modello con Training:

|  | Coefficienti di Excel | Pesi delle funzionalità di Azure |
| --- |:---:|:---:|
| Intercetta/distorsione |19470209,88 |19328500 |
| Funzionalità A |0,832653063 |0,834156 |
| Funzionalità B |11071967,08 |11007300 |
| Funzionalità C |25383318,09 |25140800 |

## <a name="next-steps"></a>Passaggi successivi
Desideravamo servizio web di Machine Learning tooconsume hello all'interno di Excel. I business analyst si basano su Excel ed è necessario un modo toocall hello Machine Learning servizio con una riga di dati di Excel web e di restituire hello stimato tooExcel valore. 

Desideravamo anche toooptimize modello in esame usando le opzioni di hello e gli algoritmi disponibili in Machine Learning Studio.

### <a name="integration-with-excel"></a>Integrazione con Excel
La soluzione è stata toooperationalize la regressione di Machine Learning del modello tramite la creazione di un servizio web dal modello con training hello. Entro pochi minuti, è possibile chiamarlo direttamente da Excel tooreturn un valore di ricavi stimati servizio web hello è stato creato. 

Hello *del Dashboard di servizi Web* sezione include una cartella di lavoro di Excel scaricabile. cartella di lavoro Hello dotato di pre-formattata hello API e schema di informazioni sui servizi web incorporati. Quando fa clic su *cartella di lavoro di Excel scaricare*, verrà visualizzata la cartella di lavoro hello e che è possibile salvarlo tooyour computer locale. 

![][1]

Con hello cartella di lavoro aperta, copiare i parametri predefiniti nella sezione relativa ai parametri hello blu come illustrato di seguito. Dopo aver immettono i parametri di hello, Excel effettua una chiamata toohello servizio web Machine Learning e hello etichette con punteggio stimate verranno visualizzato nella sezione valori stimati hello verde. cartella di lavoro Hello continuerà toocreate stime per i parametri in base al modello con training per tutti gli elementi di riga immessa in parametri. Per ulteriori informazioni su come toouse tale funzionalità, vedere [utilizzo di un servizio Web di Azure Machine Learning da Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Ottimizzazione e altri esperimenti
Ora che abbiamo una linea di base con il nostro modello di Excel, è spostata ahead toooptimize il modello di regressione lineare di Machine Learning. È stato usato il modulo hello [Filter-Based Feature Selection] [ filter-based-feature-selection] tooimprove nella selezione di elementi di dati iniziale e ci ha consentito di ottenere un miglioramento delle prestazioni di % 4.6 errore assoluto medio. Per i progetti futuri, si utilizzerà questa funzionalità che è stato possibile salvare ci settimane in un'iterazione attraverso attributi toofind hello destra set di dati della funzionalità toouse per la modellizzazione. 

Successivamente contiamo di altri algoritmi di tooinclude come [Bayes] [ bayesian-linear-regression] o [alberi delle decisioni con Boosting] [ boosted-decision-tree-regression] nel nostro toocompare esperimento prestazioni. 

Se si desidera tooexperiment con regressione, tootry un set di dati valido è hello regressione di efficienza energetica esempio set di dati che dispone di molti attributi numerici. set di dati Hello viene fornito come parte del set di dati di esempio hello in Machine Learning Studio. È possibile utilizzare un'ampia gamma di apprendimento dei moduli toopredict carico riscaldamento o raffreddamento carico. grafico Hello seguente è che un confronto delle prestazioni di regressione differenti apprende contro hello energetico dataset stima per il carico di raffreddamento variabile di destinazione hello: 

| Modello | Errore assoluto medio | Radice dell'errore quadratico medio | Errore assoluto relativo | Errore quadratico relativo | Coefficiente di determinazione |
| --- | --- | --- | --- | --- | --- |
| Albero delle decisioni con boosting scalabile |0,930113 |1,4239 |0,106647 |0,021662 |0,978338 |
| Regressione lineare (Gradient Descent) |2,035693 |2,98006 |0,233414 |0,094881 |0,905119 |
| Regressione rete neurale |1,548195 |2,114617 |0,177517 |0,047774 |0,952226 |
| Regressione lineare (Ordinary Least Squares) |1,428273 |1,984461 |0,163767 |0,042074 |0,957926 |

## <a name="key-takeaways"></a>Risultati principali
L'esecuzione parallela della regressione di Excel e degli esperimenti di Azure Machine Learning ha aiutato a conoscere meglio questi strumenti. Creazione modello di previsione hello in Excel e confrontandolo con Machine Learning toomodels [Linear Regression] [ linear-regression] ha aiutato a informazioni su Azure Machine Learning e sono stati individuati dati tooimprove opportunità prestazioni di selezione e il modello. 

Inoltre, si è scoperto che è consigliabile toouse [Filter-Based Feature Selection] [ filter-based-feature-selection] tooaccelerate progetti di previsione. Applicando dati tooyour selezione delle funzionalità, è possibile creare un modello migliorato in Machine Learning con migliori prestazioni complessive. 

hello tootransfer di Hello capacità predittiva analitiche di previsione da Machine Learning tooExcel sistemico consente un aumento significativo in hello possibilità toosuccessfully fornire risultati pubblico di utenti tooa generali dell'azienda. 

## <a name="resources"></a>Risorse
Di seguito sono elencate alcune risorse per agevolare l'uso della regressione: 

* Regressione in Excel. Se non è mai stata provata la regressione in Excel, questa esercitazione la spiega in modo molto chiaro: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Regressione e previsione. Tyler Chessman ha scritto un articolo di blog che spiega come toodo time series forecasting in Excel, che contiene una descrizione di un buon principianti di regressione lineare. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Regressione lineare Ordinary Least Squares: difetti, problemi e ostacoli. Per un'introduzione e una discussione sulla regressione: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

