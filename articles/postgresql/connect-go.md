---
title: Connettersi a Database di Azure per PostgreSQL usando il linguaggio Go | Microsoft Docs
description: "Questa guida introduttiva fornisce un esempio di linguaggio di programmazione Go che è possibile usare per connettersi ai dati ed eseguire query da Database di Azure per PostgreSQL."
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
ms.openlocfilehash: a7555464879826c5e4f55929d23163b002664e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-go-language-to-connect-and-query-data"></a><span data-ttu-id="b6830-103">Database di Azure per PostgreSQL: usare il linguaggio Go per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="b6830-103">Azure Database for PostgreSQL: Use Go language to connect and query data</span></span>
<span data-ttu-id="b6830-104">Questa guida introduttiva illustra come connettersi a un database di Azure per PostgreSQL usando il codice scritto nel linguaggio [Go](https://golang.org/) (golang).</span><span class="sxs-lookup"><span data-stu-id="b6830-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using code written in the [Go](https://golang.org/) language (golang).</span></span> <span data-ttu-id="b6830-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="b6830-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="b6830-106">Questo articolo presuppone che si abbia familiarità con lo sviluppo con Go, ma non con Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b6830-106">This article assumes you are familiar with development using Go, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6830-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b6830-107">Prerequisites</span></span>
<span data-ttu-id="b6830-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="b6830-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="b6830-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="b6830-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="b6830-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b6830-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-go-and-pq-connector"></a><span data-ttu-id="b6830-111">Installare Go e il connettore pq</span><span class="sxs-lookup"><span data-stu-id="b6830-111">Install Go and pq connector</span></span>
<span data-ttu-id="b6830-112">Installare [Go](https://golang.org/doc/install) e il [driver Pure Go per Postgres (pq)](https://github.com/lib/pq) nel computer.</span><span class="sxs-lookup"><span data-stu-id="b6830-112">Install [Go](https://golang.org/doc/install) and the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) on your own machine.</span></span> <span data-ttu-id="b6830-113">A seconda della piattaforma, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="b6830-113">Depending on your platform, follow the steps:</span></span>

### <a name="windows"></a><span data-ttu-id="b6830-114">Windows</span><span class="sxs-lookup"><span data-stu-id="b6830-114">Windows</span></span>
1. <span data-ttu-id="b6830-115">[Scaricare](https://golang.org/dl/) e installare Go per Microsoft Windows seguendo le [istruzioni di installazione](https://golang.org/doc/install).</span><span class="sxs-lookup"><span data-stu-id="b6830-115">[Download](https://golang.org/dl/) and install Go for Microsoft Windows according to the [installation instructions](https://golang.org/doc/install).</span></span>
2. <span data-ttu-id="b6830-116">Avviare il prompt dei comandi dal menu Start.</span><span class="sxs-lookup"><span data-stu-id="b6830-116">Launch the command prompt from the start menu.</span></span>
3. <span data-ttu-id="b6830-117">Creare una cartella per il progetto, ad esempio</span><span class="sxs-lookup"><span data-stu-id="b6830-117">Make a folder for your project such.</span></span> <span data-ttu-id="b6830-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="b6830-118">`mkdir  %USERPROFILE%\go\src\postgresqlgo`.</span></span>
4. <span data-ttu-id="b6830-119">Passare alla cartella del progetto, ad esempio `cd %USERPROFILE%\go\src\postgresqlgo`.</span><span class="sxs-lookup"><span data-stu-id="b6830-119">Change directory into the project folder, such as `cd %USERPROFILE%\go\src\postgresqlgo`.</span></span>
5. <span data-ttu-id="b6830-120">Impostare la variabile di ambiente per GOPATH in modo che punti alla directory del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="b6830-120">Set the environment variable for GOPATH to point to the source code directory.</span></span> <span data-ttu-id="b6830-121">`set GOPATH=%USERPROFILE%\go`.</span><span class="sxs-lookup"><span data-stu-id="b6830-121">`set GOPATH=%USERPROFILE%\go`.</span></span>
6. <span data-ttu-id="b6830-122">Installare il [driver Pure Go per Postgres (pq)](https://github.com/lib/pq) eseguendo il comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="b6830-122">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="b6830-123">In sintesi, installare Go e quindi eseguire questi comandi nel prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="b6830-123">In summary, install Go, then run these commands in the command prompt:</span></span>
   ```cmd
   mkdir  %USERPROFILE%\go\src\postgresqlgo
   cd %USERPROFILE%\go\src\postgresqlgo
   set GOPATH=%USERPROFILE%\go
   go get github.com/lib/pq
   ```

### <a name="linux-ubuntu"></a><span data-ttu-id="b6830-124">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="b6830-124">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="b6830-125">Avviare la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="b6830-125">Launch the Bash shell.</span></span> 
2. <span data-ttu-id="b6830-126">Installare Go eseguendo `sudo apt-get install golang-go`.</span><span class="sxs-lookup"><span data-stu-id="b6830-126">Install Go by running `sudo apt-get install golang-go`.</span></span>
3. <span data-ttu-id="b6830-127">Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="b6830-127">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="b6830-128">Passare alla cartella, ad esempio `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="b6830-128">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="b6830-129">Impostare la variabile di ambiente GOPATH in modo che punti a una directory di origine valida, ad esempio la cartella go della home directory corrente.</span><span class="sxs-lookup"><span data-stu-id="b6830-129">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="b6830-130">Nella shell Bash eseguire `export GOPATH=~/go` per aggiungere la directory go come GOPATH per la sessione shell corrente.</span><span class="sxs-lookup"><span data-stu-id="b6830-130">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="b6830-131">Installare il [driver Pure Go per Postgres (pq)](https://github.com/lib/pq) eseguendo il comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="b6830-131">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="b6830-132">In sintesi, eseguire questi comandi Bash:</span><span class="sxs-lookup"><span data-stu-id="b6830-132">In summary, run these bash commands:</span></span>
   ```bash
   sudo apt-get install golang-go
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

### <a name="apple-macos"></a><span data-ttu-id="b6830-133">Apple macOS</span><span class="sxs-lookup"><span data-stu-id="b6830-133">Apple macOS</span></span>
1. <span data-ttu-id="b6830-134">Scaricare e installare Go seguendo le [istruzioni di installazione](https://golang.org/doc/install) per la piattaforma in uso.</span><span class="sxs-lookup"><span data-stu-id="b6830-134">Download and install Go according to the [installation instructions](https://golang.org/doc/install)  matching your platform.</span></span> 
2. <span data-ttu-id="b6830-135">Avviare la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="b6830-135">Launch the Bash shell.</span></span> 
3. <span data-ttu-id="b6830-136">Creare una cartella per il progetto nella home directory, ad esempio `mkdir -p ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="b6830-136">Make a folder for your project in your home directory, such as `mkdir -p ~/go/src/postgresqlgo/`.</span></span>
4. <span data-ttu-id="b6830-137">Passare alla cartella, ad esempio `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="b6830-137">Change directory into the folder, such as `cd ~/go/src/postgresqlgo/`.</span></span>
5. <span data-ttu-id="b6830-138">Impostare la variabile di ambiente GOPATH in modo che punti a una directory di origine valida, ad esempio la cartella go della home directory corrente.</span><span class="sxs-lookup"><span data-stu-id="b6830-138">Set the GOPATH environment variable to point to a valid source directory, such as your current home directory's go folder.</span></span> <span data-ttu-id="b6830-139">Nella shell Bash eseguire `export GOPATH=~/go` per aggiungere la directory go come GOPATH per la sessione shell corrente.</span><span class="sxs-lookup"><span data-stu-id="b6830-139">At the bash shell, run `export GOPATH=~/go` to add the go directory as the GOPATH for the current shell session.</span></span>
6. <span data-ttu-id="b6830-140">Installare il [driver Pure Go per Postgres (pq)](https://github.com/lib/pq) eseguendo il comando `go get github.com/lib/pq`.</span><span class="sxs-lookup"><span data-stu-id="b6830-140">Install the [Pure Go Postgres driver (pq)](https://github.com/lib/pq) by running the `go get github.com/lib/pq` command.</span></span>

   <span data-ttu-id="b6830-141">In sintesi, installare Go e quindi eseguire questi comandi Bash:</span><span class="sxs-lookup"><span data-stu-id="b6830-141">In summary, install Go, then run these bash commands:</span></span>
   ```bash
   mkdir -p ~/go/src/postgresqlgo/
   cd ~/go/src/postgresqlgo/
   export GOPATH=~/go/
   go get github.com/lib/pq
   ```

## <a name="get-connection-information"></a><span data-ttu-id="b6830-142">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="b6830-142">Get connection information</span></span>
<span data-ttu-id="b6830-143">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="b6830-143">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="b6830-144">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="b6830-144">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="b6830-145">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="b6830-145">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b6830-146">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="b6830-146">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="b6830-147">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="b6830-147">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="b6830-148">Selezionare la pagina **Panoramica** del server.</span><span class="sxs-lookup"><span data-stu-id="b6830-148">Select the server's **Overview** page.</span></span> <span data-ttu-id="b6830-149">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="b6830-149">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="b6830-150">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-go/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="b6830-150">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-go/1-connection-string.png)</span></span>
5. <span data-ttu-id="b6830-151">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** e visualizzare il nome di accesso dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="b6830-151">If you forget your server login information, navigate to the **Overview** page, and view the Server admin login name.</span></span> <span data-ttu-id="b6830-152">Se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="b6830-152">If necessary, reset the password.</span></span>

## <a name="build-and-run-go-code"></a><span data-ttu-id="b6830-153">Compilare ed eseguire il codice Go</span><span class="sxs-lookup"><span data-stu-id="b6830-153">Build and run Go code</span></span> 
1. <span data-ttu-id="b6830-154">Per scrivere codice Golang si può usare un editor di testo semplice, ad esempio Blocco note di Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) o [Nano](https://www.nano-editor.org/) in Ubuntu oppure TextEdit in macOS.</span><span class="sxs-lookup"><span data-stu-id="b6830-154">To write Golang code, you can use a simple text editor, such as Notepad in Microsoft Windows, [vi](http://manpages.ubuntu.com/manpages/xenial/man1/nvi.1.html#contenttoc5) or [Nano](https://www.nano-editor.org/) in Ubuntu, or TextEdit in macOS.</span></span> <span data-ttu-id="b6830-155">Se si preferisce un ambiente IDE (Interactive Development Environment) avanzato, provare [Gogland](https://www.jetbrains.com/go/) di Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) di Microsoft o [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="b6830-155">If you prefer a richer Interactive Development Environment (IDE) try [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span>
2. <span data-ttu-id="b6830-156">Incollare nel file di testo il codice Golang riportato nelle sezioni seguenti, quindi salvare il file nella cartella del progetto con l'estensione \*.go, ad esempio il percorso di Windows `%USERPROFILE%\go\src\postgresqlgo\createtable.go` o il percorso di Linux `~/go/src/postgresqlgo/createtable.go`.</span><span class="sxs-lookup"><span data-stu-id="b6830-156">Paste the Golang code from the sections below into text files, and save into your project folder with file extension \*.go, such as Windows path `%USERPROFILE%\go\src\postgresqlgo\createtable.go` or Linux path `~/go/src/postgresqlgo/createtable.go`.</span></span>
3. <span data-ttu-id="b6830-157">Trovare le costanti `HOST`, `DATABASE`, `USER` e `PASSWORD` nel codice e sostituire i valori di esempio con i propri valori.</span><span class="sxs-lookup"><span data-stu-id="b6830-157">Locate the `HOST`, `DATABASE`, `USER`, and `PASSWORD` constants in the code, and replace the example values with your own values.</span></span>  
4. <span data-ttu-id="b6830-158">Avviare il prompt dei comandi o la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="b6830-158">Launch the command prompt or bash shell.</span></span> <span data-ttu-id="b6830-159">Passare alla cartella del progetto,</span><span class="sxs-lookup"><span data-stu-id="b6830-159">Change directory into your project folder.</span></span> <span data-ttu-id="b6830-160">ad esempio `cd %USERPROFILE%\go\src\postgresqlgo\` in Windows.</span><span class="sxs-lookup"><span data-stu-id="b6830-160">For example, on Windows `cd %USERPROFILE%\go\src\postgresqlgo\`.</span></span> <span data-ttu-id="b6830-161">In Linux `cd ~/go/src/postgresqlgo/`.</span><span class="sxs-lookup"><span data-stu-id="b6830-161">On Linux `cd ~/go/src/postgresqlgo/`.</span></span> <span data-ttu-id="b6830-162">Alcuni degli ambienti IDE indicati offrono funzionalità di debug e di runtime che non richiedono comandi della shell.</span><span class="sxs-lookup"><span data-stu-id="b6830-162">Some of the IDE environments mentioned offer debug and runtime capabilities without requiring shell commands.</span></span>
5. <span data-ttu-id="b6830-163">Eseguire il codice digitando il comando `go run createtable.go` per compilare l'applicazione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="b6830-163">Run the code by typing the command `go run createtable.go` to compile the application and run it.</span></span> 
6. <span data-ttu-id="b6830-164">In alternativa, per compilare il codice in un'applicazione nativa, digitare `go build createtable.go` e quindi avviare `createtable.exe` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b6830-164">Alternatively, to build the code into a native application, `go build createtable.go`, then launch `createtable.exe` to run the application.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="b6830-165">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="b6830-165">Connect and create a table</span></span>
<span data-ttu-id="b6830-166">Usare il codice seguente per connettersi e creare una tabella usando l'istruzione SQL **CREATE TABLE**, seguita dalle istruzioni SQL **INSERT INTO** per aggiungere righe nella tabella.</span><span class="sxs-lookup"><span data-stu-id="b6830-166">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="b6830-167">Il codice importa tre pacchetti: il [pacchetto sql](https://golang.org/pkg/database/sql/), il [pacchetto pq](http://godoc.org/github.com/lib/pq), come driver per comunicare con il server Postgres, e il [pacchetto fmt](https://golang.org/pkg/fmt/) per l'input e l'output stampati nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b6830-167">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="b6830-168">Il codice chiama il metodo [sql.Open()](http://godoc.org/github.com/lib/pq#Open) per la connessione a Database di Azure per PostgreSQL e controlla la connessione usando il metodo [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="b6830-168">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="b6830-169">Viene usato un [handle di database](https://golang.org/pkg/database/sql/#DB), contenente il pool di connessioni per il server di database.</span><span class="sxs-lookup"><span data-stu-id="b6830-169">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="b6830-170">Il codice chiama il metodo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) più volte per eseguire diversi comandi SQL.</span><span class="sxs-lookup"><span data-stu-id="b6830-170">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method several times to run several SQL commands.</span></span> <span data-ttu-id="b6830-171">Ogni volta vengono applicati un metodo checkError() personalizzato per controllare se si è verificato un errore e un metodo panic per uscire se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="b6830-171">Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="b6830-172">Sostituire i parametri `HOST`, `DATABASE`, `USER` e `PASSWORD` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b6830-172">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="read-data"></a><span data-ttu-id="b6830-173">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="b6830-173">Read data</span></span>
<span data-ttu-id="b6830-174">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="b6830-174">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="b6830-175">Il codice importa tre pacchetti: il [pacchetto sql](https://golang.org/pkg/database/sql/), il [pacchetto pq](http://godoc.org/github.com/lib/pq), come driver per comunicare con il server Postgres, e il [pacchetto fmt](https://golang.org/pkg/fmt/) per l'input e l'output stampati nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b6830-175">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="b6830-176">Il codice chiama il metodo [sql.Open()](http://godoc.org/github.com/lib/pq#Open) per la connessione a Database di Azure per PostgreSQL e controlla la connessione usando il metodo [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="b6830-176">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="b6830-177">Viene usato un [handle di database](https://golang.org/pkg/database/sql/#DB), contenente il pool di connessioni per il server di database.</span><span class="sxs-lookup"><span data-stu-id="b6830-177">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="b6830-178">La query di selezione viene eseguita chiamando il metodo [db.Query()](https://golang.org/pkg/database/sql/#DB.Query) e le righe risultanti vengono mantenute in una variabile di tipo [rows](https://golang.org/pkg/database/sql/#Rows).</span><span class="sxs-lookup"><span data-stu-id="b6830-178">The select query is run by calling method [db.Query()](https://golang.org/pkg/database/sql/#DB.Query), and the resulting rows is kept in a variable of type [rows](https://golang.org/pkg/database/sql/#Rows).</span></span> <span data-ttu-id="b6830-179">Il codice legge i valori dei dati delle colonne nella riga corrente usando il metodo [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) ed esegue il ciclo sulle righe usando l'iteratore [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) fino ad esaurimento delle righe.</span><span class="sxs-lookup"><span data-stu-id="b6830-179">The code reads the column data values in the current row using method [rows.Scan()](https://golang.org/pkg/database/sql/#Rows.Scan) and loops over the rows using the iterator [rows.Next()](https://golang.org/pkg/database/sql/#Rows.Next) until no more rows exist.</span></span> <span data-ttu-id="b6830-180">I valori delle colonne di ogni riga vengono trasmessi alla console. Ogni volta vengono applicati un metodo checkError() personalizzato per controllare se si è verificato un errore e un metodo panic per uscire se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="b6830-180">Each row's column values are printed to the console out. Each time a custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="b6830-181">Sostituire i parametri `HOST`, `DATABASE`, `USER` e `PASSWORD` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b6830-181">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 

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
    fmt.Println("Successfully created connection to database")

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

## <a name="update-data"></a><span data-ttu-id="b6830-182">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="b6830-182">Update data</span></span>
<span data-ttu-id="b6830-183">Usare il codice seguente per connettersi e aggiornare i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="b6830-183">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="b6830-184">Il codice importa tre pacchetti: il [pacchetto sql](https://golang.org/pkg/database/sql/), il [pacchetto pq](http://godoc.org/github.com/lib/pq), come driver per comunicare con il server Postgres, e il [pacchetto fmt](https://golang.org/pkg/fmt/) per l'input e l'output stampati nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b6830-184">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="b6830-185">Il codice chiama il metodo [sql.Open()](http://godoc.org/github.com/lib/pq#Open) per la connessione a Database di Azure per PostgreSQL e controlla la connessione usando il metodo [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="b6830-185">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="b6830-186">Viene usato un [handle di database](https://golang.org/pkg/database/sql/#DB), contenente il pool di connessioni per il server di database.</span><span class="sxs-lookup"><span data-stu-id="b6830-186">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="b6830-187">Il codice chiama il metodo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) per eseguire l'istruzione SQL che aggiorna la tabella.</span><span class="sxs-lookup"><span data-stu-id="b6830-187">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="b6830-188">Vengono applicati un metodo checkError() personalizzato per controllare se si è verificato un errore e un metodo panic per uscire se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="b6830-188">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="b6830-189">Sostituire i parametri `HOST`, `DATABASE`, `USER` e `PASSWORD` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b6830-189">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Modify some data in table.
    sql_statement := "UPDATE inventory SET quantity = $2 WHERE name = $1;"
    _, err = db.Exec(sql_statement, "banana", 200)
    checkError(err)
    fmt.Println("Updated 1 row of data")
}
```

## <a name="delete-data"></a><span data-ttu-id="b6830-190">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="b6830-190">Delete data</span></span>
<span data-ttu-id="b6830-191">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="b6830-191">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="b6830-192">Il codice importa tre pacchetti: il [pacchetto sql](https://golang.org/pkg/database/sql/), il [pacchetto pq](http://godoc.org/github.com/lib/pq), come driver per comunicare con il server Postgres, e il [pacchetto fmt](https://golang.org/pkg/fmt/) per l'input e l'output stampati nella riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b6830-192">The code imports three packages: the [sql package](https://golang.org/pkg/database/sql/), the [pq package](http://godoc.org/github.com/lib/pq) as a driver to communicate with the Postgres server, and the [fmt package](https://golang.org/pkg/fmt/) for printed input and output on the command line.</span></span>

<span data-ttu-id="b6830-193">Il codice chiama il metodo [sql.Open()](http://godoc.org/github.com/lib/pq#Open) per la connessione a Database di Azure per PostgreSQL e controlla la connessione usando il metodo [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span><span class="sxs-lookup"><span data-stu-id="b6830-193">The code calls method [sql.Open()](http://godoc.org/github.com/lib/pq#Open) to connect to Azure Database for PostgreSQL, and checks the connection using method [db.Ping()](https://golang.org/pkg/database/sql/#DB.Ping).</span></span> <span data-ttu-id="b6830-194">Viene usato un [handle di database](https://golang.org/pkg/database/sql/#DB), contenente il pool di connessioni per il server di database.</span><span class="sxs-lookup"><span data-stu-id="b6830-194">A [database handle](https://golang.org/pkg/database/sql/#DB) is used throughout, holding the connection pool for the database server.</span></span> <span data-ttu-id="b6830-195">Il codice chiama il metodo [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) per eseguire l'istruzione SQL che aggiorna la tabella.</span><span class="sxs-lookup"><span data-stu-id="b6830-195">The code calls the [Exec()](https://golang.org/pkg/database/sql/#DB.Exec) method to run the SQL statement that updates the table.</span></span> <span data-ttu-id="b6830-196">Vengono applicati un metodo checkError() personalizzato per controllare se si è verificato un errore e un metodo panic per uscire se si verifica un errore.</span><span class="sxs-lookup"><span data-stu-id="b6830-196">A custom checkError() method to check if an error occurred and panic to exit if an error occurs.</span></span>

<span data-ttu-id="b6830-197">Sostituire i parametri `HOST`, `DATABASE`, `USER` e `PASSWORD` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b6830-197">Replace the `HOST`, `DATABASE`, `USER`, and `PASSWORD` parameters with your own values.</span></span> 
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
    fmt.Println("Successfully created connection to database")

    // Delete some data from table.
    sql_statement := "DELETE FROM inventory WHERE name = $1;"
    _, err = db.Exec(sql_statement, "orange")
    checkError(err)
    fmt.Println("Deleted 1 row of data")
}
```

## <a name="next-steps"></a><span data-ttu-id="b6830-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6830-198">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="b6830-199">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="b6830-199">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
