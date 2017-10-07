---
title: Azure - esponenziale anti-aliasing - Forecasting AAA(deprecated) | Documenti Microsoft
description: (Deprecato) Servizio Web - Previsione - Smorzamento esponenziale
services: machine-learning
documentationcenter: 
author: yijichen
manager: jhubbard
editor: cgronlun
ms.assetid: a4150681-6eac-4145-9eca-0cdf60781dde
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: yijichen
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: ebc732d3a47943405b0cb26a373f529a50de9005
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="54a07-103">(Deprecato) Previsione - Smorzamento esponenziale</span><span class="sxs-lookup"><span data-stu-id="54a07-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="54a07-104">è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="54a07-104">hello Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="54a07-105">Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="54a07-105">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="54a07-106">Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="54a07-106">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="54a07-107">Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/ets) implementa hello Smorzamento esponenziale modello (ETS) tooproduce le stime basate sui dati cronologici di hello specificati dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="54a07-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements hello Exponential Smoothing model (ETS) tooproduce predictions based on hello historical data provided by hello user.</span></span> <span data-ttu-id="54a07-108">Verrà hello richiesta per un aumento di prodotto specifico, quest'anno?</span><span class="sxs-lookup"><span data-stu-id="54a07-108">Will hello demand for a specific product increase this year?</span></span> <span data-ttu-id="54a07-109">È possibile prevedere le vendite del prodotto per hello stagione Natale, in modo che è possibile pianificare l'inventario in modo efficace?</span><span class="sxs-lookup"><span data-stu-id="54a07-109">Can I predict my product sales for hello Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="54a07-110">I modelli di previsione sono tooaddress apt tali domande.</span><span class="sxs-lookup"><span data-stu-id="54a07-110">Forecasting models are apt tooaddress such questions.</span></span> <span data-ttu-id="54a07-111">Dato hello oltre i dati, questi modelli esaminare tendenze nascoste e tendenze future toopredict di stagionalità.</span><span class="sxs-lookup"><span data-stu-id="54a07-111">Given hello past data, these models examine hidden trends and seasonality toopredict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="54a07-112">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="54a07-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="54a07-113">Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R.</span><span class="sxs-lookup"><span data-stu-id="54a07-113">But hello purpose of hello web service is also tooserve as an example of how Azure Machine Learning can be used toocreate web services on top of R code.</span></span> <span data-ttu-id="54a07-114">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="54a07-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="54a07-115">servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.</span><span class="sxs-lookup"><span data-stu-id="54a07-115">hello web service can then be published toohello Azure Marketplace and consumed by users and devices across hello world with no infrastructure setup by hello author of hello web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="54a07-116">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="54a07-116">Consumption of web service</span></span>
<span data-ttu-id="54a07-117">Il servizio accetta 4 argomenti e calcola le previsioni ETS hello.</span><span class="sxs-lookup"><span data-stu-id="54a07-117">This service accepts 4 arguments and calculates hello ETS forecasts.</span></span>
<span data-ttu-id="54a07-118">gli argomenti di input Hello sono:</span><span class="sxs-lookup"><span data-stu-id="54a07-118">hello input arguments are:</span></span>

* <span data-ttu-id="54a07-119">Frequenza: indica la frequenza di hello di dati non elaborati hello (giornaliera/settimanale/mensile o trimestrale/annuali).</span><span class="sxs-lookup"><span data-stu-id="54a07-119">Frequency - Indicates hello frequency of hello raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="54a07-120">Horizon: intervallo di tempo futuro della previsione</span><span class="sxs-lookup"><span data-stu-id="54a07-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="54a07-121">Data - Aggiungi nella serie temporale nuovo hello dati per volta.</span><span class="sxs-lookup"><span data-stu-id="54a07-121">Date - Add in hello new time series data for time.</span></span>
* <span data-ttu-id="54a07-122">Valore - aggiungere hello nuova serie dati i valori.</span><span class="sxs-lookup"><span data-stu-id="54a07-122">Value - Add in hello new time series data values.</span></span>

<span data-ttu-id="54a07-123">output di Hello del servizio hello è hello calcolati i valori di previsione.</span><span class="sxs-lookup"><span data-stu-id="54a07-123">hello output of hello service is hello calculated forecast values.</span></span>

<span data-ttu-id="54a07-124">L'input può essere ad esempio il seguente:</span><span class="sxs-lookup"><span data-stu-id="54a07-124">Sample input could be:</span></span> 

* <span data-ttu-id="54a07-125">Frequency - 12</span><span class="sxs-lookup"><span data-stu-id="54a07-125">Frequency - 12</span></span>
* <span data-ttu-id="54a07-126">Horizon - 12</span><span class="sxs-lookup"><span data-stu-id="54a07-126">Horizon - 12</span></span>
* <span data-ttu-id="54a07-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="54a07-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="54a07-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="54a07-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="54a07-129">Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET.</span><span class="sxs-lookup"><span data-stu-id="54a07-129">This service, as hosted on hello Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="54a07-130">Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span><span class="sxs-lookup"><span data-stu-id="54a07-130">There are multiple ways of consuming hello service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="54a07-131">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="54a07-131">Starting C# code for web service consumption:</span></span>
    public class Input
    {
            public string frequency;
            public string horizon;
            public string date;
            public string value;
    }

    public AuthenticationHeaderValue CreateBasicHeader(string username, string password)
    {
            byte[] byteArray = System.Text.Encoding.UTF8.GetBytes(username + ":" + password);
            return new AuthenticationHeaderValue("Basic", Convert.ToBase64String(byteArray));
    }

    void Main()
    {
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };
            var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }



## <a name="creation-of-web-service"></a><span data-ttu-id="54a07-132">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="54a07-132">Creation of web service</span></span>
> <span data-ttu-id="54a07-133">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="54a07-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="54a07-134">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="54a07-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="54a07-135">Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.</span><span class="sxs-lookup"><span data-stu-id="54a07-135">Below is a screenshot of hello experiment that created hello web service and example code for each of hello modules within hello experiment.</span></span>
> 
> 

<span data-ttu-id="54a07-136">In Azure Machine Learning è stato creato un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="54a07-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="54a07-137">Sono stati caricati dati di input di esempio con uno schema dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="54a07-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="54a07-138">Schema dati toohello collegato è un [Execute R Script] [ execute-r-script] modulo che genera l'errore hello ETS modello di previsione utilizzando 'ets' e 'previsione' funzioni da R.</span><span class="sxs-lookup"><span data-stu-id="54a07-138">Linked toohello data schema is an [Execute R Script][execute-r-script] module that generates hello ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="54a07-140">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="54a07-140">Module 1:</span></span>
    # Add in hello CSV file with hello data in hello format shown below 
![Dati di esempio][3]    

#### <a name="module-2"></a><span data-ttu-id="54a07-142">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="54a07-142">Module 2:</span></span>
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time-series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- ets(train_ts)
    train_model <- forecast(fit1, h = data$horizon)
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");


## <a name="limitations"></a><span data-ttu-id="54a07-143">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="54a07-143">Limitations</span></span>
<span data-ttu-id="54a07-144">Questo è un esempio molto semplice di previsione ETS.</span><span class="sxs-lookup"><span data-stu-id="54a07-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="54a07-145">Come possono essere visualizzati dal codice di esempio hello precedente, non viene implementato alcun rilevamento di errori e servizio hello si presuppone che tutte le variabili di hello sono valori continui/positive e frequenza di hello deve essere un numero intero maggiore di 1.</span><span class="sxs-lookup"><span data-stu-id="54a07-145">As can be seen from hello example code above, no error catching is implemented, and hello service assumes that all hello variables are continuous/positive values and hello frequency should be an integer greater than 1.</span></span> <span data-ttu-id="54a07-146">lunghezza Hello dei vettori di hello data e il valore deve essere hello stesso.</span><span class="sxs-lookup"><span data-stu-id="54a07-146">hello length of hello date and value vectors should be hello same.</span></span> <span data-ttu-id="54a07-147">variabile di tipo date Hello deve rispettare toohello formato "mm/gg/aaaa'.</span><span class="sxs-lookup"><span data-stu-id="54a07-147">hello date variable should adhere toohello format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="54a07-148">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="54a07-148">FAQ</span></span>
<span data-ttu-id="54a07-149">Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="54a07-149">For frequently asked questions on consumption of hello web service or publishing toohello Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

