---
title: funzionamento del servizio App di Azure aaaHow
description: Conoscere il funzionamento del servizio app
keywords: servizio app, servizio app di azure, scala, scalabile, piano di servizio app, costo del servizio app
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="15529-104">Funzionamento del Servizio app</span><span class="sxs-lookup"><span data-stu-id="15529-104">How App Service works</span></span>
<span data-ttu-id="15529-105">Servizio App di Azure è un servizio cloud che è progettato toosolve hello problemi pratici degli ingegneri odierni.</span><span class="sxs-lookup"><span data-stu-id="15529-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="15529-106">Servizio App è incentrato sulla fornitura di produttività degli sviluppatori superiore senza compromettere hello necessario toodeliver delle applicazioni su larga scala cloud.</span><span class="sxs-lookup"><span data-stu-id="15529-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="15529-107">Servizio App fornisce anche funzionalità di hello e Framework necessari per la creazione di applicazioni line-of-business dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="15529-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="15529-108">Servizio App consente di sviluppare applicazioni in più linguaggi di sviluppo, inclusi Java, PHP, Node.js, Python e linguaggi di Microsoft .NET hello.</span><span class="sxs-lookup"><span data-stu-id="15529-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="15529-109">Con il servizio app, è possibile:</span><span class="sxs-lookup"><span data-stu-id="15529-109">With App Service, you can:</span></span>

* <span data-ttu-id="15529-110">Compilare App Web altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="15529-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="15529-111">Creare rapidamente back-end di app per dispositivi mobili con un set di funzionalità specifiche e facili da usare, quali back-end di dati, autenticazione utente e notifiche push.</span><span class="sxs-lookup"><span data-stu-id="15529-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="15529-112">Implementare, distribuire e pubblicare API con app per le API.</span><span class="sxs-lookup"><span data-stu-id="15529-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="15529-113">Combinare applicazioni aziendali in flussi di lavoro e trasformare dati con app per la logica.</span><span class="sxs-lookup"><span data-stu-id="15529-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="15529-114">Tutti i tipi di app si basano su hello piattaforma scalabile e flessibile App Web, che consente agli sviluppatori toohave un ciclo di vita completo ottimizzato di esperienza derivata dalle manutenzione tooapp progettazione di app.</span><span class="sxs-lookup"><span data-stu-id="15529-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="15529-115">funzionalità del ciclo di vita Hello abilitare seguente hello:</span><span class="sxs-lookup"><span data-stu-id="15529-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="15529-116">**Creazione rapida di app**.</span><span class="sxs-lookup"><span data-stu-id="15529-116">**Quick app creation**.</span></span> <span data-ttu-id="15529-117">Iniziare da zero oppure selezionare un pacchetto di sistema di supporto operativo (OSS) da hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="15529-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="15529-118">**Distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="15529-118">**Continuous deployment**.</span></span> <span data-ttu-id="15529-119">Distribuire automaticamente nuovo codice dalle più diffuse soluzioni di controllo del codice sorgente, ad esempio TFS, GitHub e Bitbcket e sincronizzare contenuto da servizi di archiviazione online quali OneDrive e DropBox.</span><span class="sxs-lookup"><span data-stu-id="15529-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="15529-120">**Testare in ambiente di produzione**.</span><span class="sxs-lookup"><span data-stu-id="15529-120">**Test in production**.</span></span> <span data-ttu-id="15529-121">Senza problemi, creare ambienti di pre-produzione e gestire hello quantità di traffico toothem.</span><span class="sxs-lookup"><span data-stu-id="15529-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="15529-122">Eseguire il debug nel cloud hello quando necessario ed eseguito il rollback quando vengono riscontrati problemi.</span><span class="sxs-lookup"><span data-stu-id="15529-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="15529-123">**Eseguire attività asincrone e processi batch**.</span><span class="sxs-lookup"><span data-stu-id="15529-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="15529-124">Eseguire codice in un processo in background o attivare il codice in base a eventi, come l'inserimento di messaggi in una coda di archiviazione di Azure, e orari pianificati (CRON).</span><span class="sxs-lookup"><span data-stu-id="15529-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="15529-125">**Scalabilità dell'applicazione hello**.</span><span class="sxs-lookup"><span data-stu-id="15529-125">**Scaling hello app**.</span></span> <span data-ttu-id="15529-126">Utilizzare una delle numerose opzioni tooautomatically scalare il servizio orizzontalmente e verticalmente in base all'utilizzo delle risorse e il traffico.</span><span class="sxs-lookup"><span data-stu-id="15529-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="15529-127">Configurare ambienti privati di App tooyour dedicato.</span><span class="sxs-lookup"><span data-stu-id="15529-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="15529-128">**Gestione app hello**.</span><span class="sxs-lookup"><span data-stu-id="15529-128">**Maintaining hello app**.</span></span> <span data-ttu-id="15529-129">Utilizzano un gran numero di hello debug e diagnostica funzionalità toostay precedono i problemi e tooefficiently risolverli in tempo reale (con funzionalità quali il debug in tempo reale e la riparazione automatica) o dopo aver fatto hello analizzando i registri e memoria esegue il dump.</span><span class="sxs-lookup"><span data-stu-id="15529-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="15529-130">Nel suo complesso, funzionalità di servizio App consentono agli sviluppatori toofocus relativi al codice e raggiungere rapidamente uno stato stabile e altamente scalabili di produzione.</span><span class="sxs-lookup"><span data-stu-id="15529-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="15529-131">Con hello App per le API e le funzionalità di App per la logica, gli sviluppatori possono compilare applicazioni aziendali reali che colmare le barriere tra soluzioni di business e integrazione toocloud locale.</span><span class="sxs-lookup"><span data-stu-id="15529-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="15529-132">Video</span><span class="sxs-lookup"><span data-stu-id="15529-132">Videos</span></span>
* [<span data-ttu-id="15529-133">Architettura del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="15529-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="15529-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15529-134">Next steps</span></span>

<span data-ttu-id="15529-135">Per ulteriori informazioni sul servizio di App in uno dei seguenti argomenti hello:</span><span class="sxs-lookup"><span data-stu-id="15529-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="15529-136">Che cos'è Servizio app di Azure?</span><span class="sxs-lookup"><span data-stu-id="15529-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="15529-137">App Web</span><span class="sxs-lookup"><span data-stu-id="15529-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="15529-138">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="15529-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="15529-139">App per le API</span><span class="sxs-lookup"><span data-stu-id="15529-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="15529-140">Architettura del Servizio app di Azure (presentazione)</span><span class="sxs-lookup"><span data-stu-id="15529-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="15529-141">Confronto tra Azure App Service, Servizi cloud e Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="15529-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="15529-142">Informazioni sui piani del servizio app</span><span class="sxs-lookup"><span data-stu-id="15529-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="15529-143">Introduzione tooApp ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="15529-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="15529-144">Esercizio: Creare un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="15529-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="15529-145">Supporto degli stack di sviluppo del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="15529-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



