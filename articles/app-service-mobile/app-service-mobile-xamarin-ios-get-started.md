---
title: Introduzione alle app per dispositivi mobili del servizio app di Azure per app Xamarin.iOS | Documentazione Microsoft
description: Seguire questa esercitazione per iniziare a usare le app per dispositivi mobili per lo sviluppo per Xamarin iOS.
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
ms.openlocfilehash: 8dc965df2cd45366970effb29f246b0045a94717
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinios-app"></a><span data-ttu-id="1dfe6-103">Creare un'app per Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="1dfe6-103">Create a Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="1dfe6-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1dfe6-104">Overview</span></span>
<span data-ttu-id="1dfe6-105">Questa esercitazione illustra come aggiungere un servizio back-end basato sul cloud a un'app per dispositivi mobili Xamarin.iOS mediante un back-end per app per dispositivi mobili di Azure.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.iOS mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="1dfe6-106">Verranno creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.iOS *Todo list* che archivia i dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-106">You create both a new mobile app backend and a simple *Todo list* Xamarin.iOS app that stores app data in Azure.</span></span>

<span data-ttu-id="1dfe6-107">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni Xamarin.iOS relative all'uso della funzionalità di Azure App Service relativa alle app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-107">Completing this tutorial is a prerequisite for all other Xamarin.iOS tutorials about using the Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1dfe6-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="1dfe6-108">Prerequisites</span></span>
<span data-ttu-id="1dfe6-109">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1dfe6-109">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="1dfe6-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-110">An active Azure account.</span></span> <span data-ttu-id="1dfe6-111">Se non è disponibile un account, iscriversi per accedere a una versione di valutazione di Azure e ottenere un massimo di 10 app per dispositivi mobili gratuite che potranno essere usate anche dopo il termine del periodo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-111">If you don't have an account, sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="1dfe6-112">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1dfe6-112">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1dfe6-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="1dfe6-114">Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="1dfe6-114">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>
* <span data-ttu-id="1dfe6-115">Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="1dfe6-116">Vedere [Configurazione e installazione per Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="1dfe6-116">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="1dfe6-117">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="1dfe6-117">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="1dfe6-118">Seguire questa procedura per creare un back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-118">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

## <a name="configure-the-server-project"></a><span data-ttu-id="1dfe6-119">Configurare il progetto server</span><span class="sxs-lookup"><span data-stu-id="1dfe6-119">Configure the server project</span></span>
<span data-ttu-id="1dfe6-120">È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-120">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="1dfe6-121">Scaricare quindi un progetto server per un semplice back-end "todo list" e pubblicarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-121">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

<span data-ttu-id="1dfe6-122">Seguire questa procedura per configurare il progetto server per l'uso del back-end .NET o Node.js.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-122">Follow the following steps to configure the server project to use either the Node.js or .NET backend.</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinios-app"></a><span data-ttu-id="1dfe6-123">Scaricare ed eseguire l'app per Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="1dfe6-123">Download and run the Xamarin.iOS app</span></span>
1. <span data-ttu-id="1dfe6-124">Aprire il [portale di Azure] in una finestra del browser.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-124">Open the [Azure portal] in a browser window.</span></span>
2. <span data-ttu-id="1dfe6-125">Nel pannello delle impostazioni dell'app per dispositivi mobili fare clic su **Introduzione** > **Xamarin.iOS**.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-125">On the settings blade for your Mobile App, click **Get Started** > **Xamarin.iOS**.</span></span> <span data-ttu-id="1dfe6-126">Al passaggio 3 fare clic su **Crea una nuova app** , se l'opzione non è già selezionata.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-126">Under step 3, click **Create a new app** if it's not already selected.</span></span>  <span data-ttu-id="1dfe6-127">Fare quindi clic sul pulsante **Download** .</span><span class="sxs-lookup"><span data-stu-id="1dfe6-127">Next click the **Download** button.</span></span>

      <span data-ttu-id="1dfe6-128">Verrà scaricata un'applicazione client che si connette al back-end mobile.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-128">A client application that connects to your mobile backend is downloaded.</span></span> <span data-ttu-id="1dfe6-129">Salvare il file del progetto compresso nel computer locale e prendere nota del percorso.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-129">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
3. <span data-ttu-id="1dfe6-130">Estrarre il progetto scaricato e aprirlo in Xamarin Studio (o in Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="1dfe6-130">Extract the project that you downloaded, and then open it in Xamarin Studio (or Visual Studio).</span></span>

    ![][9]

    ![][8]
4. <span data-ttu-id="1dfe6-131">Premere F5 per compilare il progetto e avviare l'app nell'emulatore iPhone.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-131">Press the F5 key to build the project and start the app in the iPhone emulator.</span></span>
5. <span data-ttu-id="1dfe6-132">Nell'app digitare un testo significativo, ad esempio *Learn Xamarin*, e quindi fare clic sul pulsante **+**.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-132">In the app, type meaningful text, such as *Learn Xamarin*, and then click the **+** button.</span></span>

    ![][10]

    <span data-ttu-id="1dfe6-133">I dati della richiesta vengono inseriti nella tabella TodoItem.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-133">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="1dfe6-134">Gli elementi archiviati nella tabella vengono restituiti dal back-end per app mobili e i dati vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-134">Items stored in the table are returned by the mobile app backend, and the data is displayed in the list.</span></span>

> [!NOTE]
> <span data-ttu-id="1dfe6-135">È possibile esaminare il codice che accede al back-end dell'app per dispositivi mobili per eseguire una query e inserire i dati nel file C# QSTodoService.cs.</span><span class="sxs-lookup"><span data-stu-id="1dfe6-135">You can review the code that accesses your mobile app backend to query and insert data in the QSTodoService.cs C# file.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="1dfe6-136">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1dfe6-136">Next steps</span></span>
* [<span data-ttu-id="1dfe6-137">Aggiungere la sincronizzazione offline all'app</span><span class="sxs-lookup"><span data-stu-id="1dfe6-137">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-ios-get-started-offline-data.md)
* [<span data-ttu-id="1dfe6-138">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="1dfe6-138">Add authentication to your app </span></span>](app-service-mobile-xamarin-ios-get-started-users.md)
* [<span data-ttu-id="1dfe6-139">Aggiungere notifiche push all'app Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="1dfe6-139">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-ios-get-started-push.md)
* [<span data-ttu-id="1dfe6-140">Come usare il client gestito per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="1dfe6-140">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

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
<span data-ttu-id="1dfe6-141">[portale di Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="1dfe6-141">[Azure portal]: https://portal.azure.com/</span></span>
