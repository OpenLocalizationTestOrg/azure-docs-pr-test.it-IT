---
title: aaaAuthentication tooAzure SQL Data Warehouse | Documenti Microsoft
description: Azure Active Directory (AAD) e SQL Server authentication tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="e244b-103">TooAzure l'autenticazione SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e244b-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e244b-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e244b-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="e244b-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="e244b-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="e244b-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e244b-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="e244b-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="e244b-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="e244b-108">tooconnect tooSQL Data Warehouse, è necessario passare le credenziali di sicurezza per l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="e244b-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="e244b-109">Al momento di stabilire una connessione, alcune impostazioni di connessione sono configurate come parte della creazione della sessione di query.</span><span class="sxs-lookup"><span data-stu-id="e244b-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="e244b-110">Per ulteriori informazioni sulla sicurezza e come data warehouse di tooenable connessioni tooyour, vedere [proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="e244b-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="e244b-111">Autenticazione in SQL</span><span class="sxs-lookup"><span data-stu-id="e244b-111">SQL authentication</span></span>
<span data-ttu-id="e244b-112">tooconnect tooSQL Data Warehouse, è necessario fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="e244b-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="e244b-113">Nome del server completo</span><span class="sxs-lookup"><span data-stu-id="e244b-113">Fully qualified servername</span></span>
* <span data-ttu-id="e244b-114">Specificare l'autenticazione di SQL</span><span class="sxs-lookup"><span data-stu-id="e244b-114">Specify SQL authentication</span></span>
* <span data-ttu-id="e244b-115">Nome utente</span><span class="sxs-lookup"><span data-stu-id="e244b-115">Username</span></span>
* <span data-ttu-id="e244b-116">Password</span><span class="sxs-lookup"><span data-stu-id="e244b-116">Password</span></span>
* <span data-ttu-id="e244b-117">Database predefinito (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="e244b-117">Default database (optional)</span></span>

<span data-ttu-id="e244b-118">Per impostazione predefinita, la connessione si connette toohello *master* database e non il database utente.</span><span class="sxs-lookup"><span data-stu-id="e244b-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="e244b-119">tooconnect tooyour i database utente, è possibile scegliere toodo una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="e244b-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="e244b-120">Specificare il database predefinito hello durante la registrazione del server con Esplora oggetti di SQL Server in SSDT, SQL Server Management Studio, o nella stringa di connessione dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e244b-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="e244b-121">Ad esempio, includere il parametro InitialCatalog hello per una connessione ODBC.</span><span class="sxs-lookup"><span data-stu-id="e244b-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="e244b-122">Evidenziare i database utente hello prima di creare una sessione in SSDT.</span><span class="sxs-lookup"><span data-stu-id="e244b-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="e244b-123">istruzione Transact-SQL Hello **utilizzare MyDatabase;** non è supportata per la modifica hello database per una connessione.</span><span class="sxs-lookup"><span data-stu-id="e244b-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="e244b-124">Per informazioni di connessione tooSQL Data Warehouse con SSDT, vedere l'articolo toohello [Query con Visual Studio] [ Query with Visual Studio] articolo.</span><span class="sxs-lookup"><span data-stu-id="e244b-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="e244b-125">Autenticazione di Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="e244b-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="e244b-126">[Azure Active Directory] [ What is Azure Active Directory] l'autenticazione è un meccanismo di connessione tooMicrosoft Azure SQL Data Warehouse usando le identità in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e244b-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="e244b-127">Con l'autenticazione di Azure Active Directory, è possibile gestire centralmente le identità hello di utenti del database e altri servizi Microsoft in un'unica posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="e244b-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="e244b-128">Gestione degli ID centrale fornisce un'unica posizione toomanage agli utenti di SQL Data Warehouse e semplifica la gestione delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="e244b-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="e244b-129">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="e244b-129">Benefits</span></span>
<span data-ttu-id="e244b-130">I vantaggi di Azure Active Directory includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="e244b-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="e244b-131">Fornisce l'autenticazione Server tooSQL alternativo.</span><span class="sxs-lookup"><span data-stu-id="e244b-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="e244b-132">Consente di arrestare la proliferazione di hello delle identità tra server di database.</span><span class="sxs-lookup"><span data-stu-id="e244b-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="e244b-133">Consente la rotazione delle password in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="e244b-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="e244b-134">Consente di gestire le autorizzazioni del database tramite gruppi (AAD) esterni.</span><span class="sxs-lookup"><span data-stu-id="e244b-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="e244b-135">Consente di eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e244b-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="e244b-136">Usa contenuti identità tooauthenticate utenti di database a livello di database hello.</span><span class="sxs-lookup"><span data-stu-id="e244b-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="e244b-137">Supporta l'autenticazione basata su token per applicazioni che si connettono tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e244b-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="e244b-138">Supporta la Multi-Factor Authentication tramite l'autenticazione universale di Active Directory per SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="e244b-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="e244b-139">Per una descrizione di Multi-Factor Authentication, vedere [Il supporto SSMS per l'MFA di Azure Active Directory con database SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e244b-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e244b-140">Azure Active Directory è ancora relativamente nuovo e presenta alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="e244b-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="e244b-141">tooensure che Azure Active Directory è una scelta ottimale per l'ambiente, vedere [funzionalità Azure AD e limitazioni][Azure AD features and limitations], in particolare hello considerazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="e244b-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="e244b-142">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="e244b-142">Configuration steps</span></span>
<span data-ttu-id="e244b-143">Seguire questi passaggi tooconfigure Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="e244b-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="e244b-144">Creare e popolare un'istanza di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e244b-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="e244b-145">Facoltativo: Associare o modificare hello active directory a cui è attualmente associato alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="e244b-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="e244b-146">Creare un amministratore di Azure Active Directory per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e244b-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="e244b-147">Configurare i computer client</span><span class="sxs-lookup"><span data-stu-id="e244b-147">Configure your client computers</span></span>
5. <span data-ttu-id="e244b-148">Creare utenti del database indipendente in tooAzure del database eseguito il mapping delle identità di Active Directory</span><span class="sxs-lookup"><span data-stu-id="e244b-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="e244b-149">La connessione di data warehouse di tooyour usando le identità di Azure AD</span><span class="sxs-lookup"><span data-stu-id="e244b-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="e244b-150">Gli utenti di Azure Active Directory non sono attualmente visualizzati in Esplora oggetti di SSDT.</span><span class="sxs-lookup"><span data-stu-id="e244b-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="e244b-151">In alternativa, consente di visualizzare gli utenti di hello [Sys. database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="e244b-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="e244b-152">Trovare i dettagli di hello</span><span class="sxs-lookup"><span data-stu-id="e244b-152">Find hello details</span></span>
* <span data-ttu-id="e244b-153">Hello passaggi tooconfigure usare Azure Active Directory l'autenticazione e sono quasi identici per Database SQL di Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e244b-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e244b-154">Seguire passaggi nell'argomento hello dettagliati di hello [tooSQL connessione Database o Data Warehouse da usando Azure Active Directory l'autenticazione di SQL](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e244b-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="e244b-155">Creare ruoli personalizzati del database e aggiungere utenti toohello ruoli.</span><span class="sxs-lookup"><span data-stu-id="e244b-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="e244b-156">Concedere quindi autorizzazioni granulari toohello ruoli.</span><span class="sxs-lookup"><span data-stu-id="e244b-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="e244b-157">Per altre informazioni, vedere [Introduzione alle autorizzazioni del motore di database](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="e244b-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e244b-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e244b-158">Next steps</span></span>
<span data-ttu-id="e244b-159">toostart l'esecuzione di query del data warehouse con Visual Studio e altre applicazioni, vedere [Query con Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="e244b-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
