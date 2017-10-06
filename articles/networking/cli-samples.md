---
title: Esempi di CLI aaaAzure | Documenti Microsoft
description: Esempi dell'interfaccia della riga di comando di Azure
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 8001b7e72480cfd0122325f7fb81c32aaad072d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-networking"></a>Esempi dell'interfaccia della riga di comando di Azure per la rete

Hello nella tabella seguente include gli script toobash collegamenti compilati utilizzando hello CLI di Azure.

| | |
|-|-|
|**Connettività tra risorse di Azure**||
| [Creare una rete virtuale per le applicazioni multilivello](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea una rete virtuale con subnet front-end e back-end. Subnet con traffico toohello front-end è limitato tooHTTP e SSH, mentre il traffico toohello subnet back-end è limitato tooMySQL, porta 3306. |
| [Eseguire il peering di due reti virtuali](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea e si connette due reti virtuali in hello stessa area. |
| [Instradare il traffico attraverso un'appliance virtuale di rete](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea una rete virtuale e una macchina virtuale che è in grado di tooroute traffico tra subnet hello due subnet front-end e back-end. |
| [Filtrare il traffico della VM in ingresso e in uscita](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea una rete virtuale con subnet front-end e back-end. Il traffico di rete in ingresso subnet front-end toohello è limitato tooHTTP, SSH e HTTPS. Non è consentito il traffico in uscita toohello Internet dalla subnet di back-end hello. |
|**Bilanciamento del carico e direzione del traffico**||
| [Caricare tooVMs di bilanciare il traffico per la disponibilità elevata](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | Consente di creare più macchine virtuali in una configurazione a disponibilità elevata e con bilanciamento del carico. |
| [Eseguire il bilanciamento del carico per più siti Web sulle VM](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | Crea due macchine virtuali con più configurazioni IP, tooan aggiunti a un Set di disponibilità, accessibile tramite un servizio di bilanciamento del carico di Azure. |
| [Dirigere il traffico su più aree per la disponibilità elevata delle applicazioni](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  Crea due piani di servizio app, due app Web, un profilo di gestione traffico e due endpoint di gestione traffico. |
| | |
