---
title: aaaGet avviato con App Mobile di servizio App di Azure per le app xamarin | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di App per dispositivi mobili per lo sviluppo di xamarin. IOS.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 14428794-52ad-4b51-956c-deb296cafa34
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: syntaxc4
ms.openlocfilehash: 524c5ac4d8a29d7cb858f74132aad5d6e2201d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="cc30d-103">Creare un'app per Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="cc30d-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="cc30d-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cc30d-104">Overview</span></span>
<span data-ttu-id="cc30d-105">Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooa xamarin app per dispositivi mobili utilizzando un back-end dell'app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc30d-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="cc30d-106">Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.iOS *Todo list* che archivia i dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc30d-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="cc30d-107">Completato questa esercitazione è un prerequisito per tutte le altre esercitazioni di xamarin sulla funzionalità delle App per dispositivi mobili hello in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="cc30d-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc30d-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cc30d-108">Prerequisites</span></span>
<span data-ttu-id="cc30d-109">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="cc30d-109">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="cc30d-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cc30d-110">An active Azure account.</span></span> <span data-ttu-id="cc30d-111">Se non si dispone di un account, iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione.</span><span class="sxs-lookup"><span data-stu-id="cc30d-111">If you don't have an account, sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="cc30d-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cc30d-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cc30d-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="cc30d-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="cc30d-114">Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="cc30d-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="cc30d-115">Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="cc30d-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="cc30d-116">Vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="cc30d-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="cc30d-117">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="cc30d-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="cc30d-118">Seguire questi toocreate passaggi un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="cc30d-118">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-hello-server-project"></a><span data-ttu-id="cc30d-119">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="cc30d-119">Configure hello server project</span></span>
<span data-ttu-id="cc30d-120">È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="cc30d-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="cc30d-121">Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="cc30d-121">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

<span data-ttu-id="cc30d-122">Seguire i seguenti passaggi tooconfigure hello server progetto toouse hello back-end entrambi hello, Node.js o .NET.</span><span class="sxs-lookup"><span data-stu-id="cc30d-122">Follow hello following steps tooconfigure hello server project toouse either hello Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinios-app"></a><span data-ttu-id="cc30d-123">Scaricare ed eseguire app xamarin hello</span><span class="sxs-lookup"><span data-stu-id="cc30d-123">Download and run hello Xamarin.iOS app</span></span>
1. <span data-ttu-id="cc30d-124">Aprire hello [portale di Azure] in una finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="cc30d-124">Open hello [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="cc30d-125">Nel Pannello di hello impostazioni per l'App Mobile, fare clic su **iniziare** > **xamarin**.</span><span class="sxs-lookup"><span data-stu-id="cc30d-125">On hello settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="cc30d-126">Al passaggio 3 fare clic su **Crea una nuova app** , se l'opzione non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="cc30d-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="cc30d-127">Fare clic su hello **scaricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="cc30d-127">Next click hello **Download** button.</span></span>

      <span data-ttu-id="cc30d-128">Un'applicazione client che si connette back-end mobile tooyour viene scaricata.</span><span class="sxs-lookup"><span data-stu-id="cc30d-128">A client application that connects tooyour mobile backend is downloaded.</span></span> <span data-ttu-id="cc30d-129">Salvare il file di progetto in formato compresso hello nel computer locale e prendere nota del dove salvarla.</span><span class="sxs-lookup"><span data-stu-id="cc30d-129">Save hello compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="cc30d-130">Estrarre il progetto hello scaricato e aprirlo in Xamarin Studio (o Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="cc30d-130">Extract hello project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="cc30d-131">Premere progetto hello toobuild chiave F5 di hello e avviare l'applicazione hello nell'emulatore iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="cc30d-131">Press hello F5 key toobuild hello project and start hello app in hello iPhone emulator.</span></span>
5. <span data-ttu-id="cc30d-132">Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, quindi fare clic su hello  **+**  pulsante.</span><span class="sxs-lookup"><span data-stu-id="cc30d-132">In hello app, type meaningful text, such as *Learn Xamarin*, and then click hello **+** button.</span></span>

    ![][10]

    <span data-ttu-id="cc30d-133">Dati richiesta hello viene inseriti nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="cc30d-133">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="cc30d-134">Vengono restituiti gli elementi archiviati nella tabella hello dal back-end di hello app per dispositivi mobili e i dati vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="cc30d-134">Items stored in hello table are returned by hello mobile app backend, and the data is displayed in hello list.</span></span>

> [!NOTE]
> <span data-ttu-id="cc30d-135">È possibile esaminare il codice hello che accede a tooquery di back-end le app per dispositivi mobili e inserire i dati nel file c# QSTodoService.cs hello.</span><span class="sxs-lookup"><span data-stu-id="cc30d-135">You can review hello code that accesses your mobile app backend tooquery and insert data in hello QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="cc30d-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc30d-136">Next steps</span></span>
* [<span data-ttu-id="cc30d-137">Aggiungere app tooyour sincronizzazione Offline</span><span class="sxs-lookup"><span data-stu-id="cc30d-137">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="cc30d-138">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="cc30d-138">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="cc30d-139">Aggiungere app xamarin tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="cc30d-139">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="cc30d-140">Modalità di gestione client per App mobili di Azure hello toouse</span><span class="sxs-lookup"><span data-stu-id="cc30d-140">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Anchors. -->
[Getting started with mobile app backends]:#getting-started
[Create a new mobile app backend]:#create-new-service
[Next Steps]:#next-steps

<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-ios-get-started/xamarin-ios-quickstart.png
[8]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-vs.png
[9]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-xamarin-project-ios-xs.png
[10]: ./media/app-service-mobile-xamarin-ios-get-started/mobile-quickstart-startup-ios.png

<!-- URLs. -->
[portale di Azure]: https://portal.azure.com/
