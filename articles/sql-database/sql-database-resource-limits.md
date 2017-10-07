---
title: Limiti delle risorse del Database SQL aaaAzure | Documenti Microsoft
description: In questa pagina vengono descritti alcuni limiti di risorse comuni per il Database SQL Azure.
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 884e519f-23bb-4b73-a718-00658629646a
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2017
ms.author: carlrab
ms.openlocfilehash: 3e7be4fdc74e802d37274690531caaf138bcedb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-resource-limits"></a>Limiti delle risorse del database SQL di Azure
## <a name="overview"></a>Panoramica
Database SQL di Azure gestisce i database delle risorse hello tooa disponibili tramite due meccanismi diversi: **governance delle risorse** e **imposizione dei limiti**. Questo argomento illustra queste due aree principali relative alla gestione delle risorse.

## <a name="resource-governance"></a>Governance delle risorse
Per Database SQL di Azure toobehave uno degli obiettivi di progettazione hello dei livelli di servizio Basic, Standard, Premium e RS Premium hello è come se il database di hello è in esecuzione sul proprio computer, isolato dagli altri database. La governance delle risorse emula questo comportamento. Se hello aggregato utilizzo delle risorse raggiunge hello massimo disponibile della CPU, memoria, i/o di Log e database toohello assegnato alle risorse dei / o dati, la governance delle risorse le query di code in esecuzione e assegnare toohello query man mano che vengono accodati liberare risorse.

Come in un computer dedicato, che utilizzano tutti i risultati di risorse disponibili durante l'esecuzione di query, attualmente in esecuzione più lunga che possono portare a timeout comando in client hello. Applicazioni con intensa logica di tentativi e le applicazioni che eseguono query sul database hello con frequenza elevata possono verificarsi i messaggi di errori durante il tentativo di nuove query tooexecute quando viene raggiunto il limite di hello di richieste simultanee.

### <a name="recommendations"></a>Consigli:
Monitorare l'utilizzo delle risorse hello e tempi di risposta medio hello delle query all'approssimarsi hello uso massimo di un database. Quando si verificano latenze di query più elevate, sono disponibili tre opzioni:

1. Ridurre il numero di hello di in ingresso richieste toohello database tooprevent timeout e hello accumulo delle richieste.
2. Assegnare un database di toohello di livello superiore di prestazioni.
3. Ottimizzare le query tooreduce hello utilizzo delle risorse di ogni query. Per ulteriori informazioni, vedere hello sezione hint/ottimizzazione di Query dell'articolo hello linee guida sulle prestazioni di Database SQL di Azure.

## <a name="enforcement-of-limits"></a>imposizione di limiti
Per le risorse diverse da CPU, memoria, I/O di log e I/O di dati, al raggiungimento dei limiti le nuove richieste vengono negate. Quando un database raggiunge il limite massimo configurato di hello, gli inserimenti e aggiornamenti che aumentano la dimensione dei dati completata mentre viene selezionato e le eliminazioni toowork. I client ricevono un [messaggio di errore](sql-database-develop-error-messages.md) in base al limite di hello che è stato raggiunto.

Ad esempio, hello numero di connessioni tooa SQL database e il numero di hello di richieste simultanee che possono essere elaborati sono limitate. Database SQL consente numero hello di connessioni toohello database toobe maggiore del numero di hello richieste simultanee toosupport del pool di connessioni. Mentre il numero di hello di connessioni disponibili può essere controllato facilmente dall'applicazione hello, numero hello delle richieste parallele è spesso volte più difficile tooestimate e toocontrol. In particolare durante i carichi di picco quando l'applicazione hello invia troppe richieste o database hello raggiunga i limiti di risorse e inizia ad accumulare thread di lavoro a causa di toolonger esecuzione di query, possono essere verificati errori.

## <a name="service-tiers-and-performance-levels"></a>Livelli di servizio e livelli di prestazioni
Sono disponibili livelli di servizio e livelli di prestazioni sia per i database singoli che per i pool elastici.

### <a name="single-databases"></a>Database singoli
Per un singolo database, i limiti di hello di un database sono definiti hello database livello e le prestazioni del livello di servizio. Hello nella tabella seguente descrive le caratteristiche di hello dei database Basic, Standard, Premium e RS Premium in diversi livelli di prestazioni.

[!INCLUDE [SQL DB service tiers table](../../includes/sql-database-service-tiers-table.md)]

> [!IMPORTANT]
> I clienti che utilizzano livelli di prestazioni P11 e P15 occupare too4 TB di spazio di archiviazione incluse senza costi aggiuntivi. Questa opzione di 4 TB è attualmente disponibile in hello seguenti aree: ci East2, Stati Uniti occidentali, ci Gov Virginia, Europa occidentale, Germania centrale, Sud Asia sudorientale, Giappone orientale, Australia orientale, Canada centrale e Canada orientale.
>

### <a name="elastic-pools"></a>Pool elastici
[Pool elastici](sql-database-elastic-pool.md) condividere risorse tra i database nel pool di hello. Hello nella tabella seguente descrive le caratteristiche di hello del pool elastico Basic, Standard, Premium e RS Premium.

[!INCLUDE [SQL DB service tiers table for elastic databases](../../includes/sql-database-service-tiers-table-elastic-pools.md)]

Per una definizione espansa di ogni risorsa elencata nelle tabelle precedenti hello, vedere le descrizioni di hello in [funzionalità di livello e i limiti del servizio](sql-database-performance-guidance.md#service-tier-capabilities-and-limits). Per una panoramica dei livelli di servizio, vedere [Livelli di servizio e livelli di prestazioni del database SQL di Azure](sql-database-service-tiers.md).

## <a name="other-sql-database-limits"></a>Altri limiti relativi al database SQL
| Area | Limite | Descrizione |
| --- | --- | --- |
| Database che usano l'esportazione automatizzata per ogni sottoscrizione |10 |Esportazione automatizzata consente toocreate una pianificazione personalizzata per il backup dei database SQL. Anteprima di Hello di questa funzionalità scadrà il giorno 1 marzo 2017.  |
| Database per server |Backup too5000 |Backup too5000 database sono consentiti per ogni server. |
| DTU per server |45000 |In ogni server sono consentite 45000 DTU per il provisioning di database autonomi e pool elastici. numero totale di Hello di database autonomi e i pool consentito per ogni server è limitato solo dal numero di hello del server Dtu.  

> [!IMPORTANT]
> La funzionalità di esportazione automatizzata di database SQL di Azure, ora disponibile in anteprima, verrà ritirata il 1° marzo 2017. A partire dal 1 ° dicembre 2016, non sarà in grado di tooconfigure automatizzata esportazione in qualsiasi database SQL. Tutti i processi di esportazione automatizzata esistente continuerà toowork fino al 1 ° marzo 2017. Dopo il 1 ° dicembre 2016, è possibile utilizzare [conservazione dei backup a lungo termine](sql-database-long-term-retention.md) o [automazione di Azure](../automation/automation-intro.md) database SQL tooarchive periodicamente con PowerShell periodicamente in base tooa pianificazione di propria scelta. Per uno script di esempio, è possibile scaricare hello [script da GitHub di esempio](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-automation-automated-export).
>


## <a name="resources"></a>Risorse
[Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md)

[Livelli di servizio e livelli di prestazioni del database SQL di Azure](sql-database-service-tiers.md)

[Messaggi di errore per programmi client di Database SQL](sql-database-develop-error-messages.md)
