---
title: aaaConfigure una rete virtuale e il Gateway per ExpressRoute nel portale classico di hello | Documenti Microsoft
description: Questo articolo viene illustrato come configurare una rete virtuale per ExpressRoute tramite il modello di distribuzione classica hello e portale classico hello.
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 688817d9-51c8-4372-9af8-33fa098c7c5a
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/20/2016
ms.author: cherylmc
ms.openlocfilehash: dd1f6c5e85dbb3ad0a53ecd81c13b4d3f5c06e66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-for-expressroute-in-hello-classic-portal"></a>Creare una rete virtuale per ExpressRoute nel portale classico hello
passaggi di Hello in questo articolo verranno consentono di configurare una rete virtuale e un gateway di rete virtuale per l'uso con ExpressRoute utilizzando il modello di distribuzione classica hello e portale classico hello.

Se si desidera utilizzare le istruzioni per modello di distribuzione di gestione risorse di hello, è possibile utilizzare i seguenti articoli hello: [creare una rete virtuale mediante PowerShell](../virtual-network/virtual-networks-create-vnet-arm-ps.md) e [aggiungere tooa un Gateway VPN VNet Gestione risorse per ExpressRoute](expressroute-howto-add-gateway-resource-manager.md).

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

**Informazioni sui modelli di distribuzione di Azure**

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="create-a-classic-vnet-and-gateway"></a>Creare una rete virtuale classica e un gateway
Hello seguenti passaggi necessari per creare una rete virtuale classica e un gateway di rete virtuale. Se si dispone già di una rete virtuale classica, vedere hello [configurare una rete virtuale classica esistente](#config) sezione in questo articolo.

1. Accedi toohello [portale di Azure classico](http://manage.windowsazure.com).
2. Hello angolo in basso a sinistra della schermata ciao, fare clic su **New**. Nel riquadro di spostamento hello, fare clic su **servizi di rete**, quindi fare clic su **rete virtuale**. Fare clic su **creazione personalizzata** configurazione guidata di toobegin hello.
3. In hello **dettagli rete virtuale** pagina, immettere hello seguenti:
   
   * **Nome** : assegnare un nome alla rete virtuale. Quando si distribuiscono le macchine virtuali e istanze PaaS, pertanto è consigliabile non nome hello toomake troppo complicato, si utilizzerà il nome di rete virtuale.
   * **Percorso** : hello località è direttamente correlata toohello fisica (regione) in cui si desidera tooreside le risorse (macchine virtuali). Ad esempio, se si desidera hello macchine virtuali distribuite toothis toobe di rete virtuale che si trova fisicamente negli Stati Uniti orientali, selezionare tale posizione. È possibile modificare l'area di hello associata con la rete virtuale dopo averla creata.
4. In hello **server DNS e connettività VPN** pagina, immettere le seguenti informazioni hello e quindi fare clic sulla freccia avanti hello in basso a destra hello. 
   
   * **I server DNS** - immettere nome hello del server DNS e indirizzo IP o selezionare un server DNS registrato in precedenza dal menu di scelta rapida hello. Questa impostazione non comporta la creazione di un server DNS. Consente i server DNS di hello toospecify che si vuole toouse per la risoluzione dei nomi per la rete virtuale.
   * **Connettività Site-to-Site** : selezionare questa opzione hello casella di controllo per **configurare una VPN site-to-site**.
   * **ExpressRoute** : selezionare la casella di controllo di hello **Usa ExpressRoute**. Questa opzione viene visualizzata solo se è stata selezionata **Configura una VPN Site-To-Site**.
   * **Rete locale** -si è toohave richiesto un sito di rete locale per ExpressRoute. Tuttavia, nel caso di hello di una connessione ExpressRoute, i prefissi di indirizzo hello specificato per hello locale sito di rete verrà ignorato. Al contrario, i prefissi di indirizzo hello annunciati tooMicrosoft tramite hello circuito ExpressRoute verrà utilizzato a scopo di routing.<BR>Se si dispone già di una rete locale creata per la connessione ExpressRoute, è possibile selezionarlo dall'elenco a discesa hello. In caso contrario, selezionare **Specificare una nuova rete locale**.
5. Hello **connettività Site-to-Site** verrà visualizzata la pagina se è stata selezionata nel passaggio precedente hello toospecify una nuova rete locale. tooconfigure la rete locale, immettere le seguenti informazioni hello e quindi fare clic sulla freccia avanti hello. 
   
   * **Nome** -nome hello da toocall locale del sito di rete (locale).
   * **Spazio di indirizzi** : inclusi IP iniziale e CIDR (conteggio indirizzi). È possibile specificare qualsiasi intervallo di indirizzi, purché non si sovrappongono all'intervallo di indirizzi di hello per la rete virtuale. In genere, si specificherà intervalli di indirizzi hello per le reti locali, ma nel caso di hello di ExpressRoute, queste impostazioni non vengono utilizzate. Tuttavia, questa impostazione è necessaria nella rete locale di ordini toocreate hello quando si usa il portale classico di hello.
   * **Aggiungi spazio di indirizzi** : questa impostazione non è rilevante per ExpressRoute.
6. In hello **spazi degli indirizzi di rete virtuale** immettere hello le seguenti informazioni e quindi fare clic su hello segno di spunta tooconfigure destro inferiore hello della rete. 
   
   * **Spazio di indirizzi** : inclusi IP iniziale e conteggio indirizzi. Verificare che gli spazi degli indirizzi hello specificato non si sovrappongano agli hello gli spazi degli indirizzi presenti nella rete locale.
   * **Aggiungi subnet** inclusi IP iniziale e conteggio indirizzi. Non sono necessarie altre subnet.
   * **Aggiungi subnet gateway** -fare clic su subnet del gateway tooadd hello. subnet del gateway Hello viene utilizzato solo per il gateway di rete virtuale hello sia necessaria per questa configurazione.<BR>Hello CIDR (conteggio indirizzi) subnet del gateway per ExpressRoute deve essere/28 o superiore (/ 27/26 ecc.). Questo consente un numero sufficiente di indirizzi IP in tale configurazione toowork di subnet tooallow hello. Nel portale classico hello, se è stata selezionata la casella di controllo di hello toouse ExpressRoute, portale hello specifica una subnet del gateway con /28.  Conteggio di indirizzi CIDR hello nel portale classico hello non è possibile modificare. subnet del gateway Hello verrà visualizzato come **Gateway** nel portale classico hello, sebbene hello nome reale di subnet del gateway hello creato è effettivamente **GatewaySubnet**. È possibile visualizzare questo nome mediante PowerShell o nel portale di Azure hello.
7. Fare clic su hello segno di spunta nella parte inferiore di hello della pagina hello e la rete virtuale verrà avviata toocreate. Al termine, verrà visualizzato **creato** sotto **stato** su hello **reti** pagina nel portale classico hello.

## <a name="gw"></a>Creare il gateway hello
1. In hello **reti** pagina, fare clic su rete virtuale hello appena creato, quindi fare clic su **Dashboard** nella parte superiore di hello della pagina hello.
2. Nella parte inferiore di hello di hello **Dashboard** pagina, fare clic su **crea Gateway** e selezionare **Routing dinamico**. Fare clic su **Sì** tooconfirm che si desidera toocreate un gateway.
3. Quando si inizia a creare il gateway di hello, verrà visualizzato un messaggio che informa che gateway hello è stata avviata. Potrebbe richiedere fino a too45 minuti per toocreate gateway hello.
4. Collegamento del circuito tooa di rete. Seguire le istruzioni hello articolo hello [come toolink reti virtuali tooExpressRoute circuiti](expressroute-howto-linkvnet-classic.md).

## <a name="config"></a>Configurare una rete virtuale classica esistente per ExpressRoute
Se si dispone già di una rete virtuale classica, è possibile configurarlo nel portale classico hello tooconnect tooExpressRoute. le impostazioni di Hello sono hello stesso come sezioni hello precedenti, in modo da leggere tali toobecome sezioni familiarità con hello le impostazioni obbligatorie. Se si desidera toocreate una connessione coesistenti ExpressRoute/Site-to-Site, vedere [questo articolo](expressroute-howto-coexist-classic.md) per i passaggi di hello. Sono diversi rispetto a hello i passaggi in questo articolo.

1. Rete locale di toocreate hello è necessario prima di aggiornare altre hello impostazioni di rete virtuale. Fare clic su una nuova rete locale, è necessario quando si configura ExpressRoute tramite il portale classico di hello, toocreate **New**  **>**  **servizi di rete**  **>**  **Rete virtuale**  **>**  **rete locale aggiunta**. Seguire hello guidata passaggi toocreate hello locale di rete.
2. Utilizzare **configura** pagina rest hello tooupdate delle impostazioni di hello per la rete virtuale e tooassociate hello rete virtuale toohello rete locale.
3. Dopo avere configurato le impostazioni di hello, andare toohello [crea gateway hello](#gw) sezione del gateway di hello toocreate articolo.

## <a name="next-steps"></a>Passaggi successivi
* Se si desidera una rete virtuale tooyour di tooadd macchine virtuali, vedere [macchine virtuali di percorsi di formazione](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/).
* Se si desidera toolearn informazioni su ExpressRoute, vedere hello [panoramica relativa a ExpressRoute](expressroute-introduction.md).

