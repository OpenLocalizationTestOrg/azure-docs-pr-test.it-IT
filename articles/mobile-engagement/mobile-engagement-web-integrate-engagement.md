---
title: Integrazione di Azure Mobile Engagement SDK per Web | Microsoft Azure
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Web
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="a04a6-103">Integrare Azure Mobile Engagement in un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="a04a6-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a04a6-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a04a6-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="a04a6-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a04a6-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="a04a6-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a04a6-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="a04a6-107">Android</span><span class="sxs-lookup"><span data-stu-id="a04a6-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="a04a6-108">Le procedure contenute in questo articolo descrivono il modo più semplice per attivare le funzioni di analisi e monitoraggio di Azure Mobile Engagement in un'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="a04a6-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="a04a6-109">I passaggi seguenti sono utili per attivare la segnalazione dei log necessari per calcolare tutte le statistiche relative a utenti, sessioni, attività, arresti anomali del sistema e dati tecnici.</span><span class="sxs-lookup"><span data-stu-id="a04a6-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="a04a6-110">Per le statistiche dipendenti dall'applicazione, ad esempio eventi, errori e processi, è necessario attivare manualmente la segnalazione dei log tramite l'API di Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a04a6-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="a04a6-111">Per altre informazioni, leggere [Come usare l'API di Engagement in un'applicazione Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a04a6-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="a04a6-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="a04a6-112">Introduction</span></span>
<span data-ttu-id="a04a6-113">[Scaricare Azure Mobile Engagement SDK per Web](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="a04a6-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="a04a6-114">Il Mobile Engagement SDK per Web viene fornito come un singolo file JavaScript denominato azure-engagement.js, che deve essere incluso in ogni pagina del sito o dell'applicazione Web.</span><span class="sxs-lookup"><span data-stu-id="a04a6-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a04a6-115">Prima di eseguire questo script, è necessario eseguire uno script o un frammento di codice, scritto per configurare Mobile Engagement per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a04a6-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="a04a6-116">Compatibilità dei browser</span><span class="sxs-lookup"><span data-stu-id="a04a6-116">Browser compatibility</span></span>
<span data-ttu-id="a04a6-117">Il Mobile Engagement SDK per Web usa la codifica/decodifica JSON nativa e le richieste AJAX tra domini (basandosi sulla specifica W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="a04a6-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="a04a6-118">È compatibile con i seguenti browser:</span><span class="sxs-lookup"><span data-stu-id="a04a6-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="a04a6-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="a04a6-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="a04a6-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="a04a6-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="a04a6-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="a04a6-121">Firefox 3.5+</span></span>
* <span data-ttu-id="a04a6-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="a04a6-122">Chrome 4+</span></span>
* <span data-ttu-id="a04a6-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="a04a6-123">Safari 6+</span></span>
* <span data-ttu-id="a04a6-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="a04a6-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="a04a6-125">Configurare Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a04a6-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="a04a6-126">Scrivere uno script per creare un oggetto JavaScript `azureEngagement` globale simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="a04a6-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="a04a6-127">Poiché il sito potrebbe essere composto da più pagine, questo esempio presuppone che lo script sia incluso in ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="a04a6-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="a04a6-128">In questo esempio, l'oggetto JavaScript viene denominato `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="a04a6-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="a04a6-129">Il valore `connectionString` per l'applicazione viene visualizzato nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a04a6-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a04a6-130">`appVersionName` e `appVersionCode` sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="a04a6-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="a04a6-131">Si consiglia tuttavia di configurarli in modo che l'analisi possa elaborare le informazioni relative alla versione.</span><span class="sxs-lookup"><span data-stu-id="a04a6-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="a04a6-132">Includere script di Mobile Engagement nelle pagine</span><span class="sxs-lookup"><span data-stu-id="a04a6-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="a04a6-133">Aggiungere gli script di Mobile Engagement alle pagine in uno dei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a04a6-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="a04a6-134">Oppure:</span><span class="sxs-lookup"><span data-stu-id="a04a6-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="a04a6-135">Alias</span><span class="sxs-lookup"><span data-stu-id="a04a6-135">Alias</span></span>
<span data-ttu-id="a04a6-136">Dopo aver caricato lo script di Mobile Engagement SDK per Web, viene creato l'alias **engagement** per accedere alle API dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="a04a6-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="a04a6-137">Non è possibile usare l'alias per definire la configurazione dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="a04a6-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="a04a6-138">In questa documentazione l'alias viene usato come riferimento.</span><span class="sxs-lookup"><span data-stu-id="a04a6-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="a04a6-139">Si noti che se l'alias predefinito è in conflitto con un'altra variabile globale della pagina, sarà possibile ridefinirlo nella configurazione prima di caricare il Mobile Engagement SDK per Web nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="a04a6-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="a04a6-140">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="a04a6-140">Basic reporting</span></span>
<span data-ttu-id="a04a6-141">La segnalazione di base in Mobile Engagement riguarda le statistiche a livello di sessione, ad esempio le statistiche relative a utenti, sessioni, attività e arresti anomali del sistema.</span><span class="sxs-lookup"><span data-stu-id="a04a6-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="a04a6-142">Monitoraggio di una sessione</span><span class="sxs-lookup"><span data-stu-id="a04a6-142">Session tracking</span></span>
<span data-ttu-id="a04a6-143">Una sessione di Mobile Engagement è suddivisa in una sequenza di attività identificate da un nome.</span><span class="sxs-lookup"><span data-stu-id="a04a6-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="a04a6-144">In un sito Web classico è consigliabile dichiarare un'attività diversa in ogni pagina del sito.</span><span class="sxs-lookup"><span data-stu-id="a04a6-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="a04a6-145">Per una sito o un'applicazione Web in cui la pagina corrente non cambia mai, si desidera monitorare le attività su scala ridotta, ad esempio all'interno della pagina.</span><span class="sxs-lookup"><span data-stu-id="a04a6-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="a04a6-146">In entrambi i casi, per avviare o modificare l'attività utente corrente, chiamare la funzione `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="a04a6-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="a04a6-147">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a04a6-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="a04a6-148">Il server di Mobile Engagement termina automaticamente una sessione aperta entro 3 minuti dalla chiusura della pagina dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a04a6-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="a04a6-149">In alternativa, è possibile terminare una sessione manualmente chiamando `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="a04a6-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="a04a6-150">Ciò consente di impostare l'attività dell'utente corrente su "Idle".</span><span class="sxs-lookup"><span data-stu-id="a04a6-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="a04a6-151">La sessione terminerà dopo 10 secondi fino a quando una nuova chiamata a `engagement.agent.startActivity` riprenda la sessione.</span><span class="sxs-lookup"><span data-stu-id="a04a6-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="a04a6-152">È possibile configurare il ritardo di 10 secondi nell'oggetto engagement globale, come segue:</span><span class="sxs-lookup"><span data-stu-id="a04a6-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="a04a6-153">Non è possibile usare `engagement.agent.endActivity` nel callback `onunload` perché non è possibile eseguire chiamate AJAX in questa fase.</span><span class="sxs-lookup"><span data-stu-id="a04a6-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="a04a6-154">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="a04a6-154">Advanced reporting</span></span>
<span data-ttu-id="a04a6-155">Facoltativamente, per segnalare eventi, errori e processi specifici dell'applicazione, è necessario usare l'API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a04a6-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="a04a6-156">È possibile accedere alle API di Mobile Engagement tramite l'oggetto `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="a04a6-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="a04a6-157">È possibile accedere a tutte le funzionalità avanzate di Mobile Engagement nell'API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a04a6-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="a04a6-158">Per altre informazioni sull'API, leggere [Come usare l'API di Engagement in un'applicazione Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a04a6-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="a04a6-159">Personalizzare gli URL usati per le chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="a04a6-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="a04a6-160">È possibile personalizzare gli URL usati dal Mobile Engagement SDK per Web.</span><span class="sxs-lookup"><span data-stu-id="a04a6-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="a04a6-161">Ad esempio, per ridefinire l'URL di accesso (l'endpoint SDK per l'accesso), è possibile eseguire l'override della configurazione in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a04a6-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="a04a6-162">Se le funzioni URL restituiscono una stringa che inizia con `/`, `//`, `http://` o `https://`, lo schema predefinito non è usato.</span><span class="sxs-lookup"><span data-stu-id="a04a6-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="a04a6-163">Per impostazione predefinita, per tali URL viene usato lo schema `https://` .</span><span class="sxs-lookup"><span data-stu-id="a04a6-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="a04a6-164">Se si desidera personalizzare lo schema predefinito, eseguire l'override della configurazione in modo simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="a04a6-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
