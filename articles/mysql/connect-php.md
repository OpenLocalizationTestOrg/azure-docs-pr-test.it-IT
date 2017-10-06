---
title: La connessione tooAzure Database MySQL da PHP | Documenti Microsoft
description: "Questa Guida introduttiva offre numerosi esempi di codice PHP è possibile utilizzare tooconnect ed eseguire query di dati dal Database di Azure per MySQL."
services: mysql
author: mswutao
ms.author: wuta
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 07/12/2017
ms.openlocfilehash: b928748c473c1aef320ae2183f237b5b845e83f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-use-php-tooconnect-and-query-data"></a>Il Database di Azure per MySQL: dati di utilizzo PHP tooconnect e query
Questa Guida introduttiva illustra come tooconnect tooan Database di Azure per l'utilizzo di MySQL un [PHP](http://php.net/manual/intro-whatis.php) dell'applicazione. Viene illustrato come toouse tooquery di istruzioni SQL, inserire, aggiornare ed eliminare dati nel database di hello. In questo articolo si presuppone che si ha familiarità con lo sviluppo tramite PHP, ma che sono tooworking nuovo con il Database di Azure per MySQL.

## <a name="prerequisites"></a>Prerequisiti
Questa Guida rapida utilizza risorse di hello create in una di queste guide come punto di partenza:
- [Create an Azure Database for MySQL server using Azure portal](./quickstart-create-mysql-server-database-using-azure-portal.md) (Creare un database di Azure per il server MySQL usando il portale di Azure)
- [Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure](./quickstart-create-mysql-server-database-using-azure-cli.md)

## <a name="install-php"></a>Installare PHP
Installare PHP nel server o creare un'[app Web](https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-overview) di Azure che includa PHP.

### <a name="macos"></a>MacOS
- Scaricare [PHP versione 7.1.4](http://php.net/downloads.php)
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.macosx.php) per un'ulteriore configurazione

### <a name="linux-ubuntu"></a>Linux (Ubuntu)
- Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://php.net/downloads.php)
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.unix.php) per un'ulteriore configurazione

### <a name="windows"></a>Windows
- Scaricare [PHP versione 7.1.4 non thread-safe (x64)](http://windows.php.net/download#php-7.1)
- Installare PHP e fare riferimento toohello [manuale PHP](http://php.net/manual/install.windows.php) per un'ulteriore configurazione

## <a name="get-connection-information"></a>Ottenere informazioni di connessione
Ottenere hello connessione le informazioni necessarie tooconnect toohello Database di Azure per MySQL. È necessario hello le credenziali di nome e l'account di accesso completo del server.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel riquadro di sinistra hello, fare clic su **tutte le risorse**e quindi cercare server hello sia stato creato (ad esempio, **myserver4demo**).
3. Fare clic su nome hello del server.
4. Server di selezionare hello **proprietà** pagina. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.
 ![Nome del server del database di Azure per MySQL](./media/connect-php/1_server-properties-name-login.png)
5. Se si dimenticano le informazioni di accesso del server, passare toohello **Panoramica** pagina nome account di accesso amministratore di tooview hello Server e, se necessario, reimpostare la password di hello.

## <a name="connect-and-create-a-table"></a>Connettersi e creare una tabella
Seguente hello utilizzare codice tooconnect e crea una tabella utilizzando **CREATE TABLE** istruzione SQL. 

codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP. metodi di chiamata di codice Hello [mysqli_init](http://php.net/manual/mysqli.init.php) e [mysqli_real_connect](http://php.net/manual/mysqli.real-connect.php) tooconnect tooMySQL. Viene quindi chiamato metodo [mysqli_query](http://php.net/manual/mysqli.query.php) query hello toorun. Viene quindi chiamato metodo [mysqli_close](http://php.net/manual/mysqli.close.php) connessione hello tooclose.

Sostituire i parametri di host, username, password e db_name hello con valori personalizzati. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

// Run hello create table query
if (mysqli_query($conn, '
CREATE TABLE Products (
`Id` INT NOT NULL AUTO_INCREMENT ,
`ProductName` VARCHAR(200) NOT NULL ,
`Color` VARCHAR(50) NOT NULL ,
`Price` DOUBLE NOT NULL ,
PRIMARY KEY (`Id`)
);
')) {
printf("Table created\n");
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="insert-data"></a>Inserire dati
Seguente hello utilizzare codice tooconnect e inserire dati utilizzando un **inserire** istruzione SQL.

codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP. codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una istruzione insert, quindi associa hello parametri per ogni valore della colonna inserita con metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Sostituire i parametri di host, username, password e db_name hello con valori personalizzati. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Create an Insert prepared statement and run it
$product_name = 'BrandNewProduct';
$product_color = 'Blue';
$product_price = 15.5;
if ($stmt = mysqli_prepare($conn, "INSERT INTO Products (ProductName, Color, Price) VALUES (?, ?, ?)")) {
mysqli_stmt_bind_param($stmt, 'ssd', $product_name, $product_color, $product_price);
mysqli_stmt_execute($stmt);
printf("Insert: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

// Close hello connection
mysqli_close($conn);
?>
```

## <a name="read-data"></a>Leggere i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **selezionare** istruzione SQL.  codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP. codice Hello Usa metodo [mysqli_query](http://php.net/manual/mysqli.query.php) eseguire query sql hello e utilizza [mysqli_fetch_assoc](http://php.net/manual/mysqli-result.fetch-assoc.php) toofetch metodo hello righe risultanti.

Sostituire i parametri di host, username, password e db_name hello con valori personalizzati. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Select query
printf("Reading data from table: \n");
$res = mysqli_query($conn, 'SELECT * FROM Products');
while ($row = mysqli_fetch_assoc($res)) {
var_dump($row);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="update-data"></a>Aggiornare i dati
Seguente hello utilizzare tooconnect del codice e aggiornare hello dati utilizzando un **aggiornare** istruzione SQL.

codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP. codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate un'istruzione update preparata, quindi associa parametri hello per il valore di ogni colonna aggiornata con metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Sostituire i parametri di host, username, password e db_name hello con valori personalizzati. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Update statement
$product_name = 'BrandNewProduct';
$new_product_price = 15.1;
if ($stmt = mysqli_prepare($conn, "UPDATE Products SET Price = ? WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 'ds', $new_product_price, $product_name);
mysqli_stmt_execute($stmt);
printf("Update: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));

//Close hello connection
mysqli_stmt_close($stmt);
}

mysqli_close($conn);
?>
```


## <a name="delete-data"></a>Eliminare i dati
Seguente hello utilizzare codice tooconnect e leggere hello dati utilizzando un **eliminare** istruzione SQL. 

codice Hello utilizza hello **estensione MySQL migliorata** classe (mysqli) inclusi in PHP. codice Hello Usa metodo [mysqli_prepare](http://php.net/manual/mysqli.prepare.php) toocreate una istruzione delete, quindi associa hello parametri per hello dove clausola nell'istruzione hello metodo [mysqli_stmt_bind_param](http://php.net/manual/mysqli-stmt.bind-param.php). codice Hello viene eseguita l'istruzione hello metodo [mysqli_stmt_execute](http://php.net/manual/mysqli-stmt.execute.php) e successivamente si chiude hello istruzione metodo [mysqli_stmt_close](http://php.net/manual/mysqli-stmt.close.php).

Sostituire i parametri di host, username, password e db_name hello con valori personalizzati. 

```php
<?php
$host = 'myserver4demo.mysql.database.azure.com';
$username = 'myadmin@myserver4demo';
$password = 'your_password';
$db_name = 'your_database';

//Establishes hello connection
$conn = mysqli_init();
mysqli_real_connect($conn, $host, $username, $password, $db_name, 3306);
if (mysqli_connect_errno($conn)) {
die('Failed tooconnect tooMySQL: '.mysqli_connect_error());
}

//Run hello Delete statement
$product_name = 'BrandNewProduct';
if ($stmt = mysqli_prepare($conn, "DELETE FROM Products WHERE ProductName = ?")) {
mysqli_stmt_bind_param($stmt, 's', $product_name);
mysqli_stmt_execute($stmt);
printf("Delete: Affected %d rows\n", mysqli_stmt_affected_rows($stmt));
mysqli_stmt_close($stmt);
}

//Close hello connection
mysqli_close($conn);
?>
```

## <a name="next-steps"></a>Passaggi successivi
> [!div class="nextstepaction"]
> [Creare un'app Web PHP e MySQL in Azure](../app-service-web/app-service-web-tutorial-php-mysql.md?toc=%2fazure%2fmysql%2ftoc.json)
