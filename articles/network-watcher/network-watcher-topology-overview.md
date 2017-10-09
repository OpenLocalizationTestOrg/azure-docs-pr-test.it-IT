---
title: tootopology aaaIntroduction in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina fornisce una panoramica delle funzionalità di topologia hello Watcher di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a>Introduzione tootopology in Watcher di rete di Azure

La topologia restituisce un grafico delle risorse di rete in una rete virtuale. grafico di Hello illustra l'interconnessione hello tra hello risorse toorepresent hello fine tooend la connettività di rete.

![Panoramica della topologia][1]

Nel portale di hello topologia restituisce oggetti risorsa hello in una base di rete virtuale. relazioni Hello sono rappresentate dalle linee tra risorse hello risorse all'esterno di area di hello Watcher di rete, anche se nella risorsa hello gruppo non verrà visualizzato. risorse di Hello restituite nella visualizzazione portale hello sono un subset di componenti che sono rappresentate hello. elenco completo di hello toosee delle risorse di rete è possibile utilizzare [PowerShell](network-watcher-topology-powershell.md) o [REST](network-watcher-topology-rest.md)

> [!NOTE]
> È necessaria un'istanza del controllo di rete in ogni area che si desidera includere toorun topologia.

Poiché le risorse vengono restituite connessione hello tra di essi vengono modellati in due relazioni.

- **Contenimento** - Esempio: la rete virtuale contiene una subnet che contiene una scheda di interfaccia di rete.
- **Associazione** - Esempio: una scheda NIC è associata a una macchina virtuale

### <a name="next-steps"></a>Passaggi successivi

Informazioni su come toouse PowerShell tooretrieve hello topologia visualizzare visitando [topologia Watcher di rete con PowerShell](network-watcher-topology-powershell.md)

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
