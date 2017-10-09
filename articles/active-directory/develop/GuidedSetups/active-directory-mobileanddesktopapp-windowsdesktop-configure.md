---
title: aaaAzure AD v2 Windows Desktop Getting Started - Config | Documenti Microsoft
description: "Come un'applicazione .NET per Windows Desktop (XAML) può ottenere un token di accesso e chiamare un'API protetta dall'endpoint di Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Creare un'applicazione (Rapida)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Immettere un nome per l'applicazione e l'indirizzo di posta elettronica
3.  Verificare che sia selezionata l'opzione hello per l'installazione guidata
4.  Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)
Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:
1. Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione
2. Immettere un nome per l'applicazione e l'indirizzo di posta elettronica 
3. Verificare che l'opzione hello per l'installazione guidata non è selezionata
4. Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su Salva
5. Copiare hello GUID in ID applicazione, tornare indietro tooVisual Studio, aprire `App.xaml.cs` e sostituire `your_client_id_here` con hello ID applicazione appena registrato:

```csharp
private static string ClientId = "your_application_id_here";
```
