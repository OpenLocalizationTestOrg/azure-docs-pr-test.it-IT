---
title: AAA(deprecated) Multivariate Linear Regression - Azure | Documenti Microsoft
description: "Regressione lineare multivariata (funzionalità deprecata)"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 2fb78220-ced9-4564-a439-9e5df6772994
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 0ff7221cd06c0ef059b0c5bf327016588174dcfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-multivariate-linear-regression"></a><span data-ttu-id="0ef71-103">Regressione lineare multivariata (funzionalità deprecata)</span><span class="sxs-lookup"><span data-stu-id="0ef71-103">(deprecated) Multivariate Linear Regression</span></span>

> [!NOTE]
> <span data-ttu-id="0ef71-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="0ef71-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="0ef71-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="0ef71-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="0ef71-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="0ef71-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="0ef71-107">Si supponga che si dispone di un set di dati e come tooquickly potrebbe prevedere una variabile dipendente (y) per ogni singolo cliente (i) in base alle variabili indipendenti.</span><span class="sxs-lookup"><span data-stu-id="0ef71-107">Suppose you have a dataset and would like tooquickly predict a dependent variable (y) for each individual (i) based on independent variables.</span></span> <span data-ttu-id="0ef71-108">La regressione lineare è una tecnica statistica popolare usata per previsioni di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="0ef71-108">Linear regression is a popular statistical technique used for such predictions.</span></span> <span data-ttu-id="0ef71-109">Di seguito hello variabile dipendente y presuppone toobe un valore continuo.</span><span class="sxs-lookup"><span data-stu-id="0ef71-109">Here hello dependent variable y is assumed toobe a continuous value.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="0ef71-110">Potrebbe essere un semplice scenario in cui ingegno hello tenta peso hello toopredict di una persona (y) in base all'altezza (x).</span><span class="sxs-lookup"><span data-stu-id="0ef71-110">A simple scenario could be where hello researcher is trying toopredict hello weight of an individual (y) based on their height (x).</span></span> <span data-ttu-id="0ef71-111">Uno scenario più avanzato potrebbe essere in ingegno hello dispone di informazioni aggiuntive per singola (ad esempio, weight, sesso, race) hello e tenta di peso hello toopredict di hello singolo.</span><span class="sxs-lookup"><span data-stu-id="0ef71-111">A more advanced scenario could be where hello researcher has additional information for hello individual (such as weight, gender, race) and attempts toopredict hello weight of hello individual.</span></span> <span data-ttu-id="0ef71-112">Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) adatto hello dati toohello del modello di regressione lineare e output hello valore stimato (y) per ognuna delle osservazioni hello nei dati hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-112">This [web service](https://datamarket.azure.com/dataset/aml_labs/multivariate_regression) fits hello linear regression model toohello data and outputs hello predicted value (y) for each of hello observations in hello data.</span></span>

> <span data-ttu-id="0ef71-113">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="0ef71-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="0ef71-114">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="0ef71-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="0ef71-115">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="0ef71-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="0ef71-116">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="0ef71-117">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0ef71-117">Consumption of web service</span></span>
<span data-ttu-id="0ef71-118">I valori di variabile dipendente hello in base alle variabili indipendenti hello per tutte le osservazioni hello è stato stimato questo hello consente di servizio web.</span><span class="sxs-lookup"><span data-stu-id="0ef71-118">This web service gives hello predicted values of hello dependent variable based on hello independent variables for all of hello observations.</span></span> <span data-ttu-id="0ef71-119">servizio web Hello dati tooinput utente finale di hello previsto è una stringa in cui le righe sono separate da virgole (,) e le colonne sono separate da punti e virgola (;).</span><span class="sxs-lookup"><span data-stu-id="0ef71-119">hello web service expects hello end user tooinput data as a string where rows are separated by commas (,) and columns are separated by semicolons (;).</span></span> <span data-ttu-id="0ef71-120">servizio web Hello prevista 1 riga alla volta e non prevede hello prima colonna toobe hello variabile dipendente.</span><span class="sxs-lookup"><span data-stu-id="0ef71-120">hello web service expects 1 row at a time and expects hello first column toobe hello dependent variable.</span></span> <span data-ttu-id="0ef71-121">Un set di dati di esempio può avere un aspetto analogo al seguente:</span><span class="sxs-lookup"><span data-stu-id="0ef71-121">An example dataset could look like this:</span></span>

![Dati di esempio][1]

<span data-ttu-id="0ef71-123">Osservazioni senza una variabile dipendente devono essere immesse come "NA" per l'asse y.</span><span class="sxs-lookup"><span data-stu-id="0ef71-123">Observations without a dependent variable should be input as “NA” for y.</span></span> <span data-ttu-id="0ef71-124">Hello dati di input per hello di sopra di set di dati potrebbe essere hello seguente stringa: "10 5; 2,18; 1; 6,6; 5.3; 2.1,7; 5; 5,22; 3; 4,12; 2; 1, NA, 3, 4".</span><span class="sxs-lookup"><span data-stu-id="0ef71-124">hello data input for hello above dataset would be hello following string: “10;5;2,18;1;6,6;5.3;2.1,7;5;5,22;3;4,12;2;1,NA;3;4”.</span></span> <span data-ttu-id="0ef71-125">output di Hello hello valore stimato per ognuna delle righe hello si basa su variabili indipendenti hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-125">hello output is hello predicted value for each of hello rows based on hello independent variables.</span></span> 

> <span data-ttu-id="0ef71-126">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="0ef71-126">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="0ef71-127">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0ef71-127">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/MultipleLinearRegressionService.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="0ef71-128">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="0ef71-128">Starting C# code for web service consumption:</span></span>
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




## <a name="creation-of-web-service"></a><span data-ttu-id="0ef71-129">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="0ef71-129">Creation of web service</span></span>
> <span data-ttu-id="0ef71-130">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0ef71-130">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="0ef71-131">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="0ef71-131">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="0ef71-132">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-132">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="0ef71-133">Da Azure Machine Learning, all'interno di un esperimento vuoto nuovo è stato creato e due [Execute R Script] [ execute-r-script] moduli sono stati estratti nell'area di lavoro hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-133">From within Azure Machine Learning, a new blank experiment was created and two [Execute R Script][execute-r-script] modules were pulled onto hello workspace.</span></span> <span data-ttu-id="0ef71-134">Questo servizio Web esegue un esperimento di Azure Machine Learning con lo script R sottostante.</span><span class="sxs-lookup"><span data-stu-id="0ef71-134">This web service runs an Azure Machine Learning experiment with an underlying R script.</span></span> <span data-ttu-id="0ef71-135">Esistono sperimentare toothis 2 part: definizione di schema e di training del modello di + punteggio.</span><span class="sxs-lookup"><span data-stu-id="0ef71-135">There are 2 parts toothis experiment: schema definition, and training model + scoring.</span></span> <span data-ttu-id="0ef71-136">primo modulo Hello definisce struttura hello previsto di hello input set di dati, in cui hello prima variabile è variabile dipendente hello e variabili rimanenti hello sono indipendenti.</span><span class="sxs-lookup"><span data-stu-id="0ef71-136">hello first module defines hello expected structure of hello input dataset, where hello first variable is hello dependent variable and hello remaining variables are independent.</span></span> <span data-ttu-id="0ef71-137">secondo modulo Hello adatta un modello di regressione lineare generico per i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-137">hello second module fits a generic linear regression model for hello input data.</span></span>  

![Flusso dell'esperimento][3]

#### <a name="module-1"></a><span data-ttu-id="0ef71-139">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="0ef71-139">Module 1:</span></span>
#### <a name="schema-definition"></a><span data-ttu-id="0ef71-140">Definizione dello schema</span><span class="sxs-lookup"><span data-stu-id="0ef71-140">Schema definition</span></span>
    data <- data.frame(value = "1;2;3,4;5;6,7;8;9", stringsAsFactors=FALSE) maml.mapOutputPort("data");  

#### <a name="module-2"></a><span data-ttu-id="0ef71-141">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="0ef71-141">Module 2:</span></span>
#### <a name="lm-modeling"></a><span data-ttu-id="0ef71-142">Creazione di modelli LM</span><span class="sxs-lookup"><span data-stu-id="0ef71-142">LM modeling</span></span>
    data <- maml.mapInputPort(1) # class: data.frame  

    data.split <- strsplit(data[1,1], ",")[[1]]  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- sapply(data.split, strsplit, ";", simplify = TRUE)  
    data.split <- as.data.frame(t(data.split)) 
    data.split <- data.matrix(data.split) 
    data.split <- data.frame(data.split) 
    model <- lm(data.split)  

    out=data.frame(predict(model,data.split))  
    out <- data.frame(t(out))

    maml.mapOutputPort("out");  

## <a name="limitations"></a><span data-ttu-id="0ef71-143">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="0ef71-143">Limitations</span></span>
<span data-ttu-id="0ef71-144">Questo è un esempio molto semplice di un servizio Web di regressione lineare multipla.</span><span class="sxs-lookup"><span data-stu-id="0ef71-144">This is a very simple example of a multiple linear regression web service.</span></span> <span data-ttu-id="0ef71-145">Nessun rilevamento di errori viene implementato come possono essere visualizzati dal codice di esempio hello precedente, e presuppone servizio hello tutto ciò che è una variabile continua (nessuna funzionalità categorica consentita), come hello servizio solo input valori numerici in fase di hello della creazione di hello del sito web servizio.</span><span class="sxs-lookup"><span data-stu-id="0ef71-145">As can be seen from hello example code above, no error catching is implemented and hello service assumes everything is a continuous variable (no categorical features allowed), as hello service only inputs numeric values at hello time of hello creation of this web service.</span></span> <span data-ttu-id="0ef71-146">Inoltre, hello servizio gestisce attualmente le dimensioni dei dati limitato, a causa di natura di richiesta/risposta toohello del servizio web hello si adatta chiamata e hello delle tabelle dei fatti che hello modello ogni volta che viene chiamato servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="0ef71-146">Also, hello service currently handles limited data size, due toohello request/response nature of hello web service call and hello fact that hello model is being fit every time hello web service is called.</span></span> 

## <a name="faq"></a><span data-ttu-id="0ef71-147">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="0ef71-147">FAQ</span></span>
<span data-ttu-id="0ef71-148">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="0ef71-148">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img1.png
[2]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img2.png
[3]: ./media/machine-learning-r-csharp-multivariate-linear-regression/multireg-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

