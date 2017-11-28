---
title: aaaGet avviato con Azure Mobile Engagement per le app Web | Documenti Microsoft
description: Informazioni su come toouse Azure Mobile Engagement con analitica e notifiche push per le applicazioni Web.
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="6e054-103">Introduzione ad Azure Mobile Engagement per app Web</span><span class="sxs-lookup"><span data-stu-id="6e054-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="6e054-104">In questo argomento illustra come toouse Azure Mobile Engagement toounderstand sull'utilizzo delle App Web.</span><span class="sxs-lookup"><span data-stu-id="6e054-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="6e054-105">servizio di Azure Mobile Engagement di Hello verrà ritirata 2018 marzo ed è attualmente tooexisting disponibili solo i clienti.</span><span class="sxs-lookup"><span data-stu-id="6e054-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="6e054-106">Per altre informazioni, vedere [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="6e054-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="6e054-107">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="6e054-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="6e054-108">Visual Studio 2015 o un altro editor di propria scelta</span><span class="sxs-lookup"><span data-stu-id="6e054-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="6e054-109">Web SDK</span><span class="sxs-lookup"><span data-stu-id="6e054-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="6e054-110">Questo SDK Web è disponibile in anteprima solo supporta Analitica un determinato momento hello e non supporta ancora l'invio delle notifiche push browser o nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6e054-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="6e054-111">toocomplete questa esercitazione, è necessario disporre di un account di Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="6e054-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6e054-112">Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="6e054-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6e054-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="6e054-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="6e054-114">Configurare Mobile Engagement per l'app Web</span><span class="sxs-lookup"><span data-stu-id="6e054-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="6e054-115"><a id="connecting-app"></a>La connessione back-end Mobile Engagement toohello app</span><span class="sxs-lookup"><span data-stu-id="6e054-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="6e054-116">Questa esercitazione viene illustrato una "integrazione di base," hello set minimo richiesto toocollect dati.</span><span class="sxs-lookup"><span data-stu-id="6e054-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="6e054-117">Verrà creata un'app web di base con l'integrazione di Visual Studio toodemonstrate hello anche se è possibile seguire i passaggi di hello con qualsiasi applicazione web creata anche all'esterno di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e054-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="6e054-118">Creare una nuova app Web</span><span class="sxs-lookup"><span data-stu-id="6e054-118">Create a new Web App</span></span>
<span data-ttu-id="6e054-119">Hello passaggi seguenti si presuppongono hello utilizzo di Visual Studio 2015 se hello passaggi sono simili nelle versioni precedenti di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e054-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="6e054-120">Avviare Visual Studio e in hello **Home** selezionare **nuovo progetto**.</span><span class="sxs-lookup"><span data-stu-id="6e054-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="6e054-121">Nel menu a comparsa hello, selezionare **Web** -> **applicazione Web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="6e054-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="6e054-122">Compilare app hello **nome**, **percorso** e **Nome soluzione**, quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e054-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="6e054-123">In hello **selezionare un modello** popup, selezionare **vuoto** in **ASP.Net 4.5 modelli** e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="6e054-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="6e054-124">Ora è stata creata un nuovo progetto di App Web vuoto in cui integrare hello Azure Mobile Engagement Web SDK.</span><span class="sxs-lookup"><span data-stu-id="6e054-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="6e054-125">La connessione back-end Engagement tooMobile app</span><span class="sxs-lookup"><span data-stu-id="6e054-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="6e054-126">Creare una nuova cartella denominata **javascript** nella soluzione e aggiungere il file Web SDK JS hello **azure engagement.js** al suo interno.</span><span class="sxs-lookup"><span data-stu-id="6e054-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="6e054-127">Aggiungere un nuovo file denominato **main.js** in questa cartella di javascript con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="6e054-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="6e054-128">Verificare che stringa di connessione di tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="6e054-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="6e054-129">Questo `azureEngagement` oggetto sarà utilizzato tooaccess metodi Web SDK.</span><span class="sxs-lookup"><span data-stu-id="6e054-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio con file JS][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="6e054-131">Abilitare il monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="6e054-131">Enable real-time monitoring</span></span>
<span data-ttu-id="6e054-132">In ordine toostart l'invio dei dati e garantire che gli utenti di hello sono attivi, è necessario inviare back-end di almeno una attività toohello Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="6e054-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="6e054-133">Un'attività nel contesto di hello di un'app web è una pagina web.</span><span class="sxs-lookup"><span data-stu-id="6e054-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="6e054-134">Creare una nuova pagina denominata **home.html** nel soluzione e impostare come avvio hello pagina per l'app web.</span><span class="sxs-lookup"><span data-stu-id="6e054-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="6e054-135">Includere JavaScript di due hello che abbiamo aggiunto in precedenza in questa pagina aggiungendo hello seguente all'interno di tag body hello.</span><span class="sxs-lookup"><span data-stu-id="6e054-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="6e054-136">Aggiornare hello corpo tag toocall EngagementAgent `startActivity` (metodo)</span><span class="sxs-lookup"><span data-stu-id="6e054-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="6e054-137">Ecco come appare il file **home.html** .</span><span class="sxs-lookup"><span data-stu-id="6e054-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="6e054-138">Connettere l'app con monitoraggio in tempo reale</span><span class="sxs-lookup"><span data-stu-id="6e054-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="6e054-139">Estendere l'analisi</span><span class="sxs-lookup"><span data-stu-id="6e054-139">Extend analytics</span></span>
<span data-ttu-id="6e054-140">Di seguito sono attualmente disponibili con SDK Web che è possibile utilizzare per analitica tutti i metodi di hello:</span><span class="sxs-lookup"><span data-stu-id="6e054-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="6e054-141">Attività/Pagine Web:</span><span class="sxs-lookup"><span data-stu-id="6e054-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="6e054-142">Events</span><span class="sxs-lookup"><span data-stu-id="6e054-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="6e054-143">Errori</span><span class="sxs-lookup"><span data-stu-id="6e054-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="6e054-144">Processi</span><span class="sxs-lookup"><span data-stu-id="6e054-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

