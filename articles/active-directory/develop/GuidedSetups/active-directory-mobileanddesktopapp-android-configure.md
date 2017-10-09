---
title: 'v2 aaaAzure AD Android Guida introduttiva: configurare | Documenti Microsoft'
description: "Informazioni sul modo in cui un'app di Android può ottenere un token di accesso e chiamare l'API o le API Graph Microsoft che richiedono token di acceso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creare un'applicazione (Rapida)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Verificare che sia selezionata l'opzione hello per l'installazione guidata
4.  Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione
2. Immettere un nome per l'applicazione e l'indirizzo di posta elettronica 
3. Verificare che l'opzione hello per l'installazione guidata non è selezionata
4. Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su Salva
5.  Aprire `MainActivity` (in `app` > `java` > *`{host}.{namespace}`*)
6.  Sostituire hello *[Immettere un'applicazione hello Id qui]* nella riga hello a partire da `final static String CLIENT_ID` con ID applicazione hello appena registrato:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Aprire `AndroidManifest.xml` (in `app`  >  `manifests`) hello Aggiungi seguenti attività troppo`manifest\application` nodo. Viene registrato un `BrowserTabActivity` tooallow hello tooresume del sistema operativo all'applicazione dopo il completamento dell'autenticazione hello:
</li>
</ol>

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
In hello `BrowserTabActivity`, sostituire `[Enter hello application Id here]` con l'ID applicazione hello.
</li>
</ol>
