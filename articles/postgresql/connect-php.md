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
# <a name="azure-database-for-postgresql-use-php-tooconnect-and-query-data"></a><span data-ttu-id="09fe8-103">Il Database di Azure per PostgreSQL: dati di utilizzo PHP tooconnect e query</span><span class="sxs-lookup"><span data-stu-id="09fe8-103">Azure Database for PostgreSQL: Use PHP tooconnect and query data</span></span>
<span data-ttu-id="09fe8-104">Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di PostgreSQL un [PHP](http://php.net/manual/intro-whatis.php) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="09fe8-104">This quickstart demonstrates how tooconnect tooan Azure Database for PostgreSQL using a [PHP](http://php.net/manual/intro-whatis.php) application.</span></span> <span data-ttu-id="09fe8-105">Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-105">It shows how toouse SQL statements tooquery, insert, update, and delete data in hello database.</span></span> <span data-ttu-id="09fe8-106">In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite PHP, ma che sono tooworking nuovo con il Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-106">This article assumes you are familiar with development using PHP, but that you are new tooworking with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09fe8-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="09fe8-107">Prerequisites</span></span>
<span data-ttu-id="09fe8-108">Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:</span><span class="sxs-lookup"><span data-stu-id="09fe8-108">This quickstart uses hello resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="09fe8-109">Creare un database: portale</span><span class="sxs-lookup"><span data-stu-id="09fe8-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="09fe8-110">Creare un database: interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="09fe8-110">Create DB - Azure CLI</span></span>](quickstart-create-server-database-azure-cli.md)

## <a name="install-php"></a><span data-ttu-id="09fe8-111">Installare PHP</span><span class="sxs-lookup"><span data-stu-id="09fe8-111">Install PHP</span></span>
<span data-ttu-id="09fe8-112">Installare PHP nel server o creare un'[app Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) di Azure che includa PHP.</span><span class="sxs-lookup"><span data-stu-id="09fe8-112">Install PHP on your own server, or create an Azure [web app](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) that includes PHP.</span></span>

### <a name="windows"></a><span data-ttu-id="09fe8-113">Windows</span><span class="sxs-lookup"><span data-stu-id="09fe8-113">Windows</span></span>
- <span data-ttu-id="09fe8-114">Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://windows.php.net/download#php-7.1)</span><span class="sxs-lookup"><span data-stu-id="09fe8-114">Download [PHP 7.1.4 non-thread safe (x64) version](http://windows.php.net/download#php-7.1)</span></span>
- <span data-ttu-id="09fe8-115">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.windows.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="09fe8-115">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.windows.php) for further configuration</span></span>
- <span data-ttu-id="09fe8-116">codice Hello utilizza hello **pgsql** classe (ext/php_pgsql.dll) che è incluso nell'installazione di PHP hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-116">hello code uses hello **pgsql** class (ext/php_pgsql.dll)  that is included in hello PHP installation.</span></span> 
- <span data-ttu-id="09fe8-117">Hello abilitato **pgsql** estensione modificando i file di configurazione PHP hello, in genere si trova in `C:\Program Files\PHP\v7.1\php.ini`.</span><span class="sxs-lookup"><span data-stu-id="09fe8-117">Enabled hello **pgsql** extension by editing hello php.ini configuration file, typically located at `C:\Program Files\PHP\v7.1\php.ini`.</span></span> <span data-ttu-id="09fe8-118">file di configurazione Hello deve contenere una riga con testo hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="09fe8-118">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="09fe8-119">Se non è visualizzata, aggiungere testo hello e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-119">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="09fe8-120">Se è presente, il testo hello commentato ma con un prefisso di un punto e virgola, rimuovere il commento testo hello rimuovendo punto e virgola hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-120">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="09fe8-121">Linux (Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="09fe8-121">Linux (Ubuntu)</span></span>
- <span data-ttu-id="09fe8-122">Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="09fe8-122">Download [PHP 7.1.4 non-thread safe (x64) version](http://php.net/downloads.php)</span></span> 
- <span data-ttu-id="09fe8-123">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.unix.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="09fe8-123">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.unix.php) for further configuration</span></span>
- <span data-ttu-id="09fe8-124">codice Hello utilizza hello **pgsql** classe (php_pgsql.so).</span><span class="sxs-lookup"><span data-stu-id="09fe8-124">hello code uses hello **pgsql** class (php_pgsql.so).</span></span> <span data-ttu-id="09fe8-125">Installarla eseguendo `sudo apt-get install php-pgsql`.</span><span class="sxs-lookup"><span data-stu-id="09fe8-125">Install it by running `sudo apt-get install php-pgsql`.</span></span>
- <span data-ttu-id="09fe8-126">Hello abilitato **pgsql** estensione modificando hello `/etc/php/7.0/mods-available/pgsql.ini` file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="09fe8-126">Enabled hello **pgsql** extension by editing hello `/etc/php/7.0/mods-available/pgsql.ini` configuration file.</span></span> <span data-ttu-id="09fe8-127">file di configurazione Hello deve contenere una riga con testo hello `extension=php_pgsql.so`.</span><span class="sxs-lookup"><span data-stu-id="09fe8-127">hello configuration file should contain a line with hello text `extension=php_pgsql.so`.</span></span> <span data-ttu-id="09fe8-128">Se non è visualizzata, aggiungere testo hello e salvare file hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-128">If it is not shown, add hello text and save hello file.</span></span> <span data-ttu-id="09fe8-129">Se è presente, il testo hello commentato ma con un prefisso di un punto e virgola, rimuovere il commento testo hello rimuovendo punto e virgola hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-129">If hello text is present, but commented with a semicolon prefix, uncomment hello text by removing hello semicolon.</span></span>

### <a name="macos"></a><span data-ttu-id="09fe8-130">MacOS</span><span class="sxs-lookup"><span data-stu-id="09fe8-130">MacOS</span></span>
- <span data-ttu-id="09fe8-131">Scaricare [PHP versione 7.1.4](http://php.net/downloads.php)</span><span class="sxs-lookup"><span data-stu-id="09fe8-131">Download [PHP 7.1.4 version](http://php.net/downloads.php)</span></span>
- <span data-ttu-id="09fe8-132">Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.macosx.php) per un'ulteriore configurazione</span><span class="sxs-lookup"><span data-stu-id="09fe8-132">Install PHP and refer toohello [PHP manual](http://php.net/manual/install.macosx.php) for further configuration</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="09fe8-133">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="09fe8-133">Get connection information</span></span>
<span data-ttu-id="09fe8-134">Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-134">Get hello connection information needed tooconnect toohello Azure Database for PostgreSQL.</span></span> <span data-ttu-id="09fe8-135">È necessario hello le credenziali di nome e l'account di accesso completo del server.</span><span class="sxs-lookup"><span data-stu-id="09fe8-135">You need hello fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="09fe8-136">Accedi toohello [portale di Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="09fe8-136">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="09fe8-137">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** e Cerca server hello sia stato creato, ad esempio **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="09fe8-137">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="09fe8-138">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="09fe8-138">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="09fe8-139">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="09fe8-139">Select hello server's **Overview** page.</span></span> <span data-ttu-id="09fe8-140">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="09fe8-140">Make a note of hello **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="09fe8-141">![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/connect-php/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="09fe8-141">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-php/1-connection-string.png)</span></span>
5. <span data-ttu-id="09fe8-142">Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-142">If you forget your server login information, navigate toohello **Overview** page tooview hello Server admin login name and, if necessary, reset hello password.</span></span>

## <a name="connect-and-create-a-table"></a><span data-ttu-id="09fe8-143">Connettersi e creare una tabella</span><span class="sxs-lookup"><span data-stu-id="09fe8-143">Connect and create a table</span></span>
<span data-ttu-id="09fe8-144">Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL, seguita da **INSERT INTO** righe tooadd di istruzioni SQL in tabella hello.</span><span class="sxs-lookup"><span data-stu-id="09fe8-144">Use hello following code tooconnect and create a table using **CREATE TABLE** SQL statement, followed by **INSERT INTO** SQL statements tooadd rows into hello table.</span></span>

<span data-ttu-id="09fe8-145">il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-145">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="09fe8-146">Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun più volte, alcuni comandi e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se ogni volta che si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="09fe8-146">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) several times toorun several commands, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred each time.</span></span> <span data-ttu-id="09fe8-147">Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="09fe8-147">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="09fe8-148">Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="09fe8-148">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="read-data"></a><span data-ttu-id="09fe8-149">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="09fe8-149">Read data</span></span>
<span data-ttu-id="09fe8-150">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-150">Use hello following code tooconnect and read hello data using a **SELECT** SQL statement.</span></span> 

 <span data-ttu-id="09fe8-151">il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-151">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="09fe8-152">Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello comando SELECT, mantenendo i risultati di hello in un set di risultati, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="09fe8-152">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun hello SELECT command, keeping hello results in a result set, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span>  <span data-ttu-id="09fe8-153">set di risultati hello tooread, metodo [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) viene chiamato in un ciclo, una volta per ogni riga e la riga hello i dati vengono recuperati in una matrice `$row`, con il valore di dati per ogni colonna in ogni posizione della matrice.</span><span class="sxs-lookup"><span data-stu-id="09fe8-153">tooread hello result set, method [pg_fetch_row()](http://php.net/manual/en/function.pg-fetch-row.php) is called in a loop, once per row, and hello row data is retrieved in an array `$row`, with one data value per column in each array position.</span></span>  <span data-ttu-id="09fe8-154">set di risultati hello toofree, metodo [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) viene chiamato.</span><span class="sxs-lookup"><span data-stu-id="09fe8-154">toofree hello result set, method [pg_free_result()](http://php.net/manual/en/function.pg-free-result.php) is called.</span></span> <span data-ttu-id="09fe8-155">Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="09fe8-155">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="09fe8-156">Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="09fe8-156">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="update-data"></a><span data-ttu-id="09fe8-157">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="09fe8-157">Update data</span></span>
<span data-ttu-id="09fe8-158">Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-158">Use hello following code tooconnect and update hello data using a **UPDATE** SQL statement.</span></span>

<span data-ttu-id="09fe8-159">il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-159">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect tooAzure Database for PostgreSQL.</span></span> <span data-ttu-id="09fe8-160">Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="09fe8-160">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="09fe8-161">Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="09fe8-161">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="09fe8-162">Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="09fe8-162">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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


## <a name="delete-data"></a><span data-ttu-id="09fe8-163">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="09fe8-163">Delete data</span></span>
<span data-ttu-id="09fe8-164">Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-164">Use hello following code tooconnect and read hello data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="09fe8-165">il metodo di chiamata di codice Hello [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect troppo Azure Database PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="09fe8-165">hello code call method [pg_connect()](http://php.net/manual/en/function.pg-connect.php) tooconnect too Azure Database for PostgreSQL.</span></span> <span data-ttu-id="09fe8-166">Viene quindi chiamato metodo [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun un comando, e [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello illustra in dettaglio se si è verificato un errore.</span><span class="sxs-lookup"><span data-stu-id="09fe8-166">Then it calls method [pg_query()](http://php.net/manual/en/function.pg-query.php) toorun a command, and [pg_last_error()](http://php.net/manual/en/function.pg-last-error.php) toocheck hello details if an error occurred.</span></span> <span data-ttu-id="09fe8-167">Viene quindi chiamato metodo [pg_close()](http://php.net/manual/en/function.pg-close.php) connessione hello tooclose.</span><span class="sxs-lookup"><span data-stu-id="09fe8-167">Then it calls method [pg_close()](http://php.net/manual/en/function.pg-close.php) tooclose hello connection.</span></span>

<span data-ttu-id="09fe8-168">Sostituire hello `$host`, `$database`, `$user`, e `$password` parametri con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="09fe8-168">Replace hello `$host`, `$database`, `$user`, and `$password` parameters with your own values.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="09fe8-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09fe8-169">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="09fe8-170">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="09fe8-170">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
