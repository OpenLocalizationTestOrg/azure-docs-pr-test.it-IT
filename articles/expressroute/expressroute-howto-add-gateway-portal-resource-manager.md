---
title: 'Aggiungere un tooa di gateway di rete virtuale tra reti virtuali per ExpressRoute: portale: Azure | Documenti Microsoft'
description: "In questo articolo viene illustrata l'aggiunta di un tooan di gateway di rete virtuale già creata VNet Gestione risorse per ExpressRoute."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a>Configurare un gateway di rete virtuale per hello portale di Azure tramite ExpressRoute
> [!div class="op_single_selector"]
> * [Resource Manager - Portale di Azure](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [Resource Manager - PowerShell](expressroute-howto-add-gateway-resource-manager.md)
> * [Classica: PowerShell](expressroute-howto-add-gateway-classic.md)
> * [Video - Portale di Azure](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

In questo articolo illustra hello passaggi tooadd un gateway di rete virtuale per una rete virtuale esistente. Questo articolo illustra hello passaggi tooadd, ridimensionare e rimuovere un gateway di rete virtuale (VNet) per una rete virtuale esistente. passaggi di Hello per questa configurazione sono in particolare per le reti virtuali creati con modello di distribuzione di gestione risorse hello che verrà utilizzato in una configurazione di ExpressRoute. Per altre informazioni sui gateway di rete virtuale e sulle impostazioni di configurazione dei gateway per ExpressRoute, vedere [Informazioni sui gateway di rete virtuale per ExpressRoute](expressroute-about-virtual-network-gateways.md). 


## <a name="before-beginning"></a>Prima di iniziare

i passaggi di Hello per questa attività, utilizzare una rete virtuale in base ai valori hello hello seguente elenco di riferimento configurazione. Nelle procedure degli esempi viene usato questo elenco. È possibile copiare hello elenco toouse come riferimento, sostituendo i valori hello con valori personalizzati.

**Elenco di riferimento per la configurazione**

* Nome rete virtuale = "TestVNet"
* Spazio degli indirizzi della rete virtuale = 192.168.0.0/16
* Nome subnet: "FrontEnd" 
    * Spazio degli indirizzi della subnet = "192.168.1.0/24"
* Gruppo di risorse = "TestRG"
* Località = "Stati Uniti orientali"
* Nome subnet del gateway: "GatewaySubnet" Il nome della subnet del gateway deve sempre essere *GatewaySubnet*.
    * Spazio degli indirizzi della subnet gateway = "192.168.200.0/26"
* Nome del gateway = "ERGW"
* Nome del gateway IP = "MyERGWVIP"
* Tipo di gateway = "ExpressRoute" Questo tipo è necessario per una configurazione ExpressRoute.
* Nome IP pubblico del gateway = "MyERGWVIP"

È possibile visualizzare un [video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) relativo a questi passaggi prima di avviare la configurazione.

## <a name="create-hello-gateway-subnet"></a>Creare subnet del gateway hello

1. In hello [portal](http://portal.azure.com), passare toohello Gestione risorse rete virtuale per cui si desidera toocreate un gateway di rete virtuale.
2. In hello **impostazioni** sezione del pannello rete virtuale, fare clic su **subnet** blade di subnet tooexpand hello.
3. In hello **subnet** pannello, fare clic su **+ subnet del Gateway** tooopen hello **aggiungere subnet** blade. 
   
    ![Aggiungi subnet gateway hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Aggiungi subnet gateway hello")


4. Hello **nome** per la subnet viene automaticamente inserita hello valore 'GatewaySubnet'. Questo valore è necessario per la subnet hello Azure toorecognize come subnet del gateway hello. Regolare hello riempimento automatico **intervallo di indirizzi** valori toomatch requisiti di configurazione. È consigliabile creare una subnet del gateway con un valore /27 o superiore (/26, /25 e così via). Quindi, fare clic su **OK** toosave hello valori e creare subnet del gateway hello.

    ![Aggiunta della subnet hello](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "aggiungendo hello subnet")

## <a name="create-hello-virtual-network-gateway"></a>Creare il gateway di rete virtuale hello

1. Nel portale di hello sul lato sinistro di hello, fare clic su  **+**  e digitare 'Gateway della rete virtuale' nella ricerca. Individuare **gateway di rete virtuale** nella ricerca hello restituire e fare clic sulla voce hello. In hello **gateway di rete virtuale** pannello, fare clic su **crea** nella parte inferiore di hello del pannello hello. Verrà visualizzata hello **gateway di rete virtuale crea** blade.
2. In hello **gateway di rete virtuale crea** pannello, compilare i valori hello per il gateway di rete virtuale.

    ![Creare i campi nel pannello Gateway di rete virtuale](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Creare i campi nel pannello Gateway di rete virtuale")
3. **Nome**: assegnare un nome al gateway. Questo non è hello uguale a una subnet del gateway di denominazione. Nome di hello dell'oggetto gateway hello che si sta creando del.
4. **Tipo di gateway**: selezionare **ExpressRoute**.
5. **SKU**: lo SKU del gateway hello selezionare dall'elenco a discesa hello.
6. **Percorso**: regolare hello **percorso** campo toopoint toohello percorso in cui si trova la rete virtuale. Se il percorso di hello non punta toohello area in cui risiede la rete virtuale, rete virtuale hello non viene visualizzato nell'elenco a discesa 'Scegliere una rete virtuale' hello.
7. Scegliere toowhich di rete virtuale hello desiderato tooadd questo gateway. Fare clic su **rete virtuale** tooopen hello **scegliere una rete virtuale** blade. Selezionare hello rete virtuale. Se la rete virtuale non viene visualizzata, verificare che hello **percorso** campo punta toohello area in cui si trova la rete virtuale.
9. Definire un indirizzo IP pubblico. Fare clic su **indirizzo IP pubblico** tooopen hello **scegliere l'indirizzo IP pubblico** blade. Fare clic su **+ creare nuovi** tooopen hello **blade di indirizzo IP pubblico crea**. Immettere un nome per l'indirizzo IP pubblico. Questo pannello Crea un toowhich di oggetto indirizzo IP pubblico assegnato dinamicamente un indirizzo IP pubblico. Fare clic su **OK** toosave il pannello toothis le modifiche.
10. **Sottoscrizione**: verificare che hello corretto sottoscrizione sia selezionata.
11. **Gruppo di risorse**: questa impostazione è determinata dalla hello rete virtuale selezionata.
12. Non modificare hello **percorso** dopo aver specificato le impostazioni precedenti hello.
13. Verificare le impostazioni di hello. Se si desidera tooappear il gateway nel dashboard di hello, è possibile selezionare **toodashboard Pin** nella parte inferiore di hello del pannello hello.
14. Fare clic su **crea** toobegin creazione gateway hello. impostazioni di Hello vengono convalidate e distribuisce gateway hello. Creazione del gateway di rete virtuale può richiedere too45 minuti toocomplete.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver creato il gateway di rete virtuale hello, è possibile collegare il circuito ExpressRoute di tooan di rete virtuale. Vedere [collegare un circuito ExpressRoute di tooan rete virtuale](expressroute-howto-linkvnet-portal-resource-manager.md).
