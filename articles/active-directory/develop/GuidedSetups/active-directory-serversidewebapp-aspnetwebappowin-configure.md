---
title: aaaAzure AD v2 ASP.NET Web Server Getting Started - Config | Documenti Microsoft
description: Implementazione di accessi Microsoft in una soluzione ASP.NET con un'applicazione tradizionale basata su Web browser tramite lo standard OpenID Connect
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="6e781-103">Creare un'applicazione (Rapida)</span><span class="sxs-lookup"><span data-stu-id="6e781-103">Create an application (Express)</span></span>
<span data-ttu-id="6e781-104">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="6e781-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="6e781-105">Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="6e781-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="6e781-106">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="6e781-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="6e781-107">Verificare che sia selezionata l'opzione hello per l'installazione guidata</span><span class="sxs-lookup"><span data-stu-id="6e781-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="6e781-108">Seguire le istruzioni di hello tooadd un'applicazione tooyour l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="6e781-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="6e781-109">Aggiungere la soluzione di tooyour informazioni di registrazione applicazione (avanzate)</span><span class="sxs-lookup"><span data-stu-id="6e781-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="6e781-110">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="6e781-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="6e781-111">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione</span><span class="sxs-lookup"><span data-stu-id="6e781-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="6e781-112">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="6e781-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="6e781-113">Verificare che l'opzione hello per l'installazione guidata non è selezionata</span><span class="sxs-lookup"><span data-stu-id="6e781-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="6e781-114">Fare clic su `Add Platform`, quindi selezionare `Web`</span><span class="sxs-lookup"><span data-stu-id="6e781-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="6e781-115">Tornare indietro tooVisual Studio e, in Esplora soluzioni selezionare il progetto di hello e osservare hello proprietà finestra (se non viene visualizzata una finestra delle proprietà, premere F4)</span><span class="sxs-lookup"><span data-stu-id="6e781-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="6e781-116">Modificare anche SSL abilitato`True`</span><span class="sxs-lookup"><span data-stu-id="6e781-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="6e781-117">Copia URL SSL hello e aggiungere questo elenco toohello URL di reindirizzamento URL nell'elenco del portale di registrazione hello di URL di reindirizzamento:</span><span class="sxs-lookup"><span data-stu-id="6e781-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="6e781-119">Aggiungere il seguente hello in `web.config` ubicato nella cartella radice hello nella sezione hello `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="6e781-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="6e781-120">Sostituire `ClientId` con hello Id applicazione appena registrato</span><span class="sxs-lookup"><span data-stu-id="6e781-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="6e781-121">Sostituire `redirectUri` con hello URL SSL del progetto</span><span class="sxs-lookup"><span data-stu-id="6e781-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
