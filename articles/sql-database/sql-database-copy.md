---
title: aaaCopy un database SQL di Azure | Documenti Microsoft
description: Creare una copia di un database SQL di Azure
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.date: 06/15/2017
ms.author: carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 64a297d819d6da89600fda60abe8394ae405abfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-an-azure-sql-database"></a>Copiare un database SQL di Azure

Database SQL di Azure fornisce diversi metodi per la creazione di una copia coerente delle transazioni SQL Azure esistenti del database su entrambi hello stesso server o un altro server. È possibile copiare un database SQL tramite T-SQL, PowerShell o hello portale di Azure. 

## <a name="overview"></a>Panoramica

Una copia del database è uno snapshot del database di origine hello ora hello della richiesta di copia hello. È possibile selezionare hello nello stesso server o un altro server, il relativo livello di prestazioni e di servizio o un livello di prestazioni diverse all'interno di hello stesso livello di servizio (edizione). Una volta completata la copia hello, diventa un database indipendente, completamente funzionante. A questo punto, è possibile aggiornare o effettuare il downgrade tooany edition. autorizzazioni, utenti e account di accesso hello possono essere gestite in modo indipendente.  

## <a name="logins-in-hello-database-copy"></a>Account di accesso in una copia del database hello

Quando si copia un toohello database nello stesso server logico, hello stessi account di accesso può essere usato in entrambi i database. Hello entità di sicurezza utilizzata database hello toocopy diventa proprietario del database nel nuovo database hello hello. Tutti gli utenti di database, le relative autorizzazioni e la sicurezza (SID) di identificatori sono copiati toohello copia del database.  

Quando si copia un database tooa altro server logico, sicurezza hello principale nel nuovo server hello diventa proprietario del database nel nuovo database hello hello. Se si utilizza [utenti del database indipendente](sql-database-manage-logins.md) per accedere ai dati, assicurarsi che entrambi hello primario e i database secondari sono sempre hello stesse credenziali utente, in modo che dopo aver hello copia completata immediatamente accessibili con hello stesso credenziali. 

Se si utilizza [Azure Active Directory](../active-directory/active-directory-whatis.md), è possibile eliminare completamente hello necessario per la gestione delle credenziali nella copia hello. Tuttavia, quando si copia nuovo server di hello database tooa, accesso basato su account di accesso hello potrebbe non funzionare, poiché gli account di accesso di hello non sono presenti nel nuovo server hello. toolearn sulla gestione degli account di accesso quando si copia un database tooa server logico diverso, vedere [come sicurezza toomanage SQL Azure database dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md). 

Dopo il completamento della copia hello e prima di altri utenti vengono mappate nuovamente, hello account di accesso che ha avviato la copia, hello proprietario del database hello, può effettuare l'accesso solo toohello nuovo database. vedere tooresolve gli account di accesso al termine dell'operazione di copia hello [risolvere gli account di accesso](#resolve-logins).

## <a name="copy-a-database-by-using-hello-azure-portal"></a>Copiare un database utilizzando hello portale di Azure

toocopy hello Azure pagina del portale, hello open per il database e quindi fare clic su un database utilizzando **copia**. 

   ![Copia del database](./media/sql-database-copy/database-copy.png)

## <a name="copy-a-database-by-using-powershell"></a>Copiare un database tramite PowerShell

un database tramite PowerShell, usare hello toocopy [New AzureRmSqlDatabaseCopy](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

Per un esempio completo, vedere [copiare un server di database tooa nuova](scripts/sql-database-copy-database-to-new-server-powershell.md).

## <a name="copy-a-database-by-using-transact-sql"></a>Copiare un database tramite Transact-SQL

Database di log nel database master toohello con account di accesso dell'entità a livello di server hello o hello creati database hello da toocopy. Per toosucceed di copia del database, gli account di accesso che non sono entità di livello server hello devono essere membri del ruolo dbmanager hello. Per ulteriori informazioni sull'account di accesso e il server toohello connessione, vedere [gestire gli account di accesso](sql-database-manage-logins.md).

Avviare la copia di database di origine hello con hello [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) istruzione. L'esecuzione di questa istruzione Avvia processo di copia del database hello. Poiché la copia di un database è un processo asincrono, hello istruzione CREATE DATABASE restituisce prima hello copia del database è stata completata.

### <a name="copy-a-sql-database-toohello-same-server"></a>Copiare un toohello di database SQL nello stesso server
Database di log nel database master toohello con account di accesso dell'entità a livello di server hello o hello creati database hello da toocopy. Per toosucceed di copia del database, gli account di accesso che non sono entità di livello server hello devono essere membri del ruolo dbmanager hello.

Questo comando copia Database1 tooa nuovo database denominato Database2 su hello nello stesso server. A seconda delle dimensioni di hello del database, hello operazione di copia potrebbe richiedere alcuni toocomplete ora.

    -- Execute on hello master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-tooa-different-server"></a>Copiare un altro server tooa database SQL

Database di log nel database master toohello del server di destinazione hello, hello database server SQL in cui il nuovo database di hello toobe creato. Utilizzare un account di accesso come proprietario del database hello hello del database di origine nel server di database SQL di origine hello è hello stesso nome e password. account di accesso di Hello nel server di destinazione hello deve anche essere un membro del ruolo dbmanager hello o essere l'account di accesso hello a livello di server principale.

Questo comando copia Database1 nel nuovo database denominato Database2 su server2 tooa server1. A seconda delle dimensioni di hello del database, hello operazione di copia potrebbe richiedere alcuni toocomplete ora.

    -- Execute on hello master database of hello target server (server2)
    -- Start copying from Server1 tooServer2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-hello-progress-of-hello-copying-operation"></a>Monitorare lo stato di avanzamento hello di hello operazione di copia

Monitoraggio processo di copia hello eseguendo una query su visualizzazioni di Sys. Databases e Sys.dm database_copies hello. Durante la copia di hello è in corso, hello **state_desc** colonna della vista sys. Databases hello per il nuovo database hello è troppo**COPYING**.

* Se la copia di hello non riesce, hello **state_desc** colonna della vista sys. Databases hello per il nuovo database hello è troppo**ritiene**. Eseguire hello istruzione DROP sul nuovo database hello e riprovare più tardi.
* Se la copia di hello ha esito positivo, hello **state_desc** colonna della vista sys. Databases hello per il nuovo database hello è troppo**ONLINE**. Hello copia è completa e hello nuovo database è un database normale che può essere modificato indipendentemente dalla hello database di origine.

> [!NOTE]
> Se si decide di toocancel hello copia mentre è in corso, eseguire hello [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) istruzione sul nuovo database hello. In alternativa, l'istruzione DROP DATABASE hello nel database di origine hello anche Annulla hello processo di copia.
> 

## <a name="resolve-logins"></a>Risolvere gli account di accesso

Dopo aver hello nuovo database è online nel server di destinazione hello, utilizzare hello [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) istruzione tooremap hello utenti hello toologins nel server di destinazione hello di nuovo database. gli utenti isolati (orfani) tooresolve, vedere [risolvere i problemi relativi agli utenti isolati](https://msdn.microsoft.com/library/ms175475.aspx). Vedere anche [come sicurezza toomanage SQL Azure database dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md).

Tutti gli utenti nel nuovo database hello mantengano le autorizzazioni di hello cui disponevano nel database di origine hello. utente Hello che ha avviato una copia del database hello diventa proprietario del database hello del nuovo database hello e viene assegnato un nuovo ID di sicurezza (SID). Dopo il completamento della copia hello e prima di altri utenti vengono mappate nuovamente, hello account di accesso che ha avviato la copia, hello proprietario del database hello, può effettuare l'accesso solo toohello nuovo database.

toolearn sulla gestione di utenti e account di accesso quando si copia un database tooa server logico diverso, vedere [come sicurezza toomanage SQL Azure database dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md).

## <a name="next-steps"></a>Passaggi successivi

* Per informazioni sugli account di accesso, vedere [gestire gli account di accesso](sql-database-manage-logins.md) e [come sicurezza toomanage SQL Azure database dopo il ripristino di emergenza](sql-database-geo-replication-security-config.md).
* tooexport un database, vedere [esportare hello database tooa BACPAC](sql-database-export.md).
