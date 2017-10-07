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
# <a name="azure-database-for-postgresql-use-python-tooconnect-and-query-data"></a>Il Database di Azure per PostgreSQL: dati di utilizzo Python tooconnect e query
Questa Guida introduttiva illustra come toouse [Python](https://python.org) tooconnect tooan Database di Azure per PostgreSQL. Viene inoltre illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello da macOS Ubuntu Linux e le piattaforme Windows. passaggi di Hello in questo articolo si presuppone che ha familiarità con lo sviluppo usando Python e tooworking nuovo con il Database di Azure per PostgreSQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Creare un database: portale](quickstart-create-server-database-portal.md)
- [Creare un database: interfaccia della riga di comando](quickstart-create-server-database-azure-cli.md)

Altri elementi necessari:
- [Python](https://www.python.org/downloads/) installato
- Pacchetto [pip](https://pip.pypa.io/en/stable/installing/) installato. È già installato se si usano i file binari Python 2 (>=2.7.9) o Python 3 (>=3.4) scaricati da [python.org](https://python.org).

## <a name="install-hello-python-connection-libraries-for-postgresql"></a>Installare le librerie di connessione di hello Python per PostgreSQL
Installare hello [psycopg2](http://initd.org/psycopg/docs/install.html) pacchetto, in modo da database hello tooconnect e query. è psycopg2 [disponibile in PyPI](https://pypi.python.org/pypi/psycopg2/) sotto forma di hello di [rotellina](http://pythonwheels.com/) pacchetti per le piattaforme più comuni di hello (Linux e OS x, Windows). Utilizzare pip versione tooget hello binario del modulo hello incluse tutte le dipendenze di hello.

1. Nel computer in uso avviare un'interfaccia della riga di comando:
    - In Linux, avviare shell Bash hello.
    - Sul macOS, avviare hello Terminal.
    - In Windows, avviare hello prompt dei comandi dal Menu Start hello.
2. Verificare che si utilizza hello la versione più recente di pip eseguendo un comando, ad esempio:
    ```cmd
    pip install -U pip
    ```

3. Eseguire hello pacchetto psycopg2 hello tooinstall di comando seguente:
    ```cmd
    pip install psycopg2
    ```

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e cercare **mypgserver 20170401** (server hello appena creato).
3. Fare clic sul nome di server hello **mypgserver 20170401**.
4. Server di selezionare hello **Panoramica** pagina e prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-python/1-connection-string.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="how-toorun-python-code"></a>Come toorun codice Python
Questo argomento contiene in totale quattro esempi di codice, ognuno dei quali esegue una funzione specifica. Hello istruzioni seguenti indicano come toocreate un file di testo, inserire un blocco di codice e quindi salvare il file hello in modo che è possibile eseguire in un secondo momento. Impossibile verificare toocreate quattro file distinti, uno per ogni blocco di codice.

- Usando l'editor di testo preferito, creare un nuovo file.
- Copiare e incollare uno degli esempi di codice hello in sezioni che seguono in file di testo hello hello. Sostituire hello **host**, **dbname**, **utente**, e **password** parametri con valori di hello specificato al momento della creazione hello Server e database.
- Salvare il file di hello con estensione. py hello (ad esempio postgres.py) nella cartella del progetto. Se si esegue hello del sistema operativo Windows, è possibile che tooselect codifica UTF-8 quando si salva il file hello. 
- Avviare shell di prompt dei comandi o Bash hello e quindi modificare ad esempio cartella di progetto tooyour directory hello, `cd postgres`.
-  codice hello toorun, hello tipo comando Python seguito dal nome di file hello, ad esempio `Python postgres.py`.

> [!NOTE]
> A partire da Python versione 3, potrebbe essere visualizzato l'errore di hello `SyntaxError: Missing parentheses in call too'print'` durante l'esecuzione di hello blocchi di codice seguente. In tal caso, sostituire ogni comando toohello chiamata `print "string"` con una chiamata di funzione utilizzano le parentesi, ad esempio `print("string")`.

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect e caricare i dati di hello usando [psycopg2.connect](http://initd.org/psycopg/docs/connection.html) funzione **inserire** istruzione SQL. Hello [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione è tooexecute utilizzati nella query SQL hello database PostgreSQL. Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.

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

Dopo aver hello codice viene eseguito correttamente, output di hello viene visualizzato come segue:

![Output della riga di comando](media/connect-python/2-example-python-output.png)

## <a name="read-data"></a>Leggere i dati
Esempio di codice seguente hello di utilizzare dati hello tooread inseriti utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **selezionare** istruzione SQL. Questa funzione accetta una query e restituisce un set di risultati che possono eseguire un'iterazione utilizzando hello [cursor.fetchall()](http://initd.org/psycopg/docs/cursor.html#cursor.fetchall). Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="update-data"></a>Aggiornare i dati
Esempio di codice utilizzare hello seguente riga di inventario hello tooupdate precedentemente inserito utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **aggiornamento** istruzione SQL. Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="delete-data"></a>Eliminare i dati
Esempio di codice seguente di hello utilizzare toodelete un articolo di magazzino è inserito in precedenza utilizzando [cursor.execute](http://initd.org/psycopg/docs/cursor.html#execute) funzione **eliminare** istruzione SQL. Sostituire l'host hello, dbname, utente e password parametri con valori di hello specificato al momento della creazione hello server e database.

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

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
