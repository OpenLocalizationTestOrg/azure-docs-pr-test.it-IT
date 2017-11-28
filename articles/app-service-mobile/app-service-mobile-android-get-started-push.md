---
title: aaaAdd push notifiche tooyour app Android con App per dispositivi mobili | Documenti Microsoft
description: Informazioni su app Android tooyour di notifiche push toouse toosend di App per dispositivi mobili.
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="ae819-103">Aggiungere app per Android tooyour le notifiche push</span><span class="sxs-lookup"><span data-stu-id="ae819-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="ae819-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ae819-104">Overview</span></span>
<span data-ttu-id="ae819-105">In questa esercitazione, si aggiunge toohello le notifiche push [Android introduttiva] progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="ae819-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="ae819-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="ae819-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="ae819-107">Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ae819-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae819-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ae819-108">Prerequisites</span></span>
<span data-ttu-id="ae819-109">Sono necessari i seguenti elementi di hello:</span><span class="sxs-lookup"><span data-stu-id="ae819-109">You need hello following:</span></span>

* <span data-ttu-id="ae819-110">Un IDE, in base al back-end del progetto:</span><span class="sxs-lookup"><span data-stu-id="ae819-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="ae819-111">[Android Studio](https://developer.android.com/sdk/index.html) se questa app ha un back-end Node.js.</span><span class="sxs-lookup"><span data-stu-id="ae819-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="ae819-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) o versione successiva se questa app ha un back-end Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="ae819-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="ae819-113">Android 2.3 o versione successiva, Google Repository 27 o versione successiva e Google Play Services 9.0.2 o versione successiva per Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="ae819-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="ae819-114">Hello completo [Android introduttiva].</span><span class="sxs-lookup"><span data-stu-id="ae819-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="ae819-115">Creare un progetto che supporta Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="ae819-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="ae819-116">Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="ae819-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="ae819-117">Configurare le notifiche push toosend Azure</span><span class="sxs-lookup"><span data-stu-id="ae819-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="ae819-118">Abilitare le notifiche push per il progetto server hello</span><span class="sxs-lookup"><span data-stu-id="ae819-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="ae819-119">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="ae819-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="ae819-120">In questa sezione aggiornare le notifiche di push client toohandle app Android.</span><span class="sxs-lookup"><span data-stu-id="ae819-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="ae819-121">Verificare la versione di Android SDK</span><span class="sxs-lookup"><span data-stu-id="ae819-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="ae819-122">Il passaggio successivo è tooinstall Google Play services.</span><span class="sxs-lookup"><span data-stu-id="ae819-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="ae819-123">Google Cloud Messaging è alcuni requisiti del livello minimi API per lo sviluppo e test, quali hello **minSdkVersion** proprietà nel manifesto hello devono essere conformi alle.</span><span class="sxs-lookup"><span data-stu-id="ae819-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="ae819-124">Se si sta testando con un dispositivo meno recente, consultare [impostare backup di Google Play Services SDK] toodetermine bassa come è possibile impostare questo valore e impostarlo in modo appropriato.</span><span class="sxs-lookup"><span data-stu-id="ae819-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="ae819-125">Aggiungi progetto toohello di Google Play services</span><span class="sxs-lookup"><span data-stu-id="ae819-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="ae819-126">Aggiungere codice</span><span class="sxs-lookup"><span data-stu-id="ae819-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="ae819-127">Test app hello contro hello pubblicati servizio mobile</span><span class="sxs-lookup"><span data-stu-id="ae819-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="ae819-128">È possibile testare app hello, collegando direttamente un telefono Android tramite un cavo USB o un dispositivo virtuale nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="ae819-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae819-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae819-129">Next steps</span></span>
<span data-ttu-id="ae819-130">Ora che è stata completata questa esercitazione, è consigliabile continuare su tooone di hello seguenti esercitazioni:</span><span class="sxs-lookup"><span data-stu-id="ae819-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="ae819-131">[Aggiungere app Android di autenticazione tooyour](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="ae819-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="ae819-132">Informazioni su come progetto di tooadd autenticazione toohello todolist delle Guide rapide in Android usando un provider di identità supportati.</span><span class="sxs-lookup"><span data-stu-id="ae819-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="ae819-133">[Attivare la sincronizzazione offline per l'app Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="ae819-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="ae819-134">Informazioni su come offline tooadd supportano tooyour app con un back-end App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="ae819-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="ae819-135">Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="ae819-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android introduttiva]: app-service-mobile-android-get-started.md

[impostare backup di Google Play Services SDK]:https://developers.google.com/android/guides/setup (Configurare Google Play Services SDK)
