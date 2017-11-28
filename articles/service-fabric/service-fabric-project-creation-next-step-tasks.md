---
title: Passaggi successivi per la creazione del progetto di Service Fabric | Microsoft Docs
description: "In questo articolo vengono forniti collegamenti a un set di attività di sviluppo principali per Infrastruttura di servizi"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 74019850c507902d9ef7ec47a364fff234aaf32b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="25d28-103">Applicazione dell'infrastruttura di servizi e fasi successive</span><span class="sxs-lookup"><span data-stu-id="25d28-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="25d28-104">L'applicazione Service Fabric di Azure è stata creata.</span><span class="sxs-lookup"><span data-stu-id="25d28-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="25d28-105">In questo articolo si descrive la costruzione del progetto e alcuni potenziali passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="25d28-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="25d28-106">L'applicazione</span><span class="sxs-lookup"><span data-stu-id="25d28-106">Your application</span></span>
<span data-ttu-id="25d28-107">Ogni nuova applicazione include un progetto di applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d28-107">Every new application includes an application project.</span></span> <span data-ttu-id="25d28-108">Potrebbero essere presenti uno o due progetti aggiuntivi in base al tipo di servizio scelto.</span><span class="sxs-lookup"><span data-stu-id="25d28-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="25d28-109">Il progetto dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="25d28-109">The application project</span></span>
<span data-ttu-id="25d28-110">Il progetto dell'applicazione è composto da:</span><span class="sxs-lookup"><span data-stu-id="25d28-110">The application project consists of:</span></span>

* <span data-ttu-id="25d28-111">Un set di riferimenti ai servizi che costituiscono l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d28-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="25d28-112">Tre profili di pubblicazione (locale a 1 nodo, locale a 5 nodi e cloud) che consentono di gestire le preferenze per l'uso in ambienti diversi, ad esempio relative a un endpoint del cluster e alla scelta di eseguire o meno distribuzioni di aggiornamento per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="25d28-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="25d28-113">Tre file di parametri dell'applicazione (identici a quelli riportati in precedenza), che consentono di gestire configurazioni dell'applicazione specifiche per ogni ambiente, ad esempio il numero di partizioni da creare per un servizio.</span><span class="sxs-lookup"><span data-stu-id="25d28-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="25d28-114">Uno script di distribuzione che consente di distribuire l'applicazione dalla riga di comando o nell'ambito di una pipeline di integrazione e distribuzione continua automatizzata.</span><span class="sxs-lookup"><span data-stu-id="25d28-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="25d28-115">Il manifesto dell'applicazione, che descrive l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d28-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="25d28-116">Il manifesto è disponibile nella cartella ApplicationPackageRoot.</span><span class="sxs-lookup"><span data-stu-id="25d28-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="25d28-117">Servizio senza stato</span><span class="sxs-lookup"><span data-stu-id="25d28-117">Stateless service</span></span>
<span data-ttu-id="25d28-118">Quando si aggiunge un nuovo servizio senza stato, Visual Studio aggiunge alla soluzione un progetto del servizio, che include un tipo proveniente da `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="25d28-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="25d28-119">Il servizio incrementa una variabile locale in un contatore.</span><span class="sxs-lookup"><span data-stu-id="25d28-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="25d28-120">Servizio con stato</span><span class="sxs-lookup"><span data-stu-id="25d28-120">Stateful service</span></span>
<span data-ttu-id="25d28-121">Quando si aggiunge un nuovo servizio con stato, Visual Studio aggiunge alla soluzione un progetto del servizio, che include un tipo proveniente da `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="25d28-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="25d28-122">Il servizio incrementa un contatore nel relativo metodo `RunAsync` e archivia il risultato in un `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="25d28-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="25d28-123">Servizio Actor</span><span class="sxs-lookup"><span data-stu-id="25d28-123">Actor service</span></span>
<span data-ttu-id="25d28-124">Quando si aggiunge un nuovo Reliable Actor, Visual Studio aggiunge due progetti alla soluzione: un progetto attore e un progetto interfaccia.</span><span class="sxs-lookup"><span data-stu-id="25d28-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="25d28-125">Il progetto attore fornisce metodi per l'impostazione e il recupero del valore di un contatore che viene mantenuto in modo affidabile all'interno dello stato dell'attore.</span><span class="sxs-lookup"><span data-stu-id="25d28-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="25d28-126">Il progetto di interfaccia fornisce un'interfaccia che può essere utilizzata da altri servizi per richiamare l'attore.</span><span class="sxs-lookup"><span data-stu-id="25d28-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="25d28-127">API Web senza stato</span><span class="sxs-lookup"><span data-stu-id="25d28-127">Stateless Web API</span></span>
<span data-ttu-id="25d28-128">Il progetto API Web senza stato fornisce un servizio Web di base che è possibile usare per aprire l'applicazione ai client esterni.</span><span class="sxs-lookup"><span data-stu-id="25d28-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="25d28-129">Per altre informazioni su come è strutturato il progetto, vedere [Introduzione ai servizi API Web di Service Fabric con self-hosting OWIN](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="25d28-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="25d28-130">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="25d28-130">ASP.NET core</span></span>
<span data-ttu-id="25d28-131">Service Fabric SDK offre lo stesso set di modelli ASP.NET Core disponibile per i progetti ASP.NET Core autonomi: modello vuoto, [API Web][aspnet-webapi] e [applicazione Web][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="25d28-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="25d28-132">Eseguibili guest e contenitori guest</span><span class="sxs-lookup"><span data-stu-id="25d28-132">Guest executables and guest containers</span></span>

<span data-ttu-id="25d28-133">Un "guest" di Service Fabric è un servizio che non è creato con i modelli di programmazione della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="25d28-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="25d28-134">È possibile comprimere i file binari per un guest [direttamente nel pacchetto dell'applicazione](service-fabric-deploy-existing-app.md) o [tramite un'immagine del contenitore](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="25d28-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="25d28-135">Visual Studio crea in entrambi i casi gli elementi necessari nella cartella **ApplicationPackageRoot** del progetto dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d28-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="25d28-136">Visual Studio non creerà un nuovo progetto di servizio perché il codice esiste già in una qualche posizione.</span><span class="sxs-lookup"><span data-stu-id="25d28-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="25d28-137">Se si desidera gestire i progetti guest insieme al progetto dell'applicazione di Service Fabric, è possibile aggiungerli alla soluzione di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="25d28-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25d28-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25d28-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="25d28-139">Creare un cluster di Azure</span><span class="sxs-lookup"><span data-stu-id="25d28-139">Create an Azure cluster</span></span>
<span data-ttu-id="25d28-140">LSDK di Infrastruttura di servizi fornisce un cluster locale per lo sviluppo e il test.</span><span class="sxs-lookup"><span data-stu-id="25d28-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="25d28-141">Per creare un cluster in Azure, vedere [Creare un cluster di Service Fabric in Azure tramite il portale di Azure][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="25d28-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="25d28-142">Pubblicazione dell'applicazione in Azure</span><span class="sxs-lookup"><span data-stu-id="25d28-142">Publish your application to Azure</span></span>
<span data-ttu-id="25d28-143">È possibile pubblicare l'applicazione direttamente da Visual Studio in un cluster di Azure.</span><span class="sxs-lookup"><span data-stu-id="25d28-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="25d28-144">Per informazioni, vedere [Publishing your application to Azure][publish-app-to-azure] (Pubblicare l'applicazione in Azure).</span><span class="sxs-lookup"><span data-stu-id="25d28-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="25d28-145">Visualizzare il cluster con Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="25d28-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="25d28-146">Service Fabric Explorer offre un modo semplice per la visualizzazione del cluster, tra cui le applicazioni distribuite e il layout fisico.</span><span class="sxs-lookup"><span data-stu-id="25d28-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="25d28-147">Per altre informazioni, vedere [Visualizzare il cluster con Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="25d28-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="25d28-148">Effettuare il versioning e aggiornare i servizi</span><span class="sxs-lookup"><span data-stu-id="25d28-148">Version and upgrade your services</span></span>
<span data-ttu-id="25d28-149">Service Fabric consente il controllo indipendente delle versioni e l'aggiornamento di servizi indipendenti in un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="25d28-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="25d28-150">Per altre informazioni, vedere [Versioning and upgrading your services][app-upgrade-tutorial] (Controllo delle versione e aggiornamento dei servizi).</span><span class="sxs-lookup"><span data-stu-id="25d28-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="25d28-151">Configurare l'integrazione continua con Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="25d28-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="25d28-152">Per informazioni su come impostare un processo di integrazione continua per l'applicazione di Service Fabric, vedere [Configurare l'integrazione e la distribuzione continue di Service Fabric con Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="25d28-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
