---
title: La connessione tooAzure Database MySQL Python | Documenti Microsoft
description: "Questa Guida rapida fornisce che esempi è possibile utilizzare tooconnect ed eseguire query sui dati dal Database di Azure per MySQL di codice Python diversi."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: python
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: 9df5211adcab886a502fd138347aed8fb587cd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a><span data-ttu-id="6a570-103">Il Database di Azure per MySQL: dati di utilizzo Python tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="6a570-103">Azure Database for MySQL: Use Python tooconnect and query data</span></span>
<span data-ttu-id="6a570-104">Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-104">This quickstart demonstrates how toouse [Python](https://python.org) tooconnect tooan Azure Database for MySQL.</span></span> <span data-ttu-id="6a570-105">Usa tooquery istruzioni SQL, insert, update e delete dati nel database di hello da piattaforme del sistema operativo Mac, Ubuntu Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="6a570-105">It uses SQL statements tooquery, insert, update, and delete data in hello database from Mac OS, Ubuntu Linux, and Windows platforms.</span></span> <span data-ttu-id="6a570-106">passaggi di Hello in questo articolo si presuppone che ha familiarità con lo sviluppo usando Python e tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-106">hello steps in this article assume that you are familiar with developing using Python and are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a570-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6a570-107">Prerequisites</span></span>
<span data-ttu-id="6a570-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="6a570-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="6a570-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="6a570-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- [<span data-ttu-id="6a570-110">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6a570-110">Create an Azure Database for MySQL server using Azure CLI</span></span>](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a><span data-ttu-id="6a570-111">Installare Python e hello connettore MySQL</span><span class="sxs-lookup"><span data-stu-id="6a570-111">Install Python and hello MySQL connector</span></span>
<span data-ttu-id="6a570-112">Installare [Python](https://www.python.org/downloads/) hello e [connettore MySQL per Python](https://dev.mysql.com/downloads/connector/python/) sul proprio computer.</span><span class="sxs-lookup"><span data-stu-id="6a570-112">Install [Python](https://www.python.org/downloads/) and hello [MySQL connector for Python](https://dev.mysql.com/downloads/connector/python/) on your own machine.</span></span> <span data-ttu-id="6a570-113">A seconda della piattaforma, attenersi alla seguente procedura hello:</span><span class="sxs-lookup"><span data-stu-id="6a570-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="6a570-114">Windows</span><span class="sxs-lookup"><span data-stu-id="6a570-114">Windows</span></span>
1. <span data-ttu-id="6a570-115">Scaricare e installare Python 2.7 da [python.org](https://www.python.org/downloads/windows/).</span><span class="sxs-lookup"><span data-stu-id="6a570-115">Download and Install Python 2.7 from [python.org](https://www.python.org/downloads/windows/).</span></span> 
2. <span data-ttu-id="6a570-116">Verificare l'installazione di Python hello avviando hello il prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="6a570-116">Check hello Python installation by launching hello command prompt.</span></span> <span data-ttu-id="6a570-117">Eseguire il comando hello `C:\python27\python.exe -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-117">Run hello command `C:\python27\python.exe -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="6a570-118">Installare il connettore di Python hello per MySQL [mysql.com](https://dev.mysql.com/downloads/connector/python/) versione di Python tooyour corrispondente.</span><span class="sxs-lookup"><span data-stu-id="6a570-118">Install hello Python connector for MySQL from [mysql.com](https://dev.mysql.com/downloads/connector/python/) corresponding tooyour version of Python.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="6a570-119">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="6a570-119">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="6a570-120">In Linux (Ubuntu), Python viene in genere installato come parte dell'installazione predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-120">In Linux (Ubuntu), Python is typically installed as part of hello default installation.</span></span>
2. <span data-ttu-id="6a570-121">Verificare l'installazione di Python hello avviando shell bash hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-121">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="6a570-122">Eseguire il comando hello `python -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-122">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="6a570-123">Il controllo installazione PIP hello eseguendo hello `pip show pip -V` comando toosee numero di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-123">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span> 
4. <span data-ttu-id="6a570-124">PIP può essere incluso in alcune versioni di Python.</span><span class="sxs-lookup"><span data-stu-id="6a570-124">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="6a570-125">Se non è installato PIP, è possibile installare hello [PIP] (https://pip.pypa.io/en/stable/installing/), pacchetto eseguendo comando `sudo apt-get install python-pip`.</span><span class="sxs-lookup"><span data-stu-id="6a570-125">If PIP is not installed, you may install hello [PIP] (https://pip.pypa.io/en/stable/installing/) package, by running command `sudo apt-get install python-pip`.</span></span>
5. <span data-ttu-id="6a570-126">Aggiornamento PIP toohello versione più recente, eseguendo hello `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="6a570-126">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="6a570-127">Installare il connettore di MySQL hello per Python e le relative dipendenze utilizzando il comando PIP hello:</span><span class="sxs-lookup"><span data-stu-id="6a570-127">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a><span data-ttu-id="6a570-128">MacOS</span><span class="sxs-lookup"><span data-stu-id="6a570-128">MacOS</span></span>
1. <span data-ttu-id="6a570-129">In Mac OS, Python viene in genere installato come parte dell'installazione del sistema operativo predefinita di hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-129">In Mac OS, Python is typically installed as part of hello default OS installation.</span></span>
2. <span data-ttu-id="6a570-130">Verificare l'installazione di Python hello avviando shell bash hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-130">Check hello Python installation by launching hello bash shell.</span></span> <span data-ttu-id="6a570-131">Eseguire il comando hello `python -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-131">Run hello command `python -V` using hello uppercase V switch toosee hello version number.</span></span>
3. <span data-ttu-id="6a570-132">Il controllo installazione PIP hello eseguendo hello `pip show pip -V` comando toosee numero di versione di hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-132">Check hello PIP installation by running hello `pip show pip -V` command toosee hello version number.</span></span>
4. <span data-ttu-id="6a570-133">PIP può essere incluso in alcune versioni di Python.</span><span class="sxs-lookup"><span data-stu-id="6a570-133">PIP may be included in some versions of Python.</span></span> <span data-ttu-id="6a570-134">Se non è installato PIP, è possibile installare hello [PIP](https://pip.pypa.io/en/stable/installing/) pacchetto.</span><span class="sxs-lookup"><span data-stu-id="6a570-134">If PIP is not installed, you may install hello [PIP](https://pip.pypa.io/en/stable/installing/) package.</span></span>
5. <span data-ttu-id="6a570-135">Aggiornamento PIP toohello versione più recente, eseguendo hello `pip install -U pip` comando.</span><span class="sxs-lookup"><span data-stu-id="6a570-135">Update PIP toohello latest version, by running hello `pip install -U pip` command.</span></span>
6. <span data-ttu-id="6a570-136">Installare il connettore di MySQL hello per Python e le relative dipendenze utilizzando il comando PIP hello:</span><span class="sxs-lookup"><span data-stu-id="6a570-136">Install hello MySQL connector for Python, and its dependencies by using hello PIP command:</span></span>

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a><span data-ttu-id="6a570-137">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="6a570-137">Get connection information</span></span>
<span data-ttu-id="6a570-138">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-138">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="6a570-139">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="6a570-139">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="6a570-140">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6a570-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6a570-141">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello avere piegato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="6a570-141">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="6a570-142">Fare clic sul nome di server hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="6a570-142">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="6a570-143">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="6a570-143">Select hello server's **Properties** page.</span></span> <span data-ttu-id="6a570-144">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="6a570-144">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="6a570-145">![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-python/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="6a570-145">![Azure Database for MySQL - Server Admin Login](./media/connect-python/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="6a570-146">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-146">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>
   

## <a name="run-python-code"></a><span data-ttu-id="6a570-147">Eseguire il codice Python</span><span class="sxs-lookup"><span data-stu-id="6a570-147">Run Python Code</span></span>
- <span data-ttu-id="6a570-148">Incollare il codice hello in un file di testo e salvare il file hello in una cartella di progetto con py estensione di file, ad esempio C:\pythonmysql\createtable.py o /home/username/pythonmysql/createtable.py</span><span class="sxs-lookup"><span data-stu-id="6a570-148">Paste hello code into a text file, and save hello file into a project folder with file extension .py, such as C:\pythonmysql\createtable.py or /home/username/pythonmysql/createtable.py</span></span>
- <span data-ttu-id="6a570-149">codice hello toorun, avviare prompt dei comandi di hello o della shell bash.</span><span class="sxs-lookup"><span data-stu-id="6a570-149">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="6a570-150">Passare alla cartella del progetto `cd pythonmysql`.</span><span class="sxs-lookup"><span data-stu-id="6a570-150">Change directory into your project folder `cd pythonmysql`.</span></span> <span data-ttu-id="6a570-151">Quindi digitare il comando di python hello seguito dal nome di file hello `python createtable.py` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-151">Then type hello python command followed by hello file name `python createtable.py` toorun hello application.</span></span> <span data-ttu-id="6a570-152">Nel sistema operativo Windows hello, se python.exe non viene trovato, si potrebbe fornire hello toohello di percorso completo dell'eseguibile oppure aggiungere il percorso di Python hello nella variabile di ambiente path hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-152">On hello Windows OS, if python.exe is not found, you may provide hello full path toohello executable, or add hello Python path into hello path environment variable.</span></span> `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="6a570-153">Connettersi, creare tabelle e inserire dati</span><span class="sxs-lookup"><span data-stu-id="6a570-153">Connect, create table, and insert data</span></span>
<span data-ttu-id="6a570-154">Seguente hello utilizzare codice tooconnect toohello server, creare una tabella e caricare i dati di hello usando un **inserire** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-154">Use hello following code tooconnect toohello server, create a table, and load hello data using an **INSERT** SQL statement.</span></span> 

<span data-ttu-id="6a570-155">Nel codice hello libreria mysql.connector hello viene importata.</span><span class="sxs-lookup"><span data-stu-id="6a570-155">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="6a570-156">Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-156">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="6a570-157">codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue query SQL hello database MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-157">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="6a570-158">Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="6a570-158">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Drop previous table of same name if one exists
  cursor.execute("DROP TABLE IF EXISTS inventory;")
  print("Finished dropping table (if existed).")

  # Create table
  cursor.execute("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
  print("Finished creating table.")

  # Insert some data into table
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("banana", 150))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("orange", 154))
  print("Inserted",cursor.rowcount,"row(s) of data.")
  cursor.execute("INSERT INTO inventory (name, quantity) VALUES (%s, %s);", ("apple", 100))
  print("Inserted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="read-data"></a><span data-ttu-id="6a570-159">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="6a570-159">Read data</span></span>
<span data-ttu-id="6a570-160">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-160">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="6a570-161">Nel codice hello libreria mysql.connector hello viene importata.</span><span class="sxs-lookup"><span data-stu-id="6a570-161">In hello code, hello mysql.connector library is imported.</span></span> <span data-ttu-id="6a570-162">Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-162">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="6a570-163">codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue l'istruzione SQL hello database MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-163">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> <span data-ttu-id="6a570-164">le righe di dati Hello vengono letti utilizzando hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) metodo.</span><span class="sxs-lookup"><span data-stu-id="6a570-164">hello data rows are read using hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) method.</span></span> <span data-ttu-id="6a570-165">Hello set di risultati viene mantenuto in una riga di raccolta e una per iteratore è tooloop utilizzato su righe hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-165">hello result set is kept in a collection row and a for iterator is used tooloop over hello rows.</span></span>

<span data-ttu-id="6a570-166">Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="6a570-166">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Read data
  cursor.execute("SELECT * FROM inventory;")
  rows = cursor.fetchall()
  print("Read",cursor.rowcount,"row(s) of data.")

  # Print all rows
  for row in rows:
    print("Data row = (%s, %s, %s)" %(str(row[0]), str(row[1]), str(row[2])))

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="update-data"></a><span data-ttu-id="6a570-167">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="6a570-167">Update data</span></span>
<span data-ttu-id="6a570-168">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-168">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span> 

<span data-ttu-id="6a570-169">Nel codice hello libreria mysql.connector hello viene importata.</span><span class="sxs-lookup"><span data-stu-id="6a570-169">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="6a570-170">Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-170">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="6a570-171">codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue l'istruzione SQL hello database MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-171">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL statement against MySQL database.</span></span> 

<span data-ttu-id="6a570-172">Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="6a570-172">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Update a data row in hello table
  cursor.execute("UPDATE inventory SET quantity = %s WHERE name = %s;", (200, "banana"))
  print("Updated",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="delete-data"></a><span data-ttu-id="6a570-173">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="6a570-173">Delete data</span></span>
<span data-ttu-id="6a570-174">Seguente hello utilizzare codice tooconnect e rimuovere dati tramite un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-174">Use hello following code tooconnect and remove data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="6a570-175">Nel codice hello libreria mysql.connector hello viene importata.</span><span class="sxs-lookup"><span data-stu-id="6a570-175">In hello code, hello mysql.connector library is imported.</span></span>  <span data-ttu-id="6a570-176">Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello.</span><span class="sxs-lookup"><span data-stu-id="6a570-176">hello [connect()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) function is used tooconnect tooAzure Database for MySQL using hello [connection arguments](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) in hello config collection.</span></span> <span data-ttu-id="6a570-177">codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue query SQL hello database MySQL.</span><span class="sxs-lookup"><span data-stu-id="6a570-177">hello code uses a cursor on hello connection, and [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) method executes hello SQL query against MySQL database.</span></span> 

<span data-ttu-id="6a570-178">Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.</span><span class="sxs-lookup"><span data-stu-id="6a570-178">Replace hello `host`, `user`, `password`, and `database` parameters with hello values that you specified when you created hello server and database.</span></span>

```Python
import mysql.connector
from mysql.connector import errorcode

# Obtain connection string information from hello portal
config = {
  'host':'myserver4demo.mysql.database.azure.com',
  'user':'myadmin@myserver4demo',
  'password':'yourpassword',
  'database':'quickstartdb'
}

# Construct connection string
try:
   conn = mysql.connector.connect(**config)
   print("Connection established.")
except mysql.connector.Error as err:
  if err.errno == errorcode.ER_ACCESS_DENIED_ERROR:
    print("Something is wrong with hello user name or password.")
  elif err.errno == errorcode.ER_BAD_DB_ERROR:
    print("Database does not exist.")
  else:
    print(err)
else:
  cursor = conn.cursor()

  # Delete a data row in hello table
  cursor.execute("DELETE FROM inventory WHERE name=%(param1)s;", {'param1':"orange"})
  print("Deleted",cursor.rowcount,"row(s) of data.")

  # Cleanup
  conn.commit()
  cursor.close()
  conn.close()
  print("Done.")
```

## <a name="next-steps"></a><span data-ttu-id="6a570-179">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6a570-179">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6a570-180">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="6a570-180">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
