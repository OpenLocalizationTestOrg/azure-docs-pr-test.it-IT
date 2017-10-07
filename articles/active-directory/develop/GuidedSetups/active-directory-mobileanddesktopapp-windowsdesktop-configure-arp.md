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
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Aggiungere app tooyour informazioni di registrazione dell'applicazione hello
In questo passaggio, è necessario tooadd hello Id applicazione tooyour progetto.

1.  Aprire `App.xaml.cs` e sostituire riga hello contenente hello `ClientId` con:

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>Passaggi successivi

[Test e convalida](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
