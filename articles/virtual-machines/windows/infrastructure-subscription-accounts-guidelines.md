---
title: aaaSubscription e gli account per le macchine virtuali Windows in Azure | Documenti Microsoft
description: Informazioni su hello progettazione e implementazione di linee guida fondamentali per le sottoscrizioni e account in Azure.
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 761fa847-78b0-4078-a33a-d95d198d1029
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f9dc712af559b04490be1dc721a9b9f7fe9ed88f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-subscription-and-accounts-guidelines-for-windows-vms"></a>Linee guida per le sottoscrizioni e gli account Azure per macchine virtuali Windows

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

In questo articolo si incentra sulla comprensione di come si espande tooapproach sottoscrizione e account di gestione, come l'ambiente e un utente di base.

## <a name="implementation-guidelines-for-subscriptions-and-accounts"></a>Linee guida per l'implementazione di sottoscrizioni e account
Decisioni:

* Il set di account e sottoscrizioni è necessario toohost l'infrastruttura o il carico di lavoro IT?
* Come toobreak verso il basso hello gerarchia toofit organizzazione?

Attività:

* Definire la gerarchia logica dell'organizzazione che si desidera toomanage dal livello di sottoscrizione.
* toomatch questa gerarchia logica, definire gli account di hello necessari e le sottoscrizioni con ogni account.
* Creare set di hello di sottoscrizioni e gli account utilizzando la convenzione di denominazione.

## <a name="subscriptions-and-accounts"></a>Sottoscrizioni e account
toowork con Azure, è necessario uno o più sottoscrizioni di Azure. Nell'ambito di tali sottoscrizioni sono presenti risorse come le macchine virtuali o le reti virtuali.

* I clienti aziendali hanno in genere un'iscrizione Enterprise, risorse di primo piano hello nella gerarchia di hello, e tooone associato o altri account.
* Per utenti e i clienti senza un'iscrizione Enterprise, risorse di primo piano hello sono account hello.
* Le sottoscrizioni sono associati tooaccounts e possono essere presenti uno o più sottoscrizioni per l'account. Azure record di informazioni a livello di sottoscrizione hello di fatturazione.

A causa di limite toohello due di livelli della gerarchia in relazione tra Account o una sottoscrizione di hello, è importante tooalign convenzione di denominazione hello di account e sottoscrizioni toohello esigenze di fatturazione. Ad esempio, una società globale Usa Azure, possono scegliere account toohave uno per ogni area e avranno sottoscrizioni gestite a livello di area hello:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub01.png)

Ad esempio, è possibile utilizzare hello seguente struttura:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub02.png)

Se un'area decide toohave più gruppo specifico di una sottoscrizione associata tooa, convenzione di denominazione hello deve includere un tooencode modo hello dati aggiuntivi sul conto hello o nome della sottoscrizione hello. Questa organizzazione consente Ritocco dei fatturazione dati toogenerate hello nuovi livelli di gerarchia durante la fatturazione di report:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub03.png)

organizzazione Hello potrebbe essere simile hello di esempio seguente:

![](./media/virtual-machines-common-infrastructure-service-guidelines/sub04.png)

Viene fornita la fatturazione dettagliata tramite un file scaricabile, per un singolo account o per tutti gli account di un contratto Enterprise.

## <a name="next-steps"></a>Passaggi successivi
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

