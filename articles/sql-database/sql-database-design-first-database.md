---
title: aaaDesign di un database SQL di Azure | Documenti Microsoft
description: Informazioni su toodesign di un database SQL di Azure.
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
ms.openlocfilehash: 65f0a1594cbdda7480abf32a847266a073e7560d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-sql-database"></a><span data-ttu-id="3c973-103">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="3c973-103">Design your first Azure SQL database</span></span>

<span data-ttu-id="3c973-104">Database SQL di Azure è un relazionale database-come a un servizio (DBaaS) in hello Cloud Microsoft ("Azure").</span><span class="sxs-lookup"><span data-stu-id="3c973-104">Azure SQL Database is a relational database-as-a service (DBaaS) in hello Microsoft Cloud ("Azure").</span></span> <span data-ttu-id="3c973-105">In questa esercitazione, è illustrato come toouse hello portale di Azure e [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) per:</span><span class="sxs-lookup"><span data-stu-id="3c973-105">In this tutorial, you learn how toouse hello Azure portal and [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS) to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="3c973-106">Creare un database in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c973-106">Create a database in hello Azure portal</span></span>
> * <span data-ttu-id="3c973-107">Impostare una regola firewall di livello server nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="3c973-107">Set up a server-level firewall rule in hello Azure portal</span></span>
> * <span data-ttu-id="3c973-108">La connessione a database toohello con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3c973-108">Connect toohello database with SSMS</span></span>
> * <span data-ttu-id="3c973-109">Creare tabelle con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3c973-109">Create tables with SSMS</span></span>
> * <span data-ttu-id="3c973-110">Eseguire il caricamento bulk dei dati con BCP</span><span class="sxs-lookup"><span data-stu-id="3c973-110">Bulk load data with BCP</span></span>
> * <span data-ttu-id="3c973-111">Eseguire una query su quei dati con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3c973-111">Query that data with SSMS</span></span>
> * <span data-ttu-id="3c973-112">Ripristinare tooa database hello precedente [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c973-112">Restore hello database tooa previous [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) in hello Azure portal</span></span>

<span data-ttu-id="3c973-113">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="3c973-113">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c973-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="3c973-114">Prerequisites</span></span>

<span data-ttu-id="3c973-115">toocomplete questa esercitazione, verificare che è stato installato:</span><span class="sxs-lookup"><span data-stu-id="3c973-115">toocomplete this tutorial, make sure you have installed:</span></span>
- <span data-ttu-id="3c973-116">versione più recente di Hello di [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span><span class="sxs-lookup"><span data-stu-id="3c973-116">hello newest version of [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS).</span></span>
- <span data-ttu-id="3c973-117">versione più recente di Hello di [BCP e SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span><span class="sxs-lookup"><span data-stu-id="3c973-117">hello newest version of [BCP and SQLCMD](https://www.microsoft.com/download/details.aspx?id=36433).</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="3c973-118">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="3c973-118">Log in toohello Azure portal</span></span>

<span data-ttu-id="3c973-119">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c973-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="3c973-120">Creare un database SQL vuoto</span><span class="sxs-lookup"><span data-stu-id="3c973-120">Create a blank SQL database</span></span>

<span data-ttu-id="3c973-121">Un database SQL di Azure viene creato con un set definito di [risorse di calcolo e di archiviazione](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3c973-121">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="3c973-122">Hello database viene creato all'interno di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) e in un [server logico di Database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="3c973-122">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="3c973-123">Seguire questi toocreate passaggi un database SQL vuoto.</span><span class="sxs-lookup"><span data-stu-id="3c973-123">Follow these steps toocreate a blank SQL database.</span></span> 

1. <span data-ttu-id="3c973-124">Fare clic su hello **New** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-124">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="3c973-125">Selezionare **database** da hello **New** pagina e selezionare **Database SQL** da hello **database** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c973-125">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span> 

   ![creare database vuoto](./media/sql-database-design-first-database/create-empty-database.png)

3. <span data-ttu-id="3c973-127">Compilare il modulo di Database SQL hello con hello le seguenti informazioni, come mostrato nella precedente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="3c973-127">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="3c973-128">Impostazione</span><span class="sxs-lookup"><span data-stu-id="3c973-128">Setting</span></span>       | <span data-ttu-id="3c973-129">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="3c973-129">Suggested value</span></span> | <span data-ttu-id="3c973-130">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c973-130">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3c973-131">**Database name** (Nome database)</span><span class="sxs-lookup"><span data-stu-id="3c973-131">**Database name**</span></span> | <span data-ttu-id="3c973-132">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="3c973-132">mySampleDatabase</span></span> | <span data-ttu-id="3c973-133">Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="3c973-133">For valid database names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="3c973-134">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="3c973-134">**Subscription**</span></span> | <span data-ttu-id="3c973-135">Sottoscrizione in uso</span><span class="sxs-lookup"><span data-stu-id="3c973-135">Your subscription</span></span>  | <span data-ttu-id="3c973-136">Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="3c973-136">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="3c973-137">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="3c973-137">**Resource group**</span></span> | <span data-ttu-id="3c973-138">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3c973-138">myResourceGroup</span></span> | <span data-ttu-id="3c973-139">Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="3c973-139">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="3c973-140">**Select source** (Seleziona origine)</span><span class="sxs-lookup"><span data-stu-id="3c973-140">**Select source**</span></span> | <span data-ttu-id="3c973-141">Database vuoto</span><span class="sxs-lookup"><span data-stu-id="3c973-141">Blank database</span></span> | <span data-ttu-id="3c973-142">Indica che deve essere creato un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="3c973-142">Specifies that a blank database should be created.</span></span> |

4. <span data-ttu-id="3c973-143">Fare clic su **Server** toocreate e configurare un nuovo server per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="3c973-143">Click **Server** toocreate and configure a new server for your new database.</span></span> <span data-ttu-id="3c973-144">Compilare hello **nuovo modulo server** con hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="3c973-144">Fill out hello **New server form** with hello following information:</span></span> 

   | <span data-ttu-id="3c973-145">Impostazione</span><span class="sxs-lookup"><span data-stu-id="3c973-145">Setting</span></span>       | <span data-ttu-id="3c973-146">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="3c973-146">Suggested value</span></span> | <span data-ttu-id="3c973-147">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c973-147">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3c973-148">**Server name** (Nome server)</span><span class="sxs-lookup"><span data-stu-id="3c973-148">**Server name**</span></span> | <span data-ttu-id="3c973-149">Qualsiasi nome globalmente univoco</span><span class="sxs-lookup"><span data-stu-id="3c973-149">Any globally unique name</span></span> | <span data-ttu-id="3c973-150">Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="3c973-150">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="3c973-151">**Nome di accesso amministratore server**</span><span class="sxs-lookup"><span data-stu-id="3c973-151">**Server admin login**</span></span> | <span data-ttu-id="3c973-152">Qualsiasi nome valido</span><span class="sxs-lookup"><span data-stu-id="3c973-152">Any valid name</span></span> | <span data-ttu-id="3c973-153">Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="3c973-153">For valid login names, see [Database Identifiers](https://docs.microsoft.com/sql/relational-databases/databases/database-identifiers).</span></span>|
   | <span data-ttu-id="3c973-154">**Password**</span><span class="sxs-lookup"><span data-stu-id="3c973-154">**Password**</span></span> | <span data-ttu-id="3c973-155">Qualsiasi password valida</span><span class="sxs-lookup"><span data-stu-id="3c973-155">Any valid password</span></span> | <span data-ttu-id="3c973-156">La password deve contenere almeno 8 caratteri e deve contenere caratteri di tre delle seguenti categorie di hello: lettere maiuscole, lettere minuscole, numeri e caratteri non alfanumerici.</span><span class="sxs-lookup"><span data-stu-id="3c973-156">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="3c973-157">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="3c973-157">**Location**</span></span> | <span data-ttu-id="3c973-158">Qualsiasi località valida</span><span class="sxs-lookup"><span data-stu-id="3c973-158">Any valid location</span></span> | <span data-ttu-id="3c973-159">Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="3c973-159">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   ![Creare il server di database](./media//sql-database-design-first-database/create-database-server.png)

5. <span data-ttu-id="3c973-161">Fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="3c973-161">Click **Select**.</span></span>

6. <span data-ttu-id="3c973-162">Fare clic su **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="3c973-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="3c973-163">Per esercitazione selezionare **20 DTU** e **250** GB di memoria.</span><span class="sxs-lookup"><span data-stu-id="3c973-163">For this tutorial, select **20 DTUs** and **250** GB of storage.</span></span>

   ![Creare il database s1](./media/sql-database-design-first-database/create-empty-database-pricing-tier.png)

7. <span data-ttu-id="3c973-165">Fare clic su **Apply**.</span><span class="sxs-lookup"><span data-stu-id="3c973-165">Click **Apply**.</span></span>  

8. <span data-ttu-id="3c973-166">Selezionare un **delle regole di confronto** per database vuoto di hello (per questa esercitazione, hello Usa il valore predefinito).</span><span class="sxs-lookup"><span data-stu-id="3c973-166">Select a **collation** for hello blank database (for this tutorial, use hello default value).</span></span> <span data-ttu-id="3c973-167">Per altre informazioni sulle regole di confronto, vedere [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations) (Regole di confronto)</span><span class="sxs-lookup"><span data-stu-id="3c973-167">For more information about collations, see [Collations](https://docs.microsoft.com/sql/t-sql/statements/collations)</span></span>

9. <span data-ttu-id="3c973-168">Fare clic su **crea** database hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="3c973-168">Click **Create** tooprovision hello database.</span></span> <span data-ttu-id="3c973-169">Provisioning richiede circa un minuto e mezzo di toocomplete.</span><span class="sxs-lookup"><span data-stu-id="3c973-169">Provisioning takes about a minute and a half toocomplete.</span></span> 

10. <span data-ttu-id="3c973-170">Sulla barra degli strumenti hello, fare clic su **notifiche** toomonitor processo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-170">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![notifica](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="3c973-172">Creare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="3c973-172">Create a server-level firewall rule</span></span>

<span data-ttu-id="3c973-173">Hello servizio Database SQL consente di creare un firewall hello a livello server che impedisce la connessione server toohello o da qualsiasi database nel server di hello, solo una regola del firewall creata firewall hello tooopen per indirizzi IP specifici strumenti e applicazioni esterne.</span><span class="sxs-lookup"><span data-stu-id="3c973-173">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="3c973-174">Seguire questi passaggi toocreate un [regola del firewall a livello di server SQL Database](sql-database-firewall-configure.md) per indirizzo IP del client e abilitare la connettività esterna tramite firewall del Database SQL hello per solo l'indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3c973-174">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="3c973-175">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="3c973-175">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="3c973-176">Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="3c973-176">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="3c973-177">In questo caso, è possibile connettersi tooyour server di Database SQL di Azure, a meno che il reparto IT consente di aprire la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="3c973-177">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="3c973-178">Al termine della distribuzione di hello, fare clic su **database SQL** dal menu a sinistra di hello e quindi fare clic su **mySampleDatabase** su hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c973-178">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="3c973-179">pagina di panoramica per l'apertura del database, che mostra hello completamente Hello completo del server (ad esempio **mynewserver20170313.database.windows.net**) e offre opzioni per un'ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="3c973-179">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="3c973-180">Copiare il nome completo del server per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="3c973-180">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3c973-181">È necessario il server di tooyour tooconnect nome completo del server e i relativi database nelle successive guide introduttive.</span><span class="sxs-lookup"><span data-stu-id="3c973-181">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![Nome del server](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="3c973-183">Fare clic su **impostare firewall server** sulla barra degli strumenti hello, come illustrato nella figura precedente hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-183">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="3c973-184">Hello **le impostazioni del Firewall** verrà visualizzata la pagina per il server di Database SQL di hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-184">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 


3. <span data-ttu-id="3c973-186">Fare clic su **Aggiungi indirizzo IP del client** su hello barra degli strumenti tooadd il corrente l'indirizzo IP di tooa nuova regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="3c973-186">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="3c973-187">Una regola del firewall può aprire la porta 1433 per un indirizzo IP singolo o un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="3c973-187">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="3c973-188">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="3c973-188">Click **Save**.</span></span> <span data-ttu-id="3c973-189">Una regola del firewall a livello di server viene creata per l'indirizzo IP corrente, aprire la porta 1433 sul server logico hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-189">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![Impostare la regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="3c973-191">Fare clic su **OK** e quindi chiudere hello **le impostazioni del Firewall** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c973-191">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="3c973-192">È ora possibile connettersi a server di Database SQL toohello e i relativi database tramite SQL Server Management Studio o un altro strumento di propria scelta da questo indirizzo IP utilizzando l'account amministratore di server hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3c973-192">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c973-193">Per impostazione predefinita, l'accesso attraverso il firewall di Database SQL hello è abilitato per tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c973-193">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="3c973-194">Fare clic su **OFF** su toodisable questa pagina per tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3c973-194">Click **OFF** on this page toodisable for all Azure services.</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="3c973-195">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="3c973-195">SQL server connection information</span></span>

<span data-ttu-id="3c973-196">Ottenere hello nome completo del server per il server di Database SQL di Azure nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-196">Get hello fully qualified server name for your Azure SQL Database server in hello Azure portal.</span></span> <span data-ttu-id="3c973-197">Utilizzare hello server completo tooconnect tooyour server dei nomi utilizzando SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3c973-197">You use hello fully qualified server name tooconnect tooyour server using SQL Server Management Studio.</span></span>

1. <span data-ttu-id="3c973-198">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="3c973-198">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="3c973-199">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c973-199">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="3c973-200">In hello **Essentials** riquadro hello pagina del portale Azure per il database, individuare e copiare hello **nome Server**.</span><span class="sxs-lookup"><span data-stu-id="3c973-200">In hello **Essentials** pane in hello Azure portal page for your database, locate and then copy hello **Server name**.</span></span>

   ![informazioni di connessione](./media/sql-database-connect-query-dotnet/server-name.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="3c973-202">La connessione a database toohello con SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="3c973-202">Connect toohello database with SSMS</span></span>

<span data-ttu-id="3c973-203">Utilizzare [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish un server di Database SQL di Azure tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="3c973-203">Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) tooestablish a connection tooyour Azure SQL Database server.</span></span>

1. <span data-ttu-id="3c973-204">Aprire SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="3c973-204">Open SQL Server Management Studio.</span></span>

2. <span data-ttu-id="3c973-205">In hello **connettersi tooServer** finestra di dialogo immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="3c973-205">In hello **Connect tooServer** dialog box, enter hello following information:</span></span>

   | <span data-ttu-id="3c973-206">Impostazione</span><span class="sxs-lookup"><span data-stu-id="3c973-206">Setting</span></span>       | <span data-ttu-id="3c973-207">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="3c973-207">Suggested value</span></span> | <span data-ttu-id="3c973-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="3c973-208">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="3c973-209">Tipo di server</span><span class="sxs-lookup"><span data-stu-id="3c973-209">Server type</span></span> | <span data-ttu-id="3c973-210">Motore di database</span><span class="sxs-lookup"><span data-stu-id="3c973-210">Database engine</span></span> | <span data-ttu-id="3c973-211">Questo valore è obbligatorio</span><span class="sxs-lookup"><span data-stu-id="3c973-211">This value is required</span></span> |
   | <span data-ttu-id="3c973-212">Nome server</span><span class="sxs-lookup"><span data-stu-id="3c973-212">Server name</span></span> | <span data-ttu-id="3c973-213">nome completo del server Hello</span><span class="sxs-lookup"><span data-stu-id="3c973-213">hello fully qualified server name</span></span> | <span data-ttu-id="3c973-214">Hello il nome deve essere simile al seguente: **mynewserver20170313.database.windows.net**.</span><span class="sxs-lookup"><span data-stu-id="3c973-214">hello name should be something like this: **mynewserver20170313.database.windows.net**.</span></span> |
   | <span data-ttu-id="3c973-215">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="3c973-215">Authentication</span></span> | <span data-ttu-id="3c973-216">Autenticazione di SQL Server</span><span class="sxs-lookup"><span data-stu-id="3c973-216">SQL Server Authentication</span></span> | <span data-ttu-id="3c973-217">L'autenticazione di SQL è hello unico tipo di autenticazione che è stato configurato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="3c973-217">SQL Authentication is hello only authentication type that we have configured in this tutorial.</span></span> |
   | <span data-ttu-id="3c973-218">Login</span><span class="sxs-lookup"><span data-stu-id="3c973-218">Login</span></span> | <span data-ttu-id="3c973-219">account amministratore di server Hello</span><span class="sxs-lookup"><span data-stu-id="3c973-219">hello server admin account</span></span> | <span data-ttu-id="3c973-220">Si tratta di hello con l'account specificato durante la creazione di server hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-220">This is hello account that you specified when you created hello server.</span></span> |
   | <span data-ttu-id="3c973-221">Password</span><span class="sxs-lookup"><span data-stu-id="3c973-221">Password</span></span> | <span data-ttu-id="3c973-222">password Hello per l'account di amministratore del server</span><span class="sxs-lookup"><span data-stu-id="3c973-222">hello password for your server admin account</span></span> | <span data-ttu-id="3c973-223">Si tratta hello password specificata durante la creazione di server hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-223">This is hello password that you specified when you created hello server.</span></span> |

   ![connettersi tooserver](./media/sql-database-connect-query-ssms/connect.png)

3. <span data-ttu-id="3c973-225">Fare clic su **opzioni** in hello **connettersi tooserver** la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="3c973-225">Click **Options** in hello **Connect tooserver** dialog box.</span></span> <span data-ttu-id="3c973-226">In hello **connettersi toodatabase** immettere **mySampleDatabase** tooconnect toothis database.</span><span class="sxs-lookup"><span data-stu-id="3c973-226">In hello **Connect toodatabase** section, enter **mySampleDatabase** tooconnect toothis database.</span></span>

   ![connettersi toodb nel server](./media/sql-database-connect-query-ssms/options-connect-to-db.png)  

4. <span data-ttu-id="3c973-228">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="3c973-228">Click **Connect**.</span></span> <span data-ttu-id="3c973-229">verrà visualizzata la finestra di Esplora oggetti Hello in SSMS.</span><span class="sxs-lookup"><span data-stu-id="3c973-229">hello Object Explorer window opens in SSMS.</span></span> 

5. <span data-ttu-id="3c973-230">In Esplora oggetti espandere **database** e quindi espandere **mySampleDatabase** oggetti hello tooview nel database di esempio hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-230">In Object Explorer, expand **Databases** and then expand **mySampleDatabase** tooview hello objects in hello sample database.</span></span>

   ![oggetti di database](./media/sql-database-connect-query-ssms/connected.png)  

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="3c973-232">Creare tabelle nel database di hello</span><span class="sxs-lookup"><span data-stu-id="3c973-232">Create tables in hello database</span></span> 

<span data-ttu-id="3c973-233">Creare uno schema di database con quattro tabelle che modellano un sistema di gestione degli studenti per le università tramite [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span><span class="sxs-lookup"><span data-stu-id="3c973-233">Create a database schema with four tables that model a student management system for universities using [Transact-SQL](https://docs.microsoft.com/sql/t-sql/language-reference):</span></span>

- <span data-ttu-id="3c973-234">Person</span><span class="sxs-lookup"><span data-stu-id="3c973-234">Person</span></span>
- <span data-ttu-id="3c973-235">Corso</span><span class="sxs-lookup"><span data-stu-id="3c973-235">Course</span></span>
- <span data-ttu-id="3c973-236">Studente</span><span class="sxs-lookup"><span data-stu-id="3c973-236">Student</span></span>
- <span data-ttu-id="3c973-237">Accreditare quel modello come un sistema di gestione degli studenti per le università</span><span class="sxs-lookup"><span data-stu-id="3c973-237">Credit that model a student management system for universities</span></span>

<span data-ttu-id="3c973-238">Hello diagramma seguente viene illustrato come queste tabelle vengono correlate tooeach altri.</span><span class="sxs-lookup"><span data-stu-id="3c973-238">hello following diagram shows how these tables are related tooeach other.</span></span> <span data-ttu-id="3c973-239">Alcune di queste tabelle fanno riferimento a delle colonne in altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="3c973-239">Some of these tables reference columns in other tables.</span></span> <span data-ttu-id="3c973-240">Ad esempio, fa riferimento a tabella Student hello hello **PersonId** colonna di hello **persona** tabella.</span><span class="sxs-lookup"><span data-stu-id="3c973-240">For example, hello Student table references hello **PersonId** column of hello **Person** table.</span></span> <span data-ttu-id="3c973-241">Uno Studio hello diagramma toounderstand come hello tabelle in questa esercitazione sono correlati tooone un altro.</span><span class="sxs-lookup"><span data-stu-id="3c973-241">Study hello diagram toounderstand how hello tables in this tutorial are related tooone another.</span></span> <span data-ttu-id="3c973-242">Per un esame approfondito come tabelle di database efficace toocreate, vedere [creare tabelle di database efficace](https://msdn.microsoft.com/library/cc505842.aspx).</span><span class="sxs-lookup"><span data-stu-id="3c973-242">For an in-depth look at how toocreate effective database tables, see [Create effective database tables](https://msdn.microsoft.com/library/cc505842.aspx).</span></span> <span data-ttu-id="3c973-243">Per informazioni sulla scelta dei tipi di dati, vedere [Tipi di dati](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span><span class="sxs-lookup"><span data-stu-id="3c973-243">For information about choosing data types, see [Data types](https://docs.microsoft.com/sql/t-sql/data-types/data-types-transact-sql).</span></span>

> [!NOTE]
> <span data-ttu-id="3c973-244">È inoltre possibile utilizzare hello [Progettazione tabelle in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate e progettare le tabelle.</span><span class="sxs-lookup"><span data-stu-id="3c973-244">You can also use hello [table designer in SQL Server Management Studio](https://msdn.microsoft.com/library/hh272695.aspx) toocreate and design your tables.</span></span> 

![Relazioni tra tabelle](./media/sql-database-design-first-database/tutorial-database-tables.png)

1. <span data-ttu-id="3c973-246">In Esplora oggetti fare clic con il pulsante destro del mouse su **mySampleDatabase** e scegliere **Nuova query**.</span><span class="sxs-lookup"><span data-stu-id="3c973-246">In Object Explorer, right-click **mySampleDatabase** and click **New Query**.</span></span> <span data-ttu-id="3c973-247">Query vuota viene visualizzata una finestra che è connesso tooyour database.</span><span class="sxs-lookup"><span data-stu-id="3c973-247">A blank query window opens that is connected tooyour database.</span></span>

2. <span data-ttu-id="3c973-248">Nella finestra query hello eseguire hello query toocreate quattro tabelle del database seguenti:</span><span class="sxs-lookup"><span data-stu-id="3c973-248">In hello query window, execute hello following query toocreate four tables in your database:</span></span> 

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

3. <span data-ttu-id="3c973-250">Espandere il nodo 'tabelle' hello nelle tabelle hello oggetto di SQL Server Management Studio Esplora toosee hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="3c973-250">Expand hello 'tables' node in hello SQL Server Management Studio Object explorer toosee hello tables you created.</span></span>

   ![tabelle create con SQL Server Management Studio](./media/sql-database-design-first-database/ssms-tables-created.png)

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="3c973-252">Caricamento dei dati nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="3c973-252">Load data into hello tables</span></span>

1. <span data-ttu-id="3c973-253">Creare una cartella denominata **SampleTableData** nei dati di esempio toostore cartella di download per il database.</span><span class="sxs-lookup"><span data-stu-id="3c973-253">Create a folder called **SampleTableData** in your Downloads folder toostore sample data for your database.</span></span> 

2. <span data-ttu-id="3c973-254">Esempio hello pulsante destro del mouse collegamenti e salvarli in hello **SampleTableData** cartella.</span><span class="sxs-lookup"><span data-stu-id="3c973-254">Right-click hello following links and save them into hello **SampleTableData** folder.</span></span> 

   - [<span data-ttu-id="3c973-255">SampleCourseData</span><span class="sxs-lookup"><span data-stu-id="3c973-255">SampleCourseData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCourseData)
   - [<span data-ttu-id="3c973-256">SamplePersonData</span><span class="sxs-lookup"><span data-stu-id="3c973-256">SamplePersonData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SamplePersonData)
   - [<span data-ttu-id="3c973-257">SampleStudentData</span><span class="sxs-lookup"><span data-stu-id="3c973-257">SampleStudentData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleStudentData)
   - [<span data-ttu-id="3c973-258">SampleCreditData</span><span class="sxs-lookup"><span data-stu-id="3c973-258">SampleCreditData</span></span>](https://sqldbtutorial.blob.core.windows.net/tutorials/SampleCreditData)

3. <span data-ttu-id="3c973-259">Aprire una finestra del prompt dei comandi e passare toohello SampleTableData cartella.</span><span class="sxs-lookup"><span data-stu-id="3c973-259">Open a command prompt window and navigate toohello SampleTableData folder.</span></span>

4. <span data-ttu-id="3c973-260">Eseguire i seguenti dati di esempio tooinsert comandi in sostituzione di valori hello per le tabelle di hello hello **ServerName**, **DatabaseName**, **UserName**e **Password** con i valori hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="3c973-260">Execute hello following commands tooinsert sample data into hello tables replacing hello values for **ServerName**, **DatabaseName**, **UserName**, and **Password** with hello values for your environment.</span></span>
  
   ```bcp
   bcp Course in SampleCourseData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Person in SamplePersonData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Student in SampleStudentData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   bcp Credit in SampleCreditData -S <ServerName>.database.windows.net -d <DatabaseName> -U <Username> -P <password> -q -c -t ","
   ```

<span data-ttu-id="3c973-261">Sono ora stati caricati i dati di esempio nelle tabelle di hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="3c973-261">You have now loaded sample data into hello tables you created earlier.</span></span>

## <a name="query-data"></a><span data-ttu-id="3c973-262">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="3c973-262">Query data</span></span>

<span data-ttu-id="3c973-263">Eseguire le seguenti query tooretrieve informazioni dalle tabelle di database hello hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-263">Execute hello following queries tooretrieve information from hello database tables.</span></span> <span data-ttu-id="3c973-264">Vedere [la scrittura di query SQL](https://technet.microsoft.com/library/bb264565.aspx) toolearn ulteriori informazioni sulla scrittura di query SQL.</span><span class="sxs-lookup"><span data-stu-id="3c973-264">See [Writing SQL Queries](https://technet.microsoft.com/library/bb264565.aspx) toolearn more about writing SQL queries.</span></span> <span data-ttu-id="3c973-265">Hello prima query unisce in join toofind tutte le quattro tabelle invece di tutti gli studenti hello da ' Dominick Pope' hanno un livello superiore al 75% nella propria classe.</span><span class="sxs-lookup"><span data-stu-id="3c973-265">hello first query joins all four tables toofind all hello students taught by 'Dominick Pope' who have a grade higher than 75% in his class.</span></span> <span data-ttu-id="3c973-266">seconda query Hello unisce tutte e quattro le tabelle e trova tutti i corsi mai registrati in cui 'Noe Coleman'.</span><span class="sxs-lookup"><span data-stu-id="3c973-266">hello second query joins all four tables and finds all courses in which 'Noe Coleman' has ever enrolled.</span></span>

1. <span data-ttu-id="3c973-267">In una finestra di query di SQL Server Management Studio, eseguire hello seguente query:</span><span class="sxs-lookup"><span data-stu-id="3c973-267">In a SQL Server Management Studio query window, execute hello following query:</span></span>

   ```sql 
   -- Find hello students taught by Dominick Pope who have a grade higher than 75%

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

2. <span data-ttu-id="3c973-268">In una finestra di query di SQL Server Management Studio, eseguire la query seguente:</span><span class="sxs-lookup"><span data-stu-id="3c973-268">In a SQL Server Management Studio query window, execute following query:</span></span>

   ```sql
   -- Find all hello courses in which Noe Coleman has ever enrolled

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

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="3c973-269">Ripristinare un punto precedente tooa di database nel tempo</span><span class="sxs-lookup"><span data-stu-id="3c973-269">Restore a database tooa previous point in time</span></span>

<span data-ttu-id="3c973-270">Si supponga di aver eliminato accidentalmente una tabella.</span><span class="sxs-lookup"><span data-stu-id="3c973-270">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="3c973-271">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="3c973-271">This is something you cannot easily recover from.</span></span> <span data-ttu-id="3c973-272">Database SQL di Azure consente toogo tooany indietro punto nel tempo di hello ultimo backup too35 giorni e nel nuovo database di tempo tooa questo punto di ripristino.</span><span class="sxs-lookup"><span data-stu-id="3c973-272">Azure SQL Database allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new database.</span></span> <span data-ttu-id="3c973-273">È possibile toorecover questo database i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="3c973-273">You can you this database toorecover your deleted data.</span></span> <span data-ttu-id="3c973-274">Hello seguenti passaggi punto di ripristino hello esempio database tooa prima dell'aggiunta di tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-274">hello following steps restore hello sample database tooa point before hello tables were added.</span></span>

1. <span data-ttu-id="3c973-275">Nella pagina Database SQL di hello per il database, fare clic su **ripristinare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-275">On hello SQL Database page for your database, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="3c973-276">Hello **ripristinare** verrà visualizzata la pagina.</span><span class="sxs-lookup"><span data-stu-id="3c973-276">hello **Restore** page opens.</span></span>

   ![ripristinare](./media/sql-database-design-first-database/restore.png)

2. <span data-ttu-id="3c973-278">Compilare hello **ripristinare** form con le informazioni necessarie hello:</span><span class="sxs-lookup"><span data-stu-id="3c973-278">Fill out hello **Restore** form with hello required information:</span></span>
    * <span data-ttu-id="3c973-279">Nome database: specificare un nome per il database</span><span class="sxs-lookup"><span data-stu-id="3c973-279">Database name: Provide a database name</span></span> 
    * <span data-ttu-id="3c973-280">Punto nel tempo: Seleziona hello **momento** scheda hello ripristino modulo</span><span class="sxs-lookup"><span data-stu-id="3c973-280">Point-in-time: Select hello **Point-in-time** tab on hello Restore form</span></span> 
    * <span data-ttu-id="3c973-281">Punto di ripristino: selezionare un'ora che si verifica prima che il database di hello è stata modificata</span><span class="sxs-lookup"><span data-stu-id="3c973-281">Restore point: Select a time that occurs before hello database was changed</span></span>
    * <span data-ttu-id="3c973-282">Server di destinazione: non è possibile modificare questo valore quando si ripristina un database</span><span class="sxs-lookup"><span data-stu-id="3c973-282">Target server: You cannot change this value when restoring a database</span></span> 
    * <span data-ttu-id="3c973-283">Pool di database elastici: selezionare **Nessuno**</span><span class="sxs-lookup"><span data-stu-id="3c973-283">Elastic database pool: Select **None**</span></span>  
    * <span data-ttu-id="3c973-284">Piano tariffario: selezionare **20 DTUs** (20 DTU) e **250 GB** di memoria.</span><span class="sxs-lookup"><span data-stu-id="3c973-284">Pricing tier: Select **20 DTUs** and **250 GB** of storage.</span></span>

   ![punto di ripristino](./media/sql-database-design-first-database/restore-point.png)

3. <span data-ttu-id="3c973-286">Fare clic su **OK** toorestore hello database troppo[tooa punto di ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) prima dell'aggiunta di tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="3c973-286">Click **OK** toorestore hello database too[restore tooa point in time](sql-database-recovery-using-backups.md#point-in-time-restore) before hello tables were added.</span></span> <span data-ttu-id="3c973-287">Ripristino di un punto diverso tooa di database nel tempo, viene creato un database di duplicati in hello stesso server di database originale hello hello temporizzazione specifica, purché venga incluso il periodo di memorizzazione hello per le [livello di servizio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="3c973-287">Restoring a database tooa different point in time creates a duplicate database in hello same server as hello original database as of hello point in time you specify, as long as it is within hello retention period for your [service tier](sql-database-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c973-288">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3c973-288">Next Steps</span></span> 
<span data-ttu-id="3c973-289">In questa esercitazione è stato attività di base del database, ad esempio creare un database e tabelle, caricare e query sui dati e hello database tooa precedente punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="3c973-289">In this tutorial, you learned basic database tasks such as create a database and tables, load and query data, and restore hello database tooa previous point in time.</span></span> <span data-ttu-id="3c973-290">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="3c973-290">You learned how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="3c973-291">Creare un database</span><span class="sxs-lookup"><span data-stu-id="3c973-291">Create a database</span></span>
> * <span data-ttu-id="3c973-292">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="3c973-292">Set up a firewall rule</span></span>
> * <span data-ttu-id="3c973-293">La connessione a database toohello con [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span><span class="sxs-lookup"><span data-stu-id="3c973-293">Connect toohello database with [SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx) (SSMS)</span></span>
> * <span data-ttu-id="3c973-294">Creare tabelle</span><span class="sxs-lookup"><span data-stu-id="3c973-294">Create tables</span></span>
> * <span data-ttu-id="3c973-295">Eseguire il caricamento bulk dei dati</span><span class="sxs-lookup"><span data-stu-id="3c973-295">Bulk load data</span></span>
> * <span data-ttu-id="3c973-296">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="3c973-296">Query that data</span></span>
> * <span data-ttu-id="3c973-297">Hello database tooa precedente punto di ripristino temporizzato utilizzando il Database SQL [ripristino temporizzato](sql-database-recovery-using-backups.md#point-in-time-restore) funzionalità</span><span class="sxs-lookup"><span data-stu-id="3c973-297">Restore hello database tooa previous point in time using SQL Database [point in time restore](sql-database-recovery-using-backups.md#point-in-time-restore) capabilities</span></span>

<span data-ttu-id="3c973-298">Spostare toohello toolearn esercitazione successiva sulla progettazione di un database tramite Visual Studio e c#.</span><span class="sxs-lookup"><span data-stu-id="3c973-298">Advance toohello next tutorial toolearn about designing a database using Visual Studio and C#.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="3c973-299">Progettare un database SQL di Azure e connettersi con C# e ADO.NET</span><span class="sxs-lookup"><span data-stu-id="3c973-299">Design an Azure SQL database and connect with C# and ADO.NET</span></span>](sql-database-design-first-database-csharp.md)
