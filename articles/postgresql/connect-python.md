---
title: Connettersi a Database di Azure per PostgreSQL da Python | Microsoft Docs
description: "Questa guida introduttiva fornisce un esempio di codice Python che può essere usato per connettersi ai dati ed eseguire query da Database di Azure per PostgreSQL."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 08/15/2017
ms.openlocfilehash: d682d94143fb9fd5e2c2a578c3cb0dcfa101462c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-python-to-connect-and-query-data"></a><span data-ttu-id="31e5f-103">Database di Azure per PostgreSQL: usare Python per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="31e5f-103">Azure Database for PostgreSQL: Use Python to connect and query data</span></span>
<span data-ttu-id="31e5f-104">Questa guida introduttiva illustra come usare [Python](https://python.org) per connettersi a un database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="31e5f-104">This quickstart demonstrates how to use [Python](https://python.org) to connect to an Azure Database for PostgreSQL.</span></span> <span data-ttu-id="31e5f-105">Descrive anche come usare istruzioni SQL per eseguire query e inserire, aggiornare ed eliminare dati nel database dalle piattaforme macOS, Ubuntu Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="31e5f-105">It also demonstrates how to use SQL statements to query, insert, update, and delete data in the database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="31e5f-106">Le procedure descritte in questo articolo presuppongono che si abbia familiarità con lo sviluppo con Python, ma non con Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="31e5f-106">The steps in this article assume that you are familiar with developing using Python and are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31e5f-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="31e5f-107">Prerequisites</span></span>
<span data-ttu-id="31e5f-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="31e5f-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="31e5f-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="31e5f-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="31e5f-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="31e5f-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="31e5f-111">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="31e5f-111">You also need:</span></span>
- <span data-ttu-id="31e5f-112">[Python](https://www.python.org/downloads/) installato</span><span class="sxs-lookup"><span data-stu-id="31e5f-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="31e5f-113">Pacchetto [pip](https://pip.pypa.io/en/stable/installing/) installato. È già installato se si usano i file binari Python 2 (>=2.7.9) o Python 3 (>=3.4) scaricati da [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="31e5f-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-the-python-connection-libraries-for-postgresql"></a><span data-ttu-id="31e5f-114">Installare le raccolte di connessioni Python per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="31e5f-114">Install the Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="31e5f-115">Installare il pacchetto [psycopg2](http://initd.org/psycopg/docs/install.html), che consente di connettersi ed eseguire query sul database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-115">Install the [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you to connect and query the database.</span></span> <span data-ttu-id="31e5f-116">psycopg2 è [disponibile in PyPI](https://pypi.python.org/pypi/psycopg2/) sotto forma di pacchetti [wheel](http://pythonwheels.com/) per le piattaforme più comuni (Linux, OSX e Windows).</span><span class="sxs-lookup"><span data-stu-id="31e5f-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in the form of [wheel](http://pythonwheels.com/) packages for the most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="31e5f-117">Usare pip install per ottenere la versione binaria del modulo con tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="31e5f-117">Use pip install to get the binary version of the module including all the dependencies.</span></span>

1. <span data-ttu-id="31e5f-118">Nel computer in uso avviare un'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="31e5f-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="31e5f-119">In Linux avviare la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="31e5f-119">On Linux, launch the Bash shell.</span></span>
    - <span data-ttu-id="31e5f-120">In macOS avviare il terminale.</span><span class="sxs-lookup"><span data-stu-id="31e5f-120">On macOS, launch the Terminal.</span></span>
    - <span data-ttu-id="31e5f-121">In Windows avviare il prompt dei comandi dal menu Start.</span><span class="sxs-lookup"><span data-stu-id="31e5f-121">On Windows, launch the Command Prompt from the Start Menu.</span></span>
2. <span data-ttu-id="31e5f-122">Assicurarsi di usare la versione più aggiornata di pip eseguendo un comando come questo:</span><span class="sxs-lookup"><span data-stu-id="31e5f-122">Ensure that you are using the most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="31e5f-123">Eseguire questo comando per installare il pacchetto psycopg2:</span><span class="sxs-lookup"><span data-stu-id="31e5f-123">Run the following command to install the psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="31e5f-124">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="31e5f-124">Get connection information</span></span>
<span data-ttu-id="31e5f-125">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="31e5f-125">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="31e5f-126">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="31e5f-126">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="31e5f-127">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="31e5f-127">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="31e5f-128">Scegliere **Tutte le risorse** dal menu a sinistra nel portale di Azure e cercare **mypgserver-20170401**, ossia il server appena creato.</span><span class="sxs-lookup"><span data-stu-id="31e5f-128">From the left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (the server you just created).</span></span>
3. <span data-ttu-id="31e5f-129">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-129">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="31e5f-130">Selezionare la pagina **Panoramica** del server e prendere nota dei valori riportati in **Nome server** e **Nome di accesso dell'amministratore server**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-130">Select the server's **Overview** page, and then make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="31e5f-131">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="31e5f-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="31e5f-132">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server e, se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="31e5f-132">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="how-to-run-python-code"></a><span data-ttu-id="31e5f-133">Come eseguire codice Python</span><span class="sxs-lookup"><span data-stu-id="31e5f-133">How to run Python code</span></span>
<span data-ttu-id="31e5f-134">Questo argomento contiene in totale quattro esempi di codice, ognuno dei quali esegue una funzione specifica.</span><span class="sxs-lookup"><span data-stu-id="31e5f-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="31e5f-135">Le istruzioni seguenti indicano come creare un file di testo, inserire un blocco di codice e quindi salvare il file per poterlo eseguire in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="31e5f-135">The following instructions indicate how to create a text file, insert a code block, and then save the file so that you can run it later.</span></span> <span data-ttu-id="31e5f-136">Assicurarsi di creare quattro file separati, uno per ogni blocco di codice.</span><span class="sxs-lookup"><span data-stu-id="31e5f-136">Be sure to create four separate files, one for each code block.</span></span>

- <span data-ttu-id="31e5f-137">Usando l'editor di testo preferito, creare un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="31e5f-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="31e5f-138">Copiare e incollare uno degli esempi di codice delle sezioni seguenti nel file di testo.</span><span class="sxs-lookup"><span data-stu-id="31e5f-138">Copy and paste one of the code samples in the following sections into the text file.</span></span> <span data-ttu-id="31e5f-139">Sostituire i parametri **host**, **dbname**, **user** e **password** con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-139">Replace the **host**, **dbname**, **user**, and **password** parameters with the values that you specified when you created the server and database.</span></span>
- <span data-ttu-id="31e5f-140">Salvare il file con l'estensione py (ad esempio, postgres.py) nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="31e5f-140">Save the file with the .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="31e5f-141">Se si esegue il sistema operativo Windows, quando si salva il file assicurarsi di selezionare la codifica UTF-8.</span><span class="sxs-lookup"><span data-stu-id="31e5f-141">If you are running the Windows OS, be sure to select UTF-8 encoding when saving the file.</span></span> 
- <span data-ttu-id="31e5f-142">Avviare il prompt dei comandi o la shell Bash e quindi passare alla cartella del progetto, ad esempio: `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="31e5f-142">Launch the Command Prompt or Bash shell and then change the directory to your project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="31e5f-143">Per eseguire il codice, digitare il comando Python seguito dal nome del file, ad esempio `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="31e5f-143">To run the code, type the Python command followed by the file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="31e5f-144">A partire da Python versione 3, quando si eseguono i blocchi di codice seguenti potrebbe essere visualizzato l'errore `SyntaxError: Missing parentheses in call to 'print'`.</span><span class="sxs-lookup"><span data-stu-id="31e5f-144">Starting in Python version 3, you may see the error `SyntaxError: Missing parentheses in call to 'print'` when running the following code blocks.</span></span> <span data-ttu-id="31e5f-145">In tal caso, sostituire ogni chiamata al comando `print "string"` con una chiamata di funzione con parentesi, ad esempio `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="31e5f-145">If that happens, replace each call to the command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="31e5f-146">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="31e5f-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="31e5f-147">Usare il codice seguente per connettersi e caricare i dati usando la funzione [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) con un'istruzione SQL **INSERT**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-147">Use the following code to connect and load the data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="31e5f-148">La funzione [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) viene usata per eseguire la query SQL sul database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="31e5f-148">The [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used to execute the SQL query against PostgreSQL database.</span></span> <span data-ttu-id="31e5f-149">Sostituire i parametri host, dbname, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-149">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Drop previous table of same name if one exists
cursor.execute("DROP TABLE IF EXISTS inventory;")
print "Finished dropping table (if existed)"

# Create table
cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
print "Finished creating table"

# Insert some data into table
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
print "Inserted 3 rows of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

<span data-ttu-id="31e5f-150">Al termine dell'esecuzione del codice, viene visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="31e5f-150">After the code runs successfully, the output appears as follows:</span></span>

![Output della riga di comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="31e5f-152">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="31e5f-152">Read data</span></span>
<span data-ttu-id="31e5f-153">Usare il codice seguente per leggere i dati inseriti usando la funzione [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-153">Use the following code to read the data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="31e5f-154">Questa funzione accetta una query e restituisce un set di risultati su cui è possibile eseguire l'iterazione tramite [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="31e5f-154">This function accepts a query and returns a result set that can be iterated over with the use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="31e5f-155">Sostituire i parametri host, dbname, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-155">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Fetch all rows from table
cursor.execute("SELECT * FROM inventory;")
rows = cursor.fetchall()

# Print all rows
for row in rows:
    print "Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2]))

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="update-data"></a><span data-ttu-id="31e5f-156">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="31e5f-156">Update data</span></span>
<span data-ttu-id="31e5f-157">Usare il codice seguente per aggiornare la riga d'inventario inserita in precedenza tramite la funzione [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con l'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-157">Use the following code to update the inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="31e5f-158">Sostituire i parametri host, dbname, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-158">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Update a data row in the table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="31e5f-159">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="31e5f-159">Delete data</span></span>
<span data-ttu-id="31e5f-160">Usare il codice seguente per eliminare un articolo di magazzino inserito in precedenza tramite la funzione [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) con l'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="31e5f-160">Use the following code to delete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="31e5f-161">Sostituire i parametri host, dbname, user e password con i valori specificati al momento della creazione del server e del database.</span><span class="sxs-lookup"><span data-stu-id="31e5f-161">Replace the host, dbname, user, and password parameters with the values that you specified when you created the server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from the portal
host = "mypgserver-20170401.postgres.database.azure.com"
user = "mylogin@mypgserver-20170401"
dbname = "mypgsqldb"
password = "<server_admin_password>"
sslmode = "require"

# Construct connection string
conn_string = "host={0} user={1} dbname={2} password={3} sslmode={4}".format(host, user, dbname, password, sslmode)
conn = psycopg2.connect(conn_string) 
print "Connection established"

cursor = conn.cursor()

# Delete data row from table
cursor.execute("DELETE FROM inventory WHERE name = %s;", ("orange",))
print "Deleted 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="31e5f-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="31e5f-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="31e5f-163">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="31e5f-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
