---
title: Panoramica approfondita dei piani di servizio app di Azure | Documentazione Microsoft
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
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="353b1-104">Panoramica approfondita dei piani di servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="353b1-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="353b1-105">I piani di servizio app rappresentano la raccolta di risorse fisiche usate per ospitare le app.</span><span class="sxs-lookup"><span data-stu-id="353b1-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="353b1-106">I piani di servizio app definiscono:</span><span class="sxs-lookup"><span data-stu-id="353b1-106">App Service plans define:</span></span>

- <span data-ttu-id="353b1-107">Area (Stati Uniti occidentali, Stati Uniti orientali e così via)</span><span class="sxs-lookup"><span data-stu-id="353b1-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="353b1-108">Numero di scala (una, due, tre istanze e così via)</span><span class="sxs-lookup"><span data-stu-id="353b1-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="353b1-109">Dimensione dell'istanza (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="353b1-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="353b1-110">SKU (Gratuito, Condiviso, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="353b1-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="353b1-111">Nel [Servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714) le app Web, le app per dispositivi mobili, le app per le API e le app per le funzioni (o Funzioni) vengono tutte eseguite in un piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="353b1-112">Le app appartenenti alla stessa sottoscrizione e area possono condividere lo stesso piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="353b1-113">Tutte le applicazioni assegnate a un **piano di servizio app**  condividono le risorse definite dal piano,</span><span class="sxs-lookup"><span data-stu-id="353b1-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="353b1-114">in modo da consentire un risparmio sui costi quando si ospitano più app in un unico piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="353b1-115">Il **piano di servizio app** può essere ridimensionato da SKU **Free** e **Shared** a SKU **Basic**, **Standard** e **Premium** fornendo anche l'accesso ad altre risorse e funzionalità.</span><span class="sxs-lookup"><span data-stu-id="353b1-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="353b1-116">Se il piano di servizio app è impostato sullo SKU **Basic** o superiore, è possibile controllare le **dimensioni** e il numero di scala delle VM.</span><span class="sxs-lookup"><span data-stu-id="353b1-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="353b1-117">Se il piano è configurato per usare due istanze "piccole" nel livello di servizio Standard, ad esempio, tutte le app associate al piano vengono eseguite in entrambe le istanze</span><span class="sxs-lookup"><span data-stu-id="353b1-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="353b1-118">e hanno accesso alle funzionalità previste dal livello di servizio Standard.</span><span class="sxs-lookup"><span data-stu-id="353b1-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="353b1-119">Le istanze del piano in cui vengono eseguite le app sono completamente gestite e a disponibilità elevata.</span><span class="sxs-lookup"><span data-stu-id="353b1-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="353b1-120">L'unità **SKU** e la **scalabilità** del piano di servizio app determina il costo e non il numero di app ospitate nel piano.</span><span class="sxs-lookup"><span data-stu-id="353b1-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="353b1-121">Questo articolo illustra le principali caratteristiche, come livello e scalabilità, di un piano di servizio app e il modo in cui queste caratteristiche influiscono sulla gestione delle app.</span><span class="sxs-lookup"><span data-stu-id="353b1-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="353b1-122">App e piani di servizio app</span><span class="sxs-lookup"><span data-stu-id="353b1-122">Apps and App Service plans</span></span>

<span data-ttu-id="353b1-123">Un'app in un servizio app può essere associata a un solo piano per volta.</span><span class="sxs-lookup"><span data-stu-id="353b1-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="353b1-124">App e piani sono inclusi in un **gruppo di risorse**.</span><span class="sxs-lookup"><span data-stu-id="353b1-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="353b1-125">Un gruppo di risorse funge da confine del ciclo di vita per ogni risorsa al suo interno.</span><span class="sxs-lookup"><span data-stu-id="353b1-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="353b1-126">È possibile usare i gruppi di risorse per gestire contemporaneamente tutte le parti di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="353b1-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="353b1-127">Dato che un unico gruppo di risorse può includere più piani di servizio app, è possibile allocare app diverse a risorse fisiche diverse.</span><span class="sxs-lookup"><span data-stu-id="353b1-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="353b1-128">Si possono ad esempio separare le risorse tra ambienti di sviluppo, test e produzione.</span><span class="sxs-lookup"><span data-stu-id="353b1-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="353b1-129">L'uso di ambienti separati per la produzione e lo sviluppo e test consente di isolare le risorse.</span><span class="sxs-lookup"><span data-stu-id="353b1-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="353b1-130">In questo modo, l'esecuzione di un test di carico su una nuova versione delle app non usa le stesse risorse delle app di produzione, che devono rispondere alle richieste dei clienti reali.</span><span class="sxs-lookup"><span data-stu-id="353b1-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="353b1-131">Quando in un unico gruppo di risorse sono inclusi più piani, è anche possibile definire un'applicazione che copre più aree geografiche.</span><span class="sxs-lookup"><span data-stu-id="353b1-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="353b1-132">Ad esempio, un'app a disponibilità elevata in esecuzione in due aree include almeno due piani, uno per ogni area, e un'app associata a ogni piano.</span><span class="sxs-lookup"><span data-stu-id="353b1-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="353b1-133">In una situazione di questo tipo, tutte le copie dell'app sono contenute in un unico gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="353b1-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="353b1-134">La disponibilità di un gruppo di risorse con più piani e più app semplifica la gestione, il controllo e la visualizzazione dell'integrità dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="353b1-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="353b1-135">Creare un piano di servizio app o usare quello esistente</span><span class="sxs-lookup"><span data-stu-id="353b1-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="353b1-136">Quando si crea un'app, è consigliabile creare anche un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="353b1-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="353b1-137">D'altra parte, se l'app è un componente di un'applicazione più grande, l'app deve essere creata nel gruppo di risorse allocato per tale applicazione.</span><span class="sxs-lookup"><span data-stu-id="353b1-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="353b1-138">Sia che l'app sia completamente nuova o faccia parte di un'applicazione più grande, si può scegliere di usare un piano esistente per l'hosting o di crearne uno nuovo.</span><span class="sxs-lookup"><span data-stu-id="353b1-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="353b1-139">La decisione dipende principalmente dalla capacità e dal carico previsto.</span><span class="sxs-lookup"><span data-stu-id="353b1-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="353b1-140">Si consiglia di isolare l'app in un nuovo piano di servizio app nei casi seguenti:</span><span class="sxs-lookup"><span data-stu-id="353b1-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="353b1-141">L'app usa molte risorse.</span><span class="sxs-lookup"><span data-stu-id="353b1-141">App is resource-intensive.</span></span>
- <span data-ttu-id="353b1-142">L'app ha fattori di scala diversi dalle altre app ospitate in un piano esistente.</span><span class="sxs-lookup"><span data-stu-id="353b1-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="353b1-143">L'app necessita di risorse in un'area geografica diversa.</span><span class="sxs-lookup"><span data-stu-id="353b1-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="353b1-144">In questo modo è possibile allocare un nuovo set di risorse per l'app e ottenere un maggiore controllo delle app.</span><span class="sxs-lookup"><span data-stu-id="353b1-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="353b1-145">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="353b1-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="353b1-146">Se è disponibile un ambiente del servizio app, vedere la documentazione specifica per gli ambienti del servizio app in [Creare un piano di servizio app](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan).</span><span class="sxs-lookup"><span data-stu-id="353b1-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="353b1-147">È possibile creare un piano di servizio app vuoto dalla funzionalità di esplorazione dei piani di servizio app o durante la creazione di un'app.</span><span class="sxs-lookup"><span data-stu-id="353b1-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="353b1-148">Nel [portale di Azure](https://portal.azure.com) fare clic su **Nuovo** > **Web e dispositivi mobili** e quindi selezionare **App Web** o un altro tipo di app del servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Creare un'app nel portale di Azure.][createWebApp]

<span data-ttu-id="353b1-150">È quindi possibile selezionare o creare il piano di servizio app per la nuova app.</span><span class="sxs-lookup"><span data-stu-id="353b1-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Creare un piano di servizio app.][createASP]

<span data-ttu-id="353b1-152">Per creare un piano di servizio app, fare clic su **[+] Crea nuovo**, digitare il nome in **Piano di servizio app** e quindi selezionare una **Località** appropriata.</span><span class="sxs-lookup"><span data-stu-id="353b1-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="353b1-153">Fare clic su **Piano tariffario**e quindi selezionare un piano tariffario appropriato per il servizio.</span><span class="sxs-lookup"><span data-stu-id="353b1-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="353b1-154">Selezionare **Visualizza tutto** per visualizzare altre opzioni sui prezzi, ad esempio **Gratuito** e **Condiviso**.</span><span class="sxs-lookup"><span data-stu-id="353b1-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="353b1-155">Dopo aver scelto il piano tariffario, fare clic sul pulsante **Seleziona** .</span><span class="sxs-lookup"><span data-stu-id="353b1-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="353b1-156">Spostare un'app in un piano di servizio app diverso</span><span class="sxs-lookup"><span data-stu-id="353b1-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="353b1-157">È possibile spostare un'app in un piano di servizio app diverso nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="353b1-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="353b1-158">Le app possono essere spostate tra i piani solo se i piani si trovano nello stesso gruppo di risorse e nella stessa area geografica.</span><span class="sxs-lookup"><span data-stu-id="353b1-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="353b1-159">Per spostare un'applicazione in un altro piano:</span><span class="sxs-lookup"><span data-stu-id="353b1-159">To move an app to another plan:</span></span>

- <span data-ttu-id="353b1-160">Passare all'app che si desidera spostare.</span><span class="sxs-lookup"><span data-stu-id="353b1-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="353b1-161">Nel **Menu** cercare la sezione **Piano di servizio app**.</span><span class="sxs-lookup"><span data-stu-id="353b1-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="353b1-162">Selezionare **Cambia il piano di servizio app** per avviare il processo.</span><span class="sxs-lookup"><span data-stu-id="353b1-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="353b1-163">**Cambia il piano di servizio app** apre il selettore **Piano di servizio app**.</span><span class="sxs-lookup"><span data-stu-id="353b1-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="353b1-164">A questo punto, è possibile scegliere un piano esistente in cui spostare l'app.</span><span class="sxs-lookup"><span data-stu-id="353b1-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="353b1-165">L'interfaccia utente del piano di servizio app selezionato viene filtrato in base ai criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="353b1-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="353b1-166">È presente nello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="353b1-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="353b1-167">È presente nella stessa area geografica</span><span class="sxs-lookup"><span data-stu-id="353b1-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="353b1-168">È presente nello stesso spazio Web</span><span class="sxs-lookup"><span data-stu-id="353b1-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="353b1-169">Uno spazio Web è un costrutto logico all'interno del servizio app che definisce un raggruppamento di risorse del server.</span><span class="sxs-lookup"><span data-stu-id="353b1-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="353b1-170">Un'area geografica (ad esempio Stati Uniti occidentali) contiene molti spazi Web per allocare i clienti che usano il servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="353b1-171">Attualmente le risorse del servizio app non possono essere spostate tra spazi Web.</span><span class="sxs-lookup"><span data-stu-id="353b1-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Pannello di selezione Piano di servizio app.][change]

<span data-ttu-id="353b1-173">È previsto un piano tariffario diverso per ogni piano.</span><span class="sxs-lookup"><span data-stu-id="353b1-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="353b1-174">Quando si sposta un sito dal livello gratuito al livello Standard, ad esempio, tutte le app assegnate possono usare le funzionalità e le risorse del livello Standard.</span><span class="sxs-lookup"><span data-stu-id="353b1-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="353b1-175">Clonare un'app in un piano di servizio app diverso</span><span class="sxs-lookup"><span data-stu-id="353b1-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="353b1-176">Se si vuole spostare l'app in un'area diversa, in alternativa consiste nel clonarla.</span><span class="sxs-lookup"><span data-stu-id="353b1-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="353b1-177">Con la clonazione si crea una copia dell'app in un piano di servizio app nuovo o esistente di qualsiasi area.</span><span class="sxs-lookup"><span data-stu-id="353b1-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="353b1-178">**Clona app** è disponibile nella sezione **Strumenti di sviluppo** del menu.</span><span class="sxs-lookup"><span data-stu-id="353b1-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="353b1-179">La clonazione presenta alcune limitazioni, illustrate nell'articolo [Clonazione di app del servizio app di Azure con il portale di Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="353b1-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="353b1-180">Scalare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="353b1-180">Scale an App Service plan</span></span>

<span data-ttu-id="353b1-181">Sono disponibili tre modi per ridimensionare un piano:</span><span class="sxs-lookup"><span data-stu-id="353b1-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="353b1-182">**Modificare il piano tariffario del piano**.</span><span class="sxs-lookup"><span data-stu-id="353b1-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="353b1-183">Un piano del livello Basic può essere convertito in Standard e tutte le app assegnate potranno usare le funzionalità del livello Standard.</span><span class="sxs-lookup"><span data-stu-id="353b1-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="353b1-184">**Modificare le dimensioni delle istanze del piano**.</span><span class="sxs-lookup"><span data-stu-id="353b1-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="353b1-185">Un piano con livello Basic che usa istanze piccole, ad esempio, può essere modificato per usare istanze grandi.</span><span class="sxs-lookup"><span data-stu-id="353b1-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="353b1-186">Tutte le app associate al piano ora possono usare le risorse di memoria e CPU aggiuntive offerte dalle maggiori dimensioni delle istanze.</span><span class="sxs-lookup"><span data-stu-id="353b1-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="353b1-187">**Modificare il numero di istanze del piano**.</span><span class="sxs-lookup"><span data-stu-id="353b1-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="353b1-188">Un piano Standard con tre istanze, ad esempio, può essere aumentato fino a 10 istanze.</span><span class="sxs-lookup"><span data-stu-id="353b1-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="353b1-189">Un piano Premium può essere aumentato fino a 20 istanze (a seconda della disponibilità).</span><span class="sxs-lookup"><span data-stu-id="353b1-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="353b1-190">Tutte le app associate al piano ora possono usare le risorse di memoria e CPU aggiuntive offerte dal maggior numero di istanze.</span><span class="sxs-lookup"><span data-stu-id="353b1-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="353b1-191">È possibile modificare il piano tariffario e le dimensioni delle istanze facendo clic sulla voce **Aumenta prestazioni** nelle impostazioni dell'app o del piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="353b1-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="353b1-192">Le modifiche vengono applicate al piano di servizio app e interessano tutte le app ospitate.</span><span class="sxs-lookup"><span data-stu-id="353b1-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Impostare i valori per aumentare le prestazioni di un'app.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="353b1-194">Pulizia del piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="353b1-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="353b1-195">Anche i **piani di servizio app** a cui non sono associate app vengono addebitati, in quanto continuano a riservare la capacità di calcolo.</span><span class="sxs-lookup"><span data-stu-id="353b1-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="353b1-196">Per evitare costi imprevisti, dopo aver eliminato l'ultima app ospitata in un piano di servizio app, viene eliminato anche il piano di servizio app vuoto risultante.</span><span class="sxs-lookup"><span data-stu-id="353b1-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="353b1-197">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="353b1-197">Summary</span></span>

<span data-ttu-id="353b1-198">I piani di servizio app rappresentano un set di funzionalità e capacità che è possibile condividere tra le app.</span><span class="sxs-lookup"><span data-stu-id="353b1-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="353b1-199">I piani di servizio app garantiscono la possibilità di allocare app specifiche a un set di risorse e ottimizzare ulteriormente l'utilizzo delle risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="353b1-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="353b1-200">In questo modo, se si vuole risparmiare denaro sull'ambiente di test è possibile condividere un piano tra più app.</span><span class="sxs-lookup"><span data-stu-id="353b1-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="353b1-201">È anche possibile ottimizzare la velocità effettiva nell'ambiente di produzione scalandolo in più aree e piani.</span><span class="sxs-lookup"><span data-stu-id="353b1-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="353b1-202">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="353b1-202">What's changed</span></span>

- <span data-ttu-id="353b1-203">Per una guida relativa al passaggio da Siti Web al servizio App, vedere [Servizio app di Azure e i servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="353b1-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
