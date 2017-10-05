---
title: Integrazione di Android SDK per Azure Mobile Engagement
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
ms.openlocfilehash: 0282abbf44406cac89c13520bc2a4e375817ed1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-gcm-with-mobile-engagement"></a><span data-ttu-id="1f3e8-103">Come integrare GCM con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1f3e8-103">How to Integrate GCM with Mobile Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1f3e8-104">Prima di usare questa guida, è necessario eseguire la procedura di integrazione descritta nel documento relativo all'integrazione di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="1f3e8-105">Il documento è utile solo se è già stato integrato il modulo di copertura e si intende eseguire il push dei dispositivi Google Play.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-105">This document is useful only if you already integrated the Reach module and plan to push Google Play devices.</span></span> <span data-ttu-id="1f3e8-106">Per integrare le campagne Reach nell'applicazione, leggere prima l'articolo relativo all'integrazione del servizio Reach di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="1f3e8-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="1f3e8-107">Introduction</span></span>
<span data-ttu-id="1f3e8-108">L'integrazione di GCM consente il push dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-108">Integrating GCM allows your application to be pushed.</span></span>

<span data-ttu-id="1f3e8-109">I payload GCM di cui viene eseguito il push sull’SDK contengono sempre la chiave `azme` nell'oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-109">GCM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="1f3e8-110">Pertanto se si usa GCM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-110">Thus if you use GCM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f3e8-111">Solo i dispositivi che eseguono Android 2.2 o versioni successive, con Google Play installato e con la connessione a Google in background abilitata, possono essere riattivati da GCM. È comunque possibile integrare questo codice in modo sicuro in dispositivi non supportati (usa solo elementi di tipo Intent).</span><span class="sxs-lookup"><span data-stu-id="1f3e8-111">Only devices running Android 2.2 or above, having Google Play installed and having Google background connection enabled can be pushed using GCM; however, you can integrate this code safely on unsupported devices (it just uses intents).</span></span>
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a><span data-ttu-id="1f3e8-112">Creare un progetto Google Cloud Messaging con chiave API</span><span class="sxs-lookup"><span data-stu-id="1f3e8-112">Create a Google Cloud Messaging project with API key</span></span>
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a><span data-ttu-id="1f3e8-113">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="1f3e8-113">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="1f3e8-114">Gestione delle registrazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="1f3e8-114">Managing device registrations</span></span>
<span data-ttu-id="1f3e8-115">Ogni dispositivo deve inviare un comando di registrazione ai server Google; in caso contrario non sarà raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-115">Each device must send a registration command to the Google servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="1f3e8-116">Un dispositivo può anche annullare la registrazione alle notifiche GCM (la registrazione del dispositivo viene annullata automaticamente se l'applicazione viene disinstallata).</span><span class="sxs-lookup"><span data-stu-id="1f3e8-116">A device can also unregister from GCM notifications (the device is automatically unregistered if the application is uninstalled).</span></span>

<span data-ttu-id="1f3e8-117">Se non si usa [Google Play SDK] oppure se l'Intent di registrazione non viene inviato manualmente, è possibile fare in modo che Engagement registri automaticamente il dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-117">If you don't use [Google Play SDK] or you don't already send the registration intent yourself, you can make Engagement register the device automatically for you.</span></span>

<span data-ttu-id="1f3e8-118">Per abilitare questa funzionalità, aggiungere il codice seguente nel file `AndroidManifest.xml`, all'interno del tag `<application/>`:</span><span class="sxs-lookup"><span data-stu-id="1f3e8-118">To enable this, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag:</span></span>

            <!-- If only 1 sender, don't forget the \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="1f3e8-119">Comunicare l'ID di registrazione al servizio push di Engagement e ricevere le notifiche</span><span class="sxs-lookup"><span data-stu-id="1f3e8-119">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="1f3e8-120">Per comunicare l'ID di registrazione del dispositivo al servizio push di Engagement e ricevere le relative notifiche, aggiungere quanto segue al file `AndroidManifest.xml`, all'interno del tag `<application/>` (anche se si gestiscono autonomamente le registrazioni dei dispositivi):</span><span class="sxs-lookup"><span data-stu-id="1f3e8-120">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you manage device registrations yourself):</span></span>

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

<span data-ttu-id="1f3e8-121">Assicurarsi di avere le seguenti autorizzazioni nel file `AndroidManifest.xml` (dopo il tag `</application>`).</span><span class="sxs-lookup"><span data-stu-id="1f3e8-121">Ensure you have the following permissions in your `AndroidManifest.xml` (after the `</application>` tag).</span></span>

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-to-your-gcm-api-key"></a><span data-ttu-id="1f3e8-122">Concedere a Mobile Engagement l'accesso alla chiave API GCM</span><span class="sxs-lookup"><span data-stu-id="1f3e8-122">Grant Mobile Engagement access to your GCM API Key</span></span>
<span data-ttu-id="1f3e8-123">Seguire [questa guida](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) per concedere a Mobile Engagement l'accesso alla chiave API GCM.</span><span class="sxs-lookup"><span data-stu-id="1f3e8-123">Follow [this guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) to grant Mobile Engagement access to your GCM API Key.</span></span>

<span data-ttu-id="1f3e8-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span><span class="sxs-lookup"><span data-stu-id="1f3e8-124">[Google Play SDK]:https://developers.google.com/cloud-messaging/android/start</span></span>
