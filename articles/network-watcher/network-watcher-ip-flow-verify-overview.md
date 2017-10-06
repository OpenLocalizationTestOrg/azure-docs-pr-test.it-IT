---
title: flusso tooIP aaaIntroduction verificare in Watcher di rete di Azure | Documenti Microsoft
description: "Questa pagina viene fornita una panoramica di hello IP Watcher di rete di flusso di verificare la funzionalità"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a>Flusso tooIP introduzione verificare in Watcher di rete di Azure

Flusso IP verificare controlla se un pacchetto è consentito o negato tooor da una macchina virtuale in base alle informazioni di 5 tuple. Tali informazioni sono costituite da direzione, protocollo, indirizzo IP locale, indirizzo IP remoto, porta locale e porta remota. Se i pacchetti hello viene negato da un gruppo di sicurezza, viene restituito il nome di hello della regola hello negato pacchetti hello. Mentre è possibile scegliere qualsiasi indirizzo IP di origine o destinazione, questa funzionalità consente agli amministratori di diagnosticare rapidamente i problemi di connettività da o toohello internet e da o toohello nell'ambiente locale.

La verifica del flusso IP esamina l'interfaccia di rete di una macchina virtuale. Il flusso del traffico viene quindi verificata in base a tooor impostazioni hello configurato dall'interfaccia di rete. Questa funzionalità è utile per confermare se una regola in un gruppo di sicurezza di rete sta bloccando tooor di traffico in ingresso o in uscita da una macchina virtuale.

Un'istanza di toobe esigenze Watcher di rete creato in tutte le aree che si prevede di flusso IP toorun verificare. Watcher di rete è un servizio regionale e possono essere eseguiti solo sulle risorse in hello stessa area. Questa operazione non influenza hello risultati del flusso IP verificare come route hello associato hello che NIC verrà comunque restituito.

![1][1]

## <a name="next-steps"></a>Passaggi successivi

Visitare il seguente articolo toolearn se un pacchetto è consentito o negato per una macchina virtuale specifica tramite il portale di hello hello. [Controllare se il traffico è consentito in una macchina virtuale con flusso verificare IP tramite il portale di hello](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












