---
title: Abilitare Transparent Data Encryption per Estensione database (T-SQL) - Azure | Documentazione Microsoft
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
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="6463c-103">Abilitare Transparent Data Encryption (TDE) per Estensione database su Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="6463c-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6463c-104">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="6463c-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="6463c-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="6463c-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="6463c-106">La funzionalità Transparent Data Encryption (TDE) consente di proteggersi da attività dannose eseguendo in tempo reale la crittografia e la decrittografia dei database, dei backup associati e dei file di log delle transazioni inattivi, senza dover apportare modifiche all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="6463c-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="6463c-107">TDE esegue la crittografia dell'archiviazione di un intero database usando una chiave simmetrica detta "chiave di crittografia del database".</span><span class="sxs-lookup"><span data-stu-id="6463c-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="6463c-108">La chiave di crittografia del database è protetta da un certificato server incorporato.</span><span class="sxs-lookup"><span data-stu-id="6463c-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="6463c-109">Il certificato server incorporato è univoco per ogni server Azure.</span><span class="sxs-lookup"><span data-stu-id="6463c-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="6463c-110">Microsoft ruota automaticamente questi certificati almeno ogni 90 giorni.</span><span class="sxs-lookup"><span data-stu-id="6463c-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="6463c-111">Per una descrizione generale della funzionalità TDE, vedere [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="6463c-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="6463c-112">Abilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="6463c-112">Enabling Encryption</span></span>
<span data-ttu-id="6463c-113">Per abilitare la funzionalità TDE per un database di Azure che archivia i dati migrati da un database SQL Server con Estensione abilitata, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6463c-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="6463c-114">Connettere il database *master* sul server Azure che ospita il database usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master</span><span class="sxs-lookup"><span data-stu-id="6463c-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="6463c-115">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="6463c-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="6463c-116">Disabilitazione della crittografia</span><span class="sxs-lookup"><span data-stu-id="6463c-116">Disabling Encryption</span></span>
<span data-ttu-id="6463c-117">Per disabilitare TDE per un database di Azure che archivia i dati migrati da un database SQL Server con Estensione abilitata, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6463c-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="6463c-118">Connettere il database *master* usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master.</span><span class="sxs-lookup"><span data-stu-id="6463c-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="6463c-119">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="6463c-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="6463c-120">Verifica della crittografia</span><span class="sxs-lookup"><span data-stu-id="6463c-120">Verifying Encryption</span></span>
<span data-ttu-id="6463c-121">Per verificare lo stato della crittografia per un database di Azure che archivia i dati migrati da un database SQL Server con Estensione abilitata, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="6463c-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="6463c-122">Connettere il database *master* o dell'istanza usando un account di accesso di un amministratore o di un membro del ruolo **dbmanager** nel database master.</span><span class="sxs-lookup"><span data-stu-id="6463c-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="6463c-123">Eseguire l'istruzione seguente per crittografare il database.</span><span class="sxs-lookup"><span data-stu-id="6463c-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="6463c-124">Il risultato ```1``` indica un database crittografato, ```0``` indica un database non crittografato.</span><span class="sxs-lookup"><span data-stu-id="6463c-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
<span data-ttu-id="6463c-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="6463c-125">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->

<!--Link references-->
