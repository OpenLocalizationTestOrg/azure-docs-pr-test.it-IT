---
title: Scienza aaaData nella macchina virtuale di analisi scientifica dei dati di Linux hello | Documenti Microsoft
description: "Modalità tooperform diversi analisi scientifica dei dati comuni di attività con hello VM Linux di analisi scientifica dei dati."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 34ef0b10-9270-474f-8800-eecb183bbce4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: bradsev;paulsh
ms.openlocfilehash: 78764825f2e834fa4ddb7fdc2f59418dbe736e1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-on-hello-linux-data-science-virtual-machine"></a>Analisi scientifica dei dati su hello macchina virtuale di analisi scientifica dei dati di Linux
Questa procedura dettagliata viene illustrato come tooperform attività più comuni analisi scientifica dei dati con hello VM Linux di analisi scientifica dei dati. Hello Linux Data Science macchina virtuale (DSVM) è un'immagine di macchina virtuale disponibile in Azure che sia già installato con una raccolta di strumenti utilizzati per analitica dei dati e machine learning. i componenti software chiave Hello vengono classificati in hello [hello provisioning macchina virtuale di analisi scientifica dei dati di Linux](machine-learning-data-science-linux-dsvm-intro.md) argomento. Hello immagine di macchina virtuale rende facile tooget avviato esegue l'analisi scientifica dei dati in minuti, senza dovere tooinstall e configurare ognuno di strumenti hello singolarmente. È possibile facilmente scalabilità verticale hello macchina virtuale, se necessario e arrestare quando non è in uso. caratteristiche che rendono questa risorsa flessibile e conveniente.

attività di analisi scientifica dei dati illustrate in questa procedura dettagliata Hello seguire passaggi hello illustrati in hello [processo di analisi scientifica dei dati di Team](https://azure.microsoft.com/documentation/learning-paths/data-science-process/). Questo processo fornisce un approccio sistematico toodata dell'analisi scientifica dei che consente ai team di esperti di dati tooeffectively collaborare in hello del ciclo di vita di compilazione di applicazioni intelligenti. processo di analisi scientifica dei dati Hello fornisce inoltre un framework iterativo di analisi scientifica dei dati che può essere seguito da un singolo.

Consente di analizzare hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) set di dati in questa procedura dettagliata. Si tratta di un set di messaggi di posta elettronica sono contrassegnati come posta indesiderata o ham (ovvero non sono posta indesiderata), nonché alcune statistiche per il contenuto di hello di messaggi di posta elettronica hello. statistiche Hello inclusione verranno esaminate in hello successivamente ma una sezione.

## <a name="prerequisites"></a>Prerequisiti
Prima di poter utilizzare una macchina di virtuale analisi scientifica dei dati di Linux, è necessario disporre delle seguenti hello:

* Una **sottoscrizione di Azure**. Se non è già disponibile, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/free/).
* Una [**macchina virtuale Linux per l'analisi scientifica dei dati**](https://azure.microsoft.com/marketplace/partners/microsoft-ads/linux-data-science-vm). Per informazioni sul provisioning di questa macchina virtuale, vedere [hello provisioning macchina virtuale di analisi scientifica dei dati di Linux](machine-learning-data-science-linux-dsvm-intro.md).
* [X2Go](http://wiki.x2go.org/doku.php) installato nel computer con una sessione di XFCE aperta. Per informazioni sull'installazione e la configurazione di un **client X2Go**, vedere [Installazione e configurazione del client X2Go](machine-learning-data-science-linux-dsvm-intro.md#installing-and-configuring-x2go-client). 
* Un **account Azure ML**. Se si dispone già di uno, iscriversi a uno nuovo in hello [home page di Azure ml](https://studio.azureml.net/). Non vi è un toohelp di livello di utilizzo gratuita iniziare.

## <a name="download-hello-spambase-dataset"></a>Scaricare hello spambase set di dati
Hello [spambase](https://archive.ics.uci.edu/ml/datasets/spambase) set di dati è un numero relativamente ridotto di dati che contiene solo 4601 esempi. Si tratta di un toouse dimensioni pratico per dimostrare che alcune delle funzionalità chiave di hello di hello VM di analisi scientifica dei dati che mantiene i requisiti di risorse hello adeguato.

> [!NOTE]
> Questa procedura dettagliata è stata creata in una macchina virtuale Linux per l'analisi scientifica dei dati di dimensioni D2 v2. La dimensione DSVM è in grado di gestire procedure hello in questa procedura dettagliata.
>
>

Se è necessario più spazio di archiviazione, è possibile creare ulteriori dischi e collegarli tooyour macchina virtuale. Questi dischi utilizzano permanente archiviazione di Azure, pertanto i relativi dati vengono mantenuti anche quando reprovisioning server hello scadenza tooresizing o è stato arrestato. tooadd un disco e collegarlo tooyour macchina virtuale, seguire le istruzioni hello [aggiungere una VM Linux di tooa disco](../virtual-machines/linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Questi passaggi utilizzano l'interfaccia della riga di comando Azure (Azure CLI), che è già installato in hello DSVM hello. Pertanto, queste procedure possono essere eseguite interamente da hello macchina virtuale stessa. Un'altra opzione tooincrease trovi toouse [file di Azure](../storage/files/storage-how-to-use-files-linux.md).

dati hello toodownload, aprire una finestra terminale ed eseguire questo comando:

    wget http://archive.ics.uci.edu/ml/machine-learning-databases/spambase/spambase.data

file scaricato Hello non dispone di una riga di intestazione, pertanto è necessario creare un altro file con un'intestazione. Eseguire toocreate questo comando di un file con le intestazioni appropriate hello:

    echo 'word_freq_make, word_freq_address, word_freq_all, word_freq_3d,word_freq_our, word_freq_over, word_freq_remove, word_freq_internet,word_freq_order, word_freq_mail, word_freq_receive, word_freq_will,word_freq_people, word_freq_report, word_freq_addresses, word_freq_free,word_freq_business, word_freq_email, word_freq_you, word_freq_credit,word_freq_your, word_freq_font, word_freq_000, word_freq_money,word_freq_hp, word_freq_hpl, word_freq_george, word_freq_650, word_freq_lab,word_freq_labs, word_freq_telnet, word_freq_857, word_freq_data,word_freq_415, word_freq_85, word_freq_technology, word_freq_1999,word_freq_parts, word_freq_pm, word_freq_direct, word_freq_cs, word_freq_meeting,word_freq_original, word_freq_project, word_freq_re, word_freq_edu,word_freq_table, word_freq_conference, char_freq_semicolon, char_freq_leftParen,char_freq_leftBracket, char_freq_exclamation, char_freq_dollar, char_freq_pound, capital_run_length_average,capital_run_length_longest, capital_run_length_total, spam' > headers

Quindi concatenare due file con il comando hello di hello:

    cat spambase.data >> headers
    mv headers spambaseHeaders.data

set di dati Hello dispone di diversi tipi di statistiche su ogni messaggio di posta elettronica:

* Ad esempio colonne ***word\_freq\_WORD*** indicare hello percentuale di parole nel messaggio di posta elettronica hello che corrispondono a *WORD*. Ad esempio, se *word\_freq\_rendere* è 1, quindi sono stati % 1 di tutte le parole nel messaggio di posta elettronica hello *rendere*.
* Ad esempio colonne ***char\_freq\_CHAR*** indicare hello percentuale di tutti i caratteri nel messaggio di posta elettronica hello che sono stati *CHAR*.
* ***capitale\_eseguire\_lunghezza\_più lunga*** hello la lunghezza massima di una sequenza di lettere maiuscole.
* ***capitale\_eseguire\_lunghezza\_Media*** hello lunghezza media di tutte le sequenze di lettere maiuscole.
* ***capitale\_eseguire\_lunghezza\_totale*** è hello lunghezza totale di tutte le sequenze di lettere maiuscole.
* ***posta indesiderata*** indica se posta elettronica hello è stato considerato posta indesiderata o non (1 = posta indesiderata, 0 = non spam).

## <a name="explore-hello-dataset-with-microsoft-r-open"></a>Esplorare hello set di dati con Microsoft R Open
Di seguito esaminare i dati di hello ed eseguire alcune learning macchina di base con r. hello VM di analisi scientifica dei dati viene fornito con [Microsoft R Open](https://mran.revolutionanalytics.com/open/) pre-installato. Hello librerie matematiche multithreading in questa versione di R offrono prestazioni migliori rispetto alle versioni diverse a thread singolo. Microsoft R Open fornisce inoltre la riproducibilità utilizzando uno snapshot del repository di pacchetti CRAN hello.

gli esempi utilizzati in questa procedura dettagliata, hello clone di codice tooget copie di hello **Azure-Machine-Learning--analisi scientifica dei dati** repository tramite git, di cui è preinstallato in hello macchina virtuale. Dalla riga di comando git hello, eseguire:

    git clone https://github.com/Azure/Azure-MachineLearning-DataScience.git

Aprire una finestra terminale e avviare una nuova sessione di R con la console interattiva hello R.

> [!NOTE]
> È anche possibile utilizzare RStudio per hello seguire le procedure seguenti. tooinstall RStudio, eseguire il comando seguente in un terminal:`./Desktop/DSVM\ tools/installRStudio.sh`
>
>

dati hello tooimport e configurare l'ambiente di hello, eseguire:

    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

toosee le statistiche di riepilogo su ogni colonna:

    summary(data)

Per una visualizzazione diversa dei dati hello:

    str(data)

Questo mostra è hello tipo di ogni variabile e hello innanzitutto alcuni valori nel set di dati hello.

Hello *posta indesiderata* colonna è stato letto come un numero intero, ma è effettivamente un categorico variabile (o fattore). tooset il relativo tipo:

    data$spam <- as.factor(data$spam)

toodo alcune analisi esplorativa, utilizzare hello [ggplot2](http://ggplot2.org/) del pacchetto, una libreria grafica diffusa per R che è già installata nella macchina virtuale hello. Si noti, dai dati di riepilogo hello visualizzati in precedenza, la presenza di statistiche di riepilogo sulla frequenza di hello del carattere punto esclamativo hello. Si tracciare le frequenze qui con hello seguenti comandi:

    library(ggplot2)
    ggplot(data) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Poiché la barra hello zero è inclinazione tracciato hello, consente la rimozione:

    email_with_exclamation = data[data$char_freq_exclamation > 0, ]
    ggplot(email_with_exclamation) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

La densità non semplice superiore a 1 sembra interessante. Per esaminare solo quei dati, eseguire:

    ggplot(data[data$char_freq_exclamation > 1, ]) + geom_histogram(aes(x=char_freq_exclamation), binwidth=0.25)

Per dividere quindi i dati in posta indesiderata e non indesiderata, eseguire:

    ggplot(data[data$char_freq_exclamation > 1, ], aes(x=char_freq_exclamation)) +
    geom_density(lty=3) +
    geom_density(aes(fill=spam, colour=spam), alpha=0.55) +
    xlab("spam") +
    ggtitle("Distribution of spam \nby frequency of !") +
    labs(fill="spam", y="Density")

Questi esempi dovrebbero consentire di toomake grafici simili di hello tooexplore altre colonne hello dati in essi contenuti.

## <a name="train-and-test-an-ml-model"></a>Eseguire il training di un modello ML e testarlo
Ora si train un paio di machine learning modelli di messaggi di posta elettronica hello tooclassify nel set di dati hello come contenente span o ham. Questa sezione illustra come eseguire il training di un modello di albero delle decisioni e di un modello di foresta casuale e quindi testarne la correttezza delle previsioni.

> [!NOTE]
> Hello rpart (partizionamento ricorsivo e alberi di regressione) utilizzato nel seguente codice hello è già installato su hello VM di analisi scientifica dei dati.
>
>

In primo luogo, si suddividere hello set di dati in set di training e di test:

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

Creare quindi un hello tooclassify di albero delle decisioni messaggi di posta elettronica.

    require(rpart)
    model.rpart <- rpart(spam ~ ., method = "class", data = trainSet)
    plot(model.rpart)
    text(model.rpart)

Di seguito è riportato il risultato di hello:

![1](./media/machine-learning-data-science-linux-dsvm-walkthrough/decision-tree.png)

toodetermine sulle prestazioni per la formazione di hello impostato, utilizzare hello seguente codice:

    trainSetPred <- predict(model.rpart, newdata = trainSet, type = "class")
    t <- table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

il grado di toodetermine che esegue nel set di test hello:

    testSetPred <- predict(model.rpart, newdata = testSet, type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy

Viene ora esaminato un modello di foresta casuale. Foreste casuali eseguire il training di una grande varietà di alberi delle decisioni e di output di una classe che è la modalità di hello di classificazioni hello da tutti gli alberi delle decisioni singoli di hello. Forniscono un computer più potente apprendimento approccio come saranno corretti per la tendenza hello di un toooverfit modello di albero delle decisioni un set di dati di training.

    require(randomForest)
    trainVars <- setdiff(colnames(data), 'spam')
    model.rf <- randomForest(x=trainSet[, trainVars], y=trainSet$spam)

    trainSetPred <- predict(model.rf, newdata = trainSet[, trainVars], type = "class")
    table(`Actual Class` = trainSet$spam, `Predicted Class` = trainSetPred)

    testSetPred <- predict(model.rf, newdata = testSet[, trainVars], type = "class")
    t <- table(`Actual Class` = testSet$spam, `Predicted Class` = testSetPred)
    accuracy <- sum(diag(t))/sum(t)
    accuracy


## <a name="deploy-a-model-tooazure-ml"></a>Distribuire un tooAzure modello ML
[Azure Machine Learning Studio](https://studio.azureml.net/) (Azure ml) è un servizio cloud che rende facile toobuild e distribuisce modelli analitica predittiva. Una delle funzionalità di nice hello di Azure ml è toopublish il possibilità qualsiasi R funzione come un servizio web. Hello pacchetto R AzureML rende toodo di facile distribuzione direttamente dal nostro sessione R per hello DSVM.

toodeploy codice albero delle decisioni di hello dalla sezione precedente di hello, è necessario toosign in tooAzure Machine Learning Studio. È necessario l'ID dell'area di lavoro e un toosign del token di autorizzazione in. toofind i valori e inizializzare le variabili di Azure ml hello con essi:

Selezionare **impostazioni** dal menu a sinistra di hello. Prendere nota del valore **WORKSPACE ID**(ID area di lavoro). ![2](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-id.png)

Selezionare **token di autorizzazione** dal menu overhead hello e prendere nota del **primario Token di autorizzazione**.![ 3](./media/machine-learning-data-science-linux-dsvm-walkthrough/workspace-token.png)

Hello carico **Azure ml** del pacchetto e quindi impostare i valori delle variabili di hello con l'ID di token e l'area di lavoro nella sessione di R in hello DSVM:

    require(AzureML)
    wsAuth = "<authorization-token>"
    wsID = "<workspace-id>"


Consente di semplificare hello modello toomake tooimplement di più facile questa dimostrazione. Selezionare hello tre variabili nella radice toohello più vicino di hello decisione dell'albero e compilare un nuovo albero utilizzando solo le tre variabili:

    colNames <- c("char_freq_dollar", "word_freq_remove", "word_freq_hp", "spam")
    smallTrainSet <- trainSet[, colNames]
    smallTestSet <- testSet[, colNames]
    model.rpart <- rpart(spam ~ ., method = "class", data = smallTrainSet)

Abbiamo bisogno di una funzione di stima che utilizza le funzionalità di hello come input e restituisce hello valori stimati:

    predictSpam <- function(char_freq_dollar, word_freq_remove, word_freq_hp) {
        predictDF <- predict(model.rpart, data.frame("char_freq_dollar" = char_freq_dollar,
        "word_freq_remove" = word_freq_remove, "word_freq_hp" = word_freq_hp))
        return(colnames(predictDF)[apply(predictDF, 1, which.max)])
    }

Pubblicare hello predictSpam funzione tooAzureML utilizzando hello **publishWebService** funzione:

    spamWebService <- publishWebService("predictSpam",
        "spamWebService",
        list("char_freq_dollar"="float", "word_freq_remove"="float","word_freq_hp"="float"),
        list("spam"="int"),
        wsID, wsAuth)

Questa funzione accetta hello **predictSpam** di funzione, viene creato un servizio web denominato **spamWebService** con definito input e output e restituisce informazioni sul nuovo endpoint hello.

Visualizzazione dei dettagli di hello ha pubblicato il servizio, incluse le chiavi di accesso e l'endpoint API con il comando hello:

    spamWebService[[2]]

tootry impostarlo su hello prime 10 righe del set di test hello:

    consumeDataframe(spamWebService$endpoints[[1]]$PrimaryKey, spamWebService$endpoints[[1]]$ApiLocation, smallTestSet[1:10, 1:3])


## <a name="use-other-tools-available"></a>Usare altri strumenti disponibili
nelle restanti sezioni Hello mostrano come toouse alcuni degli strumenti hello installato hello VM Linux di analisi scientifica dei dati. Ecco hello elenco degli strumenti illustrati:

* XGBoost
* Python
* JupyterHub
* Rattle
* PostgreSQL e Squirrel SQL
* SQL Server Data Warehouse

## <a name="xgboost"></a>XGBoost
[XGBoost](https://xgboost.readthedocs.org/en/latest/) è uno strumento che consente un'implementazione di albero con boosting rapida e accurata.

    require(xgboost)
    data <- read.csv("spambaseHeaders.data")
    set.seed(123)

    rnd <- runif(dim(data)[1])
    trainSet = subset(data, rnd <= 0.7)
    testSet = subset(data, rnd > 0.7)

    bst <- xgboost(data = data.matrix(trainSet[,0:57]), label = trainSet$spam, nthread = 2, nrounds = 2, objective = "binary:logistic")

    pred <- predict(bst, data.matrix(testSet[, 0:57]))
    accuracy <- 1.0 - mean(as.numeric(pred > 0.5) != testSet$spam)
    print(paste("test accuracy = ", accuracy))

XGBoost permette anche di eseguire chiamate da Python o da una riga di comando.

## <a name="python"></a>Python
Per lo sviluppo usando Python, distribuzioni di hello Anaconda Python 2.7 e 3.5 sono state installate in hello DSVM.

> [!NOTE]
> include Hello distribuzione Anaconda [Condas](http://conda.pydata.org/docs/index.html), che può essere utilizzato toocreate ambienti personalizzati per Python con diverse versioni e/o i pacchetti installati in essi contenuti.
>
>

Consente di lettura in alcuni set di dati spambase hello e classificare i messaggi di posta elettronica hello con macchine a vettori di supporto in scikit-informazioni su:

    import pandas
    from sklearn import svm    
    data = pandas.read_csv("spambaseHeaders.data", sep = ',\s*')
    X = data.ix[:, 0:57]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toomake stime:

    clf.predict(X.ix[0:20, :])

tooshow come toopublish un endpoint di Azure ml, si crea un modello più semplice hello tre variabili come abbiamo quando è pubblicato il modello R hello in precedenza.

    X = data.ix[["char_freq_dollar", "word_freq_remove", "word_freq_hp"]]
    y = data.ix[:, 57]
    clf = svm.SVC()
    clf.fit(X, y)

toopublish hello modello tooAzureML:

    # Publish hello model.
    workspace_id = "<workspace-id>"
    workspace_token = "<workspace-token>"
    from azureml import services
    @services.publish(workspace_id, workspace_token)
    @services.types(char_freq_dollar = float, word_freq_remove = float, word_freq_hp = float)
    @services.returns(int) # 0 or 1
    def predictSpam(char_freq_dollar, word_freq_remove, word_freq_hp):
        inputArray = [char_freq_dollar, word_freq_remove, word_freq_hp]
        return clf.predict(inputArray)

    # Get some info about hello resulting model.
    predictSpam.service.url
    predictSpam.service.api_key

    # Call hello model
    predictSpam.service(1, 1, 1)

> [!NOTE]
> È disponibile solo per Python 2.7 e non è ancora supportato nella versione 3.5. Eseguire con **/anaconda/bin/python2.7**.
>
>

## <a name="jupyterhub"></a>JupyterHub
distribuzione Anaconda Hello in hello DSVM viene fornito con un server Jupyter notebook, un codice di Julia, Python o R tooshare ambiente multipiattaforma e analisi. notebook Jupyter Hello è accessibile tramite JupyterHub. Per eseguire l'accesso, usare il nome utente e la password locali di ***https://\<Nome DNS o indirizzo IP della VM\>:8000/***. Tutti i file di configurazione per JupyterHub si trovano nella directory **/etc/jupyterhub**.

Numerosi blocchi appunti di esempio sono già installati nel hello VM:

* Vedere hello [IntroToJupyterPython.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroToJupyterPython.ipynb) per un raccoglitore di Python di esempio.
* Per un notebook di [R](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IntroTutorialinR.ipynb) di esempio, vedere **IntroTutorialinR** .
* Vedere hello [IrisClassifierPyMLWebService](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Data-Science-Virtual-Machine/Samples/Notebooks/IrisClassifierPyMLWebService.ipynb) per un altro esempio **Python** notebook.

> [!NOTE]
> linguaggio Julia Hello è disponibile anche dalla riga di comando hello in hello VM Linux di analisi scientifica dei dati.
>
>

## <a name="rattle"></a>Rattle
[Rattle](https://cran.r-project.org/web/packages/rattle/index.html) (strumento di analisi R tooLearn hello facilmente) è uno strumento grafico R per il data mining. Ha un'interfaccia intuitiva che rende facile tooload, esplorare e trasformare i dati e compilare e valutare i modelli.  articolo Hello [Rattle: GUI di Data Mining dati A per R](https://journal.r-project.org/archive/2009-2/RJournal_2009-2_Williams.pdf) fornisce una procedura dettagliata che illustra le funzionalità.

Installare e avviare sonagli con hello seguenti comandi:

    if(!require("rattle")) install.packages("rattle")
    require(rattle)
    rattle()

> [!NOTE]
> Su hello DSVM non è necessaria l'installazione. Ma sonagli venga chiesto di pacchetti aggiuntivi tooinstall durante il caricamento.
>
>

Rattle usa un'interfaccia basata su schede. La maggior parte delle schede hello corrisponde toosteps in hello [il processo di analisi scientifica dei dati](https://azure.microsoft.com/documentation/learning-paths/data-science-process/), ad esempio il caricamento dei dati o esplorazione. processo di analisi scientifica dei dati Hello flusso da sinistra tooright tramite schede hello. Ma l'ultima scheda hello contiene un log di comandi hello R eseguiti da sonagli.

tooload e configurare i set di dati hello:

* file hello tooload, seleziona hello **dati** scheda, quindi
* Scegliere il selettore di hello successivo troppo**Filename** e scegliere **spambaseHeaders.data**.
* file hello tooload. Selezionare **Execute** nella riga superiore di hello dei pulsanti. Verrà visualizzato un riepilogo di ogni colonna, incluso il tipo di dati identificato, se si tratta di un input, una destinazione o altro tipo di variabile e il numero di hello di valori univoci.
* Sonaglio ha identificato correttamente hello **posta indesiderata** colonna come destinazione di hello. Colonna di hello selezionare posta indesiderata, quindi hello set **il tipo di dati di destinazione** troppo**Categoric**.

dati hello tooexplore:

* Seleziona hello **Esplora** scheda.
* Fare clic su **riepilogo**, quindi **Execute**, toosee alcune informazioni sui tipi di variabile hello e alcune statistiche di riepilogo.
* tooview altri tipi di statistiche relative a ogni variabile, selezionare altre opzioni come **descrizione** o **nozioni di base**.

Hello **Esplora** scheda consente anche toogenerate molti dettagliati vengono tracciati. un istogramma che mostra i dati di hello tooplot:

* Scegliere **Distributions**(Distribuzioni).
* Selezionare **Histogram** (Istogramma) per **word_freq_remove** e **word_freq_you**.
* Scegliere **Execute**(Esegui). Dovrebbe essere che entrambi densità è rappresentata in un'unica area grafica, in cui è possibile determinare tale parola hello "si" viene visualizzato più spesso in messaggi di posta elettronica di "Rimuovi".

grafici di correlazione Hello sono interessanti. toocreate uno:

* Scegliere **correlazione** come hello **tipo**, quindi
* Scegliere **Execute**(Esegui).
* Rattle avvisa l'utente che è consigliabile usare un massimo di 40 variabili. Selezionare **Sì** tracciato hello tooview.

Esistono alcune correlazioni interessanti che sono: "la tecnologia" è strettamente correlata troppo "HP" e "lab", ad esempio. Si è anche strettamente correlato troppo "650", perché il codice di area hello donatori di set di dati hello è 650.

i valori numerici Hello per le correlazioni hello tra le parole sono disponibili nella finestra Esplora hello. È interessante toonote, ad esempio, che "tecnologia" negativamente sia correlata con "i" e "money".

Sonaglio può trasformare hello dataset toohandle alcuni problemi comuni. Ad esempio, consente la funzionalità toorescale, attribuire valori mancanti, gestire gli outlier e rimuovere le variabili o le osservazioni con i dati mancanti. Rattle può anche identificare le regole di associazione tra le osservazioni e/o le variabili. Queste schede non rientrano nell'ambito di questa procedura dettagliata introduttiva.

Rattle permette anche di eseguire l'analisi a cluster. Consente di escludere alcuni tooread più facilmente funzionalità toomake hello output. In hello **dati** scegliere **ignora** tooeach successivo delle variabili di hello ad eccezione di questi dieci elementi:

* word_freq_hp
* word_freq_technology
* word_freq_george
* word_freq_remove
* word_freq_your
* word_freq_dollar
* word_freq_money
* capital_run_length_longest
* word_freq_business
* spam

Tornare toohello **Cluster** scegliere **KMeans**e set hello *numero di cluster* too4. Scegliere **Execute**(Esegui). Hello risultati vengono visualizzati nella finestra di output di hello. Un cluster ha una frequenza elevata di "george" e "hp" ed è probabilmente un messaggio di lavoro legittimo.

un modello di machine learning di albero decisionale toobuild:

* Seleziona hello **modello** scheda
* Scegliere **albero** come hello **tipo**.
* Selezionare **Execute** albero hello toodisplay forma testo hello nella finestra di output.
* Seleziona hello **disegnare** pulsante tooview una versione con interfaccia grafica. Questa è molto simile a quello dell'albero toohello sono stati ottenuti in precedenza mediante *rpart*.

Una delle funzionalità di nice hello di sonagli è toorun il possibilità di apprendimento diversi metodi e valutarli rapidamente. Ecco la procedura hello:

* Scegliere **tutti** per hello **tipo**.
* Scegliere **Execute**(Esegui).
* Al termine è possibile fare clic su ogni singolo **tipo**, ad esempio **SVM**e visualizzare i risultati di hello.
* È inoltre possibile confrontare le prestazioni di hello dei modelli di hello sulla convalida hello impostato utilizzando hello **Evaluate** scheda. Ad esempio, hello **errore matrice** selezione Mostra la matrice di confusione hello, errore generale e di errore di classe Media per ogni modello nel set convalida hello.
* È anche possibile tracciare le curve ROC, eseguire analisi di sensibilità e altri tipi di valutazioni del modello.

Dopo aver terminato la compilazione di modelli, selezionare hello **Log** scheda codice hello R tooview eseguito da sonagli durante la sessione. È possibile selezionare hello **esportare** toosave pulsante è.

> [!NOTE]
> La versione corrente di Rattle contiene un bug. toomodify hello script o utilizzarla toorepeat i passaggi in un secondo momento, è necessario inserire un carattere # davanti * esportare questo file di registro... * nel testo hello del log hello.
>
>

## <a name="postgresql--squirrel-sql"></a>PostgreSQL e Squirrel SQL
Hello DSVM include PostgreSQL installato. PostgreSQL è un sofisticato database relazionale open source. Questa sezione viene illustrato come tooload il set di dati di posta indesiderata in PostgreSQL e quindi eseguire una query.

Prima di caricare dati hello, è necessario l'autenticazione di password tooallow da hello localhost. Al prompt dei comandi, eseguire:

    sudo gedit /var/lib/pgsql/data/pg_hba.conf

Nella parte inferiore di hello hello del file di configurazione sono più righe in cui vengono hello connessioni consentita:

    # "local" is for Unix domain socket connections only
    local   all             all                                     trust
    # IPv4 local connections:
    host    all             all             127.0.0.1/32            ident
    # IPv6 local connections:
    host    all             all             ::1/128                 ident

Modificare hello "IPv4 le connessioni locali" riga toouse md5 anziché ident, pertanto è possibile accedere con un nome utente e password:

    # IPv4 local connections:
    host    all             all             127.0.0.1/32            md5

E riavviare il servizio di postgres hello:

    sudo systemctl restart postgresql

toolaunch psql, un terminale interactive per PostgreSQL, come utente postgres incorporato hello, eseguire hello comando seguente da un prompt dei comandi:

    sudo -u postgres psql

Creare un nuovo account utente, utilizzando hello stesso nome utente come account Linux attualmente si è connessi come hello e assegnare una password:

    CREATE USER <username> WITH CREATEDB;
    CREATE DATABASE <username>;
    ALTER USER <username> password '<password>';
    \quit

Accedere quindi toopsql come l'utente:

    psql

E l'importazione di dati di hello in un nuovo database:

    CREATE DATABASE spam;
    \c spam
    CREATE TABLE data (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer);
    \copy data FROM /home/<username>/spambase.data DELIMITER ',' CSV;
    \quit

A questo punto, consente di esplorare i dati di hello ed eseguire alcune query utilizzando **esce SQL**, uno strumento grafico che consente di interagire con i database tramite un driver JDBC.

tooget avviato, avviare SQL esce dal menu di applicazioni hello. tooset driver hello:

* Selezionare **Windows** e quindi **View Drivers** (Visualizza driver).
* Fare clic con il pulsante destro del mouse su **PostgreSQL** e selezionare **Modify Driver** (Modifica driver).
* Selezionare **Extra Class Path** (Percorso classe extra) e quindi **Add** (Aggiungi).
* Immettere ***/usr/share/java/jdbcdrivers/postgresql-9.4.1208.jre6.jar*** per hello **nome File** e
* Scegliere **Open**(Apri).
* Scegliere List Drivers (Elenca driver), selezionare **org.postgresql.Driver** in **Class Name** (Nome classe) e quindi scegliere **OK**.

tooset di server locali di hello connessione toohello:

* Selezionare **Windows** e quindi **View Aliases** (Visualizza alias).
* Scegliere hello  **+**  pulsante toomake un nuovo alias.
* Il nome *database posta indesiderata*, scegliere **PostgreSQL** in hello **Driver** elenco a discesa.
* Impostare l'URL di hello troppo*jdbc:postgresql://localhost/spam*.
* Immettere il proprio *nome utente* e la *password*.
* Fare clic su **OK**.
* hello tooopen **connessione** finestra, fare doppio clic su hello ***database posta indesiderata*** alias.
* Selezionare **Connessione**.

toorun alcune query:

* Seleziona hello **SQL** scheda.
* Immettere una query semplice, ad esempio `SELECT * from data;` nella casella di testo query hello nella parte superiore di hello della scheda SQL hello.
* Premere **Ctrl-Invio** toorun è. Per impostazione predefinita esce SQL restituisce hello prime 100 righe della query.

Esistono numerose altre query che è possibile eseguire tooexplore questi dati. Ad esempio, funzionamento hello frequenza della parola hello *rendere* differiscono tra posta indesiderata e ham?

    SELECT avg(word_freq_make), spam from data group by spam;

O le caratteristiche di hello di posta elettronica che contengono spesso *3d*?

    SELECT * from data order by word_freq_3d desc;

La maggior parte dei messaggi di posta elettronica dispone di un'occorrenza elevata di *3d* sono apparentemente inviare posta indesiderata, pertanto potrebbe essere una funzionalità utile per la creazione di messaggi di posta elettronica un hello tooclassify modello predittivo.

Se si desidera tooperform l'apprendimento con i dati archiviati in un database PostgreSQL, è consigliabile utilizzare [MADlib](http://madlib.incubator.apache.org/).

## <a name="sql-server-data-warehouse"></a>SQL Server Data Warehouse
Azure SQL Data Warehouse è un database basato sul cloud, con possibilità di aumentare il numero di istanze, che può elaborare volumi massivi di dati sia relazionali che non relazionali. Per altre informazioni, vedere [Informazioni su Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md)

tooconnect toohello dati del data warehouse e creazione tabella hello hello esecuzione seguente comando al prompt dei comandi:

    sqlcmd -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -I

Al prompt dei comandi sqlcmd hello:

    CREATE TABLE spam (word_freq_make real, word_freq_address real, word_freq_all real, word_freq_3d real,word_freq_our real, word_freq_over real, word_freq_remove real, word_freq_internet real,word_freq_order real, word_freq_mail real, word_freq_receive real, word_freq_will real,word_freq_people real, word_freq_report real, word_freq_addresses real, word_freq_free real,word_freq_business real, word_freq_email real, word_freq_you real, word_freq_credit real,word_freq_your real, word_freq_font real, word_freq_000 real, word_freq_money real,word_freq_hp real, word_freq_hpl real, word_freq_george real, word_freq_650 real, word_freq_lab real,word_freq_labs real, word_freq_telnet real, word_freq_857 real, word_freq_data real,word_freq_415 real, word_freq_85 real, word_freq_technology real, word_freq_1999 real,word_freq_parts real, word_freq_pm real, word_freq_direct real, word_freq_cs real, word_freq_meeting real,word_freq_original real, word_freq_project real, word_freq_re real, word_freq_edu real,word_freq_table real, word_freq_conference real, char_freq_semicolon real, char_freq_leftParen real,char_freq_leftBracket real, char_freq_exclamation real, char_freq_dollar real, char_freq_pound real, capital_run_length_average real, capital_run_length_longest real, capital_run_length_total real, spam integer) WITH (CLUSTERED COLUMNSTORE INDEX, DISTRIBUTION = ROUND_ROBIN);
    GO

Per copiare dati con bcp, eseguire:

    bcp spam in spambaseHeaders.data -q -c -t  ',' -S <server-name>.database.windows.net -d <database-name> -U <username> -P <password> -F 1 -r "\r\n"

> [!NOTE]
> bcp prevista di tipo UNIX, perciò dobbiamo bcp tootell che con il flag - r hello terminazioni riga Hello file scaricato hello sono stile di Windows.
>
>

Eseguire query con sqlcmd:

    select top 10 spam, char_freq_dollar from spam;
    GO

È anche possibile eseguire query con Squirrel SQL. Ripetere i passaggi simili per PostgreSQL, tramite il quale è reperibile in hello Microsoft MSSQL Server JDBC Driver ***/usr/share/java/jdbcdrivers/sqljdbc42.jar***.

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica degli argomenti che consentono di eseguire attività di hello che costituiscono il processo di analisi scientifica dei dati hello in Azure, vedere [processo di analisi scientifica dei dati di Team](http://aka.ms/datascienceprocess).

Per una descrizione di altre procedure dettagliate end-to-end che illustrano i passaggi hello hello Team processo di analisi scientifica dei dati per scenari specifici, vedere [procedure dettagliate di processo di analisi scientifica dei dati di Team](data-science-process-walkthroughs.md). procedure dettagliate di Hello anche illustrano come toocombine cloud e locali strumenti e servizi in un flusso di lavoro o la pipeline di toocreate un'applicazione intelligente.
