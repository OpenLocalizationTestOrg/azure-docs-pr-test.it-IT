---
title: Usare Java per eseguire query sul database SQL di Azure | Microsoft Docs
description: Questo argomento illustra come usare Java per creare un programma che si connette a un database SQL di Azure ed esegue query usando istruzioni Transact-SQL.
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
ms.openlocfilehash: 103b0755ab89a13297cfdc9ec72416664da8c1e9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="use-java-to-query-an-azure-sql-database"></a><span data-ttu-id="853c4-103">Usare Java per eseguire query su un database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="853c4-103">Use Java to query an Azure SQL database</span></span>

<span data-ttu-id="853c4-104">Questa guida introduttiva illustra come usare [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) per connettersi a un database SQL di Azure e quindi usare istruzioni Transact-SQL per eseguire query sui dati.</span><span class="sxs-lookup"><span data-stu-id="853c4-104">This quick start demonstrates how to use [Java](https://docs.microsoft.com/sql/connect/jdbc/microsoft-jdbc-driver-for-sql-server) to connect to an Azure SQL database and then use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="853c4-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="853c4-105">Prerequisites</span></span>

<span data-ttu-id="853c4-106">Per completare questa esercitazione introduttiva, accertarsi di avere i prerequisiti seguenti:</span><span class="sxs-lookup"><span data-stu-id="853c4-106">To complete this quick start tutorial, make sure you have the following prerequisites:</span></span>

- <span data-ttu-id="853c4-107">un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="853c4-107">An Azure SQL database.</span></span> <span data-ttu-id="853c4-108">Questa guida introduttiva usa le risorse create in una delle guide introduttive seguenti:</span><span class="sxs-lookup"><span data-stu-id="853c4-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="853c4-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="853c4-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="853c4-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="853c4-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="853c4-111">Creare un database: PowerShell</span><span class="sxs-lookup"><span data-stu-id="853c4-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="853c4-112">Una [regola del firewall a livello di server](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) per l'indirizzo IP pubblico del computer usato per questa esercitazione introduttiva.</span><span class="sxs-lookup"><span data-stu-id="853c4-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>

- <span data-ttu-id="853c4-113">Avere installato Java e il software correlato per il sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="853c4-113">You have installed Java and related software for your operating system.</span></span>

    - <span data-ttu-id="853c4-114">**MacOS**: installare Homebrew e Java, quindi installare Maven.</span><span class="sxs-lookup"><span data-stu-id="853c4-114">**MacOS**: Install Homebrew and Java, and then install Maven.</span></span> <span data-ttu-id="853c4-115">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span><span class="sxs-lookup"><span data-stu-id="853c4-115">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/mac/).</span></span>
    - <span data-ttu-id="853c4-116">**Ubuntu**: installare Java Development Kit e quindi Maven.</span><span class="sxs-lookup"><span data-stu-id="853c4-116">**Ubuntu**:  Install the Java Development Kit, and install Maven.</span></span> <span data-ttu-id="853c4-117">Vedere i [passaggi 1.2, 1.3 e 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="853c4-117">See [Step 1.2, 1.3, and 1.4](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/).</span></span>
    - <span data-ttu-id="853c4-118">**Windows**: installare Java Development Kit e Maven.</span><span class="sxs-lookup"><span data-stu-id="853c4-118">**Windows**: Install the Java Development Kit, and Maven.</span></span> <span data-ttu-id="853c4-119">Vedere i [passaggi 1.2 e 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span><span class="sxs-lookup"><span data-stu-id="853c4-119">See [Step 1.2 and 1.3](https://www.microsoft.com/sql-server/developer-get-started/java/windows/).</span></span>    

## <a name="sql-server-connection-information"></a><span data-ttu-id="853c4-120">Informazioni di connessione SQL Server</span><span class="sxs-lookup"><span data-stu-id="853c4-120">SQL server connection information</span></span>

<span data-ttu-id="853c4-121">Ottenere le informazioni di connessione necessarie per connettersi al database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="853c4-121">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="853c4-122">Nelle procedure successive saranno necessari il nome completo del server, il nome del database e le informazioni di accesso.</span><span class="sxs-lookup"><span data-stu-id="853c4-122">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="853c4-123">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="853c4-123">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="853c4-124">Scegliere **Database SQL** dal menu a sinistra, quindi fare clic sul database nella pagina **Database SQL**.</span><span class="sxs-lookup"><span data-stu-id="853c4-124">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="853c4-125">Nella pagina **Panoramica** per il database, verificare il nome completo del server, come illustrato nell'immagine seguente. È possibile passare il puntatore sul nome del server per visualizzare l'opzione **Fare clic per copiare**.</span><span class="sxs-lookup"><span data-stu-id="853c4-125">On the **Overview** page for your database, review the fully qualified server name as shown in the following image: You can hover over the server name to bring up the **Click to copy** option.</span></span>  

   ![server-name](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="853c4-127">Se si dimenticano le informazioni di accesso per il server, passare alla pagina del server di database SQL per visualizzare il nome dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="853c4-127">If you forget your server login information, navigate to the SQL Database server page to view the server admin name.</span></span>  <span data-ttu-id="853c4-128">Se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="853c4-128">If necessary, reset the password.</span></span>     

## <a name="create-maven-project-and-dependencies"></a><span data-ttu-id="853c4-129">**Creare il progetto Maven e le dipendenze**</span><span class="sxs-lookup"><span data-stu-id="853c4-129">**Create Maven project and dependencies**</span></span>
1. <span data-ttu-id="853c4-130">Dal terminale creare un nuovo progetto Maven denominato **sqltest**.</span><span class="sxs-lookup"><span data-stu-id="853c4-130">From the terminal, create a new Maven project called **sqltest**.</span></span> 

   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=sqltest" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```

2. <span data-ttu-id="853c4-131">Quando richiesto, immettere **Y**.</span><span class="sxs-lookup"><span data-stu-id="853c4-131">Enter **Y** when prompted.</span></span>
3. <span data-ttu-id="853c4-132">Passare alla directory **sqltest** e aprire ***pom.xml*** con l'editor di testo preferito.</span><span class="sxs-lookup"><span data-stu-id="853c4-132">Change directory to **sqltest** and open ***pom.xml*** with your favorite text editor.</span></span>  <span data-ttu-id="853c4-133">Aggiungere **Microsoft JDBC Driver per SQL Server** alle dipendenze del progetto usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="853c4-133">Add the **Microsoft JDBC Driver for SQL Server** to your project's dependencies using the following code:</span></span>

   ```xml
   <dependency>
       <groupId>com.microsoft.sqlserver</groupId>
       <artifactId>mssql-jdbc</artifactId>
       <version>6.2.1.jre8</version>
   </dependency>
   ```

4. <span data-ttu-id="853c4-134">In ***pom.xml*** aggiungere anche le proprietà seguenti al progetto.</span><span class="sxs-lookup"><span data-stu-id="853c4-134">Also in ***pom.xml***, add the following properties to your project.</span></span>  <span data-ttu-id="853c4-135">Se non è presente una sezione properties, è possibile aggiungerla dopo le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="853c4-135">If you don't have a properties section, you can add it after the dependencies.</span></span>

   ```xml
   <properties>
       <maven.compiler.source>1.8</maven.compiler.source>
       <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```

5. <span data-ttu-id="853c4-136">Salvare e chiudere ***pom.xml***.</span><span class="sxs-lookup"><span data-stu-id="853c4-136">Save and close ***pom.xml***.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="853c4-137">Inserire il codice per eseguire query sul database SQL</span><span class="sxs-lookup"><span data-stu-id="853c4-137">Insert code to query SQL database</span></span>

1. <span data-ttu-id="853c4-138">Nel progetto Maven in ..\sqltest\src\main\java\com\sqlsamples\App.java dovrebbe essere già presente un file denominato ***App.java***.</span><span class="sxs-lookup"><span data-stu-id="853c4-138">You should already have a file called ***App.java*** in your Maven project located at:  ..\sqltest\src\main\java\com\sqlsamples\App.java</span></span>

2. <span data-ttu-id="853c4-139">Aprire il file, sostituirne il contenuto con il codice seguente e aggiungere i valori appropriati per il server, il database, l'utente e la password.</span><span class="sxs-lookup"><span data-stu-id="853c4-139">Open the file and replace its contents with the following code and add the appropriate values for your server, database, user, and password.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.DriverManager;

   public class App {

    public static void main(String[] args) {
    
        // Connect to database
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

## <a name="run-the-code"></a><span data-ttu-id="853c4-140">Eseguire il codice</span><span class="sxs-lookup"><span data-stu-id="853c4-140">Run the code</span></span>

1. <span data-ttu-id="853c4-141">Al prompt dei comandi eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="853c4-141">At the command prompt, run the following commands:</span></span>

   ```bash
   mvn package
   mvn -q exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   ```

2. <span data-ttu-id="853c4-142">Verificare che vengano restituite le prime 20 righe e quindi chiudere la finestra dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="853c4-142">Verify that the top 20 rows are returned and then close the application window.</span></span>


## <a name="next-steps"></a><span data-ttu-id="853c4-143">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="853c4-143">Next steps</span></span>
- [<span data-ttu-id="853c4-144">Progettare il primo database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="853c4-144">Design your first Azure SQL database</span></span>](sql-database-design-first-database.md)
- [<span data-ttu-id="853c4-145">Driver Microsoft JDBC per SQL Server</span><span class="sxs-lookup"><span data-stu-id="853c4-145">Microsoft JDBC Driver for SQL Server</span></span>](https://github.com/microsoft/mssql-jdbc)
- [<span data-ttu-id="853c4-146">Segnalare problemi e porre domande</span><span class="sxs-lookup"><span data-stu-id="853c4-146">Report issues/ask questions</span></span>](https://github.com/microsoft/mssql-jdbc/issues)

