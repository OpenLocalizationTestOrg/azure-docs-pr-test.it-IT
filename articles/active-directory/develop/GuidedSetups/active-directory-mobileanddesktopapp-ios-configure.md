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
## <a name="create-an-application-express"></a>Creare un'applicazione (Rapida)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Verificare che sia selezionata l'opzione hello per l'installazione guidata
4.  Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)

1.  Andare troppo[portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Verificare che l'opzione hello per l'installazione guidata non è selezionata
4.  Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su `Save`
5.  Tornare tooXcode. In `ViewController.swift`, sostituire riga hello inizia con '`let kClientID`' con ID applicazione hello appena registrato:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
CTRL + clic <code>Info.plist</code> toobring alto dal menu di scelta rapida hello e quindi fare clic su: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
In hello <code>dict</code> nodo principale, aggiungere hello seguenti:
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
Sostituire <i> <code>[Your_Application_Id_Here]</code> </i> con hello Id applicazione appena registrato
</li>
</ol>
