---
title: Aggiungere notifiche push all'app Android con App per dispositivi mobili | Documentazione Microsoft
description: Informazioni su come usare App per dispositivi mobili per inviare notifiche push all'app Android.
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="204bc-103">Aggiungere notifiche push all'app Android</span><span class="sxs-lookup"><span data-stu-id="204bc-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="204bc-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="204bc-104">Overview</span></span>
<span data-ttu-id="204bc-105">In questa esercitazione vengono aggiunte notifiche push al progetto [avvio rapido di Android], in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="204bc-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="204bc-106">Se non si usa il progetto server di avvio rapido scaricato, è necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="204bc-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="204bc-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="204bc-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="204bc-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="204bc-108">Prerequisites</span></span>
<span data-ttu-id="204bc-109">Sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="204bc-109">You need the following:</span></span>

* <span data-ttu-id="204bc-110">Un IDE, in base al back-end del progetto:</span><span class="sxs-lookup"><span data-stu-id="204bc-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="204bc-111">[Android Studio](https://developer.android.com/sdk/index.html) se questa app ha un back-end Node.js.</span><span class="sxs-lookup"><span data-stu-id="204bc-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="204bc-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) o versione successiva se questa app ha un back-end Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="204bc-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="204bc-113">Android 2.3 o versione successiva, Google Repository 27 o versione successiva e Google Play Services 9.0.2 o versione successiva per Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="204bc-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="204bc-114">Completare l'[avvio rapido di Android].</span><span class="sxs-lookup"><span data-stu-id="204bc-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="204bc-115">Creare un progetto che supporta Google Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="204bc-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="204bc-116">Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="204bc-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="204bc-117">Configurare Azure per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="204bc-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="204bc-118">Abilitare le notifiche push per il progetto server</span><span class="sxs-lookup"><span data-stu-id="204bc-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="204bc-119">Aggiungere notifiche push all'app</span><span class="sxs-lookup"><span data-stu-id="204bc-119">Add push notifications to your app</span></span>
<span data-ttu-id="204bc-120">In questa sezione l'app del client Android viene aggiornata in modo da gestire le notifiche push.</span><span class="sxs-lookup"><span data-stu-id="204bc-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="204bc-121">Verificare la versione di Android SDK</span><span class="sxs-lookup"><span data-stu-id="204bc-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="204bc-122">Il passaggio successivo comporta l'installazione di Google Play Services.</span><span class="sxs-lookup"><span data-stu-id="204bc-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="204bc-123">Google Cloud Messaging prevede alcuni requisiti minimi a livello di API per lo sviluppo e i test. È necessario che la proprietà **minSdkVersion** nel file manifesto sia conforme a tali requisiti.</span><span class="sxs-lookup"><span data-stu-id="204bc-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="204bc-124">Se il test viene eseguito con un dispositivo meno recente, vedere [Set Up Google Play Services SDK] (Configurare Google Play Services SDK) per determinare il livello minimo su cui è possibile impostare tale valore.</span><span class="sxs-lookup"><span data-stu-id="204bc-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="204bc-125">Aggiungere Google Play Services al progetto</span><span class="sxs-lookup"><span data-stu-id="204bc-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="204bc-126">Aggiungere codice</span><span class="sxs-lookup"><span data-stu-id="204bc-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="204bc-127">Eseguire il test dell'app sul servizio mobile pubblicato</span><span class="sxs-lookup"><span data-stu-id="204bc-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="204bc-128">È possibile eseguire il test dell'app collegando direttamente un telefono Android con un cavo USB oppure usando un dispositivo virtuale nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="204bc-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="204bc-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="204bc-129">Next steps</span></span>
<span data-ttu-id="204bc-130">Dopo aver completato questa esercitazione, continuare con una delle esercitazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="204bc-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="204bc-131">[Aggiungere l'autenticazione all'app Android](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="204bc-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="204bc-132">Questa esercitazione spiega come aggiungere l'autenticazione al progetto introduttivo TodoList in Android tramite un provider di identità supportato.</span><span class="sxs-lookup"><span data-stu-id="204bc-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="204bc-133">[Attivare la sincronizzazione offline per l'app Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="204bc-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="204bc-134">Informazioni su come aggiungere il supporto offline all'app usando il back-end di App per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="204bc-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="204bc-135">Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="204bc-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="204bc-136">[avvio rapido di Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="204bc-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="204bc-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup (Configurare Google Play Services SDK)</span><span class="sxs-lookup"><span data-stu-id="204bc-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
