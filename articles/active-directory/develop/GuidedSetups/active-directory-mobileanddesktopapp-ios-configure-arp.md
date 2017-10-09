---
title: iOS v2 aaaAzure AD Getting Started - configurare ARP () | Documenti Microsoft
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
ms.openlocfilehash: e5087e13160243d808b1d02771fa66fb332cfad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Aggiungere app tooyour informazioni di registrazione dell'applicazione hello

In questo passaggio, è necessario tooadd hello Id applicazione tooyour progetto:

1.  In `ViewController.swift`, sostituire riga hello inizia con '`let kClientID`' con:
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
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
            <string>msal[Enter hello application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
