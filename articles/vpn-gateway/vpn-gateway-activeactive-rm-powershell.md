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
ms.openlocfilehash: a9f71b566ffdb163f95634835f64589a700d712f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="c4687-103">Configurare connessioni di rete privata virtuale da sito a sito active-active con gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="c4687-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="c4687-104">Questo articolo illustra i passaggi per creare connessioni cross-permise active-active e da rete virtuale a rete virtuale usando il modello di distribuzione Resource Manager e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4687-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="c4687-105">Informazioni sulle connessioni cross-premise a disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="c4687-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="c4687-106">Per ottenere una disponibilità elevata per la connettività cross-premise e da rete virtuale a rete virtuale, occorre distribuire più gateway VPN e stabilire più connessioni parallele tra le reti e Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="c4687-107">Per una panoramica delle opzioni di connettività e della topologia, vedere [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) (Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata).</span><span class="sxs-lookup"><span data-stu-id="c4687-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="c4687-108">In questo articolo vengono fornite le istruzioni per configurare una connessione VPN cross-premise active-active tra due reti virtuali:</span><span class="sxs-lookup"><span data-stu-id="c4687-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="c4687-109">Parte 1: creare e configurare il gateway VPN di Azure in modalità active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="c4687-110">Parte 2: stabilire connessioni cross-premise active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="c4687-111">Parte 3: stabilire connessioni da rete virtuale a rete virtuale active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="c4687-112">Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby</span><span class="sxs-lookup"><span data-stu-id="c4687-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="c4687-113">È possibile combinare questi elementi per creare una topologia di rete altamente scalabile e più complessa adatta alle proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="c4687-113">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c4687-114">Notare che la modalità active-active usa solo gli SKU seguenti:</span><span class="sxs-lookup"><span data-stu-id="c4687-114">Please note that the active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="c4687-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="c4687-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="c4687-116">HighPerformance (per SKU precedenti legacy)</span><span class="sxs-lookup"><span data-stu-id="c4687-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="c4687-117"><a name ="aagateway"></a>Parte 1: creare e configurare gateway VPN active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="c4687-118">Con i seguenti passaggi si configurerà il gateway VPN di Azure in modalità active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-118">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="c4687-119">Le differenze principali tra i gateway active-active e active-standby sono:</span><span class="sxs-lookup"><span data-stu-id="c4687-119">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="c4687-120">È necessario creare due configurazioni IP del gateway con due indirizzi IP pubblici</span><span class="sxs-lookup"><span data-stu-id="c4687-120">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="c4687-121">È necessario impostare il contrassegno EnableActiveActiveFeature</span><span class="sxs-lookup"><span data-stu-id="c4687-121">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="c4687-122">Lo SKU del gateway deve essere VpnGw1, VpnGw2, VpnGw3 o HighPerformance (SKU legacy).</span><span class="sxs-lookup"><span data-stu-id="c4687-122">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="c4687-123">Le altre proprietà corrispondono a quelle dei gateway non active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-123">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="c4687-124">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="c4687-124">Before you begin</span></span>
* <span data-ttu-id="c4687-125">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="c4687-126">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4687-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c4687-127">È necessario installare i cmdlet di PowerShell per Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-127">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="c4687-128">Per altre informazioni sull'installazione di cmdlet PowerShell, vedere [Overview of Azure PowerShell](/powershell/azure/overview) (Panoramica di Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="c4687-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="c4687-129">Passaggio 1: Creare e configurare VNet1</span><span class="sxs-lookup"><span data-stu-id="c4687-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4687-130">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="c4687-130">1. Declare your variables</span></span>
<span data-ttu-id="c4687-131">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="c4687-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="c4687-132">Nell'esempio seguente vengono dichiarate le variabili usando i valori per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="c4687-132">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="c4687-133">Assicurarsi di sostituire i valori con quelli reali durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="c4687-133">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="c4687-134">Queste variabili possono essere usate se si esegue la procedura per acquisire familiarità con questo tipo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="c4687-134">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="c4687-135">Modificare le variabili, quindi copiarle e incollarle nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4687-135">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="c4687-136">2. Connettersi alla sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c4687-136">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="c4687-137">Verificare di passare alla modalità PowerShell per usare i cmdlet di Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="c4687-137">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="c4687-138">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="c4687-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="c4687-139">Aprire la console di PowerShell e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="c4687-139">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="c4687-140">Per connettersi, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4687-140">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="c4687-141">3. Creare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="c4687-141">3. Create TestVNet1</span></span>
<span data-ttu-id="c4687-142">Nell'esempio seguente vengono create una rete virtuale denominata TestVNet1 e tre subnet, denominate GatewaySubnet, FrontEnd e Backend.</span><span class="sxs-lookup"><span data-stu-id="c4687-142">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="c4687-143">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="c4687-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="c4687-144">Se si assegnano altri nomi, la creazione del gateway avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c4687-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="c4687-145">Passaggio 2: creare il gateway VPN per TestVNet1 con la modalità active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-145">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="c4687-146">1. Creare gli indirizzi IP pubblici e le configurazioni IP del gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-146">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="c4687-147">Richiedere due indirizzi IP pubblici da allocare al gateway che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c4687-147">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="c4687-148">Si definiranno anche le configurazioni subnet e IP necessarie.</span><span class="sxs-lookup"><span data-stu-id="c4687-148">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="c4687-149">2. Creare il gateway VPN per la configurazione active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-149">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="c4687-150">Creare il gateway di rete virtuale per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c4687-150">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="c4687-151">Notare che sono presenti due voci GatewayIpConfig e che viene impostato il contrassegno EnableActiveActiveFeature.</span><span class="sxs-lookup"><span data-stu-id="c4687-151">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="c4687-152">La creazione di un gateway può richiedere anche oltre 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="c4687-152">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="c4687-153">3. Ottenere gli indirizzi IP pubblici del gateway e l'indirizzo IP di peering BGP</span><span class="sxs-lookup"><span data-stu-id="c4687-153">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="c4687-154">Una volta creato il gateway, sarà necessario ottenere l'indirizzo IP del peer BGP nel gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-154">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="c4687-155">Questo indirizzo è necessario per configurare il gateway VPN di Azure come peer BGP per i dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="c4687-155">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="c4687-156">Usare i cmdlet seguenti per visualizzare i due indirizzi IP pubblici allocati per il gateway VPN e gli indirizzi IP di peering BGP corrispondenti per ogni istanza del gateway:</span><span class="sxs-lookup"><span data-stu-id="c4687-156">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

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

<span data-ttu-id="c4687-157">L'ordine degli indirizzi IP pubblici per le istanze del gateway e i relativi indirizzi di peering BGP corrispondono.</span><span class="sxs-lookup"><span data-stu-id="c4687-157">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="c4687-158">In questo esempio, la VM del gateway con l'indirizzo IP pubblico 40.112.190.5 userà 10.12.255.4 come indirizzo di peering BGP, mentre il gateway con 138.91.156.129 userà 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="c4687-158">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="c4687-159">Queste informazioni sono necessarie quando si configurano dispositivi VPN locali che si connettono al gateway active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-159">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="c4687-160">Il gateway è mostrato nel diagramma riportato di seguito con tutti gli indirizzi:</span><span class="sxs-lookup"><span data-stu-id="c4687-160">The gateway is shown in the diagram below with all addresses:</span></span>

![active-active gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="c4687-162">Una volta creato il gateway, è possibile usarlo per stabilire una connessione da rete virtuale a rete virtuale o cross-premise active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-162">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="c4687-163">Le sezioni seguenti illustrano i passaggi per completare l'esercizio.</span><span class="sxs-lookup"><span data-stu-id="c4687-163">The following sections will walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="c4687-164"><a name ="aacrossprem"></a>Parte 2: stabilire una connessione cross-premise active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="c4687-165">Per stabilire una connessione cross-premise, è necessario creare un gateway di rete locale per rappresentare il dispositivo VPN locale e una connessione per connettere il gateway VPN di Azure al gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="c4687-165">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="c4687-166">In questo esempio, il gateway VPN di Azure è in modalità active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-166">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="c4687-167">Di conseguenza, anche se sono presenti un solo dispositivo VPN locale (gateway di rete locale) e una risorsa di connessione, entrambe le istanze del gateway VPN di Azure stabiliranno tunnel VPN S2S con il dispositivo locale.</span><span class="sxs-lookup"><span data-stu-id="c4687-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="c4687-168">Prima di procedere, verificare di avere completato la [Parte 1](#aagateway) di questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="c4687-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="c4687-169">Passaggio 1: Creare e configurare il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="c4687-169">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4687-170">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="c4687-170">1. Declare your variables</span></span>
<span data-ttu-id="c4687-171">Questo esercizio continuerà a creare la configurazione illustrata nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="c4687-171">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="c4687-172">Sostituire i valori con quelli desiderati per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="c4687-172">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="c4687-173">È necessario tenere presenti due aspetti relativi ai parametri del gateway di rete:</span><span class="sxs-lookup"><span data-stu-id="c4687-173">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="c4687-174">Il gateway di rete locale può essere nella stessa località e nello stesso gruppo di risorse del gateway VPN oppure in altri.</span><span class="sxs-lookup"><span data-stu-id="c4687-174">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="c4687-175">In questo esempio vengono mostrati in gruppi di risorse diversi ma nello stesso percorso di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-175">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="c4687-176">Se è presente un solo dispositivo VPN locale come illustrato sopra, la connessione di tipo active-active può funzionare con o senza protocollo BGP.</span><span class="sxs-lookup"><span data-stu-id="c4687-176">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="c4687-177">In questo esempio viene usato il protocollo BGP per la connessione cross-premise.</span><span class="sxs-lookup"><span data-stu-id="c4687-177">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="c4687-178">Se è abilitato BGP, il prefisso che è necessario dichiarare per il gateway di rete locale è l'indirizzo host dell'indirizzo IP di peering BGP nel dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c4687-178">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="c4687-179">In questo caso, è un prefisso /32 di "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="c4687-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="c4687-180">Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="c4687-181">Se sono gli stessi, è necessario modificare l'ASN della rete virtuale se il dispositivo VPN locale usa già l'ASN per il peering con altri vicini BGP.</span><span class="sxs-lookup"><span data-stu-id="c4687-181">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="c4687-182">2. Creare il gateway di rete locale per Site5</span><span class="sxs-lookup"><span data-stu-id="c4687-182">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="c4687-183">Prima di proseguire, verificare di essere ancora connessi alla sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="c4687-183">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="c4687-184">Creare il gruppo di risorse se non è ancora stato creato.</span><span class="sxs-lookup"><span data-stu-id="c4687-184">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="c4687-185">Passaggio 2: Connettere il gateway di rete virtuale e il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="c4687-185">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="c4687-186">1. Ottenere i due gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-186">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="c4687-187">2. Creare la connessione da TestVNet1 a Site5</span><span class="sxs-lookup"><span data-stu-id="c4687-187">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="c4687-188">In questo passaggio si creerà la connessione da TestVNet1 a Site5_1 con "EnableBGP" impostato su $True.</span><span class="sxs-lookup"><span data-stu-id="c4687-188">In this step, you will create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="c4687-189">3. Parametri di VPN e BGP per il dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="c4687-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="c4687-190">L'esempio seguente elenca i parametri che si immetteranno nella sezione della configurazione BGP nel dispositivo VPN locale per questo esercizio:</span><span class="sxs-lookup"><span data-stu-id="c4687-190">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="c4687-191">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="c4687-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="c4687-192">Site5 BGP IP         : 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="c4687-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="c4687-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c4687-193">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="c4687-194">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="c4687-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="c4687-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span><span class="sxs-lookup"><span data-stu-id="c4687-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5</span></span>
    - <span data-ttu-id="c4687-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="c4687-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129</span></span>
    - <span data-ttu-id="c4687-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="c4687-197">Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5                        Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129</span></span>
    - <span data-ttu-id="c4687-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span><span class="sxs-lookup"><span data-stu-id="c4687-198">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="c4687-199">La connessione verrà stabilita in pochi minuti e la sessione di peering BGP verrà avviata una volta stabilità la connessione IPSec.</span><span class="sxs-lookup"><span data-stu-id="c4687-199">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="c4687-200">In questo esempio finora è stato configurato un solo dispositivo VPN locale; il risultato è nel diagramma di seguito:</span><span class="sxs-lookup"><span data-stu-id="c4687-200">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="c4687-202">Passaggio 3: connettere due dispositivi VPN locali al gateway VPN active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-202">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="c4687-203">Se si dispone di due dispositivi VPN nella stessa rete locale, è possibile ottenere ridondanza doppia connettendo il gateway VPN di Azure al secondo dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="c4687-203">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="c4687-204">1. Creare il secondo gateway di rete locale per Site5</span><span class="sxs-lookup"><span data-stu-id="c4687-204">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="c4687-205">Notare che l'indirizzo IP del gateway, il prefisso dell'indirizzo e l'indirizzo di peering BGP per il secondo gateway di rete locale non devono sovrapporsi al gateway di rete locale precedente per la stessa rete locale.</span><span class="sxs-lookup"><span data-stu-id="c4687-205">Note that the gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="c4687-206">2. Connettere il gateway di rete virtuale e il secondo gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="c4687-206">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="c4687-207">Creare la connessione da TestVNet1 a Site5_2 con "EnableBGP" impostato su $True.</span><span class="sxs-lookup"><span data-stu-id="c4687-207">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="c4687-208">3. Parametri di VPN e BGP per il secondo dispositivo VPN locale</span><span class="sxs-lookup"><span data-stu-id="c4687-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="c4687-209">In modo analogo, di seguito sono elencati i parametri che verranno immessi nel secondo dispositivo VPN:</span><span class="sxs-lookup"><span data-stu-id="c4687-209">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="c4687-210">Una volta che viene stabilita la connessione (tunnel), si disporrà di dispositivi VPN a doppia ridondanza e di tunnel che connettono la rete locale e Azure:</span><span class="sxs-lookup"><span data-stu-id="c4687-210">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="c4687-212"><a name ="aav2v"></a>Parte 3: stabilire una connessione da rete virtuale a rete virtuale active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="c4687-213">In questa sezione viene creata una connessione da rete virtuale a rete virtuale active-active con BGP.</span><span class="sxs-lookup"><span data-stu-id="c4687-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="c4687-214">Le istruzioni seguenti sono la prosecuzione dei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="c4687-214">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="c4687-215">È necessario completare la [Parte 1](#aagateway) per creare e configurare TestVNet1 e il gateway VPN con BGP.</span><span class="sxs-lookup"><span data-stu-id="c4687-215">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="c4687-216">Passaggio 1: Creare TestVNet2 e il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="c4687-216">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="c4687-217">È importante verificare che lo spazio di indirizzi IP della nuova rete virtuale, TestVNet2, non si sovrapponga ad altri di intervalli di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c4687-217">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="c4687-218">In questo esempio le reti virtuali appartengono alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c4687-218">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="c4687-219">È possibile configurare connessioni da rete virtuale a rete virtuale tra sottoscrizioni diverse. Per altri dettagli, vedere [Configurare una connessione da rete virtuale a rete virtuale](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c4687-219">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="c4687-220">Assicurarsi di aggiungere "-EnableBgp $True" quando si creano le connessioni per abilitare BGP.</span><span class="sxs-lookup"><span data-stu-id="c4687-220">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="c4687-221">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="c4687-221">1. Declare your variables</span></span>
<span data-ttu-id="c4687-222">Sostituire i valori con quelli desiderati per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="c4687-222">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="c4687-223">2. Creare TestVNet2 nel nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c4687-223">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="c4687-224">3. Creare il gateway VPN active-active per TestVNet2</span><span class="sxs-lookup"><span data-stu-id="c4687-224">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="c4687-225">Richiedere due indirizzi IP pubblici da allocare al gateway che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="c4687-225">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="c4687-226">Si definiranno anche le configurazioni subnet e IP necessarie.</span><span class="sxs-lookup"><span data-stu-id="c4687-226">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="c4687-227">Creare il gateway VPN con il numero AS e il contrassegno "EnableActiveActiveFeature".</span><span class="sxs-lookup"><span data-stu-id="c4687-227">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="c4687-228">Si noti che è necessario eseguire l'override dell'ASN predefinito nei gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4687-228">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="c4687-229">Gli ASN per le reti virtuali connesse devono essere diversi per abilitare BGP e il routing di transito.</span><span class="sxs-lookup"><span data-stu-id="c4687-229">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="c4687-230">Passaggio 2: Connettere i gateway TestVNet1 e TestVNet2</span><span class="sxs-lookup"><span data-stu-id="c4687-230">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="c4687-231">In questo esempio entrambi i gateway sono nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c4687-231">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="c4687-232">È possibile completare questo passaggio nella stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c4687-232">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="c4687-233">1. Ottenere entrambi i gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-233">1. Get both gateways</span></span>
<span data-ttu-id="c4687-234">Eseguire l'accesso e connettersi alla Sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="c4687-234">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="c4687-235">2. Creare entrambe le connessioni</span><span class="sxs-lookup"><span data-stu-id="c4687-235">2. Create both connections</span></span>
<span data-ttu-id="c4687-236">In questo passaggio si creerà la connessione da TestVNet1 a TestVNet2 e la connessione da TestVNet2 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="c4687-236">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="c4687-237">Assicurarsi di abilitare BGP per ENTRAMBE le connessioni.</span><span class="sxs-lookup"><span data-stu-id="c4687-237">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="c4687-238">Dopo avere completato questi passaggi, la connessione verrà stabilita in pochi minuti e la sessione di peering BGP sarà attiva una volta completata la connessione da rete virtuale e rete virtuale con doppia ridondanza:</span><span class="sxs-lookup"><span data-stu-id="c4687-238">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="c4687-240"><a name ="aaupdate"></a>Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby</span><span class="sxs-lookup"><span data-stu-id="c4687-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="c4687-241">Nell'ultima sezione verrà descritto come configurare un gateway VPN di Azure esistente dalla modalità active-standby alla modalità active-active o viceversa.</span><span class="sxs-lookup"><span data-stu-id="c4687-241">The last section will describe how you can configure an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="c4687-242">Questa sezione include i passaggi per ridimensionare uno SKU legacy (SKU precedente) di un gateway VPN già creato da Standard a HighPerformance.</span><span class="sxs-lookup"><span data-stu-id="c4687-242">This section includes the steps to resize a legacy SKU (old SKU) of an already created VPN gateway from Standard to HighPerformance.</span></span> <span data-ttu-id="c4687-243">Questi passaggi non consentono di aggiornare uno SKU legacy precedente a uno dei nuovi SKU.</span><span class="sxs-lookup"><span data-stu-id="c4687-243">These steps do not upgrade an old legacy SKU to one of the new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-to-active-active-gateway"></a><span data-ttu-id="c4687-244">Configurare un gateway da active-standby a active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-244">Configure an active-standby gateway to active-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="c4687-245">1. Parametri del gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-245">1. Gateway parameters</span></span>
<span data-ttu-id="c4687-246">Nell'esempio seguente un gateway active-standby viene convertito in gateway active-active.</span><span class="sxs-lookup"><span data-stu-id="c4687-246">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="c4687-247">È necessario creare un altro indirizzo IP pubblico, quindi aggiungere una seconda configurazione IP del gateway.</span><span class="sxs-lookup"><span data-stu-id="c4687-247">You need to create another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="c4687-248">Di seguito vengono illustrati i parametri usati:</span><span class="sxs-lookup"><span data-stu-id="c4687-248">Below shows the parameters used:</span></span>

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

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="c4687-249">2. Creare un altro indirizzo IP pubblico, quindi aggiungere una seconda configurazione IP del gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-249">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="c4687-250">3. Abilitare la modalità active-active e aggiornare il gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-250">3. Enable active-active mode and update the gateway</span></span>
<span data-ttu-id="c4687-251">È necessario impostare l'oggetto del gateway in PowerShell per attivare l'aggiornamento effettivo.</span><span class="sxs-lookup"><span data-stu-id="c4687-251">You must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="c4687-252">Anche lo SKU del gateway della rete virtuale deve essere modificato (ridimensionato) in HighPerformance, perché è stato creato in precedenza come Standard.</span><span class="sxs-lookup"><span data-stu-id="c4687-252">The SKU of the virtual network gateway must also be changed (resized) to HighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="c4687-253">Questo aggiornamento può richiedere da 30 a 45 minuti.</span><span class="sxs-lookup"><span data-stu-id="c4687-253">This update can take 30 to 45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-to-active-standby-gateway"></a><span data-ttu-id="c4687-254">Configurare un gateway da active-active a active-standby</span><span class="sxs-lookup"><span data-stu-id="c4687-254">Configure an active-active gateway to active-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="c4687-255">1. Parametri del gateway</span><span class="sxs-lookup"><span data-stu-id="c4687-255">1. Gateway parameters</span></span>
<span data-ttu-id="c4687-256">Usare gli stessi parametri riportati sopra e ottenere il nome della configurazione IP che si desidera rimuovere.</span><span class="sxs-lookup"><span data-stu-id="c4687-256">Use the same parameters as above, get the name of the IP configuration you want to remove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="c4687-257">2. Rimuovere la configurazione IP del gateway e disabilitare la modalità active-active</span><span class="sxs-lookup"><span data-stu-id="c4687-257">2. Remove the gateway IP configuration and disable the active-active mode</span></span>
<span data-ttu-id="c4687-258">In modo analogo, impostare l'oggetto del gateway in PowerShell per attivare l'aggiornamento effettivo.</span><span class="sxs-lookup"><span data-stu-id="c4687-258">Similarly, you must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="c4687-259">Questo aggiornamento può richiedere fino a 30-45 minuti.</span><span class="sxs-lookup"><span data-stu-id="c4687-259">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4687-260">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4687-260">Next steps</span></span>
<span data-ttu-id="c4687-261">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="c4687-261">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="c4687-262">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="c4687-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>