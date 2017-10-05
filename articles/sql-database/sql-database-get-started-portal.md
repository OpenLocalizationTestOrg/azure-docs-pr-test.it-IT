---
title: 'Portale di Azure: creare un database SQL | Microsoft Docs'
description: Informazioni su come creare un server logico di database SQL, una regola del firewall a livello di server e database nel portale di Azure. Viene illustrato anche come effettuare una query su un database SQL di Azure usando il portale di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: a863cf3ad08040906850f64db6505f30bcfa72eb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-azure-sql-database-in-the-azure-portal"></a><span data-ttu-id="2c85e-105">Creare un database SQL di Azure nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="2c85e-105">Create an Azure SQL database in the Azure portal</span></span>

<span data-ttu-id="2c85e-106">Questa esercitazione introduttiva illustra come creare un database SQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-106">This quick start tutorial walks through how to create a SQL database in Azure.</span></span> <span data-ttu-id="2c85e-107">Il database SQL di Azure è un'offerta di "database distribuito come servizio" che consente di eseguire e ridimensionare i database di SQL Server a disponibilità elevata nel cloud.</span><span class="sxs-lookup"><span data-stu-id="2c85e-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you to run and scale highly available SQL Server databases in the cloud.</span></span> <span data-ttu-id="2c85e-108">Questa guida introduttiva illustra come iniziare a creare un database SQL con il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-108">This quick start shows you how to get started by creating a SQL database using the Azure portal.</span></span>

<span data-ttu-id="2c85e-109">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="2c85e-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="2c85e-110">Accedere al Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-110">Log in to the Azure portal</span></span>

<span data-ttu-id="2c85e-111">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2c85e-111">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="2c85e-112">Creazione di un database SQL</span><span class="sxs-lookup"><span data-stu-id="2c85e-112">Create a SQL database</span></span>

<span data-ttu-id="2c85e-113">Un database SQL di Azure viene creato con un set definito di [risorse di calcolo e di archiviazione](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2c85e-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="2c85e-114">Il database viene creato in un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) e in un [server logico di database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="2c85e-114">The database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="2c85e-115">Seguire questi passaggi per creare un database SQL contenente i dati di esempio di Adventure Works LT.</span><span class="sxs-lookup"><span data-stu-id="2c85e-115">Follow these steps to create a SQL database containing the Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="2c85e-116">Fare clic sul pulsante **Nuovo** nell'angolo superiore sinistro del portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-116">Click the **New** button found on the upper left-hand corner of the Azure portal.</span></span>

2. <span data-ttu-id="2c85e-117">Selezionare **Database** nella pagina **Nuovo** e quindi **Database SQL** nella pagina **Database**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-117">Select **Databases** from the **New** page, and select **SQL Database** from the **Databases** page.</span></span>

   ![Creare il database 1](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="2c85e-119">Compilare il modulo Database SQL con le informazioni seguenti, come illustrato nell'immagine precedente:</span><span class="sxs-lookup"><span data-stu-id="2c85e-119">Fill out the SQL Database form with the following information, as shown on the preceding image:</span></span>   

   | <span data-ttu-id="2c85e-120">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2c85e-120">Setting</span></span>       | <span data-ttu-id="2c85e-121">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="2c85e-121">Suggested value</span></span> | <span data-ttu-id="2c85e-122">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2c85e-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="2c85e-123">**Database name** (Nome database)</span><span class="sxs-lookup"><span data-stu-id="2c85e-123">**Database name**</span></span> | <span data-ttu-id="2c85e-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="2c85e-124">mySampleDatabase</span></span> | <span data-ttu-id="2c85e-125">Per i nomi di database validi, vedere [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="2c85e-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="2c85e-126">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="2c85e-126">**Subscription**</span></span> | <span data-ttu-id="2c85e-127">Sottoscrizione in uso</span><span class="sxs-lookup"><span data-stu-id="2c85e-127">Your subscription</span></span>  | <span data-ttu-id="2c85e-128">Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="2c85e-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="2c85e-129">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="2c85e-129">**Resource group**</span></span>  | <span data-ttu-id="2c85e-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c85e-130">myResourceGroup</span></span> | <span data-ttu-id="2c85e-131">Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="2c85e-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="2c85e-132">**Seleziona origine**</span><span class="sxs-lookup"><span data-stu-id="2c85e-132">**Source source**</span></span> | <span data-ttu-id="2c85e-133">Sample (AdventureWorksLT) (Esempio - AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="2c85e-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="2c85e-134">Carica lo schema e i dati di AdventureWorksLT nel nuovo database</span><span class="sxs-lookup"><span data-stu-id="2c85e-134">Loads the AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="2c85e-135">È necessario selezionare il database di esempio in questo modulo perché verrà usato nel resto di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="2c85e-135">You must select the sample database on this form because it is used in the remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="2c85e-136">In **Server** fare clic su **Configurare le impostazioni necessarie** e compilare il server SQL (server logico) con le informazioni seguenti, come illustrato nell'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="2c85e-136">Under **Server**, click **Configure required settings** and fill out the SQL server (logical server) form with the following information, as shown on the following image:</span></span>   

   | <span data-ttu-id="2c85e-137">Impostazione</span><span class="sxs-lookup"><span data-stu-id="2c85e-137">Setting</span></span>       | <span data-ttu-id="2c85e-138">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="2c85e-138">Suggested value</span></span> | <span data-ttu-id="2c85e-139">Descrizione</span><span class="sxs-lookup"><span data-stu-id="2c85e-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="2c85e-140">**Server name** (Nome server)</span><span class="sxs-lookup"><span data-stu-id="2c85e-140">**Server name**</span></span> | <span data-ttu-id="2c85e-141">Qualsiasi nome globalmente univoco</span><span class="sxs-lookup"><span data-stu-id="2c85e-141">Any globally unique name</span></span> | <span data-ttu-id="2c85e-142">Per i nomi di server validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="2c85e-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="2c85e-143">**Nome di accesso amministratore server**</span><span class="sxs-lookup"><span data-stu-id="2c85e-143">**Server admin login**</span></span> | <span data-ttu-id="2c85e-144">Qualsiasi nome valido</span><span class="sxs-lookup"><span data-stu-id="2c85e-144">Any valid name</span></span> | <span data-ttu-id="2c85e-145">Per i nomi di accesso validi, vedere [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) (Identificatori di database).</span><span class="sxs-lookup"><span data-stu-id="2c85e-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="2c85e-146">**Password**</span><span class="sxs-lookup"><span data-stu-id="2c85e-146">**Password**</span></span> | <span data-ttu-id="2c85e-147">Qualsiasi password valida</span><span class="sxs-lookup"><span data-stu-id="2c85e-147">Any valid password</span></span> | <span data-ttu-id="2c85e-148">La password deve almeno 8 caratteri e contenere caratteri inclusi in tre delle categorie seguenti: caratteri maiuscoli, caratteri minuscoli, numeri e caratteri non alfanumerici.</span><span class="sxs-lookup"><span data-stu-id="2c85e-148">Your password must have at least 8 characters and must contain characters from three of the following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="2c85e-149">**Sottoscrizione**</span><span class="sxs-lookup"><span data-stu-id="2c85e-149">**Subscription**</span></span> | <span data-ttu-id="2c85e-150">Sottoscrizione in uso</span><span class="sxs-lookup"><span data-stu-id="2c85e-150">Your subscription</span></span> | <span data-ttu-id="2c85e-151">Per informazioni dettagliate sulle sottoscrizioni, vedere [Subscriptions](https://account.windowsazure.com/Subscriptions) (Sottoscrizioni).</span><span class="sxs-lookup"><span data-stu-id="2c85e-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="2c85e-152">**Gruppo di risorse**</span><span class="sxs-lookup"><span data-stu-id="2c85e-152">**Resource group**</span></span> | <span data-ttu-id="2c85e-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2c85e-153">myResourceGroup</span></span> | <span data-ttu-id="2c85e-154">Per i nomi di gruppi di risorse validi, vedere [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Regole di denominazione e restrizioni).</span><span class="sxs-lookup"><span data-stu-id="2c85e-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="2c85e-155">**Posizione**</span><span class="sxs-lookup"><span data-stu-id="2c85e-155">**Location**</span></span> | <span data-ttu-id="2c85e-156">Qualsiasi località valida</span><span class="sxs-lookup"><span data-stu-id="2c85e-156">Any valid location</span></span> | <span data-ttu-id="2c85e-157">Per informazioni sulle aree, vedere [Aree di Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="2c85e-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="2c85e-158">L'account di accesso amministratore server e la password qui specificati sono necessari per accedere al server e ai relativi database più avanti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="2c85e-158">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="2c85e-159">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="2c85e-159">Remember or record this information for later use.</span></span> 
   >  

   ![Creare il server di database](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="2c85e-161">Dopo aver completato il modulo, fare clic su **Seleziona**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-161">When you have completed the form, click **Select**.</span></span>

6. <span data-ttu-id="2c85e-162">Fare clic su **Piano tariffario** per specificare il livello di servizio e il livello delle prestazioni per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="2c85e-162">Click **Pricing tier** to specify the service tier and performance level for your new database.</span></span> <span data-ttu-id="2c85e-163">Usare il dispositivo di scorrimento per selezionare **20 DTU** e **250** GB di spazio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2c85e-163">Use the slider to select **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="2c85e-164">Per altre informazioni sulle DTU, vedere il relativo [articolo](sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="2c85e-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![Creare il database s1](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="2c85e-166">Dopo aver selezionato la quantità di DTU, fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-166">After selected the amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="2c85e-167">Dopo aver completato il modulo del database SQL, fare clic su **Crea** per effettuare il provisioning del database.</span><span class="sxs-lookup"><span data-stu-id="2c85e-167">Now that you have completed the SQL Database form, click **Create** to provision the database.</span></span> <span data-ttu-id="2c85e-168">Il provisioning richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="2c85e-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="2c85e-169">Sulla barra degli strumenti fare clic su **Notifiche** per monitorare il processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2c85e-169">On the toolbar, click **Notifications** to monitor the deployment process.</span></span>

   ![notifica](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="2c85e-171">Creare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="2c85e-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="2c85e-172">Il servizio di database SQL crea un firewall a livello di server che impedisce alle applicazioni e agli strumenti esterni di connettersi al server o ai database sul server a meno che non venga creata una regola del firewall per aprire il firewall per indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="2c85e-172">The SQL Database service creates a firewall at the server-level that prevents external applications and tools from connecting to the server or any databases on the server unless a firewall rule is created to open the firewall for specific IP addresses.</span></span> <span data-ttu-id="2c85e-173">Seguire questi passaggi per creare una [regola del firewall a livello di server di database SQL](sql-database-firewall-configure.md) per l'indirizzo IP del client e abilitare la connettività esterna tramite il firewall del database SQL solo per il proprio indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="2c85e-173">Follow these steps to create a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through the SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="2c85e-174">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="2c85e-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="2c85e-175">Se si sta tentando di connettersi da una rete aziendale, il traffico in uscita attraverso la porta 1433 potrebbe non essere autorizzato dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="2c85e-175">If you are trying to connect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="2c85e-176">In questo caso, non è possibile connettersi al server del database SQL di Azure, a meno che il reparto IT non apra la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="2c85e-176">If so, you cannot connect to your Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="2c85e-177">Al termine della distribuzione, scegliere **Database SQL** dal menu a sinistra e fare clic su **mySampleDatabase** nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-177">After the deployment completes, click **SQL databases** from the left-hand menu and then click **mySampleDatabase** on the **SQL databases** page.</span></span> <span data-ttu-id="2c85e-178">Si apre la pagina di panoramica per il database, in cui è indicato il nome completo del server (ad esempio, **mynewserver20170313.database.windows.net**) e in cui sono disponibili altre opzioni di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2c85e-178">The overview page for your database opens, showing you the fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="2c85e-179">Copiare il nome completo del server per usarlo in seguito.</span><span class="sxs-lookup"><span data-stu-id="2c85e-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="2c85e-180">Questo nome completo del server è necessario per connettersi al server e ai relativi database nelle guide introduttive successive.</span><span class="sxs-lookup"><span data-stu-id="2c85e-180">You need this fully qualified server name to connect to your server and its databases in subsequent quick starts.</span></span>
   > 

   ![Nome del server](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="2c85e-182">Fare clic su **Imposta firewall server** sulla barra degli strumenti, come illustrato nell'immagine precedente.</span><span class="sxs-lookup"><span data-stu-id="2c85e-182">Click **Set server firewall** on the toolbar as shown in the previous image.</span></span> <span data-ttu-id="2c85e-183">Si apre la pagina **Impostazioni del firewall** per il server del database SQL.</span><span class="sxs-lookup"><span data-stu-id="2c85e-183">The **Firewall settings** page for the SQL Database server opens.</span></span> 

   ![Regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="2c85e-185">Fare clic su **Aggiungi IP client** sulla barra degli strumenti per aggiungere l'indirizzo IP corrente a una nuova regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="2c85e-185">Click **Add client IP** on the toolbar to add your current IP address to a new firewall rule.</span></span> <span data-ttu-id="2c85e-186">Una regola del firewall può aprire la porta 1433 per un indirizzo IP singolo o un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="2c85e-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="2c85e-187">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-187">Click **Save**.</span></span> <span data-ttu-id="2c85e-188">Viene creata una regola del firewall a livello di server per l'indirizzo IP corrente, che apre la porta 1433 nel server logico.</span><span class="sxs-lookup"><span data-stu-id="2c85e-188">A server-level firewall rule is created for your current IP address opening port 1433 on the logical server.</span></span>

   ![Impostare la regola del firewall del server](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="2c85e-190">Fare clic su **OK** e quindi chiudere la pagina **Impostazioni del firewall**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-190">Click **OK** and then close the **Firewall settings** page.</span></span>

<span data-ttu-id="2c85e-191">È ora possibile connettersi al server del database SQL e ai relativi database usando SQL Server Management Studio o un altro strumento di propria scelta da questo indirizzo IP, con l'account amministratore del server creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2c85e-191">You can now connect to the SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using the server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c85e-192">Per impostazione predefinita, l'accesso attraverso il firewall del database SQL è abilitato per tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-192">By default, access through the SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="2c85e-193">Selezionando **NO** in questa pagina permette di disabilitare tutti i servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c85e-193">Click **OFF** on this page to disable for all Azure services.</span></span>
>

## <a name="query-the-sql-database"></a><span data-ttu-id="2c85e-194">Effettuare una query sul database SQL</span><span class="sxs-lookup"><span data-stu-id="2c85e-194">Query the SQL database</span></span>

<span data-ttu-id="2c85e-195">Ora che è stato creato un database di esempio in Azure, usare lo strumento di query predefinito nel portale di Azure per verificare la possibilità di connettersi al database ed eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="2c85e-195">Now that you have created a sample database in Azure, let’s use the built-in query tool within the Azure portal to confirm that you can connect to the database and query the data.</span></span> 

1. <span data-ttu-id="2c85e-196">Nella pagina Database SQL del database fare clic su **Strumenti** sulla barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="2c85e-196">On the SQL Database page for your database, click **Tools** on the toolbar.</span></span> <span data-ttu-id="2c85e-197">Si apre la pagina **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-197">The **Tools** page opens.</span></span>

   ![Menu Strumenti](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="2c85e-199">Fare clic su **Editor di query (anteprima)**, fare clic sulla casella di controllo **Condizioni per l'anteprima** e quindi su **OK**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-199">Click **Query editor (preview)**, click the **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="2c85e-200">Si apre la pagina Editor di query.</span><span class="sxs-lookup"><span data-stu-id="2c85e-200">The Query editor page opens.</span></span>

3. <span data-ttu-id="2c85e-201">Fare clic su **Accedi** e quindi, quando viene richiesto, selezionare **Autenticazione di SQL Server** e infine immettere l'account e la password di accesso amministratore server creata prima.</span><span class="sxs-lookup"><span data-stu-id="2c85e-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide the server admin login and password that you created earlier.</span></span>

   ![Accesso](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="2c85e-203">Fare clic su **OK** per accedere.</span><span class="sxs-lookup"><span data-stu-id="2c85e-203">Click **OK** to log in.</span></span>

5. <span data-ttu-id="2c85e-204">Dopo l'autenticazione, digitare la query seguente nel riquadro dell'editor di query.</span><span class="sxs-lookup"><span data-stu-id="2c85e-204">After you are authenticated, type the following query in the query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="2c85e-205">Fare clic su **Esegui** e quindi esaminare i risultati della query nel riquadro **Risultati**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-205">Click **Run** and then review the query results in the **Results** pane.</span></span>

   ![Risultati dell'Editor di query](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="2c85e-207">Chiudere la pagina **Editor di query** e la pagina **Strumenti**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-207">Close the **Query editor** page and the **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="2c85e-208">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="2c85e-208">Clean up resources</span></span>

<span data-ttu-id="2c85e-209">Se queste risorse non sono necessarie per un'altra guida introduttiva/esercitazione (vedere [Passaggi successivi](#next-steps)), è possibile eliminarle seguendo questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2c85e-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing the following:</span></span>


1. <span data-ttu-id="2c85e-210">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic su **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-210">From the left-hand menu in the Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="2c85e-211">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare **myResourceGroup** nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="2c85e-211">On your resource group page, click **Delete**, type **myResourceGroup** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c85e-212">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c85e-212">Next steps</span></span>

<span data-ttu-id="2c85e-213">Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti.</span><span class="sxs-lookup"><span data-stu-id="2c85e-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="2c85e-214">Per altre informazioni, scegliere uno strumento di seguito:</span><span class="sxs-lookup"><span data-stu-id="2c85e-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="2c85e-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="2c85e-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="2c85e-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="2c85e-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="2c85e-217">.NET</span><span class="sxs-lookup"><span data-stu-id="2c85e-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="2c85e-218">PHP</span><span class="sxs-lookup"><span data-stu-id="2c85e-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="2c85e-219">Node.JS</span><span class="sxs-lookup"><span data-stu-id="2c85e-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="2c85e-220">Java</span><span class="sxs-lookup"><span data-stu-id="2c85e-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="2c85e-221">Python</span><span class="sxs-lookup"><span data-stu-id="2c85e-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="2c85e-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="2c85e-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
