---
title: (Deprecato) Normal Distribution Web Service Suite - Azure | Documentazione Microsoft
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
redirect_document_id: TRUE
ms.openlocfilehash: 79d1621330ad56b0c62ca46cfac424c2306e371f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-normal-distribution-suite"></a><span data-ttu-id="bdab1-103">(Deprecato) Normal Distribution Suite</span><span class="sxs-lookup"><span data-stu-id="bdab1-103">(deprecated) Normal Distribution Suite</span></span>

> [!NOTE]
> <span data-ttu-id="bdab1-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="bdab1-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="bdab1-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="bdab1-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bdab1-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="bdab1-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bdab1-107">Normal Distribution Suite è un set di servizi Web di esempio ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) che semplificano la generazione e la gestione delle distribuzioni normali.</span><span class="sxs-lookup"><span data-stu-id="bdab1-107">The Normal Distribution Suite is a set of sample web services ([Generator](https://datamarket.azure.com/dataset/aml_labs/ndg7), [Quantile Calculator](https://datamarket.azure.com/dataset/aml_labs/ndq5), [Probability Calculator](https://datamarket.azure.com/dataset/aml_labs/ndp5)) that help in generating and handling normal distributions.</span></span> <span data-ttu-id="bdab1-108">I servizi permettono la generazione di una sequenza di distribuzioni normali di qualsiasi lunghezza, calcolando i quantili rispetto alla probabilità specificata e calcolando la probabilità in base a un quantile specificato.</span><span class="sxs-lookup"><span data-stu-id="bdab1-108">The services allow generating a normal distribution sequence of any length, calculating quantiles from a given probability, and calculating probability from a given quantile.</span></span> <span data-ttu-id="bdab1-109">Ogni servizio emette output diversi, in base al servizio selezionato, come illustrato più avanti.</span><span class="sxs-lookup"><span data-stu-id="bdab1-109">Each of the services emits different outputs based on the selected service (see description below).</span></span> <span data-ttu-id="bdab1-110">Normal Distribution Suite è basato sulle funzioni qnorm, rnorm e pnorm del codice R, incluse nel pacchetto statistico R.</span><span class="sxs-lookup"><span data-stu-id="bdab1-110">The Normal Distribution Suite is based on the R functions qnorm, rnorm, and pnorm, which are included in R stats package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="bdab1-111">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="bdab1-111">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="bdab1-112">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="bdab1-112">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="bdab1-113">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="bdab1-113">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="bdab1-114">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="bdab1-114">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>  
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="bdab1-115">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="bdab1-115">Consumption of web service</span></span>
<span data-ttu-id="bdab1-116">Normal Distribution Suite include i tre servizi seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdab1-116">The Normal Distribution Suite includes the following 3 services.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="bdab1-117">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-117">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="bdab1-118">Questo servizio accetta quattro argomenti di una distribuzione normale e calcola il quantile associato.</span><span class="sxs-lookup"><span data-stu-id="bdab1-118">This service accepts 4 arguments of a normal distribution and calculates the associated quantile.</span></span>

<span data-ttu-id="bdab1-119">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdab1-119">The input arguments are:</span></span>

* <span data-ttu-id="bdab1-120">p: probabilità singola di un evento con distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-120">p - A single probability of an event with normal distribution.</span></span> 
* <span data-ttu-id="bdab1-121">Mean: media della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-121">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="bdab1-122">SD: deviazione standard della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-122">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="bdab1-123">Side: L per la parte inferiore della distribuzione, U per la parte superiore della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bdab1-123">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="bdab1-124">L'output del servizio corrisponde al quantile calcolato associato alla probabilità specificata.</span><span class="sxs-lookup"><span data-stu-id="bdab1-124">The output of the service is the calculated quantile that is associated with the given probability.</span></span>

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="bdab1-125">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-125">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="bdab1-126">Questo servizio accetta quattro argomenti di una distribuzione normale e calcola la probabilità associata.</span><span class="sxs-lookup"><span data-stu-id="bdab1-126">This service accepts 4 arguments of a normal distribution and calculates the associated probability.</span></span>

<span data-ttu-id="bdab1-127">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="bdab1-127">The input arguments are:</span></span>

* <span data-ttu-id="bdab1-128">q: singolo quantile di un evento con distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-128">q - A single quantile of an event with normal distribution.</span></span> 
* <span data-ttu-id="bdab1-129">Mean: media della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-129">Mean - The normal distribution mean.</span></span>
* <span data-ttu-id="bdab1-130">SD: deviazione standard della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-130">SD - The normal distribution standard deviation.</span></span> 
* <span data-ttu-id="bdab1-131">Side: L per la parte inferiore della distribuzione, U per la parte superiore della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="bdab1-131">Side - L for the lower side of the distribution and U for the upper side of the distribution.</span></span>

<span data-ttu-id="bdab1-132">L'output del servizio corrisponde alla probabilità calcolata associata al quantile specificato.</span><span class="sxs-lookup"><span data-stu-id="bdab1-132">The output of the service is the calculated probability that is associated with the given quantile.</span></span>

### <a name="normal-distribution-generator"></a><span data-ttu-id="bdab1-133">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="bdab1-133">Normal Distribution Generator</span></span>
<span data-ttu-id="bdab1-134">Questo servizio accetta tre argomenti di una distribuzione normale e genera una sequenza casuale di numeri distribuiti in modo normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-134">This service accepts 3 arguments of a normal distribution and generates a random sequence of numbers that are normally distributed.</span></span> <span data-ttu-id="bdab1-135">È necessario fornire gli argomenti seguenti nella richiesta:</span><span class="sxs-lookup"><span data-stu-id="bdab1-135">The following arguments should be provided to it within the request:</span></span>

* <span data-ttu-id="bdab1-136">n: numero di osservazioni.</span><span class="sxs-lookup"><span data-stu-id="bdab1-136">n - The number of observations.</span></span> 
* <span data-ttu-id="bdab1-137">Mean: media della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-137">mean - The normal distribution mean.</span></span>
* <span data-ttu-id="bdab1-138">SD: deviazione standard della distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-138">sd - The normal distribution standard deviation.</span></span> 

<span data-ttu-id="bdab1-139">L'output del servizio corrisponde a una sequenza di lunghezza n con una distribuzione normale basata sugli argomenti mean e sd.</span><span class="sxs-lookup"><span data-stu-id="bdab1-139">The output of the service is a sequence of length n with a normal distribution based on the mean and sd arguments.</span></span>

> <span data-ttu-id="bdab1-140">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="bdab1-140">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="bdab1-141">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per app di esempio, vedere qui: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdab1-141">There are multiple ways of consuming the service in an automated fashion (example apps are here: [Generator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionGenerator.aspx), [Probability Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionProbabilityCalculator.aspx), [Quantile Calculator](http://microsoftazuremachinelearning.azurewebsites.net/NormalDistributionQuantileCalculator.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="bdab1-142">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="bdab1-142">Starting C# code for web service consumption:</span></span>
### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="bdab1-143">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-143">Normal Distribution Quantile Calculator</span></span>
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


### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="bdab1-144">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-144">Normal Distribution Probability Calculator</span></span>
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

### <a name="normal-distribution-generator"></a><span data-ttu-id="bdab1-145">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="bdab1-145">Normal Distribution Generator</span></span>
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


## <a name="creation-of-web-service"></a><span data-ttu-id="bdab1-146">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="bdab1-146">Creation of web service</span></span>
> <span data-ttu-id="bdab1-147">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bdab1-147">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="bdab1-148">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="bdab1-148">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> 
> 
> 

<span data-ttu-id="bdab1-149">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="bdab1-149">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>

### <a name="normal-distribution-quantile-calculator"></a><span data-ttu-id="bdab1-150">Normal Distribution Quantile Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-150">Normal Distribution Quantile Calculator</span></span>
<span data-ttu-id="bdab1-151">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="bdab1-151">Experiment flow:</span></span>

![Flusso dell'esperimento][2]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(p=0.1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-probability-calculator"></a><span data-ttu-id="bdab1-153">Normal Distribution Probability Calculator:</span><span class="sxs-lookup"><span data-stu-id="bdab1-153">Normal Distribution Probability Calculator</span></span>
<span data-ttu-id="bdab1-154">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="bdab1-154">Experiment flow:</span></span>

![Flusso dell'esperimento][3]

     #Data schema with example data (replaced with data from web service)
    data.set=data.frame(q=-1,mean=0,sd=1,side='L');
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
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

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

### <a name="normal-distribution-generator"></a><span data-ttu-id="bdab1-156">Normal Distribution Generator</span><span class="sxs-lookup"><span data-stu-id="bdab1-156">Normal Distribution Generator</span></span>
<span data-ttu-id="bdab1-157">Flusso dell'esperimento</span><span class="sxs-lookup"><span data-stu-id="bdab1-157">Experiment flow:</span></span>

![Flusso dell'esperimento][4]

    #Data schema with example data (replaced with data from web service)
    data.set=data.frame(n=50,mean=0,sd=1);
    maml.mapOutputPort("data.set"); #send data to output port

    # Map 1-based optional input ports to variables
    dataset1 <- maml.mapInputPort(1) # class: data.frame

    param = dataset1
    dist = rnorm(param$n,mean=param$mean,sd=param$sd)

    output = as.data.frame(t(dist))

    # Select data.frame to be sent to the output Dataset port
    maml.mapOutputPort("output");

## <a name="limitations"></a><span data-ttu-id="bdab1-159">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="bdab1-159">Limitations</span></span>
<span data-ttu-id="bdab1-160">Questi sono esempi molto semplici relativi alla distribuzione normale.</span><span class="sxs-lookup"><span data-stu-id="bdab1-160">These are very simple examples surrounding the normal distribution.</span></span> <span data-ttu-id="bdab1-161">Come si può notare dal codice di esempio precedente, è implementata un rilevamento limitato degli errori.</span><span class="sxs-lookup"><span data-stu-id="bdab1-161">As can be seen from the example code above, little error catching is implemented.</span></span>

## <a name="faq"></a><span data-ttu-id="bdab1-162">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="bdab1-162">FAQ</span></span>
<span data-ttu-id="bdab1-163">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="bdab1-163">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-normal-distribution/normal-img1.png
[2]: ./media/machine-learning-r-csharp-normal-distribution/normal-img2.png
[3]: ./media/machine-learning-r-csharp-normal-distribution/normal-img3.png
[4]: ./media/machine-learning-r-csharp-normal-distribution/normal-img4.png

