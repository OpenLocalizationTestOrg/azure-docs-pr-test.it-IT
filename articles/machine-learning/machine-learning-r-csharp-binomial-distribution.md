---
title: 'AAA(deprecated) distribuzione binomiale Suite: Azure | Documenti Microsoft'
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
redirect_document_id: True
ms.openlocfilehash: 6f94436cd19abeb518d179f340c8d4f43fcf4520
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-binomial-distribution-suite"></a><span data-ttu-id="3cd15-103">(Deprecato) Binomial Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="3cd15-103">(deprecated) Binomial Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="3cd15-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="3cd15-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="3cd15-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="3cd15-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="3cd15-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="3cd15-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="3cd15-107">Distribuzione binomiale Suite Hello è un set di servizi web di esempio ([binomiale generatore](https://datamarket.azure.com/dataset/aml_labs/bdg5), [calcolatrice probabilità](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calcolatrice](https://datamarket.azure.com/dataset/aml_labs/bdq5)) che consentono di generare e gestione di binomiale.</span><span class="sxs-lookup"><span data-stu-id="3cd15-107">hello Binomial Distribution Suite is a set of sample web services ([Binomial Generator](https://datamarket.azure.com/dataset/aml_labs/bdg5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/bdp4), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/bdq5)) that help in generating and dealing with binomial distributions.</span></span> <span data-ttu-id="3cd15-108">Hello services consente la generazione di una sequenza di distribuzione binomiale di qualsiasi lunghezza, il calcolo dei quantili fuori specificato da un determinato quantile probabilità e il calcolo di probabilità.</span><span class="sxs-lookup"><span data-stu-id="3cd15-108">hello services allow generating a binomial distribution sequence of any length, calculating quantiles out of given probability and calculating probability from a given quantile.</span></span> <span data-ttu-id="3cd15-109">Ognuno dei servizi hello genera output diversi basati sul servizio hello selezionato (vedere la descrizione riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="3cd15-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="3cd15-110">Distribuzione binomiale Suite Hello dipende hello R funzioni qbinom rbinom e pbinom, che sono inclusi nel pacchetto di hello R statistiche.</span><span class="sxs-lookup"><span data-stu-id="3cd15-110">hello Binomial Distribution Suite is based on hello R functions qbinom, rbinom, and pbinom, which are included in hello R stats package.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="3cd15-111">Questi servizi web che poteva essere usati dagli utenti: potenzialmente direttamente nel marketplace hello, tramite un'app per dispositivi mobili, tramite un sito Web, o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="3cd15-111">These web services could be consumed by users – potentially directly on hello marketplace, through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="3cd15-112">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="3cd15-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="3cd15-113">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="3cd15-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="3cd15-114">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e non utilizzati da utenti e dispositivi attraverso HelloWorld – alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="3cd15-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world – no infrastructure setup by hello author of hello web service is required.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="3cd15-115">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="3cd15-115">Consumption of web service</span></span>
<span data-ttu-id="3cd15-116">Hello binomiale Suite include hello dopo 3 servizi.</span><span class="sxs-lookup"><span data-stu-id="3cd15-116">hello Binomial Distribution Suite includes hello following 3 services.</span></span>

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3cd15-117">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-117">Binomial Distribution Quantile Calculator</span></span>
<span data-ttu-id="3cd15-118">Il servizio accetta 4 argomenti di una distribuzione normale e calcola i quantili hello associata.</span><span class="sxs-lookup"><span data-stu-id="3cd15-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>
<span data-ttu-id="3cd15-119">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="3cd15-119">hello input arguments are:</span></span>

* <span data-ttu-id="3cd15-120">p: probabilità aggregata singola di più prove.</span><span class="sxs-lookup"><span data-stu-id="3cd15-120">p - A single aggregated probability of multiple trials.</span></span>  
* <span data-ttu-id="3cd15-121">dimensione - numero hello di prove.</span><span class="sxs-lookup"><span data-stu-id="3cd15-121">size - hello number of trials.</span></span>
* <span data-ttu-id="3cd15-122">probabilità - probabilità hello di successo in una versione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="3cd15-122">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3cd15-123">Lato - L per lato inferiore di hello della distribuzione di hello, U sul lato superiore di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="3cd15-123">Side - L for hello lower side of hello distribution, U for hello upper side of hello distribution.</span></span> 

<span data-ttu-id="3cd15-124">output di Hello del servizio hello è quantile hello calcolato che è associato a hello dato probabilità.</span><span class="sxs-lookup"><span data-stu-id="3cd15-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3cd15-125">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-125">Binomial Distribution Probability Calculator</span></span>
<span data-ttu-id="3cd15-126">Il servizio accetta 4 argomenti di una distribuzione binomiale e calcola la probabilità associata hello.</span><span class="sxs-lookup"><span data-stu-id="3cd15-126">This service accepts 4 arguments of a binomial distribution and calculates hello associated probability.</span></span>
<span data-ttu-id="3cd15-127">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="3cd15-127">hello input arguments are:</span></span>

* <span data-ttu-id="3cd15-128">q: singolo quantile di un evento con distribuzione binomiale.</span><span class="sxs-lookup"><span data-stu-id="3cd15-128">q - A single quantile of an event with binomial distribution.</span></span> 
* <span data-ttu-id="3cd15-129">dimensione - numero hello di prove.</span><span class="sxs-lookup"><span data-stu-id="3cd15-129">size - hello number of trials.</span></span>
* <span data-ttu-id="3cd15-130">probabilità - probabilità hello di successo in una versione di valutazione.</span><span class="sxs-lookup"><span data-stu-id="3cd15-130">prob - hello probability of success in a trial.</span></span>
* <span data-ttu-id="3cd15-131">lato - L per lato inferiore di hello della distribuzione di hello, U sul lato superiore di hello della distribuzione hello o E che è uguale tooa singolo numero di esiti positivi.</span><span class="sxs-lookup"><span data-stu-id="3cd15-131">side - L for hello lower side of hello distribution, U for hello upper side of hello distribution, or E that is equal tooa single number of successes.</span></span>

<span data-ttu-id="3cd15-132">output di Hello del servizio hello è hello calcolata la probabilità che è associato a hello specificato di quantili.</span><span class="sxs-lookup"><span data-stu-id="3cd15-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3cd15-133">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="3cd15-133">Binomial Distribution Generator</span></span>
<span data-ttu-id="3cd15-134">Questo servizio accetta tre argomenti di una distribuzione binomiale e genera una sequenza casuale di numeri distribuiti in modo binomiale.</span><span class="sxs-lookup"><span data-stu-id="3cd15-134">This service accepts 3 arguments of a binomial distribution and generates a random sequence of numbers that are binomially distributed.</span></span> <span data-ttu-id="3cd15-135">Hello seguenti devono essere specificati argomenti tooit richiesta hello:</span><span class="sxs-lookup"><span data-stu-id="3cd15-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="3cd15-136">n: numero di osservazioni.</span><span class="sxs-lookup"><span data-stu-id="3cd15-136">n - Number of observations.</span></span> 
* <span data-ttu-id="3cd15-137">size: numero di prove.</span><span class="sxs-lookup"><span data-stu-id="3cd15-137">size - Number of trials.</span></span>
* <span data-ttu-id="3cd15-138">prob: probabilità di successo.</span><span class="sxs-lookup"><span data-stu-id="3cd15-138">prob - Probability of success.</span></span>

<span data-ttu-id="3cd15-139">output di Hello del servizio hello è una sequenza di lunghezza n con una distribuzione binomiale basata sugli argomenti di dimensioni e la probabilità di hello.</span><span class="sxs-lookup"><span data-stu-id="3cd15-139">hello output of hello service is a sequence of length n with a binomial distribution based on hello size and prob arguments.</span></span>

> <span data-ttu-id="3cd15-140">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="3cd15-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="3cd15-141">Esistono diversi modi di utilizzo di servizio hello in modo automatico (app di esempio in questa sezione sono: [generatore](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [calcolatrice probabilità](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calcolatrice](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span><span class="sxs-lookup"><span data-stu-id="3cd15-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/BinomialDistributionQuantileCalculator)).</span></span> 

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="3cd15-142">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="3cd15-142">Starting C# code for web service consumption:</span></span>
### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3cd15-143">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-143">Binomial Distribution Quantile Calculator</span></span>
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

### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3cd15-144">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-144">Binomial Distribution Probability Calculator</span></span>
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


### <a name="binomial-distribution-generator"></a><span data-ttu-id="3cd15-145">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="3cd15-145">Binomial Distribution Generator</span></span>
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





## <a name="creation-of-web-service"></a><span data-ttu-id="3cd15-146">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="3cd15-146">Creation of web service</span></span>
> <span data-ttu-id="3cd15-147">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="3cd15-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="3cd15-148">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="3cd15-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="3cd15-149">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="3cd15-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

### <a name="binomial-distribution-quantile-calculator"></a><span data-ttu-id="3cd15-150">Binomial Distribution Quantile Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-150">Binomial Distribution Quantile Calculator</span></span>
![Creare un'area di lavoro][4]

#### <a name="module-1"></a><span data-ttu-id="3cd15-152">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="3cd15-152">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port
#### <a name="module-2"></a><span data-ttu-id="3cd15-153">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="3cd15-153">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");


### <a name="binomial-distribution-probability-calculator"></a><span data-ttu-id="3cd15-154">Binomial Distribution Probability Calculator</span><span class="sxs-lookup"><span data-stu-id="3cd15-154">Binomial Distribution Probability Calculator</span></span>
![Creare un'area di lavoro][5]

#### <a name="module-1"></a><span data-ttu-id="3cd15-156">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="3cd15-156">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(q=5,size=10,prob=.5,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port


#### <a name="module-2"></a><span data-ttu-id="3cd15-157">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="3cd15-157">Module 2:</span></span>
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

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="binomial-distribution-generator"></a><span data-ttu-id="3cd15-158">Binomial Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="3cd15-158">Binomial Distribution Generator</span></span>
![Creare un'area di lavoro][6]

#### <a name="module-1"></a><span data-ttu-id="3cd15-160">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="3cd15-160">Module 1:</span></span>
    #data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,size=10,p=.5);
    maml.mapOutputPort("data.set"); #send data toooutput port

#### <a name="module-2"></a><span data-ttu-id="3cd15-161">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="3cd15-161">Module 2:</span></span>
    dataset1 <- maml.mapInputPort(1) # class: data.frame
    param = dataset1
    dist = rbinom(param$n,param$size,param$p)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="3cd15-162">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="3cd15-162">Limitations</span></span>
<span data-ttu-id="3cd15-163">Questi sono esempi molto semplici che circonda hello binomiale.</span><span class="sxs-lookup"><span data-stu-id="3cd15-163">These are very simple examples surrounding hello binomial distribution.</span></span> <span data-ttu-id="3cd15-164">Come si può notare dal codice di esempio hello precedente, il rilevamento di errori poco viene implementato.</span><span class="sxs-lookup"><span data-stu-id="3cd15-164">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="3cd15-165">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3cd15-165">FAQ</span></span>
<span data-ttu-id="3cd15-166">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3cd15-166">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_1.png

[2]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_2.png

[3]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_3.png

[4]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_4.png

[5]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_5.png

[6]: ./media/machine-learning-r-csharp-binomial-distribution/binomial_6.png

