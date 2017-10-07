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
# <a name="add-push-notifications-tooyour-android-app"></a>Aggiungere app per Android tooyour le notifiche push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, si aggiunge toohello le notifiche push [Android introduttiva] progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, è necessario hello pacchetto estensione di notifica push. Per ulteriori informazioni, vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Prerequisiti
Sono necessari i seguenti elementi di hello:

* Un IDE, in base al back-end del progetto:

  * [Android Studio](https://developer.android.com/sdk/index.html) se questa app ha un back-end Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) o versione successiva se questa app ha un back-end Microsoft .NET.
* Android 2.3 o versione successiva, Google Repository 27 o versione successiva e Google Play Services 9.0.2 o versione successiva per Firebase Cloud Messaging.
* Hello completo [Android introduttiva].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Creare un progetto che supporta Google Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurare le notifiche push toosend Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Abilitare le notifiche push per il progetto server hello
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Aggiungere app tooyour di notifiche push
In questa sezione aggiornare le notifiche di push client toohandle app Android.

### <a name="verify-android-sdk-version"></a>Verificare la versione di Android SDK
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

Il passaggio successivo è tooinstall Google Play services. Google Cloud Messaging è alcuni requisiti del livello minimi API per lo sviluppo e test, quali hello **minSdkVersion** proprietà nel manifesto hello devono essere conformi alle.

Se si sta testando con un dispositivo meno recente, consultare [impostare backup di Google Play Services SDK] toodetermine bassa come è possibile impostare questo valore e impostarlo in modo appropriato.

### <a name="add-google-play-services-toohello-project"></a>Aggiungi progetto toohello di Google Play services
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Aggiungere codice
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Test app hello contro hello pubblicati servizio mobile
È possibile testare app hello, collegando direttamente un telefono Android tramite un cavo USB o un dispositivo virtuale nell'emulatore hello.

## <a name="next-steps"></a>Passaggi successivi
Ora che è stata completata questa esercitazione, è consigliabile continuare su tooone di hello seguenti esercitazioni:

* [Aggiungere app Android di autenticazione tooyour](app-service-mobile-android-get-started-users.md).
  Informazioni su come progetto di tooadd autenticazione toohello todolist delle Guide rapide in Android usando un provider di identità supportati.
* [Attivare la sincronizzazione offline per l'app Android](app-service-mobile-android-get-started-offline-data.md).
  Informazioni su come offline tooadd supportano tooyour app con un back-end App per dispositivi mobili. Con la sincronizzazione offline è possibile interagire con un'app per dispositivi mobili &mdash;visualizzando, aggiungendo e modificando i dati&mdash; anche quando non è disponibile una connessione di rete.

<!-- URLs -->
[Android introduttiva]: app-service-mobile-android-get-started.md

[impostare backup di Google Play Services SDK]:https://developers.google.com/android/guides/setup (Configurare Google Play Services SDK)
