---
title: Funzionamento del Servizio app di Azure
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
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="a3965-104">Funzionamento del Servizio app</span><span class="sxs-lookup"><span data-stu-id="a3965-104">How App Service works</span></span>
<span data-ttu-id="a3965-105">Il Servizio app di Azure è un servizio cloud concepito per risolvere i problemi pratici che attualmente affliggono i tecnici.</span><span class="sxs-lookup"><span data-stu-id="a3965-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="a3965-106">Il Servizio app è finalizzato a favorire la massima produttività degli sviluppatori, senza compromettere l'esigenza di fornire applicazioni a livello cloud.</span><span class="sxs-lookup"><span data-stu-id="a3965-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="a3965-107">Il servizio App offre inoltre le funzionalità e i framework necessari per la creazione di applicazioni line-of-business aziendali.</span><span class="sxs-lookup"><span data-stu-id="a3965-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="a3965-108">Il servizio App consente di sviluppare app nei linguaggi di sviluppo più comuni, tra cui Java, PHP, Node.js, Python e linguaggi di Microsoft.NET.</span><span class="sxs-lookup"><span data-stu-id="a3965-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="a3965-109">Con il servizio app, è possibile:</span><span class="sxs-lookup"><span data-stu-id="a3965-109">With App Service, you can:</span></span>

* <span data-ttu-id="a3965-110">Compilare App Web altamente scalabili.</span><span class="sxs-lookup"><span data-stu-id="a3965-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="a3965-111">Creare rapidamente back-end di app per dispositivi mobili con un set di funzionalità specifiche e facili da usare, quali back-end di dati, autenticazione utente e notifiche push.</span><span class="sxs-lookup"><span data-stu-id="a3965-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="a3965-112">Implementare, distribuire e pubblicare API con app per le API.</span><span class="sxs-lookup"><span data-stu-id="a3965-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="a3965-113">Combinare applicazioni aziendali in flussi di lavoro e trasformare dati con app per la logica.</span><span class="sxs-lookup"><span data-stu-id="a3965-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="a3965-114">Tutti i tipi di app si basano sulla piattaforma scalabile e flessibile di App Web che consente agli sviluppatori di vivere un'esperienza ottimizzata per l'intero ciclo di vita, dalla progettazione di app fino alla manutenzione.</span><span class="sxs-lookup"><span data-stu-id="a3965-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="a3965-115">Le funzionalità del ciclo di vita consentono le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3965-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="a3965-116">**Creazione rapida di app**.</span><span class="sxs-lookup"><span data-stu-id="a3965-116">**Quick app creation**.</span></span> <span data-ttu-id="a3965-117">Iniziare da zero o selezionare un pacchetto OSS da Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a3965-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="a3965-118">**Distribuzione continua**.</span><span class="sxs-lookup"><span data-stu-id="a3965-118">**Continuous deployment**.</span></span> <span data-ttu-id="a3965-119">Distribuire automaticamente nuovo codice dalle più diffuse soluzioni di controllo del codice sorgente, ad esempio TFS, GitHub e Bitbcket e sincronizzare contenuto da servizi di archiviazione online quali OneDrive e DropBox.</span><span class="sxs-lookup"><span data-stu-id="a3965-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="a3965-120">**Testare in ambiente di produzione**.</span><span class="sxs-lookup"><span data-stu-id="a3965-120">**Test in production**.</span></span> <span data-ttu-id="a3965-121">Creare senza problemi ambienti di preproduzione e gestire la quantità di traffico diretta a tali ambienti.</span><span class="sxs-lookup"><span data-stu-id="a3965-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="a3965-122">Eseguire il debug nel cloud quando necessario ed eseguire il rollback quando vengono rilevati problemi.</span><span class="sxs-lookup"><span data-stu-id="a3965-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="a3965-123">**Eseguire attività asincrone e processi batch**.</span><span class="sxs-lookup"><span data-stu-id="a3965-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="a3965-124">Eseguire codice in un processo in background o attivare il codice in base a eventi, come l'inserimento di messaggi in una coda di archiviazione di Azure, e orari pianificati (CRON).</span><span class="sxs-lookup"><span data-stu-id="a3965-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="a3965-125">**Ridimensionare l'app**.</span><span class="sxs-lookup"><span data-stu-id="a3965-125">**Scaling the app**.</span></span> <span data-ttu-id="a3965-126">Usare una delle numerose opzioni per scalare in orizzontale e in verticale le prestazioni del servizio in base all'uso di traffico e risorse.</span><span class="sxs-lookup"><span data-stu-id="a3965-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="a3965-127">Configurare ambienti privati dedicati alle app.</span><span class="sxs-lookup"><span data-stu-id="a3965-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="a3965-128">**Eseguire la manutenzione dell'app**.</span><span class="sxs-lookup"><span data-stu-id="a3965-128">**Maintaining the app**.</span></span> <span data-ttu-id="a3965-129">Usare molte delle funzionalità di debug e diagnostica per prevedere i problemi e risolverli in modo efficiente in tempo reale, usando funzionalità quali la correzione automatica e il debug in tempo reale, oppure dopo l'analisi dei log e dei dump della memoria.</span><span class="sxs-lookup"><span data-stu-id="a3965-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="a3965-130">Nel complesso le funzionalità del servizio app consentono agli sviluppatori di concentrarsi sul codice e raggiungere rapidamente uno stato di produzione stabile e altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="a3965-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="a3965-131">Con le funzionalità delle app per le API e per la logica, gli sviluppatori possono compilare applicazioni aziendali reali che superano le barriere tra le soluzioni aziendali e quelle locali e favoriscono l'integrazione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a3965-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="a3965-132">Video</span><span class="sxs-lookup"><span data-stu-id="a3965-132">Videos</span></span>
* [<span data-ttu-id="a3965-133">Architettura del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a3965-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="a3965-134">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a3965-134">Next steps</span></span>

<span data-ttu-id="a3965-135">Per altre informazioni sul servizio app, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a3965-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="a3965-136">Che cos'è Servizio app di Azure?</span><span class="sxs-lookup"><span data-stu-id="a3965-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="a3965-137">App Web</span><span class="sxs-lookup"><span data-stu-id="a3965-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="a3965-138">App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="a3965-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="a3965-139">App per le API</span><span class="sxs-lookup"><span data-stu-id="a3965-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="a3965-140">Architettura del Servizio app di Azure (presentazione)</span><span class="sxs-lookup"><span data-stu-id="a3965-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="a3965-141">Confronto tra Azure App Service, Servizi cloud e Macchine virtuali di Azure</span><span class="sxs-lookup"><span data-stu-id="a3965-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="a3965-142">Informazioni sui piani del servizio app</span><span class="sxs-lookup"><span data-stu-id="a3965-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="a3965-143">Introduzione all'ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a3965-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="a3965-144">Esercizio: Creare un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="a3965-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="a3965-145">Supporto degli stack di sviluppo del Servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="a3965-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



