---
title: "Descrizione delle unità di calcolo nel database di Azure per MySQL | Microsoft Docs"
description: "Azure DB per MySQL: questo articolo spiega i concetti relativi alle unità di calcolo e ciò che accade quando il carico di lavoro raggiunge il livello massimo per le unità di calcolo."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 09/29/2017
ms.openlocfilehash: 2c4894ae9a4235f9ced4a8d9b991238543646f53
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="explaining-compute-units-in-azure-database-for-mysql"></a>Descrizione delle unità di calcolo nel database di Azure per MySQL
Questo argomento spiega i concetti relativi alle unità di calcolo e ciò che accade quando il carico di lavoro raggiunge il livello massimo per le unità di calcolo.

## <a name="what-are-compute-units"></a>Cosa sono le unità di calcolo?
Le unità sono una misura della velocità effettiva di elaborazione della CPU garantita come disponibile per un singolo database di Azure per il server MySQL. Un'unità di calcolo è una misura combinata di risorse di CPU e memoria. In generale, 50 unità di calcolo equivalgono a metà di un core. 100 unità di calcolo equivalgono a un core. 2.000 unità di calcolo equivalgono a 20 core di velocità effettiva di elaborazione garantita disponibile per il server.

La quantità di memoria per ogni unità di calcolo è ottimizzata per i piani tariffari Basic e Standard. Raddoppiare le unità di calcolo aumentando il livello di prestazioni equivale a raddoppiare il set di risorse disponibili per quel singolo database di Azure per MySQL.

Ad esempio, 800 unità di calcolo Standard offrono una velocità effettiva della CPU e una memoria maggiori di 8 volte rispetto alla configurazione di 100 unità di calcolo Standard. Tuttavia, mentre 100 unità di calcolo Standard offrono la stessa velocità effettiva della CPU rispetto a 100 unità di calcolo Basic, la quantità di memoria preconfigurata nel piano tariffario Standard è il doppio della quantità di memoria configurata per il piano tariffario Basic. Pertanto, il piano tariffario Standard offre prestazioni migliori del carico di lavoro e una latenza delle transazioni inferiore rispetto al piano tariffario Basic con le stesse unità di calcolo selezionate.

## <a name="how-can-i-determine-the-number-of-compute-units-needed-for-my-workload"></a>Come si determina il numero di unità di calcolo necessarie per il carico di lavoro?
Se si vuole eseguire la migrazione di un server MySQL esistente eseguito in locale o in una macchina virtuale, è possibile determinare il numero di unità di calcolo stimando il numero di core di velocità effettiva di elaborazione necessari per il carico di lavoro. 

Se il server esistente nella macchina virtuale o locale usa 4 core, senza contare l'hyperthread CPU, è possibile iniziare configurando 400 unità di calcolo per il database di Azure per il server MySQL. Le unità di calcolo possono essere aumentate o ridotte in modo dinamico in base alle esigenze del carico di lavoro e praticamente senza tempi di inattività dell'applicazione. 

Monitorare il grafico delle metriche nel portale di Azure o scrivere comandi dell'interfaccia della riga di comando di Azure per misurare le unità di calcolo. Le metriche pertinenti al monitoraggio sono la percentuale dell'unità di calcolo e il limite dell'unità di calcolo.

>[!IMPORTANT]
> Se le operazioni di I/O al secondo per l'archiviazione non vengono usate al massimo, tenere sotto controllo anche l'uso delle unità di calcolo. L'aumento delle unità di calcolo potrebbe consentire una maggiore velocità effettiva di I/O riducendo il collo di bottiglia delle prestazioni risultante dalla disponibilità limitata di CPU o memoria.

## <a name="what-happens-when-i-hit-my-maximum-compute-units"></a>Raggiungimento del numero massimo di unità di calcolo
I livelli di prestazioni vengono calibrati e gestiti per offrire le risorse necessarie per eseguire il carico di lavoro del database fino ai limiti massimi consentiti per il livello di prestazioni e il piano tariffario selezionati. 

Se il carico di lavoro raggiunge i limiti massimi per le unità di calcolo o per operazioni di I/O con provisioning, è possibile continuare a usare le risorse al massimo livello consentito, ma probabilmente si riscontrerà un aumento delle latenze per le query. Questi limiti causano un rallentamento nel carico di lavoro piuttosto che errori, a meno che il rallentamento non diventi così grave da provocare il timeout delle query. 

Se il carico di lavoro raggiunge i limiti massimi per quanto riguarda il numero di connessioni, vengono generati errori espliciti. Per altre informazioni sul limite delle risorse, vedere [Limiti del Database di Azure per MySQL](concepts-limits.md).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni, vedere [Database di Azure per il piano tariffario di MySQL](./concepts-service-tiers.md).
