---
title: le route aaaTroubleshoot - PowerShell | Documenti Microsoft
description: Informazioni su come tootroubleshoot instrada nel modello di distribuzione Azure Resource Manager hello con Azure PowerShell.
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: bf7dc5e7-9399-460e-8e0d-8992dbed98a6
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 7a07806df5c1d0caee921187e6ad29f6755ab535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-routes-using-azure-powershell"></a>Risoluzione dei problemi di route con Azure PowerShell
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

### <a name="view-effective-routes-for-a-network-interface"></a>Visualizzare le route valide per un'interfaccia di rete
toosee hello aggregazione route tooa applicata l'interfaccia di rete, hello completo alla procedura seguente:

1. Avviare un tooAzure di sessione e l'account di accesso di Azure PowerShell. Se non si ha familiarità con Azure PowerShell, leggere hello [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo.
2. il comando seguente Hello restituisce tutte le route applicate tooa l'interfaccia di rete denominata *VM1 NIC1* nel gruppo di risorse hello *RG1*.
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Se non si conosce il nome di hello un'interfaccia di rete, digitare hello seguente i nomi di comando tooretrieve hello di tutte le interfacce di rete in un group.* risorse
   > 
   > 
   
       Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name
   
   Hello output seguente cerca un output simile toohello hello di subnet toohello ogni route applicato a che connessa:
   
       Name :
       State : Active
       AddressPrefix : {10.9.0.0/16}
       NextHopType : VNetLocal
       NextHopIpAddress : {}
   
       Name :
       State : Active
       AddressPrefix : {0.0.0.0/16}
       NextHopType : Internet
       NextHopIpAddress : {}
   
   Si noti seguenti hello nell'output di hello:
   
   * **Nome**: nome della route valida hello può essere vuoto, a meno che non venga specificato esplicitamente, per le route definite dall'utente. 
   * **Stato**: indica lo stato della route valida hello. Alcuni valori possibili sono "Active" o "Invalid"
   * **AddressPrefixes**: Specifica il prefisso di indirizzo hello della route valida hello in notazione CIDR. 
   * **nextHopType**: indica l'hop successivo di hello per hello route specificato. I valori possibili sono *VirtualAppliance*, *Internet*, *VNetLocal*, *VNetPeering* e *Null*. Un valore *Null* per **nextHopType** in una route definita dall'utente potrebbe indicare una route non valida. Ad esempio, se **nextHopType** è *VirtualAppliance* e hello network appliance virtuale macchina virtuale non è in uno stato di provisioning/esecuzione. Se **nextHopType** è *VPNGateway* e non è stato eseguito il provisioning/in esecuzione nella rete virtuale specificata hello alcun gateway, route hello potrebbe diventare non valide.
   * **NextHopIpAddress**: specifica hello di indirizzo IP dell'hop successivo di hello della route valida hello.
   
   Hello seguente comando restituisce le route hello in una tabella tooview più semplice:
   
       Get-AzureRmEffectiveRouteTable -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1 | Format-Table
   
   Hello output riportato di seguito è parte dell'output di hello ricevuto per uno scenario di hello descritto in precedenza:
   
       Name State AddressPrefix NextHopType NextHopIpAddress
       ---- ----- ------------- ----------- ----------------
       Active {10.9.0.0/16} VnetLocal {}
       Active {0.0.0.0/0} Internet {}
3. Non vi è alcun toohello route elencate *WestUS VNet3* rete virtuale (prefisso 10.10.0.0/16)** da *WestUS VNet1* (prefisso 10.9.0.0/16) nell'output di hello dal passaggio precedente hello. Come illustrato nella seguente immagine hello, hello collegamento di peering reti virtuali con hello *WestUS VNet3* rete virtuale è in hello *Disconnected* stato.
   
    ![](./media/virtual-network-routes-troubleshoot-portal/image4.png)
   
    collegamento bidirezionale Hello di peering hello è interrotta, che spiega perché VM1 Impossibile connettersi tooVM3 in hello *WestUS VNet3* rete virtuale. Configurare di nuovo un collegamento di peering di rete virtuale bidirezionale per le reti virtuali *WestUS VNet1* *WestUS VNet3*. output di Hello restituito dopo aver stabilito il collegamento di peering reti virtuali hello correttamente segue:
   
        Name State AddressPrefix NextHopType NextHopIpAddress
        ---- ----- ------------- ----------- ----------------
        Active {10.9.0.0/16} VnetLocal {}
        Active {10.10.0.0/16} VNetPeering {}
        Active {0.0.0.0/0} Internet {}
   
    Dopo aver determinato problema hello, è possibile aggiungere, rimuovere, o modificare le route e tabelle di route. Digitare hello successivo comando toosee un elenco di hello comandi utilizzati toodo pertanto:
   
        Get-Help *-AzureRmRouteConfig

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
  * Flussi di traffico hello potrebbero influire negativamente sulla regole Network Security Group (gruppo). Per ulteriori informazioni, vedere hello [risolvere i gruppi di sicurezza di rete](virtual-network-nsg-troubleshoot-powershell.md) articolo.

