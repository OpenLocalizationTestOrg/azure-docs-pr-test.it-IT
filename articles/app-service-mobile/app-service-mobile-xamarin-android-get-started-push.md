---
title: app xamarin di aaaAdd push notifiche tooyour | Documenti Microsoft
description: Informazioni su come toouse servizio App di Azure e gli hub di notifica di Azure toosend push delle notifiche tooyour xamarin app
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a><span data-ttu-id="02c48-103">Aggiungere app xamarin tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="02c48-103">Add push notifications tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="02c48-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="02c48-104">Overview</span></span>
<span data-ttu-id="02c48-105">In questa esercitazione, si aggiunge toohello le notifiche push [xamarin introduttiva](app-service-mobile-windows-store-dotnet-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="02c48-105">In this tutorial, you add push notifications toohello [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="02c48-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="02c48-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="02c48-107">Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="02c48-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02c48-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="02c48-108">Prerequisites</span></span>
<span data-ttu-id="02c48-109">Questa esercitazione richiede il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="02c48-109">This tutorial requires hello following:</span></span>

* <span data-ttu-id="02c48-110">Account Google attivo</span><span class="sxs-lookup"><span data-stu-id="02c48-110">An active Google account.</span></span> <span data-ttu-id="02c48-111">È possibile iscriversi a un account di Google in [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="02c48-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="02c48-112">[Componente client di Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/)</span><span class="sxs-lookup"><span data-stu-id="02c48-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="02c48-113"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="02c48-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="02c48-114"><a id="register"></a>Abilitare Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="02c48-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a><span data-ttu-id="02c48-115">Configurare Azure toosend push richieste</span><span class="sxs-lookup"><span data-stu-id="02c48-115">Configure Azure toosend push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="02c48-116"><a id="update-server"></a>Aggiornare le notifiche push di hello server progetto toosend</span><span class="sxs-lookup"><span data-stu-id="02c48-116"><a id="update-server"></a>Update hello server project toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="02c48-117"><a id="configure-app"></a>Configurare il progetto client hello per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="02c48-117"><a id="configure-app"></a>Configure hello client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="02c48-118"><a id="add-push"></a>Aggiungere app tooyour codice di notifiche push</span><span class="sxs-lookup"><span data-stu-id="02c48-118"><a id="add-push"></a>Add push notifications code tooyour app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="02c48-119"><a name="test"></a>Testare le notifiche push nell'app</span><span class="sxs-lookup"><span data-stu-id="02c48-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="02c48-120">È possibile testare l'applicazione hello utilizzando un dispositivo virtuale nell'emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="02c48-120">You can test hello app by using a virtual device in hello emulator.</span></span> <span data-ttu-id="02c48-121">Ci sono altri passaggi di configurazione richiesti durante l'esecuzione in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="02c48-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="02c48-122">Assicurarsi che si sta distribuendo tooor debug in un dispositivo virtuale con Google APIs impostato come destinazione di hello, come illustrato di seguito nella console di gestione hello dispositivo virtuale Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="02c48-122">Make sure that you are deploying tooor debugging on a virtual device that has Google APIs set as hello target, as shown below in hello Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="02c48-123">Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**, seguire i prompt hello.</span><span class="sxs-lookup"><span data-stu-id="02c48-123">Add a Google account toohello Android device by clicking **Apps** > **Settings** > **Add account**, then follow hello prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="02c48-124">Eseguire l'applicazione hello come prima e inserire un nuovo elemento di attività.</span><span class="sxs-lookup"><span data-stu-id="02c48-124">Run hello todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="02c48-125">Questa volta, viene visualizzata un'icona di notifica nell'area di notifica hello.</span><span class="sxs-lookup"><span data-stu-id="02c48-125">This time, a notification icon is displayed in hello notification area.</span></span> <span data-ttu-id="02c48-126">È possibile aprire hello notifica cassetto tooview hello full-text della notifica hello.</span><span class="sxs-lookup"><span data-stu-id="02c48-126">You can open hello notification drawer tooview hello full text of hello notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
