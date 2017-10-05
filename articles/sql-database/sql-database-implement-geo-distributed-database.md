---
title: Implementare una soluzione di database SQL di Azure con distribuzione geografica | Microsoft Docs
description: Informazioni su come configurare il database SQL di Azure e l'applicazione per il failover in un database replicato e su come testare il failover.
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
ms.openlocfilehash: 9f53f318e20dac9248906bdbe898ba4dacb286ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="42e29-103">Implementare un database con distribuzione geografica</span><span class="sxs-lookup"><span data-stu-id="42e29-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="42e29-104">In questa esercitazione vengono configurati un database SQL di Azure e l'applicazione per il failover in un'area remota e viene quindi testato il piano di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-104">In this tutorial, you configure an Azure SQL database and application for failover to a remote region, and then test your failover plan.</span></span> <span data-ttu-id="42e29-105">Si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="42e29-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="42e29-106">Creare utenti del database e concedere loro le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="42e29-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="42e29-107">Configurare una regola del firewall a livello di database</span><span class="sxs-lookup"><span data-stu-id="42e29-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="42e29-108">Creare un [gruppo di failover con replica geografica](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="42e29-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="42e29-109">Creare e compilare un'applicazione Java per eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="42e29-109">Create and compile a Java application to query an Azure SQL database</span></span>
> * <span data-ttu-id="42e29-110">Eseguire un'esercitazione sul ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="42e29-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="42e29-111">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="42e29-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="42e29-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="42e29-112">Prerequisites</span></span>

<span data-ttu-id="42e29-113">Per completare questa esercitazione, verificare che siano soddisfatti i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="42e29-113">To complete this tutorial, make sure the following prerequisites are completed:</span></span>

- <span data-ttu-id="42e29-114">Installazione della versione più recente di [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="42e29-114">Installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="42e29-115">Installazione di un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="42e29-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="42e29-116">Questa esercitazione usa il database di esempio AdventureWorksLT con il nome **mySampleDatabase** da una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="42e29-116">This tutorial uses the AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="42e29-117">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="42e29-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="42e29-118">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="42e29-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="42e29-119">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="42e29-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="42e29-120">Individuazione di un metodo per eseguire script SQL sul database. È possibile usare uno degli strumenti di query seguenti:</span><span class="sxs-lookup"><span data-stu-id="42e29-120">Have identified a method to execute SQL scripts against your database, you can use one of the following query tools:</span></span>
   - <span data-ttu-id="42e29-121">Editor di query nel [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="42e29-121">The query editor in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="42e29-122">Per altre informazioni sull'uso dell'editor di query nel portale di Azure, vedere la sezione su come [connettersi ed eseguire query con l'editor di query](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="42e29-122">For more information on using the query editor in the Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="42e29-123">Versione più recente di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server al database SQL per Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="42e29-123">The newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server to SQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="42e29-124">Versione più recente di [Visual Studio Code](https://code.visualstudio.com/docs), un editor grafico di codice per Linux, macOS e Windows che supporta estensioni, tra cui l'[estensione mssql](https://aka.ms/mssql-marketplace), per l'esecuzione di query su Microsoft SQL Server, database SQL di Azure e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="42e29-124">The newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including the [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="42e29-125">Per altre informazioni sull'uso di questo strumento con il database SQL di Azure, vedere l'articolo su come [connettersi ed eseguire query con Visual Studio Code](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="42e29-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="42e29-126">Creare utenti del database e concedere autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="42e29-126">Create database users and grant permissions</span></span>

<span data-ttu-id="42e29-127">Connettersi al database e creare account utente usando uno degli strumenti di query seguenti:</span><span class="sxs-lookup"><span data-stu-id="42e29-127">Connect to your database and create user accounts using one of the following query tools:</span></span>

- <span data-ttu-id="42e29-128">Editor di query nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="42e29-128">The Query editor in the Azure portal</span></span>
- <span data-ttu-id="42e29-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="42e29-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="42e29-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="42e29-130">Visual Studio Code</span></span>

<span data-ttu-id="42e29-131">Questi account utente vengono replicati automaticamente nel server secondario e vengono mantenuti sincronizzati.</span><span class="sxs-lookup"><span data-stu-id="42e29-131">These user accounts replicate automatically to your secondary server (and be kept in sync).</span></span> <span data-ttu-id="42e29-132">Per usare SQL Server Management Studio o Visual Studio Code potrebbe essere necessario configurare una regola del firewall, in caso di connessione da un client con un indirizzo IP per il quale non si è ancora configurato un firewall.</span><span class="sxs-lookup"><span data-stu-id="42e29-132">To use SQL Server Management Studio or Visual Studio Code, you may need to configure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="42e29-133">Per la procedura dettagliata, vedere [Creare una regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="42e29-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="42e29-134">In una finestra di query eseguire questa query per creare due account utente nel database.</span><span class="sxs-lookup"><span data-stu-id="42e29-134">In a query window, execute the following query to create two user accounts in your database.</span></span> <span data-ttu-id="42e29-135">Questo script concede autorizzazioni **db_owner** all'account **app_admin** e autorizzazioni **SELECT** e **UPDATE** all'account **app_user**.</span><span class="sxs-lookup"><span data-stu-id="42e29-135">This script grants **db_owner** permissions to the **app_admin** account and grants **SELECT** and **UPDATE** permissions to the **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user to db_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission to SalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product TO app_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="42e29-136">Creare il firewall a livello di database</span><span class="sxs-lookup"><span data-stu-id="42e29-136">Create database-level firewall</span></span>

<span data-ttu-id="42e29-137">Creare una [regola del firewall a livello di database](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) per il database SQL.</span><span class="sxs-lookup"><span data-stu-id="42e29-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="42e29-138">Questa regola del firewall a livello di database viene replicata automaticamente nel server secondario creato in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="42e29-138">This database-level firewall rule replicates automatically to the secondary server that you create in this tutorial.</span></span> <span data-ttu-id="42e29-139">Per semplicità, in questa esercitazione usare l'indirizzo IP pubblico del computer in cui si eseguono i passaggi dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="42e29-139">For simplicity (in this tutorial), use the public IP address of the computer on which you are performing the steps in this tutorial.</span></span> <span data-ttu-id="42e29-140">Per determinare l'indirizzo IP usato per la regola del firewall a livello di server per il computer corrente, vedere [Creare una regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="42e29-140">To determine the IP address used for the server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="42e29-141">Nella finestra di query aperta sostituire la query precedente con la query seguente, sostituendo gli indirizzi IP con gli indirizzi IP appropriati per l'ambiente in uso.</span><span class="sxs-lookup"><span data-stu-id="42e29-141">In your open query window, replace the previous query with the following query, replacing the IP addresses with the appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="42e29-142">Creare un gruppo di failover automatico con replica geografica attiva</span><span class="sxs-lookup"><span data-stu-id="42e29-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="42e29-143">Usando Azure PowerShell, creare un [gruppo di failover automatico con replica geografica attiva](sql-database-geo-replication-overview.md) tra il server SQL di Azure esistente e il nuovo server SQL di Azure vuoto in un'area di Azure e quindi aggiungere il database di esempio al gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and the new empty Azure SQL server in an Azure region, and then add your sample database to the failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42e29-144">Per questi cmdlet è necessario Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="42e29-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="42e29-145">Inserire le variabili per gli script di PowerShell usando i valori del server esistente e del database di esempio e specificare un valore univoco globale come nome del gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-145">Populate variables for your PowerShell scripts using the values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

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

2. <span data-ttu-id="42e29-146">Creare un server di backup vuoto nell'area di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="42e29-147">Creare un gruppo di failover tra i due server.</span><span class="sxs-lookup"><span data-stu-id="42e29-147">Create a failover group between the two servers.</span></span>

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

4. <span data-ttu-id="42e29-148">Aggiungere il database al gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-148">Add your database to the failover group.</span></span>

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

## <a name="install-java-software"></a><span data-ttu-id="42e29-149">Installare il software Java</span><span class="sxs-lookup"><span data-stu-id="42e29-149">Install Java software</span></span>

<span data-ttu-id="42e29-150">Le procedure descritte in questa sezione presuppongono che si abbia familiarità con lo sviluppo con Java ma non con il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="42e29-150">The steps in this section assume that you are familiar with developing using Java and are new to working with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="42e29-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="42e29-151">**Mac OS**</span></span>
<span data-ttu-id="42e29-152">Aprire il terminale in uso e passare alla directory in cui si prevede di creare il progetto Java.</span><span class="sxs-lookup"><span data-stu-id="42e29-152">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="42e29-153">Installare **brew** e **Maven** immettendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="42e29-153">Install **brew** and **Maven** by entering the following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="42e29-154">Per indicazioni dettagliate sull'installazione e la configurazione dell'ambiente Java e Maven, andare alla pagina [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Creare un'app con SQL Server), selezionare **Java** e quindi **MacOS** e infine seguire le istruzioni dettagliate per la configurazione di Java e Maven riportate nei passaggi 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="42e29-154">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="42e29-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="42e29-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="42e29-156">Aprire il terminale in uso e passare alla directory in cui si prevede di creare il progetto Java.</span><span class="sxs-lookup"><span data-stu-id="42e29-156">Open your terminal and navigate to a directory where you plan on creating your Java project.</span></span> <span data-ttu-id="42e29-157">Installare **Maven** immettendo i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="42e29-157">Install **Maven** by entering the following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="42e29-158">Per indicazioni dettagliate sull'installazione e la configurazione dell'ambiente Java e Maven, andare alla pagina [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Creare un'app con SQL Server), selezionare **Java** e quindi **Ubuntu** e infine seguire le istruzioni dettagliate per la configurazione di Java e Maven riportate nei passaggi 1.2, 1.3 e 1.4.</span><span class="sxs-lookup"><span data-stu-id="42e29-158">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow the detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="42e29-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="42e29-159">**Windows**</span></span>
<span data-ttu-id="42e29-160">Installare [Maven](https://maven.apache.org/download.cgi) tramite il programma di installazione ufficiale.</span><span class="sxs-lookup"><span data-stu-id="42e29-160">Install [Maven](https://maven.apache.org/download.cgi) using the official installer.</span></span> <span data-ttu-id="42e29-161">Usare Maven per gestire le dipendenze e compilare, testare ed eseguire il progetto Java.</span><span class="sxs-lookup"><span data-stu-id="42e29-161">Use Maven to help manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="42e29-162">Per indicazioni dettagliate sull'installazione e la configurazione dell'ambiente Java e Maven, andare alla pagina [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/) (Creare un'app con SQL Server), selezionare **Java** e quindi Windows e infine seguire le istruzioni dettagliate per la configurazione di Java e Maven riportate nei passaggi 1.2 e 1.3.</span><span class="sxs-lookup"><span data-stu-id="42e29-162">For detailed guidance on installing and configuring Java and Maven environment, go the [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow the detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="42e29-163">Creare il progetto SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="42e29-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="42e29-164">Nella console dei comandi (ad esempio, Bash) creare un progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="42e29-164">In the command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="42e29-165">Digitare **Y** e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="42e29-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="42e29-166">Passare alla directory del progetto appena creato.</span><span class="sxs-lookup"><span data-stu-id="42e29-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="42e29-167">Usando l'editor preferito, aprire il file pom.xml file nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="42e29-167">Using your favorite editor, open the pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="42e29-168">Aggiungere la dipendenza di Microsoft JDBC Driver per SQL Server al progetto Maven aprendo l'editor di testo preferito e copiando e incollando le righe seguenti nel file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="42e29-168">Add the Microsoft JDBC Driver for SQL Server dependency to your Maven project by opening your favorite text editor and copying and pasting the following lines into your pom.xml file.</span></span> <span data-ttu-id="42e29-169">Non sovrascrivere i valori esistenti già inseriti nel file.</span><span class="sxs-lookup"><span data-stu-id="42e29-169">Do not overwrite the existing values prepopulated in the file.</span></span> <span data-ttu-id="42e29-170">La dipendenza JDBC deve essere incollata all'interno della più estesa sezione "dependencies".</span><span class="sxs-lookup"><span data-stu-id="42e29-170">The JDBC dependency must be pasted within the larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="42e29-171">Specificare la versione di Java in base alla quale compilare il progetto aggiungendo la sezione "properties" seguente nel file pom.xml, dopo la sezione "dependencies".</span><span class="sxs-lookup"><span data-stu-id="42e29-171">Specify the version of Java to compile the project against by adding the following “properties” section into the pom.xml file after the "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="42e29-172">Aggiungere la sezione "build" seguente nel file pom.xml, dopo la sezione "properties", per supportare i file manifesto in file JAR.</span><span class="sxs-lookup"><span data-stu-id="42e29-172">Add the following "build" section into the pom.xml file after the "properties" section to support manifest files in jars.</span></span>       

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
8. <span data-ttu-id="42e29-173">Salvare e chiudere il file pom.xml.</span><span class="sxs-lookup"><span data-stu-id="42e29-173">Save and close the pom.xml file.</span></span>
9. <span data-ttu-id="42e29-174">Aprire il file App.java (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) e sostituire il contenuto con il contenuto seguente.</span><span class="sxs-lookup"><span data-stu-id="42e29-174">Open the App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace the contents with the following contents.</span></span> <span data-ttu-id="42e29-175">Sostituire il nome del gruppo di failover con il nome del proprio gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-175">Replace the failover group name with the name for your failover group.</span></span> <span data-ttu-id="42e29-176">Se si sono modificati i valori per il nome del database, l'utente o la password, modificare anche tali valori.</span><span class="sxs-lookup"><span data-stu-id="42e29-176">If you have changed the values for the database name, user, or password, change those values as well.</span></span>

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
      // Insert data into the product table with a unique product name that we can use to find the product again later
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
      // Query the data that was previously inserted into the primary database from the geo replicated database
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
      // Query the high water mark id that is stored in the table to be able to make unique inserts 
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
6. <span data-ttu-id="42e29-177">Salvare e chiudere il file App.java.</span><span class="sxs-lookup"><span data-stu-id="42e29-177">Save and close the App.java file.</span></span>

## <a name="compile-and-run-the-sqldbsample-project"></a><span data-ttu-id="42e29-178">Compilare ed eseguire il progetto SqlDbSample</span><span class="sxs-lookup"><span data-stu-id="42e29-178">Compile and run the SqlDbSample project</span></span>

1. <span data-ttu-id="42e29-179">Nella console dei comandi eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="42e29-179">In the command console, execute to following command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="42e29-180">Al termine, eseguire questo comando per eseguire l'applicazione (a meno che non venga arrestata manualmente, l'esecuzione dura circa 1 ora):</span><span class="sxs-lookup"><span data-stu-id="42e29-180">When finished, execute the following command to run the application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="42e29-181">Eseguire un'esercitazione sul ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="42e29-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="42e29-182">Chiamare il failover manuale del gruppo di failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="42e29-183">Osservare i risultati dell'applicazione durante il failover.</span><span class="sxs-lookup"><span data-stu-id="42e29-183">Observe the application results during failover.</span></span> <span data-ttu-id="42e29-184">Alcuni inserimenti avranno esito negativo durante l'aggiornamento della cache DNS.</span><span class="sxs-lookup"><span data-stu-id="42e29-184">Some inserts fail while the DNS cache refreshes.</span></span>     

3. <span data-ttu-id="42e29-185">Individuare il ruolo eseguito dal server di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="42e29-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="42e29-186">Effettuare il failback.</span><span class="sxs-lookup"><span data-stu-id="42e29-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="42e29-187">Osservare i risultati dell'applicazione durante il failback.</span><span class="sxs-lookup"><span data-stu-id="42e29-187">Observe the application results during failback.</span></span> <span data-ttu-id="42e29-188">Alcuni inserimenti avranno esito negativo durante l'aggiornamento della cache DNS.</span><span class="sxs-lookup"><span data-stu-id="42e29-188">Some inserts fail while the DNS cache refreshes.</span></span>     

6. <span data-ttu-id="42e29-189">Individuare il ruolo eseguito dal server di ripristino di emergenza.</span><span class="sxs-lookup"><span data-stu-id="42e29-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="42e29-190">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42e29-190">Next steps</span></span> 

<span data-ttu-id="42e29-191">Per altre informazioni, vedere l'articolo relativo a [gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="42e29-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
