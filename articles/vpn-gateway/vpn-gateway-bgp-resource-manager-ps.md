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
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="9223f-103">Come tooconfigure BGP nel gateway VPN di Azure tramite PowerShell</span><span class="sxs-lookup"><span data-stu-id="9223f-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="9223f-104">In questo articolo illustra hello passaggi tooenable BGP su una connessione VPN da sito a sito (S2S) di cross-premise e una connessione di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9223f-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="9223f-105">Informazioni su BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-105">About BGP</span></span>
<span data-ttu-id="9223f-106">BGP è hello protocollo di routing standard comunemente utilizzato nelle hello Internet tooexchange routing e raggiungibilità informazioni tra due o più reti.</span><span class="sxs-lookup"><span data-stu-id="9223f-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="9223f-107">Protocollo BGP consente gateway VPN di Azure hello e i dispositivi VPN locale, denominati i peer BGP o elementi adiacenti, tooexchange "Invia" che informa sulla disponibilità hello entrambi i gateway e raggiungibilità per tali prefissi toogo tramite gateway hello o router coinvolti.</span><span class="sxs-lookup"><span data-stu-id="9223f-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="9223f-108">BGP inoltre è possibile abilitare il routing di transito tra più reti mediante propagazione di route, un gateway BGP apprende da uno tooall peer BGP altri peer BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="9223f-109">Vedere [Panoramica del protocollo BGP con gateway VPN di Azure](vpn-gateway-bgp-overview.md) per ulteriori informazioni sui vantaggi di BGP e toounderstand hello requisiti tecnici e le considerazioni di usando BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="9223f-110">Introduzione a BGP nei gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="9223f-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="9223f-111">In questo articolo illustra hello toodo di passaggi hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="9223f-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="9223f-112">Parte 1: Abilitare BGP nel gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="9223f-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="9223f-113">Parte 2: Stabilire una connessione cross-premise con BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="9223f-114">Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="9223f-115">Ogni parte di istruzioni hello costituisce un blocco predefinito di base per abilitare BGP nella connettività di rete.</span><span class="sxs-lookup"><span data-stu-id="9223f-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="9223f-116">Se si completano tutte le tre parti, come illustrato nel seguente diagramma hello è compilare topologia hello:</span><span class="sxs-lookup"><span data-stu-id="9223f-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="9223f-118">È possibile combinare parti insieme toobuild una rete di transito più complessi, multi-hop, che soddisfa le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="9223f-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="9223f-119"><a name ="enablebgp"></a>Parte 1 - configurare BGP sui hello Gateway VPN di Azure</span><span class="sxs-lookup"><span data-stu-id="9223f-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="9223f-120">passaggi di configurazione Hello impostare hello i parametri BGP del gateway VPN di Azure hello come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="9223f-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="9223f-122">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="9223f-122">Before you begin</span></span>
* <span data-ttu-id="9223f-123">Verificare di possedere una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="9223f-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="9223f-124">Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9223f-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9223f-125">Installare i cmdlet di PowerShell di gestione risorse di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9223f-126">Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9223f-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="9223f-127">Passaggio 1: Creare e configurare VNet1</span><span class="sxs-lookup"><span data-stu-id="9223f-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="9223f-128">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="9223f-128">1. Declare your variables</span></span>
<span data-ttu-id="9223f-129">Per questo esercizio, si inizierà dichiarando le variabili.</span><span class="sxs-lookup"><span data-stu-id="9223f-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="9223f-130">Hello seguente dichiara variabili hello utilizzando valori hello per questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="9223f-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="9223f-131">Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione.</span><span class="sxs-lookup"><span data-stu-id="9223f-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="9223f-132">Se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione, è possibile utilizzare queste variabili.</span><span class="sxs-lookup"><span data-stu-id="9223f-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="9223f-133">Modificare le variabili di hello e quindi copiare e incollare nella console di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9223f-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="9223f-134">2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="9223f-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="9223f-135">hello toouse cmdlet di gestione risorse, accertarsi di passare in modalità tooPowerShell.</span><span class="sxs-lookup"><span data-stu-id="9223f-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="9223f-136">Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9223f-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="9223f-137">Aprire la console di PowerShell e tooyour account di connessione.</span><span class="sxs-lookup"><span data-stu-id="9223f-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="9223f-138">Utilizzare hello toohelp esempio che ci si connette seguenti:</span><span class="sxs-lookup"><span data-stu-id="9223f-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="9223f-139">3. Creare TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9223f-139">3. Create TestVNet1</span></span>
<span data-ttu-id="9223f-140">Hello esempio seguente crea una rete virtuale denominata TestVNet1 e tre subnet, uno GatewaySubnet chiamato, un front-end denominato e un back-end denominato.</span><span class="sxs-lookup"><span data-stu-id="9223f-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="9223f-141">Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="9223f-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="9223f-142">Se si assegnano altri nomi, la creazione del gateway ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="9223f-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="9223f-143">Passaggio 2: creare hello Gateway VPN per TestVNet1 con i parametri BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="9223f-144">1. Creare hello configurazioni IP e subnet</span><span class="sxs-lookup"><span data-stu-id="9223f-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="9223f-145">Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta.</span><span class="sxs-lookup"><span data-stu-id="9223f-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="9223f-146">Verrà anche definire le configurazioni IP e subnet di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="9223f-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="9223f-147">2. Creare il gateway VPN di hello con hello sotto forma di numero</span><span class="sxs-lookup"><span data-stu-id="9223f-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="9223f-148">Creare il gateway di rete virtuale hello per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9223f-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="9223f-149">BGP richiede un basato su Route gateway VPN e parametro aggiunta hello - Asn, tooset hello ASN (numero AS) per TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9223f-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="9223f-150">Se non si imposta il parametro ASN hello, ASN 65515 è assegnato.</span><span class="sxs-lookup"><span data-stu-id="9223f-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="9223f-151">Creazione di un gateway può richiedere un po' di tempo (30 minuti o più toocomplete).</span><span class="sxs-lookup"><span data-stu-id="9223f-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="9223f-152">3. Ottenere l'indirizzo IP del Peer BGP Azure hello</span><span class="sxs-lookup"><span data-stu-id="9223f-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="9223f-153">Una volta creato il gateway di hello, è necessario tooobtain hello IP Peer BGP indirizzo hello Gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="9223f-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="9223f-154">Questo indirizzo è hello tooconfigure necessari Gateway VPN di Azure come Peer BGP per i dispositivi VPN locali.</span><span class="sxs-lookup"><span data-stu-id="9223f-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="9223f-155">ultimo comando Hello Mostra le configurazioni di BGP corrispondenti hello in hello Gateway VPN di Azure. Per esempio:</span><span class="sxs-lookup"><span data-stu-id="9223f-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="9223f-156">Una volta creato il gateway di hello, è possibile utilizzare questo gateway tooestablish cross-premise o da rete connessione con BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="9223f-157">Hello nelle sezioni seguenti vengono esaminati hello passaggi toocomplete hello esercizio.</span><span class="sxs-lookup"><span data-stu-id="9223f-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="9223f-158"><a name ="crossprembbgp"></a>Parte 2: Stabilire una connessione cross-premise con BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="9223f-159">tooestablish una connessione cross-premise, è necessario toocreate toorepresent un Gateway di rete locale del dispositivo VPN locale e il gateway VPN hello tooconnect connessione con il gateway di rete locale hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="9223f-160">Sebbene esistano articoli che analizzano questi passaggi, in questo articolo contiene parametri di configurazione BGP necessarie toospecify hello hello proprietà aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="9223f-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![BGP per la connessione cross-premise](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="9223f-162">Prima di procedere, verificare di avere completato la [Parte 1](#enablebgp) di questo esercizio.</span><span class="sxs-lookup"><span data-stu-id="9223f-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="9223f-163">Passaggio 1: creare e configurare il gateway di rete locale hello</span><span class="sxs-lookup"><span data-stu-id="9223f-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="9223f-164">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="9223f-164">1. Declare your variables</span></span>

<span data-ttu-id="9223f-165">Questo esercizio continua configurazione hello toobuild illustrato nel diagramma hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="9223f-166">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="9223f-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="9223f-167">Un paio di aspetti toonote relativi parametri di gateway di rete locale hello:</span><span class="sxs-lookup"><span data-stu-id="9223f-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="9223f-168">gateway di rete locale Hello può essere nella stessa hello o un percorso diverso e risorse gruppo come hello gateway VPN.</span><span class="sxs-lookup"><span data-stu-id="9223f-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="9223f-169">In questo esempio sono in gruppi di risorse diversi in località diverse.</span><span class="sxs-lookup"><span data-stu-id="9223f-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="9223f-170">prefisso di minimo Hello toodeclare è necessario per il gateway di rete locale hello è indirizzo host hello dell'indirizzo IP Peer BGP sul dispositivo VPN.</span><span class="sxs-lookup"><span data-stu-id="9223f-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="9223f-171">In questo caso, è un prefisso /32 di "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="9223f-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="9223f-172">Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="9223f-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="9223f-173">Se si sono hello stesso, è necessario toochange l'ASN VNet se il dispositivo VPN locale utilizza già hello toopeer ASN con altri router adiacenti BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="9223f-174">Prima di continuare, verificare che si è ancora connesso tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="9223f-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="9223f-175">2. Creare il gateway di rete locale hello per Site5</span><span class="sxs-lookup"><span data-stu-id="9223f-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="9223f-176">Se non viene creato, prima di creare il gateway di rete locale hello, essere gruppo di risorse che toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="9223f-177">Si notino hello due parametri aggiuntivi per il gateway di rete locale hello: Asn e BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="9223f-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="9223f-178">Passaggio 2: connettere il gateway di rete virtuale hello e gateway di rete locale</span><span class="sxs-lookup"><span data-stu-id="9223f-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="9223f-179">1. Ottenere hello due gateway</span><span class="sxs-lookup"><span data-stu-id="9223f-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="9223f-180">2. Creare hello TestVNet1 tooSite5 connessione</span><span class="sxs-lookup"><span data-stu-id="9223f-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="9223f-181">In questo passaggio si crea connessione di hello da TestVNet1 tooSite5.</span><span class="sxs-lookup"><span data-stu-id="9223f-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="9223f-182">È necessario specificare "-EnableBGP $True" tooenable BGP per questa connessione.</span><span class="sxs-lookup"><span data-stu-id="9223f-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="9223f-183">Come illustrato in precedenza, è possibile toohave le connessioni BGP sia non BGP per hello stesso Gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="9223f-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="9223f-184">A meno che il protocollo BGP è abilitato nella proprietà di connessione hello, Azure non abilitare il protocollo BGP per questa connessione anche se i parametri BGP sono già configurati su entrambi i gateway.</span><span class="sxs-lookup"><span data-stu-id="9223f-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="9223f-185">Hello esempio seguente vengono elencati i parametri di hello che immesso nella sezione di configurazione BGP hello sul dispositivo VPN locale per questo esercizio:</span><span class="sxs-lookup"><span data-stu-id="9223f-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="9223f-186">Hello connessione dopo alcuni minuti e hello BGP peering sessione inizia dopo aver stabilito la connessione IPsec hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="9223f-187"><a name ="v2vbgp"></a>Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="9223f-188">In questa sezione consente di aggiungere una connessione di rete virtuale a con il protocollo BGP, come illustrato nel seguente diagramma hello:</span><span class="sxs-lookup"><span data-stu-id="9223f-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="9223f-190">Hello attenendosi alle istruzioni continua nei passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="9223f-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="9223f-191">È necessario completare [parte I](#enablebgp) toocreate e configurare TestVNet1 e hello Gateway VPN con il protocollo BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="9223f-192">Passaggio 1: creare TestVNet2 e hello gateway VPN</span><span class="sxs-lookup"><span data-stu-id="9223f-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="9223f-193">È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet2, non si sovrapponga ad altri intervalli di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="9223f-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="9223f-194">In questo esempio, le reti virtuali hello appartengono toohello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9223f-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="9223f-195">È possibile configurare connessioni da rete virtuale a rete virtuale tra sottoscrizioni diverse.</span><span class="sxs-lookup"><span data-stu-id="9223f-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="9223f-196">Per altre informazioni, vedere [Configurare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9223f-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="9223f-197">Assicurarsi di aggiungere hello "-EnableBgp $True" quando la creazione di hello tooenable connessioni BGP.</span><span class="sxs-lookup"><span data-stu-id="9223f-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="9223f-198">1. Dichiarare le variabili</span><span class="sxs-lookup"><span data-stu-id="9223f-198">1. Declare your variables</span></span>

<span data-ttu-id="9223f-199">Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.</span><span class="sxs-lookup"><span data-stu-id="9223f-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="9223f-200">2. Creare il nuovo gruppo di risorse hello TestVNet2</span><span class="sxs-lookup"><span data-stu-id="9223f-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="9223f-201">3. Creare il gateway VPN di hello per TestVNet2 con i parametri BGP</span><span class="sxs-lookup"><span data-stu-id="9223f-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="9223f-202">Richiedere un pubblico indirizzo toobe toohello allocato gateway IP verrà creato per la rete virtuale e definire le configurazioni IP e subnet di hello necessario.</span><span class="sxs-lookup"><span data-stu-id="9223f-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="9223f-203">Creare il gateway VPN di hello con hello come numero.</span><span class="sxs-lookup"><span data-stu-id="9223f-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="9223f-204">È necessario eseguire l'override di predefinito hello ASN nel gateway VPN di Azure.</span><span class="sxs-lookup"><span data-stu-id="9223f-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="9223f-205">Hello ASN per hello connessi a reti virtuali devono essere diversi tooenable BGP e il routing di transito.</span><span class="sxs-lookup"><span data-stu-id="9223f-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="9223f-206">Passaggio 2: connettere i gateway TestVNet1 e TestVNet2 hello</span><span class="sxs-lookup"><span data-stu-id="9223f-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="9223f-207">In questo esempio, entrambi i gateway sono in hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9223f-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="9223f-208">È possibile completare questo passaggio in hello stessa sessione di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9223f-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="9223f-209">1. Ottenere entrambi i gateway</span><span class="sxs-lookup"><span data-stu-id="9223f-209">1. Get both gateways</span></span>

<span data-ttu-id="9223f-210">Assicurarsi di accedere e connettersi tooSubscription 1.</span><span class="sxs-lookup"><span data-stu-id="9223f-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="9223f-211">2. Creare entrambe le connessioni</span><span class="sxs-lookup"><span data-stu-id="9223f-211">2. Create both connections</span></span>

<span data-ttu-id="9223f-212">In questo passaggio si creare connessione hello da TestVNet1 tooTestVNet2 e connessione hello da TestVNet2 tooTestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9223f-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="9223f-213">Impossibile verificare tooenable BGP per entrambe le connessioni.</span><span class="sxs-lookup"><span data-stu-id="9223f-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="9223f-214">Dopo aver completato questi passaggi, hello connessione dopo alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9223f-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="9223f-215">Dopo aver eseguito la connessione di rete virtuale a hello, sessione di peering BGP Hello è attivo.</span><span class="sxs-lookup"><span data-stu-id="9223f-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="9223f-216">Se è stato completato tutte le tre parti di questo esercizio, è stato stabilito hello topologia di rete seguenti:</span><span class="sxs-lookup"><span data-stu-id="9223f-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="9223f-218">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9223f-218">Next steps</span></span>

<span data-ttu-id="9223f-219">Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="9223f-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="9223f-220">Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .</span><span class="sxs-lookup"><span data-stu-id="9223f-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
