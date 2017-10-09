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
# <a name="add-push-notifications-tooyour-ios-app"></a>Aggiungere le notifiche Push tooyour iOS App
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, si aggiunge toohello le notifiche push [iOS quick start] progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push. Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.

Hello [simulatore iOS non supporta le notifiche push](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/iOS_Simulator_Guide/TestingontheiOSSimulator.html). È necessario un dispositivo iOS fisico e un'[appartenenza all'Apple Developer Program](https://developer.apple.com/programs/ios/).

## <a name="configure-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Registrare l'app per le notifiche push
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurare le notifiche push toosend Azure
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

## <a id="update-server"></a>Aggiornare le notifiche push toosend back-end
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-apns](../../includes/app-service-mobile-dotnet-backend-configure-push-apns.md)]

## <a id="add-push"></a>Aggiungere tooapp le notifiche push
[!INCLUDE [app-service-mobile-add-push-notifications-to-ios-app.md](../../includes/app-service-mobile-add-push-notifications-to-ios-app.md)]

## <a id="test"></a>Notifiche push di prova
[!INCLUDE [Test Push Notifications in App](../../includes/test-push-notifications-in-app.md)]

## <a id="more"></a>Altro
* I modelli consentono di push multipiattaforma toosend di flessibilità e push localizzata. [Come libreria Client per App mobili di Azure per iOS tooUse](app-service-mobile-ios-how-to-use-client-library.md#templates) illustra come tooregister modelli.

<!-- Anchors.  -->

<!-- Images. -->

<!-- URLs. -->
[iOS quick start]: app-service-mobile-ios-get-started.md
