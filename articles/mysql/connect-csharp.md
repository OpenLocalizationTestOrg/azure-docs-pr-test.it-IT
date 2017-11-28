---
title: La connessione tooAzure Database MySQL da c# | Documenti Microsoft
description: "Questa Guida rapida viene fornito un esempio codice c# (.NET) è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: MySQL
author: seanli1988
ms.author: seal
manager: janders
editor: jasonwhowell
ms.service: MySQL-database
ms.custom: mvc
ms.devlang: csharp
ms.topic: hero-article
ms.date: 07/10/2017
ms.openlocfilehash: 0dca98186199a40ef9cc592b93c3b2e815260273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="547af-103">Il Database di Azure per MySQL: dati tooconnect e query di utilizzo di .NET (c#)</span><span class="sxs-lookup"><span data-stu-id="547af-103">Azure Database for MySQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="547af-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di un'applicazione c# di MySQL.</span><span class="sxs-lookup"><span data-stu-id="547af-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="547af-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="547af-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="547af-106">Hello passaggi in questo articolo si presuppone che si abbia familiarità con lo sviluppo in c#, e che siano tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="547af-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="547af-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="547af-107">Prerequisites</span></span>
<span data-ttu-id="547af-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="547af-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="547af-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="547af-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="547af-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="547af-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="547af-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="547af-111">You also need to:</span></span>
- <span data-ttu-id="547af-112">Installare [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="547af-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="547af-113">Seguire passaggi hello hello collegato articolo tooinstall .NET in modo specifico per la piattaforma (Windows, Ubuntu Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="547af-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="547af-114">[Installare Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="547af-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="547af-115">Installare il [driver ODBC per MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="547af-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="547af-116">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="547af-116">Get connection information</span></span>
<span data-ttu-id="547af-117">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="547af-117">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="547af-118">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="547af-118">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="547af-119">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="547af-119">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="547af-120">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="547af-120">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="547af-121">Fare clic su nome hello del server.</span><span class="sxs-lookup"><span data-stu-id="547af-121">Click hello server name.</span></span>
4. <span data-ttu-id="547af-122">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="547af-122">Select hello server's **Properties** page.</span></span> <span data-ttu-id="547af-123">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="547af-123">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="547af-124">![Nome del server del database di Azure per MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="547af-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="547af-125">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="547af-125">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="547af-126">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="547af-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="547af-127">Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="547af-127">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="547af-128">codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="547af-128">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="547af-129">Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="547af-129">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span> 

<span data-ttu-id="547af-130">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="547af-130">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;

namespace driver
{
    class MySQLCreate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                    INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                    INSERT INTO inventory (name, quantity) VALUES ({4}, {5});",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="547af-131">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="547af-131">Read data</span></span>

<span data-ttu-id="547af-132">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="547af-132">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="547af-133">codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="547af-133">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="547af-134">Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) e metodo [ExecuteReader](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="547af-134">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) toorun hello database commands.</span></span> <span data-ttu-id="547af-135">Successivamente hello viene utilizzato codice [Read](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello record nei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="547af-135">Next hello code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="547af-136">Codice hello Usa quindi i valori hello tooparse GetInt32 e GetString nel record di hello.</span><span class="sxs-lookup"><span data-stu-id="547af-136">Then hello code uses GetInt32 and GetString tooparse hello values in hello record.</span></span>

<span data-ttu-id="547af-137">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="547af-137">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MySql.Data;
using System.Data.Odbc;


namespace driver
{
    class MySQLRead
    {

        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="547af-138">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="547af-138">Update data</span></span>
<span data-ttu-id="547af-139">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="547af-139">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="547af-140">codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="547af-140">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="547af-141">Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="547af-141">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="547af-142">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="547af-142">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLUpdate
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="547af-143">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="547af-143">Delete data</span></span>
<span data-ttu-id="547af-144">Seguente hello utilizzare codice tooconnect ed eliminare hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="547af-144">Use hello following code tooconnect and delete hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="547af-145">codice Hello utilizza la classe ODBC con metodo [Open ()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish tooMySQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="547af-145">hello code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) tooestablish a connection tooMySQL.</span></span> <span data-ttu-id="547af-146">Quindi codice hello Usa metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="547af-146">Then hello code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets hello CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) toorun hello database commands.</span></span>

<span data-ttu-id="547af-147">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="547af-147">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Data.Odbc;

namespace driver
{
    class MySQLDelete
    {
        static void Main(string[] args)
        {
            var conn = new OdbcConnection("DRIVER={MySQL ODBC 5.3 unicode Driver}; Server=myserver4demo.mysql.database.azure.com; Port=3306;" +
            " Database=quickstartdb; Uid=myadmin@myserver4demo; Pwd=server_admin_password; sslverify=0; Option=3;MULTI_STATEMENTS=1");

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
                String.Format("DELETE FROM inventory WHERE name = {0};",
                    "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="547af-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="547af-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="547af-149">Eseguire la migrazione del tooAzure database MySQL Database per utilizzo dump e ripristino di MySQL</span><span class="sxs-lookup"><span data-stu-id="547af-149">Migrate your MySQL database tooAzure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
