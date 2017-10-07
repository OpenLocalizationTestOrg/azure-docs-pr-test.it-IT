---
title: la crittografia dei dati nel Data Warehouse di SQL (T-SQL) aaaTransparent | Documenti Microsoft
description: Transparent Data Encryption (TDE) in SQL Data Warehouse (T-SQL).
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: barbkess
editor: 
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 3894431c76f14b217f3a6b9a42dbf2f4d216bad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a>Introduzione a Transparent Data Encryption (TDE)
> [!div class="op_single_selector"]
> * [Proteggere un database in SQL Data Warehouse](sql-data-warehouse-overview-manage-security.md)
> * [Autenticazione](sql-data-warehouse-authentication.md)
> * [Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse](sql-data-warehouse-encryption-tde.md)
> * [Introduzione a Transparent Data Encryption (TDE)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a>Autorizzazioni necessarie
tooenable Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager hello.

## <a name="enabling-encryption"></a>Abilitazione della crittografia
Seguire questi tooenable passaggi TDE per un SQL Data Warehouse:

1. Connettersi toohello *master* database hello server che ospita il database hello utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello
2. Eseguire hello seguente database hello tooencrypt di istruzione.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Disabilitazione della crittografia
Seguire questi toodisable passaggi TDE per un SQL Data Warehouse:

1. Connettersi toohello *master* database utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello
2. Eseguire hello seguente database hello tooencrypt di istruzione.

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> Prima di modificare le impostazioni di Transparent Data Encryption toohello, è necessario riprendere una pausa SQL Data Warehouse.
> 
> 

## <a name="verifying-encryption"></a>Verifica della crittografia
lo stato di crittografia tooverify per SQL Data Warehouse, procedura hello riportata di seguito:

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

## <a name="encryption-dmvs"></a>Viste a gestione dinamica della crittografia
* [sys.databases][sys.databases] 
* [sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
