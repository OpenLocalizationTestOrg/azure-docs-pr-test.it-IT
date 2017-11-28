---
title: Introduzione ad Android per Azure AD v2 - Configurazione | Microsoft Docs
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
ms.openlocfilehash: 945b09ccdb7537987da33d32d94a3ccacd829ffd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="84a22-103">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="84a22-103">Create an application (Express)</span></span>
<span data-ttu-id="84a22-104">È ora necessario registrare l'applicazione nel *portale di registrazione delle applicazioni Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="84a22-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="84a22-105">Registrare l'applicazione tramite il [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="84a22-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="84a22-106">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="84a22-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="84a22-107">Assicurarsi che l'opzione per l'installazione guidata sia selezionata</span><span class="sxs-lookup"><span data-stu-id="84a22-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="84a22-108">Seguire le istruzioni per ottenere l'ID dell'applicazione e incollarlo nel codice</span><span class="sxs-lookup"><span data-stu-id="84a22-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="84a22-109">Aggiungere le informazioni di registrazione dell'applicazione alla soluzione (Avanzata)</span><span class="sxs-lookup"><span data-stu-id="84a22-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="84a22-110">È ora necessario registrare l'applicazione nel *portale di registrazione delle applicazioni Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="84a22-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="84a22-111">Passare al [portale di registrazione delle applicazioni Microsoft](https://apps.dev.microsoft.com/portal/register-app) per registrare un'applicazione</span><span class="sxs-lookup"><span data-stu-id="84a22-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="84a22-112">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="84a22-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="84a22-113">Assicurarsi che l'opzione per l'installazione guidata sia deselezionata</span><span class="sxs-lookup"><span data-stu-id="84a22-113">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="84a22-114">Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="84a22-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="84a22-115">Aprire `MainActivity` (in `app` > `java` > *`{host}.{namespace}`*)</span><span class="sxs-lookup"><span data-stu-id="84a22-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="84a22-116">Sostituire *[Enter the application Id here]* nella riga che inizia con `final static String CLIENT_ID` con l'ID dell'applicazione appena registrata:</span><span class="sxs-lookup"><span data-stu-id="84a22-116">Replace the *[Enter the application Id here]* in the line starting with `final static String CLIENT_ID` with the application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="84a22-117">Aprire `AndroidManifest.xml` (in `app` > `manifests`). Aggiungere l'attività seguente al nodo `manifest\application`.</span><span class="sxs-lookup"><span data-stu-id="84a22-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="84a22-118">Verrà registrata un'attività `BrowserTabActivity` per consentire al sistema operativo di riavviare l'applicazione dopo il completamento dell'autenticazione:</span><span class="sxs-lookup"><span data-stu-id="84a22-118">This registers a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>
</li>
</ol>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="84a22-119">In `BrowserTabActivity` sostituire `[Enter the application Id here]` con l'ID dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="84a22-119">In the `BrowserTabActivity`, replace `[Enter the application Id here]` with the application ID.</span></span>
</li>
</ol>
