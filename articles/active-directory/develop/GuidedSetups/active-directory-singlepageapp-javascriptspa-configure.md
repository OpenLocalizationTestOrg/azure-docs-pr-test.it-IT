---
title: 'aaaAzure AD v2 JS SPA interattiva del programma di installazione: configurare | Documenti Microsoft'
description: Come le applicazioni SPA di Javascript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="c3f23-103">Registrare l'applicazione</span><span class="sxs-lookup"><span data-stu-id="c3f23-103">Register your application</span></span>

<span data-ttu-id="c3f23-104">Esistono più modi toocreate un'applicazione, selezionare uno di essi:</span><span class="sxs-lookup"><span data-stu-id="c3f23-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="c3f23-105">Opzione 1: Registrare l'applicazione (modalità Rapida)</span><span class="sxs-lookup"><span data-stu-id="c3f23-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="c3f23-106">Ora è necessario tooregister l'applicazione in hello *portale di registrazione dell'applicazione Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="c3f23-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="c3f23-107">Registrare l'applicazione tramite hello [portale di registrazione dell'applicazione di Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="c3f23-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="c3f23-108">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c3f23-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="c3f23-109">Assicurarsi che opzione hello *impostazione guidata* è selezionata</span><span class="sxs-lookup"><span data-stu-id="c3f23-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="c3f23-110">Seguire l'ID dell'applicazione hello tooobtain istruzioni hello e incollarlo nel codice</span><span class="sxs-lookup"><span data-stu-id="c3f23-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="c3f23-111">Opzione 2: Registrare l'applicazione (modalità avanzata)</span><span class="sxs-lookup"><span data-stu-id="c3f23-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="c3f23-112">Passare toohello [portale di registrazione dell'applicazione Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister un'applicazione</span><span class="sxs-lookup"><span data-stu-id="c3f23-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="c3f23-113">Immettere un nome per l'applicazione e l'indirizzo di posta elettronica</span><span class="sxs-lookup"><span data-stu-id="c3f23-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="c3f23-114">Assicurarsi che opzione hello *impostazione guidata* è deselezionata</span><span class="sxs-lookup"><span data-stu-id="c3f23-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="c3f23-115">Fare clic su `Add Platform`, quindi selezionare `Web`</span><span class="sxs-lookup"><span data-stu-id="c3f23-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="c3f23-116">Aggiungere hello `Redirect URL` che corrispondono l'URL dell'applicazione toohello basato sul server web.</span><span class="sxs-lookup"><span data-stu-id="c3f23-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="c3f23-117">Vedere sezioni hello per le istruzioni su come tooset / ottenere l'URL di reindirizzamento hello in Visual Studio e Python.</span><span class="sxs-lookup"><span data-stu-id="c3f23-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="c3f23-118">Fare clic su *Save*</span><span class="sxs-lookup"><span data-stu-id="c3f23-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="c3f23-119">Istruzioni di Visual Studio per ottenere l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="c3f23-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="c3f23-120">Seguire hello istruzioni tooobtain l'URL di reindirizzamento:</span><span class="sxs-lookup"><span data-stu-id="c3f23-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="c3f23-121">In *Esplora*, selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzato una finestra delle proprietà, premere `F4`)</span><span class="sxs-lookup"><span data-stu-id="c3f23-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="c3f23-122">Copiare il valore di hello da `URL` toohello Appunti:</span><span class="sxs-lookup"><span data-stu-id="c3f23-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="c3f23-123">![Proprietà del progetto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="c3f23-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="c3f23-124">Passa indietro toohello *portale di registrazione applicazione* e incollare il valore di hello come un `Redirect URL` e fare clic su "Salva"</span><span class="sxs-lookup"><span data-stu-id="c3f23-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="c3f23-125">Configurazione dell'URL di reindirizzamento per Python</span><span class="sxs-lookup"><span data-stu-id="c3f23-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="c3f23-126">Per Python, è possibile impostare una porta del server web hello tramite riga di comando.</span><span class="sxs-lookup"><span data-stu-id="c3f23-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="c3f23-127">Il programma di installazione guidata utilizza hello la porta 8080 per riferimento, ma è gratuita toouse qualsiasi porta disponibile.</span><span class="sxs-lookup"><span data-stu-id="c3f23-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="c3f23-128">In ogni caso, attenersi alle istruzioni di hello seguenti tooset un URL di reindirizzamento nelle informazioni di registrazione applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="c3f23-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="c3f23-129">Passa indietro toohello *portale di registrazione applicazione* e impostare `http://localhost:8080/` come un `Redirect URL`, oppure utilizzare `http://localhost:[port]/` se si utilizza una porta TCP personalizzata (dove *[porta]* è la porta TCP personalizzata hello numero) e fare clic su "Salva"</span><span class="sxs-lookup"><span data-stu-id="c3f23-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="c3f23-130">Configurare JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="c3f23-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="c3f23-131">Creare un file denominato `msalconfig.js` contenente le informazioni di registrazione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c3f23-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="c3f23-132">Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), mouse e scegliere: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="c3f23-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="c3f23-133">Assegnare il nome `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="c3f23-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="c3f23-134">Aggiungere i seguenti tooyour codice hello `msalconfig.js` file:</span><span class="sxs-lookup"><span data-stu-id="c3f23-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="c3f23-135">Sostituire <code>Enter_the_Application_Id_here</code> con hello Id applicazione appena registrato</span><span class="sxs-lookup"><span data-stu-id="c3f23-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
