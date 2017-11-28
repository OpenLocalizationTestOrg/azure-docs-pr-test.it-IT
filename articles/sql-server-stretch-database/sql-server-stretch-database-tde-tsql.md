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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="e659c-103">Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="e659c-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e659c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e659c-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="e659c-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="e659c-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="e659c-106">Transparent Data Encryption (TDE) contribuisce alla protezione dalle minacce di hello di attività dannose eseguendo la crittografia in tempo reale e la decrittografia del database hello, i backup associati e i file di log delle transazioni a riposo senza richiedere modifiche toohello applicazione.</span><span class="sxs-lookup"><span data-stu-id="e659c-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="e659c-107">Transparent Data Encryption crittografa l'archivio di hello di un intero database utilizzando una chiave di crittografia simmetrica hello chiamata chiave database.</span><span class="sxs-lookup"><span data-stu-id="e659c-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="e659c-108">chiave di crittografia del database Hello è protetto da un certificato server predefinito.</span><span class="sxs-lookup"><span data-stu-id="e659c-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="e659c-109">certificato server predefinito Hello è univoco per ogni server di Azure.</span><span class="sxs-lookup"><span data-stu-id="e659c-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="e659c-110">Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="e659c-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="e659c-111">Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="e659c-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="e659c-112">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="e659c-112">Enabling Encryption</span></span>
<span data-ttu-id="e659c-113">tooenable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e659c-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e659c-114">Connettersi toohello *master* database hello Azure hosting hello database del server utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="e659c-114">Connect toohello *master* database on hello Azure server hosting hello database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e659c-115">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="e659c-115">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="e659c-116">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="e659c-116">Disabling Encryption</span></span>
<span data-ttu-id="e659c-117">toodisable TDE per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e659c-117">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e659c-118">Connettersi toohello *master* database utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="e659c-118">Connect toohello *master* database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e659c-119">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="e659c-119">Execute hello following statement tooencrypt hello database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="e659c-120">Verifica della crittografia</span><span class="sxs-lookup"><span data-stu-id="e659c-120">Verifying Encryption</span></span>
<span data-ttu-id="e659c-121">lo stato di crittografia tooverify per un database di Azure a cui è archiviati i dati migrati da un database di SQL Server abilitata per l'estensione, hello hello seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e659c-121">tooverify encryption status for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="e659c-122">Connettersi toohello *master* o database dell'istanza utilizzando un account di accesso è un amministratore o un membro di hello **dbmanager** ruolo nel database master hello</span><span class="sxs-lookup"><span data-stu-id="e659c-122">Connect toohello *master* or instance database using a login that is an administrator or a member of hello **dbmanager** role in hello master database</span></span>
2. <span data-ttu-id="e659c-123">Eseguire hello seguente database hello tooencrypt di istruzione.</span><span class="sxs-lookup"><span data-stu-id="e659c-123">Execute hello following statement tooencrypt hello database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="e659c-124">Il risultato ```1``` indica un database crittografato, ```0``` indica un database non crittografato.</span><span class="sxs-lookup"><span data-stu-id="e659c-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
