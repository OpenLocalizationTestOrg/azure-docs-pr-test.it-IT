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
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a>Come tooconfigure BGP nel gateway VPN di Azure tramite PowerShell
In questo articolo illustra hello passaggi tooenable BGP su una connessione VPN da sito a sito (S2S) di cross-premise e una connessione di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.

## <a name="about-bgp"></a>Informazioni su BGP
BGP è hello protocollo di routing standard comunemente utilizzato nelle hello Internet tooexchange routing e raggiungibilità informazioni tra due o più reti. Protocollo BGP consente gateway VPN di Azure hello e i dispositivi VPN locale, denominati i peer BGP o elementi adiacenti, tooexchange "Invia" che informa sulla disponibilità hello entrambi i gateway e raggiungibilità per tali prefissi toogo tramite gateway hello o router coinvolti. BGP inoltre è possibile abilitare il routing di transito tra più reti mediante propagazione di route, un gateway BGP apprende da uno tooall peer BGP altri peer BGP.

Vedere [Panoramica del protocollo BGP con gateway VPN di Azure](vpn-gateway-bgp-overview.md) per ulteriori informazioni sui vantaggi di BGP e toounderstand hello requisiti tecnici e le considerazioni di usando BGP.

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a>Introduzione a BGP nei gateway VPN di Azure

In questo articolo illustra hello toodo di passaggi hello seguenti attività:

* [Parte 1: Abilitare BGP nel gateway VPN di Azure](#enablebgp)
* [Parte 2: Stabilire una connessione cross-premise con BGP](#crossprembgp)
* [Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP](#v2vbgp)

Ogni parte di istruzioni hello costituisce un blocco predefinito di base per abilitare BGP nella connettività di rete. Se si completano tutte le tre parti, come illustrato nel seguente diagramma hello è compilare topologia hello:

![Topologia BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

È possibile combinare parti insieme toobuild una rete di transito più complessi, multi-hop, che soddisfa le proprie esigenze.

## <a name ="enablebgp"></a>Parte 1 - configurare BGP sui hello Gateway VPN di Azure
passaggi di configurazione Hello impostare hello i parametri BGP del gateway VPN di Azure hello come illustrato nel seguente diagramma hello:

![Gateway BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a>Prima di iniziare
* Verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* Installare i cmdlet di PowerShell di gestione risorse di Azure hello. Per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). 

### <a name="step-1---create-and-configure-vnet1"></a>Passaggio 1: Creare e configurare VNet1
#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili
Per questo esercizio, si inizierà dichiarando le variabili. Hello seguente dichiara variabili hello utilizzando valori hello per questo esercizio. Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione. Se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione, è possibile utilizzare queste variabili. Modificare le variabili di hello e quindi copiare e incollare nella console di PowerShell.

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse
hello toouse cmdlet di gestione risorse, accertarsi di passare in modalità tooPowerShell. Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).

Aprire la console di PowerShell e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Creare TestVNet1
Hello esempio seguente crea una rete virtuale denominata TestVNet1 e tre subnet, uno GatewaySubnet chiamato, un front-end denominato e un back-end denominato. Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet. Se si assegnano altri nomi, la creazione del gateway ha esito negativo.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a>Passaggio 2: creare hello Gateway VPN per TestVNet1 con i parametri BGP
#### <a name="1-create-hello-ip-and-subnet-configurations"></a>1. Creare hello configurazioni IP e subnet
Pubblica IP indirizzo toobe toohello allocato gateway che si creerà per la rete virtuale della richiesta. Verrà anche definire le configurazioni IP e subnet di hello necessario.

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a>2. Creare il gateway VPN di hello con hello sotto forma di numero
Creare il gateway di rete virtuale hello per TestVNet1. BGP richiede un basato su Route gateway VPN e parametro aggiunta hello - Asn, tooset hello ASN (numero AS) per TestVNet1. Se non si imposta il parametro ASN hello, ASN 65515 è assegnato. Creazione di un gateway può richiedere un po' di tempo (30 minuti o più toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a>3. Ottenere l'indirizzo IP del Peer BGP Azure hello
Una volta creato il gateway di hello, è necessario tooobtain hello IP Peer BGP indirizzo hello Gateway VPN di Azure. Questo indirizzo è hello tooconfigure necessari Gateway VPN di Azure come Peer BGP per i dispositivi VPN locali.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

ultimo comando Hello Mostra le configurazioni di BGP corrispondenti hello in hello Gateway VPN di Azure. Per esempio:

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

Una volta creato il gateway di hello, è possibile utilizzare questo gateway tooestablish cross-premise o da rete connessione con BGP. Hello nelle sezioni seguenti vengono esaminati hello passaggi toocomplete hello esercizio.

## <a name ="crossprembbgp"></a>Parte 2: Stabilire una connessione cross-premise con BGP

tooestablish una connessione cross-premise, è necessario toocreate toorepresent un Gateway di rete locale del dispositivo VPN locale e il gateway VPN hello tooconnect connessione con il gateway di rete locale hello. Sebbene esistano articoli che analizzano questi passaggi, in questo articolo contiene parametri di configurazione BGP necessarie toospecify hello hello proprietà aggiuntive.

![BGP per la connessione cross-premise](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

Prima di procedere, verificare di avere completato la [Parte 1](#enablebgp) di questo esercizio.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Passaggio 1: creare e configurare il gateway di rete locale hello

#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili

Questo esercizio continua configurazione hello toobuild illustrato nel diagramma hello. Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

Un paio di aspetti toonote relativi parametri di gateway di rete locale hello:

* gateway di rete locale Hello può essere nella stessa hello o un percorso diverso e risorse gruppo come hello gateway VPN. In questo esempio sono in gruppi di risorse diversi in località diverse.
* prefisso di minimo Hello toodeclare è necessario per il gateway di rete locale hello è indirizzo host hello dell'indirizzo IP Peer BGP sul dispositivo VPN. In questo caso, è un prefisso /32 di "10.52.255.254/32".
* Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure. Se si sono hello stesso, è necessario toochange l'ASN VNet se il dispositivo VPN locale utilizza già hello toopeer ASN con altri router adiacenti BGP.

Prima di continuare, verificare che si è ancora connesso tooSubscription 1.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Creare il gateway di rete locale hello per Site5

Se non viene creato, prima di creare il gateway di rete locale hello, essere gruppo di risorse che toocreate hello. Si notino hello due parametri aggiuntivi per il gateway di rete locale hello: Asn e BgpPeerAddress.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Passaggio 2: connettere il gateway di rete virtuale hello e gateway di rete locale

#### <a name="1-get-hello-two-gateways"></a>1. Ottenere hello due gateway

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Creare hello TestVNet1 tooSite5 connessione

In questo passaggio si crea connessione di hello da TestVNet1 tooSite5. È necessario specificare "-EnableBGP $True" tooenable BGP per questa connessione. Come illustrato in precedenza, è possibile toohave le connessioni BGP sia non BGP per hello stesso Gateway VPN di Azure. A meno che il protocollo BGP è abilitato nella proprietà di connessione hello, Azure non abilitare il protocollo BGP per questa connessione anche se i parametri BGP sono già configurati su entrambi i gateway.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

Hello esempio seguente vengono elencati i parametri di hello che immesso nella sezione di configurazione BGP hello sul dispositivo VPN locale per questo esercizio:

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

Hello connessione dopo alcuni minuti e hello BGP peering sessione inizia dopo aver stabilito la connessione IPsec hello.

## <a name ="v2vbgp"></a>Parte 3: Stabilire una connessione da rete virtuale a rete virtuale con BGP

In questa sezione consente di aggiungere una connessione di rete virtuale a con il protocollo BGP, come illustrato nel seguente diagramma hello:

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

Hello attenendosi alle istruzioni continua nei passaggi precedenti hello. È necessario completare [parte I](#enablebgp) toocreate e configurare TestVNet1 e hello Gateway VPN con il protocollo BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Passaggio 1: creare TestVNet2 e hello gateway VPN

È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet2, non si sovrapponga ad altri intervalli di rete virtuale.

In questo esempio, le reti virtuali hello appartengono toohello stessa sottoscrizione. È possibile configurare connessioni da rete virtuale a rete virtuale tra sottoscrizioni diverse. Per altre informazioni, vedere [Configurare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md). Assicurarsi di aggiungere hello "-EnableBgp $True" quando la creazione di hello tooenable connessioni BGP.

#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili

Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Creare il nuovo gruppo di risorse hello TestVNet2

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a>3. Creare il gateway VPN di hello per TestVNet2 con i parametri BGP

Richiedere un pubblico indirizzo toobe toohello allocato gateway IP verrà creato per la rete virtuale e definire le configurazioni IP e subnet di hello necessario.

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

Creare il gateway VPN di hello con hello come numero. È necessario eseguire l'override di predefinito hello ASN nel gateway VPN di Azure. Hello ASN per hello connessi a reti virtuali devono essere diversi tooenable BGP e il routing di transito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a>Passaggio 2: connettere i gateway TestVNet1 e TestVNet2 hello

In questo esempio, entrambi i gateway sono in hello stessa sottoscrizione. È possibile completare questo passaggio in hello stessa sessione di PowerShell.

#### <a name="1-get-both-gateways"></a>1. Ottenere entrambi i gateway

Assicurarsi di accedere e connettersi tooSubscription 1.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a>2. Creare entrambe le connessioni

In questo passaggio si creare connessione hello da TestVNet1 tooTestVNet2 e connessione hello da TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Impossibile verificare tooenable BGP per entrambe le connessioni.
> 
> 

Dopo aver completato questi passaggi, hello connessione dopo alcuni minuti. Dopo aver eseguito la connessione di rete virtuale a hello, sessione di peering BGP Hello è attivo.

Se è stato completato tutte le tre parti di questo esercizio, è stato stabilito hello topologia di rete seguenti:

![BGP per la connessione da rete virtuale a rete virtuale](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a>Passaggi successivi

Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .
