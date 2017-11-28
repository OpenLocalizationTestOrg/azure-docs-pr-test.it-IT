---
title: 'Configurare il tunneling forzato per connessioni di Azure da sito a sito: versione classica | Microsoft Docs'
description: Come tooredirect o 'force' tutti tooyour di sfondo del traffico associato a Internet posizione locale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a><span data-ttu-id="eeb16-103">Configurare il tunneling forzato utilizzando il modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="eeb16-103">Configure forced tunneling using hello classic deployment model</span></span>

<span data-ttu-id="eeb16-104">Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato.</span><span class="sxs-lookup"><span data-stu-id="eeb16-104">Forced tunneling lets you redirect or "force" all Internet-bound traffic back tooyour on-premises location via a Site-to-Site VPN tunnel for inspection and auditing.</span></span> <span data-ttu-id="eeb16-105">Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali.</span><span class="sxs-lookup"><span data-stu-id="eeb16-105">This is a critical security requirement for most enterprise IT policies.</span></span> <span data-ttu-id="eeb16-106">Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure passerà sempre dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit.</span><span class="sxs-lookup"><span data-stu-id="eeb16-106">Without forced tunneling, Internet-bound traffic from your VMs in Azure will always traverse from Azure network infrastructure directly out toohello Internet, without hello option tooallow you tooinspect or audit hello traffic.</span></span> <span data-ttu-id="eeb16-107">Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="eeb16-107">Unauthorized Internet access can potentially lead tooinformation disclosure or other types of security breaches.</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="eeb16-108">In questo articolo illustra la configurazione forzato tunneling per le reti virtuali create utilizzando il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-108">This article walks you through configuring forced tunneling for virtual networks created using hello classic deployment model.</span></span> <span data-ttu-id="eeb16-109">Il tunneling forzato può essere configurato tramite PowerShell, non tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-109">Forced tunneling can be configured by using PowerShell, not through hello portal.</span></span> <span data-ttu-id="eeb16-110">Se si desidera tooconfigure tunneling per modello di distribuzione di gestione risorse di hello forzato, è possibile selezionare articolo classico da hello segue l'elenco a discesa:</span><span class="sxs-lookup"><span data-stu-id="eeb16-110">If you want tooconfigure forced tunneling for hello Resource Manager deployment model, select classic article from hello following dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eeb16-111">PowerShell - Classico</span><span class="sxs-lookup"><span data-stu-id="eeb16-111">PowerShell - Classic</span></span>](vpn-gateway-about-forced-tunneling.md)
> * [<span data-ttu-id="eeb16-112">PowerShell - Gestione risorse</span><span class="sxs-lookup"><span data-stu-id="eeb16-112">PowerShell - Resource Manager</span></span>](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a><span data-ttu-id="eeb16-113">Problemi e considerazioni</span><span class="sxs-lookup"><span data-stu-id="eeb16-113">Requirements and considerations</span></span>
<span data-ttu-id="eeb16-114">Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente.</span><span class="sxs-lookup"><span data-stu-id="eeb16-114">Forced tunneling in Azure is configured via virtual network user-defined routes (UDR).</span></span> <span data-ttu-id="eeb16-115">Reindirizzamento del traffico tooan locale sito viene espresso come un gateway VPN di Azure toohello di Route predefinita.</span><span class="sxs-lookup"><span data-stu-id="eeb16-115">Redirecting traffic tooan on-premises site is expressed as a Default Route toohello Azure VPN gateway.</span></span> <span data-ttu-id="eeb16-116">Hello nella sezione seguente sono elencate la limitazione corrente hello della tabella di routing hello e le route per una rete virtuale di Azure:</span><span class="sxs-lookup"><span data-stu-id="eeb16-116">hello following section lists hello current limitation of hello routing table and routes for an Azure Virtual Network:</span></span>

* <span data-ttu-id="eeb16-117">Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata.</span><span class="sxs-lookup"><span data-stu-id="eeb16-117">Each virtual network subnet has a built-in, system routing table.</span></span> <span data-ttu-id="eeb16-118">tabella di routing sistema Hello è hello seguenti tre gruppi di route:</span><span class="sxs-lookup"><span data-stu-id="eeb16-118">hello system routing table has hello following three groups of routes:</span></span>

  * <span data-ttu-id="eeb16-119">**Route di rete virtuale locale:** direttamente toohello destinazione macchine virtuali in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="eeb16-119">**Local VNet routes:** Directly toohello destination VMs in hello same virtual network.</span></span>
  * <span data-ttu-id="eeb16-120">**Le route locali:** gateway VPN di Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-120">**On-premises routes:** toohello Azure VPN gateway.</span></span>
  * <span data-ttu-id="eeb16-121">**Route predefinita:** direttamente toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="eeb16-121">**Default route:** Directly toohello Internet.</span></span> <span data-ttu-id="eeb16-122">I pacchetti destinati toohello gli indirizzi IP privati non coperti da route hello due precedenti verranno eliminati.</span><span class="sxs-lookup"><span data-stu-id="eeb16-122">Packets destined toohello private IP addresses not covered by hello previous two routes will be dropped.</span></span>
* <span data-ttu-id="eeb16-123">Con la versione di hello delle route definite dall'utente, è possibile creare una route predefinita di un tooadd tabella di routing e quindi associare hello routing tabella tooyour rete virtuale subnet tooenable forzato tunneling su queste subnet.</span><span class="sxs-lookup"><span data-stu-id="eeb16-123">With hello release of user-defined routes, you can create a routing table tooadd a default route, and then associate hello routing table tooyour VNet subnet(s) tooenable forced tunneling on those subnets.</span></span>
* <span data-ttu-id="eeb16-124">È necessario un sito"predefinito" tooset tra rete virtuale connessa toohello hello cross-premise siti locali.</span><span class="sxs-lookup"><span data-stu-id="eeb16-124">You need tooset a "default site" among hello cross-premises local sites connected toohello virtual network.</span></span>
* <span data-ttu-id="eeb16-125">Il tunneling forzato deve essere associato a una rete virtuale che disponga di un gateway VPN (non un gateway statico).</span><span class="sxs-lookup"><span data-stu-id="eeb16-125">Forced tunneling must be associated with a VNet that has a dynamic routing VPN gateway (not a static gateway).</span></span>
* <span data-ttu-id="eeb16-126">Il tunneling forzato ExpressRoute non viene configurato tramite questo meccanismo, ma è invece abilitato annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering.</span><span class="sxs-lookup"><span data-stu-id="eeb16-126">ExpressRoute forced tunneling is not configured via this mechanism, but instead, is enabled by advertising a default route via hello ExpressRoute BGP peering sessions.</span></span> <span data-ttu-id="eeb16-127">Vedere hello [documentazione di ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="eeb16-127">Please see hello [ExpressRoute Documentation](https://azure.microsoft.com/documentation/services/expressroute/) for more information.</span></span>

## <a name="configuration-overview"></a><span data-ttu-id="eeb16-128">Panoramica della configurazione</span><span class="sxs-lookup"><span data-stu-id="eeb16-128">Configuration overview</span></span>
<span data-ttu-id="eeb16-129">Nell'esempio seguente di hello, con tunneling hello front-end subnet non è forzato.</span><span class="sxs-lookup"><span data-stu-id="eeb16-129">In hello following example, hello Frontend subnet is not forced tunneled.</span></span> <span data-ttu-id="eeb16-130">i carichi di lavoro Hello nella subnet front-end hello continuare tooaccept e rispondere toocustomer richieste da hello Internet direttamente.</span><span class="sxs-lookup"><span data-stu-id="eeb16-130">hello workloads in hello Frontend subnet can continue tooaccept and respond toocustomer requests from hello Internet directly.</span></span> <span data-ttu-id="eeb16-131">Hello subnet di livello intermedio e back-end devono essere forzate tunnel.</span><span class="sxs-lookup"><span data-stu-id="eeb16-131">hello Mid-tier and Backend subnets are forced tunneled.</span></span> <span data-ttu-id="eeb16-132">Tutte le connessioni in uscita da tali toohello due subnet Internet sarà tooan forzata o reindirizzato nuovamente nel sito locale tramite uno dei tunnel VPN S2S hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-132">Any outbound connections from these two subnets toohello Internet will be forced or redirected back tooan on-premises site via one of hello S2S VPN tunnels.</span></span>

<span data-ttu-id="eeb16-133">Questo consente toorestrict e controllare l'accesso a Internet dalle macchine virtuali o nel cloud servizi in Azure, continuando tooenable l'architettura del servizio a più livelli necessaria.</span><span class="sxs-lookup"><span data-stu-id="eeb16-133">This allows you toorestrict and inspect Internet access from your virtual machines or cloud services in Azure, while continuing tooenable your multi-tier service architecture required.</span></span> <span data-ttu-id="eeb16-134">È inoltre possibile applicare forzato tunneling toohello intere reti virtuali se sono non presenti carichi di lavoro con connessione Internet nelle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="eeb16-134">You also can apply forced tunneling toohello entire virtual networks if there are no Internet-facing workloads in your virtual networks.</span></span>

![Tunneling forzato](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a><span data-ttu-id="eeb16-136">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="eeb16-136">Before you begin</span></span>
<span data-ttu-id="eeb16-137">Verificare di aver hello elementi prima della configurazione iniziale.</span><span class="sxs-lookup"><span data-stu-id="eeb16-137">Verify that you have hello following items before beginning configuration.</span></span>

* <span data-ttu-id="eeb16-138">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="eeb16-138">An Azure subscription.</span></span> <span data-ttu-id="eeb16-139">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeb16-139">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eeb16-140">Una rete virtuale configurata.</span><span class="sxs-lookup"><span data-stu-id="eeb16-140">A configured virtual network.</span></span> 
* <span data-ttu-id="eeb16-141">versione più recente di Hello di hello cmdlet di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eeb16-141">hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="eeb16-142">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-142">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

## <a name="configure-forced-tunneling"></a><span data-ttu-id="eeb16-143">È possibile configurare il tunneling forzato?</span><span class="sxs-lookup"><span data-stu-id="eeb16-143">Configure forced tunneling</span></span>
<span data-ttu-id="eeb16-144">Hello seguente procedura consente di specificare il tunneling forzato per una rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="eeb16-144">hello following procedure will help you specify forced tunneling for a virtual network.</span></span> <span data-ttu-id="eeb16-145">passaggi di configurazione Hello corrispondono toohello file di configurazione di rete di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="eeb16-145">hello configuration steps correspond toohello VNet network configuration file.</span></span>

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

<span data-ttu-id="eeb16-146">In questo esempio, la rete virtuale hello "MultiTier-VNet" include tre subnet: subnet 'Front-end', 'Midtier' e 'Back-end', con le connessioni locali tra quattro: 'DefaultSiteHQ' e tre rami.</span><span class="sxs-lookup"><span data-stu-id="eeb16-146">In this example, hello virtual network 'MultiTier-VNet' has three subnets: 'Frontend', 'Midtier', and 'Backend' subnets, with four cross premises connections: 'DefaultSiteHQ', and three Branches.</span></span> 

<span data-ttu-id="eeb16-147">passaggi di Hello verranno impostato hello 'DefaultSiteHQ' come connessione di hello predefinita del sito per il tunneling forzato e configurare hello Midtier e Backend subnet toouse il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="eeb16-147">hello steps will set hello 'DefaultSiteHQ' as hello default site connection for forced tunneling, and configure hello Midtier and Backend subnets toouse forced tunneling.</span></span>

1. <span data-ttu-id="eeb16-148">Creare una tabella di routing.</span><span class="sxs-lookup"><span data-stu-id="eeb16-148">Create a routing table.</span></span> <span data-ttu-id="eeb16-149">Utilizzare hello cmdlet toocreate dopo la tabella di routing.</span><span class="sxs-lookup"><span data-stu-id="eeb16-149">Use hello following cmdlet toocreate your route table.</span></span>

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. <span data-ttu-id="eeb16-150">Aggiungere una tabella di routing toohello di route predefinita.</span><span class="sxs-lookup"><span data-stu-id="eeb16-150">Add a default route toohello routing table.</span></span> 

  <span data-ttu-id="eeb16-151">Hello esempio seguente aggiunge una route toohello tabella di routing predefinita creata nel passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="eeb16-151">hello following example adds a default route toohello routing table created in Step 1.</span></span> <span data-ttu-id="eeb16-152">Si noti che hello solo route supportata è il prefisso di destinazione hello di "0.0.0.0/0" toohello hop successivo "VPNGateway".</span><span class="sxs-lookup"><span data-stu-id="eeb16-152">Note that hello only route supported is hello destination prefix of "0.0.0.0/0" toohello "VPNGateway" NextHop.</span></span>

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. <span data-ttu-id="eeb16-153">Associare subnet toohello tabella di routing hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-153">Associate hello routing table toohello subnets.</span></span> 

  <span data-ttu-id="eeb16-154">Dopo che viene creata una tabella di routing e l'aggiunta di una route, associare subnet di rete virtuale tooa tabella route hello utilizzare hello tooadd riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="eeb16-154">After a routing table is created and a route added, use hello following example tooadd or associate hello route table tooa VNet subnet.</span></span> <span data-ttu-id="eeb16-155">esempio Hello aggiunge hello route nella tabella "MyRouteTable" toohello Midtier e subnet di back-end di VNet MultiTier-VNet.</span><span class="sxs-lookup"><span data-stu-id="eeb16-155">hello example adds hello route table "MyRouteTable" toohello Midtier and Backend subnets of VNet MultiTier-VNet.</span></span>

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. <span data-ttu-id="eeb16-156">Assegnare un sito predefinito per il tunneling forzato.</span><span class="sxs-lookup"><span data-stu-id="eeb16-156">Assign a default site for forced tunneling.</span></span> 

  <span data-ttu-id="eeb16-157">In hello nel passaggio precedente, gli script di cmdlet di esempio hello hello tabella di routing creata e associata tootwo di tabella hello route della subnet della rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="eeb16-157">In hello preceding step, hello sample cmdlet scripts created hello routing table and associated hello route table tootwo of hello VNet subnets.</span></span> <span data-ttu-id="eeb16-158">passaggio rimanenti Hello è tooselect un sito locale tra le connessioni a più siti hello della rete virtuale di hello come hello sito o tunnel predefinito.</span><span class="sxs-lookup"><span data-stu-id="eeb16-158">hello remaining step is tooselect a local site among hello multi-site connections of hello virtual network as hello default site or tunnel.</span></span>

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a><span data-ttu-id="eeb16-159">Ulteriori cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="eeb16-159">Additional PowerShell cmdlets</span></span>
### <a name="toodelete-a-route-table"></a><span data-ttu-id="eeb16-160">toodelete una tabella di routing</span><span class="sxs-lookup"><span data-stu-id="eeb16-160">toodelete a route table</span></span>

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a><span data-ttu-id="eeb16-161">toolist una tabella di routing</span><span class="sxs-lookup"><span data-stu-id="eeb16-161">toolist a route table</span></span>

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a><span data-ttu-id="eeb16-162">toodelete una route da una tabella di route</span><span class="sxs-lookup"><span data-stu-id="eeb16-162">toodelete a route from a route table</span></span>

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a><span data-ttu-id="eeb16-163">tooremove una route da una subnet</span><span class="sxs-lookup"><span data-stu-id="eeb16-163">tooremove a route from a subnet</span></span>

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a><span data-ttu-id="eeb16-164">tabella di route hello toolist associata a una subnet</span><span class="sxs-lookup"><span data-stu-id="eeb16-164">toolist hello route table associated with a subnet</span></span>

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a><span data-ttu-id="eeb16-165">un sito predefinito da un gateway VPN VNet tooremove</span><span class="sxs-lookup"><span data-stu-id="eeb16-165">tooremove a default site from a VNet VPN gateway</span></span>

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```