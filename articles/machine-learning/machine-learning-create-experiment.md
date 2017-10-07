---
title: aaaA semplice esperimento in Machine Learning Studio | Documenti Microsoft
description: "Questa esercitazione di Machine Learning illustra un esperimento semplice di analisi scientifica dei dati. Si sarà stimare prezzo hello di un'automobile usando un algoritmo di regressione."
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
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a>Esercitazione di Machine Learning: Creare il primo esperimento di analisi scientifica dei dati in Azure Machine Learning Studio

Questa esercitazione è destinata agli utenti che non hanno mai usato **Azure Machine Learning Studio**.

In questa esercitazione verranno esaminati come toouse Studio hello per la prima volta toocreate un esperimento di machine learning. sperimentazione Hello testerà un modello analitico che stima il prezzo di hello di un'automobile in base alle diverse variabili, ad esempio le specifiche tecniche e verificare.

> [!NOTE]
> Questa esercitazione Mostra nozioni fondamentali di hello dei moduli come toodrag e rilascio nell'esperimento, collegarli, eseguire l'esperimento hello e visualizzare risultati hello. Non verrà toodiscuss hello argomento generale di machine learning o come tooselect e utilizzare hello 100 + dati e algoritmi manipolazione dei moduli predefiniti inclusi in Studio.
>
>Se si è nuovo learning toomachine, hello serie di video [analisi scientifica dei dati per i principianti](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) potrebbe essere toostart un buon punto. Questa serie di video è un learning toomachine introduzione grande utilizzando concetti e il linguaggio naturale.
>
>Se si ha familiarità con machine learning, ma si sta cercando le informazioni di carattere generale su Machine Learning Studio e hello algoritmi di machine learning che contiene, di seguito sono riportate alcune risorse validi:
>
- [Cos'è Machine Learning Studio?](machine-learning-what-is-ml-studio.md) : questa è una panoramica generale di Studio.
- [Nozioni di base con esempi di algoritmi di apprendimento computer](machine-learning-basics-infographic-with-algorithm-examples.md) -questo infografica è utile se si desidera toolearn informazioni sui diversi tipi di hello algoritmi di machine learning inclusi in Machine Learning Studio.
- [Machine Learning Guida](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) -questa guida vengono fornite le informazioni simili di hello infografica precedente, ma in un formato interattivo.
- [Machine learning foglio informativo algoritmo](machine-learning-algorithm-cheat-sheet.md) e [come algoritmi toochoose per Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) -questo articolo e il poster scaricabile discutere algoritmi Studio hello in profondità.
- [Machine Learning Studio: Algoritmo e modulo della Guida](https://msdn.microsoft.com/library/azure/dn905974.aspx) -si tratta di hello riferimento completo di tutti i moduli di Studio, inclusi gli algoritmi di machine learning,

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a>Vantaggi di Machine Learning Studio

Machine Learning Studio rende facile tooset di un esperimento usando i moduli di trascinamento e rilascio preprogrammati con le tecniche di modellazione predittiva.

L'uso di un'area di lavoro interattiva grafica consente di selezionare e trascinare ***set di dati*** e ***moduli*** di analisi in un'area di disegno interattiva. Si connette tooform insieme un ***sperimentare*** che vengono eseguiti in Machine Learning Studio.
Si ***creare un modello***, ***Training modello di hello***, e ***punteggio e test hello modello***.

È possibile eseguire l'iterazione sulla struttura del modello, la modifica di sperimentazione hello e si esegue fino a quando offre hello risultati che si sta cercando. Quando il modello è pronto, è possibile pubblicarlo come ***servizio Web*** in modo che altri utenti possano inviare nuovi dati e ottenere stime in cambio.

## <a name="open-machine-learning-studio"></a>Aprire Machine Learning Studio

tooget introduttiva Studio, andare troppo[https://studio.azureml.net](https://studio.azureml.net). Se è già stato effettuato l'accesso a Machine Learning Studio in precedenza, fare clic su **Sign In** (Accedi). In caso contrario fare clic su **Sign up here** (Effettuare l'iscrizione qui) e scegliere un'opzione gratuita o a pagamento.

![Accedi tooMachine Learning Studio][sign-in-to-studio]
<br/>
***Accedi tooMachine Learning Studio***

## <a name="five-steps-toocreate-an-experiment"></a>Cinque passaggi toocreate un esperimento

In questa esercitazione machine learning sarà seguire cinque passaggi di base toobuild un esperimento di Machine Learning Studio toocreate, eseguire il training e assegnare un punteggio del modello:

- **Creare un modello**
    - [Passaggio 1: Ottenere i dati]
    - [Passaggio 2: Preparare i dati di hello]
    - [Passaggio 3: Definire le caratteristiche]
- **Modello di hello Train**
    - [Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]
- **Punteggio e test hello modello**
    - [Passaggio 5: Stimare i prezzi delle nuove automobili]

[Passaggio 1: Ottenere i dati]: #step-1-get-data
[Passaggio 2: Preparare i dati di hello]: #step-2-prepare-the-data
[Passaggio 3: Definire le caratteristiche]: #step-3-define-features
[Passaggio 4: Scegliere e applicare un algoritmo di apprendimento]: #step-4-choose-and-apply-a-learning-algorithm
[Passaggio 5: Stimare i prezzi delle nuove automobili]: #step-5-predict-new-automobile-prices

> [!TIP] 
> È possibile trovare una copia di lavoro di hello seguente esperimento nella hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com). Andare troppo**[l'analisi scientifica dei dati prima di provare - stima prezzo Automobile](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**  e fare clic su **Open in Studio** toodownload una copia dell'esperimento hello nel Machine Learning Area di lavoro di Studio.


## <a name="step-1-get-data"></a>Passaggio 1: Ottenere i dati

Hello occorre innanzitutto tooperform l'apprendimento è dati.
In Machine Learning Studio sono disponibili numerosi set di dati di esempio da usare oppure è possibile importare dati da molte altre origini. In questo esempio utilizzeremo i set di dati campione hello, **dati prezzo Automobile (Raw)**, che è incluso nell'area di lavoro.
Questo set di dati include voci per diverse automobili e include informazioni su marca, modello, specifiche tecniche e prezzo.

Ecco come tooget hello set di dati nell'esperimento.

1. Creare un nuovo esperimento facendo **+ nuovo** nella parte inferiore di hello della finestra di Machine Learning Studio hello, selezionare **SPERIMENTARE**, quindi selezionare **sperimentare vuoto**.

2. sperimentazione Hello viene assegnato un nome predefinito visualizzato nella parte superiore di hello dell'area di disegno hello. Selezionare il testo e rinominarlo toosomething significativo, ad esempio, **stima prezzo Automobile**. nome Hello non deve necessariamente toobe univoco.

    ![Rinominare l'esperimento hello][rename-experiment]

2. toohello a sinistra dell'area di disegno esperimento hello è una tavolozza dei moduli e dei set di dati. Tipo **automobile** nella casella di ricerca hello nella parte superiore di hello del dataset hello toofind tavolozza con etichettato **dati prezzo Automobile (Raw)**. Trascinare l'area di disegno di set di dati toohello esperimento.

    ![Trovare set di dati automobili hello e trascinarlo nell'area di disegno esperimento hello][type-automobile]
    <br/>
    ***Trovare set di dati automobili hello e trascinarlo nell'area di disegno esperimento hello***

toosee questo aspetto dati like, fare clic sulla porta di output di hello nella parte inferiore di hello del set di dati automobili hello e quindi selezionare **Visualizza**.

![Fare clic sulla porta di output di hello e selezionare "Visualizza"][select-visualize]
<br/>
***Fare clic sulla porta di output di hello e selezionare "Visualizza"***

> [!TIP]
> Set di dati e i moduli con input e le porte di output rappresentate da cerchi piccoli - porte di input nella parte superiore di hello, porte nella parte inferiore di hello di output.
toocreate un flusso di dati attraverso l'esperimento, si accede di una porta di output della porta di input tooan un modulo di un altro.
In qualsiasi momento, è possibile scegliere quali dati hello sono simile a questo punto nel flusso di dati hello porta di output di hello del toosee set di dati o un modulo.

In questo set di dati di esempio, ogni istanza di un'automobile viene visualizzato come una riga e le variabili di hello associate a ogni automobile vengono visualizzati come colonne. Dato variabili hello di un'automobile specifica, verrà tootry toopredict hello prezzo colonna estrema destra "(price colonna 26, intitolata").

![Visualizzare i dati di un'automobile hello nella finestra di visualizzazione dati hello][visualize-auto-data]
<br/>
***Visualizzare i dati di un'automobile hello nella finestra di visualizzazione dati hello***

Finestra di visualizzazione hello Chiudi facendo hello "**x**" nell'angolo superiore destro di hello.

## <a name="step-2-prepare-hello-data"></a>Passaggio 2: Preparare i dati di hello

Prima di poter analizzare un set di dati è in genere necessario pre-elaborarlo. Ad esempio, è possibile aver notato hello i valori presenti nelle colonne di hello delle varie righe mancanti. Questi valori mancanti necessario toobe puliti quindi modello hello è possibile analizzare dati hello correttamente. In questo caso verranno rimosse le righe con i valori mancanti. Inoltre, hello **perdite normalizzato** colonna ha una proporzione elevata di valori mancanti, che dunque verrà escluso tale colonna dal modello hello completamente.

> [!TIP]
> Pulizia hello mancano i valori dei dati di input è un prerequisito per utilizzando la maggior parte dei moduli di hello.

Si aggiunge un modulo che rimuove hello **perdite normalizzato** colonna completamente, quindi è aggiungere un altro modulo che rimuove tutte le righe che mancano alcuni dati.

1. Tipo **selezionare colonne** nella casella di ricerca hello nella parte superiore di hello di hello toofind tavolozza di hello modulo [selezionare le colonne nel set di dati] [ select-columns] modulo, quindi trascinarlo toohello esperimento canvas . Questo modulo consente tooselect quali colonne di dati si desidera tooinclude o escludere hello modello.

2. Connettere hello porta di output di hello **dati prezzo Automobile (Raw)** toohello set di dati di input porta hello [selezionare le colonne nel set di dati] [ select-columns] modulo.

    ![Aggiungere l'area di disegno hello "Selezionare le colonne nel set di dati" modulo toohello sperimentazione e connetterla][type-select-columns]
    <br/>
    ***Aggiungere l'area di disegno hello "Selezionare le colonne nel set di dati" modulo toohello sperimentazione e connetterla***

3. Fare clic su hello [selezionare le colonne nel set di dati] [ select-columns] modulo e fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro.

    - A sinistra di hello, fare clic su **con regole**
    - In **Begin With** (Inizia con), fare clic su **All columns** (Tutte le colonne). In questo modo [selezionare le colonne nel set di dati] [ select-columns] toopass tramite tutte le colonne di hello (tranne le colonne siamo su tooexclude).
    - Hello elenchi a discesa, selezionare **escludere** e **i nomi delle colonne**e quindi fare clic nella casella di testo hello. Verrà visualizzato un elenco di colonne. Selezionare **perdite normalizzato**, e è aggiunto toohello casella di testo.
    - Fare clic sul selettore di colonna hello per la tooclose pulsante hello segno di spunta (OK) (in basso a destra hello).

    ![Avvia selettore di colonna hello ed escludere la colonna "perdite normalizzato" hello][launch-column-selector]
    <br/>
    ***Avvia selettore di colonna hello ed escludere la colonna "perdite normalizzato" hello***

    Riquadro delle proprietà ora hello per **selezionare le colonne nel set di dati** indica il passaggio attraverso tutte le colonne dal set di dati di hello tranne **perdite normalizzato**.

    ![riquadro Proprietà Hello mostra che colonna hello "perdite normalizzato" viene escluso][showing-excluded-column]
    <br/>
    ***riquadro Proprietà Hello mostra che colonna hello "perdite normalizzato" viene escluso***

    > [!TIP]
    È possibile aggiungere un modulo tooa commento facendo doppio clic su modulo hello e immissione di testo. Ciò consente di visualizzare a colpo d'occhio esegue il modulo hello nell'esperimento. In questo caso fare doppio clic su hello [selezionare le colonne nel set di dati] [ select-columns] modulo e il tipo hello commento "Exclude normalizzato perdite".
    >
    >


    ![Fare doppio clic su un tooadd modulo un commento][add-comment]
    <br/>
    ***Fare doppio clic su un tooadd modulo un commento***

3. Hello trascinare [Clean Missing Data] [ clean-missing-data] toohello modulo provare l'area di disegno e connetterla toohello [selezionare le colonne nel set di dati] [ select-columns] modulo. In hello **proprietà** riquadro, selezionare **Rimuovi intera riga** in **modalità di pulizia**. In questo modo [Clean Missing Data] [ clean-missing-data] dati hello tooclean rimuovendo le righe che contengono i valori mancanti. Fare doppio clic sul modulo hello e digitare il commento hello "Rimuovi righe valore mancante".

    ![Impostare la modalità di pulizia hello troppo "Rimuovi intera riga" per il modulo "Clean Missing Data" hello][set-remove-entire-row]
    <br/>
    ***Impostare la modalità di pulizia hello troppo "Rimuovi intera riga" per il modulo "Clean Missing Data" hello***

4. Eseguire l'esperimento hello facendo **eseguire** nella parte inferiore di hello della pagina hello.

    Al termine dell'esecuzione esperimento hello, tutti i moduli di hello hanno tooindicate un segno di spunta verde che è state completata. Si noti inoltre hello **al termine dell'esecuzione** stato nell'angolo superiore destro di hello.

![Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente][early-experiment-run]
<br/>
***Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente***

> [!TIP]
> Motivo per cui è stata eseguiamo esperimento hello ora? Per esperimento hello in esecuzione, le definizioni di colonna hello per i dati passano dal set di dati hello tramite hello [selezionare le colonne nel set di dati] [ select-columns] modulo e tramite hello [Clean Missing Data] [ clean-missing-data] modulo. Ciò significa che tutti i moduli la connessione è troppo[Clean Missing Data] [ clean-missing-data] anche avrà le stesse informazioni.

Svolto nella sperimentazione hello punto toothis è dati hello pulita. Se si desidera tooview hello pulito set di dati, fare clic su hello lasciato la porta di output di hello [Clean Missing Data] [ clean-missing-data] modulo e selezionare **Visualizza**. Si noti che hello **perdite normalizzato** colonna non viene più fornita e non sono presenti valori mancanti.

Ora che i dati di hello sono puliti, si è pronti toospecify quali funzionalità è archivieranno toouse nel modello predittivo hello.

## <a name="step-3-define-features"></a>Passaggio 3: Definire le caratteristiche

In Machine Learning le *caratteristiche* sono singole proprietà misurabili di un elemento a cui si è interessati. Nel set di dati corrente ogni riga rappresenta un'automobile e ogni colonna è una caratteristica di tale automobile.

Ricerca di un set ottimo di funzionalità per la creazione di un modello predittivo richiede informazioni sui problemi di hello e sperimentazione desiderate toosolve. Alcune funzionalità sono migliori per la stima destinazione hello rispetto ad altri. Alcune caratteristiche sono strettamente correlate ad altre e possono essere rimosse. Ad esempio, città mpg e autostrada mpg sono strettamente correlati in modo da poter mantenere uno e rimuovere altri hello senza stima hello in maniera significativa.

Creare ora un modello che utilizza un sottoinsieme di funzionalità hello nel set di dati. È possibile tornare più avanti e selezionare diverse funzionalità, eseguire nuovamente l'esperimento hello e vedere se si ottengono risultati migliori. Toostart, ma si proverà hello seguenti caratteristiche:

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. Trascinare un'altra [selezionare le colonne nel set di dati] [ select-columns] toohello modulo provare l'area di disegno. Connettersi a sinistra sulla porta di output di hello hello [Clean Missing Data] [ clean-missing-data] input toohello modulo di hello [selezionare le colonne nel set di dati] [ select-columns] modulo.

    ![Connettersi hello "Selezionare le colonne nel set di dati" toohello "Clean Missing Data" modulo][connect-clean-to-select]
    <br/>
    ***Connettersi hello "Selezionare le colonne nel set di dati" toohello "Clean Missing Data" modulo***

2. Fare doppio clic sul modulo hello e digitare "Selezionare le funzionalità per la stima."

2. Fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro.

3. Fare clic su **With rules**(Con regole).

4. In **Begin With** (Inizia con), fare clic su **No columns** (Nessuna colonna). Nella riga di filtro hello, selezionare **Include** e **i nomi delle colonne** e selezionare l'elenco di nomi di colonna nella casella di testo hello. In questo modo hello modulo toonot iterazione (funzionalità) tutte le colonne tranne quelle che si specificano hello.

5. Fare clic su hello segno di spunta (OK).

    ![Selezionare tooinclude colonne (funzionalità) hello nella stima hello][select-columns-to-include]
    <br/>
    ***Selezionare tooinclude colonne (funzionalità) hello nella stima hello***

Ciò produce un set di dati filtrato contenente solo le funzioni hello che desideriamo toohello toopass verrà usato nel passaggio successivo hello algoritmo di apprendimento. In seguito, è possibile tornare indietro e provare a selezionare caratteristiche diverse.

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a>Passaggio 4: Scegliere e applicare un algoritmo di apprendimento

Ora che i dati di hello sono pronti, la costruzione di un modello predittivo costituito training e test. Verrà usato il modello di dati tootrain hello e quindi verrà eseguito un test hello modello toosee la misura è in grado di toopredict prezzi.
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

*Classificazione* e *regressione* sono due tipi di algoritmi di Machine Learning sottoposti a supervisione. La classificazione stima una risposta da un set di categorie definito, ad esempio un colore (rosso, blu o verde). La regressione è toopredict usato un numero.

Dal momento che il prezzo toopredict, che è un numero, verrà utilizzato un algoritmo di regressione. Per questo esempio, verrà usato un modello *a regressione lineare* semplice.

> [!TIP]
> Se si desidera toolearn informazioni sui diversi tipi di algoritmi di machine learning e quando toouse loro, si potrebbe visualizzare video prima hello in hello analisi scientifica dei dati per serie di utenti meno esperti, [hello cinque domande risposte di analisi scientifica dei dati](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md). È anche possibile consultare hello infografica [computer nozioni di base con esempi di algoritmi di apprendimento](machine-learning-basics-infographic-with-algorithm-examples.md), o estrarlo hello [Machine learning foglio informativo algoritmo](machine-learning-algorithm-cheat-sheet.md).

Abbiamo Training modello di hello mediante l'assegnazione di un set di dati che include il prezzo di hello. modello Hello analizza dati hello e cercare le correlazioni tra le funzionalità di un'automobile e il prezzo. Quindi verrà eseguito un test del modello di hello - verrà assegnargli un set di funzionalità per automobili che si ha familiarità con e vedere come chiudere hello prevede prezzo di toopredicting hello noti.

Si userà i dati per il training del modello di hello e testarlo suddividendo dati hello in training e il testing di set di dati separato.

1. Selezionare e trascinare hello [dati divisi] [ split] toohello modulo provare l'area di disegno e connetterla toohello ultima [selezionare le colonne nel set di dati] [ select-columns] modulo.

2. Fare clic su hello [dati divisi] [ split] tooselect modulo è. Trovare hello **frazione di righe in hello set di dati di output prima** (in hello **proprietà** toohello riquadro a destra dell'area di disegno hello) e impostarlo too0.75. In questo modo, verrà usata al 75% hello tootrain hello di modello di data e contenere il 25% per il testing (in un secondo momento, è possibile sperimentare con diverse percentuali).

    ![Set hello dividere frazione di hello "Suddivisione dei dati" modulo too0.75][set-split-data-percentage]
    <br/>
    ***Set hello dividere frazione di hello "Suddivisione dei dati" modulo too0.75***

    > [!TIP]
    > Modificando hello **Random seed** parametro, è possibile produrre diversi campioni casuale per il training e testing. Questo parametro controlla il seeding del generatore di numeri pseudo-casuali hello hello.

2. Eseguire l'esperimento hello. Quando viene eseguito l'esperimento hello, hello [selezionare le colonne nel set di dati] [ select-columns] e [dati divisi] [ split] moduli passare toohello le definizioni di colonna moduli che verranno aggiunte successivamente.  

3. hello tooselect, algoritmo di apprendimento espandere hello **Machine Learning** categoria hello modulo tavolozza toohello a sinistra di hello area di disegno e quindi espandere **inizializzare modello**. Consente di visualizzare diverse categorie di moduli che possono essere algoritmi utilizzati tooinitialize machine learning. Per questo esercizio, selezionare hello [Linear Regression] [ linear-regression] modulo in hello **regressione** categoria e trascinarlo toohello esperimento canvas.
(È possibile anche trovare hello modulo digitando "linear regression" nella casella di ricerca tavolozza hello.)

4. Individuare e trascinare hello [Train Model] [ train-model] toohello modulo provare l'area di disegno. Connettere l'output di hello di hello [Linear Regression] [ linear-regression] toohello modulo lasciato input di hello [Train Model] [ train-model] modulo e connettersi hello la formazione di output dei dati (porta a sinistra) di hello [dati divisi] [ split] input di destra toohello modulo di hello [Train Model] [ train-model] modulo.

    ![Connettersi hello "Train Model" modulo tooboth hello "Linear Regression" e "Suddivisione dei dati" moduli][connect-train-model]
    <br/>
    ***Connettersi hello "Train Model" modulo tooboth hello "Linear Regression" e "Suddivisione dei dati" moduli***

5. Fare clic su hello [Train Model] [ train-model] modulo, fare clic su **selettore di colonna avvio** in hello **proprietà** riquadro e quindi seleziona hello **prezzo** colonna. Questo è il valore di hello che il modello è toopredict continua.

    Si seleziona hello **prezzo** colonna nel selettore di colonna hello spostandola hello **colonne disponibili** elenco toohello **colonne selezionate** elenco.

    ![Selezionare una colonna prezzo hello per il modulo "Train Model" hello][select-price-column]
    <br/>
    ***Selezionare una colonna prezzo hello per il modulo "Train Model" hello***

6. Eseguire l'esperimento hello.

È ora disponibile un modello di regressione con training che può essere utilizzato tooscore nuove automobili dati toomake prezzo stime.

![Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente][second-experiment-run]
<br/>
***Dopo l'esecuzione, esperimento hello dovrebbe essere simile al seguente***

## <a name="step-5-predict-new-automobile-prices"></a>Passaggio 5: Stimare i prezzi delle nuove automobili

Ora che è stata Training modello di hello utilizzando pari al 75% dei dati, è possibile usarlo tooscore hello altri 25 percento hello dati toosee prestazioni nostri funzioni del modello.

1. Individuare e trascinare hello [Score Model] [ score-model] toohello modulo provare l'area di disegno. Connettere l'output di hello di hello [Train Model] [ train-model] toohello modulo porta di input di sinistra [Score Model][score-model]. Connettersi hello test output dei dati (porta a destra) di hello [dati divisi] [ split] porta di input destra toohello modulo [Score Model][score-model].

    ![Connettersi hello "Score Model" modulo tooboth hello "Train Model" e "Suddivisione dei dati" moduli][connect-score-model]
    <br/>
    ***Connettersi hello "Score Model" modulo tooboth hello "Train Model" e "Suddivisione dei dati" moduli***

2. Eseguire l'esperimento hello e visualizzare l'output di hello di hello [Score Model] [ score-model] modulo (fare clic sulla porta di output di hello del [Score Model] [ score-model] e selezionare **Visualizzare**). Mostra output di Hello hello valori stimati per prezzo e hello valori noti hello dei dati dei test.  

    ![Output di hello "Score Model" modulo][score-model-output]
    <br/>
    ***Output di hello "Score Model" modulo***

3. Infine, verranno testate qualità hello dei risultati di hello. Selezionare e trascinare hello [Evaluate Model] [ evaluate-model] toohello modulo provare l'area di disegno e connettere l'output di hello di hello [Score Model] [ score-model] modulo toohello input di sinistra [Evaluate Model][evaluate-model].

    > [!TIP]
    > Non sono presenti due porte di input in hello [Evaluate Model] [ evaluate-model] modulo poiché può essere utilizzato toocompare due modelli side-by. In un secondo momento, è possibile aggiungere un altro esperimento toohello di algoritmo e usare [Evaluate Model] [ evaluate-model] toosee quello che offre risultati migliori.

4. Eseguire l'esperimento hello.

output di hello tooview da hello [Evaluate Model] [ evaluate-model] modulo, fare clic sulla porta di output di hello e quindi selezionare **Visualizza**.

![Risultati della valutazione per esperimento hello][evaluation-results]
<br/>
***Risultati della valutazione per esperimento hello***

Hello seguendo le statistiche viene visualizzato per il nostro modello:

- **Errore assoluto medio** (MAE): hello media degli errori assoluti (un *errore* hello differenze hello previsto valore e il valore effettivo hello).
- **Errore quadratico medio radice** (RMSE): hello di radice quadrata della media hello di errori al quadrato di stime effettuate nel set di dati di hello test.
- **Errore assoluto relativo**: hello Media errori assoluto relativo toohello assoluto basso tra i valori effettivi e Media hello di tutti i valori effettivi.
- **Errore quadratico relativo**: Media hello di errori al quadrato relativo toohello al quadrato differenza tra i valori effettivi hello e Media hello di tutti i valori effettivi.
- **Coefficiente di determinazione**: anche noto come hello **R al quadrato valore**, si tratta di una metrica statistica che indica l'idoneità un modello di rapporto dati hello.

Per ogni errore hello statistiche, più piccolo sono consigliabile. Un valore inferiore indica che le stime hello corrispondano maggiormente i valori effettivi hello. Per **coefficiente di determinazione**, hello più vicino il relativo valore è tooone (1.0), stime hello migliori hello.

## <a name="final-experiment"></a>Esperimento finale

sperimentazione finale Hello dovrebbe essere simile al seguente:

![sperimentazione finale Hello][complete-linear-regression-experiment]
<br/>
***sperimentazione finale Hello***

## <a name="next-steps"></a>Passaggi successivi

Ora che si aver completato l'esercitazione di hello prima machine learning e imposta esperimento, è possibile continuare il modello di hello tooimprove e quindi distribuirla come servizio web predittivo.

- **Eseguire l'iterazione del modello di hello tooimprove tootry** -ad esempio, è possibile modificare le funzionalità di hello è utilizzare la stima. Oppure è possibile modificare le proprietà di hello di hello [Linear Regression] [ linear-regression] algoritmo o tenta di tutto un algoritmo diverso. È anche possibile aggiungere più esperimento di machine learning algoritmi tooyour in una sola volta e confrontare i due di essi utilizzando hello [Evaluate Model] [ evaluate-model] modulo.
Per un esempio di come toocompare più modelli in un esperimento singolo, vedere [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).

    > [!TIP]
    > toocopy qualsiasi iterazione dell'esperimento, utilizzare hello **SAVE AS** pulsante nella parte inferiore di hello della pagina hello. È possibile visualizzare tutte le iterazioni di hello dell'esperimento facendo **Visualizza cronologia di esecuzione** nella parte inferiore di hello della pagina hello. Per altre informazioni, vedere [Gestire iterazioni dell'esperimento in Azure Machine Learning Studio][runhistory].

[runhistory]: machine-learning-manage-experiment-iterations.md

- **Distribuire il modello di hello come un servizio web predittivo** : quando si è soddisfatti del modello, è possibile distribuire un toobe di servizio web utilizzato prezzi delle automobili toopredict utilizzando nuovi dati. Per altre informazioni dettagliate, vedere [Distribuire un servizio Web di Azure Machine Learning][publish].

[publish]: machine-learning-publish-a-machine-learning-web-service.md

Desidera toolearn altre? Per una procedura dettagliata più ampia e dettagliata del processo di hello di creazione, training, valutazione e distribuzione di un modello, vedere [sviluppare una soluzione predittiva mediante Azure Machine Learning][walkthrough].

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

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
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
