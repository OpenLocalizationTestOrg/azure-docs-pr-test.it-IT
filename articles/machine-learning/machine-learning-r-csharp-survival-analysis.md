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
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="74d77-103">(Deprecato) Analisi di sopravvivenza</span><span class="sxs-lookup"><span data-stu-id="74d77-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="74d77-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="74d77-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="74d77-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="74d77-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="74d77-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="74d77-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="74d77-107">In molti scenari, risultato principale di hello in valutazione è evento tooan hello di interesse.</span><span class="sxs-lookup"><span data-stu-id="74d77-107">Under many scenarios, hello main outcome under assessment is hello time tooan event of interest.</span></span> <span data-ttu-id="74d77-108">In altre parole, domanda hello "quando l'evento si verifica?"</span><span class="sxs-lookup"><span data-stu-id="74d77-108">In other words, hello question “when this event will occur?”</span></span> <span data-ttu-id="74d77-109">è la domanda che viene posta.</span><span class="sxs-lookup"><span data-stu-id="74d77-109">is asked.</span></span> <span data-ttu-id="74d77-110">Esempi, provare a situazioni in cui i dati di hello descrivono hello tempo (giorni, anni, chilometraggio e così via) fino a quando hello si verifica l'evento di interesse (relapse malattia, gradi PhD ricevuto, riempimento freni errore).</span><span class="sxs-lookup"><span data-stu-id="74d77-110">As examples, consider situations where hello data describes hello elapsed time (days, years, mileage, etc.) until hello event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="74d77-111">Ogni istanza dei dati hello rappresenta un oggetto specifico (un paziente, uno studente, un'automobile e così via).</span><span class="sxs-lookup"><span data-stu-id="74d77-111">Each instance in hello data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="74d77-112">Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) risponde domanda hello "che cos'è la probabilità hello che hello evento di interesse verrà eseguita da n tempo per l'oggetto x?"</span><span class="sxs-lookup"><span data-stu-id="74d77-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers hello question “what is hello probability that hello event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="74d77-113">Fornendo un modello di analisi di sopravvivenza, il servizio web consente agli utenti toosupply dati tootrain hello modello e testarlo.</span><span class="sxs-lookup"><span data-stu-id="74d77-113">By providing a survival analysis model, this web service enables users toosupply data tootrain hello model and test it.</span></span> <span data-ttu-id="74d77-114">tema principale di Hello dell'esperimento hello è toomodel hello hello trascorso tempo fino a quando non si verifica l'evento hello di interesse.</span><span class="sxs-lookup"><span data-stu-id="74d77-114">hello main theme of hello experiment is toomodel hello length of hello elapsed time until hello event of interest occurs.</span></span> 

> <span data-ttu-id="74d77-115">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="74d77-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="74d77-116">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="74d77-116">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="74d77-117">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="74d77-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="74d77-118">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="74d77-118">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="74d77-119">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="74d77-119">Consumption of web service</span></span>
<span data-ttu-id="74d77-120">schema di dati di input Hello del servizio web hello viene visualizzato in hello nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="74d77-120">hello input data schema of hello web service is shown in hello following table.</span></span> <span data-ttu-id="74d77-121">Sono necessari sei tipi di informazioni come input hello: dati di training, dati di testing, tempo di interesse, indice hello della dimensione "ora", l'indice di hello della dimensione "evento" e i tipi di variabile hello (continua o fattore).</span><span class="sxs-lookup"><span data-stu-id="74d77-121">Six pieces of information are needed as hello input: training data, testing data, time of interest, hello index of "time" dimension, hello index of "event" dimension, and hello variable types (continuous or factor).</span></span> <span data-ttu-id="74d77-122">dati di training Hello sono rappresentati con una stringa, in cui le righe di hello sono separate da virgola e hello colonne sono separate da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="74d77-122">hello training data is represented with a string, where hello rows are separated by comma, and hello columns are separated by semicolon.</span></span> <span data-ttu-id="74d77-123">numero di Hello delle funzionalità dei dati hello è flessibile.</span><span class="sxs-lookup"><span data-stu-id="74d77-123">hello number of features of hello data is flexible.</span></span> <span data-ttu-id="74d77-124">Tutti gli elementi di hello nella stringa di input hello devono essere numerici.</span><span class="sxs-lookup"><span data-stu-id="74d77-124">All hello elements in hello input string must be numeric.</span></span> <span data-ttu-id="74d77-125">Nei dati di training hello, dimensione temporale"hello" indica il numero di hello di unità di tempo (giorni, anni, chilometraggio e così via) trascorso dal punto di partenza hello di hello studiare (un paziente ricezione programmi trattamento somministrato il farmaco, uno Studio PhD inizio studente, un'automobile avvio toobe basato su, ecc.) fino a quando non hello evento di interesse (paziente hello restituzione toodrug utilizzo, grado di dottorato di hello studente ottenere hello, car hello con errore freni riempimento e così via) si verifica.</span><span class="sxs-lookup"><span data-stu-id="74d77-125">In hello training data, hello “time” dimension indicates hello number of time units (days, years, mileage, etc.) elapsed since hello starting point of hello study (a patient receiving drug treatment programs, a student starting PhD study, a car starting toobe driven, etc.) until hello event of interest (hello patient returning toodrug usage, hello student obtaining hello PhD degree, hello car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="74d77-126">dimensione di "evento" Hello indica se alla fine hello Studio hello evento hello di interesse.</span><span class="sxs-lookup"><span data-stu-id="74d77-126">hello “event” dimension indicates whether hello event of interest occurs at hello end of hello study.</span></span> <span data-ttu-id="74d77-127">Il valore "evento = 1" significa che l'evento di interesse hello avviene in fase di hello indicato dalla dimensione di "temporale" hello; "evento = 0" indica che l'evento di interesse hello non si è verificato hello di tempo indicato dalla dimensione di "ora" hello.</span><span class="sxs-lookup"><span data-stu-id="74d77-127">A value of “event=1” means that hello event of interest occurs at hello time indicated by hello “time” dimension; “event=0” means that hello event of interest has not occurred by hello time indicated by hello “time” dimension.</span></span>

* <span data-ttu-id="74d77-128">trainingdata: una stringa di caratteri.</span><span class="sxs-lookup"><span data-stu-id="74d77-128">trainingdata - A character string.</span></span> <span data-ttu-id="74d77-129">Le righe sono separate da virgola e le colonne sono separate da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="74d77-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="74d77-130">Ogni riga include la dimensione "time", la dimensione "event" e le variabili del predittore.</span><span class="sxs-lookup"><span data-stu-id="74d77-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="74d77-131">testingdata: una riga di dati che include variabili di predittore per un oggetto specifico.</span><span class="sxs-lookup"><span data-stu-id="74d77-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="74d77-132">time_of_interest - hello tempo di interesse n.</span><span class="sxs-lookup"><span data-stu-id="74d77-132">time_of_interest - hello elapsed time of interest n.</span></span>
* <span data-ttu-id="74d77-133">index_time - indice di colonna hello della dimensione di "temporale" hello (a partire da 1).</span><span class="sxs-lookup"><span data-stu-id="74d77-133">index_time - hello column index of hello “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="74d77-134">index_event - indice di colonna hello della dimensione "evento" hello (a partire da 1).</span><span class="sxs-lookup"><span data-stu-id="74d77-134">index_event - hello column index of hello “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="74d77-135">variable_types: stringa di caratteri con punto e virgola come separatore.</span><span class="sxs-lookup"><span data-stu-id="74d77-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="74d77-136">0 rappresenta le variabili continue e 1 variabili di fattore.</span><span class="sxs-lookup"><span data-stu-id="74d77-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="74d77-137">output di Hello è hello probabilità di un evento che si verifica entro una data specifica.</span><span class="sxs-lookup"><span data-stu-id="74d77-137">hello output is hello probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="74d77-138">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="74d77-138">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="74d77-139">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span><span class="sxs-lookup"><span data-stu-id="74d77-139">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="74d77-140">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="74d77-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="74d77-141">interpretazione di Hello di questo test è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="74d77-141">hello interpretation of this test is as follows.</span></span> <span data-ttu-id="74d77-142">Presupponendo che l'obiettivo di hello di dati hello è il tempo trascorso hello toomodel finché hello restituire toodrug utilizzo per pazienti hello che hanno ricevuto uno dei programmi di hello due modalità di gestione.</span><span class="sxs-lookup"><span data-stu-id="74d77-142">Assuming hello goal of hello data is toomodel hello elapsed time until hello return toodrug usage for hello patients who received one of hello two treatment programs.</span></span> <span data-ttu-id="74d77-143">output di hello web servizio letture Hello: per pazienti da 35 anni, con precedente libbre di farmaco trattamento 2 volte, prendendo programma trattamento tempo residenziale hello, e con l'utilizzo di heroin sia cocaine, probabilità hello di restituzione utilizzo somministrato il farmaco toohello 95.64% by giorno 500.</span><span class="sxs-lookup"><span data-stu-id="74d77-143">hello output of hello web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking hello long residential treatment program, and with both heroin and cocaine usage, hello probability of returning toohello drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="74d77-144">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="74d77-144">Creation of web service</span></span>
> <span data-ttu-id="74d77-145">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="74d77-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="74d77-146">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="74d77-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="74d77-147">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="74d77-147">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="74d77-148">Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli sono stati estratti nell'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="74d77-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="74d77-149">Hello dello schema di dati è stato creato con una semplice [Execute R Script][execute-r-script], che definisce schema dati di input hello per il servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="74d77-149">hello data schema was created with a simple [Execute R Script][execute-r-script], which defines hello input data schema for hello web service.</span></span> <span data-ttu-id="74d77-150">Questo modulo viene quindi collegato secondo toohello [Execute R Script] [ execute-r-script] modulo, che di lavoro principale.</span><span class="sxs-lookup"><span data-stu-id="74d77-150">This module is then linked toohello second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="74d77-151">ovvero la pre-elaborazione dei dati, la compilazione dei modelli e le previsioni.</span><span class="sxs-lookup"><span data-stu-id="74d77-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="74d77-152">In fase di pre-elaborazione dei dati hello, i dati di input hello rappresentati da una stringa lunga viene trasformati e convertiti in un frame di dati.</span><span class="sxs-lookup"><span data-stu-id="74d77-152">In hello data preprocessing step, hello input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="74d77-153">Nel passaggio di compilazione del modello di hello, un pacchetto R esterno "survival_2.37 7.zip" prima di tutto è installato per l'esecuzione di analisi di sopravvivenza.</span><span class="sxs-lookup"><span data-stu-id="74d77-153">In hello model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="74d77-154">Funzione "coxph" hello viene quindi eseguito dopo un'attività di elaborazione dei dati della serie.</span><span class="sxs-lookup"><span data-stu-id="74d77-154">Then hello “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="74d77-155">Dettagli Hello della funzione "coxph" hello per l'analisi di sopravvivenza possono essere letti dalla documentazione hello R.</span><span class="sxs-lookup"><span data-stu-id="74d77-155">hello details of hello “coxph” function for survival analysis can be read from hello R documentation.</span></span> <span data-ttu-id="74d77-156">Nel passaggio di stima hello, viene fornita un'istanza di test nel modello con training a hello con funzione di "surfit" hello, e curva sopravvivenza hello per questa istanza di test viene prodotto come variabile "curve".</span><span class="sxs-lookup"><span data-stu-id="74d77-156">In hello prediction step, a testing instance is supplied into hello trained model with hello “surfit” function, and hello survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="74d77-157">Infine, viene ottenuto probabilità hello di tempo hello di interesse.</span><span class="sxs-lookup"><span data-stu-id="74d77-157">Finally, hello probability of hello time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="74d77-158">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="74d77-158">Experiment flow:</span></span>
![flusso dell'esperimento][1]

#### <a name="module-1"></a><span data-ttu-id="74d77-160">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="74d77-160">Module 1:</span></span>
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

#### <a name="module-2"></a><span data-ttu-id="74d77-161">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="74d77-161">Module 2:</span></span>
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




## <a name="limitations"></a><span data-ttu-id="74d77-162">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="74d77-162">Limitations</span></span>
<span data-ttu-id="74d77-163">Questo servizio Web può accettare solo valori numerici come variabili della funzionalità (colonne).</span><span class="sxs-lookup"><span data-stu-id="74d77-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="74d77-164">colonna "evento" Hello può richiedere solo valore 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="74d77-164">hello “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="74d77-165">colonna "tempo" Hello deve toobe un numero intero positivo.</span><span class="sxs-lookup"><span data-stu-id="74d77-165">hello “time” column needs toobe a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="74d77-166">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="74d77-166">FAQ</span></span>
<span data-ttu-id="74d77-167">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="74d77-167">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

