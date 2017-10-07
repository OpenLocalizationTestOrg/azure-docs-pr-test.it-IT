---
title: sicurezza del Database SQL di Azure per il ripristino di emergenza aaaConfigure | Documenti Microsoft
description: In questo argomento vengono illustrate considerazioni sulla sicurezza per la configurazione e la gestione della sicurezza dopo un ripristino del database o un server secondario tooa di failover in caso di hello di un'interruzione del centro dati o di altro tipo di emergenza
services: sql-database
documentationcenter: na
author: anosov1960
manager: jhubbard
editor: monicar
ms.assetid: c7c898c9-69d4-4e16-8b7e-720bbb3353dd
ms.service: sql-database
ms.custom: business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 10/13/2016
ms.author: sashan
ms.openlocfilehash: c3172568e1b8ad2a53958200aa6cf19b4a9434ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a>Configurare e gestire la sicurezza dei database SQL di Azure per il ripristino geografico o il failover 

> [!NOTE]
> La [replica geografica attiva](sql-database-geo-replication-overview.md) è ora disponibile per tutti i database in tutti i livelli di servizio.
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a>Panoramica dei requisiti di autenticazione per il ripristino di emergenza
Questo argomento descrive tooconfigure requisiti di autenticazione hello e controllo [replica geografica attiva](sql-database-geo-replication-overview.md) e hello i passaggi necessari tooset backup di database secondario toohello di accesso utente. Viene inoltre descritto come abilitare i database di access toohello recuperato dopo l'utilizzo di [ripristino a livello geografico](sql-database-recovery-using-backups.md#geo-restore). Per altre informazioni sulle opzioni di ripristino, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).

## <a name="disaster-recovery-with-contained-users"></a>Ripristino di emergenza con gli utenti indipendenti
A differenza degli utenti tradizionale, che deve essere eseguito il mapping nel database master hello toologins, un utente indipendente è gestito completamente dal database hello stesso. Questo approccio presenta due vantaggi. Nello scenario di ripristino di emergenza hello, gli utenti di hello possono continuare tooconnect toohello nuovo database primario o database di hello recuperato mediante geo-restore senza configurazione aggiuntiva, perché il database di hello gestisce gli utenti di hello. Dal punto di vista dell'accesso, questa configurazione offre anche vantaggi a livello di scalabilità e prestazioni. Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx). 

compromesso di Hello principale è che Gestione processo di ripristino di emergenza hello su larga scala più impegnativa. Quando si dispone di più database hello tale uso stesso account di accesso, Gestione credenziali hello utilizzando contenuti agli utenti in più database possono annullare i vantaggi hello di utenti indipendenti. Ad esempio, criteri di rotazione hello password richiedono che modifiche in modo coerente in più database anziché la modifica della password per account di accesso hello hello una volta nel database master hello. Per questo motivo, se si dispone di più database hello che usa lo stesso nome utente e password, gli utenti indipendenti consiglia di non utilizzare. 

## <a name="how-tooconfigure-logins-and-users"></a>Come tooconfigure account di accesso e utenti
Se si utilizza l'account di accesso e utenti (anziché gli utenti indipendenti), è necessario eseguire passaggi aggiuntivi tooinsure tale hello stessi account di accesso esiste nel database master hello. Hello nelle sezioni seguenti considerazioni coinvolti e ulteriori passaggi di hello.

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a>Configurare accesso tooa secondario o recuperata database utente
Affinché toobe database secondario hello utilizzabile come un database secondario di sola lettura e tooensure accesso appropriato toohello nuovo database o hello database primario recuperato utilizzando ripristino a livello geografico, hello master database hello del server di destinazione deve disporre di hello configurazione di sicurezza appropriate prima ripristino hello.

autorizzazioni specifiche di Hello per ogni passaggio sono descritte più avanti in questo argomento.

Preparazione tooa di accesso utente replica geografica secondaria deve essere eseguita durante la configurazione di replica geografica. Preparazione dell'accesso utente database ripristinato geografica toohello deve essere eseguita in qualsiasi momento server originale hello è online (ad esempio come parte di drill di ripristino di emergenza hello).

> [!NOTE]
> Se si esegue il failover o il ripristino geografico tooa server che non dispone di account di accesso configurato correttamente, accesso tooit sarà l'account amministratore del server toohello limitato.
> 
> 

Impostazione di account di accesso nel server di destinazione hello comporta tre passaggi descritti di seguito:

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a>1. Determinare gli account di accesso con database di access toohello primario:
Hello del processo di hello è innanzitutto necessario duplicare gli account di accesso nel server di destinazione hello toodetermine. Questa operazione viene eseguita con una coppia di istruzioni SELECT, uno nel database master logico hello nel server di origine hello e uno nel database primario di hello stesso.

Hello solo l'amministratore del server o un membro di hello **LoginManager** ruolo del server è possibile determinare gli account di accesso hello nel server di origine hello con hello segue l'istruzione SELECT. 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

Solo un membro del ruolo del database db_owner hello, utente dbo hello o amministratore del server, è possibile determinare tutti hello utente entità di database nel database primario hello.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a>2. Trovare hello SID per l'account di accesso hello identificato nel passaggio 1:
Confrontando l'output di hello di query hello dalla sezione precedente hello e hello corrispondente SID, è possibile eseguire il mapping utente toodatabase con accesso server hello. Account di accesso che dispongono di un utente del database con un SID corrispondente sono database toothat di accesso utente con questo nome utente del database principale. 

Hello nella query seguente può essere utilizzato toosee tutte le entità utente hello e i relativi SID in un database. Solo un membro di hello db_owner del database del server o del ruolo amministratore può eseguire questa query.

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> Hello **INFORMATION_SCHEMA** e **sys** gli utenti hanno *NULL* SID e hello **guest** SID è **0x00**. Hello **dbo** SID può iniziare con *0x01060000000001648000000000048454*, se hello database è stato salve server anziché un membro di **DbManager**.
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a>3. Creare gli account di accesso di hello sul server di destinazione hello:
Hello ultimo passaggio è toogo toohello server di destinazione o server e generare gli account di accesso hello con hello SID appropriati. sintassi di base Hello è come indicato di seguito.

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> Se si desidera toogrant utente accesso toohello secondario, ma non i toohello primario, è possibile farlo mediante la modifica di account di accesso utente hello nel server primario hello utilizzando la seguente sintassi hello.
> 
> ALTER LOGIN <login name> DISABLE
> 
> DISABLE non modifica la password di hello, pertanto è sempre possibile abilitarla se necessario.
> 
> 

## <a name="next-steps"></a>Passaggi successivi
* Per altre informazioni sulla gestione dell'accesso al database e degli account di accesso, vedere [Protezione del database SQL: gestire l'accesso al database e la sicurezza degli account di accesso](sql-database-manage-logins.md).
* Per altre informazioni sugli utenti di database indipendente, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).
* Per informazioni sull'uso e la configurazione della replica geografica attiva, vedere [Replica geografica attiva](sql-database-geo-replication-overview.md)
* Per informazioni sull'uso del ripristino geografico, vedere l'argomento sul [ripristino geografico](sql-database-recovery-using-backups.md#geo-restore)

