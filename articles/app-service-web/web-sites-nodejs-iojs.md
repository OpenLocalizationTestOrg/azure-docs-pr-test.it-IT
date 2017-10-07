---
title: aaaHow toouse io.js con App Web di servizio App di Azure
description: Informazioni su come un'app web nel servizio App di Azure con io.js toouse.
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="b0240-103">Come io.js toouse con App Web di servizio App di Azure</span><span class="sxs-lookup"><span data-stu-id="b0240-103">How toouse io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="b0240-104">divisione di nodo comuni Hello [io.js] funzionalità progetto Node.js di vari tooJoyent differenze, incluso un modello di controllo più aperto, un ciclo di rilascio più veloce e una più rapida adozione di nuove funzionalità JavaScript sperimentali.</span><span class="sxs-lookup"><span data-stu-id="b0240-104">hello popular Node fork [io.js] features various differences tooJoyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="b0240-105">Benché su [Siti Web di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) siano preinstallate molte versioni di Node.js, è consentito anche un file binario Node.js fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="b0240-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="b0240-106">In questo articolo vengono descritti due metodi di attivazione dell'utilizzo di hello di io.js nelle App Web di servizio App: hello utilizzo di uno script di distribuzione estesa, che configura automaticamente Azure toouse hello io.js disponibile più recente, nonché il caricamento manuale di un file binario io.js hello.</span><span class="sxs-lookup"><span data-stu-id="b0240-106">This article discusses two methods enabling hello use of io.js on App Service Web Apps: hello use of an extended deployment script, which automatically configures Azure toouse hello latest available io.js version, as well as hello manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="b0240-107">Utilizzo di uno script di distribuzione</span><span class="sxs-lookup"><span data-stu-id="b0240-107">Using a Deployment Script</span></span>
<span data-ttu-id="b0240-108">Durante la distribuzione di un'app Node.js App del servizio Web App esegue un numero di comandi di piccole dimensioni tooensure che hello ambiente è configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b0240-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands tooensure that hello environment is configured properly.</span></span> <span data-ttu-id="b0240-109">Tramite uno script di distribuzione, questo processo può essere personalizzato tooinclude hello download e configurazione di io.js.</span><span class="sxs-lookup"><span data-stu-id="b0240-109">Using a deployment script, this process can be customized tooinclude hello download and configuration of io.js.</span></span>

<span data-ttu-id="b0240-110">Hello [io.js Script di distribuzione](https://github.com/felixrieseberg/iojs-azure) è disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="b0240-110">hello [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="b0240-111">io.js tooenable nell'app web, è sufficiente copiare **.deployment**, **deploy** e **IISNode.yml** toohello radice della cartella dell'applicazione e distribuire le app tooWeb.</span><span class="sxs-lookup"><span data-stu-id="b0240-111">tooenable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** toohello root of your application folder and deploy tooWeb Apps.</span></span>  

<span data-ttu-id="b0240-112">primo file Hello, **.deployment**, indica le applicazioni Web toorun **deploy** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b0240-112">hello first file, **.deployment**, instructs Web Apps toorun **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="b0240-113">Questo script esegue tutti i passaggi di solito hello per un'applicazione Node.js, ma anche Scarica hello versione io.js.</span><span class="sxs-lookup"><span data-stu-id="b0240-113">This script runs all hello usual steps for a Node.js application, but also downloads hello latest version of io.js.</span></span> <span data-ttu-id="b0240-114">Infine, **IISNode.yml** Configura App Web toouse hello appena scaricato io.js binario anziché un file binario Node.js di pre-installato.</span><span class="sxs-lookup"><span data-stu-id="b0240-114">Finally, **IISNode.yml** configures Web Apps toouse just hello downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="b0240-115">hello tooupdate utilizzata io.js binario, eseguire nuovamente la distribuzione dell'applicazione - script hello verrà scaricato una nuova versione di io.js che viene distribuita un'applicazione hello ogni volta.</span><span class="sxs-lookup"><span data-stu-id="b0240-115">tooupdate hello used io.js binary, just redeploy your application - hello script will download a new version of io.js every single time hello application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="b0240-116">Utilizzo dell'installazione manuale</span><span class="sxs-lookup"><span data-stu-id="b0240-116">Using Manual Installation</span></span>
<span data-ttu-id="b0240-117">l'installazione manuale di una versione personalizzata io.js Hello include solo due passaggi.</span><span class="sxs-lookup"><span data-stu-id="b0240-117">hello manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="b0240-118">Scaricare innanzitutto hello **win-x64** binario direttamente da hello [io.js distribuzione].</span><span class="sxs-lookup"><span data-stu-id="b0240-118">First, download hello **win-x64** binary directly from hello [io.js distribution].</span></span> <span data-ttu-id="b0240-119">Sono necessari due file: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="b0240-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="b0240-120">Salva entrambi file tooa cartella all'interno di un'applicazione web, ad esempio **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="b0240-120">Save both files tooa folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="b0240-121">tooconfigure App Web toouse **iojs.exe** anziché una versione di nodo pre-installata, è possibile creare un **IISNode.yml** file alla radice dell'applicazione hello e aggiungere hello successiva riga.</span><span class="sxs-lookup"><span data-stu-id="b0240-121">tooconfigure Web Apps toouse **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at hello root of your application and add hello following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b0240-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0240-122">Next Steps</span></span>
<span data-ttu-id="b0240-123">In questo articolo è stato descritto come io.js toouse con App del servizio Web App, utilizzando sia forniti gli script di distribuzione, nonché l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="b0240-123">In this article you learned how toouse io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="b0240-124">io.js è in fase di intenso sviluppo e viene aggiornato più di frequente rispetto a Node.js.</span><span class="sxs-lookup"><span data-stu-id="b0240-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="b0240-125">Una serie di moduli Node.js potrebbe non funzionare con [io.js; consultare io.js su GitHub] per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="b0240-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b0240-126">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="b0240-126">What's changed</span></span>
* <span data-ttu-id="b0240-127">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b0240-127">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b0240-128">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="b0240-128">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b0240-129">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="b0240-129">No credit cards required; no commitments.</span></span>
> 
> 

[io.js]: https://iojs.org
[io.js distribuzione]: https://iojs.org/dist/
[io.js; consultare io.js su GitHub]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
