---
title: aaaOnline backup e ripristino con Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come tooperform automatica di backup e ripristino in un database di Azure Cosmos DB.
keywords: backup e ripristino, backup online
services: cosmos-db
documentationcenter: 
author: RahulPrasad16
manager: jhubbard
editor: monicar
ms.assetid: 98eade4a-7ef4-4667-b167-6603ecd80b79
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/11/2017
ms.author: raprasa
ms.openlocfilehash: a0b464c95681dfc7b5462b02bf04c2c43d6bc16f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-online-backup-and-restore-with-azure-cosmos-db"></a>Backup online automatico e ripristino con Azure Cosmos DB
Azure Cosmos DB esegue automaticamente il backup di tutti i dati a intervalli regolari. i backup automatici di Hello vengono eseguiti senza influire sulle prestazioni di hello o la disponibilità delle operazioni di database. Tutti i backup vengono archiviati separatamente in un altro servizio di archiviazione, oltre a essere replicati a livello globale per garantire la resilienza in caso di emergenze locali. i backup automatici Hello sono destinati a scenari quando si elimina accidentalmente il contenitore DB Comos e versioni successive richiede il recupero dei dati o una soluzione di ripristino di emergenza.  

In questo articolo inizia con un riepilogo rapido della ridondanza dei dati hello e della disponibilità in Cosmos DB e quindi vengono illustrati i backup. 

## <a name="high-availability-with-cosmos-db---a-recap"></a>Disponibilità elevata con Cosmos DB: riepilogo
COSMOS DB è progettato toobe [distribuiti in modo globale](distribute-data-globally.md) : consente di velocità effettiva tooscale tra più aree di Azure con criteri basati su failover e le API multihosting trasparente. Come un'offerta di sistema di database [disponibilità del 99,99% SLA](https://azure.microsoft.com/support/legal/sla/cosmos-db), tutte le scritture hello in DB Cosmos sono dischi toolocal commit in modo permanente da un quorum di repliche all'interno di un data center locale prima del riconoscimento toohello client. Si noti che la disponibilità elevata del database Cosmos hello si basa su archiviazione locale e non dipende da qualsiasi tecnologia di archiviazione esterna. Inoltre, se l'account di database è associato a più di un'area di Azure, le operazioni di scrittura vengono replicate anche nelle altre aree. tooscale la velocità effettiva e accedere ai dati a bassa latenza, è possibile includere molte leggere aree associate all'account di database nel modo desiderato. In ogni area lettura dati hello (replicata) viene mantenuti in modo durevole tra un set di repliche.  

Come illustrato nel seguente diagramma hello, è un singolo contenitore Cosmos DB [partizionati orizzontalmente](partition-data.md). Una partizione"" è identificata da un cerchio nel seguente diagramma hello e ogni partizione viene reso disponibile tramite un set di repliche. Si tratta di distribuzione locale di hello in una singola regione di Azure (indicata dall'asse X hello). Inoltre, ogni partizione (con il relativo set di replica corrispondente) quindi viene distribuito a livello globale in più regioni associati all'account di database (ad esempio, in questa illustrazione hello tre aree: Stati Uniti orientali, Stati Uniti occidentali e India centrale). "set di partizioni" Hello viene distribuita a livello globale entità è costituita da più copie dei dati in ogni area (indicato dalle asse hello Y). È possibile assegnare priorità aree toohello associate all'account di database e Cosmos DB comporta in modo trasparente area successiva toohello di failover in caso di emergenza. È possibile simulare manualmente failover tootest hello end-to-end disponibilità dell'applicazione.  

Hello immagine seguente illustra elevato hello di ridondanza con DB Cosmos.

![Elevato grado di ridondanza con Cosmos DB](./media/online-backup-and-restore/redundancy.png)

![Elevato grado di ridondanza con Cosmos DB](./media/online-backup-and-restore/global-distribution.png)

## <a name="full-automatic-online-backups"></a>Backup online, completi, automatici
È possibile che il contenitore o il database venga eliminato. Con Cosmos DB, non solo i dati, ma i backup hello dei dati vengono eseguite anche emergenze tooregional altamente ridondante e flessibile. I backup automatici vengono attualmente eseguiti ogni quattro ore circa; ogni volta vengono archiviati i due backup più recenti. Se dati hello viene accidentalmente eliminato o danneggiato,. [contattare il supporto tecnico di Azure](https://azure.microsoft.com/support/options/) entro 8 ore. 

Hello backup senza influire sulle prestazioni di hello o la disponibilità delle operazioni di database. COSMOS DB accetta backup hello in background hello senza utilizzare i servizio aggiornamento destinatari provisioning o influire sulle prestazioni di hello e senza influire sulla disponibilità hello del database. 

A differenza dei dati archiviati in DB Cosmos, i backup automatici hello vengono archiviati nel servizio di archiviazione Blob di Azure. caricamento di latenza bassa/efficiente hello tooguarantee, snapshot hello del backup è istanza tooan caricato nell'archiviazione Blob di Azure in hello area scrittura corrente hello dell'account di database DB Cosmos stessa area. Per garantire la resilienza in situazioni di emergenza, ogni snapshot dei dati di backup nell'archiviazione Blob di Azure viene replicato nuovamente tramite area tooanother archiviazione con ridondanza geografica (GRS). Hello diagramma seguente mostra che l'intero contenitore Cosmos DB hello (con tutte le tre partizioni primarie negli Stati Uniti occidentali, in questo esempio) viene eseguito il backup in un account di archiviazione Blob di Azure remoto negli Stati Uniti occidentali e quindi GRS replicati tooEast ci. 

Hello immagine seguente illustra i backup completi periodici di tutte le entità di database Cosmos in archiviazione di Azure di archiviazione con ridondanza geografica.

![Backup completi periodici di tutte le entità di Cosmos DB nell'archiviazione con ridondanza geografica di Azure](./media/online-backup-and-restore/automatic-backup.png)

## <a name="backup-retention-period"></a>Periodo di conservazione dei backup
Come descritto in precedenza, Azure Cosmos DB accetta gli snapshot dei dati ogni quattro ore e consente di mantenere gli snapshot delle ultime due hello di ogni partizione per 30 giorni. In base alle normative di conformità, gli snapshot vengono eliminati dopo 90 giorni.

Se si desidera toomaintain proprio snapshot, è possibile utilizzare l'opzione di tooJSON esportazione hello in hello Azure Cosmos DB [dello strumento di migrazione dei dati](import-data.md#export-to-json-file) tooschedule ulteriori backup. 

## <a name="restoring-a-database-from-an-online-backup"></a>Ripristino di un database da un backup online
Se si elimina accidentalmente il database o la raccolta, è possibile [un ticket di supporto](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) o [contattare il supporto Azure](https://azure.microsoft.com/support/options/) dati hello toorestore dall'ultimo backup automatico di hello. Se è necessario toorestore il database a causa di problema di danneggiamento dei dati, vedere [gestisce il danneggiamento dei dati](#handling-data-corruption) in base alle esigenze tootake ulteriori passaggi tooprevent hello danneggiato dati dai backup hello penetrazione. Per uno snapshot specifico del toobe backup ripristinato, DB Cosmos richiede che i dati di hello erano disponibili per la durata di hello del ciclo di backup hello per lo snapshot.

## <a name="handling-data-corruption"></a>Gestione del danneggiamento dei dati
DB Cosmos Azure mantiene backup ultime due di hello di ogni partizione nel sistema hello. Questo modello è molto utili quando un contenitore (raccolta di documenti, grafico e tabella) o un database viene accidentalmente eliminato perché una delle ultime versioni hello può essere ripristinata. Tuttavia, in hello caso in cui quando gli utenti possono comportare un problema di danneggiamento dei dati, Azure Cosmos DB potrebbe non essere consapevole di danneggiamento dei dati hello ed ed è possibile che hello danneggiamento possibile evitare i backup hello. Non appena vengono rilevati dati danneggiati, è necessario eliminare il contenitore di hello danneggiato (raccolta/grafico o tabella) in modo che i backup siano protetti dalla sovrascrittura con dati danneggiati. Dopo l'ultimo backup hello potrebbe essere quattro ore, è possibile utilizzare utente hello [modificare feed](change-feed.md) toocapture e archivio hello ultime quattro ore di dati prima di eliminare il contenitore di hello.

## <a name="next-steps"></a>Passaggi successivi

vedere il database in più data center, tooreplicate [distribuire i dati a livello globale con DB Cosmos](distribute-data-globally.md). 

toofile contattare il supporto tecnico di Azure, [un ticket dal portale di Azure hello](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).

