---
title: "Aggiungere più tooa di connessioni VPN gateway da sito a sito tra reti virtuali: portale di Azure: Gestione risorse | Documenti Microsoft"
description: "Aggiungere più siti S2S connessioni tooa gateway VPN con una connessione esistente"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a>Aggiungere un tooa di connessione da sito a sito rete virtuale con una connessione gateway VPN esistente

> [!div class="op_single_selector"]
> * [Portale di Azure](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classico)](vpn-gateway-multi-site.md)
>
> 

Questo articolo viene illustrato l'utilizzo di hello tooadd portale Azure da sito a sito (S2S) connessioni tooa gateway VPN con una connessione esistente. Questo tipo di connessione è spesso tooas cui una configurazione "multi-site". È possibile aggiungere un tooa connessione S2S rete virtuale che dispone già di una connessione S2S, connessione Point-to-Site o rete connessione. Quando si aggiungono delle connessioni, esistono alcune limitazioni di cui è necessario tenere conto. Controllare hello [prima di iniziare](#before) sezione tooverify questo articolo prima di iniziare la configurazione. 

Questo articolo riguarda tooVNets creato con modello di distribuzione di gestione risorse di hello che dispone di un gateway VPN RouteBased. Questi passaggi non vengono applicano le configurazioni di connessione coesistenti tooExpressRoute/Site-to-Site. Per informazioni sulle connessioni coesistenti vedere [Creare connessioni coesistenti da sito a sito ed ExpressRoute](../expressroute/expressroute-howto-coexist-resource-manager.md).

### <a name="deployment-models-and-methods"></a>Metodi e modelli di distribuzione
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

Questa tabella viene aggiornata man mano che per questa configurazione diventano disponibili nuovi articoli e altri strumenti. Quando un articolo è disponibile, è un collegamento direttamente tooit da questa tabella.

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a>Prima di iniziare
Verificare hello seguenti elementi:

* Non si sta creando una connessione coesistente ExpressRoute/da sito a sito.
* Si dispone di una rete virtuale che è stata creata con modello di distribuzione di gestione risorse di hello con una connessione esistente.
* gateway di rete virtuale Hello per la rete virtuale è di tipo RouteBased. Se si dispone di un gateway VPN PolicyBased, è necessario eliminare il gateway di rete virtuale hello e creare un nuovo gateway VPN come tipo RouteBased.
* Nessuno degli intervalli di indirizzi hello si sovrappongono per uno qualsiasi dei hello reti virtuali che esegue la connessione a questa rete virtuale.
* Si dispone di dispositivi VPN con compatibilità e chi è in grado di tooconfigure è. Vedere [Informazioni sui dispositivi VPN](vpn-gateway-about-vpn-devices.md). Se si non ha familiarità con la configurazione del dispositivo VPN o si ha familiarità con gli intervalli di indirizzi IP hello nella configurazione di rete locale, è necessario toocoordinate con qualcuno in grado di fornire i dettagli per l'utente.
* Si dispone di un indirizzo IP pubblico esterno per il dispositivo VPN. L'indirizzo IP non può trovarsi dietro un NAT.

## <a name="part1"></a>Parte 1: Configurare una connessione
1. Da un browser, passare toohello [portale di Azure](http://portal.azure.com) e, se necessario, accedere con l'account di Azure.
2. Fare clic su **tutte le risorse** e individuare il **gateway di rete virtuale** dall'elenco di hello delle risorse e farvi clic sopra.
3. In hello **gateway di rete virtuale** pannello, fare clic su **connessioni**.
   
    ![Pannello connessioni](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Pannello connessioni")<br>
4. In hello **connessioni** pannello, fare clic su **+ Aggiungi**.
   
    ![Pulsante di connessione Aggiungi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Aggiungi pulsante di connessione")<br>
5. In hello **Aggiungi connessione** pannello, compilare hello seguenti campi:
   
   * **Nome:** hello Nome sito toohello toogive si sta creando una connessione hello.
   * **Tipo di connessione**: selezionare **Da sito a sito (IPSec)**.
     
     ![Pannello connessione Aggiungi](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Pannello di Aggiungi connessione")<br>

## <a name="part2"></a>Parte 2: Aggiungere un gateway di rete locale
1. Fare clic su **Gateway di rete locale** ***Scegli un gateway di rete locale***. Verrà aperta hello **scegliere gateway di rete locale** blade.
   
    ![Gateway di rete locale scegliere](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "scegliere gateway di rete locale")<br>
2. Fare clic su **Crea nuovo** tooopen hello **gateway di rete locale crea** blade.
   
    ![Pannello di gateway di rete locale crea](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "crea gateway di rete locale")<br>
3. In hello **gateway di rete locale crea** pannello, compilare hello seguenti campi:
   
   * **Nome:** hello Nome risorsa del gateway di rete locale toohello toogive.
   * **Indirizzo IP:** hello indirizzo IP pubblico del dispositivo VPN hello nel sito di hello che si desidera tooconnect per.
   * **Lo spazio degli indirizzi:** spazio degli indirizzi hello che si desidera toobe indirizzato toohello nuovo sito di rete locale.
4. Fare clic su **OK** su hello **gateway di rete locale crea** modifiche hello toosave di blade.

## <a name="part3"></a>Parte 3: aggiungere una chiave condivisa hello e creare la connessione hello
1. In hello **Aggiungi connessione** pannello, aggiungere una chiave condivisa hello che si desidera toouse toocreate la connessione. È possibile ottenere la chiave condivisa hello dal dispositivo VPN o crearla qui e quindi configurare il hello toouse di dispositivi VPN stessa chiave condivisa. Hello importante aspetto è che le chiavi di hello sono esattamente hello stesso.
   
    ![Chiave condivisa](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Chiave condivisa")<br>
2. Nella parte inferiore di hello del pannello hello, fare clic su **OK** connessione hello toocreate.

## <a name="part4"></a>Parte 4: verificare una connessione VPN hello


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a>Passaggi successivi

Una volta completata la connessione, è possibile aggiungere macchine virtuali tooyour le reti virtuali. Vedere le macchine virtuali hello [percorso di apprendimento](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) per ulteriori informazioni.
