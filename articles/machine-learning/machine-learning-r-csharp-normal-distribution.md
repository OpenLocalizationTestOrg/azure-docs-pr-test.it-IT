---
title: 'AAA(deprecated) Suite di servizio Web di distribuzione normale: Azure | Documenti Microsoft'
description: (Deprecato) Normal Distribution Web Service Suite
services: machine-learning
documentationcenter: 
author: ireiter
manager: jhubbard
editor: cgronlun
ms.assetid: aab7b92e-953b-43d8-b0af-031394406bfe
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
ms.openlocfilehash: 8bdb5afd9fee88587f548d7c5299480f64289bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="85d2d-103">(Deprecato) Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="85d2d-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="85d2d-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="85d2d-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="85d2d-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="85d2d-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="85d2d-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="85d2d-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="85d2d-107">Gruppo di distribuzione normale Hello è un set di servizi web di esempio ([generatore](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calcolatrice](https://datamarket.azure.com/dataset/aml_labs/ndq5), [calcolatrice probabilità](https://datamarket.azure.com/dataset/aml_labs/ndp5)) che facilitano la generazione e la gestione distribuzioni normali.</span><span class="sxs-lookup"><span data-stu-id="85d2d-107">hello Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="85d2d-108">servizi Hello consentono la generazione di una sequenza di distribuzione normale di qualsiasi lunghezza, il calcolo dei quantili da una probabilità specificata e il calcolo delle probabilità da un determinato quantile.</span><span class="sxs-lookup"><span data-stu-id="85d2d-108">hello services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="85d2d-109">Ognuno dei servizi hello genera output diversi basati sul servizio hello selezionato (vedere la descrizione riportata di seguito).</span><span class="sxs-lookup"><span data-stu-id="85d2d-109">Each of hello services emits different outputs based on hello selected service (see description below).</span></span> <span data-ttu-id="85d2d-110">Gruppo di distribuzione normale di Hello dipende hello R funzioni qnorm rnorm e pnorm, che sono inclusi nel pacchetto di statistiche di R.</span><span class="sxs-lookup"><span data-stu-id="85d2d-110">hello Normal Distribution Suite is based on hello R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="85d2d-111">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="85d2d-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="85d2d-112">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="85d2d-112">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="85d2d-113">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="85d2d-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="85d2d-114">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-114">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="85d2d-115">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="85d2d-115">Consumption of web service</span></span>
<span data-ttu-id="85d2d-116">Hello distribuzione normale Suite include hello dopo 3 servizi.</span><span class="sxs-lookup"><span data-stu-id="85d2d-116">hello Normal Distribution Suite includes hello following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="85d2d-117">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="85d2d-118">Il servizio accetta 4 argomenti di una distribuzione normale e calcola i quantili hello associata.</span><span class="sxs-lookup"><span data-stu-id="85d2d-118">This service accepts 4 arguments of a normal distribution and calculates hello associated quantile.</span></span>

<span data-ttu-id="85d2d-119">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="85d2d-119">hello input arguments are:</span></span>

* <span data-ttu-id="85d2d-120">p: probabilità singola di un evento con distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="85d2d-121">Media - Media distribuzione normale hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-121">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="85d2d-122">SD - hello la deviazione standard di distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-122">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="85d2d-123">Lato - L per lato inferiore di hello della distribuzione hello e U sul lato superiore di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-123">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="85d2d-124">output di Hello del servizio hello è quantile hello calcolato che è associato a hello dato probabilità.</span><span class="sxs-lookup"><span data-stu-id="85d2d-124">hello output of hello service is hello calculated quantile that is associated with hello given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="85d2d-125">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="85d2d-126">Il servizio accetta 4 argomenti di una distribuzione normale e calcola la probabilità associata hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-126">This service accepts 4 arguments of a normal distribution and calculates hello associated probability.</span></span>

<span data-ttu-id="85d2d-127">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="85d2d-127">hello input arguments are:</span></span>

* <span data-ttu-id="85d2d-128">q: singolo quantile di un evento con distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="85d2d-129">Media - Media distribuzione normale hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-129">Mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="85d2d-130">SD - hello la deviazione standard di distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-130">SD - hello normal distribution standard deviation.</span></span> 
* <span data-ttu-id="85d2d-131">Lato - L per lato inferiore di hello della distribuzione hello e U sul lato superiore di hello della distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-131">Side - L for hello lower side of hello distribution and U for hello upper side of hello distribution.</span></span>

<span data-ttu-id="85d2d-132">output di Hello del servizio hello è hello calcolata la probabilità che è associato a hello specificato di quantili.</span><span class="sxs-lookup"><span data-stu-id="85d2d-132">hello output of hello service is hello calculated probability that is associated with hello given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="85d2d-133">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="85d2d-133">Normal Distribution Generator</span></span>
<span data-ttu-id="85d2d-134">Questo servizio accetta tre argomenti di una distribuzione normale e genera una sequenza casuale di numeri distribuiti in modo normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="85d2d-135">Hello seguenti devono essere specificati argomenti tooit richiesta hello:</span><span class="sxs-lookup"><span data-stu-id="85d2d-135">hello following arguments should be provided tooit within hello request:</span></span>

* <span data-ttu-id="85d2d-136">n - numero di hello di osservazioni.</span><span class="sxs-lookup"><span data-stu-id="85d2d-136">n - hello number of observations.</span></span> 
* <span data-ttu-id="85d2d-137">Media - Media distribuzione normale hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-137">mean - hello normal distribution mean.</span></span>
* <span data-ttu-id="85d2d-138">SD - hello la deviazione standard di distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="85d2d-138">sd - hello normal distribution standard deviation.</span></span> 

<span data-ttu-id="85d2d-139">output di Hello del servizio hello è una sequenza di lunghezza n con una distribuzione normale in base agli argomenti Media e sd hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-139">hello output of hello service is a sequence of length n with a normal distribution based on hello mean and sd arguments.</span></span>

> <span data-ttu-id="85d2d-140">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="85d2d-140">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="85d2d-141">Esistono diversi modi di utilizzo di servizio hello in modo automatico (app di esempio in questa sezione sono: [generatore](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [calcolatrice probabilità](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calcolatrice](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span><span class="sxs-lookup"><span data-stu-id="85d2d-141">There are multiple ways of consuming hello service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="85d2d-142">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="85d2d-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="85d2d-143">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-143">Normal Distribution Quantile Calculator</span></span>
    public class Input
    {
            public string p;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { p = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="85d2d-144">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-144">Normal Distribution Probability Calculator</span></span>
    public class Input
    {
            public string q;
            public string mean;
            public string sd;
            public string side;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { q = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text, side = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }

### <a name="normal-distribution-generator"></a><span data-ttu-id="85d2d-145">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="85d2d-145">Normal Distribution Generator</span></span>
    public class Input
    {
            public string n;
            public string mean;
            public string sd;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { n = TextBox1.Text, mean = TextBox2.Text, sd = TextBox3.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a><span data-ttu-id="85d2d-146">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="85d2d-146">Creation of web service</span></span>
> <span data-ttu-id="85d2d-147">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="85d2d-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="85d2d-148">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="85d2d-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="85d2d-149">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-149">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="85d2d-150">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="85d2d-151">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="85d2d-151">Experiment flow:</span></span>

![Flusso dell'esperimento][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    if (param$p < 0 ) {
    print('Bad input: p must be between 0 and 1')
    param$p = 0
    } else if (param$p > 1) {
    print('Bad input: p must be between 0 and 1')
    param$p = 1
    }
    q = qnorm(param$p,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    q = 2* param$mean - q
    } else if (param$side =='L') {
    q = q
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(q)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="85d2d-153">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="85d2d-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="85d2d-154">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="85d2d-154">Experiment flow:</span></span>

![Flusso dell'esperimento][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    prob = pnorm(param$q,mean=param$mean,sd=param$sd)

    if (param$side == 'U'){
    prob = 1 - prob
    } else if (param$side =='B') {
    prob = ifelse(prob<=0.5,prob * 2, 1)
    } else if (param$side =='L') {
    prob = prob
    } else {
    print("Invalid side choice")
    }

    output = as.data.frame(prob)

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="85d2d-156">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="85d2d-156">Normal Distribution Generator</span></span>
<span data-ttu-id="85d2d-157">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="85d2d-157">Experiment flow:</span></span>

![Flusso dell'esperimento][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data toooutput port

    # Map 1-based optional input ports toovariables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame toobe sent toohello output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="85d2d-159">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="85d2d-159">Limitations</span></span>
<span data-ttu-id="85d2d-160">Questi sono esempi molto semplici che circonda distribuzione normale hello.</span><span class="sxs-lookup"><span data-stu-id="85d2d-160">These are very simple examples surrounding hello normal distribution.</span></span> <span data-ttu-id="85d2d-161">Come si può notare dal codice di esempio hello precedente, il rilevamento di errori poco viene implementato.</span><span class="sxs-lookup"><span data-stu-id="85d2d-161">As can be seen from hello example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="85d2d-162">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="85d2d-162">FAQ</span></span>
<span data-ttu-id="85d2d-163">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="85d2d-163">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

