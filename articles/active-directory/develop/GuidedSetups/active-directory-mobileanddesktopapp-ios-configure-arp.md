---
title: 'Introduzione a iOS con Azure AD v2: configurazione (ARP) | Microsoft Docs'
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
ms.openlocfilehash: 50cb4a2803b6aebe8b39ec9fb02da2293c1065fa
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="d4b9f-103">Aggiungere le informazioni di registrazione dell'applicazione all'app</span><span class="sxs-lookup"><span data-stu-id="d4b9f-103">Add the application’s registration information to your app</span></span>

<span data-ttu-id="d4b9f-104">In questo passaggio è necessario aggiungere l'ID applicazione al progetto:</span><span class="sxs-lookup"><span data-stu-id="d4b9f-104">In this step, you need to add the Application Id to your project:</span></span>

1.  <span data-ttu-id="d4b9f-105">In `ViewController.swift` sostituire la riga che inizia con "`let kClientID`":</span><span class="sxs-lookup"><span data-stu-id="d4b9f-105">In `ViewController.swift`, replace the line starting with '`let kClientID`' with:</span></span>
```swift
let kClientID = "[Enter the application Id here]"
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="d4b9f-106">Digitale Control+ clic su <code>Info.plist</code> per visualizzare il menu di scelta rapida e quindi fare clic su: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="d4b9f-106">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="d4b9f-107">Sotto il nodo radice <code>dict</code> aggiungere quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d4b9f-107">Under the <code>dict</code> root node, add the following:</span></span>
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
            <string>msal[Enter the application Id here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
