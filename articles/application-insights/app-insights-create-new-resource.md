---
title: una nuova risorsa di Azure Application Insights aaaCreate | Documenti Microsoft
description: Impostare manualmente il monitoraggio di Application Insights per una nuova applicazione live.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Creare una risorsa di Application Insights
Application Insights di Azure visualizza dati relativi all'applicazione in una *risorsa* di Microsoft Azure. Creazione di una nuova risorsa, pertanto fa parte di [configurazione di Application Insights toomonitor una nuova applicazione][start]. In molti casi, la creazione di una risorsa può essere eseguita automaticamente da hello IDE. Ma in alcuni casi, crei manualmente una risorsa, ad esempio, in cui le compilazioni toohave risorse diverse per lo sviluppo e produzione dell'applicazione.

Dopo aver creato la risorsa hello, ottenere la chiave di strumentazione, utilizzare tale hello tooconfigure SDK in un'applicazione hello. i collegamenti alla chiavi risorsa Hello hello risorsa toohello telemetria.

## <a name="sign-up-toomicrosoft-azure"></a>Effettuare l'iscrizione tooMicrosoft Azure
Se non si ha ancora un [account Microsoft, è possibile ottenerne uno ora](http://live.com). (se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, si ha già un account Microsoft).

È inoltre necessaria una sottoscrizione troppo[Microsoft Azure](http://azure.com). Se il team o l'organizzazione dispone di una sottoscrizione di Azure, il proprietario di hello può aggiungere l'utente tooit, utilizzando il Windows Live ID. Si paga solo l'uso effettivo. piano di base predefinito Hello consente una certa quantità di utilizzo sperimentale gratuitamente.

Quando si ha accesso tooa sottoscrizione, l'accesso Insights tooApplication in [http://portal.azure.com](https://portal.azure.com)e utilizzare il toologin Live ID.

## <a name="create-an-application-insights-resource"></a>Creare una risorsa Application Insights
In hello [portal.azure.com](https://portal.azure.com), aggiungere una risorsa di Application Insights:

![Fare clic su Nuovo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Tipo di applicazione** influisce su ciò che viene visualizzato nel pannello della panoramica hello e le proprietà di hello disponibili in [Esplora metrica][metrics]. Se il tipo dell'app non è visualizzato, scegliere Generale.
* **sottoscrizione** è il proprio account di pagamento in Azure.
* **gruppo di risorse** è utile per gestire le proprietà come il controllo di accesso. Se altre risorse di Azure è già stato creato, è possibile scegliere tooput questa nuova risorsa in hello nello stesso gruppo.
* Il **percorso** è la posizione in cui vengono conservati i dati.
* **PIN toodashboard** assegna un riquadro di accesso rapido per la risorsa per la Home page di Azure. Consigliato.

Dopo aver creato l'app, verrà visualizzato un nuovo pannello che mostra i dati sulle prestazioni e l'utilizzo dell'app. 

tooit indietro tooget successivo accesso in tooAzure, cercare il riquadro avvio rapido dell'applicazione su hello avviare Lavagna (schermata iniziale). Oppure fare clic su Sfoglia toofind è.

## <a name="copy-hello-instrumentation-key"></a>Copiare la chiave di strumentazione hello
chiave di strumentazione Hello identifica risorse hello creato. È necessario toogive toohello SDK.

![Essentials fare clic su hello chiave di strumentazione, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Installare SDK hello nell'app
Installare Application Insights SDK hello nell'app. Questo passaggio dipende fortemente dal tipo di hello dell'applicazione. 

Utilizzare hello strumentazione chiave tooconfigure [SDK installato in un'applicazione hello][start].

Hello SDK include i moduli standard che inviano dati di telemetria senza che sia necessario toowrite qualsiasi codice. azioni dell'utente tootrack o diagnosi dei problemi in modo più dettagliato, [utilizzare API hello] [ api] toosend propri dati di telemetria.

## <a name="monitor"></a>Visualizzare i dati di telemetria
Chiude hello rapido avviare blade di blade tooreturn tooyour applicazione hello portale di Azure.

Fare clic su hello ricerca riquadro toosee [ricerca diagnostica][diagnostic], dove vengono visualizzati gli eventi prima di hello. 

Se si prevedono più dati, fare clic su **Aggiorna** dopo pochi secondi.

## <a name="creating-a-resource-automatically"></a>Creazione automatica di una risorsa
È possibile scrivere un [script di PowerShell](app-insights-powershell.md) toocreate una risorsa automaticamente.

## <a name="next-steps"></a>Passaggi successivi
* [Creare un dashboard](app-insights-dashboards.md)
* [Ricerca diagnostica](app-insights-diagnostic-search.md)
* [Esplorare le metriche](app-insights-metrics-explorer.md)
* [Scrivere query di Analisi](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

