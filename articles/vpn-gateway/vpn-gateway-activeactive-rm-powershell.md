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
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a>Configurare connessioni di rete privata virtuale da sito a sito active-active con gateway VPN di Azure

In questo articolo illustra hello passaggi toocreate attivo-attivo cross-premise e connessioni di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.

## <a name="about-highly-available-cross-premises-connections"></a>Informazioni sulle connessioni cross-premise a disponibilità elevata
disponibilità elevata tooachieve per cross-premise e connettività di rete virtuale a, è necessario distribuire più gateway VPN e stabilire più connessioni parallele tra Azure e le reti. Per una panoramica delle opzioni di connettività e della topologia, vedere [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) (Connettività cross-premise e da rete virtuale a rete virtuale a disponibilità elevata).

In questo articolo vengono fornite istruzioni hello tooset backup attivo-attivo cross-premise connessione VPN e attivo-attivo connessione tra due reti virtuali:

* [Parte 1: creare e configurare il gateway VPN di Azure in modalità active-active](#aagateway)
* [Parte 2: stabilire connessioni cross-premise active-active](#aacrossprem)
* [Parte 3: stabilire connessioni da rete virtuale a rete virtuale active-active](#aav2v)
* [Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby](#aaupdate)

È possibile combinare queste toobuild insieme una topologia di rete più complessa, a elevata disponibilità che soddisfa le proprie esigenze.

> [!IMPORTANT]
> Si noti che la modalità attivo-attivo hello utilizza hello solo gli SKU di seguito: 
  * VpnGw1, VpnGw2, VpnGw3
  * HighPerformance (per SKU precedenti legacy)
> 
> 

## <a name ="aagateway"></a>Parte 1: creare e configurare gateway VPN active-active
Hello alla procedura seguente configurerà il gateway VPN di Azure in modalità attivo-attivo. differenze principali di Hello tra i gateway attivo-attivo e attivo-standby hello:

* È necessario toocreate due configurazioni IP del Gateway con due indirizzi IP pubblici
* È necessario impostare il flag di EnableActiveActiveFeature hello
* lo SKU del gateway Hello deve essere VpnGw1, VpnGw2, VpnGw3 o ad alte prestazioni (SKU legacy).

Hello altre proprietà sono hello come gateway di hello attivo-attivo. 

### <a name="before-you-begin"></a>Prima di iniziare
* Verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* È necessario che i cmdlet PowerShell di gestione risorse di Azure di tooinstall hello. Vedere [Panoramica di Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.

### <a name="step-1---create-and-configure-vnet1"></a>Passaggio 1: Creare e configurare VNet1
#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili
Per questo esercizio, si inizierà dichiarando le variabili. esempio Hello seguente dichiara variabili di hello utilizzando valori hello per questo esercizio. Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione. Se si eseguono tramite hello passaggi toobecome familiarità con questo tipo di configurazione, è possibile utilizzare queste variabili. Modificare le variabili di hello e quindi copiare e incollare nella console di PowerShell.

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse
Accertarsi di passare hello toouse di modalità tooPowerShell cmdlet di gestione risorse. Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).

Aprire la console di PowerShell e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a>3. Creare TestVNet1
esempio Hello seguente crea una rete virtuale denominata TestVNet1 e tre subnet, uno GatewaySubnet chiamato, un front-end denominato e un back-end denominato. Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet. Se si assegnano altri nomi, la creazione del gateway avrà esito negativo.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a>Passaggio 2: creare il gateway VPN di hello per TestVNet1 con modalità attivo-attivo
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a>1. Creare gli indirizzi IP pubblici hello e le configurazioni IP gateway
Richiesta due pubblica indirizzi toobe toohello allocato gateway IP che verrà creato per la rete virtuale. Verrà inoltre definire subnet hello e le configurazioni IP necessari.

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a>2. Creare il gateway VPN di hello con configurazione attivo / attivo
Creare il gateway di rete virtuale hello per TestVNet1. Si noti che sono presenti due voci GatewayIpConfig e hello EnableActiveActiveFeature flag è impostato. Creazione di un gateway può richiedere un po' di tempo (45 minuti o più toocomplete).

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a>3. Ottenere gli indirizzi IP pubblici di hello gateway e l'indirizzo IP Peer BGP di hello
Una volta creato il gateway di hello, occorre tooobtain hello IP Peer BGP indirizzo hello Gateway VPN di Azure. Questo indirizzo è hello tooconfigure necessari Gateway VPN di Azure come Peer BGP per i dispositivi VPN locali.

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

Utilizzare hello seguente cmdlet tooshow hello due indirizzi IP pubblici allocati per il gateway VPN e indirizzi IP Peer BGP corrispondenti per ogni istanza del gateway:

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

ordine di Hello di indirizzi IP pubblici hello per le istanze di gateway hello e indirizzi di Peering BGP corrispondenti sono hello hello stesso. In questo esempio, il gateway di hello macchina virtuale con indirizzo IP pubblico di 40.112.190.5 utilizzerà 10.12.255.4 come relativo indirizzo di Peering BGP e gateway hello con 138.91.156.129 utilizzerà 10.12.255.5. Queste informazioni sono necessarie quando si configura in locale i dispositivi VPN gateway attivo-attivo toohello la connessione. gateway Hello è illustrato nel diagramma hello seguito con tutti gli indirizzi:

![active-active gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

Una volta creato il gateway di hello, è possibile utilizzare questo gateway tooestablish attivo-attivo cross-premise o da rete connessione. Nelle sezioni che seguono Hello guiderà hello passaggi toocomplete hello esercizio.

## <a name ="aacrossprem"></a>Parte 2: stabilire una connessione cross-premise active-active
tooestablish una connessione cross-premise, è necessario toocreate toorepresent un Gateway di rete locale del dispositivo VPN locale e il gateway VPN di Azure hello tooconnect connessione con il gateway di rete locale hello. In questo esempio, i gateway VPN di Azure hello è in modalità attivo-attivo. Di conseguenza, anche se è presente un solo in locale il dispositivo VPN (gateway di rete locale) e risorse di una connessione, entrambe le istanze del gateway VPN di Azure consentirà di stabilire il tunnel VPN S2S con dispositivo locale hello.

Prima di procedere, verificare di avere completato la [Parte 1](#aagateway) di questo esercizio.

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a>Passaggio 1: creare e configurare il gateway di rete locale hello
#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili
Questo esercizio continuerà configurazione hello toobuild illustrato nel diagramma hello. Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

Un paio di aspetti toonote relativi parametri di gateway di rete locale hello:

* gateway di rete locale Hello può essere nella stessa hello o un percorso diverso e risorse gruppo come hello gateway VPN. In questo esempio viene loro in diversi gruppi di risorse, ma in hello nello stesso percorso di Azure.
* Se è presente un solo dispositivo VPN di on-premise come illustrato in precedenza, connessione attivo-attivo hello può funzionare con o senza protocollo BGP. Questo esempio viene utilizzato il protocollo BGP per la connessione tra più sedi hello.
* Se BGP è abilitato, il prefisso di hello toodeclare è necessario per il gateway di rete locale hello è l'indirizzo host hello dell'indirizzo IP Peer BGP sul dispositivo VPN. In questo caso, è un prefisso /32 di "10.52.255.253/32".
* Si ricordi che è necessario usare ASN BGP diversi nelle reti locali e nella rete virtuale di Azure. Se si sono hello stesso, è necessario toochange l'ASN VNet se il dispositivo VPN locale utilizza già hello toopeer ASN con altri router adiacenti BGP.

#### <a name="2-create-hello-local-network-gateway-for-site5"></a>2. Creare il gateway di rete locale hello per Site5
Prima di continuare, verificare che si è ancora connesso tooSubscription 1. Creare il gruppo di risorse hello se non è ancora stato creato.

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a>Passaggio 2: connettere il gateway di rete virtuale hello e gateway di rete locale
#### <a name="1-get-hello-two-gateways"></a>1. Ottenere hello due gateway

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a>2. Creare hello TestVNet1 tooSite5 connessione
In questo passaggio si creerà hello connessione da TestVNet1 tooSite5_1 con "EnableBGP" impostare troppo$ True.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a>3. Parametri di VPN e BGP per il dispositivo VPN locale
esempio Hello seguente elenca i parametri di hello che immetterà hello sezione di configurazione BGP sul dispositivo VPN locale per questo esercizio:

    - Site5 ASN            : 65050
    - Site5 BGP IP         : 10.52.255.253
    - I prefissi tooannounce:, ad esempio, 10.51.0.0/16 e 10.52.0.0/16
    - Azure VNet ASN       : 65010
    - Azure rete virtuale BGP IP 1: 10.12.255.4 per too40.112.190.5 tunnel
    - Azure rete virtuale BGP IP 2: 10.12.255.5 per too138.91.156.129 tunnel
    - Le route statiche: destinazione 10.12.255.4/32, hop successivo hello VPN tunnel interfaccia too40.112.190.5 destinazione 10.12.255.5/32, too138.91.156.129 interfaccia tunnel di hop successivo hello VPN
    - eBGP Multihop: verificare l'opzione "multihop" hello per eBGP è abilitato nel dispositivo, se necessario

Hello devono connettersi dopo qualche minuto e sessione di peering BGP hello inizierà dopo aver stabilito la connessione IPsec hello. In questo esempio finora è configurato un solo dispositivo VPN locale, risultante in diagramma hello illustrato di seguito:

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a>Passaggio 3: connettere due sedi dispositivi toohello attivo-attivo VPN gateway VPN
Se sono presenti due dispositivi VPN hello stesso locale rete, è possibile ottenere ridondanza duale connessione hello Azure dispositivo gateway VPN toohello secondo VPN.

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a>1. Creare il gateway di rete locale secondo hello per Site5
Si noti che l'indirizzo peer BGP per gateway di rete locale hello secondo indirizzo IP del gateway hello e prefisso di indirizzo non devono sovrapporsi a gateway di rete locale per hello precedente hello stessa rete in locale.

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a>2. Connettersi al gateway di rete virtuale hello e gateway di rete locale secondo hello
Il nome di connessione hello TestVNet1 tooSite5_2 con "EnableBGP" impostare troppo$ True

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a>3. Parametri di VPN e BGP per il secondo dispositivo VPN locale
Analogamente, di sotto di elenchi di parametri di hello immetterà dispositivo VPN secondo hello:

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

Una volta stabiliti i connessione hello (tunnel), si disporrà di duali dispositivi VPN ridondanti e tunnel che connette la rete locale e Azure:

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a>Parte 3: stabilire una connessione da rete virtuale a rete virtuale active-active
In questa sezione viene creata una connessione da rete virtuale a rete virtuale active-active con BGP. 

istruzioni di Hello seguenti continuano nei passaggi precedenti di hello elencati in precedenza. È necessario completare [parte 1](#aagateway) toocreate e configurare TestVNet1 e hello Gateway VPN con il protocollo BGP. 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a>Passaggio 1: creare TestVNet2 e hello gateway VPN
È importante toomake assicurarsi che lo spazio di indirizzi IP hello di hello nuova rete virtuale, TestVNet2, non si sovrapponga ad altri intervalli di rete virtuale.

In questo esempio, le reti virtuali hello appartengono toohello stessa sottoscrizione. È possibile impostare le connessioni di rete virtuale a tra diverse sottoscrizioni. consultare troppo[configurare una connessione di rete virtuale a](vpn-gateway-vnet-vnet-rm-ps.md) toolearn ulteriori informazioni, vedere. Assicurarsi di aggiungere hello "-EnableBgp $True" quando la creazione di hello tooenable connessioni BGP.

#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili
Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

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

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a>2. Creare il nuovo gruppo di risorse hello TestVNet2

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a>3. Creare i gateway VPN di hello attivo-attivo per TestVNet2
Richiesta due pubblica indirizzi toobe toohello allocato gateway IP che verrà creato per la rete virtuale. Verrà inoltre definire subnet hello e le configurazioni IP necessari.

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

Creare i gateway VPN hello con hello come numero e hello flag "EnableActiveActiveFeature". Si noti che è necessario eseguire l'override di predefinito hello ASN nel gateway VPN di Azure. Hello ASN per hello connessi a reti virtuali devono essere diversi tooenable BGP e il routing di transito.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
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
In questo passaggio si creerà connessione hello da TestVNet1 tooTestVNet2 e connessione hello da TestVNet2 tooTestVNet1.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> Impossibile verificare tooenable BGP per entrambe le connessioni.
> 
> 

Dopo aver completato questi passaggi, stabilirà la connessione hello in pochi minuti e sessione di peering BGP hello sarà backup dopo aver eseguito la connessione di rete virtuale a hello con doppia ridondanza:

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a>Parte 4: aggiornare il gateway esistente tra modalità active-active e active-standby
ultima sezione Hello viene descritto come configurare un gateway VPN di Azure esistente dalla modalità tooactive attivo attivo-standby o viceversa.

> [!NOTE]
> Questa sezione include hello passaggi tooresize uno SKU legacy (SKU precedente) di un gateway VPN già creato da tooHighPerformance Standard. Questi passaggi non aggiornare un vecchio tooone SKU legacy di hello SKU di nuovo.
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a>Configurare un gateway tooactive attivo attivo-standby gateway
#### <a name="1-gateway-parameters"></a>1. Parametri del gateway
Hello di esempio seguente converte un gateway attivo-standby in un gateway attivo-attivo. È necessario toocreate un altro indirizzo IP pubblico, quindi aggiungere una seconda configurazione IP del Gateway. Di seguito viene illustrato hello utilizzati i parametri:

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

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a>2. Creare l'indirizzo IP pubblico hello, quindi aggiungere una configurazione IP del gateway secondo hello

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a>3. Abilitare i gateway di hello modalità e l'aggiornamento attivo-attivo
È necessario impostare l'oggetto gateway hello in aggiornamento effettivo hello tootrigger di PowerShell. Hello SKU di gateway di rete virtuale hello deve essere modificato tooHighPerformance (ridimensionata) quando è stato creato in precedenza come Standard.

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

Questo aggiornamento può richiedere 30 minuti too45.

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a>Configurare un gateway tooactive standby gateway attivo-attivo
#### <a name="1-gateway-parameters"></a>1. Parametri del gateway
Utilizzare hello stesso parametri indicati in precedenza, ottenere il nome di hello della configurazione IP hello desiderata tooremove.

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a>2. Rimuovere una configurazione IP del gateway hello e disabilitare la modalità di hello attivo-attivo
Analogamente, è necessario impostare l'oggetto gateway hello in aggiornamento effettivo hello tootrigger di PowerShell.

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

Questo aggiornamento può richiedere fino too30 troppo 45 minuti.

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .
