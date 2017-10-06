---
title: integrazione di Mobile Engagement Web SDK aaaAzure | Documenti Microsoft
description: "Hello procedure per hello Azure Mobile Engagement Web SDK e gli aggiornamenti più recenti"
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
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="77051-103">Integrare Azure Mobile Engagement in un'applicazione Web</span><span class="sxs-lookup"><span data-stu-id="77051-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="77051-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="77051-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="77051-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="77051-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="77051-106">iOS</span><span class="sxs-lookup"><span data-stu-id="77051-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="77051-107">Android</span><span class="sxs-lookup"><span data-stu-id="77051-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="77051-108">procedure Hello in questo articolo vengono descritti analitica hello più semplice modo tooactivate hello e funzioni in Azure Mobile Engagement nell'applicazione web di monitoraggio.</span><span class="sxs-lookup"><span data-stu-id="77051-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="77051-109">Seguire hello passaggi tooactivate hello report del log che sono necessari toocompute tutte le statistiche sugli utenti, sessioni, attività, arresti anomali del sistema e technicals.</span><span class="sxs-lookup"><span data-stu-id="77051-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="77051-110">Per le statistiche di dipendenti dall'applicazione, ad esempio eventi, errori e i processi, è necessario attivare manualmente i report di log utilizzando l'API di Azure Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="77051-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="77051-111">Per ulteriori informazioni, vedere [come toouse hello avanzate tag API in un'applicazione web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="77051-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="77051-112">Introduzione</span><span class="sxs-lookup"><span data-stu-id="77051-112">Introduction</span></span>
<span data-ttu-id="77051-113">[Scaricare hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="77051-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="77051-114">Hello Web di Mobile Engagement SDK viene fornito come un singolo file JavaScript, azure-engagement.js, aver tooinclude in ogni pagina dell'applicazione web o del sito.</span><span class="sxs-lookup"><span data-stu-id="77051-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77051-115">Prima di eseguire questo script, è necessario eseguire uno script o scrivere tooconfigure Mobile Engagement per l'applicazione di frammento di codice.</span><span class="sxs-lookup"><span data-stu-id="77051-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="77051-116">Compatibilità dei browser</span><span class="sxs-lookup"><span data-stu-id="77051-116">Browser compatibility</span></span>
<span data-ttu-id="77051-117">Hello Mobile Engagement Web SDK Usa JSON native di codifica e decodifica inoltre le richieste AJAX toocross dominio (basarsi sulla specifica W3C CORS hello).</span><span class="sxs-lookup"><span data-stu-id="77051-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="77051-118">È compatibile con hello seguenti browser:</span><span class="sxs-lookup"><span data-stu-id="77051-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="77051-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="77051-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="77051-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="77051-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="77051-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="77051-121">Firefox 3.5+</span></span>
* <span data-ttu-id="77051-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="77051-122">Chrome 4+</span></span>
* <span data-ttu-id="77051-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="77051-123">Safari 6+</span></span>
* <span data-ttu-id="77051-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="77051-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="77051-125">Configurare Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="77051-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="77051-126">Scrivere uno script che crea globale `azureEngagement` oggetto JavaScript, come in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="77051-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="77051-127">Poiché il sito potrebbe essere composto da più pagine, questo esempio presuppone che lo script sia incluso in ogni pagina.</span><span class="sxs-lookup"><span data-stu-id="77051-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="77051-128">In questo esempio è denominato oggetto JavaScript hello `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="77051-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="77051-129">Hello `connectionString` valore per l'applicazione viene visualizzata nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="77051-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="77051-130">`appVersionName` e `appVersionCode` sono facoltativi.</span><span class="sxs-lookup"><span data-stu-id="77051-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="77051-131">Si consiglia tuttavia di configurarli in modo che l'analisi possa elaborare le informazioni relative alla versione.</span><span class="sxs-lookup"><span data-stu-id="77051-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="77051-132">Includere script di Mobile Engagement nelle pagine</span><span class="sxs-lookup"><span data-stu-id="77051-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="77051-133">Aggiungere pagine tooyour gli script di Mobile Engagement in uno dei seguenti modi hello:</span><span class="sxs-lookup"><span data-stu-id="77051-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="77051-134">Oppure:</span><span class="sxs-lookup"><span data-stu-id="77051-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="77051-135">Alias</span><span class="sxs-lookup"><span data-stu-id="77051-135">Alias</span></span>
<span data-ttu-id="77051-136">Dopo il caricamento di uno script di Mobile Engagement Web SDK hello crea hello **engagement** tooaccess alias hello API SDK.</span><span class="sxs-lookup"><span data-stu-id="77051-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="77051-137">Non è possibile utilizzare questa configurazione di alias toodefine hello SDK.</span><span class="sxs-lookup"><span data-stu-id="77051-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="77051-138">In questa documentazione l'alias viene usato come riferimento.</span><span class="sxs-lookup"><span data-stu-id="77051-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="77051-139">Si noti che se l'alias predefinito hello in conflitto con un'altra variabile globale dalla pagina, è possibile ridefinirla nella configurazione di hello come indicato di seguito prima di caricare hello Mobile Engagement Web SDK:</span><span class="sxs-lookup"><span data-stu-id="77051-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="77051-140">Segnalazione di base</span><span class="sxs-lookup"><span data-stu-id="77051-140">Basic reporting</span></span>
<span data-ttu-id="77051-141">La segnalazione di base in Mobile Engagement riguarda le statistiche a livello di sessione, ad esempio le statistiche relative a utenti, sessioni, attività e arresti anomali del sistema.</span><span class="sxs-lookup"><span data-stu-id="77051-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="77051-142">Monitoraggio di una sessione</span><span class="sxs-lookup"><span data-stu-id="77051-142">Session tracking</span></span>
<span data-ttu-id="77051-143">Una sessione di Mobile Engagement è suddivisa in una sequenza di attività identificate da un nome.</span><span class="sxs-lookup"><span data-stu-id="77051-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="77051-144">In un sito Web classico è consigliabile dichiarare un'attività diversa in ogni pagina del sito.</span><span class="sxs-lookup"><span data-stu-id="77051-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="77051-145">Per una sito o applicazione web in cui hello pagina corrente non cambia mai, le attività di hello tootrack su scala ridotta, potrebbe essere, ad esempio all'interno di pagina hello.</span><span class="sxs-lookup"><span data-stu-id="77051-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="77051-146">Ovvero, toostart o modifica hello attività corrente dell'utente chiamata hello `engagement.agent.startActivity` (funzione).</span><span class="sxs-lookup"><span data-stu-id="77051-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="77051-147">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77051-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="77051-148">server di Mobile Engagement Hello termina automaticamente una sessione aperta all'interno di tre minuti dopo la chiusura di una pagina dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="77051-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="77051-149">In alternativa, è possibile terminare una sessione manualmente chiamando `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="77051-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="77051-150">Consente di impostare too'Idle attività utente corrente di hello.'</span><span class="sxs-lookup"><span data-stu-id="77051-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="77051-151">sessione Hello terminerà dopo 10 secondi, a meno che una nuova chiamata`engagement.agent.startActivity` riprende una sessione di hello.</span><span class="sxs-lookup"><span data-stu-id="77051-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="77051-152">È possibile configurare il ritardo di 10 secondi hello nell'oggetto globale engagement hello, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="77051-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="77051-153">Non è possibile utilizzare `engagement.agent.endActivity` in hello `onunload` callback perché in questa fase non è possibile apportare le chiamate AJAX.</span><span class="sxs-lookup"><span data-stu-id="77051-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="77051-154">Segnalazione avanzata</span><span class="sxs-lookup"><span data-stu-id="77051-154">Advanced reporting</span></span>
<span data-ttu-id="77051-155">Facoltativamente, se si desidera processi, errori ed eventi di tooreport specifiche dell'applicazione, è necessario toouse hello API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77051-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="77051-156">Si accede hello API di Mobile Engagement tramite hello `engagement.agent` oggetto.</span><span class="sxs-lookup"><span data-stu-id="77051-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="77051-157">È possibile accedere a tutti i hello avanzate funzionalità di Mobile Engagement in hello API di Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="77051-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="77051-158">API Hello è descritta in dettaglio nell'articolo hello [come toouse hello avanzate tag API in un'applicazione web di Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="77051-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="77051-159">Personalizzare gli URL hello utilizzati per le chiamate AJAX</span><span class="sxs-lookup"><span data-stu-id="77051-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="77051-160">È possibile personalizzare gli URL che hello che usa Web di Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="77051-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="77051-161">Ad esempio, tooredefine hello log URL (hello SDK dell'endpoint per la registrazione), è possibile eseguire l'override di configurazione hello come segue:</span><span class="sxs-lookup"><span data-stu-id="77051-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="77051-162">Se le funzioni dell'URL restituiranno una stringa che inizia con `/`, `//`, `http://`, o `https://`, non viene utilizzato lo schema predefinito di hello.</span><span class="sxs-lookup"><span data-stu-id="77051-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="77051-163">Per impostazione predefinita, hello `https://` schema viene utilizzato per tali URL.</span><span class="sxs-lookup"><span data-stu-id="77051-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="77051-164">Se si desidera schema predefinito di hello toocustomize, eseguire l'override di configurazione hello, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="77051-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
