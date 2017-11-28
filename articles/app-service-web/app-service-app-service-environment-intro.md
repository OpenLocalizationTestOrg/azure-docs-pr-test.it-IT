---
title: aaaIntroduction tooApp v1 ambiente del servizio
description: "Informazioni sulla funzionalità hello v1 ambiente del servizio App che fornisce l'unità di scala sicura, dedicata appartenenti a un rete virtuale per l'esecuzione di tutte le app."
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
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="f93bb-103">Introduzione tooApp v1 ambiente del servizio</span><span class="sxs-lookup"><span data-stu-id="f93bb-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="f93bb-104">Questo articolo è sull'ambiente del servizio App v1 hello.</span><span class="sxs-lookup"><span data-stu-id="f93bb-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="f93bb-105">È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente.</span><span class="sxs-lookup"><span data-stu-id="f93bb-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="f93bb-106">informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="f93bb-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="f93bb-107">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f93bb-107">Overview</span></span>
<span data-ttu-id="f93bb-108">Un ambiente di servizio app è un'opzione del piano di servizio [Premium][PremiumTier] di Servizio app di Azure che fornisce un ambiente completamente isolato e dedicato all'esecuzione sicura delle app di Servizio di Azure su larga scala, tra cui [app Web][WebApps], [app per dispositivi mobili][MobileApps], e [app per le API][APIApps].</span><span class="sxs-lookup"><span data-stu-id="f93bb-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="f93bb-109">Gli ambienti di servizi di app sono ideali per i carichi di lavoro dell'applicazione che richiedono:</span><span class="sxs-lookup"><span data-stu-id="f93bb-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="f93bb-110">Scalabilità molto elevata</span><span class="sxs-lookup"><span data-stu-id="f93bb-110">Very high scale</span></span>
* <span data-ttu-id="f93bb-111">Isolamento e accesso alla rete protetto</span><span class="sxs-lookup"><span data-stu-id="f93bb-111">Isolation and secure network access</span></span>

<span data-ttu-id="f93bb-112">I clienti possono creare più ambienti di servizi di applicazione in una singola area di Azure, nonché in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="f93bb-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="f93bb-113">Questo rende gli Ambienti di servizio dell’App ideali per i livelli dell’applicazione con scalabilità orizzontale senza stato, nel supportare i carichi di lavoro elevati RPS.</span><span class="sxs-lookup"><span data-stu-id="f93bb-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="f93bb-114">Gli ambienti del servizio App sono isolati toorunning solo le applicazioni di un singolo cliente e vengono sempre distribuiti in una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="f93bb-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="f93bb-115">Sono dotate di un controllo accurato sul traffico di rete sia in ingresso e in uscita dell'applicazione e le applicazioni possono stabilire connessioni protette ad alta velocità su alle risorse aziendali locali tooon reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="f93bb-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="f93bb-116">Tutti gli articoli e in che modo-per informazioni su degli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f93bb-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="f93bb-117">Per una panoramica di come gli ambienti del servizio App abilitare su larga scala e proteggere l'accesso alla rete, vedere hello [approfondimento AzureCon] [ AzureConDeepDive] negli ambienti di servizio App.</span><span class="sxs-lookup"><span data-stu-id="f93bb-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="f93bb-118">Per un'analisi approfondita sulla scalabilità orizzontale utilizzando più ambienti di servizio App vedere l'articolo di hello sul toosetup un [footprint app distribuita geograficamente][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="f93bb-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="f93bb-119">toosee come è stato configurato l'architettura di sicurezza hello illustrata in hello AzureCon analisi approfondita, vedere l'articolo hello sull'implementazione di un [a più livelli di architettura di sicurezza](app-service-app-service-environment-layered-security.md) con gli ambienti del servizio App.</span><span class="sxs-lookup"><span data-stu-id="f93bb-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="f93bb-120">Le app in esecuzione in ambienti di servizio app possono avere l'accesso controllato da dispositivi upstream, quali i firewall di applicazione web (WAF).</span><span class="sxs-lookup"><span data-stu-id="f93bb-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="f93bb-121">articolo Hello in [configurazione di un WAF per gli ambienti del servizio App](app-service-app-service-environment-web-application-firewall.md) illustra questo scenario.</span><span class="sxs-lookup"><span data-stu-id="f93bb-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="f93bb-122">Risorse di calcolo dedicate</span><span class="sxs-lookup"><span data-stu-id="f93bb-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="f93bb-123">Calcolo hello le risorse in un ambiente del servizio App sono tutte dedicato esclusivamente tooa singola sottoscrizione e un ambiente del servizio App può essere configurato con le risorse di calcolo toofifty (50) per l'uso esclusivo da un'unica applicazione.</span><span class="sxs-lookup"><span data-stu-id="f93bb-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="f93bb-124">Un ambiente del servizio App è costituito da un pool di risorse di calcolo front-end, nonché i pool di risorse di calcolo lavoro uno toothree.</span><span class="sxs-lookup"><span data-stu-id="f93bb-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="f93bb-125">pool di server front-end Hello contiene risorse di calcolo responsabile della terminazione SSL come il bilanciamento del carico automatico e di richieste di app all'interno di un ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="f93bb-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="f93bb-126">Ogni pool di lavoro contiene le risorse di calcolo allocate troppo[piani di servizio App][AppServicePlan], che a sua volta contiene uno o più applicazioni di servizio App di Azure.</span><span class="sxs-lookup"><span data-stu-id="f93bb-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="f93bb-127">Poiché possono essere i pool di lavoro diverso toothree in un ambiente del servizio App, è necessario hello flessibilità toochoose diversi le risorse di calcolo per ogni pool di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f93bb-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="f93bb-128">Ad esempio, questo consente di pool di lavoro uno toocreate con risorse di calcolo meno potenti per piani di servizio App previsto per le applicazioni di sviluppo o test.</span><span class="sxs-lookup"><span data-stu-id="f93bb-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="f93bb-129">Un secondo (o perfino un terzo) pool di lavoro potrebbe usare risorse di calcolo più potenti dedicate ai piani di servizio app che eseguono le app di produzione.</span><span class="sxs-lookup"><span data-stu-id="f93bb-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="f93bb-130">Per ulteriori informazioni sulla quantità di hello di calcolo risorse disponibili toohello front-end e i pool di lavoro, vedere [come un ambiente del servizio App tooConfigure][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="f93bb-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="f93bb-131">Per informazioni dettagliate su hello disponibile calcolano le dimensioni delle risorse supportati in un ambiente del servizio App, consultare hello [prezzi del servizio App] [ AppServicePricing] pagina ed esaminare le opzioni disponibili hello per gli ambienti del servizio App hello Premium piano tariffario.</span><span class="sxs-lookup"><span data-stu-id="f93bb-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="f93bb-132">Supporto della rete virtuale</span><span class="sxs-lookup"><span data-stu-id="f93bb-132">Virtual Network Support</span></span>
<span data-ttu-id="f93bb-133">Un ambiente del servizio app può essere creato **in** una rete virtuale di Azure Resource Manager **o** in una rete virtuale del modello di distribuzione classica. [Altre informazioni sulle reti virtuali][MoreInfoOnVirtualNetworks].</span><span class="sxs-lookup"><span data-stu-id="f93bb-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="f93bb-134">Poiché un ambiente del servizio App è sempre presente in una rete virtuale e, in modo più preciso all'interno di una subnet di una rete virtuale, è possibile sfruttare le funzionalità di sicurezza hello di reti virtuali toocontrol entrambe le comunicazioni di rete in ingresso e in uscita.</span><span class="sxs-lookup"><span data-stu-id="f93bb-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="f93bb-135">Un ambiente del servizio app può avere connessione a Internet con un indirizzo IP pubblico o connessione interna con un indirizzo del Servizio di bilanciamento del carico interno di Azure.</span><span class="sxs-lookup"><span data-stu-id="f93bb-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="f93bb-136">È possibile utilizzare [gruppi di sicurezza di rete] [ NetworkSecurityGroups] toorestrict in ingresso subnet toohello le comunicazioni di rete in cui si trova un ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="f93bb-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="f93bb-137">In questo modo le app toorun dietro a monte dispositivi e servizi, ad esempio i firewall applicazione web e i provider SaaS di rete.</span><span class="sxs-lookup"><span data-stu-id="f93bb-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="f93bb-138">Le applicazioni inoltre spesso necessitano tooaccess alle risorse aziendali, ad esempio servizi web e database interni.</span><span class="sxs-lookup"><span data-stu-id="f93bb-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="f93bb-139">Un approccio comune è toomake flusso all'interno di una rete virtuale di Azure il traffico di rete disponibili toointernal solo questi endpoint.</span><span class="sxs-lookup"><span data-stu-id="f93bb-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="f93bb-140">Una volta che un ambiente del servizio App è unita in join toohello stessa rete virtuale come hello interno servizi delle applicazioni in esecuzione nell'ambiente di hello può accedervi, inclusi gli endpoint raggiungibili tramite [Site-to-Site] [ SiteToSite]e [Azure ExpressRoute] [ ExpressRoute] connessioni.</span><span class="sxs-lookup"><span data-stu-id="f93bb-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="f93bb-141">Per ulteriori dettagli sul funzionamento gli ambienti del servizio App con le reti virtuali e reti locali consultare i seguenti articoli hello [architettura di rete][NetworkArchitectureOverview], [controllo in ingresso Traffico][ControllingInboundTraffic], e [connessione in modo sicuro tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="f93bb-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="f93bb-142">introduttiva</span><span class="sxs-lookup"><span data-stu-id="f93bb-142">Getting started</span></span>
<span data-ttu-id="f93bb-143">tooget avviato con gli ambienti del servizio App, vedere [come tooCreate un ambiente del servizio App][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="f93bb-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="f93bb-144">Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="f93bb-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="f93bb-145">Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="f93bb-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="f93bb-146">Per una panoramica dell'architettura di rete dell'ambiente del servizio App hello, vedere hello [Cenni preliminari sull'architettura di rete] [ NetworkArchitectureOverview] articolo.</span><span class="sxs-lookup"><span data-stu-id="f93bb-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="f93bb-147">Per ulteriori informazioni sull'uso di un ambiente del servizio App con ExpressRoute, vedere hello articolo seguente [Express Route e gli ambienti del servizio App][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="f93bb-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


