---
title: Aggiungere notifiche push all'app per iOS con le app per dispositivi mobili di Azure
description: Informazioni su come usare le app per dispositivi mobili di Azure per inviare notifiche push all'app per iOS.
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
ms.openlocfilehash: 08a8c35b89386bd0dbe7bba406a6985a5a0d7eb8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-ios-app"></a><span data-ttu-id="ea397-103">Aggiungere notifiche push all'app iOS</span><span class="sxs-lookup"><span data-stu-id="ea397-103">Add Push Notifications to your iOS App</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="ea397-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ea397-104">Overview</span></span>
<span data-ttu-id="ea397-105">In questa esercitazione vengono aggiunte notifiche push al progetto [avvio rapido di iOS], in modo che una notifica push venga inviata al dispositivo a ogni inserimento di record.</span><span class="sxs-lookup"><span data-stu-id="ea397-105">In this tutorial, you add push notifications to the [iOS quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="ea397-106">Se non si usa il progetto server di avvio rapido scaricato, sarà necessario aggiungere il pacchetto di estensione di notifica push.</span><span class="sxs-lookup"><span data-stu-id="ea397-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="ea397-107">Per altre informazioni, vedere [Usare l'SDK del server back-end .NET per App per dispositivi mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ea397-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

<span data-ttu-id="ea397-108">[Il simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span><span class="sxs-lookup"><span data-stu-id="ea397-108">The [iOS simulator does not support push notifications](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html).</span></span> <span data-ttu-id="ea397-109">È necessario un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/).</span><span class="sxs-lookup"><span data-stu-id="ea397-109">You need a physical iOS device and an [Apple Developer Program membership](https://developer.apple.com/programs/ios/).</span></span>

## <span data-ttu-id="ea397-110"><a name="configure-hub"></a>Configurare un hub di notifica</span><span class="sxs-lookup"><span data-stu-id="ea397-110"><a name="configure-hub"></a>Configure Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="ea397-111"><a id="register"></a>Registrare l'app per le notifiche push</span><span class="sxs-lookup"><span data-stu-id="ea397-111"><a id="register"></a>Register app for push notifications</span></span>
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="ea397-112">Configurare Azure per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="ea397-112">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <span data-ttu-id="ea397-113"><a id="update-server"></a>Aggiornare il codice back-end per l'invio di notifiche push</span><span class="sxs-lookup"><span data-stu-id="ea397-113"><a id="update-server"></a>Update backend to send push notifications</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <span data-ttu-id="ea397-114"><a id="add-push"></a>Aggiungere notifiche push all'app</span><span class="sxs-lookup"><span data-stu-id="ea397-114"><a id="add-push"></a>Add push notifications to app</span></span>
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <span data-ttu-id="ea397-115"><a id="test"></a>Notifiche push di prova</span><span class="sxs-lookup"><span data-stu-id="ea397-115"><a id="test"></a>Test push notifications</span></span>
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <span data-ttu-id="ea397-116"><a id="more"></a>Altro</span><span class="sxs-lookup"><span data-stu-id="ea397-116"><a id="more"></a>More</span></span>
* <span data-ttu-id="ea397-117">I modelli offrono flessibilità per inviare notifiche push multipiattaforma e push localizzati.</span><span class="sxs-lookup"><span data-stu-id="ea397-117">Templates give you flexibility to send cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="ea397-118">[Come usare la libreria client iOS per le app per dispositivi mobili di Azure](app-service-mobile-ios-how-to-use-client-library.md#templates) illustra come registrare modelli.</span><span class="sxs-lookup"><span data-stu-id="ea397-118">[How to Use iOS Client Library for Azure Mobile Apps](app-service-mobile-ios-how-to-use-client-library.md#templates) shows you how to register templates.</span></span>

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
<span data-ttu-id="ea397-119">[avvio rapido di iOS]: app-service-mobile-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="ea397-119">[iOS quick start]: app-service-mobile-ios-get-started.md</span></span>
