---
title: aaaAzure AD v2 Windows Desktop Getting Started - Config | Documenti Microsoft
description: "Come un'applicazione .NET per Windows Desktop (XAML) può ottenere un token di accesso e chiamare un'API protetta dall'endpoint di Azure Active Directory v2."
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="c8c0d-103">Aggiungere app tooyour informazioni di registrazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c8c0d-103">Add hello application’s registration information tooyour app</span></span>
<span data-ttu-id="c8c0d-104">In questo passaggio, è necessario tooadd hello Id applicazione tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="c8c0d-104">In this step, you need tooadd hello Application Id tooyour project.</span></span>

1.  <span data-ttu-id="c8c0d-105">Aprire `App.xaml.cs` e sostituire riga hello contenente hello `ClientId` con:</span><span class="sxs-lookup"><span data-stu-id="c8c0d-105">Open `App.xaml.cs` and replace hello line containing hello `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="c8c0d-106">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c8c0d-106">What is Next</span></span>

[<span data-ttu-id="c8c0d-107">Test e convalida</span><span class="sxs-lookup"><span data-stu-id="c8c0d-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
