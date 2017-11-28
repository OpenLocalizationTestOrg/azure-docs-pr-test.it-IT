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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="fee46-103">Configurare l'App Web ASP.NET con le informazioni di registrazione dell'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fee46-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="fee46-104">In questo passaggio si configurare il toouse progetto SSL e quindi utilizzare le informazioni di registrazione dell'applicazione hello URL SSL tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="fee46-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="fee46-105">Successivamente, aggiungere un'applicazione hello' soluzione tooyour informazioni di registrazione tramite *Web. config*.</span><span class="sxs-lookup"><span data-stu-id="fee46-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="fee46-106">In Esplora soluzioni selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzata una finestra delle proprietà, premere F4)</span><span class="sxs-lookup"><span data-stu-id="fee46-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="fee46-107">Modifica `SSL Enabled` troppo`True`</span><span class="sxs-lookup"><span data-stu-id="fee46-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="fee46-108">Copiare il valore di hello da `SSL URL` in precedenza e incollarlo in hello `Redirect URL` campo nella parte superiore di hello di questa pagina, quindi fare clic su *aggiornamento*:</span><span class="sxs-lookup"><span data-stu-id="fee46-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="fee46-109">![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="fee46-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="fee46-110">Aggiungere il seguente hello in `web.config` file si trova nella cartella della radice sezione `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="fee46-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
