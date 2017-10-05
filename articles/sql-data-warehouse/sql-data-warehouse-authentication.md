---
title: Autenticazione in Azure SQL Data Warehouse | Microsoft Docs
description: Autenticazione di Azure Active Directory (AAD) e SQL Server in Azure SQL Data Warehouse.
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
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="b2c6d-103">Autenticazione in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2c6d-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2c6d-104">Proteggere un database in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2c6d-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="b2c6d-105">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="b2c6d-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="b2c6d-106">Introduzione a Transparent Data Encryption (TDE) di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2c6d-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="b2c6d-107">Introduzione a Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="b2c6d-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="b2c6d-108">Per connettersi a SQL Data Warehouse è necessario passare le credenziali di sicurezza per scopi di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="b2c6d-109">Al momento di stabilire una connessione, alcune impostazioni di connessione sono configurate come parte della creazione della sessione di query.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="b2c6d-110">Per altre informazioni sulla sicurezza e sull'attivazione di connessioni al data warehouse, vedere l'articolo [Proteggere un database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="b2c6d-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="b2c6d-111">Autenticazione in SQL</span><span class="sxs-lookup"><span data-stu-id="b2c6d-111">SQL authentication</span></span>
<span data-ttu-id="b2c6d-112">Per connettersi a SQL Data Warehouse è necessario fornire le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2c6d-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="b2c6d-113">Nome del server completo</span><span class="sxs-lookup"><span data-stu-id="b2c6d-113">Fully qualified servername</span></span>
* <span data-ttu-id="b2c6d-114">Specificare l'autenticazione di SQL</span><span class="sxs-lookup"><span data-stu-id="b2c6d-114">Specify SQL authentication</span></span>
* <span data-ttu-id="b2c6d-115">Nome utente</span><span class="sxs-lookup"><span data-stu-id="b2c6d-115">Username</span></span>
* <span data-ttu-id="b2c6d-116">Password</span><span class="sxs-lookup"><span data-stu-id="b2c6d-116">Password</span></span>
* <span data-ttu-id="b2c6d-117">Database predefinito (facoltativo)</span><span class="sxs-lookup"><span data-stu-id="b2c6d-117">Default database (optional)</span></span>

<span data-ttu-id="b2c6d-118">Per impostazione predefinita la connessione si collega al database *master* e non al database utente.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="b2c6d-119">Per connettersi al database utente è possibile scegliere di effettuare una delle seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="b2c6d-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="b2c6d-120">Specificare il database predefinito per la registrazione del server con Esplora oggetti di SQL Server in SSDT, SSMS o nella stringa di connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="b2c6d-121">Ad esempio, includere il parametro InitialCatalog per una connessione ODBC.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="b2c6d-122">Selezionare il database utente prima di creare una sessione in SSDT.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="b2c6d-123">L'istruzione Transact-SQL **USE MyDatabase;** non è supportata per la modifica del database per una connessione.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="b2c6d-124">Per informazioni sulla connessione a SQL Data Warehouse con SSDT, fare riferimento all'articolo [Eseguire query con Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b2c6d-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="b2c6d-125">Autenticazione di Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="b2c6d-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="b2c6d-126">L'autenticazione di [Azure Active Directory][What is Azure Active Directory] è un meccanismo di connessione a SQL Data Warehouse di Microsoft Azure tramite le identità di Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b2c6d-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="b2c6d-127">Con l'autenticazione di Azure Active Directory è possibile gestire in una posizione centrale le identità degli utenti del database e altri servizi Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="b2c6d-128">La gestione centrale degli ID consente di gestire gli utenti di SQL Data Warehouse in un'unica posizione e semplifica la gestione delle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="b2c6d-129">Vantaggi</span><span class="sxs-lookup"><span data-stu-id="b2c6d-129">Benefits</span></span>
<span data-ttu-id="b2c6d-130">I vantaggi di Azure Active Directory includono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="b2c6d-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="b2c6d-131">Offre un'alternativa all'autenticazione di SQL Server.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="b2c6d-132">Contribuisce ad arrestare la proliferazione delle identità utente nei server di database.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="b2c6d-133">Consente la rotazione delle password in un'unica posizione.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="b2c6d-134">Consente di gestire le autorizzazioni del database tramite gruppi (AAD) esterni.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="b2c6d-135">Consente di eliminare l'archiviazione delle password abilitando l'autenticazione integrata di Windows e altre forme di autenticazione supportate da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="b2c6d-136">Usa gli utenti di database indipendente per autenticare le identità a livello di database.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="b2c6d-137">Supporta l'autenticazione basata su token per le applicazioni che si connettono a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="b2c6d-138">Supporta la Multi-Factor Authentication tramite l'autenticazione universale di Active Directory per SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="b2c6d-139">Per una descrizione di Multi-Factor Authentication, vedere [Il supporto SSMS per l'MFA di Azure Active Directory con database SQL e SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2c6d-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b2c6d-140">Azure Active Directory è ancora relativamente nuovo e presenta alcune limitazioni.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="b2c6d-141">Per assicurarsi che Azure Active Directory sia ideale per l'ambiente in uso, vedere [le funzionalità e le limitazioni di Azure AD][Azure AD features and limitations], in particolare le considerazioni aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="b2c6d-142">Procedura di configurazione</span><span class="sxs-lookup"><span data-stu-id="b2c6d-142">Configuration steps</span></span>
<span data-ttu-id="b2c6d-143">Seguire questa procedura per configurare l'autenticazione di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="b2c6d-144">Creare e popolare un'istanza di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b2c6d-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="b2c6d-145">Facoltativo: associare o modificare l'istanza di Active Directory attualmente associata alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="b2c6d-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="b2c6d-146">Creare un amministratore di Azure Active Directory per Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="b2c6d-147">Configurare i computer client</span><span class="sxs-lookup"><span data-stu-id="b2c6d-147">Configure your client computers</span></span>
5. <span data-ttu-id="b2c6d-148">Creare gli utenti di database indipendente nel database di cui è stato eseguito il mapping alle identità di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c6d-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="b2c6d-149">Connettersi al data warehouse usando le identità di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b2c6d-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="b2c6d-150">Gli utenti di Azure Active Directory non sono attualmente visualizzati in Esplora oggetti di SSDT.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="b2c6d-151">Come soluzione alternativa è possibile visualizzare gli utenti in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2c6d-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="b2c6d-152">Informazioni dettagliate</span><span class="sxs-lookup"><span data-stu-id="b2c6d-152">Find the details</span></span>
* <span data-ttu-id="b2c6d-153">La procedura per configurare e usare l'autenticazione di Azure Active Directory è quasi uguale per il database SQL di Azure e Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b2c6d-154">Seguire la procedura riportata nell'argomento [Connessione al database SQL oppure a SQL Data Warehouse con l'autenticazione di Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b2c6d-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="b2c6d-155">Creare ruoli di database personalizzati e aggiungere utenti ai ruoli.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="b2c6d-156">Concedere quindi autorizzazioni granulari ai ruoli.</span><span class="sxs-lookup"><span data-stu-id="b2c6d-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="b2c6d-157">Per altre informazioni, vedere [Introduzione alle autorizzazioni del motore di database](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="b2c6d-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2c6d-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b2c6d-158">Next steps</span></span>
<span data-ttu-id="b2c6d-159">Per iniziare a eseguire query sul data warehouse con Visual Studio e altre applicazioni, vedere [Eseguire query con Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="b2c6d-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
