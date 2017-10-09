---
title: aaaCreate una piattaforma UWP (Universal Windows) che utilizza in App per dispositivi mobili | Documenti Microsoft
description: Seguire questa esercitazione tooget introduttive sull'utilizzo di back-end delle app mobili di Azure per lo sviluppo di app Universal Windows Platform (UWP) in c#, Visual Basic o JavaScript.
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a><span data-ttu-id="7a354-103">Creare un'app Windows</span><span class="sxs-lookup"><span data-stu-id="7a354-103">Create a Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="7a354-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="7a354-104">Overview</span></span>
<span data-ttu-id="7a354-105">Questa esercitazione viene illustrato come del servizio app di Windows della piattaforma UWP (Universal) tooa tooadd un back-end basato su cloud.</span><span class="sxs-lookup"><span data-stu-id="7a354-105">This tutorial shows you how tooadd a cloud-based backend service tooa Universal Windows Platform (UWP) app.</span></span> <span data-ttu-id="7a354-106">Per altre informazioni, vedere [Informazioni sulle app per dispositivi mobili](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="7a354-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span> <span data-ttu-id="7a354-107">di seguito Hello sono acquisizioni dello schermo da app hello completata:</span><span class="sxs-lookup"><span data-stu-id="7a354-107">hello following are screen captures from hello completed app:</span></span>

![App desktop completata](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
<span data-ttu-id="7a354-109">Esecuzione in un computer desktop.</span><span class="sxs-lookup"><span data-stu-id="7a354-109">Running on a desktop.</span></span>

![App per telefono completata](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
<span data-ttu-id="7a354-111">Esecuzione in un telefono.</span><span class="sxs-lookup"><span data-stu-id="7a354-111">Running on a phone</span></span>

<span data-ttu-id="7a354-112">Il completamento di questa esercitazione costituisce un prerequisito per tutte le altre esercitazioni delle app per dispositivi mobili relative ad app UWP.</span><span class="sxs-lookup"><span data-stu-id="7a354-112">Completing this tutorial is a prerequisite for all other Mobile App tutorials for UWP apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a354-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7a354-113">Prerequisites</span></span>
<span data-ttu-id="7a354-114">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7a354-114">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7a354-115">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="7a354-115">An active Azure account.</span></span> <span data-ttu-id="7a354-116">Se non si dispone di un account, è possibile iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione.</span><span class="sxs-lookup"><span data-stu-id="7a354-116">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="7a354-117">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7a354-117">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="7a354-118">[Visual Studio Community 2015] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7a354-118">[Visual Studio Community 2015] or a later version.</span></span>

## <a name="create-a-new-azure-mobile-app-backend"></a><span data-ttu-id="7a354-119">Creare un nuovo back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="7a354-119">Create a new Azure Mobile App backend</span></span>
<span data-ttu-id="7a354-120">Seguire questi toocreate passaggi un nuova App per dispositivi mobili di back-end.</span><span class="sxs-lookup"><span data-stu-id="7a354-120">Follow these steps toocreate a new Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="7a354-121">È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7a354-121">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="7a354-122">Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7a354-122">Next, you will download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="7a354-123">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="7a354-123">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a><span data-ttu-id="7a354-124">Scaricare ed eseguire il progetto di client hello</span><span class="sxs-lookup"><span data-stu-id="7a354-124">Download and run hello client project</span></span>
<span data-ttu-id="7a354-125">Dopo aver configurato il back-end dell'App per dispositivi mobili, è possibile creare una nuova app client o modificare un tooAzure di tooconnect app esistente.</span><span class="sxs-lookup"><span data-stu-id="7a354-125">Once you have configured your Mobile App backend, you can either create a new client app or modify an existing app tooconnect tooAzure.</span></span> <span data-ttu-id="7a354-126">In questa sezione si scarica un progetto di modello di app UWP di back-end App Mobile di tooyour tooconnect personalizzato.</span><span class="sxs-lookup"><span data-stu-id="7a354-126">In this section, you download a UWP app template project that is customized tooconnect tooyour Mobile App backend.</span></span>

1. <span data-ttu-id="7a354-127">In hello **introduttiva** pannello per il back-end App Mobile, fare clic su **crea una nuova app** > **scaricare**, quindi estrarre i file di progetto hello compresso tooyour computer locale.</span><span class="sxs-lookup"><span data-stu-id="7a354-127">Back in hello **Quick start** blade for your Mobile App backend, click **Create a new app** > **Download**, then extract hello compressed project files tooyour local computer.</span></span>

    ![Download del progetto di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. <span data-ttu-id="7a354-129">(Facoltativo) Aggiungere toohello di progetto app UWP hello stessa soluzione come progetto server hello.</span><span class="sxs-lookup"><span data-stu-id="7a354-129">(Optional) Add hello UWP app project toohello same solution as hello server project.</span></span> <span data-ttu-id="7a354-130">Questo rende più semplice toodebug e i test sia hello back-end app e hello in hello stessa soluzione di Visual Studio, se si sceglie toodo questa operazione.</span><span class="sxs-lookup"><span data-stu-id="7a354-130">This makes it easier toodebug and test both hello app and hello backend in hello same Visual Studio solution, if you choose toodo so.</span></span> <span data-ttu-id="7a354-131">tooadd una soluzione di toohello progetto di app UWP, è necessario utilizzare Visual Studio 2015 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="7a354-131">tooadd a UWP app project toohello solution, you must be using Visual Studio 2015 or a later version.</span></span>
3. <span data-ttu-id="7a354-132">Con app UWP hello come progetto di avvio hello, premere hello F5 chiave toodeploy e app hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="7a354-132">With hello UWP app as hello startup project, press hello F5 key toodeploy and run hello app.</span></span>
4. <span data-ttu-id="7a354-133">Nell'app hello, digitare un testo significativo, ad esempio *esercitazione hello completo*, in hello **Insert a TodoItem** casella di testo e quindi fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="7a354-133">In hello app, type meaningful text, such as *Complete hello tutorial*, in hello **Insert a TodoItem** text box, and then click **Save**.</span></span>

    ![Desktop completo di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    <span data-ttu-id="7a354-135">Consente di inviare un POST richiesta toohello nuova app per dispositivi mobili back-end che è ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="7a354-135">This sends a POST request toohello new mobile app backend that's hosted in Azure.</span></span>
5. <span data-ttu-id="7a354-136">(Facoltativo) Arrestare l'applicazione hello e riavviarla in un altro dispositivo o un emulatore per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="7a354-136">(Optional) Stop hello app and restart it on a different device or mobile emulator.</span></span>

    ![Telefono completo di guida introduttiva di Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    <span data-ttu-id="7a354-138">Si noti che i dati salvati dal passaggio precedente hello venga caricati dalla Azure dopo l'avvio di hello app UWP.</span><span class="sxs-lookup"><span data-stu-id="7a354-138">Notice that data saved from hello previous step is loaded from Azure after hello UWP app starts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a354-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7a354-139">Next steps</span></span>
* [<span data-ttu-id="7a354-140">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="7a354-140">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="7a354-141">Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="7a354-141">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="7a354-142">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="7a354-142">Add push notifications tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  <span data-ttu-id="7a354-143">Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push toosend App Mobile back-end toouse gli hub di notifica di Azure.</span><span class="sxs-lookup"><span data-stu-id="7a354-143">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="7a354-144">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="7a354-144">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="7a354-145">Informazioni su come offline tooadd supportano un'applicazione con un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="7a354-145">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="7a354-146">Sincronizzazione non in linea consente agli utenti finali toointeract con un'app mobile&mdash;visualizzazione, aggiunta o modifica dei dati&mdash;anche quando è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="7a354-146">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
