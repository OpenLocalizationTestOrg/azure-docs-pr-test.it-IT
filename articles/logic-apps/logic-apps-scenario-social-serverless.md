---
title: aaaScenario - creare un dashboard di insights di clienti con Azure senza | Documenti Microsoft
description: "Un esempio di come è possibile compilare un cliente toomanage dashboard commenti e suggerimenti, dati di social networking e altro ancora con le applicazioni di logica di Azure e le funzioni di Azure."
keywords: 
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/29/2017
ms.author: jehollan
ms.openlocfilehash: db175e895e37aa795a9c34bf4d65566bf68f8c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-real-time-customer-insights-dashboard-with-azure-logic-apps-and-azure-functions"></a>Creare un dashboard Customer Insights in tempo reale con App per la logica di Azure e Funzioni di Azure

Gli strumenti di Azure senza forniscono potenti funzionalità tooquickly compilare e ospitare applicazioni in cloud hello, senza dovere toothink sull'infrastruttura.  In questo scenario, verrà creato un tootrigger dashboard ai suggerimenti dei clienti, analizzare i commenti e suggerimenti con machine learning e pubblicare informazioni dettagliate di un'origine come Power BI o Azure Data Lake.

## <a name="overview-of-hello-scenario-and-tools-used"></a>Panoramica dello scenario di hello e strumenti utilizzati

In ordine tooimplement questa soluzione, verranno utilizzate componenti chiave di hello due delle App senza server in Azure: [Azure funzioni](https://azure.microsoft.com/services/functions/) e [Azure logica app](https://azure.microsoft.com/services/logic-apps/).

Logica App è un motore del flusso di lavoro senza server nel cloud hello.  Fornisce l'orchestrazione tra i componenti server e si connette anche tooover 100 servizi e le API.  Per questo scenario, si creerà un tootrigger app logica ai suggerimenti dei clienti.  Alcuni dei connettori hello che consentono di reazione feedback toocustomer includono Outlook.com, Office 365, Monkey sondaggio, Twitter e una richiesta HTTP [da un web form](https://blogs.msdn.microsoft.com/logicapps/2017/01/30/calling-a-logic-app-from-an-html-form/).  Per hello del flusso di lavoro riportato di seguito, si esegue il monitoraggio un hashtag su Twitter.

Le funzioni forniscono senza calcolo nel cloud hello.  In questo scenario, si utilizzerà le funzioni di Azure tooflag TWEET dai clienti in base a una serie di parole chiave predefinite.

può essere l'intera soluzione Hello [compilati in Visual Studio](logic-apps-deploy-from-vs.md) e [distribuito come parte di un modello di risorsa](logic-apps-create-deploy-template.md).  È inoltre presente procedura dettagliata video dello scenario hello [su Channel 9](http://aka.ms/logicappsdemo).

## <a name="build-hello-logic-app-tootrigger-on-customer-data"></a>Compilare hello logica app tootrigger sui dati dei clienti

Dopo aver [creazione di un'app di logica](logic-apps-create-a-logic-app.md) in Visual Studio o hello portale di Azure:

1. Aggiungere un trigger per **On New Tweets** (All'arrivo di nuovi tweet) da Twitter
2. Configurare hello trigger toolisten tootweets su una parola chiave o hashtag.

   > [!NOTE]
   > proprietà ricorrenza Hello trigger hello determinerà frequenza dei controlli per i nuovi elementi per i trigger basate sul polling hello logica app

   ![Esempio di trigger di Twitter][1]

Questa app ora verrà attivata all'arrivo di tutti i nuovi tweet.  È quindi possibile richiedere che i dati tweet e comprendere più sentiment hello espresso.  A tale scopo si usa hello [servizio cognitivi Azure](https://azure.microsoft.com/services/cognitive-services/) sentiment toodetect del testo.

1. Fare clic su **Nuovo passaggio**
1. Selezionare o cercare hello **testo Analitica** connettore
1. Seleziona hello **rilevare Sentiment** operazione
1. Se richiesto, fornire una chiave di servizi cognitivi valida per il servizio Analitica testo hello
1. Aggiungere hello **Tweet testo** come hello tooanalyze di testo.

Ora che abbiamo dati tweet hello e approfondimenti su tweet hello, un numero di altri connettori può essere rilevante:
* Power BI - aggiungere righe tooStreaming set di dati: TWEET visualizzazione in tempo reale in un dashboard di Power BI.
* Azure Data Lake - accodare il file: aggiungere cliente dati tooan Azure Data Lake dataset tooinclude nei processi analitica.
* SQL. Aggiunta di righe: archivia i dati in un database per recuperarli in seguito.
* Slack. Invio messaggio: avvisa un canale di Slack all'arrivo di commenti negativi che richiedono l'esecuzione di azioni.

Una funzione di Azure può essere anche usato toodo più personalizzato di calcolo sui dati hello.

## <a name="enriching-hello-data-with-an-azure-function"></a>Arricchimento dei dati di hello con una funzione di Azure

Prima di poter creare una funzione, è necessario toohave un'app di funzione nella nostra sottoscrizione di Azure.  Informazioni dettagliate sulla creazione di una funzione di Azure nel portale di hello possono [sono disponibili qui](../azure-functions/functions-create-first-azure-function-azure-portal.md)

Per toobe una funzione chiamata direttamente da un'app di logica, è necessario toohave HTTP attivare associazione.  È consigliabile utilizzare hello **HttpTrigger** modello.

In questo scenario, il corpo della richiesta di hello Azure funzione hello sarebbe testo tweet hello.  Nel codice della funzione hello, definire semplicemente la logica nel Se testo tweet hello contiene una parola chiave o una frase.  funzione Hello stessa poteva essere tenuta semplice o complesso come necessario per lo scenario di hello.

Alla fine di hello della funzione hello, restituiscono semplicemente un'app di logica di risposta toohello con alcuni dati.  Può trattarsi di un semplice valore booleano (ad esempio, `containsKeyword`) o di un oggetto complesso.

![Passaggio della funzione di Azure configurata][2]

> [!TIP]
> Quando si accede a una risposta complessa da una funzione in un'app di logica, azione hello analizzare JSON.

Dopo aver salvata la funzione hello, può essere aggiunto in hello logica app creato in precedenza.  Nell'app logica hello:

1. Fare clic su tooadd un **nuovo passaggio**
1. Seleziona hello **Azure funzioni** connettore
1. Selezionare toochoose una funzione esistente e passare toohello funzione creata
1. Inviare in hello **testo Tweet** per hello **corpo della richiesta**

## <a name="running-and-monitoring-hello-solution"></a>In esecuzione e hello soluzione di monitoraggio

Uno dei vantaggi di hello di orchestrazioni senza server nell'App per la logica di creazione è debug avanzato hello e funzionalità di monitoraggio.  Qualsiasi esecuzione (correnti o cronologici) può essere visualizzati all'interno di Visual Studio, hello portale di Azure o tramite l'API REST hello e SDK.

Uno dei hello tootest di modi più semplice un'app logica utilizza hello **eseguire** pulsante nella finestra di progettazione hello.  Fare clic su **eseguire** continuerà trigger hello toopoll ogni 5 secondi fino a quando non viene rilevato un evento e fornire una visualizzazione in tempo reale durante l'avanzamento hello eseguire.

Cronologia di esecuzione precedente può essere visualizzati nel pannello della panoramica hello hello portale di Azure o utilizzando Visual Studio Cloud Explorer hello.

## <a name="creating-a-deployment-template-for-automated-deployments"></a>Creazione di un modello per le distribuzioni automatizzate

Dopo aver sviluppata una soluzione, possono essere acquisito e distribuito tramite tooany di modello area di Azure nel mondo hello una distribuzione di Azure.  Tale operazione è utile non solo per modificare i parametri delle diverse versioni di questo flusso di lavoro, ma anche per integrare la soluzione in una pipeline di compilazione e rilascio.  Per informazioni dettagliate sulla creazione di un modello di distribuzione, vedere [questo articolo](logic-apps-create-deploy-template.md).

Funzioni di Azure possono anche essere incorporate nel modello di distribuzione hello - dell'intera soluzione hello con tutte le dipendenze può essere gestiti come un singolo modello.  Un esempio di un modello di distribuzione di funzione è reperibile in hello [repository di modelli di avvio rapido di Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-function-app-create-dynamic).

## <a name="next-steps"></a>Passaggi successivi

* [Vedere altri esempi e scenari per App per la logica di Azure](logic-apps-examples-and-scenarios.md)
* [Guardare un video con la procedura dettagliata sulla creazione di questa soluzione end-to-end](http://aka.ms/logicappsdemo)
* [Informazioni su come toohandle e catch eccezioni all'interno di un'app di logica](logic-apps-exception-handling.md)

<!-- Image References -->
[1]: ./media/logic-apps-scenario-social-serverless/twitter.png
[2]: ./media/logic-apps-scenario-social-serverless/function.png