---
title: La connessione tooAzure Database PostgreSQL Usa Java | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice Java è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
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
ms.openlocfilehash: 8f6e0a47a0d6dfebf29eb56c31ccccabd7c2b670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="33d1a-103">Il Database di Azure per PostgreSQL: dati di utilizzo Java tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="33d1a-103">Azure Database for PostgreSQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="33d1a-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di un'applicazione Java PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a Java application.</span></span> <span data-ttu-id="33d1a-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="33d1a-106">Hello passaggi in questo articolo si presuppone che si abbia familiarità con lo sviluppo con Java e che siano tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33d1a-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="33d1a-107">Prerequisites</span></span>
<span data-ttu-id="33d1a-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="33d1a-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="33d1a-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="33d1a-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="33d1a-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="33d1a-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="33d1a-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="33d1a-111">You also need to:</span></span>
- <span data-ttu-id="33d1a-112">Scaricare hello [Driver JDBC PostgreSQL](https://jdbc.postgresql.org/download.html) corrispondente alla versione di Java e hello Java Development Kit.</span><span class="sxs-lookup"><span data-stu-id="33d1a-112">Download hello [PostgreSQL JDBC Driver](https://jdbc.postgresql.org/download.html) matching your version of Java and hello Java Development Kit.</span></span>
- <span data-ttu-id="33d1a-113">Includere hello file jar di JDBC PostgreSQL (ad esempio postgresql 42.1.1.jar) nell'applicazione classpath.</span><span class="sxs-lookup"><span data-stu-id="33d1a-113">Include hello PostgreSQL JDBC jar file (for example postgresql-42.1.1.jar) in your application classpath.</span></span> <span data-ttu-id="33d1a-114">Per altre informazioni, vedere i [dettagli sul classpath](https://jdbc.postgresql.org/documentation/head/classpath.html).</span><span class="sxs-lookup"><span data-stu-id="33d1a-114">For more information, see [classpath details](https://jdbc.postgresql.org/documentation/head/classpath.html).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="33d1a-115">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="33d1a-115">Get connection information</span></span>
<span data-ttu-id="33d1a-116">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-116">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="33d1a-117">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="33d1a-117">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="33d1a-118">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="33d1a-118">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="33d1a-119">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="33d1a-119">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="33d1a-120">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="33d1a-120">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="33d1a-121">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="33d1a-121">Select hello server's **Overview** page.</span></span> <span data-ttu-id="33d1a-122">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="33d1a-122">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="33d1a-123">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-java/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="33d1a-123">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-java/1-connection-string.png)</span></span>
5. <span data-ttu-id="33d1a-124">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-124">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="33d1a-125">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="33d1a-125">Connect, create table, and insert data</span></span>
<span data-ttu-id="33d1a-126">Hello utilizzare codice tooconnect e carico hello dati seguenti utilizzando la funzione hello con un **inserire** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-126">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="33d1a-127">metodi di Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), e [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) vengono utilizzati tooconnect, eliminare e creare la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-127">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, drop, and create hello table.</span></span> <span data-ttu-id="33d1a-128">Hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) oggetto è utilizzato toobuild i comandi insert hello, con valori di parametro hello toobind setString() e setInt().</span><span class="sxs-lookup"><span data-stu-id="33d1a-128">hello [prepareStatement](https://jdbc.postgresql.org/documentation/head/query.html) object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="33d1a-129">Metodo [ExecuteUpdate ()](https://jdbc.postgresql.org/documentation/head/update.html) esecuzioni hello comando per ogni set di parametri.</span><span class="sxs-lookup"><span data-stu-id="33d1a-129">Method [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) runs hello command for each set of parameters.</span></span> 

<span data-ttu-id="33d1a-130">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="33d1a-130">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
    
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="read-data"></a><span data-ttu-id="33d1a-131">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="33d1a-131">Read data</span></span>
<span data-ttu-id="33d1a-132">Esempio di codice seguente hello di utilizzare dati hello tooread con un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-132">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="33d1a-133">metodi di Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), e [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) vengono utilizzati tooconnect, creare ed eseguire l'istruzione select hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-133">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [createStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeQuery()](https://jdbc.postgresql.org/documentation/head/query.html) are used tooconnect, create, and run hello select statement.</span></span> <span data-ttu-id="33d1a-134">elaborazione dei risultati di Hello utilizzando un [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) oggetto.</span><span class="sxs-lookup"><span data-stu-id="33d1a-134">hello results are processed using a [ResultSet](https://www.postgresql.org/docs/7.4/static/jdbc-query.html) object.</span></span> 

<span data-ttu-id="33d1a-135">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="33d1a-135">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
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
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}

```

## <a name="update-data"></a><span data-ttu-id="33d1a-136">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="33d1a-136">Update data</span></span>
<span data-ttu-id="33d1a-137">Esempio di codice seguente hello di utilizzare dati hello toochange con un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-137">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="33d1a-138">metodi di Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), e [ExecuteUpdate ()](https://jdbc.postgresql.org/documentation/head/update.html) vengono utilizzati tooconnect, preparare ed eseguire l'istruzione update hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-138">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello update statement.</span></span> 

<span data-ttu-id="33d1a-139">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="33d1a-139">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Modify some data in table.
                int nRowsUpdated = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?;");
                preparedStatement.setInt(1, 200);
                preparedStatement.setString(2, "banana");
                nRowsUpdated += preparedStatement.executeUpdate();
                System.out.println(String.format("Updated %d row(s) of data.", nRowsUpdated));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```
## <a name="delete-data"></a><span data-ttu-id="33d1a-140">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="33d1a-140">Delete data</span></span>
<span data-ttu-id="33d1a-141">Esempio di codice seguente hello di utilizzare dati tooremove con un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="33d1a-141">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="33d1a-142">metodi di Hello [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), e [ExecuteUpdate ()](https://jdbc.postgresql.org/documentation/head/update.html) vengono utilizzati tooconnect, preparare ed eseguire l'istruzione delete hello.</span><span class="sxs-lookup"><span data-stu-id="33d1a-142">hello methods [getConnection()](https://www.postgresql.org/docs/7.4/static/jdbc-use.html), [prepareStatement()](https://jdbc.postgresql.org/documentation/head/query.html), and [executeUpdate()](https://jdbc.postgresql.org/documentation/head/update.html) are used tooconnect, prepare, and run hello delete statement.</span></span> 

<span data-ttu-id="33d1a-143">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="33d1a-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

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

        // check that hello driver is installed
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
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("ssl", "true");

            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase.", e);
        }
        if (connection != null) 
        { 
            System.out.println("Successfully created connection toodatabase.");
        
            // Perform some SQL queries over hello connection.
            try
            {
                // Delete some data from table.
                int nRowsDeleted = 0;
                PreparedStatement preparedStatement = connection.prepareStatement("DELETE FROM inventory WHERE name = ?;");
                preparedStatement.setString(1, "orange");
                nRowsDeleted += preparedStatement.executeUpdate();
                System.out.println(String.format("Deleted %d row(s) of data.", nRowsDeleted));
    
                // NOTE No need toocommit all changes toodatabase, as auto-commit is enabled by default.
            }
            catch (SQLException e)
            {
                throw new SQLException("Encountered an error when executing given sql statement.", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase.");
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="33d1a-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33d1a-144">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="33d1a-145">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="33d1a-145">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
