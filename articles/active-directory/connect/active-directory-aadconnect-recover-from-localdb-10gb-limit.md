---
title: 'Azure AD Connect: Come limitare toorecover da 10GB LocalDB problema | Documenti Microsoft'
description: Questo argomento viene descritto come toorecover sincronizzazione di Azure AD Connect del servizio quando viene rilevato LocalDB 10GB limitare problema.
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 41d081af-ed89-4e17-be34-14f7e80ae358
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: 7b8ce6e19b68837639017bb0315eda4b924d525a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-how-toorecover-from-localdb-10-gb-limit"></a>Azure AD Connect: Modalità toorecover dal limite di 10 GB di LocalDB
Azure AD Connect richiede un Server SQL database toostore identità dei dati. È possibile utilizzare hello predefinito installato SQL Server 2012 Express LocalDB con Azure AD Connect o usare la propria SQL completa. SQL Server Express impone un limite di 10 GB. Quando si usa LocalDB e viene raggiunto questo limite, il servizio di sincronizzazione Azure AD Connect non può più essere avviato o eseguire la sincronizzazione correttamente. In questo articolo vengono illustrate operazioni di ripristino hello.

## <a name="symptoms"></a>Sintomi
Esistono due sintomi comuni:

* Servizio Azure AD Connect sincronizzazione **è in esecuzione** ma non riesce toosynchronize con *"arrestata-database-disco-full"* errore.

* Servizio Azure AD Connect sincronizzazione **è Impossibile toostart**. Quando si tenta di servizio hello toostart, non riesce con messaggio di errore e di evento 6323 *"hello server ha rilevato un errore perché SQL Server ha esaurito lo spazio su disco."*

## <a name="short-term-recovery-steps"></a>Procedura di ripristino a breve termine
Questa sezione vengono fornite hello passaggi tooreclaim DB spazio per l'operazione di servizio Azure AD Connect sincronizzazione tooresume. Hello passaggi includono:
1. [Determinare lo stato del servizio di sincronizzazione hello](#determine-the-synchronization-service-status)
2. [Compattazione di database hello](#shrink-the-database)
3. [Eliminare i dati della cronologia di esecuzione](#delete-run-history-data)
4. [Abbreviare il periodo di conservazione dei dati della cronologia di esecuzione](#shorten-retention-period-for-run-history-data)

### <a name="determine-hello-synchronization-service-status"></a>Determinare lo stato del servizio di sincronizzazione hello
Innanzitutto, determinare se il servizio di sincronizzazione hello è ancora in esecuzione o non:

1. Accedi tooyour Azure AD Connect server come amministratore.

2. Andare troppo**Gestione controllo servizi**.

3. Controllare lo stato di hello di **Microsoft Azure AD Sync**.


4. Se è in esecuzione, non arrestare o riavviare il servizio di hello. Ignora [database hello compattazione](#shrink-the-database) passaggio e andare troppo[Elimina dati di cronologia di esecuzione](#delete-run-history-data) passaggio.

5. Se non è in esecuzione, provare il servizio di hello toostart. Se il servizio hello viene avviato correttamente, ignorare [database hello compattazione](#shrink-the-database) passaggio e andare troppo[Elimina dati di cronologia di esecuzione](#delete-run-history-data) passaggio. In caso contrario, continuare con [database hello compattazione](#shrink-the-database) passaggio.

### <a name="shrink-hello-database"></a>Compattazione di database hello
Utilizzare toofree operazione di compattazione hello backup hello di toostart sufficiente spazio DB servizio di sincronizzazione. Consente di liberare spazio database rimuovendo gli spazi vuoti nel database di hello. Si tratta del miglior tentativo possibile, dato che non è certo che sia sempre possibile recuperare lo spazio. toolearn più sull'operazione di compattazione, leggere questo articolo [compattare un database](https://msdn.microsoft.com/library/ms189035.aspx).

> [!IMPORTANT]
> Ignorare questo passaggio se è possibile ottenere hello toorun di servizio di sincronizzazione. Non è consigliabile tooshrink hello DB SQL quanto può causare toopoor prestazioni a causa di frammentazione tooincreased.

nome Hello database hello creato per Azure AD Connect è **ADSync**. tooperform un'operazione di compattazione, è necessario accedere come hello sysadmin o proprietario del database hello. Durante l'installazione di Azure AD Connect, hello seguendo gli account viene concessi diritti di amministratore:
* Amministratori locali
* account utente Hello era toorun usato Azure AD Connect installazione.
* account del servizio di sincronizzazione che viene usato come contesto del servizio Azure AD Connect sincronizzazione operativo hello Hello.
* gruppo locale di Hello ADSyncAdmins creato durante l'installazione.

1. Eseguire il backup dei database hello copiando **ADSync.mdf** e **ADSync_log.ldf** file che si trovano in `%ProgramFiles%\program files\Microsoft Azure AD Sync\Data` tooa di posizione sicura.

2. Avviare una nuova sessione di PowerShell.

3. Passare toofolder `%ProgramFiles%\Program Files\Microsoft SQL Server\110\Tools\Binn`.

4. Avviare **sqlcmd** utilità eseguendo il comando hello `./SQLCMD.EXE -S “(localdb)\.\ADSync” -U <Username> -P <Password>`, utilizzando credenziali hello del ruolo sysadmin o hello database DBO.

5. database hello tooshrink, al prompt dei comandi sqlcmd hello (1 >), immettere `DBCC Shrinkdatabase(ADSync,1);`, seguito da `GO` nella riga successiva hello.

6. Se l'operazione hello ha esito positivo, riprovare hello toostart servizio di sincronizzazione. Se è possibile avviare il servizio di sincronizzazione hello, andare troppo[Elimina dati di cronologia di esecuzione](#delete-run-history-data) passaggio. In caso contrario, contattare il supporto tecnico.

### <a name="delete-run-history-data"></a>Eliminare i dati della cronologia di esecuzione
Per impostazione predefinita, Azure AD Connect mantiene fino tooseven di giorni di dati di cronologia di esecuzione. In questo passaggio è eliminare hello spazio di tooreclaim DB dati di cronologia di esecuzione in modo che sia possibile avviare servizio Azure AD Connect sincronizzazione sincronizzando di nuovo.

1.  Avviare **Synchronization Service Manager** da passare → tooSTART servizio di sincronizzazione.

2.  Passare toohello **operazioni** scheda.

3.  In **Actions** (Azioni) selezionare **Clear Runs** (Cancella esecuzioni).

4.  È possibile scegliere **Clear all runs** (Cancella tutte le esecuzioni) oppure **Clear runs before<date>** (Cancella esecuzioni precedenti a). È consigliabile iniziare cancellando i dati della cronologia di esecuzione che risalgono a più di due giorni di prima. Se si continua toorun problema di dimensioni di database, quindi scegliere hello **deselezionare tutte le esecuzioni** opzione.

### <a name="shorten-retention-period-for-run-history-data"></a>Abbreviare il periodo di conservazione dei dati della cronologia di esecuzione
Questo passaggio è probabilità hello tooreduce dell'esecuzione di problema di limite di 10 GB hello dopo più cicli di sincronizzazione.

1. Aprire una nuova sessione di PowerShell.

2. Eseguire `Get-ADSyncScheduler` e prendere nota di hello PurgeRunHistoryInterval proprietà che specifica il periodo di memorizzazione corrente hello.

3. Eseguire `Set-ADSyncScheduler -PurgeRunHistoryInterval 2.00:00:00` giorni tootwo periodo di conservazione hello tooset. Regolare il periodo di memorizzazione hello come appropriato.

## <a name="long-term-solution--migrate-toofull-sql"></a>Soluzione a lungo termine di migrazione toofull SQL
Problema di hello è in genere indicativa che dimensioni del database di 10 GB non sono più sufficiente per Azure AD Connect toosynchronize il tooAzure di Active Directory locale AD. È consigliabile passare versione completa di hello toousing di SQL server. È possibile sostituire direttamente hello del database locale di una distribuzione esistente di Azure AD Connect con database hello versione completa di hello di SQL. In alternativa, è necessario distribuire un nuovo server di Azure AD Connect versione completa di hello di SQL. Si consiglia di effettuare una migrazione di attività in cui nuovo server Azure AD Connect hello (con database SQL) viene distribuito come server di gestione temporanea, successivo server in Azure AD Connect esistente a toohello (con LocalDB). 
* Per istruzioni su come tooconfigure SQL remoto con Azure AD Connect, fare riferimento tooarticle [installazione personalizzata di Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom).
* Per istruzioni sulla migrazione di attività per l'aggiornamento di Azure AD Connect, consultare tooarticle [Azure AD Connect: l'aggiornamento da una precedente toohello versione più recente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version#swing-migration).

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
