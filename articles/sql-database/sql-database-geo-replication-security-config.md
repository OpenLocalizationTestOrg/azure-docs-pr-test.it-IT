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
# <a name="configure-and-manage-azure-sql-database-security-for-geo-restore-or-failover"></a><span data-ttu-id="bd1e3-103">Configurare e gestire la sicurezza dei database SQL di Azure per il ripristino geografico o il failover</span><span class="sxs-lookup"><span data-stu-id="bd1e3-103">Configure and manage Azure SQL Database security for geo-restore or failover</span></span> 

> [!NOTE]
> <span data-ttu-id="bd1e3-104">La [replica geografica attiva](sql-database-geo-replication-overview.md) è ora disponibile per tutti i database in tutti i livelli di servizio.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-104">[Active geo-replication](sql-database-geo-replication-overview.md) is now available for all databases in all service tiers.</span></span>
>  

## <a name="overview-of-authentication-requirements-for-disaster-recovery"></a><span data-ttu-id="bd1e3-105">Panoramica dei requisiti di autenticazione per il ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="bd1e3-105">Overview of authentication requirements for disaster recovery</span></span>
<span data-ttu-id="bd1e3-106">Questo argomento descrive tooconfigure requisiti di autenticazione hello e controllo [replica geografica attiva](sql-database-geo-replication-overview.md) e hello i passaggi necessari tooset backup di database secondario toohello di accesso utente.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-106">This topic describes hello authentication requirements tooconfigure and control [active geo-replication](sql-database-geo-replication-overview.md) and hello steps required tooset up user access toohello secondary database.</span></span> <span data-ttu-id="bd1e3-107">Viene inoltre descritto come abilitare i database di access toohello recuperato dopo l'utilizzo di [ripristino a livello geografico](sql-database-recovery-using-backups.md#geo-restore).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-107">It also describes how enable access toohello recovered database after using [geo-restore](sql-database-recovery-using-backups.md#geo-restore).</span></span> <span data-ttu-id="bd1e3-108">Per altre informazioni sulle opzioni di ripristino, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-108">For more information on recovery options, see [Business Continuity Overview](sql-database-business-continuity.md).</span></span>

## <a name="disaster-recovery-with-contained-users"></a><span data-ttu-id="bd1e3-109">Ripristino di emergenza con gli utenti indipendenti</span><span class="sxs-lookup"><span data-stu-id="bd1e3-109">Disaster recovery with contained users</span></span>
<span data-ttu-id="bd1e3-110">A differenza degli utenti tradizionale, che deve essere eseguito il mapping nel database master hello toologins, un utente indipendente è gestito completamente dal database hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-110">Unlike traditional users, which must be mapped toologins in hello master database, a contained user is managed completely by hello database itself.</span></span> <span data-ttu-id="bd1e3-111">Questo approccio presenta due vantaggi.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-111">This has two benefits.</span></span> <span data-ttu-id="bd1e3-112">Nello scenario di ripristino di emergenza hello, gli utenti di hello possono continuare tooconnect toohello nuovo database primario o database di hello recuperato mediante geo-restore senza configurazione aggiuntiva, perché il database di hello gestisce gli utenti di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-112">In hello disaster recovery scenario, hello users can continue tooconnect toohello new primary database or hello database recovered using geo-restore without any additional configuration, because hello database manages hello users.</span></span> <span data-ttu-id="bd1e3-113">Dal punto di vista dell'accesso, questa configurazione offre anche vantaggi a livello di scalabilità e prestazioni.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-113">There are also potential scalability and performance benefits from this configuration from a login perspective.</span></span> <span data-ttu-id="bd1e3-114">Per altre informazioni, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-114">For more information, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span> 

<span data-ttu-id="bd1e3-115">compromesso di Hello principale è che Gestione processo di ripristino di emergenza hello su larga scala più impegnativa.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-115">hello main trade-off is that managing hello disaster recovery process at scale is more challenging.</span></span> <span data-ttu-id="bd1e3-116">Quando si dispone di più database hello tale uso stesso account di accesso, Gestione credenziali hello utilizzando contenuti agli utenti in più database possono annullare i vantaggi hello di utenti indipendenti.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-116">When you have multiple databases that use hello same login, maintaining hello credentials using contained users in multiple databases may negate hello benefits of contained users.</span></span> <span data-ttu-id="bd1e3-117">Ad esempio, criteri di rotazione hello password richiedono che modifiche in modo coerente in più database anziché la modifica della password per account di accesso hello hello una volta nel database master hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-117">For example, hello password rotation policy requires that changes be made consistently in multiple databases rather than changing hello password for hello login once in hello master database.</span></span> <span data-ttu-id="bd1e3-118">Per questo motivo, se si dispone di più database hello che usa lo stesso nome utente e password, gli utenti indipendenti consiglia di non utilizzare.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-118">For this reason, if you have multiple databases that use hello same user name and password, using contained users is not recommended.</span></span> 

## <a name="how-tooconfigure-logins-and-users"></a><span data-ttu-id="bd1e3-119">Come tooconfigure account di accesso e utenti</span><span class="sxs-lookup"><span data-stu-id="bd1e3-119">How tooconfigure logins and users</span></span>
<span data-ttu-id="bd1e3-120">Se si utilizza l'account di accesso e utenti (anziché gli utenti indipendenti), è necessario eseguire passaggi aggiuntivi tooinsure tale hello stessi account di accesso esiste nel database master hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-120">If you are using logins and users (rather than contained users), you must take extra steps tooinsure that hello same logins exist in hello master database.</span></span> <span data-ttu-id="bd1e3-121">Hello nelle sezioni seguenti considerazioni coinvolti e ulteriori passaggi di hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-121">hello following sections outline hello steps involved and additional considerations.</span></span>

### <a name="set-up-user-access-tooa-secondary-or-recovered-database"></a><span data-ttu-id="bd1e3-122">Configurare accesso tooa secondario o recuperata database utente</span><span class="sxs-lookup"><span data-stu-id="bd1e3-122">Set up user access tooa secondary or recovered database</span></span>
<span data-ttu-id="bd1e3-123">Affinché toobe database secondario hello utilizzabile come un database secondario di sola lettura e tooensure accesso appropriato toohello nuovo database o hello database primario recuperato utilizzando ripristino a livello geografico, hello master database hello del server di destinazione deve disporre di hello configurazione di sicurezza appropriate prima ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-123">In order for hello secondary database toobe usable as a read-only secondary database, and tooensure proper access toohello new primary database or hello database recovered using geo-restore, hello master database of hello target server must have hello appropriate security configuration in place before hello recovery.</span></span>

<span data-ttu-id="bd1e3-124">autorizzazioni specifiche di Hello per ogni passaggio sono descritte più avanti in questo argomento.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-124">hello specific permissions for each step are described later in this topic.</span></span>

<span data-ttu-id="bd1e3-125">Preparazione tooa di accesso utente replica geografica secondaria deve essere eseguita durante la configurazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-125">Preparing user access tooa geo-replication secondary should be performed as part configuring geo-replication.</span></span> <span data-ttu-id="bd1e3-126">Preparazione dell'accesso utente database ripristinato geografica toohello deve essere eseguita in qualsiasi momento server originale hello è online (ad esempio come parte di drill di ripristino di emergenza hello).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-126">Preparing user access toohello geo-restored databases should be performed at any time when hello original server is online (e.g. as part of hello DR drill).</span></span>

> [!NOTE]
> <span data-ttu-id="bd1e3-127">Se si esegue il failover o il ripristino geografico tooa server che non dispone di account di accesso configurato correttamente, accesso tooit sarà l'account amministratore del server toohello limitato.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-127">If you fail over or geo-restore tooa server that does not have properly configured logins, access tooit will be limited toohello server admin account.</span></span>
> 
> 

<span data-ttu-id="bd1e3-128">Impostazione di account di accesso nel server di destinazione hello comporta tre passaggi descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="bd1e3-128">Setting up logins on hello target server involves three steps outlined below:</span></span>

#### <a name="1-determine-logins-with-access-toohello-primary-database"></a><span data-ttu-id="bd1e3-129">1. Determinare gli account di accesso con database di access toohello primario:</span><span class="sxs-lookup"><span data-stu-id="bd1e3-129">1. Determine logins with access toohello primary database:</span></span>
<span data-ttu-id="bd1e3-130">Hello del processo di hello è innanzitutto necessario duplicare gli account di accesso nel server di destinazione hello toodetermine.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-130">hello first step of hello process is toodetermine which logins must be duplicated on hello target server.</span></span> <span data-ttu-id="bd1e3-131">Questa operazione viene eseguita con una coppia di istruzioni SELECT, uno nel database master logico hello nel server di origine hello e uno nel database primario di hello stesso.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-131">This is accomplished with a pair of SELECT statements, one in hello logical master database on hello source server and one in hello primary database itself.</span></span>

<span data-ttu-id="bd1e3-132">Hello solo l'amministratore del server o un membro di hello **LoginManager** ruolo del server è possibile determinare gli account di accesso hello nel server di origine hello con hello segue l'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-132">Only hello server admin or a member of hello **LoginManager** server role can determine hello logins on hello source server with hello following SELECT statement.</span></span> 

    SELECT [name], [sid] 
    FROM [sys].[sql_logins] 
    WHERE [type_desc] = 'SQL_Login'

<span data-ttu-id="bd1e3-133">Solo un membro del ruolo del database db_owner hello, utente dbo hello o amministratore del server, è possibile determinare tutti hello utente entità di database nel database primario hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-133">Only a member of hello db_owner database role, hello dbo user, or server admin, can determine all of hello database user principals in hello primary database.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

#### <a name="2-find-hello-sid-for-hello-logins-identified-in-step-1"></a><span data-ttu-id="bd1e3-134">2. Trovare hello SID per l'account di accesso hello identificato nel passaggio 1:</span><span class="sxs-lookup"><span data-stu-id="bd1e3-134">2. Find hello SID for hello logins identified in step 1:</span></span>
<span data-ttu-id="bd1e3-135">Confrontando l'output di hello di query hello dalla sezione precedente hello e hello corrispondente SID, è possibile eseguire il mapping utente toodatabase con accesso server hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-135">By comparing hello output of hello queries from hello previous section and matching hello SIDs, you can map hello server login toodatabase user.</span></span> <span data-ttu-id="bd1e3-136">Account di accesso che dispongono di un utente del database con un SID corrispondente sono database toothat di accesso utente con questo nome utente del database principale.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-136">Logins that have a database user with a matching SID have user access toothat database as that database user principal.</span></span> 

<span data-ttu-id="bd1e3-137">Hello nella query seguente può essere utilizzato toosee tutte le entità utente hello e i relativi SID in un database.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-137">hello following query can be used toosee all of hello user principals and their SIDs in a database.</span></span> <span data-ttu-id="bd1e3-138">Solo un membro di hello db_owner del database del server o del ruolo amministratore può eseguire questa query.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-138">Only a member of hello db_owner database role or server admin can run this query.</span></span>

    SELECT [name], [sid]
    FROM [sys].[database_principals]
    WHERE [type_desc] = 'SQL_USER'

> [!NOTE]
> <span data-ttu-id="bd1e3-139">Hello **INFORMATION_SCHEMA** e **sys** gli utenti hanno *NULL* SID e hello **guest** SID è **0x00**.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-139">hello **INFORMATION_SCHEMA** and **sys** users have *NULL* SIDs, and hello **guest** SID is **0x00**.</span></span> <span data-ttu-id="bd1e3-140">Hello **dbo** SID può iniziare con *0x01060000000001648000000000048454*, se hello database è stato salve server anziché un membro di **DbManager**.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-140">hello **dbo** SID may start with *0x01060000000001648000000000048454*, if hello database creator was hello server admin instead of a member of **DbManager**.</span></span>
> 
> 

#### <a name="3-create-hello-logins-on-hello-target-server"></a><span data-ttu-id="bd1e3-141">3. Creare gli account di accesso di hello sul server di destinazione hello:</span><span class="sxs-lookup"><span data-stu-id="bd1e3-141">3. Create hello logins on hello target server:</span></span>
<span data-ttu-id="bd1e3-142">Hello ultimo passaggio è toogo toohello server di destinazione o server e generare gli account di accesso hello con hello SID appropriati.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-142">hello last step is toogo toohello target server, or servers, and generate hello logins with hello appropriate SIDs.</span></span> <span data-ttu-id="bd1e3-143">sintassi di base Hello è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-143">hello basic syntax is as follows.</span></span>

    CREATE LOGIN [<login name>]
    WITH PASSWORD = <login password>,
    SID = <desired login SID>

> [!NOTE]
> <span data-ttu-id="bd1e3-144">Se si desidera toogrant utente accesso toohello secondario, ma non i toohello primario, è possibile farlo mediante la modifica di account di accesso utente hello nel server primario hello utilizzando la seguente sintassi hello.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-144">If you want toogrant user access toohello secondary, but not toohello primary, you can do that by altering hello user login on hello primary server by using hello following syntax.</span></span>
> 
> <span data-ttu-id="bd1e3-145">ALTER LOGIN <login name> DISABLE</span><span class="sxs-lookup"><span data-stu-id="bd1e3-145">ALTER LOGIN <login name> DISABLE</span></span>
> 
> <span data-ttu-id="bd1e3-146">DISABLE non modifica la password di hello, pertanto è sempre possibile abilitarla se necessario.</span><span class="sxs-lookup"><span data-stu-id="bd1e3-146">DISABLE doesn’t change hello password, so you can always enable it if needed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bd1e3-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bd1e3-147">Next steps</span></span>
* <span data-ttu-id="bd1e3-148">Per altre informazioni sulla gestione dell'accesso al database e degli account di accesso, vedere [Protezione del database SQL: gestire l'accesso al database e la sicurezza degli account di accesso](sql-database-manage-logins.md).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-148">For more information on managing database access and logins, see [SQL Database security: Manage database access and login security](sql-database-manage-logins.md).</span></span>
* <span data-ttu-id="bd1e3-149">Per altre informazioni sugli utenti di database indipendente, vedere [Utenti di database indipendente: rendere portabile un database](https://msdn.microsoft.com/library/ff929188.aspx).</span><span class="sxs-lookup"><span data-stu-id="bd1e3-149">For more information on contained database users, see [Contained Database Users - Making Your Database Portable](https://msdn.microsoft.com/library/ff929188.aspx).</span></span>
* <span data-ttu-id="bd1e3-150">Per informazioni sull'uso e la configurazione della replica geografica attiva, vedere [Replica geografica attiva](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="bd1e3-150">For information about using and configuring active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md)</span></span>
* <span data-ttu-id="bd1e3-151">Per informazioni sull'uso del ripristino geografico, vedere l'argomento sul [ripristino geografico](sql-database-recovery-using-backups.md#geo-restore)</span><span class="sxs-lookup"><span data-stu-id="bd1e3-151">For information about using geo-restore, see [geo-restore](sql-database-recovery-using-backups.md#geo-restore)</span></span>

