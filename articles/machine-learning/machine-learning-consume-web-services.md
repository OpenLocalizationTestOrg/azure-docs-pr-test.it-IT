---
title: aaaHow tooconsume un servizio Web di Azure Machine Learning | Documenti Microsoft
description: "Dopo aver distribuito un servizio di machine learning, hello servizio Web RESTFul rese disponibile può essere utilizzato come servizio di richiesta-risposta in tempo reale o come un servizio esecuzione batch."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.author: garye
ms.openlocfilehash: 19095604169e5af1daed12c17ba66258233178bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconsume-an-azure-machine-learning-web-service"></a>Come un servizio Web di Azure Machine Learning tooconsume

Dopo aver distribuito un modello predittivo Azure Machine Learning come servizio Web, è possibile utilizzare un toosend API REST, dati e ottenere stime. È possibile inviare dati hello in tempo reale o in modalità batch.

È possibile trovare altre informazioni su come toocreate e distribuire un servizio Web di Machine Learning tramite Machine Learning Studio di seguito:

* Per un'esercitazione su come toocreate un esperimento di Machine Learning Studio, vedere [l'esperimento prima di creare](machine-learning-create-experiment.md).
* Per informazioni dettagliate su come toodeploy un servizio Web, vedere [distribuire un servizio Web di Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
* Per ulteriori informazioni su Machine Learning in generale, visitare hello [Centro documentazione di Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a>Panoramica
Con il servizio Web di Azure Machine Learning hello, un'applicazione esterna comunica con un modello del flusso di lavoro di Machine Learning assegnazione dei punteggi in tempo reale. Una chiamata al servizio Web di Machine Learning restituisce i risultati della stima tooan di applicazione esterna. una chiamata al servizio Web di Machine Learning toomake, passare una chiave API che viene creata quando si distribuisce una stima. servizio Web di Machine Learning Hello è basato su REST, una scelta di architettura comune per i progetti di programmazione web.

Azure Machine Learning dispone di due tipi di servizi:

* Il servizio di richiesta-risposta (RR) – una bassa latenza, servizio altamente scalabile che offre un'interfaccia toohello modelli senza stato creato e distribuito da hello Machine Learning Studio.
* Servizio esecuzione batch (BES). Un servizio asincrono che valuta un batch di record di dati.

Per altre informazioni sui servizi Web di Machine Learning, vedere [Distribuire un servizio Web di Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).

## <a name="get-an-azure-machine-learning-authorization-key"></a>Ottenere una chiave di autorizzazione Azure Machine Learning
Quando si distribuisce l'esperimento, le chiavi API vengono generate per hello servizio Web. È possibile recuperare le chiavi di hello da diverse posizioni.

### <a name="from-hello-microsoft-azure-machine-learning-web-services-portal"></a>Dal portale di servizi Web di Microsoft Azure Machine Learning: hello
Accedi toohello [servizi Web di Microsoft Azure Machine Learning](https://services.azureml.net) portale.

chiave di hello API tooretrieve per un servizio Web di nuova Machine Learning:

1. Nel portale di servizi Web di Azure Machine Learning hello, fare clic su **servizi Web** menu in alto hello.
2. Fare clic su servizio Web hello per cui si desidera chiave hello tooretrieve.
3. Scegliere dal menu superiore hello **consumare**.
4. Copiare e salvare hello **chiave primaria**.

chiave di hello API tooretrieve per un servizio Web di classico Machine Learning:

1. Nel portale di servizi Web di Azure Machine Learning hello, fare clic su **servizi Web classico** menu in alto hello.
2. Fare clic su servizio Web hello con cui si lavora.
3. Fare clic su endpoint hello per cui si desidera chiave hello tooretrieve.
4. Scegliere dal menu superiore hello **consumare**.
5. Copiare e salvare hello **chiave primaria**.

### <a name="classic-web-service"></a>Servizio Web classico
 È inoltre possibile recuperare una chiave per un servizio Web classico da Machine Learning Studio o hello portale di Azure classico.

#### <a name="machine-learning-studio"></a>Machine Learning Studio
1. In Machine Learning Studio, fare clic su **servizi WEB** a sinistra di hello.
2. Fare clic su un servizio Web. Hello **chiave API** in hello **DASHBOARD** scheda.

#### <a name="azure-classic-portal"></a>portale di Azure classico
1. Fare clic su **MACHINE LEARNING** a sinistra di hello.
2. Fare clic su area di lavoro hello in cui si trova il servizio Web.
3. Fare clic su **WEB SERVICES**.
4. Fare clic su un servizio Web.
5. Fare clic su un endpoint. Hello "Chiave API" non è attivo hello in basso a destra.

## <a id="connect"></a>La connessione del servizio Web di Machine Learning tooa
È possibile connettersi tooa servizio Web di Machine Learning utilizzando qualsiasi linguaggio di programmazione che supporta la risposta e richiesta HTTP. È possibile visualizzare gli esempi in C#, Python e R da una pagina della guida del servizio Web di Machine Learning.

**Guida alle API di Machine Learning** Una Guida per l'API di Machine Learning viene creata quando si distribuisce un servizio Web. Vedere [Procedura dettagliata di Azure Machine Learning - Distribuire il servizio Web](machine-learning-walkthrough-5-publish-web-service.md).
Guida di Machine Learning API Hello contiene dettagli su una stima del servizio Web.

1. Fare clic su servizio Web hello con cui si lavora.
2. Fare clic su endpoint hello per cui si desidera tooview hello pagina della Guida di API.
3. Scegliere dal menu superiore hello **consumare**.
4. Fare clic su **pagina della Guida API** in hello richiesta-risposta o gli endpoint di esecuzione del Batch.

**la Guida di Machine Learning API tooview per un servizio Web nuovo**

Nel portale dei servizi Web Azure Machine Learning hello:

1. Fare clic su **servizi WEB** nel menu superiore hello.
2. Fare clic su servizio Web hello per cui si desidera chiave hello tooretrieve.

Fare clic su **consumare** tooget hello URI per la richiesta Reposonse hello e servizi per l'esecuzione Batch e codice di esempio in c#, R e Python.

Fare clic su **Swagger API** tooget Swagger documentazione di base per hello API chiamata da hello specificato gli URI.

### <a name="c-sample"></a>Esempio C#
tooconnect tooa servizio Web di Machine Learning, utilizzare un **HttpClient** passando ScoreData. ScoreData contiene un FeatureVector, un vettore di n-dimensionale delle funzionalità numerico che rappresenta hello ScoreData. Servizio di Machine Learning toohello l'autenticazione con una chiave API.

tooconnect tooa servizio Web di Machine Learning, hello **webapi** è necessario installare il pacchetto NuGet.

**Installare il Nuget Microsoft.AspNet.WebApi.Client in Visual Studio**

1. Pubblicare il set di dati di hello Download da UCI: 2 per adulti classe dataset servizio Web.
2. Fare clic su **Strumenti** > **Gestione pacchetti NuGet** > **Console di Gestione pacchetti**.
3. Scegliere **Install-Package Microsoft.AspNet.WebApi.Client**.

**Nell'esempio di codice hello toorun**

1. Pubblicare "esempio 1: scaricare set di dati da UCI: adulto 2 classe dataset" esperimento, parte della raccolta di Machine Learning esempio hello.
2. Assegnare apiKey con chiave hello da un servizio Web. Vedere la sezione precedente **Ottenere una chiave di autorizzazione di Azure Machine Learning** .
3. Assegnare serviceUri con hello URI della richiesta.

### <a name="python-sample"></a>Esempio Python
tooconnect tooa servizio Web di Machine Learning, utilizzare hello **urllib2** libreria passando ScoreData. ScoreData contiene un FeatureVector, un vettore di n-dimensionale delle funzionalità numerico che rappresenta hello ScoreData. Servizio di Machine Learning toohello l'autenticazione con una chiave API.

**Nell'esempio di codice hello toorun**

1. Distribuire "esempio 1: scaricare set di dati da UCI: adulto 2 classe dataset" esperimento, parte della raccolta di Machine Learning esempio hello.
2. Assegnare apiKey con chiave hello da un servizio Web. Vedere hello **ottenere una chiave di autorizzazione di Azure Machine Learning** sezione parte iniziale di hello di questo articolo.
3. Assegnare serviceUri con hello URI della richiesta.

