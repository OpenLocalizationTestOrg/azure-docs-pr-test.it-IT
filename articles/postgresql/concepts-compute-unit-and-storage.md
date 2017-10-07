---
title: "Descrizione delle unità di calcolo nel database di Azure per PostgreSQL | Microsoft Docs"
description: "Database di Azure per PostgreSQL: questo articolo illustra i concetti di hello di unità di calcolo e cosa accade quando il carico di lavoro raggiunge hello massimo di unità di calcolo."
services: postgresql
author: kamathsun
ms.author: sukamat
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 42ec766ff6ce82ceee34d42e0f4a4ad86bc7b45d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="explaining-compute-units-in-azure-database-for-postgresql"></a>Descrizione delle unità di calcolo nel database di Azure per PostgreSQL
Questo articolo viene illustrato il concetto di hello di unità di calcolo e cosa accade quando i carico di lavoro raggiunge hello massimo di unità di calcolo.

## <a name="what-are-compute-units"></a>Cosa sono le unità di calcolo?
Calcolo delle unità sono una misura della velocità effettiva di elaborazione della CPU che è garantita tooa disponibili toobe singolo Database di Azure per server PostgreSQL. Un'unità di calcolo è una misura combinata di risorse di CPU e memoria. In generale, 50 unità di calcolo equivalgono toohalf di un core. 100 unità di calcolo equivalgono tooone core. Unità di calcolo 2000 equivalgono tootwenty core del server di elaborazione garantita la velocità effettiva tooyour disponibili.

quantità di Hello di memoria per ogni unità di calcolo è ottimizzato per hello Basic e i livelli di prezzo Standard. Raddoppiando hello unità di calcolo per aumentare il livello di prestazioni hello equivale a set di hello toodoubling di risorse disponibili toothat singolo Database di Azure per PostgreSQL.

Ad esempio, 800 unità di calcolo Standard offrono una velocità effettiva della CPU e una memoria maggiori di 8 volte rispetto alla configurazione di 100 unità di calcolo Standard. Tuttavia, anche se le unità di calcolo 100 Standard fornisce hello stessa velocità effettiva della CPU rispetto tooBasic 100 unità di calcolo, hello memoria preconfigurato nel piano tariffario Standard è double il hello quantità di memoria configurata per livello di prezzo di base. Pertanto, piano tariffario Standard fornisce migliorare le prestazioni del carico di lavoro e la latenza delle transazioni inferiore rispetto a livello di prezzo di base con hello che stesse unità di calcolo selezionata.

## <a name="how-can-i-determine-hello-number-of-compute-units-needed-for-my-workload"></a>Come è possibile determinare il numero di hello di unità di calcolo necessarie per il carico di lavoro?
Se si vuole toomigrate un server PostgreSQL esistente in esecuzione in locale o in una macchina virtuale, è possibile determinare il numero di hello di unità di calcolo tramite la stima il numero di core della velocità effettiva di elaborazione è necessario il carico di lavoro. 

Se il server esistente nella macchina virtuale o locale sta attualmente usando 4 core, senza contare l'hyperthread CPU, è possibile iniziare configurando 400 unità di calcolo per il database di Azure per il server PostgreSQL. Le unità di calcolo possono essere aumentate o ridotte in modo dinamico in base alle esigenze del carico di lavoro praticamente senza tempi di inattività dell'applicazione. 

Grafico di metriche di monitoraggio hello in hello Azure portal o scrittura CLI di Azure i comandi - toomeasure unità di calcolo. Le metriche pertinenti toomonitor sono percentuale di unità di calcolo hello e limite di unità di calcolo.

>[!IMPORTANT]
> Se si trova l'account di archiviazione IOPS non completamente utilizzate toohello massimo, prendere in considerazione monitoraggio utilizzo nonché di hello calcolo unità. Generazione di unità di calcolo hello potrebbe consentono una velocità effettiva dei / o riducendo collo di bottiglia delle prestazioni hello scadenza toolimited CPU o memoria.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>Raggiungimento del numero massimo di unità di calcolo
Livelli di prestazioni sono calibrati e governato tooprovide risorse toorun toohello limiti max per piano tariffario selezionato hello e livello di prestazioni del carico di lavoro del database. 

Se il carico di lavoro raggiunge i limiti massimi di hello in sia hello calcolo unità o i limiti IOPS provisioning, è possibile continuare le risorse di hello tooutilize livello hello massimo consentito, ma le query sono le latenze toosee probabilmente aumentato. Questi limiti non generano errori, ma piuttosto un rallentamento del carico di lavoro di hello, a meno che il rallentamento hello più grave in modo che le query timeout. 

Se il carico di lavoro raggiunge i limiti massimi di hello numero di connessioni, vengono generati errori espliciti. Per altre informazioni sul limite delle risorse, vedere [Limiti del Database di Azure per PostgreSQL](concepts-limits.md).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere [Database di Azure per il piano tariffario di PostgreSQL](./concepts-service-tiers.md).
