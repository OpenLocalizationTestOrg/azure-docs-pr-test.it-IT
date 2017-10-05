---
title: Connettersi a Database di Azure per PostgreSQL da C# | Microsoft Docs
description: "Questa guida introduttiva fornisce un esempio di codice C# (.NET) che è possibile usare per connettersi ai dati ed eseguire query da Database di Azure per PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="e717b-103">Database di Azure per PostgreSQL: usare .NET (C#) per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="e717b-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="e717b-104">Questa guida introduttiva illustra come connettersi a un database di Azure per PostgreSQL usando un'applicazione C#.</span><span class="sxs-lookup"><span data-stu-id="e717b-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="e717b-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="e717b-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="e717b-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con C#, ma non con Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e717b-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e717b-107">Prerequisites</span></span>
<span data-ttu-id="e717b-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="e717b-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="e717b-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="e717b-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="e717b-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="e717b-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="e717b-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="e717b-111">You also need to:</span></span>
- <span data-ttu-id="e717b-112">Installare [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="e717b-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="e717b-113">Seguire la procedura descritta nell'articolo collegato per installare .NET per la specifica piattaforma in uso (Windows, Ubuntu Linux o macOS).</span><span class="sxs-lookup"><span data-stu-id="e717b-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="e717b-114">Installare [Visual Studio](https://www.visualstudio.com/downloads/) o Visual Studio Code per digitare e modificare il codice.</span><span class="sxs-lookup"><span data-stu-id="e717b-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="e717b-115">Installare la libreria [Npgsql](http://www.npgsql.org/doc/index.html) come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="e717b-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="e717b-116">Installare i riferimenti Npgsql nella soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e717b-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="e717b-117">Per stabilire la connessione dall'applicazione C# a PostgreSQL, usare la libreria open source ADO.NET denominata Npgsql.</span><span class="sxs-lookup"><span data-stu-id="e717b-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="e717b-118">NuGet consente di scaricare e gestire facilmente i riferimenti.</span><span class="sxs-lookup"><span data-stu-id="e717b-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="e717b-119">Creare una nuova soluzione C# o aprirne una esistente:</span><span class="sxs-lookup"><span data-stu-id="e717b-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="e717b-120">In Visual Studio creare una soluzione scegliendo **Nuovo** > **Progetto** dal menu File.</span><span class="sxs-lookup"><span data-stu-id="e717b-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="e717b-121">Nella finestra di dialogo Nuovo progetto espandere **Modelli** > **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="e717b-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="e717b-122">Scegliere un modello appropriato, ad esempio **Console App (.NET Core)** (App console - .NET Core).</span><span class="sxs-lookup"><span data-stu-id="e717b-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="e717b-123">Usare Gestione pacchetti NuGet per installare Npgsql:</span><span class="sxs-lookup"><span data-stu-id="e717b-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="e717b-124">Scegliere **Gestione pacchetti NuGet** dal menu **Strumenti** > **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="e717b-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="e717b-125">In **Console di Gestione pacchetti** digitare `Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="e717b-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="e717b-126">Il comando di installazione scarica Npgsql.dll e gli assembly correlati e li aggiunge come dipendenze nella soluzione.</span><span class="sxs-lookup"><span data-stu-id="e717b-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="e717b-127">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="e717b-127">Get connection information</span></span>
<span data-ttu-id="e717b-128">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="e717b-129">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="e717b-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="e717b-130">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e717b-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e717b-131">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="e717b-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="e717b-132">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="e717b-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="e717b-133">Selezionare la pagina **Panoramica** del server.</span><span class="sxs-lookup"><span data-stu-id="e717b-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="e717b-134">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="e717b-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="e717b-135">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="e717b-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="e717b-136">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="e717b-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="e717b-137">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="e717b-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="e717b-138">Usare il codice seguente per connettersi e caricare i dati usando le istruzioni SQL **CREATE TABLE** e **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="e717b-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="e717b-139">Il codice usa la classe NpgsqlCommand con il metodo [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) per stabilire una connessione a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="e717b-140">Il codice usa quindi il metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="e717b-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="e717b-141">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="e717b-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
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

## <a name="read-data"></a><span data-ttu-id="e717b-142">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="e717b-142">Read data</span></span>
<span data-ttu-id="e717b-143">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="e717b-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="e717b-144">Il codice usa la classe NpgsqlCommand con il metodo [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) per stabilire una connessione a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="e717b-145">Il codice usa quindi il metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) e il metodo [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="e717b-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="e717b-146">Il codice usa poi [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) per passare ai record nei risultati.</span><span class="sxs-lookup"><span data-stu-id="e717b-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="e717b-147">Il codice usa quindi [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) e [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) per analizzare i valori nel record.</span><span class="sxs-lookup"><span data-stu-id="e717b-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="e717b-148">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="e717b-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="update-data"></a><span data-ttu-id="e717b-149">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="e717b-149">Update data</span></span>
<span data-ttu-id="e717b-150">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="e717b-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="e717b-151">Il codice usa la classe NpgsqlCommand con il metodo [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) per stabilire una connessione a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="e717b-152">Il codice usa quindi il metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="e717b-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="e717b-153">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="e717b-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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


## <a name="delete-data"></a><span data-ttu-id="e717b-154">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="e717b-154">Delete data</span></span>
<span data-ttu-id="e717b-155">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="e717b-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="e717b-156">Il codice usa la classe NpgsqlCommand con il metodo [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) per stabilire una connessione a PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="e717b-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="e717b-157">Il codice usa quindi il metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText e chiama il metodo [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) per eseguire i comandi di database.</span><span class="sxs-lookup"><span data-stu-id="e717b-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="e717b-158">Sostituire i parametri Host, DBName, User e Password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="e717b-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

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

## <a name="next-steps"></a><span data-ttu-id="e717b-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e717b-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="e717b-160">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="e717b-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
