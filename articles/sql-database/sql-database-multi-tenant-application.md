---
title: applicazione SaaS multi-tenant di aaaImplement con Database SQL di Azure | Documenti Microsoft
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
ms.openlocfilehash: b87b8f296e2c20a8f674b56375f43fdc92df76d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a><span data-ttu-id="67cbc-103">Implementare applicazioni SaaS multi-tenant usando il database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="67cbc-103">Implement a multi-tenant SaaS application using Azure SQL Database</span></span>

<span data-ttu-id="67cbc-104">Un'applicazione multi-tenant è un'applicazione ospitata in un ambiente cloud e che fornisce hello stesso insieme di servizi toohundreds o migliaia di tenant che ha non condividere o visualizzare i dati di altro.</span><span class="sxs-lookup"><span data-stu-id="67cbc-104">A multi-tenant application is an application hosted in a cloud environment and that provides hello same set of services toohundreds or thousands of tenants who do not share or see each other’s data.</span></span> <span data-ttu-id="67cbc-105">Un esempio è un'applicazione SaaS che offre servizi tootenants in un ambiente ospitato su cloud.</span><span class="sxs-lookup"><span data-stu-id="67cbc-105">An example is an SaaS application that provides services tootenants in a cloud-hosted environment.</span></span> <span data-ttu-id="67cbc-106">Questo modello consente di isolare dati hello per ogni tenant e ottimizza distribuzione hello delle risorse per costo.</span><span class="sxs-lookup"><span data-stu-id="67cbc-106">This model isolates hello data for each tenant and optimizes hello distribution of resources for cost.</span></span> 

<span data-ttu-id="67cbc-107">Questa esercitazione viene illustrato come toocreate un'applicazione SaaS multi-tenant con Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="67cbc-107">This tutorial demonstrates how toocreate a multi-tenant SaaS application using Azure SQL Database.</span></span>

<span data-ttu-id="67cbc-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="67cbc-108">In this tutorial, you will learn to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="67cbc-109">Impostare un toosupport ambiente di database di un'applicazione SaaS multi-tenant, usando il modello di Database per tenant hello</span><span class="sxs-lookup"><span data-stu-id="67cbc-109">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="67cbc-110">Creare un catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-110">Create a tenant catalog</span></span>
> * <span data-ttu-id="67cbc-111">Eseguire il provisioning di un database tenant e registrarlo nel catalogo di hello tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-111">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="67cbc-112">Configurare un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="67cbc-112">Set up a sample Java application</span></span> 
> * <span data-ttu-id="67cbc-113">Accedere ai database tenant con una semplice applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="67cbc-113">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="67cbc-114">Eliminare un tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-114">Delete a tenant</span></span>

<span data-ttu-id="67cbc-115">Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="67cbc-115">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67cbc-116">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="67cbc-116">Prerequisites</span></span>

<span data-ttu-id="67cbc-117">toocomplete questa esercitazione, verificare che sono:</span><span class="sxs-lookup"><span data-stu-id="67cbc-117">toocomplete this tutorial, make sure you have:</span></span>

* <span data-ttu-id="67cbc-118">Versione più recente di hello installato di PowerShell e hello [più recente di Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="67cbc-118">Installed hello newest version of PowerShell and hello [latest Azure PowerShell SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="67cbc-119">Versione più recente di hello installato di [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span><span class="sxs-lookup"><span data-stu-id="67cbc-119">Installed hello latest version of [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).</span></span> <span data-ttu-id="67cbc-120">Versione più recente di hello di SQLPackage, un'utilità della riga di comando che può essere utilizzato tooautomate una gamma di attività di sviluppo del database viene installato anche l'installazione di SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="67cbc-120">Installing SQL Server Management Studio also installs hello latest version of SQLPackage, a command-line utility that can be used tooautomate a range of database development tasks.</span></span>

* <span data-ttu-id="67cbc-121">Hello installato [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) hello e [più recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installati nel computer.</span><span class="sxs-lookup"><span data-stu-id="67cbc-121">Installed hello [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) and hello [latest JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installed on your machine.</span></span> 

* <span data-ttu-id="67cbc-122">Installato [Apache Maven](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="67cbc-122">Installed [Apache Maven](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="67cbc-123">Verrà utilizzato Maven toohelp gestire le dipendenze, compilare, testare ed eseguire progetto Java di esempio hello</span><span class="sxs-lookup"><span data-stu-id="67cbc-123">Maven will be used toohelp manage dependencies, build, test and run hello sample Java project</span></span>

## <a name="set-up-data-environment"></a><span data-ttu-id="67cbc-124">Configurare l'ambiente dati</span><span class="sxs-lookup"><span data-stu-id="67cbc-124">Set up data environment</span></span>

<span data-ttu-id="67cbc-125">Verrà eseguito il provisioning di un database per ogni tenant.</span><span class="sxs-lookup"><span data-stu-id="67cbc-125">You will be provisioning a database per tenant.</span></span> <span data-ttu-id="67cbc-126">modello di database per tenant Hello offre hello massimo grado di isolamento tra tenant, con un costo ridotto DevOps.</span><span class="sxs-lookup"><span data-stu-id="67cbc-126">hello database-per-tenant model provides hello highest degree of isolation between tenants, with little DevOps cost.</span></span> <span data-ttu-id="67cbc-127">costo di hello toooptimize delle risorse cloud, verrà inoltre eseguito il provisioning dei database tenant hello in un pool elastico che consente prestazioni di prezzo hello toooptimize per un gruppo di database.</span><span class="sxs-lookup"><span data-stu-id="67cbc-127">toooptimize hello cost of cloud resources, you will also be provisioning hello tenant databases into an elastic pool which allows you toooptimize hello price performance for a group of databases.</span></span> <span data-ttu-id="67cbc-128">toolearn su altro database provisioning modelli [vedere qui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span><span class="sxs-lookup"><span data-stu-id="67cbc-128">toolearn about other database provisioning models [see here](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).</span></span>

<span data-ttu-id="67cbc-129">Seguire toocreate questi passaggi, un server SQL e un pool elastico che ospiterà tutti i database tenant.</span><span class="sxs-lookup"><span data-stu-id="67cbc-129">Follow these steps toocreate a SQL server and an elastic pool that will host all your tenant databases.</span></span> 

1. <span data-ttu-id="67cbc-130">Creare variabili valori toostore che verranno utilizzati nel resto di hello di esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-130">Create variables toostore values that will be used in hello rest of hello tutorial.</span></span> <span data-ttu-id="67cbc-131">Verificare che toomodify hello IP indirizzo variabile tooinclude l'indirizzo IP</span><span class="sxs-lookup"><span data-stu-id="67cbc-131">Make sure toomodify hello IP address variable tooinclude your IP address</span></span> 
   
   ```PowerShell 
   # Set an admin login and password for your database
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   
   # Create random unique names for logical server and tenants
   $servername = "server-$(Get-Random)"
   $tenant1 = "geolamice"
   $tenant2 = "ranplex"
   
   # Store current client IP address (modify tooinclude your IP address)
   $startIpAddress = 0.0.0.0 
   $endIpAddress = 0.0.0.0
   ```
   
2. <span data-ttu-id="67cbc-132">Account di accesso tooAzure e creare un pool di server ed elastico SQL</span><span class="sxs-lookup"><span data-stu-id="67cbc-132">Login tooAzure and create a SQL server and elastic pool</span></span> 
   
   ```PowerShell
   # Login tooAzure 
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
   
## <a name="create-tenant-catalog"></a><span data-ttu-id="67cbc-133">Creare il catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-133">Create tenant catalog</span></span> 

<span data-ttu-id="67cbc-134">In un'applicazione SaaS multi-tenant, è importante tooknow memorizzazione informazioni per un tenant.</span><span class="sxs-lookup"><span data-stu-id="67cbc-134">In a multi-tenant SaaS application, it’s important tooknow where information for a tenant is stored.</span></span> <span data-ttu-id="67cbc-135">Vengono in genere archiviate in un database del catalogo.</span><span class="sxs-lookup"><span data-stu-id="67cbc-135">This is commonly stored in a catalog database.</span></span> <span data-ttu-id="67cbc-136">database del catalogo Hello è toohold usato un mapping tra un tenant e un database in cui sono memorizzati i dati del tenant.</span><span class="sxs-lookup"><span data-stu-id="67cbc-136">hello catalog database is used toohold a mapping between a tenant and a database in which that tenant’s data is stored.</span></span>  <span data-ttu-id="67cbc-137">modello di base Hello si applica se multi-tenant o viene utilizzato un database singolo tenant.</span><span class="sxs-lookup"><span data-stu-id="67cbc-137">hello basic pattern applies whether a multi-tenant or a single-tenant database is used.</span></span>

<span data-ttu-id="67cbc-138">Seguire questi toocreate passaggi un database di catalogo per un'applicazione SaaS esempio hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-138">Follow these steps toocreate a catalog database for hello sample SaaS application.</span></span>

```PowerShell
# Create empty database in pool
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName "tenantCatalog" `
    -ElasticPoolName "myElasticPool"

# Create table tootrack mapping between tenants and their databases
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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a><span data-ttu-id="67cbc-139">Eseguire il provisioning del database per 'tenant1' e registrare nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-139">Provision database for 'tenant1' and register in tenant catalog</span></span> 
<span data-ttu-id="67cbc-140">Utilizzare Powershell tooprovision un database per un nuovo tenant 'tenant1' e registrare il tenant nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-140">Use Powershell tooprovision a database for a new tenant 'tenant1' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant1'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant1 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register 'tenant1' in hello tenant catalog 
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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a><span data-ttu-id="67cbc-141">Eseguire il provisioning del database per 'tenant2' e registrare nel catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-141">Provision database for 'tenant2' and register in tenant catalog</span></span>
<span data-ttu-id="67cbc-142">Utilizzare Powershell tooprovision un database per un nuovo tenant 'tenant2' e registrare il tenant nel catalogo di hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-142">Use Powershell tooprovision a database for a new tenant 'tenant2' and register this tenant in hello catalog.</span></span> 

```PowerShell
# Create empty database in pool for 'tenant2'
New-AzureRmSqlDatabase  -ResourceGroupName "myResourceGroup" `
    -ServerName $servername `
    -DatabaseName $tenant2 `
    -ElasticPoolName "myElasticPool"

# Create table WhoAmI and insert tenant name into hello table 
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

# Register tenant 'tenant2' in hello tenant catalog 
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

## <a name="set-up-sample-java-application"></a><span data-ttu-id="67cbc-143">Configurare l'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="67cbc-143">Set up sample Java application</span></span> 

1. <span data-ttu-id="67cbc-144">Creare un progetto Maven.</span><span class="sxs-lookup"><span data-stu-id="67cbc-144">Create a maven project.</span></span> <span data-ttu-id="67cbc-145">Digitare il seguente hello in una finestra del prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="67cbc-145">Type hello following in a command prompt window:</span></span>
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. <span data-ttu-id="67cbc-146">Aggiungere questa dipendenza, il livello di linguaggio e i file manifesto nel file di JAR toohello pom.xml toosupport opzione di compilazione:</span><span class="sxs-lookup"><span data-stu-id="67cbc-146">Add this dependency, language level, and build option toosupport manifest files in jars toohello pom.xml file:</span></span>
   
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

3. <span data-ttu-id="67cbc-147">Aggiungere il seguente hello in file App.java hello:</span><span class="sxs-lookup"><span data-stu-id="67cbc-147">Add hello following into hello App.java file:</span></span>

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
   
   System.out.println(" " + CMD_QUIT + " - quit hello application\n");
   
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
   
   // List all tenants that currently exist in hello system
   
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
   
   // Query hello data that was previously inserted into hello primary database from hello geo replicated database
   
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

4. <span data-ttu-id="67cbc-148">Salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-148">Save hello file.</span></span>

5. <span data-ttu-id="67cbc-149">Passare toocommand console ed eseguire</span><span class="sxs-lookup"><span data-stu-id="67cbc-149">Go toocommand console and execute</span></span>

   ```bash
   mvn package
   ```

6. <span data-ttu-id="67cbc-150">Al termine, eseguire hello dopo l'applicazione hello toorun</span><span class="sxs-lookup"><span data-stu-id="67cbc-150">When finished, execute hello following toorun hello application</span></span> 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
<span data-ttu-id="67cbc-151">Se l'operazione viene eseguita correttamente, output di Hello viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="67cbc-151">hello output will look like this if it runs successfully:</span></span>

```
############################

## SAAS DATABASE TUTORIAL ##

############################

OPTIONS

LIST - list tenants

QUERY <NAME> - connect and tenant query tenant <NAME>

QUIT - quit hello application

* List hello tenants

* Query tenants you created
```

## <a name="delete-first-tenant"></a><span data-ttu-id="67cbc-152">Eliminare il primo tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-152">Delete first tenant</span></span> 
<span data-ttu-id="67cbc-153">Utilizzare PowerShell toodelete hello tenant database e del catalogo voce per il tenant prima hello.</span><span class="sxs-lookup"><span data-stu-id="67cbc-153">Use PowerShell toodelete hello tenant database and catalog entry for hello first tenant.</span></span>

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

<span data-ttu-id="67cbc-154">Provare a connettersi troppo utilizzando 'tenant1' hello applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="67cbc-154">Try connecting too'tenant1' using hello Java application.</span></span> <span data-ttu-id="67cbc-155">Si otterrà un errore per segnalare che tale tenant hello non esiste.</span><span class="sxs-lookup"><span data-stu-id="67cbc-155">You will get an error stating that hello tenant does not exist.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67cbc-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67cbc-156">Next steps</span></span> 

<span data-ttu-id="67cbc-157">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="67cbc-157">In this tutorial, you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="67cbc-158">Impostare un toosupport ambiente di database di un'applicazione SaaS multi-tenant, usando il modello di Database per tenant hello</span><span class="sxs-lookup"><span data-stu-id="67cbc-158">Set up a database environment toosupport a multi-tenant SaaS application, using hello Database-per-tenant pattern</span></span>
> * <span data-ttu-id="67cbc-159">Creare un catalogo di tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-159">Create a tenant catalog</span></span>
> * <span data-ttu-id="67cbc-160">Eseguire il provisioning di un database tenant e registrarlo nel catalogo di hello tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-160">Provision a tenant database and register it in hello tenant catalog</span></span>
> * <span data-ttu-id="67cbc-161">Configurare un'applicazione Java di esempio</span><span class="sxs-lookup"><span data-stu-id="67cbc-161">Set up a sample Java application</span></span> 
> * <span data-ttu-id="67cbc-162">Accedere ai database tenant con una semplice applicazione console Java</span><span class="sxs-lookup"><span data-stu-id="67cbc-162">Access tenant databases simple a Java console application</span></span>
> * <span data-ttu-id="67cbc-163">Eliminare un tenant</span><span class="sxs-lookup"><span data-stu-id="67cbc-163">Delete a tenant</span></span>

* <span data-ttu-id="67cbc-164">Esempi di attività comuni di PowerShell, vedere [Esempi di Azure PowerShell per database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span><span class="sxs-lookup"><span data-stu-id="67cbc-164">PowerShell samples for common tasks, see [SQL Database PowerShell samples](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)</span></span>

* <span data-ttu-id="67cbc-165">Modelli di progettazione per applicazioni SaaS multi-tenant, vedere [Modelli di progettazione per le applicazioni SaaS multi-tenant e il database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span><span class="sxs-lookup"><span data-stu-id="67cbc-165">Design patterns for multi-tenant SaaS applications see [Design patterns](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)</span></span>

* <span data-ttu-id="67cbc-166">Esempi di Java per attività comuni di Azure, vedere [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/)</span><span class="sxs-lookup"><span data-stu-id="67cbc-166">Java samples for common Azure tasks, see [Java Developer Center](https://azure.microsoft.com/develop/java/)</span></span>



