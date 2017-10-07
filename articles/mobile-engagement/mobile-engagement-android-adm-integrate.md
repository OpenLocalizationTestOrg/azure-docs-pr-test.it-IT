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
# <a name="how-toointegrate-adm-with-engagement"></a>Come tooIntegrate ADM con Engagement
> [!IMPORTANT]
> È necessario seguire una procedura di integrazione hello descritta in hello come tooIntegrate Engagement in Android documento prima di seguire questa Guida.
> 
> Questo documento è utile solo se già integrato hello Reach modulo e piano toopush Amazon dispositivi. campagne di copertura toointegrate nell'applicazione, leggere prima come tooIntegrate copertura di Engagement in Android.
> 
> 

## <a name="introduction"></a>Introduzione
L'integrazione ADM consente toobe l'applicazione inserita quando destinate a dispositivi Android Amazon.

Payload ADM inserito toohello SDK sempre contenere hello `azme` chiave nell'oggetto dati hello. Pertanto se si usa ADM per uno scopo diverso nell'applicazione, è possibile filtrare le notifiche push in base a tale chiave.

> [!IMPORTANT]
> Solo i dispositivi Amazon Kindle che eseguono Android 4.0.3 o versioni successive sono supportati da Amazon Device Messaging. È comunque possibile integrare questo codice in modo sicuro in altri dispositivi.
> 
> 

## <a name="sign-up-tooadm"></a>Effettuare l'iscrizione tooADM
Se questa operazione non è già stata eseguita, è necessario abilitare ADM nel proprio account Amazon.

procedura Hello è descritta in: [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Al termine dell'esecuzione di stored procedure di hello, viene visualizzato:

* OAuth credenziali (un ID Client e un segreto Client) per toopush in grado di Engagement toobe i dispositivi.
* Una chiave API che deve essere integrata nell'applicazione.

## <a name="sdk-integration"></a>Integrazione dell'SDK
### <a name="managing-device-registrations"></a>Gestione delle registrazioni dei dispositivi
Ogni dispositivo deve inviare un toohello di comando di registrazione server ADM, in caso contrario non è raggiungibile.

Se si usa già hello [libreria client ADM]e dispone già di [integrato ADM] è possibile passare direttamente tooandroid-sdk-adm-ricezione.

Se non è stata integrata ADM, Engagement ha un tooenable modo più semplice che nell'applicazione:

Modificare il file `AndroidManifest.xml`:

* Aggiungere hello Amazon dello spazio dei nomi, file hello deve iniziare simile al seguente:
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* Inside hello `<application/>` tag, aggiungere in questa sezione:
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Dopo aver aggiunto il tag di amazon hello, è possibile che un errore di compilazione se la destinazione di compilazione del progetto è di sotto di Android 2.1. Si dispone di toouse un **Android 2.1 +** compilazione destinazione (non preoccuparti, perché è ancora possibile avere un `minSdkVersion` impostare too4).
* Integrare hello chiave API ADM come asset seguendo [questa procedura].

Seguire quindi hello istruzioni delle sezioni Avanti hello.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Comunicare il servizio registrazione id toohello Engagement Push e ricevere le notifiche
In ordine toocommunicate hello identificativo di hello dispositivo toohello Engagement Push del servizio e ricevere le notifiche, aggiungere hello seguente tooyour `AndroidManifest.xml` file, all'interno di hello `<application/>` tag (anche se si utilizza ADM senza Engagement):

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

Verificare di aver hello queste autorizzazioni nel `AndroidManifest.xml` (prima hello `</application>` tag).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Concedere le credenziali OAuth di Engagement
Inviare le credenziali OAuth (ID client e Segreto client) al portale di Engagement.

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[libreria client ADM]:https://developer.amazon.com/sdk/adm/setup.html
[integrato ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[questa procedura]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
