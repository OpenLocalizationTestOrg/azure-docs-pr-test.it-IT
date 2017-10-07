---
title: La connessione tooAzure Database MySQL mediante Go | Documenti Microsoft
description: "Questa Guida introduttiva offre numerosi esempi di codice Go è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: go
ms.topic: hero-article
ms.date: 07/18/2017
ms.openlocfilehash: e8067b807ee729e04850c5325f476806bcd54983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-go-language-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: utilizzano il comando Go language tooconnect ed eseguire query sui dati
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL codice hello scritto in [passare](https://golang.org/) language da Windows, Ubuntu Linux e Apple piattaforme macOS. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Go, ma che sono tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure)

## <a name="install-go-and-mysql-connector"></a>Installare Go e il connettore MySQL
Installare [passare](https://golang.org/doc/install) hello e [driver di sql go per MySQL](https://github.com/go-sql-driver/mysql#installation) sul proprio computer. A seconda della piattaforma, attenersi alla seguente procedura hello:

### <a name="windows"></a>Windows
1. [Scaricare](https://golang.org/dl/) e installare Go per Microsoft Windows base toohello [le istruzioni di installazione](https://golang.org/doc/install).
2. Avviare hello prompt dei comandi dal menu di avvio hello.
3. Creare una cartella per il progetto, ad esempio `mkdir  %USERPROFILE%\go\src\mysqlgo`.
4. Spostarsi nella cartella di progetto hello, ad esempio `cd %USERPROFILE%\go\src\mysqlgo`.
5. Impostare la variabile di ambiente hello per la directory del codice sorgente toohello toopoint GOPATH. `set GOPATH=%USERPROFILE%\go`.
6. Installare hello [driver di sql go per mysql](https://github.com/go-sql-driver/mysql#installation) eseguendo hello `go get github.com/go-sql-driver/mysql` comando.

   In sintesi, installare Go e quindi eseguire questi comandi nel prompt dei comandi di hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\mysqlgo
   cd %USERPROFILE%\go\src\mysqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/go-sql-driver/mysql
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Avviare shell Bash hello. 
2. Installare Go eseguendo `sudo apt-get install golang-go`.
3. Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/mysqlgo/`.
4. Spostarsi nella cartella hello, ad esempio `cd ~/go/src/mysqlgo/`.
5. Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella. Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.
6. Installare hello [driver di sql go per mysql](https://github.com/go-sql-driver/mysql#installation) eseguendo hello `go get github.com/go-sql-driver/mysql` comando.

   In sintesi, eseguire questi comandi Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

### <a name="apple-macos"></a>Apple macOS
1. Scaricare e installare andare in base toohello [le istruzioni di installazione](https://golang.org/doc/install) corrispondenti della piattaforma. 
2. Avviare shell Bash hello. 
3. Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/mysqlgo/`.
4. Spostarsi nella cartella hello, ad esempio `cd ~/go/src/mysqlgo/`.
5. Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella. Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.
6. Installare hello [driver di sql go per mysql](https://github.com/go-sql-driver/mysql#installation) eseguendo hello `go get github.com/go-sql-driver/mysql` comando.

   In sintesi, installare Go e quindi eseguire questi comandi Bash:
   ```bash
   mkdir -p ~/go/src/mysqlgo/
   cd ~/go/src/mysqlgo/
   export GOPATH=~/go/
   go get github.com/go-sql-driver/mysql
   ```

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello avere piegato, ad esempio **myserver4demo**.
3. Fare clic sul nome di server hello **myserver4demo**.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-go/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.
   

## <a name="build-and-run-go-code"></a>Compilare ed eseguire il codice Go 
1. toowrite Golang codice, è possibile utilizzare un editor di testo semplice, ad esempio Blocco note di Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) Ubuntu o TextEdit in macOS. Se si preferisce un ambiente IDE (Interactive Development Environment) avanzato, provare [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).
2. Incollare hello codice Go da sezioni hello in file di testo e salvare nella cartella del progetto con estensione \*passare, ad esempio il percorso di Windows `%USERPROFILE%\go\src\mysqlgo\createtable.go` o percorso di Linux `~/go/src/mysqlgo/createtable.go`.
3. Individuare hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` costanti nel codice hello e sostituire i valori di esempio hello con valori personalizzati. 
4. Avviare il prompt di comandi hello o della shell bash. Passare alla cartella del progetto, ad esempio `cd %USERPROFILE%\go\src\mysqlgo\` in Windows. In Linux `cd ~/go/src/mysqlgo/`.  Alcuni editor IDE hello indicato offrono funzionalità di debug e di runtime senza i comandi della shell.
5. Eseguire il codice hello digitando il comando hello `go run createtable.go` toocompile hello applicazione ed eseguirlo. 
6. In alternativa, toobuild codice hello in un'applicazione nativa, `go build createtable.go`, quindi avviare `createtable.exe` toorun un'applicazione hello.

## <a name="connect-create-table-and-insert-data"></a>Connettersi, creare tabelle e inserire dati
Seguente hello utilizzare codice tooconnect toohello server, creare una tabella e caricare i dati di hello usando un **inserire** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [driver sql passare per mysql](https://github.com/go-sql-driver/mysql#installation) come toocommunicate un driver con Database di Azure per MySQL hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/)per stampato input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database per MySQL e connessione hello controlli utilizzando metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) metodo più volte toorun diversi comandi DDL. Hello viene utilizzata anche hello [Prepare()](http://go-database-sql.org/prepared.html) e toorun Exec () preparato di istruzioni con parametri diversi tooinsert tre righe. Ogni volta che un metodo personalizzato checkError() è toocheck usato se l'errore e andare nel panico tooexit.

Sostituire hello `host`, `database`, `user`, e `password` costanti con valori personalizzati. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed).")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table.")

    // Insert some data into table.
    sqlStatement, err := db.Prepare("INSERT INTO inventory (name, quantity) VALUES (?, ?);")
    res, err := sqlStatement.Exec("banana", 150)
    checkError(err)
    rowCount, err := res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("orange", 154)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)

    res, err = sqlStatement.Exec("apple", 100)
    checkError(err)
    rowCount, err = res.RowsAffected()
    fmt.Printf("Inserted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}

```

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [driver sql passare per mysql](https://github.com/go-sql-driver/mysql#installation) come toocommunicate un driver con Database di Azure per MySQL hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/)per stampato input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database per MySQL e connessione hello controlli utilizzando metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [query ()](https://golang.org/pkg/database/sql/#DB.Query) comando select hello toorun di metodo. Esegue quindi il [Next](https://golang.org/pkg/database/sql/#Rows.Next) tooiterate tramite il set di risultati hello e [Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) tooparse hello i valori di colonna salvataggio valore hello in variabili. Ogni volta che un metodo personalizzato checkError() è toocheck usato se l'errore e andare nel panico tooexit.

Sostituire hello `host`, `database`, `user`, e `password` costanti con valori personalizzati. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Variables for printing column data when scanned.
    var (
        id       int
        name     string
        quantity int
    )

    // Read some data from hello table.
    rows, err := db.Query("SELECT id, name, quantity from inventory;")
    checkError(err)
    defer rows.Close()
    fmt.Println("Reading data:")
    for rows.Next() {
        err := rows.Scan(&id, &name, &quantity)
        checkError(err)
        fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
    }
    err = rows.Err()
    checkError(err)
    fmt.Println("Done.")
}
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [driver sql passare per mysql](https://github.com/go-sql-driver/mysql#installation) come toocommunicate un driver con Database di Azure per MySQL hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/)per stampato input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database per MySQL e connessione hello controlli utilizzando metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) comando update hello toorun di metodo. Ogni volta che un metodo personalizzato checkError() è toocheck usato se l'errore e andare nel panico tooexit.

Sostituire hello `host`, `database`, `user`, e `password` costanti con valori personalizzati. 

```Go
package main

import (
    "database/sql"
    "fmt"

    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("UPDATE inventory SET quantity = ? WHERE name = ?", 200, "banana")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e rimuovere dati tramite un **eliminare** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [driver sql passare per mysql](https://github.com/go-sql-driver/mysql#installation) come toocommunicate un driver con Database di Azure per MySQL hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/)per stampato input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://go-database-sql.org/accessing.html) tooconnect tooAzure Database per MySQL e connessione hello controlli utilizzando metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metodo comando delete. Ogni volta che un metodo personalizzato checkError() è toocheck usato se l'errore e andare nel panico tooexit.

Sostituire hello `host`, `database`, `user`, e `password` costanti con valori personalizzati. 

```Go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/go-sql-driver/mysql"
)

const (
    host     = "myserver4demo.mysql.database.azure.com"
    database = "quickstartdb"
    user     = "myadmin@myserver4demo"
    password = "yourpassword"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString = fmt.Sprintf("%s:%s@tcp(%s:3306)/%s?allowNativePasswords=true", user, password, host, database)

    // Initialize connection object.
    db, err := sql.Open("mysql", connectionString)
    checkError(err)
    defer db.Close()

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase.")

    // Modify some data in table.
    rows, err := db.Exec("DELETE FROM inventory WHERE name = ?", "orange")
    checkError(err)
    rowCount, err := rows.RowsAffected()
    fmt.Printf("Deleted %d row(s) of data.\n", rowCount)
    fmt.Println("Done.")
}
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./concepts-migrate-import-export.md)
