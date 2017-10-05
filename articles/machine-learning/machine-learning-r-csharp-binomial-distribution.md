---
title: (Deprecato) Binomial Distribution Suite - Azure | Documentazione Microsoft
description: (Deprecato) Binomial Distribution Suite
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: 6d102d57-8f20-4ab3-be31-02fcfe4d15ed
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: ireiter
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: TRUE
ms.openlocfilehash: 6f0a6d06e7401c8360a92a707a0552f41ff3657c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="962f3-103">(Deprecato) Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="962f3-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="962f3-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="962f3-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="962f3-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="962f3-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="962f3-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="962f3-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="962f3-107">Binomial Distribution Suite è un insieme di servizi Web di esempio ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) che semplificano la generazione e la gestione delle distribuzioni binomiali.</span><span class="sxs-lookup"><span data-stu-id="962f3-107">The Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="962f3-108">I servizi permettono la generazione di una sequenza di distribuzioni binomiali di qualsiasi lunghezza, calcolando i quantili rispetto alla probabilità specificata e calcolando la probabilità in base a un quantile specificato.</span><span class="sxs-lookup"><span data-stu-id="962f3-108">The services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="962f3-109">Ogni servizio emette output diversi, in base al servizio selezionato, come illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="962f3-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="962f3-110">Binomial Distribution Suite è basato sulle funzioni qbinom, rbinom e pbinom del codice R, incluse nel pacchetto statistico R.</span><span class="sxs-lookup"><span data-stu-id="962f3-110">The Binomial Distribution Suite is based on the R functions qbinom, rbinom, and pbinom, which are included in the R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="962f3-111">Questi servizi Web possono essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="962f3-111">These web services could be consumed by users – potentially directly on the marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="962f3-112">Ma lo scopo del servizio Web è anche un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="962f3-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="962f3-113">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="962f3-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="962f3-114">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del sito Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="962f3-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world – no infrastructure setup by the author of the web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="962f3-115">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="962f3-115">Consumption of web service</span></span>
<span data-ttu-id="962f3-116">Binomial Distribution Suite include i tre servizi seguenti:</span><span class="sxs-lookup"><span data-stu-id="962f3-116">The Binomial Distribution Suite includes the following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="962f3-117">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="962f3-118">Questo servizio accetta quattro argomenti di una distribuzione normale e calcola il quantile associato.</span><span class="sxs-lookup"><span data-stu-id="962f3-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>
<span data-ttu-id="962f3-119">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="962f3-119">The input arguments are:</span></span>

* <span data-ttu-id="962f3-120">p: probabilità aggregata singola di più prove.</span><span class="sxs-lookup"><span data-stu-id="962f3-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="962f3-121">size: numero di prove.</span><span class="sxs-lookup"><span data-stu-id="962f3-121">size - The number of trials.</span></span>
* <span data-ttu-id="962f3-122">prob: probabilità di successo in una prova.</span><span class="sxs-lookup"><span data-stu-id="962f3-122">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="962f3-123">Side: L per la parte inferiore della distribuzione, U per la parte superiore della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="962f3-123">Side - L for the lower side of the distribution, U for the upper side of the distribution.</span></span> 

<span data-ttu-id="962f3-124">L'output del servizio corrisponde al quantile calcolato associato alla probabilità specificata.</span><span class="sxs-lookup"><span data-stu-id="962f3-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="962f3-125">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="962f3-126">Questo servizio accetta quattro argomenti di una distribuzione binomiale e calcola la probabilità associata.</span><span class="sxs-lookup"><span data-stu-id="962f3-126">This service accepts 4 arguments of a binomial distribution and calculates the associated probability.</span></span>
<span data-ttu-id="962f3-127">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="962f3-127">The input arguments are:</span></span>

* <span data-ttu-id="962f3-128">q: singolo quantile di un evento con distribuzione binomiale.</span><span class="sxs-lookup"><span data-stu-id="962f3-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="962f3-129">size: numero di prove.</span><span class="sxs-lookup"><span data-stu-id="962f3-129">size - The number of trials.</span></span>
* <span data-ttu-id="962f3-130">prob: probabilità di successo in una prova.</span><span class="sxs-lookup"><span data-stu-id="962f3-130">prob - The probability of success in a trial.</span></span>
* <span data-ttu-id="962f3-131">side: L per la parte inferiore della distribuzione, U per la parte superiore della distribuzione oppure E che equivale a un numero singolo di successi.</span><span class="sxs-lookup"><span data-stu-id="962f3-131">side - L for the lower side of the distribution, U for the upper side of the distribution, or E that is equal to a single number of successes.</span></span>

<span data-ttu-id="962f3-132">L'output del servizio corrisponde alla probabilità calcolata associata al quantile specificato.</span><span class="sxs-lookup"><span data-stu-id="962f3-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="962f3-133">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="962f3-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="962f3-134">Questo servizio accetta tre argomenti di una distribuzione binomiale e genera una sequenza casuale di numeri distribuiti in modo binomiale.</span><span class="sxs-lookup"><span data-stu-id="962f3-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="962f3-135">È necessario fornire gli argomenti seguenti nella richiesta:</span><span class="sxs-lookup"><span data-stu-id="962f3-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="962f3-136">n: numero di osservazioni.</span><span class="sxs-lookup"><span data-stu-id="962f3-136">n - Number of observations.</span></span> 
* <span data-ttu-id="962f3-137">size: numero di prove.</span><span class="sxs-lookup"><span data-stu-id="962f3-137">size - Number of trials.</span></span>
* <span data-ttu-id="962f3-138">prob: probabilità di successo.</span><span class="sxs-lookup"><span data-stu-id="962f3-138">prob - Probability of success.</span></span>

<span data-ttu-id="962f3-139">L'output del servizio corrisponde a una sequenza di lunghezza n con una distribuzione binomiale basata sugli argomenti size e prob.</span><span class="sxs-lookup"><span data-stu-id="962f3-139">The output of the service is a sequence of length n with a binomial distribution based on the size and prob arguments.</span></span>

> <span data-ttu-id="962f3-140">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="962f3-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="962f3-141">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per app di esempio, vedere qui: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator).</span><span class="sxs-lookup"><span data-stu-id="962f3-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="962f3-142">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="962f3-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="962f3-143">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-143">Binomial Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void main()
    {
            var input = new Input() { p = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="962f3-144">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-144">Binomial Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string size;
            public string prob;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, size = TextBox2.Text, prob = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = " PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="binomial-distribution-generator"></a><span data-ttu-id="962f3-145">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="962f3-145">Binomial Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string size;
            public string p;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, size = TextBox2.Text, p = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }





## <a name="creation-of-web-service"></a><span data-ttu-id="962f3-146">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="962f3-146">Creation of web service</span></span>
> <span data-ttu-id="962f3-147">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="962f3-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="962f3-148">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="962f3-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="962f3-149">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="962f3-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="962f3-150">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-150">Binomial Distribution Quantile Calculator</span></span>
![Creare un'area di lavoro][4]

#### <a name="module-1"></a><span data-ttu-id="962f3-152">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="962f3-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port
#### <a name="module-2"></a><span data-ttu-id="962f3-153">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="962f3-153">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }

    if (param$prob < 0 ) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 0
    } else if (param$prob > 1) {
    print('Bad input: prob must be between 0 and 1')
    param$prob = 1
    }

    quantile = qbinom(param$p,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    quantile

    if (param$side == 'U'){
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = F)
    band=subset(df,x>quantile)
    } else if (param$side =='L') {
    quantile = qbinom(param$p,size=param$size,prob=param$prob,lower.tail = T)
    band=subset(df,x<=quantile)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(quantile)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="962f3-154">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="962f3-154">Binomial Distribution Probability Calculator</span></span>
![Creare un'area di lavoro][5]

#### <a name="module-1"></a><span data-ttu-id="962f3-156">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="962f3-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data to output port


#### <a name="module-2"></a><span data-ttu-id="962f3-157">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="962f3-157">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    prob = pbinom(param$q,size=param$size,prob=param$prob)
    prob.eq = dbinom(param$q,size=param$size,prob=param$prob)
    df = data.frame(x=1:param$size, prob=dbinom(1:param$size, param$size, prob=param$prob))
    prob

    if (param$side == 'U'){
    prob = 1 - prob
    band=subset(df,x>param$q)
    } else if (param$side =='E') {
    prob = prob.eq
    band=subset(df,x==param$q)
    } else if (param$side =='L') {
    prob = prob
    band=subset(df,x<=param$q)
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="962f3-158">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="962f3-158">Binomial Distribution Generator</span></span>
![Creare un'area di lavoro][6]

#### <a name="module-1"></a><span data-ttu-id="962f3-160">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="962f3-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data to output port

#### <a name="module-2"></a><span data-ttu-id="962f3-161">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="962f3-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="962f3-162">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="962f3-162">Limitations</span></span>
<span data-ttu-id="962f3-163">Questi sono esempi molto semplici relativi alla distribuzione binomiale.</span><span class="sxs-lookup"><span data-stu-id="962f3-163">These are very simple examples surrounding the binomial distribution.</span></span> <span data-ttu-id="962f3-164">Come si può notare dal codice di esempio precedente, è implementata un rilevamento limitato degli errori.</span><span class="sxs-lookup"><span data-stu-id="962f3-164">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="962f3-165">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="962f3-165">FAQ</span></span>
<span data-ttu-id="962f3-166">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="962f3-166">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

