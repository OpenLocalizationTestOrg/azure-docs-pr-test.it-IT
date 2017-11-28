---
title: Introduzione alle app per dispositivi mobili di Azure per Xamarin.Android
description: Seguire questa esercitazione per iniziare a usare le app per dispositivi mobili di Azure per lo sviluppo per Xamarin Android.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 81649dd3-544f-40ff-b9b7-60c66d683e60
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 6b41fd8090dd771fc40769c134bad258b3d4bd36
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="4e3a2-103">Creare un'app per Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4e3a2-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="4e3a2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="4e3a2-104">Overview</span></span>
<span data-ttu-id="4e3a2-105">Questa esercitazione illustra come aggiungere un servizio back-end basato sul cloud a un'app Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-105">This tutorial shows you how to add a cloud-based backend service to a Xamarin.Android app.</span></span> <span data-ttu-id="4e3a2-106">Per altre informazioni, vedere [Informazioni sulle app per dispositivi mobili](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="4e3a2-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="4e3a2-107">Di seguito è riportata una schermata dell'app completata:</span><span class="sxs-lookup"><span data-stu-id="4e3a2-107">A screenshot from the completed app is below:</span></span>

![][0]

<span data-ttu-id="4e3a2-108">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e3a2-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4e3a2-109">Prerequisites</span></span>
<span data-ttu-id="4e3a2-110">Per completare questa esercitazione è necessario soddisfare i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4e3a2-110">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="4e3a2-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-111">An active Azure account.</span></span> <span data-ttu-id="4e3a2-112">Se non si ha un account, è possibile iscriversi alla versione di valutazione di Azure e ottenere fino a un massimo di 10 app per dispositivi mobili gratuite.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-112">If you don't have an account, sign up for an Azure trial and get up to 10 free Mobile Apps.</span></span> <span data-ttu-id="4e3a2-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e3a2-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4e3a2-114">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="4e3a2-115">Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4e3a2-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="4e3a2-116">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="4e3a2-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="4e3a2-117">Seguire questa procedura per creare un back-end dell'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-117">Follow these steps to create a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="4e3a2-118">È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="4e3a2-119">Scaricare quindi un progetto server per un semplice back-end "todo list" e pubblicarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-119">Next, download a server project for a simple "todo list" backend and publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="4e3a2-120">Configurare il progetto server</span><span class="sxs-lookup"><span data-stu-id="4e3a2-120">Configure the server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinandroid-app"></a><span data-ttu-id="4e3a2-121">Scaricare ed eseguire l'app per Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4e3a2-121">Download and run the Xamarin.Android app</span></span>
1. <span data-ttu-id="4e3a2-122">In **Download and run your Xamarin.Android project** (Scarica ed esegui il progetto Xamarin.Android) scegliere il pulsante **Download** (Scarica).</span><span class="sxs-lookup"><span data-stu-id="4e3a2-122">Under **Download and run your Xamarin.Android project**, click the **Download** button.</span></span>

      <span data-ttu-id="4e3a2-123">Salvare il file del progetto compresso nel computer locale e prendere nota del percorso.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-123">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="4e3a2-124">Premere **F5** per compilare il progetto e avviare l'app.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-124">Press the **F5** key to build the project and start the app.</span></span>
3. <span data-ttu-id="4e3a2-125">Nell'app digitare un testo significativo, ad esempio *Complete the tutorial* quindi fare clic sul pulsante **Add**.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-125">In the app, type meaningful text, such as *Complete the tutorial* and then click the **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="4e3a2-126">I dati della richiesta vengono inseriti nella tabella TodoItem.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-126">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="4e3a2-127">Gli elementi archiviati nella tabella vengono restituiti dal back-end per app per dispositivi mobili e i dati vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-127">Items stored in the table are returned by the mobile app backend, and the data appears in the list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4e3a2-128">È possibile esaminare il codice che accede al back-end per app mobili per eseguire una query e inserire i dati trovati nel file C# ToDoActivity.cs.</span><span class="sxs-lookup"><span data-stu-id="4e3a2-128">You can review the code that accesses your mobile app backend to query and insert data, which is found in the ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="4e3a2-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4e3a2-129">Next steps</span></span>
* [<span data-ttu-id="4e3a2-130">Aggiungere la sincronizzazione offline all'app</span><span class="sxs-lookup"><span data-stu-id="4e3a2-130">Add Offline Sync to your app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="4e3a2-131">Add authentication to your app </span><span class="sxs-lookup"><span data-stu-id="4e3a2-131">Add authentication to your app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="4e3a2-132">Aggiungere notifiche push all'app Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="4e3a2-132">Add push notifications to your Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="4e3a2-133">Come usare il client gestito per App per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="4e3a2-133">How to use the managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
