---
title: Introduzione all'ambiente del servizio app (versione 1)
description: "Informazioni sull'ambiente del servizio app (versione 1), che offre unità di scala dedicate, aggiunte alla rete virtuale e sicure per l'esecuzione di tutte le app."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 38cb79eb32bd61cdbfb6da91d50e6713d71a2b0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="introduction-to-app-service-environment-v1"></a><span data-ttu-id="53ec2-103">Introduzione all'ambiente del servizio app (versione 1)</span><span class="sxs-lookup"><span data-stu-id="53ec2-103">Introduction to App Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="53ec2-104">Questo articolo fa riferimento all'ambiente del servizio app (versione 1),</span><span class="sxs-lookup"><span data-stu-id="53ec2-104">This article is about the App Service Environment v1.</span></span>  <span data-ttu-id="53ec2-105">Esiste una nuova versione dell'ambiente del servizio app che, oltre ad essere più facile da usare, può essere eseguita in un'infrastruttura più potente.</span><span class="sxs-lookup"><span data-stu-id="53ec2-105">There is a newer version of the App Service Environment that is easier  to use and runs on more powerful infrastructure.</span></span> <span data-ttu-id="53ec2-106">Per altre informazioni su questa nuova versione, vedere [Introduzione ad Ambiente del servizio app](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="53ec2-106">To learn more about the new version start with the [Introduction to the App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="53ec2-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="53ec2-107">Overview</span></span>
<span data-ttu-id="53ec2-108">Un ambiente di servizio app è un'opzione del piano di servizio [Premium][PremiumTier] di Servizio app di Azure che fornisce un ambiente completamente isolato e dedicato all'esecuzione sicura delle app di Servizio di Azure su larga scala, tra cui [app Web][WebApps], [app per dispositivi mobili][MobileApps], e [app per le API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="53ec2-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="53ec2-109">Gli ambienti di servizi di app sono ideali per i carichi di lavoro dell'applicazione che richiedono:</span><span class="sxs-lookup"><span data-stu-id="53ec2-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="53ec2-110">Scalabilità molto elevata</span><span class="sxs-lookup"><span data-stu-id="53ec2-110">Very high scale</span></span>
* <span data-ttu-id="53ec2-111">Isolamento e accesso alla rete protetto</span><span class="sxs-lookup"><span data-stu-id="53ec2-111">Isolation and secure network access</span></span>

<span data-ttu-id="53ec2-112">I clienti possono creare più ambienti di servizi di applicazione in una singola area di Azure, nonché in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="53ec2-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="53ec2-113">Questo rende gli Ambienti di servizio dell’App ideali per i livelli dell’applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro elevati RPS.</span><span class="sxs-lookup"><span data-stu-id="53ec2-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="53ec2-114">Gli ambienti di servizio dell’App sono isolati per eseguire solo le applicazioni di un singolo cliente e sono sempre distribuiti in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="53ec2-114">App Service Environments are isolated to running only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="53ec2-115">I clienti hanno un controllo accurato sul traffico di rete sia in ingresso che in uscita dall'applicazione e le applicazioni possono stabilire connessioni protette ad alta velocità su reti virtuali alle risorse aziendali locali.</span><span class="sxs-lookup"><span data-stu-id="53ec2-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks to on-premises corporate resources.</span></span>

<span data-ttu-id="53ec2-116">Tutti gli articoli e le procedure sugli ambienti del servizio app sono disponibili nel [File LEGGIMI per gli ambienti di servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="53ec2-116">All articles and How-To's about App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="53ec2-117">Per una panoramica del modo in cui gli ambienti del servizio app abilitano la scalabilità elevata e proteggono l'accesso alla rete, vedere l'[approfondimento di AzureCon][AzureConDeepDive] relativo agli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53ec2-117">For an overview of how App Service Environments enable high scale and secure network access, see the [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="53ec2-118">Per un approfondimento sulla scalabilità orizzontale usando più ambienti del servizio app, vedere l'articolo sulle modalità di configurazione di un [footprint di app con distribuzione geografica][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="53ec2-118">For a deep-dive on horizontally scaling using multiple App Service Environments see the article on how to setup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="53ec2-119">Per vedere come è stata configurata l'architettura di sicurezza illustrata negli approfondimenti di AzureCon, vedere l'articolo sull'implementazione di una [architettura di sicurezza a più livelli](app-service-app-service-environment-layered-security.md) con gli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53ec2-119">To see how the security architecture shown in the AzureCon Deep Dive was configured, see the article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="53ec2-120">Le app in esecuzione in ambienti di servizio app possono avere l'accesso controllato da dispositivi upstream, quali i firewall di applicazione web (WAF).</span><span class="sxs-lookup"><span data-stu-id="53ec2-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="53ec2-121">L'articolo sulla [configurazione di un WAF per gli ambienti di servizio app](app-service-app-service-environment-web-application-firewall.md) tratta di questo scenario.</span><span class="sxs-lookup"><span data-stu-id="53ec2-121">The article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="53ec2-122">Risorse di calcolo dedicate</span><span class="sxs-lookup"><span data-stu-id="53ec2-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="53ec2-123">Tutte le risorse di calcolo in un ambiente di servizio dell’app sono dedicate esclusivamente a una singola sottoscrizione e un ambiente di servizio dell’App può essere configurato con un massimo di cinquanta (50) risorse di calcolo per l'utilizzo esclusivo da parte un'unica applicazione.</span><span class="sxs-lookup"><span data-stu-id="53ec2-123">All of the compute resources in an App Service Environment are dedicated exclusively to a single subscription, and an App Service Environment can be configured with up to fifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="53ec2-124">Un ambiente del servizio app è costituito da un pool di risorse di calcolo front-end e da un numero di pool di risorse di calcolo di lavoro compreso tra uno e tre.</span><span class="sxs-lookup"><span data-stu-id="53ec2-124">An App Service Environment is composed of a front-end compute resource pool, as well as one to three worker compute resource pools.</span></span> 

<span data-ttu-id="53ec2-125">Il pool front-end contiene le risorse di calcolo responsabili della terminazione SSL e del bilanciamento del carico automatico delle richieste delle app all'interno di un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53ec2-125">The front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="53ec2-126">Ogni pool di lavoro contiene le risorse di calcolo allocate ai [piani del servizio app][AppServicePlan], che a loro volta contengono una o più app del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="53ec2-126">Each worker pool contains compute resources allocated to [App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="53ec2-127">Dato che possono essere presenti fino a tre pool di lavoro diversi in un ambiente del servizio app, è possibile scegliere in modo flessibile diverse risorse di calcolo per ogni pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="53ec2-127">Since there can be up to three different worker pools in an App Service Environment, you have the flexibility to choose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="53ec2-128">È ad esempio possibile creare un pool di lavoro con risorse di calcolo meno potenti per i piani di servizio app dedicati allo sviluppo o al test delle app.</span><span class="sxs-lookup"><span data-stu-id="53ec2-128">For example, this allows you to create one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="53ec2-129">Un secondo (o perfino un terzo) pool di lavoro potrebbe usare risorse di calcolo più potenti dedicate ai piani di servizio app che eseguono le app di produzione.</span><span class="sxs-lookup"><span data-stu-id="53ec2-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="53ec2-130">Per informazioni dettagliate sulla quantità di risorse di calcolo disponibili per il front-end e i pool di lavoro, vedere [Come configurare un ambiente del servizio app][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="53ec2-130">For more details on the quantity of compute resources available to the front-end and worker pools, see [How To Configure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="53ec2-131">Per informazioni dettagliate sulle dimensioni delle risorse di calcolo disponibili supportate in un ambiente del servizio app, visitare la pagina [Prezzi del servizio app][AppServicePricing] ed esaminare le opzioni disponibili per gli ambienti del servizio app nel piano tariffario Premium.</span><span class="sxs-lookup"><span data-stu-id="53ec2-131">For details on the available compute resource sizes supported in an App Service Environment, consult the [App Service Pricing][AppServicePricing] page and review the available options for App Service Environments in the Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="53ec2-132">Supporto della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="53ec2-132">Virtual Network Support</span></span>
<span data-ttu-id="53ec2-133">Un ambiente del servizio app può essere creato **in** una rete virtuale di Azure Resource Manager **o** in una rete virtuale del modello di distribuzione classica. [Altre informazioni sulle reti virtuali][MoreInfoOnVirtualNetworks].</span><span class="sxs-lookup"><span data-stu-id="53ec2-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="53ec2-134">Poiché un ambiente del servizio app è sempre incluso in una rete virtuale, e più precisamente, all'interno di una subnet di una rete virtuale, è possibile usufruire delle funzionalità di sicurezza delle reti virtuali per controllare le comunicazioni di rete in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="53ec2-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage the security features of virtual networks to control both inbound and outbound network communications.</span></span>  

<span data-ttu-id="53ec2-135">Un ambiente del servizio app può avere connessione a Internet con un indirizzo IP pubblico o connessione interna con un indirizzo del Servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="53ec2-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="53ec2-136">È possibile usare i [gruppi di sicurezza di rete][NetworkSecurityGroups] per limitare le comunicazioni di rete in ingresso alla subnet in cui risiede un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="53ec2-136">You can use [network security groups][NetworkSecurityGroups] to restrict inbound network communications to the subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="53ec2-137">In questo modo è possibile eseguire le app protette da dispositivi e servizi upstream, quali firewall per applicazioni Web e provider di servizi SaaS di rete.</span><span class="sxs-lookup"><span data-stu-id="53ec2-137">This allows you to run apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="53ec2-138">Spesso le app devono accedere a risorse aziendali, ad esempio database e servizi Web interni.</span><span class="sxs-lookup"><span data-stu-id="53ec2-138">Apps also frequently need to access corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="53ec2-139">In base a un approccio comune, questi endpoint vengono resi disponibili solo al traffico di rete interno in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="53ec2-139">A common approach is to make these endpoints available only to internal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="53ec2-140">Quando un ambiente del servizio app è aggiunto alla stessa rete virtuale dei servizi interni, le app in esecuzione nell'ambiente possono accedere a questi servizi, inclusi gli endpoint raggiungibili tramite connessioni [da sito a sito][SiteToSite] e connessioni [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="53ec2-140">Once an App Service Environment is joined to the same virtual network as the internal services, apps running in the environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="53ec2-141">Per altre informazioni sul funzionamento degli ambienti del servizio app con reti virtuali e reti locali, consultare gli articoli seguenti su [architettura di rete][NetworkArchitectureOverview], [controllo del traffico in ingresso][ControllingInboundTraffic] e [connessione sicura ai back-end][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="53ec2-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult the following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting to Backends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="53ec2-142">Introduzione</span><span class="sxs-lookup"><span data-stu-id="53ec2-142">Getting started</span></span>
<span data-ttu-id="53ec2-143">Per iniziare a usare gli ambienti del servizio app, vedere [Come creare un ambiente del servizio app][HowToCreateAnAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="53ec2-143">To get started with App Service Environments, see [How To Create An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="53ec2-144">Tutti gli articoli e le procedure sugli ambienti del servizio app sono disponibili nel [file LEGGIMI per gli ambienti di servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="53ec2-144">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="53ec2-145">Per altre informazioni sulla piattaforma del servizio app di Azure, vedere l'articolo relativo al [servizio app di Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="53ec2-145">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="53ec2-146">Per una panoramica dell'architettura di rete dell'ambiente del servizio app, vedere l'articolo [Panoramica dell'architettura di rete][NetworkArchitectureOverview].</span><span class="sxs-lookup"><span data-stu-id="53ec2-146">For an overview of the App Service Environment network architecture, see the [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="53ec2-147">Per altre informazioni sull'uso di un ambiente del servizio app con ExpressRoute, vedere l'articolo seguente su [Express Route e gli ambienti del servizio app][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="53ec2-147">For details on using an App Service Environment with ExpressRoute, see the following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


