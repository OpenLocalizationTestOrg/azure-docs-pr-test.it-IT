---
title: raccomandazioni di Advisor costo aaaAzure | Documenti Microsoft
description: Utilizzare Advisor Azure toooptimize hello costo delle distribuzioni di Azure.
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: 50f70c33a17f550c8753795435cdfddd51e409f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-cost-recommendations"></a>Consigli di Advisor sui costi

Advisor aiuta a ottimizzare e ridurre la spesa complessiva legata ad Azure identificando le risorse inattive e sottoutilizzate. È possibile Ottieni suggerimenti di hello **costo** scheda nel dashboard di Advisor hello.

![Scheda Costo di Advisor](./media/advisor-cost-recommendations/advisor-cost-tab2.png)

## <a name="optimize-virtual-machine-spend-by-resizing-underutilized-instances"></a>Ottimizzare la spesa correlata alle macchine virtuali ridimensionando le istanze sottoutilizzate 
Sebbene alcuni scenari di applicazione possono comportare un utilizzo ridotto in base alla progettazione, è possibile salvare spesso money gestendo hello dimensioni e il numero di macchine virtuali. Advisor monitora l'utilizzo delle macchine virtuali per 14 giorni, in modo da identificare le macchine virtuali il cui utilizzo è ridotto. Le macchine virtuali con un utilizzo della CPU pari al 5% o inferiore e un utilizzo di rete pari a 7 MB o inferiore per quattro o più giorni sono considerate macchine virtuali il cui utilizzo è ridotto.

Mostra Advisor hello costo stimato di continuare toorun la macchina virtuale, in modo da poter scegliere tooshut verso il basso oppure ridimensionarlo.  

![Consigli di Advisor sui costi per il ridimensionamento delle macchine virtuali](./media/advisor-cost-recommendations/advisor-cost-resizevms.png)

## <a name="use-a-cost-effective-solution-toomanage-performance-goals-of-multiple-sql-databases"></a>Utilizzare obiettivi di prestazioni toomanage una soluzione a costi contenuti di più database SQL
Advisor identifica le istanze di SQL Server che possono trarre vantaggio dalla creazione di pool di database elastici. Pool di database elastici forniscono toomanage una soluzione semplice e conveniente obiettivi di prestazioni hello di più database con diversi modelli di utilizzo. Per altre informazioni sui pool elastici di Azure, vedere [Cos'è un pool elastico di Azure?](https://azure.microsoft.com/en-us/documentation/articles/sql-database-elastic-pool/).

![Consigli di Advisor sui costi per pool di database elastici](./media/advisor-cost-recommendations/advisor-cost-elasticdbpools.png)

## <a name="how-tooaccess-cost-recommendations-in-azure-advisor"></a>Come tooaccess costo indicazioni in preparazione di Azure

1. Accedi toohello [portale di Azure](https://portal.azure.com).

2. Nel riquadro di sinistra hello, fare clic su **più servizi**.

3. Hello servizio dei menu, in **monitoraggio e gestione**, fare clic su **Advisor Azure**.  
 Hello Advisor dashboard viene visualizzato.

4. Nel dashboard di Advisor hello, fare clic su hello **costo** scheda.

5. Selezionare hello sottoscrizione per il quale desidera tooreceive indicazioni e quindi fare clic su **consigli**.

> [!NOTE]
> tooaccess raccomandazioni di Advisor, è innanzitutto necessario *registrare la sottoscrizione* con Advisor. Una sottoscrizione viene registrata quando un *sottoscrizione proprietario* avvia hello hello di dashboard e fa clic su Advisor **consigli** pulsante. Si tratta di un'*operazione una tantum*. Dopo la sottoscrizione hello è registrata, è possibile accedere raccomandazioni di Advisor come *proprietario*, *collaboratore*, o *lettore* per una sottoscrizione, un gruppo di risorse, o risorsa specifica.

## <a name="next-steps"></a>Passaggi successivi

toolearn sulle raccomandazioni di Advisor, vedere:
* [Introduzione tooAdvisor](advisor-overview.md)
* [esercitazione introduttiva](advisor-get-started.md)
* [Advisor Performance recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulle prestazioni)
* [Advisor High Availability recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla disponibilità elevata)
* [Advisor Security recommendations](advisor-cost-recommendations.md) (Consigli di Advisor sulla sicurezza)
