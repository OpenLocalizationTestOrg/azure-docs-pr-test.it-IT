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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="be544-103">Aggiungere app tooyour informazioni di registrazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="be544-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="be544-104">In questo passaggio, è necessario tooadd hello Client ID tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="be544-104">In this step, you need tooadd hello Client ID tooyour project.</span></span>

1.  <span data-ttu-id="be544-105">Aprire `MainActivity` (in `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="be544-105">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
2.  <span data-ttu-id="be544-106">Sostituire a partire dalla riga di hello `final static String CLIENT_ID` con:</span><span class="sxs-lookup"><span data-stu-id="be544-106">Replace hello line starting with `final static String CLIENT_ID` with:</span></span>
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. <span data-ttu-id="be544-107">Aprire: `app` > `manifests` > `AndroidManifest.xml`</span><span class="sxs-lookup"><span data-stu-id="be544-107">Open: `app` > `manifests` > `AndroidManifest.xml`</span></span>
4. <span data-ttu-id="be544-108">Aggiungere hello seguenti attività troppo`manifest\application` nodo.</span><span class="sxs-lookup"><span data-stu-id="be544-108">Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="be544-109">Questo registro un `BrowserTabActivity` tooallow hello tooresume del sistema operativo all'applicazione dopo il completamento dell'autenticazione hello:</span><span class="sxs-lookup"><span data-stu-id="be544-109">This register a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>

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

### <a name="what-is-next"></a><span data-ttu-id="be544-110">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="be544-110">What is Next</span></span>

[<span data-ttu-id="be544-111">Test e convalida</span><span class="sxs-lookup"><span data-stu-id="be544-111">Test and Validate</span></span>](active-directory-mobileanddesktopapp-android-test.md)
