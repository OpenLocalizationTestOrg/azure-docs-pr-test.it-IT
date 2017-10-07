---
title: aaaExecute Python apprendimento script | Documenti Microsoft
description: "Descrive i principi di progettazione di base per gli script Python in Azure Machine Learning nonché gli scenari di utilizzo di base, le funzionalità e le limitazioni."
keywords: apprendimento automatico di python, pandas, pandas di python, script di python, eseguire gli script di python
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ee9eb764-0d3e-4104-a797-19fc29345d39
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bradsev
ms.openlocfilehash: 8d23aaa972a46cb1a07ea0f18cc1e24933fe3e6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="execute-python-machine-learning-scripts-in-azure-machine-learning-studio"></a>Eseguire gli script di apprendimento automatico di Python in Azure Machine Learning Studio

Questo argomento descrive i principi di progettazione hello hello supporto corrente per gli script Python in Azure Machine Learning. vengono inoltre descritte fornita la funzionalità principale Hello, inclusi:

- Esecuzione di scenari di utilizzo di base
- Assegnazione di punteggi a un esperimento in un servizio Web
- Supporto per l'importazione di codice esistente
- Esportazione delle visualizzazioni
- Selezione delle funzionalità con supervisione
- Informazioni su alcune limitazioni

[Python](https://www.python.org/) è uno strumento indispensabile hello strumento un'occasione eccezionale molti esperti di dati. Le sue caratteristiche sono:

* una sintassi elegante e concisa; 
* il supporto multipiattaforma; 
* un'ampia raccolta di librerie complete; 
* strumenti di sviluppo avanzati. 

Python viene usato in tutte le fasi di un flusso di lavoro usato in genere nella modellazione di Machine Learning:

- Inserimento ed elaborazione dei dati 
- Costruzione delle funzionalità
- Training dei modelli 
- Convalida dei modelli
- distribuzione di modelli di hello

Azure Machine Learning Studio supporta l'incorporamento di script Python in varie parti di un esperimento di apprendimento automatico, nonché la relativa pubblicazione diretta come servizi Web in Microsoft Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


## <a name="design-principles-of-python-scripts-in-machine-learning"></a>Principi di progettazione degli script Python in Machine Learning

tooPython interfaccia primaria Hello in Azure Machine Learning Studio è tramite hello [Execute Python Script] [ execute-python-script] modulo illustrato nella figura 1.

![Immagine1](./media/machine-learning-execute-python-scripts/execute-machine-learning-python-scripts-module.png)

![Immagine2](./media/machine-learning-execute-python-scripts/embedded-machine-learning-python-script.png)

Figura 1. Hello **Execute Python Script** modulo.

Hello [Execute Python Script] [ execute-python-script] modulo in Azure Machine Learning Studio accetta l'input toothree e produce backup output tootwo (descritto nella seguente sezione hello), ad esempio, il relativo analogico R hello [ Eseguire lo Script R] [ execute-r-script] modulo. Hello toobe codice Python eseguita viene immesso nella casella del parametro hello come speciale denominata funzione di punto di ingresso `azureml_main`. Di seguito sono hello chiave della progettazione principi utilizzato tooimplement questo modulo.

1. *Deve essere idiomatico per gli utenti di Python.* La maggior parte degli utenti di Python struttura il codice come funzioni nei moduli. L'inserimento di un numero elevato di istruzioni eseguibili in un modo di primo livello è quindi relativamente raro. Di conseguenza, casella script hello accetta inoltre una funzione di Python appositamente denominata come toojust anziché una sequenza di istruzioni. Hello oggetti esposti nella funzione hello sono tipi di raccolta standard Python come [Pandas](http://pandas.pydata.org/) frame di dati e [NumPy](http://www.numpy.org/) matrici.
2. *Deve avere un alto livello di fedeltà tra le esecuzioni locali e nel cloud.* Hello hello tooexecute back-end utilizzato codice Python è basato su [Anaconda](https://store.continuum.io/cshop/anaconda/), ampiamente utilizzato distribuzione Python di scientifici multipiattaforma. È dotato di chiusura too200 dei pacchetti Python più comuni di hello. Di conseguenza, i professionisti possono eseguire il debug e qualificare il codice nel proprio ambiente Anaconda locale compatibile con Machine Learning di Azure. Quindi utilizzare un ambiente di sviluppo esistenti, ad esempio [IPython](http://ipython.org/) notebook o [Python Tools per Visual Studio](http://aka.ms/ptvs), toorun come parte di un esperimento di Azure ML. Hello `azureml_main` punto di ingresso è una funzione di Python vaniglia e pertanto * * * possono essere creati senza codice specifico per Azure ML o hello SDK installato.
3. *Deve essere facilmente componibile con altri moduli di Azure Machine Learning.* Hello [Execute Python Script] [ execute-python-script] modulo accetta come input e output, i set di dati standard di Azure Machine Learning. il framework sottostante Hello in modo trasparente ed efficace colma il runtime di Azure ML e Python hello. È quindi possibile usare Python in combinazione ai flussi di lavoro di Azure Machine Learning esistenti, inclusi quelli che effettuano chiamate in R e SQLite. Un data scientist può quindi creare flussi di lavoro che consentono di eseguire le operazioni seguenti:
   * Uso di Python e Pandas per la pre-elaborazione e la pulizia dei dati.
   * feed hello tooa SQL la trasformazione dei dati, aggiunta di funzionalità di tooform più set di dati
   * eseguire il training di modelli utilizzando algoritmi hello in Azure Machine Learning 
   * valutare e post-elaborazione dei risultati di hello con R.


## <a name="basic-usage-scenarios-in-ml-for-python-scripts"></a>Scenari di utilizzo di base in Machine Learning per gli script Python

In questa sezione, rivolto il sondaggio alcuni degli utilizzi di base hello di hello [Execute Python Script] [ execute-python-script] modulo. Modulo di input toohello Python vengono esposti come frame di dati Pandas. Hello funzione deve restituire un singolo frame di dati Pandas incluso nel pacchetto all'interno di un Python [sequenza](https://docs.python.org/2/c-api/sequence.html) , ad esempio una tupla, elenco o una matrice NumPy. primo elemento di Hello di questa sequenza viene quindi restituito nella porta di output del modulo hello prima hello. Questo schema è illustrato nella figura 2.

![Immagine3](./media/machine-learning-execute-python-scripts/map-of-python-script-inputs-outputs.png)

Figura 2. Mapping di tooparameters porte di input e restituiscono valori toooutput porta.

La semantica di come porte di input hello ottengono tooparameters mappata di hello dettagliate `azureml_main` funzione vengono visualizzati nella tabella 1:

![Immagine1T](./media/machine-learning-execute-python-scripts/python-script-inputs-mapped-to-parameters.png)

Tabella 1. Mapping dei parametri toofunction porte di input.

mapping di Hello tra porte di input e i parametri della funzione è posizionale:

- porta di input connessi prima Hello è mappato toohello primo parametro della funzione hello. 
- Hello secondo input (se connessi) è mappata toohello secondo parametro della funzione hello.

Vedere *Python per analisi dei dati* (o ' Reilly, 2012) da McKinney occ. Per ulteriori informazioni su Pandas Python e su come può essere utilizzato toomanipulate dati in modo efficace ed efficiente. 


## <a name="translation-of-input-and-output-types"></a>Conversione dei tipi di input e di output 
Set di dati di input in Azure Machine Learning sono fotogrammi Pandas toodata convertito. Frame di dati di output vengono convertiti i set di dati di back-tooAzure ML. Hello dopo le conversioni viene eseguita:

1. Le colonne stringa e numerici vengono convertite come-è e i valori mancanti in un set di dati vengono convertiti too'NA' i valori in Pandas. Hello stessa conversione viene eseguita nel modo nuovamente hello (valori NA Pandas sono valori toomissing convertito in Azure Machine Learning).
2. I vettori indice di Pandas non sono supportati in Azure Machine Learning. Tutti i frame di dati di input nella funzione di Python hello hanno sempre un indice numerico a 64 bit da 0 toohello numero di righe meno 1. 
3. I set di dati di Azure Machine Learning non possono avere nomi di colonna duplicati e diversi da stringhe. Se un frame di dati di output contiene le colonne non numeriche, hello framework chiama `str` sui nomi di colonna hello. Analogamente, nomi di colonna duplicati vengono automaticamente alterato tooinsure hello nomi siano univoci. toohello primo duplicato, toohello secondo duplicato (3) e così via, viene aggiunto il suffisso di Hello (2).


## <a name="operationalizing-python-scripts"></a>Rendere operativi gli script Python

Tutti i moduli [Execute Python Script][execute-python-script] (Esegui script Python) usati in un esperimento di assegnazione dei punteggi vengono chiamati al momento della pubblicazione come servizio Web. Ad esempio, la figura 3 mostra un esperimento di assegnazione dei punteggi contenente tooevaluate codice hello un'unica espressione Python. 

![Immagine4](./media/machine-learning-execute-python-scripts/figure3a.png)

![Immagine5](./media/machine-learning-execute-python-scripts/python-script-with-python-pandas.png)

Figura 3. Servizio Web per la valutazione di un'espressione Python.

Un servizio Web creato da questo esperimento:

- Accetta come input un'espressione Python, come stringa.
- Invia l'interprete Python toohello 
- Restituisce una tabella che contiene espressioni hello sia risultato hello valutata.


## <a name="importing-existing-python-script-modules"></a>Importazione di moduli di script Python esistenti

Un caso di utilizzo comune per molti esperti di dati è script Python esistenti tooincorporate negli esperimenti di Machine Learning di Azure. Anziché richiedere che tutto il codice deve essere concatenato e incollato in una casella singolo script, hello [Execute Python Script] [ execute-python-script] modulo accetta un file zip che contiene i moduli Python sulla porta di input terzo hello. file Hello è stato decompresso da framework di esecuzione hello in fase di esecuzione e il contenuto di hello viene aggiunto il percorso di libreria toohello dell'interprete Python hello. Hello `azureml_main` punto di ingresso funzione quindi possibile importare direttamente questi moduli.

Ad esempio, prendere in considerazione file hello Hello.py contenente una funzione semplice "Hello, World".

![Immagine6](./media/machine-learning-execute-python-scripts/figure4.png)

Figura 4. Funzione definita dall'utente nel file Hello.py.

Viene quindi creato un file Hello.zip contenente Hello.py:

![Immagine7](./media/machine-learning-execute-python-scripts/figure5.png)

Figura 5. File ZIP contenente codice Python definito dall'utente.

In Azure Machine Learning Studio, caricare il file zip hello come set di dati. Quindi creare ed eseguire un esperimento che usi il codice Python di hello nel file Hello.zip hello mediante l'aggiunta di toohello terza porta di input di hello **Execute Python Script** modulo, come illustrato nella figura seguente.

![Immagine8](./media/machine-learning-execute-python-scripts/figure6a.png)

![Immagine9](./media/machine-learning-execute-python-scripts/figure6b.png)

Figura 6. Esperimento di esempio con codice Python definito dall'utente caricato come file ZIP.

output del modulo Hello viene illustrato il file zip hello è stato decompresso e tale funzione hello `print_hello` è stato eseguito.
 
![image10](./media/machine-learning-execute-python-scripts/figure7.png)

Figura 7. Funzione definita dall'utente in uso all'interno di hello [Execute Python Script] [ execute-python-script] modulo.


## <a name="working-with-visualizations"></a>Utilizzo di visualizzazioni

I grafici creati usando MatplotLib che possono essere visualizzati in browser hello possono essere restituiti da hello [Execute Python Script][execute-python-script]. Ma hello grafici non sono automaticamente reindirizzato tooimages come quando si usa R. Utente hello deve esplicitamente salvare qualsiasi tracciati tooPNG file se sono toobe restituito tooAzure indietro Machine Learning. 

immagine di toogenerate da MatplotLib, è necessario completare hello seguente procedura:

* switch back-end hello troppo "AGG" da hello predefinito basato su Qt renderer 
* Creare un nuovo oggetto figura. 
* ottenere asse hello e generare grafici tutti al suo interno 
* salvare file PNG di hello figura tooa 

Questo processo è illustrato nella seguente figura 8 che crea una matrice di tracciato dispersione funzione scatter_matrix hello in Pandas hello.

![Immagine1v](./media/machine-learning-execute-python-scripts/figure-v1-8.png)

Figura 8. Toosave che matplotlib figure tooimages del codice.

Figura 9 è illustrato un esperimento che usi script hello illustrato in precedenza tooreturn rappresentata tramite la porta di output secondo hello.

![Immagine2v](./media/machine-learning-execute-python-scripts/figure-v2-9a.png) 

![Immagine2v](./media/machine-learning-execute-python-scripts/figure-v2-9b.png) 

Figura 9. Visualizzazione di tracciati generati da codice Python.

È possibili tooreturn più figure salvando i file in immagini differenti, hello Azure Machine Learning runtime preleva tutte le immagini e concatenati per la visualizzazione.


## <a name="advanced-examples"></a>Esempi avanzati

ambiente Anaconda Hello installato in Azure Machine Learning contiene pacchetti comuni, ad esempio NumPy, SciPy e Scikits-Learn. Questi pacchetti possono essere usati in modo efficace per diverse attività di elaborazione dei dati in una pipeline di Machine Learning. Ad esempio, hello script ed esperimento seguente viene illustrato hello utilizzo di strumenti di apprendimento dell'insieme di punteggi di importanza funzionalità toocompute Scikits-Learn per un set di dati. punteggi Hello possono essere utilizzato tooperform sotto la supervisione di selezione funzionalità prima di essere inseriti in un altro modello ML.

Ecco i punteggi di importanza hello toocompute funzione usato Python hello e funzionalità di hello ordine in base ai punteggi hello:

![Immagine11](./media/machine-learning-execute-python-scripts/figure8.png)

Figura 10. Funzione toorank funzionalità punteggi.
 Hello seguente esperimento quindi calcola e restituisce i punteggi di importanza hello di funzionalità nel set di dati "Pima indiano diabete" hello in Azure Machine Learning:

![image12](./media/machine-learning-execute-python-scripts/figure9a.png)
![image13](./media/machine-learning-execute-python-scripts/figure9b.png)    

Figura 11. Funzionalità di toorank esperimento hello Pima indiano diabete DataSet.

## <a name="limitations"></a>Limitazioni
Hello [Execute Python Script] [ execute-python-script] dispone attualmente di hello limitazioni seguenti:

1. *Esecuzione in modalità sandbox.* il runtime di Python Hello è attualmente in modalità sandbox e, di conseguenza, non consente l'accesso toohello toohello rete o del file system locale in modo permanente. Tutti i file salvati in locale sono isolati ed eliminati una volta terminato il modulo hello. Hello codice Python non può accedere la maggior parte delle directory nel computer di hello che è in esecuzione, viene eccezione hello hello directory corrente e nelle relative sottodirectory.
2. *Mancanza di supporto avanzato per sviluppo e debug.* modulo di Python Hello attualmente non supporta le funzionalità IDE quali intellisense il debug. Inoltre, se il modulo di hello non riesce in fase di esecuzione, hello Python completo dello stack è disponibile. Ma deve essere visualizzata nel log di output di hello per modulo hello. Attualmente si consiglia di sviluppare e debug di script Python in un ambiente come IPython e quindi importare codice hello nel modulo di hello.
3. *Output di un singolo frame di dati.* punto di ingresso Python Hello è consentito tooreturn solo un frame di dati singolo come output. Non è attualmente possibile tooreturn che Python arbitrario oggetti, ad esempio i modelli con training eseguire direttamente il runtime di Azure Machine Learning toohello. Ad esempio [Execute R Script][execute-r-script], che dispone di hello stessa limitazione, è possibile in molti casi toopickle oggetti in un byte di matrice e quindi restituiscono che all'interno di un frame di dati.
4. *Impossibilità toocustomize installazione Python*. Attualmente, hello solo modo tooadd Python moduli personalizzati sia dal meccanismo di file zip hello descritto in precedenza. Anche se ciò è fattibile per i moduli piccoli, risulta complesso per quelli grandi, specialmente quelli con DLL native o un numero elevato di moduli. 

## <a name="conclusions"></a>Conclusioni
Hello [Execute Python Script] [ execute-python-script] modulo consente un esperto di dati codice Python esistente tooincorporate nei flussi di lavoro learning computer basati su cloud in Azure Machine Learning e tooseamlessly rendere operativo come parte di un servizio web. modulo di script Python Hello interagisce naturalmente con altri moduli in Azure Machine Learning. modulo Hello può essere utilizzato per una gamma di attività da elaborazione toopre l'esplorazione dei dati e l'estrazione, funzionalità e quindi tooevaluation e post-elaborazione dei risultati di hello. il runtime di back-end Hello utilizzato per l'esecuzione si basa su Anaconda, una distribuzione di Python testata e ampiamente usata. Il back-end rende più semplice per consentire le risorse di codice esistenti tooon Lavagna in cloud hello.

Prevediamo tooprovide funzionalità aggiuntive toohello [Execute Python Script] [ execute-python-script] modulo, ad esempio hello tootrain possibilità e utilizzare i modelli di Python e tooadd supporto migliorato per hello sviluppo e debug del codice in Azure Machine Learning Studio.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](https://azure.microsoft.com/develop/python/).

<!-- Module References -->
[execute-python-script]: https://msdn.microsoft.com/library/azure/cdb56f95-7f4c-404d-bde7-5bb972e6f232/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
