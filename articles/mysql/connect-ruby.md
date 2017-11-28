---
title: La connessione tooAzure Database MySQL mediante Ruby | Documenti Microsoft
description: "Questa Guida introduttiva offre numerosi esempi di codice Ruby, è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: mysql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.devlang: ruby
ms.topic: hero-article
ms.date: 07/13/2017
ms.openlocfilehash: ff0880dcc24e96f467c9092bc663ce3dc4c2637a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a><span data-ttu-id="8f22d-103">Il Database di Azure per MySQL: dati di utilizzo Ruby tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="8f22d-103">Azure Database for MySQL: Use Ruby tooconnect and query data</span></span>
<span data-ttu-id="8f22d-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL un [Ruby](https://www.ruby-lang.org) hello e applicazione [mysql2](https://rubygems.org/gems/mysql2) indicatore da piattaforme di Windows, Ubuntu Linux e Mac.</span><span class="sxs-lookup"><span data-stu-id="8f22d-104">This quickstart demonstrates how tooconnect tooan Azure Database for MySQL using a [Ruby](https://www.ruby-lang.org) application and hello [mysql2](https://rubygems.org/gems/mysql2) gem from Windows, Ubuntu Linux, and Mac platforms.</span></span> <span data-ttu-id="8f22d-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="8f22d-106">In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Ruby, ma che sono tooworking nuovo con il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-106">This article assumes you are familiar with development using Ruby, but that you are new tooworking with Azure Database for MySQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f22d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8f22d-107">Prerequisites</span></span>
<span data-ttu-id="8f22d-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="8f22d-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- <span data-ttu-id="8f22d-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)</span><span class="sxs-lookup"><span data-stu-id="8f22d-109">[Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="8f22d-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure)</span><span class="sxs-lookup"><span data-stu-id="8f22d-110">[Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

## <a name="install-ruby"></a><span data-ttu-id="8f22d-111">Installare Ruby</span><span class="sxs-lookup"><span data-stu-id="8f22d-111">Install Ruby</span></span>
<span data-ttu-id="8f22d-112">Installare Ruby, indicatore e la libreria MySQL2 hello sul proprio computer.</span><span class="sxs-lookup"><span data-stu-id="8f22d-112">Install Ruby, Gem, and hello MySQL2 library on your own machine.</span></span> 

### <a name="windows"></a><span data-ttu-id="8f22d-113">Windows</span><span class="sxs-lookup"><span data-stu-id="8f22d-113">Windows</span></span>
1. <span data-ttu-id="8f22d-114">Scaricare e installare la versione di hello 2.3 di [Ruby](http://rubyinstaller.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8f22d-114">Download and Install hello 2.3 version of [Ruby](http://rubyinstaller.org/downloads/).</span></span>
2. <span data-ttu-id="8f22d-115">Avvia un nuovo prompt dei comandi (cmd) dal menu di avvio hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-115">Launch a new command prompt (cmd) from hello Start menu.</span></span>
3. <span data-ttu-id="8f22d-116">Spostarsi nella directory in hello Ruby directory per la versione 2.3.</span><span class="sxs-lookup"><span data-stu-id="8f22d-116">Change directory into hello Ruby directory for version 2.3.</span></span> `cd c:\Ruby23-x64\bin`
4. <span data-ttu-id="8f22d-117">Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-117">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="8f22d-118">Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-118">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
6. <span data-ttu-id="8f22d-119">Compilare il modulo di hello Mysql2 per Ruby utilizzando indicatore eseguendo il comando hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-119">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="macos"></a><span data-ttu-id="8f22d-120">MacOS</span><span class="sxs-lookup"><span data-stu-id="8f22d-120">MacOS</span></span>
1. <span data-ttu-id="8f22d-121">Installare Homebrew eseguendo il comando hello Ruby `brew install ruby`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-121">Install Ruby using Homebrew by running hello command `brew install ruby`.</span></span> <span data-ttu-id="8f22d-122">Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span><span class="sxs-lookup"><span data-stu-id="8f22d-122">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/#homebrew).</span></span>
2. <span data-ttu-id="8f22d-123">Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-123">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="8f22d-124">Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-124">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
4. <span data-ttu-id="8f22d-125">Compilare il modulo di hello Mysql2 per Ruby utilizzando indicatore eseguendo il comando hello `gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-125">Build hello Mysql2 module for Ruby using Gem by running hello command `gem install mysql2`.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="8f22d-126">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="8f22d-126">Linux (Ubuntu)</span></span>
1. <span data-ttu-id="8f22d-127">Installare Ruby eseguendo il comando di hello `sudo apt-get install ruby-full`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-127">Install Ruby by running hello command `sudo apt-get install ruby-full`.</span></span> <span data-ttu-id="8f22d-128">Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/).</span><span class="sxs-lookup"><span data-stu-id="8f22d-128">For more installation options, see hello Ruby [installation documentation](https://www.ruby-lang.org/en/documentation/installation/).</span></span>
2. <span data-ttu-id="8f22d-129">Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-129">Test hello Ruby installation by running hello command `ruby -v` toosee hello version installed.</span></span>
3. <span data-ttu-id="8f22d-130">Installare gli aggiornamenti più recenti di hello per indicatore eseguendo il comando hello `sudo gem update --system`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-130">Install hello latest updates for Gem by running hello command `sudo gem update --system`.</span></span>
4. <span data-ttu-id="8f22d-131">Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.</span><span class="sxs-lookup"><span data-stu-id="8f22d-131">Test hello Gem installation by running hello command `gem -v` toosee hello version installed.</span></span>
5. <span data-ttu-id="8f22d-132">Installare gcc hello, verificare e altri strumenti di compilazione tramite il comando hello `sudo apt-get install build-essential`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-132">Install hello gcc, make, and other build tools by running hello command `sudo apt-get install build-essential`.</span></span>
6. <span data-ttu-id="8f22d-133">Installare le librerie per sviluppatori di hello MySQL client eseguendo il comando di hello `sudo apt-get install libmysqlclient-dev`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-133">Install hello MySQL client developer libraries by running hello command `sudo apt-get install libmysqlclient-dev`.</span></span>
7. <span data-ttu-id="8f22d-134">Compilare il modulo di mysql2 hello per Ruby utilizzando indicatore eseguendo il comando hello `sudo gem install mysql2`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-134">Build hello mysql2 module for Ruby using Gem by running hello command `sudo gem install mysql2`.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="8f22d-135">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="8f22d-135">Get connection information</span></span>
<span data-ttu-id="8f22d-136">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-136">Get hello connection information needed tooconnect toohello Azure Database for MySQL.</span></span> <span data-ttu-id="8f22d-137">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="8f22d-137">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8f22d-138">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8f22d-138">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8f22d-139">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello avere piegato, ad esempio **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="8f22d-139">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have creased, such as **myserver4demo**.</span></span>
3. <span data-ttu-id="8f22d-140">Fare clic sul nome di server hello **myserver4demo**.</span><span class="sxs-lookup"><span data-stu-id="8f22d-140">Click hello server name **myserver4demo**.</span></span>
4. <span data-ttu-id="8f22d-141">Server di selezionare hello **proprietà** pagina.</span><span class="sxs-lookup"><span data-stu-id="8f22d-141">Select hello server's **Properties** page.</span></span> <span data-ttu-id="8f22d-142">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="8f22d-142">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="8f22d-143">![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-ruby/1_server-properties-name-login.png)</span><span class="sxs-lookup"><span data-stu-id="8f22d-143">![Azure Database for MySQL - Server Admin Login](./media/connect-ruby/1_server-properties-name-login.png)</span></span>
5. <span data-ttu-id="8f22d-144">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-144">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="run-ruby-code"></a><span data-ttu-id="8f22d-145">Eseguire il codice Ruby</span><span class="sxs-lookup"><span data-stu-id="8f22d-145">Run Ruby code</span></span> 
1. <span data-ttu-id="8f22d-146">Incollare hello Ruby codice dalle sezioni hello seguito nel file di testo e salvare il file hello in una cartella di progetto con RB estensione di file, ad esempio `C:\rubymysql\createtable.rb` o `/home/username/rubymysql/createtable.rb`.</span><span class="sxs-lookup"><span data-stu-id="8f22d-146">Paste hello Ruby code from hello sections below into text files, and save hello files into a project folder with file extension .rb, such as `C:\rubymysql\createtable.rb` or `/home/username/rubymysql/createtable.rb`.</span></span>
2. <span data-ttu-id="8f22d-147">codice hello toorun, avviare prompt dei comandi di hello o della shell bash.</span><span class="sxs-lookup"><span data-stu-id="8f22d-147">toorun hello code, launch hello command prompt or bash shell.</span></span> <span data-ttu-id="8f22d-148">Passare alla cartella del progetto `cd rubymysql`</span><span class="sxs-lookup"><span data-stu-id="8f22d-148">Change directory into your project folder `cd rubymysql`</span></span>
3. <span data-ttu-id="8f22d-149">Quindi digitare il comando hello ruby seguito dal nome di file hello, ad esempio `ruby createtable.rb` toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-149">Then type hello ruby command followed by hello file name, such as `ruby createtable.rb` toorun hello application.</span></span>
4. <span data-ttu-id="8f22d-150">Nel sistema operativo Windows hello, se un'applicazione hello ruby non è incluso nella variabile di ambiente path, potrebbe essere necessario toouse hello percorso completo toolaunch hello nodo dell'applicazione, ad esempio`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span><span class="sxs-lookup"><span data-stu-id="8f22d-150">On hello Windows OS, if hello ruby application is not in your path environment variable, you may need toouse hello full path toolaunch hello node application, such as `"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="8f22d-151">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="8f22d-151">Connect and create a table</span></span>
<span data-ttu-id="8f22d-152">Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-152">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="8f22d-153">codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-153">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="8f22d-154">Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) più volte toorun hello, CREATE TABLE, comandi DROP e INSERT INTO.</span><span class="sxs-lookup"><span data-stu-id="8f22d-154">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) several times toorun hello DROP, CREATE TABLE, and INSERT INTO commands.</span></span> <span data-ttu-id="8f22d-155">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="8f22d-155">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="8f22d-156">Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8f22d-156">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 
```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Drop previous table of same name if one exists
    client.query('DROP TABLE IF EXISTS inventory;')
    puts 'Finished dropping table (if existed).'

    # Drop previous table of same name if one exists.
    client.query('CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);')
    puts 'Finished creating table.'

    # Insert some data into table.
    client.query("INSERT INTO inventory VALUES(1, 'banana', 150)")
    client.query("INSERT INTO inventory VALUES(2, 'orange', 154)")
    client.query("INSERT INTO inventory VALUES(3, 'apple', 100)")
    puts 'Inserted 3 rows of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="read-data"></a><span data-ttu-id="8f22d-157">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="8f22d-157">Read data</span></span>
<span data-ttu-id="8f22d-158">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-158">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

<span data-ttu-id="8f22d-159">codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-159">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="8f22d-160">Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandi SELECT di hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-160">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello SELECT commands.</span></span> <span data-ttu-id="8f22d-161">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="8f22d-161">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="8f22d-162">Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8f22d-162">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Read data
    resultSet = client.query('SELECT * from inventory;')
    resultSet.each do |row|
        puts 'Data row = (%s, %s, %s)' % [row['id'], row['name'], row['quantity']]
    end
    puts 'Read ' + resultSet.count.to_s + ' row(s).'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="update-data"></a><span data-ttu-id="8f22d-163">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="8f22d-163">Update data</span></span>
<span data-ttu-id="8f22d-164">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-164">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="8f22d-165">codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-165">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="8f22d-166">Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun i comandi di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="8f22d-166">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello UPDATE commands.</span></span> <span data-ttu-id="8f22d-167">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="8f22d-167">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="8f22d-168">Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8f22d-168">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Update data
   client.query('UPDATE inventory SET quantity = %d WHERE name = %s;' % [200, '\'banana\''])
   puts 'Updated 1 row of data.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```


## <a name="delete-data"></a><span data-ttu-id="8f22d-169">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="8f22d-169">Delete data</span></span>
<span data-ttu-id="8f22d-170">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-170">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

<span data-ttu-id="8f22d-171">codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL.</span><span class="sxs-lookup"><span data-stu-id="8f22d-171">hello code uses a [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) class .new() method tooconnect tooAzure Database for MySQL.</span></span> <span data-ttu-id="8f22d-172">Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandi DELETE di hello toorun.</span><span class="sxs-lookup"><span data-stu-id="8f22d-172">Then it calls method [query()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun hello DELETE commands.</span></span> <span data-ttu-id="8f22d-173">Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.</span><span class="sxs-lookup"><span data-stu-id="8f22d-173">Then it calls method [close()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) tooclose hello connection before terminating.</span></span>

<span data-ttu-id="8f22d-174">Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="8f22d-174">Replace hello `host`, `database`, `username`, and `password` strings with your own values.</span></span> 

```ruby
require 'mysql2'

begin
    # Initialize connection variables.
    host = String('myserver4demo.mysql.database.azure.com')
    database = String('quickstartdb')
    username = String('myadmin@myserver4demo')
    password = String('yourpassword')

    # Initialize connection object.
    client = Mysql2::Client.new(:host => host, :username => username, :database => database, :password => password)
    puts 'Successfully created connection toodatabase.'

    # Delete data
    resultSet = client.query('DELETE FROM inventory WHERE name = %s;' % ['\'orange\''])
    puts 'Deleted 1 row.'

# Error handling
rescue Exception => e
    puts e.message

# Cleanup
ensure
    client.close if client
    puts 'Done.'
end
```

## <a name="next-steps"></a><span data-ttu-id="8f22d-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8f22d-175">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8f22d-176">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="8f22d-176">Migrate your database using Export and Import</span></span>](./concepts-migrate-import-export.md)
