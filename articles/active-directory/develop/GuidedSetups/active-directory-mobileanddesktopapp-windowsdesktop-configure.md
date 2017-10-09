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
## <a name="create-an-application-express"></a><span data-ttu-id="0602d-104">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="0602d-104">Create an application (Express)</span></span>
<span data-ttu-id="0602d-105">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="0602d-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="0602d-106">Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="0602d-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="0602d-107">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="0602d-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="0602d-108">Verificare che sia selezionata l'opzione hello per l'installazione guidata</span><span class="sxs-lookup"><span data-stu-id="0602d-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="0602d-109">Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice</span><span class="sxs-lookup"><span data-stu-id="0602d-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="0602d-110">Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)</span><span class="sxs-lookup"><span data-stu-id="0602d-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="0602d-111">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="0602d-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="0602d-112">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione</span><span class="sxs-lookup"><span data-stu-id="0602d-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="0602d-113">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="0602d-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="0602d-114">Verificare che l'opzione hello per l'installazione guidata non è selezionata</span><span class="sxs-lookup"><span data-stu-id="0602d-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="0602d-115">Fare clic su `Add Platform`, selezionare `Native Application` e quindi fare clic su Salva</span><span class="sxs-lookup"><span data-stu-id="0602d-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="0602d-116">Copiare hello GUID in ID applicazione, tornare indietro tooVisual Studio, aprire `App.xaml.cs` e sostituire `your_client_id_here` con hello ID applicazione appena registrato:</span><span class="sxs-lookup"><span data-stu-id="0602d-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
