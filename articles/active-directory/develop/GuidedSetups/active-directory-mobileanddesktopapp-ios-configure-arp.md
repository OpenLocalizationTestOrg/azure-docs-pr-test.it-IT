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
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="33998-103">Aggiungere app tooyour informazioni di registrazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="33998-103">Add hello application’s registration information tooyour app</span></span>

<span data-ttu-id="33998-104">In questo passaggio, è necessario tooadd hello Id applicazione tooyour progetto:</span><span class="sxs-lookup"><span data-stu-id="33998-104">In this step, you need tooadd hello Application Id tooyour project:</span></span>

1.  <span data-ttu-id="33998-105">In `ViewController.swift`, sostituire riga hello inizia con '`let kClientID`' con:</span><span class="sxs-lookup"><span data-stu-id="33998-105">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter hello application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="33998-106">CTRL + clic <code>Info.plist</code> toobring alto dal menu di scelta rapida hello e quindi fare clic su: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="33998-106">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="33998-107">In hello <code>dict</code> nodo principale, aggiungere hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="33998-107">Under hello <code>dict</code> root node, add hello following:</span></span>
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
