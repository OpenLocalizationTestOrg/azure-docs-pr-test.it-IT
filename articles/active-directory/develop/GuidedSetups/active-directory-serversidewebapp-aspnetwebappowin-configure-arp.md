---
title: Introduzione al server Web ASP.NET per Azure AD v2 - Configurazione | Microsoft Docs
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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="2f104-103">Configurare l'App Web ASP.NET con le informazioni di registrazione dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="2f104-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="2f104-104">In questo passaggio si configurerà il progetto in modo da usare SSL e quindi si userà l'URL SSL per configurare le informazioni di registrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f104-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="2f104-105">Successivamente, si aggiungeranno le informazioni di registrazione dell'applicazione alla soluzione tramite *web.config*.</span><span class="sxs-lookup"><span data-stu-id="2f104-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="2f104-106">In Esplora soluzioni selezionare il progetto e controllare la finestra `Properties` (se non viene visualizzata una finestra delle proprietà, premere F4)</span><span class="sxs-lookup"><span data-stu-id="2f104-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="2f104-107">Modificare `SSL Enabled` in `True`</span><span class="sxs-lookup"><span data-stu-id="2f104-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="2f104-108">Copiare il valore da `SSL URL` e incollarlo nel campo `Redirect URL` disponibile nella parte superiore della pagina e quindi fare clic su *Aggiorna*:</span><span class="sxs-lookup"><span data-stu-id="2f104-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="2f104-109">![Proprietà del progetto](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="2f104-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="2f104-110">Aggiungere il codice seguente nel file `web.config` presente nella cartella radice, nella sezione `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="2f104-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
