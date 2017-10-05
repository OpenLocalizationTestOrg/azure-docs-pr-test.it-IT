---
title: Connettersi a Database di Azure per PostgreSQL usando Ruby | Microsoft Docs
description: "Questa guida introduttiva fornisce un esempio di codice Ruby che è possibile usare per connettersi ai dati ed eseguire query da Database di Azure per PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: ruby
ms.topic: quickstart
ms.date: 06/30/2017
ms.openlocfilehash: 9153a5a843dd5c18f27a3af232fea3b152240fe1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-ruby-to-connect-and-query-data"></a><span data-ttu-id="2a820-103">Database di Azure per PostgreSQL: usare Ruby per connettersi ai dati ed eseguire query</span><span class="sxs-lookup"><span data-stu-id="2a820-103">Azure Database for PostgreSQL: Use Ruby to connect and query data</span></span>
<span data-ttu-id="2a820-104">Questa guida introduttiva illustra come connettersi a un database di Azure per PostgreSQL usando un'applicazione [Ruby](https://www.ruby-lang.org).</span><span class="sxs-lookup"><span data-stu-id="2a820-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="2a820-105">Spiega come usare le istruzioni SQL per eseguire query, inserire, aggiornare ed eliminare dati nel database.</span><span class="sxs-lookup"><span data-stu-id="2a820-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="2a820-106">Questo articolo presuppone che si abbia familiarità con lo sviluppo con Ruby, ma non con Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-106">This article assumes you are familiar with development using Ruby, but that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a820-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2a820-107">Prerequisites</span></span>
<span data-ttu-id="2a820-108">Questa guida introduttiva usa le risorse create in una delle guide seguenti come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="2a820-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2a820-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="2a820-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="2a820-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2a820-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="2a820-111">Installare Ruby</span><span class="sxs-lookup"><span data-stu-id="2a820-111">Install Ruby</span></span>
<span data-ttu-id="2a820-112">Installare Ruby nel computer.</span><span class="sxs-lookup"><span data-stu-id="2a820-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="2a820-113">Windows</span><span class="sxs-lookup"><span data-stu-id="2a820-113">Windows</span></span>
- <span data-ttu-id="2a820-114">Scaricare e installare la versione più recente di [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2a820-114">Download and Install the latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="2a820-115">Nella schermata finale del programma di installazione MSI selezionare la casella "Run 'ridk install' to install MSYS2 and development toolchain" (Esegui 'ridk install' per installare MSYS2 e la toolchain di sviluppo).</span><span class="sxs-lookup"><span data-stu-id="2a820-115">On the finish screen of the MSI installer, check the box that says "Run 'ridk install' to install MSYS2 and development toolchain."</span></span> <span data-ttu-id="2a820-116">Fare quindi clic su **Finish** (Fine) per avviare il programma di installazione successivo.</span><span class="sxs-lookup"><span data-stu-id="2a820-116">Then click **Finish** to launch the next installer.</span></span>
- <span data-ttu-id="2a820-117">Viene avviato il programma di installazione di RubyInstaller2 per Windows.</span><span class="sxs-lookup"><span data-stu-id="2a820-117">The RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="2a820-118">Digitare 2 per installare l'aggiornamento del repository MSYS2.</span><span class="sxs-lookup"><span data-stu-id="2a820-118">Type 2 to install the MSYS2 repository update.</span></span> <span data-ttu-id="2a820-119">Dopo avere terminato ed essere tornati alla richiesta di installazione, chiudere la finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="2a820-119">After it finishes and returns to the installation prompt, close the command window.</span></span>
- <span data-ttu-id="2a820-120">Avviare un nuovo prompt dei comandi (cmd) dal menu Start.</span><span class="sxs-lookup"><span data-stu-id="2a820-120">Launch a new command prompt (cmd) from the Start menu.</span></span>
- <span data-ttu-id="2a820-121">Testare l'installazione di Ruby `ruby -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-121">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-122">Testare l'installazione di Gem `gem -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-122">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-123">Eseguire il comando `gem install pg` per compilare il modulo PostgreSQL per Ruby usando Gem.</span><span class="sxs-lookup"><span data-stu-id="2a820-123">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="2a820-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="2a820-124">MacOS</span></span>
- <span data-ttu-id="2a820-125">Eseguire il comando `brew install ruby` per installare Ruby usando Homebrew.</span><span class="sxs-lookup"><span data-stu-id="2a820-125">Install Ruby using Homebrew by running the command `brew install ruby`.</span></span> <span data-ttu-id="2a820-126">Per altre opzioni di installazione, vedere la [documentazione sull'installazione](https://www.ruby-lang.org/en/documentation/installation/#homebrew) di Ruby.</span><span class="sxs-lookup"><span data-stu-id="2a820-126">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="2a820-127">Testare l'installazione di Ruby `ruby -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-127">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-128">Testare l'installazione di Gem `gem -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-128">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-129">Eseguire il comando `gem install pg` per compilare il modulo PostgreSQL per Ruby usando Gem.</span><span class="sxs-lookup"><span data-stu-id="2a820-129">Build the PostgreSQL module for Ruby using Gem by running the command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2a820-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2a820-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="2a820-131">Installare Ruby eseguendo il comando `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="2a820-131">Install Ruby by running the command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="2a820-132">Per altre opzioni di installazione, vedere la [documentazione sull'installazione](https://www.ruby-lang.org/en/documentation/installation/) di Ruby.</span><span class="sxs-lookup"><span data-stu-id="2a820-132">For more installation options, see the Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="2a820-133">Testare l'installazione di Ruby `ruby -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-133">Test the Ruby installation `ruby -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-134">Installare gli aggiornamenti più recenti per Gem eseguendo il comando `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="2a820-134">Install the latest updates for Gem by running the command `sudo gem update --system`.</span></span>
- <span data-ttu-id="2a820-135">Testare l'installazione di Gem `gem -v` per visualizzare la versione installata.</span><span class="sxs-lookup"><span data-stu-id="2a820-135">Test the Gem installation `gem -v` to see the version installed.</span></span>
- <span data-ttu-id="2a820-136">Installare gcc, make e altri strumenti di compilazione eseguendo il comando `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="2a820-136">Install the gcc, make, and other build tools by running the command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="2a820-137">Installare le librerie PostgreSQL eseguendo il comando `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="2a820-137">Install the PostgreSQL libraries by running the command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="2a820-138">Eseguire il comando `sudo gem install pg` per compilare il modulo pg di Ruby usando Gem.</span><span class="sxs-lookup"><span data-stu-id="2a820-138">Build the Ruby pg module using Gem by running the command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="2a820-139">Eseguire il codice Ruby</span><span class="sxs-lookup"><span data-stu-id="2a820-139">Run Ruby code</span></span> 
- <span data-ttu-id="2a820-140">Salvare il codice in un file di testo e salvare il file in una cartella di progetto con estensione file rb, ad esempio `C:\rubypostgres\read.rb` o `/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="2a820-140">Save the code into a text file, and save the file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="2a820-141">Per eseguire il codice, avviare il prompt dei comandi o la shell Bash.</span><span class="sxs-lookup"><span data-stu-id="2a820-141">To run the code, launch the command prompt or bash shell.</span></span> <span data-ttu-id="2a820-142">Sostituire la directory con la cartella del progetto `cd rubypostgres`, quindi digitare il comando `ruby read.rb` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a820-142">Change directory into your project folder `cd rubypostgres`, then type the command `ruby read.rb` to run the application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2a820-143">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="2a820-143">Get connection information</span></span>
<span data-ttu-id="2a820-144">Ottenere le informazioni di connessione necessarie per connettersi al database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-144">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2a820-145">Sono necessari il nome del server completo e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="2a820-145">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2a820-146">Accedere al [Portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2a820-146">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2a820-147">Nel menu a sinistra nel portale di Azure fare clic su **Tutte le risorse** e cercare il server creato, ad esempio **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="2a820-147">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="2a820-148">Fare clic sul nome del server **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="2a820-148">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2a820-149">Selezionare la pagina **Panoramica** del server.</span><span class="sxs-lookup"><span data-stu-id="2a820-149">Select the server's **Overview** page.</span></span> <span data-ttu-id="2a820-150">Annotare il **Nome server** e il **nome di accesso dell'amministratore del server**.</span><span class="sxs-lookup"><span data-stu-id="2a820-150">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2a820-151">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="2a820-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="2a820-152">Se si dimenticano le informazioni di accesso per il server, passare alla pagina **Panoramica** per visualizzare il nome di accesso dell'amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="2a820-152">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name.</span></span> <span data-ttu-id="2a820-153">Se necessario, reimpostare la password.</span><span class="sxs-lookup"><span data-stu-id="2a820-153">If necessary, reset the password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="2a820-154">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="2a820-154">Connect and create a table</span></span>
<span data-ttu-id="2a820-155">Usare il codice seguente per connettersi e creare una tabella usando l'istruzione SQL **CREATE TABLE**, seguita dalle istruzioni SQL **INSERT INTO** per aggiungere righe nella tabella.</span><span class="sxs-lookup"><span data-stu-id="2a820-155">Use the following code to connect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements to add rows into the table.</span></span>

<span data-ttu-id="2a820-156">Il codice usa un oggetto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) con il costruttore [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) per la connessione a Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-156">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2a820-157">Chiama quindi il metodo [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) per eseguire i comandi DROP, CREATE TABLE e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="2a820-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="2a820-158">Il codice cerca gli errori usando la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="2a820-158">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2a820-159">Chiama infine il metodo [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) per chiudere la connessione prima di terminare.</span><span class="sxs-lookup"><span data-stu-id="2a820-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="2a820-160">Sostituire le stringhe `host`, `database`, `user` e `password` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2a820-160">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database'

    # Drop previous table of same name if one exists
    connection.exec('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    connection.exec('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    connection.exec("INSERT INTO inventory VALUES(1, 'banana', 150)")
    connection.exec("INSERT INTO inventory VALUES(2, 'orange', 154)")
    connection.exec("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="read-data"></a><span data-ttu-id="2a820-161">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="2a820-161">Read data</span></span>
<span data-ttu-id="2a820-162">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="2a820-162">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2a820-163">Il codice usa un oggetto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) con il costruttore [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) per la connessione a Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-163">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2a820-164">Chiama quindi il metodo [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) per eseguire il comando SELECT, mantenendo i risultati in un set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2a820-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the SELECT command, keeping the results in a result set.</span></span> <span data-ttu-id="2a820-165">Viene eseguita l'iterazione della raccolta di set di risultati usando il ciclo `resultSet.each do`, mantenendo i valori della riga corrente nella variabile `row`.</span><span class="sxs-lookup"><span data-stu-id="2a820-165">The result set collection is iterated over using the `resultSet.each do` loop, keeping the current row values in the `row` variable.</span></span> <span data-ttu-id="2a820-166">Il codice cerca gli errori usando la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="2a820-166">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2a820-167">Chiama infine il metodo [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) per chiudere la connessione prima di terminare.</span><span class="sxs-lookup"><span data-stu-id="2a820-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="2a820-168">Sostituire le stringhe `host`, `database`, `user` e `password` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2a820-168">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :database => dbname, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    resultSet = connection.exec('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="update-data"></a><span data-ttu-id="2a820-169">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="2a820-169">Update data</span></span>
<span data-ttu-id="2a820-170">Usare il codice seguente per connettersi e aggiornare i dati usando un'istruzione SQL **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="2a820-170">Use the following code to connect and update the data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="2a820-171">Il codice usa un oggetto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) con il costruttore [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) per la connessione a Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-171">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2a820-172">Chiama quindi il metodo [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) per eseguire il comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="2a820-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="2a820-173">Il codice cerca gli errori usando la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="2a820-173">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2a820-174">Chiama infine il metodo [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) per chiudere la connessione prima di terminare.</span><span class="sxs-lookup"><span data-stu-id="2a820-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="2a820-175">Sostituire le stringhe `host`, `database`, `user` e `password` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2a820-175">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="2a820-176">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="2a820-176">Delete data</span></span>
<span data-ttu-id="2a820-177">Usare il codice seguente per connettersi e leggere i dati usando un'istruzione SQL **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="2a820-177">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2a820-178">Il codice usa un oggetto [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) con il costruttore [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) per la connessione a Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2a820-178">The code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) to connect to Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2a820-179">Chiama quindi il metodo [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) per eseguire il comando UPDATE.</span><span class="sxs-lookup"><span data-stu-id="2a820-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) to run the UPDATE command.</span></span> <span data-ttu-id="2a820-180">Il codice cerca gli errori usando la classe [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error).</span><span class="sxs-lookup"><span data-stu-id="2a820-180">The code checks for errors using the [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2a820-181">Chiama infine il metodo [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) per chiudere la connessione prima di terminare.</span><span class="sxs-lookup"><span data-stu-id="2a820-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) to close the connection before terminating.</span></span>

<span data-ttu-id="2a820-182">Sostituire le stringhe `host`, `database`, `user` e `password` con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2a820-182">Replace the `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

```ruby
require 'pg'

begin
    # Initialize connection variables.
    host = String('mypgserver-20170401.postgres.database.azure.com')
    database = String('postgres')
    user = String('mylogin@mypgserver-20170401')
    password = String('<server_admin_password>')

    # Initialize connection object.
    connection = PG::Connection.new(:host => host, :user => user, :dbname => database, :port => '5432', :password => password)
    puts 'Successfully created connection to database.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="2a820-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a820-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2a820-184">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="2a820-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
