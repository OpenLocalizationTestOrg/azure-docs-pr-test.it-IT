---
title: Come utilizzare io.js con Azure applicazione servizio Web App
description: Imparare a utilizzare un'applicazione web nel servizio di applicazione Azure con io.js.
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a><span data-ttu-id="3eeaa-103">Come utilizzare io.js con Azure applicazione servizio Web App</span><span class="sxs-lookup"><span data-stu-id="3eeaa-103">How to use io.js with Azure App Service Web Apps</span></span>
<span data-ttu-id="3eeaa-104">Il popolare fork del nodo [io.js] presenta diverse differenze rispetto al progetto Node.js di Joyent, incluso un modello di governance più aperto, un ciclo di rilascio presumibilmente più veloce e un'adozione più rapida delle funzionalità JavaScript nuove e sperimentali.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-104">The popular Node fork [io.js] features various differences to Joyent's Node.js project, including a more open governance model, a faster release cycle and a faster adoption of new and experimental JavaScript features.</span></span>

<span data-ttu-id="3eeaa-105">Benché su [Siti Web di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) siano preinstallate molte versioni di Node.js, è consentito anche un file binario Node.js fornito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-105">While [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps has many Node.js versions preinstalled, it also allows for an user-provided Node.js binary.</span></span> <span data-ttu-id="3eeaa-106">In questo articolo vengono descritti due metodi consente l'utilizzo di io.js applicazione servizio Web App: l'utilizzo di uno script di distribuzione estesa, che configura automaticamente Azure per utilizzare la versione più recente di io.js disponibili, nonché il caricamento manuale di un io.js binario.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-106">This article discusses two methods enabling the use of io.js on App Service Web Apps: The use of an extended deployment script, which automatically configures Azure to use the latest available io.js version, as well as the manual upload of a io.js binary.</span></span> 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a><span data-ttu-id="3eeaa-107">Utilizzo di uno script di distribuzione</span><span class="sxs-lookup"><span data-stu-id="3eeaa-107">Using a Deployment Script</span></span>
<span data-ttu-id="3eeaa-108">Durante la distribuzione di un'applicazione Node.js, Siti Web di Azure esegue una serie di piccoli comandi per garantire che l'ambiente sia configurato correttamente.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-108">Upon deployment of a Node.js app, App Service Web Apps runs a number of small commands to ensure that the environment is configured properly.</span></span> <span data-ttu-id="3eeaa-109">Usando uno script di distribuzione, questo processo può essere personalizzato in modo da includere il download e la configurazione di io.js.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-109">Using a deployment script, this process can be customized to include the download and configuration of io.js.</span></span>

<span data-ttu-id="3eeaa-110">Lo [script di distribuzione io.js](https://github.com/felixrieseberg/iojs-azure) è disponibile su GitHub.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-110">The [io.js Deployment Script](https://github.com/felixrieseberg/iojs-azure) is available on GitHub.</span></span> <span data-ttu-id="3eeaa-111">Per abilitare io.js nel proprio sito Web, è sufficiente copiare **.deployment**, **deploy.cmd** e **IISNode.yml** nella radice della cartella dell'applicazione e distribuirli in App Web.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-111">To enable io.js on your web app, simply copy **.deployment**, **deploy.cmd** and **IISNode.yml** to the root of your application folder and deploy to Web Apps.</span></span>  

<span data-ttu-id="3eeaa-112">Il primo file, **.deployment**, indica ad App Web di eseguire **deploy.cmd** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-112">The first file, **.deployment**, instructs Web Apps to run **deploy.cmd** upon deployment.</span></span> <span data-ttu-id="3eeaa-113">Questo script esegue tutti i passaggi abituali per un applicazione Node.js, ma scarica anche la versione più recente di io.js.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-113">This script runs all the usual steps for a Node.js application, but also downloads the latest version of io.js.</span></span> <span data-ttu-id="3eeaa-114">Infine, **IISNode.yml** configura App Web in modo da usare il file binario io.js appena scaricato anziché un file binario Node.js preinstallato.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-114">Finally, **IISNode.yml** configures Web Apps to use just the downloaded io.js binary instead of a pre-installed Node.js binary.</span></span>

> [!NOTE]
> <span data-ttu-id="3eeaa-115">Per aggiornare il file binario io.js usato, eseguire nuovamente la distribuzione dell'applicazione; lo script scaricherà una nuova versione di io.js ogni volta che l'applicazione viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-115">To update the used io.js binary, just redeploy your application - the script will download a new version of io.js every single time the application is deployed.</span></span>
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a><span data-ttu-id="3eeaa-116">Utilizzo dell'installazione manuale</span><span class="sxs-lookup"><span data-stu-id="3eeaa-116">Using Manual Installation</span></span>
<span data-ttu-id="3eeaa-117">L'installazione manuale di una versione personalizzata di io.js prevede solo due passaggi.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-117">The manual installation of a custom io.js version includes only two steps.</span></span> <span data-ttu-id="3eeaa-118">Innanzitutto, scaricare il file binario **win-x64** direttamente dalla [distribuzione io.js].</span><span class="sxs-lookup"><span data-stu-id="3eeaa-118">First, download the **win-x64** binary directly from the [io.js distribution].</span></span> <span data-ttu-id="3eeaa-119">Sono necessari due file: **iojs.exe** e **iojs.lib**.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-119">Required are two files - **iojs.exe** and **iojs.lib**.</span></span> <span data-ttu-id="3eeaa-120">Salvare entrambi i file in una cartella all'interno del proprio sto Web, ad esempio in **bin/iojs**.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-120">Save both files to a folder inside your web app, for example in **bin/iojs**.</span></span>

<span data-ttu-id="3eeaa-121">Per configurare App Web di Azure in modo da usare **iojs.exe** anziché una versione del nodo preinstallata, creare un file **IISNode.yml** nella directory principale dell'applicazione e aggiungere la riga seguente.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-121">To configure Web Apps to use **iojs.exe** instead of a pre-installed Node version, create a **IISNode.yml** file at the root of your application and add the following line.</span></span>

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="3eeaa-122">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3eeaa-122">Next Steps</span></span>
<span data-ttu-id="3eeaa-123">In questo articolo si è appreso come usare io.js con Siti Web di Azure, usando sia gli script di distribuzione forniti sia l'installazione manuale.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-123">In this article you learned how to use io.js with App Service Web Apps, using both provided deployment scripts as well as manual installation.</span></span> 

> [!NOTE]
> <span data-ttu-id="3eeaa-124">io.js è in fase di intenso sviluppo e viene aggiornato più di frequente rispetto a Node.js.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-124">io.js is in heavy development and updated more frequently than Node.js.</span></span> <span data-ttu-id="3eeaa-125">Una serie di moduli Node.js potrebbe non funzionare con [io.js; consultare io.js su GitHub] per la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-125">A number of Node.js modules might not work with io.js - please consult [io.js on GitHub] for troubleshooting.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="3eeaa-126">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="3eeaa-126">What's changed</span></span>
* <span data-ttu-id="3eeaa-127">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="3eeaa-127">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="3eeaa-128">Per iniziare a usare Servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-128">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3eeaa-129">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="3eeaa-129">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="3eeaa-130">[io.js]: https://iojs.org</span><span class="sxs-lookup"><span data-stu-id="3eeaa-130">[io.js]: https://iojs.org</span></span>
<span data-ttu-id="3eeaa-131">[distribuzione io.js]: https://iojs.org/dist/</span><span class="sxs-lookup"><span data-stu-id="3eeaa-131">[io.js distribution]: https://iojs.org/dist/</span></span>
<span data-ttu-id="3eeaa-132">[io.js; consultare io.js su GitHub]: https://github.com/iojs/io.js</span><span class="sxs-lookup"><span data-stu-id="3eeaa-132">[io.js on GitHub]: https://github.com/iojs/io.js</span></span>
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
