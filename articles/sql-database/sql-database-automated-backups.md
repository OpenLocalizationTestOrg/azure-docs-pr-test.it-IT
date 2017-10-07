---
title: backup del Database SQL aaaAzure automatica, con ridondanza geografica | Documenti Microsoft
description: Il database SQL crea automaticamente e ripetutamente una copia di backup locale del database a pochi minuti l'una dall'altra e usa l'archiviazione con ridondanza geografica e accesso in lettura di Azure per la ridondanza geografica.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 3ee3d49d-16fa-47cf-a3ab-7b22aa491a8d
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 8aff5356e8142707dd7cd2533a4aa5ea8fec866d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="learn-about-automatic-sql-database-backups"></a>Informazioni sui backup automatici del database SQL

Database SQL Crea backup dei database e automaticamente Usa Azure archiviazione con ridondanza geografica e accesso in lettura (RA-GRS) tooprovide ridondanza geografica. Questi backup vengono creati automaticamente e senza costi aggiuntivi. Non è necessario toodo nulla toomake che li verificarsi. I backup dei database sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza, perché proteggono i dati dal danneggiamento o dall'eliminazione accidentale. Se si desidera tookeep backup in un contenitore di archiviazione è possibile configurare un criterio di conservazione dei backup a lungo termine. Per altre informazioni, vedere [Long-term retention](sql-database-long-term-retention.md) (Conservazione a lungo termine).

## <a name="what-is-a-sql-database-backup"></a>Informazioni sul backup del database SQL

Database SQL utilizza toocreate tecnologia SQL Server [completo](https://msdn.microsoft.com/library/ms186289.aspx), [differenziale](https://msdn.microsoft.com/library/ms175526.aspx), e [log delle transazioni](https://msdn.microsoft.com/library/ms191429.aspx) backup. backup del log delle transazioni Hello in genere eseguita ogni 5-10 minuti, con frequenza hello in base a livello di prestazioni hello e la quantità di attività del database. Backup del log delle transazioni, con backup completi e differenziali, consentono di un database tooa specifico punto nel tempo toohello toorestore stesso server che ospita il database di hello. Quando si ripristina un database, hello determina quali completo, differenziale servizio e i backup del log delle transazioni necessario toobe ripristinato.


È possibile usare questi backup per:

* Ripristinare un database tooa punto nel tempo entro il periodo di memorizzazione hello. Questa operazione consente di creare un nuovo database in hello stesso server del database originale hello.
* Ripristinare un database eliminato toohello che è stata eliminata qualsiasi fase o entro il periodo di memorizzazione hello. database Hello eliminato può essere ripristinato solo hello stesso server in cui è stato creato il database originale di hello.
* Ripristinare una regione geografica tooanother di database. In questo modo si toorecover di emergenza geografica quando è possibile accedere a server e al database. Crea un nuovo database in qualsiasi server esistente in un punto qualsiasi nella HelloWorld. 
* Ripristinare un database da un backup specifico nell'insieme di credenziali di Servizi di ripristino di Azure. In questo modo è una versione precedente di hello database toosatisfy una richiesta di conformità toorestore o toorun una versione precedente di un'applicazione hello. Vedere [Conservazione a lungo termine](sql-database-long-term-retention.md).
* tooperform un ripristino, vedere [ripristinare database da backup](sql-database-recovery-using-backups.md).

> [!NOTE]
> Nell'archiviazione di Azure, il termine hello *replica* fa riferimento il file toocopying da tooanother un'unica posizione. SQL *replica di database* fa riferimento a database secondari toomultiple tookeeping sincronizzati con un database primario. 
> 

## <a name="how-much-backup-storage-is-included-at-no-cost"></a>Quanto spazio di archiviazione di backup è incluso senza costi aggiuntivi?
Database SQL fornisce too200% dello spazio di archiviazione massime del database sottoposto a provisioning come archiviazione di backup senza alcun costo aggiuntivo. Se si usa ad esempio un'istanza di database Standard con una dimensione di database con provisioning pari a 250 GB, sono disponibili 500 GB di archiviazione di backup senza costi aggiuntivi. Se il database supera hello fornita l'archiviazione di backup, è possibile scegliere periodo di memorizzazione hello tooreduce contattando il supporto tecnico di Azure. Un'altra opzione è toopay per spazio di archiviazione extra backup viene fatturato alla tariffa di hello standard archiviazione accesso in lettura geograficamente ridondante (RA-GRS). 

## <a name="how-often-do-backups-happen"></a>Con quale frequenza si verificano i backup?
I backup di database completi vengono eseguiti settimanalmente, i backup differenziali di solito sono eseguiti a intervalli di poche ore e i backup del log delle transazioni ogni 5-10 minuti. primo backup completo di Hello è pianificato subito dopo la creazione di un database. In genere viene completata entro 30 minuti, ma può richiedere più tempo quando hello database è di dimensioni significative. Ad esempio, il backup iniziale hello può richiedere più tempo in un database ripristinato o una copia del database. Dopo aver hello primo backup completo, tutti i backup ulteriore pianificazione automaticamente e gestiti automaticamente in background hello. intervallo esatto di Hello di tutti i backup del database è determinato dall'hello servizio Database SQL è un compromesso tra hello complessivo carico di lavoro di sistema. 

archiviazione di backup Hello-replica geografica si verifica in base a una pianificazione della replica di archiviazione di Azure hello.

## <a name="how-long-do-you-keep-my-backups"></a>Quanto tempo vengono conservati i backup?
Ogni backup del Database SQL dispone di un periodo di memorizzazione che si basa sull'hello [livello di servizio](sql-database-service-tiers.md) del database hello. periodo di memorizzazione Hello per un database nel:


* Il livello di servizio Base è 7 giorni.
* livello di servizio Standard è di 35 giorni.
* livello di servizio premium è di 35 giorni.

Se si esegue il downgrade del database da hello Standard o tooBasic livelli di servizio Premium, vengono salvati i backup hello per sette giorni. Tutti i backup esistenti più vecchi di sette giorni non sono più disponibili. 

Se si aggiorna il database da tooStandard livello di servizio Basic hello o Premium, Database SQL consente di mantenere i backup esistenti fino a quando non sono 35 giorni. Allo scadere dei 35, il database conserva i nuovi backup.

Se si elimina un database, Database SQL mantiene backup hello hello esattamente come avviene per un database online. Si supponga, ad esempio, che si elimina un database con livello di servizio Basic e periodo di conservazione di sette giorni. Per tre giorni viene conservato un backup dei quattro giorni precedenti.

> [!IMPORTANT]
> Se si elimina il server di SQL Azure hello che ospita i database SQL, tutti i database appartenenti a toohello server vengono anche eliminati e non possono essere recuperati. Non è possibile ripristinare un server eliminato.
> 

## <a name="how-tooextend-hello-backup-retention-period"></a>Hello tooextend backup come periodo di conservazione?
Se l'applicazione richiede che i backup di hello sono disponibili per periodo di tempo più lungo è possibile estendere il periodo di memorizzazione predefinite di hello configurando hello i criteri di conservazione dei backup a lungo termine per i singoli database (criteri LTR). In questo modo tooextend hello it compilato periodo in anni di too10 tooup 35 giorni. Per altre informazioni, vedere [Long-term retention](sql-database-long-term-retention.md) (Conservazione a lungo termine).

Dopo aver aggiunto i database di hello LTR criterio tooa tramite il portale di Azure o l'API, hello settimanale backup completo del database verrà automaticamente copiati tooyour proprietari credenziali del servizio di Azure Backup. Se il database viene crittografato con i backup hello TDE vengono crittografati automaticamente inattivi.  insieme di credenziali di servizi di Hello eliminerà automaticamente i backup scaduti in base ai timestamp e i criteri LTR hello.  In modo non è necessario toomanage pianificazione del backup hello o preoccupare pulizia hello di hello file obsoleti. supporta l'API ripristino Hello come insieme di credenziali hello è insieme di credenziali di backup archiviati in hello hello stessa sottoscrizione del database SQL. È possibile utilizzare hello portale di Azure o PowerShell tooaccess questi backup.

> [!TIP]
> Per una procedura-tooguide, vedere [Configura e il ripristino da conservazione dei backup a lungo termine di Database SQL di Azure](sql-database-long-term-backup-retention-configure.md)
>

## <a name="are-backups-encrypted"></a>I backup sono crittografati?

Quando la crittografia TDE viene abilitata per un database SQL di Azure, anche i backup vengono crittografati. Tutti i nuovi database SQL di Azure vengono configurati con la crittografia TDE abilitata per impostazione predefinita. Per altre informazioni su TDE, vedere [Transparent Data Encryption con il database SQL di Azure](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database).

## <a name="next-steps"></a>Passaggi successivi

- I backup dei database sono una parte essenziale di qualsiasi strategia di continuità aziendale e ripristino di emergenza, perché proteggono i dati dal danneggiamento o dall'eliminazione accidentale. toolearn circa hello altre soluzioni di continuità di business di Database SQL di Azure, vedere [Panoramica di continuità aziendale](sql-database-business-continuity.md).
- vedere toorestore tooa punto nel tempo tramite il portale di Azure, hello [ripristinare database tooa punto nel tempo tramite il portale di Azure hello](sql-database-recovery-using-backups.md).
- toorestore tooa punto nel tempo tramite PowerShell, vedere [database tooa punto di ripristino temporizzato tramite PowerShell](scripts/sql-database-restore-database-powershell.md).
- tooconfigure, gestire e ripristinare da conservazione a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure utilizzando hello Azure portale, vedere [con conservazione dei backup a lungo termine Gestisci hello Azure portal](sql-database-long-term-backup-retention-configure.md).
- tooconfigure, gestire e di ripristino dalla memorizzazione a lungo termine dei backup automatizzati in un insieme di credenziali di servizi di ripristino di Azure tramite PowerShell, vedere [gestire la conservazione di backup a lungo termine tramite PowerShell](sql-database-long-term-backup-retention-configure.md).
