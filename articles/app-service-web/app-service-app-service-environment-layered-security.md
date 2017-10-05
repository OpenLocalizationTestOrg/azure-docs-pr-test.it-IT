---
title: "Architettura di sicurezza su più livelli con ambienti del servizio app"
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
ms.openlocfilehash: 0fb02c13f99a8f4a46e0142c20da3b152c809b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implementing-a-layered-security-architecture-with-app-service-environments"></a><span data-ttu-id="d4ecf-103">Implementazione di un'architettura di sicurezza su più livelli con ambienti del servizio app</span><span class="sxs-lookup"><span data-stu-id="d4ecf-103">Implementing a Layered Security Architecture with App Service Environments</span></span>
## <a name="overview"></a><span data-ttu-id="d4ecf-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d4ecf-104">Overview</span></span>
<span data-ttu-id="d4ecf-105">Dato che gli ambienti del servizio app forniscono un ambiente di runtime isolato distribuito in una rete virtuale, gli sviluppatori possono creare un'architettura di sicurezza su più livelli offrendo livelli diversi di accesso alla rete per ogni livello applicazione fisico.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-105">Since App Service Environments provide an isolated runtime environment deployed into a virtual network, developers can create a layered security architecture providing differing levels of network access for each physical application tier.</span></span>

<span data-ttu-id="d4ecf-106">Un'esigenza comune è quella di nascondere i back-end delle API all'accesso a Internet generale e consentire alle API di essere chiamate solo dalle app Web upstream.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-106">A common desire is to hide API back-ends from general Internet access, and only allow APIs to be called by upstream web apps.</span></span>  <span data-ttu-id="d4ecf-107">I [gruppi di sicurezza di rete (NSG)][NetworkSecurityGroups] possono essere usati nelle subnet contenenti ambienti del servizio app per limitare l'accesso pubblico alle applicazioni API.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-107">[Network security groups (NSGs)][NetworkSecurityGroups] can be used on subnets containing App Service Environments to restrict public access to API applications.</span></span>

<span data-ttu-id="d4ecf-108">Il diagramma seguente mostra un'architettura di esempio con un elemento WebAPI basato sull'app distribuita in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-108">The diagram below shows an example architecture with a WebAPI based app deployed on an App Service Environment.</span></span>  <span data-ttu-id="d4ecf-109">Tre diverse istanze di app Web, distribuite in tre diversi ambienti del servizio app, eseguono chiamate back-end alla stessa app WebAPI.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-109">Three separate web app instances, deployed on three separate App Service Environments, make back-end calls to the same WebAPI app.</span></span>

![Architettura concettuale][ConceptualArchitecture] 

<span data-ttu-id="d4ecf-111">I segni più verdi indicano che il gruppo di sicurezza di rete nella subnet contenente "apiase" consente le chiamate in ingresso dalle app Web upstream, oltre che le chiamate da se stesso.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-111">The green plus signs indicate that the network security group on the subnet containing "apiase" allows inbound calls from the upstream web apps, as well calls from itself.</span></span>  <span data-ttu-id="d4ecf-112">Lo stesso gruppo di sicurezza di rete, tuttavia, nega esplicitamente l'accesso al traffico in ingresso generale da Internet.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-112">However the same network security group explicitly denies access to general inbound traffic from the Internet.</span></span> 

<span data-ttu-id="d4ecf-113">Il resto di questo argomento illustra in dettaglio la procedura necessaria per configurare il gruppo di sicurezza di rete nella subnet contenente "apiase".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-113">The remainder of this topic walks through the steps needed to configure the network security group on the subnet containing "apiase".</span></span>

## <a name="determining-the-network-behavior"></a><span data-ttu-id="d4ecf-114">Determinazione del comportamento della rete</span><span class="sxs-lookup"><span data-stu-id="d4ecf-114">Determining the Network Behavior</span></span>
<span data-ttu-id="d4ecf-115">Per conoscere le regole per la sicurezza della rete necessarie, si deve determinare a quali client di rete sarà consentito raggiungere l'ambiente del servizio app contenente l'app per le API e quali client verranno bloccati.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-115">In order to know what network security rules are needed, you need to determine which network clients will be allowed to reach the App Service Environment containing the API app, and which clients will be blocked.</span></span>

<span data-ttu-id="d4ecf-116">Poiché i [gruppi di sicurezza di rete][NetworkSecurityGroups] vengono applicati alle subnet e gli ambienti del servizio app vengono distribuiti nelle subnet, le regole contenute in un gruppo di sicurezza di rete si applicano a **tutte** le app in esecuzione in un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-116">Since [network security groups (NSGs)][NetworkSecurityGroups] are applied to subnets, and App Service Environments are deployed into subnets, the rules contained in an NSG apply to **all** apps running on an App Service Environment.</span></span>  <span data-ttu-id="d4ecf-117">Usando l'architettura di esempio di questo articolo, una volta applicato un gruppo di sicurezza di rete alla subnet contenente "apiase", tutte le app in esecuzione nell'ambiente del servizio app "apiase" verranno protette dallo stesso set di regole di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-117">Using the sample architecture for this article, once a network security group is applied to the subnet containing "apiase", all apps running on the "apiase" App Service Environment will be protected by the same set of security rules.</span></span> 

* <span data-ttu-id="d4ecf-118">**Determinare l'indirizzo IP in uscita dei chiamanti upstream:** quali sono gli indirizzi IP dei chiamanti upstream?</span><span class="sxs-lookup"><span data-stu-id="d4ecf-118">**Determine the outbound IP address of upstream callers:**  What is the IP address or addresses of the upstream callers?</span></span>  <span data-ttu-id="d4ecf-119">Sarà necessario consentire esplicitamente a questi indirizzi l'accesso nel gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-119">These addresses will need to be explicitly allowed access in the NSG.</span></span>  <span data-ttu-id="d4ecf-120">Poiché le chiamate tra gli ambienti del servizio app sono considerate chiamate "Internet", all'indirizzo IP in uscita assegnato a ciascuno dei tre ambienti del servizio app upstream deve essere consentito l'accesso nel gruppo di sicurezza di rete per la subnet "apiase".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-120">Since calls between App Service Environments are considered "Internet" calls, this means the outbound IP address assigned to each of the three upstream App Service Environments needs to be allowed access in the NSG for the "apiase" subnet.</span></span>   <span data-ttu-id="d4ecf-121">Per altri dettagli su come determinare l'indirizzo IP in uscita per le app in esecuzione in un ambiente del servizio app, vedere l'articolo [Panoramica dell'architettura di rete][NetworkArchitecture].</span><span class="sxs-lookup"><span data-stu-id="d4ecf-121">For more details on determining the outbound IP address for apps running in an App Service Environment see the [Network Architecture][NetworkArchitecture] Overview article.</span></span>
* <span data-ttu-id="d4ecf-122">**L'app per le API back-end dovrà chiamare se stessa?**</span><span class="sxs-lookup"><span data-stu-id="d4ecf-122">**Will the back-end API app need to call itself?**</span></span>  <span data-ttu-id="d4ecf-123">Un aspetto delicato e a volte trascurato è lo scenario in cui l'applicazione back-end deve chiamare se stessa.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-123">A sometimes overlooked and subtle point is the scenario where the back-end application needs to call itself.</span></span>  <span data-ttu-id="d4ecf-124">Se un'applicazione API back-end in un ambiente del servizio app deve chiamare se stessa, anche questa chiamata viene considerata una chiamata "Internet".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-124">If a back-end API application on an App Service Environment needs to call itself, this is also treated as an "Internet" call.</span></span>  <span data-ttu-id="d4ecf-125">Nell'architettura di esempio è necessario consentire l'accesso anche dall'indirizzo IP in uscita dell'ambiente del servizio app "apiase".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-125">In the sample architecture this requires allowing access from the outbound IP address of the "apiase" App Service Environment as well.</span></span>

## <a name="setting-up-the-network-security-group"></a><span data-ttu-id="d4ecf-126">Configurazione del gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="d4ecf-126">Setting up the Network Security Group</span></span>
<span data-ttu-id="d4ecf-127">Una volta noto il set di indirizzi IP in uscita, il passaggio successivo consiste nel creare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-127">Once the set of outbound IP addresses are known, the next step is to construct a network security group.</span></span>  <span data-ttu-id="d4ecf-128">I gruppi di sicurezza di rete possono essere creati sia per le reti virtuali basate su Resource Manager che per le reti virtuali classiche.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-128">Network security groups can be created for both Resource Manager based virtual networks, as well as classic virtual networks.</span></span>  <span data-ttu-id="d4ecf-129">Gli esempi seguenti illustrano la creazione e configurazione di un gruppo di sicurezza di rete in una rete virtuale classica usando Powershell.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-129">The examples below show creating and configuring an NSG on a classic virtual network using Powershell.</span></span>

<span data-ttu-id="d4ecf-130">Per l'architettura di esempio, gli ambienti si trovano negli Stati Uniti centro-meridionali e quindi viene creato un gruppo di sicurezza di rete vuoto in tale area:</span><span class="sxs-lookup"><span data-stu-id="d4ecf-130">For the sample architecture, the environments are located in South Central US, so an empty NSG is created in that region:</span></span>

    New-AzureNetworkSecurityGroup -Name "RestrictBackendApi" -Location "South Central US" -Label "Only allow web frontend and loopback traffic"

<span data-ttu-id="d4ecf-131">Prima viene aggiunta una regola di consenso esplicita per l'infrastruttura di gestione di Azure, come indicato nell'articolo sul [traffico in ingresso][InboundTraffic] per gli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-131">First an explicit allow rule is added for the Azure management infrastructure as noted in the article on [inbound traffic][InboundTraffic] for App Service Environments.</span></span>

    #Open ports for access by Azure management infrastructure
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW AzureMngmt" -Type Inbound -Priority 100 -Action Allow -SourceAddressPrefix 'INTERNET' -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '454-455' -Protocol TCP

<span data-ttu-id="d4ecf-132">Quindi vengono aggiunte due regole per consentire le chiamate HTTP e HTTPS dal primo ambiente del servizio app upstream ("fe1ase").</span><span class="sxs-lookup"><span data-stu-id="d4ecf-132">Next, two rules are added to allow HTTP and HTTPS calls from the first upstream App Service Environment ("fe1ase").</span></span>

    #Grant access to requests from the first upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe1ase" -Type Inbound -Priority 200 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe1ase" -Type Inbound -Priority 300 -Action Allow -SourceAddressPrefix '65.52.xx.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="d4ecf-133">Cancellare e ripetere per il secondo e il terzo ambiente del servizio app upstream ("fe2ase"e "fe3ase").</span><span class="sxs-lookup"><span data-stu-id="d4ecf-133">Rinse and repeat for the second and third upstream App Service Environments ("fe2ase"and "fe3ase").</span></span>

    #Grant access to requests from the second upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe2ase" -Type Inbound -Priority 400 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe2ase" -Type Inbound -Priority 500 -Action Allow -SourceAddressPrefix '191.238.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

    #Grant access to requests from the third upstream web front-end
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP fe3ase" -Type Inbound -Priority 600 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS fe3ase" -Type Inbound -Priority 700 -Action Allow -SourceAddressPrefix '23.98.abc.xyz'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="d4ecf-134">Infine concedere l'accesso all'indirizzo IP in uscita dell'ambiente del servizio app dell'API back-end in modo che possa richiamare se stesso.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-134">Lastly, grant access to the outbound IP address of the back-end API's App Service Environment so that it can call back into itself.</span></span>

    #Allow apps on the apiase environment to call back into itself
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP apiase" -Type Inbound -Priority 800 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTPS apiase" -Type Inbound -Priority 900 -Action Allow -SourceAddressPrefix '70.37.xyz.abc'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '443' -Protocol TCP

<span data-ttu-id="d4ecf-135">Non è necessario configurare nessuna altra regola di sicurezza di rete perché ogni gruppo di sicurezza di rete ha un set di regole predefinite che bloccano l'accesso in ingresso da Internet per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-135">No other network security rules need to be configured because every NSG has a set of default rules that block inbound access from the Internet by default.</span></span>

<span data-ttu-id="d4ecf-136">L'elenco completo di regole nel gruppo di sicurezza di rete è mostrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-136">The full list of rules in the network security group are shown below.</span></span>  <span data-ttu-id="d4ecf-137">Si noti che l'ultima regola, che è evidenziata, impedisce l'accesso in ingresso a tutti i chiamanti a cui non è stato esplicitamente concesso.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-137">Note how the last rule, which is highlighted, blocks inbound access from all callers other than those which have been explicitly granted access.</span></span>

![Configurazione del gruppo di sicurezza di rete][NSGConfiguration] 

<span data-ttu-id="d4ecf-139">Il passaggio finale consiste nell'applicare il gruppo di sicurezza di rete alla subnet contenente l'ambiente del servizio app "apiase".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-139">The final step is to apply the NSG to the subnet that contains the "apiase" App Service Environment.</span></span>  

     #Apply the NSG to the backend API subnet
    Get-AzureNetworkSecurityGroup -Name "RestrictBackendApi" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'yourvnetnamehere' -SubnetName 'API-ASE-Subnet'

<span data-ttu-id="d4ecf-140">Con il gruppo di sicurezza di rete applicato alla subnet, solo ai tre ambienti del servizio app upstream e all'ambiente del servizio app contenente il back-end dell'API è consentito chiamare l'ambiente "apiase".</span><span class="sxs-lookup"><span data-stu-id="d4ecf-140">With the NSG applied to the subnet, only the three upstream App Service Environments, and the App Service Environment containing the API back-end, are allowed to call into the "apiase" environment.</span></span>

## <a name="additional-links-and-information"></a><span data-ttu-id="d4ecf-141">Informazioni e collegamenti aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="d4ecf-141">Additional Links and Information</span></span>
<span data-ttu-id="d4ecf-142">Tutti gli articoli e le procedure sugli ambienti del servizio app sono disponibili nel [file LEGGIMI per gli ambienti di servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="d4ecf-142">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="d4ecf-143">Informazioni sui [gruppi di sicurezza di rete](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="d4ecf-143">Information about [network security groups](../virtual-network/virtual-networks-nsg.md).</span></span> 

<span data-ttu-id="d4ecf-144">Informazioni sugli [indirizzi IP in uscita][NetworkArchitecture] e sugli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-144">Understanding [outbound IP addresses][NetworkArchitecture] and App Service Environments.</span></span>

<span data-ttu-id="d4ecf-145">[Porte di rete][InboundTraffic] usate dagli ambienti del servizio app.</span><span class="sxs-lookup"><span data-stu-id="d4ecf-145">[Network ports][InboundTraffic] used by App Service Environments.</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[NetworkArchitecture]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[InboundTraffic]:  https://azure.microsoft.com/en-us/documentation/articles/app-service-app-service-environment-control-inbound-traffic/

<!-- IMAGES -->
[ConceptualArchitecture]: ./media/app-service-app-service-environment-layered-security/ConceptualArchitecture-1.png
[NSGConfiguration]:  ./media/app-service-app-service-environment-layered-security/NSGConfiguration-1.png
