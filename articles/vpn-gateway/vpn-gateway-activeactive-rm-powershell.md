---
title: Configurare connessioni di rete privata virtuale da sito a sito active-active per i gateway VPN - Azure Resource Manager - PowerShell | Microsoft Docs
description: In questo articolo viene illustrata la configurazione di connessioni active-active con i gateway VPN di Azure tramite Azure Resource Manager e PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="ccd33-103">Configurare connessioni di rete privata virtuale da sito a sito active-active con gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="ccd33-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="ccd33-104">In questo articolo illustra hello passaggi toocreate attivo-attivo cross-premise e connessioni di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccd33-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="ccd33-105">Informazioni sulle connessioni cross-premise a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="ccd33-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="ccd33-106">disponibilità elevata tooachieve per cross-premise e connettività di rete virtuale a, è necessario distribuire più gateway VPN e stabilire più connessioni parallele tra Azure e le reti.</span><span class="sxs-lookup"><span data-stu-id="ccd33-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="ccd33-107">Per una panoramica delle opzioni di connettività e della topologia, vedere [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) (Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata).</span><span class="sxs-lookup"><span data-stu-id="ccd33-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="ccd33-108">In questo articolo vengono fornite istruzioni hello tooset backup attivo-attivo cross-premise connessione VPN e attivo-attivo connessione tra due reti virtuali:</span><span class="sxs-lookup"><span data-stu-id="ccd33-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="ccd33-109">Parte 1: creare e configurare il gateway VPN di Azure in modalità active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="ccd33-110">Parte 2: stabilire connessioni cross-premise active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="ccd33-111">Parte 3: stabilire connessioni da rete virtuale a rete virtuale active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="ccd33-112">Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby</span><span class="sxs-lookup"><span data-stu-id="ccd33-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="ccd33-113">È possibile combinare queste toobuild insieme una topologia di rete più complessa, a elevata disponibilità che soddisfa le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="ccd33-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccd33-114">Si noti che la modalità attivo-attivo hello utilizza hello solo gli SKU di seguito:</span><span class="sxs-lookup"><span data-stu-id="ccd33-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="ccd33-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="ccd33-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="ccd33-116">HighPerformance (per SKU precedenti legacy)</span><span class="sxs-lookup"><span data-stu-id="ccd33-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="ccd33-117"><a name ="aagateway"></a>Parte 1: creare e configurare gateway VPN active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="ccd33-118">Hello alla procedura seguente configurerà il gateway VPN di Azure in modalità attivo-attivo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="ccd33-119">differenze principali di Hello tra i gateway attivo-attivo e attivo-standby hello:</span><span class="sxs-lookup"><span data-stu-id="ccd33-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="ccd33-120">È necessario toocreate due configurazioni IP del Gateway con due indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="ccd33-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="ccd33-121">È necessario impostare il flag di EnableActiveActiveFeature hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="ccd33-122">lo SKU del gateway Hello deve essere VpnGw1, VpnGw2, VpnGw3 o ad alte prestazioni (SKU legacy).</span><span class="sxs-lookup"><span data-stu-id="ccd33-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="ccd33-123">Hello altre proprietà sono hello come gateway di hello attivo-attivo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="ccd33-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ccd33-124">Before you begin</span></span>
* <span data-ttu-id="ccd33-125">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd33-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="ccd33-126">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ccd33-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ccd33-127">È necessario che i cmdlet PowerShell di gestione risorse di Azure di tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ccd33-128">Vedere [Panoramica di Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="ccd33-129">Passaggio 1: Creare e configurare VNet1</span><span class="sxs-lookup"><span data-stu-id="ccd33-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="ccd33-130">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="ccd33-130">1. Declare your variables</span></span>
<span data-ttu-id="ccd33-131">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="ccd33-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="ccd33-132">esempio Hello seguente dichiara variabili di hello utilizzando valori hello per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="ccd33-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="ccd33-133">Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="ccd33-134">Se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione, è possibile utilizzare queste variabili.</span><span class="sxs-lookup"><span data-stu-id="ccd33-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="ccd33-135">Modificare le variabili di hello e quindi copiare e incollare nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccd33-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="ccd33-136">2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="ccd33-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="ccd33-137">Accertarsi di passare hello toouse di modalità tooPowerShell cmdlet di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="ccd33-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="ccd33-138">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ccd33-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="ccd33-139">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ccd33-140">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="ccd33-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="ccd33-141">3. Creare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="ccd33-141">3. Create TestVNet1</span></span>
<span data-ttu-id="ccd33-142">esempio Hello seguente crea una rete virtuale denominata TestVNet1 e tre subnet, uno GatewaySubnet chiamato, un front-end denominato e un back-end denominato.</span><span class="sxs-lookup"><span data-stu-id="ccd33-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="ccd33-143">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="ccd33-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="ccd33-144">Se si assegnano altri nomi, la creazione del gateway avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="ccd33-145">Passaggio 2: creare il gateway VPN di hello per TestVNet1 con modalità attivo-attivo</span><span class="sxs-lookup"><span data-stu-id="ccd33-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="ccd33-146">1. Creare gli indirizzi IP pubblici hello e le configurazioni IP gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="ccd33-147">Richiesta due pubblica indirizzi toobe toohello allocato gateway IP che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ccd33-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="ccd33-148">Verrà inoltre definire subnet hello e le configurazioni IP necessari.</span><span class="sxs-lookup"><span data-stu-id="ccd33-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="ccd33-149">2. Creare il gateway VPN di hello con configurazione attivo / attivo</span><span class="sxs-lookup"><span data-stu-id="ccd33-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="ccd33-150">Creare il gateway di rete virtuale hello per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ccd33-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="ccd33-151">Si noti che sono presenti due voci GatewayIpConfig e hello EnableActiveActiveFeature flag è impostato.</span><span class="sxs-lookup"><span data-stu-id="ccd33-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="ccd33-152">Creazione di un gateway può richiedere un po' di tempo (45 minuti o più toocomplete).</span><span class="sxs-lookup"><span data-stu-id="ccd33-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="ccd33-153">3. Ottenere gli indirizzi IP pubblici di hello gateway e l'indirizzo IP Peer BGP di hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="ccd33-154">Una volta creato il gateway di hello, occorre tooobtain hello IP Peer BGP indirizzo hello Gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd33-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="ccd33-155">Questo indirizzo è hello tooconfigure necessari Gateway VPN di Azure come Peer BGP per i dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="ccd33-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="ccd33-156">Utilizzare hello seguente cmdlet tooshow hello due indirizzi IP pubblici allocati per il gateway VPN e indirizzi IP Peer BGP corrispondenti per ogni istanza del gateway:</span><span class="sxs-lookup"><span data-stu-id="ccd33-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="ccd33-157">ordine di Hello di indirizzi IP pubblici hello per le istanze di gateway hello e indirizzi di Peering BGP corrispondenti sono hello hello stesso.</span><span class="sxs-lookup"><span data-stu-id="ccd33-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="ccd33-158">In questo esempio, il gateway di hello macchina virtuale con indirizzo IP pubblico di 40.112.190.5 utilizzerà 10.12.255.4 come relativo indirizzo di Peering BGP e gateway hello con 138.91.156.129 utilizzerà 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="ccd33-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="ccd33-159">Queste informazioni sono necessarie quando si configura in locale i dispositivi VPN gateway attivo-attivo toohello la connessione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="ccd33-160">gateway Hello è illustrato nel diagramma hello seguito con tutti gli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="ccd33-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![active-active gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="ccd33-162">Una volta creato il gateway di hello, è possibile utilizzare questo gateway tooestablish attivo-attivo cross-premise o da rete connessione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="ccd33-163">Nelle sezioni che seguono Hello guiderà hello passaggi toocomplete hello esercizio.</span><span class="sxs-lookup"><span data-stu-id="ccd33-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="ccd33-164"><a name ="aacrossprem"></a>Parte 2: stabilire una connessione cross-premise active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="ccd33-165">tooestablish una connessione cross-premise, è necessario toocreate toorepresent un Gateway di rete locale del dispositivo VPN locale e il gateway VPN di Azure hello tooconnect connessione con il gateway di rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="ccd33-166">In questo esempio, i gateway VPN di Azure hello è in modalità attivo-attivo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="ccd33-167">Di conseguenza, anche se è presente un solo in locale il dispositivo VPN (gateway di rete locale) e risorse di una connessione, entrambe le istanze del gateway VPN di Azure consentirà di stabilire il tunnel VPN S2S con dispositivo locale hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="ccd33-168">Prima di procedere, verificare di avere completato la [Parte 1](#aagateway) di questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="ccd33-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="ccd33-169">Passaggio 1: creare e configurare il gateway di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="ccd33-170">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="ccd33-170">1. Declare your variables</span></span>
<span data-ttu-id="ccd33-171">Questo esercizio continuerà configurazione hello toobuild illustrato nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="ccd33-172">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="ccd33-173">Un paio di aspetti toonote relativi parametri di gateway di rete locale hello:</span><span class="sxs-lookup"><span data-stu-id="ccd33-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="ccd33-174">gateway di rete locale Hello può essere nella stessa hello o un percorso diverso e risorse gruppo come hello gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="ccd33-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="ccd33-175">In questo esempio viene loro in diversi gruppi di risorse, ma in hello nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd33-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="ccd33-176">Se è presente un solo dispositivo VPN di on-premise come illustrato in precedenza, connessione attivo-attivo hello può funzionare con o senza protocollo BGP.</span><span class="sxs-lookup"><span data-stu-id="ccd33-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="ccd33-177">Questo esempio viene utilizzato il protocollo BGP per la connessione tra più sedi hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="ccd33-178">Se BGP è abilitato, il prefisso di hello toodeclare è necessario per il gateway di rete locale hello è l'indirizzo host hello dell'indirizzo IP Peer BGP sul dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="ccd33-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="ccd33-179">In questo caso, è un prefisso /32 di "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="ccd33-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="ccd33-180">Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd33-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="ccd33-181">Se si sono hello stesso, è necessario toochange l'ASN VNet se il dispositivo VPN locale utilizza già hello toopeer ASN con altri router adiacenti BGP.</span><span class="sxs-lookup"><span data-stu-id="ccd33-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="ccd33-182">2. Creare il gateway di rete locale hello per Site5</span><span class="sxs-lookup"><span data-stu-id="ccd33-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="ccd33-183">Prima di continuare, verificare che si è ancora connesso tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="ccd33-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="ccd33-184">Creare il gruppo di risorse hello se non è ancora stato creato.</span><span class="sxs-lookup"><span data-stu-id="ccd33-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="ccd33-185">Passaggio 2: connettere il gateway di rete virtuale hello e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="ccd33-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="ccd33-186">1. Ottenere hello due gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="ccd33-187">2. Creare hello TestVNet1 tooSite5 connessione</span><span class="sxs-lookup"><span data-stu-id="ccd33-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="ccd33-188">In questo passaggio si creerà hello connessione da TestVNet1 tooSite5_1 con "EnableBGP" impostare troppo$ True.</span><span class="sxs-lookup"><span data-stu-id="ccd33-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="ccd33-189">3. Parametri di VPN e BGP per il dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="ccd33-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="ccd33-190">esempio Hello seguente elenca i parametri di hello che immetterà hello sezione di configurazione BGP sul dispositivo VPN locale per questo esercizio:</span><span class="sxs-lookup"><span data-stu-id="ccd33-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="ccd33-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="ccd33-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="ccd33-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="ccd33-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="ccd33-193">I prefissi tooannounce:, ad esempio, 10.51.0.0/16 e 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ccd33-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="ccd33-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="ccd33-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="ccd33-195">Azure rete virtuale BGP IP 1: 10.12.255.4 per too40.112.190.5 tunnel</span><span class="sxs-lookup"><span data-stu-id="ccd33-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="ccd33-196">Azure rete virtuale BGP IP 2: 10.12.255.5 per too138.91.156.129 tunnel</span><span class="sxs-lookup"><span data-stu-id="ccd33-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="ccd33-197">Le route statiche: destinazione 10.12.255.4/32, hop successivo hello VPN tunnel interfaccia too40.112.190.5 destinazione 10.12.255.5/32, too138.91.156.129 interfaccia tunnel di hop successivo hello VPN</span><span class="sxs-lookup"><span data-stu-id="ccd33-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="ccd33-198">eBGP Multihop: verificare l'opzione "multihop" hello per eBGP è abilitato nel dispositivo, se necessario</span><span class="sxs-lookup"><span data-stu-id="ccd33-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="ccd33-199">Hello devono connettersi dopo qualche minuto e sessione di peering BGP hello inizierà dopo aver stabilito la connessione IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="ccd33-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="ccd33-200">In questo esempio finora è configurato un solo dispositivo VPN locale, risultante in diagramma hello illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="ccd33-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="ccd33-202">Passaggio 3: connettere due sedi dispositivi toohello attivo-attivo VPN gateway VPN</span><span class="sxs-lookup"><span data-stu-id="ccd33-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="ccd33-203">Se sono presenti due dispositivi VPN hello stesso locale rete, è possibile ottenere ridondanza duale connessione hello Azure dispositivo gateway VPN toohello secondo VPN.</span><span class="sxs-lookup"><span data-stu-id="ccd33-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="ccd33-204">1. Creare il gateway di rete locale secondo hello per Site5</span><span class="sxs-lookup"><span data-stu-id="ccd33-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="ccd33-205">Si noti che l'indirizzo peer BGP per gateway di rete locale hello secondo indirizzo IP del gateway hello e prefisso di indirizzo non devono sovrapporsi a gateway di rete locale per hello precedente hello stessa rete in locale.</span><span class="sxs-lookup"><span data-stu-id="ccd33-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="ccd33-206">2. Connettersi al gateway di rete virtuale hello e gateway di rete locale secondo hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="ccd33-207">Il nome di connessione hello TestVNet1 tooSite5_2 con "EnableBGP" impostare troppo$ True</span><span class="sxs-lookup"><span data-stu-id="ccd33-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="ccd33-208">3. Parametri di VPN e BGP per il secondo dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="ccd33-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="ccd33-209">Analogamente, di sotto di elenchi di parametri di hello immetterà dispositivo VPN secondo hello:</span><span class="sxs-lookup"><span data-stu-id="ccd33-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="ccd33-210">Una volta stabiliti i connessione hello (tunnel), si disporrà di duali dispositivi VPN ridondanti e tunnel che connette la rete locale e Azure:</span><span class="sxs-lookup"><span data-stu-id="ccd33-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="ccd33-212"><a name ="aav2v"></a>Parte 3: stabilire una connessione da rete virtuale a rete virtuale active-active</span><span class="sxs-lookup"><span data-stu-id="ccd33-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="ccd33-213">In questa sezione viene creata una connessione da rete virtuale a rete virtuale active-active con BGP.</span><span class="sxs-lookup"><span data-stu-id="ccd33-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="ccd33-214">istruzioni di Hello seguenti continuano nei passaggi precedenti di hello elencati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ccd33-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="ccd33-215">È necessario completare [parte 1](#aagateway) toocreate e configurare TestVNet1 e hello Gateway VPN con il protocollo BGP.</span><span class="sxs-lookup"><span data-stu-id="ccd33-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="ccd33-216">Passaggio 1: creare TestVNet2 e hello gateway VPN</span><span class="sxs-lookup"><span data-stu-id="ccd33-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="ccd33-217">È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet2, non si sovrapponga ad altri intervalli di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ccd33-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="ccd33-218">In questo esempio, le reti virtuali hello appartengono toohello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="ccd33-219">È possibile impostare le connessioni di rete virtuale a tra diverse sottoscrizioni. consultare troppo[configurare una connessione di rete virtuale a](vpn-gateway-vnet-vnet-rm-ps.md) toolearn ulteriori informazioni, vedere.</span><span class="sxs-lookup"><span data-stu-id="ccd33-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="ccd33-220">Assicurarsi di aggiungere hello "-EnableBgp $True" quando la creazione di hello tooenable connessioni BGP.</span><span class="sxs-lookup"><span data-stu-id="ccd33-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="ccd33-221">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="ccd33-221">1. Declare your variables</span></span>
<span data-ttu-id="ccd33-222">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="ccd33-223">2. Creare il nuovo gruppo di risorse hello TestVNet2</span><span class="sxs-lookup"><span data-stu-id="ccd33-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="ccd33-224">3. Creare i gateway VPN di hello attivo-attivo per TestVNet2</span><span class="sxs-lookup"><span data-stu-id="ccd33-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="ccd33-225">Richiesta due pubblica indirizzi toobe toohello allocato gateway IP che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="ccd33-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="ccd33-226">Verrà inoltre definire subnet hello e le configurazioni IP necessari.</span><span class="sxs-lookup"><span data-stu-id="ccd33-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="ccd33-227">Creare i gateway VPN hello con hello come numero e hello flag "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="ccd33-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="ccd33-228">Si noti che è necessario eseguire l'override di predefinito hello ASN nel gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="ccd33-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="ccd33-229">Hello ASN per hello connessi a reti virtuali devono essere diversi tooenable BGP e il routing di transito.</span><span class="sxs-lookup"><span data-stu-id="ccd33-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="ccd33-230">Passaggio 2: connettere i gateway TestVNet1 e TestVNet2 hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="ccd33-231">In questo esempio, entrambi i gateway sono in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="ccd33-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="ccd33-232">È possibile completare questo passaggio in hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccd33-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="ccd33-233">1. Ottenere entrambi i gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-233">1. Get both gateways</span></span>
<span data-ttu-id="ccd33-234">Assicurarsi di accedere e connettersi tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="ccd33-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="ccd33-235">2. Creare entrambe le connessioni</span><span class="sxs-lookup"><span data-stu-id="ccd33-235">2. Create both connections</span></span>
<span data-ttu-id="ccd33-236">In questo passaggio si creerà connessione hello da TestVNet1 tooTestVNet2 e connessione hello da TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="ccd33-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="ccd33-237">Impossibile verificare tooenable BGP per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="ccd33-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="ccd33-238">Dopo aver completato questi passaggi, stabilirà la connessione hello in pochi minuti e sessione di peering BGP hello sarà backup dopo aver eseguito la connessione di rete virtuale a hello con doppia ridondanza:</span><span class="sxs-lookup"><span data-stu-id="ccd33-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="ccd33-240"><a name ="aaupdate"></a>Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby</span><span class="sxs-lookup"><span data-stu-id="ccd33-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="ccd33-241">ultima sezione Hello viene descritto come configurare un gateway VPN di Azure esistente dalla modalità tooactive attivo attivo-standby o viceversa.</span><span class="sxs-lookup"><span data-stu-id="ccd33-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd33-242">Questa sezione include hello passaggi tooresize uno SKU legacy (SKU precedente) di un gateway VPN già creato da tooHighPerformance Standard.</span><span class="sxs-lookup"><span data-stu-id="ccd33-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="ccd33-243">Questi passaggi non aggiornare un vecchio tooone SKU legacy di hello SKU di nuovo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="ccd33-244">Configurare un gateway tooactive attivo attivo-standby gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="ccd33-245">1. Parametri del gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-245">1. Gateway parameters</span></span>
<span data-ttu-id="ccd33-246">Hello di esempio seguente converte un gateway attivo-standby in un gateway attivo-attivo.</span><span class="sxs-lookup"><span data-stu-id="ccd33-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="ccd33-247">È necessario toocreate un altro indirizzo IP pubblico, quindi aggiungere una seconda configurazione IP del Gateway.</span><span class="sxs-lookup"><span data-stu-id="ccd33-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="ccd33-248">Di seguito viene illustrato hello utilizzati i parametri:</span><span class="sxs-lookup"><span data-stu-id="ccd33-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="ccd33-249">2. Creare l'indirizzo IP pubblico hello, quindi aggiungere una configurazione IP del gateway secondo hello</span><span class="sxs-lookup"><span data-stu-id="ccd33-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="ccd33-250">3. Abilitare i gateway di hello modalità e l'aggiornamento attivo-attivo</span><span class="sxs-lookup"><span data-stu-id="ccd33-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="ccd33-251">È necessario impostare l'oggetto gateway hello in aggiornamento effettivo hello tootrigger di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccd33-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="ccd33-252">Hello SKU di gateway di rete virtuale hello deve essere modificato tooHighPerformance (ridimensionata) quando è stato creato in precedenza come Standard.</span><span class="sxs-lookup"><span data-stu-id="ccd33-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="ccd33-253">Questo aggiornamento può richiedere 30 minuti too45.</span><span class="sxs-lookup"><span data-stu-id="ccd33-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="ccd33-254">Configurare un gateway tooactive standby gateway attivo-attivo</span><span class="sxs-lookup"><span data-stu-id="ccd33-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="ccd33-255">1. Parametri del gateway</span><span class="sxs-lookup"><span data-stu-id="ccd33-255">1. Gateway parameters</span></span>
<span data-ttu-id="ccd33-256">Utilizzare hello stesso parametri indicati in precedenza, ottenere il nome di hello della configurazione IP hello desiderata tooremove.</span><span class="sxs-lookup"><span data-stu-id="ccd33-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="ccd33-257">2. Rimuovere una configurazione IP del gateway hello e disabilitare la modalità di hello attivo-attivo</span><span class="sxs-lookup"><span data-stu-id="ccd33-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="ccd33-258">Analogamente, è necessario impostare l'oggetto gateway hello in aggiornamento effettivo hello tootrigger di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccd33-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="ccd33-259">Questo aggiornamento può richiedere fino too30 troppo 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="ccd33-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd33-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ccd33-260">Next steps</span></span>
<span data-ttu-id="ccd33-261">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="ccd33-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="ccd33-262">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="ccd33-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
