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
# <a name="azure-database-for-postgresql-use-go-language-tooconnect-and-query-data"></a><span data-ttu-id="faee9-103">Il Database di Azure per PostgreSQL: utilizzano il comando Go language tooconnect ed eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="faee9-103">Azure Database for PostgreSQL: Use Go language tooconnect and query data</span></span>
<span data-ttu-id="faee9-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL codice hello scritto in [passare](https://golang.org/) language (golang).</span><span class="sxs-lookup"><span data-stu-id="faee9-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using code written in hello [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="faee9-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="faee9-106">In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Go, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-106">This article assumes you are familiar with development using Go, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="faee9-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="faee9-107">Prerequisites</span></span>
<span data-ttu-id="faee9-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="faee9-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="faee9-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="faee9-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="faee9-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="faee9-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="faee9-111">Installare Go e il connettore pq</span><span class="sxs-lookup"><span data-stu-id="faee9-111">Install Go and pq connector</span></span>
<span data-ttu-id="faee9-112">Installare [passare](https://golang.org/doc/install) hello e [driver Postgres passare Pure (pq)](https://github.com/lib/pq) sul proprio computer.</span><span class="sxs-lookup"><span data-stu-id="faee9-112">Install [Go](https://golang.org/doc/install) and hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="faee9-113">A seconda della piattaforma, attenersi alla seguente procedura hello:</span><span class="sxs-lookup"><span data-stu-id="faee9-113">Depending on your platform, follow hello steps:</span></span>

### <a name="windows"></a><span data-ttu-id="faee9-114">Windows</span><span class="sxs-lookup"><span data-stu-id="faee9-114">Windows</span></span>
1. <span data-ttu-id="faee9-115">[Scaricare](https://golang.org/dl/) e installare Go per Microsoft Windows base toohello [le istruzioni di installazione](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="faee9-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according toohello [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="faee9-116">Avviare hello prompt dei comandi dal menu di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-116">Launch hello command prompt from hello start menu.</span></span>
3. <span data-ttu-id="faee9-117">Creare una cartella per il progetto, ad esempio</span><span class="sxs-lookup"><span data-stu-id="faee9-117">Make a folder for your project such.</span></span> <span data-ttu-id="faee9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="faee9-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="faee9-119">Spostarsi nella cartella di progetto hello, ad esempio `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="faee9-119">Change directory into hello project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="faee9-120">Impostare la variabile di ambiente hello per la directory del codice sorgente toohello toopoint GOPATH.</span><span class="sxs-lookup"><span data-stu-id="faee9-120">Set hello environment variable for GOPATH toopoint toohello source code directory.</span></span> <span data-ttu-id="faee9-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="faee9-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="faee9-122">Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="faee9-122">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="faee9-123">In sintesi, installare Go e quindi eseguire questi comandi nel prompt dei comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="faee9-123">In summary, install Go, then run these commands in hello command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="faee9-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="faee9-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="faee9-125">Avviare shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-125">Launch hello Bash shell.</span></span> 
2. <span data-ttu-id="faee9-126">Installare Go eseguendo `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="faee9-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="faee9-127">Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="faee9-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="faee9-128">Spostarsi nella cartella hello, ad esempio `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="faee9-128">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="faee9-129">Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella.</span><span class="sxs-lookup"><span data-stu-id="faee9-129">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="faee9-130">Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-130">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="faee9-131">Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="faee9-131">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="faee9-132">In sintesi, eseguire questi comandi Bash:</span><span class="sxs-lookup"><span data-stu-id="faee9-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="faee9-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="faee9-133">Apple macOS</span></span>
1. <span data-ttu-id="faee9-134">Scaricare e installare andare in base toohello [le istruzioni di installazione](https://golang.org/doc/install) corrispondenti della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="faee9-134">Download and install Go according toohello [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="faee9-135">Avviare shell Bash hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-135">Launch hello Bash shell.</span></span> 
3. <span data-ttu-id="faee9-136">Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="faee9-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="faee9-137">Spostarsi nella cartella hello, ad esempio `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="faee9-137">Change directory into hello folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="faee9-138">Set hello GOPATH ambiente toopoint variabile tooa directory di origine, ad esempio a casa corrente della directory passare cartella.</span><span class="sxs-lookup"><span data-stu-id="faee9-138">Set hello GOPATH environment variable toopoint tooa valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="faee9-139">Fase della shell bash hello, `export GOPATH=~/go` tooadd hello andare directory come hello GOPATH per sessione shell corrente hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-139">At hello bash shell, run `export GOPATH=~/go` tooadd hello go directory as hello GOPATH for hello current shell session.</span></span>
6. <span data-ttu-id="faee9-140">Installare hello [driver Postgres passare Pure (pq)](https://github.com/lib/pq) eseguendo hello `go get github.com/lib/pq` comando.</span><span class="sxs-lookup"><span data-stu-id="faee9-140">Install hello [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running hello `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="faee9-141">In sintesi, installare Go e quindi eseguire questi comandi Bash:</span><span class="sxs-lookup"><span data-stu-id="faee9-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="faee9-142">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="faee9-142">Get connection information</span></span>
<span data-ttu-id="faee9-143">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-143">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="faee9-144">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="faee9-144">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="faee9-145">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="faee9-145">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="faee9-146">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="faee9-146">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="faee9-147">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="faee9-147">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="faee9-148">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="faee9-148">Select hello server's **Overview** page.</span></span> <span data-ttu-id="faee9-149">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="faee9-149">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="faee9-150">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="faee9-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="faee9-151">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina e il nome account di accesso amministratore di visualizzazione hello Server.</span><span class="sxs-lookup"><span data-stu-id="faee9-151">If you forget your server login information, navigate toohello **Overview** page, and view hello Server admin login name.</span></span> <span data-ttu-id="faee9-152">Se necessario, hello reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="faee9-152">If necessary, reset hello password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="faee9-153">Compilare ed eseguire il codice Go</span><span class="sxs-lookup"><span data-stu-id="faee9-153">Build and run Go code</span></span> 
1. <span data-ttu-id="faee9-154">toowrite Golang codice, è possibile utilizzare un editor di testo semplice, ad esempio Blocco note di Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) Ubuntu o TextEdit in macOS.</span><span class="sxs-lookup"><span data-stu-id="faee9-154">toowrite Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="faee9-155">Se si preferisce un ambiente IDE (Interactive Development Environment) avanzato, provare [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="faee9-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="faee9-156">Incollare il codice Golang hello dalle sezioni hello sotto in file di testo e salvare nella cartella del progetto con estensione \*passare, ad esempio il percorso di Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` o percorso di Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="faee9-156">Paste hello Golang code from hello sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="faee9-157">Individuare hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` costanti nel codice hello e sostituire i valori di esempio hello con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="faee9-157">Locate hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in hello code, and replace hello example values with your own values.</span></span>  
4. <span data-ttu-id="faee9-158">Avviare il prompt di comandi hello o della shell bash.</span><span class="sxs-lookup"><span data-stu-id="faee9-158">Launch hello command prompt or bash shell.</span></span> <span data-ttu-id="faee9-159">Passare alla cartella del progetto,</span><span class="sxs-lookup"><span data-stu-id="faee9-159">Change directory into your project folder.</span></span> <span data-ttu-id="faee9-160">ad esempio `cd %USERPROFILE%\go\src\postgresqlgo\` in Windows.</span><span class="sxs-lookup"><span data-stu-id="faee9-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="faee9-161">In Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="faee9-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="faee9-162">Alcuni degli ambienti IDE hello indicati offrono funzionalità di debug e di runtime senza i comandi della shell.</span><span class="sxs-lookup"><span data-stu-id="faee9-162">Some of hello IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="faee9-163">Eseguire il codice hello digitando il comando hello `go run createtable.go` toocompile hello applicazione ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="faee9-163">Run hello code by typing hello command `go run createtable.go` toocompile hello application and run it.</span></span> 
6. <span data-ttu-id="faee9-164">In alternativa, toobuild codice hello in un'applicazione nativa, `go build createtable.go`, quindi avviare `createtable.exe` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-164">Alternatively, toobuild hello code into a native application, `go build createtable.go`, then launch `createtable.exe` toorun hello application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="faee9-165">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="faee9-165">Connect and create a table</span></span>
<span data-ttu-id="faee9-166">Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-166">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="faee9-167">codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-167">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="faee9-168">codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="faee9-168">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="faee9-169">Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="faee9-170">hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) metodo toorun più volte alcuni comandi SQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-170">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times toorun several SQL commands.</span></span> <span data-ttu-id="faee9-171">Ogni un toocheck metodo checkError() personalizzato se si è verificato un errore e andare nel panico tooexit se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="faee9-171">Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="faee9-172">Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="faee9-172">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="faee9-173">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="faee9-173">Read data</span></span>
<span data-ttu-id="faee9-174">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-174">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="faee9-175">codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-175">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="faee9-176">codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="faee9-176">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="faee9-177">Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="faee9-178">query select Hello viene eseguita tramite la chiamata di metodo [db. Query ()](https://golang.org/pkg/database/sql/#DB.Query), e le righe risultanti hello viene mantenuta in una variabile di tipo [righe](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="faee9-178">hello select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and hello resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="faee9-179">codice Hello legge i valori di dati colonna hello nella riga corrente di hello metodo [righe. Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) e cicli su righe hello utilizzando hello iteratore [righe. Next](https://golang.org/pkg/database/sql/#Rows.Next) fino a quando non esiste alcuna ulteriore riga.</span><span class="sxs-lookup"><span data-stu-id="faee9-179">hello code reads hello column data values in hello current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over hello rows using hello iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="faee9-180">I valori di colonna di ogni riga sono console toohello stampato out. Ogni un toocheck metodo checkError() personalizzato se si è verificato un errore e andare nel panico tooexit se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="faee9-180">Each row's column values are printed toohello console out. Each time a custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="faee9-181">Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="faee9-181">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="faee9-182">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="faee9-182">Update data</span></span>
<span data-ttu-id="faee9-183">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-183">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="faee9-184">codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-184">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="faee9-185">codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="faee9-185">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="faee9-186">Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="faee9-187">hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metodo istruzione SQL che aggiorna la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-187">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="faee9-188">Un toocheck metodo checkError() personalizzata se l'errore e andare nel panico tooexit se l'errore si verifica.</span><span class="sxs-lookup"><span data-stu-id="faee9-188">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="faee9-189">Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="faee9-189">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="delete-data"></a><span data-ttu-id="faee9-190">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="faee9-190">Delete data</span></span>
<span data-ttu-id="faee9-191">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="faee9-191">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="faee9-192">codice Hello Importa tre pacchetti: hello [pacchetto sql](https://golang.org/pkg/database/sql/), hello [pacchetto pq](http://godoc.org/github.com/lib/pq) come toocommunicate un driver con server Postgres hello e hello [pacchetto fmt](https://golang.org/pkg/fmt/) per stampa input e output nella riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-192">hello code imports three packages: hello [sql package](https://golang.org/pkg/database/sql/), hello [pq package](http://godoc.org/github.com/lib/pq) as a driver toocommunicate with hello Postgres server, and hello [fmt package](https://golang.org/pkg/fmt/) for printed input and output on hello command line.</span></span>

<span data-ttu-id="faee9-193">codice Hello chiama metodo [sql. Open ()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database PostgreSQL e connessione hello controlli con metodo [db. Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="faee9-193">hello code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) tooconnect tooAzure Database for PostgreSQL, and checks hello connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="faee9-194">Oggetto [handle di database](https://golang.org/pkg/database/sql/#DB) viene utilizzata in, che contiene il pool di connessioni hello per il server di database hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding hello connection pool for hello database server.</span></span> <span data-ttu-id="faee9-195">hello chiamate di codice Hello [Exec ()](https://golang.org/pkg/database/sql/#DB.Exec) hello toorun metodo istruzione SQL che aggiorna la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="faee9-195">hello code calls hello [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method toorun hello SQL statement that updates hello table.</span></span> <span data-ttu-id="faee9-196">Un toocheck metodo checkError() personalizzata se l'errore e andare nel panico tooexit se l'errore si verifica.</span><span class="sxs-lookup"><span data-stu-id="faee9-196">A custom checkError() method toocheck if an error occurred and panic tooexit if an error occurs.</span></span>

<span data-ttu-id="faee9-197">Sostituire hello `HOST`, `DATABASE`, `USER`, e `PASSWORD` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="faee9-197">Replace hello `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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

## <a name="next-steps"></a><span data-ttu-id="faee9-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="faee9-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="faee9-199">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="faee9-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
