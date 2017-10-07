---
title: aaaIntroduction toonext hop Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello Watcher di rete dalla capacità dell'hop successiva"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a>Hop toonext introduzione Watcher di rete di Azure

Il traffico proveniente da una macchina virtuale viene inviato a destinazione tooa in base a route valide di hello associate a una scheda di rete. Hop successivo Ottiene il tipo dell'hop successivo di hello e l'indirizzo IP di un pacchetto da una macchina virtuale specifica e una scheda di rete. In questo modo toodetermine se hello pacchetto è in corso destinazione toohello diretti o è holed traffico hello in nero. Una configurazione non corretta di route da hello utente, in cui il traffico di un percorso locale tooan diretti o da un dispositivo virtuale, può causare problemi di tooconnectivity. Hop successivo restituisce anche tabella di route hello associata all'hop successivo hello. Quando si eseguono query hop successivo itinerario hello è definito come una route definita dall'utente, verrà restituito tale route. In caso contrario l'hop successivo restituisce la route di sistema.

![Panoramica dell'hop successivo][1]

Hello seguito è riportato un elenco di tipi di hop successivi hello che possono essere restituiti quando si eseguono query hop successivo.

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

### <a name="next-steps"></a>Passaggi successivi

Informazioni su come toofind hop successivo toouse problemi con la connettività di rete, visitare il sito [controllo hello dell'hop successivo in una macchina virtuale](network-watcher-check-next-hop-portal.md)

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













