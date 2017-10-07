---
title: esercitazione aaaQuickstart per il linguaggio R per Machine Learning | Documenti Microsoft
description: Utilizzare questa esercitazione tooget avviato rapidamente utilizzando il linguaggio R hello con Azure Machine Learning Studio toocreate una soluzione di previsione di programmazione R.
keywords: guida introduttiva, linguaggio r, linguaggio di programmazione r, esercitazione di programmazione r
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 99a3a0fd-b359-481a-b236-66868deccd96
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 9995f8728f4d7bf9a5c15412015e4cf769cdac96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-tutorial-for-hello-r-programming-language-for-azure-machine-learning"></a>Esercitazione di avvio rapido per linguaggio di programmazione hello R per Azure Machine Learning

<!-- Stephen F Elston, Ph.D. -->

## <a name="introduction"></a>Introduzione
Questa esercitazione rapida consente di avviare rapidamente l'estensione Azure Machine Learning tramite linguaggio di programmazione hello R. Seguire questa esercitazione toocreate di programmazione R, testare ed eseguire codice R in Azure Machine Learning. Quando si utilizza l'esercitazione, si creerà una soluzione completa di previsione utilizzando il linguaggio R hello in Azure Machine Learning.  

Microsoft Azure Machine Learning contiene molti moduli validi per Machine Learning e per la manipolazione dei dati. viene descritto il linguaggio R potente di Hello come hello lingua franca del analitica. Fortunatamente, analitica e modifica dei dati in Azure Machine Learning può essere esteso con R. Questa combinazione fornisce hello scalabilità e facilità di distribuzione di Azure Machine Learning con flessibilità hello e analitica complete di R.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

### <a name="forecasting-and-hello-dataset"></a>Set di dati di previsione e hello
La previsione è un metodo analitico molto utile e ampiamente distribuito. Intervallo da elaborare stime di vendita degli elementi stagionali, determinare i livelli di inventario ottimale, variabili macroeconomiche toopredicting utilizzi comuni. In genere, inoltre, viene eseguita con modelli in serie temporale.

Dati della serie temporale sono dati in cui i valori hello dispone di un indice di tempo. indice di fase Hello può essere regolare, ad esempio, ogni mese o ogni minuto o irregolari. Sui dati in serie temporale si basano i modelli in serie temporale. linguaggio di programmazione Hello R contiene un framework flessibile e completa analitica per i dati della serie temporale.

In questa esercitazione prenderemo in esame la produzione casearia in California, con i relativi dati sui prezzi. Questi dati includono informazioni mensile sul prezzo hello del file System fat latte, una merce benchmark e di produzione hello di diversi prodotti da latte.

dati Hello usati in questo articolo, insieme a script R, possono essere [scaricato da qui][download]. Questi dati è stato originariamente sintetizzati utilizzando le informazioni disponibili da hello università di Wisconsin in http://future.aae.wisc.edu/tab/production.html.

### <a name="organization"></a>Organizzazione
Abbiamo avanzamento attraverso diversi passaggi per comprendere come toocreate, test e di eseguire codice di manipolazione R analitica e i dati nell'ambiente di Azure Machine Learning hello.  

* Innanzitutto verrà illustrato l'utilizzo di linguaggio hello R nell'ambiente Azure Machine Learning Studio hello base hello.
* Quindi è stato toodiscussing vari aspetti dei / o per dati, il codice R e grafica nell'ambiente di Azure Machine Learning hello.
* Prima parte di hello della nostra soluzione previsione verrà quindi creato tramite la creazione di codice per la pulizia dei dati e la trasformazione.
* Con i dati preparati si eseguirà un'analisi delle correlazioni hello tra diverse variabili hello nel set di dati.
* Infine, verrà creato un modello di previsione in serie temporale (stagionale) per la produzione di latte.

## <a id="mlstudio"></a>Interagire con il linguaggio R in Machine Learning Studio
In questa sezione vengono illustrati alcuni concetti di base dell'interazione con il linguaggio di programmazione hello R nell'ambiente di Machine Learning Studio hello. il linguaggio R Hello offre un potente strumento toocreate personalizzato analitica e dati Modifica moduli nell'ambiente Azure Machine Learning hello.

Si utilizzerà codice R toodevelop, test e debug di RStudio su una scala di piccole dimensioni. Questo codice viene quindi Taglia e Incolla in un [Execute R Script] [ execute-r-script] modulo in Machine Learning Studio pronto toorun.  

### <a name="hello-execute-r-script-module"></a>modulo Execute R Script Hello
All'interno di Machine Learning Studio, gli script di R vengono eseguiti all'interno di hello [Execute R Script] [ execute-r-script] modulo. Un esempio di hello [Execute R Script] [ execute-r-script] modulo in Machine Learning Studio è illustrato nella figura 1.

 ![Linguaggio di programmazione R: modulo Execute R Script hello selezionato in Machine Learning Studio][1]

*Figura 1. ambiente di Machine Learning Studio Hello con modulo Execute R Script hello selezionato.*

Riferimento tooFigure 1, ecco alcuni dei componenti chiave di hello dell'ambiente di Machine Learning Studio hello per l'utilizzo di hello [Execute R Script] [ execute-r-script] modulo.

* i moduli di Hello nell'esperimento hello vengono visualizzati nel riquadro centrale hello.
* parte superiore di Hello del riquadro di destra hello contiene tooview una finestra e modificare gli script R.  
* parte inferiore di Hello del riquadro di destra vengono mostrate alcune proprietà di hello [Execute R Script][execute-r-script]. È possibile visualizzare i registri errori e l'output di hello facendo clic su aree sensibili appropriato hello di questo riquadro.

Verrà, naturalmente, preso hello [Execute R Script] [ execute-r-script] più dettagliatamente nel resto di hello di questo documento.

Quando si usano funzioni R complesse, è preferibile effettuare le operazioni di modifica, test e debug in RStudio. Come con qualsiasi altro software di sviluppo, inoltre, è opportuno estendere il codice in modo incrementale, così da poterlo verificare in piccoli e semplici casi di test. Tagliare e incollare le funzioni nella finestra di script R hello di hello [Execute R Script] [ execute-r-script] modulo. Questo approccio consente tooharness sia hello RStudio ambiente di sviluppo integrato (IDE) e hello potenza di Azure Machine Learning.  

#### <a name="execute-r-code"></a>Eseguire il codice R
Qualsiasi codice R in hello [Execute R Script] [ execute-r-script] modulo verrà eseguito quando si esegue l'esperimento hello facendo clic su hello **eseguire** pulsante. Al termine dell'esecuzione, un segno di spunta verrà visualizzato nella hello [Execute R Script] [ execute-r-script] icona.

#### <a name="defensive-r-coding-for-azure-machine-learning"></a>Codice R difensivo per Azure Machine Learning
Se si sviluppa un codice R per, ad esempio, un servizio Web usando Azure Machine Learning, è necessario pianificare in che modo il codice R gestirà gli input di dati imprevisti e le eccezioni. toomaintain chiarezza, non ho incluso perlopiù in modo hello di controllo o nella maggior parte degli esempi di codice hello illustrati di gestione delle eccezioni. Tuttavia, verranno forniti diversi esempi di funzioni che prevedono l'uso della capacità di gestione delle eccezioni di R.  

Se è necessario un trattamento più completato di gestione delle eccezioni di R, è consigliabile leggere le sezioni applicabili hello del libro hello da Wickham elencati nella [appendice B - approfondimento](#appendixb).

#### <a name="debug-and-test-r-in-machine-learning-studio"></a>Eseguire il debug e testare R in Machine Learning Studio
tooreiterate, consiglia di test e debug del codice R su una scala di piccole dimensioni in RStudio. Tuttavia, vi sono casi in cui è necessario tootrack i problemi di codice R in hello [Execute R Script] [ execute-r-script] stesso. Inoltre, è buona norma toocheck i risultati in Machine Learning Studio.

Output dell'esecuzione di hello del codice R e sulla piattaforma Azure Machine Learning hello si trova principalmente nel log. ma alcune informazioni aggiuntive possono essere presenti in error.log.  

Se si verifica un errore in Machine Learning Studio durante l'esecuzione del codice R, la prima linea di condotta deve essere toolook in error.log. Questo file può contenere toohelp i messaggi di errore utile per comprendere e correggere l'errore. tooview error.log, fare clic su **Visualizza log degli errori** su hello **riquadro proprietà** per hello [Execute R Script] [ execute-r-script] contenente l'errore hello.

Ad esempio, è stata eseguita hello seguente codice R, con una variabile y non definito in un [Execute R Script] [ execute-r-script] modulo:

    x <- 1.0
    z <- x + y

Questo codice non tooexecute, causando una condizione di errore. Facendo clic su **Visualizza log degli errori** su hello **riquadro proprietà** produce hello visualizzazione illustrato nella figura 2.

  ![Finestra di popup con messaggio di errore][2]

*Figura 2. Finestra di popup con il messaggio di errore.*

Sembra che è necessario toolook nel messaggio di errore di log toosee hello R. Fare clic su hello [Execute R Script] [ execute-r-script] e quindi fare clic su hello **visualizzare log** elemento hello **riquadro proprietà** toohello destra. Verrà visualizzata una nuova finestra del browser e viene visualizzato il seguente hello.

    [Critical]     Error: Error 0063: hello following error occurred during evaluation of R script:
    ---------- Start of error message from R ----------
    object 'y' not found


    object 'y' not found
    ----------- End of error message from R -----------

Questo messaggio di errore non contiene avere sorprese e consente di identificare chiaramente il problema di hello.

valore di hello tooinspect di qualsiasi oggetto in R, è possibile stampare file di log toohello questi valori. le regole di Hello per esaminare l'oggetto valori sono essenzialmente hello stesso come in una sessione interattiva di R. Ad esempio, se si digita un nome di variabile in una riga, il valore di hello dell'oggetto hello sarà stampato toohello file di log.  

#### <a name="packages-in-machine-learning-studio"></a>Pacchetti in Machine Learning Studio
Azure Machine Learning viene fornito con più di 350 pacchetti di linguaggio R preinstallati. È possibile utilizzare hello seguente di codice hello [Execute R Script] [ execute-r-script] tooretrieve modulo un elenco di hello preinstallato pacchetti.

    data.set <- data.frame(installed.packages())
    maml.mapOutputPort("data.set")

Se non si capiscono hello ultimo line-of-questo codice di un determinato momento hello, continuare a leggere. Nel resto di hello di questo documento verranno ampiamente illustrati l'uso di R nell'ambiente di Azure Machine Learning hello.

### <a name="introduction-toorstudio"></a>Introduzione tooRStudio
RStudio è un diffuso dell'IDE per R. Si utilizzerà RStudio per la modifica, test e debug di parte di codice hello R usati in questa Guida introduttiva. Dopo aver testato ed è pronto codice R, tagliare e incollare un Machine Learning Studio dall'editor RStudio hello [Execute R Script] [ execute-r-script] modulo.  

Se non si dispone di linguaggio di programmazione hello R installato nel computer desktop, è consigliabile che eseguire questa operazione ora. Per il download gratuito di linguaggio open source R è disponibile in rete di archiviazione completa R (CRAN) hello in [http://www.r-project.org/](http://www.r-project.org/). Sono disponibili anche download per Windows, Mac OS e Linux/UNIX. Scegliere un mirror nelle vicinanze e seguire le direzioni di download di hello. Il sistema CRAN contiene anche una serie di utili pacchetti di analisi e manipolazione di dati.

Se si tooRStudio nuovo, si deve scaricare e installare la versione desktop di hello. È possibile trovare hello che rstudio Scarica per Windows, Mac OS e Linux/UNIX all'http://www.rstudio.com/products/RStudio/. Seguire le istruzioni di hello fornite tooinstall RStudio sul computer desktop.  

TooRStudio un'introduzione all'esercitazione è disponibile all'indirizzo https://support.rstudio.com/hc/sections/200107586-Using-RStudio.

Altre informazioni sull'uso di RStudio sono disponibili nell'[Appendice A][appendixa].  

## <a id="scriptmodule"></a>Ottenere dati da e verso modulo Execute R Script hello
In questa sezione verranno trattati come ottenere dati dentro e fuori da hello [Execute R Script] [ execute-r-script] modulo. Verranno esaminate come toohandle vari tipi di dati letto in e da hello [Execute R Script] [ execute-r-script] modulo.

codice completo di Hello per questa sezione è nel file zip hello scaricato in precedenza.

### <a name="load-and-check-data-in-machine-learning-studio"></a>Caricare e controllare i dati in Machine Learning Studio
#### <a id="loading"></a>Caricare set di dati hello
Si inizierà caricando hello **csdairydata.csv** file in Azure Machine Learning Studio.

* Avviare l'ambiente di Azure Machine Learning Studio.
* Fare clic su **+ nuovo** in hello inferiore sinistro della schermata e selezionare **Dataset**.
* Selezionare **dal File locale**e quindi **Sfoglia** file hello tooselect.
* Assicurarsi di avere selezionato **file CSV generico con intestazione (. csv)** come tipo hello per hello set di dati.
* Fare clic su hello segno di spunta.
* Dopo che sono stati caricati i set di dati hello, si otterranno hello nuovo set di dati facendo clic su hello **set di dati** scheda.  

#### <a name="create-an-experiment"></a>Creare un esperimento
Ora che si dispongono di alcuni dati in Machine Learning Studio, è necessario toocreate un'analisi di hello toodo esperimento.  

* Fare clic su **+ nuovo** hello basso a sinistra e selezionare **esperimento**, quindi **esperimento vuoto**.
* È possibile assegnare un nome all'esperimento selezionando e modifica, hello **esperimento creato in...**  titolo nella parte superiore di hello della pagina hello. Ad esempio, può essere modificato troppo**CA Latticini Analysis**.
* A sinistra hello della pagina esperimento hello, espandere **Saved Datasets**e quindi **set di dati personali**. Dovrebbe essere hello **cadairydata.csv** caricato in precedenza.
* Trascinamento della selezione hello **csdairydata.csv dataset** nella sperimentazione hello.
* In hello **ricerca sperimentare elementi** casella in alto di hello del riquadro di sinistra hello, tipo [Execute R Script][execute-r-script]. Verrà visualizzato il modulo hello visualizzate nell'elenco di ricerca hello.
* Trascinamento della selezione hello [Execute R Script] [ execute-r-script] modulo sulla tavolozza.  
* Connettere l'output di hello di hello **csdairydata.csv dataset** input all'estrema sinistra toohello (**Dataset1**) di hello [Execute R Script][execute-r-script].
* **Non dimenticare tooclick su 'Salva'!**  

A questo punto, l'esperimento dovrebbe essere simile a quanto riportato nella Figura 3.

![Hello CA Latticini Analysis sperimentare set di dati e il modulo Execute R Script][3]

*Figura 3. Hello CA Latticini Analysis sperimentare dal set di dati e il modulo Execute R Script.*

#### <a name="check-on-hello-data"></a>Controllo sui dati hello
Di seguito hanno un aspetto dati hello che è stato caricato l'esperimento. Nell'esperimento hello, fare clic su output di hello di hello **cadairydata.csv dataset** e selezionare **visualizzare**. Dovrebbe apparire una tabella simile a quella riportata nella Figura 4.  

![Riepilogo dei set di dati cadairydata.csv hello][4]

*Figura 4. Riepilogo dei set di dati cadairydata.csv hello.*

In questa tabella sono presenti numerose informazioni utili. Possiamo vedere hello prima diverse righe del set di dati. Se si seleziona una colonna, hello sezione relativa alle statistiche Mostra ulteriori informazioni sulla colonna hello. Ad esempio, riga del tipo di funzionalità hello Mostra quali tipi di dati di Azure Machine Learning Studio assegnato toohello colonna. Disporre di un rapido controllo di questo è un controllo di integrità valido prima di iniziare toodo qualsiasi lavoro grave.

### <a name="first-r-script"></a>Primo script R
Creare un semplice primo tooexperiment di script R con in Azure Machine Learning Studio. Dichiaro di aver creato e testato hello lo script in RStudio seguente.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    str(cadairydata)
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

A questo punto è necessario tootransfer questo tooAzure script Machine Learning Studio. Potrei semplicemente eseguire un'operazione di copia e incolla, ma in questo caso trasferirò lo script R tramite un file con estensione zip.

### <a name="data-input-toohello-execute-r-script-module"></a>Modulo Execute R Script toohello input di dati
Si dispone di un'occhiata hello input toohello [Execute R Script] [ execute-r-script] modulo. In questo esempio si leggerà i dati per California hello in hello [Execute R Script] [ execute-r-script] modulo.  

Esistono tre possibili input per hello [Execute R Script] [ execute-r-script] modulo. È possibile usarne una o tutte, in base alle esigenze. È inoltre possibile toouse una R script che non accetta alcun input.  

Diamo un'occhiata ognuno di questi input, da tooright a sinistra. È possibile visualizzare i nomi di hello di ogni input hello posizionando il cursore sull'input hello e durante la lettura della descrizione comando hello.  

#### <a name="script-bundle"></a>Script Bundle
Hello input Script Bundle consente si toopass hello del contenuto di un file zip in [Execute R Script] [ execute-r-script] modulo. È possibile utilizzare uno dei seguenti comandi tooread hello contenuto file zip hello nel codice R hello.

    source("src/yourfile.R") # Reads a zipped R script
    load("src/yourData.rdata") # Reads a zipped R data file

> [!NOTE]
> Azure Machine Learning considera i file ZIP hello come se fossero in hello src / directory, pertanto è necessario tooprefix nei nomi di file con questo nome di directory. Ad esempio, se hello zip contiene file hello `yourfile.R` e `yourData.rdata` nella radice di zip hello hello sarebbe risolvere queste informazioni come `src/yourfile.R` e `src/yourData.rdata` quando si utilizza `source` e `load`.
> 
> 

Set di dati di caricamento in già descritto [caricamento dataset hello](#loading). Dopo aver creato e testato script hello R illustrato nella sezione precedente di hello, hello seguenti:

1. Salva script hello R in un. File di R. Chiamerò il mio file di script "simpleplot.R". Di seguito è riportato il contenuto di hello.
   
        ## Only one of hello following two lines should be used
        ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
        ## If in RStudio, use hello second line with read.csv()
        cadairydata <- maml.mapInputPort(1)
        # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
        str(cadairydata)
        pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata)
        ## hello following line should be executed only when running in
        ## Azure Machine Learning Studio
        maml.mapOutputPort('cadairydata')
2. Creare un file con estensione zip e copiare al suo interno lo script creato. In Windows, è possibile fare clic sul file hello e selezionare **inviare**e quindi **cartella**. Si creerà un nuovo file zip contenente hello "simpleplot. File R".
3. Aggiungere il file toohello **set di dati** in Machine Learning Studio, che specifica il tipo di hello come **zip**. Dovrebbe essere file zip hello nel DataSet.
4. Trascinare e rilasciare file zip hello da **set di dati** su hello **area di lavoro di Machine Learning Studio**.
5. Connettere l'output di hello di hello **zip dati** icona toohello **Script Bundle** input di hello [Execute R Script] [ execute-r-script] modulo.
6. Hello tipo `source()` funzione con il nome del file zip nella finestra di codice hello per hello [Execute R Script] [ execute-r-script] modulo. In questo caso, digitare `source("src/simpleplot.R")`.  
7. Fare clic su **Save**.

Dopo aver completati questi passaggi, hello [Execute R Script] [ execute-r-script] modulo verrà eseguiti script R hello in file con estensione zip hello quando viene eseguito l'esperimento hello. A questo punto l'esperimento dovrebbe avere un aspetto simile a quello riportato nella Figura 5.

![Esperimento con script R compresso][6]

*Figura 5. Esperimento con script R compresso.*

#### <a name="dataset1"></a>Dataset1
È possibile passare una tabella rettangolare di dati R tooyour codice usando input hello Dataset1. Nel nostro hello uno script semplice `maml.mapInputPort(1)` funzione legge i dati di hello dalla porta 1. Questi dati viene quindi assegnati tooa nome variabile di frame di dati nel codice. Nello script semplice prima riga di hello del codice esegue l'assegnazione hello.

    cadairydata <- maml.mapInputPort(1)

Eseguire l'esperimento facendo clic su hello **eseguire** pulsante. Al termine dell'esecuzione di hello, fare clic su hello [Execute R Script] [ execute-r-script] modulo e quindi fare clic su **Visualizza log di output** nel riquadro Proprietà hello. Una nuova pagina da visualizzare nel browser che mostra il contenuto di hello del file di log hello. Quando si scorre verso il basso dovrebbe essere simile alla seguente hello.

    [ModuleOutput] InputDataStructure
    [ModuleOutput]
    [ModuleOutput] {
    [ModuleOutput]  "InputName":Dataset1
    [ModuleOutput]  "Rows":228
    [ModuleOutput]  "Cols":9
    [ModuleOutput]  "ColumnTypes":System.Int32,3,System.Double,5,System.String,1
    [ModuleOutput] }

Più lontano verso il basso hello pagina è informazioni più dettagliate sulle colonne hello, che avrà un aspetto simile alla seguente hello.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput]
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput]
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput]
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput]
    [ModuleOutput]  $ Month            : chr  "Jan" "Feb" "Mar" "Apr" ...
    [ModuleOutput]
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput]
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput]
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput]
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...

Questi risultati sono principalmente come previsto, con 228 osservazioni e 9 colonne nel frame di dati hello. È possibile vedere i nomi di colonna hello, tipo di dati R hello e un esempio di ogni colonna.

> [!NOTE]
> Questo stesso output di stampa è facilmente disponibile hello output dispositivo R di hello [Execute R Script] [ execute-r-script] modulo. Si parlerà di output di hello di hello [Execute R Script] [ execute-r-script] modulo nella sezione successiva hello.  
> 
> 

#### <a name="dataset2"></a>Dataset2
Hello comportamento dell'input hello Dataset2 è identica toothat di Dataset1. Consente infatti di passare nel codice R creato una seconda tabella rettangolare di dati. funzione Hello `maml.mapInputPort(2)`, con argomento hello 2, viene utilizzato toopass questi dati.  

### <a name="execute-r-script-outputs"></a>Output del modulo Execute R Script
#### <a name="output-a-dataframe"></a>Output di un frame di dati
È possibile creare contenuto hello di un frame di dati R come una tabella tramite la porta hello Dataset1 risultati rettangolare utilizzando hello `maml.mapOutputPort()` (funzione). Viene eseguita da hello successiva riga nello script R semplice.

    maml.mapOutputPort('cadairydata')

Dopo aver esperimento hello in esecuzione, fare clic su una porta di output risultati Dataset1 hello e quindi fare clic su **Visualizza**. I risultati dovrebbero essere simili a quanto visualizzato nella Figura 6.

![visualizzazione di Hello dell'output di hello di dati per California hello][7]

*Figura 6. visualizzazione di Hello dell'output di hello di hello dati per California.*

Questo output è input toohello identici, esattamente come è previsto.  

### <a name="r-device-output"></a>Output R Device
output di dispositivo di hello Hello [Execute R Script] [ execute-r-script] modulo contiene i messaggi e output della grafica. Messaggi di errore standard e di output standard da R vengono inviati toohello R Device porta di output.  

hello tooview R dispositivo di output, fare clic sulla porta hello e quindi su **Visualizza**. Viene illustrato l'output di hello standard e l'errore standard dallo script R hello nella figura 7.

![Output standard e l'errore standard da hello porta dispositivo R][8]

*Figura 7. Output standard e l'errore standard da hello porta dispositivo R.*

Scorrendo verso il basso è visualizzato l'output grafico hello script R nella figura 8.  

![Output di grafica da hello porta dispositivo R][9]

*Figura 8. L'output di hello porta R dispositivo di grafica.*  

## <a id="filtering"></a>Filtraggio e trasformazione dei dati
In questa sezione verranno eseguiti alcuni filtro dei dati di base e operazioni di trasformazione in hello dati per California. Completamento hello di questa sezione verrà abbiamo dati in un formato appropriato per la creazione di un modello analitico.  

In particolare, in questa sezione vengono eseguite diverse attività comuni di pulizia e trasformazione dei dati: trasformazione del tipo, filtraggio nei frame di dati, aggiunta di nuove colonne elaborate e trasformazioni dei valori. Lo sfondo consentono di gestire hello numerose variazioni rilevate in problemi reali.

codice R completo Hello per questa sezione è disponibile nel file zip hello scaricato in precedenza.

### <a name="type-transformations"></a>Trasformazioni di tipi
Ora che è possibile leggere i dati di hello California per codice hello R nel hello [Execute R Script] [ execute-r-script] modulo, è necessario che i dati di hello nelle colonne hello sono hello previsto tipo e il formato tooensure.  

R è un linguaggio tipizzato in modo dinamico, il che significa che i tipi di dati vengono assegnati forzatamente da uno tooanother come richiesto. i tipi di dati atomic Hello in R includono numerici, logici e caratteri. tipo di fattore Hello è usato toocompactly archiviare i dati categorici. È possibile trovare molte più informazioni sui tipi di dati nei riferimenti hello in [appendice B - approfondimento](#appendixb).

Quando i dati in formato tabulare viene letto in R da un'origine esterna, è sempre un hello toocheck buona risultante tipi nelle colonne hello. È possibile, ad esempio, che una colonna che sarebbe dovuta essere di tipo Char in realtà risulti di tipo fattore, o viceversa. In altri casi, una colonna che si pensa debba essere numerica viene rappresentata da dati di tipo carattere, ad esempio '1,23' anziché 1,23 come numero a virgola mobile.  

Fortunatamente, è facile tooconvert uno tooanother di tipo, purché il mapping è possibile. Ad esempio, non è possibile convertire 'Nevada' in un valore numerico, ma è possibile convertirlo tooa fattore (variabile categorica). Un valore numerico 1, invece, può essere convertito sia nel carattere "1" sia in un fattore.  

sintassi di Hello per queste conversioni è semplice: `as.datatype()`. Queste funzioni di conversione di tipo includono seguente hello.

* `as.numeric()`
* `as.character()`
* `as.logical()`
* `as.factor()`

Esaminando i tipi di dati delle colonne di hello è di input nella sezione precedente hello hello: tutte le colonne sono di tipo numerico, ad eccezione di hello colonna con etichettata 'Month', che è di tipo carattere di tipo. Di seguito convertire questo fattore tooa e hello risultati dei test.  

Riga hello matrice scatterplot hello creato e aggiunto una linea di conversione tooa fattore di hello 'Month' colonna eliminato. In my esperimento verrà semplicemente tagliare e incollare il codice R hello nella finestra di codice hello di hello [Execute R Script] [ execute-r-script] modulo. È inoltre possibile aggiornare il file zip hello e caricarlo tooAzure Machine Learning Studio, ma questo richiede diversi passaggi.  

    ## Only one of hello following two lines should be used
    ## If running in Machine Learning Studio, use hello first line with maml.mapInputPort()
    ## If in RStudio, use hello second line with read.csv()
    cadairydata <- maml.mapInputPort(1)
    # cadairydata  <- read.csv("cadairydata.csv", header = TRUE, stringsAsFactors = FALSE)
    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(cadairydata$Month)
    str(cadairydata) # Check hello result
    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('cadairydata')

Consente di eseguire questo codice ed esaminare per hello script R i log di output di hello. dati rilevanti Hello dal log hello sono illustrati nella figura 9.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 14 levels "Apr","April",..: 6 5 9 1 11 8 7 3 14 13 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 9. Riepilogo dei frame di dati di hello con una variabile di fattore.*

tipo di Hello per mese dovrebbe ora essere visualizzato '**fattore con 14 livelli**'. Si tratta di un problema, poiché esistono solo 12 mesi nell'anno hello. È inoltre possibile verificare toosee che tipo di hello in **Visualizza** di hello set di risultati è la porta '**Categorical**'.

problema di Hello è tale colonna non è stata codificata sistematicamente ' Month' hello. Un mese può essere denominato Aprile in alcuni casi e abbreviato in Apr. in altri. È possibile risolvere il problema, trimming too3 caratteri della stringa hello. la riga Hello di codice è ora simile hello seguenti:

    ## Ensure hello coding is consistent and convert column tooa factor
    cadairydata$Month <- as.factor(substr(cadairydata$Month, 1, 3))

Eseguire di nuovo esperimento hello e visualizzare il log di output di hello. Hello previsto i risultati vengono visualizzati nella figura 10.  

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Column 0         : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year.Month       : num  1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 10. Riepilogo dei frame di dati di hello con numero di livelli di fattore corretto.*

La variabile di fattore dispone ora 12 livelli hello desiderato.

### <a name="basic-data-frame-filtering"></a>Filtraggio di frame di dati di base
I frame di dati R supportano avanzate funzionalità di filtraggio. I set di dati, infatti, possono essere suddivisi in sottoinsiemi usando filtri logici su righe o colonne. In molto casi, tuttavia, sono necessari complessi criteri di filtro. fa riferimento a Hello in [appendice B - approfondimento](#appendixb) contengono esempi dettagliati di filtro frame di dati.  

Possiamo eseguire semplici operazioni di filtraggio anche sul nostro set di dati. Se si osserva colonne hello hello cadairydata frame di dati, si noterà due colonne non necessarie. prima colonna Hello contiene solo un numero di riga, non è molto utile. Hello seconda colonna, Year.Month, contiene le informazioni ridondanti. È possibile escludere facilmente queste colonne tramite hello seguente codice R.

> [!NOTE]
> Da ora in questa sezione verrà semplicemente visualizzare si hello codice aggiuntivo che si sta aggiungendo in hello [Execute R Script] [ execute-r-script] modulo. Ogni nuova riga verranno aggiunte **prima** hello `str()` (funzione). Utilizzare questo tooverify funzione i risultati in Azure Machine Learning Studio.
> 
> 

È possibile aggiungere hello seguente codice R toomy riga hello [Execute R Script] [ execute-r-script] modulo.

    # Remove two columns we do not need
    cadairydata <- cadairydata[, c(-1, -2)]

Eseguire questo codice nell'esperimento e controllare il risultato di hello dal log di output di hello. Questi risultati vengono mostrati nella Figura 11.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  7 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 11. Riepilogo dei frame di dati di hello con due colonne è stato rimosso.*

Ottime notizie! Si ottengono i risultati di hello previsto.

### <a name="add-a-new-column"></a>Aggiungere una nuova colonna
i modelli time series toocreate sarà utile toohave una colonna che contiene hello mesi dall'inizio di hello della serie temporale hello. Creeremo quindi una nuova colonna denominata "Month.Count".

toohelp organizzare codice hello verrà creata la prima funzione semplice, `num.month()`. Quindi si applicherà questa toocreate funzione una nuova colonna in hello frame di dati. nuovo codice Hello è come indicato di seguito.

    ## Create a new column with hello month count
    ## Function toofind hello number of months from hello first
    ## month of hello time series
    num.month <- function(Year, Month) {
      ## Find hello starting year
      min.year  <- min(Year)

      ## Compute hello number of months from hello start of hello time series
      12 * (Year - min.year) + Month - 1
    }

    ## Compute hello new column for hello dataframe
    cadairydata$Month.Count <- num.month(cadairydata$Year, cadairydata$Month.Number)

Esegui esperimento hello aggiornato e utilizzare hello output log tooview hello risultati. I risultati previsti sono illustrati nella Figura 12.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  4.37 3.69 4.54 4.28 4.47 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  51.6 56.1 68.5 65.7 73.7 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  2.11 1.93 2.16 2.13 2.23 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  0.98 0.892 0.892 0.897 0.897 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 12. Riepilogo dei frame di dati di hello con la colonna aggiuntiva hello.*

Sembra che tutto stia funzionando perfettamente. Abbiamo hello nuova colonna i valori previsti hello nel frame di dati.

### <a name="value-transformations"></a>Trasformazioni di valori
In questa sezione si eseguirà alcune trasformazioni semplici valori hello in alcune delle colonne hello il frame di dati. il linguaggio R Hello supporta le trasformazioni di valore quasi arbitrario. fa riferimento a Hello in [appendice B - approfondimento](#appendixb) contengono esempi di estensione.

Se si esamina i valori hello nei riepiloghi di hello di questo frame di dati che verrà visualizzato un valore dispari qui. In California si produce più gelato che latte? No, naturalmente, non come ciò non ha senso, sad come ciò potrebbe essere toosome noi amanti gelato. unità di Hello sono diverse. prezzo Hello è espressa in unità di noi libbre, latte è espressa in unità di 1 milione libbre Stati Uniti, gelato è in unità pari a 1.000 ci vernice e fiocchi cheese è espressa in unità di 1.000 libbre Stati Uniti. Presupponendo un peso di gelato circa 6,5 libbre al gallone, si può facilmente hello tooconvert moltiplicazione questi valori in modo che siano tutti in unità uguale di 1.000 euro.

Per il modello di previsione viene usato un modello moltiplicativo per le tendenze e l'adattamento stagionale dei dati. Una trasformazione di log consente toouse un modello lineare, semplificando il processo. È possibile applicare una trasformazione log hello nella stessa funzione in cui viene applicato il moltiplicatore hello hello.

Nel seguente codice di hello, definire una nuova funzione `log.transform()`e applicarlo toohello righe contenenti valori numerici hello. Hello R `Map()` funzione è utilizzata tooapply hello `log.transform()` toohello funzione selezionate le colonne di hello frame di dati. `Map()`è simile troppo`apply()` ma consente più di un elenco di funzione toohello argomenti. Si noti che un elenco di moltiplicatori fornisce hello secondo argomento toohello `log.transform()` (funzione). Hello `na.omit()` funzione viene utilizzata come un po' di pulizia tooensure non è mancante o valori non definiti in hello frame di dati.

    log.transform <- function(invec, multiplier = 1) {
      ## Function for hello transformation, which is hello log
      ## of hello input value times a multiplier

      warningmessages <- c("ERROR: Non-numeric argument encountered in function log.transform",
                           "ERROR: Arguments toofunction log.transform must be greate than zero",
                           "ERROR: Aggurment multiplier toofuncition log.transform must be a scaler",
                           "ERROR: Invalid time seies value encountered in function log.transform"
                           )

      ## Check hello input arguments
      if(!is.numeric(invec) | !is.numeric(multiplier)) {warning(warningmessages[1]); return(NA)}  
      if(any(invec < 0.0) | any(multiplier < 0.0)) {warning(warningmessages[2]); return(NA)}
      if(length(multiplier) != 1) {{warning(warningmessages[3]); return(NA)}}

      ## Wrap hello multiplication in tryCatch
      ## If there is an exception, print hello warningmessage to
      ## standard error and return NA
      tryCatch(log(multiplier * invec),
               error = function(e){warning(warningmessages[4]); NA})
    }


    ## Apply hello transformation function toohello 4 columns
    ## of hello dataframe with production data
    multipliers  <- list(1.0, 6.5, 1000.0, 1000.0)
    cadairydata[, 4:7] <- Map(log.transform, cadairydata[, 4:7], multipliers)

    ## Get rid of any rows with NA values
    cadairydata <- na.omit(cadairydata)  

È presente un problema di bit in hello `log.transform()` (funzione). La maggior parte di questo codice è il controllo per individuare potenziali problemi con gli argomenti di hello o gestione delle eccezioni, che possono ancora verificarsi durante i calcoli di hello. Solo alcune righe di codice effettivamente hello calcoli.

obiettivo di Hello della programmazione difensivo hello è errore hello tooprevent di una singola funzione che impedisce l'elaborazione di continuare. Un errore improvviso in un'analisi di lunga durata può essere piuttosto frustrante per gli utenti. Questa situazione, l'impostazione predefinita, i valori restituiti devono essere scelte che limiteranno tooavoid danni toodownstream elaborazione. Un messaggio è anche gli utenti tooalert prodotti che si sono verificato errato.

Se non si è programmatori toodefensive usati in R, tutto il codice può sembrare piuttosto complesso. Assiste passaggi principali hello:

1. Viene definito un vettore di quattro messaggi. Questi messaggi sono utilizzati toocommunicate informazioni su alcuni dei possibili errori di hello e le eccezioni che possono verificarsi con questo codice.
2. Per ciascun caso restituirò il valore NA. Esistono diverse altre possibilità che potrebbero avere un minor numero di effetti collaterali. Potrebbe restituire un vettore di zeri o input originale, vettore di hello, ad esempio.
3. Nella funzione di hello argomenti toohello vengono eseguiti i controlli. In ogni caso, se viene rilevato un errore, viene restituito un valore predefinito e viene generato un messaggio per hello `warning()` (funzione). Utilizzo di `warning()` anziché `stop()` come hello quest'ultimo verrà terminare l'esecuzione, esattamente ciò che si sta tentando di tooavoid. Osservare come abbia scritto questo codice in stile procedurale: un approccio funzionale sarebbe apparso in questo caso eccessivamente complesso e oscuro.
4. i calcoli di Hello log vengono eseguito il wrapping `tryCatch()` in modo che le eccezioni non causino tooprocessing un arresto improvviso. Senza `tryCatch()` , la maggior parte degli errori generati dalle funzioni R producono un segnale di arresto, che interrompe l'esecuzione.

Eseguire questo codice R nell'esperimento e un'occhiata hello stampate output nel file di log hello. È ora verranno visualizzati i valori di hello trasformato di hello quattro colonne in hello log, come illustrato nella figura 13.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving variable  cadairydata  ..."
    [ModuleOutput] 
    [ModuleOutput] [1] "Saving hello following item(s):  .maml.oport1"

*Figura 13. Riepilogo di hello trasformati valori hello frame di dati.*

È possibile notare i valori hello sono stati trasformati. La produzione di latte supera ora di gran lunga la produzione di tutti gli altri prodotti caseari, ricordandoci come si stia ora usando una scala logaritmica .

A questo punto i nostri dati sono puliti e siamo pronti per qualche operazione di modeling. Osservando la visualizzazione di hello riepilogo per i set di risultati di output di hello nostri [Execute R Script] [ execute-r-script] modulo, si noterà colonna 'Month' hello è 'Categorie' con 12 valori univoci, nuovo, esattamente come si voleva .

## <a id="timeseries"></a>Oggetti della serie temporale e analisi delle correlazioni
In questa sezione verrà alcuni oggetti serie tempo base di R di esplorare e analizzare le correlazioni hello tra alcune delle variabili di hello. L'obiettivo è toooutput un frame di dati contenente hello correlazione pairwise informazioni in diversi ritardi.

codice R completo Hello per questa sezione è nel file zip hello scaricato in precedenza.

### <a name="time-series-objects-in-r"></a>Oggetti della serie temporale in R
Come già accennato, le serie temporali sono costituite da una serie di valori di dati indicizzati per data e ora. Oggetti della serie R vengono utilizzati toocreate e gestire un indice ora hello. Esistono diversi vantaggi toousing serie oggetti. Oggetti della serie evitano di hello molti dettagli della gestione di hello serie indice i valori che sono incapsulati nell'oggetto hello. Inoltre, oggetti di time series consentono toouse hello molti metodi di serie del tempo per il tracciato, stampa, modellazione e così via.

classe serie in fase di POSIXct Hello viene comunemente utilizzato ed è relativamente semplice. Questa classe serie in fase di misura di tempo dall'inizio di hello del periodo di hello, 1 gennaio 1970. In questo esempio useremo quindi oggetti serie temporale di tipo POSIXct. Altre classi di oggetti serie temporale comunemente usate in R includono zoo e xts, serie temporali estensibili.
<!-- Additional information on R time series objects is provided in hello references in Section 5.7. [commenting because this section doesn't exist, even in hello original] -->

### <a name="time-series-object-example"></a>Esempio di oggetto della serie temporale
Iniziamo con il nostro esempio. Trascinare un **nuovo** modulo [Execute R Script][execute-r-script] nell'esperimento. Connettere hello risultato Dataset1 porta di output di hello esistente [Execute R Script] [ execute-r-script] toohello modulo Dataset1 hello nuova porta di input [Execute R Script] [ execute-r-script] modulo.

Come per gli esempi prima hello, come è stato di avanzamento tramite l'esempio hello, in alcuni momenti verrà hello solo incrementale ulteriori righe di codice R a ogni passaggio.  

#### <a name="reading-hello-dataframe"></a>Lettura hello frame di dati
Come primo passaggio, di lettura in un frame di dati e assicurarsi che si ottengono i risultati di hello previsto. Hello seguente il codice deve eseguire il processo di hello.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)
    str(cadairydata) # Check hello results

A questo punto, eseguire esperimento hello. log Hello della nuova forma di Execute R Script hello dovrebbe essere simile figura 14.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  8 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...

*Figura 14. Riepilogo dei frame di dati di hello nel modulo Execute R Script hello.*

Questi dati sono di tipi di hello previsto e formato. Notare che il fattore di tipo di colonna 'Month' hello e hello previsto è numero di livelli.

#### <a name="creating-a-time-series-object"></a>Creazione di un oggetto della serie temporale
È necessario tooadd un frame di dati tooour di oggetto serie di tempo. Sostituire codice corrente hello con seguente hello, che aggiunge una nuova colonna della classe POSIXct.

    # Comment hello following if using RStudio
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata) # Check hello results

A questo punto, controllare il Registro di hello. Dovrebbe essere simile a quello riportato nella Figura 15.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Figura 15. Riepilogo dei frame di dati di hello con un oggetto della serie.*

Possiamo vedere da hello riepilogo che tale nuova colonna hello è in realtà di classe POSIXct.

### <a name="exploring-and-transforming-hello-data"></a>Esplorazione e la trasformazione dei dati hello
Vediamo alcune delle variabili di hello in questo set di dati. Una matrice scatterplot è tooproduce un modo efficace un rapido controllo. È sostituendo hello `str()` funzione nel codice R precedente hello con hello successiva riga.

    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = cadairydata, main = "Pairwise Scatterplots of dairy time series")

Eseguiamo il codice e vediamo cosa succede. tracciato di Hello prodotta alle hello porta dispositivo R dovrebbe essere simile figura 16.

![Matrice del grafico a dispersione delle variabili selezionate][17]

*Figura 16. Matrice del grafico a dispersione delle variabili selezionate.*

È una struttura insolita relazioni hello tra queste variabili. Ad esempio nasce da tendenze nei dati hello e da tabelle dei fatti hello che non è stato standardizzato variabili hello.

### <a name="correlation-analysis"></a>Analisi delle correlazioni
analisi di correlazione tooperform dobbiamo tooboth la tendenza e standardizzare le variabili di hello. È possibile usare semplicemente hello R `scale()` (funzione), che consente di centrare e ridimensiona le variabili. e può essere eseguita più velocemente. Tuttavia, si desidera tooshow è riportato un esempio di programmazione dei difensivo in R.

Hello `ts.detrend()` funzione illustrata di seguito esegue entrambe queste operazioni. Hello due righe di codice seguenti deallocare tendenza dati hello e quindi standardizzare i valori hello.

    ts.detrend <- function(ts, Time, min.length = 3){
      ## Function toode-trend and standardize a time series

      ## Define some messages if they are NULL  
      messages <- c('ERROR: ts.detrend requires arguments ts and Time toohave hello same length',
                    'ERROR: ts.detrend requires argument ts toobe of type numeric',
                    paste('WARNING: ts.detrend has encountered a time series with length less than', as.character(min.length)),
                    'ERROR: ts.detrend has encountered a Time argument not of class POSIXct',
                    'ERROR: Detrend regression has failed in ts.detrend',
                    'ERROR: Exception occurred in ts.detrend while standardizing time series in function ts.detrend'
      )
      # Create a vector of zeros tooreturn as a default in some cases
      zerovec  <- rep(length(ts), 0.0)

      # hello input arguments are not of hello same length, return ts and quit
      if(length(Time) != length(ts)) {warning(messages[1]); return(ts)}

      # If hello ts is not numeric, just return a zero vector and quit
      if(!is.numeric(ts)) {warning(messages[2]); return(zerovec)}

      # If hello ts is too short, just return it and quit
      if((ts.length <- length(ts)) < min.length) {warning(messages[3]); return(ts)}

      ## Check that hello Time variable is of class POSIXct
      if(class(cadairydata$Time)[[1]] != "POSIXct") {warning(messages[4]); return(ts)}

      ## De-trend hello time series by using a linear model
      ts.frame  <- data.frame(ts = ts, Time = Time)
      tryCatch({ts <- ts - fitted(lm(ts ~ Time, data = ts.frame))},
               error = function(e){warning(messages[5]); zerovec})

      tryCatch( {stdev <- sqrt(sum((ts - mean(ts))^2))/(ts.length - 1)
                 ts <- ts/stdev},
                error = function(e){warning(messages[6]); zerovec})

      ts
    }  
    ## Apply hello detrend.ts function toohello variables of interest
    df.detrend <- data.frame(lapply(cadairydata[, 4:7], ts.detrend, cadairydata$Time))

    ## Plot hello results toolook at hello relationships
    pairs(~ Cotagecheese.Prod + Icecream.Prod + Milk.Prod + N.CA.Fat.Price, data = df.detrend, main = "Pairwise Scatterplots of detrended standardized time series")

È presente un problema di bit in hello `ts.detrend()` (funzione). La maggior parte di questo codice è il controllo per individuare potenziali problemi con gli argomenti di hello o gestione delle eccezioni, che possono ancora verificarsi durante i calcoli di hello. Solo alcune righe di codice effettivamente hello calcoli.

Un esempio di programmazione difensiva è già stato illustrato in [Trasformazioni di valori](#valuetransformations). Entrambi i blocchi di calcolo vengono inclusi in `tryCatch()`. Per alcuni errori effettua vettore input originale hello senso tooreturn e in altri casi, restituisce un vettore di zeri.  

Si noti che la regressione lineare hello utilizzata per la tendenza una regressione serie di tempo. variabile predittiva Hello è un oggetto della serie.  

Una volta `ts.detrend()` è definito si applicano variabili toohello di interesse per il frame di dati. È necessario forzare l'elenco risultante di hello creato da `lapply()` toodata frame di dati tramite `as.data.frame()`. A causa di aspetti difensivo `ts.detrend()`, tooprocess di errore non impedirà a una delle variabili di hello corretta elaborazione di hello ad altri utenti.  

riga finale di Hello di codice crea un scatterplot pairwise. Dopo l'esecuzione di codice hello R, i risultati di hello di hello scatterplot sono illustrati nella figura 17.

![Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata][18]

*Figura 17. Grafico a dispersione pairwise della serie temporale detrendizzata e standardizzata.*

È possibile confrontare questi toothose risultati illustrato nella figura 16. Con hello tendenza rimosso e hello variabili standardizzate, vediamo molto meno strutturato nelle relazioni di hello tra queste variabili.

Hello codice toocompute hello set correlazioni come oggetti ccf R è come indicato di seguito.

    ## A function toocompute pairwise correlations from a
    ## list of time series value vectors
    pair.cor <- function(pair.ind, ts.list, lag.max = 1, plot = FALSE){
      ccf(ts.list[[pair.ind[1]]], ts.list[[pair.ind[2]]], lag.max = lag.max, plot = plot)
    }

    ## A list of hello pairwise indices
    corpairs <- list(c(1,2), c(1,3), c(1,4), c(2,3), c(2,4), c(3,4))

    ## Compute hello list of ccf objects
    cadairycorrelations <- lapply(corpairs, pair.cor, df.detrend)  

    cadairycorrelations

Esecuzione del codice genera log hello illustrato nella figura 18.

    [ModuleOutput] Loading objects:
    [ModuleOutput]   port1
    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] [[1]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.148 0.358 0.317 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[2]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.395 -0.186 -0.238 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[3]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.059 -0.089 -0.127 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[4]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]    -1     0     1 
    [ModuleOutput] 0.140 0.294 0.293 
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] [[5]]
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput] Autocorrelations of series 'X', by lag
    [ModuleOutput] 
    [ModuleOutput] 
    [ModuleOutput]     -1      0      1 
    [ModuleOutput] -0.002 -0.074 -0.124 

*Figura 18. Elenco di ccf oggetti dall'analisi di correlazione pairwise hello.*

Per ogni intervallo è presente un valore di correlazione. Nessuno di questi valori di correlazione è sufficientemente grande toobe significativo. Possiamo quindi concludere che ciascuna variabile può essere modellata in modo indipendente.

### <a name="output-a-dataframe"></a>Output di un frame di dati
È stato calcolato correlazioni pairwise hello come un elenco di oggetti R ccf. Questa operazione presenta un bit di un problema come porta di output di set di risultati hello necessita di un frame di dati. Inoltre, oggetto ccf hello è a sua volta un elenco e si vuole solo i valori hello nell'elemento di primo hello di questo elenco, correlazioni hello in hello ritardi diversi.

Hello seguenti valori di ritardo hello estratti di codice dall'elenco di hello di oggetti ccf, che sono a loro volta gli elenchi.

    df.correlations <- data.frame(do.call(rbind, lapply(cadairycorrelations, '[[', 1)))

    c.names <- c("correlation pair", "-1 lag", "0 lag", "+1 lag")
    r.names  <- c("Corr Cot Cheese - Ice Cream",
                  "Corr Cot Cheese - Milk Prod",
                  "Corr Cot Cheese - Fat Price",
                  "Corr Ice Cream - Mik Prod",
                  "Corr Ice Cream - Fat Price",
                  "Corr Milk Prod - Fat Price")

    ## Build a dataframe with hello row names column and the
    ## correlation data frame and assign hello column names
    outframe <- cbind(r.names, df.correlations)
    colnames(outframe) <- c.names
    outframe


    ## WARNING!
    ## hello following line works only in Azure Machine Learning
    ## When running in RStudio, this code will result in an error
    #maml.mapOutputPort('outframe')

Hello prima riga di codice è difficile e alcune spiegazioni possono aiutarti a capire. Partendo dall'interno hello abbiamo seguente hello:

1. Hello '**[[**'operator con argomento hello'**1**' Seleziona hello vettore di correlazioni a ritardi hello dal primo elemento di hello hello ccf elenco di oggetti.
2. Hello `do.call()` funzione applica hello `rbind()` funzione degli elementi dell'elenco di hello di hello restituisce eseguendo `lapply()`.
3. Hello `data.frame()` funzione assegna il risultato di hello prodotto da `do.call()` tooa frame di dati.

Si noti che i nomi di riga hello in una colonna di hello frame di dati. In questo modo consente di mantenere i nomi di riga hello quando vengono restituiti da hello [Execute R Script][execute-r-script].

Esecuzione di codice hello produce l'output di hello mostrato nella figura 19 quando si **Visualizza** hello output hello porta set di risultati. i nomi di riga Hello sono nella prima colonna hello, come previsto.

![Output dei risultati dall'analisi di correlazione hello][20]

*Figura 19. Risultati di output dall'analisi di correlazione hello.*

## <a id="seasonalforecasting"></a>Esempio di serie temporale: previsione stagionale
I dati sono ora in un formato adatto per l'analisi e abbiamo determinato che non esistono significative correlazioni tra le variabili di hello. Passiamo quindi alla creazione di un modello di previsione in serie temporale, Utilizzando questo modello è verrà prevedere la produzione di latte California per hello di 2013 12 mesi.

Il nostro modello previsionale sarà costituito da due componenti: trend e stagionale. previsione completo Hello è prodotto hello di questi due componenti. Questo tipo di modello prende il nome di modello moltiplicativo, In alternativa Hello è un modello di addizione. Abbiamo già applicate variabili registro trasformazione toohello di interesse, rendendo questa analisi gestibile.

codice R completo Hello per questa sezione è nel file zip hello scaricato in precedenza.

### <a name="creating-hello-dataframe-for-analysis"></a>Creazione di hello frame di dati per l'analisi
Per iniziare, aggiungere un **nuova** [Execute R Script] [ execute-r-script] esperimento tooyour modulo. Connettersi hello **set di risultati** output di hello esistente [Execute R Script] [ execute-r-script] modulo toohello **Dataset1** input del nuovo modulo hello. risultato Hello dovrebbe essere simile alla figura 20.

![Hello sperimentare hello nuovo Execute R Script modulo aggiunto][21]

*Figura 20. Hello sperimentare dal modulo Execute R Script nuovo hello aggiunto.*

Come con l'analisi di correlazione hello che è completati, è necessario tooadd una colonna con un oggetto della serie POSIXct. Hello seguente codice verrà eseguita solo questo.

    # If running in Machine Learning Studio, uncomment hello first line with maml.mapInputPort()
    cadairydata <- maml.mapInputPort(1)

    ## Create a new column as a POSIXct object
    Sys.setenv(TZ = "PST8PDT")
    cadairydata$Time <- as.POSIXct(strptime(paste(as.character(cadairydata$Year), "-", as.character(cadairydata$Month.Number), "-01 00:00:00", sep = ""), "%Y-%m-%d %H:%M:%S"))

    str(cadairydata)

Eseguire il codice ed esaminare i log di hello. risultato Hello dovrebbe essere simile figura 21.

    [ModuleOutput] [1] "Loading variable port1..."
    [ModuleOutput] 
    [ModuleOutput] 'data.frame':    228 obs. of  9 variables:
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Number     : int  1 2 3 4 5 6 7 8 9 10 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Year             : int  1995 1995 1995 1995 1995 1995 1995 1995 1995 1995 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month            : Factor w/ 12 levels "Apr","Aug","Dec",..: 5 4 8 1 9 7 6 2 12 11 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Cotagecheese.Prod: num  1.47 1.31 1.51 1.45 1.5 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Icecream.Prod    : num  5.82 5.9 6.1 6.06 6.17 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Milk.Prod        : num  7.66 7.57 7.68 7.66 7.71 ...
    [ModuleOutput] 
    [ModuleOutput]  $ N.CA.Fat.Price   : num  6.89 6.79 6.79 6.8 6.8 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Month.Count      : num  0 1 2 3 4 5 6 7 8 9 ...
    [ModuleOutput] 
    [ModuleOutput]  $ Time             : POSIXct, format: "1995-01-01" "1995-02-01" ...

*Figura 21. Un riepilogo dei frame di dati hello.*

Con questo risultato, siamo toostart pronto l'analisi.

### <a name="create-a-training-dataset"></a>Creare un set di dati di training
Con i frame di dati hello costruito dobbiamo toocreate un set di dati di training. Questi dati verranno incluse tutte le osservazioni hello ad eccezione del fatto hello ultime 12, dell'anno hello 2013, ovvero il set di dati di test. esempio Hello subset hello frame di dati del codice e crea i tracciati delle variabili di produzione e il prezzo per hello. Quindi creare grafici di hello quattro variabili di produzione e prezzo. Una funzione anonima viene utilizzato toodefine alcuni consente per i grafici e quindi scorrere elenco hello di hello altri due argomenti con `Map()`. Se pensate che un ciclo For sarebbe stato appropriato, avete ragione. Tuttavia, poiché R è un linguaggio funzionale, adotterò un approccio funzionale.

    cadairytrain <- cadairydata[1:216, ]

    Ylabs  <- list("Log CA Cotage Cheese Production, 1000s lb",
                   "Log CA Ice Cream Production, 1000s lb",
                   "Log CA Milk Production 1000s lb",
                   "Log North CA Milk Milk Fat Price per 1000 lb")

    Map(function(y, Ylabs){plot(cadairytrain$Time, y, xlab = "Time", ylab = Ylabs, type = "l")}, cadairytrain[, 4:7], Ylabs)

L'esecuzione di codice hello produce hello serie di serie temporale è rappresentata dall'output di hello dispositivo R illustrato nella figura 22. Si noti che asse temporale hello è espressa in unità di date, un vantaggio del tempo di hello serie tracciare metodo.

![Primo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-161.png)

![Secondo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-162.png)

![Terzo tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-163.png)

![Quarto tracciato della serie temporale della produzione casearia in California e dei dati sui prezzi](./media/machine-learning-r-quickstart/unnamed-chunk-164.png)

*Figura 22. Tracciati della serie temporale della produzione casearia in California e dei dati sui prezzi.*

### <a name="a-trend-model"></a>Modello di tendenza
Dopo aver creato un oggetto di time series e avere esaminato i dati di hello, iniziamo tooconstruct un modello di tendenza per hello dati di produzione di latte California. A questo scopo, usiamo una regressione in serie temporale. Tuttavia, è evidente in base al tracciato hello che si sarà necessario più di un tooaccurately pendenza e intercetta modello hello osservato tendenza nei dati di training hello.

Dato su scala ridotta hello dei dati di hello, si verrà compilare hello modello per la tendenza di RStudio e quindi copia e Incolla modello risultante hello in Azure Machine Learning. RStudio fornisce infatti un ambiente interattivo adatto a questo tipo di analisi interattiva.

Come primo tentativo, si passerà una regressione polinomiale con accensione too3. Esiste un pericolo reale di overfitting per questi tipi di modelli. È pertanto termini di ordine superiore tooavoid migliore. Hello `I()` funzione impedisce l'interpretazione del contenuto di hello (interpreta contenuto hello 'così com'è") e consente una funzione interpretata letteralmente toowrite in un'equazione di regressione.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3), data = cadairytrain)
    summary(milk.lm)

Questo genera l'errore seguente hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^2) + I(Month.Count^3),
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12667 -0.02730  0.00236  0.02943  0.10586
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.33e+00   1.45e-01   43.60   <2e-16 ***
    ## Time              1.63e-09   1.72e-10    9.47   <2e-16 ***
    ## I(Month.Count^2) -1.71e-06   4.89e-06   -0.35    0.726
    ## I(Month.Count^3) -3.24e-08   1.49e-08   -2.17    0.031 *  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0418 on 212 degrees of freedom
    ## Multiple R-squared:  0.941,    Adjusted R-squared:  0.94
    ## F-statistic: 1.12e+03 on 3 and 212 DF,  p-value: <2e-16

Dai valori di P (Pr (> | t |)) nell'output, possiamo vedere che hello termine al quadrato potrebbe non essere significativo. Si utilizzerà hello `update()` funzione toomodify questo modello da hello di eliminazione al quadrato termine.

    milk.lm <- update(milk.lm, . ~ . - I(Month.Count^2))
    summary(milk.lm)

Questo genera l'errore seguente hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.12597 -0.02659  0.00185  0.02963  0.10696
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## (Intercept)       6.38e+00   4.07e-02   156.6   <2e-16 ***
    ## Time              1.57e-09   4.32e-11    36.3   <2e-16 ***
    ## I(Month.Count^3) -3.76e-08   2.50e-09   -15.1   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0417 on 213 degrees of freedom
    ## Multiple R-squared:  0.941,  Adjusted R-squared:  0.94
    ## F-statistic: 1.69e+03 on 2 and 213 DF,  p-value: <2e-16

L'aspetto è decisamente migliore adesso. Tutti i termini di hello sono significativi. Tuttavia, il valore di 2e-16 hello è un valore predefinito e non deve essere eseguito troppo grave.  

Come un test di integrità, questo punto, eseguire il tracciato di serie tempo dei dati di produzione per California hello con curva tendenza hello illustrata. Ho aggiunto hello seguente di codice in Azure Machine Learning hello [Execute R Script] [ execute-r-script] toocreate modello (non RStudio) hello modello ed effettuare un tracciato. il risultato di Hello è illustrato nella figura 23.

    milk.lm <- lm(Milk.Prod ~ Time + I(Month.Count^3), data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm, cadairytrain), lty = 2, col = 2)

![Dati sulla produzione di latte in California con il modello di tendenza visualizzato](./media/machine-learning-r-quickstart/unnamed-chunk-18.png)

*Figura 23. Dati sulla produzione di latte in California con il modello di tendenza visualizzato.*

Sembra che il modello di tendenza hello adatta dati hello abbastanza bene. Inoltre, non sembra toobe evidenza di adattamento in eccesso, ad esempio si deforma dispari nella curva modello hello.  

### <a name="seasonal-model"></a>Modello con stagionalità
Con un modello di tendenza in mano, è necessario toopush in e gli effetti stagionali hello. Si utilizzerà il mese di hello hello anno come una variabile fittizia attivo di hello modello lineare toocapture hello mese per mese. Si noti che quando si introducono le variabili di fattore in un modello, intercetta hello necessario non è stato calcolato. Se non eseguire questa operazione, formula hello è eccessiva specificato e R eliminerà uno di hello desiderato fattori ma mantenere il termine di intercept hello.

Poiché si dispone di un modello di tendenza soddisfacenti, è possibile utilizzare hello `update()` hello tooadd funzione nuovi termini toohello di modello esistente. Hello -1 nella formula di aggiornamento hello Elimina termine intercetta hello. Continuare a RStudio per il momento hello:

    milk.lm2 <- update(milk.lm, . ~ . + Month - 1)
    summary(milk.lm2)

Questo genera l'errore seguente hello.

    ##
    ## Call:
    ## lm(formula = Milk.Prod ~ Time + I(Month.Count^3) + Month - 1,
    ##     data = cadairytrain)
    ##
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max
    ## -0.06879 -0.01693  0.00346  0.01543  0.08726
    ##
    ## Coefficients:
    ##                   Estimate Std. Error t value Pr(>|t|)
    ## Time              1.57e-09   2.72e-11    57.7   <2e-16 ***
    ## I(Month.Count^3) -3.74e-08   1.57e-09   -23.8   <2e-16 ***
    ## MonthApr          6.40e+00   2.63e-02   243.3   <2e-16 ***
    ## MonthAug          6.38e+00   2.63e-02   242.2   <2e-16 ***
    ## MonthDec          6.38e+00   2.64e-02   241.9   <2e-16 ***
    ## MonthFeb          6.31e+00   2.63e-02   240.1   <2e-16 ***
    ## MonthJan          6.39e+00   2.63e-02   243.1   <2e-16 ***
    ## MonthJul          6.39e+00   2.63e-02   242.6   <2e-16 ***
    ## MonthJun          6.38e+00   2.63e-02   242.4   <2e-16 ***
    ## MonthMar          6.42e+00   2.63e-02   244.2   <2e-16 ***
    ## MonthMay          6.43e+00   2.63e-02   244.3   <2e-16 ***
    ## MonthNov          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## MonthOct          6.37e+00   2.63e-02   241.8   <2e-16 ***
    ## MonthSep          6.34e+00   2.63e-02   240.6   <2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ##
    ## Residual standard error: 0.0263 on 202 degrees of freedom
    ## Multiple R-squared:     1,    Adjusted R-squared:     1
    ## F-statistic: 1.42e+06 on 14 and 202 DF,  p-value: <2e-16

Vediamo che hello e del modello di non è più un termine di intercept ha fattori significativi mese 12. Questo è esattamente ciò che si voleva toosee.

Verifichiamo un altro tracciato di serie di tempo di hello California produzione per dati toosee funziona bene modello stagionali hello. Ho aggiunto hello seguente di codice in Azure Machine Learning hello [Execute R Script] [ execute-r-script] toocreate hello modello ed effettuare un tracciato.

    milk.lm2 <- lm(Milk.Prod ~ Time + I(Month.Count^3) + Month - 1, data = cadairytrain)

    plot(cadairytrain$Time, cadairytrain$Milk.Prod, xlab = "Time", ylab = "Log CA Milk Production 1000s lb", type = "l")
    lines(cadairytrain$Time, predict(milk.lm2, cadairytrain), lty = 2, col = 2)

Esecuzione del codice in Azure Machine Learning genera tracciato hello illustrato nella figura 24.

![Produzione di latte in California con un modello che include gli effetti stagionali](./media/machine-learning-r-quickstart/unnamed-chunk-20.png)

*Figura 24. Produzione di latte in California con un modello che include gli effetti stagionali.*

Hello toohello adatta dati illustrati nella figura 24 sono piuttosto incoraggianti. L'aspetto ragionevole sia tendenza hello e stagionali hello (variazione mensile).

Come un altro controllo sul nostro modello, si hanno un'occhiata residui hello. Hello calcola di codice seguente hello valori stimati tra i due modelli, consente di calcolare residui hello per modello stagionali hello e quindi vengono tracciati tali residui per i dati di training hello.

    ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute and plot hello residuals
    residuals <- cadairydata$Milk.Prod - predict2
    plot(cadairytrain$Time, residuals[1:216], xlab = "Time", ylab ="Residuals of Seasonal Model")

tracciato residuo Hello è illustrato nella figura 25.

![Residui del modello di stagionali hello per dati di training hello](./media/machine-learning-r-quickstart/unnamed-chunk-21.png)

*Figura 25. Residui del modello di stagionali hello per dati di training hello.*

Questi valori residui sembrano ragionevoli. È presente alcuna struttura specifico, ad eccezione di effetto hello di recessione hello 2008 2009, che il nostro modello non tiene conto di particolarmente appropriata.

tracciato di Hello mostrato nella figura 25 è utile per rilevare eventuali modelli dipendenti dal tempo in residui hello. approccio esplicito di Hello di calcolo e di tracciatura residui hello utilizzato inserisce residui hello in ordine temporale in tracciato hello. Se, in hello invece avevo tracciati `milk.lm$residuals`, non sarebbe stato tracciato hello in ordine temporale.

È inoltre possibile utilizzare `plot.lm()` tooproduce una serie di grafici di diagnostica.

    ## Show hello diagnostic plots for hello model
    plot(milk.lm2, ask = FALSE)

Questo codice produce una serie di tracciati diagnostici mostrati nella Figura 26.

![Prima di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-221.png)

![Secondo di grafici di diagnostica per il modello di stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-222.png)

![Terzo di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-223.png)

![Quarto di grafici di diagnostica per il modello stagionali hello](./media/machine-learning-r-quickstart/unnamed-chunk-224.png)

*Figura 26. Traccia di diagnostica per il modello stagionali hello.*

Esistono alcuni punti reparti identificati in questi grafici, ma niente di grande interesse toocause. Inoltre, si noterà dal tracciato normale Q-Q hello che residui hello sono distribuiti, toonormally Chiudi presupposto importante per modelli lineari.

### <a name="forecasting-and-model-evaluation"></a>Previsione e valutazione del modello
Non sussiste toocomplete di toodo cosa ulteriori solo un esempio. È necessaria toocompute previsioni e misurare le errore hello rispetto ai dati effettivi hello. La previsione sarà per hello di 2013 12 mesi. È possibile calcolare una misura di errore per questi dati di previsione toohello effettivo che non fa parte di questo set di dati di training. Inoltre, è possibile confrontare le prestazioni in hello 18 anni di toohello di dati di training 12 mesi di dati di test.  

Viene utilizzato un numero di metriche delle prestazioni di hello toomeasure di modelli time series. In questo caso si utilizzerà hello radice errore quadratico medio (RMS). Hello funzione seguente calcola errore hello RMS tra due serie.  

    RMS.error <- function(series1, series2, is.log = TRUE, min.length = 2){
      ## Function toocompute hello RMS error or difference between two
      ## series or vectors

      messages <- c("ERROR: Input arguments toofunction RMS.error of wrong type encountered",
                    "ERROR: Input vector toofunction RMS.error is too short",
                    "ERROR: Input vectors toofunction RMS.error must be of same length",
                    "WARNING: Funtion rms.error has received invald input time series.")

      ## Check hello arguments
      if(!is.numeric(series1) | !is.numeric(series2) | !is.logical(is.log) | !is.numeric(min.length)) {
        warning(messages[1])
        return(NA)}

      if(length(series1) < min.length) {
        warning(messages[2])
        return(NA)}

      if((length(series1) != length(series2))) {
           warning(messages[3])
        return(NA)}

      ## If is.log is TRUE exponentiate hello values, else just copy
      if(is.log) {
        tryCatch( {
          temp1 <- exp(series1)
          temp2 <- exp(series2) },
          error = function(e){warning(messages[4]); NA}
        )
      } else {
        temp1 <- series1
        temp2 <- series2
      }

     ## Compute predictions from our models
    predict1  <- predict(milk.lm, cadairydata)
    predict2  <- predict(milk.lm2, cadairydata)

    ## Compute hello RMS error in a dataframe
      tryCatch( {
        sqrt(sum((temp1 - temp2)^2) / length(temp1))},
        error = function(e){warning(messages[4]); NA})
    }

Come con hello `log.transform()` illustrato nella funzione hello "Valore trasformazioni" sezione, è molto di codice di recupero di controllo e l'eccezione Errore in questa funzione. principi di Hello utilizzati sono hello stesso. Hello lavoro viene eseguito in due posizioni racchiuso `tryCatch()`. In primo luogo, serie temporale hello sono exponentiated, poiché sono stati trattati i registri di hello valori hello. In secondo luogo, errore RMS di hello effettivo viene calcolato.  

Dotato di un hello toomeasure funzione errore RMS, compilare e consente l'output di un frame di dati contenenti errori hello RMS. Si includerà termini hello tendenza solo per modello e modello completo di hello con fattori stagionali. Hello codice hello processo utilizzando hello due modelli lineare che è stata costruita.

    ## Compute hello RMS error in a dataframe
    ## Include hello row names in hello first column so they will
    ## appear in hello output of hello Execute R Script
    RMS.df  <-  data.frame(
    rowNames = c("Trend Model", "Seasonal Model"),
      Traing = c(
      RMS.error(predict1[1:216], cadairydata$Milk.Prod[1:216]),
      RMS.error(predict2[1:216], cadairydata$Milk.Prod[1:216])),
      Forecast = c(
        RMS.error(predict1[217:228], cadairydata$Milk.Prod[217:228]),
        RMS.error(predict2[217:228], cadairydata$Milk.Prod[217:228]))
    )
    RMS.df

    ## hello following line should be executed only when running in
    ## Azure Machine Learning Studio
    maml.mapOutputPort('RMS.df')

L'esecuzione del codice produce l'output di hello mostrato nella figura 27 all'hello porta di output di set di risultati.

![Confronto di errori di RMS per i modelli di hello][26]

*Figura 27. Confronto tra gli errori di RMS per i modelli di hello.*

Da questi risultati, viene illustrato che l'aggiunta di hello fattori stagionali toohello modello riduce errore RMS hello in modo significativo. Troppo ovviamente errore hello RMS per i dati di training hello è un bit minore per hello previsione.

## <a id="appendixa"></a>Appendice a: Guida tooRStudio
RStudio sia molto ben documentato, pertanto in questa appendice verranno fornite alcune toohello collegamenti sezioni principali di hello RStudio documentazione tooget che è stato avviato.

1. Creazione di progetti
   
   È possibile organizzare e gestire il codice R nei progetti usando RStudio. documentazione di Hello che usa i progetti è reperibile all'https://support.rstudio.com/hc/articles/200526207-Using-Projects.
   
   Consiglia di seguire queste istruzioni e creare un progetto per esempi di codice hello R in questo documento.  
2. Modifica ed esecuzione di codice R
   
   RStudio offre un ambiente integrato per la modifica e l'esecuzione di codice R. La documentazione è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200484448-Editing-and-Executing-Code.
3. Debug
   
   RStudio include avanzate funzionalità di debug. La documentazione su queste funzionalità è disponibile all'indirizzo https://support.rstudio.com/hc/articles/200713843-Debugging-with-RStudio.
   
   funzionalità di risoluzione dei problemi di Hello punto di interruzione sono documentate in https://support.rstudio.com/hc/articles/200534337-Breakpoint-Troubleshooting.

## <a id="appendixb"></a>APPENDICE B: Letture di approfondimento
Questa esercitazione include nozioni fondamentali di hello di programmazione di R dei risultati che è necessario toouse hello linguaggio R in Azure Machine Learning Studio. Se non si ha familiarità con R, in CRAN sono disponibili due introduzioni:

* R per utenti meno esperti per Emmanuel Paradis è un ottimo strumento toostart in http://cran.r-project.org/doc/contrib/Paradis-rdebuts_en.pdf.  
* Un tooR introduzione da W. N. Venables et. al. fornisce informazioni più approfondite all'indirizzo http://cran.r-project.org/doc/manuals/R-intro.html.

Sono disponibili molti libri con informazioni introduttive su R. Di seguito sono elencati quelli che ritengo più utili:

* Immagine di programmazione R Hello: una presentazione di statistiche Software Design Norman Matloff è tooprogramming un'eccellente introduzione in R.  
* Guida di riferimento di R da Paul Teetor fornisce un toousing approccio problemi e soluzioni R.  
* R in Action di Robert Kabacoff, un altro libro introduttivo valido. sito Web di R rapido complementare Hello è una risorsa utile http://www.statmethods.net/.
* R da Patrick Burns è un libro sorprendentemente divertente che gestisce un numero di argomenti complesso e difficile che possono essere rilevati durante la programmazione in libro hello r. è disponibile gratuitamente a http://www.burns-stat.com/documents/books/the-r-inferno/.
* Se si desidera un approfondimento argomenti avanzati in R, hanno un'occhiata libro hello avanzate R da Hadley Wickham. versione online di Hello questa guida è disponibile gratuitamente in http://adv-r.had.co.nz/.

Un catalogo di pacchetti di R ora serie sono reperibili hello CRAN visualizzazione delle attività per l'analisi delle serie temporali: http://cran.r-project.org/web/views/TimeSeries.html. Per informazioni sui pacchetti oggetto serie di tempo specifico, è consigliabile consultare la documentazione di toohello per tale pacchetto.

libro Hello introduttivo Time Series con R Paul Cowpertwait e Andrew Metcalfe fornisce un'introduzione toousing R, per l'analisi delle serie temporali. Numerosi esempi di R sono infine disponibili in una grande quantità di testi teorici.

Alcune importanti risorse su Internet:

* DataCamp: DataCamp illustra R in comfort hello del browser con lezioni video e gli esercizi di codifica. Sono disponibili esercitazioni interattive su tecniche di hello più recente R e pacchetti. Eseguire hello libero interattivo esercitazione su R a https://www.datacamp.com/courses/introduction-to-r
* Una Guida introduttiva alla programmazione con R da Programiz https://www.programiz.com/r-programming
* Una rapida esercitazione su R di Kelly Black della Clarkson University è disponibile all'indirizzo http://www.cyclismo.org/tutorial/R/
* Oltre 60 risorse su R sono elencate all'indirizzo http://www.computerworld.com/article/2497464/business-intelligence-60-r-resources-to-improve-your-data-skills.html

<!--Image references-->
[1]: ./media/machine-learning-r-quickstart/fig1.png
[2]: ./media/machine-learning-r-quickstart/fig2.png
[3]: ./media/machine-learning-r-quickstart/fig3.png
[4]: ./media/machine-learning-r-quickstart/fig4.png
[5]: ./media/machine-learning-r-quickstart/fig5.png
[6]: ./media/machine-learning-r-quickstart/fig6.png
[7]: ./media/machine-learning-r-quickstart/fig7.png
[8]: ./media/machine-learning-r-quickstart/fig8.png
[9]: ./media/machine-learning-r-quickstart/fig9.png
[10]: ./media/machine-learning-r-quickstart/fig10.png
[11]: ./media/machine-learning-r-quickstart/fig11.png
[12]: ./media/machine-learning-r-quickstart/fig12.png
[13]: ./media/machine-learning-r-quickstart/fig13.png
[14]: ./media/machine-learning-r-quickstart/fig14.png
[15]: ./media/machine-learning-r-quickstart/fig15.png
[16]: ./media/machine-learning-r-quickstart/fig16.png
[17]: ./media/machine-learning-r-quickstart/fig17.png
[18]: ./media/machine-learning-r-quickstart/fig18.png
[19]: ./media/machine-learning-r-quickstart/fig19.png
[20]: ./media/machine-learning-r-quickstart/fig20.png
[21]: ./media/machine-learning-r-quickstart/fig21.png
[22]: ./media/machine-learning-r-quickstart/fig22.png

[26]: ./media/machine-learning-r-quickstart/fig26.png

<!--links-->
[appendixa]: #appendixa
[download]: https://azurebigdatatutorials.blob.core.windows.net/rquickstart/RFiles.zip


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
