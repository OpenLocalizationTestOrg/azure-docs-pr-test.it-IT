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
# <a name="azure-database-for-mysql-use-python-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati di utilizzo Python tooconnect e query
Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Database di Azure per MySQL. Usa tooquery istruzioni SQL, insert, update e delete dati nel database di hello da piattaforme del sistema operativo Mac, Ubuntu Linux e Windows. passaggi di Hello in questo articolo si presuppone che ha familiarità con lo sviluppo usando Python e tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-python-and-hello-mysql-connector"></a>Installare Python e hello connettore MySQL
Installare [Python](https://www.python.org/downloads/) hello e [connettore MySQL per Python](https://dev.mysql.com/downloads/connector/python/) sul proprio computer. A seconda della piattaforma, attenersi alla seguente procedura hello:

### <a name="windows"></a>Windows
1. Scaricare e installare Python 2.7 da [python.org](https://www.python.org/downloads/windows/). 
2. Verificare l'installazione di Python hello avviando hello il prompt dei comandi. Eseguire il comando hello `C:\python27\python.exe -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.
3. Installare il connettore di Python hello per MySQL [mysql.com](https://dev.mysql.com/downloads/connector/python/) versione di Python tooyour corrispondente.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. In Linux (Ubuntu), Python viene in genere installato come parte dell'installazione predefinita di hello.
2. Verificare l'installazione di Python hello avviando shell bash hello. Eseguire il comando hello `python -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.
3. Il controllo installazione PIP hello eseguendo hello `pip show pip -V` comando toosee numero di versione di hello. 
4. PIP può essere incluso in alcune versioni di Python. Se non è installato PIP, è possibile installare hello [PIP] (https://pip.pypa.io/en/stable/installing/), pacchetto eseguendo comando `sudo apt-get install python-pip`.
5. Aggiornamento PIP toohello versione più recente, eseguendo hello `pip install -U pip` comando.
6. Installare il connettore di MySQL hello per Python e le relative dipendenze utilizzando il comando PIP hello:

   ```bash
   sudo pip install mysql-connector-python-rf
   ```
 
### <a name="macos"></a>MacOS
1. In Mac OS, Python viene in genere installato come parte dell'installazione del sistema operativo predefinita di hello.
2. Verificare l'installazione di Python hello avviando shell bash hello. Eseguire il comando hello `python -V` con numero di versione toosee di commutatore di hello maiuscolo V hello.
3. Il controllo installazione PIP hello eseguendo hello `pip show pip -V` comando toosee numero di versione di hello.
4. PIP può essere incluso in alcune versioni di Python. Se non è installato PIP, è possibile installare hello [PIP](https://pip.pypa.io/en/stable/installing/) pacchetto.
5. Aggiornamento PIP toohello versione più recente, eseguendo hello `pip install -U pip` comando.
6. Installare il connettore di MySQL hello per Python e le relative dipendenze utilizzando il comando PIP hello:

   ```bash
   pip install mysql-connector-python-rf
   ```

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello avere piegato, ad esempio **myserver4demo**.
3. Fare clic sul nome di server hello **myserver4demo**.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-python/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.
   

## <a name="run-python-code"></a>Eseguire il codice Python
- Incollare il codice hello in un file di testo e salvare il file hello in una cartella di progetto con py estensione di file, ad esempio C:\pythonmysql\createtable.py o /home/username/pythonmysql/createtable.py
- codice hello toorun, avviare prompt dei comandi di hello o della shell bash. Passare alla cartella del progetto `cd pythonmysql`. Quindi digitare il comando di python hello seguito dal nome di file hello `python createtable.py` toorun un'applicazione hello. Nel sistema operativo Windows hello, se python.exe non viene trovato, si potrebbe fornire hello toohello di percorso completo dell'eseguibile oppure aggiungere il percorso di Python hello nella variabile di ambiente path hello. `C:\python27\python.exe createtable.py`

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect toohello server, creare una tabella e caricare i dati di hello usando un **inserire** istruzione SQL. 

Nel codice hello libreria mysql.connector hello viene importata. Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello. codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue query SQL hello database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

Nel codice hello libreria mysql.connector hello viene importata. Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello. codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue l'istruzione SQL hello database MySQL. le righe di dati Hello vengono letti utilizzando hello [fetchall()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-fetchall.html) metodo. Hello set di risultati viene mantenuto in una riga di raccolta e una per iteratore è tooloop utilizzato su righe hello.

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL. 

Nel codice hello libreria mysql.connector hello viene importata.  Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello. codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue l'istruzione SQL hello database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e rimuovere dati tramite un **eliminare** istruzione SQL. 

Nel codice hello libreria mysql.connector hello viene importata.  Hello [Connect ()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysql-connector-connect.html) funzione è tooAzure tooconnect utilizzati Database di MySQL mediante hello [gli argomenti di connessione](https://dev.mysql.com/doc/connector-python/en/connector-python-connectargs.html) nella raccolta delle configurazioni hello. codice Hello utilizza un cursore su connessione hello e [cursor.execute()](https://dev.mysql.com/doc/connector-python/en/connector-python-api-mysqlcursor-execute.html) metodo esegue query SQL hello database MySQL. 

Sostituire hello `host`, `user`, `password`, e `database` parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./concepts-migrate-import-export.md)
