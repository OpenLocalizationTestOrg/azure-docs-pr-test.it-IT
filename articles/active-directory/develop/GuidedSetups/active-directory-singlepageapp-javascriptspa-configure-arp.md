---
title: aaaAzure AD v2 JS SPA impostazione guidata - configurare ARP () | Documenti Microsoft
description: Illustra in che modo le applicazioni SPA di JavaScript possono chiamare un'API che richiede token di accesso dall'endpoint di Azure Active Directory v2 (ARP)
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="3f597-103">Aggiungere tooyour informazioni di registrazione dell'applicazione hello App</span><span class="sxs-lookup"><span data-stu-id="3f597-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="3f597-104">In questo passaggio, è necessario l'URL di reindirizzamento hello tooconfigure delle informazioni di registrazione dell'applicazione e quindi aggiungere un'applicazione hello Id applicazione tooyour SPA JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3f597-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="3f597-105">Configurare l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="3f597-105">Configure redirect URL</span></span>

<span data-ttu-id="3f597-106">Configurare hello `Redirect URL` campo sopra con hello URL della pagina index basato sul server web, quindi fare clic su *aggiornamento*.</span><span class="sxs-lookup"><span data-stu-id="3f597-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="3f597-107">Istruzioni di Visual Studio per ottenere l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="3f597-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="3f597-108">tooobtain l'URL di reindirizzamento, seguire le istruzioni di hello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="3f597-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="3f597-109">In *Esplora*, selezionare il progetto hello e analizzare hello `Properties` finestra (se non viene visualizzato una finestra delle proprietà, premere `F4`)</span><span class="sxs-lookup"><span data-stu-id="3f597-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="3f597-110">Copiare il valore di hello da `URL` toohello Appunti:</span><span class="sxs-lookup"><span data-stu-id="3f597-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="3f597-111">![Proprietà del progetto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="3f597-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="3f597-112">Incollare il valore di hello come un `Redirect URL` nella parte superiore di hello di questa pagina, quindi fare clic su`Update`</span><span class="sxs-lookup"><span data-stu-id="3f597-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="3f597-113">Configurazione dell'URL di reindirizzamento per Python</span><span class="sxs-lookup"><span data-stu-id="3f597-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="3f597-114">Per Python, è possibile impostare una porta del server web hello tramite riga di comando.</span><span class="sxs-lookup"><span data-stu-id="3f597-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="3f597-115">Il programma di installazione guidata utilizza hello la porta 8080 per riferimento, ma è gratuita toouse qualsiasi porta disponibile.</span><span class="sxs-lookup"><span data-stu-id="3f597-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="3f597-116">In ogni caso, attenersi alle istruzioni di hello seguenti tooset un URL di reindirizzamento nelle informazioni di registrazione applicazione hello:</span><span class="sxs-lookup"><span data-stu-id="3f597-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="3f597-117">Impostare `http://localhost:8080/` come un `Redirect URL` hello inizio di questa pagina, o utilizzare `http://localhost:[port]/` se si utilizza una porta TCP personalizzata (dove *[porta]* numero di porta TCP personalizzata hello) e quindi fare clic su 'Aggiorna'</span><span class="sxs-lookup"><span data-stu-id="3f597-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="3f597-118">Configurare l'applicazione JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="3f597-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="3f597-119">Creare un file denominato `msalconfig.js` contenente le informazioni di registrazione applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="3f597-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="3f597-120">Se si utilizza Visual Studio, progetto selezionare hello (cartella radice di progetto), mouse e scegliere: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="3f597-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="3f597-121">Assegnare il nome `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="3f597-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="3f597-122">Aggiungere i seguenti tooyour codice hello `msalconfig.js` file:</span><span class="sxs-lookup"><span data-stu-id="3f597-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
