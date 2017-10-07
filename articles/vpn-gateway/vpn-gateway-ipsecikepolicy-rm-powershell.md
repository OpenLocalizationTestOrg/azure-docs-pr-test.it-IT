---
title: 'Configurare i criteri IPsec/IKE per le connessioni VPN da sito a sito o da rete virtuale a rete virtuale: Azure Resource Manager: PowerShell | Microsoft Docs'
description: In questo articolo viene illustrata la configurazione di criteri IPsec/IKE per connessioni da sito a sito o da rete virtuale a rete virtuale con i gateway VPN di Azure tramite Azure Resource Manager e PowerShell.
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
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a>Configurare criteri IPsec/IKE per connessioni VPN da sito a sito o da rete virtuale a rete virtuale

In questo articolo illustra i passaggi di hello tooconfigure criteri IPsec/IKE per le connessioni VPN da sito a sito o di rete virtuale a con modello di distribuzione di gestione risorse di hello e PowerShell.

## <a name="about"></a>Informazioni sui parametri dei criteri IPsec e IKE per gateway VPN di Azure
Lo standard di protocollo IPsec e IKE supporta un'ampia gamma di algoritmi di crittografia in varie combinazioni. Fare riferimento troppo[sui requisiti di crittografia e i gateway VPN di Azure](vpn-gateway-about-compliance-crypto.md) toosee come questo consente di garantire cross-premise e la connettività di rete virtuale a soddisfare i requisiti di conformità o la sicurezza.

In questo articolo fornisce istruzioni toocreate e configurare un criterio IPsec/IKE e applicare una connessione nuova o esistente tooa:

* [Parte 1 - toocreate del flusso di lavoro e impostare i criteri IPsec/IKE](#workflow)
* [Parte 2: Algoritmi di crittografia supportati e vantaggi chiave](#params)
* [Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE](#crossprem)
* [Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE](#vnet2vnet)
* [Parte 5: Gestire (creare, aggiungere, rimuovere) criteri IPsec/IKE per una connessione](#managepolicy)

> [!IMPORTANT]
> 1. Si noti che i criteri IPsec/IKE funziona solo su hello SKU di gateway di seguito:
>    * ***VpnGw1, VpnGw2, VpnGw3*** (basato su route)
>    * ***Standard*** e ***HighPerformance*** (basato su route)
> 2. Per una determinata connessione è possibile specificare ***una*** sola combinazione di criteri.
> 3. È necessario specificare tutti gli algoritmi e i parametri sia per IKE (modalità principale) che per IPsec (modalità rapida). Non è consentito specificare criteri parziali.
> 4. Consultare le specifiche di fornitore dispositivo VPN criteri hello tooensure sono supportato nei dispositivi VPN locali. S2S o connessioni di rete virtuale a non è possibile stabilire se i criteri di hello non sono compatibili.

## <a name ="workflow"></a>Parte 1 - toocreate del flusso di lavoro e impostare i criteri IPsec/IKE
Questa sezione vengono descritti hello del flusso di lavoro toocreate e aggiornamento IPsec/IKE criteri su una connessione VPN S2S o di rete virtuale a:
1. Creare una rete virtuale e un gateway VPN
2. Creare un gateway di rete locale per una connessione cross-premises o un'altra rete virtuale e gateway per una connessione da rete virtuale a rete virtuale
3. Creare un criterio IPsec/IKE con gli algoritmi e i parametri selezionati
4. Creare una connessione VNet2VNet (IPsec) con i criteri IPsec/IKE hello
5. Aggiungere, aggiornare o rimuovere un criterio IPsec/IKE per una connessione esistente

istruzioni di Hello in questo articolo consente di impostare e configurare i criteri IPsec/IKE, come illustrato nel diagramma hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <a name ="params"></a>Parte 2: Algoritmi di crittografia supportati e vantaggi chiave

Hello nella tabella seguente sono elencati gli algoritmi di crittografia supportato hello e vantaggi chiave configurabile da parte dei clienti hello:

| **IPsec/IKEv2**  | **Opzioni**    |
| ---  | --- 
| Crittografia IKEv2 | AES256, AES192, AES128, DES3, DES  
| Integrità IKEv2  | SHA384, SHA256, SHA1, MD5  |
| Gruppo DH         | DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None |
| Crittografia IPsec | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None    |
| Integrità IPsec  | GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5 |
| Gruppo PFS        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None 
| Durata associazione di sicurezza in modalità rapida   | (**Facoltativo**: se non diversamente specificato, vengono usati i valori predefiniti)<br>Secondi (intero; **min. 300**/valore predefinito di 27000 secondi)<br>Kilobyte (intero; **min 1024**/valore predefinito di 102400000 KB)   |
| Selettore di traffico | UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, $False predefinito, se non diversamente specificato)    |
|  |  |

> [!IMPORTANT]
> 1. **Se GCMAES viene usato per l'algoritmo di crittografia IPsec, è necessario selezionare hello stesso algoritmo GCMAES e lunghezza della chiave per l'integrità IPsec; ad esempio, l'uso di GCMAES128 per entrambe**
> 2. Durata SA modalità principale di IKEv2 è fissata a 28.800 secondi nei gateway VPN di Azure hello
> 3. L'impostazione "UsePolicyBasedTrafficSelectors" troppo$ True in una connessione configurerà hello Azure VPN gateway tooconnect toopolicy firewall basato su VPN in locale. Se si abilita PolicyBasedTrafficSelectors, è necessario il dispositivo VPN è hello corrispondente selettori di traffico definiti con tutte le combinazioni del locale (gateway di rete locale) dei prefissi di rete da e verso i prefissi di rete virtuale di Azure, hello tooensure anziché any-a-qualsiasi. Ad esempio, se i prefissi di rete locale sono 10.1.0.0/16 e 10.2.0.0/16 e i prefissi di rete virtuale sono 192.168.0.0/16 e 172.16.0.0/16, è necessario hello toospecify selettori di traffico seguenti:
>    * 10.1.0.0/16 <====> 192.168.0.0/16
>    * 10.1.0.0/16 <====> 172.16.0.0/16
>    * 10.2.0.0/16 <====> 192.168.0.0/16
>    * 10.2.0.0/16 <====> 172.16.0.0/16

Per altre informazioni sui selettori di traffico basati su criteri, vedere [Connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Nella seguente sono elencati nella tabella Hello hello corrispondente gruppi Diffie-Hellman supportato dai criteri personalizzati di hello:

| **Gruppo Diffie-Hellman**  | **DHGroup**              | **PFSGroup** | **Lunghezza chiave** |
| --- | --- | --- | --- |
| 1                         | DHGroup1                 | PFS1         | MODP a 768 bit   |
| 2                         | DHGroup2                 | PFS2         | MODP a 1024 bit  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | MODP a 2048 bit  |
| 19                        | ECP256                   | ECP256       | ECP a 256 bit    |
| 20                        | ECP384                   | ECP284       | ECP a 384 bit    |
| 24                        | DHGroup24                | PFS24        | MODP a 2048 bit  |

Fare riferimento troppo[RFC3526](https://tools.ietf.org/html/rfc3526) e [RFC5114](https://tools.ietf.org/html/rfc5114) per altri dettagli.

## <a name ="crossprem"></a>Parte 3: Creare una nuova connessione VPN da sito a sito con criteri IPsec/IKE

In questa sezione vengono illustrati i passaggi hello di creazione di una connessione VPN S2S con un criterio IPsec/IKE. Hello seguito crea hello connessione come illustrato nel diagramma hello:

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

Per altre istruzioni dettagliate per la creazione di una connessione VPN da sito a sito, vedere [Creare una connessione VPN da sito a sito](vpn-gateway-create-site-to-site-rm-powershell.md).

### <a name="before"></a>Prima di iniziare

* Verificare di possedere una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* Installare i cmdlet di PowerShell di gestione risorse di Azure hello. Vedere [Panoramica di Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.

### <a name="createvnet1"></a>Passaggio 1: creare una rete virtuale hello gateway VPN e gateway di rete locale

#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a>2. Connettere tooyour sottoscrizione e creare un nuovo gruppo di risorse

Accertarsi di passare hello toouse di modalità tooPowerShell cmdlet di gestione risorse. Per altre informazioni, vedere [Uso di Windows PowerShell con Gestione risorse](../powershell-azure-resource-manager.md).

Aprire la console di PowerShell e tooyour account di connessione. Utilizzare hello toohelp esempio che ci si connette seguenti:

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a>3. Creare la rete virtuale hello, gateway VPN e gateway di rete locale

Hello seguente esempio crea rete virtuale di hello, TestVNet1, con tre subnet e il gateway VPN hello. Quando si sostituiscono i valori, è importante che la subnet gateway venga denominata sempre esattamente GatewaySubnet. Se si assegnano altri nomi, la creazione del gateway ha esito negativo.

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

### <a name="s2sconnection"></a>Passaggio 2: Creare una connessione VPN da sito a sito con un criterio IPsec/IKE

#### <a name="1-create-an-ipsecike-policy"></a>1. Creare un criterio IPsec/IKE

Hello lo script di esempio seguente crea un criterio IPsec/IKE con hello seguenti algoritmi e parametri:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: AES256, SHA256, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

Se si utilizza GCMAES per IPsec, è necessario utilizzare hello stesso algoritmo GCMAES e lunghezza della chiave per la crittografia di IPsec e integrità, ad esempio:

* IKEv2: AES256, SHA384, DHGroup24
* IPsec: **GCMAES256, GCMAES256**, PFS24, durata dell'associazione di sicurezza 7200 secondi e 2048 KB

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a>2. Creare una connessione VPN S2S hello con hello criteri IPsec/IKE

Creare una connessione VPN S2S e applicare i criteri IPsec/IKE hello creato in precedenza.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

È possibile aggiungere facoltativamente "-UsePolicyBasedTrafficSelectors $True" toohello creare connessione cmdlet tooenable Azure VPN gateway tooconnect toopolicy dispositivi basati su VPN in locale, come descritto in precedenza.

> [!IMPORTANT]
> Una volta specificato una connessione di un criterio IPsec/IKE, gateway VPN di Azure hello solo invierà o accettare hello IPsec/IKE proposta con gli algoritmi di crittografia specificati e per i livelli di chiave in tale particolare connessione. Assicurarsi che il dispositivo VPN locale per la connessione hello utilizza o accetta combinazione esatta criteri hello, in caso contrario non stabilisce tunnel VPN S2S hello.


## <a name ="vnet2vnet"></a>Parte 4: Creare una nuova connessione da rete virtuale a rete virtuale con criteri IPsec/IKE

passaggi di Hello di creazione di una connessione di rete virtuale a con un criterio IPsec/IKE sono simili toothat di una connessione VPN S2S. Hello seguente script di esempio creare hello connessione come illustrato nel diagramma hello:

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

Per la procedura dettagliata di creazione di una connessione da rete virtuale a rete virtuale, vedere [Creare una connessione tra reti virtuali](vpn-gateway-vnet-vnet-rm-ps.md) . È necessario completare [parte 3](#crossprem) toocreate e configurare TestVNet1 e hello Gateway VPN.

### <a name="createvnet2"></a>Passaggio 1: creare una seconda rete virtuale hello e gateway VPN

#### <a name="1-declare-your-variables"></a>1. Dichiarare le variabili

Essere tooreplace che i valori hello con hello quelli che si desidera toouse per la configurazione.

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a>2. Creare seconda rete virtuale hello e gateway VPN nel nuovo gruppo di risorse hello

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a>Passaggio 2: creare una connessione di rete virtuale toVNet con hello criteri IPsec/IKE

Toohello simile connessione VPN S2S, creare un criterio IPsec/IKE, applicare toopolicy toohello nuova connessione.

#### <a name="1-create-an-ipsecike-policy"></a>1. Creare un criterio IPsec/IKE

Hello lo script di esempio seguente crea un criterio IPsec/IKE diverso con hello seguenti algoritmi e parametri:
* IKEv2: AES128, SHA1, DHGroup14
* IPsec: GCMAES128, GCMAES128, PFS14, durata dell'associazione di sicurezza 7200 secondi e 4096 KB

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a>2. Creare connessioni di rete virtuale a con hello criteri IPsec/IKE

Creare una connessione di rete e applicare criteri IPsec/IKE hello creati. In questo esempio, entrambi i gateway sono in hello stessa sottoscrizione. È possibile toocreate e configurare entrambe le connessioni con hello stesso criterio IPsec/IKE in hello stessa sessione di PowerShell.

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> Una volta specificato una connessione di un criterio IPsec/IKE, gateway VPN di Azure hello solo invierà o accettare hello IPsec/IKE proposta con gli algoritmi di crittografia specificati e per i livelli di chiave in tale particolare connessione. Verificare che hello criteri IPsec per entrambe le connessioni sono hello stesso, in caso contrario non stabilisce la connessione di rete virtuale a.

Dopo aver completato questi passaggi, hello connessione tra qualche minuto e sarà necessario dopo la topologia della rete, come illustrato in inizio hello hello:

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <a name ="managepolicy"></a>Parte 5: Aggiornare i criteri IPsec/IKE per una connessione

ultima sezione Hello illustra come toomanage criteri IPsec/IKE per una connessione esistente S2S o di rete virtuale a. esercizio Hello riportato di seguito illustra hello dopo le operazioni su una connessione:

1. Mostra i criteri IPsec/IKE hello di una connessione
2. Aggiungere o aggiornare la connessione di tooa criteri IPsec/IKE hello
3. Rimuovere i criteri IPsec/IKE hello da una connessione

Hello stessi passaggi si applicano tooboth S2S e le connessioni di rete virtuale a.

> [!IMPORTANT]
> Il criterio IPsec/IKE è supportato solo nei gateway VPN *Standard* e *Prestazioni elevate* basati su route di Azure. Non funziona su gateway Basic hello SKU o gateway VPN basata su criteri di hello.

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a>1. Mostra i criteri IPsec/IKE hello di una connessione

Hello di esempio seguente viene illustrato come tooget hello criteri IPsec/IKE configurato su una connessione. gli script di Hello continuano anche da esercizi hello precedenti.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

ultimo comando Hello sono elencati i criteri IPsec/IKE correnti hello configurato nella connessione hello, se è presente uno. Hello output di esempio seguente è per la connessione hello:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

Se non è configurato alcun criterio IPsec/IKE, hello comando (PS > $connection6.policy) Ottiene un oggetto vuoto restituito. Ciò significa IPsec/IKE non è configurato nella connessione di hello, ma che non vi sia alcun criterio IPsec/IKE personalizzato. connessione effettiva Hello utilizza criteri predefiniti hello negoziato tra il dispositivo VPN locale e hello gateway VPN di Azure.

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a>2. Aggiungere o aggiornare un criterio IPsec/IKE per una connessione

Hello passaggi tooadd un nuovo criterio o aggiornamento di un criterio esistente in una connessione sono hello stesso: creare un nuovo criterio, quindi applicare una nuova connessione di toohello criteri hello.

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

tooenable "UsePolicyBasedTrafficSelectors" quando la connessione tooan locale dispositivo VPN basata su criteri, aggiungere hello "-UsePolicyBaseTrafficSelectors" parametro toohello cmdlet o impostarlo troppo opzione hello di $ toodisable False:

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

È possibile ottenere la connessione hello nuovamente toocheck se hello criteri vengono aggiornati.

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

Verrà visualizzato l'output di hello dall'ultima riga hello, come illustrato nell'esempio seguente hello:

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a>3. Rimuovere un criterio IPsec/IKE da una connessione

Dopo aver rimosso i criteri personalizzati di hello da una connessione, gateway VPN di Azure hello torna indietro toohello [elenco predefinito delle proposte di IPsec/IKE](vpn-gateway-about-vpn-devices.md) e nuovamente negozia con il dispositivo VPN locale.

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

È possibile utilizzare hello toocheck script stesso, se il criterio di hello è stato rimosso dalla connessione hello.

## <a name="next-steps"></a>Passaggi successivi

Per altri dettagli sui selettori di traffico basati su criteri, vedere l'articolo su come [connettere più dispositivi VPN basati su criteri locali](vpn-gateway-connect-multiple-policybased-rm-ps.md).

Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Per i passaggi, vedere [Creare la prima macchina virtuale](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) .
