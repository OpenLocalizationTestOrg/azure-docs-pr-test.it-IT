---
title: 'Guida introduttiva di aaaAzure AD v2 iOS: configurare | Documenti Microsoft'
description: "Informazioni sulle modalità per le applicazioni iOS (Swift) per chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="ec77f-103">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="ec77f-103">Create an application (Express)</span></span>
<span data-ttu-id="ec77f-104">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="ec77f-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="ec77f-105">Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="ec77f-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="ec77f-106">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ec77f-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ec77f-107">Verificare che sia selezionata l'opzione hello per l'installazione guidata</span><span class="sxs-lookup"><span data-stu-id="ec77f-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="ec77f-108">Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice</span><span class="sxs-lookup"><span data-stu-id="ec77f-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="ec77f-109">Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)</span><span class="sxs-lookup"><span data-stu-id="ec77f-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="ec77f-110">Andare troppo[portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="ec77f-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="ec77f-111">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="ec77f-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="ec77f-112">Verificare che l'opzione hello per l'installazione guidata non è selezionata</span><span class="sxs-lookup"><span data-stu-id="ec77f-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="ec77f-113">Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su `Save`</span><span class="sxs-lookup"><span data-stu-id="ec77f-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="ec77f-114">Tornare tooXcode.</span><span class="sxs-lookup"><span data-stu-id="ec77f-114">Go back tooXcode.</span></span> <span data-ttu-id="ec77f-115">In `ViewController.swift`, sostituire riga hello inizia con '`let kClientID`' con ID applicazione hello appena registrato:</span><span class="sxs-lookup"><span data-stu-id="ec77f-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="ec77f-116">CTRL + clic <code>Info.plist</code> toobring alto dal menu di scelta rapida hello e quindi fare clic su: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="ec77f-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="ec77f-117">In hello <code>dict</code> nodo principale, aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="ec77f-117">Under hello <code>dict</code> root node, add hello following:</span></span>
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
<span data-ttu-id="ec77f-118">Sostituire <i> <code>[Your_Application_Id_Here]</code> </i> con hello Id applicazione appena registrato</span><span class="sxs-lookup"><span data-stu-id="ec77f-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
