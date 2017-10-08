---
title: 'Collegare Azure VPN gateway toomultiple locale basata su criteri VPN dispositivi: Gestione risorse di Azure: PowerShell | Documenti Microsoft'
description: In questo articolo illustra la configurazione di Azure basate su route VPN gateway toomultiple basato su criteri di dispositivi VPN tramite Gestione risorse di Azure e PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a>La connessione VPN di Azure gateway toomultiple locale basata su criteri dispositivi VPN con PowerShell

In questo articolo consente di configurare un Azure basato su route VPN gateway tooconnect toomultiple locale basata su criteri dispositivi VPN sfruttando i criteri IPsec/IKE personalizzati per le connessioni VPN S2S.

## <a name="about-policy-based-and-route-based-vpn-gateways"></a>Informazioni sui gateway VPN basati su criteri e basati su route

Criteri: *e* basato su route dispositivi VPN può variare come i selettori di traffico IPsec hello sono impostati su una connessione:

* **Basata su criteri** dispositivi VPN utilizzano combinazioni di hello di prefissi da entrambi toodefine reti come il traffico è crittografati/decrittografati tramite i tunnel IPsec. Sono basati in genere su dispositivi firewall che eseguono il filtro dei pacchetti. Crittografia e decrittografia IPsec del tunnel vengono aggiunti filtri pacchetti toohello e motore di elaborazione.
* **Basato su route** dispositivi VPN usano selettori di traffico any per qualsiasi (carattere jolly) e consentono di routing/inoltro tabelle i tunnel IPsec toodifferent il traffico diretto. Sono basati in genere su piattaforme router in cui ogni tunnel IPsec è modellato come interfaccia di rete o interfaccia di tunnel virtuale.

Hello nei diagrammi seguenti evidenziare due modelli di hello:

### <a name="policy-based-vpn-example"></a>Esempio di VPN basata su criteri
![basata su criteri](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a>Esempio di VPN basata su route
![basata su route](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a>Supporto di Azure per la VPN basata su criteri
Azure supporta attualmente entrambe le modalità di gateway VPN: gateway VPN basati su route e gateway VPN basati su criteri. Sono basati su piattaforme interne diverse e quindi su specifiche diverse:

|                          | **Gateway VPN basato su criteri** | **Gateway VPN basato su route**               |
| ---                      | ---                         | ---                                      |
| **SKU del gateway di Azure**    | Basic                       | Basic, Standard, HighPerformance         |
| **Versione IKE**          | IKEv1                       | IKEv2                                    |
| **Max. connessioni da sito a sito** | **1**                       | Basic/Standard: 10<br> HighPerformance: 30 |
|                          |                             |                                          |

Con i criteri IPsec/IKE personalizzato di hello, è ora possibile configurare Azure basato su route VPN gateway toouse basata su prefisso selettori di traffico con l'opzione "**PolicyBasedTrafficSelectors**", i dispositivi VPN basata su criteri locali tooon tooconnect. Questa funzionalità consente tooconnect da una rete virtuale di Azure e toomultiple gateway VPN locale basata su criteri dispositivi VPN/firewall, rimuovere il limite di singola connessione hello hello corrente Azure basata su criteri gateway VPN.

> [!IMPORTANT]
> 1. tooenable la connettività, devono supportare i dispositivi VPN basata su criteri di on-premise **IKEv2** tooconnect toohello Azure basato su route gateway VPN. Controllare le specifiche dei dispositivi VPN.
> 2. reti locali Hello connessione tramite i dispositivi VPN basata su criteri con questo meccanismo possono connettersi solo toohello rete virtuale Azure. **Impossibile transito tooother sulle reti locali o reti virtuali tramite hello stesso gateway VPN di Azure**.
> 3. opzione di configurazione Hello fa parte del criterio di connessione IPsec/IKE personalizzata hello. Se si abilita l'opzione selettore di hello traffico basata su criteri, è necessario specificare i criteri di hello completa (algoritmi di crittografia e l'integrità IPsec/IKE chiave punti di forza e durate SA).

Hello seguente diagramma mostra il routing di transito tramite gateway VPN di Azure perché non funziona con l'opzione di hello basata su criteri:

![transito basato su criteri](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

Come illustrato nel diagramma hello, gateway VPN di Azure hello dispone i selettori di traffico da hello tooeach di rete virtuale di prefissi di rete locale hello, ma non i prefissi di hello tra le connessioni. Ad esempio, il sito locale 2, sito 3 e 4 sito può ogni comunicano tooVNet1 rispettivamente, ma non è possibile connettersi tramite hello Azure VPN gateway tooeach altri. viene illustrata l'Hello hello incrociare i selettori di traffico che non sono disponibili in gateway VPN di Azure hello in questa configurazione.

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a>Configurare selettori di traffico basati su criteri in una connessione

Hello istruzioni in seguito in questo articolo hello stesso esempio, come descritto in [criteri IPsec/IKE configurare per le connessioni S2S o di rete virtuale a](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish una connessione VPN S2S. Come illustrato nel seguente diagramma hello:

![s2s-policy](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

Hello tooenable del flusso di lavoro di questo tipo di connettività:
1. Creare la rete virtuale hello, gateway VPN e gateway di rete locale per la connessione tra più sedi locali
2. Creare un criterio IPsec/IKE
3. Applicare i criteri di hello quando si crea una connessione S2S o di rete virtuale a, e **abilitare i selettori di traffico basata su criteri hello** connessione hello
4. Se la connessione hello è già stata creata, è possibile applicare o aggiornare la connessione esistente hello criteri tooan

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a>Abilitare i selettori di traffico basati su criteri in una connessione

Assicurarsi di aver completato [parte 3 dell'articolo di criteri IPsec/IKE configurare hello](vpn-gateway-ipsecikepolicy-rm-powershell.md) per questa sezione. Hello seguente viene illustrato come utilizzare hello stessi parametri e passaggi:

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>Passaggio 1: creare una rete virtuale hello gateway VPN e gateway di rete locale

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a>1. Dichiarare le variabili & connessione tooyour sottoscrizione
Per questo esercizio, si inizierà dichiarando le variabili. Essere certi tooreplace hello i valori con valori personalizzati durante la configurazione per la produzione.

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
hello toouse cmdlet di gestione risorse, accertarsi di passare in modalità tooPowerShell. Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).

Aprire la console di PowerShell e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>2. Creare la rete virtuale hello, gateway VPN e gateway di rete locale
Hello di esempio seguente crea rete virtuale hello, TestVNet1 con tre subnet e il gateway VPN hello. Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente 'GatewaySubnet'. Se si assegnano altri nomi, la creazione del gateway ha esito negativo.

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a>Passaggio 2: Creare una connessione VPN da sito a sito con un criterio IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Creare un criterio IPsec/IKE

> [!IMPORTANT]
> È necessario un criterio IPsec/IKE in ordine tooenable "UsePolicyBasedTrafficSelectors" opzione nella connessione hello toocreate.

Hello seguente viene creato un criterio IPsec/IKE con questi algoritmi e parametri:
* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, durata dell'associazione di sicurezza 3600 secondi e 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a>2. Creare una connessione VPN S2S hello con i selettori di traffico basata su criteri e i criteri IPsec/IKE
Creare una connessione VPN S2S e applicare i criteri IPsec/IKE hello creato nel passaggio precedente hello. Tenere presenti parametri aggiuntivi hello "-UsePolicyBasedTrafficSelectors $True" che consente i selettori di traffico basata su criteri in connessione hello.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

Dopo aver completato i passaggi di hello, hello connessione VPN S2S utilizzare hello definiti criteri IPsec/IKE e abilitare i selettori di traffico basata su criteri in connessione hello. È possibile ripetere hello stessi passaggi tooadd altre connessioni tooadditional locale basata su criteri dispositivi VPN da hello stesso gateway VPN di Azure.

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a>Aggiornare i selettori di traffico basati su criteri per una connessione
Hello ultima sezione viene illustrato come i selettori di traffico basata su criteri hello tooupdate opzione per una connessione VPN S2S esistente.

### <a name="1-get-hello-connection"></a>1. Ottenere la connessione di hello
Ottenere la risorsa di connessione hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a>2. Selezionare opzione di selettori hello traffico basata su criteri
Hello seguente linea indica se i selettori di traffico basata su criteri hello vengono utilizzati per la connessione hello:

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

Se la riga hello restituisce "**True**", quindi i selettori di traffico basata su criteri sono configurati su connessione hello; in caso contrario restituisce "**False**."

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a>3. Aggiornare i selettori di traffico basata su criteri hello in una connessione
Dopo aver ottenuto la risorsa di connessione hello, è possibile abilitare o disabilitare l'opzione hello.

#### <a name="disable-usepolicybasedtrafficselectors"></a>Disabilitare UsePolicyBasedTrafficSelectors
esempio Hello Disabilita opzione selettori di hello traffico basata su criteri, ma lascia hello criteri IPsec/IKE invariato:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a>Abilitare UsePolicyBasedTrafficSelectors
esempio Hello Abilita l'opzione selettori hello traffico basata su criteri, ma lascia hello criteri IPsec/IKE invariato:

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a>Passaggi successivi
Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .

Vedere anche [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) (Configurare i criteri IPsec/IKE per le connessioni da sito a sito o da rete virtuale a rete virtuale) per altre informazioni sui criteri IPsec/IKE personalizzati.
