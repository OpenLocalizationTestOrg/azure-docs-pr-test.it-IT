---
title: Connettersi a Database di Azure per MySQL da C++ | Microsoft Docs
description: "Questa guida introduttiva offre un esempio di codice C++ che è possibile usare per connettersi ed eseguire query sui dati da Database di Azure per MySQL."
services: mysql
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: C++
ms.topic: hero-article
ms.date: 08/03/2017
ms.openlocfilehash: 63388b83b913d95136140fa4c56af0dbebbdad81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-connectorc-to-connect-and-query-data"></a><span data-ttu-id="68941-103">Database di Azure per MySQL: usare Connector/C++ per connettersi ed eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="68941-103">Azure Database for MySQL: Use Connector/C++ to connect and query data</span></span>
<span data-ttu-id="68941-104">Questa guida introduttiva illustra come connettersi a un database di Azure per MySQL usando un'applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="68941-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="68941-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="68941-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="68941-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con C++, ma non con Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-106">The steps in this article assume that you are familiar with developing using C++, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68941-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="68941-107">Prerequisites</span></span>
<span data-ttu-id="68941-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="68941-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="68941-109">Creare un database di Azure per il server MySQL tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="68941-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="68941-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="68941-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="68941-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="68941-111">You also need to:</span></span>
- <span data-ttu-id="68941-112">Installare [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="68941-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="68941-113">Installare [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="68941-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="68941-114">Installare [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="68941-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="68941-115">Installare [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="68941-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="68941-116">Installare Visual Studio e .NET</span><span class="sxs-lookup"><span data-stu-id="68941-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="68941-117">La procedura descritta in questa sezione presuppone che si abbia familiarità con lo sviluppo con .NET.</span><span class="sxs-lookup"><span data-stu-id="68941-117">The steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="68941-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="68941-118">**Windows**</span></span>
1. <span data-ttu-id="68941-119">Installare Visual Studio 2017 Community, che è un IDE gratuito, con funzionalità complete ed estendibile per creare applicazioni moderne per Android, iOS, Windows, oltre ad applicazioni Web e database e servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="68941-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="68941-120">È possibile installare la versione completa di .NET Framework o solamente .NET Core.</span><span class="sxs-lookup"><span data-stu-id="68941-120">You can install either the full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="68941-121">I frammenti di codice nella guida introduttiva sono compatibili con entrambe le versioni.</span><span class="sxs-lookup"><span data-stu-id="68941-121">The code snippets in the Quickstart work with either.</span></span> <span data-ttu-id="68941-122">Se Visual Studio è già installato nel computer, ignorare i due passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="68941-122">If you already have Visual Studio installed on your machine, skip the next two steps.</span></span>
   - <span data-ttu-id="68941-123">Scaricare il [programma di installazione di Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="68941-123">Download the [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="68941-124">Eseguire il programma di installazione e seguire le richieste di installazione per completare l'operazione.</span><span class="sxs-lookup"><span data-stu-id="68941-124">Run the installer and follow the installation prompts to complete the installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="68941-125">**Configurare Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="68941-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="68941-126">Da Visual Studio, Proprietà progetto > Proprietà di configurazione > C/C++ > Linker > Generale > Directory librerie aggiuntive, aggiungere la directory lib\opt (ad esempio: C:\Programmi (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) del connettore C++.</span><span class="sxs-lookup"><span data-stu-id="68941-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add the lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of the c++ connector.</span></span>
2. <span data-ttu-id="68941-127">Da Visual Studio, Proprietà progetto > Proprietà di configurazione > C/C++ > Generale > Directory di inclusione aggiuntive</span><span class="sxs-lookup"><span data-stu-id="68941-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="68941-128">Aggiungere la directory include/ del connettore C++ (ad esempio: C:\Programmi (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="68941-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="68941-129">Aggiungere la directory radice della libreria Boost (ad esempio: C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="68941-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="68941-130">Da Visual Studio, Proprietà progetto > Proprietà di configurazione > C/C++ > Linker > Input > Dipendenze aggiuntive, aggiungere mysqlcppconn.lib nel campo di testo</span><span class="sxs-lookup"><span data-stu-id="68941-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into the text field</span></span>
4. <span data-ttu-id="68941-131">Copiare mysqlcppconn.dll dalla cartella della libreria del connettore C++ del passaggio 3 alla stessa directory del file eseguibile dell'applicazione oppure aggiungerlo alla variabile di ambiente in modo che l'applicazione possa trovarlo.</span><span class="sxs-lookup"><span data-stu-id="68941-131">Either copy mysqlcppconn.dll from the c++ connector library folder in step 3 to the same directory as the application executable or add it to the environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="68941-132">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="68941-132">Get connection information</span></span>
<span data-ttu-id="68941-133">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-133">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="68941-134">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="68941-134">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="68941-135">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="68941-135">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="68941-136">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="68941-136">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="68941-137">Fare clic sul nome del server.</span><span class="sxs-lookup"><span data-stu-id="68941-137">Click the server name.</span></span>
4. <span data-ttu-id="68941-138">Selezionare la pagina **Proprietà** del server.</span><span class="sxs-lookup"><span data-stu-id="68941-138">Select the server's **Properties** page.</span></span> <span data-ttu-id="68941-139">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="68941-139">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="68941-140">![Nome del server del database di Azure per MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="68941-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="68941-141">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="68941-141">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="68941-142">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="68941-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="68941-143">Usare il codice seguente per connettersi e caricare i dati usando le istruzioni SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="68941-143">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="68941-144">Il codice usa la classe sql::Driver con il metodo connect() per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-144">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="68941-145">Il codice usa quindi il metodo createStatement() e il metodo execute() per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="68941-145">Then the code uses method createStatement() and execute() to run the database commands.</span></span> 

<span data-ttu-id="68941-146">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="68941-146">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```c++
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::Statement *stmt;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }

    stmt = con>createStatement();
    stmt>execute("DROP TABLE IF EXISTS inventory");
    cout << "Finished dropping table (if existed)" << endl;
    stmt>execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);");
    cout << "Finished creating table" << endl;
    delete stmt;

    pstmt = con>prepareStatement("INSERT INTO inventory(name, quantity) VALUES(?,?)");
    pstmt>setString(1, "banana");
    pstmt>setInt(2, 150);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "orange");
    pstmt>setInt(2, 154);
    pstmt>execute();
    cout << "One row inserted." << endl;

    pstmt>setString(1, "apple");
    pstmt>setInt(2, 100);
    pstmt>execute();
    cout << "One row inserted." << endl;
    
    delete pstmt;   
    delete con;
    system("pause");
    return 0;

```

## <a name="read-data"></a><span data-ttu-id="68941-147">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="68941-147">Read data</span></span>

<span data-ttu-id="68941-148">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="68941-148">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="68941-149">Il codice usa la classe sql::Driver con il metodo connect() per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-149">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="68941-150">Il codice usa quindi il metodo prepareStatement() e il metodo executeQuery() per eseguire i comandi di selezione.</span><span class="sxs-lookup"><span data-stu-id="68941-150">Then the code uses method prepareStatement() and executeQuery() to run the select commands.</span></span> <span data-ttu-id="68941-151">Il codice usa infine next() per passare ai record nei risultati.</span><span class="sxs-lookup"><span data-stu-id="68941-151">Finally the code uses next() to advance to the records in the results.</span></span> <span data-ttu-id="68941-152">Il codice usa quindi getInt() e getString() per analizzare i valori nel record.</span><span class="sxs-lookup"><span data-stu-id="68941-152">Then the code uses getInt() and getString() to parse the values in the record.</span></span>

<span data-ttu-id="68941-153">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="68941-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

//  select  
    pstmt = con>prepareStatement("SELECT * FROM inventory;");
    result = pstmt>executeQuery();  
    
    while (result>next())
        printf("Reading from table=(%d, %s, %d)\n", result>getInt(1), result>getString(2).c_str(), result>getInt(3));   
    
    delete result;
    delete pstmt;   
    delete con;
    system("pause");
    return 0;
}
```

## <a name="update-data"></a><span data-ttu-id="68941-154">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="68941-154">Update data</span></span>
<span data-ttu-id="68941-155">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="68941-155">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="68941-156">Il codice usa la classe sql::Driver con il metodo connect() per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-156">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="68941-157">Il codice usa quindi il metodo prepareStatement() e il metodo executeQuery() per eseguire i comandi di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="68941-157">Then the code uses method prepareStatement() and executeQuery() to run the update commands.</span></span> 

<span data-ttu-id="68941-158">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="68941-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }   

    //update
    pstmt = con>prepareStatement("UPDATE inventory SET quantity = ? WHERE name = ?");
    pstmt>setInt(1, 200);
    pstmt>setString(2, "banana");
    pstmt>executeQuery();
    printf("Row updated\n");
    
    delete con;
    delete pstmt;
    system("pause");
    return 0;
}
```


## <a name="delete-data"></a><span data-ttu-id="68941-159">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="68941-159">Delete data</span></span>
<span data-ttu-id="68941-160">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="68941-160">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="68941-161">Il codice usa la classe sql::Driver con il metodo connect() per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="68941-161">The code uses sql::Driver class with the connect() method to establish a connection to MySQL.</span></span> <span data-ttu-id="68941-162">Il codice usa quindi il metodo prepareStatement() e il metodo executeQuery() per eseguire i comandi di eliminazione.</span><span class="sxs-lookup"><span data-stu-id="68941-162">Then the code uses method prepareStatement() and executeQuery() to run the delete commands.</span></span>

<span data-ttu-id="68941-163">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="68941-163">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
#include <stdlib.h>
#include <iostream>
#include "stdafx.h"

#include "mysql_connection.h"
#include <cppconn/driver.h>
#include <cppconn/exception.h>
#include <cppconn/resultset.h>
#include <cppconn/prepared_statement.h>
using namespace std;

int main()
{
    sql::Driver *driver;
    sql::Connection *con;
    sql::PreparedStatement *pstmt;
    sql::ResultSet *result;

    try
    {
        driver = get_driver_instance();
        //for demonstration only. never save password in the code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect to database. Error message: " << e.what() << endl;
        system("pause");
        exit(1);
    }
        
    //delete
    pstmt = con>prepareStatement("DELETE FROM inventory WHERE name = ?");
    pstmt>setString(1, "orange");
    result = pstmt>executeQuery();
    printf("Row deleted\n");    
    
    delete pstmt;
    delete con;
    delete result;
    system("pause");
    return 0;
}
```

## <a name="next-steps"></a><span data-ttu-id="68941-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="68941-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="68941-165">Eseguire la migrazione del database MySQL a Database di Azure per MySQL usando dump e ripristino</span><span class="sxs-lookup"><span data-stu-id="68941-165">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
