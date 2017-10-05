---
title: Connessione sicura alle risorse back-end da un ambiente del servizio app
description: Informazioni su come connettersi in modo sicuro alle risorse back-end da un ambiente del servizio app.
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
ms.openlocfilehash: 0b6d3a47dc429c469b37c2c74f546cfeca580358
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="securely-connecting-to-backend-resources-from-an-app-service-environment"></a><span data-ttu-id="e33b7-103">Connessione sicura alle risorse back-end da un ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="e33b7-103">Securely Connecting to Backend Resources from an App Service Environment</span></span>
## <a name="overview"></a><span data-ttu-id="e33b7-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e33b7-104">Overview</span></span>
<span data-ttu-id="e33b7-105">Poiché un ambiente del servizio app viene sempre creato in una **rete virtuale** di Azure Resource Manager **o** in una [rete virtuale][virtualnetwork] creata con il modello di distribuzione classica, le connessioni in uscita da un ambiente del servizio app ad altre risorse back-end possono transitare esclusivamente tramite la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-105">Since an App Service Environment is always created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model [virtual network][virtualnetwork], outbound connections from an App Service Environment to other backend resources can flow exclusively over the virtual network.</span></span>  <span data-ttu-id="e33b7-106">Con una modifica recente apportata a giugno 2016, gli ambienti del servizio app possono essere distribuiti nelle reti virtuali che usano intervalli di indirizzi pubblici o spazi di indirizzi RFC1918, ovvero</span><span class="sxs-lookup"><span data-stu-id="e33b7-106">With a recent change made in June 2016, ASEs can also be deployed into virtual networks that use either public address ranges, or RFC1918 address spaces (i.e.</span></span> <span data-ttu-id="e33b7-107">indirizzi privati.</span><span class="sxs-lookup"><span data-stu-id="e33b7-107">private addresses).</span></span>  

<span data-ttu-id="e33b7-108">Ad esempio, potrebbe essere in esecuzione un'istanza di SQL Server in un cluster di macchine virtuali con la porta 1433 bloccata.</span><span class="sxs-lookup"><span data-stu-id="e33b7-108">For example, there may be a SQL Server running on a cluster of virtual machines with port 1433 locked down.</span></span>  <span data-ttu-id="e33b7-109">In base all'elenco di controllo di accesso definito per l'endpoint, potrebbe essere consentito solo l'accesso da altre risorse nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-109">The endpoint may be ACLd to only allow access from other resources on the same virtual network.</span></span>  

<span data-ttu-id="e33b7-110">Oppure, gli endpoint sensibili potrebbero essere eseguiti in locale ed essere connessi ad Azure tramite connessioni [da sito a sito][SiteToSite] o connessioni [Azure ExpressRoute][ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="e33b7-110">As another example, sensitive endpoints may run on-premises and be connected to Azure via either [Site-to-Site][SiteToSite] or [Azure ExpressRoute][ExpressRoute] connections.</span></span>  <span data-ttu-id="e33b7-111">In questo caso, solo le risorse nelle reti virtuali connesse ai tunnel da sito a sito o ExpressRoute potrebbero accedere agli endpoint locali.</span><span class="sxs-lookup"><span data-stu-id="e33b7-111">As a result, only resources in virtual networks connected to the Site-to-Site or ExpressRoute tunnels will be able to access on-premises endpoints.</span></span>

<span data-ttu-id="e33b7-112">Per tutti questi scenari, le app in esecuzione in un ambiente del servizio app potranno connettersi in modo sicuro ai server e alle risorse.</span><span class="sxs-lookup"><span data-stu-id="e33b7-112">For all of these scenarios, apps running on an App Service Environment will be able to securely connect to the various servers and resources.</span></span>  <span data-ttu-id="e33b7-113">Il traffico in uscita dalle app in esecuzione in un ambiente del servizio app agli endpoint privati nella stessa rete virtuale (o connessi alla stessa rete virtuale) transiterà solo attraverso la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-113">Outbound traffic from apps running in an App Service Environment to private endpoints in the same virtual network (or connected to the same virtual network), will only flow over the virtual network.</span></span>  <span data-ttu-id="e33b7-114">Il traffico in uscita agli endpoint privati non transiterà attraverso la rete Internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="e33b7-114">Outbound traffic to private endpoints will not flow over the public Internet.</span></span>

<span data-ttu-id="e33b7-115">Si noti che un'eccezione è rappresentata dal traffico in uscita da un ambiente del servizio app agli endpoint all'interno di una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-115">One caveat applies to outbound traffic from an App Service Environment to endpoints within a virtual network.</span></span>  <span data-ttu-id="e33b7-116">Gli ambienti del servizio app non riescono a raggiungere gli endpoint delle macchine virtuali all'interno della **stessa** subnet dell'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e33b7-116">App Service Environments cannot reach endpoints of virtual machines located in the **same** subnet as the App Service Environment.</span></span>  <span data-ttu-id="e33b7-117">Questo normalmente non costituisce un problema, purché gli ambienti del servizio app vengano distribuiti in una subnet riservata a uso esclusivo dell'ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e33b7-117">This normally should not be a problem as long as App Service Environments are deployed into a subnet reserved for exclusive use by only the App Service Environment.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="outbound-connectivity-and-dns-requirements"></a><span data-ttu-id="e33b7-118">Requisiti per DNS e connettività in uscita</span><span class="sxs-lookup"><span data-stu-id="e33b7-118">Outbound Connectivity and DNS Requirements</span></span>
<span data-ttu-id="e33b7-119">Per un corretto funzionamento dell'ambiente del servizio app, è necessario l'accesso in uscita ai vari endpoint.</span><span class="sxs-lookup"><span data-stu-id="e33b7-119">For an App Service Environment to function properly, it requires outbound access to various endpoints.</span></span> <span data-ttu-id="e33b7-120">Un elenco completo degli endpoint esterni usati da un ambiente del servizio app è disponibile nella sezione "Requisiti della connettività di rete" dell'articolo [Configurazione di rete per ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) .</span><span class="sxs-lookup"><span data-stu-id="e33b7-120">A full list of the external endpoints used by an ASE is in the "Required Network Connectivity" section of the [Network Configuration for ExpressRoute](app-service-app-service-environment-network-configuration-expressroute.md#required-network-connectivity) article.</span></span>

<span data-ttu-id="e33b7-121">Gli ambienti del servizio app richiedono un'infrastruttura DNS valida configurata per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-121">App Service Environments require a valid DNS infrastructure configured for the virtual network.</span></span>  <span data-ttu-id="e33b7-122">Se per qualsiasi motivo viene modificata la configurazione DNS dopo aver creato un ambiente di servizio app, gli sviluppatori possono forzare un ambiente di servizio app per selezionare la nuova configurazione del DNS.</span><span class="sxs-lookup"><span data-stu-id="e33b7-122">If for any reason the DNS configuration is changed after an App Service Environment has been created, developers can force an App Service Environment to pick up the new DNS configuration.</span></span>  <span data-ttu-id="e33b7-123">L'attivazione di un riavvio di ambiente in sequenza mediante l'icona "Riavvia" posizionata nella parte superiore del pannello di gestione dell'ambiente del servizio app nel portale farà sì che l'ambiente selezioni la nuova configurazione del DNS.</span><span class="sxs-lookup"><span data-stu-id="e33b7-123">Triggering a rolling environment reboot using the "Restart" icon located at the top of the App Service Environment management blade in the portal will cause the environment to pick up the new DNS configuration.</span></span>

<span data-ttu-id="e33b7-124">È anche consigliabile che i server DNS personalizzati nella rete virtuale vengano configurati prima di creare un ambiente del servizio app.</span><span class="sxs-lookup"><span data-stu-id="e33b7-124">It is also recommended that any custom DNS servers on the vnet be setup ahead of time prior to creating an App Service Environment.</span></span>  <span data-ttu-id="e33b7-125">Se la configurazione DNS della rete virtuale viene modificata durante la creazione di un ambiente del servizio app, il processo di creazione dell'ambiente del servizio app avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e33b7-125">If a virtual network's DNS configuration is changed while an App Service Environment is being created, that will result in the App Service Environment creation process failing.</span></span>  <span data-ttu-id="e33b7-126">In modo analogo, se esiste un server DNS personalizzato nell’altra estremità di un gateway VPN e il server DNS è irraggiungibile o non disponibile, anche il processo di creazione dell’ambiente del servizio App avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="e33b7-126">In a similar vein, if a custom DNS server exists on the other end of a VPN gateway, and the DNS server is unreachable or unavailable, the App Service Environment creation process will also fail.</span></span>

## <a name="connecting-to-a-sql-server"></a><span data-ttu-id="e33b7-127">Connessione a un'istanza di SQL Server</span><span class="sxs-lookup"><span data-stu-id="e33b7-127">Connecting to a SQL Server</span></span>
<span data-ttu-id="e33b7-128">Una configurazione di SQL Server comune prevede un endpoint in ascolto sulla porta 1433:</span><span class="sxs-lookup"><span data-stu-id="e33b7-128">A common SQL Server configuration has an endpoint listening on port 1433:</span></span>

![Endpoint di SQL Server][SqlServerEndpoint]

<span data-ttu-id="e33b7-130">È possibile usare due approcci per limitare il traffico a questo endpoint:</span><span class="sxs-lookup"><span data-stu-id="e33b7-130">There are two approaches for restricting traffic to this endpoint:</span></span>

* <span data-ttu-id="e33b7-131">[Elenchi di controllo di accesso di rete][NetworkAccessControlLists] (ACL di rete)</span><span class="sxs-lookup"><span data-stu-id="e33b7-131">[Network Access Control Lists][NetworkAccessControlLists] (Network ACLs)</span></span>
* <span data-ttu-id="e33b7-132">[Gruppi di sicurezza di rete][NetworkSecurityGroups]</span><span class="sxs-lookup"><span data-stu-id="e33b7-132">[Network Security Groups][NetworkSecurityGroups]</span></span>

## <a name="restricting-access-with-a-network-acl"></a><span data-ttu-id="e33b7-133">Limitazione dell'accesso con un elenco di controllo di accesso di rete</span><span class="sxs-lookup"><span data-stu-id="e33b7-133">Restricting Access With a Network ACL</span></span>
<span data-ttu-id="e33b7-134">È possibile proteggere la porta 1433 usando un elenco di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="e33b7-134">Port 1433 can be secured using a network access control list.</span></span>  <span data-ttu-id="e33b7-135">L'esempio seguente illustra come consentire gli indirizzi client originati dall'interno di una rete virtuale e bloccare l'accesso a tutti gli altri client.</span><span class="sxs-lookup"><span data-stu-id="e33b7-135">The example below whitelists client addresses originating from inside of a virtual network, and blocks access to all other clients.</span></span>

![Esempio di elenco di controllo di accesso di rete (ACL)][NetworkAccessControlListExample]

<span data-ttu-id="e33b7-137">Tutte le applicazioni in esecuzione nell'ambiente del servizio app all'interno della stessa rete virtuale di SQL Server potranno connettersi all'istanza di SQL Server usando l'indirizzo IP **interno della rete virtuale** per la macchina virtuale SQL Server.</span><span class="sxs-lookup"><span data-stu-id="e33b7-137">Any applications running in App Service Environment in the same virtual network as the SQL Server will be able to connect to the SQL Server instance using the **VNet internal** IP address for the SQL Server virtual machine.</span></span>  

<span data-ttu-id="e33b7-138">La stringa di connessione di esempio seguente fa riferimento all'instanza di SQL Server usando l'indirizzo IP privato.</span><span class="sxs-lookup"><span data-stu-id="e33b7-138">The example connection string below references the SQL Server using its private IP address.</span></span>

    Server=tcp:10.0.1.6;Database=MyDatabase;User ID=MyUser;Password=PasswordHere;provider=System.Data.SqlClient

<span data-ttu-id="e33b7-139">Sebbene la macchina virtuale disponga anche di un endpoint pubblico, i tentativi di connessione usando l'indirizzo IP pubblico verranno rifiutati a causa dell'elenco di controllo di accesso di rete.</span><span class="sxs-lookup"><span data-stu-id="e33b7-139">Although the virtual machine has a public endpoint as well, connection attempts using the public IP address will be rejected because of the network ACL.</span></span> 

## <a name="restricting-access-with-a-network-security-group"></a><span data-ttu-id="e33b7-140">Limitazione dell'accesso con un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="e33b7-140">Restricting Access With a Network Security Group</span></span>
<span data-ttu-id="e33b7-141">In alternativa, per proteggere l'accesso è possibile usare un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="e33b7-141">An alternative approach for securing access is with a network security group.</span></span>  <span data-ttu-id="e33b7-142">I gruppi di sicurezza di rete possono essere applicati alle singole macchine virtuali o a una subnet contenente macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e33b7-142">Network security groups can be applied to individual virtual machines, or to a subnet containing virtual machines.</span></span>

<span data-ttu-id="e33b7-143">È prima necessario creare un gruppo di sicurezza di rete:</span><span class="sxs-lookup"><span data-stu-id="e33b7-143">First a network security group needs to be created:</span></span>

    New-AzureNetworkSecurityGroup -Name "testNSGexample" -Location "South Central US" -Label "Example network security group for an app service environment"

<span data-ttu-id="e33b7-144">La limitazione dell'accesso al solo traffico interno della rete virtuale con un gruppo di sicurezza di rete è un'operazione estremamente semplice.</span><span class="sxs-lookup"><span data-stu-id="e33b7-144">Restricting access to only VNet internal traffic is very simple with a network security group.</span></span>  <span data-ttu-id="e33b7-145">Le regole predefinite in un gruppo di sicurezza di rete consentono l'accesso solo da altri client di rete nella stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="e33b7-145">The default rules in a network security group only allow access from other network clients in the same virtual network.</span></span>

<span data-ttu-id="e33b7-146">Di conseguenza, è possibile bloccare l'accesso a SQL Server semplicemente applicando un gruppo di sicurezza di rete con le relative regole predefinite alle macchine virtuali che eseguono SQL Server o alla subnet contenente le macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e33b7-146">As a result locking down access to SQL Server is as simple as applying a network security group with its default rules to either the virtual machines running SQL Server, or the subnet containing the virtual machines.</span></span>

<span data-ttu-id="e33b7-147">L'esempio seguente mostra come applicare un gruppo di sicurezza di rete alla subnet contenente le macchine virtuali:</span><span class="sxs-lookup"><span data-stu-id="e33b7-147">The sample below applies a network security group to the containing subnet:</span></span>

    Get-AzureNetworkSecurityGroup -Name "testNSGExample" | Set-AzureNetworkSecurityGroupToSubnet -VirtualNetworkName 'testVNet' -SubnetName 'Subnet-1'

<span data-ttu-id="e33b7-148">Il risultato finale è costituito da un set di regole di sicurezza che blocca l'accesso esterno e consente l'accesso interno al traffico proveniente dalla rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="e33b7-148">The end result is a set of security rules that block external access, while allowing VNet internal access:</span></span>

![Regole di sicurezza di rete predefinite][DefaultNetworkSecurityRules]

## <a name="getting-started"></a><span data-ttu-id="e33b7-150">Introduzione</span><span class="sxs-lookup"><span data-stu-id="e33b7-150">Getting started</span></span>
<span data-ttu-id="e33b7-151">Tutti gli articoli e le procedure sugli ambienti del servizio app sono disponibili nel [file LEGGIMI per gli ambienti di servizio dell'applicazione](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="e33b7-151">All articles and How-To's for App Service Environments are available in the [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="e33b7-152">Per iniziare a usare gli ambienti del servizio app, vedere [Introduzione all'ambiente del servizio app][IntroToAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="e33b7-152">To get started with App Service Environments, see [Introduction to App Service Environment][IntroToAppServiceEnvironment]</span></span>

<span data-ttu-id="e33b7-153">Per informazioni dettagliate su come controllare il traffico in ingresso all'ambiente del servizio app, vedere [Controllo del traffico in ingresso a un ambiente del servizio app][ControlInboundASE]</span><span class="sxs-lookup"><span data-stu-id="e33b7-153">For details around controlling inbound traffic to your App Service Environment, see [Controlling inbound traffic to an App Service Environment][ControlInboundASE]</span></span>

<span data-ttu-id="e33b7-154">Per altre informazioni sulla piattaforma del servizio app di Azure, vedere l'articolo relativo al [servizio app di Azure][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="e33b7-154">For more information about the Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

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
