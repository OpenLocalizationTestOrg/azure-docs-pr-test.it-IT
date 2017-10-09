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
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Aggiungere app xamarin tooyour di notifiche push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Panoramica
In questa esercitazione, si aggiunge toohello le notifiche push [xamarin introduttiva](app-service-mobile-windows-store-dotnet-get-started.md) progetto in modo che il dispositivo toohello viene inviata una notifica di push ogni volta che viene inserito un record.

Se non si utilizza hello scaricato il progetto server di avvio rapido, si sarà necessario hello pacchetto estensione di notifica push. Vedere [funziona con server di back-end .NET hello SDK per App mobili di Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) per ulteriori informazioni.

## <a name="prerequisites"></a>Prerequisiti
Questa esercitazione richiede il seguente hello:

* Account Google attivo È possibile iscriversi a un account di Google in [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* [Componente client di Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/)

## <a name="configure-hub"></a>Configurare un hub di notifica
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Abilitare Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Configurare Azure toosend push richieste
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Aggiornare le notifiche push di hello server progetto toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Configurare il progetto client hello per le notifiche push
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Aggiungere app tooyour codice di notifiche push
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Testare le notifiche push nell'app
È possibile testare l'applicazione hello utilizzando un dispositivo virtuale nell'emulatore hello. Ci sono altri passaggi di configurazione richiesti durante l'esecuzione in un emulatore.

1. Assicurarsi che si sta distribuendo tooor debug in un dispositivo virtuale con Google APIs impostato come destinazione di hello, come illustrato di seguito nella console di gestione hello dispositivo virtuale Android (AVD).
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Aggiungere un dispositivo Android di Google account toohello facendo **app** > **impostazioni** > **aggiungere account**, seguire i prompt hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Eseguire l'applicazione hello come prima e inserire un nuovo elemento di attività. Questa volta, viene visualizzata un'icona di notifica nell'area di notifica hello. È possibile aprire hello notifica cassetto tooview hello full-text della notifica hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
