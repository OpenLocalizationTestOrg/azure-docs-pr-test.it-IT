---
title: aaaUse Java tooquery Database SQL di Azure | Documenti Microsoft
description: In questo argomento illustra come toouse Java toocreate un programma che si connette tooan Database SQL di Azure e query tramite istruzioni Transact-SQL.
services: sql-database
documentationcenter: 
author: ajlam
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: andrela
ms.openlocfilehash: f014edbe38ca0e7b6e43f4eb4d2e53d3561bf3e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-java-tooquery-an-azure-sql-database"></a><span data-ttu-id="e0fa9-103">Usare Java tooquery un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e0fa9-103">Use Java tooquery an Azure SQL database</span></span>

<span data-ttu-id="e0fa9-104">Questa Guida introduttiva illustra come toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database e di utilizzare dati tooquery di istruzioni Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-104">This quick start demonstrates how toouse [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) tooconnect tooan Azure SQL database and then use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e0fa9-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e0fa9-105">Prerequisites</span></span>

<span data-ttu-id="e0fa9-106">Questo rapido toocomplete esercitazione per l'avvio, assicurarsi di avere hello seguenti prerequisiti:</span><span class="sxs-lookup"><span data-stu-id="e0fa9-106">toocomplete this quick start tutorial, make sure you have hello following prerequisites:</span></span>

- <span data-ttu-id="e0fa9-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-107">An Azure SQL database.</span></span> <span data-ttu-id="e0fa9-108">Questa Guida introduttiva utilizza risorse di hello create in una di queste guide introduttive:</span><span class="sxs-lookup"><span data-stu-id="e0fa9-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="e0fa9-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="e0fa9-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="e0fa9-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="e0fa9-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="e0fa9-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0fa9-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="e0fa9-112">Oggetto [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico hello del computer hello è utilizzare per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="e0fa9-113">Avere installato Java e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="e0fa9-114">**MacOS**: installare Homebrew e Java, quindi installare Maven.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="e0fa9-115">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="e0fa9-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="e0fa9-116">**Ubuntu**: installare hello Java Development Kit e Maven.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-116">**Ubuntu**:  Install hello Java Development Kit, and install Maven.</span></span> <span data-ttu-id="e0fa9-117">Vedere i [passaggi 1.2, 1.3 e 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="e0fa9-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="e0fa9-118">**Windows**: installare hello Java Development Kit e Maven.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-118">**Windows**: Install hello Java Development Kit, and Maven.</span></span> <span data-ttu-id="e0fa9-119">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="e0fa9-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="e0fa9-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0fa9-120">SQL server connection information</span></span>

<span data-ttu-id="e0fa9-121">Ottenere il database di SQL Azure toohello hello connessione le informazioni necessarie tooconnect.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-121">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="e0fa9-122">Sarà necessario hello nome completo del server, nome del database e le informazioni di accesso nelle procedure successive hello.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-122">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="e0fa9-123">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e0fa9-123">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e0fa9-124">Selezionare **database SQL** dal menu a sinistra di hello, scegliere il database in hello **database SQL** pagina.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-124">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="e0fa9-125">In hello **Panoramica** pagina per il database, esaminare hello nome completo del server, come illustrato nella seguente immagine hello: È possibile passare il mouse su toobring nome di server hello backup hello **fare clic su toocopy** opzione.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-125">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image: You can hover over hello server name toobring up hello **Click toocopy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="e0fa9-127">Se si dimenticano le informazioni di accesso del server, passare toohello Database di SQL server pagina tooview hello admin nome del server.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-127">If you forget your server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span>  <span data-ttu-id="e0fa9-128">Se necessario, hello reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-128">If necessary, reset hello password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="e0fa9-129">**Creare il progetto Maven e le dipendenze**</span><span class="sxs-lookup"><span data-stu-id="e0fa9-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="e0fa9-130">Da hello terminal, creare un nuovo progetto di Maven denominato **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-130">From hello terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="e0fa9-131">Quando richiesto, immettere **Y**.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="e0fa9-132">Modificare anche le directory**sqltest** e aprire ***pom.xml*** con un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-132">Change directory too**sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="e0fa9-133">Aggiungere hello **Microsoft JDBC Driver per SQL Server** hello le dipendenze del progetto tooyour mediante il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e0fa9-133">Add hello **Microsoft JDBC Driver for SQL Server** tooyour project's dependencies using hello following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="e0fa9-134">Anche in ***pom.xml***, aggiungere hello progetto tooyour le proprietà seguenti.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-134">Also in ***pom.xml***, add hello following properties tooyour project.</span></span>  <span data-ttu-id="e0fa9-135">Se non si dispone di una sezione di proprietà, è possibile aggiungere, dopo le dipendenze di hello.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-135">If you don't have a properties section, you can add it after hello dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="e0fa9-136">Salvare e chiudere ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="e0fa9-137">Inserire codice tooquery SQL database</span><span class="sxs-lookup"><span data-stu-id="e0fa9-137">Insert code tooquery SQL database</span></span>

1. <span data-ttu-id="e0fa9-138">Nel progetto Maven in ..\sqltest\src\main\java\com\sqlsamples\App.java dovrebbe essere già presente un file denominato ***App.java***.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="e0fa9-139">Aprire il file hello e sostituire il contenuto con il seguente hello del codice e aggiunta hello valori appropriati per il server, database, l'utente e password.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-139">Open hello file and replace its contents with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect toodatabase
           String hostName = "your_server.database.windows.net";
           String dbName = "your_database";
           String user = "your_username";
           String password = "your_password";
           String url = String.format("jdbc:sqlserver://%s:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", hostName, dbName, user, password);
           Connection connection = null;

           try {
                   connection = DriverManager.getConnection(url);
                   String schema = connection.getSchema();
                   System.out.println("Successful connection - Schema: " + schema);

                   System.out.println("Query data example:");
                   System.out.println("=========================================");

                   // Create and execute a SELECT SQL statement.
                   String selectSql = "SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName " 
                       + "FROM [SalesLT].[ProductCategory] pc "  
                       + "JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid";
                
                   try (Statement statement = connection.createStatement();
                       ResultSet resultSet = statement.executeQuery(selectSql)) {

                           // Print results from select statement
                           System.out.println("Top 20 categories:");
                           while (resultSet.next())
                           {
                               System.out.println(resultSet.getString(1) + " "
                                   + resultSet.getString(2));
                           }
                    connection.close();
                   }                   
           }
           catch (Exception e) {
                   e.printStackTrace();
           }
       }
   }
   ```

## <a name="run-hello-code"></a><span data-ttu-id="e0fa9-140">Eseguire il codice hello</span><span class="sxs-lookup"><span data-stu-id="e0fa9-140">Run hello code</span></span>

1. <span data-ttu-id="e0fa9-141">Al prompt dei comandi di hello, eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="e0fa9-141">At hello command prompt, run hello following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="e0fa9-142">Verificare che i 20 righe hello superiore vengono restituite e chiudere la finestra dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e0fa9-142">Verify that hello top 20 rows are returned and then close hello application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0fa9-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0fa9-143">Next steps</span></span>
- [<span data-ttu-id="e0fa9-144">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="e0fa9-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="e0fa9-145">Driver Microsoft JDBC per SQL Server</span><span class="sxs-lookup"><span data-stu-id="e0fa9-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="e0fa9-146">Segnalare problemi e porre domande</span><span class="sxs-lookup"><span data-stu-id="e0fa9-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

