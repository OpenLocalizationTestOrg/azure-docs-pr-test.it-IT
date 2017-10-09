---
title: 'Connettersi a una rete virtuale di tooanother di rete virtuale di Azure: PowerShell | Documenti Microsoft'
description: In questo articolo viene illustrata la connessione tra reti virtuali utilizzando Gestione risorse di Azure e PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a><span data-ttu-id="72128-103">Configurare una connessione gateway VPN tra reti virtuali usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="72128-103">Configure a VNet-to-VNet VPN gateway connection using PowerShell</span></span>

<span data-ttu-id="72128-104">In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="72128-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="72128-105">Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="72128-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="72128-106">Quando le reti virtuali connessione da sottoscrizioni diverse, le sottoscrizioni di hello non necessaria toobe associato hello stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72128-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="72128-107">passaggi Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello e utilizzano PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72128-107">hello steps in this article apply toohello Resource Manager deployment model and use PowerShell.</span></span> <span data-ttu-id="72128-108">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="72128-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="72128-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="72128-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="72128-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72128-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="72128-111">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="72128-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="72128-112">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="72128-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="72128-113">Connettersi tra modelli di distribuzione diversi - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="72128-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="72128-114">Connettersi tra modelli di distribuzione diversi - PowerShell</span><span class="sxs-lookup"><span data-stu-id="72128-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="72128-115">La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito.</span><span class="sxs-lookup"><span data-stu-id="72128-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="72128-116">Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="72128-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="72128-117">Se le reti virtuali si trovano in hello stessa area, è opportuno tooconsider collegarli tramite Peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="72128-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="72128-118">Peering reti virtuali non usa un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="72128-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="72128-119">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72128-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="72128-120">La comunicazione tra reti virtuali può essere associata a configurazioni multisito.</span><span class="sxs-lookup"><span data-stu-id="72128-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="72128-121">Consente di stabilire le topologie di rete che combinano connettività cross-premise con connettività di rete virtuale tra, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="72128-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Informazioni sulle connessioni](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="72128-123">Perché connettere reti virtuali?</span><span class="sxs-lookup"><span data-stu-id="72128-123">Why connect virtual networks?</span></span>

<span data-ttu-id="72128-124">Si consiglia le reti virtuali tooconnect per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="72128-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="72128-125">**Presenza e ridondanza in più aree geografiche**</span><span class="sxs-lookup"><span data-stu-id="72128-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="72128-126">È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="72128-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="72128-127">Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="72128-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="72128-128">Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="72128-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="72128-129">**Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**</span><span class="sxs-lookup"><span data-stu-id="72128-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="72128-130">Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse a causa di tooisolation o i requisiti amministrativi.</span><span class="sxs-lookup"><span data-stu-id="72128-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="72128-131">Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="72128-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="72128-132">Quale procedura è consigliabile seguire?</span><span class="sxs-lookup"><span data-stu-id="72128-132">Which set of steps should I use?</span></span>

<span data-ttu-id="72128-133">Questo articolo riporta due diverse procedure.</span><span class="sxs-lookup"><span data-stu-id="72128-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="72128-134">Un set di passaggi per [hello di reti virtuali che si trovano nella stessa sottoscrizione](#samesub)e un altro per [reti virtuali che risiedono in diverse sottoscrizioni](#difsub).</span><span class="sxs-lookup"><span data-stu-id="72128-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="72128-135">Hello differenza principale tra set hello è se è possibile creare e configurare tutte le risorse virtuali rete e gateway all'interno di hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72128-135">hello key difference between hello sets is whether you can create and configure all virtual network and gateway resources within hello same PowerShell session.</span></span>

<span data-ttu-id="72128-136">Hello passaggi in questo articolo usano le variabili dichiarate all'inizio di hello di ogni sezione.</span><span class="sxs-lookup"><span data-stu-id="72128-136">hello steps in this article use variables that are declared at hello beginning of each section.</span></span> <span data-ttu-id="72128-137">Se si sono già lavorando con le reti virtuali esistenti, modificare impostazioni di hello variabili tooreflect hello nel proprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="72128-137">If you already are working with existing VNets, modify hello variables tooreflect hello settings in your own environment.</span></span> <span data-ttu-id="72128-138">Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="72128-138">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

## <span data-ttu-id="72128-139"><a name="samesub"></a>Come tooconnect reti virtuali che si trovano in hello stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="72128-139"><a name="samesub"></a>How tooconnect VNets that are in hello same subscription</span></span>

![Diagramma V2V](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="72128-141">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="72128-141">Before you begin</span></span>

<span data-ttu-id="72128-142">Prima di iniziare, è necessario tooinstall hello più recente dei cmdlet di Azure Resource Manager PowerShell hello, almeno 4.0 o versione successivo.</span><span class="sxs-lookup"><span data-stu-id="72128-142">Before beginning, you need tooinstall hello latest version of hello Azure Resource Manager PowerShell cmdlets, at least 4.0 or later.</span></span> <span data-ttu-id="72128-143">Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="72128-143">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <span data-ttu-id="72128-144"><a name="Step1"></a>Passaggio 1: Pianificare gli intervalli di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="72128-144"><a name="Step1"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="72128-145">In hello alla procedura seguente, vengono create due reti virtuali insieme le subnet gateway rispettivi e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="72128-145">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="72128-146">È quindi creare una connessione VPN tra hello due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="72128-146">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="72128-147">È importante tooplan hello indirizzi IP per la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="72128-147">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="72128-148">Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="72128-148">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="72128-149">In questi esempi non viene incluso un server DNS.</span><span class="sxs-lookup"><span data-stu-id="72128-149">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="72128-150">Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="72128-150">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="72128-151">Utilizziamo hello seguente i valori negli esempi di hello:</span><span class="sxs-lookup"><span data-stu-id="72128-151">We use hello following values in hello examples:</span></span>

<span data-ttu-id="72128-152">**Valori per TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="72128-152">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="72128-153">Nome della rete virtuale: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="72128-153">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="72128-154">Gruppo di risorse: TestRG1</span><span class="sxs-lookup"><span data-stu-id="72128-154">Resource Group: TestRG1</span></span>
* <span data-ttu-id="72128-155">Location: Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="72128-155">Location: East US</span></span>
* <span data-ttu-id="72128-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="72128-156">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="72128-157">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-157">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="72128-158">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-158">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="72128-159">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="72128-159">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="72128-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="72128-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="72128-161">IP pubblico: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="72128-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="72128-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="72128-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="72128-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="72128-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="72128-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="72128-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="72128-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="72128-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="72128-166">**Valori per TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="72128-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="72128-167">Nome della rete virtuale: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="72128-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="72128-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="72128-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="72128-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="72128-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="72128-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="72128-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="72128-172">Gruppo di risorse: TestRG4</span><span class="sxs-lookup"><span data-stu-id="72128-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="72128-173">Località: Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="72128-173">Location: West US</span></span>
* <span data-ttu-id="72128-174">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="72128-174">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="72128-175">IP pubblico: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="72128-175">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="72128-176">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="72128-176">VPNType: RouteBased</span></span>
* <span data-ttu-id="72128-177">Connessione: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="72128-177">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="72128-178">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="72128-178">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="72128-179"><a name="Step2"></a>Passaggio 2: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="72128-179"><a name="Step2"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="72128-180">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="72128-180">Declare your variables.</span></span> <span data-ttu-id="72128-181">In questo esempio dichiara variabili di hello utilizzando valori hello per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="72128-181">This example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="72128-182">Nella maggior parte dei casi, è necessario sostituire i valori hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="72128-182">In most cases, you should replace hello values with your own.</span></span> <span data-ttu-id="72128-183">Tuttavia, è possibile utilizzare queste variabili, se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="72128-183">However, you can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="72128-184">Modificare le variabili di hello se necessario, quindi copiare e incollarli nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72128-184">Modify hello variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. <span data-ttu-id="72128-185">Connettere tooyour account.</span><span class="sxs-lookup"><span data-stu-id="72128-185">Connect tooyour account.</span></span> <span data-ttu-id="72128-186">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="72128-186">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="72128-187">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="72128-187">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="72128-188">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="72128-188">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. <span data-ttu-id="72128-189">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="72128-189">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="72128-190">Creazione di configurazioni di subnet per TestVNet1 hello.</span><span class="sxs-lookup"><span data-stu-id="72128-190">Create hello subnet configurations for TestVNet1.</span></span> <span data-ttu-id="72128-191">L'esempio seguente mostra come creare una rete virtuale denominata TestVNet1 e tre subnet, denominate rispettivamente GatewaySubnet, FrontEnd e Backend.</span><span class="sxs-lookup"><span data-stu-id="72128-191">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="72128-192">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="72128-192">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="72128-193">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="72128-193">If you name it something else, your gateway creation fails.</span></span>

  <span data-ttu-id="72128-194">Hello esempio seguente usa le variabili di hello impostato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="72128-194">hello following example uses hello variables that you set earlier.</span></span> <span data-ttu-id="72128-195">In questo esempio subnet del gateway hello utilizza un /27.</span><span class="sxs-lookup"><span data-stu-id="72128-195">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="72128-196">Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando almeno /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="72128-196">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="72128-197">In questo modo per sufficiente indirizzi tooaccommodate possibili configurazioni aggiuntive che è possibile in hello future.</span><span class="sxs-lookup"><span data-stu-id="72128-197">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="72128-198">Creare TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-198">Create TestVNet1.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="72128-199">Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta.</span><span class="sxs-lookup"><span data-stu-id="72128-199">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="72128-200">Si noti che hello AllocationMethod è dinamico.</span><span class="sxs-lookup"><span data-stu-id="72128-200">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="72128-201">È possibile specificare l'indirizzo IP hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="72128-201">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="72128-202">È il gateway tooyour allocata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="72128-202">It's dynamically allocated tooyour gateway.</span></span> 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="72128-203">Creare una configurazione del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="72128-203">Create hello gateway configuration.</span></span> <span data-ttu-id="72128-204">configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="72128-204">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="72128-205">Utilizzare toocreate esempio hello la configurazione del gateway.</span><span class="sxs-lookup"><span data-stu-id="72128-205">Use hello example toocreate your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="72128-206">Creare il gateway hello per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-206">Create hello gateway for TestVNet1.</span></span> <span data-ttu-id="72128-207">In questo passaggio viene creato il gateway di rete virtuale hello per le TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-207">In this step, you create hello virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="72128-208">Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="72128-208">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="72128-209">Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU.</span><span class="sxs-lookup"><span data-stu-id="72128-209">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="72128-210">Passaggio 3 - Creare e configurare TestVNet4</span><span class="sxs-lookup"><span data-stu-id="72128-210">Step 3 - Create and configure TestVNet4</span></span>

<span data-ttu-id="72128-211">Dopo aver configurato TestVNet1, creare TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="72128-211">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="72128-212">Eseguire operazioni di hello seguenti, sostituendo i valori hello con il proprio quando necessario.</span><span class="sxs-lookup"><span data-stu-id="72128-212">Follow hello steps below, replacing hello values with your own when needed.</span></span> <span data-ttu-id="72128-213">Questo passaggio può essere eseguito nell'hello stessa sessione di PowerShell perché si trova in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72128-213">This step can be done within hello same PowerShell session because it is in hello same subscription.</span></span>

1. <span data-ttu-id="72128-214">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="72128-214">Declare your variables.</span></span> <span data-ttu-id="72128-215">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="72128-215">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. <span data-ttu-id="72128-216">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="72128-216">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="72128-217">Creazione di configurazioni di subnet per TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="72128-217">Create hello subnet configurations for TestVNet4.</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="72128-218">Creare TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="72128-218">Create TestVNet4.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="72128-219">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="72128-219">Request a public IP address.</span></span>

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="72128-220">Creare una configurazione del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="72128-220">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="72128-221">Creare il gateway TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="72128-221">Create hello TestVNet4 gateway.</span></span> <span data-ttu-id="72128-222">Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway selezionato hello SKU.</span><span class="sxs-lookup"><span data-stu-id="72128-222">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a><span data-ttu-id="72128-223">Passaggio 4: creare connessioni hello</span><span class="sxs-lookup"><span data-stu-id="72128-223">Step 4 - Create hello connections</span></span>

1. <span data-ttu-id="72128-224">Ottenere entrambi i gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="72128-224">Get both virtual network gateways.</span></span> <span data-ttu-id="72128-225">Se entrambi i gateway hello hello stessa sottoscrizione, come nell'esempio hello, è possibile completare questo passaggio in hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="72128-225">If both of hello gateways are in hello same subscription, as they are in hello example, you can complete this step in hello same PowerShell session.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="72128-226">Creare hello TestVNet1 tooTestVNet4 connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-226">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="72128-227">In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="72128-227">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="72128-228">Verrà visualizzata una chiave condivisa a cui fa riferimento negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="72128-228">You'll see a shared key referenced in hello examples.</span></span> <span data-ttu-id="72128-229">È possibile utilizzare i valori per la chiave condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="72128-229">You can use your own values for hello shared key.</span></span> <span data-ttu-id="72128-230">cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="72128-230">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="72128-231">Creazione di una connessione può richiedere poco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="72128-231">Creating a connection can take a short while toocomplete.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="72128-232">Creare hello TestVNet4 tooTestVNet1 connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-232">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="72128-233">Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-233">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="72128-234">Assicurarsi che le chiavi condivise hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="72128-234">Make sure hello shared keys match.</span></span> <span data-ttu-id="72128-235">verrà stabilita connessione Hello dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="72128-235">hello connection will be established after a few minutes.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="72128-236">Verificare la connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-236">Verify your connection.</span></span> <span data-ttu-id="72128-237">Vedere la sezione hello [come tooverify connessione](#verify).</span><span class="sxs-lookup"><span data-stu-id="72128-237">See hello section [How tooverify your connection](#verify).</span></span>

## <span data-ttu-id="72128-238"><a name="difsub"></a>Come tooconnect reti virtuali che si trovano in sottoscrizioni diverse</span><span class="sxs-lookup"><span data-stu-id="72128-238"><a name="difsub"></a>How tooconnect VNets that are in different subscriptions</span></span>

![Diagramma V2V](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="72128-240">In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5,</span><span class="sxs-lookup"><span data-stu-id="72128-240">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="72128-241">che si trovano in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="72128-241">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="72128-242">le sottoscrizioni di Hello non è necessario toobe associato hello stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="72128-242">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="72128-243">Hello differenza tra questi passaggi e il set precedente hello consiste nel fatto che alcuni dei passaggi di configurazione hello necessario toobe eseguita in una sessione di PowerShell separata nel contesto di hello di sottoscrizione secondo hello.</span><span class="sxs-lookup"><span data-stu-id="72128-243">hello difference between these steps and hello previous set is that some of hello configuration steps need toobe performed in a separate PowerShell session in hello context of hello second subscription.</span></span> <span data-ttu-id="72128-244">In particolare quando le sottoscrizioni di hello due appartengono toodifferent organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="72128-244">Especially when hello two subscriptions belong toodifferent organizations.</span></span>

### <a name="step-5---create-and-configure-testvnet1"></a><span data-ttu-id="72128-245">Passaggio 5: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="72128-245">Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="72128-246">È necessario completare [passaggio 1](#Step1) e [passaggio 2](#Step2) da hello precedente sezione toocreate e configurare TestVNet1 hello Gateway VPN per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-246">You must complete [Step 1](#Step1) and [Step 2](#Step2) from hello previous section toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="72128-247">Per questa configurazione, non è necessario toocreate TestVNet4 dalla sezione precedente hello, sebbene se viene creato, non creerà conflitti con questa procedura.</span><span class="sxs-lookup"><span data-stu-id="72128-247">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="72128-248">Dopo aver completato i passaggi 1 e 2 di passaggio, continuare con passaggio 6 toocreate TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="72128-248">Once you complete Step 1 and Step 2, continue with Step 6 toocreate TestVNet5.</span></span> 

### <a name="step-6---verify-hello-ip-address-ranges"></a><span data-ttu-id="72128-249">Passaggio 6: verificare gli intervalli di indirizzi IP hello</span><span class="sxs-lookup"><span data-stu-id="72128-249">Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="72128-250">È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet5, non si sovrapponga ad altri di intervalli di rete virtuale o intervalli di gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="72128-250">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="72128-251">In questo esempio, le reti virtuali hello possono appartenere toodifferent organizzazioni.</span><span class="sxs-lookup"><span data-stu-id="72128-251">In this example, hello virtual networks may belong toodifferent organizations.</span></span> <span data-ttu-id="72128-252">Per questo esercizio, è possibile utilizzare i seguenti valori per hello TestVNet5 hello:</span><span class="sxs-lookup"><span data-stu-id="72128-252">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="72128-253">**Valori per TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="72128-253">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="72128-254">Nome della rete virtuale: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="72128-254">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="72128-255">Gruppo di risorse: TestRG5</span><span class="sxs-lookup"><span data-stu-id="72128-255">Resource Group: TestRG5</span></span>
* <span data-ttu-id="72128-256">Ubicazione: Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="72128-256">Location: Japan East</span></span>
* <span data-ttu-id="72128-257">TestVNet5: 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="72128-257">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="72128-258">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-258">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="72128-259">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="72128-259">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="72128-260">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="72128-260">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="72128-261">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="72128-261">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="72128-262">IP pubblico: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="72128-262">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="72128-263">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="72128-263">VPNType: RouteBased</span></span>
* <span data-ttu-id="72128-264">Connessione: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="72128-264">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="72128-265">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="72128-265">ConnectionType: VNet2VNet</span></span>

### <a name="step-7---create-and-configure-testvnet5"></a><span data-ttu-id="72128-266">Passaggio 7: Creare e configurare TestVNet5</span><span class="sxs-lookup"><span data-stu-id="72128-266">Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="72128-267">Questo passaggio deve essere eseguito nel contesto di hello della nuova sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="72128-267">This step must be done in hello context of hello new subscription.</span></span> <span data-ttu-id="72128-268">Questa parte può essere eseguita dall'amministratore di hello in un'altra organizzazione che possiede la sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="72128-268">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span>

1. <span data-ttu-id="72128-269">Dichiarare le variabili.</span><span class="sxs-lookup"><span data-stu-id="72128-269">Declare your variables.</span></span> <span data-ttu-id="72128-270">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="72128-270">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="72128-271">Connettersi toosubscription 5.</span><span class="sxs-lookup"><span data-stu-id="72128-271">Connect toosubscription 5.</span></span> <span data-ttu-id="72128-272">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-272">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="72128-273">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="72128-273">Use hello following sample toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="72128-274">Controllare le sottoscrizioni di hello per account hello.</span><span class="sxs-lookup"><span data-stu-id="72128-274">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="72128-275">Specificare una sottoscrizione di hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="72128-275">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="72128-276">Creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="72128-276">Create a new resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="72128-277">Creazione di configurazioni di subnet per TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="72128-277">Create hello subnet configurations for TestVNet5.</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="72128-278">Creare TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="72128-278">Create TestVNet5.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="72128-279">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="72128-279">Request a public IP address.</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="72128-280">Creare una configurazione del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="72128-280">Create hello gateway configuration.</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="72128-281">Creare il gateway TestVNet5 hello.</span><span class="sxs-lookup"><span data-stu-id="72128-281">Create hello TestVNet5 gateway.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a><span data-ttu-id="72128-282">Passaggio 8: creare connessioni hello</span><span class="sxs-lookup"><span data-stu-id="72128-282">Step 8 - Create hello connections</span></span>

<span data-ttu-id="72128-283">In questo esempio, perché sono gateway hello in diverse sottoscrizioni hello, è stato suddividere questo passaggio in due sessioni di PowerShell contrassegnate come [sottoscrizione 1] e [sottoscrizione 5].</span><span class="sxs-lookup"><span data-stu-id="72128-283">In this example, because hello gateways are in hello different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="72128-284">**[Sottoscrizione 1]**  Get gateway di rete virtuale hello per sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="72128-284">**[Subscription 1]** Get hello virtual network gateway for Subscription 1.</span></span> <span data-ttu-id="72128-285">Accedere e connettersi tooSubscription 1 prima di eseguire l'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="72128-285">Log in and connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  <span data-ttu-id="72128-286">Copia output di hello di hello segue gli elementi e inviare questi amministratore toohello 5 sottoscrizione tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="72128-286">Copy hello output of hello following elements and send these toohello administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  <span data-ttu-id="72128-287">Questi due elementi avrà toohello simile a valori output di esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="72128-287">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="72128-288">**[Sottoscrizione 5]**  Get gateway di rete virtuale hello per 5 di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="72128-288">**[Subscription 5]** Get hello virtual network gateway for Subscription 5.</span></span> <span data-ttu-id="72128-289">Accedere e connettersi tooSubscription 5 prima di eseguire l'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="72128-289">Log in and connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  <span data-ttu-id="72128-290">Copia output di hello di hello segue gli elementi e inviare questi amministratore toohello 1 sottoscrizione tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="72128-290">Copy hello output of hello following elements and send these toohello administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  <span data-ttu-id="72128-291">Questi due elementi avrà toohello simile a valori output di esempio riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="72128-291">These two elements will have values similar toohello following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="72128-292">**[Sottoscrizione 1]**  Creare hello TestVNet1 tooTestVNet5 connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-292">**[Subscription 1]** Create hello TestVNet1 tooTestVNet5 connection.</span></span> <span data-ttu-id="72128-293">In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="72128-293">In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="72128-294">Hello differenza è che vnet5gw $ non è possibile ottenere direttamente perché si trova in una sottoscrizione diversa.</span><span class="sxs-lookup"><span data-stu-id="72128-294">hello difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="72128-295">È necessario toocreate un nuovo oggetto di PowerShell con i valori hello comunicati dal 1 sottoscrizione nei passaggi hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="72128-295">You will need toocreate a new PowerShell object with hello values communicated from Subscription 1 in hello steps above.</span></span> <span data-ttu-id="72128-296">Utilizzare l'esempio hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="72128-296">Use hello example below.</span></span> <span data-ttu-id="72128-297">Sostituire i valori hello Name, Id e chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="72128-297">Replace hello Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="72128-298">cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="72128-298">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="72128-299">Creazione di una connessione può richiedere poco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="72128-299">Creating a connection can take a short while toocomplete.</span></span>

  <span data-ttu-id="72128-300">Connettersi tooSubscription 1 prima di eseguire l'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="72128-300">Connect tooSubscription 1 before running hello following example:</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="72128-301">**[Sottoscrizione 5]**  Creare hello TestVNet5 tooTestVNet1 connessione.</span><span class="sxs-lookup"><span data-stu-id="72128-301">**[Subscription 5]** Create hello TestVNet5 tooTestVNet1 connection.</span></span> <span data-ttu-id="72128-302">Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="72128-302">This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="72128-303">Hello stesso processo di creazione di un oggetto di PowerShell in base ai valori hello ottenuti da 1 a sottoscrizione applicabile in questo caso anche.</span><span class="sxs-lookup"><span data-stu-id="72128-303">hello same process of creating a PowerShell object based on hello values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="72128-304">In questo passaggio, assicurarsi che le chiavi condivise hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="72128-304">In this step, be sure that hello shared keys match.</span></span>

  <span data-ttu-id="72128-305">Connettersi tooSubscription 5 prima di eseguire l'esempio seguente hello:</span><span class="sxs-lookup"><span data-stu-id="72128-305">Connect tooSubscription 5 before running hello following example:</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <span data-ttu-id="72128-306"><a name="verify"></a>Come tooverify una connessione</span><span class="sxs-lookup"><span data-stu-id="72128-306"><a name="verify"></a>How tooverify a connection</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="72128-307"><a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="72128-307"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="72128-308">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="72128-308">Next steps</span></span>

* <span data-ttu-id="72128-309">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="72128-309">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="72128-310">Vedere hello [macchine virtuali-documentazione](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="72128-310">See hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="72128-311">Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="72128-311">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
