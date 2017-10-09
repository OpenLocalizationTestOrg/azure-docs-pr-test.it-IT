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
# <a name="annotations-on-metric-charts-in-application-insights"></a><span data-ttu-id="77f9e-103">Annotazioni sui grafici delle metriche in Application Insights</span><span class="sxs-lookup"><span data-stu-id="77f9e-103">Annotations on metric charts in Application Insights</span></span>
<span data-ttu-id="77f9e-104">Le annotazioni nei grafici di [Esplora metriche](app-insights-metrics-explorer.md) indicano dove è stata distribuita una nuova build o un altro evento significativo</span><span class="sxs-lookup"><span data-stu-id="77f9e-104">Annotations on [Metrics Explorer](app-insights-metrics-explorer.md) charts show where you deployed a new build, or other significant event.</span></span> <span data-ttu-id="77f9e-105">Rendono semplice toosee se le modifiche aveva alcun effetto sulle prestazioni dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="77f9e-105">They make it easy toosee whether your changes had any effect on your application's performance.</span></span> <span data-ttu-id="77f9e-106">Possono essere creati automaticamente da hello [sistema di compilazione di Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span><span class="sxs-lookup"><span data-stu-id="77f9e-106">They can be automatically created by hello [Visual Studio Team Services build system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs).</span></span> <span data-ttu-id="77f9e-107">È inoltre possibile creare annotazioni tooflag qualsiasi evento che si desidera che da [la loro creazione da PowerShell](#create-annotations-from-powershell).</span><span class="sxs-lookup"><span data-stu-id="77f9e-107">You can also create annotations tooflag any event you like by [creating them from PowerShell](#create-annotations-from-powershell).</span></span>

![Esempi di annotazioni con correlazione visibile con il tempo di risposta del server](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a><span data-ttu-id="77f9e-109">Annotazioni sulla versione con la build VSTS</span><span class="sxs-lookup"><span data-stu-id="77f9e-109">Release annotations with VSTS build</span></span>

<span data-ttu-id="77f9e-110">Versione annotazioni sono una funzionalità di compilazione basato su cloud hello e versione del servizio di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="77f9e-110">Release annotations are a feature of hello cloud-based build and release service of Visual Studio Team Services.</span></span> 

### <a name="install-hello-annotations-extension-one-time"></a><span data-ttu-id="77f9e-111">Installare l'estensione di annotazioni hello (una volta)</span><span class="sxs-lookup"><span data-stu-id="77f9e-111">Install hello Annotations extension (one time)</span></span>
<span data-ttu-id="77f9e-112">le annotazioni di toobe toocreate in grado di rilascio, è necessario tooinstall uno di hello disponibile in molte estensioni di Team Service hello Visual Studio Marketplace.</span><span class="sxs-lookup"><span data-stu-id="77f9e-112">toobe able toocreate release annotations, you'll need tooinstall one of hello many Team Service extensions available in hello Visual Studio Marketplace.</span></span>

1. <span data-ttu-id="77f9e-113">Accedi tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) progetto.</span><span class="sxs-lookup"><span data-stu-id="77f9e-113">Sign in tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.</span></span>
2. <span data-ttu-id="77f9e-114">In Visual Studio Marketplace, [hello versione annotazioni estensione](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)e aggiungerlo account Team Services tooyour.</span><span class="sxs-lookup"><span data-stu-id="77f9e-114">In Visual Studio Marketplace, [get hello Release Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), and add it tooyour Team Services account.</span></span>

![Nell'angolo in alto a destra della pagina Web di Team Services aprire il marketplace.](./media/app-insights-annotations/10.png)

<span data-ttu-id="77f9e-117">È necessario solo toodo questo volta per l'account di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="77f9e-117">You only need toodo this once for your Visual Studio Team Services account.</span></span> <span data-ttu-id="77f9e-118">Le annotazioni sulla versione ora possono essere configurate per qualsiasi progetto nell'account.</span><span class="sxs-lookup"><span data-stu-id="77f9e-118">Release annotations can now be configured for any project in your account.</span></span> 

### <a name="configure-release-annotations"></a><span data-ttu-id="77f9e-119">Configurare annotazioni sulla versione</span><span class="sxs-lookup"><span data-stu-id="77f9e-119">Configure release annotations</span></span>

<span data-ttu-id="77f9e-120">È necessario chiave tooget un'API distinta per ogni modello di rilascio di Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="77f9e-120">You need tooget a separate API key for each VSTS release template.</span></span>

1. <span data-ttu-id="77f9e-121">Accedi toohello [portale di Microsoft Azure](https://portal.azure.com) e aprire una risorsa di Application Insights hello che consente di monitorare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="77f9e-121">Sign in toohello [Microsoft Azure Portal](https://portal.azure.com) and open hello Application Insights resource that monitors your application.</span></span> <span data-ttu-id="77f9e-122">o [crearne una nuova](app-insights-overview.md), se necessario.</span><span class="sxs-lookup"><span data-stu-id="77f9e-122">(Or [create one now](app-insights-overview.md), if you haven't done so yet.)</span></span>
2. <span data-ttu-id="77f9e-123">Aprire **Accesso all'API**, **ID di Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="77f9e-123">Open **API Access**,  **Application Insights Id**.</span></span>
   
    ![In portal.azure.com, aprire la risorsa di Application Insights e scegliere Settings.](./media/app-insights-annotations/20.png)

4. <span data-ttu-id="77f9e-127">In una finestra distinta del browser, aprire o creare modello di versione di hello che gestisce le distribuzioni da Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="77f9e-127">In a separate browser window, open (or create) hello release template that manages your deployments from Visual Studio Team Services.</span></span> 
   
    <span data-ttu-id="77f9e-128">Aggiungere un'attività e selezionare l'attività di Application Insights versione annotazione hello dal menu di hello.</span><span class="sxs-lookup"><span data-stu-id="77f9e-128">Add a task, and select hello Application Insights Release Annotation task from hello menu.</span></span>
   
    <span data-ttu-id="77f9e-129">Hello Incolla **Id applicazione** copiata dal Pannello di accesso all'API hello.</span><span class="sxs-lookup"><span data-stu-id="77f9e-129">Paste hello **Application Id** that you copied from hello API Access blade.</span></span>
   
    ![In Visual Studio Team Services, aprire Release, selezionare una versione di rilascio e scegliere Edit.](./media/app-insights-annotations/30.png)
4. <span data-ttu-id="77f9e-133">Set hello **APIKey** variabile tooa campo `$(ApiKey)`.</span><span class="sxs-lookup"><span data-stu-id="77f9e-133">Set hello **APIKey** field tooa variable `$(ApiKey)`.</span></span>

5. <span data-ttu-id="77f9e-134">Nella finestra Azure hello, creare una nuova chiave API e richiedere una copia.</span><span class="sxs-lookup"><span data-stu-id="77f9e-134">Back in hello Azure window, create a new API Key and take a copy of it.</span></span>
   
    ![Nel Pannello di accesso all'API in hello Azure finestra hello, fare clic su Crea chiave API.](./media/app-insights-annotations/40.png)

6. <span data-ttu-id="77f9e-138">Aprire una scheda di configurazione hello del modello di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="77f9e-138">Open hello Configuration tab of hello release template.</span></span>
   
    <span data-ttu-id="77f9e-139">Creare una definizione di variabile per `ApiKey`.</span><span class="sxs-lookup"><span data-stu-id="77f9e-139">Create a variable definition for `ApiKey`.</span></span>
   
    <span data-ttu-id="77f9e-140">Incollare il toohello chiave API ApiKey definizione della variabile.</span><span class="sxs-lookup"><span data-stu-id="77f9e-140">Paste your API key toohello ApiKey variable definition.</span></span>
   
    ![Nella finestra di Team Services hello, selezionare la scheda di configurazione hello e fare clic su Aggiungi variabile.](./media/app-insights-annotations/50.png)
7. <span data-ttu-id="77f9e-143">Infine, **salvare** hello definizione di versione.</span><span class="sxs-lookup"><span data-stu-id="77f9e-143">Finally, **Save** hello release definition.</span></span>


## <a name="view-annotations"></a><span data-ttu-id="77f9e-144">Visualizzare le annotazioni</span><span class="sxs-lookup"><span data-stu-id="77f9e-144">View annotations</span></span>
<span data-ttu-id="77f9e-145">A questo punto, quando si usa hello versione modello toodeploy una nuova versione, un'annotazione verrà inviata tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="77f9e-145">Now, whenever you use hello release template toodeploy a new release, an annotation will be sent tooApplication Insights.</span></span> <span data-ttu-id="77f9e-146">le annotazioni Hello verranno visualizzati nei grafici in Esplora metriche.</span><span class="sxs-lookup"><span data-stu-id="77f9e-146">hello annotations will appear on charts in Metrics Explorer.</span></span>

<span data-ttu-id="77f9e-147">Fare clic su eventuali dettagli tooopen marcatore di annotazione sulla versione di hello, tra cui richiedente, ramo del controllo origine, definizione di versione, ambiente e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="77f9e-147">Click on any annotation marker tooopen details about hello release, including requestor, source control branch, release definition, environment, and more.</span></span>

![Fare clic su un marcatore di annotazione della versione.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a><span data-ttu-id="77f9e-149">Creare annotazioni personalizzate da PowerShell</span><span class="sxs-lookup"><span data-stu-id="77f9e-149">Create custom annotations from PowerShell</span></span>
<span data-ttu-id="77f9e-150">È anche possibile creare le annotazioni da qualsiasi processo desiderato, senza usare VS Team System.</span><span class="sxs-lookup"><span data-stu-id="77f9e-150">You can also create annotations from any process you like (without using VS Team System).</span></span> 


1. <span data-ttu-id="77f9e-151">Creare una copia locale di hello [script di Powershell da GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span><span class="sxs-lookup"><span data-stu-id="77f9e-151">Make a local copy of hello [Powershell script from GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).</span></span>

2. <span data-ttu-id="77f9e-152">Ottenere l'ID applicazione hello e creare una chiave API dal Pannello di accesso all'API hello.</span><span class="sxs-lookup"><span data-stu-id="77f9e-152">Get hello Application ID and create an API key from hello API Access blade.</span></span>

3. <span data-ttu-id="77f9e-153">Chiamare hello script simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="77f9e-153">Call hello script like this:</span></span>

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

<span data-ttu-id="77f9e-154">Si tratta di script hello toomodify semplice, ad esempio toocreate annotazioni per hello precedente.</span><span class="sxs-lookup"><span data-stu-id="77f9e-154">It's easy toomodify hello script, for example toocreate annotations for hello past.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77f9e-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77f9e-155">Next steps</span></span>

* [<span data-ttu-id="77f9e-156">Creare elementi di lavoro</span><span class="sxs-lookup"><span data-stu-id="77f9e-156">Create work items</span></span>](app-insights-diagnostic-search.md#create-work-item)
* [<span data-ttu-id="77f9e-157">Automazione con PowerShell</span><span class="sxs-lookup"><span data-stu-id="77f9e-157">Automation with PowerShell</span></span>](app-insights-powershell.md)
