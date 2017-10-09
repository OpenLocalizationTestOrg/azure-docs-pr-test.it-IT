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
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="7f60a-103">Creare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f60a-103">Create an Application Insights resource</span></span>
<span data-ttu-id="7f60a-104">Application Insights di Azure visualizza dati relativi all'applicazione in una *risorsa* di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7f60a-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="7f60a-105">Creazione di una nuova risorsa, pertanto fa parte di [configurazione di Application Insights toomonitor una nuova applicazione][start].</span><span class="sxs-lookup"><span data-stu-id="7f60a-105">Creating a new resource is therefore part of [setting up Application Insights toomonitor a new application][start].</span></span> <span data-ttu-id="7f60a-106">In molti casi, la creazione di una risorsa può essere eseguita automaticamente da hello IDE.</span><span class="sxs-lookup"><span data-stu-id="7f60a-106">In many cases, creating a resource can be done automatically by hello IDE.</span></span> <span data-ttu-id="7f60a-107">Ma in alcuni casi, crei manualmente una risorsa, ad esempio, in cui le compilazioni toohave risorse diverse per lo sviluppo e produzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f60a-107">But in some cases, you create a resource manually - for example, toohave separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="7f60a-108">Dopo aver creato la risorsa hello, ottenere la chiave di strumentazione, utilizzare tale hello tooconfigure SDK in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="7f60a-108">After you have created hello resource, you get its instrumentation key and use that tooconfigure hello SDK in hello application.</span></span> <span data-ttu-id="7f60a-109">i collegamenti alla chiavi risorsa Hello hello risorsa toohello telemetria.</span><span class="sxs-lookup"><span data-stu-id="7f60a-109">hello resource key links hello telemetry toohello resource.</span></span>

## <a name="sign-up-toomicrosoft-azure"></a><span data-ttu-id="7f60a-110">Effettuare l'iscrizione tooMicrosoft Azure</span><span class="sxs-lookup"><span data-stu-id="7f60a-110">Sign up tooMicrosoft Azure</span></span>
<span data-ttu-id="7f60a-111">Se non si ha ancora un [account Microsoft, è possibile ottenerne uno ora](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="7f60a-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="7f60a-112">(se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, si ha già un account Microsoft).</span><span class="sxs-lookup"><span data-stu-id="7f60a-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="7f60a-113">È inoltre necessaria una sottoscrizione troppo[Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="7f60a-113">You also need a subscription too[Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="7f60a-114">Se il team o l'organizzazione dispone di una sottoscrizione di Azure, il proprietario di hello può aggiungere l'utente tooit, utilizzando il Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="7f60a-114">If your team or organization has an Azure subscription, hello owner can add you tooit, using your Windows Live ID.</span></span> <span data-ttu-id="7f60a-115">Si paga solo l'uso effettivo.</span><span class="sxs-lookup"><span data-stu-id="7f60a-115">You're only charged for what you use.</span></span> <span data-ttu-id="7f60a-116">piano di base predefinito Hello consente una certa quantità di utilizzo sperimentale gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="7f60a-116">hello default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="7f60a-117">Quando si ha accesso tooa sottoscrizione, l'accesso Insights tooApplication in [http://portal.azure.com](https://portal.azure.com)e utilizzare il toologin Live ID.</span><span class="sxs-lookup"><span data-stu-id="7f60a-117">When you've got access tooa subscription, log in tooApplication Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID toologin.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="7f60a-118">Creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="7f60a-118">Create an Application Insights resource</span></span>
<span data-ttu-id="7f60a-119">In hello [portal.azure.com](https://portal.azure.com), aggiungere una risorsa di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="7f60a-119">In hello [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="7f60a-121">**Tipo di applicazione** influisce su ciò che viene visualizzato nel pannello della panoramica hello e le proprietà di hello disponibili in [Esplora metrica][metrics].</span><span class="sxs-lookup"><span data-stu-id="7f60a-121">**Application type** affects what you see on hello overview blade and hello properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="7f60a-122">Se il tipo dell'app non è visualizzato, scegliere Generale.</span><span class="sxs-lookup"><span data-stu-id="7f60a-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="7f60a-123">**sottoscrizione** è il proprio account di pagamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="7f60a-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="7f60a-124">**gruppo di risorse** è utile per gestire le proprietà come il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="7f60a-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="7f60a-125">Se altre risorse di Azure è già stato creato, è possibile scegliere tooput questa nuova risorsa in hello nello stesso gruppo.</span><span class="sxs-lookup"><span data-stu-id="7f60a-125">If you have already created other Azure resources, you can choose tooput this new resource in hello same group.</span></span>
* <span data-ttu-id="7f60a-126">Il **percorso** è la posizione in cui vengono conservati i dati.</span><span class="sxs-lookup"><span data-stu-id="7f60a-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="7f60a-127">**PIN toodashboard** assegna un riquadro di accesso rapido per la risorsa per la Home page di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f60a-127">**Pin toodashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="7f60a-128">Consigliato.</span><span class="sxs-lookup"><span data-stu-id="7f60a-128">Recommended.</span></span>

<span data-ttu-id="7f60a-129">Dopo aver creato l'app, verrà visualizzato un nuovo pannello</span><span class="sxs-lookup"><span data-stu-id="7f60a-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="7f60a-130">che mostra i dati sulle prestazioni e l'utilizzo dell'app.</span><span class="sxs-lookup"><span data-stu-id="7f60a-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="7f60a-131">tooit indietro tooget successivo accesso in tooAzure, cercare il riquadro avvio rapido dell'applicazione su hello avviare Lavagna (schermata iniziale).</span><span class="sxs-lookup"><span data-stu-id="7f60a-131">tooget back tooit next time you log in tooAzure, look for your app's quick-start tile on hello start board (home screen).</span></span> <span data-ttu-id="7f60a-132">Oppure fare clic su Sfoglia toofind è.</span><span class="sxs-lookup"><span data-stu-id="7f60a-132">Or click Browse toofind it.</span></span>

## <a name="copy-hello-instrumentation-key"></a><span data-ttu-id="7f60a-133">Copiare la chiave di strumentazione hello</span><span class="sxs-lookup"><span data-stu-id="7f60a-133">Copy hello instrumentation key</span></span>
<span data-ttu-id="7f60a-134">chiave di strumentazione Hello identifica risorse hello creato.</span><span class="sxs-lookup"><span data-stu-id="7f60a-134">hello instrumentation key identifies hello resource that you created.</span></span> <span data-ttu-id="7f60a-135">È necessario toogive toohello SDK.</span><span class="sxs-lookup"><span data-stu-id="7f60a-135">You need it toogive toohello SDK.</span></span>

![Essentials fare clic su hello chiave di strumentazione, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a><span data-ttu-id="7f60a-137">Installare SDK hello nell'app</span><span class="sxs-lookup"><span data-stu-id="7f60a-137">Install hello SDK in your app</span></span>
<span data-ttu-id="7f60a-138">Installare Application Insights SDK hello nell'app.</span><span class="sxs-lookup"><span data-stu-id="7f60a-138">Install hello Application Insights SDK in your app.</span></span> <span data-ttu-id="7f60a-139">Questo passaggio dipende fortemente dal tipo di hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7f60a-139">This step depends heavily on hello type of your application.</span></span> 

<span data-ttu-id="7f60a-140">Utilizzare hello strumentazione chiave tooconfigure [SDK installato in un'applicazione hello][start].</span><span class="sxs-lookup"><span data-stu-id="7f60a-140">Use hello instrumentation key tooconfigure [hello SDK that you install in your application][start].</span></span>

<span data-ttu-id="7f60a-141">Hello SDK include i moduli standard che inviano dati di telemetria senza che sia necessario toowrite qualsiasi codice.</span><span class="sxs-lookup"><span data-stu-id="7f60a-141">hello SDK includes standard modules that send telemetry without you having toowrite any code.</span></span> <span data-ttu-id="7f60a-142">azioni dell'utente tootrack o diagnosi dei problemi in modo più dettagliato, [utilizzare API hello] [ api] toosend propri dati di telemetria.</span><span class="sxs-lookup"><span data-stu-id="7f60a-142">tootrack user actions or diagnose issues in more detail, [use hello API][api] toosend your own telemetry.</span></span>

## <span data-ttu-id="7f60a-143"><a name="monitor"></a>Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="7f60a-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="7f60a-144">Chiude hello rapido avviare blade di blade tooreturn tooyour applicazione hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f60a-144">Close hello quick start blade tooreturn tooyour application blade in hello Azure portal.</span></span>

<span data-ttu-id="7f60a-145">Fare clic su hello ricerca riquadro toosee [ricerca diagnostica][diagnostic], dove vengono visualizzati gli eventi prima di hello.</span><span class="sxs-lookup"><span data-stu-id="7f60a-145">Click hello Search tile toosee [Diagnostic Search][diagnostic], where hello first events appear.</span></span> 

<span data-ttu-id="7f60a-146">Se si prevedono più dati, fare clic su **Aggiorna** dopo pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="7f60a-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="7f60a-147">Creazione automatica di una risorsa</span><span class="sxs-lookup"><span data-stu-id="7f60a-147">Creating a resource automatically</span></span>
<span data-ttu-id="7f60a-148">È possibile scrivere un [script di PowerShell](app-insights-powershell.md) toocreate una risorsa automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7f60a-148">You can write a [PowerShell script](app-insights-powershell.md) toocreate a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f60a-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f60a-149">Next steps</span></span>
* [<span data-ttu-id="7f60a-150">Creare un dashboard</span><span class="sxs-lookup"><span data-stu-id="7f60a-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="7f60a-151">Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="7f60a-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="7f60a-152">Esplorare le metriche</span><span class="sxs-lookup"><span data-stu-id="7f60a-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="7f60a-153">Scrivere query di Analisi</span><span class="sxs-lookup"><span data-stu-id="7f60a-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

