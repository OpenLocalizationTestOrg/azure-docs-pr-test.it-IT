---
title: (Deprecato) Classificatore binario - Azure | Documentazione Microsoft
description: (Deprecato) Classificatore binario
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 8045038a-9dcf-44b9-a6de-7f1f8e791575
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 1a83392f90bb5a9fb183334c03ccec20dd3f3520
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binary-classifier"></a><span data-ttu-id="d5578-103">(Deprecato) Classificatore binario</span><span class="sxs-lookup"><span data-stu-id="d5578-103">(deprecated) Binary Classifier</span></span>

> [!NOTE]
> <span data-ttu-id="d5578-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="d5578-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="d5578-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="d5578-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="d5578-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="d5578-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="d5578-107">Si supponga che sia disponibile un set di dati e che si voglia prevedere una variabile dipendente binaria sulla base delle variabili indipendenti.</span><span class="sxs-lookup"><span data-stu-id="d5578-107">Suppose you have a dataset and would like to predict a binary dependent variable based on the independent variables.</span></span> <span data-ttu-id="d5578-108">La 'regressione logistica' è una tecnica statistica molto usata per queste previsioni.</span><span class="sxs-lookup"><span data-stu-id="d5578-108">‘Logistic Regression’ is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="d5578-109">In questo caso la variabile dipendente è binaria o dicotomica e p è la probabilità della presenza della caratteristica di interesse.</span><span class="sxs-lookup"><span data-stu-id="d5578-109">Here the dependent variable is binary or dichotomous, and p is the probability of presence of the characteristic of interest.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d5578-110">Un semplice scenario potrebbe essere costituito, ad esempio, da una situazione in cui il ricercatore tenta di prevedere la probabilità di accettazione dell'offerta di ammissione a un'università da parte di un potenziale studente sulla base delle informazioni disponibili (voti ottenuti durante il liceo, reddito familiare, residenza, genere).</span><span class="sxs-lookup"><span data-stu-id="d5578-110">A simple scenario could be where a researcher is trying to predict whether a prospective student is likely to accept an admission offer to a university based on information (GPA in high school, family income, resident state, gender).</span></span> <span data-ttu-id="d5578-111">L'esito previsto corrisponde alla probabilità di accettazione dell'offerta di ammissione da parte di un potenziale studente.</span><span class="sxs-lookup"><span data-stu-id="d5578-111">The predicted outcome is the probability of the prospective student accepting the admission offer.</span></span> <span data-ttu-id="d5578-112">Questo [servizio Web](https://datamarket.azure.com/dataset/aml_labs/log_regression) è adatto al modello di regressione logistica per i dati e fornisce come output il valore di probabilità (y) di ogni osservazione nei dati.</span><span class="sxs-lookup"><span data-stu-id="d5578-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/log_regression) fits the logistic regression model to the data and outputs the probability value (y) for each of the observations in the data.</span></span>  

> <span data-ttu-id="d5578-113">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="d5578-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="d5578-114">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="d5578-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="d5578-115">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d5578-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="d5578-116">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="d5578-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="d5578-117">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="d5578-117">Consumption of web service</span></span>
<span data-ttu-id="d5578-118">Questo servizio Web fornisce i valori previsti della variabile dipendente sulla base delle variabili indipendenti per tutte le osservazioni.</span><span class="sxs-lookup"><span data-stu-id="d5578-118">This web service gives the predicted values of the dependent variable based on the independent variables for all of the observations.</span></span> <span data-ttu-id="d5578-119">Il servizio Web richiede che l'utente finale immetta i dati come una stringa in cui le righe sono separate da virgola (,) e le colonne sono separate da punto e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="d5578-119">The web service expects the end user to input data as a string where rows are separated by comma (,) and columns are separated by semicolon (;).</span></span> <span data-ttu-id="d5578-120">Il servizio Web richiede una riga alla volta e che la prima colonna corrisponda alla variabile dipendente.</span><span class="sxs-lookup"><span data-stu-id="d5578-120">The web service expects 1 row at a time and expects the first column to be the dependent variable.</span></span> <span data-ttu-id="d5578-121">Un set di dati di esempio può avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="d5578-121">An example dataset could look like this:</span></span>

![Dati di esempio][1]

<span data-ttu-id="d5578-123">Osservazioni senza una variabile dipendente devono essere immesse come "NA" per l'asse y.</span><span class="sxs-lookup"><span data-stu-id="d5578-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="d5578-124">L'input di dati per il set di dati precedente sarebbe analogo alla seguente stringa: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span><span class="sxs-lookup"><span data-stu-id="d5578-124">The data input for the above dataset would be the following string: “1;5;2,1;1;6,0;5.3;2.1,0;5;5,0;3;4,1;2;1,NA;3;4”.</span></span> <span data-ttu-id="d5578-125">L'output è il valore previsto per ogni riga sulla base delle variabili indipendenti.</span><span class="sxs-lookup"><span data-stu-id="d5578-125">The output is the predicted value for each of the rows based on the independent variables.</span></span> 

> <span data-ttu-id="d5578-126">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="d5578-126">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="d5578-127">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx).</span><span class="sxs-lookup"><span data-stu-id="d5578-127">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/BinaryClassifier.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="d5578-128">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="d5578-128">Starting C# code for web service consumption:</span></span>
    public class Input
    {
           public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
        byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
        return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
        var input = new Input() { value = TextBox1.Text };
        var json = JsonConvert.SerializeObject(input);
        var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
        var httpClient = new HttpClient();

        httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
        httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

        var response = httpClient.PostAsync(acitionUri, new StringContent(json));
        var result = response.Result.Content;
        var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="d5578-129">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="d5578-129">Creation of web service</span></span>
> <span data-ttu-id="d5578-130">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d5578-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="d5578-131">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="d5578-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="d5578-132">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="d5578-132">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="d5578-133">In Azure Machine Learning è stato creato un nuovo esperimento vuoto e due moduli [Execute R Script][execute-r-script] sono stati inseriti nell'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d5578-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules pulled onto the workspace.</span></span> <span data-ttu-id="d5578-134">Questo servizio Web esegue un esperimento di Azure Machine Learning con lo script R sottostante.</span><span class="sxs-lookup"><span data-stu-id="d5578-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="d5578-135">Esistono 2 parti di questo esperimento: la definizione dello schema e il modello di training + punteggio.</span><span class="sxs-lookup"><span data-stu-id="d5578-135">There are 2 parts to this experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="d5578-136">Il primo modulo definisce la struttura prevista del set di dati di input in cui la prima variabile è dipendente e le variabili rimanenti sono indipendenti.</span><span class="sxs-lookup"><span data-stu-id="d5578-136">The first module defines the expected structure of the input dataset, where the first variable is the dependent variable and the remaining variables are independent.</span></span> <span data-ttu-id="d5578-137">Il secondo modulo è appropriato per un modello di regressione logistica generico per i dati di input.</span><span class="sxs-lookup"><span data-stu-id="d5578-137">The second module fits a generic logistic regression model for the input data.</span></span>    

![Flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="d5578-139">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="d5578-139">Module 1:</span></span>
    #Schema definition  
    data <- data.frame(value = "1;2;3,1;5;6,0;8;9", stringsAsFactors=FALSE) 
    maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="d5578-140">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="d5578-140">Module 2:</span></span>
    #GLM modeling   
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]] 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE) 
    data.split <- as.data.frame(t(data.split)) data.split <- 
    data.matrix(data.split) 
    data.split <- data.frame(data.split) 

    model <- glm(data.split$V1 ~., family='binomial', data=data.split)  
    out <- data.frame(predict(model,data.split, type="response")) 
    pred1 <- as.data.frame(out) 
    group <- array(1:nrow(pred1)) 
    for (i in 1:nrow(pred1))  
        {
        if(as.numeric(pred1[i,])>0.5) {group[i]=1} 
        else {group[i]=0}
        } 
    pred2 <- as.data.frame(group) 
    maml.mapOutputPort("pred2");  


## <a name="limitations"></a><span data-ttu-id="d5578-141">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="d5578-141">Limitations</span></span>
<span data-ttu-id="d5578-142">Questo è un esempio molto semplice del servizio Web per la classificazione binaria.</span><span class="sxs-lookup"><span data-stu-id="d5578-142">This is a very simple example of a binary classification web service.</span></span> <span data-ttu-id="d5578-143">Come si può notare nell'esempio di codice precedente, il rilevamento degli errori non è implementato e il servizio presuppone che qualsiasi elemento sia una variabile binaria/continua (non sono consentite funzionalità categoriche), poiché il servizio immette come input solo valori numerici al momento della creazione del servizio Web.</span><span class="sxs-lookup"><span data-stu-id="d5578-143">As can be seen from the example code above, no error catching is implemented and the service assumes everything is a binary/continuous variable (no categorical features allowed), as the service only inputs numeric values at the time of the creation of this web service.</span></span> <span data-ttu-id="d5578-144">Il servizio, inoltre, gestisce attualmente dimensioni limitate di dati a causa della natura di richiesta/risposta della chiamata del servizio Web e del fatto che il modello viene definito ogni volta che il servizio Web viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="d5578-144">Also, the service currently handles limited data size, due to the request/response nature of the web service call and the fact that the model is being fit every time the web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="d5578-145">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="d5578-145">FAQ</span></span>
<span data-ttu-id="d5578-146">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="d5578-146">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binary-classifier/binary1.png
[2]: ./media/machine-learning-r-csharp-binary-classifier/binary2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

