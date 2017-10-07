---
title: 'Configurare il tunneling forzato per connessioni di Azure da sito a sito: versione classica | Microsoft Docs'
description: Come tooredirect o 'force' tutti tooyour di sfondo del traffico associato a Internet posizione locale.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 5c0177f1-540c-4474-9b80-f541fa44240b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 35b3a9ea370f9f962572629a69cc9aed16a87837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-forced-tunneling-using-hello-classic-deployment-model"></a>Configurare il tunneling forzato utilizzando il modello di distribuzione classica hello

Il tunneling consente di reindirizzare o "forzare" tutto associato a Internet traffico tooyour indietro percorso locale tramite un tunnel VPN da sito a sito per l'ispezione e controllo forzato. Si tratta di un requisito di sicurezza critico per la maggior parte dei criteri IT aziendali. Senza il tunneling forzato, il traffico Internet dalle macchine virtuali in Azure passerà sempre dall'infrastruttura di rete di Azure direttamente out toohello Internet, senza tooallow opzione hello è traffico hello tooinspect o audit. Accesso a Internet non autorizzato potrebbe provocare la diffusione di tooinformation o altri tipi di violazioni di sicurezza.

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

In questo articolo illustra la configurazione forzato tunneling per le reti virtuali create utilizzando il modello di distribuzione classica hello. Il tunneling forzato può essere configurato tramite PowerShell, non tramite il portale di hello. Se si desidera tooconfigure tunneling per modello di distribuzione di gestione risorse di hello forzato, è possibile selezionare articolo classico da hello segue l'elenco a discesa:

> [!div class="op_single_selector"]
> * [PowerShell - Classico](vpn-gateway-about-forced-tunneling.md)
> * [PowerShell - Gestione risorse](vpn-gateway-forced-tunneling-rm.md)
> 
> 

## <a name="requirements-and-considerations"></a>Problemi e considerazioni
Il tunneling forzato in Azure viene configurato tramite route di rete virtuale definite dall'utente. Reindirizzamento del traffico tooan locale sito viene espresso come un gateway VPN di Azure toohello di Route predefinita. Hello nella sezione seguente sono elencate la limitazione corrente hello della tabella di routing hello e le route per una rete virtuale di Azure:

* Ciascuna subnet della rete virtuale dispone di una tabella di routing di sistema integrata. tabella di routing sistema Hello è hello seguenti tre gruppi di route:

  * **Route di rete virtuale locale:** direttamente toohello destinazione macchine virtuali in hello stessa rete virtuale.
  * **Le route locali:** gateway VPN di Azure toohello.
  * **Route predefinita:** direttamente toohello Internet. I pacchetti destinati toohello gli indirizzi IP privati non coperti da route hello due precedenti verranno eliminati.
* Con la versione di hello delle route definite dall'utente, è possibile creare una route predefinita di un tooadd tabella di routing e quindi associare hello routing tabella tooyour rete virtuale subnet tooenable forzato tunneling su queste subnet.
* È necessario un sito"predefinito" tooset tra rete virtuale connessa toohello hello cross-premise siti locali.
* Il tunneling forzato deve essere associato a una rete virtuale che disponga di un gateway VPN (non un gateway statico).
* Il tunneling forzato ExpressRoute non viene configurato tramite questo meccanismo, ma è invece abilitato annunciando una route predefinita tramite hello BGP ExpressRoute le sessioni di peering. Vedere hello [documentazione di ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/) per ulteriori informazioni.

## <a name="configuration-overview"></a>Panoramica della configurazione
Nell'esempio seguente di hello, con tunneling hello front-end subnet non è forzato. i carichi di lavoro Hello nella subnet front-end hello continuare tooaccept e rispondere toocustomer richieste da hello Internet direttamente. Hello subnet di livello intermedio e back-end devono essere forzate tunnel. Tutte le connessioni in uscita da tali toohello due subnet Internet sarà tooan forzata o reindirizzato nuovamente nel sito locale tramite uno dei tunnel VPN S2S hello.

Questo consente toorestrict e controllare l'accesso a Internet dalle macchine virtuali o nel cloud servizi in Azure, continuando tooenable l'architettura del servizio a più livelli necessaria. È inoltre possibile applicare forzato tunneling toohello intere reti virtuali se sono non presenti carichi di lavoro con connessione Internet nelle reti virtuali.

![Tunneling forzato](./media/vpn-gateway-about-forced-tunneling/forced-tunnel.png)

## <a name="before-you-begin"></a>Prima di iniziare
Verificare di aver hello elementi prima della configurazione iniziale.

* Una sottoscrizione di Azure. Se non si ha una sottoscrizione di Azure, è possibile attivare i [vantaggi per i sottoscrittori di MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) oppure iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/pricing/free-trial/).
* Una rete virtuale configurata. 
* versione più recente di Hello di hello cmdlet di Azure PowerShell. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello.

## <a name="configure-forced-tunneling"></a>È possibile configurare il tunneling forzato?
Hello seguente procedura consente di specificare il tunneling forzato per una rete virtuale. passaggi di configurazione Hello corrispondono toohello file di configurazione di rete di rete virtuale.

```
<VirtualNetworkSite name="MultiTier-VNet" Location="North Europe">
     <AddressSpace>
      <AddressPrefix>10.1.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Frontend">
            <AddressPrefix>10.1.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Midtier">
            <AddressPrefix>10.1.1.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Backend">
            <AddressPrefix>10.1.2.0/23</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.1.200.0/28</AddressPrefix>
          </Subnet>
        </Subnets>
        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="DefaultSiteHQ">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch1">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch2">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Branch3">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
        </Gateway>
      </VirtualNetworkSite>
    </VirtualNetworkSite>
```

In questo esempio, la rete virtuale hello "MultiTier-VNet" include tre subnet: subnet 'Front-end', 'Midtier' e 'Back-end', con le connessioni locali tra quattro: 'DefaultSiteHQ' e tre rami. 

passaggi di Hello verranno impostato hello 'DefaultSiteHQ' come connessione di hello predefinita del sito per il tunneling forzato e configurare hello Midtier e Backend subnet toouse il tunneling forzato.

1. Creare una tabella di routing. Utilizzare hello cmdlet toocreate dopo la tabella di routing.

  ```powershell
  New-AzureRouteTable –Name "MyRouteTable" –Label "Routing Table for Forced Tunneling" –Location "North Europe"
  ```
2. Aggiungere una tabella di routing toohello di route predefinita. 

  Hello esempio seguente aggiunge una route toohello tabella di routing predefinita creata nel passaggio 1. Si noti che hello solo route supportata è il prefisso di destinazione hello di "0.0.0.0/0" toohello hop successivo "VPNGateway".

  ```powershell
  Get-AzureRouteTable -Name "MyRouteTable" | Set-AzureRoute –RouteTable "MyRouteTable" –RouteName "DefaultRoute" –AddressPrefix "0.0.0.0/0" –NextHopType VPNGateway
  ```
3. Associare subnet toohello tabella di routing hello. 

  Dopo che viene creata una tabella di routing e l'aggiunta di una route, associare subnet di rete virtuale tooa tabella route hello utilizzare hello tooadd riportato di seguito. esempio Hello aggiunge hello route nella tabella "MyRouteTable" toohello Midtier e subnet di back-end di VNet MultiTier-VNet.

  ```powershell
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Midtier" -RouteTableName "MyRouteTable"
  Set-AzureSubnetRouteTable -VirtualNetworkName "MultiTier-VNet" -SubnetName "Backend" -RouteTableName "MyRouteTable"
  ```
4. Assegnare un sito predefinito per il tunneling forzato. 

  In hello nel passaggio precedente, gli script di cmdlet di esempio hello hello tabella di routing creata e associata tootwo di tabella hello route della subnet della rete virtuale hello. passaggio rimanenti Hello è tooselect un sito locale tra le connessioni a più siti hello della rete virtuale di hello come hello sito o tunnel predefinito.

  ```powershell
  $DefaultSite = @("DefaultSiteHQ")
  Set-AzureVNetGatewayDefaultSite –VNetName "MultiTier-VNet" –DefaultSite "DefaultSiteHQ"
  ```

## <a name="additional-powershell-cmdlets"></a>Ulteriori cmdlet di PowerShell
### <a name="toodelete-a-route-table"></a>toodelete una tabella di routing

```powershell
Remove-AzureRouteTable -Name <routeTableName>
```
  
### <a name="toolist-a-route-table"></a>toolist una tabella di routing

```powershell
Get-AzureRouteTable [-Name <routeTableName> [-DetailLevel <detailLevel>]]
```

### <a name="toodelete-a-route-from-a-route-table"></a>toodelete una route da una tabella di route

```powershell
Remove-AzureRouteTable –Name <routeTableName>
```

### <a name="tooremove-a-route-from-a-subnet"></a>tooremove una route da una subnet

```powershell
Remove-AzureSubnetRouteTable –VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="toolist-hello-route-table-associated-with-a-subnet"></a>tabella di route hello toolist associata a una subnet

```powershell
Get-AzureSubnetRouteTable -VirtualNetworkName <virtualNetworkName> -SubnetName <subnetName>
```

### <a name="tooremove-a-default-site-from-a-vnet-vpn-gateway"></a>un sito predefinito da un gateway VPN VNet tooremove

```powershell
Remove-AzureVnetGatewayDefaultSite -VNetName <virtualNetworkName>
```