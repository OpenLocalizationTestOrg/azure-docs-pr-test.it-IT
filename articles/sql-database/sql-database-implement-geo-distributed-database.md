---
title: una soluzione di Database SQL di Azure distribuita geograficamente aaaImplement | Documenti Microsoft
description: Informazioni su tooconfigure il Database SQL di Azure e l'applicazione per il failover tooa replicato database e il test di failover.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="d5c2d-103">Implementare un database con distribuzione geografica</span><span class="sxs-lookup"><span data-stu-id="d5c2d-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="d5c2d-104">In questa esercitazione, configurare un database SQL di Azure e l'applicazione per l'area di failover tooa remoto e quindi testare il piano di failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="d5c2d-105">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="d5c2d-106">Creare utenti del database e concedere loro le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="d5c2d-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="d5c2d-107">Configurare una regola del firewall a livello di database</span><span class="sxs-lookup"><span data-stu-id="d5c2d-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="d5c2d-108">Creare un [gruppo di failover con replica geografica](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5c2d-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="d5c2d-109">Creare e compilare un tooquery applicazione Java un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="d5c2d-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="d5c2d-110">Eseguire un'esercitazione sul ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="d5c2d-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="d5c2d-111">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d5c2d-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d5c2d-112">Prerequisites</span></span>

<span data-ttu-id="d5c2d-113">toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="d5c2d-114">Versione più recente hello installato [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="d5c2d-115">Installazione di un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="d5c2d-116">Questa esercitazione viene utilizzato il database di esempio AdventureWorksLT hello con un nome di **mySampleDatabase** da una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="d5c2d-117">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="d5c2d-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="d5c2d-118">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d5c2d-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="d5c2d-119">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5c2d-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="d5c2d-120">Sono identificati tooexecute un metodo SQL script nel database, è possibile utilizzare uno dei seguenti strumenti di query hello:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="d5c2d-121">editor di query Hello in hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d5c2d-122">Per ulteriori informazioni sull'utilizzo dell'editor di query hello in hello portale di Azure, vedere [Connect e query tramite l'Editor di Query](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="d5c2d-123">versione più recente di Hello di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), che è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server tooSQL Database per Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="d5c2d-124">versione più recente di Hello di [codice di Visual Studio](https://code.visualstudio.com/docs), che è un editor di codice con interfaccia grafica per Linux, macOS, e Windows che supporti le estensioni, tra cui hello [estensione mssql](https://aka.ms/mssql-marketplace) per le query di Microsoft SQL Server , Database SQL di azure e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="d5c2d-125">Per altre informazioni sull'uso di questo strumento con il database SQL di Azure, vedere l'articolo su come [connettersi ed eseguire query con Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="d5c2d-126">Creare utenti del database e concedere autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="d5c2d-126">Create database users and grant permissions</span></span>

<span data-ttu-id="d5c2d-127">La connessione a database tooyour e creare gli account utente utilizzando uno dei seguenti strumenti di query hello:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="d5c2d-128">editor di Query Hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d5c2d-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="d5c2d-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="d5c2d-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="d5c2d-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d5c2d-130">Visual Studio Code</span></span>

<span data-ttu-id="d5c2d-131">Questi account utente vengono automaticamente replicano server secondario tooyour e mantenuti sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="d5c2d-132">toouse SQL Server Management Studio o codice di Visual Studio, potrebbe essere necessario tooconfigure una regola del firewall se ci si connette da un client in un indirizzo IP per il quale non è ancora configurato un firewall.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="d5c2d-133">Per la procedura dettagliata, vedere [Creare una regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="d5c2d-134">In una finestra query, eseguire hello seguente query toocreate due account utente nel database.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="d5c2d-135">Questo script concede **db_owner** autorizzazioni toohello **app_admin** account e concede il **selezionare** e **aggiornamento** toohello autorizzazioni **app_user** account.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="d5c2d-136">Creare il firewall a livello di database</span><span class="sxs-lookup"><span data-stu-id="d5c2d-136">Create database-level firewall</span></span>

<span data-ttu-id="d5c2d-137">Creare una [regola del firewall a livello di database](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) per il database SQL.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="d5c2d-138">La regola del firewall a livello di database vengono replicati automaticamente i server secondari toohello creati in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="d5c2d-139">Per semplicità (in questa esercitazione), utilizzare l'indirizzo IP pubblico hello del computer hello in cui si esegue la procedura hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="d5c2d-140">indirizzo IP di hello toodetermine utilizzato per la regola firewall di livello server hello per il computer corrente, vedere [creare un firewall di livello server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="d5c2d-141">Nella finestra di query aperta, sostituire la query precedente hello con hello query seguente, sostituendo gli indirizzi IP hello con indirizzi IP corretti hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="d5c2d-142">Creare un gruppo di failover automatico con replica geografica attiva</span><span class="sxs-lookup"><span data-stu-id="d5c2d-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="d5c2d-143">Utilizzo di PowerShell di Azure, creare un [gruppo di replica geografica attiva di failover automatico](sql-database-geo-replication-overview.md) tra il server SQL di Azure esistente e i hello nuovo vuote server SQL di Azure in un'area di Azure e quindi aggiungere il gruppo di failover toohello di esempio del database.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5c2d-144">Per questi cmdlet è necessario Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="d5c2d-145">Popolare le variabili per gli script di PowerShell utilizzando valori hello per il server esistente e il database di esempio e fornire un valore univoco globale per nome del gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="d5c2d-146">Creare un server di backup vuoto nell'area di failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="d5c2d-147">Creare un gruppo di failover tra due server hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="d5c2d-148">Aggiungere il gruppo di database toohello failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="d5c2d-149">Installare il software Java</span><span class="sxs-lookup"><span data-stu-id="d5c2d-149">Install Java software</span></span>

<span data-ttu-id="d5c2d-150">passaggi di Hello in questa sezione si presuppone che ha familiarità con lo sviluppo con Java e tooworking Nuovo Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="d5c2d-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="d5c2d-151">**Mac OS**</span></span>
<span data-ttu-id="d5c2d-152">Aprire terminale e spostarsi tooa directory in cui si prevede di creazione del progetto Java.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="d5c2d-153">Installare **brew** e **Maven** immettendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="d5c2d-154">Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**selezionare **MacOS**, quindi seguire Hello indicazioni dettagliate per la configurazione di Java e Maven nel passaggio 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="d5c2d-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="d5c2d-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="d5c2d-156">Aprire terminale e spostarsi tooa directory in cui si prevede di creazione del progetto Java.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="d5c2d-157">Installare **Maven** immettendo hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="d5c2d-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="d5c2d-158">Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**selezionare **Ubuntu**, quindi seguire Hello indicazioni dettagliate per la configurazione di Java e Maven nel passaggio 1.2, 1.3 e 1.4.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="d5c2d-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="d5c2d-159">**Windows**</span></span>
<span data-ttu-id="d5c2d-160">Installare [Maven](https://maven.apache.org/download.cgi) utilizzando Installazione guidata ufficiale hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="d5c2d-161">Utilizzare Maven toohelp di gestire le dipendenze, compilare, testare ed eseguire il progetto Java.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="d5c2d-162">Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**, selezionare Windows e quindi seguire hello istruzioni dettagliate configurazione di Java e Maven nel passaggio 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="d5c2d-163">Creare il progetto SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="d5c2d-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="d5c2d-164">Nella console di comando di hello (ad esempio Bash), creare un progetto di Maven.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="d5c2d-165">Digitare **Y** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="d5c2d-166">Passare alla directory del progetto appena creato.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="d5c2d-167">Usando l'editor preferito, aprire il file di pom.xml hello nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="d5c2d-168">Aggiungere hello Microsoft JDBC Driver per i progetti Maven tooyour dipendenza di SQL Server, aprire un editor di testo e copiare e incollare hello seguenti righe all'interno del file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="d5c2d-169">Non sovrascrivere i valori esistenti di hello già inseriti nel file hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="d5c2d-170">è necessario incollare Hello dipendenza JDBC (sezione) "dipendenze" hello più grande.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="d5c2d-171">Specificare hello versione di Java toocompile hello progetto contro aggiungendo la seguente sezione "proprietà" nel file pom.xml hello dopo la sezione "dipendenze" hello hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="d5c2d-172">Aggiungere la seguente hello "build" sezione nel file pom.xml hello dopo hello "proprietà" sezione toosupport manifesto file JAR.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="d5c2d-173">Salvare e chiudere il file di pom.xml hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="d5c2d-174">Aprire il file App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) e sostituire il contenuto di hello con hello seguente contenuto.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="d5c2d-175">Sostituire hello failover group name con il nome di hello per il gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="d5c2d-176">Se è stato modificato i valori hello per nome del database hello, un utente o password, è possibile modificare anche tali valori.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="d5c2d-177">Salvare e chiudere il file di App.java hello.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="d5c2d-178">Compilare ed eseguire il progetto di SqlDbSample hello</span><span class="sxs-lookup"><span data-stu-id="d5c2d-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="d5c2d-179">Nella console di comando hello, eseguire il comando toofollowing.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="d5c2d-180">Al termine, eseguire hello successivo comando toorun hello applicazione (viene eseguito per circa 1 ora a meno che non è stato interrotto manualmente):</span><span class="sxs-lookup"><span data-stu-id="d5c2d-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="d5c2d-181">Eseguire un'esercitazione sul ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="d5c2d-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="d5c2d-182">Chiamare il failover manuale del gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="d5c2d-183">Osservare i risultati di applicazione hello durante il failover.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-183">Observe hello application results during failover.</span></span> <span data-ttu-id="d5c2d-184">Alcuni inserimenti esito negativo mentre hello cache DNS viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="d5c2d-185">Individuare il ruolo eseguito dal server di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="d5c2d-186">Effettuare il failback.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="d5c2d-187">Osservare i risultati di applicazione hello durante il failback.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-187">Observe hello application results during failback.</span></span> <span data-ttu-id="d5c2d-188">Alcuni inserimenti esito negativo mentre hello cache DNS viene aggiornato.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="d5c2d-189">Individuare il ruolo eseguito dal server di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="d5c2d-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="d5c2d-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d5c2d-190">Next steps</span></span> 

<span data-ttu-id="d5c2d-191">Per altre informazioni, vedere l'articolo relativo a [gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d5c2d-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
