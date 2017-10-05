---
title: (Deprecato) Analisi di sopravvivenza con Azure Machine Learning | Documentazione Microsoft
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
redirect_document_id: TRUE
ms.openlocfilehash: 7d4066d5f15a39c428d8035257c4841f9b3cc775
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-survival-analysis"></a><span data-ttu-id="01e68-103">(Deprecato) Analisi di sopravvivenza</span><span class="sxs-lookup"><span data-stu-id="01e68-103">(deprecated) Survival Analysis</span></span>

> [!NOTE]
> <span data-ttu-id="01e68-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="01e68-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="01e68-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="01e68-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="01e68-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="01e68-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="01e68-107">In molti scenari l'esito principale valutato riguarda il tempo mancante per un evento rilevante.</span><span class="sxs-lookup"><span data-stu-id="01e68-107">Under many scenarios, the main outcome under assessment is the time to an event of interest.</span></span> <span data-ttu-id="01e68-108">In altri termini, "quando si verificherà questo evento?"</span><span class="sxs-lookup"><span data-stu-id="01e68-108">In other words, the question “when this event will occur?”</span></span> <span data-ttu-id="01e68-109">è la domanda che viene posta.</span><span class="sxs-lookup"><span data-stu-id="01e68-109">is asked.</span></span> <span data-ttu-id="01e68-110">Si prendano, ad esempio, in considerazione situazioni in cui i dati illustrano il tempo trascorso (giorni, anni, chilometraggio e così via) prima del verificarsi dell'evento di interesse (ricaduta di una malattia, conseguimento di un titolo di studio, guasto ai freni).</span><span class="sxs-lookup"><span data-stu-id="01e68-110">As examples, consider situations where the data describes the elapsed time (days, years, mileage, etc.) until the event of interest (disease relapse, PhD degree received, brake pad failure) occurs.</span></span> <span data-ttu-id="01e68-111">Ogni istanza dei dati rappresenta un oggetto specifico (un paziente, una persona, un'automobile e così via).</span><span class="sxs-lookup"><span data-stu-id="01e68-111">Each instance in the data represents a specific object (a patient, a student, a car, etc.).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="01e68-112">Questo [servizio Web](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) risponde alla domanda "qual è la probabilità che l'evento rilevante si verifichi entro n per l'oggetto x?".</span><span class="sxs-lookup"><span data-stu-id="01e68-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/survivalanalysis) answers the question “what is the probability that the event of interest will occur by time n for object x?”</span></span> <span data-ttu-id="01e68-113">Questo servizio Web fornisce un modello di analisi di sopravvivenza, in modo da permettere agli utenti di fornire dati al modello per eseguirne il training e testarlo.</span><span class="sxs-lookup"><span data-stu-id="01e68-113">By providing a survival analysis model, this web service enables users to supply data to train the model and test it.</span></span> <span data-ttu-id="01e68-114">Il tema principale dell'esperimento consiste nel modellare la quantità di tempo trascorsa fino al verificarsi dell'evento rilevante.</span><span class="sxs-lookup"><span data-stu-id="01e68-114">The main theme of the experiment is to model the length of the elapsed time until the event of interest occurs.</span></span> 

> <span data-ttu-id="01e68-115">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="01e68-115">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="01e68-116">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="01e68-116">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="01e68-117">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="01e68-117">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="01e68-118">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="01e68-118">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="01e68-119">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="01e68-119">Consumption of web service</span></span>
<span data-ttu-id="01e68-120">Lo schema di dati di input del servizio Web è mostrato nella tabella seguente.</span><span class="sxs-lookup"><span data-stu-id="01e68-120">The input data schema of the web service is shown in the following table.</span></span> <span data-ttu-id="01e68-121">Come input sono necessari sei set di informazioni: dati di training, dati di test, ora di interesse, indice della dimensione "time", indice della dimensione "event" e tipi di variabile (continua o fattore).</span><span class="sxs-lookup"><span data-stu-id="01e68-121">Six pieces of information are needed as the input: training data, testing data, time of interest, the index of "time" dimension, the index of "event" dimension, and the variable types (continuous or factor).</span></span> <span data-ttu-id="01e68-122">I dati di training sono rappresentati da una stringa, in cui le righe sono separate da virgola e le colonne sono separate da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="01e68-122">The training data is represented with a string, where the rows are separated by comma, and the columns are separated by semicolon.</span></span> <span data-ttu-id="01e68-123">Il numero di funzionalità dei dati è flessibile.</span><span class="sxs-lookup"><span data-stu-id="01e68-123">The number of features of the data is flexible.</span></span> <span data-ttu-id="01e68-124">Tutti gli elementi della stringa di input devono essere numerici.</span><span class="sxs-lookup"><span data-stu-id="01e68-124">All the elements in the input string must be numeric.</span></span> <span data-ttu-id="01e68-125">Nei dati di training la dimensione "time" indica il numero di unità di tempo (giorni, anni, chilometraggio e così via) trascorse dopo il punto iniziale dello studio (un paziente che si sottopone a programmi di disintossicazione, uno studente che inizia un corso di studiper PHD, l'inizio dell'uso su strada di un'automobile e così via) fino al verificarsi dell'evento rilevante (un paziente che ricomincia ad assumere droghe, lo studente che consegue il titolo di studio, un guasto ai freni di un'automobile e così via).</span><span class="sxs-lookup"><span data-stu-id="01e68-125">In the training data, the “time” dimension indicates the number of time units (days, years, mileage, etc.) elapsed since the starting point of the study (a patient receiving drug treatment programs, a student starting PhD study, a car starting to be driven, etc.) until the event of interest (the patient returning to drug usage, the student obtaining the PhD degree, the car having brake pad failure, etc.) occurs.</span></span> <span data-ttu-id="01e68-126">La dimensione "event" indica se l'evento rilevante si verifica al termine dello studio.</span><span class="sxs-lookup"><span data-stu-id="01e68-126">The “event” dimension indicates whether the event of interest occurs at the end of the study.</span></span> <span data-ttu-id="01e68-127">"event=1" indica che l'evento rilevante si verifica nel momento indicato dalla dimensione "time", mentre "event=0" indica che l'evento rilevante non si è ancora verificato entro il momento indicato dalla dimensione "time".</span><span class="sxs-lookup"><span data-stu-id="01e68-127">A value of “event=1” means that the event of interest occurs at the time indicated by the “time” dimension; “event=0” means that the event of interest has not occurred by the time indicated by the “time” dimension.</span></span>

* <span data-ttu-id="01e68-128">trainingdata: una stringa di caratteri.</span><span class="sxs-lookup"><span data-stu-id="01e68-128">trainingdata - A character string.</span></span> <span data-ttu-id="01e68-129">Le righe sono separate da virgola e le colonne sono separate da punto e virgola.</span><span class="sxs-lookup"><span data-stu-id="01e68-129">Rows are separated by comma, and columns are separated by semicolon.</span></span> <span data-ttu-id="01e68-130">Ogni riga include la dimensione "time", la dimensione "event" e le variabili del predittore.</span><span class="sxs-lookup"><span data-stu-id="01e68-130">Each row includes “time” dimension, “event” dimension, and predictor variables.</span></span>
* <span data-ttu-id="01e68-131">testingdata: una riga di dati che include variabili di predittore per un oggetto specifico.</span><span class="sxs-lookup"><span data-stu-id="01e68-131">testingdata - One row of data that contains predictor variables for a particular object.</span></span>
* <span data-ttu-id="01e68-132">time_of_interest: quantità di tempo di interesse trascorsa.</span><span class="sxs-lookup"><span data-stu-id="01e68-132">time_of_interest - The elapsed time of interest n.</span></span>
* <span data-ttu-id="01e68-133">index_time: indice della colonna della dimensione "time" (a partire da 1).</span><span class="sxs-lookup"><span data-stu-id="01e68-133">index_time - The column index of the “time” dimension (starting from 1).</span></span>
* <span data-ttu-id="01e68-134">index_event - indice della colonna della dimensione "event" (a partire da 1).</span><span class="sxs-lookup"><span data-stu-id="01e68-134">index_event - The column index of the “event” dimension (starting from 1).</span></span>
* <span data-ttu-id="01e68-135">variable_types: stringa di caratteri con punto e virgola come separatore.</span><span class="sxs-lookup"><span data-stu-id="01e68-135">variable_types - A character string with semicolons as separators in it.</span></span> <span data-ttu-id="01e68-136">0 rappresenta le variabili continue e 1 variabili di fattore.</span><span class="sxs-lookup"><span data-stu-id="01e68-136">0 represents continuous variables and 1 represents factor variables.</span></span>

<span data-ttu-id="01e68-137">L'output corrisponde alla probabilità del verificarsi di un evento entro un tempo specifico.</span><span class="sxs-lookup"><span data-stu-id="01e68-137">The output is the probability of an event occurring by a specific time.</span></span> 

> <span data-ttu-id="01e68-138">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="01e68-138">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="01e68-139">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx).</span><span class="sxs-lookup"><span data-stu-id="01e68-139">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/SurvivalAnalysis.aspx)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="01e68-140">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="01e68-140">Starting C# code for web service consumption:</span></span>
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




<span data-ttu-id="01e68-141">L'interpretazione di questo test è la seguente.</span><span class="sxs-lookup"><span data-stu-id="01e68-141">The interpretation of this test is as follows.</span></span> <span data-ttu-id="01e68-142">Si presupponga che l'obiettivo dei dati consista nel modellare il tempo trascorso fino a quando i pazienti che hanno seguito uno dei due programmi di disintossicazione ricominciano ad assumere droghe.</span><span class="sxs-lookup"><span data-stu-id="01e68-142">Assuming the goal of the data is to model the elapsed time until the return to drug usage for the patients who received one of the two treatment programs.</span></span> <span data-ttu-id="01e68-143">L’output del servizio Web sarà: per i pazienti di età pari a 35 anni, che hanno in precedenza seguito 2 volte il programma di disintossicazione, che sono stati sottoposti a un programma di disintossicazione in una comunità e che assumevano sia eroina che cocaina, la probabilità di ritorno all'assunzione di droghe è pari al 95,64% entro il giorno 500.</span><span class="sxs-lookup"><span data-stu-id="01e68-143">The output of the web service reads: for patients being 35 years old, having previous drug treatment 2 times, taking the long residential treatment program, and with both heroin and cocaine usage, the probability of returning to the drug usage is 95.64% by day 500.</span></span>

## <a name="creation-of-web-service"></a><span data-ttu-id="01e68-144">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="01e68-144">Creation of web service</span></span>
> <span data-ttu-id="01e68-145">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="01e68-145">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="01e68-146">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="01e68-146">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="01e68-147">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="01e68-147">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="01e68-148">In Azure Machine Learning è stato creato un nuovo esperimento vuoto e sono stati inseriti due moduli [Execute R Script][execute-r-script] (Esegui script R) nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="01e68-148">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto the workspace.</span></span> <span data-ttu-id="01e68-149">Lo schema di dati è stato creato con un semplice modulo [Execute R Script][execute-r-script] (Esegui script R) che definisce lo schema di dati di input per il servizio Web.</span><span class="sxs-lookup"><span data-stu-id="01e68-149">The data schema was created with a simple [Execute R Script][execute-r-script], which defines the input data schema for the web service.</span></span> <span data-ttu-id="01e68-150">Questo modulo viene quindi collegato al secondo modulo [Execute R Script][execute-r-script] (Esegui script R) che esegue la maggior parte delle operazioni,</span><span class="sxs-lookup"><span data-stu-id="01e68-150">This module is then linked to the second [Execute R Script][execute-r-script] module, which does major work.</span></span> <span data-ttu-id="01e68-151">ovvero la pre-elaborazione dei dati, la compilazione dei modelli e le previsioni.</span><span class="sxs-lookup"><span data-stu-id="01e68-151">This module does data preprocessing, model building, and predictions.</span></span> <span data-ttu-id="01e68-152">Nel passaggio di pre-elaborazione dei dati, i dati di input rappresentati da una stringa lunga vengono trasformati e convertiti in un intervallo di dati.</span><span class="sxs-lookup"><span data-stu-id="01e68-152">In the data preprocessing step, the input data represented by a long string is transformed and converted into a data frame.</span></span> <span data-ttu-id="01e68-153">Nel passaggio di compilazione del modello, viene prima di tutto installato un pacchetto R esterno denominato "survival_2.37-7.zip" per l'esecuzione dell'analisi di sopravvivenza.</span><span class="sxs-lookup"><span data-stu-id="01e68-153">In the model building step, an external R package “survival_2.37-7.zip” is first installed for conducting survival analysis.</span></span> <span data-ttu-id="01e68-154">La funzione "coxph" viene eseguita dopo una serie di attività di elaborazione dei dati.</span><span class="sxs-lookup"><span data-stu-id="01e68-154">Then the “coxph” function is executed after a series data processing tasks.</span></span> <span data-ttu-id="01e68-155">Informazioni dettagliate sulla funzione "coxph" per l'analisi di sopravvivenza sono disponibili nella documentazione su R.</span><span class="sxs-lookup"><span data-stu-id="01e68-155">The details of the “coxph” function for survival analysis can be read from the R documentation.</span></span> <span data-ttu-id="01e68-156">Nel passaggio relativo alla previsione, un'istanza di test viene fornita al modello sottoposto a training con la funzione "surfit" e la curva di sopravvivenza per questa istanza di test viene prodotta come variabile "curve".</span><span class="sxs-lookup"><span data-stu-id="01e68-156">In the prediction step, a testing instance is supplied into the trained model with the “surfit” function, and the survival curve for this testing instance is produced as “curve” variable.</span></span> <span data-ttu-id="01e68-157">Viene quindi ricavata la probabilità del tempo di interesse.</span><span class="sxs-lookup"><span data-stu-id="01e68-157">Finally, the probability of the time of interest is obtained.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="01e68-158">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="01e68-158">Experiment flow:</span></span>
![flusso dell'esperimento][1]

#### <a name="module-1"></a><span data-ttu-id="01e68-160">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="01e68-160">Module 1:</span></span>
    #Data schema with example data (replaced with data from web service)
    trainingdata="53;1;29;0;0;3,79;1;34;0;1;2,45;1;27;0;1;1,37;1;24;0;1;1,122;1;30;0;1;1,655;0;41;0;0;1,166;1;30;0;0;3,227;1;29;0;0;3,805;0;30;0;0;1,104;1;24;0;0;1,90;1;32;0;0;1,373;1;26;0;0;1,70;1;36;0;0;1”
    testingdata="35;2;1;1"
    time_of_interest="500"
    index_time="1"
    index_event="2"

    # 0 - continuous; 1 -  factor
    variable_types="0;0;1;1"

    sampleInput=data.frame(trainingdata,testingdata,time_of_interest,index_time,index_event,variable_types)

    maml.mapOutputPort("sampleInput"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="01e68-161">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="01e68-161">Module 2:</span></span>
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

    # Prepare to build model
    attach(mydata)

    for (i in 1:n_col){ mydata[,i]=as.numeric(mydata[,i])} 
    d_time=paste("X",index_time,sep = "")
    d_event=paste("X",index_event,sep = "")
    v_time_event <- c(d_time,d_event)
    v_predictors = names(mydata)[!(names(mydata) %in% v_time_event)]

    variable_types = unlist(strsplit(as.character(variable_types),";"))

    len = length(v_predictors)
    c="" # Construct the execution string
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

    # Fit a Cox proportional hazards model and get the predicted survival curve for a testing instance 
    fit=eval(parse(text=f))

    testingdata = as.data.frame(matrix(testingdata, ncol=len,byrow = TRUE),stringsAsFactors=FALSE)
    names(testingdata)=v_predictors
    for (i in 1:len){ testingdata[,i]=as.numeric(testingdata[,i])}

    curve=survfit(fit,testingdata)

    # Based on user input, find the event occurrence probability
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

    #Pull out results to send to web service
    output=paste(round(100*output, 2), "%") 
    maml.mapOutputPort("output"); #output port




## <a name="limitations"></a><span data-ttu-id="01e68-162">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="01e68-162">Limitations</span></span>
<span data-ttu-id="01e68-163">Questo servizio Web può accettare solo valori numerici come variabili della funzionalità (colonne).</span><span class="sxs-lookup"><span data-stu-id="01e68-163">This web service can take only numerical values as feature variables (columns).</span></span> <span data-ttu-id="01e68-164">La colonna "event" può richiedere solo valore 0 o 1.</span><span class="sxs-lookup"><span data-stu-id="01e68-164">The “event” column can take only value 0 or 1.</span></span> <span data-ttu-id="01e68-165">La colonna “Time”deve essere un intero positivo.</span><span class="sxs-lookup"><span data-stu-id="01e68-165">The “time” column needs to be a positive integer.</span></span>

## <a name="faq"></a><span data-ttu-id="01e68-166">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="01e68-166">FAQ</span></span>
<span data-ttu-id="01e68-167">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="01e68-167">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-survival-analysis/survive_img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

