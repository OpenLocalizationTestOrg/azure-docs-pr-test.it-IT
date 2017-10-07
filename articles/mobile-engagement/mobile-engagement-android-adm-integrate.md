---
title: aaaAzure integrazione SDK Android di Mobile Engagement
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
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a><span data-ttu-id="11ccb-103">Come tooIntegrate ADM con Engagement</span><span class="sxs-lookup"><span data-stu-id="11ccb-103">How tooIntegrate ADM with Engagement</span></span>
> [!IMPORTANT]
> <span data-ttu-id="11ccb-104">È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.</span><span class="sxs-lookup"><span data-stu-id="11ccb-104">You must follow hello integration procedure described in hello How tooIntegrate Engagement on Android document before following this guide.</span></span>
> 
> <span data-ttu-id="11ccb-105">Questo documento è utile solo se già integrato hello Reach modulo e piano toopush Amazon dispositivi.</span><span class="sxs-lookup"><span data-stu-id="11ccb-105">This document is useful only if you already integrated hello Reach module and plan toopush Amazon devices.</span></span> <span data-ttu-id="11ccb-106">campagne di copertura toointegrate nell'applicazione, leggere prima come tooIntegrate copertura di Engagement in Android.</span><span class="sxs-lookup"><span data-stu-id="11ccb-106">toointegrate Reach campaigns in your application, please read first How tooIntegrate Engagement Reach on Android.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="11ccb-107">Introduzione</span><span class="sxs-lookup"><span data-stu-id="11ccb-107">Introduction</span></span>
<span data-ttu-id="11ccb-108">L'integrazione ADM consente toobe l'applicazione inserita quando destinate a dispositivi Android Amazon.</span><span class="sxs-lookup"><span data-stu-id="11ccb-108">Integrating ADM allows your application toobe pushed when targeting Amazon Android devices.</span></span>

<span data-ttu-id="11ccb-109">Payload ADM inserito toohello SDK sempre contenere hello `azme` chiave nell'oggetto dati hello.</span><span class="sxs-lookup"><span data-stu-id="11ccb-109">ADM payloads pushed toohello SDK always contain hello `azme` key in hello data object.</span></span> <span data-ttu-id="11ccb-110">Pertanto se si usa ADM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.</span><span class="sxs-lookup"><span data-stu-id="11ccb-110">Thus if you use ADM for another purpose in your application, you can filter pushes based on that key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11ccb-111">Solo i dispositivi Amazon Kindle che eseguono Android 4.0.3 o versioni successive sono supportati da Amazon Device Messaging. È comunque possibile integrare questo codice in modo sicuro in altri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="11ccb-111">Only Amazon Kindle devices running Android 4.0.3 or above are supported by Amazon Device Messaging; however, you can integrate this code safely on other devices.</span></span>
> 
> 

## <a name="sign-up-tooadm"></a><span data-ttu-id="11ccb-112">Effettuare l'iscrizione tooADM</span><span class="sxs-lookup"><span data-stu-id="11ccb-112">Sign up tooADM</span></span>
<span data-ttu-id="11ccb-113">Se questa operazione non è già stata eseguita, è necessario abilitare ADM nel proprio account Amazon.</span><span class="sxs-lookup"><span data-stu-id="11ccb-113">If not already done, you must enable ADM on your Amazon account.</span></span>

<span data-ttu-id="11ccb-114">procedura Hello è descritta in: [ <https://developer.amazon.com/sdk/adm/credentials.html>].</span><span class="sxs-lookup"><span data-stu-id="11ccb-114">hello procedure is detailed at: [<https://developer.amazon.com/sdk/adm/credentials.html>].</span></span>

<span data-ttu-id="11ccb-115">Al termine dell'esecuzione di stored procedure di hello, viene visualizzato:</span><span class="sxs-lookup"><span data-stu-id="11ccb-115">Upon completing hello procedure, you get:</span></span>

* <span data-ttu-id="11ccb-116">OAuth credenziali (un ID Client e un segreto Client) per toopush in grado di Engagement toobe i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="11ccb-116">OAuth credentials (a Client ID and a Client Secret) for Engagement toobe able toopush your devices.</span></span>
* <span data-ttu-id="11ccb-117">Una chiave API che deve essere integrata nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="11ccb-117">An API Key that must be integrated into your application.</span></span>

## <a name="sdk-integration"></a><span data-ttu-id="11ccb-118">Integrazione dell'SDK</span><span class="sxs-lookup"><span data-stu-id="11ccb-118">SDK integration</span></span>
### <a name="managing-device-registrations"></a><span data-ttu-id="11ccb-119">Gestione delle registrazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="11ccb-119">Managing device registrations</span></span>
<span data-ttu-id="11ccb-120">Ogni dispositivo deve inviare un toohello di comando di registrazione server ADM, in caso contrario non è raggiungibile.</span><span class="sxs-lookup"><span data-stu-id="11ccb-120">Each device must send a registration command toohello ADM servers, otherwise they can't be reached.</span></span>

<span data-ttu-id="11ccb-121">Se si usa già hello [libreria client ADM]e dispone già di [integrato ADM] è possibile passare direttamente tooandroid-sdk-adm-ricezione.</span><span class="sxs-lookup"><span data-stu-id="11ccb-121">If you already use hello [ADM client library], and already have [integrated ADM] you can directly go tooandroid-sdk-adm-receive.</span></span>

<span data-ttu-id="11ccb-122">Se non è stata integrata ADM, Engagement ha un tooenable modo più semplice che nell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="11ccb-122">If you have not integrated ADM yet, Engagement has a simpler way tooenable it in your application:</span></span>

<span data-ttu-id="11ccb-123">Modificare il file `AndroidManifest.xml`:</span><span class="sxs-lookup"><span data-stu-id="11ccb-123">Edit your `AndroidManifest.xml` file:</span></span>

* <span data-ttu-id="11ccb-124">Aggiungere hello Amazon dello spazio dei nomi, file hello deve iniziare simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="11ccb-124">Add hello Amazon namespace, hello file should begin like this:</span></span>
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* <span data-ttu-id="11ccb-125">Inside hello `<application/>` tag, aggiungere in questa sezione:</span><span class="sxs-lookup"><span data-stu-id="11ccb-125">Inside hello `<application/>` tag, add this section:</span></span>
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* <span data-ttu-id="11ccb-126">Dopo aver aggiunto il tag di amazon hello, è possibile che un errore di compilazione se la destinazione di compilazione del progetto è di sotto di Android 2.1.</span><span class="sxs-lookup"><span data-stu-id="11ccb-126">After adding hello amazon tag, you may have a build error if your Project Build Target is below Android 2.1.</span></span> <span data-ttu-id="11ccb-127">Si dispone di toouse un **Android 2.1 +** compilazione destinazione (non preoccuparti, perché è ancora possibile avere un `minSdkVersion` impostare too4).</span><span class="sxs-lookup"><span data-stu-id="11ccb-127">You have toouse an **Android 2.1+** build target (don't worry, you can still have a `minSdkVersion` set too4).</span></span>
* <span data-ttu-id="11ccb-128">Integrare hello chiave API ADM come asset seguendo [questa procedura].</span><span class="sxs-lookup"><span data-stu-id="11ccb-128">Integrate hello ADM API Key as an asset by following [this procedure].</span></span>

<span data-ttu-id="11ccb-129">Seguire quindi hello istruzioni delle sezioni Avanti hello.</span><span class="sxs-lookup"><span data-stu-id="11ccb-129">Then follow hello instructions of hello next sections.</span></span>

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a><span data-ttu-id="11ccb-130">Comunicare il servizio registrazione id toohello Engagement Push e ricevere le notifiche</span><span class="sxs-lookup"><span data-stu-id="11ccb-130">Communicate registration id toohello Engagement Push service and receive notifications</span></span>
<span data-ttu-id="11ccb-131">In ordine toocommunicate hello identificativo di hello dispositivo toohello Engagement Push del servizio e ricevere le notifiche, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag (anche se si utilizza ADM senza Engagement):</span><span class="sxs-lookup"><span data-stu-id="11ccb-131">In order toocommunicate hello registration id of hello device toohello Engagement Push service and receive its notifications, add hello following tooyour `AndroidManifest.xml` file, inside hello `<application/>` tag (even if you use ADM without Engagement):</span></span>

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

<span data-ttu-id="11ccb-132">Verificare di aver hello queste autorizzazioni nel `AndroidManifest.xml` (prima hello `</application>` tag).</span><span class="sxs-lookup"><span data-stu-id="11ccb-132">Ensure you have hello following permissions in your `AndroidManifest.xml` (before hello `</application>` tag).</span></span>

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a><span data-ttu-id="11ccb-133">Concedere le credenziali OAuth di Engagement</span><span class="sxs-lookup"><span data-stu-id="11ccb-133">Grant Engagement OAuth credentials</span></span>
<span data-ttu-id="11ccb-134">Inviare le credenziali OAuth (ID client e Segreto client) al portale di Engagement.</span><span class="sxs-lookup"><span data-stu-id="11ccb-134">Submit your OAuth Credentials (Client ID and Client Secret) in Engagement Portal.</span></span>

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[libreria client ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrato ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[questa procedura]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
