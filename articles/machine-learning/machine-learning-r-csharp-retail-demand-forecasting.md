---
title: AAA(deprecated) Forecasting - ETS + STL - Azure | Documenti Microsoft
description: (Deprecato) Previsione - ETS + STL
services: machine-learning
documentationcenter: 
author: xueshanz
manager: jhubbard
editor: cgronlun
ms.assetid: 153eab4d-6293-45e1-9871-ec339e810dd9
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
ms.openlocfilehash: 550d423898d46564936fdcfbf05b7c88d2e292c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-forecasting---ets--stl"></a>(Deprecato) Previsione - ETS + STL

> [!NOTE]
> è stata ritirata Hello Microsoft DataMarket e questa API è stata deprecata. 
> 
> Sono disponibili molte esperimenti di esempio utile e API hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com). Per ulteriori informazioni sulla raccolta hello, vedere [condivisione e individuare le risorse in Cortana Intelligence Gallery hello](machine-learning-gallery-how-to-use-contribute-publish.md).

Questo [servizio web](https://datamarket.azure.com/dataset/aml_labs/demand_forecast) implementa stagionali tendenza scomposizione (STL) e anti-aliasing esponenziale (ETS) stime tooproduce modelli basato su dati cronologici di hello specificati dall'utente hello. Verrà hello richiesta per un aumento di prodotto specifico, quest'anno? È possibile prevedere le vendite del prodotto per hello stagione Natale, in modo che è possibile pianificare l'inventario in modo efficace? I modelli di previsione sono tooaddress apt tali domande. Dato hello oltre i dati, questi modelli esaminare tendenze nascoste e tendenze future toopredict di stagionalità. 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

> Questo servizio Web può essere utilizzato dagli utenti: potenzialmente tramite un'app mobile, un sito Web o anche in un computer locale, ad esempio. Ma scopo hello del servizio web hello anche tooserve come esempio di come Azure Machine Learning è possibile servizi web utilizzati toocreate su codice R. Con poche righe di codice R e la selezione di alcuni pulsanti in Azure Machine Learning Studio è possibile creare un esperimento con codice R e pubblicarlo come servizio Web. servizio web Hello può quindi essere pubblicata toohello Azure Marketplace e utilizzato da utenti e dispositivi attraverso HelloWorld con alcuna installazione dell'infrastruttura dall'autore hello del servizio web hello.  
> 
> 

## <a name="consumption-of-web-service"></a>Uso del servizio Web
Il servizio accetta 4 argomenti e calcola le previsioni hello.
gli argomenti di input Hello sono:

* Frequenza: indica la frequenza di hello di dati non elaborati hello (giornaliera/settimanale/mensile o trimestrale/annuali).
* Horizon: intervallo di tempo futuro della previsione
* Data - Aggiungi nella serie temporale nuovo hello dati per volta.
* Valore - aggiungere hello nuova serie dati i valori.

output di Hello del servizio hello è hello calcolati i valori di previsione.

L'input può essere ad esempio il seguente: 

* Frequency - 12
* Horizon - 12
* Date - 1/15/2012;2/15/2012;3/15/2012;4/15/2012;5/15/2012;6/15/2012;7/15/2012;8/15/2012;9/15/2012;10/15/2012;11/15/2012;12/15/2012; 1/15/2013;2/15/2013;3/15/2013;4/15/2013;5/15/2013;6/15/2013;7/15/2013;8/15/2013;9/15/2013;10/15/2013;11/15/2013;12/15/2013; 1/15/2014;2/15/2014;3/15/2014;4/15/2014;5/15/2014;6/15/2014;7/15/2014;8/15/2014;9/15/2014
* Value - 3.479;3.68;3.832;3.941;3.797;3.586;3.508;3.731;3.915;3.844;3.634;3.549;3.557;3.785;3.782;3.601;3.544;3.556;3.65;3.709;3.682;3.511; 3.429;3.51;3.523;3.525;3.626;3.695;3.711;3.711;3.693;3.571;3.509

> Questo servizio, ospitato in Azure Marketplace, hello è un servizio OData. questi può essere chiamati tramite i metodi POST o GET. 
> 
> 

Esistono diversi modi di utilizzo di servizio hello in modo automatico (è un'app di esempio [qui](http://microsoftazuremachinelearning.azurewebsites.net/StlEtsForecasting.aspx)).

### <a name="starting-c-code-for-web-service-consumption"></a>Codice C# iniziale per l'uso del servizio Web:
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
            var input = new Input() { frequency = TextBox1.Text, horizon = TextBox2.Text, date = TextBox3.Text, value = TextBox4.Text };         var json = JsonConvert.SerializeObject(input);
            var acitionUri = "PutAPIURLHere,e.g.https://api.datamarket.azure.com/..../v1/Score";
            var httpClient = new HttpClient();

            httpClient.DefaultRequestHeaders.Authorization = CreateBasicHeader("PutEmailAddressHere", "ChangeToAPIKey");
            httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));

            var response = httpClient.PostAsync(acitionUri, new StringContent(json));
            var result = response.Result.Content;
            var scoreResult = result.ReadAsStringAsync().Result;
    }


## <a name="creation-of-web-service"></a>Creazione del servizio Web
> Questo servizio Web è stato creato tramite Azure Machine Learning. Per una versione di prova gratuita e per video introduttivi sulla creazione di esperimenti e sulla [pubblicazione di servizi Web](machine-learning-publish-a-machine-learning-web-service.md), vedere [azure.com/ml](http://azure.com/ml). Di seguito è riportata una schermata dell'esperimento hello creato codice di esempio e servizio web hello per ciascuno dei moduli di hello all'interno di sperimentazione hello.
> 
> 

In Azure Machine Learning è stato creato un nuovo esperimento vuoto. Sono stati caricati dati di input di esempio con uno schema dati predefinito. Schema dati toohello collegato è un [Execute R Script] [ execute-r-script] modulo, che genera l'errore STL ed ETS i modelli di previsione utilizzando 'stl', 'ets,' e 'previsione' funge da R. 

### <a name="experiment-flow"></a>Flusso dell'esperimento
![Flusso dell'esperimento][2]

#### <a name="module-1"></a>Modulo 1:
    # Add in hello CSV file with hello data in hello format shown below 
![Dati di esempio][3]    

#### <a name="module-2"></a>Modulo 2:
    # Data input
    data <- maml.mapInputPort(1) # class: data.frame
    library(forecast)

    # Preprocessing
    colnames(data) <- c("frequency", "horizon", "dates", "values")
    dates <- strsplit(data$dates, ";")[[1]]
    values <- strsplit(data$values, ";")[[1]]

    dates <- as.Date(dates, format = '%m/%d/%Y')
    values <- as.numeric(values)

    # Fit a time series model
    train_ts<- ts(values, frequency=data$frequency)
    fit1 <- stl(train_ts,  s.window="periodic")
    train_model <- forecast(fit1, h = data$horizon, method = 'ets')
    plot(train_model)

    # Produce forcasting
    train_pred <- round(train_model$mean,2)
    data.forecast <- as.data.frame(t(train_pred))
    colnames(data.forecast) <- paste("Forecast", 1:data$horizon, sep="")

    # Data output
    maml.mapOutputPort("data.forecast");

## <a name="limitations"></a>Limitazioni
Questo è un esempio molto semplice di previsione ETS+STL. Come possono essere visualizzati dal codice di esempio hello precedente, non viene implementato alcun rilevamento di errori e servizio hello si presuppone che tutte le variabili di hello sono valori continui/positive e frequenza di hello deve essere un numero intero maggiore di 1. Hello lunghezza dei vettori di hello data e il valore deve essere hello stesso e lunghezza hello della serie temporale hello deve essere maggiore di 2 * frequenza. variabile di tipo date Hello deve rispettare toohello formato "mm/gg/aaaa'.

## <a name="faq"></a>domande frequenti
Per domande frequenti sull'utilizzo del servizio web hello o pubblicazione toohello Azure Marketplace, vedere [qui](machine-learning-marketplace-faq.md).

[1]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img1.png
[2]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img2.png
[3]: ./media/machine-learning-r-csharp-retail-demand-forecasting/retail-img3.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/

