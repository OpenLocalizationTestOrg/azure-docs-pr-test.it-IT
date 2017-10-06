---
title: aaaAzure integrazione SDK Android di Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Come tooIntegrate GCM con Engagement Mobile
> [!IMPORTANT]
> È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.
> 
> Questo documento è utile solo se è già integrata hello raggiunga toopush modulo e piano di Google Play i dispositivi. campagne di copertura toointegrate nell'applicazione, leggere prima come tooIntegrate copertura di Engagement in Android.
> 
> 

## <a name="introduction"></a>Introduzione
L'integrazione GCM consente l'applicazione toobe inserito.

Payload GCM inserito toohello SDK sempre contenere hello `azme` chiave nell'oggetto dati hello. Pertanto se si usa GCM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.

> [!IMPORTANT]
> Solo i dispositivi che eseguono Android 2.2 o versioni successive, con Google Play installato e con la connessione a Google in background abilitata, possono essere riattivati da GCM. È comunque possibile integrare questo codice in modo sicuro in dispositivi non supportati (usa solo elementi di tipo Intent).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Creare un progetto Google Cloud Messaging con chiave API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Integrazione dell'SDK
### <a name="managing-device-registrations"></a>Gestione delle registrazioni dei dispositivi
Ogni dispositivo deve inviare un toohello di comando di registrazione server Google, in caso contrario non è raggiungibile.

Un dispositivo può anche annullare la registrazione delle notifiche GCM (dispositivo hello viene automaticamente annullata se viene disinstallata l'applicazione hello).

Se non si utilizza [Google Play SDK] o già è non inviare finalità registrazione hello, è possibile apportare Engagement registrazione dispositivo hello automatica per l'utente.

tooenable, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag:

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicare il servizio registrazione id toohello Engagement Push e ricevere le notifiche
In ordine toocommunicate hello identificativo di hello dispositivo toohello Engagement Push del servizio e ricevere le notifiche, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag (anche se si gestiscono le registrazioni dispositivo manualmente):

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

Verificare di aver hello queste autorizzazioni nel `AndroidManifest.xml` (dopo hello `</application>` tag).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Engagement Mobile concedere accesso tooyour chiave API GCM
Seguire [questa Guida](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Engagement Mobile access tooyour chiave API GCM.

[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start
