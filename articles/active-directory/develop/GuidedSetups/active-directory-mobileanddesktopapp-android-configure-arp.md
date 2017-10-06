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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Aggiungere app tooyour informazioni di registrazione dell'applicazione hello

In questo passaggio, è necessario tooadd hello Client ID tooyour progetto.

1.  Aprire `MainActivity` (in `app` > `java` > *`{host}.{namespace}`*)
2.  Sostituire a partire dalla riga di hello `final static String CLIENT_ID` con:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Aprire: `app` > `manifests` > `AndroidManifest.xml`
4. Aggiungere hello seguenti attività troppo`manifest\application` nodo. Questo registro un `BrowserTabActivity` tooallow hello tooresume del sistema operativo all'applicazione dopo il completamento dell'autenticazione hello:

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

### <a name="what-is-next"></a>Passaggi successivi

[Test e convalida](active-directory-mobileanddesktopapp-android-test.md)
