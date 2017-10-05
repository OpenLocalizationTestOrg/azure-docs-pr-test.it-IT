---
title: Implementare applicazioni SaaS multi-tenant con il database SQL di Azure | Documentazione Microsoft
description: Implementare applicazioni SaaS multi-tenant con il database SQL di Azure.
services: sql-database
documentationcenter: 
author: AyoOlubeko
manager: jhubbard
editor: monicar
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,scale out apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/08/2017
ms.author: AyoOlubek
ms.openlocfilehash: 0aea69d86a51c38c99a72f46737de1eea27bef83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="08cf0-103">Implementare applicazioni SaaS multi-tenant usando il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="08cf0-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="08cf0-104">Un'applicazione multi-tenant è un'applicazione ospitata in un ambiente cloud che fornisce lo stesso set di servizi a centinaia o migliaia di tenant che non condividono o non visualizzano i dati degli altri.</span><span class="sxs-lookup"><span data-stu-id="08cf0-104">A multi-tenant application is an application hosted in a cloud environment and that provides the same set of services to hundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="08cf0-105">Un esempio è un'applicazione SaaS che fornisce servizi ai tenant in un ambiente ospitato nel cloud.</span><span class="sxs-lookup"><span data-stu-id="08cf0-105">An example is an SaaS application that provides services to tenants in a cloud-hosted environment.</span></span> <span data-ttu-id="08cf0-106">Questo modello consente di isolare i dati per ogni tenant e ottimizza la distribuzione delle risorse di costo.</span><span class="sxs-lookup"><span data-stu-id="08cf0-106">This model isolates the data for each tenant and optimizes the distribution of resources for cost.</span></span> 

<span data-ttu-id="08cf0-107">Questa esercitazione illustra come creare un'applicazione SaaS multi-tenant con database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="08cf0-107">This tutorial demonstrates how to create a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="08cf0-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="08cf0-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="08cf0-109">Configurare un ambiente database per supportare un'applicazione SaaS multi-tenant, usando il modello database per ogni tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-109">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="08cf0-110">Creare un catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="08cf0-111">Eseguire il provisioning del database tenant e registrarlo nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-111">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="08cf0-112">Configurare un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="08cf0-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="08cf0-113">Accedere ai database tenant con una semplice applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="08cf0-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="08cf0-114">Eliminare un tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-114">Delete a tenant</span></span>

<span data-ttu-id="08cf0-115">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="08cf0-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08cf0-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="08cf0-116">Prerequisites</span></span>

<span data-ttu-id="08cf0-117">Per completare questa esercitazione, accertarsi di avere:</span><span class="sxs-lookup"><span data-stu-id="08cf0-117">To complete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="08cf0-118">Installato la versione più recente di PowerShell e di [Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="08cf0-118">Installed the newest version of PowerShell and the [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="08cf0-119">Installato la versione più recente di [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="08cf0-119">Installed the latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="08cf0-120">Installando SQL Server Management Studio viene installata anche la versione più recente di SQLPackage, un'utilità della riga di comando utilizzabile per automatizzare varie attività di sviluppo di database.</span><span class="sxs-lookup"><span data-stu-id="08cf0-120">Installing SQL Server Management Studio also installs the latest version of SQLPackage, a command-line utility that can be used to automate a range of database development tasks.</span></span>

* <span data-ttu-id="08cf0-121">Installato [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) e la [versione più recente di JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="08cf0-121">Installed the [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and the [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="08cf0-122">Installato [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="08cf0-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="08cf0-123">Maven è utilizzabile per gestire le dipendenze, compilare, testare ed eseguire il progetto Java di esempio</span><span class="sxs-lookup"><span data-stu-id="08cf0-123">Maven will be used to help manage dependencies, build, test and run the sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="08cf0-124">Configurare l'ambiente dati</span><span class="sxs-lookup"><span data-stu-id="08cf0-124">Set up data environment</span></span>

<span data-ttu-id="08cf0-125">Verrà eseguito il provisioning di un database per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="08cf0-126">Il modello database per ogni tenant offre il massimo livello di isolamento tra tenant, con costi DevOps ridotti.</span><span class="sxs-lookup"><span data-stu-id="08cf0-126">The database-per-tenant model provides the highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="08cf0-127">Per ottimizzare i costi delle risorse cloud, verrà anche eseguito il provisioning dei database tenant in un pool elastico che consente di ottimizzare prezzi e prestazioni per un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="08cf0-127">To optimize the cost of cloud resources, you will also be provisioning the tenant databases into an elastic pool which allows you to optimize the price performance for a group of databases.</span></span> <span data-ttu-id="08cf0-128">Per informazioni su altri modelli di provisioning di database [vedere qui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="08cf0-128">To learn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="08cf0-129">Seguire questi passaggi per creare un server SQL e un pool elastico che ospiterà tutti i database tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-129">Follow these steps to create a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="08cf0-130">Creare variabili per archiviare i valori che verranno usati nel resto dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="08cf0-130">Create variables to store values that will be used in the rest of the tutorial.</span></span> <span data-ttu-id="08cf0-131">Assicurarsi di modificare la variabile indirizzo IP per includere il proprio indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="08cf0-131">Make sure to modify the IP address variable to include your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify to include your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="08cf0-132">Accedere ad Azure e creare un server SQL e un pool elastico</span><span class="sxs-lookup"><span data-stu-id="08cf0-132">Login to Azure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login to Azure 
   Login-AzureRmAccount
   
   # Create resource group 
   New-AzureRmResourceGroup -Name "myResourceGroup" -Location "northcentralus"
   
   # Create logical SQL Server with firewall rules 
   New-AzureRmSqlServer -ResourceGroupName "myResourceGroup" `
       -ServerName $servername `
       -Location "northcentralus" `
       -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   
   New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourcegroupname `
       -ServerName $servername `
       -FirewallRuleName "singleAddress" -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
   
   # Create elastic pool 
   New-AzureRmSqlElasticPool -ResourceGroupName "myResourceGroup"
       -ServerName $servername `
       -ElasticPoolName "myElasticPool" `
       -Edition "Standard" `
       -Dtu 50 `
       -DatabaseDtuMin 10 `
       -DatabaseDtuMax 20
   ```
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="08cf0-133">Creare il catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-133">Create tenant catalog</span></span> 

<span data-ttu-id="08cf0-134">In un'applicazione SaaS multi-tenant è importante sapere dove sono archiviate le informazioni per un tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-134">In a multi-tenant SaaS application, it’s important to know where information for a tenant is stored.</span></span> <span data-ttu-id="08cf0-135">Vengono in genere archiviate in un database del catalogo.</span><span class="sxs-lookup"><span data-stu-id="08cf0-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="08cf0-136">Il database del catalogo viene usato per contenere un mapping tra un tenant e un database in cui sono archiviati i dati del tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-136">The catalog database is used to hold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="08cf0-137">Si applica il modello base se viene usato un database a singolo tenant o multi-tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-137">The basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="08cf0-138">Seguire questi passaggi per creare un database di catalogo per l'applicazione SaaS di esempio.</span><span class="sxs-lookup"><span data-stu-id="08cf0-138">Follow these steps to create a catalog database for the sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table to track mapping between tenants and their databases
$commandText = "
CREATE TABLE Tenants
(
   TenantId         INT IDENTITY PRIMARY KEY,
   TenantName       NVARCHAR(128) NOT NULL,
   TenantDatabase   NVARCHAR(128) NOT NULL
);

CREATE INDEX IX_TenantName ON Tenants (TenantName);"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="08cf0-139">Eseguire il provisioning del database per 'tenant1' e registrare nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="08cf0-140">Usare Powershell per eseguire il provisioning di un database per un nuovo tenant 'tenant1' e registrare il tenant nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="08cf0-140">Use Powershell to provision a database for a new tenant 'tenant1' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant1');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant1 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register 'tenant1' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant1', '$tenant1');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="08cf0-141">Eseguire il provisioning del database per 'tenant2' e registrare nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="08cf0-142">Usare Powershell per eseguire il provisioning di un database per un nuovo tenant 'tenant2' e registrare il tenant nel catalogo.</span><span class="sxs-lookup"><span data-stu-id="08cf0-142">Use Powershell to provision a database for a new tenant 'tenant2' and register this tenant in the catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into the table 
$commandText = "
CREATE TABLE WhoAmI (TenantName NVARCHAR(128) NOT NULL);
INSERT INTO WhoAmI VALUES ('Tenant $tenant2');"

Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database $tenant2 `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Register tenant 'tenant2' in the tenant catalog 
$commandText = "
INSERT INTO Tenants VALUES ('$tenant2', '$tenant2');"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection
```

## <a name="set-up-sample-java-application"></a><span data-ttu-id="08cf0-143">Configurare l'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="08cf0-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="08cf0-144">Creare un progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="08cf0-144">Create a maven project.</span></span> <span data-ttu-id="08cf0-145">Digitare quanto segue in una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="08cf0-145">Type the following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="08cf0-146">Aggiungere la dipendenza, il livello di linguaggio e compilare l'opzione per supportare i file manifesto in file JAR nel file pom.xml:</span><span class="sxs-lookup"><span data-stu-id="08cf0-146">Add this dependency, language level, and build option to support manifest files in jars to the pom.xml file:</span></span>
   
   ```XML
   <dependency>
         <groupId>com.microsoft.sqlserver</groupId>
         <artifactId>mssql-jdbc</artifactId>
         <version>6.1.0.jre8</version>
   </dependency>
   
   <properties>
         <maven.compiler.source>1.8</maven.compiler.source>
         <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   
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

3. <span data-ttu-id="08cf0-147">Aggiungere il codice seguente nel file App.Java:</span><span class="sxs-lookup"><span data-stu-id="08cf0-147">Add the following into the App.java file:</span></span>

   ```java 
   package com.sqldbsamples;
   
   import java.util.Map;
   
   import java.util.HashMap;
   
   import java.io.BufferedReader;
   
   import java.io.InputStreamReader;
   
   import java.sql.Connection;
   
   import java.sql.Statement;
   
   import java.sql.PreparedStatement;
   
   import java.sql.ResultSet;
   
   import java.sql.DriverManager;
   
   public class App {
   
   private static final String SERVER_NAME = "your-server-name";
   
   private static final String CATALOG_DB_NAME = "tenantCatalog";
   
   private static final String USER = "ServerAdmin";
   
   private static final String PASSWORD = "ChangeYourAdminPassword1";
   
   private static final String CATALOG_DB_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, CATALOG_DB_NAME, USER, PASSWORD);
   
   private static final String CMD_LIST = "LIST";

   private static final String CMD_QUERY = "QUERY";

   private static final String CMD_QUIT = "QUIT";
   
   public static void main(String[] args) {
   
   System.out.println("\n############################");
   
   System.out.println("## SAAS DATABASE TUTORIAL ##");
   
   System.out.println("############################\n");
   
   System.out.println("OPTIONS");
   
   System.out.println(" " + CMD_LIST + " - list tenants");
   
   System.out.println(" " + CMD_QUERY + " <NAME> - connect and tenant query tenant <NAME>");
   
   System.out.println(" " + CMD_QUIT + " - quit the application\n");
   
   try (BufferedReader br = new BufferedReader(new InputStreamReader(System.in))) {
   
   while(true) {
   
   String[] input = br.readLine().split("\\s");
   
   if (null != input && input.length > 0) {
   
   if (input[0].equalsIgnoreCase(CMD_LIST)) {
   
   listTenants();
   
   } else if (input[0].toLowerCase().startsWith(CMD_QUERY.toLowerCase()) && input.length == 2) {
   
   queryTenant(input[1].trim());
   
   } else if (input[0].equalsIgnoreCase(CMD_QUIT)) {
   
   break;
   
   } else {
   
   System.out.println(" -> Command not supported");
   
   }
   
   }
   
   System.out.println("");
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void listTenants() {
   
   // List all tenants that currently exist in the system
   
   String sql = "SELECT TenantName FROM Tenants";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   Statement stmt = connection.createStatement();
   
   ResultSet resultSet = stmt.executeQuery(sql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   }
   
   private static void queryTenant(String name) {
   
   // Query the data that was previously inserted into the primary database from the geo replicated database
   
   String url = null;
   
   String sql = "SELECT TenantDatabase FROM Tenants WHERE TenantName = ?";
   
   try (Connection connection = DriverManager.getConnection(CATALOG_DB_URL);
   
   PreparedStatement pstmt = connection.prepareStatement(sql)) {
   
   pstmt.setString(1, name);
   
   try (ResultSet resultSet = pstmt.executeQuery()) {
   
   if (resultSet.next()) {
   
   url = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", SERVER_NAME, resultSet.getString(1), USER, PASSWORD);
   
   }
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   if (null != url) {
   
   String tenantSql = "SELECT TenantName FROM WhoAmI";
   
   try (Connection connection = DriverManager.getConnection(url);
   
   Statement stmt = connection.createStatement();

   ResultSet resultSet = stmt.executeQuery(tenantSql)) {
   
   while (resultSet.next()) {
   
   System.out.println(" -> Entry in table WhoAmI in tenant " + name + " is: " + resultSet.getString(1));
   
   }
   
   } catch (Exception e) {
   
   System.out.println(e.getMessage());
   
   e.printStackTrace();
   
   }
   
   } else {
   
   System.out.println(" -> Tenant " + name + " not found");
   
   }
   
   }
   
   }
   ```

4. <span data-ttu-id="08cf0-148">Salvare il file.</span><span class="sxs-lookup"><span data-stu-id="08cf0-148">Save the file.</span></span>

5. <span data-ttu-id="08cf0-149">Passare alla console dei comandi ed eseguire</span><span class="sxs-lookup"><span data-stu-id="08cf0-149">Go to command console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="08cf0-150">Al termine, eseguire il comando seguente per eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="08cf0-150">When finished, execute the following to run the application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="08cf0-151">L'output sarà simile al seguente se viene eseguito correttamente:</span><span class="sxs-lookup"><span data-stu-id="08cf0-151">The output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit the application

* List the tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="08cf0-152">Eliminare il primo tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-152">Delete first tenant</span></span> 
<span data-ttu-id="08cf0-153">Usare PowerShell per eliminare il database tenant e la voce di catalogo per il primo tenant.</span><span class="sxs-lookup"><span data-stu-id="08cf0-153">Use PowerShell to delete the tenant database and catalog entry for the first tenant.</span></span>

```PowerShell
# Remove 'tenant1' from catalog 
$commandText = "DELETE FROM Tenants WHERE TenantName = '$tenant1';"
Invoke-SqlCmd `
    -Username $adminlogin `
    -Password $password `
    -ServerInstance ($servername + ".database.windows.net") `
    -Database "tenantCatalog" `
    -ConnectionTimeout 30 `
    -Query $commandText `
    -EncryptConnection

# Delete database 
Remove-AzureRmSqlDatabase -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1
```

<span data-ttu-id="08cf0-154">Provare a connettersi a 'tenant1' usando l'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="08cf0-154">Try connecting to 'tenant1' using the Java application.</span></span> <span data-ttu-id="08cf0-155">Si otterrà un errore che informa che il tenant non esiste.</span><span class="sxs-lookup"><span data-stu-id="08cf0-155">You will get an error stating that the tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08cf0-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08cf0-156">Next steps</span></span> 

<span data-ttu-id="08cf0-157">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="08cf0-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="08cf0-158">Configurare un ambiente database per supportare un'applicazione SaaS multi-tenant, usando il modello database per ogni tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-158">Set up a database environment to support a multi-tenant SaaS application, using the Database-per-tenant pattern</span></span>
> * <span data-ttu-id="08cf0-159">Creare un catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="08cf0-160">Eseguire il provisioning del database tenant e registrarlo nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-160">Provision a tenant database and register it in the tenant catalog</span></span>
> * <span data-ttu-id="08cf0-161">Configurare un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="08cf0-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="08cf0-162">Accedere ai database tenant con una semplice applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="08cf0-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="08cf0-163">Eliminare un tenant</span><span class="sxs-lookup"><span data-stu-id="08cf0-163">Delete a tenant</span></span>

* <span data-ttu-id="08cf0-164">Esempi di attività comuni di PowerShell, vedere [Esempi di Azure PowerShell per database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="08cf0-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="08cf0-165">Modelli di progettazione per applicazioni SaaS multi-tenant, vedere [Modelli di progettazione per le applicazioni SaaS multi-tenant e il database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="08cf0-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="08cf0-166">Esempi di Java per attività comuni di Azure, vedere [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="08cf0-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



