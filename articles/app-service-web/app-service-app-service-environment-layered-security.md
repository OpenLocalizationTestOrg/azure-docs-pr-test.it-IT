---
title: Architettura di sicurezza con gli ambienti del servizio App aaaLayered
description: "Implementazione di un'architettura di sicurezza su più livelli con ambienti del servizio app."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 73ce0213-bd3e-4876-b1ed-5ecad4ad5601
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2016
ms.author: stefsch
ms.openlocfilehash: 0627ba6fa849908506fe62c451c888c147cabc03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="946ce-103">Implementazione di un'architettura di sicurezza su più livelli con ambienti del servizio app</span><span class="sxs-lookup"><span data-stu-id="946ce-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="946ce-104">Overview</span><span class="sxs-lookup"><span data-stu-id="946ce-104">Overview</span></span>
<span data-ttu-id="946ce-105">Dato che gli ambienti del servizio app forniscono un ambiente di runtime isolato distribuito in una rete virtuale, gli sviluppatori possono creare un'architettura di sicurezza su più livelli offrendo livelli diversi di accesso alla rete per ogni livello applicazione fisico.</span><span class="sxs-lookup"><span data-stu-id="946ce-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="946ce-106">Un comune desiderio è toohide API back-end da accesso generale a Internet e consentire solo le API toobe chiamato dall'App web a monte.</span><span class="sxs-lookup"><span data-stu-id="946ce-106">A common desire is toohide API back-ends from general Internet access, and only allow APIs toobe called by upstream web apps.</span></span>  <span data-ttu-id="946ce-107">[Rete di sicurezza gruppi] [ NetworkSecurityGroups] può essere utilizzato in subnet contenente gli ambienti del servizio App toorestrict accesso pubblico tooAPI applicazioni.</span><span class="sxs-lookup"><span data-stu-id="946ce-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments toorestrict public access tooAPI applications.</span></span>

<span data-ttu-id="946ce-108">diagramma Hello riportato di seguito è illustrata un'architettura di esempio con un'applicazione WebAPI basata distribuita in un ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="946ce-108">hello diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="946ce-109">Tre istanze di app web separato, distribuite in tre App servizio ambienti separati, effettuare chiamate di back-end toohello WebAPI alla stessa app.</span><span class="sxs-lookup"><span data-stu-id="946ce-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls toohello same WebAPI app.</span></span>

![Architettura concettuale][ConceptualArchitecture] 

<span data-ttu-id="946ce-111">i segni più verde Hello indicare tale hello gruppo di sicurezza di rete nella subnet hello contenente "apiase" consente chiamate in ingresso da hello App web a monte, anche se chiamate da se stessa.</span><span class="sxs-lookup"><span data-stu-id="946ce-111">hello green plus signs indicate that hello network security group on hello subnet containing "apiase" allows inbound calls from hello upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="946ce-112">Tuttavia, hello stesso gruppo di sicurezza di rete nega esplicitamente l'accesso toogeneral il traffico da Internet hello in ingresso.</span><span class="sxs-lookup"><span data-stu-id="946ce-112">However hello same network security group explicitly denies access toogeneral inbound traffic from hello Internet.</span></span> 

<span data-ttu-id="946ce-113">resto Hello di questo argomento vengono illustrati il gruppo di sicurezza rete hello passaggi necessari tooconfigure hello nella subnet hello contenente "apiase".</span><span class="sxs-lookup"><span data-stu-id="946ce-113">hello remainder of this topic walks through hello steps needed tooconfigure hello network security group on hello subnet containing "apiase".</span></span>

## <a name="determining-hello-network-behavior"></a><span data-ttu-id="946ce-114">Determinare il comportamento di rete hello</span><span class="sxs-lookup"><span data-stu-id="946ce-114">Determining hello Network Behavior</span></span>
<span data-ttu-id="946ce-115">In ordine tooknow quale sia la sicurezza di rete sono necessarie regole, è necessario toodetermine i client di rete che potrà essere tooreach hello ambiente del servizio App contenente hello app per le API e i client che verranno bloccati.</span><span class="sxs-lookup"><span data-stu-id="946ce-115">In order tooknow what network security rules are needed, you need toodetermine which network clients will be allowed tooreach hello App Service Environment containing hello API app, and which clients will be blocked.</span></span>

<span data-ttu-id="946ce-116">Poiché [sicurezza gruppi di rete] [ NetworkSecurityGroups] sono toosubnets applicate e gli ambienti del servizio App sono distribuiti in subnet, hello contenuti in un gruppo regole troppo**tutti** App in esecuzione in un ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="946ce-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied toosubnets, and App Service Environments are deployed into subnets, hello rules contained in an NSG apply too**all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="946ce-117">Utilizzando l'architettura di esempio hello per questo articolo, una volta che un gruppo di sicurezza di rete è applicato toohello subnet contenente "apiase", tutte le App in esecuzione su hello "apiase" ambiente del servizio App saranno protetti da hello stesso insieme di regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="946ce-117">Using hello sample architecture for this article, once a network security group is applied toohello subnet containing "apiase", all apps running on hello "apiase" App Service Environment will be protected by hello same set of security rules.</span></span> 

* <span data-ttu-id="946ce-118">**Determinare l'indirizzo IP in uscita hello dei chiamanti upstream:** che cos'è l'indirizzo IP hello o gli indirizzi dei chiamanti upstream hello?</span><span class="sxs-lookup"><span data-stu-id="946ce-118">**Determine hello outbound IP address of upstream callers:**  What is hello IP address or addresses of hello upstream callers?</span></span>  <span data-ttu-id="946ce-119">Questi indirizzi saranno necessario toobe esplicitamente consentito l'accesso in hello gruppo.</span><span class="sxs-lookup"><span data-stu-id="946ce-119">These addresses will need toobe explicitly allowed access in hello NSG.</span></span>  <span data-ttu-id="946ce-120">Poiché le chiamate tra gli ambienti del servizio App vengono considerate chiamate "Internet", ciò significa hello in uscita IP indirizzo assegnato tooeach di hello tre upstream gli ambienti del servizio App esigenze toobe hello gruppo per la subnet "apiase" hello consentito l'accesso.</span><span class="sxs-lookup"><span data-stu-id="946ce-120">Since calls between App Service Environments are considered "Internet" calls, this means hello outbound IP address assigned tooeach of hello three upstream App Service Environments needs toobe allowed access in hello NSG for hello "apiase" subnet.</span></span>   <span data-ttu-id="946ce-121">Per ulteriori informazioni su come determinare l'indirizzo IP in uscita hello per le applicazioni in esecuzione in un ambiente del servizio App, vedere hello [architettura di rete] [ NetworkArchitecture] articolo introduttivo.</span><span class="sxs-lookup"><span data-stu-id="946ce-121">For more details on determining hello outbound IP address for apps running in an App Service Environment see hello [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="946ce-122">**App per le API back-end hello necessario toocall stesso?**</span><span class="sxs-lookup"><span data-stu-id="946ce-122">**Will hello back-end API app need toocall itself?**</span></span>  <span data-ttu-id="946ce-123">Un punto sofisticato e talvolta trascurato è uno scenario di hello in cui un'applicazione hello back-end deve toocall stesso.</span><span class="sxs-lookup"><span data-stu-id="946ce-123">A sometimes overlooked and subtle point is hello scenario where hello back-end application needs toocall itself.</span></span>  <span data-ttu-id="946ce-124">Se un'applicazione API back-end in un ambiente del servizio App deve toocall stesso, questo viene considerato come una chiamata di "Internet".</span><span class="sxs-lookup"><span data-stu-id="946ce-124">If a back-end API application on an App Service Environment needs toocall itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="946ce-125">Architettura di esempio hello questa funzionalità richiede che consente l'accesso dall'indirizzo IP in uscita di hello di hello "apiase" ambiente del servizio App anche.</span><span class="sxs-lookup"><span data-stu-id="946ce-125">In hello sample architecture this requires allowing access from hello outbound IP address of hello "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-hello-network-security-group"></a><span data-ttu-id="946ce-126">Impostazione di hello il gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="946ce-126">Setting up hello Network Security Group</span></span>
<span data-ttu-id="946ce-127">Una volta hello set di indirizzi IP in uscita sono noti, hello è tooconstruct un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="946ce-127">Once hello set of outbound IP addresses are known, hello next step is tooconstruct a network security group.</span></span>  <span data-ttu-id="946ce-128">I gruppi di sicurezza di rete possono essere creati sia per le reti virtuali basate su Resource Manager che per le reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="946ce-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="946ce-129">Ecco alcuni esempi di Hello mostrano creazione e configurazione di un gruppo in una rete virtuale classica tramite Powershell.</span><span class="sxs-lookup"><span data-stu-id="946ce-129">hello examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="946ce-130">Per l'architettura di esempio hello, ambienti hello si trovano nel centro-meridionali, quindi viene creato un gruppo vuoto in tale area:</span><span class="sxs-lookup"><span data-stu-id="946ce-130">For hello sample architecture, hello environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="946ce-131">Esplicita consentire innanzitutto regola viene aggiunto per l'infrastruttura di gestione di Azure hello come indicato nell'articolo hello in [il traffico in ingresso] [ InboundTraffic] per gli ambienti del servizio App.</span><span class="sxs-lookup"><span data-stu-id="946ce-131">First an explicit allow rule is added for hello Azure management infrastructure as noted in hello article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="946ce-132">Successivamente, due regole vengono aggiunte tooallow HTTP e HTTPS chiamate da hello prima upstream ambiente del servizio App ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="946ce-132">Next, two rules are added tooallow HTTP and HTTPS calls from hello first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access toorequests from hello first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="946ce-133">Sciacquare e ripetere l'operazione per hello secondo e terzo upstream App gli ambienti del servizio ("fe2ase" e "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="946ce-133">Rinse and repeat for hello second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access toorequests from hello second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access toorequests from hello third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="946ce-134">Infine, concedere accesso toohello indirizzo IP in uscita dell'ambiente del servizio App dell'API di hello back-end in modo che possa chiamare nuovamente in se stessa.</span><span class="sxs-lookup"><span data-stu-id="946ce-134">Lastly, grant access toohello outbound IP address of hello back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on hello apiase environment toocall back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="946ce-135">Nessun altre regole di sicurezza di rete necessario toobe configurato in quanto ogni gruppo include un set di regole predefinite che bloccano l'accesso in ingresso da Internet hello per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="946ce-135">No other network security rules need toobe configured because every NSG has a set of default rules that block inbound access from hello Internet by default.</span></span>

<span data-ttu-id="946ce-136">elenco completo di Hello delle regole nel gruppo di sicurezza di rete hello è illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="946ce-136">hello full list of rules in hello network security group are shown below.</span></span>  <span data-ttu-id="946ce-137">Si noti come regola, ultimo hello è evidenziato, blocca l'accesso in ingresso da tutti i chiamanti diversi da quelli di cui è stato esplicitamente concesso l'accesso.</span><span class="sxs-lookup"><span data-stu-id="946ce-137">Note how hello last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configurazione del gruppo di sicurezza di rete][NSGConfiguration] 

<span data-ttu-id="946ce-139">passaggio finale Hello è la subnet tooapply hello NSG toohello contenente hello "apiase" ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="946ce-139">hello final step is tooapply hello NSG toohello subnet that contains hello "apiase" App Service Environment.</span></span>  

     #Apply hello NSG toohello backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="946ce-140">Con subnet toohello di gruppo applicato hello, hello tre ambienti di servizio App a monte e hello hello contenitore ambiente del servizio App API back-end, sono consentiti solo toocall nell'ambiente "apiase" hello.</span><span class="sxs-lookup"><span data-stu-id="946ce-140">With hello NSG applied toohello subnet, only hello three upstream App Service Environments, and hello App Service Environment containing hello API back-end, are allowed toocall into hello "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="946ce-141">Informazioni e collegamenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="946ce-141">Additional Links and Information</span></span>
<span data-ttu-id="946ce-142">Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="946ce-142">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="946ce-143">Informazioni sui [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="946ce-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="946ce-144">Informazioni sugli [indirizzi IP in uscita][NetworkArchitecture] e sugli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="946ce-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="946ce-145">[Porte di rete][InboundTraffic] usate dagli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="946ce-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
