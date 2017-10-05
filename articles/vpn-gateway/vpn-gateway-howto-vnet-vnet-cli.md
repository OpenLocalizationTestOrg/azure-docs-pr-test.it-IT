---
title: 'Connettere una rete virtuale a un''altra rete virtuale: interfaccia della riga di comando di Azure | Microsoft Docs'
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
ms.openlocfilehash: ae42f661b39e8b6170fd415d758404fb33009ccc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a><span data-ttu-id="5689f-103">Configurare una connessione gateway VPN tra reti virtuali usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5689f-103">Configure a VNet-to-VNet VPN gateway connection using Azure CLI</span></span>

<span data-ttu-id="5689f-104">Questo articolo descrive come creare una connessione gateway VPN tra reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="5689f-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="5689f-105">Le reti virtuali possono trovarsi in aree geografiche uguali o diverse e in sottoscrizioni uguali o diverse.</span><span class="sxs-lookup"><span data-stu-id="5689f-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="5689f-106">Quando si connettono reti virtuali da sottoscrizioni diverse, non è necessario che le sottoscrizioni siano associate allo stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5689f-106">When connecting VNets from different subscriptions, the subscriptions do not need to be associated with the same Active Directory tenant.</span></span> 

<span data-ttu-id="5689f-107">La procedura illustrata in questo articolo si applica al modello di distribuzione Resource Manager e usano l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="5689f-107">The steps in this article apply to the Resource Manager deployment model and use Azure CLI.</span></span> <span data-ttu-id="5689f-108">È anche possibile creare questa configurazione usando strumenti o modelli di distribuzione diversi selezionando un'opzione differente nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="5689f-108">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5689f-109">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5689f-109">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="5689f-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5689f-110">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="5689f-111">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5689f-111">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="5689f-112">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="5689f-112">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="5689f-113">Connettersi tra modelli di distribuzione diversi - Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5689f-113">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="5689f-114">Connettersi tra modelli di distribuzione diversi - PowerShell</span><span class="sxs-lookup"><span data-stu-id="5689f-114">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

<span data-ttu-id="5689f-115">La connessione di una rete virtuale a un'altra rete virtuale (da rete virtuale a rete virtuale) è simile alla connessione di una rete virtuale a un percorso di sito locale.</span><span class="sxs-lookup"><span data-stu-id="5689f-115">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="5689f-116">Entrambi i tipi di connettività utilizzano un gateway VPN per fornire un tunnel sicuro tramite IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="5689f-116">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="5689f-117">Se le reti virtuali si trovano nella stessa area, è consigliabile considerare la possibilità di connetterle tramite peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="5689f-117">If your VNets are in the same region, you may want to consider connecting them using VNet Peering.</span></span> <span data-ttu-id="5689f-118">Peering reti virtuali non usa un gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="5689f-118">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="5689f-119">Per altre informazioni, vedere [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5689f-119">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span>

<span data-ttu-id="5689f-120">La comunicazione tra reti virtuali può essere associata a configurazioni multisito.</span><span class="sxs-lookup"><span data-stu-id="5689f-120">VNet-to-VNet communication can be combined with multi-site configurations.</span></span> <span data-ttu-id="5689f-121">In questo modo è possibile definire topologie di rete che consentono di combinare la connettività cross-premise con la connettività tra reti virtuali, come illustrato nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="5689f-121">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![Informazioni sulle connessioni](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <span data-ttu-id="5689f-123"><a name="why"></a>Perché connettere reti virtuali?</span><span class="sxs-lookup"><span data-stu-id="5689f-123"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="5689f-124">È possibile connettere reti virtuali per i seguenti motivi:</span><span class="sxs-lookup"><span data-stu-id="5689f-124">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="5689f-125">**Presenza e ridondanza in più aree geografiche**</span><span class="sxs-lookup"><span data-stu-id="5689f-125">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="5689f-126">È possibile configurare la sincronizzazione o la replica geografica con connettività sicura senza passare da endpoint con connessione Internet.</span><span class="sxs-lookup"><span data-stu-id="5689f-126">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="5689f-127">Con Gestione traffico e il servizio di bilanciamento del carico di Azure è possibile configurare il carico di lavoro a disponibilità elevata con ridondanza geografica in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="5689f-127">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="5689f-128">Un esempio importante è rappresentato dalla configurazione SQL AlwaysOn con gruppi di disponibilità distribuiti in più aree di Azure.</span><span class="sxs-lookup"><span data-stu-id="5689f-128">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="5689f-129">**Applicazioni multilivello in singole aree geografiche con isolamento o limite amministrativo**</span><span class="sxs-lookup"><span data-stu-id="5689f-129">**Regional multi-tier applications with isolation or administrative boundary**</span></span>

  * <span data-ttu-id="5689f-130">All'interno di una stessa area è possibile configurare applicazioni multilivello con più reti virtuali connesse tra loro a causa dell'isolamento o di requisiti amministrativi.</span><span class="sxs-lookup"><span data-stu-id="5689f-130">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="5689f-131">Per altre informazioni sulle connessioni da rete virtuale a rete virtuale, vedere la sezione [Domande frequenti relative alla connessione da rete virtuale a rete virtuale](#faq) alla fine di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="5689f-131">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span>

### <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="5689f-132">Quale procedura è consigliabile seguire?</span><span class="sxs-lookup"><span data-stu-id="5689f-132">Which set of steps should I use?</span></span>

<span data-ttu-id="5689f-133">Questo articolo riporta due diverse procedure.</span><span class="sxs-lookup"><span data-stu-id="5689f-133">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="5689f-134">Una per le [reti virtuali che si trovano nella stessa sottoscrizione](#samesub) e un'altra per le [reti virtuali che si trovano in sottoscrizioni diverse](#difsub).</span><span class="sxs-lookup"><span data-stu-id="5689f-134">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span>

## <span data-ttu-id="5689f-135"><a name="samesub"></a>Connettere reti virtuali che si trovano nella stessa sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5689f-135"><a name="samesub"></a>Connect VNets that are in the same subscription</span></span>

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="5689f-137">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="5689f-137">Before you begin</span></span>

<span data-ttu-id="5689f-138">Prima di iniziare, installare la versione più recente dei comandi dell'interfaccia della riga di comando (2.0 o successiva).</span><span class="sxs-lookup"><span data-stu-id="5689f-138">Before beginning, install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="5689f-139">Per informazioni sull'installazione dei comandi dell'interfaccia della riga di comando, vedere [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="5689f-139">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

### <span data-ttu-id="5689f-140"><a name="Plan"></a>Pianificare gli intervalli di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="5689f-140"><a name="Plan"></a>Plan your IP address ranges</span></span>

<span data-ttu-id="5689f-141">Nei passaggi seguenti vengono create due reti virtuali con le rispettive subnet del gateway e le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-141">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="5689f-142">Viene quindi configurata una connessione VPN tra le due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="5689f-142">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="5689f-143">È importante pianificare gli intervalli di indirizzi IP per la configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="5689f-143">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="5689f-144">Tenere presente che è necessario assicurarsi che nessuno di intervalli di rete virtuale o intervalli di rete locale si sovrappongano in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="5689f-144">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span> <span data-ttu-id="5689f-145">In questi esempi non viene incluso un server DNS.</span><span class="sxs-lookup"><span data-stu-id="5689f-145">In these examples, we do not include a DNS server.</span></span> <span data-ttu-id="5689f-146">Per usare la risoluzione dei nomi per le reti virtuali, vedere [Risoluzione dei nomi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="5689f-146">If you want name resolution for your virtual networks, see [Name resolution](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>

<span data-ttu-id="5689f-147">Negli esempi vengono usati i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="5689f-147">We use the following values in the examples:</span></span>

<span data-ttu-id="5689f-148">**Valori per TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="5689f-148">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="5689f-149">Nome della rete virtuale: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5689f-149">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="5689f-150">Gruppo di risorse: TestRG1</span><span class="sxs-lookup"><span data-stu-id="5689f-150">Resource Group: TestRG1</span></span>
* <span data-ttu-id="5689f-151">Location: Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="5689f-151">Location: East US</span></span>
* <span data-ttu-id="5689f-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5689f-152">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="5689f-153">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-153">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="5689f-154">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-154">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="5689f-155">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5689f-155">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="5689f-156">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="5689f-156">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="5689f-157">IP pubblico: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="5689f-157">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="5689f-158">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5689f-158">VPNType: RouteBased</span></span>
* <span data-ttu-id="5689f-159">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="5689f-159">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="5689f-160">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="5689f-160">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="5689f-161">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5689f-161">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="5689f-162">**Valori per TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="5689f-162">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="5689f-163">Nome della rete virtuale: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5689f-163">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="5689f-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5689f-164">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="5689f-165">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-165">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="5689f-166">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-166">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="5689f-167">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="5689f-167">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="5689f-168">Gruppo di risorse: TestRG4</span><span class="sxs-lookup"><span data-stu-id="5689f-168">Resource Group: TestRG4</span></span>
* <span data-ttu-id="5689f-169">Località: Stati Uniti occidentali</span><span class="sxs-lookup"><span data-stu-id="5689f-169">Location: West US</span></span>
* <span data-ttu-id="5689f-170">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="5689f-170">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="5689f-171">IP pubblico: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="5689f-171">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="5689f-172">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5689f-172">VPNType: RouteBased</span></span>
* <span data-ttu-id="5689f-173">Connessione: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="5689f-173">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="5689f-174">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5689f-174">ConnectionType: VNet2VNet</span></span>


### <span data-ttu-id="5689f-175"><a name="Connect"></a>Passaggio 1: Connettersi alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="5689f-175"><a name="Connect"></a>Step 1 - Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <span data-ttu-id="5689f-176"><a name="TestVNet1"></a>Passaggio 2: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5689f-176"><a name="TestVNet1"></a>Step 2 - Create and configure TestVNet1</span></span>

1. <span data-ttu-id="5689f-177">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5689f-177">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. <span data-ttu-id="5689f-178">Creare TestVNet1 e le subnet per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-178">Create TestVNet1 and the subnets for TestVNet1.</span></span> <span data-ttu-id="5689f-179">Questo esempio crea una rete virtuale denominata TestVNet1 e una subnet denominata FrontEnd.</span><span class="sxs-lookup"><span data-stu-id="5689f-179">This example creates a virtual network named TestVNet1 and a subnet named FrontEnd.</span></span>

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. <span data-ttu-id="5689f-180">Creare uno spazio indirizzi aggiuntivo per la subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="5689f-180">Create an additional address space for the backend subnet.</span></span> <span data-ttu-id="5689f-181">Si noti che in questo passaggio vengono specificati sia lo spazio indirizzi creato prima che lo spazio indirizzi aggiuntivo che si vuole aggiungere.</span><span class="sxs-lookup"><span data-stu-id="5689f-181">Notice that in this step, we specify both the address space that we created earlier, and the additional address space that we want to add.</span></span> <span data-ttu-id="5689f-182">Infatti il comando [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) sovrascrive le impostazioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="5689f-182">This is because the [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) command overwrites the previous settings.</span></span> <span data-ttu-id="5689f-183">Quando si usa questo comando, assicurarsi di specificare tutti i prefissi degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="5689f-183">Make sure to specify all of the address prefixes when using this command.</span></span>

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. <span data-ttu-id="5689f-184">Creare la subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="5689f-184">Create the backend subnet.</span></span>
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. <span data-ttu-id="5689f-185">Creare la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="5689f-185">Create the gateway subnet.</span></span> <span data-ttu-id="5689f-186">Si noti che la subnet del gateway viene denominata "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="5689f-186">Notice that the gateway subnet is named 'GatewaySubnet'.</span></span> <span data-ttu-id="5689f-187">Questo nome è obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="5689f-187">This name is required.</span></span> <span data-ttu-id="5689f-188">In questo esempio, la subnet del gateway usa /27.</span><span class="sxs-lookup"><span data-stu-id="5689f-188">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="5689f-189">Nonostante sia possibile creare una subnet del gateway con dimensioni di /29 soltanto, è consigliabile crearne una più grande che includa più indirizzi selezionando almeno /28 o /27.</span><span class="sxs-lookup"><span data-stu-id="5689f-189">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="5689f-190">In questo modo saranno disponibili indirizzi sufficienti per supportare in futuro le possibili configurazioni aggiuntive desiderate.</span><span class="sxs-lookup"><span data-stu-id="5689f-190">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. <span data-ttu-id="5689f-191">Richiedere un indirizzo IP pubblico da allocare per il gateway che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5689f-191">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="5689f-192">Si noti che AllocationMethod è dinamico.</span><span class="sxs-lookup"><span data-stu-id="5689f-192">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="5689f-193">Non è possibile specificare l'indirizzo IP che si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="5689f-193">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="5689f-194">Viene allocato in modo dinamico per il gateway.</span><span class="sxs-lookup"><span data-stu-id="5689f-194">It's dynamically allocated to your gateway.</span></span>

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. <span data-ttu-id="5689f-195">Creare il gateway di rete virtuale per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-195">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="5689f-196">Le configurazioni da rete virtuale a rete virtuale richiedono un tipo di VpnType RouteBased.</span><span class="sxs-lookup"><span data-stu-id="5689f-196">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="5689f-197">Se si esegue questo comando usando il parametro '--no-wait', non viene visualizzato alcun output o commento.</span><span class="sxs-lookup"><span data-stu-id="5689f-197">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="5689f-198">Il parametro "--no-wait" consente la creazione in background del gateway.</span><span class="sxs-lookup"><span data-stu-id="5689f-198">The '--no-wait' parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="5689f-199">Questo non significa che la creazione del gateway VPN termina immediatamente.</span><span class="sxs-lookup"><span data-stu-id="5689f-199">It does not mean that the VPN gateway finishes creating immediately.</span></span> <span data-ttu-id="5689f-200">La creazione di un gateway spesso richiede anche più di 45 minuti di tempo a seconda dell'SKU gateway usato.</span><span class="sxs-lookup"><span data-stu-id="5689f-200">Creating a gateway can often take 45 minutes or more, depending on the gateway SKU that you use.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5689f-201"><a name="TestVNet4"></a>Passaggio 3: Creare e configurare TestVNet4</span><span class="sxs-lookup"><span data-stu-id="5689f-201"><a name="TestVNet4"></a>Step 3 - Create and configure TestVNet4</span></span>

1. <span data-ttu-id="5689f-202">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5689f-202">Create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. <span data-ttu-id="5689f-203">Creare TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-203">Create TestVNet4.</span></span>

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. <span data-ttu-id="5689f-204">Creare altre subnet per TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-204">Create additional subnets for TestVNet4.</span></span>

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. <span data-ttu-id="5689f-205">Creare la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="5689f-205">Create the gateway subnet.</span></span>

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. <span data-ttu-id="5689f-206">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="5689f-206">Request a Public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. <span data-ttu-id="5689f-207">Creare il gateway di rete virtuale TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-207">Create the TestVNet4 virtual network gateway.</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5689f-208"><a name="createconnect"></a>Passaggio 4: Creare le connessioni</span><span class="sxs-lookup"><span data-stu-id="5689f-208"><a name="createconnect"></a>Step 4 - Create the connections</span></span>

<span data-ttu-id="5689f-209">Ora sono disponibili due reti virtuali con i gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="5689f-209">You now have two VNets with VPN gateways.</span></span> <span data-ttu-id="5689f-210">Il passaggio successivo prevede la creazione di connessioni gateway VPN tra i gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5689f-210">The next step is to create VPN gateway connections between the virtual network gateways.</span></span> <span data-ttu-id="5689f-211">Se sono stati usati gli esempi precedenti, i gateway di rete virtuale sono in gruppi di risorse diversi.</span><span class="sxs-lookup"><span data-stu-id="5689f-211">If you used the examples above, your VNet gateways are in different resource groups.</span></span> <span data-ttu-id="5689f-212">Quando i gateway sono in gruppi di risorse diversi, è necessario identificare e specificare gli ID risorsa per ogni gateway quando si stabilisce una connessione.</span><span class="sxs-lookup"><span data-stu-id="5689f-212">When gateways are in different resource groups, you need to identify and specify the resource IDs for each gateway when making a connection.</span></span> <span data-ttu-id="5689f-213">Se le reti virtuali sono nello stesso gruppo di risorse, è possibile usare il [secondo set di istruzioni](#samerg) perché non è necessario specificare gli ID risorsa.</span><span class="sxs-lookup"><span data-stu-id="5689f-213">If your VNets are in the same resource group, you can use the [second set of instructions](#samerg) because you don't need to specify the resource IDs.</span></span>

### <span data-ttu-id="5689f-214"><a name="diffrg"></a>Per connettere reti virtuali che si trovano in gruppi di risorse diversi</span><span class="sxs-lookup"><span data-stu-id="5689f-214"><a name="diffrg"></a>To connect VNets that reside in different resource groups</span></span>

1. <span data-ttu-id="5689f-215">Ottenere l'ID di risorsa di VNet1GW dall'output del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5689f-215">Get the Resource ID of VNet1GW from the output of the following command:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="5689f-216">Nell'output trovare la riga "id:".</span><span class="sxs-lookup"><span data-stu-id="5689f-216">In the output, find the "id:" line.</span></span> <span data-ttu-id="5689f-217">I valori tra virgolette sono necessari per creare la connessione nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="5689f-217">The values within the quotes are needed to create the connection in the next section.</span></span> <span data-ttu-id="5689f-218">Copiare questi valori in un editor di testo, ad esempio il Blocco note, per poterli incollare facilmente quando si crea la connessione.</span><span class="sxs-lookup"><span data-stu-id="5689f-218">Copy these values to a text editor, such as Notepad, so that you can easily paste them when creating your connection.</span></span>

  <span data-ttu-id="5689f-219">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="5689f-219">Example output:</span></span>

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

  <span data-ttu-id="5689f-220">Copiare i valori dopo **"id":** tra virgolette.</span><span class="sxs-lookup"><span data-stu-id="5689f-220">Copy the values after **"id":** within the quotes.</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. <span data-ttu-id="5689f-221">Ottenere l'ID risorsa di VNet4GW e copiare i valori in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="5689f-221">Get the Resource ID of VNet4GW and copy the values to a text editor.</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. <span data-ttu-id="5689f-222">Creare la connessione da TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-222">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="5689f-223">In questo passaggio viene creata la connessione da TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-223">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="5689f-224">È presente una chiave condivisa a cui si fa riferimento negli esempi.</span><span class="sxs-lookup"><span data-stu-id="5689f-224">There is a shared key referenced in the examples.</span></span> <span data-ttu-id="5689f-225">È possibile utilizzare i propri valori specifici per la chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="5689f-225">You can use your own values for the shared key.</span></span> <span data-ttu-id="5689f-226">L'importante è che la chiave condivisa corrisponda per entrambe le configurazioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-226">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="5689f-227">Il completamento della creazione di una connessione richiede un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="5689f-227">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. <span data-ttu-id="5689f-228">Creare la connessione da TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-228">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="5689f-229">Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-229">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="5689f-230">Assicurarsi che le chiavi condivise corrispondano.</span><span class="sxs-lookup"><span data-stu-id="5689f-230">Make sure the shared keys match.</span></span> <span data-ttu-id="5689f-231">Per stabilire la connessione, sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5689f-231">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. <span data-ttu-id="5689f-232">Verificare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-232">Verify your connections.</span></span> <span data-ttu-id="5689f-233">Vedere [Verificare la connessione](#verify).</span><span class="sxs-lookup"><span data-stu-id="5689f-233">See [Verify your connection](#verify).</span></span>

### <span data-ttu-id="5689f-234"><a name="samerg"></a>Per connettere reti virtuali che si trovano nello stesso gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5689f-234"><a name="samerg"></a>To connect VNets that reside in the same resource group</span></span>

1. <span data-ttu-id="5689f-235">Creare la connessione da TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-235">Create the TestVNet1 to TestVNet4 connection.</span></span> <span data-ttu-id="5689f-236">In questo passaggio viene creata la connessione da TestVNet1 a TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="5689f-236">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="5689f-237">Si noti che i gruppi di risorse sono uguali negli esempi.</span><span class="sxs-lookup"><span data-stu-id="5689f-237">Notice the resource groups are the same in the examples.</span></span> <span data-ttu-id="5689f-238">Viene anche visualizzata una chiave condivisa a cui si fa riferimento negli esempi.</span><span class="sxs-lookup"><span data-stu-id="5689f-238">You also see a shared key referenced in the examples.</span></span> <span data-ttu-id="5689f-239">È possibile usare i propri valori per la chiave condivisa che però deve essere la stessa per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-239">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="5689f-240">Il completamento della creazione di una connessione richiede un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="5689f-240">Creating a connection takes a short while to complete.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. <span data-ttu-id="5689f-241">Creare la connessione da TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-241">Create the TestVNet4 to TestVNet1 connection.</span></span> <span data-ttu-id="5689f-242">Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet4 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-242">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="5689f-243">Assicurarsi che le chiavi condivise corrispondano.</span><span class="sxs-lookup"><span data-stu-id="5689f-243">Make sure the shared keys match.</span></span> <span data-ttu-id="5689f-244">Per stabilire la connessione, sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="5689f-244">It takes a few minutes to establish the connection.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. <span data-ttu-id="5689f-245">Verificare le connessioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-245">Verify your connections.</span></span> <span data-ttu-id="5689f-246">Vedere [Verificare la connessione](#verify).</span><span class="sxs-lookup"><span data-stu-id="5689f-246">See [Verify your connection](#verify).</span></span>

## <span data-ttu-id="5689f-247"><a name="difsub"></a>Connettere reti virtuali che si trovano in sottoscrizioni diverse</span><span class="sxs-lookup"><span data-stu-id="5689f-247"><a name="difsub"></a>Connect VNets that are in different subscriptions</span></span>

![Diagramma V2V](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

<span data-ttu-id="5689f-249">In questo scenario vengono connesse le reti virtuali TestVNet1 e TestVNet5,</span><span class="sxs-lookup"><span data-stu-id="5689f-249">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="5689f-250">Le reti virtuali si trovano in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="5689f-250">The VNets reside different subscriptions.</span></span> <span data-ttu-id="5689f-251">Non è necessario che le sottoscrizioni siano associate allo stesso tenant di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5689f-251">The subscriptions do not need to be associated with the same Active Directory tenant.</span></span> <span data-ttu-id="5689f-252">I passaggi di questa configurazione permettono di aggiungere un'altra connessione tra reti virtuali per connettere TestVNet1 e TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="5689f-252">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span></span>

### <span data-ttu-id="5689f-253"><a name="TestVNet1diff"></a>Passaggio 5: Creare e configurare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="5689f-253"><a name="TestVNet1diff"></a>Step 5 - Create and configure TestVNet1</span></span>

<span data-ttu-id="5689f-254">Queste istruzioni sono il proseguimento dei passaggi delle sezioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="5689f-254">These instructions continue from the steps in the preceding sections.</span></span> <span data-ttu-id="5689f-255">È necessario completare il [passaggio 1](#Connect) e il [passaggio 2](#TestVNet1) per creare e configurare TestVNet1 e il gateway VPN per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-255">You must complete [Step 1](#Connect) and [Step 2](#TestVNet1) to create and configure TestVNet1 and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="5689f-256">Per questo configurazione, non è necessario creare TestVNet4 dalla sezione precedente, ma, se è già stata creata, non si verificheranno conflitti con questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="5689f-256">For this configuration, you are not required to create TestVNet4 from the previous section, although if you do create it, it will not conflict with these steps.</span></span> <span data-ttu-id="5689f-257">Al termine, continuare con il passaggio 6 (sotto).</span><span class="sxs-lookup"><span data-stu-id="5689f-257">Once you complete Step 1 and Step 2, continue with Step 6 (below).</span></span>

### <span data-ttu-id="5689f-258"><a name="verifyranges"></a>Passaggio 6: Verificare gli intervalli di indirizzi IP</span><span class="sxs-lookup"><span data-stu-id="5689f-258"><a name="verifyranges"></a>Step 6 - Verify the IP address ranges</span></span>

<span data-ttu-id="5689f-259">Quando si creano connessioni aggiuntive, è importante verificare che lo spazio di indirizzi IP della nuova rete virtuale non si sovrapponga a nessuno degli altri intervalli di rete virtuale o intervalli di gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="5689f-259">When creating additional connections, it's important to verify that the IP address space of the new virtual network does not overlap with any of your other VNet ranges or local network gateway ranges.</span></span> <span data-ttu-id="5689f-260">Per questo esercizio è possibile usare i valori seguenti per TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="5689f-260">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="5689f-261">**Valori per TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="5689f-261">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="5689f-262">Nome della rete virtuale: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="5689f-262">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="5689f-263">Gruppo di risorse: TestRG5</span><span class="sxs-lookup"><span data-stu-id="5689f-263">Resource Group: TestRG5</span></span>
* <span data-ttu-id="5689f-264">Ubicazione: Giappone orientale</span><span class="sxs-lookup"><span data-stu-id="5689f-264">Location: Japan East</span></span>
* <span data-ttu-id="5689f-265">TestVNet5: 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5689f-265">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="5689f-266">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-266">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="5689f-267">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="5689f-267">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="5689f-268">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="5689f-268">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="5689f-269">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="5689f-269">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="5689f-270">IP pubblico: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="5689f-270">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="5689f-271">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="5689f-271">VPNType: RouteBased</span></span>
* <span data-ttu-id="5689f-272">Connessione: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="5689f-272">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="5689f-273">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="5689f-273">ConnectionType: VNet2VNet</span></span>

### <span data-ttu-id="5689f-274"><a name="TestVNet5"></a>Passaggio 7: Creare e configurare TestVNet5</span><span class="sxs-lookup"><span data-stu-id="5689f-274"><a name="TestVNet5"></a>Step 7 - Create and configure TestVNet5</span></span>

<span data-ttu-id="5689f-275">Questo passaggio deve essere eseguito nel contesto della nuova sottoscrizione, la sottoscrizione 5.</span><span class="sxs-lookup"><span data-stu-id="5689f-275">This step must be done in the context of the new subscription, Subscription 5.</span></span> <span data-ttu-id="5689f-276">Questa parte può essere eseguita dall'amministratore in un'altra organizzazione che possiede la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5689f-276">This part may be performed by the administrator in a different organization that owns the subscription.</span></span> <span data-ttu-id="5689f-277">Per passare da una sottoscrizione all'altra, usare "az account list --all" per elencare le sottoscrizioni disponibili per l'account, quindi usare "az account set --subscription <subscriptionID>" per passare alla sottoscrizione che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="5689f-277">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="5689f-278">Verificare di essere connessi alla sottoscrizione 5, quindi creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="5689f-278">Make sure you are connected to Subscription 5, then create a resource group.</span></span>

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. <span data-ttu-id="5689f-279">Creare TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="5689f-279">Create TestVNet5.</span></span>

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. <span data-ttu-id="5689f-280">Aggiungere le subnet.</span><span class="sxs-lookup"><span data-stu-id="5689f-280">Add subnets.</span></span>

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. <span data-ttu-id="5689f-281">Aggiungere la subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="5689f-281">Add the gateway subnet.</span></span>

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. <span data-ttu-id="5689f-282">Richiedere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="5689f-282">Request a public IP address.</span></span>

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. <span data-ttu-id="5689f-283">Creare il gateway di TestVNet5</span><span class="sxs-lookup"><span data-stu-id="5689f-283">Create the TestVNet5 gateway</span></span>

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <span data-ttu-id="5689f-284"><a name="connections5"></a>Passaggio 8: Creare le connessioni</span><span class="sxs-lookup"><span data-stu-id="5689f-284"><a name="connections5"></a>Step 8 - Create the connections</span></span>

<span data-ttu-id="5689f-285">Il passaggio è stato suddiviso in due sessioni dell'interfaccia della riga di comando contrassegnate come **[Sottoscrizione 1]** e **[Sottoscrizione 5]** perché i gateway si trovano in sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="5689f-285">We split this step into two CLI sessions marked as **[Subscription 1]**, and **[Subscription 5]** because the gateways are in the different subscriptions.</span></span> <span data-ttu-id="5689f-286">Per passare da una sottoscrizione all'altra, usare "az account list --all" per elencare le sottoscrizioni disponibili per l'account, quindi usare "az account set --subscription <subscriptionID>" per passare alla sottoscrizione che si vuole usare.</span><span class="sxs-lookup"><span data-stu-id="5689f-286">To switch between subscriptions use 'az account list --all' to list the subscriptions available to your account, then use 'az account set --subscription <subscriptionID>' to switch to the subscription that you want to use.</span></span>

1. <span data-ttu-id="5689f-287">**[Sottoscrizione 1]** Eseguire l'accesso e connettersi alla sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="5689f-287">**[Subscription 1]** Log in and connect to Subscription 1.</span></span> <span data-ttu-id="5689f-288">Usare il comando seguente per ottenere il nome e l'ID del gateway dall'output:</span><span class="sxs-lookup"><span data-stu-id="5689f-288">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  <span data-ttu-id="5689f-289">Copiare l'output per "id:".</span><span class="sxs-lookup"><span data-stu-id="5689f-289">Copy the output for "id:".</span></span> <span data-ttu-id="5689f-290">Inviare l'ID e il nome del gateway della rete virtuale (VNet1GW) all'amministratore della sottoscrizione 5 tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="5689f-290">Send the ID and the name of the VNet gateway (VNet1GW) to the administrator of Subscription 5 via email or another method.</span></span>

  <span data-ttu-id="5689f-291">Output di esempio:</span><span class="sxs-lookup"><span data-stu-id="5689f-291">Example output:</span></span>

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. <span data-ttu-id="5689f-292">**[Sottoscrizione 5]** Eseguire l'accesso e connettersi alla sottoscrizione 5.</span><span class="sxs-lookup"><span data-stu-id="5689f-292">**[Subscription 5]** Log in and connect to Subscription 5.</span></span> <span data-ttu-id="5689f-293">Usare il comando seguente per ottenere il nome e l'ID del gateway dall'output:</span><span class="sxs-lookup"><span data-stu-id="5689f-293">Run the following command to get the name and ID of the Gateway from the output:</span></span>

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  <span data-ttu-id="5689f-294">Copiare l'output per "id:".</span><span class="sxs-lookup"><span data-stu-id="5689f-294">Copy the output for "id:".</span></span> <span data-ttu-id="5689f-295">Inviare l'ID e il nome del gateway della rete virtuale (VNet5GW) all'amministratore della sottoscrizione 1 tramite posta elettronica o un altro metodo.</span><span class="sxs-lookup"><span data-stu-id="5689f-295">Send the ID and the name of the VNet gateway (VNet5GW) to the administrator of Subscription 1 via email or another method.</span></span>

3. <span data-ttu-id="5689f-296">**[Sottoscrizione 1]** In questo passaggio viene creata la connessione da TestVNet1 a TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="5689f-296">**[Subscription 1]** In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="5689f-297">È possibile usare i propri valori per la chiave condivisa che però deve essere la stessa per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="5689f-297">You can use your own values for the shared key, however, the shared key must match for both connections.</span></span> <span data-ttu-id="5689f-298">Il completamento della creazione di una connessione può richiedere un po' di tempo.</span><span class="sxs-lookup"><span data-stu-id="5689f-298">Creating a connection can take a short while to complete.</span></span> <span data-ttu-id="5689f-299">Connettersi alla Sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="5689f-299">Make sure you connect to Subscription 1.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. <span data-ttu-id="5689f-300">**[Sottoscrizione 5]** Questo passaggio è simile a quello precedente, ma riguarda la creazione della connessione da TestVNet5 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="5689f-300">**[Subscription 5]** This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="5689f-301">Verificare che le chiavi condivise corrispondano e di essere connessi alla sottoscrizione 5.</span><span class="sxs-lookup"><span data-stu-id="5689f-301">Make sure that the shared keys match and that you connect to Subscription 5.</span></span>

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <span data-ttu-id="5689f-302"><a name="verify"></a>Verificare le connessioni</span><span class="sxs-lookup"><span data-stu-id="5689f-302"><a name="verify"></a>Verify the connections</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <span data-ttu-id="5689f-303"><a name="faq"></a>Domande frequenti sulle connessioni da rete virtuale a rete virtuale</span><span class="sxs-lookup"><span data-stu-id="5689f-303"><a name="faq"></a>VNet-to-VNet FAQ</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="5689f-304">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5689f-304">Next steps</span></span>

* <span data-ttu-id="5689f-305">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="5689f-305">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="5689f-306">Per altre informazioni, vedere la [documentazione sulle macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="5689f-306">For more information, see the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="5689f-307">Per informazioni su BGP, vedere [Panoramica di BGP](vpn-gateway-bgp-overview.md) e [Come configurare BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5689f-307">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
