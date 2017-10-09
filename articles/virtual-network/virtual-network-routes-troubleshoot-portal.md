---
title: le route aaaTroubleshoot - portale | Documenti Microsoft
description: Informazioni su come route tootroubleshoot nel modello di distribuzione Azure Resource Manager hello utilizzando hello portale di Azure.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bdd8b6dc-02fb-4057-bb23-8289caa9de89
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 579bae91ef3200852032b3953d3cc5d26deada86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-hello-azure-portal"></a>Risoluzione dei problemi delle route usando hello portale di Azure
> [!div class="op_single_selector"]
> * [Portale di Azure](virtual-network-routes-troubleshoot-portal.md)
> * [PowerShell](virtual-network-routes-troubleshoot-powershell.md)
>
>

Se si verificano tooor problemi connettività di rete dalla macchina virtuale di Azure (VM), le route possono influire dei flussi di traffico della macchina virtuale. Questo articolo fornisce una panoramica delle funzionalità di diagnostica per le route toohelp risolvere il problema.

Le tabelle di route sono associate alle subnet e valgono per tutte le interfacce di rete della subnet. Hello seguenti tipi di route può essere applicati tooeach interfaccia di rete:

* **Route di sistema:** per impostazione predefinita, ogni subnet creata in una rete virtuale di Azure dispone di tabelle di route di sistema che consentono il traffico di rete virtuale locale, il traffico locale tramite gateway VPN e il traffico Internet. Le route di sistema esistono anche per le reti virtuali con peering.
* **Le route BGP:** propagate interfacce toonetwork attraverso ExpressRoute o le connessioni VPN da sito a sito. Altre informazioni su routing BGP leggendo hello [BGP con gateway VPN](../vpn-gateway/vpn-gateway-bgp-overview.md) e [panoramica relativa a ExpressRoute](../expressroute/expressroute-introduction.md) articoli.
* **Le route definite dall'utente (UDR):** se si usano dispositivi di rete virtuali o sono a tunneling forzato rete locale tooan del traffico tramite una VPN site-to-site, è possibile route definite dall'utente (UDRs) associate con la tabella di route della subnet. Se non si ha familiarità con UDRs, leggere hello [le route definite dall'utente](virtual-networks-udr-overview.md#user-defined-routes) articolo.

Con hello route diverse che possono essere applicati tooa l'interfaccia di rete, può essere difficile toodetermine le route di aggregazione sono efficaci. toohelp risoluzione dei problemi di connettività di rete VM, è possibile visualizzare tutte le route efficaci hello per un'interfaccia di rete nel modello di distribuzione Azure Resource Manager hello.

## <a name="using-effective-routes-tootroubleshoot-vm-traffic-flow"></a>Utilizzo di VM route valide tootroubleshoot il flusso del traffico
In questo articolo Usa hello segue scenario come tooillustrate un esempio come tootroubleshoot hello effettiva instrada per un'interfaccia di rete:

Una macchina virtuale (*VM1*) connessi toohello rete virtuale (*VNet1*, prefisso: 10.9.0.0/16) ha esito negativo tooconnect tooa VM(VM3) in una rete virtuale appena peered (*VNet3*, prefisso 10.10.0.0/16). Sono disponibili UDRs o BGP non instrada applicato tooVM1-NIC1 rete interfaccia connessa toohello macchina virtuale, vengono applicate solo le route di sistema.

Questo articolo spiega come hello toodetermine causa dell'errore di connessione hello, utilizzando la funzionalità di route valide nel modello di distribuzione di gestione delle risorse di Azure.
Mentre l'esempio hello Usa solo le route di sistema, hello stessi passaggi può essere utilizzati toodetermine errori di connessione in ingresso e in uscita su qualsiasi tipo di route.

> [!NOTE]
> Se la macchina virtuale è associata più di una scheda di rete, controllare route valide per ogni hello NIC tooand di problemi la connettività di rete toodiagnose da una macchina virtuale.
>
>

### <a name="view-effective-routes-for-a-virtual-machine"></a>Visualizzare le route valide per una macchina virtuale
toosee hello aggregazione route che vengono applicato tooa macchina virtuale, hello completo alla procedura seguente:

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **più servizi**, quindi fare clic su **macchine virtuali** nell'elenco visualizzato hello.
3. Selezionare tootroubleshoot una macchina virtuale dall'elenco di hello che viene visualizzata e viene visualizzato un pannello della macchina virtuale con opzioni.
4. Fare clic su **Diagnostica e risoluzione dei problemi** e quindi selezionare un problema comune. Per questo esempio, **toomy macchina virtuale di Windows non riesco a connettermi** è selezionata.

    ![](./media/virtual-network-routes-troubleshoot-portal/image1.png)
5. Passaggi appaiono sotto problema hello, come illustrato nella seguente immagine hello:

    ![](./media/virtual-network-routes-troubleshoot-portal/image2.png)

    Fare clic su *route valide* nell'elenco di hello di procedure consigliate.
6. Hello **route valide** pannello viene visualizzato, come illustrato nella seguente immagine hello:

    ![](./media/virtual-network-routes-troubleshoot-portal/image3.png)

    Se la VM ha una sola interfaccia di rete, sarà selezionata per impostazione predefinita. Se si dispone di più di una scheda di rete, selezionare hello NIC per cui si desidera route valide di tooview hello.

   > [!NOTE]
   > Se hello VM associata a hello NIC non è in esecuzione, non verranno visualizzate route valide. Solo i primi 200 route valide hello vengono visualizzate nel portale di hello. Per l'elenco completo di hello, fare clic su **scaricare**. È possibile filtrare ulteriormente i risultati hello da file CSV scaricato hello.
   >
   >

    Si noti seguenti hello nell'output di hello:

   * **Origine**: indica il tipo di hello della route. Le route di sistema vengono visualizzate come *Default*, le route definite dall'utente come *User* e le route del gateway (statiche o BGP) come *VPNGateway*.
   * **Stato**: indica lo stato della route valida hello. Alcuni valori possibili sono *Active* o *Invalid*.
   * **AddressPrefixes**: Specifica il prefisso di indirizzo hello della route valida hello in notazione CIDR.
   * **nextHopType**: indica l'hop successivo di hello per hello route specificato. I valori possibili sono *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* e *Null*. Un valore *Null* per **nextHopType** in una route definita dall'utente potrebbe indicare una route non valida. Ad esempio, se **nextHopType** è *VirtualAppliance* e hello network appliance virtuale macchina virtuale non è in uno stato di provisioning/esecuzione. Se **nextHopType** è *VPNGateway* e non è stato eseguito il provisioning/in esecuzione nella rete virtuale specificata hello alcun gateway, route hello potrebbe diventare non valide.
7. Non vi è alcun toohello route elencate *WestUS VNET3* rete virtuale (prefisso 10.10.0.0/16) da hello *WestUS VNet1* (prefisso 10.9.0.0/16) in immagine hello nel passaggio precedente hello. Nella seguente immagine di hello, collegamento di peering hello è hello *Disconnected* stato:

    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)

    collegamento bidirezionale Hello di peering hello è interrotta, che spiega perché VM1 Impossibile connettersi tooVM3 in hello *WestUS VNet3* rete virtuale.
8. Hello immagine seguente mostra le route hello dopo la definizione di collegamento di peering hello bidirezionale:

    ![](./media/virtual-network-routes-troubleshoot-portal/image5.png)

Per la risoluzione dei problemi più scenari per la valutazione di tunneling forzato e route, leggere hello [considerazioni](virtual-network-routes-troubleshoot-portal.md#considerations) sezione di questo articolo.

### <a name="view-effective-routes-for-a-network-interface"></a>Visualizzare le route valide per un'interfaccia di rete
In caso di impatto sul flusso del traffico di rete per una determinata interfaccia di rete, è possibile visualizzare direttamente un elenco completo delle route valide nell'interfaccia di rete. toosee hello aggregazione route che vengono applicato tooa NIC, hello completo alla procedura seguente:

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **Altri servizi** e quindi su **Interfacce di rete**
3. Ricerca per nome hello di una scheda di rete nell'elenco di hello o selezionarlo dall'elenco di hello visualizzato. In questo esempio si seleziona **VM1-NIC1** .
4. Selezionare **route valide** in hello **interfaccia di rete** pannello, come illustrato nella seguente immagine hello:

       ![](./media/virtual-network-routes-troubleshoot-portal/image6.png)

    Hello **ambito** interfaccia di rete toohello valori predefiniti selezionato.

      ![](./media/virtual-network-routes-troubleshoot-portal/image7.png)

### <a name="view-effective-routes-for-a-route-table"></a>Visualizzare le route valide per una tabella di route
Quando si modificano le route definite dall'utente (UDRs) in una tabella di route, è consigliabile impatto hello tooreview delle route hello aggiunto in una determinata macchina virtuale. Una tabella di route può essere associata a qualsiasi numero di subnet. È ora possibile visualizzare tutte le route effettiva di hello per tutti hello NIC che una tabella di routing specificato viene applicata, senza la necessità di contesto tooswitch da hello pannello tabella di route specificato.

Per questo esempio, la route definita dall'utente *UDRoute* è specificata nella tabella di route *UDRouteTable*. Questa route invia tutto il traffico Internet da *Subnet1* in hello *WestUS VNet1* rete virtuale, attraverso un accessorio virtuale di rete (NVA), in *Subnet2* di hello stessa rete virtuale. route Hello è illustrato nella seguente immagine hello:

![](./media/virtual-network-routes-troubleshoot-portal/image8.png)

toosee hello aggregazione le route per una tabella di route, hello completo alla procedura seguente:

1. Portale di Azure all'indirizzo https://portal.azure.com toohello di account di accesso.
2. Fare clic su **Altri servizi** e quindi su **Tabelle route**
3. Elenco di hello ricerca per la tabella di route hello desidera toosee le route di aggregazione per e selezionarlo. In questo esempio si seleziona **UDRouteTable** . Viene visualizzato un pannello per la tabella di route hello selezionato, come illustrato nella seguente immagine hello:

    ![](./media/virtual-network-routes-troubleshoot-portal/image9.png)
4. Selezionare **route valide** in hello **tabella di Route** blade. Hello **ambito** è impostata una tabella di route toohello selezionata.
5. Una tabella di routing può essere applicato toomultiple subnet. Seleziona hello **Subnet** desiderato tooreview dall'elenco di hello. In questo esempio si seleziona **Subnet1** .
6. Selezionare un'opzione in **Interfaccia di rete**. Sono elencate tutte le schede di rete connessa toohello selezionato subnet. In questo esempio si seleziona **VM1-NIC1** .

    ![](./media/virtual-network-routes-troubleshoot-portal/image10.png)

   > [!NOTE]
   > Se hello NIC non è associata a una macchina virtuale in esecuzione, non vengono visualizzati alcuna route valide.
   >
   >

## <a name="considerations"></a>Considerazioni
Alcuni aspetti tookeep presente durante la revisione elenco hello di route restituito:

* Il routing è basato sulla corrispondenza del prefisso più lunga (LPM) tra le route definite dall'utente, BGP e di sistema. Se è presente più di una route con hello stesso LPM corrispondono, quindi una route viene selezionata in base origine hello seguente ordine:

  * Route definita dall'utente
  * Route BGP
  * Route di sistema (predefinita)

    Con route efficaci, è possibile visualizzare solo le route efficaci che corrispondono a LPM in base a tutte le route di hello disponibile. Mostrando come route hello vengono effettivamente valutate per una scheda di rete specificato, questo rende molto più semplice tootroubleshoot specifica le route che potrebbero influire negativamente sulla connettività da e verso la macchina virtuale.
* Se si dispone di UDRs e inviano traffico tooa virtuale altri dispositivi di rete (NVA), con *VirtualAppliance* come **nextHopType**, verificare che l'inoltro IP sia abilitato sul traffico di hello NVA ricevente hello o i pacchetti vengono eliminati.
* Se è abilitato il tunneling forzato, tutto il traffico Internet in uscita sarà indirizzati tooon locale. RDP/SSH da Internet tooyour che macchina virtuale potrebbe non funzionare con questa impostazione, a seconda di come hello locale gestisce tale traffico.
  Il tunneling forzato può essere abilitato:
  * Se si usa una VPN site-to-site, impostando una route definita dall'utente con nextHopType come Gateway VPN
  * Se una route predefinita è pubblicizzata su BGP
* Per la rete virtuale peering correttamente, il traffico toowork una route di sistema **nextHopType** *VNetPeering* deve essere presente per il peering hello intervallo prefisso della rete virtuale. Se non esiste e hello peering reti virtuali, una route di tale collegamento ha un aspetto corretto:
  * Attendere alcuni secondi e riprovare, se si tratta di un collegamento di peering appena stabilito. Occasionalmente Accetta route toopropagate più interfacce di rete tooall hello in una subnet.
  * Flussi di traffico hello potrebbero influire negativamente sulla regole Network Security Group (gruppo). Per ulteriori informazioni, vedere hello [risolvere i gruppi di sicurezza di rete](virtual-network-nsg-troubleshoot-portal.md) articolo.
