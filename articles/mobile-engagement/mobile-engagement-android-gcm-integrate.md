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
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a><span data-ttu-id="2fefa-103">Come tooIntegrate GCM con Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="2fefa-103">How tooIntegrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="2fefa-104">È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="2fefa-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="2fefa-105">Questo documento è utile solo se è già integrata hello raggiunga toopush modulo e piano di Google Play i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="2fefa-105">This document is useful only if you already integrated hello Reach module and plan toopush Google Play devices.</span></span> <span data-ttu-id="2fefa-106">campagne di copertura toointegrate nell'applicazione, leggere prima come tooIntegrate copertura di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="2fefa-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="2fefa-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="2fefa-107">Introduction</span></span>
<span data-ttu-id="2fefa-108">L'integrazione GCM consente l'applicazione toobe inserito.</span><span class="sxs-lookup"><span data-stu-id="2fefa-108">Integrating GCM allows your application toobe pushed.</span></span>

<span data-ttu-id="2fefa-109">Payload GCM inserito toohello SDK sempre contenere hello `azme` chiave nell'oggetto dati hello.</span><span class="sxs-lookup"><span data-stu-id="2fefa-109">GCM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="2fefa-110">Pertanto se si usa GCM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="2fefa-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fefa-111">Solo i dispositivi che eseguono Android 2.2 o versioni successive, con Google Play installato e con la connessione a Google in background abilitata, possono essere riattivati da GCM. È comunque possibile integrare questo codice in modo sicuro in dispositivi non supportati (usa solo elementi di tipo Intent).</span><span class="sxs-lookup"><span data-stu-id="2fefa-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="2fefa-112">Creare un progetto Google Cloud Messaging con chiave API</span><span class="sxs-lookup"><span data-stu-id="2fefa-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="2fefa-113">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="2fefa-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="2fefa-114">Gestione delle registrazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="2fefa-114">Managing device registrations</span></span>
<span data-ttu-id="2fefa-115">Ogni dispositivo deve inviare un toohello di comando di registrazione server Google, in caso contrario non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="2fefa-115">Each device must send a registration command toohello Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="2fefa-116">Un dispositivo può anche annullare la registrazione delle notifiche GCM (dispositivo hello viene automaticamente annullata se viene disinstallata l'applicazione hello).</span><span class="sxs-lookup"><span data-stu-id="2fefa-116">A device can also unregister from GCM notifications (hello device is automatically unregistered if hello application is uninstalled).</span></span>

<span data-ttu-id="2fefa-117">Se non si utilizza [Google Play SDK] o già è non inviare finalità registrazione hello, è possibile apportare Engagement registrazione dispositivo hello automatica per l'utente.</span><span class="sxs-lookup"><span data-stu-id="2fefa-117">If you don't use [Google Play SDK] or you don't already send hello registration intent yourself, you can make Engagement register hello device automatically for you.</span></span>

<span data-ttu-id="2fefa-118">tooenable, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag:</span><span class="sxs-lookup"><span data-stu-id="2fefa-118">tooenable this, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="2fefa-119">Comunicare il servizio registrazione id toohello Engagement Push e ricevere le notifiche</span><span class="sxs-lookup"><span data-stu-id="2fefa-119">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="2fefa-120">In ordine toocommunicate hello identificativo di hello dispositivo toohello Engagement Push del servizio e ricevere le notifiche, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag (anche se si gestiscono le registrazioni dispositivo manualmente):</span><span class="sxs-lookup"><span data-stu-id="2fefa-120">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="2fefa-121">Verificare di aver hello queste autorizzazioni nel `AndroidManifest.xml` (dopo hello `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="2fefa-121">Ensure you have hello following permissions in your `AndroidManifest.xml` (after hello `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="2fefa-122">Engagement Mobile concedere accesso tooyour chiave API GCM</span><span class="sxs-lookup"><span data-stu-id="2fefa-122">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="2fefa-123">Seguire [questa Guida](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Engagement Mobile access tooyour chiave API GCM.</span><span class="sxs-lookup"><span data-stu-id="2fefa-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement access tooyour GCM API Key.</span></span>

[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start
