---
title: Connettersi a Database di Azure per PostgreSQL usando Java | Microsoft Docs
description: "Questa guida introduttiva fornisce un esempio di codice Java che è possibile usare per connettersi ai dati ed eseguire query da Database di Azure per PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: java
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 730a3f464b4437c260d09abc026a186a0e26293c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-java-to-connect-and-query-data"></a><span data-ttu-id="c7bc7-103">Database di Azure per PostgreSQL: usare Java per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="c7bc7-103">Azure Database for PostgreSQL: Use Java to connect and query data</span></span>
<span data-ttu-id="c7bc7-104">Questa guida introduttiva illustra come connettersi a un database di Azure per PostgreSQL usando un'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="c7bc7-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="c7bc7-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con Java, ma non con Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-106">The steps in this article assume that you are familiar with developing using Java, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7bc7-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c7bc7-107">Prerequisites</span></span>
<span data-ttu-id="c7bc7-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="c7bc7-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="c7bc7-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="c7bc7-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="c7bc7-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c7bc7-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="c7bc7-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="c7bc7-111">You also need to:</span></span>
- <span data-ttu-id="c7bc7-112">Scaricare il [driver JDBC PostgreSQL](https://jdbc.postgresql.org/download.html) corrispondente alla versione di Java e Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-112">Download the [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and the Java Development Kit.</span></span>
- <span data-ttu-id="c7bc7-113">Includere il file JAR JDBC PostgreSQL (ad esempio postgresql-42.1.1.jar) nel classpath dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-113">Include the PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="c7bc7-114">Per altre informazioni, vedere i [dettagli sul classpath](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="c7bc7-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="c7bc7-115">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="c7bc7-115">Get connection information</span></span>
<span data-ttu-id="c7bc7-116">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-116">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="c7bc7-117">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-117">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="c7bc7-118">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c7bc7-118">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c7bc7-119">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-119">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="c7bc7-120">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-120">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="c7bc7-121">Selezionare la pagina **Panoramica** del server.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-121">Select the server's **Overview** page.</span></span> <span data-ttu-id="c7bc7-122">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-122">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="c7bc7-123">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="c7bc7-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="c7bc7-124">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-124">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="c7bc7-125">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="c7bc7-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="c7bc7-126">Usare il codice seguente per connettersi e caricare i dati usando la funzione con un'istruzione SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-126">Use the following code to connect and load the data using the function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="c7bc7-127">I metodi [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) ed [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) vengono usati per connettersi ed eliminare e creare la tabella.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-127">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, drop, and create the table.</span></span> <span data-ttu-id="c7bc7-128">L'oggetto [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) viene usato per compilare i comandi di inserimento, con setString() e setInt() per associare i valori dei parametri.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-128">The [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used to build the insert commands, with setString() and setInt() to bind the parameter values.</span></span> <span data-ttu-id="c7bc7-129">Il metodo [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) esegue il comando per ogni set di parametri.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs the command for each set of parameters.</span></span> 

<span data-ttu-id="c7bc7-130">Sostituire i parametri host, database, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-130">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Drop previous table of same name if one exists.
                Statement statement = connection.createStatement();
                statement.execute("DROP TABLE IF EXISTS inventory;");
                System.out.println("Finished dropping table (if existed).");
    
                // Create table.
                statement.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
                System.out.println("Created table.");
    
                // Insert some data into table.
                int nRowsInserted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("INSERT INTO inventory (name, quantity) VALUES (?, ?);");
                preparedStatement.setString(1, "banana");
                preparedStatement.setInt(2, 150);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "orange");
                preparedStatement.setInt(2, 154);
                nRowsInserted += preparedStatement.executeUpdate();

                preparedStatement.setString(1, "apple");
                preparedStatement.setInt(2, 100);
                nRowsInserted += preparedStatement.executeUpdate();
                System.out.println(String.format("Inserted %d row(s) of data.", nRowsInserted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="c7bc7-131">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="c7bc7-131">Read data</span></span>
<span data-ttu-id="c7bc7-132">Usare il codice seguente per leggere i dati con un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-132">Use the following code to read the data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="c7bc7-133">I metodi [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html) ed [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) vengono usati per connettersi e creare ed eseguire l'istruzione SELECT.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-133">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used to connect, create, and run the select statement.</span></span> <span data-ttu-id="c7bc7-134">I risultati vengono elaborati usando un oggetto [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html).</span><span class="sxs-lookup"><span data-stu-id="c7bc7-134">The results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="c7bc7-135">Sostituire i parametri host, database, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-135">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
    
                Statement statement = connection.createStatement();
                ResultSet results = statement.executeQuery("SELECT * from inventory;");
                while (results.next())
                {
                    String outputString = 
                        String.format(
                            "Data row = (%s, %s, %s)",
                            results.getString(1),
                            results.getString(2),
                            results.getString(3));
                    System.out.println(outputString);
                }
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="c7bc7-136">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="c7bc7-136">Update data</span></span>
<span data-ttu-id="c7bc7-137">Usare il codice seguente per modificare i dati con un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-137">Use the following code to change the data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="c7bc7-138">I metodi [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) ed [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) vengono usati per connettersi e preparare ed eseguire l'istruzione UPDATE.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-138">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the update statement.</span></span> 

<span data-ttu-id="c7bc7-139">Sostituire i parametri host, database, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-139">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="c7bc7-140">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="c7bc7-140">Delete data</span></span>
<span data-ttu-id="c7bc7-141">Usare il codice seguente per rimuovere i dati con un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-141">Use the following code to remove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="c7bc7-142">I metodi [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html) ed [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) vengono usati per connettersi e preparare ed eseguire l'istruzione DELETE.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-142">The methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used to connect, prepare, and run the delete statement.</span></span> 

<span data-ttu-id="c7bc7-143">Sostituire i parametri host, database, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="c7bc7-143">Replace the host, database, user, and password parameters with the values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {

        // Initialize connection variables.
        String host = "mypgserver-20170401.postgres.database.azure.com";
        String database = "mypgsqldb";
        String user = "mylogin@mypgserver-20170401";
        String password = "<server_admin_password>";

        // check that the driver is installed
        try
        {
            Class.forName("org.postgresql.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("PostgreSQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("PostgreSQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:postgresql://%s/%s", host, database);
            
            // set up the connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed to create connection to database.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection to database.");
        
            // Perform some SQL queries over the connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need to commit all changes to database, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed to create connection to database.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="c7bc7-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c7bc7-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="c7bc7-145">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="c7bc7-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
