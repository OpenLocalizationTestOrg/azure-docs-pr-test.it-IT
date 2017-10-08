---
title: 'Configurare il tunneling forzato per connessioni di Azure da sito a sito: Resource Manager | Microsoft Docs'
description: Come tooredirect o 'force' tutti tooyour di sfondo del traffico associato a Internet posizione locale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cbe58db8-b598-4c9f-ac88-62c865eb8721
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: cherylmc
ms.openlocfilehash: 6bc52c04ab0749a674c9863be5e4f9a9f7c98df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-azure-resource-manager-deployment-model"></a>Configurare il tunneling forzato con modello di distribuzione Azure Resource Manager hello

Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato. Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali. Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure sempre attraversa dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit. Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)] 

In questo articolo illustra la configurazione forzato tunneling per le reti virtuali create con modello di distribuzione di gestione risorse di hello. Il tunneling forzato può essere configurato tramite PowerShell, non tramite il portale di hello. Se si desidera tooconfigure tunneling per il modello di distribuzione classica hello forzato, è possibile selezionare articolo classico da hello segue l'elenco a discesa:

> [!div class="op_single_selector"]
> * [PowerShell - Classico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Gestione risorse](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="about-forced-tunneling"></a>Informazioni sul tunneling forzato

Hello seguente diagramma illustra il funzionamento del tunneling forzato. 

![Tunneling forzato](./media/vpn-gateway-forced-tunneling-rm/forced-tunnel.png)

Nell'esempio riportato sopra, hello hello tunneled front-end subnet non è forzato. i carichi di lavoro Hello nella subnet front-end hello continuare tooaccept e rispondere toocustomer richieste da hello Internet direttamente. Hello subnet di livello intermedio e back-end devono essere forzate tunnel. Tutte le connessioni in uscita da tali toohello due subnet Internet sarà tooan forzata o reindirizzato nuovamente nel sito locale tramite uno dei tunnel VPN S2S hello.

Questo consente toorestrict e controllare l'accesso a Internet dalle macchine virtuali o nel cloud servizi in Azure, continuando tooenable l'architettura del servizio a più livelli necessaria. Se sono non presenti carichi di lavoro con connessione Internet nelle reti virtuali, è possibile applicare forzato tunneling toohello intere reti virtuali.

## <a name="requirements-and-considerations"></a>Problemi e considerazioni

Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente. Reindirizzamento del traffico tooan locale sito viene espresso come un gateway VPN di Azure toohello di Route predefinita. Per altre informazioni sulle route definite dall'utente e sulle reti virtuali, vedere [Route definite dall'utente e inoltro IP](../virtual-network/virtual-networks-udr-overview.md).

* Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata. tabella di routing sistema Hello è hello seguenti tre gruppi di route:
  
  * **Route di rete virtuale locale:** direttamente toohello destinazione macchine virtuali in hello stessa rete virtuale.
  * **Le route locali:** gateway VPN di Azure toohello.
  * **Route predefinita:** direttamente toohello Internet. I pacchetti destinati toohello gli indirizzi IP privati non coperti da route hello due precedenti vengono eliminati.
* Questa procedura utilizza le route definite dall'utente (UDR) toocreate un tooadd tabella di routing una route predefinita e quindi associare hello routing tabella tooyour rete virtuale subnet tooenable forzato tunneling su queste subnet.
* Il tunneling forzato deve essere associato a una rete virtuale con un gateway VPN basato su route. È necessario un sito"predefinito" tooset tra rete virtuale connessa toohello hello cross-premise siti locali. Inoltre, hello locale dispositivo VPN deve essere configurato utilizzando 0.0.0.0/0 come selettori di traffico. 
* Il tunneling forzato ExpressRoute non viene configurato tramite questo meccanismo, ma è invece abilitato annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering. Per ulteriori informazioni, vedere hello [documentazione di ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/).

## <a name="configuration-overview"></a>Panoramica della configurazione

Hello seguente procedura consente di creare un gruppo di risorse e una rete virtuale. Si passerà quindi alla creazione di un gateway VPN e alla configurazione del tunneling forzato. In questa procedura, dispone di tre subnet rete virtuale hello 'MultiTier-VNet': 'Front-end', 'Midtier' e 'Back-end', con quattro connessioni più sedi: 'DefaultSiteHQ' e tre rami.

procedura Hello imposta hello 'DefaultSiteHQ' come connessione di hello predefinita del sito per il tunneling forzato e configurare hello 'Midtier' e 'Back-end' subnet toouse il tunneling forzato.

## <a name="before-you-begin"></a>Prima di iniziare

Installare hello l'ultima versione di hello cmdlet PowerShell di gestione risorse di Azure. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.

### <a name="toolog-in"></a>toolog in

[!INCLUDE [toolog in](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="configure-forced-tunneling"></a>È possibile configurare il tunneling forzato?

1. Creare un gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name 'ForcedTunneling' -Location 'North Europe'
  ```
2. Creare una rete virtuale e specificare le subnet.

  ```powershell 
  $s1 = New-AzureRmVirtualNetworkSubnetConfig -Name "Frontend" -AddressPrefix "10.1.0.0/24"
  $s2 = New-AzureRmVirtualNetworkSubnetConfig -Name "Midtier" -AddressPrefix "10.1.1.0/24"
  $s3 = New-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -AddressPrefix "10.1.2.0/24"
  $s4 = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix "10.1.200.0/28"
  $vnet = New-AzureRmVirtualNetwork -Name "MultiTier-VNet" -Location "North Europe" -ResourceGroupName "ForcedTunneling" -AddressPrefix "10.1.0.0/16" -Subnet $s1,$s2,$s3,$s4
  ```
3. Creare hello gateway di rete locale.

  ```powershell
  $lng1 = New-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.111" -AddressPrefix "192.168.1.0/24"
  $lng2 = New-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.112" -AddressPrefix "192.168.2.0/24"
  $lng3 = New-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.113" -AddressPrefix "192.168.3.0/24"
  $lng4 = New-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -GatewayIpAddress "111.111.111.114" -AddressPrefix "192.168.4.0/24"
  ```
4. Creare una regola route e di tabella di route hello.

  ```powershell
  New-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" –Location "North Europe"
  $rt = Get-AzureRmRouteTable –Name "MyRouteTable" -ResourceGroupName "ForcedTunneling" 
  Add-AzureRmRouteConfig -Name "DefaultRoute" -AddressPrefix "0.0.0.0/0" -NextHopType VirtualNetworkGateway -RouteTable $rt
  Set-AzureRmRouteTable -RouteTable $rt
  ```
5. Associare hello route tabella toohello Midtier e subnet di back-end.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name "MultiTier-Vnet" -ResourceGroupName "ForcedTunneling"
  Set-AzureRmVirtualNetworkSubnetConfig -Name "MidTier" -VirtualNetwork $vnet -AddressPrefix "10.1.1.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetworkSubnetConfig -Name "Backend" -VirtualNetwork $vnet -AddressPrefix "10.1.2.0/24" -RouteTable $rt
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```
6. Creare hello Gateway con un sito predefinito. Questo passaggio accetta alcuni toocomplete tempo, in alcuni casi a 45 minuti o più, perché la creazione e la configurazione di gateway hello.<br> Hello **- GatewayDefaultSite** è hello parametro del cmdlet che consente di hello forzato routing toowork di configurazione, fare attenzione tooconfigure questa impostazione in modo corretto. Questo parametro è disponibile solo in PowerShell 1.0 o versioni successive.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name "GatewayIP" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -AllocationMethod Dynamic
  $gwsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  $ipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name "gwIpConfig" -SubnetId $gwsubnet.Id -PublicIpAddressId $pip.Id
  New-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -IpConfigurations $ipconfig -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -GatewayDefaultSite $lng1 -EnableBgp $false
  ```
7. Stabilire le connessioni VPN da sito a sito hello.

  ```powershell
  $gateway = Get-AzureRmVirtualNetworkGateway -Name "Gateway1" -ResourceGroupName "ForcedTunneling"
  $lng1 = Get-AzureRmLocalNetworkGateway -Name "DefaultSiteHQ" -ResourceGroupName "ForcedTunneling" 
  $lng2 = Get-AzureRmLocalNetworkGateway -Name "Branch1" -ResourceGroupName "ForcedTunneling" 
  $lng3 = Get-AzureRmLocalNetworkGateway -Name "Branch2" -ResourceGroupName "ForcedTunneling" 
  $lng4 = Get-AzureRmLocalNetworkGateway -Name "Branch3" -ResourceGroupName "ForcedTunneling" 
    
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng1 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection2" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng2 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection3" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng3 -ConnectionType IPsec -SharedKey "preSharedKey"
  New-AzureRmVirtualNetworkGatewayConnection -Name "Connection4" -ResourceGroupName "ForcedTunneling" -Location "North Europe" -VirtualNetworkGateway1 $gateway -LocalNetworkGateway2 $lng4 -ConnectionType IPsec -SharedKey "preSharedKey"
    
  Get-AzureRmVirtualNetworkGatewayConnection -Name "Connection1" -ResourceGroupName "ForcedTunneling"
  ```