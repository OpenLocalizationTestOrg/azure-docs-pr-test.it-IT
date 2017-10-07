---
title: Transparent Data Encryption per estensione Database TSQL - Azure aaaEnable | Documenti Microsoft
description: Abilitare Transparent Data Encryption (TDE) per Estensione database di SQL Server su Azure TSQL
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: jhubbard
editor: 
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: a9ba23649656fb344480d79438a1115f0eb353bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Portale di Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia del database hello, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche toohello applicazione.

Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database. chiave di crittografia del database Hello è protetto da un certificato server predefinito. certificato server predefinito Hello è univoco per ogni server di Azure. Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni. Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Abilitazione della crittografia
tooenable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:

1. Connettersi toohello *master* database hello Azure hosting hello database del server utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello
2. Eseguire hello seguente database hello tooencrypt di istruzione.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Disabilitazione della crittografia
toodisable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:

1. Connettersi toohello *master* database utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello
2. Eseguire hello seguente database hello tooencrypt di istruzione.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Verifica della crittografia
lo stato di crittografia tooverify per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:

1. Connettersi toohello *master* o database dell'istanza utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello
2. Eseguire hello seguente database hello tooencrypt di istruzione.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

Il risultato ```1``` indica un database crittografato, ```0``` indica un database non crittografato.

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
