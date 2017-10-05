---
title: (Deprecato) Previsione - Smorzamento esponenziale - Azure | Documentazione Microsoft
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
redirect_document_id: TRUE
ms.openlocfilehash: 736d5d4adb8ecfd1e3372d273b64917f4a2e76ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-forecasting---exponential-smoothing"></a><span data-ttu-id="def60-103">(Deprecato) Previsione - Smorzamento esponenziale</span><span class="sxs-lookup"><span data-stu-id="def60-103">(deprecated) Forecasting - Exponential Smoothing</span></span>

> [!NOTE]
> <span data-ttu-id="def60-104">Microsoft DataMarket è in fase di ritiro e questa API è stata deprecata.</span><span class="sxs-lookup"><span data-stu-id="def60-104">The Microsoft DataMarket is being retired and this API has been deprecated.</span></span> 
> 
> <span data-ttu-id="def60-105">Numerose API e molti esperimenti utili di esempio sono disponibili in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="def60-105">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="def60-106">Per altre informazioni sulla raccolta, vedere [Condividere e scoprire risorse in Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span><span class="sxs-lookup"><span data-stu-id="def60-106">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="def60-107">Questo [servizio Web](https://datamarket.azure.com/dataset/aml_labs/ets) implementa il modello di livellamento esponenziale (ETS, Exponential Smoothing) per produrre previsioni basate sui dati cronologici forniti dall'utente.</span><span class="sxs-lookup"><span data-stu-id="def60-107">This [web service](https://datamarket.azure.com/dataset/aml_labs/ets) implements the Exponential Smoothing model (ETS) to produce predictions based on the historical data provided by the user.</span></span> <span data-ttu-id="def60-108">Si verificherà un incremento nella domanda di un prodotto specifico quest'anno?</span><span class="sxs-lookup"><span data-stu-id="def60-108">Will the demand for a specific product increase this year?</span></span> <span data-ttu-id="def60-109">È possibile prevedere le vendite dei prodotti per la stagione natalizia, per pianificare in modo efficace l'inventario?</span><span class="sxs-lookup"><span data-stu-id="def60-109">Can I predict my product sales for the Christmas season, so that I can effectively plan my inventory?</span></span> <span data-ttu-id="def60-110">I modelli di previsione sono progettati per rispondere a queste domande.</span><span class="sxs-lookup"><span data-stu-id="def60-110">Forecasting models are apt to address such questions.</span></span> <span data-ttu-id="def60-111">Partendo dai dati passati, questi modelli esaminano le tendenze nascoste e la stagionalità per prevedere le tendenze future.</span><span class="sxs-lookup"><span data-stu-id="def60-111">Given the past data, these models examine hidden trends and seasonality to predict future trends.</span></span>  

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> <span data-ttu-id="def60-112">Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio.</span><span class="sxs-lookup"><span data-stu-id="def60-112">This web service could be consumed by users – potentially through a mobile app, through a website, or even on a local computer, for example.</span></span> <span data-ttu-id="def60-113">Ma lo scopo del servizio Web è anche fornire un esempio di come è possibile utilizzare Azure Machine Learning per creare servizi Web in codice R.</span><span class="sxs-lookup"><span data-stu-id="def60-113">But the purpose of the web service is also to serve as an example of how Azure Machine Learning can be used to create web services on top of R code.</span></span> <span data-ttu-id="def60-114">Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web.</span><span class="sxs-lookup"><span data-stu-id="def60-114">With just a few lines of R code and clicks of a button within Azure Machine Learning Studio, an experiment can be created with R code and published as a web service.</span></span> <span data-ttu-id="def60-115">Il servizio Web può essere quindi pubblicato in Azure Marketplace e può essere usato da utenti e dispositivi in tutto il mondo, senza che l'autore del servizio Web debba configurare alcuna infrastruttura.</span><span class="sxs-lookup"><span data-stu-id="def60-115">The web service can then be published to the Azure Marketplace and consumed by users and devices across the world with no infrastructure setup by the author of the web service.</span></span>
> 
> 

## <a name="consumption-of-web-service"></a><span data-ttu-id="def60-116">Uso del servizio Web</span><span class="sxs-lookup"><span data-stu-id="def60-116">Consumption of web service</span></span>
<span data-ttu-id="def60-117">Questo servizio accetta quattro argomenti e calcola le previsioni ETS.</span><span class="sxs-lookup"><span data-stu-id="def60-117">This service accepts 4 arguments and calculates the ETS forecasts.</span></span>
<span data-ttu-id="def60-118">Gli argomenti di input sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="def60-118">The input arguments are:</span></span>

* <span data-ttu-id="def60-119">Frequency: indica la frequenza dei dati non elaborati (giornaliera/settimanale/mensile/trimestrale/annuale)</span><span class="sxs-lookup"><span data-stu-id="def60-119">Frequency - Indicates the frequency of the raw data (daily/weekly/monthly/quarterly/yearly).</span></span>
* <span data-ttu-id="def60-120">Horizon: intervallo di tempo futuro della previsione</span><span class="sxs-lookup"><span data-stu-id="def60-120">Horizon - Future forecast time-frame.</span></span>
* <span data-ttu-id="def60-121">Date: consente di immettere i nuovi dati relativi alle serie temporali per il tempo</span><span class="sxs-lookup"><span data-stu-id="def60-121">Date - Add in the new time series data for time.</span></span>
* <span data-ttu-id="def60-122">Value: consente di aggiungere i nuovi valori delle serie di dati.</span><span class="sxs-lookup"><span data-stu-id="def60-122">Value - Add in the new time series data values.</span></span>

<span data-ttu-id="def60-123">L'output del servizio è costituito dai valori calcolati della previsione.</span><span class="sxs-lookup"><span data-stu-id="def60-123">The output of the service is the calculated forecast values.</span></span>

<span data-ttu-id="def60-124">L'input può essere ad esempio il seguente:</span><span class="sxs-lookup"><span data-stu-id="def60-124">Sample input could be:</span></span> 

* <span data-ttu-id="def60-125">Frequency - 12</span><span class="sxs-lookup"><span data-stu-id="def60-125">Frequency - 12</span></span>
* <span data-ttu-id="def60-126">Horizon - 12</span><span class="sxs-lookup"><span data-stu-id="def60-126">Horizon - 12</span></span>
* <span data-ttu-id="def60-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span><span class="sxs-lookup"><span data-stu-id="def60-127">Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014</span></span>
* <span data-ttu-id="def60-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span><span class="sxs-lookup"><span data-stu-id="def60-128">Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509</span></span>

> <span data-ttu-id="def60-129">Questo servizio, come ospitato in Azure Marketplace, è un servizio OData ed è possibile utilizzare i metodi POST o GET per effettuare le chiamate.</span><span class="sxs-lookup"><span data-stu-id="def60-129">This service, as hosted on the Azure Marketplace, is an OData service; these may be called through POST or GET methods.</span></span> 
> 
> 

<span data-ttu-id="def60-130">Sono disponibili molte opzioni per l'uso del servizio in modalità automatica. Per un'app di esempio, vedere [qui](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx).</span><span class="sxs-lookup"><span data-stu-id="def60-130">There are multiple ways of consuming the service in an automated fashion (an example app is [here](http://microsoftazuremachinelearning.azurewebsites.net/etsForecasting.aspx)).</span></span>

### <a name="starting-c-code-for-web-service-consumption"></a><span data-ttu-id="def60-131">Codice C# iniziale per l'uso del servizio Web:</span><span class="sxs-lookup"><span data-stu-id="def60-131">Starting C# code for web service consumption:</span></span>
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



## <a name="creation-of-web-service"></a><span data-ttu-id="def60-132">Creazione del servizio Web</span><span class="sxs-lookup"><span data-stu-id="def60-132">Creation of web service</span></span>
> <span data-ttu-id="def60-133">Questo servizio Web è stato creato tramite Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="def60-133">This web service was created using Azure Machine Learning.</span></span> <span data-ttu-id="def60-134">Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml).</span><span class="sxs-lookup"><span data-stu-id="def60-134">For a free trial, as well as introductory videos on creating experiments and [publishing web services](machine-learning-publish-a-machine-learning-web-service.md), please see [azure.com/ml](http://azure.com/ml).</span></span> <span data-ttu-id="def60-135">La schermata seguente mostra un esperimento per la creazione del servizio Web e codice di esempio per ogni modulo incluso nell'esperimento.</span><span class="sxs-lookup"><span data-stu-id="def60-135">Below is a screenshot of the experiment that created the web service and example code for each of the modules within the experiment.</span></span>
> 
> 

<span data-ttu-id="def60-136">In Azure Machine Learning è stato creato un nuovo esperimento vuoto.</span><span class="sxs-lookup"><span data-stu-id="def60-136">From within Azure Machine Learning, a new blank experiment was created.</span></span> <span data-ttu-id="def60-137">Sono stati caricati dati di input di esempio con uno schema dati predefinito.</span><span class="sxs-lookup"><span data-stu-id="def60-137">Sample input data was uploaded with a predefined data schema.</span></span> <span data-ttu-id="def60-138">Un modulo [Execute R Script][execute-r-script] (Esegui script R) è collegato allo schema dati e genera i modelli di previsione ETS usando le funzioni 'ets' e 'forecast' di R.</span><span class="sxs-lookup"><span data-stu-id="def60-138">Linked to the data schema is an [Execute R Script][execute-r-script] module that generates the ETS forecasting model by using ‘ets’ and ‘forecast’ functions from R.</span></span> 

![Flusso dell'esperimento][2]

#### <a name="module-1"></a><span data-ttu-id="def60-140">Modulo 1:</span><span class="sxs-lookup"><span data-stu-id="def60-140">Module 1:</span></span>
    # Add in the CSV file with the data in the format shown below 
![Dati di esempio][3]    

#### <a name="module-2"></a><span data-ttu-id="def60-142">Modulo 2:</span><span class="sxs-lookup"><span data-stu-id="def60-142">Module 2:</span></span>
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


## <a name="limitations"></a><span data-ttu-id="def60-143">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="def60-143">Limitations</span></span>
<span data-ttu-id="def60-144">Questo è un esempio molto semplice di previsione ETS.</span><span class="sxs-lookup"><span data-stu-id="def60-144">This is a very simple example for ETS forecasting.</span></span> <span data-ttu-id="def60-145">Come si può notare nell'esempio di codice precedente, il rilevamento di errori non è implementato, il servizio presuppone che tutte le variabili siano valori continui/positivi e la frequenza deve essere un numero intero maggiore di 1. La lunghezza dei vettori di data e valore deve essere uguale.</span><span class="sxs-lookup"><span data-stu-id="def60-145">As can be seen from the example code above, no error catching is implemented, and the service assumes that all the variables are continuous/positive values and the frequency should be an integer greater than 1.</span></span> <span data-ttu-id="def60-146">La lunghezza dei vettori della data e il valore deve essere la stessa.</span><span class="sxs-lookup"><span data-stu-id="def60-146">The length of the date and value vectors should be the same.</span></span> <span data-ttu-id="def60-147">La variabile relativa alla data deve avere il formato 'mm/dd/yyyy'.</span><span class="sxs-lookup"><span data-stu-id="def60-147">The date variable should adhere to the format ‘mm/dd/yyyy’.</span></span>

## <a name="faq"></a><span data-ttu-id="def60-148">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="def60-148">FAQ</span></span>
<span data-ttu-id="def60-149">Per le domande frequenti relative all'uso del servizio Web o alla pubblicazione in Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).</span><span class="sxs-lookup"><span data-stu-id="def60-149">For frequently asked questions on consumption of the web service or publishing to the Azure Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img1.png
[2]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img2.png
[3]: ./media/machine-learning-r-csharp-forecasting-exponential-smoothing/ets-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

