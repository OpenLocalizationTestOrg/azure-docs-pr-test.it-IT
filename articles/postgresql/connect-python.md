---
title: La connessione tooAzure Database PostgreSQL da Python | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice Python, che è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
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
ms.openlocfilehash: 7d6d9f5424fb39ad8837999d4788b4363c818887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="2c332-103">Il Database di Azure per PostgreSQL: dati di utilizzo Python tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="2c332-103">Azure Database for PostgreSQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="2c332-104">Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2c332-105">Viene inoltre illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello da macOS Ubuntu Linux e le piattaforme Windows.</span><span class="sxs-lookup"><span data-stu-id="2c332-105">It also demonstrates how toouse SQL statements tooquery, insert, update, and delete data in hello database from macOS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="2c332-106">passaggi di Hello in questo articolo si presuppone che ha familiarità con lo sviluppo usando Python e tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c332-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2c332-107">Prerequisites</span></span>
<span data-ttu-id="2c332-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="2c332-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2c332-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="2c332-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="2c332-110">Creare un database: interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="2c332-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="2c332-111">Altri elementi necessari:</span><span class="sxs-lookup"><span data-stu-id="2c332-111">You also need:</span></span>
- <span data-ttu-id="2c332-112">[Python](https://www.python.org/downloads/) installato</span><span class="sxs-lookup"><span data-stu-id="2c332-112">[python](https://www.python.org/downloads/) installed</span></span>
- <span data-ttu-id="2c332-113">Pacchetto [pip](https://pip.pypa.io/en/stable/installing/) installato. È già installato se si usano i file binari Python 2 (>=2.7.9) o Python 3 (>=3.4) scaricati da [python.org](https://python.org).</span><span class="sxs-lookup"><span data-stu-id="2c332-113">[pip](https://pip.pypa.io/en/stable/installing/) package installed (pip is already installed if you're working with Python 2 >=2.7.9 or Python 3 >=3.4 binaries downloaded from [python.org](https://python.org).</span></span>

## <a name="install-hello-python-connection-libraries-for-postgresql"></a><span data-ttu-id="2c332-114">Installare le librerie di connessione di hello Python per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2c332-114">Install hello Python connection libraries for PostgreSQL</span></span>
<span data-ttu-id="2c332-115">Installare hello [psycopg2](http://initd.org/psycopg/docs/install.html) pacchetto, in modo da database hello tooconnect e query.</span><span class="sxs-lookup"><span data-stu-id="2c332-115">Install hello [psycopg2](http://initd.org/psycopg/docs/install.html) package, which enables you tooconnect and query hello database.</span></span> <span data-ttu-id="2c332-116">è psycopg2 [disponibile in PyPI](https://pypi.python.org/pypi/psycopg2/) sotto forma di hello di [rotellina](http://pythonwheels.com/) pacchetti per le piattaforme più comuni di hello (Linux e OS x, Windows).</span><span class="sxs-lookup"><span data-stu-id="2c332-116">psycopg2 is [available on PyPI](https://pypi.python.org/pypi/psycopg2/) in hello form of [wheel](http://pythonwheels.com/) packages for hello most common platforms (Linux, OSX, Windows).</span></span> <span data-ttu-id="2c332-117">Utilizzare pip versione tooget hello binario del modulo hello incluse tutte le dipendenze di hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-117">Use pip install tooget hello binary version of hello module including all hello dependencies.</span></span>

1. <span data-ttu-id="2c332-118">Nel computer in uso avviare un'interfaccia della riga di comando:</span><span class="sxs-lookup"><span data-stu-id="2c332-118">On your own computer, launch a command-line interface:</span></span>
    - <span data-ttu-id="2c332-119">In Linux, avviare shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-119">On Linux, launch hello Bash shell.</span></span>
    - <span data-ttu-id="2c332-120">Sul macOS, avviare hello Terminal.</span><span class="sxs-lookup"><span data-stu-id="2c332-120">On macOS, launch hello Terminal.</span></span>
    - <span data-ttu-id="2c332-121">In Windows, avviare hello prompt dei comandi dal Menu Start hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-121">On Windows, launch hello Command Prompt from hello Start Menu.</span></span>
2. <span data-ttu-id="2c332-122">Verificare che si utilizza hello la versione più recente di pip eseguendo un comando, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2c332-122">Ensure that you are using hello most current version of pip by running a command such as:</span></span>
    ```cmd
    pip install -U pip
    ```

3. <span data-ttu-id="2c332-123">Eseguire hello pacchetto psycopg2 hello tooinstall di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2c332-123">Run hello following command tooinstall hello psycopg2 package:</span></span>
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a><span data-ttu-id="2c332-124">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="2c332-124">Get connection information</span></span>
<span data-ttu-id="2c332-125">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-125">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2c332-126">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="2c332-126">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2c332-127">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2c332-127">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2c332-128">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e cercare **mypgserver 20170401** (server hello appena creato).</span><span class="sxs-lookup"><span data-stu-id="2c332-128">From hello left-hand menu in Azure portal, click **All resources** and search for **mypgserver-20170401** (hello server you just created).</span></span>
3. <span data-ttu-id="2c332-129">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="2c332-129">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2c332-130">Server di selezionare hello **Panoramica** pagina e prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="2c332-130">Select hello server's **Overview** page, and then make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2c332-131">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-python/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="2c332-131">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-python/1-connection-string.png)</span></span>
5. <span data-ttu-id="2c332-132">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-132">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="how-toorun-python-code"></a><span data-ttu-id="2c332-133">Come toorun codice Python</span><span class="sxs-lookup"><span data-stu-id="2c332-133">How toorun Python code</span></span>
<span data-ttu-id="2c332-134">Questo argomento contiene in totale quattro esempi di codice, ognuno dei quali esegue una funzione specifica.</span><span class="sxs-lookup"><span data-stu-id="2c332-134">This topic contains a total of four code samples, each of which performs a specific function.</span></span> <span data-ttu-id="2c332-135">Hello istruzioni seguenti indicano come toocreate un file di testo, inserire un blocco di codice e quindi salvare il file hello in modo che è possibile eseguire in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2c332-135">hello following instructions indicate how toocreate a text file, insert a code block, and then save hello file so that you can run it later.</span></span> <span data-ttu-id="2c332-136">Impossibile verificare toocreate quattro file distinti, uno per ogni blocco di codice.</span><span class="sxs-lookup"><span data-stu-id="2c332-136">Be sure toocreate four separate files, one for each code block.</span></span>

- <span data-ttu-id="2c332-137">Usando l'editor di testo preferito, creare un nuovo file.</span><span class="sxs-lookup"><span data-stu-id="2c332-137">Using your favorite text editor, create a new file.</span></span>
- <span data-ttu-id="2c332-138">Copiare e incollare uno degli esempi di codice hello in sezioni che seguono in file di testo hello hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-138">Copy and paste one of hello code samples in hello following sections into hello text file.</span></span> <span data-ttu-id="2c332-139">Sostituire hello **host**, **dbname**, **utente**, e **password** parametri con valori di hello specificato al momento della creazione hello Server e database.</span><span class="sxs-lookup"><span data-stu-id="2c332-139">Replace hello **host**, **dbname**, **user**, and **password** parameters with hello values that you specified when you created hello server and database.</span></span>
- <span data-ttu-id="2c332-140">Salvare il file di hello con estensione. py hello (ad esempio postgres.py) nella cartella del progetto.</span><span class="sxs-lookup"><span data-stu-id="2c332-140">Save hello file with hello .py extension (for example postgres.py) into your project folder.</span></span> <span data-ttu-id="2c332-141">Se si esegue hello del sistema operativo Windows, è possibile che tooselect codifica UTF-8 quando si salva il file hello.</span><span class="sxs-lookup"><span data-stu-id="2c332-141">If you are running hello Windows OS, be sure tooselect UTF-8 encoding when saving hello file.</span></span> 
- <span data-ttu-id="2c332-142">Avviare shell di prompt dei comandi o Bash hello e quindi modificare ad esempio cartella di progetto tooyour directory hello, `cd postgres`.</span><span class="sxs-lookup"><span data-stu-id="2c332-142">Launch hello Command Prompt or Bash shell and then change hello directory tooyour project folder, for example `cd postgres`.</span></span>
-  <span data-ttu-id="2c332-143">codice hello toorun, hello tipo comando Python seguito dal nome di file hello, ad esempio `Python postgres.py`.</span><span class="sxs-lookup"><span data-stu-id="2c332-143">toorun hello code, type hello Python command followed by hello file name, for example `Python postgres.py`.</span></span>

> [!NOTE]
> <span data-ttu-id="2c332-144">A partire da Python versione 3, potrebbe essere visualizzato l'errore di hello `SyntaxError: Missing parentheses in call too'print'` durante l'esecuzione di hello blocchi di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="2c332-144">Starting in Python version 3, you may see hello error `SyntaxError: Missing parentheses in call too'print'` when running hello following code blocks.</span></span> <span data-ttu-id="2c332-145">In tal caso, sostituire ogni comando toohello chiamata `print "string"` con una chiamata di funzione utilizzano le parentesi, ad esempio `print("string")`.</span><span class="sxs-lookup"><span data-stu-id="2c332-145">If that happens, replace each call toohello command `print "string"` with a function call using parenthesis, such as `print("string")`.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="2c332-146">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="2c332-146">Connect, create table, and insert data</span></span>
<span data-ttu-id="2c332-147">Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funzione **inserire** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-147">Use hello following code tooconnect and load hello data using [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) function with **INSERT** SQL statement.</span></span> <span data-ttu-id="2c332-148">Hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-148">hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function is used tooexecute hello SQL query against PostgreSQL database.</span></span> <span data-ttu-id="2c332-149">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="2c332-149">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

<span data-ttu-id="2c332-150">Dopo aver hello codice viene eseguito correttamente, output di hello viene visualizzato come segue:</span><span class="sxs-lookup"><span data-stu-id="2c332-150">After hello code runs successfully, hello output appears as follows:</span></span>

![Output della riga di comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a><span data-ttu-id="2c332-152">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="2c332-152">Read data</span></span>
<span data-ttu-id="2c332-153">Esempio di codice seguente hello di utilizzare dati hello tooread inseriti utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-153">Use hello following code tooread hello data inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **SELECT** SQL statement.</span></span> <span data-ttu-id="2c332-154">Questa funzione accetta una query e restituisce un set di risultati che possono eseguire un'iterazione utilizzando hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span><span class="sxs-lookup"><span data-stu-id="2c332-154">This function accepts a query and returns a result set that can be iterated over with hello use of [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall).</span></span> <span data-ttu-id="2c332-155">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="2c332-155">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

## <a name="update-data"></a><span data-ttu-id="2c332-156">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="2c332-156">Update data</span></span>
<span data-ttu-id="2c332-157">Esempio di codice utilizzare hello seguente riga di inventario hello tooupdate precedentemente inserito utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **aggiornamento** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-157">Use hello following code tooupdate hello inventory row that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **UPDATE** SQL statement.</span></span> <span data-ttu-id="2c332-158">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="2c332-158">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

# Update a data row in hello table
cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
print "Updated 1 row of data"

# Cleanup
conn.commit()
cursor.close()
conn.close()
```

## <a name="delete-data"></a><span data-ttu-id="2c332-159">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="2c332-159">Delete data</span></span>
<span data-ttu-id="2c332-160">Esempio di codice seguente di hello utilizzare toodelete un articolo di magazzino è inserito in precedenza utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2c332-160">Use hello following code toodelete an inventory item that you previously inserted using [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) function with **DELETE** SQL statement.</span></span> <span data-ttu-id="2c332-161">Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="2c332-161">Replace hello host, dbname, user, and password parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import psycopg2

# Update connection string information obtained from hello portal
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

## <a name="next-steps"></a><span data-ttu-id="2c332-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2c332-162">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2c332-163">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="2c332-163">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
