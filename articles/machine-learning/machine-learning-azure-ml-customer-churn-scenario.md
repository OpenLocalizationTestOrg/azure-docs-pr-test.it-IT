---
title: aaaAnalyzing cliente varianza tramite Machine Learning | Documenti Microsoft
description: Casi di studio sullo sviluppo di un modello integrato per l'analisi e l'assegnazione dei punteggi di varianza del cliente
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Analisi della varianza del cliente tramite Azure Machine Learning
## <a name="overview"></a>Panoramica
Questo argomento illustra un'implementazione di riferimento di un progetto di analisi della varianza del cliente compilata tramite Azure Machine Learning. Questo articolo prende in esame i modelli associati generici per olistico per risolvere il problema di hello di varianza industriali cliente. È inoltre misurare l'accuratezza di hello di modelli compilati utilizzando Machine Learning ed è valutare le direzioni per uno sviluppo ulteriore.  

### <a name="acknowledgements"></a>Riconoscimenti
Questo esperimento è stato sviluppato e testato da Serge Berger, Principal Data Scientist presso Microsoft e Roger Barga, in precedenza Product Manager per Microsoft Azure Machine Learning. il team di documentazione di Azure Hello esprime riconosce le competenze e ringraziamenti per la condivisione di questo white paper.

> [!NOTE]
> non sono disponibili pubblicamente i dati Hello utilizzati per questa sperimentazione. Per un esempio di come toobuild un apprendimento del modello per l'analisi della varianza del, vedere: [delle vendite al dettaglio di varianza del modello](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>problema di Hello di varianza del cliente
Aziende mercato consumer hello e in tutti i settori dell'organizzazione hanno toodeal con varianza. In certi casi una varianza eccessiva può arrivare a influenzare i criteri decisionali. soluzione tradizionale Hello toopredict churners elevata tendenza e di soddisfare esigenze tramite un servizio concierge, campagne di marketing o applicando dispense speciali. Questi approcci possono variare da tooindustry settore e anche da un tooanother cluster consumer specifico all'interno di un settore (ad esempio, telecomunicazioni).

Hello accomunati dal fatto che le aziende hanno bisogno toominimize questi tentativi di conservazione di clienti speciale. Di conseguenza, una metodologia naturale verrà tooscore ogni cliente con probabilità hello di varianza e risolvere le prime hello N quelli. potrebbe essere hello principali clienti Hello quelli più remunerativo; in scenari più sofisticati, ad esempio, una funzione dei profitti è impiegata durante la selezione di hello di candidati per dispensa speciale. Tuttavia, queste considerazioni sono solo una parte della strategia globale di hello per la gestione di varianza. Le aziende hanno anche tootake nel rischio di account e tolleranza al rischio associato, hello livello e il costo di intervento hello e la segmentazione plausibile cliente.  

## <a name="industry-outlook-and-approaches"></a>Prospettive e approcci di settore
La gestione sofisticata della varianza è un indicatore di maturità di un settore. Hello classico esempio è il settore di telecomunicazioni hello in cui i sottoscrittori sono noti toofrequently commutatore da un provider tooanother. Questa varianza volontaria rappresenta un motivo principale di preoccupazione. Inoltre, i provider accumulati conoscenza significativa su *varianza del driver*, che sono fattori di hello tooswitch di clienti tale unità.

Ad esempio, scelta palmari o il dispositivo è un driver noto di varianza in business cellulare hello. Di conseguenza, un criterio comune è il prezzo hello toosubsidize di un ricevitore su nuovi iscritti e l'addebito ai clienti per un aggiornamento di un tooexisting prezzo completo. In passato, questo criterio ha portato toocustomers salto da un provider tooanother tooget uno sconto nuova, che a sua volta, è richiesto toorefine provider strategie.

L'elevata volatilità nelle offerte legate ai dispositivi è un fattore in grado di invalidare velocemente i modelli di varianza che si basano sui modelli di dispositivo attuali. Inoltre, telefoni cellulari non sono solo per i dispositivi di telecomunicazione; sono anche istruzioni modo (potrebbe essere preferibile hello iPhone), e tali social predittori sono di fuori ambito hello telecomunicazioni regolare dei set di dati.

risultato Hello per la modellazione è che è non è possibile definire un criterio audio semplicemente eliminando motivi noti per varianza. Infatti, una strategia di modellazione continua, che include modelli classici che quantificano le variabili di categoria (ad esempio alberi decisionali) è **obbligatoria**.

Utilizza grandi set di dati sui clienti, le organizzazioni eseguono analitica dei dati di grandi dimensioni (in particolare, la varianza del rilevamento in base ai dati di grandi dimensioni) come un problema di toohello efficace. È possibile trovare informazioni sul problema di hello big data approccio toohello di varianza in hello indicazioni sulla sezione ETL.  

## <a name="methodology-toomodel-customer-churn"></a>Varianza del cliente di metodologia toomodel
Una comune problemi processo toosolve cliente varianza è illustrata nelle figure 1-3:  

1. Un modello di rischio consente tooconsider influenza azioni probabilità e al rischio.
2. Un modello di intervento consente tooconsider come livello hello dell'intervento possa influire sulle probabilità hello dell'importo hello e della varianza del valore di durata cliente (CLV).
3. Questa analisi si presta tooa analisi qualitativa tooa alzati di livello la campagna di marketing destinato offerta hello di toodeliver segmenti cliente ottimale.  

![][1]

Questo approccio predittiva finalizzata è varianza tootreat modo migliore di hello, ma è dotato di complessità: abbiamo toodevelop una traccia e sistema per le dipendenze più modelli tra i modelli di hello. interazione di Hello tra i modelli può essere incapsulate come illustrato nel seguente diagramma hello:  

![][2]

*Figura 4: archetipo multi modello unificato*  

Interazione tra i modelli di hello è chiave se ci sono toodeliver conservazione di toocustomer un approccio olistico. Ogni modello necessariamente diminuisce nel tempo; Pertanto, architettura hello è un ciclo implicito (simile toohello sistema per l'impostazione standard di data mining dati hello metodologia, [***3***]).  

Hello ciclo complessivo di marketing di decisione di rischio per la segmentazione/decomposizione è ancora una struttura generalizzata, ovvero problemi aziendali toomany applicabile. Analisi varianza sono semplicemente un rappresentante sicuro di questo gruppo di problemi perché utilizza un tutti i tratti hello di un problema di business complessa che non consente una soluzione predittiva semplificata. Hello social hello approccio moderno toochurn gli aspetti non sono particolarmente evidenziati nell'approccio hello, ma gli aspetti di social networking hello sono incapsulati nel sistema per la modellazione di hello, come avviene in qualsiasi modello.  

Un'aggiunta interessante in questo ambito è l'analisi dei Big Data. Telecomunicazioni e delle vendite al dettaglio aziende raccolgono completo dati relativi ai clienti ed è facilmente possibile prevede che hello necessario per la connettività di più modello diventerà una tendenza comune, data emergono tendenze, ad esempio hello Internet of Things e dispositivi universali, che consentono di soluzioni smart tooemploy business a più livelli.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Implementazione di hello modellazione di sistema per in Machine Learning Studio
Dato problema hello descritto in precedenza, hello migliore modo tooimplement una modellazione integrata e assegnazione dei punteggi approccio novità In questa sezione viene illustrato tale processo tramite l'utilizzo di Azure Machine Learning Studio.  

approccio di più modelli Hello è necessaria quando si progetta un sistema globale di rilevazione per varianza. Anche hello (predittiva) parte dell'approccio hello di punteggio deve essere più modello.  

Hello diagramma seguente mostra il prototipo hello che abbiamo creato, che utilizza quattro algoritmi punteggio della varianza del toopredict Machine Learning Studio. Hello per l'utilizzo di un approccio più modello, infatti, non solo toocreate un'accuratezza di tooincrease classificazione insieme, ma anche tooprotect adattamento in eccesso e selezione di funzionalità rigorosa tooimprove.  

![][3]

*Figura 5: Prototipo di un approccio di modellazione della varianza*  

Hello nelle sezioni seguenti forniscono ulteriori dettagli sul prototipo hello valutazione modello implementate tramite Machine Learning Studio.  

### <a name="data-selection-and-preparation"></a>Selezione e preparazione dei dati
dati Hello utilizzato modelli hello toobuild e i clienti di punteggio è stato ottenuto da una soluzione verticale CRM, con hello dati offuscati tooprotect privacy dei clienti. dati Hello contengano informazioni sulle 8.000 sottoscrizioni in hello Stati Uniti e combina tre origini: provisioning dati (metadati sottoscrizione), i dati di attività (utilizzo del sistema hello) e i dati di supporto tecnico clienti. Hello dati non includono aziende di tutte le informazioni relative ai clienti di hello; ad esempio, non include i punteggi di fedeltà dei metadati o carta di credito.  

Per semplicità, i processi ETL e di pulizia dei dati sono esclusi dall'ambito, in quanto si presuppone che la preparazione dei dati sia già stata completata altrove.   

Selezione funzionalità per la modellazione è basato sul punteggio preliminare importanza del set di hello dei predittori, inclusi nel processo di hello che usa il modulo di foresta casuale hello. Per l'implementazione di hello in Machine Learning Studio, è calcolato hello Media, mediana e gli intervalli per le funzionalità rappresentative. Ad esempio, è aggiunto aggregazioni per i dati qualitativo hello, ad esempio i valori minimi e massimo per l'attività dell'utente.    

È anche acquisite informazioni temporali per hello ultimi sei mesi. È stato analizzato di dati per un anno ed è stabilito che anche se vi sono statisticamente significative tendenze, effetto hello varianza è notevolmente ridotta dopo sei mesi.  

Hello più importante è che hello del processo di, incluse ETL, selezione funzionalità e modellazione è stata implementata in Machine Learning Studio, l'utilizzo di origini dati in Microsoft Azure.   

Hello nei diagrammi seguenti illustrano i dati di hello è stata utilizzata.  

![][4]

*Figura 6: Estratto dell'origine dati (offuscati)*  

![][5]

*Figure 7: Funzionalità estratte dall'origine dati*
 

> Si noti che questi dati sono privati e pertanto non possono essere condivisa modello hello e dati.
> Tuttavia, per un modello simile utilizzando dati pubblicamente disponibili, vedere questo esperimento di esempio in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [varianza del cliente di telecomunicazioni](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> informazioni su come è possibile implementare un modello di analisi varianza utilizzando Cortana Intelligence Suite toolearn, si consiglia inoltre di [questo video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) da Senior Program Manager relative a Wee Hyong Tok. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Algoritmi utilizzati nel prototipo hello
È stato usato hello seguenti quattro algoritmi di machine learning prototipo hello toobuild (alcuna personalizzazione):  

1. Regressione logistica (LR)
2. Albero delle decisioni incrementato (BT)
3. Percezione media (AP)
4. Macchina a vettori di supporto (SVM)  

Hello seguente diagramma viene illustrata una parte dell'area di progettazione esperimento hello, che indica la sequenza di hello in cui hello sono stati creati modelli:  

![][6]  

*Figura 8: Creazione di modelli in Machine Learning Studio*  

### <a name="scoring-methods"></a>Metodi di assegnazione delle valutazioni
Viene calcolato il punteggio modelli hello quattro usando un set di dati di training con etichette.  

È stata inviata anche hello valutazione confrontabili modello compilato tramite hello desktop edition SAS Enterprise Miner 12 tooa set di dati. È misurata accuratezza hello del modello di firma di accesso condiviso hello e di tutti e quattro i modelli di Machine Learning Studio.  

## <a name="results"></a>Risultati
In questa sezione viene presentato il nostro conclusioni sull'accuratezza hello dei modelli di hello, basati su set di dati di punteggio hello.  

### <a name="accuracy-and-precision-of-scoring"></a>Accuratezza e precisione dei valori
Implementazione di hello in Azure Machine Learning è in genere, dietro SAS offre una precisione di circa 10-15% (Area nella curva o AUC).  

Tuttavia, metrica più importante di hello la varianza sono tasso di classificazione non corretta di hello:, ovvero di churners delle prime N hello come stimato dal classificatore hello, quali di essi ha effettivamente **non** varianza e ancora ricevuto un trattamento speciale? hello il diagramma seguente Confronta questo tasso di classificazione non corretta per tutti i modelli di hello:  

![][7]

*Figure 9: Area sottesa dalla curva del prototipo Passau*

### <a name="using-auc-toocompare-results"></a>Utilizzo dei risultati toocompare AUC
Area nella curva (AUC) è un parametro che rappresenta una misura globale di *separability* tra distribuzioni hello di punteggi per popolamenti positivi e negativi. È simile grafico ricevitore operatore caratteristica (ROC) tradizionale di toohello, ma una differenza importante è che metrica AUC hello richiede toochoose un valore soglia. Invece riepiloga i risultati di hello su **tutti** scelte possibili. Al contrario, grafico ROC tradizionale hello Mostra tasso positivo hello asse verticale hello e hello false tasso di positivi sull'asse orizzontale hello e hello classificazione soglia varia.   

AUC è in genere utilizzato come misura di vale la pena per diversi algoritmi (o sistemi diversi) poiché consente di confrontare tramite i relativi valori AUC toobe di modelli. Si tratta di un approccio comune in settori come la meteorologia e la bioscienza. AUC rappresenta quindi uno strumento popolare per la gestione delle prestazioni dei classificatori.  

### <a name="comparing-misclassification-rates"></a>Confronto dei tassi di classificazione non corretta
Velocità di classificazione non corretta di hello in hello set di dati in questione è confrontati utilizzando i dati CRM hello di circa 8.000 sottoscrizioni.  

* frequenza di classificazione non corretta di Hello SAS è 10-15%.
* frequenza di classificazione non corretta di Machine Learning Studio Hello è 15-20% per churners top 200-300 hello.  

In base al settore telecomunicazioni hello, è importante tooaddress solo i clienti che dispongono di hello toochurn rischio più elevato offrendo loro un servizio concierge o un trattamento speciale. In questo senso, implementazione di Machine Learning Studio hello si ottiene risultati coerente con il modello di firma di accesso condiviso hello.  

Da hello stesso token, l'accuratezza è più importante della precisione in quanto si intende principalmente correttamente la classificazione churners potenziale.  

Hello seguente diagramma da Wikipedia viene illustrata la relazione hello in un elemento grafico brillante, per comprendere:  

![][8]

*Figura 10: Compromesso tra accuratezza e precisione*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Risultati di accuratezza e precisione per il modello di albero decisionale incrementato
Hello seguente grafico visualizza hello raw risultante dalla valutazione utilizzando il prototipo di Machine Learning hello per hello con Boosting modello decision Trees, che avviene hello toobe più accurato tra quattro modelli di hello:  

![][9]

*Figure 11: modello di albero delle decisioni con boosting*

## <a name="performance-comparison"></a>Confronto delle prestazioni
Abbiamo confrontato velocità hello in corrispondenza del quale è stato scored dati utilizzando modelli di Machine Learning Studio hello e un modello confrontabile creato utilizzando hello desktop edition SAS Enterprise Miner 12.1.  

Hello nella tabella seguente vengono riepilogate le prestazioni di hello degli algoritmi hello:  

*Tabella 1. Prestazioni generali (precisione) degli algoritmi hello*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Modello medio |il modello migliore Hello |Prestazioni scarse |Modello medio |

modelli di Hello ospitati in Machine Learning Studio buoni SAS 15-25% per la velocità di esecuzione, ma la precisione è stata ampiamente Equilibra.  

## <a name="discussion-and-recommendations"></a>Discussione e raccomandazioni
In base al settore telecomunicazioni hello, diverse procedure consigliate sono emersi tooanalyze varianza, tra cui:  

* Derivare metriche per quattro categorie fondamentali:
  * **Entità (ad esempio, una sottoscrizione)**. Eseguire il provisioning di informazioni di base su sottoscrizione hello e/o i clienti che sono soggetto hello di varianza.
  * **Attività**. Ottenere tutte le informazioni sull'utilizzo di possibili sono entità toohello correlati, ad esempio, numero di hello degli account di accesso.
  * **Supporto tecnico**. Raccogliere informazioni dal cliente supporto registri tooindicate eventuale sottoscrizione hello interazioni con il cliente o problemi di supporto.
  * **Dati commerciali e competitivi**. Ottenere informazioni possibili sui clienti hello (ad esempio, può essere tootrack non disponibile o disco).
* Utilizza la selezione di funzionalità toodrive importanza. Ciò implica che il modello di albero delle decisioni con Boosting hello è sempre un approccio promessa.  

Hello utilizzo di questi quattro categorie crea hello illusione che una semplice *deterministica* approccio, in base a indici corretto in base a fattori ragionevole per categoria, dovrebbe essere sufficiente tooidentify clienti al rischio di varianza. Sfortunatamente, per quanto questa nozione appaia plausibile, si tratta di un intendimento errato. motivo di Hello è che la varianza è un effetto temporale e fattori hello toochurn sono in genere negli Stati transitori. Comportare un cliente tooconsider lasciando oggi potrebbe essere diversi domani e certamente sarà diverso sei mesi da adesso. Pertanto, un modello *probabilistico* è una necessità.  

Questa osservazione importante è spesso trascurata in azienda, che in genere si preferisce un tooanalytics approccio orientato ai intelligence aziendali, soprattutto perché è un semplice vendere e ammette automazione semplice.  

Tuttavia, promessa hello di analitica self-service tramite Machine Learning Studio è che le quattro categorie di hello di informazioni, sono compatibili per reparto, diventano un'origine importante per machine learning sulla varianza.  

Un'altra funzionalità interessante presto in Azure Machine Learning è hello possibilità tooadd un repository toohello modulo personalizzato dei moduli predefiniti che sono già disponibili. Questa funzionalità, in pratica, crea un'opportunità tooselect librerie e creare modelli per i mercati verticali. È un'importante differenza di Azure Machine Learning hello mercato.  

Ci auguriamo che toocontinue in questo argomento in analitica dei dati di hello toobig future, in particolare correlati.
  

## <a name="conclusion"></a>Conclusioni
Questo documento descrive un problema comune di hello tootackling sottoposte di varianza del cliente tramite un framework generico. Viene considerato un prototipo per la valutazione dei modelli ed è implementato utilizzando Azure Machine Learning. Infine, viene valutata accuratezza hello e prestazioni della soluzione di prototipo hello con gli algoritmi toocomparable conto nella firma di accesso condiviso.  

**Per altre informazioni:**  

Il documento è stato di aiuto? Gradiremmo ricevere commenti e suggerimenti. Informazioni su una scala da 1 too5 (scarso) (eccellente), valutazione questo white paper e perché assegnare questa valutazione? ad esempio:  

* La valutazione è alta scadenza toohaving buoni esempi, catture di schermata eccellenti, spiegazioni chiare o per altri motivi?
* La valutazione è bassa scadenza toopoor esempi, catture di schermata fuzzy o poco chiaro?  

Questi commenti e suggerimenti ci aiuteranno a migliorare la qualità della documentazione pubblicata hello.   

[Invia commenti e suggerimenti](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Riferimenti
[1] Analitica predittiva: oltre stime hello, w. McKnight, gestione, luglio/agosto 2011, p.18 a 20.  

[2] Articolo di Wikipedia relativo all'[accuratezza e alla precisione](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0: Guida dettagliata sul data mining](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [Big Data Marketing: coinvolgere i clienti e valorizzare i prodotti in modo più efficace](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) (Modello di varianza Telco) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Appendice
![][10]

*Figura 12: Snapshot di una presentazione sul prototipo di varianza*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
