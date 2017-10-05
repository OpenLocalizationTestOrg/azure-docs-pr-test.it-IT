---
title: Progettare il primo database SQL di Azure | Microsoft Docs
description: Informazioni su come progettare il primo database SQL di Azure.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop databases
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 08/03/2017
ms.author: carlrab
ms.openlocfilehash: 69cfffdae5ce2db53acc6d668dbe468c3ef22dc2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="b0252-103">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="b0252-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="b0252-104">Il database SQL di Azure è un database relazionale come servizio (DBaaS, Database-As-A-Service) disponibile in Microsoft Cloud ("Azure").</span><span class="sxs-lookup"><span data-stu-id="b0252-104">Azure SQL Database is a relational database-as-a service (DBaaS) in the Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="b0252-105">Questa esercitazione illustra come usare il portale di Azure e [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) per le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0252-105">In this tutorial, you learn how to use the Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b0252-106">Creare un database nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0252-106">Create a database in the Azure portal</span></span>
> * <span data-ttu-id="b0252-107">Impostare una regola del firewall a livello di server nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0252-107">Set up a server-level firewall rule in the Azure portal</span></span>
> * <span data-ttu-id="b0252-108">Connettersi al database con SSMS</span><span class="sxs-lookup"><span data-stu-id="b0252-108">Connect to the database with SSMS</span></span>
> * <span data-ttu-id="b0252-109">Creare tabelle con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b0252-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="b0252-110">Eseguire il caricamento bulk dei dati con BCP</span><span class="sxs-lookup"><span data-stu-id="b0252-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="b0252-111">Eseguire una query su quei dati con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b0252-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="b0252-112">Ripristinare il database a un [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b0252-112">Restore the database to a previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in the Azure portal</span></span>

<span data-ttu-id="b0252-113">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="b0252-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0252-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b0252-114">Prerequisites</span></span>

<span data-ttu-id="b0252-115">Per completare questa esercitazione, accertarsi di avere installato:</span><span class="sxs-lookup"><span data-stu-id="b0252-115">To complete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="b0252-116">La versione più recente di [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="b0252-116">The newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="b0252-117">La versione più recente di [BCP e SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="b0252-117">The newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="b0252-118">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-118">Log in to the Azure portal</span></span>

<span data-ttu-id="b0252-119">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b0252-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="b0252-120">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="b0252-120">Create a blank SQL database</span></span>

<span data-ttu-id="b0252-121">Un database SQL di Azure viene creato con un set definito di [risorse di calcolo e di archiviazione](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="b0252-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="b0252-122">Il database viene creato in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) e in un [server logico di database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="b0252-122">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="b0252-123">Per creare un database SQL vuoto, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="b0252-123">Follow these steps to create a blank SQL database.</span></span> 

1. <span data-ttu-id="b0252-124">Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-124">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="b0252-125">Selezionare **Database** nella pagina **Nuovo** e quindi **Database SQL** nella pagina **Database**.</span><span class="sxs-lookup"><span data-stu-id="b0252-125">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span> 

   ![creare database vuoto](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="b0252-127">Compilare il modulo Database SQL con le informazioni seguenti, come illustrato nell'immagine precedente:</span><span class="sxs-lookup"><span data-stu-id="b0252-127">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="b0252-128">Impostazione</span><span class="sxs-lookup"><span data-stu-id="b0252-128">Setting</span></span>       | <span data-ttu-id="b0252-129">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="b0252-129">Suggested value</span></span> | <span data-ttu-id="b0252-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0252-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="b0252-131">**Database name** (Nome database)</span><span class="sxs-lookup"><span data-stu-id="b0252-131">**Database name**</span></span> | <span data-ttu-id="b0252-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="b0252-132">mySampleDatabase</span></span> | <span data-ttu-id="b0252-133">Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="b0252-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="b0252-134">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="b0252-134">**Subscription**</span></span> | <span data-ttu-id="b0252-135">Sottoscrizione in uso</span><span class="sxs-lookup"><span data-stu-id="b0252-135">Your subscription</span></span>  | <span data-ttu-id="b0252-136">Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="b0252-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="b0252-137">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="b0252-137">**Resource group**</span></span> | <span data-ttu-id="b0252-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0252-138">myResourceGroup</span></span> | <span data-ttu-id="b0252-139">Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="b0252-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="b0252-140">**Select source** (Seleziona origine)</span><span class="sxs-lookup"><span data-stu-id="b0252-140">**Select source**</span></span> | <span data-ttu-id="b0252-141">Database vuoto</span><span class="sxs-lookup"><span data-stu-id="b0252-141">Blank database</span></span> | <span data-ttu-id="b0252-142">Indica che deve essere creato un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="b0252-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="b0252-143">Fare clic su **Server** per creare e configurare un nuovo server per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="b0252-143">Click **Server** to create and configure a new server for your new database.</span></span> <span data-ttu-id="b0252-144">Compilare il **modulo del nuovo server** con le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0252-144">Fill out the **New server form** with the following information:</span></span> 

   | <span data-ttu-id="b0252-145">Impostazione</span><span class="sxs-lookup"><span data-stu-id="b0252-145">Setting</span></span>       | <span data-ttu-id="b0252-146">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="b0252-146">Suggested value</span></span> | <span data-ttu-id="b0252-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0252-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="b0252-148">**Server name** (Nome server)</span><span class="sxs-lookup"><span data-stu-id="b0252-148">**Server name**</span></span> | <span data-ttu-id="b0252-149">Qualsiasi nome globalmente univoco</span><span class="sxs-lookup"><span data-stu-id="b0252-149">Any globally unique name</span></span> | <span data-ttu-id="b0252-150">Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="b0252-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="b0252-151">**Nome di accesso amministratore server**</span><span class="sxs-lookup"><span data-stu-id="b0252-151">**Server admin login**</span></span> | <span data-ttu-id="b0252-152">Qualsiasi nome valido</span><span class="sxs-lookup"><span data-stu-id="b0252-152">Any valid name</span></span> | <span data-ttu-id="b0252-153">Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="b0252-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="b0252-154">**Password**</span><span class="sxs-lookup"><span data-stu-id="b0252-154">**Password**</span></span> | <span data-ttu-id="b0252-155">Qualsiasi password valida</span><span class="sxs-lookup"><span data-stu-id="b0252-155">Any valid password</span></span> | <span data-ttu-id="b0252-156">La password deve almeno 8 caratteri e contenere caratteri inclusi in tre delle categorie seguenti: caratteri maiuscoli, caratteri minuscoli, numeri e caratteri non alfanumerici.</span><span class="sxs-lookup"><span data-stu-id="b0252-156">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="b0252-157">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="b0252-157">**Location**</span></span> | <span data-ttu-id="b0252-158">Qualsiasi località valida</span><span class="sxs-lookup"><span data-stu-id="b0252-158">Any valid location</span></span> | <span data-ttu-id="b0252-159">Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="b0252-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![Creare il server di database](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="b0252-161">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="b0252-161">Click **Select**.</span></span>

6. <span data-ttu-id="b0252-162">Fare clic su **Piano tariffario** per specificare il livello di servizio e il livello delle prestazioni per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="b0252-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="b0252-163">Per esercitazione selezionare **20 DTU** e **250** GB di memoria.</span><span class="sxs-lookup"><span data-stu-id="b0252-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![Creare il database s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="b0252-165">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b0252-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="b0252-166">Selezionare **regole di confronto** per il database vuoto. Per questa esercitazione usare il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="b0252-166">Select a **collation** for the blank database (for this tutorial, use the default value).</span></span> <span data-ttu-id="b0252-167">Per altre informazioni sulle regole di confronto, vedere [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations) (Regole di confronto)</span><span class="sxs-lookup"><span data-stu-id="b0252-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="b0252-168">Fare clic su **Crea** per effettuare il provisioning del database.</span><span class="sxs-lookup"><span data-stu-id="b0252-168">Click **Create** to provision the database.</span></span> <span data-ttu-id="b0252-169">Il provisioning richiede circa un minuto e mezzo per il completamento.</span><span class="sxs-lookup"><span data-stu-id="b0252-169">Provisioning takes about a minute and a half to complete.</span></span> 

10. <span data-ttu-id="b0252-170">Sulla barra degli strumenti fare clic su **Notifiche** per monitorare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b0252-170">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![notifica](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="b0252-172">Creare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="b0252-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="b0252-173">Il servizio di database SQL crea un firewall a livello di server che impedisce alle applicazioni e agli strumenti esterni di connettersi al server o ai database sul server a meno che non venga creata una regola del firewall per aprire il firewall per indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="b0252-173">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="b0252-174">Seguire questi passaggi per creare una [regola del firewall a livello di server di database SQL](sql-database-firewall-configure.md) per l'indirizzo IP del client e abilitare la connettività esterna tramite il firewall del database SQL solo per il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="b0252-174">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="b0252-175">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="b0252-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="b0252-176">Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 1433 potrebbe non essere autorizzato dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="b0252-176">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="b0252-177">In questo caso, non è possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="b0252-177">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="b0252-178">Al termine della distribuzione, scegliere **Database SQL** dal menu a sinistra e fare clic su **mySampleDatabase** nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="b0252-178">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="b0252-179">Si apre la pagina di panoramica per il database, in cui è indicato il nome completo del server (ad esempio, **mynewserver20170313.database.windows.net**) e in cui sono disponibili altre opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="b0252-179">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="b0252-180">Copiare il nome completo del server per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="b0252-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b0252-181">Questo nome completo del server è necessario per connettersi al server e ai relativi database nelle guide introduttive successive.</span><span class="sxs-lookup"><span data-stu-id="b0252-181">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![Nome del server](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="b0252-183">Fare clic su **Imposta firewall server** sulla barra degli strumenti, come illustrato nell'immagine precedente.</span><span class="sxs-lookup"><span data-stu-id="b0252-183">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="b0252-184">Si apre la pagina **Impostazioni del firewall** per il server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="b0252-184">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="b0252-186">Fare clic su **Aggiungi IP client** sulla barra degli strumenti per aggiungere l'indirizzo IP corrente a una nuova regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="b0252-186">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="b0252-187">Una regola del firewall può aprire la porta 1433 per un indirizzo IP singolo o un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="b0252-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="b0252-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b0252-188">Click **Save**.</span></span> <span data-ttu-id="b0252-189">Viene creata una regola del firewall a livello di server per l'indirizzo IP corrente, che apre la porta 1433 nel server logico.</span><span class="sxs-lookup"><span data-stu-id="b0252-189">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![Impostare la regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="b0252-191">Fare clic su **OK** e quindi chiudere la pagina **Impostazioni del firewall**.</span><span class="sxs-lookup"><span data-stu-id="b0252-191">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="b0252-192">È ora possibile connettersi al server del database SQL e ai relativi database usando SQL Server Management Studio o un altro strumento di propria scelta da questo indirizzo IP, con l'account amministratore del server creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b0252-192">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0252-193">Per impostazione predefinita, l'accesso attraverso il firewall del database SQL è abilitato per tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-193">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="b0252-194">Selezionando **NO** in questa pagina permette di disabilitare tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-194">Click **OFF** on this page to disable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="b0252-195">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="b0252-195">SQL server connection information</span></span>

<span data-ttu-id="b0252-196">Ottenere il nome completo del server per il server del database SQL di Azure nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-196">Get the fully qualified server name for your Azure SQL Database server in the Azure portal.</span></span> <span data-ttu-id="b0252-197">Usare il nome completo del server per connettersi al server tramite SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b0252-197">You use the fully qualified server name to connect to your server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="b0252-198">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b0252-198">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b0252-199">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="b0252-199">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="b0252-200">Nel riquadro **Informazioni di base** della pagina del portale di Azure per il database individuare e quindi copiare il **Nome server**.</span><span class="sxs-lookup"><span data-stu-id="b0252-200">In the **Essentials** pane in the Azure portal page for your database, locate and then copy the **Server name**.</span></span>

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-to-the-database-with-ssms"></a><span data-ttu-id="b0252-202">Connettersi al database con SSMS</span><span class="sxs-lookup"><span data-stu-id="b0252-202">Connect to the database with SSMS</span></span>

<span data-ttu-id="b0252-203">Usare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) per stabilire una connessione al server del database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b0252-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) to establish a connection to your Azure SQL Database server.</span></span>

1. <span data-ttu-id="b0252-204">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="b0252-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="b0252-205">Nella finestra di dialogo **Connetti al server** immettere le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="b0252-205">In the **Connect to Server** dialog box, enter the following information:</span></span>

   | <span data-ttu-id="b0252-206">Impostazione</span><span class="sxs-lookup"><span data-stu-id="b0252-206">Setting</span></span>       | <span data-ttu-id="b0252-207">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="b0252-207">Suggested value</span></span> | <span data-ttu-id="b0252-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b0252-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="b0252-209">Tipo di server</span><span class="sxs-lookup"><span data-stu-id="b0252-209">Server type</span></span> | <span data-ttu-id="b0252-210">Motore di database</span><span class="sxs-lookup"><span data-stu-id="b0252-210">Database engine</span></span> | <span data-ttu-id="b0252-211">Questo valore è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="b0252-211">This value is required</span></span> |
   | <span data-ttu-id="b0252-212">Nome server</span><span class="sxs-lookup"><span data-stu-id="b0252-212">Server name</span></span> | <span data-ttu-id="b0252-213">Nome completo del server</span><span class="sxs-lookup"><span data-stu-id="b0252-213">The fully qualified server name</span></span> | <span data-ttu-id="b0252-214">Il nome sarà simile a: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="b0252-214">The name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="b0252-215">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="b0252-215">Authentication</span></span> | <span data-ttu-id="b0252-216">Autenticazione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="b0252-216">SQL Server Authentication</span></span> | <span data-ttu-id="b0252-217">L'autenticazione SQL è il solo tipo di autenticazione configurato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b0252-217">SQL Authentication is the only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="b0252-218">Login</span><span class="sxs-lookup"><span data-stu-id="b0252-218">Login</span></span> | <span data-ttu-id="b0252-219">Account amministratore del server</span><span class="sxs-lookup"><span data-stu-id="b0252-219">The server admin account</span></span> | <span data-ttu-id="b0252-220">Si tratta dell'account specificato quando è stato creato il server.</span><span class="sxs-lookup"><span data-stu-id="b0252-220">This is the account that you specified when you created the server.</span></span> |
   | <span data-ttu-id="b0252-221">Password</span><span class="sxs-lookup"><span data-stu-id="b0252-221">Password</span></span> | <span data-ttu-id="b0252-222">Password per l'account amministratore del server</span><span class="sxs-lookup"><span data-stu-id="b0252-222">The password for your server admin account</span></span> | <span data-ttu-id="b0252-223">Si tratta della password specificata quando è stato creato il server.</span><span class="sxs-lookup"><span data-stu-id="b0252-223">This is the password that you specified when you created the server.</span></span> |

   ![connetti al server](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="b0252-225">Fare clic su **Opzioni** nella finestra di dialogo **Connetti al server**.</span><span class="sxs-lookup"><span data-stu-id="b0252-225">Click **Options** in the **Connect to server** dialog box.</span></span> <span data-ttu-id="b0252-226">Nella sezione **Connetti al database** immettere **mySampleDatabase** per connettersi a tale database.</span><span class="sxs-lookup"><span data-stu-id="b0252-226">In the **Connect to database** section, enter **mySampleDatabase** to connect to this database.</span></span>

   ![connettersi al database nel server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="b0252-228">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="b0252-228">Click **Connect**.</span></span> <span data-ttu-id="b0252-229">La finestra Esplora oggetti viene visualizzata in SSMS.</span><span class="sxs-lookup"><span data-stu-id="b0252-229">The Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="b0252-230">In Esplora oggetti espandere **Database** e quindi espandere **mySampleDatabase** per visualizzare gli oggetti disponibili nel database di esempio.</span><span class="sxs-lookup"><span data-stu-id="b0252-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** to view the objects in the sample database.</span></span>

   ![oggetti di database](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-the-database"></a><span data-ttu-id="b0252-232">Creare tabelle nel database</span><span class="sxs-lookup"><span data-stu-id="b0252-232">Create tables in the database</span></span> 

<span data-ttu-id="b0252-233">Creare uno schema di database con quattro tabelle che modellano un sistema di gestione degli studenti per le università tramite [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="b0252-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="b0252-234">Person</span><span class="sxs-lookup"><span data-stu-id="b0252-234">Person</span></span>
- <span data-ttu-id="b0252-235">Corso</span><span class="sxs-lookup"><span data-stu-id="b0252-235">Course</span></span>
- <span data-ttu-id="b0252-236">Studente</span><span class="sxs-lookup"><span data-stu-id="b0252-236">Student</span></span>
- <span data-ttu-id="b0252-237">Accreditare quel modello come un sistema di gestione degli studenti per le università</span><span class="sxs-lookup"><span data-stu-id="b0252-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="b0252-238">Nel diagramma seguente viene illustrato come queste tabelle sono correlate tra loro.</span><span class="sxs-lookup"><span data-stu-id="b0252-238">The following diagram shows how these tables are related to each other.</span></span> <span data-ttu-id="b0252-239">Alcune di queste tabelle fanno riferimento a delle colonne in altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="b0252-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="b0252-240">Ad esempio, la tabella Student fa riferimento alla colonna **PersonId** della tabella **Person**.</span><span class="sxs-lookup"><span data-stu-id="b0252-240">For example, the Student table references the **PersonId** column of the **Person** table.</span></span> <span data-ttu-id="b0252-241">Studiare il diagramma per comprendere come sono correlate tra loro le tabelle in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b0252-241">Study the diagram to understand how the tables in this tutorial are related to one another.</span></span> <span data-ttu-id="b0252-242">Per un esame approfondito su come creare tabelle di database efficaci, vedere [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx) (Creare tabelle di database efficaci).</span><span class="sxs-lookup"><span data-stu-id="b0252-242">For an in-depth look at how to create effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="b0252-243">Per informazioni sulla scelta dei tipi di dati, vedere [Tipi di dati](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="b0252-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="b0252-244">È anche possibile usare la [Progettazione delle tabelle in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) per creare e progettare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="b0252-244">You can also use the [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) to create and design your tables.</span></span> 

![Relazioni tra tabelle](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="b0252-246">In Esplora oggetti fare clic con il pulsante destro del mouse su **mySampleDatabase** e scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="b0252-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="b0252-247">Viene visualizzata una finestra di query vuota, connessa al database.</span><span class="sxs-lookup"><span data-stu-id="b0252-247">A blank query window opens that is connected to your database.</span></span>

2. <span data-ttu-id="b0252-248">Nella finestra di query, eseguire la query seguente per creare quattro tabelle nel database:</span><span class="sxs-lookup"><span data-stu-id="b0252-248">In the query window, execute the following query to create four tables in your database:</span></span> 

   ```sql 
   -- Create Person table

   CREATE TABLE Person
   (
   PersonId   INT IDENTITY PRIMARY KEY,
   FirstName   NVARCHAR(128) NOT NULL,
   MiddelInitial NVARCHAR(10),
   LastName   NVARCHAR(128) NOT NULL,
   DateOfBirth   DATE NOT NULL
   )
   
   -- Create Student table
 
   CREATE TABLE Student
   (
   StudentId INT IDENTITY PRIMARY KEY,
   PersonId  INT REFERENCES Person (PersonId),
   Email   NVARCHAR(256)
   )
   
   -- Create Course table
 
   CREATE TABLE Course
   (
   CourseId  INT IDENTITY PRIMARY KEY,
   Name   NVARCHAR(50) NOT NULL,
   Teacher   NVARCHAR(256) NOT NULL
   ) 

   -- Create Credit table
 
   CREATE TABLE Credit
   (
   StudentId   INT REFERENCES Student (StudentId),
   CourseId   INT REFERENCES Course (CourseId),
   Grade   DECIMAL(5,2) CHECK (Grade <= 100.00),
   Attempt   TINYINT,
   CONSTRAINT  [UQ_studentgrades] UNIQUE CLUSTERED
   (
   StudentId, CourseId, Grade, Attempt
   )
   )
   ```

   ![Creare tabelle](./media/sql-database-design-first-database/create-tables.png)

3. <span data-ttu-id="b0252-250">Espandere il nodo "tabelle" in SQL Server Management Studio Object Explorer per visualizzare le tabelle create.</span><span class="sxs-lookup"><span data-stu-id="b0252-250">Expand the 'tables' node in the SQL Server Management Studio Object explorer to see the tables you created.</span></span>

   ![tabelle create con SQL Server Management Studio](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-the-tables"></a><span data-ttu-id="b0252-252">Caricare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="b0252-252">Load data into the tables</span></span>

1. <span data-ttu-id="b0252-253">Creare una cartella denominata **SampleTableData** nella cartella download per archiviare i dati di esempio per il database.</span><span class="sxs-lookup"><span data-stu-id="b0252-253">Create a folder called **SampleTableData** in your Downloads folder to store sample data for your database.</span></span> 

2. <span data-ttu-id="b0252-254">Fare doppio clic sui seguenti collegamenti e salvarli nella cartella **SampleTableData**.</span><span class="sxs-lookup"><span data-stu-id="b0252-254">Right-click the following links and save them into the **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="b0252-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="b0252-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="b0252-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="b0252-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="b0252-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="b0252-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="b0252-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="b0252-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="b0252-259">Aprire una finestra del prompt dei comandi e passare alla cartella SampleTableData.</span><span class="sxs-lookup"><span data-stu-id="b0252-259">Open a command prompt window and navigate to the SampleTableData folder.</span></span>

4. <span data-ttu-id="b0252-260">Eseguire i comandi seguenti per inserire dei dati di esempio nelle tabelle sostituendo i valori per **ServerName**, **DatabaseName**, **UserName** e **Password** con i valori dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="b0252-260">Execute the following commands to insert sample data into the tables replacing the values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with the values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="b0252-261">A questo punto, sono stati caricati i dati di esempio nelle tabelle create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b0252-261">You have now loaded sample data into the tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="b0252-262">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="b0252-262">Query data</span></span>

<span data-ttu-id="b0252-263">Eseguire le query seguenti per recuperare informazioni dalle tabelle del database.</span><span class="sxs-lookup"><span data-stu-id="b0252-263">Execute the following queries to retrieve information from the database tables.</span></span> <span data-ttu-id="b0252-264">Vedere [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) (Scrittura di query SQL) per altre informazioni sulla scrittura di query SQL.</span><span class="sxs-lookup"><span data-stu-id="b0252-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) to learn more about writing SQL queries.</span></span> <span data-ttu-id="b0252-265">La prima query unisce tutte e quattro le tabelle per trovare tutti gli studenti a cui ha insegnato "Dominick Pope" che hanno un livello superiore al 75% nella sua classe.</span><span class="sxs-lookup"><span data-stu-id="b0252-265">The first query joins all four tables to find all the students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="b0252-266">La seconda query unisce tutte e quattro le tabelle e trova tutti i corsi in cui si è registrato "Noe Coleman".</span><span class="sxs-lookup"><span data-stu-id="b0252-266">The second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="b0252-267">In una finestra di query di SQL Server Management Studio, eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="b0252-267">In a SQL Server Management Studio query window, execute the following query:</span></span>

   ```sql 
   -- Find the students taught by Dominick Pope who have a grade higher than 75%

   SELECT  person.FirstName,
   person.LastName,
   course.Name,
   credit.Grade
   FROM  Person AS person
   INNER JOIN Student AS student ON person.PersonId = student.PersonId
   INNER JOIN Credit AS credit ON student.StudentId = credit.StudentId
   INNER JOIN Course AS course ON credit.CourseId = course.courseId
   WHERE course.Teacher = 'Dominick Pope' 
   AND Grade > 75
   ```

2. <span data-ttu-id="b0252-268">In una finestra di query di SQL Server Management Studio, eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="b0252-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all the courses in which Noe Coleman has ever enrolled

   SELECT  course.Name,
   course.Teacher,
   credit.Grade
   FROM  Course AS course
   INNER JOIN Credit AS credit ON credit.CourseId = course.CourseId
   INNER JOIN Student AS student ON student.StudentId = credit.StudentId
   INNER JOIN Person AS person ON person.PersonId = student.PersonId
   WHERE person.FirstName = 'Noe'
   AND person.LastName = 'Coleman'
   ```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="b0252-269">Ripristinare un database a un momento precedente</span><span class="sxs-lookup"><span data-stu-id="b0252-269">Restore a database to a previous point in time</span></span>

<span data-ttu-id="b0252-270">Si supponga di aver eliminato accidentalmente una tabella.</span><span class="sxs-lookup"><span data-stu-id="b0252-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="b0252-271">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="b0252-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="b0252-272">Il Database SQL di Azure consente di tornare in qualsiasi punto degli ultimi 35 giorni e di ripristinare questo punto nel tempo in un nuovo database.</span><span class="sxs-lookup"><span data-stu-id="b0252-272">Azure SQL Database allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new database.</span></span> <span data-ttu-id="b0252-273">È possibile usare questo database per ripristinare i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="b0252-273">You can you this database to recover your deleted data.</span></span> <span data-ttu-id="b0252-274">La procedura seguente consente di ripristinare il database di esempio in un punto precedente all'aggiunta delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="b0252-274">The following steps restore the sample database to a point before the tables were added.</span></span>

1. <span data-ttu-id="b0252-275">Nella pagina Database SQL del database fare clic su **Ripristina** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="b0252-275">On the SQL Database page for your database, click **Restore** on the toolbar.</span></span> <span data-ttu-id="b0252-276">Si apre la pagina **Ripristina** .</span><span class="sxs-lookup"><span data-stu-id="b0252-276">The **Restore** page opens.</span></span>

   ![ripristinare](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="b0252-278">Compilare il modulo **Ripristina** con le informazioni obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="b0252-278">Fill out the **Restore** form with the required information:</span></span>
    * <span data-ttu-id="b0252-279">Nome database: specificare un nome per il database</span><span class="sxs-lookup"><span data-stu-id="b0252-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="b0252-280">Temporizzato: Selezionare la scheda **Temporizzato** del modulo Ripristino</span><span class="sxs-lookup"><span data-stu-id="b0252-280">Point-in-time: Select the **Point-in-time** tab on the Restore form</span></span> 
    * <span data-ttu-id="b0252-281">Punto di ripristino: selezionare un punto nel tempo precedente alla modifica del database</span><span class="sxs-lookup"><span data-stu-id="b0252-281">Restore point: Select a time that occurs before the database was changed</span></span>
    * <span data-ttu-id="b0252-282">Server di destinazione: non è possibile modificare questo valore quando si ripristina un database</span><span class="sxs-lookup"><span data-stu-id="b0252-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="b0252-283">Pool di database elastici: selezionare **Nessuno**</span><span class="sxs-lookup"><span data-stu-id="b0252-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="b0252-284">Piano tariffario: selezionare **20 DTUs** (20 DTU) e **250 GB** di memoria.</span><span class="sxs-lookup"><span data-stu-id="b0252-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![punto di ripristino](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="b0252-286">Fare clic su **OK** per ripristinare il database da ripristinare [ in un punto nel tempo ](sql-database-recovery-using-backups.md#point-in-time-restore) precedente all'aggiunta delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="b0252-286">Click **OK** to restore the database to [restore to a point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before the tables were added.</span></span> <span data-ttu-id="b0252-287">Il ripristino di un database in un altro punto nel tempo crea un duplicato del database nello stesso server del database originale nel punto nel tempo specificato, a condizione che si trovi nell'ambito del periodo di conservazione per il [livello di servizio](sql-database-service-tiers.md) applicato.</span><span class="sxs-lookup"><span data-stu-id="b0252-287">Restoring a database to a different point in time creates a duplicate database in the same server as the original database as of the point in time you specify, as long as it is within the retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0252-288">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b0252-288">Next Steps</span></span> 
<span data-ttu-id="b0252-289">Questa esercitazione ha illustrato le attività di base che è possibile eseguire con i database, come creare database e tabelle, caricare dati, eseguire query sui dati e ripristinare un database a un momento precedente.</span><span class="sxs-lookup"><span data-stu-id="b0252-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore the database to a previous point in time.</span></span> <span data-ttu-id="b0252-290">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="b0252-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b0252-291">Creare un database</span><span class="sxs-lookup"><span data-stu-id="b0252-291">Create a database</span></span>
> * <span data-ttu-id="b0252-292">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="b0252-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="b0252-293">Connettersi al database con [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="b0252-293">Connect to the database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="b0252-294">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="b0252-294">Create tables</span></span>
> * <span data-ttu-id="b0252-295">Eseguire il caricamento bulk dei dati</span><span class="sxs-lookup"><span data-stu-id="b0252-295">Bulk load data</span></span>
> * <span data-ttu-id="b0252-296">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="b0252-296">Query that data</span></span>
> * <span data-ttu-id="b0252-297">Ripristinare il database a un momento precedente usando le funzionalità di [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) del database SQL</span><span class="sxs-lookup"><span data-stu-id="b0252-297">Restore the database to a previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="b0252-298">Per informazioni sulla progettazione di un database con Visual Studio e C#, passare all'esercitazione successiva.</span><span class="sxs-lookup"><span data-stu-id="b0252-298">Advance to the next tutorial to learn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="b0252-299">Progettare un database SQL di Azure e connettersi con C# e ADO.NET</span><span class="sxs-lookup"><span data-stu-id="b0252-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
