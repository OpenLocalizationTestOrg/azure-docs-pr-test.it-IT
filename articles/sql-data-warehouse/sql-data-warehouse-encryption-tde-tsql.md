---
title: Transparent Data Encryption in SQL Data Warehouse (T-SQL) | Documentazione Microsoft
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
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="e4532-103">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="e4532-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e4532-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e4532-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="e4532-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e4532-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="e4532-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e4532-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="e4532-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="e4532-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="e4532-108">Autorizzazioni necessarie</span><span class="sxs-lookup"><span data-stu-id="e4532-108">Required Permssions</span></span>
<span data-ttu-id="e4532-109">Per abilitare Transparent Data Encryption (TDE), è necessario essere un amministratore o un membro del ruolo dbmanager.</span><span class="sxs-lookup"><span data-stu-id="e4532-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="e4532-110">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="e4532-110">Enabling Encryption</span></span>
<span data-ttu-id="e4532-111">Per abilitare TDE per un SQL Data Warehouse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e4532-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="e4532-112">Connettere il database *master* sul server che ospita il database usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master.</span><span class="sxs-lookup"><span data-stu-id="e4532-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e4532-113">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="e4532-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="e4532-114">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="e4532-114">Disabling Encryption</span></span>
<span data-ttu-id="e4532-115">Per disabilitare TDE per un SQL Data Warehouse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e4532-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="e4532-116">Connettere il database *master* usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master.</span><span class="sxs-lookup"><span data-stu-id="e4532-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e4532-117">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="e4532-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> <span data-ttu-id="e4532-118">Prima di modificare le impostazioni TDE, è necessario interrompere la sospensione di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e4532-118">A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.</span></span>
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="e4532-119">Verifica della crittografia</span><span class="sxs-lookup"><span data-stu-id="e4532-119">Verifying Encryption</span></span>
<span data-ttu-id="e4532-120">Per verificare lo stato della crittografia per un SQL Data Warehouse, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e4532-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="e4532-121">Connettere il database *master* o dell'istanza usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master.</span><span class="sxs-lookup"><span data-stu-id="e4532-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="e4532-122">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="e4532-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="e4532-123">Il risultato ```1``` indica un database crittografato, ```0``` indica un database non crittografato.</span><span class="sxs-lookup"><span data-stu-id="e4532-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="e4532-124">Viste a gestione dinamica della crittografia</span><span class="sxs-lookup"><span data-stu-id="e4532-124">Encryption DMVs</span></span>
* <span data-ttu-id="e4532-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="e4532-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="e4532-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="e4532-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
