---
title: 'Configurare connessioni coesistenti ExpressRoute e VPN da sito a sito - Versione classica: Azure| Microsoft Docs'
description: "In questo articolo illustra la configurazione di una connessione VPN da sito a sito che può coesistere per il modello di distribuzione classica hello ed ExpressRoute."
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: dcf1a5af-a289-466a-b812-0bfedbd2bda0
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: abb30fff55e8ec243f2920c5b2f70c43717755fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-expressroute-and-site-to-site-coexisting-connections-classic"></a>Configurare connessioni coesistenti ExpressRoute e da sito a sito (versione classica)
> [!div class="op_single_selector"]
> * [PowerShell - Gestione risorse](expressroute-howto-coexist-resource-manager.md)
> * [PowerShell - Classico](expressroute-howto-coexist-classic.md)
> 
> 

Con possibilità di hello tooconfigure VPN Site-to-Site ed ExpressRoute presenta diversi vantaggi. È possibile configurare la VPN da sito a sito come un percorso sicuro failover per ExressRoute o usare VPN da sito a sito tooconnect toosites che non sono connessi tramite ExpressRoute. Verranno illustrate hello passaggi tooconfigure entrambi gli scenari in questo articolo. In questo articolo si applica il modello di distribuzione classica toohello. Questa configurazione non è disponibile nel portale di hello.

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

> [!IMPORTANT]
> Circuiti ExpressRoute devono essere pre-configurati prima di seguire le istruzioni di hello seguenti. Assicurarsi di aver seguito le guide di hello troppo[creare un circuito ExpressRoute](expressroute-howto-circuit-classic.md) e [configurare il routing](expressroute-howto-routing-classic.md) prima di seguire i passaggi di hello riportati di seguito.
> 
> 

## <a name="limits-and-limitations"></a>Limiti e limitazioni
* **L'instradamento del transito non è supportato.** Con Azure non è possibile attivare il routing tra la rete locale connessa tramite la VPN da sito a sito e la rete locale connessa tramite ExpressRoute.
* **La connessione da punto a sito non è supportata.** Non è possibile abilitare toohello di connessioni VPN point-to-site stessa rete virtuale che è connesso tooExpressRoute. VPN Point-to-site ed ExpressRoute non può coesistere per hello stessa rete virtuale.
* **Impossibile abilitare il tunneling forzato su gateway VPN da sito a sito hello.** È possibile solo "forzare" tutto associato a Internet traffico tooyour indietro rete locale tramite ExpressRoute.
* **Il gateway SKU Basic non è supportato.** È necessario utilizzare un gateway non base SKU per entrambi hello [gateway ExpressRoute](expressroute-about-virtual-network-gateways.md) hello e [gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **È supportato solo il gateway VPN basato su route.** È necessario usare un [gateway VPN basato su route](../vpn-gateway/vpn-gateway-about-vpngateways.md).
* **Deve essere configurata una route statica per il gateway VPN.** Se la rete locale è connesso tooboth ExpressRoute e una Site-to-Site VPN, è necessario disporre una route statica configurata nel toohello di connessione di rete locale tooroute hello Site-to-Site VPN rete Internet pubblica.
* **Il gateway ExpressRoute deve essere configurato prima.** È necessario creare innanzitutto gateway ExpressRoute hello prima di aggiungere gateway VPN da sito a sito hello.

## <a name="configuration-designs"></a>Progetti di configurazione
### <a name="configure-a-site-to-site-vpn-as-a-failover-path-for-expressroute"></a>Configurare una VPN da sito a sito come percorso di failover per ExpressRoute
È possibile configurare una connessione VPN da sito a sito come backup per ExpressRoute. Si applica solo toovirtual reti collegate toohello Azure percorso di peering privato. Non esiste alcuna soluzione di failover basato su VPN per i servizi accessibili tramite i peering pubblico di Azure e Microsoft. Hello circuito ExpressRoute è sempre collegamento primario hello. Flusso dei dati tramite il percorso VPN Site-to-Site hello solo se hello circuito ExpressRoute ha esito negativo. 

> [!NOTE]
> Mentre il circuito ExpressRoute è preferito tramite VPN Site-to-Site quando entrambe le route sono hello stesso, Azure utilizzerà hello più lunga prefisso corrispondenza toochoose hello route verso la destinazione del pacchetto di hello.
> 
> 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario1.jpg)

### <a name="configure-a-site-to-site-vpn-tooconnect-toosites-not-connected-through-expressroute"></a>Configurare un toosites tooconnect VPN da sito a sito non è connesso tramite ExpressRoute
È possibile configurare la rete in cui alcuni siti si connettono direttamente tooAzure tramite VPN Site-to-Site e alcuni siti si connettono tramite ExpressRoute. 

![Coesistenza](media/expressroute-howto-coexist-classic/scenario2.jpg)

> [!NOTE]
> Non è possibile configurare una rete virtuale come router di transito.
> 
> 

## <a name="selecting-hello-steps-toouse"></a>Selezione di hello passaggi toouse
Esistono due diversi set di procedure toochoose dall'ordine tooconfigure nelle connessioni in cui possono coesistere. procedura di configurazione di Hello selezionato dipenderà se si dispone di una rete virtuale esistente che si desidera tooconnect a o si desidera toocreate una nuova rete virtuale.

* Non dispone di una rete virtuale e necessario toocreate uno.
  
    Se si dispone già di una rete virtuale, questa procedura assiste l'utente la creazione di una nuova rete virtuale utilizzando il modello di distribuzione classica hello e creazione di nuove connessioni di VPN Site-to-Site ed ExpressRoute. tooconfigure, eseguire i passaggi nella sezione articolo hello hello [toocreate una nuova rete virtuale e le connessioni coesistenti](#new).
* È già disponibile una rete virtuale con modello di distribuzione classica.
  
    E’ possibile che esista già una rete virtuale con una connessione VPN da sito a sito o una connessione ExpressRoute. Hello articolo sezione [tooconfigure coexsiting connessioni per una rete virtuale di già esistente](#add) consentirà di eliminazione del gateway hello e quindi la creazione di nuove connessioni VPN Site-to-Site ed ExpressRoute. Si noti che, quando si creano hello nuove connessioni, è necessario completare i passaggi di hello in un ordine specifico. Non utilizzare istruzioni hello toocreate altri articoli del gateway e connessioni.
  
    In questa procedura, la creazione di connessioni che possono coesistere verrà richiedono toodelete è il gateway e quindi configurare nuovi gateway. Ciò significa che si disporrà di tempo di inattività per le connessioni cross-premise mentre eliminare e ricreare il gateway e connessioni, ma non è necessario toomigrate le macchine virtuali o servizi tooa nuova rete virtuale. Le macchine virtuali e servizi sarà comunque in grado di toocommunicate out tramite bilanciamento del carico hello durante la configurazione del gateway se sono pertanto toodo configurato.

## <a name="new"></a>connessioni coesistenti e toocreate una nuova rete virtuale
Questa procedura illustra come creare una rete virtuale e connessioni da sito a sito ed ExpressRoute coesistenti.

1. È necessario tooinstall hello più recente di hello cmdlet di Azure PowerShell. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello. Si noti che i cmdlet di hello che verrà utilizzato per questa configurazione potrebbero essere leggermente diversi rispetto a ciò che potrebbe acquisire familiarità con. I cmdlet di hello toouse che è possibile specificare in queste istruzioni. 
2. Creare uno schema per la rete virtuale. Per ulteriori informazioni sullo schema di configurazione di hello, vedere [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   
    Quando si crea lo schema, assicurarsi di che usare hello seguenti valori:
   
   * subnet del gateway per la rete virtuale hello Hello deve essere /27 o un prefisso (ad esempio /26 o /25) più breve.
   * tipo di connessione gateway Hello "dedicato".
     
             <VirtualNetworkSite name="MyAzureVNET" Location="Central US">
               <AddressSpace>
                 <AddressPrefix>10.17.159.192/26</AddressPrefix>
               </AddressSpace>
               <Subnets>
                 <Subnet name="Subnet-1">
                   <AddressPrefix>10.17.159.192/27</AddressPrefix>
                 </Subnet>
                 <Subnet name="GatewaySubnet">
                   <AddressPrefix>10.17.159.224/27</AddressPrefix>
                 </Subnet>
               </Subnets>
               <Gateway>
                 <ConnectionsToLocalNetwork>
                   <LocalNetworkSiteRef name="MyLocalNetwork">
                     <Connection type="Dedicated" />
                   </LocalNetworkSiteRef>
                 </ConnectionsToLocalNetwork>
               </Gateway>
             </VirtualNetworkSite>
3. Dopo la creazione e configurazione dei file di schema xml, caricare il file hello. Verrà creata la rete virtuale.
   
    Utilizzare hello tooupload cmdlet seguenti il file, sostituendo il valore di hello con valori personalizzati.
   
        Set-AzureVNetConfig -ConfigurationPath 'C:\NetworkConfig.xml'
4. <a name="gw"></a>Creare un gateway ExpressRoute. Toospecify assicurarsi di essere hello GatewaySKU come *Standard*, *ad alte prestazioni*, o *UltraPerformance* e il tipo di gateway come hello *DynamicRouting*.
   
    Utilizzare hello di esempio seguente, sostituendo i valori hello per uso personale.
   
        New-AzureVNetGateway -VNetName MyAzureVNET -GatewayType DynamicRouting -GatewaySKU HighPerformance
5. Collegare il circuito ExpressRoute toohello di hello ExpressRoute gateway. Dopo questo passaggio è stato completato, viene stabilita connessione hello tra la rete locale e Azure tramite ExpressRoute.
   
        New-AzureDedicatedCircuitLink -ServiceKey <service-key> -VNetName MyAzureVNET
6. <a name="vpngw"></a>Creare quindi il gateway VPN da sito a sito. Hello GatewaySKU deve essere *Standard*, *ad alte prestazioni*, o *UltraPerformance* e hello il tipo di gateway deve essere *DynamicRouting*.
   
        New-AzureVirtualNetworkGateway -VNetName MyAzureVNET -GatewayName S2SVPN -GatewayType DynamicRouting -GatewaySKU  HighPerformance
   
    tooretrieve hello virtuale gateway le impostazioni di rete, inclusi ID gateway hello e indirizzo IP pubblico hello, utilizzano hello `Get-AzureVirtualNetworkGateway` cmdlet.
   
        Get-AzureVirtualNetworkGateway
   
        GatewayId            : 348ae011-ffa9-4add-b530-7cb30010565e
        GatewayName          : S2SVPN
        LastEventData        :
        GatewayType          : DynamicRouting
        LastEventTimeStamp   : 5/29/2015 4:41:41 PM
        LastEventMessage     : Successfully created a gateway for hello following virtual network: GNSDesMoines
        LastEventID          : 23002
        State                : Provisioned
        VIPAddress           : 104.43.x.y
        DefaultSite          :
        GatewaySKU           : HighPerformance
        Location             :
        VnetId               : 979aabcf-e47f-4136-ab9b-b4780c1e1bd5
        SubnetId             :
        EnableBgp            : False
        OperationDescription : Get-AzureVirtualNetworkGateway
        OperationId          : 42773656-85e1-a6b6-8705-35473f1e6f6a
        OperationStatus      : Succeeded
7. Creare un'entità gateway VPN del sito locale. Questo comando non configura il gateway VPN locale. Invece, consente di impostazioni del gateway locale hello tooprovide, ad esempio indirizzo IP pubblico hello e hello locale lo spazio degli indirizzi, in modo che hello gateway VPN di Azure può connettersi tooit.
   
   > [!IMPORTANT]
   > sito locale di Hello per hello VPN da sito a sito non è definito in netcfg hello. In alternativa, è necessario utilizzare i parametri del sito locale hello toospecify questo cmdlet. È possibile definire tramite portale o file netcfg hello.
   > 
   > 
   
    Utilizzare hello di esempio seguente, sostituendo i valori hello con valori personalizzati.
   
        New-AzureLocalNetworkGateway -GatewayName MyLocalNetwork -IpAddress <MyLocalGatewayIp> -AddressSpace <MyLocalNetworkAddress>
   
   > [!NOTE]
   > Se la rete locale include più route, è possibile passarle tutte come una matrice.  $MyLocalNetworkAddress = @("10.1.2.0/24","10.1.3.0/24","10.2.1.0/24")  
   > 
   > 

    tooretrieve hello virtuale gateway le impostazioni di rete, inclusi ID gateway hello e indirizzo IP pubblico hello, utilizzano hello `Get-AzureVirtualNetworkGateway` cmdlet. Vedere hello di esempio seguente.

        Get-AzureLocalNetworkGateway

        GatewayId            : 532cb428-8c8c-4596-9a4f-7ae3a9fcd01b
        GatewayName          : MyLocalNetwork
        IpAddress            : 23.39.x.y
        AddressSpace         : {10.1.2.0/24}
        OperationDescription : Get-AzureLocalNetworkGateway
        OperationId          : ddc4bfae-502c-adc7-bd7d-1efbc00b3fe5
        OperationStatus      : Succeeded


1. Configurare il gateway VPN locale dispositivo tooconnect toohello nuovo. Utilizzare le informazioni di hello recuperato nel passaggio 6 quando si configura il dispositivo VPN. Per altre informazioni sulla configurazione del dispositivo VPN, vedere l'articolo relativo alla [configurazione del dispositivo VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md).
2. Collegamento hello Site-to-Site VPN gateway in gateway locale toohello Azure.
   
    In questo esempio, connectedEntityId è l'ID del gateway locale hello, che è possibile trovare eseguendo `Get-AzureLocalNetworkGateway`. È possibile trovare virtualNetworkGatewayId utilizzando hello `Get-AzureVirtualNetworkGateway` cmdlet. Dopo questo passaggio, viene stabilita la connessione di hello tra la rete locale e Azure tramite hello connessione VPN da sito a sito.

        New-AzureVirtualNetworkGatewayConnection -connectedEntityId <local-network-gateway-id> -gatewayConnectionName Azure2Local -gatewayConnectionType IPsec -sharedKey abc123 -virtualNetworkGatewayId <azure-s2s-vpn-gateway-id>

## <a name="add"></a>tooconfigure coexsiting connessioni per una rete virtuale di già esistente
Se si dispone di una rete virtuale esistente, è possibile controllare la dimensione della subnet gateway hello. Se subnet del gateway hello /28 o /29, è necessario eliminare il gateway di rete virtuale hello e aumentare la dimensione della subnet gateway hello. Hello passaggi in questa sezione verranno illustrato come toodo che.

Se subnet del gateway hello è /27 o superiore e la rete virtuale hello è connesso tramite ExpressRoute, è possibile ignorare i passaggi di hello riportati di seguito e andare troppo["Passaggio 6: creare un gateway VPN da sito a sito"](#vpngw) nella sezione precedente hello.

> [!NOTE]
> Quando si elimina gateway esistente hello, sedi locali perderà rete virtuale tooyour hello mentre si lavora in questa configurazione.
> 
> 

1. È necessario tooinstall hello più recente di hello cmdlet PowerShell di gestione risorse di Azure. Vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) per ulteriori informazioni sull'installazione dei cmdlet di PowerShell hello. Si noti che i cmdlet di hello che verrà utilizzato per questa configurazione potrebbero essere leggermente diversi rispetto a ciò che potrebbe acquisire familiarità con. I cmdlet di hello toouse che è possibile specificare in queste istruzioni. 
2. Eliminare il gateway ExpressRoute o VPN da sito a sito esistente hello. Utilizzare hello cmdlet seguenti, sostituendo i valori hello con valori personalizzati.
   
        Remove-AzureVNetGateway –VnetName MyAzureVNET
3. Esportare lo schema di rete virtuale hello. Utilizzare hello cmdlet di PowerShell seguente, sostituendo i valori hello con valori personalizzati.
   
        Get-AzureVNetConfig –ExportToFile “C:\NetworkConfig.xml”
4. Modifica schema di file di configurazione di rete hello in modo che sia di subnet del gateway hello /27 o un prefisso (ad esempio /26 o /25) più breve. Vedere hello di esempio seguente. 
   
   > [!NOTE]
   > Se non si dispone di indirizzi IP sufficiente la dimensione di subnet gateway di rete virtuale tooincrease hello a sinistra, è necessario tooadd più spazio di indirizzi IP. Per ulteriori informazioni sullo schema di configurazione di hello, vedere [dello schema di configurazione di rete virtuale di Azure](https://msdn.microsoft.com/library/azure/jj157100.aspx).
   > 
   > 
   
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.17.159.224/27</AddressPrefix>
          </Subnet>
5. Se il gateway precedente era una VPN Site-to-Site, è necessario modificare anche il tipo di connessione hello troppo**dedicato**.
   
                 <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="MyLocalNetwork">
                      <Connection type="Dedicated" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
6. A questo punto, si avrà una rete virtuale senza gateway. toocreate nuovi gateway e completare le connessioni, è possibile procedere con [passaggio 4: creare un gateway ExpressRoute](#gw), trovato in hello precedente set di passaggi.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni su ExpressRoute, vedere hello [domande frequenti su ExpressRoute](expressroute-faqs.md)

