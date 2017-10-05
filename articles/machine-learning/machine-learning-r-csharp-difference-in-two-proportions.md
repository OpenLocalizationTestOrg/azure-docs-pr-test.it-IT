---
title: (Deprecato) Differenza nel test sulle proporzioni - Azure | Documentazione Microsoft
description: (Deprecato) Differenza nel test sulle proporzioni
services: machine-learning
documentationcenter: 
author: aniedea
manager: jhubbard
editor: cgronlun
ms.assetid: 9356b821-5345-44f6-8e26-719f2dea5e6d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: aniedea
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: a08f91ca76eef2562caeb9eb64cec5e549ed2f5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="3cd72-103">(Deprecato) Differenza nel test sulle proporzioni</span><span class="sxs-lookup"><span data-stu-id="3cd72-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="3cd72-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="3cd72-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3cd72-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3cd72-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3cd72-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3cd72-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3cd72-107">Due proporzioni presentano differenze a livello statistico?</span><span class="sxs-lookup"><span data-stu-id="3cd72-107">Are two proportions statistically different?</span></span> <span data-ttu-id="3cd72-108">Si supponga che un utente voglia confrontare due film per determinare se un film ha ottenuto una proporzione significativamente superiore di "mi piace" rispetto all'altro.</span><span class="sxs-lookup"><span data-stu-id="3cd72-108">Suppose a user wants to compare two movies to determine if one movie has a significantly higher proportion of ‘likes’ when compared to the other.</span></span> <span data-ttu-id="3cd72-109">Con un campione di grandi dimensioni, potrebbe esservi una differenza statisticamente significativa tra le proporzioni 0,50 e 0,51.</span><span class="sxs-lookup"><span data-stu-id="3cd72-109">With a large sample, there could be a statistically significant difference between the proportions 0.50 and 0.51.</span></span> <span data-ttu-id="3cd72-110">Con un campione di piccole dimensioni, potrebbero non essere disponibili dati sufficienti per determinare se queste proporzioni sono effettivamente diverse.</span><span class="sxs-lookup"><span data-stu-id="3cd72-110">With a small sample, there may not be enough data to determine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="3cd72-111">Questo [servizio Web](https://datamarket.azure.com/dataset/aml_labs/prop_test) esegue una verifica dell'ipotesi relativa alla differenza tra le due proporzioni in base all'input utente del numero di successi e del numero totale di prove per i due gruppi di confronto.</span><span class="sxs-lookup"><span data-stu-id="3cd72-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of the difference in two proportions based on user input of the number of successes and the total number of trials for the 2 comparison groups.</span></span> <span data-ttu-id="3cd72-112">Questo scenario si può verificare in caso di chiamata del servizio Web dall’interno di un'app di confronto tra film, per comunicare a un utente se uno dei film è effettivamente più apprezzato rispetto all'altro sulla base delle classificazioni dei film.</span><span class="sxs-lookup"><span data-stu-id="3cd72-112">In one possible scenario, this web service could be called from within a movie comparison app, telling the user whether one of the movies is really ‘liked’ more often than the other, based on movie ratings.</span></span>

> <span data-ttu-id="3cd72-113">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="3cd72-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3cd72-114">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="3cd72-114">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="3cd72-115">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="3cd72-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3cd72-116">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="3cd72-116">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3cd72-117">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="3cd72-117">Consumption of web service</span></span>
<span data-ttu-id="3cd72-118">Questo servizio accetta quattro argomenti ed esegue una verifica dell'ipotesi delle proporzioni.</span><span class="sxs-lookup"><span data-stu-id="3cd72-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="3cd72-119">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="3cd72-119">The input arguments are:</span></span>

* <span data-ttu-id="3cd72-120">Successes1: numero di eventi con esito positivo nel campione 1.</span><span class="sxs-lookup"><span data-stu-id="3cd72-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="3cd72-121">Successes2: numero di eventi con esito positivo nel campione 2.</span><span class="sxs-lookup"><span data-stu-id="3cd72-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="3cd72-122">Total1: dimensione del campione 1.</span><span class="sxs-lookup"><span data-stu-id="3cd72-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="3cd72-123">Total2: dimensione del campione 2.</span><span class="sxs-lookup"><span data-stu-id="3cd72-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="3cd72-124">L'output del servizio è il risultato della verifica dell'ipotesi, insieme alla statistica chi quadrato, ai gradi di libertà, al valore p, la proporzione nel campione 1/2 e ai limiti dell'intervallo di confidenza.</span><span class="sxs-lookup"><span data-stu-id="3cd72-124">The output of the service is the result of the hypothesis test along with the chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="3cd72-125">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="3cd72-125">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3cd72-126">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cd72-126">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3cd72-127">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="3cd72-127">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string successes1;
            public string successes2;
            public string total1;
            public string total2;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { successes1 = TextBox1.Text, successes2 = TextBox2.Text, total1 = TextBox3.Text, total2 = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="3cd72-128">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="3cd72-128">Creation of web service</span></span>
> <span data-ttu-id="3cd72-129">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3cd72-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3cd72-130">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3cd72-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3cd72-131">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="3cd72-131">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="3cd72-132">In Azure Machine Learning è stato creato un nuovo esperimento vuoto con due moduli [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="3cd72-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="3cd72-133">Lo schema di dati nel primo modulo è definito, mentre il secondo modulo usa il comando prop.test in R per eseguire la verifica dell'ipotesi per due proporzioni.</span><span class="sxs-lookup"><span data-stu-id="3cd72-133">In the first module the data schema is defined, while the second module uses the prop.test command within R to perform the hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="3cd72-134">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="3cd72-134">Experiment flow:</span></span>
![Flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="3cd72-136">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="3cd72-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data to output port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="3cd72-137">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="3cd72-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"The proportions are different!",
    "The proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="3cd72-138">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="3cd72-138">Limitations</span></span>
<span data-ttu-id="3cd72-139">Questo è un esempio molto semplice per la verifica della differenza tra due proporzioni.</span><span class="sxs-lookup"><span data-stu-id="3cd72-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="3cd72-140">Come si può notare dall'esempio di codice precedente, il rilevamento degli errori non è implementato e il servizio presuppone che tutte le variabili siano continue.</span><span class="sxs-lookup"><span data-stu-id="3cd72-140">As can be seen from the example code above, no error catching is implemented and the service assumes that all the variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="3cd72-141">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3cd72-141">FAQ</span></span>
<span data-ttu-id="3cd72-142">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3cd72-142">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

