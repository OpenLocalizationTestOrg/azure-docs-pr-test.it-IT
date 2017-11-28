---
title: Aggiungere notifiche push all'app Android per Xamarin | Documentazione Microsoft
description: Informazioni su come usare Servizio app di Azure e Hub di notifica di Azure per inviare notifiche push all'app per Xamarin Android.
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="bd2d1-103">Aggiungere notifiche push all'app Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="bd2d1-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="bd2d1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="bd2d1-104">Overview</span></span>
<span data-ttu-id="bd2d1-105">In questa esercitazione vengono aggiunte notifiche push al progetto [avvio rapido di Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md), in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="bd2d1-106">Se non si usa il progetto server di avvio rapido scaricato, sarà necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="bd2d1-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="bd2d1-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd2d1-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="bd2d1-108">Prerequisites</span></span>
<span data-ttu-id="bd2d1-109">Per completare questa esercitazione, è necessario disporre di:</span><span class="sxs-lookup"><span data-stu-id="bd2d1-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="bd2d1-110">Account Google attivo</span><span class="sxs-lookup"><span data-stu-id="bd2d1-110">An active Google account.</span></span> <span data-ttu-id="bd2d1-111">È possibile iscriversi a un account di Google in [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="bd2d1-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="bd2d1-112">[Componente client di Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/)</span><span class="sxs-lookup"><span data-stu-id="bd2d1-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="bd2d1-113"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="bd2d1-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="bd2d1-114"><a id="register"></a>Abilitare Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="bd2d1-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="bd2d1-115">Configurare Azure per l'invio di richieste push</span><span class="sxs-lookup"><span data-stu-id="bd2d1-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="bd2d1-116"><a id="update-server"></a>Aggiornare il progetto server per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="bd2d1-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="bd2d1-117"><a id="configure-app"></a>Configurare il progetto client per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="bd2d1-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="bd2d1-118"><a id="add-push"></a>Aggiungere il codice delle notifiche push all'app</span><span class="sxs-lookup"><span data-stu-id="bd2d1-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="bd2d1-119"><a name="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="bd2d1-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="bd2d1-120">È possibile testare l'app mediante un dispositivo virtuale nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="bd2d1-121">Ci sono altri passaggi di configurazione richiesti durante l'esecuzione in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="bd2d1-122">Assicurarsi di distribuire o eseguire il debug su un dispositivo virtuale che ha le API Google API impostate come destinazione, come illustrato di seguito nel gestore del dispositivo virtuale Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="bd2d1-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="bd2d1-123">Aggiungere un account Google al dispositivo Android facendo clic su **Apps** (App) > **Settings** (Impostazioni) > **Add account** (Aggiungi account), quindi seguire le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="bd2d1-124">Eseguire l'app todolist come fatto in precedenza e inserire un nuovo elemento todo.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="bd2d1-125">Questa volta, viene visualizzata un'icona di notifica nell'area di notifica.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="bd2d1-126">È possibile aprire la cassetta della notifica per visualizzare il testo completo della notifica.</span><span class="sxs-lookup"><span data-stu-id="bd2d1-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
