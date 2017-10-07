---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: CLI | Documenti Microsoft'
description: "Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questa procedura consentirà di creare una connessione gateway VPN da sito a sito cross-premise usando l'interfaccia della riga di comando."
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
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a><span data-ttu-id="feb1a-104">Creare una rete virtuale con una connessione VPN da sito a sito usando l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="feb1a-104">Create a virtual network with a Site-to-Site VPN connection using CLI</span></span>

<span data-ttu-id="feb1a-105">Questo articolo illustra come toouse hello Azure CLI toocreate una connessione gateway VPN da sito a sito dal toohello di rete locale rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-105">This article shows you how toouse hello Azure CLI toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="feb1a-106">passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="feb1a-107">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="feb1a-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span><br>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="feb1a-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="feb1a-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="feb1a-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="feb1a-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="feb1a-110">CLI</span><span class="sxs-lookup"><span data-stu-id="feb1a-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="feb1a-111">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="feb1a-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

<span data-ttu-id="feb1a-113">Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="feb1a-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="feb1a-114">Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="feb1a-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="feb1a-115">Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="feb1a-116">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="feb1a-116">Before you begin</span></span>

<span data-ttu-id="feb1a-117">Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:</span><span class="sxs-lookup"><span data-stu-id="feb1a-117">Verify that you have met hello following criteria before beginning configuration:</span></span>

* <span data-ttu-id="feb1a-118">Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è.</span><span class="sxs-lookup"><span data-stu-id="feb1a-118">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="feb1a-119">Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-119">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="feb1a-120">Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="feb1a-120">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="feb1a-121">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="feb1a-121">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="feb1a-122">Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente.</span><span class="sxs-lookup"><span data-stu-id="feb1a-122">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="feb1a-123">Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="feb1a-123">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="feb1a-124">Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-124">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="feb1a-125">Verificare di aver installato la versione più recente di comandi CLI di hello (2.0 o versione successiva).</span><span class="sxs-lookup"><span data-stu-id="feb1a-125">Verify that you have installed latest version of hello CLI commands (2.0 or later).</span></span> <span data-ttu-id="feb1a-126">Per informazioni sull'installazione di comandi CLI hello, vedere [installare Azure CLI 2.0](/cli/azure/install-azure-cli) e [Introduzione a Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="feb1a-126">For information about installing hello CLI commands, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli) and [Get Started with Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>

### <span data-ttu-id="feb1a-127"><a name="example"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="feb1a-127"><a name="example"></a>Example values</span></span>

<span data-ttu-id="feb1a-128">È possibile utilizzare hello seguente valori toocreate un ambiente di test, o fare riferimento a valori toothese toobetter comprendere esempi hello in questo articolo:</span><span class="sxs-lookup"><span data-stu-id="feb1a-128">You can use hello following values toocreate a test environment, or refer toothese values toobetter understand hello examples in this article:</span></span>

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

## <span data-ttu-id="feb1a-129"><a name="Login"></a>1. Connettere tooyour sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="feb1a-129"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="feb1a-130"><a name="rg"></a>2. Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="feb1a-130"><a name="rg"></a>2. Create a resource group</span></span>

<span data-ttu-id="feb1a-131">Hello seguente viene creato un gruppo di risorse denominato 'TestRG1' nel percorso 'eastus' hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-131">hello following example creates a resource group named 'TestRG1' in hello 'eastus' location.</span></span> <span data-ttu-id="feb1a-132">Se si dispone già di un gruppo di risorse nell'area di hello che si desidera toocreate la rete virtuale, è possibile utilizzare invece che uno.</span><span class="sxs-lookup"><span data-stu-id="feb1a-132">If you already have a resource group in hello region that you want toocreate your VNet, you can use that one instead.</span></span>

```azurecli
az group create --name TestRG1 --location eastus
```

## <span data-ttu-id="feb1a-133"><a name="VNet"></a>3. Crea rete virtuale</span><span class="sxs-lookup"><span data-stu-id="feb1a-133"><a name="VNet"></a>3. Create a virtual network</span></span>

<span data-ttu-id="feb1a-134">Se si dispone già di una rete virtuale, crearne uno utilizzando hello [creazione della rete virtuale di rete az](/cli/azure/network/vnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-134">If you don't already have a virtual network, create one using hello [az network vnet create](/cli/azure/network/vnet#create) command.</span></span> <span data-ttu-id="feb1a-135">Quando si crea una rete virtuale, assicurarsi che gli spazi degli indirizzi hello specificato non si sovrappongano agli hello gli spazi degli indirizzi presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-135">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="feb1a-136">Hello seguente viene creata una rete virtuale denominata 'TestVNet1' e una subnet, 'Subnet1'.</span><span class="sxs-lookup"><span data-stu-id="feb1a-136">hello following example creates a virtual network named 'TestVNet1' and a subnet, 'Subnet1'.</span></span>

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## <span data-ttu-id="feb1a-137">4. <a name="gwsub"></a>Creare subnet del gateway hello</span><span class="sxs-lookup"><span data-stu-id="feb1a-137">4. <a name="gwsub"></a>Create hello gateway subnet</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="feb1a-138">Per questa configurazione, è necessaria anche una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="feb1a-138">For this configuration, you also need a gateway subnet.</span></span> <span data-ttu-id="feb1a-139">gateway di rete virtuale Hello utilizza una subnet del gateway che contiene gli indirizzi IP hello utilizzate dai servizi gateway VPN di hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-139">hello virtual network gateway uses a gateway subnet that contains hello IP addresses that are used by hello VPN gateway services.</span></span> <span data-ttu-id="feb1a-140">Quando si crea una subnet del gateway, deve essere denominata "GatewaySubnet".</span><span class="sxs-lookup"><span data-stu-id="feb1a-140">When you create a gateway subnet, it must be named 'GatewaySubnet'.</span></span> <span data-ttu-id="feb1a-141">Se si assegna un nome diverso, la subnet viene creata, ma non verrà trattata da Azure come una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="feb1a-141">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="feb1a-142">dimensioni Hello di subnet del gateway hello specificati dipendono dalla configurazione di gateway VPN hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="feb1a-142">hello size of hello gateway subnet that you specify depends on hello VPN gateway configuration that you want toocreate.</span></span> <span data-ttu-id="feb1a-143">Sebbene sia possibile toocreate assuma /29 una subnet del gateway, è consigliabile creare una subnet più grande che include più indirizzi selezionando /27 o /28.</span><span class="sxs-lookup"><span data-stu-id="feb1a-143">While it is possible toocreate a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting /27 or /28.</span></span> <span data-ttu-id="feb1a-144">Utilizzando una subnet del gateway più grande consente sufficiente IP indirizzi tooaccommodate future configurazioni possibili.</span><span class="sxs-lookup"><span data-stu-id="feb1a-144">Using a larger gateway subnet allows for enough IP addresses tooaccommodate possible future configurations.</span></span>

<span data-ttu-id="feb1a-145">Hello utilizzare [creare subnet della rete virtuale rete az](/cli/azure/network/vnet/subnet#create) subnet del gateway hello toocreate comando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-145">Use hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command toocreate hello gateway subnet.</span></span>

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <span data-ttu-id="feb1a-146"><a name="localnet"></a>5. Creare il gateway di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="feb1a-146"><a name="localnet"></a>5. Create hello local network gateway</span></span>

<span data-ttu-id="feb1a-147">gateway di rete locale Hello si riferisce solitamente percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="feb1a-147">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="feb1a-148">Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione.</span><span class="sxs-lookup"><span data-stu-id="feb1a-148">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="feb1a-149">È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="feb1a-149">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="feb1a-150">specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-150">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="feb1a-151">Se la rete locale viene modificata, è possibile aggiornare facilmente i prefissi hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-151">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="feb1a-152">Utilizzare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="feb1a-152">Use hello following values:</span></span>

* <span data-ttu-id="feb1a-153">Hello *--indirizzo ip del gateway* hello di indirizzo IP del dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-153">hello *--gateway-ip-address* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="feb1a-154">Il dispositivo VPN non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="feb1a-154">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="feb1a-155">Hello *-prefissi di indirizzi locale* sono di spazi degli indirizzi locale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-155">hello *--local-address-prefixes* are your on-premises address spaces.</span></span>

<span data-ttu-id="feb1a-156">Hello utilizzare [locale-gateway di rete az creare](/cli/azure/network/local-gateway#create) comando tooadd un gateway di rete locale con più prefissi di indirizzo:</span><span class="sxs-lookup"><span data-stu-id="feb1a-156">Use hello [az network local-gateway create](/cli/azure/network/local-gateway#create) command tooadd a local network gateway with multiple address prefixes:</span></span>

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <span data-ttu-id="feb1a-157"><a name="PublicIP"></a>6. Richiedere un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="feb1a-157"><a name="PublicIP"></a>6. Request a Public IP address</span></span>

<span data-ttu-id="feb1a-158">Un gateway VPN deve avere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="feb1a-158">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="feb1a-159">Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-159">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="feb1a-160">indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-160">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="feb1a-161">Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*.</span><span class="sxs-lookup"><span data-stu-id="feb1a-161">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="feb1a-162">Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici.</span><span class="sxs-lookup"><span data-stu-id="feb1a-162">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="feb1a-163">Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour.</span><span class="sxs-lookup"><span data-stu-id="feb1a-163">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="feb1a-164">Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="feb1a-164">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="feb1a-165">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="feb1a-165">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="feb1a-166">Hello utilizzare [az rete public-ip creare](/cli/azure/network/public-ip#create) comando toorequest un indirizzo IP pubblico dinamica.</span><span class="sxs-lookup"><span data-stu-id="feb1a-166">Use hello [az network public-ip create](/cli/azure/network/public-ip#create) command toorequest a Dynamic Public IP address.</span></span>

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <span data-ttu-id="feb1a-167"><a name="CreateGateway"></a>7. Creare il gateway VPN hello</span><span class="sxs-lookup"><span data-stu-id="feb1a-167"><a name="CreateGateway"></a>7. Create hello VPN gateway</span></span>

<span data-ttu-id="feb1a-168">Creare il gateway VPN di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-168">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="feb1a-169">Creazione di un gateway VPN può richiedere too45 minuti o più toocomplete.</span><span class="sxs-lookup"><span data-stu-id="feb1a-169">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="feb1a-170">Utilizzare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="feb1a-170">Use hello following values:</span></span>

* <span data-ttu-id="feb1a-171">Hello *-tipo di gateway* per un sito a sito è configurazione *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="feb1a-171">hello *--gateway-type* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="feb1a-172">tipo di gateway Hello è sempre configurazione toohello specifico che si sta implementando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-172">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="feb1a-173">Per altre informazioni, vedere [Tipi di gateway](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span><span class="sxs-lookup"><span data-stu-id="feb1a-173">For more information, see [Gateway types](vpn-gateway-about-vpn-gateway-settings.md#gwtype).</span></span>
* <span data-ttu-id="feb1a-174">Hello *- vpn-tipo* può essere *tipo RouteBased* (definita tooas un Gateway dinamico nella parte della documentazione), o *basato su criteri* (tooas un Gateway statico in alcune definito documentazione).</span><span class="sxs-lookup"><span data-stu-id="feb1a-174">hello *--vpn-type* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="feb1a-175">impostazione di Hello è toorequirements specifico del dispositivo hello che si desidera connettersi.</span><span class="sxs-lookup"><span data-stu-id="feb1a-175">hello setting is specific toorequirements of hello device that you are connecting to.</span></span> <span data-ttu-id="feb1a-176">Per altre informazioni sui tipi di gateway VPN, vedere [Informazioni sulle impostazioni di configurazione del gateway VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span><span class="sxs-lookup"><span data-stu-id="feb1a-176">For more information about VPN gateway types, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md#vpntype).</span></span>
* <span data-ttu-id="feb1a-177">Selezionare hello SKU di Gateway che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="feb1a-177">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="feb1a-178">Esistono limitazioni di configurazione per alcuni SKU.</span><span class="sxs-lookup"><span data-stu-id="feb1a-178">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="feb1a-179">Per altre informazioni, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="feb1a-179">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>

<span data-ttu-id="feb1a-180">Creare il gateway VPN hello utilizzando hello [creare reti virtuali-gateway di rete az](/cli/azure/network/vnet-gateway#create) comando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-180">Create hello VPN gateway using hello [az network vnet-gateway create](/cli/azure/network/vnet-gateway#create) command.</span></span> <span data-ttu-id="feb1a-181">Se si esegue questo comando hello utilizzando il parametro '-- Nessun - wait', non sono visibili eventuali commenti e suggerimenti o output.</span><span class="sxs-lookup"><span data-stu-id="feb1a-181">If you run this command using hello '--no-wait' parameter, you don't see any feedback or output.</span></span> <span data-ttu-id="feb1a-182">Questo parametro consente toocreate gateway hello in background hello.</span><span class="sxs-lookup"><span data-stu-id="feb1a-182">This parameter allows hello gateway toocreate in hello background.</span></span> <span data-ttu-id="feb1a-183">Sono necessari circa 45 minuti toocreate un gateway.</span><span class="sxs-lookup"><span data-stu-id="feb1a-183">It takes around 45 minutes toocreate a gateway.</span></span>

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <span data-ttu-id="feb1a-184"><a name="VPNDevice"></a>8. Configurare il dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="feb1a-184"><a name="VPNDevice"></a>8. Configure your VPN device</span></span>

<span data-ttu-id="feb1a-185">Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="feb1a-185">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="feb1a-186">In questo passaggio viene configurato il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="feb1a-186">In this step, you configure your VPN device.</span></span> <span data-ttu-id="feb1a-187">Quando si configura il dispositivo VPN, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="feb1a-187">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="feb1a-188">Chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="feb1a-188">A shared key.</span></span> <span data-ttu-id="feb1a-189">Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="feb1a-189">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="feb1a-190">In questi esempi viene usata una chiave condivisa semplice.</span><span class="sxs-lookup"><span data-stu-id="feb1a-190">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="feb1a-191">Si consiglia di generare un toouse chiave più complesse.</span><span class="sxs-lookup"><span data-stu-id="feb1a-191">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="feb1a-192">Hello indirizzo IP pubblico del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-192">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="feb1a-193">È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="feb1a-193">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="feb1a-194">toofind hello indirizzo IP pubblico del gateway di rete virtuale, utilizzare hello [elenco public-ip di rete az](/cli/azure/network/public-ip#list) comando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-194">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="feb1a-195">Per facilitare la lettura, output di hello è elenco hello toodisplay formattato di indirizzi IP pubblici in formato tabella.</span><span class="sxs-lookup"><span data-stu-id="feb1a-195">For easy reading, hello output is formatted toodisplay hello list of public IPs in table format.</span></span>

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="feb1a-196"><a name="CreateConnection"></a>9. Creare la connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="feb1a-196"><a name="CreateConnection"></a>9. Create hello VPN connection</span></span>

<span data-ttu-id="feb1a-197">Creare la connessione VPN Site-to-Site hello tra il gateway di rete virtuale e il dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="feb1a-197">Create hello Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="feb1a-198">Retribuzione particolare attenzione toohello condiviso valore chiave, che deve corrispondere a hello configurato condivisa valore della chiave per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="feb1a-198">Pay particular attention toohello shared key value, which must match hello configured shared key value for your VPN device.</span></span>

<span data-ttu-id="feb1a-199">Creare una connessione hello utilizzando hello [az vpn di rete-connessione creare](/cli/azure/network/vpn-connection#create) comando.</span><span class="sxs-lookup"><span data-stu-id="feb1a-199">Create hello connection using hello [az network vpn-connection create](/cli/azure/network/vpn-connection#create) command.</span></span>

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

<span data-ttu-id="feb1a-200">Poco dopo, hello connessione verrà stabilita.</span><span class="sxs-lookup"><span data-stu-id="feb1a-200">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="feb1a-201"><a name="toverify"></a>10. Verificare una connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="feb1a-201"><a name="toverify"></a>10. Verify hello VPN connection</span></span>

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

<span data-ttu-id="feb1a-202">Se si desidera toouse un altro metodo tooverify la connessione, vedere [verificare una connessione VPN Gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-202">If you want toouse another method tooverify your connection, see [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

## <span data-ttu-id="feb1a-203"><a name="connectVM"></a>macchina virtuale di tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="feb1a-203"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <span data-ttu-id="feb1a-204"><a name="tasks"></a>Attività comuni</span><span class="sxs-lookup"><span data-stu-id="feb1a-204"><a name="tasks"></a>Common tasks</span></span>

<span data-ttu-id="feb1a-205">Questa sezione contiene i comandi comuni che risultano utili quando si usano configurazioni da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="feb1a-205">This section contains common commands that are helpful when working with site-to-site configurations.</span></span> <span data-ttu-id="feb1a-206">Per hello l'elenco completo di comandi CLI di rete, vedere [CLI di Azure - rete](/cli/azure/network).</span><span class="sxs-lookup"><span data-stu-id="feb1a-206">For hello full list of CLI networking commands, see [Azure CLI - Networking](/cli/azure/network).</span></span>

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="feb1a-207">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="feb1a-207">Next steps</span></span>

* <span data-ttu-id="feb1a-208">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="feb1a-208">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="feb1a-209">Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="feb1a-209">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="feb1a-210">Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-210">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
* <span data-ttu-id="feb1a-211">Per informazioni sul tunneling forzato, vedere [Informazioni sul tunneling forzato](vpn-gateway-forced-tunneling-rm.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-211">For information about Forced Tunneling, see [About Forced Tunneling](vpn-gateway-forced-tunneling-rm.md).</span></span>
* <span data-ttu-id="feb1a-212">Per informazioni sulle connessioni da rete attiva a rete attiva a disponibilità elevata, vedere [Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata](vpn-gateway-highlyavailable.md).</span><span class="sxs-lookup"><span data-stu-id="feb1a-212">For information about Highly Available Active-Active connections, see [Highly Available cross-premises and VNet-to-VNet connectivity](vpn-gateway-highlyavailable.md).</span></span>
* <span data-ttu-id="feb1a-213">Per un elenco di comandi dell'interfaccia della riga di comando di Azure di rete, vedere [Azure CLI](https://docs.microsoft.com/cli/azure/network) (Interfaccia della riga di comando di Azure).</span><span class="sxs-lookup"><span data-stu-id="feb1a-213">For a list of networking Azure CLI commands, see [Azure CLI](https://docs.microsoft.com/cli/azure/network).</span></span>