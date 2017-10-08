---
title: 'La connessione di rete virtuale tooanother rete virtuale: CLI di Azure | Documenti Microsoft'
description: Questo articolo illustra la connessione tra reti virtuali tramite Azure Resource Manager e l'interfaccia della riga di comando di Azure.
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="151b8-103">Configurare una connessione gateway VPN tra reti virtuali usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="151b8-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="151b8-104">In questo articolo illustra come toocreate una connessione gateway VPN tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="151b8-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="151b8-105">Hello reti virtuali possono essere hello stesso o in aree diverse in e da hello uguali o diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="151b8-106">Quando le reti virtuali connessione da sottoscrizioni diverse, le sottoscrizioni di hello non necessaria toobe associato hello stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="151b8-106">When connecting VNets from different subscriptions, hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> 

<span data-ttu-id="151b8-107">passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello e utilizzano CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="151b8-107">hello steps in this article apply toohello Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="151b8-108">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="151b8-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="151b8-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="151b8-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="151b8-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="151b8-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="151b8-111">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="151b8-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="151b8-112">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="151b8-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="151b8-113">Connettersi tra modelli di distribuzione diversi - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="151b8-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="151b8-114">Connettersi tra modelli di distribuzione diversi - PowerShell</span><span class="sxs-lookup"><span data-stu-id="151b8-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="151b8-115">La connessione di una rete virtuale (VNet a VNet) tooanother di rete virtuale è simile tooconnecting un percorso di rete virtuale tooan locale del sito.</span><span class="sxs-lookup"><span data-stu-id="151b8-115">Connecting a virtual network tooanother virtual network (VNet-to-VNet) is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="151b8-116">Entrambi i tipi di connettività di utilizzare un tooprovide gateway VPN un tunnel sicuro tramite IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="151b8-116">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="151b8-117">Se le reti virtuali si trovano in hello stessa area, è opportuno tooconsider collegarli tramite Peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="151b8-117">If your VNets are in hello same region, you may want tooconsider connecting them using VNet Peering.</span></span> <span data-ttu-id="151b8-118">Peering reti virtuali non usa un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="151b8-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="151b8-119">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="151b8-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="151b8-120">La comunicazione tra reti virtuali può essere associata a configurazioni multisito.</span><span class="sxs-lookup"><span data-stu-id="151b8-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="151b8-121">Consente di stabilire le topologie di rete che combinano connettività cross-premise con connettività di rete virtuale tra, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="151b8-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in hello following diagram:</span></span>

![Informazioni sulle connessioni](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="151b8-123"><a name="why"></a>Perché connettere reti virtuali?</span><span class="sxs-lookup"><span data-stu-id="151b8-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="151b8-124">Si consiglia le reti virtuali tooconnect per hello seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="151b8-124">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="151b8-125">**Presenza e ridondanza in più aree geografiche**</span><span class="sxs-lookup"><span data-stu-id="151b8-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="151b8-126">È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="151b8-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="151b8-127">Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="151b8-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="151b8-128">Un esempio importante è tooset SQL Always on con gruppi di disponibilità, la distribuzione tra più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="151b8-128">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="151b8-129">**Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**</span><span class="sxs-lookup"><span data-stu-id="151b8-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="151b8-130">Hello nella stessa area, è possibile configurare applicazioni multilivello con più reti virtuali connesse a causa di tooisolation o i requisiti amministrativi.</span><span class="sxs-lookup"><span data-stu-id="151b8-130">Within hello same region, you can set up multi-tier applications with multiple virtual networks connected together due tooisolation or administrative requirements.</span></span>

<span data-ttu-id="151b8-131">Per ulteriori informazioni sulle connessioni di rete virtuale a, vedere hello [domande frequenti per rete virtuale a](#faq) alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="151b8-131">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="151b8-132">Quale procedura è consigliabile seguire?</span><span class="sxs-lookup"><span data-stu-id="151b8-132">Which set of steps should I use?</span></span>

<span data-ttu-id="151b8-133">Questo articolo riporta due diverse procedure.</span><span class="sxs-lookup"><span data-stu-id="151b8-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="151b8-134">Un set di passaggi per [hello di reti virtuali che si trovano nella stessa sottoscrizione](#samesub)e un altro per [reti virtuali che risiedono in diverse sottoscrizioni](#difsub).</span><span class="sxs-lookup"><span data-stu-id="151b8-134">One set of steps for [VNets that reside in hello same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="151b8-135"><a name="samesub"></a>Connettere reti virtuali presenti hello stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="151b8-135"><a name="samesub"></a>Connect VNets that are in hello same subscription</span></span>

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="151b8-137">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="151b8-137">Before you begin</span></span>

<span data-ttu-id="151b8-138">Prima di iniziare, installare hello versione i comandi CLI hello (2.0 o versione successivo).</span><span class="sxs-lookup"><span data-stu-id="151b8-138">Before beginning, install hello latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="151b8-139">Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="151b8-139">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="151b8-140"><a name="Plan"></a>Pianificare gli intervalli di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="151b8-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="151b8-141">In hello alla procedura seguente, vengono create due reti virtuali insieme le subnet gateway rispettivi e configurazioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-141">In hello following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="151b8-142">È quindi creare una connessione VPN tra hello due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="151b8-142">We then create a VPN connection between hello two VNets.</span></span> <span data-ttu-id="151b8-143">È importante tooplan hello indirizzi IP per la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="151b8-143">It’s important tooplan hello IP address ranges for your network configuration.</span></span> <span data-ttu-id="151b8-144">Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="151b8-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="151b8-145">In questi esempi non viene incluso un server DNS.</span><span class="sxs-lookup"><span data-stu-id="151b8-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="151b8-146">Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="151b8-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="151b8-147">Utilizziamo hello seguente i valori negli esempi di hello:</span><span class="sxs-lookup"><span data-stu-id="151b8-147">We use hello following values in hello examples:</span></span>

<span data-ttu-id="151b8-148">**Valori per TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="151b8-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="151b8-149">Nome della rete virtuale: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="151b8-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="151b8-150">Gruppo di risorse: TestRG1</span><span class="sxs-lookup"><span data-stu-id="151b8-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="151b8-151">Location: Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="151b8-151">Location: East US</span></span>
* <span data-ttu-id="151b8-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="151b8-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="151b8-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="151b8-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="151b8-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="151b8-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="151b8-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="151b8-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="151b8-157">IP pubblico: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="151b8-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="151b8-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="151b8-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="151b8-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="151b8-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="151b8-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="151b8-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="151b8-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="151b8-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="151b8-162">**Valori per TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="151b8-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="151b8-163">Nome della rete virtuale: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="151b8-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="151b8-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="151b8-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="151b8-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="151b8-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="151b8-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="151b8-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="151b8-168">Gruppo di risorse: TestRG4</span><span class="sxs-lookup"><span data-stu-id="151b8-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="151b8-169">Località: Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="151b8-169">Location: West US</span></span>
* <span data-ttu-id="151b8-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="151b8-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="151b8-171">IP pubblico: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="151b8-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="151b8-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="151b8-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="151b8-173">Connessione: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="151b8-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="151b8-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="151b8-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="151b8-175"><a name="Connect"></a>Passaggio 1: connettere tooyour sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="151b8-175"><a name="Connect"></a>Step 1 - Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="151b8-176"><a name="TestVNet1"></a>Passaggio 2: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="151b8-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="151b8-177">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="151b8-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="151b8-178">Creare subnet TestVNet1 e hello per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-178">Create TestVNet1 and hello subnets for TestVNet1.</span></span> <span data-ttu-id="151b8-179">Questo esempio crea una rete virtuale denominata TestVNet1 e una subnet denominata FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="151b8-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="151b8-180">Creare uno spazio di indirizzi aggiuntivi per la subnet di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-180">Create an additional address space for hello backend subnet.</span></span> <span data-ttu-id="151b8-181">Si noti che in questo passaggio è specificare sia lo spazio degli indirizzi di hello creato in precedenza e hello ulteriore spazio degli indirizzi che si desidera tooadd.</span><span class="sxs-lookup"><span data-stu-id="151b8-181">Notice that in this step, we specify both hello address space that we created earlier, and hello additional address space that we want tooadd.</span></span> <span data-ttu-id="151b8-182">Infatti, hello [aggiornamento rete virtuale di rete az](https://docs.microsoft.com/cli/azure/network/vnet#update) comando sovrascrive le impostazioni precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-182">This is because hello [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites hello previous settings.</span></span> <span data-ttu-id="151b8-183">Verificare che toospecify tutti i prefissi di indirizzo hello quando si utilizza questo comando.</span><span class="sxs-lookup"><span data-stu-id="151b8-183">Make sure toospecify all of hello address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="151b8-184">Creare subnet back-end hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-184">Create hello backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="151b8-185">Creare subnet del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-185">Create hello gateway subnet.</span></span> <span data-ttu-id="151b8-186">Si noti che la subnet gateway hello è denominata 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="151b8-186">Notice that hello gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="151b8-187">Questo nome è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="151b8-187">This name is required.</span></span> <span data-ttu-id="151b8-188">In questo esempio subnet del gateway hello utilizza un /27.</span><span class="sxs-lookup"><span data-stu-id="151b8-188">In this example, hello gateway subnet is using a /27.</span></span> <span data-ttu-id="151b8-189">Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando almeno /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="151b8-189">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="151b8-190">In questo modo per sufficiente indirizzi tooaccommodate possibili configurazioni aggiuntive che è possibile in hello future.</span><span class="sxs-lookup"><span data-stu-id="151b8-190">This will allow for enough addresses tooaccommodate possible additional configurations that you may want in hello future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="151b8-191">Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta.</span><span class="sxs-lookup"><span data-stu-id="151b8-191">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="151b8-192">Si noti che hello AllocationMethod è dinamico.</span><span class="sxs-lookup"><span data-stu-id="151b8-192">Notice that hello AllocationMethod is Dynamic.</span></span> <span data-ttu-id="151b8-193">È possibile specificare l'indirizzo IP hello che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="151b8-193">You cannot specify hello IP address that you want toouse.</span></span> <span data-ttu-id="151b8-194">È il gateway tooyour allocata in modo dinamico.</span><span class="sxs-lookup"><span data-stu-id="151b8-194">It's dynamically allocated tooyour gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="151b8-195">Creare il gateway di rete virtuale hello per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-195">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="151b8-196">Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="151b8-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="151b8-197">Se si esegue questo comando hello utilizzando il parametro '-- Nessun - wait', non sono visibili eventuali commenti e suggerimenti o output.</span><span class="sxs-lookup"><span data-stu-id="151b8-197">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="151b8-198">Hello '-- Nessun - wait' parametro consente toocreate gateway hello in background hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-198">hello '--no-wait' parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="151b8-199">Questo significa che tale gateway VPN hello termine della creazione immediatamente.</span><span class="sxs-lookup"><span data-stu-id="151b8-199">It does not mean that hello VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="151b8-200">Creazione di un gateway può richiedere spesso 45 minuti o più, a seconda di gateway hello SKU in uso.</span><span class="sxs-lookup"><span data-stu-id="151b8-200">Creating a gateway can often take 45 minutes or more, depending on hello gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="151b8-201"><a name="TestVNet4"></a>Passaggio 3: Creare e configurare TestVNet4</span><span class="sxs-lookup"><span data-stu-id="151b8-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="151b8-202">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="151b8-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="151b8-203">Creare TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="151b8-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="151b8-204">Creare altre subnet per TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="151b8-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="151b8-205">Creare subnet del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-205">Create hello gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="151b8-206">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="151b8-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="151b8-207">Creare il gateway di rete virtuale TestVNet4 hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-207">Create hello TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="151b8-208"><a name="createconnect"></a>Passaggio 4: creare connessioni hello</span><span class="sxs-lookup"><span data-stu-id="151b8-208"><a name="createconnect"></a>Step 4 - Create hello connections</span></span>

<span data-ttu-id="151b8-209">Ora sono disponibili due reti virtuali con i gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="151b8-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="151b8-210">passaggio successivo Hello è connessioni gateway VPN di toocreate tra il gateway di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-210">hello next step is toocreate VPN gateway connections between hello virtual network gateways.</span></span> <span data-ttu-id="151b8-211">Se è stata utilizzata negli esempi di hello sopra riportati, i gateway si trovano in gruppi di risorse diverso.</span><span class="sxs-lookup"><span data-stu-id="151b8-211">If you used hello examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="151b8-212">Quando il gateway si trovano in gruppi di risorse diversi, è necessario tooidentify e specificare l'ID di risorsa hello per ogni gateway per stabilire una connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-212">When gateways are in different resource groups, you need tooidentify and specify hello resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="151b8-213">Se le reti virtuali si trovano in hello stesso gruppo di risorse, è possibile utilizzare hello [secondo set di istruzioni](#samerg) perché non è necessario l'ID di risorsa toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-213">If your VNets are in hello same resource group, you can use hello [second set of instructions](#samerg) because you don't need toospecify hello resource IDs.</span></span>

### <span data-ttu-id="151b8-214"><a name="diffrg"></a>tooconnect reti virtuali che si trovano in diversi gruppi di risorse</span><span class="sxs-lookup"><span data-stu-id="151b8-214"><a name="diffrg"></a>tooconnect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="151b8-215">Ottenere ID risorsa di VNet1GW hello dall'output di hello di hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="151b8-215">Get hello Resource ID of VNet1GW from hello output of hello following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="151b8-216">Nell'output di hello, trovare hello "id:" riga.</span><span class="sxs-lookup"><span data-stu-id="151b8-216">In hello output, find hello "id:" line.</span></span> <span data-ttu-id="151b8-217">i valori di Hello virgolette hello sono necessari toocreate hello connessione nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-217">hello values within hello quotes are needed toocreate hello connection in hello next section.</span></span> <span data-ttu-id="151b8-218">Copiare questi editor di testo tooa valori, ad esempio Blocco note, in modo che sia possibile incollarli facilmente quando si crea la connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-218">Copy these values tooa text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="151b8-219">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="151b8-219">Example output:</span></span>

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  <span data-ttu-id="151b8-220">Copiare i valori hello dopo **"id":** virgolette hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-220">Copy hello values after **"id":** within hello quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="151b8-221">Ottenere hello ID risorsa di VNet4GW e copia hello valori tooa editor di testo.</span><span class="sxs-lookup"><span data-stu-id="151b8-221">Get hello Resource ID of VNet4GW and copy hello values tooa text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="151b8-222">Creare hello TestVNet1 tooTestVNet4 connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-222">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="151b8-223">In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="151b8-223">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="151b8-224">È una chiave condivisa a cui fa riferimento negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-224">There is a shared key referenced in hello examples.</span></span> <span data-ttu-id="151b8-225">È possibile utilizzare i valori per la chiave condivisa hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-225">You can use your own values for hello shared key.</span></span> <span data-ttu-id="151b8-226">cosa è la chiave condivisa hello importante Hello deve corrispondere per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-226">hello important thing is that hello shared key must match for both connections.</span></span> <span data-ttu-id="151b8-227">Creazione di una connessione richiede poco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="151b8-227">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="151b8-228">Creare hello TestVNet4 tooTestVNet1 connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-228">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="151b8-229">Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-229">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="151b8-230">Assicurarsi che le chiavi condivise hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="151b8-230">Make sure hello shared keys match.</span></span> <span data-ttu-id="151b8-231">Richiede pochi minuti connessione hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="151b8-231">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="151b8-232">Verificare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-232">Verify your connections.</span></span> <span data-ttu-id="151b8-233">Vedere [Verificare la connessione](#verify).</span><span class="sxs-lookup"><span data-stu-id="151b8-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="151b8-234"><a name="samerg"></a>tooconnect reti virtuali che risiedono in hello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="151b8-234"><a name="samerg"></a>tooconnect VNets that reside in hello same resource group</span></span>

1. <span data-ttu-id="151b8-235">Creare hello TestVNet1 tooTestVNet4 connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-235">Create hello TestVNet1 tooTestVNet4 connection.</span></span> <span data-ttu-id="151b8-236">In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet4.</span><span class="sxs-lookup"><span data-stu-id="151b8-236">In this step, you create hello connection from TestVNet1 tooTestVNet4.</span></span> <span data-ttu-id="151b8-237">Gruppi di risorse di notifica hello sono hello stesso negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-237">Notice hello resource groups are hello same in hello examples.</span></span> <span data-ttu-id="151b8-238">È inoltre possibile visualizzare una chiave condivisa a cui fa riferimento negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-238">You also see a shared key referenced in hello examples.</span></span> <span data-ttu-id="151b8-239">È possibile utilizzare i valori per la chiave condivisa hello, tuttavia, la chiave condivisa hello deve corrispondere per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-239">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="151b8-240">Creazione di una connessione richiede poco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="151b8-240">Creating a connection takes a short while toocomplete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="151b8-241">Creare hello TestVNet4 tooTestVNet1 connessione.</span><span class="sxs-lookup"><span data-stu-id="151b8-241">Create hello TestVNet4 tooTestVNet1 connection.</span></span> <span data-ttu-id="151b8-242">Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet4 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-242">This step is similar toohello one above, except you are creating hello connection from TestVNet4 tooTestVNet1.</span></span> <span data-ttu-id="151b8-243">Assicurarsi che le chiavi condivise hello corrispondano.</span><span class="sxs-lookup"><span data-stu-id="151b8-243">Make sure hello shared keys match.</span></span> <span data-ttu-id="151b8-244">Richiede pochi minuti connessione hello tooestablish.</span><span class="sxs-lookup"><span data-stu-id="151b8-244">It takes a few minutes tooestablish hello connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="151b8-245">Verificare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-245">Verify your connections.</span></span> <span data-ttu-id="151b8-246">Vedere [Verificare la connessione](#verify).</span><span class="sxs-lookup"><span data-stu-id="151b8-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="151b8-247"><a name="difsub"></a>Connettere reti virtuali che si trovano in sottoscrizioni diverse</span><span class="sxs-lookup"><span data-stu-id="151b8-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="151b8-249">In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5,</span><span class="sxs-lookup"><span data-stu-id="151b8-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="151b8-250">Hello reti virtuali si trovano diverse sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-250">hello VNets reside different subscriptions.</span></span> <span data-ttu-id="151b8-251">le sottoscrizioni di Hello non è necessario toobe associato hello stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="151b8-251">hello subscriptions do not need toobe associated with hello same Active Directory tenant.</span></span> <span data-ttu-id="151b8-252">nei passaggi Hello per questa configurazione aggiunge una connessione di rete virtuale a aggiuntiva in ordine tooconnect TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="151b8-252">hello steps for this configuration add an additional VNet-to-VNet connection in order tooconnect TestVNet1 tooTestVNet5.</span></span>

### <span data-ttu-id="151b8-253"><a name="TestVNet1diff"></a>Passaggio 5: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="151b8-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="151b8-254">Queste istruzioni continuano da passi hello in hello sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="151b8-254">These instructions continue from hello steps in hello preceding sections.</span></span> <span data-ttu-id="151b8-255">È necessario completare [passaggio 1](#Connect) e [passaggio 2](#TestVNet1) toocreate e configurare TestVNet1 e hello Gateway VPN per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) toocreate and configure TestVNet1 and hello VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="151b8-256">Per questa configurazione, non è necessario toocreate TestVNet4 dalla sezione precedente hello, sebbene se viene creato, non creerà conflitti con questa procedura.</span><span class="sxs-lookup"><span data-stu-id="151b8-256">For this configuration, you are not required toocreate TestVNet4 from hello previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="151b8-257">Al termine, continuare con il passaggio 6 (sotto).</span><span class="sxs-lookup"><span data-stu-id="151b8-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="151b8-258"><a name="verifyranges"></a>Passaggio 6: verificare gli intervalli di indirizzi IP hello</span><span class="sxs-lookup"><span data-stu-id="151b8-258"><a name="verifyranges"></a>Step 6 - Verify hello IP address ranges</span></span>

<span data-ttu-id="151b8-259">Quando si creano connessioni aggiuntive, è importante tooverify che non si sovrapponga a spazio di indirizzi IP hello della nuova rete virtuale hello con uno qualsiasi di altri intervalli di rete virtuale o intervalli di gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="151b8-259">When creating additional connections, it's important tooverify that hello IP address space of hello new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="151b8-260">Per questo esercizio, è possibile utilizzare i seguenti valori per hello TestVNet5 hello:</span><span class="sxs-lookup"><span data-stu-id="151b8-260">For this exercise, you can use hello following values for hello TestVNet5:</span></span>

<span data-ttu-id="151b8-261">**Valori per TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="151b8-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="151b8-262">Nome della rete virtuale: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="151b8-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="151b8-263">Gruppo di risorse: TestRG5</span><span class="sxs-lookup"><span data-stu-id="151b8-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="151b8-264">Ubicazione: Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="151b8-264">Location: Japan East</span></span>
* <span data-ttu-id="151b8-265">TestVNet5: 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="151b8-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="151b8-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="151b8-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="151b8-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="151b8-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="151b8-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="151b8-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="151b8-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="151b8-270">IP pubblico: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="151b8-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="151b8-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="151b8-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="151b8-272">Connessione: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="151b8-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="151b8-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="151b8-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="151b8-274"><a name="TestVNet5"></a>Passaggio 7: Creare e configurare TestVNet5</span><span class="sxs-lookup"><span data-stu-id="151b8-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="151b8-275">Questo passaggio deve essere eseguito nel contesto di hello di hello nuova sottoscrizione 5 di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="151b8-275">This step must be done in hello context of hello new subscription, Subscription 5.</span></span> <span data-ttu-id="151b8-276">Questa parte può essere eseguita dall'amministratore di hello in un'altra organizzazione che possiede la sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-276">This part may be performed by hello administrator in a different organization that owns hello subscription.</span></span> <span data-ttu-id="151b8-277">tooswitch tra l'utilizzo di sottoscrizioni ' elenco di account az - tutti ' toolist hello account tooyour disponibili sottoscrizioni, quindi utilizzare ' set di account az - sottoscrizione <subscriptionID>' tooswitch toohello sottoscrizione che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="151b8-277">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="151b8-278">Verificare che si sono connessi tooSubscription 5, quindi crea un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="151b8-278">Make sure you are connected tooSubscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="151b8-279">Creare TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="151b8-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="151b8-280">Aggiungere le subnet.</span><span class="sxs-lookup"><span data-stu-id="151b8-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="151b8-281">Aggiungi subnet gateway hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-281">Add hello gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="151b8-282">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="151b8-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="151b8-283">Creare il gateway TestVNet5 hello</span><span class="sxs-lookup"><span data-stu-id="151b8-283">Create hello TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="151b8-284"><a name="connections5"></a>Passaggio 8: creare connessioni hello</span><span class="sxs-lookup"><span data-stu-id="151b8-284"><a name="connections5"></a>Step 8 - Create hello connections</span></span>

<span data-ttu-id="151b8-285">Verranno suddivise in questo passaggio in due sessioni CLI contrassegnato come **[sottoscrizione 1]**, e **[sottoscrizione 5]** perché sono gateway hello in diverse sottoscrizioni hello.</span><span class="sxs-lookup"><span data-stu-id="151b8-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because hello gateways are in hello different subscriptions.</span></span> <span data-ttu-id="151b8-286">tooswitch tra l'utilizzo di sottoscrizioni ' elenco di account az - tutti ' toolist hello account tooyour disponibili sottoscrizioni, quindi utilizzare ' set di account az - sottoscrizione <subscriptionID>' tooswitch toohello sottoscrizione che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="151b8-286">tooswitch between subscriptions use 'az account list --all' toolist hello subscriptions available tooyour account, then use 'az account set --subscription <subscriptionID>' tooswitch toohello subscription that you want toouse.</span></span>

1. <span data-ttu-id="151b8-287">**[Sottoscrizione 1]**  Accedi e connettersi tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="151b8-287">**[Subscription 1]** Log in and connect tooSubscription 1.</span></span> <span data-ttu-id="151b8-288">Comando che segue hello esecuzione tooget hello nome e l'ID di hello Gateway dall'output di hello:</span><span class="sxs-lookup"><span data-stu-id="151b8-288">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="151b8-289">Copia output di hello per "id:".</span><span class="sxs-lookup"><span data-stu-id="151b8-289">Copy hello output for "id:".</span></span> <span data-ttu-id="151b8-290">Inviare hello ID e nome hello di hello rete virtuale (VNet1GW) toohello amministratore del gateway di 5 sottoscrizione tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="151b8-290">Send hello ID and hello name of hello VNet gateway (VNet1GW) toohello administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="151b8-291">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="151b8-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="151b8-292">**[Sottoscrizione 5]**  Accedi e connettersi tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="151b8-292">**[Subscription 5]** Log in and connect tooSubscription 5.</span></span> <span data-ttu-id="151b8-293">Comando che segue hello esecuzione tooget hello nome e l'ID di hello Gateway dall'output di hello:</span><span class="sxs-lookup"><span data-stu-id="151b8-293">Run hello following command tooget hello name and ID of hello Gateway from hello output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="151b8-294">Copia output di hello per "id:".</span><span class="sxs-lookup"><span data-stu-id="151b8-294">Copy hello output for "id:".</span></span> <span data-ttu-id="151b8-295">Inviare hello ID e nome hello di hello rete virtuale (VNet5GW) toohello amministratore del gateway 1 sottoscrizione tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="151b8-295">Send hello ID and hello name of hello VNet gateway (VNet5GW) toohello administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="151b8-296">**[Sottoscrizione 1]**  In questo passaggio si crea connessione di hello da TestVNet1 tooTestVNet5.</span><span class="sxs-lookup"><span data-stu-id="151b8-296">**[Subscription 1]** In this step, you create hello connection from TestVNet1 tooTestVNet5.</span></span> <span data-ttu-id="151b8-297">È possibile utilizzare i valori per la chiave condivisa hello, tuttavia, la chiave condivisa hello deve corrispondere per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="151b8-297">You can use your own values for hello shared key, however, hello shared key must match for both connections.</span></span> <span data-ttu-id="151b8-298">Creazione di una connessione può richiedere poco toocomplete.</span><span class="sxs-lookup"><span data-stu-id="151b8-298">Creating a connection can take a short while toocomplete.</span></span> <span data-ttu-id="151b8-299">Assicurarsi che ci si connette tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="151b8-299">Make sure you connect tooSubscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="151b8-300">**[Sottoscrizione 5]**  Questo passaggio è simile toohello uno precedente, ma si sta creando la connessione hello da TestVNet5 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="151b8-300">**[Subscription 5]** This step is similar toohello one above, except you are creating hello connection from TestVNet5 tooTestVNet1.</span></span> <span data-ttu-id="151b8-301">Verificare che tale hello condiviso in corrispondenza delle chiavi e che ci si connette tooSubscription 5.</span><span class="sxs-lookup"><span data-stu-id="151b8-301">Make sure that hello shared keys match and that you connect tooSubscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="151b8-302"><a name="verify"></a>Verificare le connessioni hello</span><span class="sxs-lookup"><span data-stu-id="151b8-302"><a name="verify"></a>Verify hello connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="151b8-303"><a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="151b8-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="151b8-304">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="151b8-304">Next steps</span></span>

* <span data-ttu-id="151b8-305">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="151b8-305">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="151b8-306">Per ulteriori informazioni, vedere hello [macchine virtuali-documentazione](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="151b8-306">For more information, see hello [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="151b8-307">Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="151b8-307">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
