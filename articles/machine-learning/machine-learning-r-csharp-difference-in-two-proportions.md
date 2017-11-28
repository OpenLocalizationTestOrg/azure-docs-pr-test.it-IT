---
title: Differenza in percentuale di Test - Azure AAA(deprecated) | Documenti Microsoft
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
redirect_document_id: True
ms.openlocfilehash: 820aad377f9dec12b0ef455974aaa95f6e8d723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-difference-in-proportions-test"></a><span data-ttu-id="31c16-103">(Deprecato) Differenza nel test sulle proporzioni</span><span class="sxs-lookup"><span data-stu-id="31c16-103">(deprecated) Difference in Proportions Test</span></span>

> [!NOTE]
> <span data-ttu-id="31c16-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="31c16-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="31c16-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="31c16-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="31c16-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="31c16-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="31c16-107">Due proporzioni presentano differenze a livello statistico?</span><span class="sxs-lookup"><span data-stu-id="31c16-107">Are two proportions statistically different?</span></span> <span data-ttu-id="31c16-108">Si supponga che un utente desideri toocompare due filmati toodetermine se un filmato ha una proporzione notevolmente maggiore di "mi piace' quando confrontati toohello altri.</span><span class="sxs-lookup"><span data-stu-id="31c16-108">Suppose a user wants toocompare two movies toodetermine if one movie has a significantly higher proportion of ‘likes’ when compared toohello other.</span></span> <span data-ttu-id="31c16-109">Con un esempio di grandi dimensioni, potrebbe esserci una differenza tra percentuali hello 0,50 e 0.51 statisticamente significativa.</span><span class="sxs-lookup"><span data-stu-id="31c16-109">With a large sample, there could be a statistically significant difference between hello proportions 0.50 and 0.51.</span></span> <span data-ttu-id="31c16-110">Con un piccolo esempio, si potrebbe non essere sufficiente toodetermine dati se queste proporzioni in realtà sono diverse.</span><span class="sxs-lookup"><span data-stu-id="31c16-110">With a small sample, there may not be enough data toodetermine if these proportions are actually different.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="31c16-111">Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/prop_test) esegue un test di ipotesi di differenza hello in due proporzioni in base all'input utente hello numero di esiti positivi del numero totale di hello di versioni di valutazione per i gruppi di confronto hello 2.</span><span class="sxs-lookup"><span data-stu-id="31c16-111">This [web service](https://datamarket.azure.com/dataset/aml_labs/prop_test) conducts a hypothesis test of hello difference in two proportions based on user input of hello number of successes and hello total number of trials for hello 2 comparison groups.</span></span> <span data-ttu-id="31c16-112">In uno scenario, il servizio web potrebbe essere chiamato all'interno di un'app di confronto di film, che indica hello se uno dei filmati hello è 'dinamica' più spesso degli altri, hello in base alle classificazioni di film.</span><span class="sxs-lookup"><span data-stu-id="31c16-112">In one possible scenario, this web service could be called from within a movie comparison app, telling hello user whether one of hello movies is really ‘liked’ more often than hello other, based on movie ratings.</span></span>

> <span data-ttu-id="31c16-113">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="31c16-113">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="31c16-114">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="31c16-114">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="31c16-115">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="31c16-115">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="31c16-116">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="31c16-116">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="31c16-117">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="31c16-117">Consumption of web service</span></span>
<span data-ttu-id="31c16-118">Questo servizio accetta quattro argomenti ed esegue una verifica dell'ipotesi delle proporzioni.</span><span class="sxs-lookup"><span data-stu-id="31c16-118">This service accepts 4 arguments and does a hypothesis test of proportions.</span></span>

<span data-ttu-id="31c16-119">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="31c16-119">hello input arguments are:</span></span>

* <span data-ttu-id="31c16-120">Successes1: numero di eventi con esito positivo nel campione 1.</span><span class="sxs-lookup"><span data-stu-id="31c16-120">Successes1 - Number of success events in sample 1.</span></span>
* <span data-ttu-id="31c16-121">Successes2: numero di eventi con esito positivo nel campione 2.</span><span class="sxs-lookup"><span data-stu-id="31c16-121">Successes2 - Number of success events in sample 2.</span></span>
* <span data-ttu-id="31c16-122">Total1: dimensione del campione 1.</span><span class="sxs-lookup"><span data-stu-id="31c16-122">Total1 -  Size of sample 1.</span></span>
* <span data-ttu-id="31c16-123">Total2: dimensione del campione 2.</span><span class="sxs-lookup"><span data-stu-id="31c16-123">Total2 - Size of sample 2.</span></span>

<span data-ttu-id="31c16-124">output di Hello del servizio hello è risultato hello dell'ipotesi hello test insieme hello chi-quadrato statistica, df, p-valore e proporzioni nei limiti di 1/2 e l'intervallo di confidenza di esempio.</span><span class="sxs-lookup"><span data-stu-id="31c16-124">hello output of hello service is hello result of hello hypothesis test along with hello chi-square statistic, df, p-value, and proportion in sample 1/2 and confidence interval bounds.</span></span>

> <span data-ttu-id="31c16-125">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="31c16-125">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="31c16-126">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span><span class="sxs-lookup"><span data-stu-id="31c16-126">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/DifferenceInProportionsTest.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="31c16-127">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="31c16-127">Starting C# code for web service consumption:</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="31c16-128">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="31c16-128">Creation of web service</span></span>
> <span data-ttu-id="31c16-129">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="31c16-129">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="31c16-130">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="31c16-130">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="31c16-131">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="31c16-131">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="31c16-132">In Azure Machine Learning è stato creato un nuovo esperimento vuoto con due moduli [Execute R Script][execute-r-script] (Esegui script R).</span><span class="sxs-lookup"><span data-stu-id="31c16-132">From within Azure Machine Learning, a new blank experiment was created with two [Execute R Script][execute-r-script] modules.</span></span> <span data-ttu-id="31c16-133">Nel primo modulo hello schema dati hello è definito, mentre il secondo modulo hello utilizza il comando prop.test hello all'interno dei test di ipotesi R tooperform hello per le 2 proporzioni.</span><span class="sxs-lookup"><span data-stu-id="31c16-133">In hello first module hello data schema is defined, while hello second module uses hello prop.test command within R tooperform hello hypothesis test for 2 proportions.</span></span> 

### <a name="experiment-flow"></a><span data-ttu-id="31c16-134">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="31c16-134">Experiment flow:</span></span>
![Flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="31c16-136">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="31c16-136">Module 1:</span></span>
    ####Schema definition  
    data.set=data.frame(successes1=50,successes2=60,total1=100,total2=100);
    maml.mapOutputPort("data.set"); #send data toooutput port
    dataset1 = maml.mapInputPort(1) #read data from input port


#### <a name="module-2"></a><span data-ttu-id="31c16-137">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="31c16-137">Module 2:</span></span>
    test=prop.test(c(dataset1$successes1[1],dataset1$successes2[1]),c(dataset1$total1[1],dataset1$total2[1])) #conduct hypothesis test

    result=data.frame(
    result=ifelse(test$p.value<0.05,"hello proportions are different!",
    "hello proportions aren't different statistically."),
    ChiSquarestatistic=round(test$statistic,2),df=test$parameter,
    pvalue=round(test$p.value,4),
    proportion1=round(test$estimate[1],4),
    proportion2=round(test$estimate[2],4),
    confintlow=round(test$conf.int[1],4),
    confinthigh=round(test$conf.int[2],4)) 

    maml.mapOutputPort("result"); #output port


## <a name="limitations"></a><span data-ttu-id="31c16-138">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="31c16-138">Limitations</span></span>
<span data-ttu-id="31c16-139">Questo è un esempio molto semplice per la verifica della differenza tra due proporzioni.</span><span class="sxs-lookup"><span data-stu-id="31c16-139">This is a very simple example for a test of difference in 2 proportions.</span></span> <span data-ttu-id="31c16-140">Come si può notare dal codice di esempio hello precedente, non viene implementato alcun rilevamento di errori e servizio hello si presuppone che tutte le variabili di hello continua.</span><span class="sxs-lookup"><span data-stu-id="31c16-140">As can be seen from hello example code above, no error catching is implemented and hello service assumes that all hello variables are continuous.</span></span>

## <a name="faq"></a><span data-ttu-id="31c16-141">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="31c16-141">FAQ</span></span>
<span data-ttu-id="31c16-142">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="31c16-142">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img1.png
[2]: ./media/machine-learning-r-csharp-difference-in-two-proportions/hyptest-img2.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

