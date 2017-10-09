---
title: aaaAdd tooiOS le notifiche Push App con App mobili di Azure
description: Informazioni su app iOS tooyour di notifiche push toouse toosend di App mobili di Azure.
services: app-service\mobile
documentationcenter: ios
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: fa503833-d23e-4925-8d93-341bb3fbab7d
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/10/2016
ms.author: glenga
ms.openlocfilehash: 11588c56bc8987a71257dbad4fcdebf1b3209b1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-ios-app"></a><span data-ttu-id="40b47-103">Aggiungere le notifiche Push tooyour iOS App</span><span class="sxs-lookup"><span data-stu-id="40b47-103">Add Push Notifications tooyour iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="40b47-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="40b47-104">Overview</span></span>
<span data-ttu-id="40b47-105">In questa esercitazione, si aggiunge toohello le notifiche push [iOS quick start] progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.</span><span class="sxs-lookup"><span data-stu-id="40b47-105">In this tutorial, you add push notifications toohello [iOS quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="40b47-106">Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="40b47-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="40b47-107">Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="40b47-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="40b47-108">Hello [simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="40b47-108">hello [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="40b47-109">È necessario un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="40b47-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="40b47-110"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="40b47-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="40b47-111"><a id="register"></a>Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="40b47-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="40b47-112">Configurare le notifiche push toosend Azure</span><span class="sxs-lookup"><span data-stu-id="40b47-112">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="40b47-113"><a id="update-server"></a>Aggiornare le notifiche push toosend back-end</span><span class="sxs-lookup"><span data-stu-id="40b47-113"><a id="update-server"></a>Update backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="40b47-114"><a id="add-push"></a>Aggiungere tooapp le notifiche push</span><span class="sxs-lookup"><span data-stu-id="40b47-114"><a id="add-push"></a>Add push notifications tooapp</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="40b47-115"><a id="test"></a>Notifiche push di prova</span><span class="sxs-lookup"><span data-stu-id="40b47-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="40b47-116"><a id="more"></a>Altro</span><span class="sxs-lookup"><span data-stu-id="40b47-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="40b47-117">I modelli consentono di push multipiattaforma toosend di flessibilità e push localizzata.</span><span class="sxs-lookup"><span data-stu-id="40b47-117">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="40b47-118">[Come libreria Client per App mobili di Azure per iOS tooUse](app-service-mobile-ios-how-to-use-client-library.md#templates) illustra come tooregister modelli.</span><span class="sxs-lookup"><span data-stu-id="40b47-118">[How tooUse iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how tooregister templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS quick start]: app-service-mobile-ios-get-started.md
