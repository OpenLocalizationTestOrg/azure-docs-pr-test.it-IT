---
title: ripristino di emergenza Database aaaSQL | Documenti Microsoft
description: "Informazioni su come un database da un'interruzione del Data Center regionale con toorecover hello Database SQL di Azure la replica geografica attiva e funzionalità di ripristino a livello geografico."
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: 4800960e-3f9d-40ce-9e55-fb7f2784c067
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/14/2017
ms.author: sashan
ms.openlocfilehash: bae08485863067748107ec4808e52d8e88e2de0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-database-or-failover-tooa-secondary"></a>Ripristinare un Database SQL di Azure o il failover tooa è secondario
Database SQL di Azure offre hello funzionalità per il ripristino di un'interruzione di seguito:

* [Replica geografica attiva](sql-database-geo-replication-overview.md)
* [Ripristino geografico](sql-database-recovery-using-backups.md#point-in-time-restore)

toolearn sugli scenari di continuità aziendale e le funzionalità di hello per supportare questi scenari, vedere [la continuità aziendale](sql-database-business-continuity.md).

### <a name="prepare-for-hello-event-of-an-outage"></a>Preparazione per l'evento hello di interruzione
Per il successo con l'area dati di ripristino tooanother con replica geografica attiva o i backup con ridondanza geografica, è necessario tooprepare un server in un altro data center interruzione toobecome hello nuovo server primario deve hello devono verificarsi nonché passaggi ben definiti testato e documentato tooensure un ripristino senza problemi. La procedura di preparazione comprende:

* Identificare i server logici disponibili hello in un'altra area toobecome hello nuovo server primario. Con la replica geografica attiva, questo sarà almeno uno e forse ogni server secondario hello. Per il ripristino geografico, si tratterà in genere un server in hello [area abbinata](../best-practices-availability-paired-regions.md) per area hello in cui si trova il database.
* Identificare e facoltativamente definire, regole del firewall a livello di server hello necessarie in per gli utenti tooaccess hello nuovo database primario.
* Determinare come verrà tooredirect utenti toohello nuovo server primario, ad esempio la modifica di stringhe di connessione oppure modificando le voci DNS.
* Identificare e, facoltativamente, creare, hello gli account di accesso che deve essere presente nel database master di hello nel nuovo server primario hello e verificare che questi account di accesso dispone delle autorizzazioni appropriate nel database master hello, se presente. Per altre informazioni, vedere [Come gestire la sicurezza del database SQL di Azure dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md)
* Identificare le regole di avviso che saranno necessario toobe toomap aggiornato toohello nuovo database primario.
* Configurazione del controllo di hello documento sul database primario corrente hello
* [Esercitazione per il ripristino di emergenza](sql-database-disaster-recovery-drills.md). toosimulate un'interruzione del servizio per il ripristino geografico, è possibile eliminare o rinominare un errore di connettività di hello origine database toocause dell'applicazione. toosimulate un'interruzione del servizio per la replica geografica attiva, è possibile disabilitare l'applicazione web hello o macchina virtuale connessa toohello database o il failover hello database toocause applicazione gli errori di connettività.

## <a name="when-tooinitiate-recovery"></a>Quando il ripristino tooinitiate
operazione di ripristino Hello influisce su un'applicazione hello. Richiede la modifica di reindirizzamento tramite DNS o stringa di connessione SQL hello e può provocare la perdita permanente dei dati. Pertanto, deve essere eseguita solo quando l'interruzione hello è probabilmente toolast più obiettivo tempo di ripristino dell'applicazione. Quando l'applicazione hello è distribuito tooproduction che occorre eseguire il monitoraggio regolare dell'integrità delle applicazioni hello e utilizzare hello tooassert punti di ripristino hello è garantito di dati seguenti:

1. Errore di connettività permanente dal database toohello livello di applicazione hello.
2. Hello portale di Azure viene visualizzato un avviso su un evento imprevisto nell'area di hello con effetti estesi.
3. server di Database SQL di Azure Hello viene contrassegnato come danneggiato.

A seconda l'applicazione tolleranza toodowntime e possibili business responsabilità dell'utente è possibile considerare le opzioni di ripristino seguenti hello.

Hello utilizzare [Get Recoverable Database](https://msdn.microsoft.com/library/dn800985.aspx) (*LastAvailableBackupDate*) punto di ripristino di replica geografica tooget hello più recente.

## <a name="wait-for-service-recovery"></a>Attendere il ripristino del servizio
Hello Azure i team lavorano attentamente la disponibilità del servizio toorestore come rapidamente possibile, ma a seconda della causa radice di hello può richiedere ore o giorni.  Se l'applicazione può tollerare i tempi di inattività significativi è semplicemente possibile attendere toocomplete ripristino hello. In tal caso, non è necessaria alcuna azione da parte dell'utente. È possibile visualizzare lo stato del servizio corrente hello nel nostro [Dashboard di integrità del servizio di Azure](https://azure.microsoft.com/status/). Dopo il ripristino di hello dell'area di hello verrà ripristinata la disponibilità dell'applicazione.

## <a name="fail-over-toogeo-replicated-secondary-database"></a>Eseguire il failover toogeo alla replica di database secondario
Se i tempi di inattività dell'applicazione possono comportare una responsabilità aziendale, è consigliabile usare database con replica geografica nell'applicazione. Disponibilità di ripristino tooquickly applicazione hello in un'area diversa in caso di interruzione verrà attivata. Informazioni su come troppo[configurare la replica geografica](sql-database-geo-replication-portal.md).

database di disponibilità toorestore di hello è necessario tooinitiate hello failover toohello replica geografica secondaria usando uno dei metodi di hello è supportato.

Utilizzare uno dei seguenti guide toofail sul database secondario di replica geografica tooa hello:

* [Eseguire il failover tooa replica geografica secondaria, tramite il portale di Azure](sql-database-geo-replication-portal.md)
* [Eseguire il failover tooa replica geografica secondaria tramite PowerShell](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
* [Eseguire il failover tooa replica geografica secondaria utilizzando T-SQL](sql-database-geo-replication-transact-sql.md)

## <a name="recover-using-geo-restore"></a>Ripristino tramite il ripristino geografico
Se i tempi di inattività dell'applicazione non comporta la responsabilità di business è possibile utilizzare [ripristino a livello geografico](sql-database-recovery-using-backups.md) come toorecover un metodo al database dell'applicazione. Crea una copia del database hello dal relativo backup con ridondanza geografica più recente.

## <a name="configure-your-database-after-recovery"></a>Configurare il database dopo il ripristino
Se si utilizza la replica geografica failover o toorecover ripristino a livello geografico di un'interruzione, è necessario assicurarsi che i nuovi database hello connettività toohello sia configurato correttamente in modo che può essere ripresi funzione normale applicazione hello. Questo è un elenco di controllo di tooget attività di produzione del database ripristinato pronta.

### <a name="update-connection-strings"></a>Aggiornare le stringhe di connessione
Poiché il database ripristinato si trova in un server diverso, è necessario tooupdate di connessione stringa toopoint toothat server dell'applicazione.

Per ulteriori informazioni sulla modifica di stringhe di connessione, vedere il linguaggio di sviluppo appropriata hello per le [raccolta connessioni](sql-database-libraries.md).

### <a name="configure-firewall-rules"></a>Configurare le regole firewall
È necessario assicurarsi che le regole del firewall hello configurata nel server e in corrispondenza di hello database quelli che sono stati configurati nel server primario di hello e database primario toomake. Per altre informazioni, vedere [Procedura: Configurare le impostazioni del firewall (Database SQL di Azure)](sql-database-configure-firewall-settings.md).

### <a name="configure-logins-and-database-users"></a>Configurare gli account di accesso e gli utenti del database
È necessario che tutti gli accessi hello utilizzati dall'applicazione nel server siano presenti hello che ospita il database ripristinato toomake. Per altre informazioni, vedere [Configurazione della sicurezza per la replica geografica](sql-database-geo-replication-security-config.md).

> [!NOTE]
> È necessario configurare e testare le regole del firewall del server e gli account di accesso (con le relative autorizzazioni) durante un'analisi di ripristino di emergenza. Questi oggetti a livello di server e la configurazione potrebbe non essere disponibile durante un'interruzione di hello.
> 
> 

### <a name="setup-telemetry-alerts"></a>Avvisi di telemetria di configurazione
È necessario che le impostazioni della regola di avviso esistenti siano aggiornati toomap toohello ripristinati database hello diversi server e toomake.

Per altre informazioni sulle regole di avviso per il database, vedere [Ricevere notifiche di avviso](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) e [Tracciare l’integrità del servizio](../monitoring-and-diagnostics/insights-service-health.md).

### <a name="enable-auditing"></a>Attivare il controllo
Se il controllo è obbligatorio tooaccess del database, è necessario tooenable controllo dopo il ripristino di database hello. Per altre informazioni, vedere l'articolo sul [controllo del database](sql-database-auditing.md).

## <a name="next-steps"></a>Passaggi successivi
* toolearn sui backup di Database di SQL Azure automatizzati, vedere [backup automatici di Database SQL](sql-database-automated-backups.md)
* toolearn sugli scenari di progettazione e il ripristino di continuità aziendale, vedere [gli scenari di continuità](sql-database-business-continuity.md)
* toolearn sull'utilizzo di backup automatico per il ripristino, vedere [ripristinare un database dai backup avviate dal servizio hello](sql-database-recovery-using-backups.md)

