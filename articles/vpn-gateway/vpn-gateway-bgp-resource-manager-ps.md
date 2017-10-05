---
title: Configurare BGP sui gateway VPN di Azure - Resource Manager - PowerShell | Microsoft Docs
description: In questo articolo viene illustrata la configurazione di BGP con i gateway VPN di Azure tramite Azure Resource Manager e PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: b00a3fe7ba4b12c2e9c486188c292cd6fafb60a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="73afe-103">Come configurare BGP sui gateway VPN di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="73afe-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="73afe-104">Questo articolo illustra i passaggi per abilitare BGP in una connessione VPN da sito a sito (S2S) cross-premise e in una connessione da rete virtuale a rete virtuale usando il modello di distribuzione Resource Manager e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73afe-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="73afe-105">Informazioni su BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-105">About BGP</span></span>
<span data-ttu-id="73afe-106">BGP è il protocollo di routing standard comunemente usato in Internet per lo scambio di informazioni di routing e raggiungibilità tra due o più reti.</span><span class="sxs-lookup"><span data-stu-id="73afe-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="73afe-107">BGP consente ai gateway VPN di Azure e ai dispositivi VPN locali, detti peer BGP o router adiacenti, lo scambio di "route" che indicano a entrambi i gateway la disponibilità e la raggiungibilità di tali prefissi per il passaggio attraverso i gateway o i router coinvolti.</span><span class="sxs-lookup"><span data-stu-id="73afe-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="73afe-108">BGP può anche abilitare il routing di transito tra più reti propagando a tutti gli altri peer BGP le route che un gateway BGP apprende da un peer BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="73afe-109">Vedere [Panoramica di BGP con i gateway VPN di Azure](vpn-gateway-bgp-overview.md) per altre informazioni sui vantaggi di BGP e per conoscere i requisiti tecnici e le considerazioni sull'uso di BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="73afe-110">Introduzione a BGP nei gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="73afe-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="73afe-111">L'articolo illustra la procedura per eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="73afe-111">This article walks you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="73afe-112">Parte 1: Abilitare BGP nel gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="73afe-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="73afe-113">Parte 2: Stabilire una connessione cross-premise con BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="73afe-114">Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="73afe-115">Ogni parte delle istruzioni costituisce un blocco predefinito di base per abilitare BGP nella connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="73afe-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="73afe-116">Se si completano tutte e tre le parti, si crea la topologia illustrata nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="73afe-116">If you complete all three parts, you build the topology as shown in the following diagram:</span></span>

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="73afe-118">È possibile combinare le parti per creare una rete di transito a più hop più complessa per soddisfare le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="73afe-118">You can combine parts together to build a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="73afe-119"><a name ="enablebgp"></a>Parte 1: Configurare BGP nel gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="73afe-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="73afe-120">La procedura di configurazione configura i parametri BGP nel gateway VPN di Azure come illustrato nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="73afe-120">The configuration steps set up the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="73afe-122">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="73afe-122">Before you begin</span></span>
* <span data-ttu-id="73afe-123">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="73afe-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="73afe-124">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="73afe-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="73afe-125">Installare i cmdlet di PowerShell per Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="73afe-125">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="73afe-126">Per altre informazioni sull'installazione dei cmdlet di PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="73afe-126">For more information about installing the PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="73afe-127">Passaggio 1: Creare e configurare VNet1</span><span class="sxs-lookup"><span data-stu-id="73afe-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="73afe-128">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="73afe-128">1. Declare your variables</span></span>
<span data-ttu-id="73afe-129">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="73afe-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="73afe-130">L'esempio seguente dichiara le variabili usando i valori per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="73afe-130">The following example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="73afe-131">Assicurarsi di sostituire i valori con quelli reali durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="73afe-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="73afe-132">Queste variabili possono essere usate se si esegue la procedura per acquisire familiarità con questo tipo di configurazione.</span><span class="sxs-lookup"><span data-stu-id="73afe-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="73afe-133">Modificare le variabili, quindi copiarle e incollarle nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73afe-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
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
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="73afe-134">2. Connettersi alla sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="73afe-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="73afe-135">Per usare i cmdlet di Resource Manager assicurarsi di passare alla modalità PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73afe-135">To use the Resource Manager cmdlets, Make sure you switch to PowerShell mode.</span></span> <span data-ttu-id="73afe-136">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="73afe-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="73afe-137">Aprire la console di PowerShell e connettersi al proprio account.</span><span class="sxs-lookup"><span data-stu-id="73afe-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="73afe-138">Per connettersi, usare l'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="73afe-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="73afe-139">3. Creare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="73afe-139">3. Create TestVNet1</span></span>
<span data-ttu-id="73afe-140">L'esempio seguente mostra come creare una rete virtuale denominata TestVNet1 e tre subnet, denominate rispettivamente GatewaySubnet, FrontEnd e Backend.</span><span class="sxs-lookup"><span data-stu-id="73afe-140">The following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="73afe-141">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="73afe-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="73afe-142">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="73afe-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="73afe-143">Passaggio 2: Creare il gateway VPN per TestVNet1 con i parametri BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="73afe-144">1. Creare le configurazioni IP e subnet</span><span class="sxs-lookup"><span data-stu-id="73afe-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="73afe-145">Richiedere un indirizzo IP pubblico da allocare per il gateway che verrà creato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="73afe-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="73afe-146">Verranno create anche le configurazioni necessarie per subnet e IP.</span><span class="sxs-lookup"><span data-stu-id="73afe-146">You'll also define the required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="73afe-147">2. Creare il gateway VPN con il numero AS</span><span class="sxs-lookup"><span data-stu-id="73afe-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="73afe-148">Creare il gateway di rete virtuale per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="73afe-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="73afe-149">Per impostare il parametro ASN (AS Number, numero AS) per TestVNet1BGP, sono necessari un gateway VPN basato su route e il parametro aggiuntivo, -Asn.</span><span class="sxs-lookup"><span data-stu-id="73afe-149">BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="73afe-150">Se non si imposta il parametro ASN, a questo viene assegnato il valore 65515.</span><span class="sxs-lookup"><span data-stu-id="73afe-150">If you do not set the ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="73afe-151">La creazione di un gateway può richiedere un po' di tempo (30 minuti o più).</span><span class="sxs-lookup"><span data-stu-id="73afe-151">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="73afe-152">3. Ottenere l'indirizzo IP del peer BGP di Azure</span><span class="sxs-lookup"><span data-stu-id="73afe-152">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="73afe-153">Dopo la creazione del gateway, è necessario ottenere l'indirizzo IP del peer BGP per il gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="73afe-153">Once the gateway is created, you need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="73afe-154">Questo indirizzo è necessario per configurare il gateway VPN di Azure come peer BGP per i dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="73afe-154">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="73afe-155">L'ultimo comando visualizza le configurazioni BGP corrispondenti nel gateway VPN di Azure, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="73afe-155">The last command shows the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="73afe-156">Una volta creato il gateway, è possibile usarlo per stabilire una connessione cross-premise o una connessione da rete virtuale a rete virtuale con BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-156">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="73afe-157">Le sezioni seguenti illustrano i passaggi per il completamento dell'esercizio.</span><span class="sxs-lookup"><span data-stu-id="73afe-157">The following sections walk through the steps to complete the exercise.</span></span>

## <span data-ttu-id="73afe-158"><a name ="crossprembbgp"></a>Parte 2: Stabilire una connessione cross-premise con BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="73afe-159">Per stabilire una connessione cross-premise, è necessario creare un gateway di rete locale per rappresentare il dispositivo VPN locale e una connessione per connettere il gateway VPN al gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="73afe-159">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the VPN gateway with the local network gateway.</span></span> <span data-ttu-id="73afe-160">Anche se sono disponibili articoli che descrivono questi passaggi in dettaglio, questo articolo contiene le proprietà aggiuntive necessarie per specificare i parametri di configurazione di BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-160">While there are articles that walk you through these steps, this article contains the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP per la connessione cross-premise](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="73afe-162">Prima di procedere, verificare di avere completato la [Parte 1](#enablebgp) di questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="73afe-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="73afe-163">Passaggio 1: Creare e configurare il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="73afe-163">Step 1 - Create and configure the local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="73afe-164">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="73afe-164">1. Declare your variables</span></span>

<span data-ttu-id="73afe-165">Questo esercizio continua a creare la configurazione illustrata nel diagramma.</span><span class="sxs-lookup"><span data-stu-id="73afe-165">This exercise continues to build the configuration shown in the diagram.</span></span> <span data-ttu-id="73afe-166">Sostituire i valori con quelli desiderati per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="73afe-166">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="73afe-167">È necessario tenere presenti due aspetti relativi ai parametri del gateway di rete:</span><span class="sxs-lookup"><span data-stu-id="73afe-167">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="73afe-168">Il gateway di rete locale può essere nella stessa località e nello stesso gruppo di risorse del gateway VPN oppure in altri.</span><span class="sxs-lookup"><span data-stu-id="73afe-168">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="73afe-169">In questo esempio sono in gruppi di risorse diversi in località diverse.</span><span class="sxs-lookup"><span data-stu-id="73afe-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="73afe-170">Il prefisso minimo che è necessario dichiarare per il gateway di rete locale è l'indirizzo host dell'indirizzo IP del peer BGP nel dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="73afe-170">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="73afe-171">In questo caso, è un prefisso /32 di "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="73afe-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="73afe-172">Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="73afe-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="73afe-173">Se sono gli stessi, è necessario modificare l'ASN della rete virtuale se il dispositivo VPN locale usa già l'ASN per il peering con altri vicini BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-173">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="73afe-174">Prima di proseguire, verificare di essere ancora connessi alla sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="73afe-174">Before you continue, make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="73afe-175">2. Creare il gateway di rete locale per Site5</span><span class="sxs-lookup"><span data-stu-id="73afe-175">2. Create the local network gateway for Site5</span></span>

<span data-ttu-id="73afe-176">Assicurarsi di creare il gruppo di risorse se non è stato creato, prima di creare il gateway di rete locale.</span><span class="sxs-lookup"><span data-stu-id="73afe-176">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="73afe-177">Si notino i due parametri aggiuntivi per il gateway di rete locale: Asn e BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="73afe-177">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="73afe-178">Passaggio 2: Connettere il gateway di rete virtuale e il gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="73afe-178">Step 2 - Connect the VNet gateway and local network gateway</span></span>

#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="73afe-179">1. Ottenere i due gateway</span><span class="sxs-lookup"><span data-stu-id="73afe-179">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="73afe-180">2. Creare la connessione da TestVNet1 a Site5</span><span class="sxs-lookup"><span data-stu-id="73afe-180">2. Create the TestVNet1 to Site5 connection</span></span>

<span data-ttu-id="73afe-181">In questo passaggio viene creata la connessione da TestVNet1 a Site5.</span><span class="sxs-lookup"><span data-stu-id="73afe-181">In this step, you create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="73afe-182">È necessario specificare "-EnableBgp $True" per abilitare BGP per questa connessione.</span><span class="sxs-lookup"><span data-stu-id="73afe-182">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="73afe-183">Come illustrato in precedenza, è possibile avere connessioni sia BGP che non BGP per lo stesso gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="73afe-183">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="73afe-184">A meno che BGP non venga abilitato nella proprietà della connessione, Azure non abiliterà BGP per questa connessione nemmeno se i parametri BGP sono già configurati in entrambi i gateway.</span><span class="sxs-lookup"><span data-stu-id="73afe-184">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="73afe-185">L'esempio seguente elenca i parametri da immettere nella sezione della configurazione BGP nel dispositivo VPN locale per questo esercizio:</span><span class="sxs-lookup"><span data-stu-id="73afe-185">The following example lists the parameters you enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="73afe-186">La connessione viene stabilita in pochi minuti e la sessione di peering BGP viene avviata non appena stabilita la connessione IPsec.</span><span class="sxs-lookup"><span data-stu-id="73afe-186">The connection is established after a few minutes, and the BGP peering session starts once the IPsec connection is established.</span></span>

## <span data-ttu-id="73afe-187"><a name ="v2vbgp"></a>Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="73afe-188">Questa sezione aggiunge una connessione da rete virtuale a rete virtuale con BGP, come illustrato nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="73afe-188">This section adds a VNet-to-VNet connection with BGP, as shown in the following diagram:</span></span>

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="73afe-190">Le istruzioni seguenti sono la prosecuzione dei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="73afe-190">The following instructions continue from the previous steps.</span></span> <span data-ttu-id="73afe-191">È necessario completare la [Parte I](#enablebgp) per creare e configurare TestVNet1 e il gateway VPN con BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-191">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="73afe-192">Passaggio 1: Creare TestVNet2 e il gateway VPN</span><span class="sxs-lookup"><span data-stu-id="73afe-192">Step 1 - Create TestVNet2 and the VPN gateway</span></span>

<span data-ttu-id="73afe-193">È importante verificare che lo spazio di indirizzi IP della nuova rete virtuale, TestVNet2, non si sovrapponga ad altri di intervalli di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="73afe-193">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="73afe-194">In questo esempio le reti virtuali appartengono alla stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="73afe-194">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="73afe-195">È possibile configurare connessioni da rete virtuale a rete virtuale tra sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="73afe-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="73afe-196">Per altre informazioni, vedere [Configurare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="73afe-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="73afe-197">Assicurarsi di aggiungere "-EnableBgp $True" quando si creano le connessioni per abilitare BGP.</span><span class="sxs-lookup"><span data-stu-id="73afe-197">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="73afe-198">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="73afe-198">1. Declare your variables</span></span>

<span data-ttu-id="73afe-199">Sostituire i valori con quelli desiderati per la propria configurazione.</span><span class="sxs-lookup"><span data-stu-id="73afe-199">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="73afe-200">2. Creare TestVNet2 nel nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="73afe-200">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="73afe-201">3. Creare il gateway VPN per TestVNet2 con i parametri BGP</span><span class="sxs-lookup"><span data-stu-id="73afe-201">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="73afe-202">Richiedere un indirizzo IP pubblico da allocare al gateway che verrà creato per la rete virtuale e definire le configurazioni necessarie per subnet e IP.</span><span class="sxs-lookup"><span data-stu-id="73afe-202">Request a public IP address to be allocated to the gateway you will create for your VNet and define the required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="73afe-203">Creare il gateway VPN con il numero AS.</span><span class="sxs-lookup"><span data-stu-id="73afe-203">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="73afe-204">È necessario eseguire l'override dell'ASN predefinito nei gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="73afe-204">You must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="73afe-205">Gli ASN per le reti virtuali connesse devono essere diversi per abilitare BGP e il routing di transito.</span><span class="sxs-lookup"><span data-stu-id="73afe-205">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="73afe-206">Passaggio 2: Connettere i gateway TestVNet1 e TestVNet2</span><span class="sxs-lookup"><span data-stu-id="73afe-206">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="73afe-207">In questo esempio entrambi i gateway sono nella stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="73afe-207">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="73afe-208">È possibile completare questo passaggio nella stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="73afe-208">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="73afe-209">1. Ottenere entrambi i gateway</span><span class="sxs-lookup"><span data-stu-id="73afe-209">1. Get both gateways</span></span>

<span data-ttu-id="73afe-210">Eseguire l'accesso e connettersi alla Sottoscrizione 1.</span><span class="sxs-lookup"><span data-stu-id="73afe-210">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="73afe-211">2. Creare entrambe le connessioni</span><span class="sxs-lookup"><span data-stu-id="73afe-211">2. Create both connections</span></span>

<span data-ttu-id="73afe-212">In questo passaggio vengono create le connessioni rispettivamente da TestVNet1 a TestVNet2 e da TestVNet2 a TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="73afe-212">In this step, you create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="73afe-213">Assicurarsi di abilitare BGP per ENTRAMBE le connessioni.</span><span class="sxs-lookup"><span data-stu-id="73afe-213">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="73afe-214">Dopo il completamento di questi passaggi, la connessione viene stabilita entro pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="73afe-214">After completing these steps, the connection is established after a few minutes.</span></span> <span data-ttu-id="73afe-215">Non appena completata la connessione da rete virtuale a rete virtuale, la sessione di peering BGP è attiva.</span><span class="sxs-lookup"><span data-stu-id="73afe-215">The BGP peering session is up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="73afe-216">Se sono state completate tutte e tre le parti di questo esercizio, è stata stabilita la topologia di rete seguente:</span><span class="sxs-lookup"><span data-stu-id="73afe-216">If you completed all three parts of this exercise, you have established the following network topology:</span></span>

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="73afe-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="73afe-218">Next steps</span></span>

<span data-ttu-id="73afe-219">Dopo aver completato la connessione, è possibile aggiungere macchine virtuali alle reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="73afe-219">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="73afe-220">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="73afe-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>