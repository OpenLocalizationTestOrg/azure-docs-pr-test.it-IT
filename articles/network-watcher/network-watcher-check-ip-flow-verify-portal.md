---
title: Verificare il traffico aaaVerify con flusso di controllo indirizzo IP rete di Azure - portale di Azure | Documenti Microsoft
description: "Questo articolo viene descritto come toocheck se tooor il traffico da una macchina virtuale è consentito o negato"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Verifica se il traffico non è consentito o negato tooor da una macchina virtuale con IP flusso verificare un componente del controllo di rete di Azure

> [!div class="op_single_selector"]
> - [Portale di Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Interfaccia della riga di comando 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [Interfaccia della riga di comando 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [API REST di Azure](network-watcher-check-ip-flow-verify-rest.md)


Verificare di flusso IP è una funzionalità di controllo di rete che consente tooverify se il traffico consentito tooor da una macchina virtuale. è possibile eseguire la convalida di Hello per il traffico in ingresso o in uscita. Questo scenario è utile tooget uno stato corrente di fatto una macchina virtuale possono comunicare con la risorsa esterna tooan o un'altra risorsa. Verificare di flusso IP può essere utilizzato tooverify se le regole di sicurezza gruppo (rete) sono configurate correttamente e risolvere i problemi di flussi che sono bloccati dalle regole di gruppo. Un altro motivo per l'uso di IP flusso verificare tooensure che si desidera bloccare il traffico viene bloccato correttamente dal gruppo hello.

## <a name="before-you-begin"></a>Prima di iniziare

Questo scenario si presuppone che si sono già stati seguiti i passaggi di hello in [creare un controllo di rete](network-watcher-create.md) toocreate Watcher di rete o dispone di un'istanza esistente del controllo di rete. scenario di Hello si suppone inoltre che un gruppo di risorse con una macchina virtuale valida toobe utilizzato.

## <a name="scenario"></a>Scenario

Questo scenario Usa tooverify IP flusso verificare se una macchina virtuale possono comunicare con computer tooanother sulla porta 443. Regola di sicurezza hello che nega il traffico viene restituito se il traffico hello viene negato. toolearn ulteriori informazioni su IP flusso verificare, visitare [IP Flow verificare Overview](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Eseguire la verifica del flusso IP

Passare tooyour Watcher di rete e fare clic su **flusso IP verificare**. Selezionare macchina virtuale hello e interfaccia di rete tooverify traffico da. Immettere le eventuali informazioni di filtro aggiuntive e fare clic su **Controlla**.

Quando si fa clic su **controllare**, flusso hello in base ai criteri di hello immessa è selezionato. risultato Hello è **accesso consentito** o **accesso negato**. Se l'accesso è negato, hello gruppo di sicurezza (rete) e regola di sicurezza che bloccano il traffico è disponibile. Se un attacco denial hello del traffico è il comportamento previsto, la regola hello è riuscita.

> [!NOTE]
> Flusso IP verificare richiede che venga allocata risorsa macchina virtuale hello.

Come si può vedere dal hello seguente immagine, è consentito il traffico HTTPS in uscita hello.

![Panoramica della verifica del flusso IP][1]

Come mostrato nella seguente immagine hello, viene modificato il traffico tooinbound e hello in entrata too123 porta modificata. Traffico ora viene negato, il messaggio hello "Accesso negato" viene fornito insieme hello rete gruppo e sicurezza regola di sicurezza negare il traffico di hello.

![Risultati del flusso di IP][2]

## <a name="next-steps"></a>Passaggi successivi

Se il traffico viene bloccato e non può essere, vedere [gestire gruppi di sicurezza di rete](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack verso il basso hello rete sicurezza e gruppo di regole di sicurezza definiti.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













