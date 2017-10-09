---
title: annotazioni aaaRelease per Application Insights | Documenti Microsoft
description: Aggiungi la distribuzione o compilazione marcatori grafici di Esplora metriche tooyour in Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Annotazioni sui grafici delle metriche in Application Insights
Le annotazioni nei grafici di [Esplora metriche](app-insights-metrics-explorer.md) indicano dove è stata distribuita una nuova build o un altro evento significativo Rendono semplice toosee se le modifiche aveva alcun effetto sulle prestazioni dell'applicazione. Possono essere creati automaticamente da hello [sistema di compilazione di Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). È inoltre possibile creare annotazioni tooflag qualsiasi evento che si desidera che da [la loro creazione da PowerShell](#create-annotations-from-powershell).

![Esempi di annotazioni con correlazione visibile con il tempo di risposta del server](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Annotazioni sulla versione con la build VSTS

Versione annotazioni sono una funzionalità di compilazione basato su cloud hello e versione del servizio di Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Installare l'estensione di annotazioni hello (una volta)
le annotazioni di toobe toocreate in grado di rilascio, è necessario tooinstall uno di hello disponibile in molte estensioni di Team Service hello Visual Studio Marketplace.

1. Accedi tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) progetto.
2. In Visual Studio Marketplace, [hello versione annotazioni estensione](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)e aggiungerlo account Team Services tooyour.

![Nell'angolo in alto a destra della pagina Web di Team Services aprire il marketplace. Scegliere Visual Studio Team Services, quindi nella sezione relativa a compilazione e rilascio scegliere Altre informazioni.](./media/app-insights-annotations/10.png)

È necessario solo toodo questo volta per l'account di Visual Studio Team Services. Le annotazioni sulla versione ora possono essere configurate per qualsiasi progetto nell'account. 

### <a name="configure-release-annotations"></a>Configurare annotazioni sulla versione

È necessario chiave tooget un'API distinta per ogni modello di rilascio di Visual Studio Team Services.

1. Accedi toohello [portale di Microsoft Azure](https://portal.azure.com) e aprire una risorsa di Application Insights hello che consente di monitorare l'applicazione. o [crearne una nuova](app-insights-overview.md), se necessario.
2. Aprire **Accesso all'API**, **ID di Application Insights**.
   
    ![In portal.azure.com, aprire la risorsa di Application Insights e scegliere Settings. Aprire API Access. Copiare l'ID applicazione hello](./media/app-insights-annotations/20.png)

4. In una finestra distinta del browser, aprire o creare modello di versione di hello che gestisce le distribuzioni da Visual Studio Team Services. 
   
    Aggiungere un'attività e selezionare l'attività di Application Insights versione annotazione hello dal menu di hello.
   
    Hello Incolla **Id applicazione** copiata dal Pannello di accesso all'API hello.
   
    ![In Visual Studio Team Services, aprire Release, selezionare una versione di rilascio e scegliere Edit. Fare clic su Add Task e scegliere l'annotazione sulla versione di Application Insights. Incollare hello ID applicazione Insights.](./media/app-insights-annotations/30.png)
4. Set hello **APIKey** variabile tooa campo `$(ApiKey)`.

5. Nella finestra Azure hello, creare una nuova chiave API e richiedere una copia.
   
    ![Nel Pannello di accesso all'API in hello Azure finestra hello, fare clic su Crea chiave API. Inserire un commento, controllare le annotazioni di scrittura e fare clic su Genera chiave. Copiare hello nuova chiave.](./media/app-insights-annotations/40.png)

6. Aprire una scheda di configurazione hello del modello di versione di hello.
   
    Creare una definizione di variabile per `ApiKey`.
   
    Incollare il toohello chiave API ApiKey definizione della variabile.
   
    ![Nella finestra di Team Services hello, selezionare la scheda di configurazione hello e fare clic su Aggiungi variabile. Impostare tooApiKey nome hello in valore hello, incollare la chiave di hello che appena generato e fare clic sull'icona di blocco hello.](./media/app-insights-annotations/50.png)
7. Infine, **salvare** hello definizione di versione.


## <a name="view-annotations"></a>Visualizzare le annotazioni
A questo punto, quando si usa hello versione modello toodeploy una nuova versione, un'annotazione verrà inviata tooApplication Insights. le annotazioni Hello verranno visualizzati nei grafici in Esplora metriche.

Fare clic su eventuali dettagli tooopen marcatore di annotazione sulla versione di hello, tra cui richiedente, ramo del controllo origine, definizione di versione, ambiente e altro ancora.

![Fare clic su un marcatore di annotazione della versione.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Creare annotazioni personalizzate da PowerShell
È anche possibile creare le annotazioni da qualsiasi processo desiderato, senza usare VS Team System. 


1. Creare una copia locale di hello [script di Powershell da GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Ottenere l'ID applicazione hello e creare una chiave API dal Pannello di accesso all'API hello.

3. Chiamare hello script simile al seguente:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Si tratta di script hello toomodify semplice, ad esempio toocreate annotazioni per hello precedente.

## <a name="next-steps"></a>Passaggi successivi

* [Creare elementi di lavoro](app-insights-diagnostic-search.md#create-work-item)
* [Automazione con PowerShell](app-insights-powershell.md)
