---
title: visualizzazione del gruppo toosecurity aaaIntroduction in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello funzionalità di visualizzazione sicurezza Watcher di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a>Visualizzazione del gruppo protezione toonetwork introduzione in Watcher di rete di Azure

I gruppi di sicurezza di rete sono associati a un livello di subnet o a un livello di scheda di interfaccia di rete. Quando associato a un livello di subnet, si applica le istanze VM hello tooall nella subnet hello. Visualizzazione del gruppo di sicurezza di rete restituisce tutti i NSGs hello configurata e le regole che sono associate a un livello di interfaccia di rete e subnet per una macchina virtuale per fornire informazioni sulle configurazione hello. Inoltre, le regole di sicurezza efficace hello vengono restituite per ognuna delle schede NIC hello in una macchina virtuale. Usando la visualizzazione dei gruppi di sicurezza di rete, è possibile valutare le vulnerabilità di rete di una VM, ad esempio le porte aperte. È anche possibile verificare se il gruppo di sicurezza di rete funzioni come previsto in base a un [confronto tra hello configurato e regole di sicurezza efficace hello](network-watcher-nsg-auditing-powershell.md).

Un caso d'uso più esteso include la conformità alla sicurezza e il controllo della sicurezza. È possibile definire un set prescrittivo di regole di sicurezza come modello per la governance della sicurezza nell'organizzazione. Un controllo di conformità periodico può essere implementato in un modo programmatico confrontando le regole di normative hello con regole efficaci hello per ognuna delle macchine virtuali di hello nella rete.

In hello regole portale siano divisi da effettivo, Subnet, l'interfaccia di rete e predefiniti. Ciò fornisce una visualizzazione semplice in macchina virtuale di hello regole applicate tooa. Un pulsante di download viene fornito tooeasily scaricare tutte le regole di sicurezza hello indipendentemente dalla scheda hello in un file CSV.

![Visualizzazione di un gruppo di sicurezza][1]

È possibile selezionare le regole e i prefissi di gruppo di sicurezza di rete e di origine e di destinazione hello tooshow apre un nuovo pannello. Questo pannello è possibile passare direttamente toohello risorsa del gruppo di sicurezza di rete.

![Drill-down][2]

### <a name="next-steps"></a>Passaggi successivi

Informazioni su come tooaudit la sicurezza della rete gruppo impostazioni visitando [delle impostazioni di controllo gruppo di sicurezza di rete con PowerShell](network-watcher-nsg-auditing-powershell.md)

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









