---
title: ottimizzazione di Database SQL di Azure automatica aaaEnable | Documenti Microsoft
description: "È possibile abilitare facilmente l'ottimizzazione automatica nel database SQL di Azure."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a>Abilitare l'ottimizzazione automatica

Database SQL di Azure è un servizio di dati gestiti automaticamente che costantemente controlla le query e identifica l'azione di hello che è possibile eseguire tooimprove delle prestazioni del carico di lavoro. È possibile esaminare le raccomandazioni e applicarle manualmente oppure delegare al database SQL di Azure l'applicazione automatica delle azioni correttive, condizione nota come **modalità di ottimizzazione automatica**. L'ottimizzazione automatica può essere abilitata a livello di database di hello server hello o.

## <a name="enable-automatic-tuning-on-server"></a>Abilitare l'ottimizzazione automatica nel server

tooenable automatico ottimizzazione sul server di Database SQL di Azure, passare toohello server in Azure nel portale e quindi selezionare **ottimizzazione automatica** nel menu hello. Selezionare opzioni di ottimizzazione automatica tooenable desiderata e scegliere di hello **applica**:

![Server](./media/sql-database-automatic-tuning-enable/server.png)

Opzioni nel server di ottimizzazione automatici sono applicati tooall database server hello. Per impostazione predefinita, tutti i database ereditano la configurazione di hello dal relativo server padre, ma ciò può essere sottoposto a override e specificare singolarmente per ogni database.

## <a name="configure-automatic-tuning-on-database"></a>Configurare l'ottimizzazione automatica per il database

Hello Azure attiva portale si tooindividually specificare la configurazione di ottimizzazione automatica di hello in ciascun database.

> [!NOTE]
> raccomandazione generale Hello è toomanage hello ottimizzazione configurazione automatica a livello di server in questo caso hello stesse impostazioni di configurazione possono essere applicate automaticamente in ogni database. Configurare l'ottimizzazione automatica in un singolo database se hello database diversi che gli altri hello nello stesso server.
>

tooenable automatico ottimizzazione su un singolo database, passare toohello database nel portale di Azure hello e poi selezionare **ottimizzazione automatica**. È possibile configurare le impostazioni di hello tooinherit un singolo database dal database hello selezionando la casella di controllo hello oppure è possibile specificare singolarmente configurazione hello per un database.

![Database](./media/sql-database-automatic-tuning-enable/database.png)

Dopo aver selezionato la configurazione appropriata, fare clic su **Applica**.

## <a name="next-steps"></a>Passaggi successivi
* Hello lettura [articolo ottimizzazione automatica](sql-database-automatic-tuning.md) toolearn ulteriori informazioni sull'ottimizzazione automatica e la modalità consente di migliorare le prestazioni.
* Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.
* Vedere [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) toolearn sulla visualizzazione impatto sulle prestazioni hello per le prime query.
