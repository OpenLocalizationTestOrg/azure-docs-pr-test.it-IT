---
title: iniziare aaaAzure SQL Data Warehouse - esercitazione | Documenti Microsoft
description: "Questa esercitazione viene illustrato come tooprovision e caricare i dati in Azure SQL Data Warehouse. Si apprenderà inoltre hello nozioni fondamentali per la scalabilità, la sospensione e l'ottimizzazione."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: barbkess
ms.assetid: 52DFC191-E094-4B04-893F-B64D5828A900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: quickstart
ms.date: 01/26/2017
ms.author: elbutter;barbkess
ms.openlocfilehash: edd2a21b0fe49ca8e9792c7c512310339a822c55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-data-warehouse"></a><span data-ttu-id="81181-104">Introduzione a SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="81181-104">Get started with SQL Data Warehouse</span></span>

<span data-ttu-id="81181-105">Questa esercitazione viene illustrato come tooprovision e caricare i dati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-105">This tutorial shows how tooprovision and load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="81181-106">Si apprenderà inoltre hello nozioni fondamentali per la scalabilità, la sospensione e l'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="81181-106">You’ll also learn hello basics about scaling, pausing, and tuning.</span></span> <span data-ttu-id="81181-107">Al termine, che verrà tooquery pronto ed esplorare il data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-107">When you’re finished, you’ll be ready tooquery and explore your data warehouse.</span></span>

<span data-ttu-id="81181-108">**Toocomplete tempo stimato:** si tratta di un'esercitazione end-to-end con codice di esempio che accetta toocomplete circa 30 minuti dopo che siano soddisfatti i prerequisiti di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-108">**Estimated time toocomplete:** This is an end-to-end tutorial with example code that takes about 30 minutes toocomplete once you have met hello prerequisites.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="81181-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="81181-109">Prerequisites</span></span>

<span data-ttu-id="81181-110">esercitazione Hello presuppone che si ha familiarità con concetti di base di SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-110">hello tutorial assumes you are familiar with SQL Data Warehouse basic concepts.</span></span> <span data-ttu-id="81181-111">Se sono necessarie informazioni introduttive, vedere [Informazioni su Azure SQL Data Warehouse](sql-data-warehouse-overview-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="81181-111">If you need an introduction, see [What is SQL Data Warehouse?](sql-data-warehouse-overview-what-is.md)</span></span> 

### <a name="sign-up-for-microsoft-azure"></a><span data-ttu-id="81181-112">Iscrizione a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="81181-112">Sign up for Microsoft Azure</span></span>
<span data-ttu-id="81181-113">Se si dispone già di un account di Microsoft Azure, è necessario toosign per uno toouse questo servizio.</span><span class="sxs-lookup"><span data-stu-id="81181-113">If you don't already have a Microsoft Azure account, you need toosign up for one toouse this service.</span></span> <span data-ttu-id="81181-114">Se si ha già un account, è possibile ignorare questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="81181-114">If you already have an account, you may skip this step.</span></span> 

1. <span data-ttu-id="81181-115">Spostarsi tra le pagine di account toohello [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span><span class="sxs-lookup"><span data-stu-id="81181-115">Navigate toohello account pages [https://azure.microsoft.com/account/](https://azure.microsoft.com/account/)</span></span>
2. <span data-ttu-id="81181-116">Creare un account Azure gratuito o acquistare un account.</span><span class="sxs-lookup"><span data-stu-id="81181-116">Create a free Azure account, or purchase an account.</span></span>
3. <span data-ttu-id="81181-117">Seguire le istruzioni di hello</span><span class="sxs-lookup"><span data-stu-id="81181-117">Follow hello instructions</span></span>

### <a name="install-appropriate-sql-client-drivers-and-tools"></a><span data-ttu-id="81181-118">Installare i driver del client SQL e gli strumenti appropriati</span><span class="sxs-lookup"><span data-stu-id="81181-118">Install appropriate SQL client drivers and tools</span></span>

<span data-ttu-id="81181-119">La maggior parte degli strumenti client di SQL è possono connettersi tooSQL Data Warehouse utilizzando JDBC, ODBC o ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="81181-119">Most SQL client tools can connect tooSQL Data Warehouse by using JDBC, ODBC, or ADO.NET.</span></span> <span data-ttu-id="81181-120">A causa di toohello numero elevato di funzionalità di T-SQL che supporta SQL Data Warehouse, alcune applicazioni client non sono completamente compatibili con SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-120">Due toohello large number of T-SQL features that SQL Data Warehouse supports, some client applications are not fully compatible with SQL Data Warehouse.</span></span>

<span data-ttu-id="81181-121">Se si esegue un sistema operativo Windows, è consigliabile usare [Visual Studio] o [SQL Server Management Studio].</span><span class="sxs-lookup"><span data-stu-id="81181-121">If you are running a Windows operating system, we recommend using either [Visual Studio] or [SQL Server Management Studio].</span></span>

[!INCLUDE [Create a new logical server](../../includes/sql-data-warehouse-create-logical-server.md)] 

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="81181-122">Creare un SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="81181-122">Create a SQL Data Warehouse</span></span>

<span data-ttu-id="81181-123">SQL Data Warehouse è un tipo di database speciale, progettato per l'elaborazione parallela massiva (MPP, Massively Parallel Processing).</span><span class="sxs-lookup"><span data-stu-id="81181-123">A SQL Data Warehouse is a special type of database that is designed for massively parallel processing.</span></span> <span data-ttu-id="81181-124">database Hello è distribuita tra più nodi e di elaborazione delle query in parallelo.</span><span class="sxs-lookup"><span data-stu-id="81181-124">hello database is distributed across multiple nodes and processes queries in parallel.</span></span> <span data-ttu-id="81181-125">SQL Data Warehouse è un nodo del controllo che coordina le attività di hello di tutti i nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-125">SQL Data Warehouse has a control node that orchestrates hello activities of all hello nodes.</span></span> <span data-ttu-id="81181-126">i nodi di Hello utilizzano toomanage Database SQL i dati.</span><span class="sxs-lookup"><span data-stu-id="81181-126">hello nodes themselves use SQL Database toomanage your data.</span></span>  

> [!NOTE]
> <span data-ttu-id="81181-127">La creazione di un'istanza di SQL Data Warehouse può avere come risultato un nuovo servizio fatturabile.</span><span class="sxs-lookup"><span data-stu-id="81181-127">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="81181-128">Per altre informazioni, vedere [SQL Data Warehouse Prezzi](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="81181-128">For more information, see [SQL Data Warehouse pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>
>

### <a name="create-a-data-warehouse"></a><span data-ttu-id="81181-129">Creare un data warehouse</span><span class="sxs-lookup"><span data-stu-id="81181-129">Create a data warehouse</span></span>

1. <span data-ttu-id="81181-130">Sign in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="81181-130">Sign into hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="81181-131">Fare clic su **Nuovo** > **Database** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="81181-131">Click **New** > **Databases** > **SQL Data Warehouse**.</span></span>

    <span data-ttu-id="81181-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png)![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span><span class="sxs-lookup"><span data-stu-id="81181-132">![NewBlade](../../includes/media/sql-data-warehouse-create-dw/blade-click-new.png) ![SelectDW](../../includes/media/sql-data-warehouse-create-dw/blade-select-dw.png)</span></span>

3. <span data-ttu-id="81181-133">Compilare i dettagli della distribuzione</span><span class="sxs-lookup"><span data-stu-id="81181-133">Fill out deployment details</span></span>

    <span data-ttu-id="81181-134">**Nome database**: scegliere un nome qualsiasi.</span><span class="sxs-lookup"><span data-stu-id="81181-134">**Database Name**: Pick anything you'd like.</span></span> <span data-ttu-id="81181-135">Se si dispone di più data warehouse, è consigliabile che i nomi di includono i dettagli, ad esempio area hello, ambiente, ad esempio *mydw-westus-1-test*.</span><span class="sxs-lookup"><span data-stu-id="81181-135">If you have multiple data warehouses, we recommend your names include details such as hello region, environment, for example *mydw-westus-1-test*.</span></span>

    <span data-ttu-id="81181-136">**Sottoscrizione**: sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81181-136">**Subscription**: Your Azure subscription</span></span>

    <span data-ttu-id="81181-137">**Gruppo di risorse**: creare un gruppo di risorse o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="81181-137">**Resource Group**: Create a resource group or use an existing resource group.</span></span>
    > [!NOTE]
    > <span data-ttu-id="81181-138">I gruppi di risorse sono utili per l'amministrazione delle risorse, ad esempio per la definizione dell'ambito del controllo di accesso e per la distribuzione basata su modelli.</span><span class="sxs-lookup"><span data-stu-id="81181-138">Resource groups are useful for resource administration such as scoping access control and templated deployment.</span></span> <span data-ttu-id="81181-139">Per altre informazioni sui gruppi di risorse di Azure e sulle procedure consigliate, vedere [qui](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span><span class="sxs-lookup"><span data-stu-id="81181-139">Read more about Azure resource groups and best practices [here](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups)</span></span>

    <span data-ttu-id="81181-140">**Origine**: database vuoto.</span><span class="sxs-lookup"><span data-stu-id="81181-140">**Source**: Blank Database</span></span>

    <span data-ttu-id="81181-141">**Server**: creato nel server di selezionare hello [prerequisiti].</span><span class="sxs-lookup"><span data-stu-id="81181-141">**Server**: Select hello server you created in [Prerequisites].</span></span>

    <span data-ttu-id="81181-142">**Regole di confronto**: lasciare regole di confronto predefinite hello SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="81181-142">**Collation**: Leave hello default collation SQL_Latin1_General_CP1_CI_AS.</span></span>

    <span data-ttu-id="81181-143">**Selezionare prestazioni**: È consigliabile iniziare con 400DWU standard hello.</span><span class="sxs-lookup"><span data-stu-id="81181-143">**Select performance**: We recommend starting with hello standard 400DWU.</span></span>

4. <span data-ttu-id="81181-144">Scegliere **Pin toodashboard** ![tooDashboard Pin](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="81181-144">Choose **Pin toodashboard** ![Pin tooDashboard](./media/sql-data-warehouse-get-started-tutorial/pin-to-dashboard.png)</span></span>

5. <span data-ttu-id="81181-145">Tranquillamente e attendere il toodeploy warehouse dati!</span><span class="sxs-lookup"><span data-stu-id="81181-145">Sit back and wait for your data warehouse toodeploy!</span></span> <span data-ttu-id="81181-146">È norma per questo processo tootake alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="81181-146">It's normal for this process tootake several minutes.</span></span> <span data-ttu-id="81181-147">portale Hello notifica quando il data warehouse è toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="81181-147">hello portal notifies you when your data warehouse is ready toouse.</span></span> 

## <a name="connect-toosql-data-warehouse"></a><span data-ttu-id="81181-148">Connettersi tooSQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="81181-148">Connect tooSQL Data Warehouse</span></span>

<span data-ttu-id="81181-149">In questa esercitazione utilizza SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-149">This tutorial uses SQL Server Management Studio (SSMS) tooconnect toohello data warehouse.</span></span> <span data-ttu-id="81181-150">È possibile connettere tooSQL Data Warehouse tramite questi connettori supportati: ADO.NET, JDBC, ODBC e PHP.</span><span class="sxs-lookup"><span data-stu-id="81181-150">You can connect tooSQL Data Warehouse through these supported connectors: ADO.NET, JDBC, ODBC, and PHP.</span></span> <span data-ttu-id="81181-151">È possibile che le funzionalità siano limitate per gli strumenti non supportati da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="81181-151">Remember, functionality might be limited for tools that are not supported by Microsoft.</span></span>


### <a name="get-connection-information"></a><span data-ttu-id="81181-152">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="81181-152">Get connection information</span></span>

<span data-ttu-id="81181-153">data warehouse di tooconnect tooyour, è necessario tooconnect tramite hello logico SQL server è stato creato in [prerequisiti].</span><span class="sxs-lookup"><span data-stu-id="81181-153">tooconnect tooyour data warehouse, you need tooconnect through hello logical SQL server you created in [Prerequisites].</span></span>

1. <span data-ttu-id="81181-154">Selezionare il data warehouse dal dashboard di hello o cercare le risorse.</span><span class="sxs-lookup"><span data-stu-id="81181-154">Select your data warehouse from hello dashboard or search for it in your resources.</span></span>

    ![Dashboard di SQL Data Warehouse](./media/sql-data-warehouse-get-started-tutorial/sql-dw-dashboard.png)

2. <span data-ttu-id="81181-156">Trovare il nome completo di hello per server SQL logico hello.</span><span class="sxs-lookup"><span data-stu-id="81181-156">Find hello full name for hello logical SQL server.</span></span>

    ![Selezionare il nome del server](./media/sql-data-warehouse-get-started-tutorial/select-server.png)

3. <span data-ttu-id="81181-158">Aprire SQL Server Management Studio e utilizzare un oggetto explorer tooconnect toothis server usando credenziali di amministratore server hello è stato creato in [prerequisiti]</span><span class="sxs-lookup"><span data-stu-id="81181-158">Open SSMS and use object explorer tooconnect toothis server using hello server admin credentials you created in [Prerequisites]</span></span>

    ![Connettersi con SSMS](./media/sql-data-warehouse-get-started-tutorial/ssms-connect.png)

<span data-ttu-id="81181-160">Se viene eseguito correttamente, è ora connesso tooyour logico SQL server.</span><span class="sxs-lookup"><span data-stu-id="81181-160">If all goes correctly, you should now be connected tooyour logical SQL server.</span></span> <span data-ttu-id="81181-161">Poiché è stato eseguito l'accesso hello amministratore del server, è possibile connettersi a database tooany ospitato dal server di hello, tra cui database master hello.</span><span class="sxs-lookup"><span data-stu-id="81181-161">Since you logged in as hello server admin, you can connect tooany database hosted by hello server, including hello master database.</span></span> 

<span data-ttu-id="81181-162">Account di amministratore di un solo server e dispone di hello la maggior parte dei privilegi di qualsiasi utente.</span><span class="sxs-lookup"><span data-stu-id="81181-162">There is only one server admin account and it has hello most privileges of any user.</span></span> <span data-ttu-id="81181-163">Prestare attenzione tooallow non Troppi utenti la password di amministratore dell'organizzazione tooknow hello.</span><span class="sxs-lookup"><span data-stu-id="81181-163">Be careful not tooallow too many people in your organization tooknow hello admin password.</span></span> 

<span data-ttu-id="81181-164">È anche possibile usare un account di amministratore di Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="81181-164">You can also have an Azure active directory admin account.</span></span> <span data-ttu-id="81181-165">Microsoft non fornire qui i dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-165">We don't provide hello details here.</span></span> <span data-ttu-id="81181-166">Se si desidera toolearn ulteriori informazioni sull'utilizzo di autenticazione di Azure Active Directory, vedere [autenticazione di Azure AD](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span><span class="sxs-lookup"><span data-stu-id="81181-166">If you want toolearn more about using Azure Active Directory authentication, see [Azure AD authentication](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).</span></span>

<span data-ttu-id="81181-167">Verrà ora illustrata la creazione di altri account di accesso e utenti.</span><span class="sxs-lookup"><span data-stu-id="81181-167">Next, we explore creating additional logins and users.</span></span>


## <a name="create-a-database-user"></a><span data-ttu-id="81181-168">Creare un utente database</span><span class="sxs-lookup"><span data-stu-id="81181-168">Create a database user</span></span>

<span data-ttu-id="81181-169">In questo passaggio viene creato un tooaccess di account utente del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-169">In this step, you create a user account tooaccess your data warehouse.</span></span> <span data-ttu-id="81181-170">Viene inoltre illustrata la modalità toogive toorun di possibilità hello tale utente esegue una query con una grande quantità di memoria e risorse della CPU.</span><span class="sxs-lookup"><span data-stu-id="81181-170">We also show you how toogive that user hello ability toorun queries with a large amount of memory and CPU resources.</span></span>

### <a name="notes-about-resource-classes-for-allocating-resources-tooqueries"></a><span data-ttu-id="81181-171">Note sulle classi di risorse per l'allocazione delle risorse tooqueries</span><span class="sxs-lookup"><span data-stu-id="81181-171">Notes about resource classes for allocating resources tooqueries</span></span>

- <span data-ttu-id="81181-172">tookeep dati sicuri, non utilizzare query toorun amministratore del server hello nei database di produzione.</span><span class="sxs-lookup"><span data-stu-id="81181-172">tookeep your data safe, don't use hello server admin toorun queries on your production databases.</span></span> <span data-ttu-id="81181-173">Ha hello la maggior parte dei privilegi di qualsiasi utente e utilizzarlo tooperform operazioni sui dati utente inserisce i dati a rischio.</span><span class="sxs-lookup"><span data-stu-id="81181-173">It has hello most privileges of any user and using it tooperform operations on user data puts your data at risk.</span></span> <span data-ttu-id="81181-174">Inoltre, poiché l'amministratore del server hello deve tooperform le operazioni di gestione, viene eseguito operazioni con solo una piccola allocazione di memoria e risorse della CPU.</span><span class="sxs-lookup"><span data-stu-id="81181-174">Also, since hello server admin is meant tooperform management operations, it runs operations with only a small allocation of memory and CPU resources.</span></span> 

- <span data-ttu-id="81181-175">SQL Data Warehouse vengono utilizzati i ruoli di database predefiniti, chiamata tooallocate quantità di memoria, le risorse della CPU e concorrenza slot toousers diverse classi di risorse.</span><span class="sxs-lookup"><span data-stu-id="81181-175">SQL Data Warehouse uses pre-defined database roles, called resource classes, tooallocate different amounts of memory, CPU resources, and concurrency slots toousers.</span></span> <span data-ttu-id="81181-176">Ogni utente può appartenere a classe di risorse di piccola, Media, grande o molto grande tooa.</span><span class="sxs-lookup"><span data-stu-id="81181-176">Each user can belong tooa small, medium, large, or extra-large resource class.</span></span> <span data-ttu-id="81181-177">Hello classe di risorse dell'utente determina hello risorse hello utente è toorun query e operazioni di caricamento.</span><span class="sxs-lookup"><span data-stu-id="81181-177">hello user's resource class determines hello resources hello user has toorun queries and load operations.</span></span>

- <span data-ttu-id="81181-178">Per la compressione dati ottimale, utente hello potrebbe essere necessario tooload di grandi dimensioni o allocazioni di dimensioni molto grandi.</span><span class="sxs-lookup"><span data-stu-id="81181-178">For optimal data compression, hello user may need tooload with large or extra large resource allocations.</span></span> <span data-ttu-id="81181-179">Per altre informazioni sulle classi di risorse, vedere [qui](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span><span class="sxs-lookup"><span data-stu-id="81181-179">Read more about resource classes [here](./sql-data-warehouse-develop-concurrency.md#resource-classes):</span></span>

### <a name="create-an-account-that-can-control-a-database"></a><span data-ttu-id="81181-180">Creare un account che possa controllare un database</span><span class="sxs-lookup"><span data-stu-id="81181-180">Create an account that can control a database</span></span>

<span data-ttu-id="81181-181">Poiché si è connessi in hello amministratore del server è necessario utenti e accessi toocreate autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="81181-181">Since you are currently logged in as hello server admin you have permissions toocreate logins and users.</span></span>

1. <span data-ttu-id="81181-182">Usando SSMS o un altro client di query, aprire una nuova query per **master**.</span><span class="sxs-lookup"><span data-stu-id="81181-182">Using SSMS or another query client, open a new query for **master**.</span></span>

    ![Nuova query nel master](./media/sql-data-warehouse-get-started-tutorial/query-on-server.png)

    ![Nuova query nel master 1](./media/sql-data-warehouse-get-started-tutorial/query-on-master.png)

2. <span data-ttu-id="81181-185">Nella finestra query hello, eseguire questo toocreate comando T-SQL, un account di accesso denominato MedRCLogin e un utente denominato LoadingUser.</span><span class="sxs-lookup"><span data-stu-id="81181-185">In hello query window, run this T-SQL command toocreate a login named MedRCLogin and user named LoadingUser.</span></span> <span data-ttu-id="81181-186">Questo account di accesso può connettersi toohello logico SQL server.</span><span class="sxs-lookup"><span data-stu-id="81181-186">This login can connect toohello logical SQL server.</span></span>

    ```sql
    CREATE LOGIN MedRCLogin WITH PASSWORD = 'a123reallySTRONGpassword!';
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

3. <span data-ttu-id="81181-187">Ora l'esecuzione di query hello *database SQL Data Warehouse*, creare un utente del database basato su account di accesso creato tooaccess hello ed eseguire operazioni sul database hello.</span><span class="sxs-lookup"><span data-stu-id="81181-187">Now querying hello *SQL Data Warehouse database*, create a database user based on hello login you created tooaccess and perform operations on hello database.</span></span>

    ```sql
    CREATE USER LoadingUser FOR LOGIN MedRCLogin;
    ```

4. <span data-ttu-id="81181-188">Assegnare hello database controllo autorizzazioni toohello database utente denominato NYT.</span><span class="sxs-lookup"><span data-stu-id="81181-188">Give hello database user control permissions toohello database called NYT.</span></span> 

    ```sql
    GRANT CONTROL ON DATABASE::[NYT] tooLoadingUser;
    ```
    > [!NOTE]
    > <span data-ttu-id="81181-189">Se il nome del database contiene segni meno, toowrap assicurarsi di essere in parentesi quadre.</span><span class="sxs-lookup"><span data-stu-id="81181-189">If your database name has hyphens in it, be sure toowrap it in brackets!</span></span> 
    >

### <a name="give-hello-user-medium-resource-allocations"></a><span data-ttu-id="81181-190">Assegnare le allocazioni di hello utente medio di risorse</span><span class="sxs-lookup"><span data-stu-id="81181-190">Give hello user medium resource allocations</span></span>

1. <span data-ttu-id="81181-191">Eseguire questo toomake comando T-SQL it un membro della classe di risorse medium hello, che viene chiamato mediumrc.</span><span class="sxs-lookup"><span data-stu-id="81181-191">Run this T-SQL command toomake it a member of hello medium resource class, which is called mediumrc.</span></span> 

    ```sql
    EXEC sp_addrolemember 'mediumrc', 'LoadingUser';
    ```
    > [!NOTE]
    > <span data-ttu-id="81181-192">Fare clic su [qui](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn ulteriori informazioni sulle classi di concorrenza e la risorsa.</span><span class="sxs-lookup"><span data-stu-id="81181-192">Click [here](sql-data-warehouse-develop-concurrency.md#resource-classes) toolearn more about concurrency and resource classes!</span></span> 
    >

2. <span data-ttu-id="81181-193">Connessione server logico toohello con nuove credenziali hello</span><span class="sxs-lookup"><span data-stu-id="81181-193">Connect toohello logical server with hello new credentials</span></span>

    ![Accedere con il nuovo account](./media/sql-data-warehouse-get-started-tutorial/new-login.png)


## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="81181-195">Caricare dati dall'archiviazione BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="81181-195">Load data from Azure blob storage</span></span>

<span data-ttu-id="81181-196">Si è ora dati tooload pronto in data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-196">You are now ready tooload data into your data warehouse.</span></span> <span data-ttu-id="81181-197">Questo passaggio illustra come blob di dati di file cab di tooload New York City taxi da un'archiviazione di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="81181-197">This step shows you how tooload New York City taxi cab data from a public Azure storage blob.</span></span> 

- <span data-ttu-id="81181-198">Un modo comune dati tooload in SQL Data Warehouse sono toofirst spostare risorse di archiviazione blob tooAzure dati hello e caricarla in un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-198">A common way tooload data into SQL Data Warehouse is toofirst move hello data tooAzure blob storage, and then load it into your data warehouse.</span></span> <span data-ttu-id="81181-199">toomake è più facile toounderstand come tooload, sono disponibili dati di file cab taxi New York già ospitati in un blob di archiviazione di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="81181-199">toomake it easier toounderstand how tooload, we have New York taxi cab data already hosted in a public Azure storage blob.</span></span> 

- <span data-ttu-id="81181-200">Per riferimento futuro, toolearn come tooget tooAzure i dati blob di archiviazione o tooload direttamente dall'origine in SQL Data Warehouse, vedere hello [durante il caricamento di panoramica](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="81181-200">For future reference, toolearn how tooget your data tooAzure blob storage or tooload it directly from your source into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>


### <a name="define-external-data"></a><span data-ttu-id="81181-201">Definire i dati esterni</span><span class="sxs-lookup"><span data-stu-id="81181-201">Define external data</span></span>

1. <span data-ttu-id="81181-202">Creare una chiave master.</span><span class="sxs-lookup"><span data-stu-id="81181-202">Create a master key.</span></span> <span data-ttu-id="81181-203">È necessario solo toocreate una chiave master una sola volta per ogni database.</span><span class="sxs-lookup"><span data-stu-id="81181-203">You only need toocreate a master key once per database.</span></span> 

    ```sql
    CREATE MASTER KEY;
    ```

2. <span data-ttu-id="81181-204">Definire il percorso di hello del blob di Azure che contiene i dati di file cab taxi hello hello.</span><span class="sxs-lookup"><span data-stu-id="81181-204">Define hello location of hello Azure blob that contains hello taxi cab data.</span></span>  

    ```sql
    CREATE EXTERNAL DATA SOURCE NYTPublic
    WITH
    (
        TYPE = Hadoop,
        LOCATION = 'wasbs://2013@nytpublic.blob.core.windows.net/'
    );
    ```

3. <span data-ttu-id="81181-205">Definire i formati di file esterni hello</span><span class="sxs-lookup"><span data-stu-id="81181-205">Define hello external file formats</span></span>

    <span data-ttu-id="81181-206">Hello ```CREATE EXTERNAL FILE FORMAT``` comando è toospecify utilizzato il formato di file che contengono dati esterni hello.</span><span class="sxs-lookup"><span data-stu-id="81181-206">hello ```CREATE EXTERNAL FILE FORMAT``` command is used toospecify the format of files that contain hello external data.</span></span> <span data-ttu-id="81181-207">Questi file includono testo delimitato da uno o più caratteri, definiti delimitatori.</span><span class="sxs-lookup"><span data-stu-id="81181-207">They contain text separated by one or more characters called delimiters.</span></span> <span data-ttu-id="81181-208">A scopo dimostrativo, i dati di file cab di hello taxi vengono archiviati come dati non compressi e come dati compressi gzip.</span><span class="sxs-lookup"><span data-stu-id="81181-208">For demonstration purposes, hello taxi cab data is stored both as uncompressed data and as gzip compressed data.</span></span>

    <span data-ttu-id="81181-209">Eseguire questi comandi di T-SQL toodefine due formati: non compressi e compressi.</span><span class="sxs-lookup"><span data-stu-id="81181-209">Run these T-SQL commands toodefine two different formats: uncompressed and compressed.</span></span>

    ```sql
    CREATE EXTERNAL FILE FORMAT uncompressedcsv
    WITH (
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( 
            FIELD_TERMINATOR = ',',
            STRING_DELIMITER = '',
            DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        )
    );

    CREATE EXTERNAL FILE FORMAT compressedcsv
    WITH ( 
        FORMAT_TYPE = DELIMITEDTEXT,
        FORMAT_OPTIONS ( FIELD_TERMINATOR = '|',
            STRING_DELIMITER = '',
        DATE_FORMAT = '',
            USE_TYPE_DEFAULT = False
        ),
        DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
    );
    ```

4.  <span data-ttu-id="81181-210">Creare uno schema per il formato di file esterni.</span><span class="sxs-lookup"><span data-stu-id="81181-210">Create a schema for your external file format.</span></span> 

    ```sql
    CREATE SCHEMA ext;
    ```
5. <span data-ttu-id="81181-211">Creare tabelle esterne di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-211">Create hello external tables.</span></span> <span data-ttu-id="81181-212">Queste tabelle fanno riferimento a dati archiviati nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="81181-212">These tables reference data stored in Azure blob storage.</span></span> <span data-ttu-id="81181-213">Eseguire hello toocreate comandi T-SQL seguente diverse tabelle esterne che toohello punto tutti i blob di Azure è stato definito in precedenza nell'origine dati esterna.</span><span class="sxs-lookup"><span data-stu-id="81181-213">Run hello following T-SQL commands toocreate several external tables that all point toohello Azure blob we defined previously in our external data source.</span></span>

```sql
    CREATE EXTERNAL TABLE [ext].[Date] 
    (
        [DateID] int NOT NULL,
        [Date] datetime NULL,
        [DateBKey] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DaySuffix] varchar(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeek] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInMonth] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfWeekInYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfQuarter] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DayOfYear] varchar(3) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfMonth] varchar(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [WeekOfYear] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Month] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthOfQuarter] varchar(2) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Quarter] char(1) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [QuarterName] varchar(9) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Year] char(4) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [YearName] char(7) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MonthYear] char(10) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [MMYYYY] char(6) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FirstDayOfMonth] date NULL,
        [LastDayOfMonth] date NULL,
        [FirstDayOfQuarter] date NULL,
        [LastDayOfQuarter] date NULL,
        [FirstDayOfYear] date NULL,
        [LastDayOfYear] date NULL,
        [IsHolidayUSA] bit NULL,
        [IsWeekday] bit NULL,
        [HolidayUSA] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Date',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    );
    
    CREATE EXTERNAL TABLE [ext].[Geography]
    (
        [GeographyID] int NOT NULL,
        [ZipCodeBKey] varchar(10) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [County] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [City] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [State] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [Country] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [ZipCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Geography',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0 
    );
        
    
    CREATE EXTERNAL TABLE [ext].[HackneyLicense]
    (
        [HackneyLicenseID] int NOT NULL,
        [HackneyLicenseBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HackneyLicenseCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'HackneyLicense',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    
    CREATE EXTERNAL TABLE [ext].[Medallion]
    (
        [MedallionID] int NOT NULL,
        [MedallionBKey] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [MedallionCode] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL
    )
    WITH
    (
        LOCATION = 'Medallion',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
        
    CREATE EXTERNAL TABLE [ext].[Time]
    (
        [TimeID] int NOT NULL,
        [TimeBKey] varchar(8) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [HourNumber] tinyint NOT NULL,
        [MinuteNumber] tinyint NOT NULL,
        [SecondNumber] tinyint NOT NULL,
        [TimeInSecond] int NOT NULL,
        [HourlyBucket] varchar(15) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL,
        [DayTimeBucketGroupKey] int NOT NULL,
        [DayTimeBucket] varchar(100) COLLATE SQL_Latin1_General_CP1_CI_AS NOT NULL
    )
    WITH
    (
        LOCATION = 'Time',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    
    CREATE EXTERNAL TABLE [ext].[Trip]
    (
        [DateID] int NOT NULL,
        [MedallionID] int NOT NULL,
        [HackneyLicenseID] int NOT NULL,
        [PickupTimeID] int NOT NULL,
        [DropoffTimeID] int NOT NULL,
        [PickupGeographyID] int NULL,
        [DropoffGeographyID] int NULL,
        [PickupLatitude] float NULL,
        [PickupLongitude] float NULL,
        [PickupLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [DropoffLatitude] float NULL,
        [DropoffLongitude] float NULL,
        [DropoffLatLong] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [PassengerCount] int NULL,
        [TripDurationSeconds] int NULL,
        [TripDistanceMiles] float NULL,
        [PaymentType] varchar(50) COLLATE SQL_Latin1_General_CP1_CI_AS NULL,
        [FareAmount] money NULL,
        [SurchargeAmount] money NULL,
        [TaxAmount] money NULL,
        [TipAmount] money NULL,
        [TollsAmount] money NULL,
        [TotalAmount] money NULL
    )
    WITH
    (
        LOCATION = 'Trip2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = compressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
    
    CREATE EXTERNAL TABLE [ext].[Weather]
    (
        [DateID] int NOT NULL,
        [GeographyID] int NOT NULL,
        [PrecipitationInches] float NOT NULL,
        [AvgTemperatureFahrenheit] float NOT NULL
    )
    WITH
    (
        LOCATION = 'Weather2013',
        DATA_SOURCE = NYTPublic,
        FILE_FORMAT = uncompressedcsv,
        REJECT_TYPE = value,
        REJECT_VALUE = 0
    )
    ;
```

### <a name="import-hello-data-from-azure-blob-storage"></a><span data-ttu-id="81181-214">Importare dati hello dall'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="81181-214">Import hello data from Azure blob storage.</span></span>

<span data-ttu-id="81181-215">SQL Data Warehouse supporta un'istruzione chiave denominata CREATE TABLE AS SELECT (CTAS).</span><span class="sxs-lookup"><span data-stu-id="81181-215">SQL Data Warehouse supports a key statement called CREATE TABLE AS SELECT (CTAS).</span></span> <span data-ttu-id="81181-216">Questa istruzione crea una nuova tabella in base ai risultati di hello di un'istruzione select.</span><span class="sxs-lookup"><span data-stu-id="81181-216">This statement creates a new table based on hello results of a select statement.</span></span> <span data-ttu-id="81181-217">Hello nuova tabella include hello stessi colonne e tipi di dati come risultato di hello hello istruzione select.</span><span class="sxs-lookup"><span data-stu-id="81181-217">hello new table has hello same columns and data types as hello results of hello select statement.</span></span>  <span data-ttu-id="81181-218">Si tratta di un dati tooimport modo elegante dall'archiviazione blob di Azure in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-218">This is an elegant way tooimport data from Azure blob storage into SQL Data Warehouse.</span></span>

1. <span data-ttu-id="81181-219">Eseguire questo script tooimport i dati.</span><span class="sxs-lookup"><span data-stu-id="81181-219">Run this script tooimport your data.</span></span>

    ```sql
    CREATE TABLE [dbo].[Date]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Date]
    OPTION (LABEL = 'CTAS : Load [dbo].[Date]')
    ;
    
    CREATE TABLE [dbo].[Geography]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS
    SELECT * FROM [ext].[Geography]
    OPTION (LABEL = 'CTAS : Load [dbo].[Geography]')
    ;
    
    CREATE TABLE [dbo].[HackneyLicense]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[HackneyLicense]
    OPTION (LABEL = 'CTAS : Load [dbo].[HackneyLicense]')
    ;
    
    CREATE TABLE [dbo].[Medallion]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Medallion]
    OPTION (LABEL = 'CTAS : Load [dbo].[Medallion]')
    ;
    
    CREATE TABLE [dbo].[Time]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Time]
    OPTION (LABEL = 'CTAS : Load [dbo].[Time]')
    ;
    
    CREATE TABLE [dbo].[Weather]
    WITH
    ( 
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Weather]
    OPTION (LABEL = 'CTAS : Load [dbo].[Weather]')
    ;
    
    CREATE TABLE [dbo].[Trip]
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    AS SELECT * FROM [ext].[Trip]
    OPTION (LABEL = 'CTAS : Load [dbo].[Trip]')
    ;
    ```

2. <span data-ttu-id="81181-220">Visualizzare i dati man mano che vengono caricati.</span><span class="sxs-lookup"><span data-stu-id="81181-220">View your data as it loads.</span></span>

   <span data-ttu-id="81181-221">Vengono caricati alcuni GB di dati, che vengono compressi in indici cluster columnstore a prestazioni elevate.</span><span class="sxs-lookup"><span data-stu-id="81181-221">You’re loading several GBs of data and compressing it into highly performant clustered columnstore indexes.</span></span> <span data-ttu-id="81181-222">Eseguire hello seguente query che utilizza uno stato di hello tooshow viste a gestione dinamica del carico hello.</span><span class="sxs-lookup"><span data-stu-id="81181-222">Run hello following query that uses a dynamic management views (DMVs) tooshow hello status of hello load.</span></span> <span data-ttu-id="81181-223">Dopo avere avviato la query hello, trascinare un caffè e un allenamento mentre SQL Data Warehouse non alcuni pesante.</span><span class="sxs-lookup"><span data-stu-id="81181-223">After starting hello query, grab a coffee and a snack while SQL Data Warehouse does some heavy lifting.</span></span>
    
    ```sql
    SELECT
        r.command,
        s.request_id,
        r.status,
        count(distinct input_name) as nbr_files,
        sum(s.bytes_processed)/1024/1024/1024 as gb_processed
    FROM 
        sys.dm_pdw_exec_requests r
        INNER JOIN sys.dm_pdw_dms_external_work s
        ON r.request_id = s.request_id
    WHERE
        r.[label] = 'CTAS : Load [dbo].[Date]' OR
        r.[label] = 'CTAS : Load [dbo].[Geography]' OR
        r.[label] = 'CTAS : Load [dbo].[HackneyLicense]' OR
        r.[label] = 'CTAS : Load [dbo].[Medallion]' OR
        r.[label] = 'CTAS : Load [dbo].[Time]' OR
        r.[label] = 'CTAS : Load [dbo].[Weather]' OR
        r.[label] = 'CTAS : Load [dbo].[Trip]'
    GROUP BY
        r.command,
        s.request_id,
        r.status
    ORDER BY
        nbr_files desc, 
        gb_processed desc;
    ```

3. <span data-ttu-id="81181-224">Visualizzare tutte le query di sistema.</span><span class="sxs-lookup"><span data-stu-id="81181-224">View all system queries.</span></span>

    ```sql
    SELECT * FROM sys.dm_pdw_exec_requests;
    ```

4. <span data-ttu-id="81181-225">I dati vengono caricati in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-225">Enjoy seeing your data nicely loaded into your Azure SQL Data Warehouse.</span></span>

    ![Visualizzare i dati caricati](./media/sql-data-warehouse-get-started-tutorial/see-data-loaded.png)


## <a name="improve-query-performance"></a><span data-ttu-id="81181-227">Ottimizzare le prestazioni di query</span><span class="sxs-lookup"><span data-stu-id="81181-227">Improve query performance</span></span>

<span data-ttu-id="81181-228">Esistono diversi le prestazioni delle query tooimprove modi e tooachieve hello velocità delle prestazioni di SQL Data Warehouse progettato tooprovide.</span><span class="sxs-lookup"><span data-stu-id="81181-228">There are several ways tooimprove query performance and tooachieve hello high-speed performance that SQL Data Warehouse is designed tooprovide.</span></span>  

### <a name="see-hello-effect-of-scaling-on-query-performance"></a><span data-ttu-id="81181-229">Vedere l'effetto di hello dell'aumento delle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="81181-229">See hello effect of scaling on query performance</span></span> 

<span data-ttu-id="81181-230">Le prestazioni delle query tooimprove unidirezionale sono tooscale risorse modificando hello DWU servizio livello per il data warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-230">One way tooimprove query performance is tooscale resources by changing hello DWU service level for your data warehouse.</span></span> <span data-ttu-id="81181-231">Ogni livello di servizio ha un costo maggiore, ma è possibile ridurre o sospendere le risorse in qualsiasi momento.</span><span class="sxs-lookup"><span data-stu-id="81181-231">Each service level costs more, but you can scale back or pause resources at any time.</span></span> 

<span data-ttu-id="81181-232">In questo passaggio si confrontano le prestazioni in due diverse impostazioni DWU.</span><span class="sxs-lookup"><span data-stu-id="81181-232">In this step, you compare performance at two different DWU settings.</span></span>

<span data-ttu-id="81181-233">Innanzitutto, consente di ridimensionare ridimensionamento hello verso il basso too100 DWU in modo è possibile ottenere un'idea di come un nodo di calcolo potrebbe eseguire autonomamente.</span><span class="sxs-lookup"><span data-stu-id="81181-233">First, let's scale hello sizing down too100 DWU so we can get an idea of how one compute node might perform on its own.</span></span>

1. <span data-ttu-id="81181-234">Passare toohello portale e selezionare il Data Warehouse di SQL.</span><span class="sxs-lookup"><span data-stu-id="81181-234">Go toohello portal and select your SQL Data Warehouse.</span></span>

2. <span data-ttu-id="81181-235">Selezione scala nel Pannello di hello SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-235">Select scale in hello SQL Data Warehouse blade.</span></span> 

    ![Ridimensionare SQL Data Warehouse dal portale](./media/sql-data-warehouse-get-started-tutorial/scale-dw.png)

3. <span data-ttu-id="81181-237">Riscontri di salvataggio e ridurre le prestazioni di hello barra too100 DWU.</span><span class="sxs-lookup"><span data-stu-id="81181-237">Scale down hello performance bar too100 DWU and hit save.</span></span>

    ![Ridimensionare e salvare](./media/sql-data-warehouse-get-started-tutorial/scale-and-save.png)

4. <span data-ttu-id="81181-239">Attendere il toofinish operazione di scala.</span><span class="sxs-lookup"><span data-stu-id="81181-239">Wait for your scale operation toofinish.</span></span>

    > [!NOTE]
    > <span data-ttu-id="81181-240">Non è possibile eseguire query durante la modifica scala hello.</span><span class="sxs-lookup"><span data-stu-id="81181-240">Queries cannot run while changing hello scale.</span></span> <span data-ttu-id="81181-241">Il ridimensionamento **termina** tutte le query attualmente in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="81181-241">Scaling **kills** your currently running queries.</span></span> <span data-ttu-id="81181-242">È possibile riavviarle al termine dell'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-242">You can restart them when hello operation is finished.</span></span>
    >
    
5. <span data-ttu-id="81181-243">Eseguire un'operazione di analisi sui dati di andata e ritorno hello, selezionando hello milioni voci superiore per tutte le colonne di hello.</span><span class="sxs-lookup"><span data-stu-id="81181-243">Do a scan operation on hello trip data, selecting hello top million entries for all hello columns.</span></span> <span data-ttu-id="81181-244">Se si è rapidamente toomove eager su, è disponibile tooselect meno righe.</span><span class="sxs-lookup"><span data-stu-id="81181-244">If you're eager toomove on quickly, feel free tooselect fewer rows.</span></span> <span data-ttu-id="81181-245">Prendere nota di hello tempo toorun questa operazione.</span><span class="sxs-lookup"><span data-stu-id="81181-245">Take note of hello time it takes toorun this operation.</span></span>

    ```sql
    SELECT TOP(1000000) * FROM dbo.[Trip]
    ```
6. <span data-ttu-id="81181-246">Ridimensionare il data warehouse di eseguire il backup too400 DWU.</span><span class="sxs-lookup"><span data-stu-id="81181-246">Scale your data warehouse back too400 DWU.</span></span> <span data-ttu-id="81181-247">Tenere presente che ogni 100 DWU consiste nell'aggiunta di un altro calcolo nodo tooyour Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-247">Remember, each 100 DWU is adding another compute node tooyour Azure SQL Data Warehouse.</span></span>

7. <span data-ttu-id="81181-248">Eseguire di nuovo la query hello!</span><span class="sxs-lookup"><span data-stu-id="81181-248">Run hello query again!</span></span> <span data-ttu-id="81181-249">La differenza dovrebbe essere significativa.</span><span class="sxs-lookup"><span data-stu-id="81181-249">You should notice a significant difference.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="81181-250">Poiché query hello restituisce una grande quantità di dati, la disponibilità di larghezza di banda hello della macchina di hello in esecuzione SQL Server Management Studio potrebbe essere un collo di bottiglia delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="81181-250">Because hello query returns a lot of data, hello bandwidth availability of hello machine running SSMS may be a performance bottleneck.</span></span> <span data-ttu-id="81181-251">e ciò potrebbe impedire di notare miglioramenti delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="81181-251">This can result in you not seeing any performance improvements!</span></span>

> [!NOTE]
> <span data-ttu-id="81181-252">Questo perché SQL Data Warehouse fa uso dell'elaborazione parallela massiva (Massively Parallel Processing, MPP).</span><span class="sxs-lookup"><span data-stu-id="81181-252">Since SQL Data Warehouse uses massively parallel processing.</span></span> <span data-ttu-id="81181-253">Le query che analizzano o eseguono le funzioni analitiche milioni di righe potenza hello true di Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="81181-253">Queries that scan or perform analytic functions on millions of rows experience hello true power of Azure SQL Data Warehouse.</span></span>
>

### <a name="see-hello-effect-of-statistics-on-query-performance"></a><span data-ttu-id="81181-254">Vedere l'effetto di hello delle statistiche sulle prestazioni delle query</span><span class="sxs-lookup"><span data-stu-id="81181-254">See hello effect of statistics on query performance</span></span>

1. <span data-ttu-id="81181-255">Eseguire una query che join hello tabella data con la tabella di andata e ritorno di hello</span><span class="sxs-lookup"><span data-stu-id="81181-255">Run a query that joins hello Date table with hello Trip table</span></span>

    ```sql
    SELECT TOP (1000000) 
        dt.[DayOfWeek],
        tr.[MedallionID],
        tr.[HackneyLicenseID],
        tr.[PickupTimeID],
        tr.[DropoffTimeID],
        tr.[PickupGeographyID],
        tr.[DropoffGeographyID],
        tr.[PickupLatitude],
        tr.[PickupLongitude],
        tr.[PickupLatLong],
        tr.[DropoffLatitude],
        tr.[DropoffLongitude],
        tr.[DropoffLatLong],
        tr.[PassengerCount],
        tr.[TripDurationSeconds],
        tr.[TripDistanceMiles],
        tr.[PaymentType],
        tr.[FareAmount],
        tr.[SurchargeAmount],
        tr.[TaxAmount],
        tr.[TipAmount],
        tr.[TollsAmount],
        tr.[TotalAmount]
    FROM [dbo].[Trip] as tr
        JOIN dbo.[Date] as dt
        ON  tr.DateID = dt.DateID
    ```

    <span data-ttu-id="81181-256">Questa query richiede un certo tempo, in quanto SQL Data Warehouse contiene dati tooshuffle prima di eseguire il join hello.</span><span class="sxs-lookup"><span data-stu-id="81181-256">This query takes a while because SQL Data Warehouse has tooshuffle data before it can perform hello join.</span></span> <span data-ttu-id="81181-257">Join non hanno dati tooshuffle se sono dati progettato toojoin hello allo stesso modo, viene distribuito.</span><span class="sxs-lookup"><span data-stu-id="81181-257">Joins do not have tooshuffle data if they are designed toojoin data in hello same way it is distributed.</span></span> <span data-ttu-id="81181-258">L'argomento non viene approfondito oltre in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="81181-258">That's a deeper subject.</span></span> 

2. <span data-ttu-id="81181-259">Le statistiche fanno la differenza.</span><span class="sxs-lookup"><span data-stu-id="81181-259">Statistics make a difference.</span></span> 
3. <span data-ttu-id="81181-260">Eseguire le statistiche toocreate istruzione sulle colonne di join hello.</span><span class="sxs-lookup"><span data-stu-id="81181-260">Run this statement toocreate statistics on hello join columns.</span></span>

    ```sql
    CREATE STATISTICS [dbo.Date DateID stats] ON dbo.Date (DateID);
    CREATE STATISTICS [dbo.Trip DateID stats] ON dbo.Trip (DateID);
    ```

    > [!NOTE]
    > <span data-ttu-id="81181-261">SQL Data Warehouse non gestisce automaticamente le statistiche.</span><span class="sxs-lookup"><span data-stu-id="81181-261">SQL DW does not automatically manage statistics for you.</span></span> <span data-ttu-id="81181-262">Le statistiche sono importanti per le prestazioni delle query ed è consigliabile creare e aggiornare le statistiche.</span><span class="sxs-lookup"><span data-stu-id="81181-262">Statistics are important for query performance and it is highly recommended you create and update statistics.</span></span>
    > 
    > <span data-ttu-id="81181-263">**La maggior parte dei vantaggi hello si ottengono con le statistiche su colonne coinvolte nel join, le colonne utilizzate nelle hello dove clausola e le colonne disponibili in GROUP BY.**</span><span class="sxs-lookup"><span data-stu-id="81181-263">**You gain hello most benefit by having statistics on columns involved in joins, columns used in hello WHERE clause and columns found in GROUP BY.**</span></span>
    >

3. <span data-ttu-id="81181-264">Eseguire di nuovo query hello dai prerequisiti e osservare le differenze di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="81181-264">Run hello query from Prerequisites again and observe any performance differences.</span></span> <span data-ttu-id="81181-265">Anche se le differenze di hello delle prestazioni delle query non come delicate come la scalabilità verticale, si noterà un velocizzare.</span><span class="sxs-lookup"><span data-stu-id="81181-265">While hello differences in query performance will not be as drastic as scaling up, you should notice a  speed-up.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="81181-266">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81181-266">Next steps</span></span>

<span data-ttu-id="81181-267">È ora pronto tooquery ed esplorare.</span><span class="sxs-lookup"><span data-stu-id="81181-267">You're now ready tooquery and explore.</span></span> <span data-ttu-id="81181-268">Vedere le procedure consigliate o i suggerimenti.</span><span class="sxs-lookup"><span data-stu-id="81181-268">Check out our best practices or tips.</span></span>

<span data-ttu-id="81181-269">Se il termine esplorazione per giorno hello, rendere toopause che l'istanza.</span><span class="sxs-lookup"><span data-stu-id="81181-269">If you're done exploring for hello day, make sure toopause your instance!</span></span> <span data-ttu-id="81181-270">Nell'ambiente di produzione, si può verificare un notevole risparmio per la sospensione e la scalabilità toomeet le esigenze aziendali.</span><span class="sxs-lookup"><span data-stu-id="81181-270">In production, you can experience enormous savings by pausing and scaling toomeet your business needs.</span></span>

![Sospendi](./media/sql-data-warehouse-get-started-tutorial/pause.png)

## <a name="useful-readings"></a><span data-ttu-id="81181-272">Vedere anche</span><span class="sxs-lookup"><span data-stu-id="81181-272">Useful readings</span></span>

<span data-ttu-id="81181-273">[Gestione della concorrenza e del carico di lavoro][]</span><span class="sxs-lookup"><span data-stu-id="81181-273">[Concurrency and Workload Management][]</span></span>

<span data-ttu-id="81181-274">[Procedure consigliate per Azure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="81181-274">[Best practices for Azure SQL Data Warehouse][]</span></span>

<span data-ttu-id="81181-275">[Monitoraggio delle query][]</span><span class="sxs-lookup"><span data-stu-id="81181-275">[Query Monitoring][]</span></span>

<span data-ttu-id="81181-276">[Post di blog Prime 10 procedure consigliate per la creazione di un data warehouse relazionale di dimensioni elevate][]</span><span class="sxs-lookup"><span data-stu-id="81181-276">[Top 10 Best Practices for Building a Large Scale Relational Data Warehouse][]</span></span>

<span data-ttu-id="81181-277">[La migrazione dei dati tooAzure SQL Data Warehouse][]</span><span class="sxs-lookup"><span data-stu-id="81181-277">[Migrating Data tooAzure SQL Data Warehouse][]</span></span>

[Gestione della concorrenza e del carico di lavoro]: sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example
[Procedure consigliate per Azure SQL Data Warehouse]: sql-data-warehouse-best-practices.md#hash-distribute-large-tables
[Monitoraggio delle query]: sql-data-warehouse-manage-monitor.md
[Post di blog Prime 10 procedure consigliate per la creazione di un data warehouse relazionale di dimensioni elevate]: https://blogs.msdn.microsoft.com/sqlcat/2013/09/16/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse/
[La migrazione dei dati tooAzure SQL Data Warehouse]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/



[!INCLUDE [Additional Resources](../../includes/sql-data-warehouse-article-footer.md)]

<!-- Internal Links -->
[prerequisiti]: sql-data-warehouse-get-started-tutorial.md#prerequisites

<!--Other Web references-->
[Visual Studio]: https://www.visualstudio.com/
[SQL Server Management Studio]: https://msdn.microsoft.com/en-us/library/mt238290.aspx
