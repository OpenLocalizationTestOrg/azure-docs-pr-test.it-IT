---
title: aaaConnect tooAzure Database PostgreSQL usando il linguaggio Go | Documenti Microsoft
description: "Questa Guida rapida viene fornito un Go programmazione language esempio è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: go
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: aa3c93da03116b8fcb54557494dccfad558e5f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a>Il Database di Azure per PostgreSQL: utilizzano il comando Go language tooconnect ed eseguire query sui dati
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL codice hello scritto in [passare](https://golang.org/) language (golang). Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Go, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Creare un database: portale](quickstart-create-server-database-portal.md)
- [Creare un database: interfaccia della riga di comando di Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a>Installare Go e il connettore pq
Installare [passare](https://golang.org/doc/install) hello e [driver Postgres passare Pure (pq)](https://github.com/lib/pq) sul proprio computer. A seconda della piattaforma, attenersi alla seguente procedura hello:

### <a name="windows"></a>Windows
1. [Scaricare](https://golang.org/dl/) e installare Go per Microsoft Windows base toohello [le istruzioni di installazione](https://golang.org/doc/install).
2. Avviare hello prompt dei comandi dal menu di avvio hello.
3. Creare una cartella per il progetto, ad esempio `mkdir  %USERPROFILE%\go\src\postgresqlgo`.
4. Spostarsi nella cartella di progetto hello, ad esempio `cd %USERPROFILE%\go\src\postgresqlgo`.
5. Impostare la variabile di ambiente hello per la directory del codice sorgente toohello toopoint GOPATH. `set GOPATH=%USERPROFILE%\go`.
6. Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.

   In sintesi, installare Go e quindi eseguire questi comandi nel prompt dei comandi di hello:
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Avviare shell Bash hello. 
2. Installare Go eseguendo `sudo apt-get install golang-go`.
3. Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.
4. Spostarsi nella cartella hello, ad esempio `cd ~/go/src/postgresqlgo/`.
5. Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella. Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.
6. Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.

   In sintesi, eseguire questi comandi Bash:
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a>Apple macOS
1. Scaricare e installare andare in base toohello [le istruzioni di installazione](https://golang.org/doc/install) corrispondenti della piattaforma. 
2. Avviare shell Bash hello. 
3. Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.
4. Spostarsi nella cartella hello, ad esempio `cd ~/go/src/postgresqlgo/`.
5. Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella. Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.
6. Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.

   In sintesi, installare Go e quindi eseguire questi comandi Bash:
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.
3. Fare clic sul nome di server hello **mypgserver 20170401**.
4. Server di selezionare hello **Panoramica** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-go/1-connection-string.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina e il nome account di accesso amministratore di visualizzazione hello Server. Se necessario, hello reimpostazione della password.

## <a name="build-and-run-go-code"></a>Compilare ed eseguire il codice Go 
1. toowrite Golang codice, è possibile utilizzare un editor di testo semplice, ad esempio Blocco note di Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) Ubuntu o TextEdit in macOS. Se si preferisce un ambiente IDE (Interactive Development Environment) avanzato, provare [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).
2. Incollare il codice Golang hello dalle sezioni hello sotto in file di testo e salvare nella cartella del progetto con estensione \*passare, ad esempio il percorso di Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` o percorso di Linux `~/go/src/postgresqlgo/createtable.go`.
3. Individuare hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` costanti nel codice hello e sostituire i valori di esempio hello con valori personalizzati.  
4. Avviare il prompt di comandi hello o della shell bash. Passare alla cartella del progetto, ad esempio `cd %USERPROFILE%\go\src\postgresqlgo\` in Windows. In Linux `cd ~/go/src/postgresqlgo/`. Alcuni degli ambienti IDE hello indicati offrono funzionalità di debug e di runtime senza i comandi della shell.
5. Eseguire il codice hello digitando il comando hello `go run createtable.go` toocompile hello applicazione ed eseguirlo. 
6. In alternativa, toobuild codice hello in un'applicazione nativa, `go build createtable.go`, quindi avviare `createtable.exe` toorun un'applicazione hello.

## <a name="connect-and-create-a-table"></a>Connettersi e creare una tabella
Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) metodo toorun più volte alcuni comandi SQL. Ogni un toocheck metodo checkError() personalizzato se si è verificato un errore e andare nel panico tooexit se si verifica un errore.

Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Drop previous table of same name if one exists.
    _, err = db.Exec("DROP TABLE IF EXISTS inventory;")
    checkError(err)
    fmt.Println("Finished dropping table (if existed)")

    // Create table.
    _, err = db.Exec("CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);")
    checkError(err)
    fmt.Println("Finished creating table")

    // Insert some data into table.
    sql_statement := "INSERT INTO inventory (name, quantity) VALUES ($1, $2);"
    _, err = db.Exec(sql_statement, "banana", 150)
    checkError(err)
    _, err = db.Exec(sql_statement, "orange", 154)
    checkError(err)
    _, err = db.Exec(sql_statement, "apple", 100)
    checkError(err)
    fmt.Println("Inserted 3 rows of data")
}
```

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. query select Hello viene eseguita tramite la chiamata di metodo [db. Query ()](https://golang.org/pkg/database/sql/#DB.Query), e le righe risultanti hello viene mantenuta in una variabile di tipo [righe](https://golang.org/pkg/database/sql/#Rows). codice Hello legge i valori di dati colonna hello nella riga corrente di hello metodo [righe. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) e cicli su righe hello utilizzando hello iteratore [righe. Next](https://golang.org/pkg/database/sql/#Rows.Next) fino a quando non esiste alcuna ulteriore riga. I valori di colonna di ogni riga sono console toohello stampato out. Ogni un toocheck metodo checkError() personalizzato se si è verificato un errore e andare nel panico tooexit se si verifica un errore.

Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati. 

```go
package main

import (
    "database/sql"
    "fmt"
    _ "github.com/lib/pq"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {

    // Initialize connection string.
    var connectionString string = fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Read rows from table.
    var id int
    var name string
    var quantity int

    sql_statement := "SELECT * from inventory;"
    rows, err := db.Query(sql_statement)
    checkError(err)

    for rows.Next() {
        switch err := rows.Scan(&id, &name, &quantity); err {
        case sql.ErrNoRows:
            fmt.Println("No rows were returned")
        case nil:
            fmt.Printf("Data row = (%d, %s, %d)\n", id, name, quantity)
        default:
            checkError(err)
        }
    }
}
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metodo istruzione SQL che aggiorna la tabella hello. Un toocheck metodo checkError() personalizzata se l'errore e andare nel panico tooexit se l'errore si verifica.

Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.

codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping). Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello. hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metodo istruzione SQL che aggiorna la tabella hello. Un toocheck metodo checkError() personalizzata se l'errore e andare nel panico tooexit se l'errore si verifica.

Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati. 
```go
package main

import (
  "database/sql"
  _ "github.com/lib/pq"
  "fmt"
)

const (
    // Initialize connection constants.
    HOST     = "mypgserver-20170401.postgres.database.azure.com"
    DATABASE = "mypgsqldb"
    USER     = "mylogin@mypgserver-20170401"
    PASSWORD = "<server_admin_password>"
)

func checkError(err error) {
    if err != nil {
        panic(err)
    }
}

func main() {
    
    // Initialize connection string.
    var connectionString string = 
        fmt.Sprintf("host=%s user=%s password=%s dbname=%s sslmode=require", HOST, USER, PASSWORD, DATABASE)

    // Initialize connection object.
    db, err := sql.Open("postgres", connectionString)
    checkError(err)

    err = db.Ping()
    checkError(err)
    fmt.Println("Successfully created connection toodatabase")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
