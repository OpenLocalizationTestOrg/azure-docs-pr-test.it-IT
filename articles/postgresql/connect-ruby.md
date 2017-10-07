---
title: aaaConnect tooAzure Database PostgreSQL utilizzando Ruby | Documenti Microsoft
description: "Questa Guida rapida viene fornito un esempio di codice Ruby è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
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
ms.openlocfilehash: 7a0c8c92023452b40ca19d76fa659744f3e9a236
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="2f8f2-103">Il Database di Azure per PostgreSQL: dati di utilizzo Ruby tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="2f8f2-103">Azure Database for PostgreSQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="2f8f2-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL un [Ruby](https://www.ruby-lang.org) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [Ruby](https://www.ruby-lang.org) application.</span></span> <span data-ttu-id="2f8f2-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="2f8f2-106">In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Ruby, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f8f2-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f8f2-107">Prerequisites</span></span>
<span data-ttu-id="2f8f2-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="2f8f2-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="2f8f2-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="2f8f2-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="2f8f2-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="2f8f2-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a><span data-ttu-id="2f8f2-111">Installare Ruby</span><span class="sxs-lookup"><span data-stu-id="2f8f2-111">Install Ruby</span></span>
<span data-ttu-id="2f8f2-112">Installare Ruby nel computer.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-112">Install Ruby on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="2f8f2-113">Windows</span><span class="sxs-lookup"><span data-stu-id="2f8f2-113">Windows</span></span>
- <span data-ttu-id="2f8f2-114">Download e installazione hello versione [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2f8f2-114">Download and Install hello latest version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
- <span data-ttu-id="2f8f2-115">In hello schermata del programma di installazione MSI hello fine, hello casella contenente "Esegui 'Installa ridk' tooinstall MSYS2 e sviluppo toolchain."</span><span class="sxs-lookup"><span data-stu-id="2f8f2-115">On hello finish screen of hello MSI installer, check hello box that says "Run 'ridk install' tooinstall MSYS2 and development toolchain."</span></span> <span data-ttu-id="2f8f2-116">Quindi fare clic su **fine** programma di installazione toolaunch hello successivo.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-116">Then click **Finish** toolaunch hello next installer.</span></span>
- <span data-ttu-id="2f8f2-117">Consente di avviare il programma di installazione di Hello RubyInstaller2 per Windows.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-117">hello RubyInstaller2 for Windows installer launches.</span></span> <span data-ttu-id="2f8f2-118">Tipo di aggiornamento dell'archivio hello MSYS2 tooinstall 2.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-118">Type 2 tooinstall hello MSYS2 repository update.</span></span> <span data-ttu-id="2f8f2-119">Dopo che viene completata e restituisce toohello richiesta di installazione, chiudere la finestra di comando hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-119">After it finishes and returns toohello installation prompt, close hello command window.</span></span>
- <span data-ttu-id="2f8f2-120">Avvia un nuovo prompt dei comandi (cmd) dal menu di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-120">Launch a new command prompt (cmd) from hello Start menu.</span></span>
- <span data-ttu-id="2f8f2-121">Hello test installazione Ruby `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-121">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-122">Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-122">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-123">Compilare il modulo di PostgreSQL hello per Ruby utilizzando indicatore eseguendo il comando hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-123">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="macos"></a><span data-ttu-id="2f8f2-124">MacOS</span><span class="sxs-lookup"><span data-stu-id="2f8f2-124">MacOS</span></span>
- <span data-ttu-id="2f8f2-125">Installare Homebrew eseguendo il comando hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-125">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="2f8f2-126">Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span><span class="sxs-lookup"><span data-stu-id="2f8f2-126">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew)</span></span>
- <span data-ttu-id="2f8f2-127">Hello test installazione Ruby `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-127">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-128">Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-128">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-129">Compilare il modulo di PostgreSQL hello per Ruby utilizzando indicatore eseguendo il comando hello `gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-129">Build hello PostgreSQL module for Ruby using Gem by running hello command `gem install pg`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="2f8f2-130">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="2f8f2-130">Linux (Ubuntu)</span></span>
- <span data-ttu-id="2f8f2-131">Installare Ruby eseguendo il comando di hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-131">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="2f8f2-132">Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="2f8f2-132">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
- <span data-ttu-id="2f8f2-133">Hello test installazione Ruby `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-133">Test hello Ruby installation `ruby -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-134">Installare gli aggiornamenti più recenti di hello per indicatore eseguendo il comando hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-134">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
- <span data-ttu-id="2f8f2-135">Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-135">Test hello Gem installation `gem -v` toosee hello version installed.</span></span>
- <span data-ttu-id="2f8f2-136">Installare gcc hello, verificare e altri strumenti di compilazione tramite il comando hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-136">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
- <span data-ttu-id="2f8f2-137">Installare le librerie PostgreSQL hello eseguendo il comando di hello `sudo apt-get install libpq-dev`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-137">Install hello PostgreSQL libraries by running hello command `sudo apt-get install libpq-dev`.</span></span>
- <span data-ttu-id="2f8f2-138">Compilare il modulo pg Ruby hello utilizzando indicatore eseguendo il comando hello `sudo gem install pg`.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-138">Build hello Ruby pg module using Gem by running hello command `sudo gem install pg`.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="2f8f2-139">Eseguire il codice Ruby</span><span class="sxs-lookup"><span data-stu-id="2f8f2-139">Run Ruby code</span></span> 
- <span data-ttu-id="2f8f2-140">Salvare il codice hello in un file di testo e salvare il file hello in una cartella di progetto con RB estensione di file, ad esempio `C:\rubypostgres\read.rb` o`/home/username/rubypostgres/read.rb`</span><span class="sxs-lookup"><span data-stu-id="2f8f2-140">Save hello code into a text file, and save hello file into a project folder with file extension .rb, such as `C:\rubypostgres\read.rb` or `/home/username/rubypostgres/read.rb`</span></span>
- <span data-ttu-id="2f8f2-141">codice hello toorun, avviare prompt dei comandi di hello o della shell bash.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-141">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="2f8f2-142">Passare alla directory nella cartella del progetto `cd rubypostgres`, quindi digitare il comando hello `ruby read.rb` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-142">Change directory into your project folder `cd rubypostgres`, then type hello command `ruby read.rb` toorun hello application.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="2f8f2-143">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="2f8f2-143">Get connection information</span></span>
<span data-ttu-id="2f8f2-144">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-144">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="2f8f2-145">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-145">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="2f8f2-146">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2f8f2-146">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2f8f2-147">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-147">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="2f8f2-148">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-148">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="2f8f2-149">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-149">Select hello server's **Overview** page.</span></span> <span data-ttu-id="2f8f2-150">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-150">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="2f8f2-151">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-ruby/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="2f8f2-151">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-ruby/1-connection-string.png)</span></span>
5. <span data-ttu-id="2f8f2-152">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** nome account di accesso amministratore Server hello tooview della pagina.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-152">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name.</span></span> <span data-ttu-id="2f8f2-153">Se necessario, hello reimpostazione della password.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-153">If necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="2f8f2-154">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="2f8f2-154">Connect and create a table</span></span>
<span data-ttu-id="2f8f2-155">Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-155">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="2f8f2-156">codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-156">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="2f8f2-157">Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) comandi di menu, CREATE TABLE e INSERT INTO hello toorun.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-157">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="2f8f2-158">Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-158">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2f8f2-159">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-159">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f8f2-160">Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-160">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 
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
    puts 'Successfully created connection toodatabase'

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

## <a name="read-data"></a><span data-ttu-id="2f8f2-161">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="2f8f2-161">Read data</span></span>
<span data-ttu-id="2f8f2-162">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-162">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="2f8f2-163">codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-163">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="2f8f2-164">Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando SELECT, mantenendo i risultati di hello in un set di risultati.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-164">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello SELECT command, keeping hello results in a result set.</span></span> <span data-ttu-id="2f8f2-165">Hello raccolta di set di risultati viene eseguita un'iterazione hello `resultSet.each do` ciclo, mantenendo i valori correnti della riga hello in hello `row` variabile.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-165">hello result set collection is iterated over using hello `resultSet.each do` loop, keeping hello current row values in hello `row` variable.</span></span> <span data-ttu-id="2f8f2-166">Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-166">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2f8f2-167">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-167">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f8f2-168">Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-168">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

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

## <a name="update-data"></a><span data-ttu-id="2f8f2-169">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="2f8f2-169">Update data</span></span>
<span data-ttu-id="2f8f2-170">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-170">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="2f8f2-171">codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-171">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="2f8f2-172">Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-172">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="2f8f2-173">Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-173">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2f8f2-174">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-174">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f8f2-175">Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-175">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
    puts 'Updated 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```


## <a name="delete-data"></a><span data-ttu-id="2f8f2-176">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="2f8f2-176">Delete data</span></span>
<span data-ttu-id="2f8f2-177">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-177">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="2f8f2-178">codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-178">hello code uses a  [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) object with constructor [new()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="2f8f2-179">Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-179">Then it calls method [exec()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello UPDATE command.</span></span> <span data-ttu-id="2f8f2-180">Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-180">hello code checks for errors using hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) class.</span></span> <span data-ttu-id="2f8f2-181">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-181">Then it calls method [close()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="2f8f2-182">Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="2f8f2-182">Replace hello `host`, `database`, `user`, and `password` strings with your own values.</span></span> 

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
    puts 'Successfully created connection toodatabase.'

    # Modify some data in table.
    connection.exec('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row of data.'

rescue PG::Error => e
    puts e.message 
    
ensure
    connection.close if connection
end
```

## <a name="next-steps"></a><span data-ttu-id="2f8f2-183">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f8f2-183">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="2f8f2-184">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="2f8f2-184">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
