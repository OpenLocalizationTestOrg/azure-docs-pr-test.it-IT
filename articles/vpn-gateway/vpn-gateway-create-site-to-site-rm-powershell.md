---
title: 'Connettere il tooan di rete locale rete virtuale di Azure: VPN Site-to-Site: PowerShell | Documenti Microsoft'
description: "Passaggi toocreate una connessione IPsec da locale rete tooan rete virtuale di Azure su hello rete Internet pubblica. Questa procedura consentirà di creare una connessione gateway VPN da sito a sito cross-premise usando PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="518bc-104">Creare una rete virtuale con una connessione VPN da sito a sito usando PowerShell e Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="518bc-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="518bc-105">Questo articolo illustra come connessione di PowerShell toocreate una Site-to-Site VPN gateway da locale toouse rete toohello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-105">This article shows you how toouse PowerShell toocreate a Site-to-Site VPN gateway connection from your on-premises network toohello VNet.</span></span> <span data-ttu-id="518bc-106">passaggi di Hello in questo articolo si applicano al modello di distribuzione di gestione delle risorse toohello.</span><span class="sxs-lookup"><span data-stu-id="518bc-106">hello steps in this article apply toohello Resource Manager deployment model.</span></span> <span data-ttu-id="518bc-107">È inoltre possibile creare questa configurazione tramite uno strumento di distribuzione diverso o un modello di distribuzione selezionando un'opzione diversa da hello seguente elenco:</span><span class="sxs-lookup"><span data-stu-id="518bc-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="518bc-108">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="518bc-108">Azure portal</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="518bc-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="518bc-109">PowerShell</span></span>](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [<span data-ttu-id="518bc-110">CLI</span><span class="sxs-lookup"><span data-stu-id="518bc-110">CLI</span></span>](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [<span data-ttu-id="518bc-111">Portale di Azure (classico)</span><span class="sxs-lookup"><span data-stu-id="518bc-111">Azure portal (classic)</span></span>](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [<span data-ttu-id="518bc-112">Portale classico (versione classica)</span><span class="sxs-lookup"><span data-stu-id="518bc-112">Classic portal (classic)</span></span>](vpn-gateway-site-to-site-create.md)
> 
>


<span data-ttu-id="518bc-113">Una connessione gateway VPN da sito a sito viene usato tooconnect tooan rete virtuale di Azure di rete locale tramite un tunnel VPN IPsec/IKE (IKEv1 o IKEv2).</span><span class="sxs-lookup"><span data-stu-id="518bc-113">A Site-to-Site VPN gateway connection is used tooconnect your on-premises network tooan Azure virtual network over an IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="518bc-114">Questo tipo di connessione richiede un VPN dispositivo si trova in locale che dispone di un tooit di indirizzo IP pubblico accessibile pubblicamente.</span><span class="sxs-lookup"><span data-stu-id="518bc-114">This type of connection requires a VPN device located on-premises that has an externally facing public IP address assigned tooit.</span></span> <span data-ttu-id="518bc-115">Per altre informazioni sui gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="518bc-115">For more information about VPN gateways, see [About VPN gateway](vpn-gateway-about-vpngateways.md).</span></span>

![Diagramma della connessione cross-premise gateway VPN da sito a sito](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <span data-ttu-id="518bc-117"><a name="before"></a>Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="518bc-117"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="518bc-118">Verificare che siano stati soddisfatti i seguenti criteri prima di iniziare la configurazione di hello:</span><span class="sxs-lookup"><span data-stu-id="518bc-118">Verify that you have met hello following criteria before beginning your configuration:</span></span>

* <span data-ttu-id="518bc-119">Assicurarsi di disporre di un dispositivo VPN compatibile e un utente che è in grado di tooconfigure è.</span><span class="sxs-lookup"><span data-stu-id="518bc-119">Make sure you have a compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="518bc-120">Per altre informazioni sui dispositivi VPN compatibili e sulla configurazione dei dispositivi, vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="518bc-120">For more information about compatible VPN devices and device configuration, see [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="518bc-121">Verificare di avere un indirizzo IPv4 pubblico esterno per il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-121">Verify that you have an externally facing public IPv4 address for your VPN device.</span></span> <span data-ttu-id="518bc-122">L'indirizzo IP non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="518bc-122">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="518bc-123">Se non si ha familiarità con gli intervalli di indirizzi IP hello nello configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente.</span><span class="sxs-lookup"><span data-stu-id="518bc-123">If you are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="518bc-124">Quando si crea questa configurazione, è necessario specificare i prefissi intervallo indirizzi IP hello che Azure indirizzerà percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="518bc-124">When you create this configuration, you must specify hello IP address range prefixes that Azure will route tooyour on-premises location.</span></span> <span data-ttu-id="518bc-125">Nessuna delle subnet hello della rete locale può in giro con subnet della rete virtuale che si desidera tooconnect per hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-125">None of hello subnets of your on-premises network can over lap with hello virtual network subnets that you want tooconnect to.</span></span>
* <span data-ttu-id="518bc-126">Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="518bc-126">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="518bc-127">I cmdlet di PowerShell vengono aggiornati di frequente e sarà in genere necessario tooupdate il PowerShell cmdlet tooget hello funzionalità più recenti funzionalità.</span><span class="sxs-lookup"><span data-stu-id="518bc-127">PowerShell cmdlets are updated frequently and you will typically need tooupdate your PowerShell cmdlets tooget hello latest feature functionality.</span></span> <span data-ttu-id="518bc-128">Se non vengono aggiornati i cmdlet di PowerShell, i valori hello specificati potrebbero non riuscire.</span><span class="sxs-lookup"><span data-stu-id="518bc-128">If you don't update your PowerShell cmdlets, hello values specified may fail.</span></span> <span data-ttu-id="518bc-129">Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni su come scaricare e installare i cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="518bc-129">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information about downloading and installing PowerShell cmdlets.</span></span>

### <span data-ttu-id="518bc-130"><a name="example"></a>Valori di esempio</span><span class="sxs-lookup"><span data-stu-id="518bc-130"><a name="example"></a>Example values</span></span>

<span data-ttu-id="518bc-131">esempi di Hello in questo articolo utilizzano hello seguenti valori.</span><span class="sxs-lookup"><span data-stu-id="518bc-131">hello examples in this article use hello following values.</span></span> <span data-ttu-id="518bc-132">È possibile utilizzare questi toocreate valori un ambiente di test, o fare riferimento toothem toobetter comprendere esempi hello in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="518bc-132">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <span data-ttu-id="518bc-133"><a name="Login"></a>1. Connettere tooyour sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="518bc-133"><a name="Login"></a>1. Connect tooyour subscription</span></span>

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <span data-ttu-id="518bc-134"><a name="VNet"></a>2. Creare una rete virtuale e una subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="518bc-134"><a name="VNet"></a>2. Create a virtual network and a gateway subnet</span></span>

<span data-ttu-id="518bc-135">Se non si ha una rete virtuale, crearne una.</span><span class="sxs-lookup"><span data-stu-id="518bc-135">If you don't already have a virtual network, create one.</span></span> <span data-ttu-id="518bc-136">Quando si crea una rete virtuale, assicurarsi che gli spazi degli indirizzi hello specificato non si sovrappongano agli hello gli spazi degli indirizzi presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="518bc-136">When creating a virtual network, make sure that hello address spaces you specify don't overlap any of hello address spaces that you have on your on-premises network.</span></span>

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <span data-ttu-id="518bc-137"><a name="vnet"></a>toocreate una rete virtuale e una subnet del gateway</span><span class="sxs-lookup"><span data-stu-id="518bc-137"><a name="vnet"></a>toocreate a virtual network and a gateway subnet</span></span>

<span data-ttu-id="518bc-138">Questo esempio crea una rete virtuale e una subnet del gateway.</span><span class="sxs-lookup"><span data-stu-id="518bc-138">This example creates a virtual network and a gateway subnet.</span></span> <span data-ttu-id="518bc-139">Se si dispone già di una rete virtuale, è necessario tooadd una subnet del gateway per visualizzare [tooadd una gateway subnet tooa rete virtuale è già stato creato](#gatewaysubnet).</span><span class="sxs-lookup"><span data-stu-id="518bc-139">If you already have a virtual network that you need tooadd a gateway subnet to, see [tooadd a gateway subnet tooa virtual network you have already created](#gatewaysubnet).</span></span>

<span data-ttu-id="518bc-140">Creare un gruppo di risorse:</span><span class="sxs-lookup"><span data-stu-id="518bc-140">Create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

<span data-ttu-id="518bc-141">Creare la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-141">Create your virtual network.</span></span>

1. <span data-ttu-id="518bc-142">Impostare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-142">Set hello variables.</span></span>

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. <span data-ttu-id="518bc-143">Creare hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-143">Create hello VNet.</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <span data-ttu-id="518bc-144"><a name="gatewaysubnet"></a>una rete virtuale di subnet tooa gateway tooadd è già stato creato</span><span class="sxs-lookup"><span data-stu-id="518bc-144"><a name="gatewaysubnet"></a>tooadd a gateway subnet tooa virtual network you have already created</span></span>

1. <span data-ttu-id="518bc-145">Impostare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-145">Set hello variables.</span></span>

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. <span data-ttu-id="518bc-146">Creare subnet del gateway hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-146">Create hello gateway subnet.</span></span>

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. <span data-ttu-id="518bc-147">Impostare la configurazione hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-147">Set hello configuration.</span></span>

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## <span data-ttu-id="518bc-148">3. <a name="localnet"></a>Creare il gateway di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="518bc-148">3. <a name="localnet"></a>Create hello local network gateway</span></span>

<span data-ttu-id="518bc-149">gateway di rete locale Hello si riferisce solitamente percorso locale tooyour.</span><span class="sxs-lookup"><span data-stu-id="518bc-149">hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="518bc-150">Assegnare un nome mediante il quale Azure può fare riferimento tooit, quindi specificare l'indirizzo IP hello a sito di hello di toowhich di dispositivo VPN locale hello verrà creata una connessione.</span><span class="sxs-lookup"><span data-stu-id="518bc-150">You give hello site a name by which Azure can refer tooit, then specify hello IP address of hello on-premises VPN device toowhich you will create a connection.</span></span> <span data-ttu-id="518bc-151">È inoltre possibile specificare i prefissi di indirizzo IP hello che verranno distribuiti tramite il dispositivo VPN toohello di hello VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="518bc-151">You also specify hello IP address prefixes that will be routed through hello VPN gateway toohello VPN device.</span></span> <span data-ttu-id="518bc-152">specificare i prefissi di indirizzo Hello sono prefissi hello presenti nella rete locale.</span><span class="sxs-lookup"><span data-stu-id="518bc-152">hello address prefixes you specify are hello prefixes located on your on-premises network.</span></span> <span data-ttu-id="518bc-153">Se la rete locale viene modificata, è possibile aggiornare facilmente i prefissi hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-153">If your on-premises network changes, you can easily update hello prefixes.</span></span>

<span data-ttu-id="518bc-154">Utilizzare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="518bc-154">Use hello following values:</span></span>

* <span data-ttu-id="518bc-155">Hello *GatewayIPAddress* hello di indirizzo IP del dispositivo VPN locale.</span><span class="sxs-lookup"><span data-stu-id="518bc-155">hello *GatewayIPAddress* is hello IP address of your on-premises VPN device.</span></span> <span data-ttu-id="518bc-156">Il dispositivo VPN non può trovarsi dietro un NAT.</span><span class="sxs-lookup"><span data-stu-id="518bc-156">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="518bc-157">Hello *AddressPrefix* sono locale lo spazio degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="518bc-157">hello *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="518bc-158">tooadd un gateway di rete locale con un singolo prefisso di indirizzo:</span><span class="sxs-lookup"><span data-stu-id="518bc-158">tooadd a local network gateway with a single address prefix:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

<span data-ttu-id="518bc-159">tooadd un gateway di rete locale con più prefissi di indirizzo:</span><span class="sxs-lookup"><span data-stu-id="518bc-159">tooadd a local network gateway with multiple address prefixes:</span></span>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

<span data-ttu-id="518bc-160">toomodify prefissi di indirizzi IP per il gateway di rete locale:</span><span class="sxs-lookup"><span data-stu-id="518bc-160">toomodify IP address prefixes for your local network gateway:</span></span><br>
<span data-ttu-id="518bc-161">Talvolta è possibile modificare i prefissi del gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="518bc-161">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="518bc-162">passaggi di Hello vengono toomodify l'indirizzo IP prefissi dipendono dal fatto di aver creato una connessione gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-162">hello steps you take toomodify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="518bc-163">Vedere hello [prefissi di indirizzi IP di modifica di un gateway di rete locale](#modify) sezione di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="518bc-163">See hello [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <span data-ttu-id="518bc-164"><a name="PublicIP"></a>4. Richiedere un indirizzo IP pubblico</span><span class="sxs-lookup"><span data-stu-id="518bc-164"><a name="PublicIP"></a>4. Request a Public IP address</span></span>

<span data-ttu-id="518bc-165">Un gateway VPN deve avere un indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="518bc-165">A VPN gateway must have a Public IP address.</span></span> <span data-ttu-id="518bc-166">Richiesta innanzitutto la risorsa indirizzo IP hello e fare riferimento tooit durante la creazione del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-166">You first request hello IP address resource, and then refer tooit when creating your virtual network gateway.</span></span> <span data-ttu-id="518bc-167">indirizzo IP Hello viene assegnata dinamicamente toohello risorsa quando viene creato gateway VPN hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-167">hello IP address is dynamically assigned toohello resource when hello VPN gateway is created.</span></span> <span data-ttu-id="518bc-168">Il gateway VPN supporta attualmente solo l'allocazione degli indirizzi IP pubblici *dinamici*.</span><span class="sxs-lookup"><span data-stu-id="518bc-168">VPN Gateway currently only supports *Dynamic* Public IP address allocation.</span></span> <span data-ttu-id="518bc-169">Non è possibile richiedere un'assegnazione degli indirizzi IP pubblici statici.</span><span class="sxs-lookup"><span data-stu-id="518bc-169">You cannot request a Static Public IP address assignment.</span></span> <span data-ttu-id="518bc-170">Tuttavia, ciò non significa che l'indirizzo IP hello cambia dopo che è stato assegnato come gateway VPN tooyour.</span><span class="sxs-lookup"><span data-stu-id="518bc-170">However, this does not mean that hello IP address changes after it has been assigned tooyour VPN gateway.</span></span> <span data-ttu-id="518bc-171">Hello unica volta in cui le modifiche all'indirizzo IP pubblico hello quando è hello gateway viene eliminato e ricreato.</span><span class="sxs-lookup"><span data-stu-id="518bc-171">hello only time hello Public IP address changes is when hello gateway is deleted and re-created.</span></span> <span data-ttu-id="518bc-172">Non viene modificato in caso di ridimensionamento, reimpostazione o altre manutenzioni/aggiornamenti del gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-172">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of your VPN gateway.</span></span>

<span data-ttu-id="518bc-173">Richiedere un indirizzo IP pubblico che verrà assegnato tooyour di gateway VPN di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-173">Request a Public IP address that will be assigned tooyour virtual network VPN gateway.</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <span data-ttu-id="518bc-174"><a name="GatewayIPConfig"></a>5. Creare una configurazione di indirizzamento IP del gateway hello</span><span class="sxs-lookup"><span data-stu-id="518bc-174"><a name="GatewayIPConfig"></a>5. Create hello gateway IP addressing configuration</span></span>

<span data-ttu-id="518bc-175">configurazione del gateway Hello definisce subnet hello e toouse di indirizzo IP pubblico hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-175">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="518bc-176">Utilizzare la configurazione del gateway di hello toocreate riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="518bc-176">Use hello following example toocreate your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <span data-ttu-id="518bc-177"><a name="CreateGateway"></a>6. Creare il gateway VPN hello</span><span class="sxs-lookup"><span data-stu-id="518bc-177"><a name="CreateGateway"></a>6. Create hello VPN gateway</span></span>

<span data-ttu-id="518bc-178">Creare il gateway VPN di rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-178">Create hello virtual network VPN gateway.</span></span> <span data-ttu-id="518bc-179">Creazione di un gateway VPN può richiedere too45 minuti o più toocomplete.</span><span class="sxs-lookup"><span data-stu-id="518bc-179">Creating a VPN gateway can take up too45 minutes or more toocomplete.</span></span>

<span data-ttu-id="518bc-180">Utilizzare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="518bc-180">Use hello following values:</span></span>

* <span data-ttu-id="518bc-181">Hello *- il tipo di gateway* per un sito a sito è configurazione *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="518bc-181">hello *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="518bc-182">tipo di gateway Hello è sempre configurazione toohello specifico che si sta implementando.</span><span class="sxs-lookup"><span data-stu-id="518bc-182">hello gateway type is always specific toohello configuration that you are implementing.</span></span> <span data-ttu-id="518bc-183">Ad esempio, altre configurazioni di gateway possono richiedere -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="518bc-183">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="518bc-184">Hello *- VpnType* può essere *tipo RouteBased* (definita tooas un Gateway dinamico nella parte della documentazione), o *basato su criteri* (denominato tooas un Gateway statico in una parte della documentazione ).</span><span class="sxs-lookup"><span data-stu-id="518bc-184">hello *-VpnType* can be *RouteBased* (referred tooas a Dynamic Gateway in some documentation), or *PolicyBased* (referred tooas a Static Gateway in some documentation).</span></span> <span data-ttu-id="518bc-185">Per altre informazioni sui tipi di gateway VPN, vedere [Informazioni sul gateway VPN](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="518bc-185">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="518bc-186">Selezionare hello SKU di Gateway che si desidera toouse.</span><span class="sxs-lookup"><span data-stu-id="518bc-186">Select hello Gateway SKU that you want toouse.</span></span> <span data-ttu-id="518bc-187">Esistono limitazioni di configurazione per alcuni SKU.</span><span class="sxs-lookup"><span data-stu-id="518bc-187">There are configuration limitations for certain SKUs.</span></span> <span data-ttu-id="518bc-188">Per altre informazioni, vedere [SKU del gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="518bc-188">For more information, see [Gateway SKUs](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span> <span data-ttu-id="518bc-189">Se si verifica un errore durante la creazione di gateway VPN hello riguardanti hello - GatewaySku, verificare di aver installato una versione più recente di hello hello di cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="518bc-189">If you get an error when creating hello VPN gateway regarding hello -GatewaySku, verify that you have installed hello latest version of hello PowerShell cmdlets.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <span data-ttu-id="518bc-190"><a name="ConfigureVPNDevice"></a>7. Configurare il dispositivo VPN</span><span class="sxs-lookup"><span data-stu-id="518bc-190"><a name="ConfigureVPNDevice"></a>7. Configure your VPN device</span></span>

<span data-ttu-id="518bc-191">Rete locale tooan di connessioni da sito a sito richiedono un dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-191">Site-to-Site connections tooan on-premises network require a VPN device.</span></span> <span data-ttu-id="518bc-192">In questo passaggio viene configurato il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-192">In this step, you configure your VPN device.</span></span> <span data-ttu-id="518bc-193">Quando si configura il dispositivo VPN, è necessario hello segue:</span><span class="sxs-lookup"><span data-stu-id="518bc-193">When configuring your VPN device, you need hello following:</span></span>

- <span data-ttu-id="518bc-194">Chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="518bc-194">A shared key.</span></span> <span data-ttu-id="518bc-195">Questo è hello stesso condiviso chiave specificate al momento della creazione della connessione VPN da sito a sito.</span><span class="sxs-lookup"><span data-stu-id="518bc-195">This is hello same shared key that you specify when creating your Site-to-Site VPN connection.</span></span> <span data-ttu-id="518bc-196">In questi esempi viene usata una chiave condivisa semplice.</span><span class="sxs-lookup"><span data-stu-id="518bc-196">In our examples, we use a basic shared key.</span></span> <span data-ttu-id="518bc-197">Si consiglia di generare un toouse chiave più complesse.</span><span class="sxs-lookup"><span data-stu-id="518bc-197">We recommend that you generate a more complex key toouse.</span></span>
- <span data-ttu-id="518bc-198">Hello indirizzo IP pubblico del gateway di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="518bc-198">hello Public IP address of your virtual network gateway.</span></span> <span data-ttu-id="518bc-199">È possibile visualizzare l'indirizzo IP pubblico hello utilizzando hello portale di Azure, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="518bc-199">You can view hello public IP address by using hello Azure portal, PowerShell, or CLI.</span></span> <span data-ttu-id="518bc-200">hello toofind indirizzo IP pubblico del gateway di rete virtuale con PowerShell, usare hello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="518bc-200">toofind hello Public IP address of your virtual network gateway using PowerShell, use hello following example:</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <span data-ttu-id="518bc-201"><a name="CreateConnection"></a>8. Creare la connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="518bc-201"><a name="CreateConnection"></a>8. Create hello VPN connection</span></span>

<span data-ttu-id="518bc-202">Creare quindi connessione Site-to-Site VPN hello tra il gateway di rete virtuale e il dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-202">Next, create hello Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="518bc-203">Essere certi tooreplace hello i valori con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="518bc-203">Be sure tooreplace hello values with your own.</span></span> <span data-ttu-id="518bc-204">chiave condivisa Hello deve corrispondere il valore di hello utilizzato per la configurazione del dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-204">hello shared key must match hello value you used for your VPN device configuration.</span></span> <span data-ttu-id="518bc-205">Si noti che hello '-ConnectionType' per il sito a sito è *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="518bc-205">Notice that hello '-ConnectionType' for Site-to-Site is *IPsec*.</span></span>

1. <span data-ttu-id="518bc-206">Impostare le variabili di hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-206">Set hello variables.</span></span>
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. <span data-ttu-id="518bc-207">Creare la connessione hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-207">Create hello connection.</span></span>
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

<span data-ttu-id="518bc-208">Poco dopo, hello connessione verrà stabilita.</span><span class="sxs-lookup"><span data-stu-id="518bc-208">After a short while, hello connection will be established.</span></span>

## <span data-ttu-id="518bc-209"><a name="toverify"></a>9. Verificare una connessione VPN hello</span><span class="sxs-lookup"><span data-stu-id="518bc-209"><a name="toverify"></a>9. Verify hello VPN connection</span></span>

<span data-ttu-id="518bc-210">Esistono alcuni modi diversi tooverify la connessione VPN.</span><span class="sxs-lookup"><span data-stu-id="518bc-210">There are a few different ways tooverify your VPN connection.</span></span>

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <span data-ttu-id="518bc-211"><a name="connectVM"></a>macchina virtuale di tooconnect tooa</span><span class="sxs-lookup"><span data-stu-id="518bc-211"><a name="connectVM"></a>tooconnect tooa virtual machine</span></span>

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <span data-ttu-id="518bc-212"><a name="modify"></a>Modificare i prefissi degli indirizzi IP per un gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="518bc-212"><a name="modify"></a>Modify IP address prefixes for a local network gateway</span></span>

<span data-ttu-id="518bc-213">Se i prefissi di indirizzi IP hello indirizzato percorso locale tooyour da modificano, è possibile modificare il gateway di rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="518bc-213">If hello IP address prefixes that you want routed tooyour on-premises location change, you can modify hello local network gateway.</span></span> <span data-ttu-id="518bc-214">Sono disponibili due set di istruzioni.</span><span class="sxs-lookup"><span data-stu-id="518bc-214">Two sets of instructions are provided.</span></span> <span data-ttu-id="518bc-215">istruzioni di Hello che prescelto variano a seconda se è già stato creato la connessione del gateway.</span><span class="sxs-lookup"><span data-stu-id="518bc-215">hello instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="518bc-216"><a name="modifygwipaddress"></a>Modificare l'indirizzo IP del gateway hello per un gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="518bc-216"><a name="modifygwipaddress"></a>Modify hello gateway IP address for a local network gateway</span></span>

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="518bc-217">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="518bc-217">Next steps</span></span>

*  <span data-ttu-id="518bc-218">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="518bc-218">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="518bc-219">Per altre informazioni, vedere [Macchine virtuali](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="518bc-219">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="518bc-220">Per informazioni su BGP, vedere hello [BGP Panoramica](vpn-gateway-bgp-overview.md) e [come tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="518bc-220">For information about BGP, see hello [BGP Overview](vpn-gateway-bgp-overview.md) and [How tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>
