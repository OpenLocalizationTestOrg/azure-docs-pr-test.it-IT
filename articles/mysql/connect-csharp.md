---
title: Connettersi a Database di Azure per MySQL da C# | Microsoft Docs
description: "Questa guida introduttiva offre un esempio di codice C# (.NET) che è possibile usare per connettersi ed eseguire query sui dati da Database di Azure per MySQL."
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
ms.openlocfilehash: f1488f6b4a240165c71c95f759af73d6b9fd7bfe
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="azure-database-for-mysql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="fee49-103">Database di Azure per MySQL: usare .NET (C#) per connettersi ed eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="fee49-103">Azure Database for MySQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="fee49-104">Questa guida introduttiva illustra come connettersi a un database di Azure per MySQL usando un'applicazione C#.</span><span class="sxs-lookup"><span data-stu-id="fee49-104">This quickstart demonstrates how to connect to an Azure Database for MySQL using a C# application.</span></span> <span data-ttu-id="fee49-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="fee49-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="fee49-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con C#, ma non con Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fee49-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fee49-107">Prerequisites</span></span>
<span data-ttu-id="fee49-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="fee49-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="fee49-109">Creare un database di Azure per il server MySQL tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="fee49-109">Create an Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
- [<span data-ttu-id="fee49-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="fee49-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

<span data-ttu-id="fee49-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="fee49-111">You also need to:</span></span>
- <span data-ttu-id="fee49-112">Installare [.NET](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="fee49-112">Install [.NET](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="fee49-113">Seguire la procedura descritta nell'articolo collegato per installare .NET per la specifica piattaforma in uso (Windows, Ubuntu Linux o macOS).</span><span class="sxs-lookup"><span data-stu-id="fee49-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="fee49-114">[Installare Visual Studio](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fee49-114">Install [Visual Studio](https://www.visualstudio.com/downloads/).</span></span>
- <span data-ttu-id="fee49-115">Installare il [driver ODBC per MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span><span class="sxs-lookup"><span data-stu-id="fee49-115">Install [ODBC Driver for MySQL](https://dev.mysql.com/downloads/connector/odbc/).</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="fee49-116">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="fee49-116">Get connection information</span></span>
<span data-ttu-id="fee49-117">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-117">Get the connection information needed to connect to the Azure Database for MySQL.</span></span> <span data-ttu-id="fee49-118">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="fee49-118">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="fee49-119">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fee49-119">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="fee49-120">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="fee49-120">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="fee49-121">Fare clic sul nome del server.</span><span class="sxs-lookup"><span data-stu-id="fee49-121">Click the server name.</span></span>
4. <span data-ttu-id="fee49-122">Selezionare la pagina **Proprietà** del server.</span><span class="sxs-lookup"><span data-stu-id="fee49-122">Select the server's **Properties** page.</span></span> <span data-ttu-id="fee49-123">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="fee49-123">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="fee49-124">![Nome del server del database di Azure per MySQL](./media/connect-csharp/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="fee49-124">![Azure Database for MySQL server name](./media/connect-csharp/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="fee49-125">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="fee49-125">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="fee49-126">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="fee49-126">Connect, create table, and insert data</span></span>
<span data-ttu-id="fee49-127">Usare il codice seguente per connettersi e caricare i dati usando le istruzioni SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="fee49-127">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="fee49-128">Il codice usa la classe ODBC con il metodo [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-128">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="fee49-129">Il codice usa quindi il metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="fee49-129">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span> 

<span data-ttu-id="fee49-130">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="fee49-130">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }

    }
}

```

## <a name="read-data"></a><span data-ttu-id="fee49-131">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="fee49-131">Read data</span></span>

<span data-ttu-id="fee49-132">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="fee49-132">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="fee49-133">Il codice usa la classe ODBC con il metodo [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-133">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="fee49-134">Il codice usa quindi il metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) e il metodo [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="fee49-134">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx) and method [ExecuteReader()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executereader(v=vs.110).aspx) to run the database commands.</span></span> <span data-ttu-id="fee49-135">Il codice usa poi [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) per passare ai record nei risultati.</span><span class="sxs-lookup"><span data-stu-id="fee49-135">Next the code uses [Read()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcdatareader.read(v=vs.110).aspx) to advance to the records in the results.</span></span> <span data-ttu-id="fee49-136">Il codice usa quindi GetInt32 e GetString per analizzare i valori nel record.</span><span class="sxs-lookup"><span data-stu-id="fee49-136">Then the code uses GetInt32 and GetString to parse the values in the record.</span></span>

<span data-ttu-id="fee49-137">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="fee49-137">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}


```

## <a name="update-data"></a><span data-ttu-id="fee49-138">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="fee49-138">Update data</span></span>
<span data-ttu-id="fee49-139">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="fee49-139">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="fee49-140">Il codice usa la classe ODBC con il metodo [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-140">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="fee49-141">Il codice usa quindi il metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="fee49-141">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="fee49-142">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="fee49-142">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}



```


## <a name="delete-data"></a><span data-ttu-id="fee49-143">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="fee49-143">Delete data</span></span>
<span data-ttu-id="fee49-144">Usare il codice seguente per connettersi ed eliminare i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="fee49-144">Use the following code to connect and delete the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="fee49-145">Il codice usa la classe ODBC con il metodo [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) per stabilire una connessione a MySQL.</span><span class="sxs-lookup"><span data-stu-id="fee49-145">The code uses ODBC class with method [Open()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.open(v=vs.110).aspx) to establish a connection to MySQL.</span></span> <span data-ttu-id="fee49-146">Il codice usa quindi il metodo [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="fee49-146">Then the code uses method [CreateCommand()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbcconnection.createcommand(v=vs.110).aspx), sets the CommandText property, and calls method [ExecuteNonQuery()](https://msdn.microsoft.com/en-us/library/system.data.odbc.odbccommand.executenonquery(v=vs.110).aspx) to run the database commands.</span></span>

<span data-ttu-id="fee49-147">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="fee49-147">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

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

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}

```

## <a name="next-steps"></a><span data-ttu-id="fee49-148">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fee49-148">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="fee49-149">Eseguire la migrazione del database MySQL a Database di Azure per MySQL usando dump e ripristino</span><span class="sxs-lookup"><span data-stu-id="fee49-149">Migrate your MySQL database to Azure Database for MySQL using dump and restore</span></span>](concepts-migrate-dump-restore.md)
