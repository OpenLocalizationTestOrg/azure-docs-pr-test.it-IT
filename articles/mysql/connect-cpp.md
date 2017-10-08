---
title: La connessione tooAzure Database MySQL da C++ | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice C++, è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
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
ms.openlocfilehash: d027597bf02b1eacab9b8808957399f6e54e63cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-connectorc-tooconnect-and-query-data"></a><span data-ttu-id="78f69-103">Il Database di Azure per MySQL: dati tooconnect e query di utilizzare connettore/C++</span><span class="sxs-lookup"><span data-stu-id="78f69-103">Azure Database for MySQL: Use Connector/C++ tooconnect and query data</span></span>
<span data-ttu-id="78f69-104">Questa Guida introduttiva illustra come Database di Azure tooconnect tooan per MySQL mediante un'applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="78f69-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C++ application.</span></span> <span data-ttu-id="78f69-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="78f69-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="78f69-106">Hello passaggi in questo articolo si presuppone che si ha familiarità con lo sviluppo usando C++ e che siano tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-106">hello steps in this article assume that you are familiar with developing using C++, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78f69-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="78f69-107">Prerequisites</span></span>
<span data-ttu-id="78f69-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="78f69-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="78f69-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="78f69-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="78f69-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="78f69-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="78f69-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="78f69-111">You also need to:</span></span>
- <span data-ttu-id="78f69-112">Installare [.NET Framework](https://www.microsoft.com/net/download)</span><span class="sxs-lookup"><span data-stu-id="78f69-112">Install [.NET Framework](https://www.microsoft.com/net/download)</span></span>
- <span data-ttu-id="78f69-113">Installare [Visual Studio](https://www.visualstudio.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="78f69-113">Install [Visual Studio](https://www.visualstudio.com/downloads/)</span></span>
- <span data-ttu-id="78f69-114">Installare [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span><span class="sxs-lookup"><span data-stu-id="78f69-114">Install [MySQL Connector/C++](https://dev.mysql.com/downloads/connector/cpp/)</span></span> 
- <span data-ttu-id="78f69-115">Installare [Boost](http://www.boost.org/)</span><span class="sxs-lookup"><span data-stu-id="78f69-115">Install [Boost](http://www.boost.org/)</span></span>

## <a name="install-visual-studio-and-net"></a><span data-ttu-id="78f69-116">Installare Visual Studio e .NET</span><span class="sxs-lookup"><span data-stu-id="78f69-116">Install Visual Studio and .NET</span></span>
<span data-ttu-id="78f69-117">passaggi di Hello in questa sezione si presuppongono che si abbia familiarità con lo sviluppo con .NET.</span><span class="sxs-lookup"><span data-stu-id="78f69-117">hello steps in this section assume that you are familiar with developing using .NET.</span></span>

### <a name="windows"></a><span data-ttu-id="78f69-118">**Windows**</span><span class="sxs-lookup"><span data-stu-id="78f69-118">**Windows**</span></span>
1. <span data-ttu-id="78f69-119">Installare Visual Studio 2017 Community, che è un IDE gratuito, con funzionalità complete ed estendibile per creare applicazioni moderne per Android, iOS, Windows, oltre ad applicazioni Web e database e servizi cloud.</span><span class="sxs-lookup"><span data-stu-id="78f69-119">Install Visual Studio 2017 Community, which is a full featured, extensible, free IDE for creating modern applications for Android, iOS, Windows, as well as web & database applications and cloud services.</span></span> <span data-ttu-id="78f69-120">È possibile installare hello completa di .NET Framework o solo a .NET Core.</span><span class="sxs-lookup"><span data-stu-id="78f69-120">You can install either hello full .NET Framework or just .NET Core.</span></span> <span data-ttu-id="78f69-121">frammenti di codice Hello hello Guida introduttiva di lavoro con uno.</span><span class="sxs-lookup"><span data-stu-id="78f69-121">hello code snippets in hello Quickstart work with either.</span></span> <span data-ttu-id="78f69-122">Se si dispone già di Visual Studio installati nel computer, ignorare hello due passaggi successivi.</span><span class="sxs-lookup"><span data-stu-id="78f69-122">If you already have Visual Studio installed on your machine, skip hello next two steps.</span></span>
   - <span data-ttu-id="78f69-123">Scaricare hello [programma di installazione di Visual Studio 2017](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span><span class="sxs-lookup"><span data-stu-id="78f69-123">Download hello [Visual Studio 2017 installer](https://www.visualstudio.com/thank-you-downloading-visual-studio/?sku=Community&rel=15).</span></span> 
   - <span data-ttu-id="78f69-124">Eseguire il programma di installazione hello e seguire hello installazione richieste toocomplete hello installazione.</span><span class="sxs-lookup"><span data-stu-id="78f69-124">Run hello installer and follow hello installation prompts toocomplete hello installation.</span></span>

### <a name="configure-visual-studio"></a><span data-ttu-id="78f69-125">**Configurare Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="78f69-125">**Configure Visual Studio**</span></span>
1. <span data-ttu-id="78f69-126">Da Visual Studio, proprietà del progetto > proprietà di configurazione > C/C++ > linker > generale > Directory librerie aggiuntive, aggiungere directory lib\opt hello (ad esempio: C:\Program Files (x86) \MySQL\MySQL connettore C++ 1.1.9\lib\opt) di hello c + + connettore.</span><span class="sxs-lookup"><span data-stu-id="78f69-126">From Visual Studio, project property > configuration properties > C/C++ > linker > general > additional library directories, add hello lib\opt directory (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\lib\opt) of hello c++ connector.</span></span>
2. <span data-ttu-id="78f69-127">Da Visual Studio, Proprietà progetto > Proprietà di configurazione > C/C++ > Generale > Directory di inclusione aggiuntive</span><span class="sxs-lookup"><span data-stu-id="78f69-127">From Visual Studio, project property > configuration properties > C/C++ > general > additional include directories</span></span>
   - <span data-ttu-id="78f69-128">Aggiungere la directory include/ del connettore C++ (ad esempio: C:\Programmi (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span><span class="sxs-lookup"><span data-stu-id="78f69-128">Add include/ directory of c++ connector (i.e.: C:\Program Files (x86)\MySQL\MySQL Connector C++ 1.1.9\include\)</span></span>
   - <span data-ttu-id="78f69-129">Aggiungere la directory radice della libreria Boost (ad esempio: C:\boost_1_64_0\)</span><span class="sxs-lookup"><span data-stu-id="78f69-129">Add Boost library's root directory (i.e.: C:\boost_1_64_0\)</span></span>
3. <span data-ttu-id="78f69-130">Da Visual Studio, proprietà del progetto > proprietà di configurazione > C/C++ > linker > Input > dipendenze aggiuntive, aggiungere mysqlcppconn.lib nel campo di testo hello</span><span class="sxs-lookup"><span data-stu-id="78f69-130">From Visual Studio, project property > configuration properties > C/C++ > linker > Input > Additional Dependencies, add mysqlcppconn.lib into hello text field</span></span>
4. <span data-ttu-id="78f69-131">Entrambi mysqlcppconn.dll copia dalla hello c + + connettore cartella libreria nel passaggio 3 toohello stessa directory del file eseguibile dell'applicazione hello o aggiungere la variabile di ambiente toohello poterlo trovare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="78f69-131">Either copy mysqlcppconn.dll from hello c++ connector library folder in step 3 toohello same directory as hello application executable or add it toohello environment variable so your application can find it.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="78f69-132">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="78f69-132">Get connection information</span></span>
<span data-ttu-id="78f69-133">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-133">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="78f69-134">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="78f69-134">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="78f69-135">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="78f69-135">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="78f69-136">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="78f69-136">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="78f69-137">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="78f69-137">Click hello server name.</span></span>
4. <span data-ttu-id="78f69-138">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="78f69-138">Select hello server's **Properties** page.</span></span> <span data-ttu-id="78f69-139">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="78f69-139">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="78f69-140">![Nome del server del database di Azure per MySQL](./media/connect-cpp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="78f69-140">![Azure Database for MySQL server name](./media/connect-cpp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="78f69-141">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="78f69-141">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="78f69-142">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="78f69-142">Connect, create table, and insert data</span></span>
<span data-ttu-id="78f69-143">Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-143">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="78f69-144">codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="78f69-144">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="78f69-145">Codice hello utilizza quindi metodo Execute () e createStatement() toorun hello i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="78f69-145">Then hello code uses method createStatement() and execute() toorun hello database commands.</span></span> 

<span data-ttu-id="78f69-146">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="78f69-146">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="read-data"></a><span data-ttu-id="78f69-147">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="78f69-147">Read data</span></span>

<span data-ttu-id="78f69-148">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-148">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="78f69-149">codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="78f69-149">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="78f69-150">Quindi codice hello Usa metodo prepareStatement() ed executeQuery() toorun hello selezionare comandi.</span><span class="sxs-lookup"><span data-stu-id="78f69-150">Then hello code uses method prepareStatement() and executeQuery() toorun hello select commands.</span></span> <span data-ttu-id="78f69-151">Codice di hello utilizzerà infine Next tooadvance toohello record nei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="78f69-151">Finally hello code uses next() tooadvance toohello records in hello results.</span></span> <span data-ttu-id="78f69-152">Codice hello Usa quindi i valori hello tooparse getInt() e GetString () nel record di hello.</span><span class="sxs-lookup"><span data-stu-id="78f69-152">Then hello code uses getInt() and getString() tooparse hello values in hello record.</span></span>

<span data-ttu-id="78f69-153">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="78f69-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="update-data"></a><span data-ttu-id="78f69-154">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="78f69-154">Update data</span></span>
<span data-ttu-id="78f69-155">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-155">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="78f69-156">codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="78f69-156">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="78f69-157">Codice hello utilizza quindi metodo prepareStatement() ed executeQuery() toorun hello i comandi di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="78f69-157">Then hello code uses method prepareStatement() and executeQuery() toorun hello update commands.</span></span> 

<span data-ttu-id="78f69-158">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="78f69-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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


## <a name="delete-data"></a><span data-ttu-id="78f69-159">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="78f69-159">Delete data</span></span>
<span data-ttu-id="78f69-160">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="78f69-160">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> <span data-ttu-id="78f69-161">codice Hello Usa la classe sql::Driver con hello Connect () metodo tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="78f69-161">hello code uses sql::Driver class with hello connect() method tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="78f69-162">Usa metodo prepareStatement() quindi codice hello executeQuery() toorun hello comandi e delete.</span><span class="sxs-lookup"><span data-stu-id="78f69-162">Then hello code uses method prepareStatement() and executeQuery() toorun hello delete commands.</span></span>

<span data-ttu-id="78f69-163">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="78f69-163">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        //for demonstration only. never save password in hello code!
        con = driver>connect("tcp://myserver4demo.mysql.database.azure.com:3306/quickstartdb", "myadmin@myserver4demo", "server_admin_password");
    }
    catch (sql::SQLException e)
    {
        cout << "Could not connect toodatabase. Error message: " << e.what() << endl;
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

## <a name="next-steps"></a><span data-ttu-id="78f69-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="78f69-164">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="78f69-165">Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL</span><span class="sxs-lookup"><span data-stu-id="78f69-165">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
