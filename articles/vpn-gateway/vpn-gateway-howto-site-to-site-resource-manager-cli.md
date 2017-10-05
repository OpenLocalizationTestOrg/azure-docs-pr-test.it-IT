---
title: 'Connettere la rete locale a una rete virtuale di Azure: VPN da sito a sito: interfaccia della riga di comando | Microsoft Docs'
description: "Passaggi per creare una connessione IPsec dalla rete locale a una rete virtuale di Azure tramite Internet pubblico. Questa procedura consentirà di creare una connessione gateway VPN da sito a sito cross-premise usando l'interfaccia della riga di comando."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: 019c5421dc470b18c9087417b93c241cc5730f77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="801d1-104">Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="801d1-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="801d1-105">Questo articolo illustra come usare l'interfaccia della riga di comando di Azure per creare una connessione gateway VPN da sito a sito dalla rete locale alla rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="801d1-105">This article shows you how to use the Azure CLI to create a Site-to-Site VPN gateway connection from your on-premises network to the VNet.</span></span> <span data-ttu-id="801d1-106">I passaggi di questo articolo sono applicabili al modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="801d1-106">The steps in this article apply to the Resource Manager deployment model.</span></span> <span data-ttu-id="801d1-107">È anche possibile creare questa configurazione usando strumenti o modelli di distribuzione diversi selezionando un'opzione differente nell'elenco seguente:</span><span class="sxs-lookup"><span data-stu-id="801d1-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="801d1-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="801d1-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="801d1-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="801d1-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="801d1-110">CLI</span><span class="sxs-lookup"><span data-stu-id="801d1-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="801d1-111">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="801d1-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="801d1-113">Una connessione gateway VPN da sito a sito viene usata per connettere la rete locale a una rete virtuale di Azure tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="801d1-113">A Site-to-Site VPN gateway connection is used to connect your on-premises network to an Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="801d1-114">Questo tipo di connessione richiede un dispositivo VPN che si trova in locale con un indirizzo IP pubblico esterno assegnato.</span><span class="sxs-lookup"><span data-stu-id="801d1-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned to it.</span></span> <span data-ttu-id="801d1-115">Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="801d1-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="801d1-116">Before you begin</span></span>

<span data-ttu-id="801d1-117">Prima di iniziare la configurazione, verificare di soddisfare i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="801d1-117">Verify that you have met the following criteria before beginning configuration:</span></span>

* <span data-ttu-id="801d1-118">Verificare di avere un dispositivo VPN compatibile e che sia presente un utente in grado di configurarlo.</span><span class="sxs-lookup"><span data-stu-id="801d1-118">Make sure you have a compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="801d1-119">Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="801d1-120">Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="801d1-121">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="801d1-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="801d1-122">Se non si ha familiarità con gli intervalli degli indirizzi IP disponibili nella configurazione della rete locale, è necessario coordinarsi con qualcuno che possa fornire tali dettagli.</span><span class="sxs-lookup"><span data-stu-id="801d1-122">If you are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="801d1-123">Quando si crea questa configurazione, è necessario specificare i prefissi degli intervalli di indirizzi IP che Azure instraderà alla posizione locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-123">When you create this configuration, you must specify the IP address range prefixes that Azure will route to your on-premises location.</span></span> <span data-ttu-id="801d1-124">Nessuna delle subnet della rete locale può sovrapporsi alle subnet della rete virtuale a cui ci si vuole connettere.</span><span class="sxs-lookup"><span data-stu-id="801d1-124">None of the subnets of your on-premises network can over lap with the virtual network subnets that you want to connect to.</span></span>
* <span data-ttu-id="801d1-125">Verificare di avere installato la versione più recente dei comandi dell'interfaccia della riga di comando (2.0 o successiva).</span><span class="sxs-lookup"><span data-stu-id="801d1-125">Verify that you have installed latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="801d1-126">Per informazioni sull'installazione dei comandi dell'interfaccia della riga di comando, vedere [Install Azure CLI 2.0](/cli/azure/install-azure-cli) (Installare l'interfaccia della riga di comando di Azure 2.0) e [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli) (Introduzione all'interfaccia della riga di comando di Azure 2.0).</span><span class="sxs-lookup"><span data-stu-id="801d1-126">For information about installing the CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="801d1-127"><a name="example"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="801d1-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="801d1-128">È possibile usare i valori seguenti per creare un ambiente di test o fare riferimento a questi valori per comprendere meglio gli esempi di questo articolo:</span><span class="sxs-lookup"><span data-stu-id="801d1-128">You can use the following values to create a test environment, or refer to these values to better understand the examples in this article:</span></span>

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <span data-ttu-id="801d1-129"><a name="Login"></a>1. Eseguire la connessione alla sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="801d1-129"><a name="Login"></a>1. Connect to your subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="801d1-130"><a name="rg"></a>2. Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="801d1-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="801d1-131">L'esempio seguente crea un gruppo di risorse denominato "TestRG1" nella località "eastus".</span><span class="sxs-lookup"><span data-stu-id="801d1-131">The following example creates a resource group named 'TestRG1' in the 'eastus' location.</span></span> <span data-ttu-id="801d1-132">Se è già disponibile un gruppo di risorse nell'area in cui si vuole creare la rete virtuale, è possibile usarlo.</span><span class="sxs-lookup"><span data-stu-id="801d1-132">If you already have a resource group in the region that you want to create your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="801d1-133"><a name="VNet"></a>3. Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="801d1-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="801d1-134">Se non si ha già una rete virtuale, crearne una usando il comando [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="801d1-134">If you don't already have a virtual network, create one using the [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="801d1-135">Quando si crea una rete virtuale, verificare che gli spazi di indirizzi specificati non si sovrappongano agli spazi di indirizzi presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-135">When creating a virtual network, make sure that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="801d1-136">L'esempio seguente crea una rete virtuale denominata "TestVNet1" e una subnet "Subnet1".</span><span class="sxs-lookup"><span data-stu-id="801d1-136">The following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="801d1-137">4. <a name="gwsub"></a>Creare la subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="801d1-137">4. <a name="gwsub"></a>Create the gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="801d1-138">Per questa configurazione, è necessaria anche una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="801d1-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="801d1-139">Il gateway di rete virtuale usa una subnet del gateway che contiene gli indirizzi IP usati dai servizi del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-139">The virtual network gateway uses a gateway subnet that contains the IP addresses that are used by the VPN gateway services.</span></span> <span data-ttu-id="801d1-140">Quando si crea una subnet del gateway, deve essere denominata "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="801d1-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="801d1-141">Se si assegna un nome diverso, la subnet viene creata, ma non verrà trattata da Azure come una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="801d1-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="801d1-142">Le dimensioni della subnet del gateway specificata dipendono dalla configurazione del gateway VPN che si vuole creare.</span><span class="sxs-lookup"><span data-stu-id="801d1-142">The size of the gateway subnet that you specify depends on the VPN gateway configuration that you want to create.</span></span> <span data-ttu-id="801d1-143">Nonostante sia possibile creare una subnet del gateway con dimensioni di /29 soltanto, è consigliabile crearne una più grande che includa più indirizzi selezionando /27 o /28.</span><span class="sxs-lookup"><span data-stu-id="801d1-143">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="801d1-144">L'uso di una subnet del gateway di dimensioni maggiori consente un numero sufficiente di indirizzi IP per eventuali configurazioni future.</span><span class="sxs-lookup"><span data-stu-id="801d1-144">Using a larger gateway subnet allows for enough IP addresses to accommodate possible future configurations.</span></span>

<span data-ttu-id="801d1-145">Usare il comando [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) per creare la subnet gateway.</span><span class="sxs-lookup"><span data-stu-id="801d1-145">Use the [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command to create the gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="801d1-146"><a name="localnet"></a>5. Creare il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="801d1-146"><a name="localnet"></a>5. Create the local network gateway</span></span>

<span data-ttu-id="801d1-147">Il gateway di rete locale in genere fa riferimento al percorso locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-147">The local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="801d1-148">Assegnare al sito un nome che Azure possa usare come riferimento, quindi specificare l'indirizzo IP del dispositivo VPN locale con cui si creerà una connessione.</span><span class="sxs-lookup"><span data-stu-id="801d1-148">You give the site a name by which Azure can refer to it, then specify the IP address of the on-premises VPN device to which you will create a connection.</span></span> <span data-ttu-id="801d1-149">Specificare anche i prefissi degli indirizzi IP che verranno instradati tramite il gateway VPN al dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-149">You also specify the IP address prefixes that will be routed through the VPN gateway to the VPN device.</span></span> <span data-ttu-id="801d1-150">I prefissi degli indirizzi specificati sono quelli disponibili nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-150">The address prefixes you specify are the prefixes located on your on-premises network.</span></span> <span data-ttu-id="801d1-151">Se la rete locale viene modificata, è possibile aggiornare facilmente i prefissi.</span><span class="sxs-lookup"><span data-stu-id="801d1-151">If your on-premises network changes, you can easily update the prefixes.</span></span>

<span data-ttu-id="801d1-152">Usare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="801d1-152">Use the following values:</span></span>

* <span data-ttu-id="801d1-153">*--gateway-ip-address* è l'indirizzo IP del dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-153">The *--gateway-ip-address* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="801d1-154">Il dispositivo VPN non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="801d1-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="801d1-155">*--local-address-prefixes* sono gli spazi di indirizzi locali.</span><span class="sxs-lookup"><span data-stu-id="801d1-155">The *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="801d1-156">Usare il comando [az network local-gateway create](/cli/azure/network/local-gateway#create) per aggiungere un gateway di rete locale con più prefissi degli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="801d1-156">Use the [az network local-gateway create](/cli/azure/network/local-gateway#create) command to add a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="801d1-157"><a name="PublicIP"></a>6. Richiedere un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="801d1-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="801d1-158">Un gateway VPN deve avere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="801d1-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="801d1-159">È necessario richiedere prima di tutto la risorsa dell'indirizzo IP e quindi farvi riferimento durante la creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="801d1-159">You first request the IP address resource, and then refer to it when creating your virtual network gateway.</span></span> <span data-ttu-id="801d1-160">L'indirizzo IP viene assegnato dinamicamente alla risorsa durante la creazione del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-160">The IP address is dynamically assigned to the resource when the VPN gateway is created.</span></span> <span data-ttu-id="801d1-161">Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*.</span><span class="sxs-lookup"><span data-stu-id="801d1-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="801d1-162">Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici.</span><span class="sxs-lookup"><span data-stu-id="801d1-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="801d1-163">Ciò non significa tuttavia che l'indirizzo IP viene modificato dopo l'assegnazione al gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-163">However, this does not mean that the IP address changes after it has been assigned to your VPN gateway.</span></span> <span data-ttu-id="801d1-164">L'indirizzo IP pubblico viene modificato solo quando il gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="801d1-164">The only time the Public IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="801d1-165">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="801d1-166">Usare il comando [az network public-ip create](/cli/azure/network/public-ip#create) per richiedere un indirizzo IP pubblico dinamico.</span><span class="sxs-lookup"><span data-stu-id="801d1-166">Use the [az network public-ip create](/cli/azure/network/public-ip#create) command to request a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="801d1-167"><a name="CreateGateway"></a>7. Creare il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="801d1-167"><a name="CreateGateway"></a>7. Create the VPN gateway</span></span>

<span data-ttu-id="801d1-168">Creare il gateway VPN di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="801d1-168">Create the virtual network VPN gateway.</span></span> <span data-ttu-id="801d1-169">Per completare la creazione di un gateway VPN, possono essere necessari fino a 45 minuti o più.</span><span class="sxs-lookup"><span data-stu-id="801d1-169">Creating a VPN gateway can take up to 45 minutes or more to complete.</span></span>

<span data-ttu-id="801d1-170">Usare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="801d1-170">Use the following values:</span></span>

* <span data-ttu-id="801d1-171">Il valore di *--gateway-type* per una configurazione da sito a sito è *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="801d1-171">The *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="801d1-172">Il tipo di gateway è sempre specifico della configurazione che si sta implementando.</span><span class="sxs-lookup"><span data-stu-id="801d1-172">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="801d1-173">Per altre informazioni, vedere [Tipi di gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="801d1-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="801d1-174">Il valore di *--vpn-type* può essere *RouteBased*, talvolta definito gateway dinamico nella documentazione, o *PolicyBased*, talvolta definito gateway statico nella documentazione.</span><span class="sxs-lookup"><span data-stu-id="801d1-174">The *--vpn-type* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="801d1-175">L'impostazione è specifica dei requisiti del dispositivo a cui ci si connette.</span><span class="sxs-lookup"><span data-stu-id="801d1-175">The setting is specific to requirements of the device that you are connecting to.</span></span> <span data-ttu-id="801d1-176">Per altre informazioni sui tipi di gateway VPN, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="801d1-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="801d1-177">Selezionare lo SKU del gateway da usare.</span><span class="sxs-lookup"><span data-stu-id="801d1-177">Select the Gateway SKU that you want to use.</span></span> <span data-ttu-id="801d1-178">Esistono limitazioni di configurazione per alcuni SKU.</span><span class="sxs-lookup"><span data-stu-id="801d1-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="801d1-179">Per altre informazioni, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="801d1-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="801d1-180">Creare il gateway VPN usando il comando [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create).</span><span class="sxs-lookup"><span data-stu-id="801d1-180">Create the VPN gateway using the [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="801d1-181">Se si esegue questo comando usando il parametro '--no-wait', non viene visualizzato alcun output o commento.</span><span class="sxs-lookup"><span data-stu-id="801d1-181">If you run this command using the '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="801d1-182">Questo parametro consente la creazione in background del gateway.</span><span class="sxs-lookup"><span data-stu-id="801d1-182">This parameter allows the gateway to create in the background.</span></span> <span data-ttu-id="801d1-183">La creazione di un gateway richiede circa 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="801d1-183">It takes around 45 minutes to create a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="801d1-184"><a name="VPNDevice"></a>8. Configurare il dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="801d1-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="801d1-185">Le connessioni da sito a sito verso una rete locale richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-185">Site-to-Site connections to an on-premises network require a VPN device.</span></span> <span data-ttu-id="801d1-186">In questo passaggio viene configurato il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="801d1-187">Durante la configurazione del dispositivo VPN, è necessario quanto segue:</span><span class="sxs-lookup"><span data-stu-id="801d1-187">When configuring your VPN device, you need the following:</span></span>

- <span data-ttu-id="801d1-188">Chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="801d1-188">A shared key.</span></span> <span data-ttu-id="801d1-189">Si tratta della stessa chiave condivisa che viene specificata durante la creazione della connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="801d1-189">This is the same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="801d1-190">In questi esempi viene usata una chiave condivisa semplice.</span><span class="sxs-lookup"><span data-stu-id="801d1-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="801d1-191">È consigliabile generare una chiave più complessa per l'uso effettivo.</span><span class="sxs-lookup"><span data-stu-id="801d1-191">We recommend that you generate a more complex key to use.</span></span>
- <span data-ttu-id="801d1-192">Indirizzo IP pubblico del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="801d1-192">The Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="801d1-193">È possibile visualizzare l'indirizzo IP pubblico usando il portale di Azure, PowerShell o l'interfaccia della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="801d1-193">You can view the public IP address by using the Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="801d1-194">Per trovare l'indirizzo IP pubblico del gateway di rete virtuale, usare il comando [az network public-ip list](/cli/azure/network/public-ip#list).</span><span class="sxs-lookup"><span data-stu-id="801d1-194">To find the public IP address of your virtual network gateway, use the [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="801d1-195">Per facilitare la lettura, la formattazione dell'output visualizza l'elenco di IP pubblici in formato tabella.</span><span class="sxs-lookup"><span data-stu-id="801d1-195">For easy reading, the output is formatted to display the list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="801d1-196"><a name="CreateConnection"></a>9. Creare la connessione VPN</span><span class="sxs-lookup"><span data-stu-id="801d1-196"><a name="CreateConnection"></a>9. Create the VPN connection</span></span>

<span data-ttu-id="801d1-197">Creare la connessione VPN da sito a sito tra il gateway di rete virtuale e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="801d1-197">Create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="801d1-198">Prestare particolare attenzione al valore della chiave condivisa, che deve corrispondere al valore della chiave condivisa configurato per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="801d1-198">Pay particular attention to the shared key value, which must match the configured shared key value for your VPN device.</span></span>

<span data-ttu-id="801d1-199">Creare la connessione usando il comando [az network vpn-connection create](/cli/azure/network/vpn-connection#create).</span><span class="sxs-lookup"><span data-stu-id="801d1-199">Create the connection using the [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="801d1-200">La connessione verrà stabilita in breve tempo.</span><span class="sxs-lookup"><span data-stu-id="801d1-200">After a short while, the connection will be established.</span></span>

## <span data-ttu-id="801d1-201"><a name="toverify"></a>10. Verificare la connessione VPN</span><span class="sxs-lookup"><span data-stu-id="801d1-201"><a name="toverify"></a>10. Verify the VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="801d1-202">Per usare un altro metodo per verificare la connessione, vedere [Verificare una connessione di Gateway VPN](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-202">If you want to use another method to verify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="801d1-203"><a name="connectVM"></a>Per connettersi a una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="801d1-203"><a name="connectVM"></a>To connect to a virtual machine</span></span>

[!INCLUDE [Connect to a VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="801d1-204"><a name="tasks"></a>Attività comuni</span><span class="sxs-lookup"><span data-stu-id="801d1-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="801d1-205">Questa sezione contiene i comandi comuni che risultano utili quando si usano configurazioni da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="801d1-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="801d1-206">Per l'elenco completo dei comandi di rete dell'interfaccia della riga di comando, vedere [Azure CLI - Networking](/cli/azure/network) (Interfaccia della riga di comando di Azure - Rete).</span><span class="sxs-lookup"><span data-stu-id="801d1-206">For the full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="801d1-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="801d1-207">Next steps</span></span>

* <span data-ttu-id="801d1-208">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="801d1-208">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="801d1-209">Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="801d1-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="801d1-210">Per informazioni su BGP, vedere [Panoramica di BGP](vpn-gateway-bgp-overview.md) e [Come configurare BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-210">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="801d1-211">Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="801d1-212">Per informazioni sulle connessioni da rete attiva a rete attiva a disponibilità elevata, vedere [Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="801d1-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="801d1-213">Per un elenco di comandi dell'interfaccia della riga di comando di Azure di rete, vedere [Azure CLI](https://docs.microsoft.com/cli/azure/network) (Interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="801d1-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>