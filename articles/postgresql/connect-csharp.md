---
title: La connessione tooAzure Database PostgreSQL da c# | Documenti Microsoft
description: "Questa Guida rapida viene fornito un esempio codice c# (.NET) è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
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
ms.openlocfilehash: 5ba7426f8ad263193cdb208b3531da0ceff181dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-net-c-tooconnect-and-query-data"></a><span data-ttu-id="d4355-103">Il Database di Azure per PostgreSQL: dati tooconnect e query di utilizzo di .NET (c#)</span><span class="sxs-lookup"><span data-stu-id="d4355-103">Azure Database for PostgreSQL: Use .NET (C#) tooconnect and query data</span></span>
<span data-ttu-id="d4355-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di un'applicazione c# PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="d4355-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="d4355-106">Hello passaggi in questo articolo si presuppone che si abbia familiarità con lo sviluppo in c#, e che siano tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-106">hello steps in this article assume that you are familiar with developing using C#, and that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4355-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d4355-107">Prerequisites</span></span>
<span data-ttu-id="d4355-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="d4355-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="d4355-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="d4355-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="d4355-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d4355-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="d4355-111">È anche necessario:</span><span class="sxs-lookup"><span data-stu-id="d4355-111">You also need to:</span></span>
- <span data-ttu-id="d4355-112">Installare [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="d4355-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="d4355-113">Seguire passaggi hello hello collegato articolo tooinstall .NET in modo specifico per la piattaforma (Windows, Ubuntu Linux o Mac OS).</span><span class="sxs-lookup"><span data-stu-id="d4355-113">Follow hello steps in hello linked article tooinstall .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="d4355-114">Installare [Visual Studio](https://www.visualstudio.com/downloads/) o codice tootype e modifica di codice di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d4355-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code tootype and edit code.</span></span>
- <span data-ttu-id="d4355-115">Installare la libreria [Npgsql](http://www.npgsql.org/doc/index.html) come descritto di seguito.</span><span class="sxs-lookup"><span data-stu-id="d4355-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="d4355-116">Installare i riferimenti Npgsql nella soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d4355-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="d4355-117">tooconnect da hello c# tooPostgreSQL applicazione, utilizzare libreria ADO.NET open source di hello chiamata Npgsql.</span><span class="sxs-lookup"><span data-stu-id="d4355-117">tooconnect from hello C# application tooPostgreSQL, use hello open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="d4355-118">NuGet consente di scaricare e gestire facilmente i riferimenti di hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-118">NuGet helps download and manage hello references easily.</span></span>

1. <span data-ttu-id="d4355-119">Creare una nuova soluzione C# o aprirne una esistente:</span><span class="sxs-lookup"><span data-stu-id="d4355-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="d4355-120">In Visual Studio creare una soluzione scegliendo **Nuovo** > **Progetto** dal menu File.</span><span class="sxs-lookup"><span data-stu-id="d4355-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="d4355-121">Nella finestra di dialogo Nuovo progetto hello, espandere **modelli** > **Visual c#**.</span><span class="sxs-lookup"><span data-stu-id="d4355-121">In hello New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="d4355-122">Scegliere un modello appropriato, ad esempio **Console App (.NET Core)** (App console - .NET Core).</span><span class="sxs-lookup"><span data-stu-id="d4355-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="d4355-123">Usare Gestione pacchetti Nuget tooinstall Npgsql hello:</span><span class="sxs-lookup"><span data-stu-id="d4355-123">Use hello Nuget Package Manager tooinstall Npgsql:</span></span>
   - <span data-ttu-id="d4355-124">Fare clic su hello **strumenti** menu > **Gestione pacchetti NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d4355-124">Click hello **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="d4355-125">In hello **Package Manager Console**, tipo`Install-Package Npgsql`</span><span class="sxs-lookup"><span data-stu-id="d4355-125">In hello **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="d4355-126">Hello installare comando download hello Npgsql.dll e gli assembly correlati e li aggiunge come dipendenze nelle soluzioni hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-126">hello install command downloads hello Npgsql.dll and related assemblies and adds them as dependencies in hello solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d4355-127">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="d4355-127">Get connection information</span></span>
<span data-ttu-id="d4355-128">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-128">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="d4355-129">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="d4355-129">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="d4355-130">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d4355-130">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="d4355-131">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d4355-131">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="d4355-132">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="d4355-132">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="d4355-133">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="d4355-133">Select hello server's **Overview** page.</span></span> <span data-ttu-id="d4355-134">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="d4355-134">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="d4355-135">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="d4355-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="d4355-136">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-136">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="d4355-137">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="d4355-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="d4355-138">Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando **CREATE TABLE** e **INSERT INTO** istruzioni SQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-138">Use hello following code tooconnect and load hello data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="d4355-139">codice Hello utilizza la classe NpgsqlCommand con metodo [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="d4355-139">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d4355-140">Quindi codice hello Usa metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-140">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span> 

<span data-ttu-id="d4355-141">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="d4355-141">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="d4355-142">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="d4355-142">Read data</span></span>
<span data-ttu-id="d4355-143">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-143">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="d4355-144">codice Hello utilizza la classe NpgsqlCommand con metodo [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="d4355-144">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d4355-145">Quindi codice hello Usa metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) e metodo [ExecuteReader](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-145">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) toorun hello database commands.</span></span> <span data-ttu-id="d4355-146">Successivamente hello viene utilizzato codice [Read](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello record nei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-146">Next hello code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) tooadvance toohello records in hello results.</span></span> <span data-ttu-id="d4355-147">Quindi utilizza codice hello [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) e [GetString ()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) valori hello tooparse nel record di hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-147">Then hello code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) tooparse hello values in hello record.</span></span>

<span data-ttu-id="d4355-148">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="d4355-148">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="d4355-149">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="d4355-149">Update data</span></span>
<span data-ttu-id="d4355-150">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-150">Use hello following code tooconnect and read hello data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="d4355-151">codice Hello utilizza la classe NpgsqlCommand con metodo [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="d4355-151">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d4355-152">Quindi codice hello Usa metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-152">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="d4355-153">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="d4355-153">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="d4355-154">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="d4355-154">Delete data</span></span>
<span data-ttu-id="d4355-155">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="d4355-155">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="d4355-156">codice Hello utilizza la classe NpgsqlCommand con metodo [Open ()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish tooPostgreSQL una connessione.</span><span class="sxs-lookup"><span data-stu-id="d4355-156">hello code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) tooestablish a connection tooPostgreSQL.</span></span> <span data-ttu-id="d4355-157">Quindi codice hello Usa metodo [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), imposta la proprietà CommandText hello e chiama metodo [ExecuteNonQuery](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun i comandi di database hello.</span><span class="sxs-lookup"><span data-stu-id="d4355-157">Then hello code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets hello CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) toorun hello database commands.</span></span>

<span data-ttu-id="d4355-158">Sostituire i parametri di Host, DBName, utente e Password hello con i valori hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="d4355-158">Replace hello Host, DBName, User, and Password parameters with hello values that you specified when you created hello server and database.</span></span> 

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
        // Obtain connection string information from hello portal
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

            Console.WriteLine("Press RETURN tooexit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="d4355-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4355-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="d4355-160">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="d4355-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
