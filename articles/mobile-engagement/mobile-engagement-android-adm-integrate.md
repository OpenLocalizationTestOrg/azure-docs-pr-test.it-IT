---
title: Integrazione di Android SDK per Azure Mobile Engagement
description: Ultimi aggiornamenti e procedure relativi ad Azure Mobile Engagement SDK per Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 43987962ea2b7b825b88643d18b4db65f1f1670e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-integrate-adm-with-engagement"></a><span data-ttu-id="b4b0f-103">Come integrare ADM con Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b4b0f-103">How to Integrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b4b0f-104">Prima di usare questa guida, è necessario eseguire la procedura di integrazione descritta nel documento relativo all'integrazione di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-104">You must follow the integration procedure described in the How to Integrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="b4b0f-105">Il documento è utile solo se è già stato integrato il modulo di copertura e si intende eseguire il push dei dispositivi Amazon.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-105">This document is useful only if you already integrated the Reach module and plan to push Amazon devices.</span></span> <span data-ttu-id="b4b0f-106">Per integrare le campagne Reach nell'applicazione, leggere prima l'articolo relativo all'integrazione del servizio Reach di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-106">To integrate Reach campaigns in your application, please read first How to Integrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="b4b0f-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="b4b0f-107">Introduction</span></span>
<span data-ttu-id="b4b0f-108">L'integrazione di ADM consente il push dell'applicazione quando è destinata a dispositivi Android Amazon.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-108">Integrating ADM allows your application to be pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="b4b0f-109">I payload ADM di cui viene eseguito il push sull’SDK contengono sempre la chiave `azme` nell'oggetto dati.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-109">ADM payloads pushed to the SDK always contain the `azme` key in the data object.</span></span> <span data-ttu-id="b4b0f-110">Pertanto se si usa ADM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4b0f-111">Solo i dispositivi Amazon Kindle che eseguono Android 4.0.3 o versioni successive sono supportati da Amazon Device Messaging. È comunque possibile integrare questo codice in modo sicuro in altri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-to-adm"></a><span data-ttu-id="b4b0f-112">Iscriversi ad ADM</span><span class="sxs-lookup"><span data-stu-id="b4b0f-112">Sign up to ADM</span></span>
<span data-ttu-id="b4b0f-113">Se questa operazione non è già stata eseguita, è necessario abilitare ADM nel proprio account Amazon.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="b4b0f-114">La procedura è descritta in dettaglio all'indirizzo: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="b4b0f-114">The procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="b4b0f-115">Dopo aver completato la procedura, si ottiene quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b4b0f-115">Upon completing the procedure, you get:</span></span>

* <span data-ttu-id="b4b0f-116">Le credenziali OAuth (ID e segreto client) che consentono a Engagement di eseguire il push dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-116">OAuth credentials (a Client ID and a Client Secret) for Engagement to be able to push your devices.</span></span>
* <span data-ttu-id="b4b0f-117">Una chiave API che deve essere integrata nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="b4b0f-118">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="b4b0f-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="b4b0f-119">Gestione delle registrazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="b4b0f-119">Managing device registrations</span></span>
<span data-ttu-id="b4b0f-120">Ogni dispositivo deve inviare un comando di registrazione ai server ADM; in caso contrario non saranno raggiungibili.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-120">Each device must send a registration command to the ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="b4b0f-121">Se si usa già la [libreria client ADM] e si è già [integrato ADM], è possibile passare direttamente ad android-sdk-adm-receive.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-121">If you already use the [ADM client library], and already have [integrated ADM] you can directly go to android-sdk-adm-receive.</span></span>

<span data-ttu-id="b4b0f-122">Se ADM non è stato ancora integrato, Engagement offre un modo più semplice per abilitarlo nell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="b4b0f-122">If you have not integrated ADM yet, Engagement has a simpler way to enable it in your application:</span></span>

<span data-ttu-id="b4b0f-123">Modificare il file `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="b4b0f-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="b4b0f-124">Aggiungere lo spazio dei nomi Amazon. Il file deve iniziare nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="b4b0f-124">Add the Amazon namespace, the file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="b4b0f-125">All'interno del tag `<application/>` aggiungere questa sezione:</span><span class="sxs-lookup"><span data-stu-id="b4b0f-125">Inside the `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="b4b0f-126">Dopo aver aggiunto il tag di Amazon, può verificarsi un errore di compilazione se come destinazione di compilazione del progetto è impostata una versione precedente Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-126">After adding the amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="b4b0f-127">È necessario usare una destinazione di compilazione **Android 2.1** o versione successiva, anche se è ancora possibile avere una proprietà `minSdkVersion` impostata su 4.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-127">You have to use an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set to 4).</span></span>
* <span data-ttu-id="b4b0f-128">Integrare la chiave API di ADM come asset seguendo [questa procedura].</span><span class="sxs-lookup"><span data-stu-id="b4b0f-128">Integrate the ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="b4b0f-129">Seguire quindi le istruzioni riportate nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-129">Then follow the instructions of the next sections.</span></span>

### <a name="communicate-registration-id-to-the-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="b4b0f-130">Comunicare l'ID di registrazione al servizio push di Engagement e ricevere le notifiche</span><span class="sxs-lookup"><span data-stu-id="b4b0f-130">Communicate registration id to the Engagement Push service and receive notifications</span></span>
<span data-ttu-id="b4b0f-131">Per comunicare l'ID di registrazione del dispositivo al servizio push di Engagement e ricevere le notifiche, aggiungere quanto segue al file `AndroidManifest.xml`, all'interno del tag `<application/>` (anche se si usa ADM senza Engagement):</span><span class="sxs-lookup"><span data-stu-id="b4b0f-131">In order to communicate the registration id of the device to the Engagement Push service and receive its notifications, add the following to your `AndroidManifest.xml` file, inside the `<application/>` tag (even if you use ADM without Engagement):</span></span>

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

<span data-ttu-id="b4b0f-132">Assicurarsi di avere le seguenti autorizzazioni nel file `AndroidManifest.xml` (prima del tag `</application>`).</span><span class="sxs-lookup"><span data-stu-id="b4b0f-132">Ensure you have the following permissions in your `AndroidManifest.xml` (before the `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="b4b0f-133">Concedere le credenziali OAuth di Engagement</span><span class="sxs-lookup"><span data-stu-id="b4b0f-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="b4b0f-134">Inviare le credenziali OAuth (ID client e Segreto client) al portale di Engagement.</span><span class="sxs-lookup"><span data-stu-id="b4b0f-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

<span data-ttu-id="b4b0f-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span><span class="sxs-lookup"><span data-stu-id="b4b0f-135">[<https://developer.amazon.com/sdk/adm/credentials.html>]:https://developer.amazon.com/sdk/adm/credentials.html</span></span>
<span data-ttu-id="b4b0f-136">[libreria client ADM]:https://developer.amazon.com/sdk/adm/setup.html</span><span class="sxs-lookup"><span data-stu-id="b4b0f-136">[ADM client library]:https://developer.amazon.com/sdk/adm/setup.html</span></span>
<span data-ttu-id="b4b0f-137">[integrato ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span><span class="sxs-lookup"><span data-stu-id="b4b0f-137">[integrated ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html</span></span>
<span data-ttu-id="b4b0f-138">[questa procedura]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span><span class="sxs-lookup"><span data-stu-id="b4b0f-138">[this procedure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset</span></span>
