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
# <a name="implement-a-geo-distributed-database"></a>Implementare un database con distribuzione geografica

In questa esercitazione, configurare un database SQL di Azure e l'applicazione per l'area di failover tooa remoto e quindi testare il piano di failover. Si apprenderà come: 

> [!div class="checklist"]
> * Creare utenti del database e concedere loro le autorizzazioni
> * Configurare una regola del firewall a livello di database
> * Creare un [gruppo di failover con replica geografica](sql-database-geo-replication-overview.md)
> * Creare e compilare un tooquery applicazione Java un database SQL di Azure
> * Eseguire un'esercitazione sul ripristino di emergenza

Se non si ha una sottoscrizione di Azure, [creare un account gratuito](https://azure.microsoft.com/free/) prima di iniziare.


## <a name="prerequisites"></a>Prerequisiti

toocomplete completamento di questa esercitazione, assicurarsi che i hello seguenti prerequisiti:

- Versione più recente hello installato [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs). 
- Installazione di un database SQL di Azure. Questa esercitazione viene utilizzato il database di esempio AdventureWorksLT hello con un nome di **mySampleDatabase** da una di queste guide introduttive:

   - [Creare un database: portale](sql-database-get-started-portal.md)
   - [Creare un database: interfaccia della riga di comando](sql-database-get-started-cli.md)
   - [Creare un database: PowerShell](sql-database-get-started-powershell.md)

- Sono identificati tooexecute un metodo SQL script nel database, è possibile utilizzare uno dei seguenti strumenti di query hello:
   - editor di query Hello in hello [portale di Azure](https://portal.azure.com). Per ulteriori informazioni sull'utilizzo dell'editor di query hello in hello portale di Azure, vedere [Connect e query tramite l'Editor di Query](sql-database-get-started-portal.md#query-the-sql-database).
   - versione più recente di Hello di [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), che è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server tooSQL Database per Microsoft Windows.
   - versione più recente di Hello di [codice di Visual Studio](https://code.visualstudio.com/docs), che è un editor di codice con interfaccia grafica per Linux, macOS, e Windows che supporti le estensioni, tra cui hello [estensione mssql](https://aka.ms/mssql-marketplace) per le query di Microsoft SQL Server , Database SQL di azure e SQL Data Warehouse. Per altre informazioni sull'uso di questo strumento con il database SQL di Azure, vedere l'articolo su come [connettersi ed eseguire query con Visual Studio Code](sql-database-connect-query-vscode.md). 

## <a name="create-database-users-and-grant-permissions"></a>Creare utenti del database e concedere autorizzazioni

La connessione a database tooyour e creare gli account utente utilizzando uno dei seguenti strumenti di query hello:

- editor di Query Hello in hello portale di Azure
- SQL Server Management Studio
- Visual Studio Code

Questi account utente vengono automaticamente replicano server secondario tooyour e mantenuti sincronizzati. toouse SQL Server Management Studio o codice di Visual Studio, potrebbe essere necessario tooconfigure una regola del firewall se ci si connette da un client in un indirizzo IP per il quale non è ancora configurato un firewall. Per la procedura dettagliata, vedere [Creare una regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).

- In una finestra query, eseguire hello seguente query toocreate due account utente nel database. Questo script concede **db_owner** autorizzazioni toohello **app_admin** account e concede il **selezionare** e **aggiornamento** toohello autorizzazioni **app_user** account. 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a>Creare il firewall a livello di database

Creare una [regola del firewall a livello di database](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) per il database SQL. La regola del firewall a livello di database vengono replicati automaticamente i server secondari toohello creati in questa esercitazione. Per semplicità (in questa esercitazione), utilizzare l'indirizzo IP pubblico hello del computer hello in cui si esegue la procedura hello in questa esercitazione. indirizzo IP di hello toodetermine utilizzato per la regola firewall di livello server hello per il computer corrente, vedere [creare un firewall di livello server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).  

- Nella finestra di query aperta, sostituire la query precedente hello con hello query seguente, sostituendo gli indirizzi IP hello con indirizzi IP corretti hello per l'ambiente.  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a>Creare un gruppo di failover automatico con replica geografica attiva 

Utilizzo di PowerShell di Azure, creare un [gruppo di replica geografica attiva di failover automatico](sql-database-geo-replication-overview.md) tra il server SQL di Azure esistente e i hello nuovo vuote server SQL di Azure in un'area di Azure e quindi aggiungere il gruppo di failover toohello di esempio del database.

> [!IMPORTANT]
> Per questi cmdlet è necessario Azure PowerShell 4.0. [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. Popolare le variabili per gli script di PowerShell utilizzando valori hello per il server esistente e il database di esempio e fornire un valore univoco globale per nome del gruppo di failover.

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

2. Creare un server di backup vuoto nell'area di failover.

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. Creare un gruppo di failover tra due server hello.

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

4. Aggiungere il gruppo di database toohello failover.

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

## <a name="install-java-software"></a>Installare il software Java

passaggi di Hello in questa sezione si presuppone che ha familiarità con lo sviluppo con Java e tooworking Nuovo Database SQL di Azure. 

### <a name="mac-os"></a>**Mac OS**
Aprire terminale e spostarsi tooa directory in cui si prevede di creazione del progetto Java. Installare **brew** e **Maven** immettendo hello seguenti comandi: 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**selezionare **MacOS**, quindi seguire Hello indicazioni dettagliate per la configurazione di Java e Maven nel passaggio 1.2 e 1.3.

### <a name="linux-ubuntu"></a>**Linux (Ubuntu)**
Aprire terminale e spostarsi tooa directory in cui si prevede di creazione del progetto Java. Installare **Maven** immettendo hello seguenti comandi:

```bash
sudo apt-get install maven
```

Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**selezionare **Ubuntu**, quindi seguire Hello indicazioni dettagliate per la configurazione di Java e Maven nel passaggio 1.2, 1.3 e 1.4.

### <a name="windows"></a>**Windows**
Installare [Maven](https://maven.apache.org/download.cgi) utilizzando Installazione guidata ufficiale hello. Utilizzare Maven toohelp di gestire le dipendenze, compilare, testare ed eseguire il progetto Java. Per istruzioni dettagliate sull'installazione e configurazione di ambiente Java e Maven, visitare hello [compilare un'app usando SQL Server](https://www.microsoft.com/sql-server/developer-get-started/)selezionare **Java**, selezionare Windows e quindi seguire hello istruzioni dettagliate configurazione di Java e Maven nel passaggio 1.2 e 1.3.

## <a name="create-sqldbsample-project"></a>Creare il progetto SqlDbSample

1. Nella console di comando di hello (ad esempio Bash), creare un progetto di Maven. 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. Digitare **Y** e premere **INVIO**.
3. Passare alla directory del progetto appena creato.

   ```bash
   cd SqlDbSamples
   ```

4. Usando l'editor preferito, aprire il file di pom.xml hello nella cartella del progetto. 

5. Aggiungere hello Microsoft JDBC Driver per i progetti Maven tooyour dipendenza di SQL Server, aprire un editor di testo e copiare e incollare hello seguenti righe all'interno del file pom.xml. Non sovrascrivere i valori esistenti di hello già inseriti nel file hello. è necessario incollare Hello dipendenza JDBC (sezione) "dipendenze" hello più grande.   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. Specificare hello versione di Java toocompile hello progetto contro aggiungendo la seguente sezione "proprietà" nel file pom.xml hello dopo la sezione "dipendenze" hello hello. 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. Aggiungere la seguente hello "build" sezione nel file pom.xml hello dopo hello "proprietà" sezione toosupport manifesto file JAR.       

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
8. Salvare e chiudere il file di pom.xml hello.
9. Aprire il file App.java hello (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) e sostituire il contenuto di hello con hello seguente contenuto. Sostituire hello failover group name con il nome di hello per il gruppo di failover. Se è stato modificato i valori hello per nome del database hello, un utente o password, è possibile modificare anche tali valori.

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
6. Salvare e chiudere il file di App.java hello.

## <a name="compile-and-run-hello-sqldbsample-project"></a>Compilare ed eseguire il progetto di SqlDbSample hello

1. Nella console di comando hello, eseguire il comando toofollowing.

   ```bash
   mvn package
   ```
2. Al termine, eseguire hello successivo comando toorun hello applicazione (viene eseguito per circa 1 ora a meno che non è stato interrotto manualmente):

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a>Eseguire un'esercitazione sul ripristino di emergenza

1. Chiamare il failover manuale del gruppo di failover. 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. Osservare i risultati di applicazione hello durante il failover. Alcuni inserimenti esito negativo mentre hello cache DNS viene aggiornato.     

3. Individuare il ruolo eseguito dal server di ripristino di emergenza.

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. Effettuare il failback.

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. Osservare i risultati di applicazione hello durante il failback. Alcuni inserimenti esito negativo mentre hello cache DNS viene aggiornato.     

6. Individuare il ruolo eseguito dal server di ripristino di emergenza.

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a>Passaggi successivi 

Per altre informazioni, vedere l'articolo relativo a [gruppi di failover e replica geografica attiva](sql-database-geo-replication-overview.md).
