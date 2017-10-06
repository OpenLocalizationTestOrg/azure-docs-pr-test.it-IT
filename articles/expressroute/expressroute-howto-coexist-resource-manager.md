---
title: 'Configurare connessioni coesistenti ExpressRoute e VPN da sito a sito - Resource Manager: Azure| Microsoft Docs'
description: Questo articolo illustra come configurare connessioni VPN da sito a sito ed ExpressRoute coesistenti per il modello di distribuzione di Azure Resource Manager.
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7717b14-3da3-4a6d-b78e-a5020766bc2c
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: charwen,cherylmc
ms.openlocfilehash: efda9f89d95617c8c4e75af91b20631dc468d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections"></a>Configurare connessioni coesistenti ExpressRoute e da sito a sito
> [!div class="op_single_selector"]
> * [PowerShell - Gestione risorse](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classico](expressroute-howto-coexist-classic.md)
> 
> 

La configurazione di connessioni coesistenti di tipo VPN da sito a sito ed ExpressRoute offre diversi vantaggi. È possibile configurare una VPN da sito a sito come un percorso di failover sicura per ExressRoute o usare una VPN Site-to-Site tooconnect toosites che non sono connessi tramite ExpressRoute. Viene illustrata l'hello passaggi tooconfigure entrambi gli scenari in questo articolo. In questo articolo si applica al modello di distribuzione di gestione delle risorse toohello e utilizza PowerShell. Questa configurazione non è disponibile nel portale di Azure hello.

> [!IMPORTANT]
> Circuiti ExpressRoute devono essere pre-configurati prima di seguire le istruzioni di hello seguenti. Assicurarsi di aver seguito le guide di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-arm.md) e [configurare il routing](expressroute-howto-routing-arm.md) prima di procedere.
> 
> 

## <a name="limits-and-limitations"></a>Limiti e limitazioni
* **L'instradamento del transito non è supportato.** Con Azure non è possibile attivare il routing tra la rete locale connessa tramite la VPN da sito a sito e la rete locale connessa tramite ExpressRoute.
* **Il gateway SKU Basic non è supportato.** È necessario utilizzare un gateway non base SKU per entrambi hello [gateway ExpressRoute](expressroute-about-virtual-network-gateways.md) hello e [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **È supportato solo il gateway VPN basato su route.** È necessario usare un [gateway VPN basato su route](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Deve essere configurata una route statica per il gateway VPN.** Se la rete locale è connesso tooboth ExpressRoute e una Site-to-Site VPN, è necessario disporre una route statica configurata nel toohello di connessione di rete locale tooroute hello Site-to-Site VPN rete Internet pubblica.
* **Gateway ExpressRoute devono essere configurate per prime e collegati tooa circuito.** È necessario creare innanzitutto gateway ExpressRoute hello e collegamento circuito tooa prima di aggiungere gateway VPN Site-to-Site hello.

## <a name="configuration-designs"></a>Progetti di configurazione
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurare una VPN da sito a sito come percorso di failover per ExpressRoute
È possibile configurare una connessione VPN da sito a sito come backup per ExpressRoute. Si applica solo toovirtual reti collegate toohello Azure percorso di peering privato. Non esiste alcuna soluzione di failover basato su VPN per i servizi accessibili tramite i peering pubblico di Azure e Microsoft. Hello circuito ExpressRoute è sempre collegamento primario hello. I dati passano attraverso il percorso VPN Site-to-Site hello solo se hello circuito ExpressRoute ha esito negativo.

> [!NOTE]
> Mentre il circuito ExpressRoute è preferito tramite VPN Site-to-Site quando entrambe le route sono hello stesso, Azure utilizzerà hello più lunga prefisso corrispondenza toochoose hello route verso la destinazione del pacchetto di hello.
> 
> 

![Coesistenza](media/expressroute-howto-coexist-resource-manager/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurare un toosites tooconnect VPN da sito a sito non è connesso tramite ExpressRoute
È possibile configurare la rete in cui alcuni siti si connettono direttamente tooAzure tramite VPN Site-to-Site e alcuni siti si connettono tramite ExpressRoute. 

![Coesistenza](media/expressroute-howto-coexist-resource-manager/scenario2.jpg)

> [!NOTE]
> Non è possibile configurare una rete virtuale come router di transito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Selezione di hello passaggi toouse
Esistono due diversi set di procedure toochoose da. procedura di configurazione di Hello selezionato dipende se si dispone di una rete virtuale esistente che si desidera tooconnect a o si desidera toocreate una nuova rete virtuale.

* Non dispone di una rete virtuale e necessario toocreate uno.
  
    Se non è disponibile una rete virtuale, questa procedura consente la creazione di una nuova rete virtuale e di nuove connessioni ExpressRoute e VPN da sito a sito usando il modello di distribuzione di Resource Manager. tooconfigure una rete virtuale, seguire i passaggi hello [toocreate una nuova rete virtuale e le connessioni coesistenti](#new).
* È già disponibile una rete virtuale con modello di distribuzione di Azure Resource Manager.
  
    E’ possibile che esista già una rete virtuale con una connessione VPN da sito a sito o una connessione ExpressRoute. Hello [tooconfigure connessioni coesistenti per una rete virtuale di già esistente](#add) sezione disponibili informazioni dettagliate sull'eliminazione del gateway hello e quindi la creazione di nuove connessioni di VPN Site-to-Site ed ExpressRoute. Quando si creano hello nuove connessioni, è necessario completare i passaggi di hello in un ordine specifico. Non utilizzare istruzioni hello toocreate altri articoli del gateway e connessioni.
  
    In questa procedura, la creazione di connessioni che possono coesistere richiede toodelete è il gateway e quindi configurare nuovi gateway. È tempo di inattività per le connessioni cross-premise mentre eliminare e ricreare il gateway e connessioni, ma non è necessario toomigrate le macchine virtuali o servizi tooa nuova rete virtuale. Le macchine virtuali e servizi sarà comunque in grado di toocommunicate out tramite bilanciamento del carico hello durante la configurazione del gateway se sono pertanto toodo configurato.

## <a name="new"></a>connessioni coesistenti e toocreate una nuova rete virtuale
Questa procedura illustra come creare una rete virtuale e connessioni da sito a sito ed ExpressRoute coesistenti.

1. Installare hello l'ultima versione di hello cmdlet di Azure PowerShell. Per informazioni sull'installazione hello cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Hello cmdlet da utilizzare per questa configurazione potrebbe essere leggermente diverso rispetto a ciò che potrebbe acquisire familiarità con. I cmdlet di hello toouse che è possibile specificare in queste istruzioni.
2. Accedi tooyour account e configurare un ambiente di hello.

  ```powershell
  login-AzureRmAccount
  Select-AzureRmSubscription -SubscriptionName 'yoursubscription'
  $location = "Central US"
  $resgrp = New-AzureRmResourceGroup -Name "ErVpnCoex" -Location $location
  $VNetASN = 65010
  ```
3. Creare una rete virtuale con una subnet del gateway. Per ulteriori informazioni sulla configurazione di rete virtuale hello, vedere [configurazione di rete virtuale di Azure](../virtual-network/virtual-networks-create-vnet-arm-ps.md).
   
   > [!IMPORTANT]
   > Hello Subnet del Gateway deve essere /27 o un prefisso (ad esempio /26 o /25) più breve.
   > 
   > 
   
    Creare una nuova rete virtuale.

  ```powershell
  $vnet = New-AzureRmVirtualNetwork -Name "CoexVnet" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AddressPrefix "10.200.0.0/16"
  ```
   
    Aggiungere le subnet.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name "App" -VirtualNetwork $vnet -AddressPrefix "10.200.1.0/24"
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salvare la configurazione di rete virtuale hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
4. <a name="gw"></a>Creare un gateway ExpressRoute. Per ulteriori informazioni sulla configurazione di gateway ExpressRoute hello, vedere [configurazione del gateway ExpressRoute](expressroute-howto-add-gateway-resource-manager.md). Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "ERGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "ERGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  $gw = New-AzureRmVirtualNetworkGateway -Name "ERGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "ExpressRoute" -GatewaySku Standard
  ```
5. Collegare il circuito ExpressRoute toohello di hello ExpressRoute gateway. Dopo questo passaggio è stato completato, viene stabilita connessione hello tra la rete locale e Azure tramite ExpressRoute. Per ulteriori informazioni sull'operazione di collegamento hello, vedere [tooExpressRoute reti virtuali collegamento](expressroute-howto-linkvnet-arm.md).

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "YourCircuit" -ResourceGroupName "YourCircuitResourceGroup"
  New-AzureRmVirtualNetworkGatewayConnection -Name "ERConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $gw -PeerId $ckt.Id -ConnectionType ExpressRoute
  ```
6. <a name="vpngw"></a>Creare quindi il gateway VPN da sito a sito. Per ulteriori informazioni sulla configurazione del gateway VPN hello, vedere [configurare una rete virtuale con una connessione Site-to-Site](../vpn-gateway/vpn-gateway-create-site-to-site-rm-powershell.md). Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance*. necessario Hello VpnType *tipo RouteBased*.

  ```powershell
  $gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $gwIP = New-AzureRmPublicIpAddress -Name "VPNGatewayIP" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -AllocationMethod Dynamic
  $gwConfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "VPNGatewayIpConfig" -SubnetId $gwSubnet.Id -PublicIpAddressId $gwIP.Id
  New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard"
  ```
   
    Il gateway VPN di Azure supporta il protocollo di routing BGP. È possibile specificare ASN (numero AS) per la rete virtuale tramite l'aggiunta di switch - Asn hello in hello comando seguente. Non specificare questo parametro verrà tooAS predefinito numero 65515.

  ```powershell
  $azureVpn = New-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -IpConfigurations $gwConfig -GatewayType "Vpn" -VpnType "RouteBased" -GatewaySku "Standard" -Asn $VNetASN
  ```
   
    È possibile trovare hello IP peer BGP e hello sotto forma di numero utilizzato da Azure per il gateway VPN hello in $azureVpn.BgpSettings.BgpPeeringAddress e $azureVpn.BgpSettings.Asn. Per altre informazioni, vedere [Configurare BGP](../vpn-gateway/vpn-gateway-bgp-resource-manager-ps.md) per il gateway VPN di VPN.
7. Creare un'entità gateway VPN del sito locale. Questo comando non configura il gateway VPN locale. Invece, consente di impostazioni del gateway locale hello tooprovide, ad esempio indirizzo IP pubblico hello e hello locale lo spazio degli indirizzi, in modo che hello gateway VPN di Azure può connettersi tooit.
   
    Se il dispositivo VPN locale supporta solo il routing statico, è possibile configurare le route statiche hello in hello seguente modo:

  ```powershell
  $MyLocalNetworkAddress = @("10.100.0.0/16","10.101.0.0/16","10.102.0.0/16")
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress *<Public IP>* -AddressPrefix $MyLocalNetworkAddress
  ```
   
    Se il dispositivo VPN locale supporta hello BGP e si desidera tooenable il routing dinamico, è necessario tooknow hello BGP peering IP e hello come numero la VPN locale dispositivo usa.

  ```powershell
  $localVPNPublicIP = "<Public IP>"
  $localBGPPeeringIP = "<Private IP for hello BGP session>"
  $localBGPASN = "<ASN>"
  $localAddressPrefix = $localBGPPeeringIP + "/32"
  $localVpn = New-AzureRmLocalNetworkGateway -Name "LocalVPNGateway" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -GatewayIpAddress $localVPNPublicIP -AddressPrefix $localAddressPrefix -BgpPeeringAddress $localBGPPeeringIP -Asn $localBGPASN
  ```
8. Configurare il gateway VPN locale dispositivo tooconnect toohello nuovo VPN di Azure. Per altre informazioni sulla configurazione del dispositivo VPN, vedere l'articolo relativo alla [configurazione del dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
9. Collegamento hello Site-to-Site VPN gateway in gateway locale toohello Azure.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  New-AzureRmVirtualNetworkGatewayConnection -Name "VPNConnection" -ResourceGroupName $resgrp.ResourceGroupName -Location $location -VirtualNetworkGateway1 $azureVpn -LocalNetworkGateway2 $localVpn -ConnectionType IPsec -SharedKey <yourkey>
  ```

## <a name="add"></a>connessioni coesistenti tooconfigure per una rete virtuale di già esistente
Se si dispone di una rete virtuale esistente, è possibile controllare la dimensione della subnet gateway hello. Se subnet del gateway hello /28 o /29, è necessario eliminare il gateway di rete virtuale hello e aumentare la dimensione della subnet gateway hello. Hello passaggi in questa sezione viene illustrato come toodo che.

Se subnet del gateway hello è /27 o superiore e la rete virtuale hello è connesso tramite ExpressRoute, è possibile ignorare i passaggi di hello riportati di seguito e andare troppo["Passaggio 6: creare un gateway VPN da sito a sito"](#vpngw) nella sezione precedente hello. 

> [!NOTE]
> Quando si elimina gateway esistente hello, sedi locali perderà rete virtuale tooyour hello mentre si lavora in questa configurazione. 
> 
> 

1. È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell. Per ulteriori informazioni sull'installazione di cmdlet, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview). Hello cmdlet da utilizzare per questa configurazione potrebbe essere leggermente diverso rispetto a ciò che potrebbe acquisire familiarità con. I cmdlet di hello toouse che è possibile specificare in queste istruzioni. 
2. Eliminare il gateway ExpressRoute o VPN da sito a sito esistente hello.

  ```powershell 
  Remove-AzureRmVirtualNetworkGateway -Name <yourgatewayname> -ResourceGroupName <yourresourcegroup>
  ```
3. Eliminare la subnet del gateway.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup> Remove-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet -VirtualNetwork $vnet
  ```
4. Aggiungere una subnet del gateway di /27 o superiore.
   
   > [!NOTE]
   > Se non si dispone di indirizzi IP sufficiente la dimensione di subnet gateway di rete virtuale tooincrease hello a sinistra, è necessario tooadd più spazio di indirizzi IP.
   > 
   > 

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name <yourvnetname> -ResourceGroupName <yourresourcegroup>
  Add-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet -AddressPrefix "10.200.255.0/24"
  ```
   
    Salvare la configurazione di rete virtuale hello.

  ```powershell
  $vnet = Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
5. A questo punto, si ha una rete virtuale senza gateway. toocreate nuovi gateway e completare le connessioni, è possibile procedere con [passaggio 4: creare un gateway ExpressRoute](#gw), trovato in hello precedente set di passaggi.

## <a name="tooadd-point-to-site-configuration-toohello-vpn-gateway"></a>gateway VPN di tooadd configurazione point-to-site toohello
È possibile eseguire operazioni di hello seguenti gateway VPN di tooyour tooadd Point-to-Site configurazione in una configurazione di coesistenza.

1. Aggiungere un pool di indirizzi client VPN.

  ```powershell
  $azureVpn = Get-AzureRmVirtualNetworkGateway -Name "VPNGateway" -ResourceGroupName $resgrp.ResourceGroupName
  Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $azureVpn -VpnClientAddressPool "10.251.251.0/24"
  ```
2. Caricare hello tooAzure certificato radice VPN del gateway VPN. In questo esempio si presuppone che il certificato radice hello viene archiviato nel computer locale di hello in cui viene eseguito hello seguendo i cmdlet di PowerShell.

  ```powershell
  $p2sCertFullName = "RootErVpnCoexP2S.cer" 
  $p2sCertMatchName = "RootErVpnCoexP2S" 
  $p2sCertToUpload=get-childitem Cert:\CurrentUser\My | Where-Object {$_.Subject -match $p2sCertMatchName} 
  if ($p2sCertToUpload.count -eq 1){write-host "cert found"} else {write-host "cert not found" exit} 
  $p2sCertData = [System.Convert]::ToBase64String($p2sCertToUpload.RawData) Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $p2sCertFullName -VirtualNetworkGatewayname $azureVpn.Name -ResourceGroupName $resgrp.ResourceGroupName -PublicCertData $p2sCertData
  ```

Per altre informazioni sulle VPN da punto a sito, vedere [Configurare una connessione da punto a sito](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md).

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md).
