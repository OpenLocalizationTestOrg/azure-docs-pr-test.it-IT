---
title: Analisi di sopravvivenza con Azure Machine Learning AAA(deprecated) | Documenti Microsoft
description: "(Deprecato) Probabilità che si verifichino eventi di analisi di sopravvivenza"
services: machine-learning
documentationcenter: 
author: zhangya
manager: jhubbard
editor: cgronlun
ms.assetid: a142fc45-cdfb-4971-910e-05dab8bc699e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: zhangya
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: af946d8df5ba650a9d74fbabbe3b15d3a07dd508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-survival-analysis"></a>(Deprecato) Analisi di sopravvivenza

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

In molti scenari, risultato principale di hello in valutazione è evento tooan hello di interesse. In altre parole, domanda hello "quando l'evento si verifica?" è la domanda che viene posta. Esempi, provare a situazioni in cui i dati di hello descrivono hello tempo (giorni, anni, chilometraggio e così via) fino a quando hello si verifica l'evento di interesse (relapse malattia, gradi PhD ricevuto, riempimento freni errore). Ogni istanza dei dati hello rappresenta un oggetto specifico (un paziente, uno studente, un'automobile e così via).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) risponde domanda hello "che cos'è la probabilità hello che hello evento di interesse verrà eseguita da n tempo per l'oggetto x?" Fornendo un modello di analisi di sopravvivenza, il servizio web consente agli utenti toosupply dati tootrain hello modello e testarlo. tema principale di Hello dell'esperimento hello è toomodel hello hello trascorso tempo fino a quando non si verifica l'evento hello di interesse. 

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
schema di dati di input Hello del servizio web hello viene visualizzato in hello nella tabella seguente. Sono necessari sei tipi di informazioni come input hello: dati di training, dati di testing, tempo di interesse, indice hello della dimensione "ora", l'indice di hello della dimensione "evento" e i tipi di variabile hello (continua o fattore). dati di training Hello sono rappresentati con una stringa, in cui le righe di hello sono separate da virgola e hello colonne sono separate da punto e virgola. numero di Hello delle funzionalità dei dati hello è flessibile. Tutti gli elementi di hello nella stringa di input hello devono essere numerici. Nei dati di training hello, dimensione temporale"hello" indica il numero di hello di unità di tempo (giorni, anni, chilometraggio e così via) trascorso dal punto di partenza hello di hello studiare (un paziente ricezione programmi trattamento somministrato il farmaco, uno Studio PhD inizio studente, un'automobile avvio toobe basato su, ecc.) fino a quando non hello evento di interesse (paziente hello restituzione toodrug utilizzo, grado di dottorato di hello studente ottenere hello, car hello con errore freni riempimento e così via) si verifica. dimensione di "evento" Hello indica se alla fine hello Studio hello evento hello di interesse. Il valore "evento = 1" significa che l'evento di interesse hello avviene in fase di hello indicato dalla dimensione di "temporale" hello; "evento = 0" indica che l'evento di interesse hello non si è verificato hello di tempo indicato dalla dimensione di "ora" hello.

* trainingdata: una stringa di caratteri. Le righe sono separate da virgola e le colonne sono separate da punto e virgola. Ogni riga include la dimensione "time", la dimensione "event" e le variabili del predittore.
* testingdata: una riga di dati che include variabili di predittore per un oggetto specifico.
* time_of_interest - hello tempo di interesse n.
* index_time - indice di colonna hello della dimensione di "temporale" hello (a partire da 1).
* index_event - indice di colonna hello della dimensione "evento" hello (a partire da 1).
* variable_types: stringa di caratteri con punto e virgola come separatore. 0 rappresenta le variabili continue e 1 variabili di fattore.

output di Hello è hello probabilità di un evento che si verifica entro una data specifica. 

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)). 

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
    public class Input
    {
            public string trainingdata;
            public string testingdata;
            public string timeofinterest;
            public string indextime;
            public string indexevent;
            public string variabletypes;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { trainingdata = TextBox1.Text, testingdata = TextBox2.Text, timeofinterest = TextBox3.Text, indextime = TextBox4.Text, indexevent = TextBox5.Text, variabletypes = TextBox6.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }




interpretazione di Hello di questo test è come indicato di seguito. Presupponendo che l'obiettivo di hello di dati hello è il tempo trascorso hello toomodel finché hello restituire toodrug utilizzo per pazienti hello che hanno ricevuto uno dei programmi di hello due modalità di gestione. output di hello web servizio letture Hello: per pazienti da 35 anni, con precedente libbre di farmaco trattamento 2 volte, prendendo programma trattamento tempo residenziale hello, e con l'utilizzo di heroin sia cocaine, probabilità hello di restituzione utilizzo somministrato il farmaco toohello 95.64% by giorno 500.

## <a name="creation-of-web-service"></a>Creazione del servizio Web
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli sono stati estratti nell'area di lavoro hello. Hello dello schema di dati è stato creato con una semplice [Execute R Script][execute-r-script], che definisce schema dati di input hello per il servizio web hello. Questo modulo viene quindi collegato secondo toohello [Execute R Script] [ execute-r-script] modulo, che di lavoro principale. ovvero la pre-elaborazione dei dati, la compilazione dei modelli e le previsioni. In fase di pre-elaborazione dei dati hello, i dati di input hello rappresentati da una stringa lunga viene trasformati e convertiti in un frame di dati. Nel passaggio di compilazione del modello di hello, un pacchetto R esterno "survival_2.37 7.zip" prima di tutto è installato per l'esecuzione di analisi di sopravvivenza. Funzione "coxph" hello viene quindi eseguito dopo un'attività di elaborazione dei dati della serie. Dettagli Hello della funzione "coxph" hello per l'analisi di sopravvivenza possono essere letti dalla documentazione hello R. Nel passaggio di stima hello, viene fornita un'istanza di test nel modello con training a hello con funzione di "surfit" hello, e curva sopravvivenza hello per questa istanza di test viene prodotto come variabile "curve". Infine, viene ottenuto probabilità hello di tempo hello di interesse. 

### <a name="experiment-flow"></a>Flusso dell'esperimento
![flusso dell'esperimento][1]

#### <a name="module-1"></a>Modulo 1:
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data toooutput port

#### <a name="module-2"></a>Modulo 2:
    #Read data from input port
    data <- maml.mapInputPort(1) 
    colnames(data) <- c("trainingdata","testingdata","time_of_interest","index_time","index_event","variable_types")

    # Preprocessing training data
    traindingdata=data$trainingdata
    y=strsplit(as.character(data$trainingdata),",")
    n_row=length(unlist(y))
    z=sapply(unlist(y), strsplit, ";", simplify = TRUE)
    mydata <- data.frame(matrix(unlist(z), nrow=n_row, byrow=T), stringsAsFactors=FALSE)
    n_col=ncol(mydata)

    # Preprocessing testing data
    testingdata=as.character(data$testingdata)
    testingdata=unlist(strsplit(testingdata,";"))

    # Preprocessing other input parameters
    time_of_interest=data$time_of_interest
    time_of_interest=as.numeric(as.character(time_of_interest))
    index_time = data$index_time
    index_event = data$index_event
    variable_types = data$variable_types

    # Necessary R packages
    install.packages("src/packages_survival/survival_2.37-7.zip",lib=".",repos=NULL,verbose=TRUE)
    library(survival)

    # Prepare toobuild model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct hello execution string
    for (i in 1:len){
    if(i==len){
    if(variable_types[i]!=0){ c=paste(c, "factor(",v_predictors[i],")",sep="")}
     else{ c=paste(c, v_predictors[i])}
    }else{
    if(variable_types[i]!=0){c=paste(c, "factor(",v_predictors[i],") + ",sep="")}
    else{c=paste(c, v_predictors[i],"+")}
    }
    }
    f=paste("coxph(Surv(",d_time,",",d_event,") ~")
    f=paste(f,c)
    f=paste(f,", data=mydata )")

    # Fit a Cox proportional hazards model and get hello predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find hello event occurrence probability
    position_closest=which.min(abs(prob_event$time - time_of_interest))

    if(prob_event[position_closest,"time"]==time_of_interest){# exact match
    output=prob_event[position_closest,"prob"]
    }else{# not exact match
    if(time_of_interest>max(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else if(time_of_interest<min(prob_event$time)){
    output=prob_event[position_closest,"prob"]
    }else{output=(prob_event[position_closest,"prob"]+prob_event[position_closest+1,"prob"])/2}
    }

    #Pull out results toosend tooweb service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a>Limitazioni
Questo servizio Web può accettare solo valori numerici come variabili della funzionalità (colonne). colonna "evento" Hello può richiedere solo valore 0 o 1. colonna "tempo" Hello deve toobe un numero intero positivo.

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

