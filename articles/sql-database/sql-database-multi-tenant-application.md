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
# <a name="implement-a-multi-tenant-saas-application-using-azure-sql-database"></a>Implementare applicazioni SaaS multi-tenant usando il database SQL di Azure

Un'applicazione multi-tenant è un'applicazione ospitata in un ambiente cloud e che fornisce hello stesso insieme di servizi toohundreds o migliaia di tenant che ha non condividere o visualizzare i dati di altro. Un esempio è un'applicazione SaaS che offre servizi tootenants in un ambiente ospitato su cloud. Questo modello consente di isolare dati hello per ogni tenant e ottimizza distribuzione hello delle risorse per costo. 

Questa esercitazione viene illustrato come toocreate un'applicazione SaaS multi-tenant con Database SQL di Azure.

In questa esercitazione si apprenderà come:
> [!div class="checklist"]
> * Impostare un toosupport ambiente di database di un'applicazione SaaS multi-tenant, usando il modello di Database per tenant hello
> * Creare un catalogo di tenant
> * Eseguire il provisioning di un database tenant e registrarlo nel catalogo di hello tenant
> * Configurare un'applicazione Java di esempio 
> * Accedere ai database tenant con una semplice applicazione console Java
> * Eliminare un tenant

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione, verificare che sono:

* Versione più recente di hello installato di PowerShell e hello [più recente di Azure PowerShell SDK](http://azure.microsoft.com/downloads/)

* Versione più recente di hello installato di [SQL Server Management Studio](http://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Versione più recente di hello di SQLPackage, un'utilità della riga di comando che può essere utilizzato tooautomate una gamma di attività di sviluppo del database viene installato anche l'installazione di SQL Server Management Studio.

* Hello installato [Java Runtime Environment (JRE) 8](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) hello e [più recente JAVA Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) installati nel computer. 

* Installato [Apache Maven](https://maven.apache.org/download.cgi). Verrà utilizzato Maven toohelp gestire le dipendenze, compilare, testare ed eseguire progetto Java di esempio hello

## <a name="set-up-data-environment"></a>Configurare l'ambiente dati

Verrà eseguito il provisioning di un database per ogni tenant. modello di database per tenant Hello offre hello massimo grado di isolamento tra tenant, con un costo ridotto DevOps. costo di hello toooptimize delle risorse cloud, verrà inoltre eseguito il provisioning dei database tenant hello in un pool elastico che consente prestazioni di prezzo hello toooptimize per un gruppo di database. toolearn su altro database provisioning modelli [vedere qui](sql-database-design-patterns-multi-tenancy-saas-applications.md#multi-tenant-data-models).

Seguire toocreate questi passaggi, un server SQL e un pool elastico che ospiterà tutti i database tenant. 

1. Creare variabili valori toostore che verranno utilizzati nel resto di hello di esercitazione hello. Verificare che toomodify hello IP indirizzo variabile tooinclude l'indirizzo IP 
   
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
   
2. Account di accesso tooAzure e creare un pool di server ed elastico SQL 
   
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
   
## <a name="create-tenant-catalog"></a>Creare il catalogo di tenant 

In un'applicazione SaaS multi-tenant, è importante tooknow memorizzazione informazioni per un tenant. Vengono in genere archiviate in un database del catalogo. database del catalogo Hello è toohold usato un mapping tra un tenant e un database in cui sono memorizzati i dati del tenant.  modello di base Hello si applica se multi-tenant o viene utilizzato un database singolo tenant.

Seguire questi toocreate passaggi un database di catalogo per un'applicazione SaaS esempio hello.

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

## <a name="provision-database-for-tenant1-and-register-in-tenant-catalog"></a>Eseguire il provisioning del database per 'tenant1' e registrare nel catalogo di tenant 
Utilizzare Powershell tooprovision un database per un nuovo tenant 'tenant1' e registrare il tenant nel catalogo di hello. 

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

## <a name="provision-database-for-tenant2-and-register-in-tenant-catalog"></a>Eseguire il provisioning del database per 'tenant2' e registrare nel catalogo di tenant
Utilizzare Powershell tooprovision un database per un nuovo tenant 'tenant2' e registrare il tenant nel catalogo di hello. 

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

## <a name="set-up-sample-java-application"></a>Configurare l'applicazione Java di esempio 

1. Creare un progetto Maven. Digitare il seguente hello in una finestra del prompt dei comandi:
   
   ```
   mvn archetype:generate -DgroupId=com.microsoft.sqlserver -DartifactId=mssql-jdbc -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
   ```
   
2. Aggiungere questa dipendenza, il livello di linguaggio e i file manifesto nel file di JAR toohello pom.xml toosupport opzione di compilazione:
   
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

3. Aggiungere il seguente hello in file App.java hello:

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

4. Salvare il file hello.

5. Passare toocommand console ed eseguire

   ```bash
   mvn package
   ```

6. Al termine, eseguire hello dopo l'applicazione hello toorun 
   
   ```
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```
   
Se l'operazione viene eseguita correttamente, output di Hello viene visualizzato come segue:

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

## <a name="delete-first-tenant"></a>Eliminare il primo tenant 
Utilizzare PowerShell toodelete hello tenant database e del catalogo voce per il tenant prima hello.

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

Provare a connettersi troppo utilizzando 'tenant1' hello applicazione Java. Si otterrà un errore per segnalare che tale tenant hello non esiste.

## <a name="next-steps"></a>Passaggi successivi 

Questa esercitazione illustra come:
> [!div class="checklist"]
> * Impostare un toosupport ambiente di database di un'applicazione SaaS multi-tenant, usando il modello di Database per tenant hello
> * Creare un catalogo di tenant
> * Eseguire il provisioning di un database tenant e registrarlo nel catalogo di hello tenant
> * Configurare un'applicazione Java di esempio 
> * Accedere ai database tenant con una semplice applicazione console Java
> * Eliminare un tenant

* Esempi di attività comuni di PowerShell, vedere [Esempi di Azure PowerShell per database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-powershell-samples)

* Modelli di progettazione per applicazioni SaaS multi-tenant, vedere [Modelli di progettazione per le applicazioni SaaS multi-tenant e il database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-design-patterns-multi-tenancy-saas-applications)

* Esempi di Java per attività comuni di Azure, vedere [Centro per sviluppatori Java](https://azure.microsoft.com/develop/java/)



