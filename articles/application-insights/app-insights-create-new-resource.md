---
title: Creare una nuova risorsa di Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: 5f8814ee943424c1c278ab3732129d4459f83819
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-insights-resource"></a><span data-ttu-id="fec99-103">Creare una risorsa di Application Insights</span><span class="sxs-lookup"><span data-stu-id="fec99-103">Create an Application Insights resource</span></span>
<span data-ttu-id="fec99-104">Application Insights di Azure visualizza dati relativi all'applicazione in una *risorsa* di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fec99-104">Azure Application Insights displays data about your application in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="fec99-105">La creazione di una nuova risorsa fa dunque parte della [configurazione di Application Insights per monitorare una nuova applicazione][start].</span><span class="sxs-lookup"><span data-stu-id="fec99-105">Creating a new resource is therefore part of [setting up Application Insights to monitor a new application][start].</span></span> <span data-ttu-id="fec99-106">In molti casi, la creazione di una risorsa può essere eseguita automaticamente dall'IDE.</span><span class="sxs-lookup"><span data-stu-id="fec99-106">In many cases, creating a resource can be done automatically by the IDE.</span></span> <span data-ttu-id="fec99-107">In alcuni casi si crea tuttavia una risorsa manualmente, ad esempio per disporre di risorse separate per le compilazioni di sviluppo e produzione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fec99-107">But in some cases, you create a resource manually - for example, to have separate resources for development and production builds of your application.</span></span>

<span data-ttu-id="fec99-108">Dopo aver creato la risorsa, si ottiene la relativa chiave di strumentazione, che consente di configurare l'SDK nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fec99-108">After you have created the resource, you get its instrumentation key and use that to configure the SDK in the application.</span></span> <span data-ttu-id="fec99-109">La chiave della risorsa collega i dati di telemetria alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="fec99-109">The resource key links the telemetry to the resource.</span></span>

## <a name="sign-up-to-microsoft-azure"></a><span data-ttu-id="fec99-110">Iscriversi a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fec99-110">Sign up to Microsoft Azure</span></span>
<span data-ttu-id="fec99-111">Se non si ha ancora un [account Microsoft, è possibile ottenerne uno ora](http://live.com).</span><span class="sxs-lookup"><span data-stu-id="fec99-111">If you haven't got a [Microsoft account, get one now](http://live.com).</span></span> <span data-ttu-id="fec99-112">(se si usano servizi come Outlook.com, OneDrive, Windows Phone o XBox Live, si ha già un account Microsoft).</span><span class="sxs-lookup"><span data-stu-id="fec99-112">(If you use services like Outlook.com, OneDrive, Windows Phone, or XBox Live, you already have a Microsoft account.)</span></span>

<span data-ttu-id="fec99-113">È necessaria anche una sottoscrizione di [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="fec99-113">You also need a subscription to [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="fec99-114">Se il team o l'organizzazione ha una sottoscrizione di Azure, il proprietario potrà aggiungere l'utente alla sottoscrizione usando Windows Live ID.</span><span class="sxs-lookup"><span data-stu-id="fec99-114">If your team or organization has an Azure subscription, the owner can add you to it, using your Windows Live ID.</span></span> <span data-ttu-id="fec99-115">Si paga solo l'uso effettivo.</span><span class="sxs-lookup"><span data-stu-id="fec99-115">You're only charged for what you use.</span></span> <span data-ttu-id="fec99-116">Il piano Basic predefinito consente di accedere a un certo uso sperimentale gratuito.</span><span class="sxs-lookup"><span data-stu-id="fec99-116">The default basic plan allows for a certain amount of experimental use free of charge.</span></span>

<span data-ttu-id="fec99-117">Dopo aver ottenuto una sottoscrizione, accedere ad Application Insights all'indirizzo [http://portal.azure.com](https://portal.azure.com) usando il proprio Live ID.</span><span class="sxs-lookup"><span data-stu-id="fec99-117">When you've got access to a subscription, log in to Application Insights at [http://portal.azure.com](https://portal.azure.com), and use your Live ID to login.</span></span>

## <a name="create-an-application-insights-resource"></a><span data-ttu-id="fec99-118">Creare una risorsa Application Insights</span><span class="sxs-lookup"><span data-stu-id="fec99-118">Create an Application Insights resource</span></span>
<span data-ttu-id="fec99-119">In [portal.azure.com](https://portal.azure.com)aggiungere una nuova risorsa di Application Insights:</span><span class="sxs-lookup"><span data-stu-id="fec99-119">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Fare clic su Nuovo, Application Insights](./media/app-insights-create-new-resource/01-new.png)

* <span data-ttu-id="fec99-121">Il **tipo di applicazione** influisce sul contenuto del pannello Panoramica e sulle proprietà disponibili in [Esplora metriche][metrics].</span><span class="sxs-lookup"><span data-stu-id="fec99-121">**Application type** affects what you see on the overview blade and the properties available in [metric explorer][metrics].</span></span> <span data-ttu-id="fec99-122">Se il tipo dell'app non è visualizzato, scegliere Generale.</span><span class="sxs-lookup"><span data-stu-id="fec99-122">If you don't see your type of app, choose General.</span></span>
* <span data-ttu-id="fec99-123">**sottoscrizione** è il proprio account di pagamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="fec99-123">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="fec99-124">**gruppo di risorse** è utile per gestire le proprietà come il controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="fec99-124">**Resource group** is a convenience for managing properties like access control.</span></span> <span data-ttu-id="fec99-125">Se sono già state create altre risorse di Azure, è possibile inserire questa nuova risorsa nello stesso gruppo.</span><span class="sxs-lookup"><span data-stu-id="fec99-125">If you have already created other Azure resources, you can choose to put this new resource in the same group.</span></span>
* <span data-ttu-id="fec99-126">Il **percorso** è la posizione in cui vengono conservati i dati.</span><span class="sxs-lookup"><span data-stu-id="fec99-126">**Location** is where we keep your data.</span></span>
* <span data-ttu-id="fec99-127">**Aggiungi al dashboard** inserisce un riquadro di accesso rapido alla risorsa nella home page di Azure.</span><span class="sxs-lookup"><span data-stu-id="fec99-127">**Pin to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> <span data-ttu-id="fec99-128">Consigliato.</span><span class="sxs-lookup"><span data-stu-id="fec99-128">Recommended.</span></span>

<span data-ttu-id="fec99-129">Dopo aver creato l'app, verrà visualizzato un nuovo pannello</span><span class="sxs-lookup"><span data-stu-id="fec99-129">When your app has been created, a new blade opens.</span></span> <span data-ttu-id="fec99-130">che mostra i dati sulle prestazioni e l'utilizzo dell'app.</span><span class="sxs-lookup"><span data-stu-id="fec99-130">This blade is where you see performance and usage data about your app.</span></span> 

<span data-ttu-id="fec99-131">Per visualizzare di nuovo questo pannello al successivo accesso ad Azure, cercare il riquadro di avvio rapido dell'app nella schermata iniziale.</span><span class="sxs-lookup"><span data-stu-id="fec99-131">To get back to it next time you log in to Azure, look for your app's quick-start tile on the start board (home screen).</span></span> <span data-ttu-id="fec99-132">In alternativa, fare clic su Sfoglia per cercarlo.</span><span class="sxs-lookup"><span data-stu-id="fec99-132">Or click Browse to find it.</span></span>

## <a name="copy-the-instrumentation-key"></a><span data-ttu-id="fec99-133">Eseguire una copia della chiave di strumentazione</span><span class="sxs-lookup"><span data-stu-id="fec99-133">Copy the instrumentation key</span></span>
<span data-ttu-id="fec99-134">La chiave di strumentazione identifica la risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="fec99-134">The instrumentation key identifies the resource that you created.</span></span> <span data-ttu-id="fec99-135">È necessario fornirla all'SDK.</span><span class="sxs-lookup"><span data-stu-id="fec99-135">You need it to give to the SDK.</span></span>

![Fare clic su Informazioni di base, quindi sulla chiave di strumentazione e infine premere CTRL+C.](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-the-sdk-in-your-app"></a><span data-ttu-id="fec99-137">Installare l’SDK nell'app</span><span class="sxs-lookup"><span data-stu-id="fec99-137">Install the SDK in your app</span></span>
<span data-ttu-id="fec99-138">Installare Application Insights SDK nell'app.</span><span class="sxs-lookup"><span data-stu-id="fec99-138">Install the Application Insights SDK in your app.</span></span> <span data-ttu-id="fec99-139">Questo passaggio dipende dal tipo di applicazione.</span><span class="sxs-lookup"><span data-stu-id="fec99-139">This step depends heavily on the type of your application.</span></span> 

<span data-ttu-id="fec99-140">Usare la chiave di strumentazione per configurare l'[SDK installato nell'applicazione][start].</span><span class="sxs-lookup"><span data-stu-id="fec99-140">Use the instrumentation key to configure [the SDK that you install in your application][start].</span></span>

<span data-ttu-id="fec99-141">L'SDK include i moduli standard che inviano dati di telemetria senza che occorra scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="fec99-141">The SDK includes standard modules that send telemetry without you having to write any code.</span></span> <span data-ttu-id="fec99-142">Per rilevare le azioni degli utenti o diagnosticare i problemi in modo più dettagliato, [usare l'API][api] per inviare dati di telemetria personalizzati.</span><span class="sxs-lookup"><span data-stu-id="fec99-142">To track user actions or diagnose issues in more detail, [use the API][api] to send your own telemetry.</span></span>

## <span data-ttu-id="fec99-143"><a name="monitor"></a>Visualizzare i dati di telemetria</span><span class="sxs-lookup"><span data-stu-id="fec99-143"><a name="monitor"></a>See telemetry data</span></span>
<span data-ttu-id="fec99-144">Chiudere il pannello di avvio rapido per tornare al pannello dell'applicazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fec99-144">Close the quick start blade to return to your application blade in the Azure portal.</span></span>

<span data-ttu-id="fec99-145">Fare clic sul riquadro Cerca per vedere [Diagnostic Search][diagnostic] (Ricerca diagnostica), ovvero la finestra in cui vengono visualizzati i primi eventi.</span><span class="sxs-lookup"><span data-stu-id="fec99-145">Click the Search tile to see [Diagnostic Search][diagnostic], where the first events appear.</span></span> 

<span data-ttu-id="fec99-146">Se si prevedono più dati, fare clic su **Aggiorna** dopo pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="fec99-146">If you're expecting more data, click **Refresh** after a few seconds  .</span></span>

## <a name="creating-a-resource-automatically"></a><span data-ttu-id="fec99-147">Creazione automatica di una risorsa</span><span class="sxs-lookup"><span data-stu-id="fec99-147">Creating a resource automatically</span></span>
<span data-ttu-id="fec99-148">È possibile scrivere uno [script di PowerShell](app-insights-powershell.md) per creare automaticamente una risorsa.</span><span class="sxs-lookup"><span data-stu-id="fec99-148">You can write a [PowerShell script](app-insights-powershell.md) to create a resource automatically.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fec99-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fec99-149">Next steps</span></span>
* [<span data-ttu-id="fec99-150">Creare un dashboard</span><span class="sxs-lookup"><span data-stu-id="fec99-150">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="fec99-151">Ricerca diagnostica</span><span class="sxs-lookup"><span data-stu-id="fec99-151">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="fec99-152">Esplorare le metriche</span><span class="sxs-lookup"><span data-stu-id="fec99-152">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="fec99-153">Scrivere query di Analisi</span><span class="sxs-lookup"><span data-stu-id="fec99-153">Write Analytics queries</span></span>](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

