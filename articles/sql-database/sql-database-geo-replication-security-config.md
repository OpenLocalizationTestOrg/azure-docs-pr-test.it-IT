---
title: Configurare la sicurezza del database SQL di Azure per il ripristino di emergenza | Documentazione Microsoft
description: Questo argomento illustra considerazioni sulla configurazione e la gestione della sicurezza dopo il ripristino di un database o il failover in un server secondario dovuto a un'interruzione del data center o ad altre situazioni di emergenza
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
ms.openlocfilehash: de5e1732dab570b80692efcdd08e4ed2d8c98800
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="59afb-103">Configurare e gestire la sicurezza dei database SQL di Azure per il ripristino geografico o il failover</span><span class="sxs-lookup"><span data-stu-id="59afb-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="59afb-104">La [replica geografica attiva](sql-database-geo-replication-overview.md) è ora disponibile per tutti i database in tutti i livelli di servizio.</span><span class="sxs-lookup"><span data-stu-id="59afb-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="59afb-105">Panoramica dei requisiti di autenticazione per il ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="59afb-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="59afb-106">Questo argomento illustra i requisiti di autenticazione per configurare e controllare la [replica geografica attiva](sql-database-geo-replication-overview.md) e i passaggi necessari per configurare l'accesso utente al database secondario.</span><span class="sxs-lookup"><span data-stu-id="59afb-106">This topic describes the authentication requirements to configure and control [active geo-replication](sql-database-geo-replication-overview.md) and the steps required to set up user access to the secondary database.</span></span> <span data-ttu-id="59afb-107">Descrive anche come abilitare l'accesso al database ripristinato dopo il [ripristino geografico](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="59afb-107">It also describes how enable access to the recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="59afb-108">Per altre informazioni sulle opzioni di ripristino, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="59afb-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="59afb-109">Ripristino di emergenza con gli utenti indipendenti</span><span class="sxs-lookup"><span data-stu-id="59afb-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="59afb-110">A differenza degli utenti tradizionali per i quali deve essere eseguito il mapping agli account di accesso nel database master, un utente indipendente viene gestito completamente dal database stesso.</span><span class="sxs-lookup"><span data-stu-id="59afb-110">Unlike traditional users, which must be mapped to logins in the master database, a contained user is managed completely by the database itself.</span></span> <span data-ttu-id="59afb-111">Questo approccio presenta due vantaggi.</span><span class="sxs-lookup"><span data-stu-id="59afb-111">This has two benefits.</span></span> <span data-ttu-id="59afb-112">Nello scenario di ripristino di emergenza, gli utenti possono continuare a connettersi al nuovo database primario o al database ripristinato con il ripristino geografico senza alcuna configurazione aggiuntiva, perché il database gestisce gli utenti.</span><span class="sxs-lookup"><span data-stu-id="59afb-112">In the disaster recovery scenario, the users can continue to connect to the new primary database or the database recovered using geo-restore without any additional configuration, because the database manages the users.</span></span> <span data-ttu-id="59afb-113">Dal punto di vista dell'accesso, questa configurazione offre anche vantaggi a livello di scalabilità e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="59afb-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="59afb-114">Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="59afb-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="59afb-115">Il compromesso principale è rappresentato dal fatto che il processo di ripristino di emergenza su vasta scala è più complesso da gestire.</span><span class="sxs-lookup"><span data-stu-id="59afb-115">The main trade-off is that managing the disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="59afb-116">Quando si dispone di più database che usano lo stesso account di accesso, la gestione delle credenziali usate dagli utenti indipendenti in più database può annullare il vantaggio rappresentato dagli utenti indipendenti.</span><span class="sxs-lookup"><span data-stu-id="59afb-116">When you have multiple databases that use the same login, maintaining the credentials using contained users in multiple databases may negate the benefits of contained users.</span></span> <span data-ttu-id="59afb-117">Ad esempio, i criteri di rotazione delle password richiedono l'applicazione coerente delle modifiche in più database anziché la modifica singola della password per l'accesso nel database master.</span><span class="sxs-lookup"><span data-stu-id="59afb-117">For example, the password rotation policy requires that changes be made consistently in multiple databases rather than changing the password for the login once in the master database.</span></span> <span data-ttu-id="59afb-118">Per questo motivo l'uso degli utenti indipendenti non è consigliato in presenza di molti database che usano lo stesso nome utente e la stessa password.</span><span class="sxs-lookup"><span data-stu-id="59afb-118">For this reason, if you have multiple databases that use the same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-to-configure-logins-and-users"></a><span data-ttu-id="59afb-119">Come configurare gli account di accesso e gli utenti</span><span class="sxs-lookup"><span data-stu-id="59afb-119">How to configure logins and users</span></span>
<span data-ttu-id="59afb-120">Se si usano account di accesso e utenti tradizionali, invece di utenti indipendenti, è necessario eseguire altri passaggi per assicurare che nel database master siano presenti gli stessi account di accesso.</span><span class="sxs-lookup"><span data-stu-id="59afb-120">If you are using logins and users (rather than contained users), you must take extra steps to insure that the same logins exist in the master database.</span></span> <span data-ttu-id="59afb-121">Le sezioni seguenti illustrano i passaggi da eseguire, oltre a considerazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="59afb-121">The following sections outline the steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-to-a-secondary-or-recovered-database"></a><span data-ttu-id="59afb-122">Impostare l'accesso utente a un database secondario o ripristinato</span><span class="sxs-lookup"><span data-stu-id="59afb-122">Set up user access to a secondary or recovered database</span></span>
<span data-ttu-id="59afb-123">Per fare in modo che il database secondario sia utilizzabile come database secondario di sola lettura e per garantire l'accesso appropriato al nuovo database primario o al database ripristinato con il ripristino geografico, è necessario che nel database master del server di destinazione sia presente la configurazione di sicurezza appropriata prima del ripristino.</span><span class="sxs-lookup"><span data-stu-id="59afb-123">In order for the secondary database to be usable as a read-only secondary database, and to ensure proper access to the new primary database or the database recovered using geo-restore, the master database of the target server must have the appropriate security configuration in place before the recovery.</span></span>

<span data-ttu-id="59afb-124">Le autorizzazioni specifiche per ogni passaggio sono descritte più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="59afb-124">The specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="59afb-125">La preparazione dell'accesso utente a un database secondario con replica geografica deve essere eseguita durante la configurazione della replica geografica.</span><span class="sxs-lookup"><span data-stu-id="59afb-125">Preparing user access to a geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="59afb-126">La preparazione dell'accesso utente ai database ripristinati con il ripristino geografico deve essere eseguita in qualsiasi momento quando il server originale è online, ad esempio nel contesto dell'analisi del ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="59afb-126">Preparing user access to the geo-restored databases should be performed at any time when the original server is online (e.g. as part of the DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="59afb-127">Se si esegue il failover o il ripristino geografico in un server che non presenta account di accesso configurati adeguatamente, l'accesso sarà limitato all'account amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="59afb-127">If you fail over or geo-restore to a server that does not have properly configured logins, access to it will be limited to the server admin account.</span></span>
> 
> 

<span data-ttu-id="59afb-128">La configurazione degli account di accesso nel server di destinazione prevede i tre passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="59afb-128">Setting up logins on the target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-to-the-primary-database"></a><span data-ttu-id="59afb-129">1. Determinare gli account di accesso che possono accedere al database primario:</span><span class="sxs-lookup"><span data-stu-id="59afb-129">1. Determine logins with access to the primary database:</span></span>
<span data-ttu-id="59afb-130">Il primo passaggio della procedura consiste nel determinare quali account di accesso devono essere duplicati nel server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="59afb-130">The first step of the process is to determine which logins must be duplicated on the target server.</span></span> <span data-ttu-id="59afb-131">A questo scopo, è necessario usare una coppia di istruzioni SELECT, una nel database master logico nel server di origine e una nel database primario stesso.</span><span class="sxs-lookup"><span data-stu-id="59afb-131">This is accomplished with a pair of SELECT statements, one in the logical master database on the source server and one in the primary database itself.</span></span>

<span data-ttu-id="59afb-132">Solo l'amministratore del server o un membro del ruolo del server **LoginManager** può determinare gli account di accesso nel server di origine con l'istruzione SELECT seguente.</span><span class="sxs-lookup"><span data-stu-id="59afb-132">Only the server admin or a member of the **LoginManager** server role can determine the logins on the source server with the following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="59afb-133">Solo un membro del ruolo del database db_owner, l'utente dbo o l'amministratore del server può determinare tutte le entità utente nel database primario.</span><span class="sxs-lookup"><span data-stu-id="59afb-133">Only a member of the db_owner database role, the dbo user, or server admin, can determine all of the database user principals in the primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-the-sid-for-the-logins-identified-in-step-1"></a><span data-ttu-id="59afb-134">2. Trovare il SID degli account di accesso identificati nel passaggio 1:</span><span class="sxs-lookup"><span data-stu-id="59afb-134">2. Find the SID for the logins identified in step 1:</span></span>
<span data-ttu-id="59afb-135">Confrontando l'output delle query illustrate nella sezione precedente e trovando una corrispondenza per i SID, è possibile eseguire il mapping dell'account di accesso del server all'utente del database.</span><span class="sxs-lookup"><span data-stu-id="59afb-135">By comparing the output of the queries from the previous section and matching the SIDs, you can map the server login to database user.</span></span> <span data-ttu-id="59afb-136">Gli account di accesso che hanno un utente del database con un SID corrispondente hanno anche l'accesso utente a quel database come entità utente.</span><span class="sxs-lookup"><span data-stu-id="59afb-136">Logins that have a database user with a matching SID have user access to that database as that database user principal.</span></span> 

<span data-ttu-id="59afb-137">La query seguente può essere usata per visualizzare tutte le entità utente e i relativi SID in un database.</span><span class="sxs-lookup"><span data-stu-id="59afb-137">The following query can be used to see all of the user principals and their SIDs in a database.</span></span> <span data-ttu-id="59afb-138">Questa query può essere eseguita solo da un membro del ruolo del database db_owner o dall'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="59afb-138">Only a member of the db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="59afb-139">Gli utenti **INFORMATION_SCHEMA** e **sys** avranno SID *NULL*, mentre il SID **guest** è **0x00**.</span><span class="sxs-lookup"><span data-stu-id="59afb-139">The **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and the **guest** SID is **0x00**.</span></span> <span data-ttu-id="59afb-140">Il SID **dbo** può iniziare con *0x01060000000001648000000000048454* se il database è stato creato dall'amministratore del server invece che da un membro di **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="59afb-140">The **dbo** SID may start with *0x01060000000001648000000000048454*, if the database creator was the server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-the-logins-on-the-target-server"></a><span data-ttu-id="59afb-141">3. Creare gli account di accesso nel server di destinazione:</span><span class="sxs-lookup"><span data-stu-id="59afb-141">3. Create the logins on the target server:</span></span>
<span data-ttu-id="59afb-142">L'ultimo passaggio consiste nel generare gli account di accesso con i SID appropriati nel server o nei server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="59afb-142">The last step is to go to the target server, or servers, and generate the logins with the appropriate SIDs.</span></span> <span data-ttu-id="59afb-143">La sintassi di base è la seguente.</span><span class="sxs-lookup"><span data-stu-id="59afb-143">The basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="59afb-144">Se si vuole concedere l'accesso utente al database secondario, ma non al database primario, è possibile modificare l'account di accesso utente nel server primario usando la sintassi seguente.</span><span class="sxs-lookup"><span data-stu-id="59afb-144">If you want to grant user access to the secondary, but not to the primary, you can do that by altering the user login on the primary server by using the following syntax.</span></span>
> 
> <span data-ttu-id="59afb-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="59afb-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="59afb-146">DISABLE non modifica la password, pertanto è sempre possibile abilitare l'accesso, se necessario.</span><span class="sxs-lookup"><span data-stu-id="59afb-146">DISABLE doesn’t change the password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="59afb-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="59afb-147">Next steps</span></span>
* <span data-ttu-id="59afb-148">Per altre informazioni sulla gestione dell'accesso al database e degli account di accesso, vedere [Protezione del database SQL: gestire l'accesso al database e la sicurezza degli account di accesso](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="59afb-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="59afb-149">Per altre informazioni sugli utenti di database indipendente, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="59afb-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="59afb-150">Per informazioni sull'uso e la configurazione della replica geografica attiva, vedere [Replica geografica attiva](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="59afb-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="59afb-151">Per informazioni sull'uso del ripristino geografico, vedere l'argomento sul [ripristino geografico](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="59afb-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

