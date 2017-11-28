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
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="c8892-103">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="c8892-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c8892-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8892-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="c8892-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="c8892-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="c8892-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c8892-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="c8892-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="c8892-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="c8892-108">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="c8892-108">Required Permssions</span></span>
<span data-ttu-id="c8892-109">tooenable Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager hello.</span><span class="sxs-lookup"><span data-stu-id="c8892-109">tooenable Transparent Data Encryption (TDE), you must be an administrator or a member of hello dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="c8892-110">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="c8892-110">Enabling Encryption</span></span>
<span data-ttu-id="c8892-111">Seguire questi tooenable passaggi TDE per un SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="c8892-111">Follow these steps tooenable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="c8892-112">Connettersi toohello *master* database hello server che ospita il database hello utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="c8892-112">Connect toohello *master* database on hello server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c8892-113">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c8892-113">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="c8892-114">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="c8892-114">Disabling Encryption</span></span>
<span data-ttu-id="c8892-115">Seguire questi toodisable passaggi TDE per un SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="c8892-115">Follow these steps toodisable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="c8892-116">Connettersi toohello *master* database utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="c8892-116">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c8892-117">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c8892-117">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="c8892-118">Prima di modificare le impostazioni di Transparent Data Encryption toohello, è necessario riprendere una pausa SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c8892-118">A paused SQL Data Warehouse must be resumed before making changes toohello TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="c8892-119">Verifica della crittografia</span><span class="sxs-lookup"><span data-stu-id="c8892-119">Verifying Encryption</span></span>
<span data-ttu-id="c8892-120">lo stato di crittografia tooverify per SQL Data Warehouse, procedura hello riportata di seguito:</span><span class="sxs-lookup"><span data-stu-id="c8892-120">tooverify encryption status for a SQL Data Warehouse, follow hello steps below:</span></span>

1. <span data-ttu-id="c8892-121">Connettersi toohello *master* o database dell'istanza utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="c8892-121">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="c8892-122">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c8892-122">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="c8892-123">Il risultato ```1``` indica un database crittografato, ```0``` indica un database non crittografato.</span><span class="sxs-lookup"><span data-stu-id="c8892-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="c8892-124">Viste a gestione dinamica della crittografia</span><span class="sxs-lookup"><span data-stu-id="c8892-124">Encryption DMVs</span></span>
* <span data-ttu-id="c8892-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="c8892-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="c8892-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="c8892-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
