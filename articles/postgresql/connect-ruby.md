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
# <a name="azure-database-for-postgresql-use-ruby-tooconnect-and-query-data"></a>Il Database di Azure per PostgreSQL: dati di utilizzo Ruby tooconnect e query
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL un [Ruby](https://www.ruby-lang.org) dell'applicazione. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite Ruby, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Creare un database: portale](quickstart-create-server-database-portal.md)
- [Creare un database: interfaccia della riga di comando di Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-ruby"></a>Installare Ruby
Installare Ruby nel computer. 

### <a name="windows"></a>Windows
- Download e installazione hello versione [Ruby](http://rubyinstaller.org/downloads/).
- In hello schermata del programma di installazione MSI hello fine, hello casella contenente "Esegui 'Installa ridk' tooinstall MSYS2 e sviluppo toolchain." Quindi fare clic su **fine** programma di installazione toolaunch hello successivo.
- Consente di avviare il programma di installazione di Hello RubyInstaller2 per Windows. Tipo di aggiornamento dell'archivio hello MSYS2 tooinstall 2. Dopo che viene completata e restituisce toohello richiesta di installazione, chiudere la finestra di comando hello.
- Avvia un nuovo prompt dei comandi (cmd) dal menu di avvio hello.
- Hello test installazione Ruby `ruby -v` versione hello toosee installata.
- Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.
- Compilare il modulo di PostgreSQL hello per Ruby utilizzando indicatore eseguendo il comando hello `gem install pg`.

### <a name="macos"></a>MacOS
- Installare Homebrew eseguendo il comando hello Ruby `brew install ruby`. Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/#homebrew)
- Hello test installazione Ruby `ruby -v` versione hello toosee installata.
- Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.
- Compilare il modulo di PostgreSQL hello per Ruby utilizzando indicatore eseguendo il comando hello `gem install pg`.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Installare Ruby eseguendo il comando di hello `sudo apt-get install ruby-full`. Per altre opzioni di installazione, vedere hello Ruby [nella documentazione di installazione](https://www.ruby-lang.org/en/documentation/installation/).
- Hello test installazione Ruby `ruby -v` versione hello toosee installata.
- Installare gli aggiornamenti più recenti di hello per indicatore eseguendo il comando hello `sudo gem update --system`.
- Testare l'installazione dell'indicatore hello `gem -v` versione hello toosee installata.
- Installare gcc hello, verificare e altri strumenti di compilazione tramite il comando hello `sudo apt-get install build-essential`.
- Installare le librerie PostgreSQL hello eseguendo il comando di hello `sudo apt-get install libpq-dev`.
- Compilare il modulo pg Ruby hello utilizzando indicatore eseguendo il comando hello `sudo gem install pg`.

## <a name="run-ruby-code"></a>Eseguire il codice Ruby 
- Salvare il codice hello in un file di testo e salvare il file hello in una cartella di progetto con RB estensione di file, ad esempio `C:\rubypostgres\read.rb` o`/home/username/rubypostgres/read.rb`
- codice hello toorun, avviare prompt dei comandi di hello o della shell bash. Passare alla directory nella cartella del progetto `cd rubypostgres`, quindi digitare il comando hello `ruby read.rb` toorun un'applicazione hello.

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.
3. Fare clic sul nome di server hello **mypgserver 20170401**.
4. Server di selezionare hello **Panoramica** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-ruby/1-connection-string.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** nome account di accesso amministratore Server hello tooview della pagina. Se necessario, hello reimpostazione della password.

## <a name="connect-and-create-a-table"></a>Connettersi e creare una tabella
Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.

codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) comandi di menu, CREATE TABLE e INSERT INTO hello toorun. Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati. 
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

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando SELECT, mantenendo i risultati di hello in un set di risultati. Hello raccolta di set di risultati viene eseguita un'iterazione hello `resultSet.each do` ciclo, mantenendo i valori correnti della riga hello in hello `row` variabile. Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati. 

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

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.

codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando di aggiornamento. Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati. 

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


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

codice Hello viene utilizzato un [PG::Connection](http://www.rubydoc.info/gems/pg/PG/Connection) oggetto con un costruttore [New ()](http://www.rubydoc.info/gems/pg/PG%2FConnection:initialize) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [Exec ()](http://www.rubydoc.info/gems/pg/PG/Connection#exec-instance_method) toorun hello comando di aggiornamento. Hello codice controlla gli errori utilizzando hello [PG::Error](http://www.rubydoc.info/gems/pg/PG/Error) classe. Viene quindi chiamato metodo [Close ()](http://www.rubydoc.info/gems/pg/PG/Connection#lo_close-instance_method) connessione hello tooclose prima della chiusura.

Sostituire hello `host`, `database`, `user`, e `password` stringhe con valori personalizzati. 

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

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
