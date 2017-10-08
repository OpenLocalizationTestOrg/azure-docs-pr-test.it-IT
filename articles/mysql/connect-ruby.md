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
# <a name="azure-database-for-mysql-use-ruby-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati di utilizzo Ruby tooconnect e query
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL un [Ruby](https://www.ruby-lang.org) hello e applicazione [mysql2](https://rubygems.org/gems/mysql2) indicatore da piattaforme di Windows, Ubuntu Linux e Mac. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Ruby, ma che sono tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Create an Azure Database for MySQL server using Azure CLI](./quickstart-create-mysql-server-database-using-azure-cli.md) (Creare un database di Azure per il server MySQL usando l'interfaccia della riga di comando di Azure)

## <a name="install-ruby"></a>Installare Ruby
Installare Ruby, indicatore e la libreria MySQL2 hello sul proprio computer. 

### <a name="windows"></a>Windows
1. Scaricare e installare la versione di hello 2.3 di [Ruby](http://rubyinstaller.org/downloads/).
2. Avvia un nuovo prompt dei comandi (cmd) dal menu di avvio hello.
3. Spostarsi nella directory in hello Ruby directory per la versione 2.3. `cd c:\Ruby23-x64\bin`
4. Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.
5. Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.
6. Compilare il modulo di hello Mysql2 per Ruby utilizzando indicatore eseguendo il comando hello `gem install mysql2`.

### <a name="macos"></a>MacOS
1. Installare Homebrew eseguendo il comando hello Ruby `brew install ruby`. Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/#homebrew).
2. Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.
3. Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.
4. Compilare il modulo di hello Mysql2 per Ruby utilizzando indicatore eseguendo il comando hello `gem install mysql2`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
1. Installare Ruby eseguendo il comando di hello `sudo apt-get install ruby-full`. Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/).
2. Hello test Ruby installazione eseguendo il comando hello `ruby -v` versione hello toosee installata.
3. Installare gli aggiornamenti più recenti di hello per indicatore eseguendo il comando hello `sudo gem update --system`.
4. Testare l'installazione dell'indicatore hello eseguendo il comando hello `gem -v` versione hello toosee installata.
5. Installare gcc hello, verificare e altri strumenti di compilazione tramite il comando hello `sudo apt-get install build-essential`.
6. Installare le librerie per sviluppatori di hello MySQL client eseguendo il comando di hello `sudo apt-get install libmysqlclient-dev`.
7. Compilare il modulo di mysql2 hello per Ruby utilizzando indicatore eseguendo il comando hello `sudo gem install mysql2`.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello avere piegato, ad esempio **myserver4demo**.
3. Fare clic sul nome di server hello **myserver4demo**.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per MySQL - Accesso dell'amministratore del server](./media/connect-ruby/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="run-ruby-code"></a>Eseguire il codice Ruby 
1. Incollare hello Ruby codice dalle sezioni hello seguito nel file di testo e salvare il file hello in una cartella di progetto con RB estensione di file, ad esempio `C:\rubymysql\createtable.rb` o `/home/username/rubymysql/createtable.rb`.
2. codice hello toorun, avviare prompt dei comandi di hello o della shell bash. Passare alla cartella del progetto `cd rubymysql`
3. Quindi digitare il comando hello ruby seguito dal nome di file hello, ad esempio `ruby createtable.rb` toorun un'applicazione hello.
4. Nel sistema operativo Windows hello, se un'applicazione hello ruby non è incluso nella variabile di ambiente path, potrebbe essere necessario toouse hello percorso completo toolaunch hello nodo dell'applicazione, ad esempio`"c:\Ruby23-x64\bin\ruby.exe" createtable.rb`

## <a name="connect-and-create-a-table"></a>Connettersi e creare una tabella
Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.

codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL. Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) più volte toorun hello, CREATE TABLE, comandi DROP e INSERT INTO. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati. 
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

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL. Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun comandi SELECT di hello. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati. 

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

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.

codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL. Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) toorun i comandi di aggiornamento hello. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati. 

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


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

codice Hello viene utilizzato un [mysql2::client](http://www.rubydoc.info/gems/mysql2/0.4.8) classe .new() metodo tooconnect tooAzure Database per MySQL. Viene quindi chiamato metodo [query ()](http://www.rubydoc.info/gems/mysql2/0.4.8#Usage) comandi DELETE di hello toorun. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/mysql2/0.4.8/Mysql2/Client#close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `username`, e `password` stringhe con valori personalizzati. 

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

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./concepts-migrate-import-export.md)
