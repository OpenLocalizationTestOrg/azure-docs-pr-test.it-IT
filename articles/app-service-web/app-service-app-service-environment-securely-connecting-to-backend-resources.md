---
title: aaaSecurely connessione tooBackEnd le risorse da un ambiente del servizio App
description: "Informazioni sulle modalità di connessione toobackend risorse toosecurely da un ambiente del servizio App."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: f82eb283-a6e7-4923-a00b-4b4ccf7c4b5b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: stefsch
ms.openlocfilehash: 6311d3fc301512ea3c4ed8f14f268f75755aa415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="securely-connecting-toobackend-resources-from-an-app-service-environment"></a><span data-ttu-id="080a3-103">In modo sicuro connessione tooBackend le risorse da un ambiente del servizio App</span><span class="sxs-lookup"><span data-stu-id="080a3-103">Securely Connecting tooBackend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="080a3-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="080a3-104">Overview</span></span>
<span data-ttu-id="080a3-105">Poiché un ambiente del servizio App viene sempre creato nello **entrambi** una rete virtuale di Azure Resource Manager, **o** un modello di distribuzione classica [rete virtuale] [ virtualnetwork], le connessioni in uscita dalle risorse di back-end tooother ambiente del servizio App possono scorrere in modo esclusivo la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment tooother backend resources can flow exclusively over hello virtual network.</span></span>  <span data-ttu-id="080a3-106">Con una modifica recente apportata a giugno 2016, gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano intervalli di indirizzi pubblici o spazi di indirizzi RFC1918, ovvero indirizzi privati.</span><span class="sxs-lookup"><span data-stu-id="080a3-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e. private addresses).</span></span>  

<span data-ttu-id="080a3-107">Ad esempio, potrebbe essere in esecuzione un'istanza di SQL Server in un cluster di macchine virtuali con la porta 1433 bloccata.</span><span class="sxs-lookup"><span data-stu-id="080a3-107">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="080a3-108">endpoint Hello potrebbe essere ACLd tooonly consentire l'accesso da altre risorse nella stessa rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-108">hello endpoint may be ACLd tooonly allow access from other resources on hello same virtual network.</span></span>  

<span data-ttu-id="080a3-109">Ad esempio, sensibili endpoint potrebbe essere eseguiti in locale e tooAzure connesso tramite [Site-to-Site] [ SiteToSite] o [Azure ExpressRoute] [ ExpressRoute] connessioni.</span><span class="sxs-lookup"><span data-stu-id="080a3-109">As another example, sensitive endpoints may run on-premises and be connected tooAzure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="080a3-110">Di conseguenza, solo le risorse in reti virtuali connesse toohello Site-to-Site o ExpressRoute tunnel saranno endpoint locali in grado di tooaccess.</span><span class="sxs-lookup"><span data-stu-id="080a3-110">As a result, only resources in virtual networks connected toohello Site-to-Site or ExpressRoute tunnels will be able tooaccess on-premises endpoints.</span></span>

<span data-ttu-id="080a3-111">Per tutti questi scenari, le App in esecuzione in un ambiente del servizio App verrà essere toosecurely in grado di connettere toohello diversi server e le risorse.</span><span class="sxs-lookup"><span data-stu-id="080a3-111">For all of these scenarios, apps running on an App Service Environment will be able toosecurely connect toohello various servers and resources.</span></span>  <span data-ttu-id="080a3-112">Traffico in uscita da applicazioni in esecuzione in un endpoint dell'ambiente del servizio App tooprivate hello stessa rete virtuale (o connesso toohello stessa rete virtuale), sarà solo flusso in rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-112">Outbound traffic from apps running in an App Service Environment tooprivate endpoints in hello same virtual network (or connected toohello same virtual network), will only flow over hello virtual network.</span></span>  <span data-ttu-id="080a3-113">Il traffico in uscita tooprivate endpoint non trasmetterà su hello rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="080a3-113">Outbound traffic tooprivate endpoints will not flow over hello public Internet.</span></span>

<span data-ttu-id="080a3-114">Un'avvertenza si applica toooutbound traffico da un ambiente del servizio App di tooendpoints all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="080a3-114">One caveat applies toooutbound traffic from an App Service Environment tooendpoints within a virtual network.</span></span>  <span data-ttu-id="080a3-115">Gli ambienti del servizio App non può raggiungere l'endpoint delle macchine virtuali presenti nella hello **stesso** subnet come hello ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="080a3-115">App Service Environments cannot reach endpoints of virtual machines located in hello **same** subnet as hello App Service Environment.</span></span>  <span data-ttu-id="080a3-116">In genere non deve essere un problema, purché gli ambienti del servizio App vengono distribuiti in una subnet riservata per l'uso esclusivo da solo hello ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="080a3-116">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only hello App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="080a3-117">Requisiti per DNS e connettività in uscita</span><span class="sxs-lookup"><span data-stu-id="080a3-117">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="080a3-118">Per un ambiente del servizio App di toofunction correttamente, è necessario endpoint toovarious accesso in uscita.</span><span class="sxs-lookup"><span data-stu-id="080a3-118">For an App Service Environment toofunction properly, it requires outbound access toovarious endpoints.</span></span> <span data-ttu-id="080a3-119">È un elenco completo di endpoint esterni di hello utilizzato da un ASE nella sezione "Necessaria la connettività di rete" di hello hello [configurazione di rete per ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) articolo.</span><span class="sxs-lookup"><span data-stu-id="080a3-119">A full list of hello external endpoints used by an ASE is in hello "Required Network Connectivity" section of hello [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="080a3-120">Gli ambienti del servizio App richiedono un'infrastruttura DNS valida configurata per la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-120">App Service Environments require a valid DNS infrastructure configured for hello virtual network.</span></span>  <span data-ttu-id="080a3-121">Se per qualsiasi hello motivo la configurazione del DNS viene modificata dopo aver creato un ambiente del servizio App, gli sviluppatori possono forzare toopick un ambiente del servizio App hello configurazione del nuovo DNS.</span><span class="sxs-lookup"><span data-stu-id="080a3-121">If for any reason hello DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment toopick up hello new DNS configuration.</span></span>  <span data-ttu-id="080a3-122">Attivazione di un riavvio in sequenza di ambiente facendo clic sull'icona "Riavvia" hello che si trova nella parte superiore di hello di hello ambiente del servizio App Pannello di gestione nel portale di hello causerà hello ambiente toopick hello configurazione del nuovo DNS.</span><span class="sxs-lookup"><span data-stu-id="080a3-122">Triggering a rolling environment reboot using hello "Restart" icon located at hello top of hello App Service Environment management blade in hello portal will cause hello environment toopick up hello new DNS configuration.</span></span>

<span data-ttu-id="080a3-123">È inoltre consigliabile che qualsiasi server DNS personalizzati in rete virtuale hello è necessario installare prima fase precedente toocreating un ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="080a3-123">It is also recommended that any custom DNS servers on hello vnet be setup ahead of time prior toocreating an App Service Environment.</span></span>  <span data-ttu-id="080a3-124">Se la configurazione DNS della rete virtuale viene modificata durante la creazione di un ambiente del servizio App, si avranno esito negativo processo di creazione dell'ambiente del servizio App di hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-124">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in hello App Service Environment creation process failing.</span></span>  <span data-ttu-id="080a3-125">Infine proposta, se esiste un server DNS personalizzato su hello altra entità finale di un gateway VPN e server DNS hello è hello non è raggiungibile o non disponibile, non sarà possibile eseguire il processo di creazione dell'ambiente del servizio App.</span><span class="sxs-lookup"><span data-stu-id="080a3-125">In a similar vein, if a custom DNS server exists on hello other end of a VPN gateway, and hello DNS server is unreachable or unavailable, hello App Service Environment creation process will also fail.</span></span>

## <a name="connecting-tooa-sql-server"></a><span data-ttu-id="080a3-126">Connessione tooa SQL Server</span><span class="sxs-lookup"><span data-stu-id="080a3-126">Connecting tooa SQL Server</span></span>
<span data-ttu-id="080a3-127">Una configurazione di SQL Server comune prevede un endpoint in ascolto sulla porta 1433:</span><span class="sxs-lookup"><span data-stu-id="080a3-127">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Endpoint di SQL Server][SqlServerEndpoint]

<span data-ttu-id="080a3-129">Sono disponibili due approcci per la limitazione dell'endpoint toothis traffico:</span><span class="sxs-lookup"><span data-stu-id="080a3-129">There are two approaches for restricting traffic toothis endpoint:</span></span>

* <span data-ttu-id="080a3-130">[Elenchi di controllo di accesso di rete][NetworkAccessControlLists] (ACL di rete)</span><span class="sxs-lookup"><span data-stu-id="080a3-130">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="080a3-131">[Gruppi di sicurezza di rete][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="080a3-131">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="080a3-132">Limitazione dell'accesso con un elenco di controllo di accesso di rete</span><span class="sxs-lookup"><span data-stu-id="080a3-132">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="080a3-133">È possibile proteggere la porta 1433 usando un elenco di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="080a3-133">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="080a3-134">gli indirizzi di esempio Hello di sotto delle whitelist client provenienti da all'interno di una rete virtuale e blocca l'accesso tooall altri client.</span><span class="sxs-lookup"><span data-stu-id="080a3-134">hello example below whitelists client addresses originating from inside of a virtual network, and blocks access tooall other clients.</span></span>

![Esempio di elenco di controllo di accesso di rete (ACL)][NetworkAccessControlListExample]

<span data-ttu-id="080a3-136">Tutte le applicazioni in esecuzione nell'ambiente del servizio App in hello stessa rete virtuale di SQL Server hello verrà istanza di SQL Server in grado di tooconnect toohello utilizzando hello **rete virtuale interna** indirizzo IP per la macchina virtuale di SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-136">Any applications running in App Service Environment in hello same virtual network as hello SQL Server will be able tooconnect toohello SQL Server instance using hello **VNet internal** IP address for hello SQL Server virtual machine.</span></span>  

<span data-ttu-id="080a3-137">stringa di connessione di esempio Hello sotto riferimenti hello SQL Server tramite il relativo indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="080a3-137">hello example connection string below references hello SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="080a3-138">Anche se macchina virtuale hello include anche un endpoint pubblico, tentativi di connessione tramite indirizzo IP pubblico hello verranno rifiutati a causa di ACL di rete hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-138">Although hello virtual machine has a public endpoint as well, connection attempts using hello public IP address will be rejected because of hello network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="080a3-139">Limitazione dell'accesso con un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="080a3-139">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="080a3-140">In alternativa, per proteggere l'accesso è possibile usare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="080a3-140">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="080a3-141">Gruppi di sicurezza di rete possono essere applicato tooindividual le macchine virtuali, o subnet tooa contenenti macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="080a3-141">Network security groups can be applied tooindividual virtual machines, or tooa subnet containing virtual machines.</span></span>

<span data-ttu-id="080a3-142">Un gruppo di sicurezza di rete deve prima toobe creato:</span><span class="sxs-lookup"><span data-stu-id="080a3-142">First a network security group needs toobe created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="080a3-143">Limitazione dell'accesso tooonly traffico di rete virtuale interna è molto semplice con un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="080a3-143">Restricting access tooonly VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="080a3-144">le regole predefinite di Hello in un gruppo di sicurezza di rete consentono l'accesso solo da altri client di rete in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="080a3-144">hello default rules in a network security group only allow access from other network clients in hello same virtual network.</span></span>

<span data-ttu-id="080a3-145">Di conseguenza il blocco di tooSQL accesso Server è semplice come l'applicazione di un gruppo di sicurezza di rete con impostazione predefinita le regole tooeither hello macchine virtuali in esecuzione SQL Server o subnet hello contenenti macchine virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="080a3-145">As a result locking down access tooSQL Server is as simple as applying a network security group with its default rules tooeither hello virtual machines running SQL Server, or hello subnet containing hello virtual machines.</span></span>

<span data-ttu-id="080a3-146">esempio Hello seguente si applica a una subnet contenente toohello della rete sicurezza gruppo:</span><span class="sxs-lookup"><span data-stu-id="080a3-146">hello sample below applies a network security group toohello containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="080a3-147">risultato finale Hello è un set di regole di sicurezza che bloccano l'accesso esterno, pur consentendo l'accesso di rete virtuale interna:</span><span class="sxs-lookup"><span data-stu-id="080a3-147">hello end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Regole di sicurezza di rete predefinite][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="080a3-149">introduttiva</span><span class="sxs-lookup"><span data-stu-id="080a3-149">Getting started</span></span>
<span data-ttu-id="080a3-150">Tutti gli articoli e in che modo-per per gli ambienti del servizio App sono disponibili in hello [file Leggimi per gli ambienti del servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="080a3-150">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="080a3-151">tooget avviato con gli ambienti del servizio App, vedere [tooApp introduzione dell'ambiente del servizio][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="080a3-151">tooget started with App Service Environments, see [Introduction tooApp Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="080a3-152">Per informazioni dettagliate sugli controllare il traffico in entrata tooyour ambiente del servizio App, vedere [controllare il traffico in entrata tooan ambiente del servizio App][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="080a3-152">For details around controlling inbound traffic tooyour App Service Environment, see [Controlling inbound traffic tooan App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="080a3-153">Per ulteriori informazioni sulla piattaforma Azure App Service hello, vedere [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="080a3-153">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[ControlInboundTraffic]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[NetworkAccessControlLists]: https://azure.microsoft.com/documentation/articles/virtual-networks-acl/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[IntroToAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ControlInboundASE]:  http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/ 

<!-- IMAGES -->
[SqlServerEndpoint]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/SqlServerEndpoint01.png
[NetworkAccessControlListExample]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/NetworkAcl01.png
[DefaultNetworkSecurityRules]: ./media/app-service-app-service-environment-securely-connecting-to-backend-resources/DefaultNetworkSecurityRules01.png 
