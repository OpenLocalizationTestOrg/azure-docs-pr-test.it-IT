---
title: aaaConnect tooAzure Database PostgreSQL tramite PHP | Documenti Microsoft
description: "Questa Guida rapida fornisce un esempio di codice PHP, è possibile utilizzare tooconnect e cercare i dati dal Database di Azure PostgreSQL."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: php
ms.topic: quickstart
ms.date: 06/29/2017
ms.openlocfilehash: 008505e837e37cb8c7fea3fc164b3446c3580e46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a>Il Database di Azure per PostgreSQL: dati di utilizzo PHP tooconnect e query
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL un [PHP](http://php.net/manual/intro-whatis.php) dell'applicazione. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite PHP, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Creare un database: portale](quickstart-create-server-database-portal.md)
- [Creare un database: interfaccia della riga di comando di Azure](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a>Installare PHP
Installare PHP nel server o creare un'[app Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) di Azure che includa PHP.

### <a name="windows"></a>Windows
- Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://windows.php.net/download#php-7.1)
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.windows.php) per un'ulteriore configurazione
- codice Hello utilizza hello **pgsql** classe (ext/php_pgsql.dll) che è incluso nell'installazione di PHP hello. 
- Hello abilitato **pgsql** estensione modificando i file di configurazione PHP hello, in genere si trova in `C:\Program Files\PHP\v7.1\php.ini`. file di configurazione Hello deve contenere una riga con testo hello `extension=php_pgsql.so`. Se non è visualizzata, aggiungere testo hello e salvare file hello. Se è presente, il testo hello commentato ma con un prefisso di un punto e virgola, rimuovere il commento testo hello rimuovendo punto e virgola hello.

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://php.net/downloads.php) 
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.unix.php) per un'ulteriore configurazione
- codice Hello utilizza hello **pgsql** classe (php_pgsql.so). Installarla eseguendo `sudo apt-get install php-pgsql`.
- Hello abilitato **pgsql** estensione modificando hello `/etc/php/7.0/mods-available/pgsql.ini` file di configurazione. file di configurazione Hello deve contenere una riga con testo hello `extension=php_pgsql.so`. Se non è visualizzata, aggiungere testo hello e salvare file hello. Se è presente, il testo hello commentato ma con un prefisso di un punto e virgola, rimuovere il commento testo hello rimuovendo punto e virgola hello.

### <a name="macos"></a>MacOS
- Scaricare [PHP versione 7.1.4](http://php.net/downloads.php)
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.macosx.php) per un'ulteriore configurazione

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.
3. Fare clic sul nome di server hello **mypgserver 20170401**.
4. Server di selezionare hello **Panoramica** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-php/1-connection-string.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="connect-and-create-a-table"></a>Connettersi e creare una tabella
Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.

il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun più volte, alcuni comandi e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se ogni volta che si è verificato un errore. Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.

Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password") 
        or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");
    print "Successfully created connection toodatabase.<br/>";

    // Drop previous table of same name if one exists.
    $query = "DROP TABLE IF EXISTS inventory;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished dropping table (if existed).<br/>";

    // Create table.
    $query = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    print "Finished creating table.<br/>";

    // Insert some data into table.
    $name = '\'banana\'';
    $quantity = 150;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($1, $2);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'orange\'';
    $quantity = 154;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");

    $name = '\'apple\'';
    $quantity = 100;
    $query = "INSERT INTO inventory (name, quantity) VALUES ($name, $quantity);";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error()). "<br/>";

    print "Inserted 3 rows of data.<br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL. 

 il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello comando SELECT, mantenendo i risultati di hello in un set di risultati, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore.  set di risultati hello tooread, metodo [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) viene chiamato in un ciclo, una volta per ogni riga e la riga hello i dati vengono recuperati in una matrice `$row`, con il valore di dati per ogni colonna in ogni posizione della matrice.  set di risultati hello toofree, metodo [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) viene chiamato. Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.

Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";
    
    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). "<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Perform some SQL queries over hello connection.
    $query = "SELECT * from inventory";
    $result_set = pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). "<br/>");
    while ($row = pg_fetch_row($result_set))
    {
        print "Data row = ($row[0], $row[1], $row[2]). <br/>";
    }

    // Free result_set
    pg_free_result($result_set);

    // Closing connection
    pg_close($connection);
?>
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.

il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL. Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore. Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.

Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
                or die("Failed toocreate connection toodatabase: ". pg_last_error(). ".<br/>");

    print "Successfully created connection toodatabase. <br/>";

    // Modify some data in table.
    $new_quantity = 200;
    $name = '\'banana\'';
    $query = "UPDATE inventory SET quantity = $new_quantity WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ".<br/>");
    print "Updated 1 row of data. </br>";

    // Closing connection
    pg_close($connection);
?>
```


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

 il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect troppo Azure Database PostgreSQL. Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore. Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.

Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati. 

```php
<?php
    // Initialize connection variables.
    $host = "mypgserver-20170401.postgres.database.azure.com";
    $database = "mypgsqldb";
    $user = "mylogin@mypgserver-20170401";
    $password = "<server_admin_password>";

    // Initialize connection object.
    $connection = pg_connect("host=$host dbname=$database user=$user password=$password")
            or die("Failed toocreate connection toodatabase: ". pg_last_error(). ". </br>");

    print "Successfully created connection toodatabase. <br/>";

    // Delete some data from table.
    $name = '\'orange\'';
    $query = "DELETE FROM inventory WHERE name = $name;";
    pg_query($connection, $query) 
        or die("Encountered an error when executing given sql statement: ". pg_last_error(). ". <br/>");
    print "Deleted 1 row of data. <br/>";

    // Closing connection
    pg_close($connection);
?>
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Eseguire la migrazione del database usando le funzionalità di esportazione e importazione](./howto-migrate-using-export-and-import.md)
