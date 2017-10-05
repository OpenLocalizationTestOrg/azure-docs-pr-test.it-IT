---
title: Impostazione guidata di JS SPA per Azure AD v2 - Configurazione (ARP) | Microsoft Docs
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
ms.openlocfilehash: 708f4ff606d79639de979918a9cacd4ed75db311
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="92916-103">Aggiungere le informazioni di registrazione dell'applicazione all'app</span><span class="sxs-lookup"><span data-stu-id="92916-103">Add the application’s registration information to your App</span></span>

<span data-ttu-id="92916-104">In questo passaggio è necessario configurare l'URL di reindirizzamento delle informazioni di registrazione dell'applicazione e quindi aggiungere l'ID dell'applicazione per l'applicazione SPA di JavaScript.</span><span class="sxs-lookup"><span data-stu-id="92916-104">In this step, you need to configure the Redirect URL of your application registration information and then add the Application Id to your JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="92916-105">Configurare l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="92916-105">Configure redirect URL</span></span>

<span data-ttu-id="92916-106">Configurare il campo `Redirect URL` in alto con l'URL della pagina index.html basata sul server Web, quindi fare clic su *Aggiorna*.</span><span class="sxs-lookup"><span data-stu-id="92916-106">Configure the `Redirect URL` field above with the URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="92916-107">Istruzioni di Visual Studio per ottenere l'URL di reindirizzamento</span><span class="sxs-lookup"><span data-stu-id="92916-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="92916-108">Per ottenere l'URL di reindirizzamento, seguire queste istruzioni:</span><span class="sxs-lookup"><span data-stu-id="92916-108">To obtain your redirect URL, follow the instructions below:</span></span>
> 1.    <span data-ttu-id="92916-109">In *Esplora soluzioni* selezionare il progetto e controllare la finestra `Properties`. Se non viene visualizzata una finestra delle proprietà, premere `F4`.</span><span class="sxs-lookup"><span data-stu-id="92916-109">In *Solution Explorer*, select the project and look at the `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="92916-110">Copiare il valore da `URL` negli Appunti:</span><span class="sxs-lookup"><span data-stu-id="92916-110">Copy the value from `URL` to the clipboard:</span></span><br/> <span data-ttu-id="92916-111">![Proprietà del progetto](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="92916-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="92916-112">Incollare il valore come `Redirect URL` nella parte superiore della pagina, quindi fare clic su `Update`</span><span class="sxs-lookup"><span data-stu-id="92916-112">Paste the value as a `Redirect URL` on the top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="92916-113">Configurazione dell'URL di reindirizzamento per Python</span><span class="sxs-lookup"><span data-stu-id="92916-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="92916-114">Per Python è possibile configurare la porta del server Web tramite la riga di comando.</span><span class="sxs-lookup"><span data-stu-id="92916-114">For Python, you can set the web server port via command line.</span></span> <span data-ttu-id="92916-115">Questa configurazione guidata usa la porta 8080 come riferimento, ma è possibile usare qualsiasi altra porta disponibile.</span><span class="sxs-lookup"><span data-stu-id="92916-115">This guided setup uses the port 8080 for reference but feel free to use any other port available.</span></span> <span data-ttu-id="92916-116">In ogni caso, seguire le istruzioni riportate di seguito per configurare un URL di reindirizzamento nelle informazioni di registrazione dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="92916-116">In any case, follow the instructions below to set up a redirect URL in the application registration information:</span></span><br/>
> <span data-ttu-id="92916-117">Impostare `http://localhost:8080/` come `Redirect URL` nella parte superiore della pagina o usare `http://localhost:[port]/` se si usa un una porta TCP personalizzata, dove *[port]* è il numero di porta TCP', quindi fare clic su 'Update' (Aggiorna).</span><span class="sxs-lookup"><span data-stu-id="92916-117">Set `http://localhost:8080/` as a `Redirect URL` on the top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is the custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="92916-118">Configurare l'applicazione JavaScript SPA</span><span class="sxs-lookup"><span data-stu-id="92916-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="92916-119">Creare un file denominato `msalconfig.js` contenente le informazioni di registrazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="92916-119">Create a file named `msalconfig.js` containing the application registration information.</span></span> <span data-ttu-id="92916-120">Se si usa Visual Studio, selezionare il progetto (cartella radice del progetto), fare clic con il pulsante destro del mouse e scegliere `Add` > `New Item` > `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="92916-120">If you are using Visual Studio, select the project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="92916-121">Assegnare il nome `msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="92916-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="92916-122">Aggiungere il codice seguente al file `msalconfig.js`:</span><span class="sxs-lookup"><span data-stu-id="92916-122">Add the following code to your `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter the application Id here]",
    redirectUri: location.origin
};
``` 
