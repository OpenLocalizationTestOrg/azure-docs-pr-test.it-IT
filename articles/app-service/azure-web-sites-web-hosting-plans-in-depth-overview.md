---
title: panoramica dettagliata dei piani aaaAzure servizio App | Documenti Microsoft
description: Informazioni sui piani di servizio app per Azure App Service e sui vantaggi offerti all'esperienza di gestione.
keywords: servizio app, servizio app di azure, scala, scalabile, piano di servizio app, costo del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="408c6-104">Panoramica approfondita dei piani di servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="408c6-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="408c6-105">Piani di servizio App rappresentano raccolta hello di risorse fisiche utilizzate toohost app.</span><span class="sxs-lookup"><span data-stu-id="408c6-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="408c6-106">I piani di servizio app definiscono:</span><span class="sxs-lookup"><span data-stu-id="408c6-106">App Service plans define:</span></span>

- <span data-ttu-id="408c6-107">Area (Stati Uniti occidentali, Stati Uniti orientali e così via)</span><span class="sxs-lookup"><span data-stu-id="408c6-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="408c6-108">Numero di scala (una, due, tre istanze e così via)</span><span class="sxs-lookup"><span data-stu-id="408c6-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="408c6-109">Dimensione dell'istanza (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="408c6-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="408c6-110">SKU (Gratuito, Condiviso, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="408c6-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="408c6-111">Nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) le app Web, le app per dispositivi mobili, le app per le API e le app per le funzioni (o Funzioni) vengono tutte eseguite in un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="408c6-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="408c6-112">App in hello stessa sottoscrizione e area possono condividere un piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="408c6-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="408c6-113">Tutte le applicazioni assegnate tooan **piano di servizio App** condividere risorse hello da essa definite.</span><span class="sxs-lookup"><span data-stu-id="408c6-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="408c6-114">in modo da consentire un risparmio sui costi quando si ospitano più app in un unico piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="408c6-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="408c6-115">Il **piano di servizio App** possibile scalare da **libero** e **Shared** SKU troppo**base**, **Standard**, e **Premium** SKU è accedere alle risorse di toomore e funzionalità lungo hello modo.</span><span class="sxs-lookup"><span data-stu-id="408c6-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="408c6-116">Se il piano di servizio App è stato impostato troppo**base** SKU o versione successiva, quindi è possibile controllare hello **dimensioni** e scala conteggio di hello macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="408c6-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="408c6-117">Ad esempio, se il piano è configurato toouse due istanze di "small" nel livello di servizio standard hello, eseguite tutte le applicazioni che sono associate a tale piano in entrambe le istanze.</span><span class="sxs-lookup"><span data-stu-id="408c6-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="408c6-118">Le app prevedono inoltre le funzionalità di livello di accesso toohello servizio standard.</span><span class="sxs-lookup"><span data-stu-id="408c6-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="408c6-119">Le istanze del piano in cui vengono eseguite le app sono completamente gestite e a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="408c6-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="408c6-120">Hello **SKU** e **scala** di servizio App hello piano determina hello costo e hello non il numero di App ospitate in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="408c6-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="408c6-121">Questo articolo esamina caratteristiche principali di hello, ad esempio livello e scala, di un piano di servizio App e come essi entrano in gioco durante la gestione delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="408c6-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="408c6-122">App e piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="408c6-122">Apps and App Service plans</span></span>

<span data-ttu-id="408c6-123">Un'app in un servizio app può essere associata a un solo piano per volta.</span><span class="sxs-lookup"><span data-stu-id="408c6-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="408c6-124">App e piani sono inclusi in un **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="408c6-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="408c6-125">Un gruppo di risorse funge da limite di hello del ciclo di vita per ogni risorsa che si trova all'interno di esso.</span><span class="sxs-lookup"><span data-stu-id="408c6-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="408c6-126">È possibile utilizzare risorse gruppi toomanage tutte le parti di hello di un'applicazione contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="408c6-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="408c6-127">Poiché un singolo gruppo di risorse può avere più piani di servizio App, è possibile allocare risorse fisiche toodifferent diverse app.</span><span class="sxs-lookup"><span data-stu-id="408c6-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="408c6-128">Si possono ad esempio separare le risorse tra ambienti di sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="408c6-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="408c6-129">L'uso di ambienti separati per la produzione e lo sviluppo e test consente di isolare le risorse.</span><span class="sxs-lookup"><span data-stu-id="408c6-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="408c6-130">In questo modo, test di carico rispetto a una nuova versione di App non si contendono hello stesso risorse come le applicazioni di produzione, che servono i clienti reali.</span><span class="sxs-lookup"><span data-stu-id="408c6-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="408c6-131">Quando in un unico gruppo di risorse sono inclusi più piani, è anche possibile definire un'applicazione che copre più aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="408c6-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="408c6-132">Ad esempio, un'app a disponibilità elevata in esecuzione in due aree include almeno due piani, uno per ogni area, e un'app associata a ogni piano.</span><span class="sxs-lookup"><span data-stu-id="408c6-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="408c6-133">In questo caso, tutte le copie dell'app hello hello quindi sono contenute in un singolo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="408c6-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="408c6-134">Un gruppo di risorse con più piani e più App semplifica toomanage semplice, controllo e l'integrità di hello di visualizzazione di un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="408c6-135">Creare un piano di servizio app o usare quello esistente</span><span class="sxs-lookup"><span data-stu-id="408c6-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="408c6-136">Quando si crea un'app, è consigliabile creare anche un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="408c6-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="408c6-137">In hello altra parte, se questa applicazione è un componente per l'applicazione di grandi dimensioni, creare nel gruppo di risorse hello allocata per l'applicazione di dimensioni maggiori.</span><span class="sxs-lookup"><span data-stu-id="408c6-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="408c6-138">Se l'applicazione hello è un'applicazione completamente nuova o una parte di uno più grande, è possibile scegliere toouse un toohost piano esistente, o crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="408c6-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="408c6-139">La decisione dipende principalmente dalla capacità e dal carico previsto.</span><span class="sxs-lookup"><span data-stu-id="408c6-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="408c6-140">Si consiglia di isolare l'app in un nuovo piano di servizio app nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="408c6-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="408c6-141">L'app usa molte risorse.</span><span class="sxs-lookup"><span data-stu-id="408c6-141">App is resource-intensive.</span></span>
- <span data-ttu-id="408c6-142">App include diversi fattori di scala da hello altre App ospitate in un piano esistente.</span><span class="sxs-lookup"><span data-stu-id="408c6-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="408c6-143">L'app necessita di risorse in un'area geografica diversa.</span><span class="sxs-lookup"><span data-stu-id="408c6-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="408c6-144">In questo modo è possibile allocare un nuovo set di risorse per l'app e ottenere un maggiore controllo delle app.</span><span class="sxs-lookup"><span data-stu-id="408c6-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="408c6-145">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="408c6-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="408c6-146">Se si dispone di un ambiente del servizio App, è possibile esaminare hello documentazione specifici tooApp gli ambienti del servizio qui: [creare un piano di servizio App in un ambiente del servizio App](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="408c6-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="408c6-147">È possibile creare un piano di servizio App vuoto da hello esperienza di esplorazione piano di servizio App o come parte della creazione di app.</span><span class="sxs-lookup"><span data-stu-id="408c6-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="408c6-148">In hello [portale di Azure](https://portal.azure.com), fare clic su **New** > **Web e dispositivi mobili**, quindi selezionare **App Web** o di altro tipo di applicazione di servizio App.</span><span class="sxs-lookup"><span data-stu-id="408c6-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Creare un'app nel portale di Azure hello.][createWebApp]

<span data-ttu-id="408c6-150">È quindi possibile selezionare o creare il piano di servizio App per la nuova app hello hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Creare un piano di servizio app.][createASP]

<span data-ttu-id="408c6-152">toocreate un piano di servizio App, fare clic su **[+] crea nuovi**, hello tipo **piano di servizio App** nome e quindi selezionare un'opzione appropriata **percorso**.</span><span class="sxs-lookup"><span data-stu-id="408c6-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="408c6-153">Fare clic su **tariffario**, quindi selezionare un piano tariffario appropriato per il servizio di hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="408c6-154">Selezionare **visualizzare tutti** tooview più prezzi opzioni, ad esempio **libero** e **Shared**.</span><span class="sxs-lookup"><span data-stu-id="408c6-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="408c6-155">Dopo aver selezionato hello a livello di prezzo, fare clic su hello **selezionare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="408c6-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="408c6-156">Spostare un piano di servizio App diverso app tooa</span><span class="sxs-lookup"><span data-stu-id="408c6-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="408c6-157">È possibile spostare un piano di servizio App diverso app tooa hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="408c6-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="408c6-158">È possibile spostare le applicazioni tra i piani, purché si applica ai piani hello in hello stesso gruppo di risorse e area geografica.</span><span class="sxs-lookup"><span data-stu-id="408c6-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="408c6-159">toomove un piano di tooanother app:</span><span class="sxs-lookup"><span data-stu-id="408c6-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="408c6-160">Passare toohello app che si desidera toomove.</span><span class="sxs-lookup"><span data-stu-id="408c6-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="408c6-161">In hello **Menu**, cercare hello **piano di servizio App** sezione.</span><span class="sxs-lookup"><span data-stu-id="408c6-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="408c6-162">Selezionare **piano di servizio App modifica** processo hello toostart.</span><span class="sxs-lookup"><span data-stu-id="408c6-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="408c6-163">**Piano di servizio App modifica** apre hello **piano di servizio App** selettore.</span><span class="sxs-lookup"><span data-stu-id="408c6-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="408c6-164">A questo punto, è possibile scegliere un toomove piano esistente in app.</span><span class="sxs-lookup"><span data-stu-id="408c6-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="408c6-165">il piano di servizio App seleziona Hello dell'interfaccia utente verrà filtrato per hello seguenti criteri:</span><span class="sxs-lookup"><span data-stu-id="408c6-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="408c6-166">Esiste all'interno di hello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="408c6-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="408c6-167">Esiste in hello stessa area geografica</span><span class="sxs-lookup"><span data-stu-id="408c6-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="408c6-168">Esiste all'interno di hello stesso spazio Web</span><span class="sxs-lookup"><span data-stu-id="408c6-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="408c6-169">Uno spazio Web è un costrutto logico all'interno del servizio app che definisce un raggruppamento di risorse del server.</span><span class="sxs-lookup"><span data-stu-id="408c6-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="408c6-170">Un'area geografica (ad esempio Stati Uniti occidentali) contiene spazi Web molti clienti tooallocate ordine tramite il servizio App.</span><span class="sxs-lookup"><span data-stu-id="408c6-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="408c6-171">Attualmente, le risorse del servizio App non sono in grado di toobe spostata tra gli spazi Web.</span><span class="sxs-lookup"><span data-stu-id="408c6-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Pannello di selezione Piano di servizio app.][change]

<span data-ttu-id="408c6-173">È previsto un piano tariffario diverso per ogni piano.</span><span class="sxs-lookup"><span data-stu-id="408c6-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="408c6-174">Ad esempio, lo spostamento di un sito da un livello Standard di tooa livello gratuito, Abilita tutte le app assegnato tooit toouse hello funzionalità e risorse di livello Standard hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="408c6-175">Clonare un piano di servizio App diverso app tooa</span><span class="sxs-lookup"><span data-stu-id="408c6-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="408c6-176">Se si desidera toomove hello app tooa altra area geografica, un'alternativa consiste app la clonazione.</span><span class="sxs-lookup"><span data-stu-id="408c6-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="408c6-177">Con la clonazione si crea una copia dell'app in un piano di servizio app nuovo o esistente di qualsiasi area.</span><span class="sxs-lookup"><span data-stu-id="408c6-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="408c6-178">È possibile trovare **Clone App** in hello **gli strumenti di sviluppo** sezione del menu hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="408c6-179">La clonazione presenta alcune limitazioni, illustrate nell'articolo [Clonazione di app del servizio app di Azure con il portale di Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="408c6-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="408c6-180">Scalare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="408c6-180">Scale an App Service plan</span></span>

<span data-ttu-id="408c6-181">Esistono tre modi tooscale un piano:</span><span class="sxs-lookup"><span data-stu-id="408c6-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="408c6-182">**Livello di prezzo del piano di modifica hello**.</span><span class="sxs-lookup"><span data-stu-id="408c6-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="408c6-183">Un piano di livello Basic hello può essere convertito tooStandard e tutte le app assegnato tooit toouse funzionalità hello del livello Standard hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="408c6-184">**Modifica delle dimensioni dell'istanza del piano di hello**.</span><span class="sxs-lookup"><span data-stu-id="408c6-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="408c6-185">Ad esempio, un piano di livello Basic hello che utilizza le istanze di piccole dimensioni può essere modificato toouse istanze di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="408c6-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="408c6-186">Tutte le app che sono associate a tale piano ora è possono utilizzare memoria aggiuntiva hello e risorse della CPU di hello offerte di dimensioni maggiori istanza.</span><span class="sxs-lookup"><span data-stu-id="408c6-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="408c6-187">**Modificare il numero di istanze del piano di hello**.</span><span class="sxs-lookup"><span data-stu-id="408c6-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="408c6-188">Ad esempio, un piano Standard che viene ridimensionato toothree istanze può essere scalato too10 istanze.</span><span class="sxs-lookup"><span data-stu-id="408c6-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="408c6-189">È possibile aggiungere un piano Premium istanze too20 (tooavailability soggetto).</span><span class="sxs-lookup"><span data-stu-id="408c6-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="408c6-190">Tutte le app che sono associate a tale piano ora è possono utilizzare memoria aggiuntiva hello e risorse della CPU di hello maggiore offerte di numero di istanza.</span><span class="sxs-lookup"><span data-stu-id="408c6-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="408c6-191">È possibile modificare i prezzi di livello e istanza dimensioni facendo hello hello **scalabilità verticale** elemento nelle impostazioni per l'applicazione hello o hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="408c6-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="408c6-192">Le modifiche si applicano toohello piano di servizio App e influiscono su tutte le app che vi risiedono.</span><span class="sxs-lookup"><span data-stu-id="408c6-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Impostare i valori tooscale di un'app.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="408c6-194">Pulizia del piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="408c6-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="408c6-195">**Piani di servizio app** che non dispongono di alcun toothem App associata continuerà a essere addebitato poiché continuano capacità di calcolo tooreserve hello.</span><span class="sxs-lookup"><span data-stu-id="408c6-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="408c6-196">tooavoid impreviste spese quando viene eliminato l'app di ultima hello ospitato in un piano di servizio App, hello vuoto risulta viene eliminato anche il piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="408c6-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="408c6-197">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="408c6-197">Summary</span></span>

<span data-ttu-id="408c6-198">I piani di servizio app rappresentano un set di funzionalità e capacità che è possibile condividere tra le app.</span><span class="sxs-lookup"><span data-stu-id="408c6-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="408c6-199">I piani di servizio App offrono si hello set tooa di flessibilità tooallocate App specifiche di risorse e ottimizza l'utilizzo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="408c6-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="408c6-200">In questo modo, se si desidera toosave nell'ambiente di testing, è possibile condividere un piano tra più app.</span><span class="sxs-lookup"><span data-stu-id="408c6-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="408c6-201">È anche possibile ottimizzare la velocità effettiva nell'ambiente di produzione scalandolo in più aree e piani.</span><span class="sxs-lookup"><span data-stu-id="408c6-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="408c6-202">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="408c6-202">What's changed</span></span>

- <span data-ttu-id="408c6-203">Per una modifica di toohello della Guida da tooApp di siti Web del servizio, vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="408c6-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
