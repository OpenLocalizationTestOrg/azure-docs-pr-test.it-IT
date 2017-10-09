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
## <a name="create-an-application-express"></a><span data-ttu-id="8825e-103">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="8825e-103">Create an application (Express)</span></span>
<span data-ttu-id="8825e-104">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="8825e-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="8825e-105">Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="8825e-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="8825e-106">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="8825e-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="8825e-107">Verificare che sia selezionata l'opzione hello per l'installazione guidata</span><span class="sxs-lookup"><span data-stu-id="8825e-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="8825e-108">Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice</span><span class="sxs-lookup"><span data-stu-id="8825e-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="8825e-109">Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)</span><span class="sxs-lookup"><span data-stu-id="8825e-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="8825e-110">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="8825e-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="8825e-111">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione</span><span class="sxs-lookup"><span data-stu-id="8825e-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="8825e-112">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="8825e-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="8825e-113">Verificare che l'opzione hello per l'installazione guidata non è selezionata</span><span class="sxs-lookup"><span data-stu-id="8825e-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="8825e-114">Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="8825e-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="8825e-115">Aprire `MainActivity` (in `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="8825e-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="8825e-116">Sostituire hello *[Immettere un'applicazione hello Id qui]* nella riga hello a partire da `final static String CLIENT_ID` con ID applicazione hello appena registrato:</span><span class="sxs-lookup"><span data-stu-id="8825e-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="8825e-117">Aprire `AndroidManifest.xml` (in `app`  >  `manifests`) hello Aggiungi seguenti attività troppo`manifest\application` nodo.</span><span class="sxs-lookup"><span data-stu-id="8825e-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="8825e-118">Viene registrato un `BrowserTabActivity` tooallow hello tooresume del sistema operativo all'applicazione dopo il completamento dell'autenticazione hello:</span><span class="sxs-lookup"><span data-stu-id="8825e-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="8825e-119">In hello `BrowserTabActivity`, sostituire `[Enter hello application Id here]` con l'ID applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8825e-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
