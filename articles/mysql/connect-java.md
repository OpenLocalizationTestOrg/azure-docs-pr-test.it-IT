---
title: La connessione tooAzure Database MySQL mediante Java | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice Java è possibile usare tooconnect ed eseguire query sui dati da un Database di Azure per il database MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.devlang: java
ms.date: 06/20/2017
ms.openlocfilehash: d584b5491d29700b36fae26800c59d93ceb3e265
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-java-tooconnect-and-query-data"></a><span data-ttu-id="0bbe5-103">Il Database di Azure per MySQL: dati di utilizzo Java tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="0bbe5-103">Azure Database for MySQL: Use Java tooconnect and query data</span></span>
<span data-ttu-id="0bbe5-104">Questa Guida introduttiva illustra come Database di Azure tooconnect tooan per MySQL mediante un'applicazione Java.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a Java application.</span></span> <span data-ttu-id="0bbe5-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="0bbe5-106">Hello passaggi in questo articolo si presuppone che si abbia familiarità con lo sviluppo con Java e che siano tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-106">hello steps in this article assume that you are familiar with developing using Java, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bbe5-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0bbe5-107">Prerequisites</span></span>
<span data-ttu-id="0bbe5-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="0bbe5-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="0bbe5-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="0bbe5-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="0bbe5-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0bbe5-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="0bbe5-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="0bbe5-111">You also need to:</span></span>
- <span data-ttu-id="0bbe5-112">Scaricare il driver JDBC di hello [MySQL connettore/J](https://dev.mysql.com/downloads/connector/j/)</span><span class="sxs-lookup"><span data-stu-id="0bbe5-112">Download hello JDBC driver [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/)</span></span>
- <span data-ttu-id="0bbe5-113">Includere i file jar JDBC hello (ad esempio mysql-connector-java-5.1.42-bin.jar) in classpath dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-113">Include hello JDBC jar file (for example mysql-connector-java-5.1.42-bin.jar) into your application classpath.</span></span> <span data-ttu-id="0bbe5-114">In caso di problemi, vedere la documentazione dell'ambiente relativa alle specifiche per il percorso delle classi, ad esempio [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) o [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span><span class="sxs-lookup"><span data-stu-id="0bbe5-114">If you have trouble with this, please consult your environment's documentation for class path specifics, such as [Apache Tomcat](https://tomcat.apache.org/tomcat-7.0-doc/class-loader-howto.html) or [Java SE](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/classpath.html)</span></span>
- <span data-ttu-id="0bbe5-115">Verificare che il Database di Azure per la sicurezza della connessione a MySQL è configurato con firewall hello aprire e modificare impostazioni SSL per l'applicazione tooconnect correttamente.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-115">Ensure your Azure Database for MySQL connection security is configured with hello firewall opened and SSL settings adjusted for your application tooconnect successfully.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="0bbe5-116">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="0bbe5-116">Get connection information</span></span>
<span data-ttu-id="0bbe5-117">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="0bbe5-118">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="0bbe5-119">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0bbe5-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0bbe5-120">Nel riquadro di sinistra hello, fare clic su **tutte le risorse**e quindi cercare server hello sia stato creato (ad esempio, **myserver4demo**).</span><span class="sxs-lookup"><span data-stu-id="0bbe5-120">In hello left pane, click **All resources**, and then search for hello server you have created (for example, **myserver4demo**).</span></span>
3. <span data-ttu-id="0bbe5-121">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-121">Click hello server name.</span></span>
4. <span data-ttu-id="0bbe5-122">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="0bbe5-123">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="0bbe5-124">![Nome del server del database di Azure per MySQL](./media/connect-java/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="0bbe5-124">![Azure Database for MySQL server name](./media/connect-java/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="0bbe5-125">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="0bbe5-126">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="0bbe5-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="0bbe5-127">Hello utilizzare codice tooconnect e carico hello dati seguenti utilizzando la funzione hello con un **inserire** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-127">Use hello following code tooconnect and load hello data using hello function with an **INSERT** SQL statement.</span></span> <span data-ttu-id="0bbe5-128">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) metodo è usato tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-128">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0bbe5-129">Metodi [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) ed Execute () vengono utilizzati toodrop e creare la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-129">Methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and execute() are used toodrop and create hello table.</span></span> <span data-ttu-id="0bbe5-130">l'oggetto prepareStatement Hello è toobuild utilizzati i comandi insert hello, con valori di parametro hello toobind setString() e setInt().</span><span class="sxs-lookup"><span data-stu-id="0bbe5-130">hello prepareStatement object is used toobuild hello insert commands, with setString() and setInt() toobind hello parameter values.</span></span> <span data-ttu-id="0bbe5-131">Metodo executeUpdate (paragrafo) esegue il comando hello per ogni set di valori dei parametri tooinsert hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-131">Method executeUpdate() runs hello command for each set of parameters tooinsert hello values.</span></span> 

<span data-ttu-id="0bbe5-132">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-132">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class CreateTableInsertRows {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="read-data"></a><span data-ttu-id="0bbe5-133">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="0bbe5-133">Read data</span></span>
<span data-ttu-id="0bbe5-134">Esempio di codice seguente hello di utilizzare dati hello tooread con un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-134">Use hello following code tooread hello data with a **SELECT** SQL statement.</span></span> <span data-ttu-id="0bbe5-135">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) metodo è usato tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-135">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0bbe5-136">metodi di Hello [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) ed executeQuery() vengono utilizzati tooconnect ed eseguire l'istruzione select hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-136">hello methods [createStatement()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-statements.html) and executeQuery() are used tooconnect and run hello select statement.</span></span> <span data-ttu-id="0bbe5-137">elaborazione dei risultati di Hello utilizzando un [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) oggetto.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-137">hello results are processed using a [ResultSet](https://docs.oracle.com/javase/tutorial/jdbc/basics/retrieving.html) object.</span></span> 

<span data-ttu-id="0bbe5-138">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-138">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class ReadTable {

    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);

            // Set connection properties.
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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
                throw new SQLException("Encountered an error when executing given sql statement", e);
            }       
        }
        else {
            System.out.println("Failed toocreate connection toodatabase."); 
        }
        System.out.println("Execution finished.");
    }
}
```

## <a name="update-data"></a><span data-ttu-id="0bbe5-139">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="0bbe5-139">Update data</span></span>
<span data-ttu-id="0bbe5-140">Esempio di codice seguente hello di utilizzare dati hello toochange con un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-140">Use hello following code toochange hello data with an **UPDATE** SQL statement.</span></span> <span data-ttu-id="0bbe5-141">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) metodo è usato tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-141">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span> <span data-ttu-id="0bbe5-142">metodi di Hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) ed ExecuteUpdate () vengono utilizzati tooprepare ed eseguire l'istruzione update hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-142">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="0bbe5-143">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-143">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class UpdateTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables. 
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";

        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }
        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");

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

## <a name="delete-data"></a><span data-ttu-id="0bbe5-144">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="0bbe5-144">Delete data</span></span>
<span data-ttu-id="0bbe5-145">Esempio di codice seguente hello di utilizzare dati tooremove con un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-145">Use hello following code tooremove data with a **DELETE** SQL statement.</span></span> <span data-ttu-id="0bbe5-146">Hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) metodo è usato tooconnect tooMySQL.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-146">hello [getConnection()](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-usagenotes-connect-drivermanager.html) method is used tooconnect tooMySQL.</span></span>  <span data-ttu-id="0bbe5-147">metodi di Hello [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) ed ExecuteUpdate () vengono utilizzati tooprepare ed eseguire l'istruzione update hello.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-147">hello methods [prepareStatement()](http://docs.oracle.com/javase/tutorial/jdbc/basics/prepared.html) and executeUpdate() are used tooprepare and run hello update statement.</span></span> 

<span data-ttu-id="0bbe5-148">Sostituire l'host hello, database, utente e password parametri con valori di hello specificato al momento della creazione di server e database.</span><span class="sxs-lookup"><span data-stu-id="0bbe5-148">Replace hello host, database, user, and password parameters with hello values that you specified when you created your own server and database.</span></span>

```java
import java.sql.*;
import java.util.Properties;

public class DeleteTable {
    public static void main (String[] args)  throws Exception
    {
        // Initialize connection variables.
        String host = "myserver4demo.mysql.database.azure.com";
        String database = "quickstartdb";
        String user = "myadmin@myserver4demo";
        String password = "<server_admin_password>";
        
        // check that hello driver is installed
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
        }
        catch (ClassNotFoundException e)
        {
            throw new ClassNotFoundException("MySQL JDBC driver NOT detected in library path.", e);
        }

        System.out.println("MySQL JDBC driver detected in library path.");

        Connection connection = null;

        // Initialize connection object
        try
        {
            String url = String.format("jdbc:mysql://%s/%s", host, database);
            
            // set up hello connection properties
            Properties properties = new Properties();
            properties.setProperty("user", user);
            properties.setProperty("password", password);
            properties.setProperty("useSSL", "true");
            properties.setProperty("verifyServerCertificate", "true");
            properties.setProperty("requireSSL", "false");
            
            // get connection
            connection = DriverManager.getConnection(url, properties);
        }
        catch (SQLException e)
        {
            throw new SQLException("Failed toocreate connection toodatabase", e);
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

## <a name="next-steps"></a><span data-ttu-id="0bbe5-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0bbe5-149">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="0bbe5-150">Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL</span><span class="sxs-lookup"><span data-stu-id="0bbe5-150">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
