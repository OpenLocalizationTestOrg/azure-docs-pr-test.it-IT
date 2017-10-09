---
title: aaaGet avviato con App mobili di Azure per le app xamarin
description: Seguire questa esercitazione tooget avviato tramite app mobili di Azure per lo sviluppo di Xamarin Android
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
ms.openlocfilehash: 38710660d9328fe3c068efca972f76aa8b6e049b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinandroid-app"></a><span data-ttu-id="86f5c-103">Creare un'app per Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="86f5c-103">Create a Xamarin.Android App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="86f5c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="86f5c-104">Overview</span></span>
<span data-ttu-id="86f5c-105">Questa esercitazione viene illustrato come tooadd un back-end basato su cloud service tooa xamarin app.</span><span class="sxs-lookup"><span data-stu-id="86f5c-105">This tutorial shows you how tooadd a cloud-based backend service tooa Xamarin.Android app.</span></span> <span data-ttu-id="86f5c-106">Per altre informazioni, vedere [Informazioni sulle app per dispositivi mobili](app-service-mobile-value-prop.md).</span><span class="sxs-lookup"><span data-stu-id="86f5c-106">For more information, see [What are Mobile Apps](app-service-mobile-value-prop.md).</span></span>

<span data-ttu-id="86f5c-107">Di seguito viene riportata una schermata da app hello completata:</span><span class="sxs-lookup"><span data-stu-id="86f5c-107">A screenshot from hello completed app is below:</span></span>

![][0]

<span data-ttu-id="86f5c-108">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Android.</span><span class="sxs-lookup"><span data-stu-id="86f5c-108">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Android apps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86f5c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="86f5c-109">Prerequisites</span></span>
<span data-ttu-id="86f5c-110">toocomplete questa esercitazione, è necessario hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="86f5c-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="86f5c-111">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="86f5c-111">An active Azure account.</span></span> <span data-ttu-id="86f5c-112">Se non si dispone di un account, iscriversi a una versione di valutazione di Azure e ottenere le App per dispositivi mobili too10 disponibile.</span><span class="sxs-lookup"><span data-stu-id="86f5c-112">If you don't have an account, sign up for an Azure trial and get up too10 free Mobile Apps.</span></span> <span data-ttu-id="86f5c-113">Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86f5c-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="86f5c-114">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="86f5c-114">Visual Studio with Xamarin.</span></span> <span data-ttu-id="86f5c-115">Per le istruzioni vedere [Configurazione e installazione di Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) .</span><span class="sxs-lookup"><span data-stu-id="86f5c-115">See [Setup and install for Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) for instructions.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="86f5c-116">Creare un back-end dell'app per dispositivi mobili di Azure</span><span class="sxs-lookup"><span data-stu-id="86f5c-116">Create an Azure Mobile App backend</span></span>
<span data-ttu-id="86f5c-117">Seguire questi toocreate passaggi un back-end dell'App Mobile.</span><span class="sxs-lookup"><span data-stu-id="86f5c-117">Follow these steps toocreate a Mobile App backend.</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="86f5c-118">È stato eseguito il provisioning di un back-end dell'app per dispositivi mobili di Azure che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="86f5c-118">You have now provisioned an Azure Mobile App backend that can be used by your mobile client applications.</span></span> <span data-ttu-id="86f5c-119">Successivamente, scaricare un progetto server di un semplice "elenco di attività" back-end e pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="86f5c-119">Next, download a server project for a simple "todo list" backend and publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="86f5c-120">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="86f5c-120">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinandroid-app"></a><span data-ttu-id="86f5c-121">Scaricare ed eseguire app xamarin hello</span><span class="sxs-lookup"><span data-stu-id="86f5c-121">Download and run hello Xamarin.Android app</span></span>
1. <span data-ttu-id="86f5c-122">In **scaricare ed eseguire il progetto xamarin**, fare clic su hello **scaricare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86f5c-122">Under **Download and run your Xamarin.Android project**, click hello **Download** button.</span></span>

      <span data-ttu-id="86f5c-123">Salvare computer locale tooyour file progetto compresso hello e prendere nota del dove salvarla.</span><span class="sxs-lookup"><span data-stu-id="86f5c-123">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>
2. <span data-ttu-id="86f5c-124">Hello premere **F5** progetto hello toobuild della chiave e riavviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="86f5c-124">Press hello **F5** key toobuild hello project and start hello app.</span></span>
3. <span data-ttu-id="86f5c-125">Nell'app hello, digitare un testo significativo, ad esempio *esercitazione hello completo* e quindi fare clic su hello **Aggiungi** pulsante.</span><span class="sxs-lookup"><span data-stu-id="86f5c-125">In hello app, type meaningful text, such as *Complete hello tutorial* and then click hello **Add** button.</span></span>

    ![][10]

    <span data-ttu-id="86f5c-126">Dati richiesta hello viene inseriti nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="86f5c-126">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="86f5c-127">Vengono restituiti gli elementi archiviati nella tabella hello dal back-end di hello app per dispositivi mobili e i dati vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="86f5c-127">Items stored in hello table are returned by hello mobile app backend, and the data appears in hello list.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86f5c-128">È possibile esaminare il codice hello che accede a tooquery di back-end le app per dispositivi mobili e inserire i dati, disponibile in c# ToDoActivity.cs file hello.</span><span class="sxs-lookup"><span data-stu-id="86f5c-128">You can review hello code that accesses your mobile app backend tooquery and insert data, which is found in hello ToDoActivity.cs C# file.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="86f5c-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="86f5c-129">Next steps</span></span>
* [<span data-ttu-id="86f5c-130">Aggiungere app tooyour sincronizzazione Offline</span><span class="sxs-lookup"><span data-stu-id="86f5c-130">Add Offline Sync tooyour app</span></span>](app-service-mobile-xamarin-android-get-started-offline-data.md)
* [<span data-ttu-id="86f5c-131">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="86f5c-131">Add authentication tooyour app </span></span>](app-service-mobile-xamarin-android-get-started-users.md)
* [<span data-ttu-id="86f5c-132">Aggiungere app xamarin tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="86f5c-132">Add push notifications tooyour Xamarin.Android app</span></span>](app-service-mobile-xamarin-android-get-started-push.md)
* [<span data-ttu-id="86f5c-133">Modalità di gestione client per App mobili di Azure hello toouse</span><span class="sxs-lookup"><span data-stu-id="86f5c-133">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)

<!-- Images. -->
[0]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-completed-android.png
[6]: ./media/app-service-mobile-xamarin-android-get-started/mobile-portal-quickstart-xamarin.png
[8]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-vs.png
[9]: ./media/app-service-mobile-xamarin-android-get-started/mobile-xamarin-project-android-xs.png
[10]: ./media/app-service-mobile-xamarin-android-get-started/mobile-quickstart-startup-android.png

<!-- URLs. -->
[Azure Portal]: https://azure.portal.com/
[Visual Studio]: https://go.microsoft.com/fwLink/p/?LinkID=534203
